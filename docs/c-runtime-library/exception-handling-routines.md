---
title: 异常处理例程
ms.date: 11/04/2016
f1_keywords:
- c.exceptions
helpviewer_keywords:
- exception handling, routines
ms.assetid: f60548c6-850a-4e1e-a79b-a2a6a541ab62
ms.openlocfilehash: 09d58e49d3c9dc9b4b8ef40f725e927603e3e47c
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50507453"
---
# <a name="exception-handling-routines"></a>异常处理例程

在程序执行期间使用 C++ 异常处理函数从意外事件恢复。

## <a name="exception-handling-functions"></a>异常处理函数

|函数|使用|
|--------------|---------|
|[_set_se_translator](../c-runtime-library/reference/set-se-translator.md)|将 Win32 异常（C 结构的异常）处理为 C++ 类型的异常|
|[set_terminate](../c-runtime-library/reference/set-terminate-crt.md)|安装 terminate 将调用的自身的终止例程|
|[set_unexpected](../c-runtime-library/reference/set-unexpected-crt.md)|安装要由 unexpected 调用的自身的终止函数|
|[terminate](../c-runtime-library/reference/terminate-crt.md)|引发异常后在特定情况下自动调用。 terminate 函数调用 abort 或使用 set_terminate 指定的函数|
|[unexpected](../c-runtime-library/reference/unexpected-crt.md)|调用 terminate 或使用 set_unexpected 指定的函数。 不会在当前 Microsoft C++ 异常处理实现中使用 unexpected 函数|

## <a name="see-also"></a>请参阅

[按类别分的通用 C 运行时例程](../c-runtime-library/run-time-routines-by-category.md)<br/>
