

[document-general-service design](https://qima.atlassian.net/wiki/spaces/IT/pages/2879520949/document-general-service+design)


### How to onboard?


1. 分析当前系统中的业务场景
	1. lotus 生成 IC
	2. 发票
  面临的问题
  1. 相似的业务在各个服务中出现，使用了不同技术

  希望解决什么问题
	  1. 集中管理业务模板
	  2. 组织间共用服务
	  3. 整合并节约系统和人力资源

阶段节点
	1. 调查当前相关业务及技术实现
		1. qima-one 
		2. qsp 
	2. 如何做，技术选型
	3. 技术架构设计，数据库设计，接口设计
	4. 开展项目，实现相关逻辑
		1. 模板管理
		2. 文件渲染及转换
计划 进度

1. 我们在  `doc_generation_template` 定义了 `out-put-type` , 这个应该是不可以编辑的。因为在具体的业务中，其他服务生成 file 以后可能需要去查询， 那么他根据 src-id 和 out-put-type 就可以去 `file-service` 中查询生成的文件。
2. 