---
ms.openlocfilehash: 04c4fb4c8e9da8c58a5e26f78a7b13aa6a0df4a0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614685"
---
### <a name="changes-in-path-normalization"></a>パスの正規化の変更

#### <a name="details"></a>説明

.NET Framework 4.6.2 を対象とするアプリより、ランタイムによってパスを正規化する方法が変わりました。パスの正規化では、パスまたはファイルを識別する文字列を変更し、対象のオペレーティング システムの有効なパスに準拠するようにします。 通常、正規化では次のことを行います。

- コンポーネントとディレクトリの区切り記号を正規化する。
- 現在のディレクトリを相対パスに適用する。
- パスの相対ディレクトリ (.) または親ディレクトリ (..) を評価する。
- 指定した文字をトリミングする。
.NET Framework 4.6.2 を対象とするアプリより、パス正規化の次の変更が既定で有効になっています。
  - ランタイムはオペレーティング システムの [GetFullPathName](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamew) 関数に従って、パスを正規化します。
- 正規化では、ディレクトリ セグメントの末尾 (ディレクトリ名の末尾のスペースなど) がトリミングされなくなりました。
- `\\.\` や `\\?\` (mscorlib.dll のファイル I/O API の場合) を含む、完全に信頼できるデバイス パス構文がサポートされます。
- ランタイムではデバイス構文パスは検証されません。
- 代替データ ストリームにアクセスするためのデバイス構文の使用はサポートされています。
これらの変更でパフォーマンスが向上すると同時に、以前はアクセス不可だったパスにメソッドでアクセスできるようになります。 .NET Framework 4.6.1 以前のバージョンを対象とするアプリが .NET Framework 4.6.2 以降で実行される場合、この変更の影響は受けません。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.6.2 以降を対象とするアプリの場合、アプリケーション構成ファイルの `<runtime>` セクションに次の行を追加することでこの変更を無効にし、従来の正規化を使用できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />
</runtime>
```

.NET Framework 4.6.1 以前を対象とするが、.NET Framework 4.6.2 以降で実行されるアプリの場合、アプリケーション構成ファイルの `<runtime>` セクションに次の行を追加することで、パス正規化の変更を有効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |
