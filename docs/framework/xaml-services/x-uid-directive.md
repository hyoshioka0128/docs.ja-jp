---
title: x:Uid ディレクティブ
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: 32cfd9ab0cf6037c731b619e81a7504ac92d5fb9
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837182"
---
# <a name="xuid-directive"></a>x:Uid ディレクティブ
マークアップ要素の一意の識別子を提供します。 多くのシナリオでは、この一意識別子は、XAML ローカリゼーションプロセスおよびツールによって使用されます。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用  
  
```xaml  
<object x:Uid="identifier"... />  
```  
  
## <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|`identifier`|`x:Uid` のコンシューマーによって解釈されるときに、ファイル内で一意である必要がある、手動で作成または自動生成された文字列。|  
  
## <a name="remarks"></a>Remarks  
 [MS XAML] では、`x:Uid` はディレクティブとして定義されます。 詳細については、「 [\[\]」セクション 5.3.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。  
  
 `x:Uid` は、前述の XAML ローカライズシナリオによって、また、ローカリゼーションに使用される識別子が `x:Name`のプログラミングモデルへの影響に依存しないため、`x:Name` とは異なります。 また、`x:Name` は XAML 名前スコープによって管理されます。ただし、`x:Uid` は、XAML 言語で定義された一意性の強制の概念には適用されません。 XAML プロセッサは、広範な意味で (ローカライズプロセスに含まれていないプロセッサ)、`x:Uid` 値の一意性を強制することは想定されていません。 その責任は、値の発行元によって異なります。 1つの XAML ソース内で `x:Uid` 値の一意性が期待されるのは、専用のグローバリゼーションプロセスやツールなど、値のコンシューマーにとっては妥当です。 一般的な一意性モデルは、`x:Uid` 値は、XAML を表す XML エンコードファイル内で一意であるということです。  
  
 特定の XAML スキーマについて十分な知識を持つツールは、マークアップでテキスト文字列値が検出されるすべてのケースではなく、真のローカライズ可能な文字列に対してのみ `x:Uid` を適用することを選択できます。  
  
 フレームワークでは、定義する型に属性 <xref:System.Windows.Markup.UidPropertyAttribute> を適用することによって、オブジェクトモデルの特定のプロパティを `x:Uid` の別名として指定できます。 フレームワークで特定のプロパティが指定されている場合、同じオブジェクトの `x:Uid` とエイリアスを持つメンバーの両方を指定することは無効です。 `x:Uid` とエイリアス化されたメンバーの両方が指定されている場合、.NET Framework XAML サービス API は通常、この場合に <xref:System.Xaml.XamlDuplicateMemberException> をスローします。  
  
## <a name="wpf-usage-notes"></a>WPF の使用上の注意  
 WPF のローカリゼーションプロセスと、XAML の BAML 形式での `x:Uid` のロールの詳細については、「 [wpf のグローバリゼーション](../wpf/advanced/globalization-for-wpf.md)」または「<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>」を参照してください。  
  
## <a name="see-also"></a>参照

- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [WPF のグローバリゼーション](../wpf/advanced/globalization-for-wpf.md)
