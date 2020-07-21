---
ms.openlocfilehash: b861dbaa02c97a03c015fdf4e63d25c40c90ea0a
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721460"
---
### <a name="boolean-parameter-of-signedcmscomputesignature-is-respected"></a>SignedCms.ComputeSignature のブール型パラメーターの尊重

.NET Core では、<xref:System.Security.Cryptography.Pkcs.SignedCms.ComputeSignature(System.Security.Cryptography.Pkcs.CmsSigner,System.Boolean)?displayProperty=nameWithType> メソッドのブール型の `silent` パラメーターが尊重されます。 このパラメーターが `true` に設定されている場合、PIN プロンプトは表示されません。

#### <a name="change-description"></a>変更の説明

.NET Framework では、<xref:System.Security.Cryptography.Pkcs.SignedCms.ComputeSignature(System.Security.Cryptography.Pkcs.CmsSigner,System.Boolean)?displayProperty=nameWithType> メソッドの `silent` パラメーターは無視され、プロバイダーから要求された場合は常に PIN プロンプトが表示されます。 .NET Core では、`silent` パラメーターが尊重されます。`true` に設定すると、プロバイダーから要求される場合でも PIN プロンプトは表示されません。

.NET Core のバージョン 2.1 では、CMS/PKCS #7 メッセージのサポートが導入されました。

#### <a name="version-introduced"></a>導入されたバージョン

2.1

#### <a name="recommended-action"></a>推奨アクション

必要に応じて PIN プロンプトが表示されるようにするには、デスクトップ アプリケーションで <xref:System.Security.Cryptography.Pkcs.SignedCms.ComputeSignature(System.Security.Cryptography.Pkcs.CmsSigner,System.Boolean)?displayProperty=nameWithType> を呼び出し、ブール型パラメーターを `false` に設定する必要があります。 結果の動作は、サイレント コンテキストが無効かどうかに関係なく .NET Framework と同じになります。

#### <a name="category"></a>カテゴリ

暗号

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.Pkcs.SignedCms.ComputeSignature(System.Security.Cryptography.Pkcs.CmsSigner,System.Boolean)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Security.Cryptography.Pkcs.SignedCms.ComputeSignature(System.Security.Cryptography.Pkcs.CmsSigner,System.Boolean)`

-->
