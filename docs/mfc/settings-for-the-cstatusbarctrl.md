---
title: CStatusBarCtrl 的设置
ms.date: 11/04/2016
f1_keywords:
- CStatusBarCtrl
helpviewer_keywords:
- status bar controls [MFC], settings
- CStatusBarCtrl class [MFC], settings
ms.assetid: adeba0c3-17f3-435c-b140-a57845e9ce49
ms.openlocfilehash: a4806cdc81a536aac0b9472ca043d4d2de027495
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50676520"
---
# <a name="settings-for-the-cstatusbarctrl"></a>CStatusBarCtrl 的设置

默认位置[CStatusBarCtrl](../mfc/reference/cstatusbarctrl-class.md)状态窗口的父窗口底部，但可以指定要让其显示在父窗口工作区顶部的 CCS_TOP 样式。

可以指定要包括在右端的大小调整手柄的 SBARS_SIZEGRIP 样式`CStatusBarCtrl`状态窗口。 大小调整手柄类似于大小调整边框；它是用户可以通过单击和拖动来重设父窗口大小的矩形区域。

> [!NOTE]
>  如果合并 CCS_TOP 和 SBARS_SIZEGRIP 样式，即使系统将其绘制在状态窗口中不起作用的结果的大小调整手柄。

状态窗口的窗口过程将自动设置控件窗口的初始大小和位置。 宽度与父窗口工作区的一样。 高度基于实际选入状态窗口设备上下文的字体的度量值和窗口边框的宽度。

每当收到 WM_SIZE 消息时，窗口过程自动调整状态窗口的大小。 通常情况下，当父窗口的大小更改时，父级将 WM_SIZE 消息发送到状态窗口。

可以通过调用设置状态窗口绘图区的最小高度[SetMinHeight](../mfc/reference/cstatusbarctrl-class.md#setminheight)，以像素为单位指定最小高度。 绘图区不包括窗口边框。

通过调用检索状态窗口的边框的宽度[GetBorders](../mfc/reference/cstatusbarctrl-class.md#getborders)。 此成员函数包含指向三元素数组（将收到水平边框、垂直边框和矩形之间的边框的宽度）的指针。

## <a name="see-also"></a>请参阅

[使用 CStatusBarCtrl](../mfc/using-cstatusbarctrl.md)<br/>
[控件](../mfc/controls-mfc.md)

