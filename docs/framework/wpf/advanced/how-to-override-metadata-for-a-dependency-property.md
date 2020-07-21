---
title: '方法: 依存関係プロパティのメタデータをオーバーライドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- metadata [WPF], overriding for dependency properties
- dependency properties [WPF], overriding metadata for
- overriding metadata for dependency properties [WPF]
ms.assetid: f90f026e-60d8-428a-933d-edf0dba4441f
ms.openlocfilehash: ef0309ae0d03c8278134012e645960996c6f93c4
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610510"
---
# <a name="how-to-override-metadata-for-a-dependency-property"></a>方法: 依存関係プロパティのメタデータをオーバーライドする
この例では、継承したクラスの既定の依存関係プロパティのメタデータを、<xref:System.Windows.DependencyProperty.OverrideMetadata%2A> メソッドを呼び出して型固有のメタデータを提供することで、オーバーライドする方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.PropertyMetadata> を定義することにより、クラスで依存関係プロパティの動作 (既定値、プロパティ システム コールバックなど) を定義できます。 多くの依存関係プロパティ クラスで、登録プロセスの一部として既定のメタデータが既に確立されています。 これには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API の一部である依存関係プロパティが含まれます。 クラス継承により依存関係プロパティを継承するクラスは、メタデータで変更できるプロパティの特性がサブクラス固有の要件に合致するように、元のメタデータをオーバーライドできます。  
  
 依存関係プロパティでのメタデータのオーバーライドは、そのプロパティがプロパティ システムによって使用される (プロパティを登録するオブジェクトの特定のインスタンスがインスタンス化されるタイミングに相当) 前に実行する必要があります。 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> の呼び出しは、自身を <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> の `forType` パラメーターとして提供する型の静的コンストラクター内で実行される必要があります。 所有者型のインスタンスが存在する場合にメタデータを変更しようとすると、例外は発生しませんが、プロパティ システムに不整合な動作が発生します。 また、メタデータは 1 つの型につき 1 回しかオーバーライドできません。 それ以降に同じ型のメタデータをオーバーライドしようとすると、例外が発生します。  
  
 次の例では、`MyAdvancedStateControl` カスタム クラスが、`MyAdvancedStateControl` によって `StateProperty` に提供されるメタデータを、新しいプロパティ メタデータでオーバーライドします。 たとえば、新しく構築された `MyAdvancedStateControl` インスタンスでプロパティが照会されると、`StateProperty` の既定値は `true` となります。  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
[!code-csharp[PropertySystemEsoterics#MyAdvancedStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#myadvancedstatecontrol)]
[!code-vb[PropertySystemEsoterics#MyAdvancedStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#myadvancedstatecontrol)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.DependencyProperty>
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
- [方法トピック](properties-how-to-topics.md)
