---
title: Xamarin の制限事項
ms.date: 12/13/2019
description: Xamarin の使用時に経験する制限事項について説明します。
ms.openlocfilehash: 192f25954726919dc66d706e755e0853404b4d85
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450406"
---
# <a name="xamarin-limitations"></a>Xamarin の制限事項

Microsoft.Data.Sqlite は .NET Standard 2.0 を対象とし、Xamarin でサポートされています。 次の表は、既定の SQLitePCLRaw バンドルによってネイティブ SQLite バイナリが提供されるプラットフォームを示しています。 別のバンドルを使用する場合、または独自のネイティブ SQLite バイナリを用意する場合の詳細については、「[カスタム SQLite のバージョン](custom-versions.md)」を参照してください。

| プラットフォーム | SQLite バイナリ |
| --- | --- |
| **Xamarin.Android** | — |
| &nbsp;&nbsp;&nbsp;&nbsp;`arm64-v8a` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`armeabi-v7a` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`x86` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`x86_64` | ✔ |
| **Xamarin.iOS** | ✔ |
| **Xamarin.Mac** | ✔ |
| **Xamarin.TVOS** | ✔ |
| **UWP** | — |
| &nbsp;&nbsp;&nbsp;&nbsp;`arm` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`arm64` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`x64` | ✔ |
| &nbsp;&nbsp;&nbsp;&nbsp;`x86` | ✔ |

## <a name="ios"></a>iOS

Microsoft.Data.Sqlite では、SQLitePCLRaw バンドルの初期化が自動的に試みられます。 しかし、Xamarin.iOS の事前 (AOT) コンパイルに制限があるため、この試みは失敗し、次のエラーが表示されます。

> `SQLitePCL.raw.SetProvider()` を呼び出す必要があります。(You need to call SQLitePCL.raw.SetProvider().) バンドル パッケージを使用している場合、これは `SQLitePCL.Batteries.Init()` を呼び出すことによって行われます。(If you're using a bundle package, this is done by calling SQLitePCL.Batteries.Init().)

バンドルを初期化するには、Microsoft. Data. Sqlite を使用する前に次のコード行をアプリに追加してください。

```csharp
SQLitePCL.Batteries_V2.Init();
```

## <a name="see-also"></a>関連項目

* [非同期の制限事項](async.md)
* [カスタム SQLite のバージョン](custom-versions.md)
