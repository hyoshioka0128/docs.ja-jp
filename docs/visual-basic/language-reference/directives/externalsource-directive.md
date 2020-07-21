---
title: '#ExternalSource ディレクティブ'
ms.date: 07/20/2015
f1_keywords:
- '#Externalsource'
- '#ExternalSource'
- vb.ExternalSource
- Externalsource
- vb.#ExternalSource
- ExternalSource
helpviewer_keywords:
- ExternalSource directive (#ExternalSource)
- '#ExternalSource directive'
ms.assetid: 243bc6a2-34c3-4eeb-a776-9fd2bf988149
ms.openlocfilehash: e4c7704c32c3a6c73e069d0b7129d5386696b438
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402993"
---
# <a name="externalsource-directive"></a>#ExternalSource ディレクティブ

ソース コードの特定の行と、ソースの外部のテキストとの間のマッピングを示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
#ExternalSource( StringLiteral , IntLiteral )  
    [ LogicalLine+ ]  
#End ExternalSource  
```  
  
## <a name="parts"></a>指定項目  

 `StringLiteral`  
 外部ソースへのパスです。  
  
 `IntLiteral`  
 外部ソースの最初の行の行番号です。  
  
 `LogicalLine`  
 外部ソースでエラーが発生した行です。  
  
 `#End ExternalSource`  
 `#ExternalSource` ブロックを終了します。  
  
## <a name="remarks"></a>Remarks  

 このディレクティブは、コンパイラとデバッガーによってのみ使用されます。  
  
 ソース ファイルには、外部ソース ディレクティブを含めることができます。これは、ソース ファイル内の特定のコード行と、.aspx ファイルなどのソースの外部のテキストとの間のマッピングを示します。 コンパイル時に指定されたソース コードでエラーが発生した場合、外部ソースからのものとして識別されます。  
  
 外部ソース ディレクティブはコンパイルには影響しません。また、入れ子にすることはできません。 これらはアプリケーションによる内部使用のみを目的としています。  
  
## <a name="see-also"></a>関連項目

- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
