---
ms.openlocfilehash: 53d74db1a77e62cc64250658281fd3e4706fe494
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614636"
---
### <a name="allow-unicode-bidirectional-control-characters-in-uris"></a>URI での Unicode の双方向制御文字の許可

#### <a name="details"></a>説明

Unicode では、テキストの方向を指定するために使用される特殊な制御文字をいくつか指定します。 以前のバージョンの .NET Framework では、これらの文字は、パーセントでエンコードされたフォームに存在する場合でも、すべての URI から正しく削除されませんでした。 [RFC 3987](https://tools.ietf.org/html/rfc3987) により適切に従うために、これらの文字を URI で使用できるようにしました。 これらの文字は、URI でエンコードされていないことがわかった場合、パーセントでエンコードされます。 パーセントでエンコードされていることがわかった場合は、そのままです。

#### <a name="suggestion"></a>提案される解決策

4\.7.2 以降のバージョンの .NET Framework を対象とするアプリケーションの場合は、Unicode の双方向文字のサポートが既定で有効になります。 この変更が望ましくない場合、アプリケーションの構成ファイルの `<runtime>` セクションに次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) スイッチを追加することで無効にできます。

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.Uri.DontKeepUnicodeBidiFormattingCharacters=true" />
</runtime>
```

以前のバージョンの .NET Framework を対象とするが、.NET Framework 4.7.2 以降のバージョンで実行するアプリケーションの場合、Unicode の双方向文字のサポートが既定で無効になります。 アプリケーションの構成ファイルの `<runtime>` セクションに次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) スイッチを追加することで有効にできます。

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.Uri.DontKeepUnicodeBidiFormattingCharacters=false" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Uri?displayProperty=nameWithType>
