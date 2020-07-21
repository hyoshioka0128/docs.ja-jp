---
title: ColorConvertedBitmap のマークアップ拡張機能
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], ColorConvertedBitmap markup extension
- ColorConvertedBitmap markup extension [WPF]
ms.assetid: 18321c18-c898-4470-93fa-a702b47770c1
ms.openlocfilehash: a5b491723a036c1b1fd0bb61736e6f2ee53fbcd3
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141225"
---
# <a name="colorconvertedbitmap-markup-extension"></a>ColorConvertedBitmap のマークアップ拡張機能
埋め込みプロファイルのないビットマップ ソースを指定する方法を提供します。 カラー コンテキストおよびプロファイルは、画像ソースの URI と同様に、URI によって指定されます。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xml  
<object property="{ColorConvertedBitmap imageSource sourceIIC destinationIIC}" ... />
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`imageSource`|プロファイルにされていないビットマップの URI。|  
|`sourceIIC`|ソース プロファイル構成の URI。|  
|`destinationIIC`|ターゲット プロファイル構成の URI。|  
  
## <a name="remarks"></a>Remarks  
 このマークアップ拡張では、<xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A> などの画像ソース プロパティ値の関連するセットを設定することが意図されています。  
  
 属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `ColorConvertedBitmap` (または `ColorConvertedBitmapExtension`) は、プロパティ要素の構文では使用できません。これは、最初のコンストラクターの値としてのみ値を設定できるだめです (拡張識別子の後の文字列)。  
  
 `ColorConvertedBitmap` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のすべてのマークアップ拡張では、それぞれの属性構文で { と } の 2 つの記号が使用されます。これは規約であり、これに従って [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、マークアップ拡張で属性を処理する必要があることが認識されます。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [イメージングの概要](../graphics-multimedia/imaging-overview.md)
