---
title: 编译器错误 C3655
ms.date: 11/04/2016
f1_keywords:
- C3655
helpviewer_keywords:
- C3655
ms.assetid: 724919ab-2915-4b61-8794-44648e162d62
ms.openlocfilehash: 268994b2e694c6260a3fc9e9edf102ec0127ee31
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50448592"
---
# <a name="compiler-error-c3655"></a>编译器错误 C3655

function： 函数已经显式重写

函数可以仅显式重写一次。 有关详细信息，请参阅[显式重写](../../windows/explicit-overrides-cpp-component-extensions.md)。

下面的示例生成 C3655:

```
// C3655.cpp
// compile with: /clr /c
public ref struct B {
   virtual void f();
   virtual void g();
};

public ref struct D : B {
   virtual void f() new sealed = B::f;
   virtual void g() new sealed = B::f;   // C3655
   // try the following line instead
   // virtual void g() new sealed = B::g;
};
```