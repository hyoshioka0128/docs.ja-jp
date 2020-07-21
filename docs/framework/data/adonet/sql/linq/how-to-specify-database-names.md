---
title: '方法: データベースの名前を指定する'
ms.date: 03/30/2017
ms.assetid: b80f0fd2-7f75-45fe-9e12-496f80f183df
ms.openlocfilehash: 0daf754edf624410e0ea725acd6c266ccb7828dc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781583"
---
# <a name="how-to-specify-database-names"></a>方法: データベースの名前を指定する
<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 属性の <xref:System.Data.Linq.Mapping.DatabaseAttribute> プロパティを使用すると、接続によってデータベースの名前が提供されない場合に、名前を指定できます。  
  
 コード例については、「<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>」を参照してください。  
  
### <a name="to-specify-the-name-of-the-database"></a>データベースの名前を指定するには  
  
1. データベースのクラス宣言に <xref:System.Data.Linq.Mapping.DatabaseAttribute> 属性を追加します。  
  
2. <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 属性に <xref:System.Data.Linq.Mapping.DatabaseAttribute> プロパティを追加します。  
  
3. <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> プロパティ値を目的の名前に設定します。  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
