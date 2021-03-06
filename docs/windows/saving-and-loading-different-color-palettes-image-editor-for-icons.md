---
title: 保存和加载不同的调色板（图标的图像编辑器）
ms.date: 11/04/2016
f1_keywords:
- vc.editors.image.color
helpviewer_keywords:
- color palettes [C++]
- palettes
- palettes, Image editor
- colors [C++], Image editor
- Image editor [C++], palettes
ms.assetid: 694b6346-e606-4f19-aa01-9b4ceb47f423
ms.openlocfilehash: 847004210d5c0672fe013c51e59de5c9f849f977
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50447978"
---
# <a name="saving-and-loading-different-color-palettes-image-editor-for-icons"></a>保存和加载不同的调色板（图标的图像编辑器）

可以保存和加载**颜色**包含调色板，其[自定义颜色](../windows/customizing-or-changing-colors-image-editor-for-icons.md)。 (默认情况下**颜色**启动 Visual Studio 时，会自动加载最近使用的调色板。)

> [!TIP]
> 由于**图像**编辑器具有无法还原默认**颜色**面板中，应保存默认**颜色**如名下调色板*standard.pal*或*default.pal* ，以便可以轻松还原默认设置。

### <a name="to-save-a-custom-colors-palette"></a>保存自定义调色板

1. 从**图像**菜单中，选择**保存调色板**。

2. 导航到要用于保存调色板的目录并键入调色板的名称。

3. 单击“保存” 。

### <a name="to-load-a-custom-colors-palette"></a>加载自定义调色板

1. 从**图像**菜单中，选择**加载调色板**。

2. 在中[加载调色板对话框](../windows/load-palette-colors-dialog-box-image-editor-for-icons.md)，导航到正确的目录，然后选择你想要加载的调色板。 **颜色**使用.pal 文件扩展名保存调色板。

## <a name="requirements"></a>要求

无

## <a name="see-also"></a>请参阅

[加速键](../windows/accelerator-keys-image-editor-for-icons.md)<br/>
[处理颜色](../windows/working-with-color-image-editor-for-icons.md)