---
title: 优化控件绘制
ms.date: 11/04/2016
helpviewer_keywords:
- MFC ActiveX controls [MFC], optimizing
ms.assetid: 29ff985d-9bf5-4678-b62d-aad12def75fb
ms.openlocfilehash: 9096c43088c89ceef9e57d0e3a994340f9115d6b
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50487342"
---
# <a name="optimizing-control-drawing"></a>优化控件绘制

在指示某个控件将自身绘制到容器提供的设备上下文中时，它通常会将 GDI 对象（如钢笔、画笔和字体）选择到设备上下文中，执行其绘制操作，并还原之前的 GDI 对象。 假设容器有多个要绘制到相同设备上下文中的控件，且每个控件选择其所需的 GDI 对象，那么，如果控件不单个地还原之前选中的对象，则可以节省时间。 绘制所有控件之后，容器可以自动还原原始对象。

若要检测容器是否支持此技术，控件可调用[colecontrol:: Isoptimizeddraw](../mfc/reference/colecontrol-class.md#isoptimizeddraw)成员函数。 如果此函数返回 **，则返回 TRUE**，控件可以跳过还原之前选中的对象的一般步骤。

考虑具有以下（未优化的）`OnDraw` 函数的控件：

[!code-cpp[NVC_MFC_AxOpt#15](../mfc/codesnippet/cpp/optimizing-control-drawing_1.cpp)]

本例中的钢笔和画笔是局部变量，这意味着将在它们超出范围时（`OnDraw` 函数结束时）调用其析构函数。 析构函数将尝试删除对应的 GDI 对象。 但是，如果您打算在从 `OnDraw` 返回时仍让它们留在设备上下文中，则不应将它们删除。

若要防止[CPen](../mfc/reference/cpen-class.md)并[CBrush](../mfc/reference/cbrush-class.md)对象时销毁`OnDraw`完成之后，将其存储在成员变量而不是本地变量。 在控件的类声明中，添加两个新成员变量的声明：

[!code-cpp[NVC_MFC_AxOpt#16](../mfc/codesnippet/cpp/optimizing-control-drawing_2.h)]
[!code-cpp[NVC_MFC_AxOpt#17](../mfc/codesnippet/cpp/optimizing-control-drawing_3.h)]

然后，可以按如下方法重写 `OnDraw` 函数：

[!code-cpp[NVC_MFC_AxOpt#18](../mfc/codesnippet/cpp/optimizing-control-drawing_4.cpp)]

每次调用 `OnDraw` 时，此方法将避免创建钢笔和画笔。 速度提升是以维护附加实例数据为代价的。

如果更改 ForeColor 或 BackColor 属性，则需要重新创建钢笔或画笔。 若要执行此操作，重写[OnForeColorChanged](../mfc/reference/colecontrol-class.md#onforecolorchanged)并[OnBackColorChanged](../mfc/reference/colecontrol-class.md#onbackcolorchanged)成员函数：

[!code-cpp[NVC_MFC_AxOpt#19](../mfc/codesnippet/cpp/optimizing-control-drawing_5.cpp)]

最后，若要清除不必要的 `SelectObject` 调用，请修改 `OnDraw`，方法如下：

[!code-cpp[NVC_MFC_AxOpt#20](../mfc/codesnippet/cpp/optimizing-control-drawing_6.cpp)]

## <a name="see-also"></a>请参阅

[MFC ActiveX 控件：优化](../mfc/mfc-activex-controls-optimization.md)<br/>
[COleControl 类](../mfc/reference/colecontrol-class.md)<br/>
[MFC ActiveX 控件](../mfc/mfc-activex-controls.md)<br/>
[MFC ActiveX 控件](../mfc/mfc-activex-controls.md)<br/>
[MFC ActiveX 控件向导](../mfc/reference/mfc-activex-control-wizard.md)<br/>
[MFC ActiveX 控件：绘制 ActiveX 控件](../mfc/mfc-activex-controls-painting-an-activex-control.md)

