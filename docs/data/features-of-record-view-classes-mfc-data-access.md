---
title: 记录视图类的功能（MFC 数据访问）
ms.date: 11/04/2016
helpviewer_keywords:
- record views, classes
- record view classes
ms.assetid: e7b2820f-09c4-483f-83c0-317e8be42bdf
ms.openlocfilehash: 2feda8f8f446e02a5056287c656707ea038f5387
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50461147"
---
# <a name="features-of-record-view-classes--mfc-data-access"></a>记录视图类的功能（MFC 数据访问）

您可以执行基于窗体的数据访问编程的类[CFormView](../mfc/reference/cformview-class.md)，但[CRecordView](../mfc/reference/crecordview-class.md)通常是更好的类进行派生。 除了其`CFormView`功能， `CRecordView`:

- 提供窗体控件和关联的记录集对象之间的对话框数据交换 (DDX)。

- 处理移动第一个、 移动到下一步、 移动上一个和移动最后一个命令浏览关联记录集对象中的记录。

- 当用户移到另一条记录时，更新将更改为当前记录。

有关导航的详细信息，请参阅[记录视图： 支持在记录视图中导航](../data/supporting-navigation-in-a-record-view-mfc-data-access.md)。

## <a name="see-also"></a>请参阅

[记录视图（MFC 数据访问）](../data/record-views-mfc-data-access.md)<br/>
[ODBC 驱动程序列表](../data/odbc/odbc-driver-list.md)