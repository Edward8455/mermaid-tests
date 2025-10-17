graph TD
    subgraph 5-Stage Shift Register
        direction LR
        A1(a₁) --> A2(a₂) --> A3(a₃) --> A4(a₄) --> A5(a₅)
    end
    A5 -- 输出序列 --> Output(Output)
    A1 --.-> XOR(⊕)
    A4 --.-> XOR
    XOR -- 反馈 --> A1
