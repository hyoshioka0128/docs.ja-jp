---
title: -quiet
ms.date: 07/20/2015
f1_keywords:
- -quiet
- quiet
helpviewer_keywords:
- -quiet compiler option [Visual Basic]
- /quiet compiler option [Visual Basic]
- quiet compiler option [Visual Basic]
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
ms.openlocfilehash: f894ed6a778e026ffd3976a63fe3b677eb6a9557
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400527"
---
# <a name="-quiet"></a>-quiet

コンパイラで構文関連のエラーと警告のコードが表示されないようにします。

## <a name="syntax"></a>構文

```console
-quiet
```

## <a name="remarks"></a>Remarks

既定では、`-quiet` は無効です。 コンパイラで構文に関連するエラーまたは警告が報告されるときに、ソース コードの行も出力されます。 コンパイラの出力を解析するアプリケーションでは、コンパイラで診断テキストのみが出力される方が便利な場合があります。

次の例の `Module1` では、`-quiet` を使用せずにコンパイルされた場合に、ソース コードを含むエラーが出力されます。

```vb
Module Module1
    Sub Main()
        x()
    End Sub
End Module
```

Output:

```console
C:\projects\vb2.vb(3) : error BC30451: 'x' is not declared. It may be inaccessible due to its protection level.

        x()
        ~
```

`-quiet` を使用してコンパイルすると、コンパイラからは次のものだけが出力されます。

```console
E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.
```

> [!NOTE]
> `-quiet` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。

## <a name="example"></a>例

次のコードでは `T2.vb` がコンパイルされ、構文に関連するコンパイラ診断のコードが表示されません。

```console
vbc -quiet t2.vb
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
