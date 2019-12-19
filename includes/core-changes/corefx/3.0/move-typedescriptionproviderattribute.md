---
ms.openlocfilehash: 4d479636f41095610eaf39f92ad0dad4863ab8b5
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74568197"
---
### <a name="typedescriptionproviderattribute-moved-to-another-assembly"></a>TypeDescriptionProviderAttribute は別のアセンブリに移動されました

<xref:System.ComponentModel.TypeDescriptionProviderAttribute> クラスは異動されました。

#### <a name="change-description"></a>変更の説明

.NET Core 2.2 およびそれ以前のバージョンでは、<xref:System.ComponentModel.TypeDescriptionProviderAttribute> クラスは *System.ComponentModel.TypeConverter* アセンブリにあります。

.NET Core 3.0 以降では、*System.ObjectModel* アセンブリに含まれています。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨される操作

この変更によって影響を受けるのは、リフレクションを使用し、<xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> などのメソッドや、型が特定のアセンブリにあることを想定している <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> のオーバーロードを呼び出すことによって、<xref:System.ComponentModel.TypeDescriptionProviderAttribute> 型を読み込んでいるアプリケーションのみです。 これに該当する場合は、メソッドの呼び出しで参照されているアセンブリを、型の新しいアセンブリの場所を反映するように更新する必要があります。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- なし

<!--

### Affected APIs

- Not detectable via API analysis

-->
