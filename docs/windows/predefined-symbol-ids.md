---
title: 预定义的符号 ID
ms.date: 11/04/2016
helpviewer_keywords:
- symbols [C++], predefined IDs
- predefined symbol IDs
ms.assetid: 91a5d610-1a04-47e8-b8a4-63ad650a90df
ms.openlocfilehash: cb2f80315e0480c3fcb73092123cad88712dff05
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50477293"
---
# <a name="predefined-symbol-ids"></a>预定义的符号 ID

开始新项目时，根据项目类型预定义了一些符号 ID 供你使用。 这些符号 ID 支持 MFC 等各种库和项目类型。 它们表示通常包含于任何应用程序或硬件项（如鼠标或打印机）动作中的常见任务。

处理资源时，这些符号 ID 变得很重要。 它们可用于编辑快捷键表，其中一些已与虚拟键相关联。 它们还可供你完成[属性窗口](/visualstudio/ide/reference/properties-window)。 你可以将任何预定义的符号 ID 分配给新资源，也可以向它们分配快捷键，与该符号 ID 关联的功能会自动与该密钥组合关联。

以下具有预定义符号的库将显示为项目的一部分：

- [MFC 预定义的符号](../windows/mfc-predefined-symbols.md)

- [ATL 预定义的符号](../windows/atl-predefined-symbols.md)

- [Win32 预定义符号](../windows/win32-predefined-symbols.md)

   > [!NOTE]
   > 预定义的符号始终是只读的。

## <a name="requirements"></a>要求

Win32、MFC 或 ATL

## <a name="see-also"></a>请参阅

[符号：资源标识符](../windows/symbols-resource-identifiers.md)