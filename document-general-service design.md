

[document-general-service design](https://qima.atlassian.net/wiki/spaces/IT/pages/2879520949/document-general-service+design)

### background and goal

-   QIMA business
    
    

### roadmap

-   2022 Q4
    
    -   Evaluate tech solutions and work out a clear document-general-service design
        
    -   Setup a new java macro service with q-core architecture
        
    -   MVP: able to render excel and convert it to pdf with API call
        
-   2023 Q1
    

### tech investigation

        
2.  Spire (recommend)
    
    1.  Easy/Safety/Efficient
        
    2.  Well-documented and friendly community&official support
        
    3.  The free version license is able to render/convert the excel files with a page number is not more than 3, able to cover our current scenario
        
    4.  No extra development effort for upgrading the license
        
3.  Aspose
    
    1.  The free version has a watermark and often loses style during converting the file format
        
    2.  The advanced version is the most expensive one among the solutions
        
4.  easyexcel+jodconverter+libreoffice
    
    1.  free set of solution
        
    2.  Libreoffice is used in QSP service before
        
    3.  need to install Libreoffice in ecs
        

### Architecture

Draw.io Diagram

Loading app...

-   core engine for render and file format conversion
    
-   template management
    
    -   file
        
    -   parameter
        
        -   bucket
            
-   job management
    
    -   checking status and error
        

### schema design

### API design

-   verify doc size
    
-     
    

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