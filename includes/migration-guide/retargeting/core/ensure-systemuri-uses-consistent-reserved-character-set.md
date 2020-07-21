---
ms.openlocfilehash: 21921156295d89aad04f3197fef9fa322f3c8c87
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614661"
---
### <a name="ensure-systemuri-uses-a-consistent-reserved-character-set"></a>System.Uri で一貫した予約文字セットが確実に使用されるようになった

#### <a name="details"></a>説明

<xref:System.Uri?displayProperty=fullName> では、場合によってはデコードされていたパーセントでエンコードされた特定の文字の状態が常に保たれるようになりました。 これは、URI のパス、クエリ、フラグメント、ユーザー情報コンポーネントにアクセスするプロパティやメソッド全体に適用されます。 以下の両方に該当する場合にのみ、動作が変わります。

- `:`、`'`、`(`、`)`、`!`、`*` のいずれかの予約文字のエンコードされたフォームが URI に含まれている。
- Unicode またはエンコードの予約されていない文字が URI に含まれている。 上記の両方に該当する場合、エンコードの予約文字はエンコードされたままです。 以前のバージョンの .NET Framework では、デコードされます。

#### <a name="suggestion"></a>提案される解決策

4\.7.2 以降のバージョンの .NET Framework を対象とするアプリケーションの場合は、新しいデコード動作が既定で有効になります。 この変更が望ましくない場合、アプリケーションの構成ファイルの `<runtime>` セクションに次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) スイッチを追加することで無効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets=true" />
</runtime>
```

以前のバージョンの .NET Framework を対象とするが、.NET Framework 4.7.2 以降のバージョンで実行するアプリケーションの場合、新しいデコード動作が既定で無効になります。 これを有効にするには、次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) スイッチをアプリケーション構成ファイルの `<runtime>` セクションに追加します。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets=false" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Uri?displayProperty=nameWithType>
