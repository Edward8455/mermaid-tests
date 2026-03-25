graph LR
    Student["【外部实体】学生"]
    Admin["【外部实体】管理员"]
    System(("图书在线预约系统"))

    Student -- "预约请求、查询请求、取消请求" --> System
    System -- "查询结果、预约反馈" --> Student

    Admin -- "图书上下架信息、预约处理指令" --> System
    System -- "处理状态报表" --> Admin

    style System fill:#f9f,stroke:#333,stroke-width:4px
    classDiagram
    class 预约请求 {
        +String 学号
        +String 图书编号
        +Date 预约日期
        +String 操作类型_预约或取消
    }
    
    class 图书信息 {
        +String 图书编号
        +String 书名
        +String 作者
        +String 出版社
        +String 状态_可借_已借出_已预约
    }
    
    class 学生信息 {
        +String 学号
        +String 姓名
        +String 学院
        +String 联系方式
    }
    
    class 预约记录 {
        +String 预约单号
        +String 学号
        +String 图书编号
        +DateTime 提交时间
        +String 记录状态
    }
    
    class 查询请求 {
        +String 查询条件
    }
    stateDiagram-v2
    [*] --> 待处理 : 学生提交预约
    
    待处理 --> 已预约成功 : 审核通过或有库存
    待处理 --> 预约失败 : 无库存
    待处理 --> 已取消 : 学生点击取消
    
    已预约成功 --> 已取消 : 学生点击取消
    已预约成功 --> [*] : 学生取走实体书
    已预约成功 --> 已失效 : 超过48小时未取
    
    已失效 --> [*]
    预约失败 --> [*]
    已取消 --> [*]
