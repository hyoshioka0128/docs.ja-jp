---
title: レコード長が正しくありません。
ms.date: 07/20/2015
f1_keywords:
- vbrID59
ms.assetid: 0926a3a4-177b-4452-9b33-d8a01e24cc21
ms.openlocfilehash: 7ec0a8c27f425ec717bca5d45d5dfd2b601c11d5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665736"
---
# <a name="bad-record-length"></a>レコード長が正しくありません。
このエラーでは以下の原因が考えられます。  
  
- `FileGet`、`FileGetObject`、`FilePut`、または `FilePutObject` ステートメントに指定されたレコード変数の長さが、対応する `FileOpen` ステートメントに指定された長さと異なります。  
  
- `FilePut` または `FilePutObject` ステートメント内の変数は、可変長文字列であるか、またはそれを含んでいます。  
  
- `FilePut` または `FilePutObject` 内の変数は、`Variant` 型であるか、またはそれを含んでいます。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. レコード変数の型を定義しているユーザー定義型の固定長変数のサイズの合計が、`FileOpen` ステートメントの `Len` 句に記述されている値と同じであることを確認してください。  
  
2. `FilePut` または `FilePutObject` ステートメント内の変数が、可変長文字列であるか、またはそれを含んでいる場合、可変長文字列が `FileOpen` ステートメントの `Len` 句に指定されているレコード長よりも少なくとも 2 文字短いことを確認してください。  
  
3. `FilePut` または `FilePutObject` 内の変数が `Variant` であるか、またはそれを含んでいる場合、可変長文字列が、`FileOpen` ステートメントの `Len` 句に指定されているレコード長よりも少なくとも 4 バイト短いことを確認してください。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.FileSystem.FileGet%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FileGetObject%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FilePut%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FilePutObject%2A>
