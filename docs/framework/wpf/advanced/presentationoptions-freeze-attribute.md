---
title: PresentationOptions:Freeze 属性
ms.date: 03/30/2017
helpviewer_keywords:
- Freeze attribute [WPF]
- Freezable elements [WPF]
- PresentationOptions prefix [WPF]
ms.assetid: 391032dd-2fba-4804-bb8a-3b071797a9f4
ms.openlocfilehash: d3e0cee293a9585b972b0145da953976ed94b74c
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991421"
---
# <a name="presentationoptionsfreeze-attribute"></a>PresentationOptions:Freeze 属性
含まれている <xref:System.Windows.Freezable> 要素上で <xref:System.Windows.Freezable.IsFrozen%2A> 状態を `true` に設定します。 `PresentationOptions:Freeze` 属性が指定されていない <xref:System.Windows.Freezable> の既定の動作では、<xref:System.Windows.Freezable.IsFrozen%2A> は読み込み時は `false` であり、実行時は一般的な <xref:System.Windows.Freezable> 動作に依存します。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xaml  
<object  
  xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="PresentationOptions">  
    <freezableElement PresentationOptions:Freeze="true"/>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`PresentationOptions`|XML 1.0 仕様に従った、任意の有効なプレフィックス文字列を指定できる XML 名前空間プレフィックス。 このドキュメントでは、プレフィックス `PresentationOptions` が識別のために使用されます。|  
|`freezableElement`|<xref:System.Windows.Freezable> のあらゆる派生クラスをインスタンス化する要素。|  
  
## <a name="remarks"></a>Remarks  
 `Freeze` 属性は、`http://schemas.microsoft.com/winfx/2006/xaml/presentation/options` XML 名前空間で定義されている唯一の属性またはその他のプログラミング要素です。 `Freeze` 属性は、特にルート要素宣言の一部として [mc:Ignorable 属性](mc-ignorable-attribute.md) を使用して無視可能として指定できるように、この特別な名前空間に存在します。 `Freeze` を無視可能とできるようにする必要がある理由は、すべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサ実装で読み込み時に <xref:System.Windows.Freezable> を凍結できるわけではないためです。この機能は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 仕様には含まれていません。  
  
 `Freeze` 属性を処理する機能は、コンパイル済みアプリケーションの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を処理する [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサに特に組み込まれています。 この属性はどのクラスでもサポートされていません。また、属性の構文は拡張または変更できません。 独自の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサを実装する場合は、読み込み時に <xref:System.Windows.Freezable> 要素の `Freeze` 属性を処理するときに、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの固定動作を並列処理することを選択できます。  
  
 `Freeze` 属性の値が `true` 以外の場合 (大文字と小文字は区別されません)、読み込み時エラーが生成されます (`Freeze` 属性を `false` として指定することはエラーではありませんが、既に既定値であるため、`false` に設定しても何も行われません)。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Freezable>
- [Freezable オブジェクトの概要](freezable-objects-overview.md)
- [mc:Ignorable 属性](mc-ignorable-attribute.md)
