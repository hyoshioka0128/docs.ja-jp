---
ms.openlocfilehash: 09027863ff2f0009a14578db35db870c27369726
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721227"
---
### <a name="types-in-microsoftvisualbasicapplicationservices-namespace-not-available"></a>Microsoft.VisualBasic.ApplicationServices 名前空間の型は使用できません

<xref:Microsoft.VisualBasic.ApplicationServices?displayProperty=fullName> 名前空間の型は使用できません。

#### <a name="version-introduced"></a>導入されたバージョン

.NET Core 3.0 Preview 8

#### <a name="change-description"></a>変更の説明

<xref:Microsoft.VisualBasic.ApplicationServices?displayProperty=fullName> 名前空間の型は、一部の .NET Core 3.0 プレビュー リリースで使用できました。 それらは、.NET Core 3.0 Preview 9 以降では使用できなくなりました。

これらの型は、今後のリリースでの不要なアセンブリの依存関係や破壊的変更を回避するために削除されました。

#### <a name="recommended-action"></a>推奨アクション

コードが <xref:Microsoft.VisualBasic.ApplicationServices> 型とそのメンバーの使用に依存している場合は、.NET クラス ライブラリ内の対応する型またはメンバーを使用できる可能性があります。 たとえば、一部の <xref:System.Environment?displayProperty=nameWithType> および <xref:System.Security.Principal.WindowsIdentity?displayProperty=nameWithType> メンバーには、<xref:Microsoft.VisualBasic.ApplicationServices.User?displayProperty=nameWithType> クラスのプロパティと同等の機能が用意されています。

#### <a name="category"></a>カテゴリ

Visual Basic

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.VisualBasic.ApplicationServices?displayProperty=fullName>

<!--

#### Affected APIs

- `N:Microsoft.VisualBasic.ApplicationServices`

-->
