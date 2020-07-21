---
title: '@ (応答ファイルの指定)'
ms.date: 03/13/2018
helpviewer_keywords:
- '@ (Specify Response File) compiler option [Visual Basic]'
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
ms.openlocfilehash: 91cf1b5a55d16ab47a83fbd259dd1d83d8e9c31a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403097"
---
# <a name="-specify-response-file-visual-basic"></a>@ (応答ファイルの指定) (Visual Basic)

コンパイラ オプションおよびコンパイルするソース コード ファイルを含むファイルを指定します。

## <a name="syntax"></a>構文

```console
@response_file
```

## <a name="arguments"></a>引数

`response_file`  
必須です。 コンパイラ オプションやコンパイルするソース コード ファイルの一覧を含むファイルです。 ファイル名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。

## <a name="remarks"></a>Remarks

コンパイラでは、応答ファイルで指定されたコンパイラ オプションとソースコード ファイルが、コマンド ラインで指定した場合と同じように処理されます。

コンパイル時に複数の応答ファイルを指定するには、次のように複数の応答ファイル オプションを指定します。

```console
@file1.rsp @file2.rsp
```

応答ファイルでは、複数のコンパイラ オプションとソース コード ファイルを 1 行に表示されます。 1 つのコンパイラ オプションは 1 行に表示される必要があります (複数行にまたがることはできません)。 応答ファイルには、`#` 記号で始まるコメントを記述できます。

コマンド ラインで指定されたオプションと、1 つ以上の応答ファイルで指定されたオプションを組み合わせることができます。 コンパイラでは、検出した順にコマンド オプションが処理されます。 このため、コマンド ライン引数によって、応答ファイルで先に指定したオプションをオーバーライドできます。 反対に、応答ファイルのオプションにより、コマンド ラインや他の応答ファイルで先に指定したオプションがオーバーライドされることもあります。

Visual Basic では、Vbc.exe ファイルと同じディレクトリに Vbc.rsp ファイルが提供されます。 `-noconfig` オプションを使用しない限り、Vbc.rsp ファイルは既定で含まれます。 詳細については、「[-noconfig](noconfig.md)」を参照してください。

> [!NOTE]
> `@` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。

## <a name="example"></a>例

次の行は、サンプルの応答ファイルの一部です。

```console
# build the first output file
-target:exe
-out:MyExe.exe
source1.vb
source2.vb
```

## <a name="example"></a>例

次の例では、`@` オプションを `File1.rsp` という名前の応答ファイルと共に使用する方法を示します。

```console
vbc @file1.rsp
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-noconfig](noconfig.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
