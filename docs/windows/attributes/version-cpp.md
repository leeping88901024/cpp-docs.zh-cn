---
title: 版本 （c + + COM 属性）
ms.date: 10/02/2018
f1_keywords:
- vc-attr.version
helpviewer_keywords:
- version attribute
- version information, version attribute
ms.assetid: db6ce5d8-82c2-4329-b1a8-8ca2f67342cb
ms.openlocfilehash: 01c4cca846326d237fdacd19187a44e21bd15913
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50519309"
---
# <a name="version-c"></a>version (C++)

标识类的多个版本间的特定版本。

## <a name="syntax"></a>语法

```cpp
[ version("version") ]
```

### <a name="parameters"></a>参数

*版本*<br/>
版本号`coclass`。 如果未指定，则将在.idl 文件中放置 1.0。

## <a name="remarks"></a>备注

**版本**c + + 属性具有相同的功能[版本](/windows/desktop/Midl/version)MIDL 特性并将传递给生成的.idl 文件。

## <a name="example"></a>示例

请参阅[可绑定](bindable.md)的示例使用的示例**版本**。

## <a name="requirements"></a>要求

### <a name="attribute-context"></a>特性上下文

|||
|-|-|
|**适用对象**|**类**，**结构**|
|**可重复**|否|
|**必需的特性**|**coclass**|
|**无效的特性**|无|

有关特性上下文的详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>请参阅

[编译器特性](compiler-attributes.md)<br/>
[类特性](class-attributes.md)