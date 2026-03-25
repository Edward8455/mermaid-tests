```mermaid
graph LR
    %% 定义外部实体和系统
    Student["【外部实体】学生"]
    Admin["【外部实体】管理员"]
    System(("图书在线预约系统"))

    %% 学生侧的火力交互
    Student -- "预约请求、查询请求、取消请求" --> System
    System -- "查询结果、预约反馈" --> Student

    %% 管理员侧的火力交互
    Admin -- "图书上下架信息、预约处理指令" --> System
    System -- "处理状态报表" --> Admin

    %% 给节点上点重装机甲的颜色（可选）
    style System fill:#f9f,stroke:#333,stroke-width:4px

classDiagram
    class 预约请求 {
        +String 学号
        +String 图书编号
        +Date 预约日期
        +Enum 操作类型 [预约 | 取消]
    }
    
    class 图书信息 {
        +String 图书编号
        +String 书名
        +String 作者
        +String 出版社
        +Enum 状态 [可借 | 已借出 | 已预约]
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
        +Enum 记录状态 [待处理 | 成功 | 失败 | 已取消]
    }
    
    class 查询请求 {
        +Enum 查询条件 [按书名查询 | 按作者查询 | 按图书编号查询]
    }

stateDiagram-v2
    %% 定义初始和结束节点
    [*] --> 待处理 : 学生提交预约
    
    %% 核心状态流转
    待处理 --> 已预约成功 : 管理员审核通过 / 系统确认有库存
    待处理 --> 预约失败 : 无库存
    待处理 --> 已取消 : 学生点击取消
    
    %% 成功后的分支走向
    已预约成功 --> 已取消 : 学生点击取消
    已预约成功 --> [*] : 学生取走实体书 (转为借阅记录)
    已预约成功 --> 已失效 : 超过 48 小时未取
    
    %% 终态收尾
    已失效 --> [*]
    预约失败 --> [*]
    已取消 --> [*]
    end
```
