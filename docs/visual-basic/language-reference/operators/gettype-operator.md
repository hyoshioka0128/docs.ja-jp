---
title: GetType Operator
ms.date: 07/20/2015
f1_keywords:
- vb.GetType
helpviewer_keywords:
- GetType operator [Visual Basic]
- GetType keyword [Visual Basic]
ms.assetid: 4f733297-2503-4607-850c-15eba65fff90
ms.openlocfilehash: 37644a9c37ffde084120c5f1e1ee8c87a04ffc3c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371156"
---
# <a name="gettype-operator-visual-basic"></a>GetType 演算子 (Visual Basic)
指定した型の <xref:System.Type> オブジェクトを返します。 <xref:System.Type> オブジェクトは、そのプロパティ、メソッド、イベントなど、型に関する情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```vb  
GetType(typename)  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---|---|  
|`typename`|情報を必要とする型の名前。|  
  
## <a name="remarks"></a>Remarks  
 `GetType` 演算子は、指定された `typename` の <xref:System.Type> オブジェクトを返します。 定義された型の名前を `typename` で渡すことができます。 次に例を示します。  
  
- Visual Basic の任意のデータ型 (`Boolean` や `Date` など)。  
  
- .NET Framework の任意のクラス、構造体、モジュール、インターフェイス (<xref:System.ArgumentException?displayProperty=nameWithType> や <xref:System.Double?displayProperty=nameWithType> など)。  
  
- アプリケーションで定義されている任意のクラス、構造体、モジュール、インターフェイス。  
  
- アプリケーションで定義されている任意の配列。  
  
- アプリケーションで定義されている任意のデリゲート。  
  
- Visual Basic、.NET Framework、お使いのアプリケーションによって定義された任意の列挙型。  
  
 オブジェクト変数の型オブジェクトを取得する場合は、<xref:System.Type.GetType%2A?displayProperty=nameWithType> メソッドを使用します。  
  
 `GetType` 演算子は、次のような場合に役立つことがあります。  
  
- 実行時に型のメタデータにアクセスする必要がある場合。 <xref:System.Type> オブジェクトは、型のメンバーやデプロイ情報などのメタデータを提供します。 これは、たとえば、アセンブリについて検討するときに必要になります。 詳細については、「<xref:System.Reflection?displayProperty=nameWithType>」を参照してください。  
  
- 2 つのオブジェクト参照を比較して、それらが同じ型のインスタンスを参照しているかどうかを確認する必要がある場合。 そうである場合、`GetType` は同じ <xref:System.Type> オブジェクトへの参照を返します。  
  
## <a name="example"></a>例  
 `GetType` 演算子の使用例を次に示します。  
  
 [!code-vb[VbVbalrOperators#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#26)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
