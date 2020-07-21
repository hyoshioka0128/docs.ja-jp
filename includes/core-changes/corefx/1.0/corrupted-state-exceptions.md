---
ms.openlocfilehash: 394f2daebad7b6af94bee4d7876796e87fe8ab19
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135628"
---
### <a name="handling-corrupted-state-exceptions-is-not-supported"></a>破損状態例外の処理がサポートされない

.NET Core ではプロセス破損状態例外の処理はサポートされません。

#### <a name="change-description"></a>変更の説明

以前は、マネージド コード例外ハンドラーにより (たとえば、C# の [try-catch](../../../../docs/csharp/language-reference/keywords/try-catch.md) ステートメントを使用して)、プロセス破損状態例外をキャッチして処理することができました。

.NET Core 1.0 以降では、プロセス破損状態例外をマネージド コードで処理することはできません。 共通言語ランタイムでは、プロセス破損状態例外がマネージド コードに提供されません。

#### <a name="version-introduced"></a>導入されたバージョン

1

#### <a name="recommended-action"></a>推奨アクション

代わりに、そのような例外をもたらした状況に対処することで、プロセス破損状態例外を処理する必要がないようにします。 プロセス破損状態例外をどうしても処理する必要がある場合は、C または C++ のコードで例外ハンドラーを記述します。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=fullName>
- [legacyCorruptedStateExceptionsPolicy 要素](~/docs/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element.md)

<!--

#### Affected APIs

- `T:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute`

-->
