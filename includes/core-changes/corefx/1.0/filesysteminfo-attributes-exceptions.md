---
ms.openlocfilehash: 2ea9abca7578c2ddf92712a1c597f8f1ff4a5c0c
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021820"
---
### <a name="unauthorizedaccessexception-thrown-by-filesysteminfoattributes"></a>FileSystemInfo.Attributes によってスローされる UnauthorizedAccessException

.NET Core では、呼び出し元がファイル属性値を設定しようとして、書き込みアクセス許可がない場合、<xref:System.UnauthorizedAccessException> がスローされます。

#### <a name="change-description"></a>変更の説明

.NET Framework では、呼び出し元が <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType> でファイル属性値を設定しようとして、書き込みアクセス許可がない場合、<xref:System.ArgumentException> がスローされます。 .NET Core では、代わりに <xref:System.UnauthorizedAccessException> がスローされます (.NET Core では、呼び出し元が無効なファイル属性を設定しようとした場合でも <xref:System.ArgumentException> がスローされます)。

#### <a name="version-introduced"></a>導入されたバージョン

1

#### <a name="recommended-action"></a>推奨アクション

必要に応じて、<xref:System.ArgumentException> の代わりに、または追加として、<xref:System.UnauthorizedAccessException> をキャッチするように `catch` ステートメントを変更します。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.IO.FileSystemInfo.Attributes`

-->
