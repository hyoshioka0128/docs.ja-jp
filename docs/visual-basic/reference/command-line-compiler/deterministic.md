---
title: -deterministic
ms.date: 04/11/2018
helpviewer_keywords:
- deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
ms.openlocfilehash: 0cf9aceef54998f269e9e377fe5d0a48492969c0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408687"
---
# <a name="-deterministic"></a>-deterministic

同一の入力に対して、バイト単位の出力がコンパイル全体で同一のアセンブリをコンパイラに生成させます。

## <a name="syntax"></a>構文

```console
-deterministic
```

## <a name="remarks"></a>Remarks

既定では、コンパイラはタイムスタンプと乱数から生成された GUID を追加するため、指定した入力のセットからのコンパイラの出力は固有になります。 `-deterministic` オプションを使用して、*決定論的アセンブリ*を生成します。そのバイナリ コンテンツは、入力が同じである限り、コンパイル全体で同一になります。

コンパイラでは決定性のために次の入力が考慮されます。

- コマンド ライン パラメーターのシーケンス。
- コンパイラの .rsp 応答ファイルの内容。
- 使用されるコンパイラの正確なバージョン、およびその参照先のアセンブリ。
- 現在のディレクトリ パス。
- すべてのファイルのバイナリ コンテンツは、以下を含めて、直接または間接のいずれかでコンパイラに明示的に渡されます。
  - ソース ファイル
  - 参照アセンブリ
  - 参照モジュール
  - リソース
  - 厳密な名前のキー ファイル
  - @ 応答ファイル
  - アナライザー
  - ルールセット
  - アナライザーによって使用される可能性がある追加のファイル
- 現在のカルチャ (診断と例外メッセージが生成される言語)。
- エンコードが指定されていない場合の既定のエンコード (または現在のコード ページ)。
- コンパイラの検索パス上のファイルの有無、および内容 (たとえば、`-lib` や `-recurse` で指定)。
- コンパイラが実行される CLR プラットフォーム。
- `%LIBPATH%` の値。アナライザーの依存関係の読み込みに影響する場合があります。

ソースを公開用に利用できる場合、バイナリが信頼できる発行元からコンパイルされているかどうかを確立するために、決定論的コンパイルを使用できます。 これは、バイナリへの変更に依存しているビルド ステップを実行する必要があるかどうかを決定するために、継続的なビルド システムで役立つ場合もあります。

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
