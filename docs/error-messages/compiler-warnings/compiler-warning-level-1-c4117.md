---
title: 编译器警告（等级 1）C4117
ms.date: 11/04/2016
f1_keywords:
- C4117
helpviewer_keywords:
- C4117
ms.assetid: c45aa281-4cc1-4dfd-bd32-bd7a60ddd577
ms.openlocfilehash: 657963dd0199c1474f0cef566e5a177a16247521
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50466207"
---
# <a name="compiler-warning-level-1-c4117"></a>编译器警告（等级 1）C4117

保留“name”宏名；已忽略“Command”

### <a name="to-fix-by-checking-the-following-possible-causes"></a>通过检查以下可能的原因进行修复

1. 尝试定义或取消定义预定义的宏。

1. 尝试定义或取消定义预处理器运算符 **defined**。

以下示例生成 C4117：

```
// C4117.cpp
// compile with: /W1
#define __FILE__ test         // C4117. __FILE__ is a predefined macro
#define ValidMacroName test   // ok

int main() {
}
```