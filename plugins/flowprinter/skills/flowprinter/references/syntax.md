# Mermaid 语法参考

高级图表类型的详细语法规则。需要具体语法细节时请加载本文件。

---

## 时序图语法

### 消息
```
->>   实线箭头
-->>  虚线箭头
-)    实线空心箭头
--)   虚线空心箭头
```

### 激活与注释
```mermaid
sequenceDiagram
    participant A
    participant B
    A->>+B: Request (activates B)
    Note right of B: Processing
    B-->>-A: Response (deactivates B)
    Note over A,B: Both involved
```

### 循环与条件
```mermaid
sequenceDiagram
    loop Every minute
        A->>B: Heartbeat
    end
    alt Success
        B-->>A: OK
    else Failure
        B-->>A: Error
    end
    opt Optional
        A->>B: Extra call
    end
```

---

## 类图语法

### 关系
```
<|--  继承
*--   组合
o--   聚合
-->   关联
--    连接（实线）
..>   依赖
..|>  实现
```

### 类定义
```mermaid
classDiagram
    class Animal {
        +String name
        +int age
        +makeSound() void
        -privateMethod() int
        #protectedMethod()
    }
    Animal <|-- Dog
    Animal <|-- Cat
```

---

## ER 图语法

### 基数
```
||--||  一对一
||--o{  一对多
}o--o{  多对多
||--o|  一对零或一
```

### 示例
```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE_ITEM : contains
    PRODUCT }|--o{ LINE_ITEM : "ordered in"
```

---

## 甘特图语法

```mermaid
gantt
    title Project Schedule
    dateFormat YYYY-MM-DD
    section Phase 1
        Task 1: a1, 2024-01-01, 30d
        Task 2: a2, after a1, 20d
    section Phase 2
        Task 3: 2024-02-15, 25d
        Milestone: milestone, m1, 2024-03-15, 0d
```

### 任务状态
```
done     已完成任务
active   当前任务
crit     关键路径
```

---

## 用户旅程图语法

```mermaid
journey
    title User Shopping Experience
    section Browse
        Visit website: 5: User
        Search product: 4: User
    section Purchase
        Add to cart: 5: User
        Checkout: 3: User
        Payment: 4: User
```

评分范围：1（差）到 5（优秀）

---

## XY 图语法

```mermaid
xychart
    title "Monthly Sales"
    x-axis [Jan, Feb, Mar, Apr]
    y-axis "Revenue" 0 --> 150
    bar [65, 78, 52, 91]
    line [65, 78, 52, 91]
```

---

## 看板语法

```mermaid
kanban
  Todo
    [Design System]
  InProgress
    [Implement Feature]
  Done
    [Setup CI/CD]
```

---

## 布局与样式

### 方向
- `TB` / `TD` — 从上到下（默认）
- `LR` — 从左到右
- `RL` — 从右到左
- `BT` — 从下到上

### 节点样式
```mermaid
flowchart TD
    A[Node A]
    B[Node B]
    style A fill:#90EE90,stroke:#333,stroke-width:2px
    style B fill:#ff6b6b,color:white
```

### 类定义样式
```mermaid
flowchart TD
    A:::success --> B:::warning
    classDef success fill:#2ECC71,color:white
    classDef warning fill:#F39C12,color:white
```

### 连线样式
```mermaid
flowchart TD
    A --> B
    linkStyle 0 stroke:#ff0000,stroke-width:2px
```

---

## 子图进阶

### 嵌套子图
```mermaid
flowchart TB
    subgraph outer["Outer Group"]
        subgraph inner["Inner Group"]
            A --> B
        end
        C --> inner
    end
```

### 子图方向
```mermaid
flowchart LR
    subgraph sub["Vertical Inside"]
        direction TB
        A --> B --> C
    end
    D --> sub
```
