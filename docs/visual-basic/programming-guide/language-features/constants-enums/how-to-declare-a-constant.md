---
title: '方法: 定数を宣言する'
ms.date: 07/20/2015
f1_keywords:
- vb.constant
helpviewer_keywords:
- Integer data type [Visual Basic], declaring constants
- Single data type [Visual Basic], declaring constants
- Const statement [Visual Basic], declaring constants
- procedures [Visual Basic], declaration
- data types [Visual Basic], constants
- Long data type [Visual Basic], declaring constants
- Visual Basic code, declaring variables and constants
- Double data type [Visual Basic], declaring constants
- Boolean data type [Visual Basic], declaring constants
- modules, declaring constants
- Byte data type [Visual Basic], declaring constants
- constants [Visual Basic], declaring
- Date data type [Visual Basic], declaring constants
- String data type [Visual Basic], declaring constants
- declaring constants [Visual Basic], const keyword
- Currency data type [Visual Basic], declaring constants and variants
- module-level constants and variables
- Object data type [Visual Basic], declaring constants
ms.assetid: f901b4fa-481f-4621-822e-427060577ad1
ms.openlocfilehash: ffaa98f6af3d4b276f5c0b1153841acdea0809d7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414480"
---
# <a name="how-to-declare-a-constant-visual-basic"></a>方法: 定数を宣言する (Visual Basic)
定数とその値を宣言するには、`Const` ステートメントを使用します。 定数を宣言することで、値にわかりやすい名前を割り当てます。 宣言した定数を変更したり、新しい値を割り当てたりすることはできません。  
  
 定数の宣言は、プロシージャ内、またはモジュール、クラス、構造体の宣言セクション内で行います。 既定では、クラスレベルまたは構造体レベルの定数は `Private` になりますが、適切なコード アクセス レベルで `Public`、`Friend`、`Protected`、または `Protected Friend` として宣言することもできます。  
  
 定数には、有効なシンボリック名 (ルールは変数名を作成する場合のものと同じ)、および数値型または文字列型の定数と演算子 (関数呼び出し以外) で構成される式を指定する必要があります。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-declare-a-constant"></a>定数を宣言するには  
  
- 次の例のように、アクセス指定子、`Const` キーワード、式を含んだ宣言を記述します。  
  
     [!code-vb[VbEnumsTask#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#8)]  
  
     [Option Infer](../../../language-reference/statements/option-infer-statement.md) に `Off` を指定し、[Option Strict](../../../language-reference/statements/option-strict-statement.md) に `On` を指定した場合は、データ型 (`Boolean`、`Byte`、`Char`、`DateTime`、`Decimal`、`Double`、`Integer`、`Long`、`Short`、`Single`、または `String`) を指定して明示的に定数を宣言する必要があります。  
  
     `Option Infer` に `On` を指定するか、`Option Strict` に `Off` を指定している場合は、`As` 句でデータ型を指定することなく定数を宣言できます。 コンパイラは、式の型から定数の型を判断します。 詳細については、[定数とリテラルのデータ型](constant-and-literal-data-types.md)に関するページを参照してください。  
  
### <a name="to-declare-a-constant-that-has-an-explicitly-stated-data-type"></a>データ型を明記した定数を宣言するには  
  
- 次の例のように、`As` キーワードと明示的なデータ型を含む宣言を記述します。  
  
     [!code-vb[VbEnumsTask#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#9)]  
  
     1 行で複数の定数を宣言することはできますが、1 行に 1 つのみ定数を宣言した方がコードは読みやすくなります。 1 行で複数の定数を宣言する場合、すべてに同じアクセス レベルを設定する必要があります (`Public`、`Private`、`Friend`、`Protected`、または `Protected Friend`)。  
  
### <a name="to-declare-multiple-constants-on-a-single-line"></a>1 行で複数の定数を宣言するには  
  
- 次の例に示すように、各宣言をコンマと空白で区切ります。  
  
    ```vb  
    Public Const Four As Integer = 4, Five As Integer = 5, Six As Integer = 44  
    ```  
  
## <a name="see-also"></a>関連項目

- [Const ステートメント](../../../language-reference/statements/const-statement.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [定数の概要](constants-overview.md)
- [方法: 定数を宣言する](how-to-declare-a-constant.md)
- [ユーザー定義定数](user-defined-constants.md)
- [定数とリテラルのデータ型](constant-and-literal-data-types.md)
- [方法: 関連する定数値をまとめてグループ化する](how-to-group-related-constant-values-together.md)
- [列挙型の概要](enumerations-overview.md)
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: 列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [方法: 列挙値に関連付けられている文字列を確認する](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [列挙型を使用する状況](when-to-use-an-enumeration.md)

- [列挙型の概要](enumerations-overview.md)
- [定数の概要](constants-overview.md)
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
