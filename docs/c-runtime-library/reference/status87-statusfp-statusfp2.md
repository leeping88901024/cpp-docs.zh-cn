---
title: _status87, _statusfp, _statusfp2
ms.date: 04/05/2018
apiname:
- _statusfp2
- _statusfp
- _status87
apilocation:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-runtime-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _statusfp2
- _statusfp
- statusfp2
- _status87
- status87
- statusfp
helpviewer_keywords:
- floating-point functions, getting status word
- floating-point numbers, status word
- status87 function
- status word, getting floating point
- statusfp function
- _statusfp function
- _statusfp2 function
- statusfp2 function
- _status87 function
- floating-point functions
- status word
ms.assetid: 7ef963fa-b1fb-429d-94d6-fbf282ab7432
ms.openlocfilehash: 271c28dd4e267e5b3b702858cc398689e3e35d6f
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50597507"
---
# <a name="status87-statusfp-statusfp2"></a>_status87, _statusfp, _statusfp2

获取浮点状态字。

## <a name="syntax"></a>语法

```C
unsigned int _status87( void );
unsigned int _statusfp( void );
void _statusfp2(unsigned int *px86, unsigned int *pSSE2)
```

### <a name="parameters"></a>参数

*px86*<br/>
此地址用 x87 浮点单元的状态字填充。

*pSSE2*<br/>
此地址用 SSE2 浮点单元的状态字填充。

## <a name="return-value"></a>返回值

有关 **_status87**并 **_statusfp**，则返回的值中的位表示浮点状态。 请参阅 FLOAT。H 包含返回的位的定义文件 **_statusfp**。 许多数学库函数修改了浮点状态字，结果不可预知。 优化可以重新排序、 组合和消除浮点运算调用到周围 **_status87**， **_statusfp**，和相关函数。 使用 [/Od（禁用（调试））](../../build/reference/od-disable-debug.md)编译器选项或 [fenv_access](../../preprocessor/fenv-access.md) pragma 指令，可防止对浮点操作重新排序的优化。 返回值从 **_clearfp**和 **_statusfp**，并返回参数的 **_statusfp2**，如果执行了较少的浮点操作更可靠之间的浮点状态字的已知状态。

## <a name="remarks"></a>备注

**_Statusfp**函数获取浮点状态字。 状态字是浮点异常处理程序检测出的浮点处理程序状态和其他条件的组合（例如，浮点堆栈溢出和下溢）。 在返回状态字的内容之前检查未屏蔽的异常。 这表示通知调用方挂起异常。 在 x86 平台， **_statusfp**返回 x87 和 SSE2 浮点状态的组合。 在 x64 平台上，返回的状态基于 SSE 的 MXCSR 状态。 在 ARM 平台上 **_statusfp**从 FPSCR 寄存器返回状态。

**_statusfp**是一个独立于平台的、 可移植的版本 **_status87**。 它等同于 **_status87** Intel (x86) 平台上和也受 x64 和 ARM 平台。 若要确保你的浮点代码可移植到所有体系结构，使用 **_statusfp**。 如果你只面向 x86 平台，你可以使用 **_status87**或 **_statusfp**。

我们建议 **_statusfp2**的同时具有 x87 和 SSE2 浮点处理器的芯片 （如 Pentium IV)。 有关 **_statusfp2**，通过使用 x87 或 SSE2 浮点处理器的浮点状态字填充地址。 对于支持 x87 和 SSE2 浮点处理器的芯片，EM_AMBIGUOUS 设置为 1，如果 **_statusfp**或 **_controlfp**使用和操作是不明确，因为它可以引用 x87 或 SSE2浮点状态字。 **_Statusfp2**函数仅支持在 x86 平台。

这些函数没有用处[/clr （公共语言运行时编译）](../../build/reference/clr-common-language-runtime-compilation.md)因为公共语言运行时 (CLR) 仅支持默认浮点精度。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_status87**， **_statusfp**， **_statusfp2**|\<float.h>|

有关其他兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_statusfp.c
// Build by using: cl /W4 /Ox /nologo crt_statusfp.c
// This program creates various floating-point errors and
// then uses _statusfp to display messages that indicate these problems.

#include <stdio.h>
#include <float.h>
#pragma fenv_access(on)

double test( void )
{
   double a = 1e-40;
   float b;
   double c;

   printf("Status = 0x%.8x - clear\n", _statusfp());

   // Assignment into b is inexact & underflows:
   b = (float)(a + 1e-40);
   printf("Status = 0x%.8x - inexact, underflow\n", _statusfp());

   // c is denormal:
   c = b / 2.0;
   printf("Status = 0x%.8x - inexact, underflow, denormal\n",
            _statusfp());

   // Clear floating point status:
   _clearfp();
   return c;
}

int main(void)
{
   return (int)test();
}
```

```Output
Status = 0x00000000 - clear
Status = 0x00000003 - inexact, underflow
Status = 0x00080003 - inexact, underflow, denormal
```

## <a name="see-also"></a>请参阅

[浮点支持](../../c-runtime-library/floating-point-support.md)<br/>
[_clear87、_clearfp](clear87-clearfp.md)<br/>
[_control87、_controlfp、\__control87_2](control87-controlfp-control87-2.md)<br/>
