---
title: Auto
ms.date: 07/20/2015
f1_keywords:
- vb.Auto
helpviewer_keywords:
- Auto keyword [Visual Basic], external references
- Declare statement [Visual Basic], marshaling strings
- Auto keyword [Visual Basic]
- Auto keyword [Visual Basic], marshaling strings
ms.assetid: bf79ba95-a62c-48a5-916f-0ac7a52c13ec
ms.openlocfilehash: b9bdeed55788252c71b8fb1c995c140cbfdf60eb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373129"
---
# <a name="auto-visual-basic"></a>Auto (Visual Basic)
Visual Basic で、宣言されている外部プロシージャの外部名に基づいて、.NET Framework ルールに従い、文字列をマーシャリングする必要があることを指定します。  
  
 プロジェクトの外部で定義されたプロシージャを呼び出すと、Visual Basic コンパイラが、プロシージャを正しく呼び出すために必要な情報にアクセスできません。 この情報には、プロシージャの配置場所、識別方法、呼び出し元のシーケンスと戻り値の型、および使用されている文字列の文字セットが含まれます。 [Declare ステートメント](../statements/declare-statement.md)は、外部プロシージャへの参照を作成し、この必要な情報を提供します。  
  
 `Declare` ステートメントの `charsetmodifier` 部分では、外部プロシージャの呼び出し時に、文字列をマーシャリングするための文字セット情報を指定します。 これは、Visual Basic が外部ファイルで外部プロシージャ名を検索する方法にも影響します。 `Auto` 修飾子は、Visual Basic が .NET Framework の規則に従って文字列をマーシャリングし、実行時プラットフォームの基本文字セットを決定して、最初の検索が失敗した場合には外部プロシージャ名を変更する可能性があることを指定します。 詳細については、「[Declare ステートメント](../statements/declare-statement.md)」の「文字セット」を参照してください。  
  
 文字セット修飾子が指定されていない場合は、`Ansi` が既定値になります。  
  
## <a name="remarks"></a>Remarks  
 `Auto` 修飾子は、次のコンテキストで使用できます。  
  
 [Declare ステートメント](../statements/declare-statement.md)  
  
## <a name="smart-device-developer-notes"></a>スマート デバイス開発者向けのメモ  
 このキーワードはサポートされていません。  
  
## <a name="see-also"></a>関連項目

- [Ansi](ansi.md)
- [Unicode](unicode.md)
- [キーワード](../keywords/index.md)
