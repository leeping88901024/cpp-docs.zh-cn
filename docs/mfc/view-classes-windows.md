---
title: 视图类 (Windows)
ms.date: 11/04/2016
f1_keywords:
- vc.classes.view
helpviewer_keywords:
- form and record views [MFC]
- splitter window classes [MFC]
- view classes [MFC], Windows
ms.assetid: b11683fb-9f43-4de3-9499-2b55775f9870
ms.openlocfilehash: 5fc08ec23e0a2b2ba105aa3a633ee862dc452450
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50462291"
---
# <a name="view-classes-windows"></a>视图类 (Windows)

`CView` 和其派生的类是表示框架窗口的工作区的子窗口。 视图显示数据，并接受输入文档。

视图类是与文档类和使用文档模板对象的框架窗口类相关联。

[CView](../mfc/reference/cview-class.md)<br/>
特定于应用程序的数据视图的文档的基类。 视图显示数据，并接受用户输入来编辑或选择的数据。 从派生视图类`CView`。

[CScrollView](../mfc/reference/cscrollview-class.md)<br/>
带滚动功能的视图的基类。 派生视图类从`CScrollView`的自动滚动。

## <a name="form-and-record-views"></a>窗体和记录视图

窗体视图也滚动视图。 它们基于对话框模板。

记录视图派生自窗体视图。 除了对话框模板，它们还具有与数据库的连接。

[CFormView](../mfc/reference/cformview-class.md)<br/>
在对话框模板中定义其布局滚动视图。 从派生类`CFormView`以实现基于对话框模板的用户界面。

[CDaoRecordView](../mfc/reference/cdaorecordview-class.md)<br/>
提供了一种直接连接到数据访问对象 (DAO) 记录集对象的视图。 像所有窗体视图中，`CDaoRecordView`基于对话框模板。

[CRecordView](../mfc/reference/crecordview-class.md)<br/>
提供了一种直接连接到开放式数据库连接 (ODBC) 记录集对象的视图。 像所有窗体视图中，`CRecordView`基于对话框模板。

[CHtmlEditView](../mfc/reference/chtmleditview-class.md)<br/>
窗体视图提供 webbrowser 控件中 HTML 编辑平台功能。

## <a name="control-views"></a>控件视图

控件视图显示为其视图的控件。

[CCtrlView](../mfc/reference/cctrlview-class.md)<br/>
与 Windows 控件相关联的所有视图的基类。 根据控件的视图如下所述。

[CEditView](../mfc/reference/ceditview-class.md)<br/>
包含 Windows 标准的视图编辑控件 (请参阅[CEdit](../mfc/reference/cedit-class.md))。 编辑控件支持文本编辑、 搜索、 替换和滚动功能。

[CRichEditView](../mfc/reference/cricheditview-class.md)<br/>
一个包含 Windows 丰富视图编辑控件 (请参阅[CRichEditCtrl](../mfc/reference/cricheditctrl-class.md))。 一个编辑控件的功能，除了格式文本编辑控件支持字体、 颜色、 段落格式设置，和嵌入的 OLE 对象。

[CListView](../mfc/reference/clistview-class.md)<br/>
包含 Windows 列表控件的视图 (请参阅[CListCtrl](../mfc/reference/clistctrl-class.md))。 列表控件显示的项，其中每个包括的一个图标和标签时，在文件资源管理器的方式类似于在右窗格中的集合。

[Ctreeview 类](../mfc/reference/ctreeview-class.md)<br/>
包含 Windows 树控件的视图 (请参阅[CTreeCtrl](../mfc/reference/ctreectrl-class.md))。 树控件显示图标和标签的排列方式类似于左窗格中的文件资源管理器中的层次的列表。

## <a name="related-classes"></a>相关的类

`CSplitterWnd` 可以在单个框架窗口内有多个视图。 `CPrintDialog` 和`CPrintInfo`支持视图的打印和打印预览功能。 `CRichEditDoc` 并`CRichEditCntrItem`与一起使用`CRichEditView`实现 OLE 容器功能。

[CSplitterWnd](../mfc/reference/csplitterwnd-class.md)<br/>
用户可以将拆分为多个窗格窗口。 这些窗格可由用户或固定的大小可调整大小。

[CPrintDialog](../mfc/reference/cprintdialog-class.md)<br/>
提供用于打印文件的标准对话框。

[CPrintInfo](../mfc/reference/cprintinfo-structure.md)<br/>
包含有关打印或打印预览作业的信息的结构。 由`CView`打印体系结构。

[CRichEditDoc](../mfc/reference/cricheditdoc-class.md)<br/>
维护中的 OLE 客户端项的列表`CRichEditView`。

[CRichEditCntrItem](../mfc/reference/cricheditcntritem-class.md)<br/>
提供对 OLE 项存储在客户端访问`CRichEditView`。

## <a name="see-also"></a>请参阅

[类概述](../mfc/class-library-overview.md)

