# Flowable篇

拓展阅读：https://blog.csdn.net/FBB360JAVA/article/details/131141005

## Flowable的基础概念

### Flowable 的出现是为了什么

Flowable 是一个轻量级的业务流程管理 (BPM) 和工作流引擎。它的出现是为了满足以下需求：

1. **自动化业务流程**：帮助企业和开发者自动化和优化复杂的业务流程，减少手动操作，提高效率。
2. **提高流程管理灵活性**：通过图形化流程定义和灵活的流程引擎，方便业务人员和开发者快速定义和调整业务流程。
3. **流程监控与优化**：提供强大的流程监控和分析功能，帮助企业及时发现流程中的瓶颈和问题，从而优化流程。
4. **可扩展性和集成**：支持与其他系统和服务的集成，具备良好的扩展性，适应不断变化的业务需求。

### Flowable 的优势

Flowable 在众多 BPM 和工作流引擎中脱颖而出的原因在于其多方面的优势：

1. **开源和免费**：Flowable 是一个开源项目，社区版免费使用，降低了企业的成本。
2. **轻量级**：相比其他 BPM 引擎，Flowable 设计轻量，易于嵌入和部署，特别适合微服务架构。
3. **灵活性和可扩展性**：支持 **BPMN 2.0**、CMMN 1.1 和 DMN 1.1 标准，具备高度的灵活性和可扩展性，能够适应各种复杂的业务场景。
4. **易用的API**：提供丰富且易用的 Java API，开发者可以方便地将其集成到现有的 Java 应用中。
5. **强大的Spring支持**：与 Spring Boot 无缝集成，使得在 Spring 应用中使用 Flowable 变得非常简单。
6. **社区和文档支持**：拥有活跃的社区和详尽的文档，为开发者提供了丰富的学习资源和支持。
7. **健壮的事务管理**：支持复杂的事务管理，确保流程执行的可靠性和一致性。
8. **良好的监控和管理工具**：提供 Flowable Modeler、Flowable Admin 等工具，方便用户进行流程设计、监控和管理。

## Flowable环境配置

### pom 依赖

```xml
<!-- Flowable Engine -->
<dependency>
    <groupId>org.flowable</groupId>
    <artifactId>flowable-spring-boot-starter</artifactId>
    <version>6.7.2</version>
</dependency>
```

### 配置Flowable

1. **配置初始化**：在 Spring Boot 启动时，Spring 容器会自动扫描并加载 `FlowableConfig` 类。
2. **Bean 创建**：当 Spring 发现 `processEngine` 方法被 `@Bean` 注解标注时，会调用该方法并将返回的 `ProcessEngine` 实例注册为一个 Spring Bean。
3. **依赖注入**：通过依赖注入的方式，`SpringProcessEngineConfiguration` 实例会自动传递给 `processEngine` 方法。
4. **引擎构建**：`processEngine` 方法调用 `configuration.buildProcessEngine()`，构建并返回一个 `ProcessEngine` 实例。
5. **引擎使用**：返回的 `ProcessEngine` 实例可以在应用的其他部分通过依赖注入的方式使用，以管理和执行业务流程。

```java
@Configuration
public class FlowableConfig implements EngineConfigurationConfigurer<SpringProcessEngineConfiguration> {
    
    @Resource
    private DataSource dataSource;
    
    @Override
    public void configure(SpringProcessEngineConfiguration config) {
        config.setDataSource(dataSource);
        config.setDatabaseSchemaUpdate(ProcessEngineConfiguration.DB_SCHEMA_UPDATE_TRUE);
    }
    
    @Bean
    public ProcessEngine processEngine(SpringProcessEngineConfiguration configuration) {
        return configuration.buildProcessEngine();
    }
}
```

### SpringProcessEngineConfiguration 常用字段

下面的表格列出了 `SpringProcessEngineConfiguration` 和 `ProcessEngineConfiguration` 的一些常用字段及其说明：

| 字段                        | 说明                                   | 示例值                                             |
| --------------------------- | -------------------------------------- | -------------------------------------------------- |
| `dataSource`                | 设置 Flowable 引擎使用的数据源         | `dataSource`                                       |
| `databaseSchemaUpdate`      | 设置数据库模式更新策略，见下文详细解释 | `ProcessEngineConfiguration.DB_SCHEMA_UPDATE_TRUE` |
| `asyncExecutorActivate`     | 是否启用异步执行器                     | `true`                                             |
| `historyLevel`              | 设置历史记录级别                       | `ProcessEngineConfiguration.HISTORY_FULL`          |
| `mailServerHost`            | 设置邮件服务器主机                     | `smtp.example.com`                                 |
| `mailServerPort`            | 设置邮件服务器端口                     | `587`                                              |
| `mailServerUsername`        | 设置邮件服务器用户名                   | `user@example.com`                                 |
| `mailServerPassword`        | 设置邮件服务器密码                     | `password`                                         |
| `jobExecutorActivate`       | 是否启用作业执行器                     | `true`                                             |
| `asyncExecutorCorePoolSize` | 设置异步执行器核心线程池大小           | `10`                                               |
| `asyncExecutorMaxPoolSize`  | 设置异步执行器最大线程池大小           | `50`                                               |

### 数据库模式更新策略

| 更新策略           | 常量名                         | 说明                                                         | 适用场景                                                     |
| ------------------ | ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **不更新**         | `DB_SCHEMA_UPDATE_FALSE`       | 不对数据库表进行任何操作。如果表不存在或结构不匹配，启动时会抛出异常。 | 生产环境中，需要手动管理数据库表结构。                       |
| **创建**           | `DB_SCHEMA_UPDATE_CREATE`      | 如果数据库表不存在，会自动创建表。如果表已经存在，不会做任何修改。 | 开发或测试环境中，首次启动应用时自动创建数据库表。           |
| **删除并重新创建** | `DB_SCHEMA_UPDATE_DROP_CREATE` | 启动时删除已存在的表，然后重新创建表，所有现有数据会丢失。   | 开发或测试环境中，每次启动时都有一个干净的数据库结构。       |
| **更新**           | `DB_SCHEMA_UPDATE_TRUE`        | 如果数据库表不存在，会自动创建表。如果表已经存在，会自动更新表结构以匹配最新的模式。 | 开发、测试和某些生产环境中，允许自动管理数据库表的更新。     |
| **创建并删除**     | `DB_SCHEMA_UPDATE_CREATE_DROP` | 启动时创建表，但在引擎关闭时删除表，通常用于测试目的。       | 单元测试或集成测试环境中，确保测试环境在每次测试后自动清理。 |

## 常见的Java类/实例

### ProcessEngine

Flowable 引擎的核心接口，用于管理和执行流程定义，提供了与流程引擎交互的各种 API 方法。

通过 `ProcessEngine`，可以获取各种服务（例如 `RuntimeService`、`TaskService`、`RepositoryService` 等），这些服务用于管理和执行流程实例、任务等。

```java
@Bean
public ProcessEngine processEngine(SpringProcessEngineConfiguration configuration) {
    return configuration.buildProcessEngine();
}
```

### RepositoryService

`RepositoryService` 是 Flowable 提供的一个服务接口，主要用于管理流程定义和流程部署。它提供了一系列方法来部署新流程定义、查询已经部署的流程定义、管理流程资源等。

#### RepositoryService 主要方法

以下是 `RepositoryService` 中一些常用的方法及其说明：

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `createDeployment()`                                         | 创建一个新的部署对象，用于部署流程定义文件。                 |
| `deploy(DeploymentBuilder deployment)`                       | 执行部署，将流程定义文件部署到引擎中。                       |
| `createProcessDefinitionQuery()`                             | 创建一个新的查询对象，用于查询流程定义。                     |
| `getProcessDefinition(String processDefinitionId)`           | 根据流程定义ID查询流程定义。                                 |
| `getDeploymentResourceNames(String deploymentId)`            | 获取某个部署的资源名称列表。                                 |
| `getResourceAsStream(String deploymentId, String resourceName)` | 获取某个部署中指定资源的输入流。                             |
| `deleteDeployment(String deploymentId)`                      | 删除某个部署，可以选择是否级联删除相关的流程实例和历史数据。 |
| `suspendProcessDefinitionById(String processDefinitionId)`   | 挂起指定ID的流程定义，挂起后该流程定义将无法启动新的流程实例。 |
| `activateProcessDefinitionById(String processDefinitionId)`  | 激活指定ID的流程定义，恢复其启动新流程实例的能力。           |

#### 示例代码

以下是一个在 Spring Boot 中使用 `RepositoryService` 的示例代码，包括如何部署一个新的流程定义和查询已经部署的流程定义。

##### 部署流程定义

1. **创建部署对象**：通过 `repositoryService.createDeployment()` 创建一个新的部署对象。
2. **添加资源**：使用 `addClasspathResource("processes/my-process.bpmn20.xml")` 将 BPMN 文件添加到部署对象中。
3. **设置部署名称**：使用 `name("My Process Deployment")` 设置部署的名称。
4. **执行部署**：调用 `deploy()` 方法执行部署，将流程定义文件部署到 Flowable 引擎中。

```java
@Service
public class FlowableDeploymentService {

    @Resource
    private RepositoryService repositoryService;

    public void deployProcessDefinition() {
        Deployment deployment = repositoryService.createDeployment()
            .addClasspathResource("processes/my-process.bpmn20.xml")
            .name("My Process Deployment")
            .deploy();

        System.out.println("Deployment ID: " + deployment.getId());
    }
}

```

##### 查询流程定义

1. **创建查询对象**：通过 `repositoryService.createProcessDefinitionQuery()` 创建一个新的查询对象。
2. **设置查询条件**：使用 `orderByProcessDefinitionKey().asc()` 按照流程定义的 Key 进行升序排序。
3. **执行查询**：调用 `list()` 方法执行查询，返回一个包含所有符合条件的流程定义列表。
4. **处理查询结果**：遍历查询结果，输出每个流程定义的名称和版本。

```java
public class FlowableQueryService {

    @Resource
    private RepositoryService repositoryService;

    public String  queryProcessDefinitions() {
        List<ProcessDefinition> processDefinitions = repositoryService.createProcessDefinitionQuery()
            .orderByProcessDefinitionKey()
            .asc()
            .list();

        for (ProcessDefinition pd : processDefinitions) {
            System.out.println("Found process definition: " + pd.getName() + ", version: " + pd.getVersion());
            System.out.println("Process Definition ID: " + pd.getId());
        }

        // 获取第一个流程定义的ID
        if (!processDefinitions.isEmpty()) {
            ProcessDefinition pd = processDefinitions.get(0);
            String processDefinitionId = pd.getId();
            System.out.println("Process Definition ID: " + processDefinitionId);
            return processDefinitionId;
        }

        return null;
    }
}
```

### ProcessDefinition

`ProcessDefinition` 是 Flowable 中的一个接口，表示一个流程定义。流程定义是指在 BPMN 2.0 XML 文件中定义的流程模型。`ProcessDefinition` 对象包含了流程定义的元数据，例如 ID、名称、版本等。

#### ProcessDefinition 的主要方法

以下是 `ProcessDefinition` 接口中的一些常用方法及其说明：

| 方法                       | 返回类型  | 说明                                                         |
| -------------------------- | --------- | ------------------------------------------------------------ |
| `getId()`                  | `String`  | 返回流程定义的唯一标识符。                                   |
| `getKey()`                 | `String`  | 返回流程定义的 key，这是一个唯一标识符，用于流程定义的版本控制。 |
| `getName()`                | `String`  | 返回流程定义的名称。                                         |
| `getCategory()`            | `String`  | 返回流程定义的类别。                                         |
| `getVersion()`             | `int`     | 返回流程定义的版本号。                                       |
| `getDeploymentId()`        | `String`  | 返回部署该流程定义的部署 ID。                                |
| `getResourceName()`        | `String`  | 返回定义该流程的 BPMN 资源文件的名称。                       |
| `getDiagramResourceName()` | `String`  | 返回定义该流程的 BPMN 图形文件的名称（如果有）。             |
| `isSuspended()`            | `boolean` | 返回流程定义是否被挂起。                                     |
| `hasStartFormKey()`        | `boolean` | 返回流程定义是否有启动表单。                                 |
| `getDescription()`         | `String`  | 返回流程定义的描述信息。                                     |

#### 示例代码

以下是一些示例代码，展示如何使用 `RepositoryService` 来查询和管理 `ProcessDefinition` 对象。

##### 查询所有流程定义

1. **创建查询对象**：通过 `repositoryService.createProcessDefinitionQuery()` 创建一个新的查询对象。
2. **设置查询条件**：使用 `orderByProcessDefinitionKey().asc()` 按照流程定义的 Key 进行升序排序。
3. **执行查询**：调用 `list()` 方法执行查询，返回一个包含所有符合条件的流程定义列表。
4. **处理查询结果**：遍历查询结果，输出每个流程定义的 ID、Key、名称、版本和部署 ID。

```java
@Service
public class FlowableProcessDefinitionService {

    @Resource
    private RepositoryService repositoryService;

    public void queryProcessDefinitions() {
        List<ProcessDefinition> processDefinitions = repositoryService.createProcessDefinitionQuery()
            .orderByProcessDefinitionKey()
            .asc()
            .list();

        for (ProcessDefinition pd : processDefinitions) {
            System.out.println("Process Definition ID: " + pd.getId());
            System.out.println("Process Definition Key: " + pd.getKey());
            System.out.println("Process Definition Name: " + pd.getName());
            System.out.println("Process Definition Version: " + pd.getVersion());
            System.out.println("Process Definition Deployment ID: " + pd.getDeploymentId());
        }
    }
}
```

##### 查询特定流程定义

1. **通过 ID 查询流程定义**：使用 `repositoryService.getProcessDefinition(processDefinitionId)` 方法，根据流程定义的 ID 查询特定的流程定义。
2. **输出流程定义信息**：输出查询到的流程定义的 ID、Key、名称、版本和部署 ID。

```java
@Service
public class FlowableProcessDefinitionService {

    @Resource
    private RepositoryService repositoryService;

    public void queryProcessDefinitionById(String processDefinitionId) {
        ProcessDefinition pd = repositoryService.getProcessDefinition(processDefinitionId);

        System.out.println("Process Definition ID: " + pd.getId());
        System.out.println("Process Definition Key: " + pd.getKey());
        System.out.println("Process Definition Name: " + pd.getName());
        System.out.println("Process Definition Version: " + pd.getVersion());
        System.out.println("Process Definition Deployment ID: " + pd.getDeploymentId());
    }
}
```

```java
@Test
void test() {
    // 部署流程定义并获取ID
    String processDefinitionId = flowableQueryService.queryProcessDefinitions();

    // 使用获取到的流程定义ID查询详细信息
    if (processDefinitionId != null) {
        flowableProcessDefinitionService.queryProcessDefinitionById(processDefinitionId);
    }
}
```

### Deployment

在 Flowable 中，`Deployment` 表示一个流程定义或其他资源的部署。通过部署，Flowable 引擎将 BPMN 文件、表单、规则和其他资源注册到引擎中，从而使这些资源可以被执行和管理。

`Deployment` 接口提供了用于获取部署信息的方法。以下是一些常用的方法及其说明：

| 方法                  | 返回类型                | 说明                   |
| --------------------- | ----------------------- | ---------------------- |
| `getId()`             | `String`                | 返回部署的唯一标识符。 |
| `getName()`           | `String`                | 返回部署的名称。       |
| `getCategory()`       | `String`                | 返回部署的类别。       |
| `getDeploymentTime()` | `Date`                  | 返回部署的时间。       |
| `getTenantId()`       | `String`                | 返回租户ID。           |
| `getResources()`      | `Map<String, Resource>` | 返回部署中包含的资源。 |

部署实例，通过RepositoryService获取。部署之后可以查询流程定义，也可以启动流程实例。详见[RepositoryService](###RepositoryService)

### RuntimeService

`RuntimeService` 是 Flowable 的核心服务之一，主要负责管理流程实例的运行状态。通过 `RuntimeService` 可以启动流程实例、查询流程实例、获取和设置流程变量等。

#### 常用方法和属性

`RuntimeService` 提供了许多用于管理流程实例的方法：

| 方法                                                         | 返回类型               | 说明                                      |
| ------------------------------------------------------------ | ---------------------- | ----------------------------------------- |
| `startProcessInstanceByKey(String processDefinitionKey)`     | `ProcessInstance`      | 根据流程定义的 key 启动一个新的流程实例。 |
| `createProcessInstanceQuery()`                               | `ProcessInstanceQuery` | 创建一个新的流程实例查询对象。            |
| `getVariables(String executionId)`                           | `Map<String, Object>`  | 获取指定执行实例的所有流程变量。          |
| `setVariable(String executionId, String variableName, Object value)` | `void`                 | 设置指定执行实例的单个流程变量。          |
| `signalEventReceived(String signalName)`                     | `void`                 | 触发信号事件。                            |

#### 示例代码和详细讲解

##### 启动流程实例

1. **创建流程实例**：通过 `runtimeService.startProcessInstanceByKey("myProcess")` 启动一个新的流程实例。
2. **获取流程实例信息**：通过返回的 `ProcessInstance` 对象获取流程实例的 ID 和其他信息。

```java
@Service
public class FlowableRuntimeService {

    @Autowired
    private RuntimeService runtimeService;

    public ProcessInstance startProcessInstance(String processDefinitionKey) {
        // 启动流程实例
        ProcessInstance processInstance = runtimeService.startProcessInstanceByKey(processDefinitionKey);

        // 输出流程实例信息
        System.out.println("Process Instance ID: " + processInstance.getId());
        System.out.println("Process Definition ID: " + processInstance.getProcessDefinitionId());

        return processInstance;
    }
}
```

**详解：**

1. `runtimeService.startProcessInstanceByKey(processDefinitionKey)`：根据流程定义的 key 启动一个新的流程实例。
2. `processInstance.getId()`：获取流程实例的唯一标识符。
3. `processInstance.getProcessDefinitionId()`：获取流程定义的 ID。

```java
// 部署流程定义并获取ID
ProcessDefinition processDefinition = flowableQueryService.queryProcessDefinitions();

// 使用获取到的流程定义ID查询详细信息
if (processDefinition != null) {
    flowableRuntimeService.startProcessInstance(processDefinition.getKey());
}
```

##### 查询流程实例

1. **创建查询对象**：通过 `runtimeService.createProcessInstanceQuery()` 创建一个新的流程实例查询对象。
2. **设置查询条件**：使用 `processDefinitionKey("myProcess").list()` 查询所有指定流程定义 key 的流程实例。
3. **处理查询结果**：遍历查询结果，输出每个流程实例的 ID 和其他信息。

```java
@Service
public class FlowableProcessInstanceQueryService {

    @Autowired
    private RuntimeService runtimeService;

    public void queryProcessInstances(String processDefinitionKey) {
        // 创建查询对象
        List<ProcessInstance> processInstances = runtimeService.createProcessInstanceQuery()
            .processDefinitionKey(processDefinitionKey) // 设置查询条件
            .list(); // 执行查询

        // 处理查询结果
        for (ProcessInstance processInstance : processInstances) {
            System.out.println("Process Instance ID: " + processInstance.getId());
            System.out.println("Process Definition ID: " + processInstance.getProcessDefinitionId());
            System.out.println("Process Instance Start Time: " + processInstance.getStartTime());
        }
    }
}
```

**详解：**

1. `runtimeService.createProcessInstanceQuery()`：创建一个新的流程实例查询对象。
2. `.processDefinitionKey(processDefinitionKey)`：设置查询条件为指定的流程定义 key。
3. `.list()`：执行查询并返回结果列表。
4. `processInstance.getId()`：获取流程实例的唯一标识符。
5. `processInstance.getProcessDefinitionId()`：获取流程定义的 ID。
6. `processInstance.getStartTime()`：获取流程实例的开始时间。

##### 获取和设置流程变量

1. **获取流程变量**：通过 `runtimeService.getVariables(processInstanceId)` 获取指定执行实例的所有流程变量。
2. **设置流程变量**：通过 `runtimeService.setVariable(processInstanceId, variableName, value)` 设置指定执行实例的单个流程变量。

```java
@Service
public class FlowableVariableService {

    @Autowired
    private RuntimeService runtimeService;

    public Map<String, Object> getProcessVariables(String processInstanceId) {
        // 获取流程变量
        return runtimeService.getVariables(processInstanceId);
    }

    public void setProcessVariable(String processInstanceId, String variableName, Object value) {
        // 设置流程变量
        runtimeService.setVariable(processInstanceId, variableName, value);
    }
}
```

**详解：**

1. `runtimeService.getVariables(executionId)`：获取指定执行实例的所有流程变量。
2. `runtimeService.setVariable(executionId, variableName, value)`：设置指定执行实例的单个流程变量。

```java
// 部署流程定义并获取ID
ProcessDefinition processDefinition = flowableQueryService.queryProcessDefinitions();

// 使用获取到的流程定义ID查询详细信息
if (processDefinition != null) {
    ProcessInstance processInstance = flowableRuntimeService.startProcessInstance(processDefinition.getKey());

    String processInstanceId = processInstance.getId();
    String variableName = "testVariable";
    String variableValue = "testValue";
    flowableVariableService.setProcessVariable(processInstanceId, variableName, variableValue);

    Map<String, Object> processVariables = flowableVariableService.getProcessVariables(processInstanceId);

    System.out.println("processVariables : " + processVariables);
}
```

##### 带有业务键的流程实例

业务键（Business Key）在 Flowable 中的主要作用是将流程实例与业务数据关联起来，从而在查询和管理流程实例时，可以通过业务键快速找到对应的业务数据。通过在启动流程实例时指定业务键，并在查询流程实例时使用业务键，可以方便地管理和查询流程实例。

```java
public ProcessInstance startProcessInstanceByKey(String processDefinitionKey, String businessKey) {
    // 启动流程实例
    ProcessInstance processInstance = runtimeService.startProcessInstanceByKey(processDefinitionKey, businessKey);

    // 输出流程实例信息
    System.out.println("Process Instance ID: " + processInstance.getId());
    System.out.println("Process Definition ID: " + processInstance.getProcessDefinitionId());

    return processInstance;
}
```

```java
public void  getProcessInstanceByBusinessKey(String businessKey){
    ProcessInstance processInstance = runtimeService.createProcessInstanceQuery().processInstanceBusinessKey(businessKey).singleResult();
    System.out.println("processInstance：" + processInstance);
}
```

```java
// 部署流程定义并获取ID
ProcessDefinition processDefinition = flowableQueryService.queryProcessDefinitions();

// 使用获取到的流程定义ID查询详细信息
if (processDefinition != null) {
    ProcessInstance processInstance = flowableRuntimeService.startProcessInstanceByKey(processDefinition.getKey(), "AAAA");
    flowableProcessInstanceQueryService.getProcessInstanceByBusinessKey(processDefinition.getKey());
}
```

### ProcessInstance

`ProcessInstance` 是 Flowable 中表示一个具体执行中的流程实例的接口。它提供了访问流程实例相关信息的方法，如流程实例的 ID、流程定义的 ID、业务键、启动时间等。详见[RuntimeService](###RuntimeService)。

以下是 `ProcessInstance` 接口的一些常用方法和属性：

| 方法                       | 返回类型  | 说明                                         |
| -------------------------- | --------- | -------------------------------------------- |
| `getId()`                  | `String`  | 返回流程实例的唯一标识。                     |
| `getProcessDefinitionId()` | `String`  | 返回流程实例对应的流程定义的唯一标识。       |
| `getBusinessKey()`         | `String`  | 返回流程实例的业务键。                       |
| `getStartTime()`           | `Date`    | 返回流程实例的启动时间。                     |
| `getEndTime()`             | `Date`    | 返回流程实例的结束时间（如果流程已经结束）。 |
| `getName()`                | `String`  | 返回流程实例的名称。                         |
| `isEnded()`                | `boolean` | 判断流程实例是否已经结束。                   |
| `getKey()`                 | `String`  | 返回流程实例的 Key。                         |

### TaskService

### JavaDelegate

### 其他

## 核心数据库表

### 数据库介绍

### 通用数据表

### 历史表（由HistoryService接口操作）

### 用户相关表（由IdentityService接口操作）

### 流程定义和流程模板相关表（由RepositoryService接口操作）

### 流程运行时表（由RuntimeService接口操作）

## 在Spring Boot中简单使用Flowable

### Flowable入门：数据库表的生成

### 请假审批案例的实现

#### 项目结构

#### 配置文件（application.yml）

#### 流程定义文件（holiday-request.bpmn20.xml）

#### 数据传输对象（HolidayRequestDTO）

#### 流程服务接口（HolidayRequestProcessService）

#### 流程服务实现（HolidayRequestProcessServiceImpl）

#### 外部系统调用委派（CallExternalSystemDelegate）

#### 拒绝邮件发送服务（SendRejectionMail）

#### 流程控制器（HolidayRequestProcessController）

#### 运行与结果展示