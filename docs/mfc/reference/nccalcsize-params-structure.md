---
title: NCCALCSIZE_PARAMS 结构
ms.date: 11/04/2016
f1_keywords:
- NCCALCSIZE_PARAMS
helpviewer_keywords:
- NCCALCSIZE_PARAMS structure [MFC]
ms.assetid: 3424cd9f-806a-4089-82fb-414187589edf
ms.openlocfilehash: 3dbe1fcdb941a94876dd95a0eed86d6f4a3e15c6
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50443766"
---
# <a name="nccalcsizeparams-structure"></a>NCCALCSIZE_PARAMS 结构

`NCCALCSIZE_PARAMS`结构包含处理 WM_NCCALCSIZE 消息时使用应用程序可以计算大小、 位置和客户端区域的一个窗口中的有效内容的信息。

## <a name="syntax"></a>语法

```
typedef struct tagNCCALCSIZE_PARAMS {
    RECT rgrc[3];
    PWINDOWPOS lppos;
} NCCALCSIZE_PARAMS;
```

#### <a name="parameters"></a>参数

*rgrc*<br/>
指定的矩形的数组。 第一个包含新的坐标，已被移动或调整大小的窗口。 它已移动或调整大小之前，第二个包含窗口的坐标。 第三个包含前它已移动或调整大小的窗口工作区的坐标。 如果在窗口的子窗口，坐标是相对于父窗口的客户端区域。 如果窗口为顶级窗口，坐标是相对于屏幕。

*lppos*<br/>
指向[WINDOWPOS](../../mfc/reference/windowpos-structure1.md)结构，它包含导致要移动或调整大小的窗口的操作中指定的大小和位置值。

## <a name="requirements"></a>要求

**标头：** winuser.h

## <a name="see-also"></a>请参阅

[结构、样式、回调和消息映射](../../mfc/reference/structures-styles-callbacks-and-message-maps.md)<br/>
[CWnd::OnNcCalcSize](../../mfc/reference/cwnd-class.md#onnccalcsize)

