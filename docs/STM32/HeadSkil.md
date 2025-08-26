# 使用 `#pragma once` 编写头文件技巧

`#pragma once` 是 C/C++ 语言中的预处理指令，用于防止头文件被重复包含（多重包含保护）。

## 作用

当一个头文件以 `#pragma once` 开头时，无论它被 `#include` 多少次，编译器只会处理一次，避免重复定义错误。

## 传统写法

等价于传统的多重包含保护写法：

```c
#ifndef MOTOR_PINS_H
#define MOTOR_PINS_H
// ...头文件内容...
#endif
```

## 优点

- `#pragma once` 更简洁
- 不需要手动编写宏名
- 可读性更高

> **注意**：虽然大多数现代编译器都支持 `#pragma once`，但极少数老旧编译器可能不支持。