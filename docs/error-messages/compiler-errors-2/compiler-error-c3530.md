---
title: 编译器错误 C3530
ms.date: 11/04/2016
f1_keywords:
- C3530
helpviewer_keywords:
- C3530
ms.assetid: 21be81ce-b699-4c74-81bc-80a0c34d2d5a
ms.openlocfilehash: 90f6000c7d4c4bfa0d610bd5942df0b958e47c60
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50643620"
---
# <a name="compiler-error-c3530"></a>编译器错误 C3530

'auto' 不能与任何其他类型说明符组合

与一起使用的类型说明符`auto`关键字。

### <a name="to-correct-this-error"></a>更正此错误

1. 不使用的变量声明中使用的类型说明符`auto`关键字。

## <a name="example"></a>示例

下面的示例会产生 C3530，因为变量`x`声明两个`auto`关键字和类型`int`，因为使用编译该示例 **/zc: auto**。

```
// C3530.cpp
// Compile with /Zc:auto
int main()
{
   auto int x;   // C3530
   return 0;
}
```

## <a name="see-also"></a>请参阅

[auto 关键字](../../cpp/auto-keyword.md)