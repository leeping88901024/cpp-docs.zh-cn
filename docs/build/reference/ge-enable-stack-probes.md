---
title: /Ge（启用堆栈探测）
ms.date: 11/04/2016
f1_keywords:
- /ge
helpviewer_keywords:
- -Ge compiler option [C++]
- enable stack probes
- /Ge compiler option [C++]
- stack, stack probes
- stack probes
- stack checking calls
- Ge compiler option [C++]
ms.assetid: 4b54deae-4e3c-4bfa-95f3-ba23590f7258
ms.openlocfilehash: 485a6a479f4d0d6c9e5eb745eda894a01f356e8c
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50448927"
---
# <a name="ge-enable-stack-probes"></a>/Ge（启用堆栈探测）

激活堆栈探测每个函数调用需要存储的本地变量。

## <a name="syntax"></a>语法

```
/Ge
```

## <a name="remarks"></a>备注

此机制是重写的堆栈探测功能的情况下很有用。 建议你使用[/Gh (启用 _penter 挂钩函数)](../../build/reference/gh-enable-penter-hook-function.md)而不是重写堆栈探测。

[/Gs （控制堆栈检查调用）](../../build/reference/gs-control-stack-checking-calls.md)具有相同的效果。

**/Ge**是不推荐使用; 开始在 Visual Studio 2005 中，编译器会自动生成堆栈检查。 有关不推荐使用的编译器选项的列表，请参阅**已弃用并删除的编译器选项**中[按类别列出的编译器选项](../../build/reference/compiler-options-listed-by-category.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[使用项目属性](../../ide/working-with-project-properties.md)。

1. 单击 **“C/C++”** 文件夹。

1. 点击“命令行”  属性页。

1. 在 **“附加选项”** 框中键入编译器选项。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>。

## <a name="see-also"></a>请参阅

[编译器选项](../../build/reference/compiler-options.md)<br/>
[设置编译器选项](../../build/reference/setting-compiler-options.md)