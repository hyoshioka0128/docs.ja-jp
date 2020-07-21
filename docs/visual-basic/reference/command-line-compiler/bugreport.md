---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 02d84bceb0242988c70889ddd5d3dc7530f6e808
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793546"
---
# <a name="-bugreport"></a>-bugreport

バグ レポートを提出するときに使用できるファイルを作成します。

## <a name="syntax"></a>構文

```console
-bugreport:file
```

## <a name="arguments"></a>引数

|用語|定義|
|---|---|
|`file`|必須です。 バグ レポートが含まれるファイルの名前。 ファイル名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。|

## <a name="remarks"></a>Remarks

`file` に次の情報が追加されます。

- コンパイル時のすべてのソースコード ファイルのコピー。

- コンパイルで使用されたコンパイラ オプションの一覧。

- コンパイラ、共通言語ランタイム、およびオペレーティング システムに関するバージョン情報。

- コンパイラの出力 (指定されている場合)。

- 問題の説明。プロンプトが表示されます。

- 問題の修正方法についての説明。プロンプトが表示されます。

すべてのソースコード ファイルのコピーが `file` に含まれるため、できるだけ短いプログラムで (疑わしい) コードの欠陥を再現することをお勧めします。

> [!IMPORTANT]
> `-bugreport` オプションを指定すると、機密情報が含まれる可能性のあるファイルが生成されます。 これには、現在の時刻、コンパイラ バージョン、.NET Framework バージョン、OS バージョン、ユーザー名、コンパイラが実行されたときのコマンドライン引数、すべてのソース コード、および参照アセンブリのバイナリ形式が含まれます。 このオプションには、Web.config ファイルで ASP.NET アプリケーションのサーバー側コンパイルのコマンドライン オプションを指定することでアクセスできます。 これを回避するには、Machine.config ファイルを変更して、ユーザーがサーバーでコンパイルできないようにします。

このオプションが `-errorreport:prompt`、`-errorreport:queue`、または `-errorreport:send` と共に使用され、アプリケーションで内部コンパイラ エラーが発生した場合、`file` 内の情報が Microsoft Corporation に送信されます。 その情報は、Microsoft のエンジニアがエラーの原因を特定するのに役立ちます。また、Visual Basic の次のリリースの向上に役立つ場合があります。 既定では、情報は Microsoft に送信されません。 しかし、既定で有効になっている `-errorreport:queue` を使用して、アプリケーションをコンパイルすると、アプリケーションによってそのエラー レポートが収集されます。 その後、コンピューターの管理者がログインすると、エラー レポート システムにポップアップ ウィンドウが表示され、ログオン後に発生したエラー レポートを管理者が Microsoft に転送できるようになります。

> [!NOTE]
> `-bugreport` オプションは、Visual Studio 開発環境内からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。

## <a name="example"></a>例

次の例では、*T2.vb* をコンパイルし、すべてのバグ レポート情報を *Problem.txt* ファイルに配置します。

```console
vbc -bugreport:problem.txt t2.vb
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-debug (Visual Basic)](debug.md)
- [-errorreport](errorreport.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [securityPolicy の trustLevel 要素 (ASP.NET 設定スキーマ)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
