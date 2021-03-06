---
title: FILETIME 结构
ms.date: 11/04/2016
f1_keywords:
- FILETIME
helpviewer_keywords:
- FILETIME structure [MFC]
ms.assetid: e09557e2-b6d7-4dd5-a5b9-6328bca88595
ms.openlocfilehash: f70792b83637018e707b6ee48d1b169f28d46d71
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50514928"
---
# <a name="filetime-structure"></a>FILETIME 结构

`FILETIME`结构是 64 位值表示从 1601 年 1 月 1 日起 100 纳秒间隔数。

## <a name="syntax"></a>语法

```
typedef struct _FILETIME {
    DWORD dwLowDateTime;   /* low 32 bits */
    DWORD dwHighDateTime;  /* high 32 bits */
} FILETIME, *PFILETIME, *LPFILETIME;
```

#### <a name="parameters"></a>参数

*dwLowDateTime*<br/>
指定最小的文件时间的 32 位。

*dwHighDateTime*<br/>
指定高 32 位的文件时间。

## <a name="requirements"></a>要求

**标头：** windef.h

## <a name="see-also"></a>请参阅

[结构、样式、回调和消息映射](../../mfc/reference/structures-styles-callbacks-and-message-maps.md)<br/>
[CTime::CTime](../../atl-mfc-shared/reference/ctime-class.md#ctime)

