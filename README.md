```mermaid
graph TD
    subgraph 5-Stage Shift Register
        direction LR
        A1(a₁) --> A2(a₂) --> A3(a₃) --> A4(a₄) --> A5(a₅)
    end
    A5 -- 输出序列 --> Output(Output)

    XOR_Gate(⊕)  // 定义XOR门节点，文本为⊕

    A1 --.-> XOR_Gate
    A4 --.-> XOR_Gate
    XOR_Gate -- 反馈 --> A1
```
