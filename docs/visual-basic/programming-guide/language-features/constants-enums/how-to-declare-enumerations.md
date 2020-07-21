---
title: '方法: 列挙型を宣言する'
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- enumerations [Visual Basic], declaring
- declaring enumerations [Visual Basic]
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
ms.openlocfilehash: c8f228c205c93adf7f2f555dc840a7daac61950b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414454"
---
# <a name="how-to-declare-enumerations-visual-basic"></a>方法: 列挙型を宣言する (Visual Basic)
列挙型は、クラスまたはモジュールの宣言セクションで `Enum` ステートメントを使用して作成します。 メソッド内で列挙型を宣言することはできません。 `Private`、`Protected`、`Friend`、`Public` のいずれかを使用して、適切なアクセス レベルを指定します。  
  
 `Enum` 型には、名前、基になる型、フィールド一式を、それぞれ定数で指定します。 名前は、有効な Visual Basic .NET 修飾子である必要があります。 基になる型は、いずれかの整数型 (`Byte`、`Short`、`Long` または `Integer`) である必要があります。 `Integer` が既定値です。 列挙型の型指定は常に厳密であり、整数型との互換性はありません。  
  
 列挙型に浮動小数点値を指定することはできません。 `Option Strict On` を指定して列挙型に浮動小数点値を割り当てた場合、コンパイラ エラーが発生します。 `Option Strict` に `Off` を指定した場合は、値は自動的に `Enum` 型に変換されます。  
  
 名前、および `Imports` ステートメントにより名前の修飾を不要にする方法については、[列挙型と名前の修飾](enumerations-and-name-qualification.md)に関するページを参照してください。  
  
### <a name="to-declare-an-enumeration"></a>列挙型を宣言するには  
  
1. 次の例に示すように、コード アクセス レベル、`Enum` キーワード、有効な名前を含む宣言を記述し、それぞれで異なる `Enum` を宣言します。  
  
     [!code-vb[VbEnumsTask#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#3)]  
  
2. 列挙型の定数を定義します。 既定では、列挙型の最初の定数は `0` に初期化され、以降の定数は前の定数より 1 大きい値に初期化されます。 たとえば、次の列挙型 `Days` では、`Sunday` という定数の値は `0`、`Monday` という定数の値は `1`、`Tuesday` という定数の値は `2` のようになります。  
  
     [!code-vb[VbEnumsTask#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#4)]  
  
3. 代入ステートメントを使用することで、列挙型の定数に値を明示的に割り当てることができます。 負の数値を含む任意の整数値を割り当てられます。 たとえば、エラー状態を示す 0 未満の値を定数に設定できます。 次の列挙型では、定数 `Invalid` に値 `–1` を、定数 `Sunday` に値 `0` を明示的に割り当てています。 `Saturday` は列挙型の最初の定数であるため、これも値 `0` に初期化されます。 `Monday` の値は (`Sunday` の値より 1 大きい) `1`、`Tuesday` の値は `2` のようになります。  
  
     [!code-vb[VbEnumsTask#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#5)]  
  
### <a name="to-declare-an-enumeration-as-an-explicit-type"></a>明示的な型として列挙型を宣言するには  
  
- 列挙型の型は、次の例に示すように `As` 句を使用して指定します。  
  
     [!code-vb[VbEnumsTask#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [方法: Visual Basic で列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [方法: 列挙値に関連付けられている文字列を確認する](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)
- [定数の概要](constants-overview.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
