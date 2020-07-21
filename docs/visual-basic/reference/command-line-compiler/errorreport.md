---
title: -errorreport
ms.date: 08/14/2018
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
ms.openlocfilehash: b6a1c8fce17e3e5a54366c2ff4dff4e6aa668f56
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408661"
---
# <a name="-errorreport"></a>-errorreport

Visual Basic コンパイラで内部コンパイラ エラーを報告する方法を指定します。

## <a name="syntax"></a>構文

```console
-errorreport:{ prompt | queue | send | none }
```

## <a name="remarks"></a>Remarks

このオプションでは、Microsoft の Visual Basic チームに Visual Basic 内部コンパイラ エラー (ICE) を報告する便利な方法が提供されます。 既定では、コンパイラによって Microsoft に情報が送信されることはありません。 ただし、このオプションを使用すると、内部コンパイラ エラーが発生した場合に、エラーを Microsoft に報告することができます。 その情報は、Microsoft のエンジニアが原因を特定するのに役立ちます。また、Visual Basic の次のリリースの向上に役立つ場合があります。

マシンまたはユーザー ポリシーによるアクセス許可によっては、レポートを送信できない場合があります。

次の表に、`-errorreport` オプションの結果をまとめています。

|オプション|動作|
|---|---|
|`prompt`|内部コンパイラ エラーが発生すると、コンパイラによって収集された正確なデータを表示するためのダイアログ ボックスが表示されます。 エラー レポートに機密情報が含まれているかどうかを確認し、Microsoft に送信するかどうかを決定することができます。 送信する場合、マシンとユーザーのポリシー設定でそれが許可されていれば、コンパイラによってデータが Microsoft に送信されます。|
|`queue`|エラー レポートを待ち行列に入れます。 管理者特権でログインすると、最後にログインした後に発生したすべてのエラーを報告することができます (エラーの報告を 3 日ごとに複数回送信するように求めるメッセージは表示されません)。 `-errorreport` オプションが指定されていない場合は、これが既定の動作です。|
|`send`|内部コンパイラ エラーが発生した場合、マシンとユーザーのポリシー設定で許可されていれば、コンパイラによってデータが Microsoft に送信されます。<br /><br /> オプション `-errorreport:send` では、[Windows エラー報告](/windows/desktop/wer/windows-error-reporting)システム設定でレポートが有効になっている場合、Microsoft にエラー情報を自動的に送信するよう試みられます。 |
|`none`|内部コンパイラ エラーが発生すると、そのエラーは収集されず、Microsoft に送信されません。|

コンパイラによって、エラー発生時にスタックを含むデータが送信されます。これには通常、いくつかのソース コードが含まれています。 `-errorreport` を [-bugreport](bugreport.md) オプションと共に使用すると、ソース ファイル全体が送信されます。

Microsoft のエンジニアがエラーをより簡単に再現できるようになるため、このオプションを [-bugreport](bugreport.md) オプションと共に使用することをお勧めします。

> [!NOTE]
> `-errorreport` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。

## <a name="example"></a>例

次のコードでは、`T2.vb` のコンパイルが試行されます。コンパイラで内部コンパイラ エラーが発生した場合は、Microsoft にエラー レポートを送信するように求められます。

```console
vbc -errorreport:prompt t2.vb
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [-bugreport](bugreport.md)
