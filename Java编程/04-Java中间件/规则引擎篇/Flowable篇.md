# Flowable篇

一 、Flowable 的出现是为了什么
二、Flowable 的优势
三、常见的Java类/实例
3.1 ProcessEngine
3.2 RepositoryService
3.3 ProcessDefinition
3.4 Deployment
3.5 RuntimeService
3.6 ProcessInstance
3.7 TaskService
3.8 JavaDelegate
3.9 其他
四、核心数据库表
4.1 数据库
4.2 通用数据表（2个）
4.3 历史表（8个，HistoryService接口操作的表）
4.4 用户相关表（4个，IdentityService接口操作的表）
4.5 流程定义、流程模板相关表（3个，RepositoryService接口操作的表）
4.6 流程运行时表（6个，RuntimeService接口操作的表）
五、在SpringBoot中简单使用
5.1 Flowable入门之表的生成
5.2 请假审批案例的实现
5.2.1 项目结构
5.2.2 application.yml
5.2.3 holiday-request.bpmn20.xml
5.2.4 HolidayRequestDTO
5.2.5 HolidayRequestProcessService
5.2.6 HolidayRequestProcessServiceImpl
5.2.7 CallExternalSystemDelegate
5.2.8 SendRejectionMail
5.2.9 HolidayRequestProcessController
5.2.10 运行&结果展示

原文链接：https://blog.csdn.net/FBB360JAVA/article/details/131141005