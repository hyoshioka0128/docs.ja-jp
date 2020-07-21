---
title: 列挙型を使用する状況
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
ms.openlocfilehash: ba69249e16b8c0ee06d57d06d192874a283b295e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403538"
---
# <a name="when-to-use-an-enumeration-visual-basic"></a>列挙型を使用する状況 (Visual Basic)
列挙型を使用すると、一連の関連する定数を簡単に操作できます。 列挙型 (`Enum`) は、一連の値のシンボリック名です。 列挙型はデータ型扱いであり、これを使用することで、変数やプロパティと共に使用する一連の定数を作成することができます。  
  
## <a name="when-to-use-an-enumeration"></a>列挙型を使用する状況  
 プロシージャで受け取れる変数の個数が限られている場合には、必ず列挙型の使用を検討してください。 列挙型を使用すると、コードの明瞭さと読みやすさが増します。わかりやすい名前を使用すると特に効果的です。  
  
 列挙型を使用する利点は次のとおりです。  
  
- 数の入れ替えや入力間違いによるエラーを減らせます。  
  
- 値を後で変更しやすくなります。  
  
- コードが読みやすくなり、コードにエラーが紛れ込む可能性を抑えられます。  
  
- 上位互換性を確保できます。 列挙型を使用すると、今後メンバー名に対応する値が変更された場合に、コードでエラーが発生する確率が小さくなります。  
  
## <a name="naming-enumerations"></a>列挙型に名前を付ける  
 列挙型メンバーにはなんらかの名前付け規則を適用してください。 Visual Basic で列挙型メンバーを検出した場合、参照対象の別の型ライブラリに同じ名前が含まれていると、例外がスローされます。 アプリケーションまたはコンポーネントの値を特定できる、一意の接頭辞を使用してください。  
  
 列挙型のメンバーを参照する場合は、列挙型名でメンバー名を修飾するか、`Imports` ステートメントを使用する必要があります。 詳細については、[列挙型と名前の修飾](enumerations-and-name-qualification.md)に関するページを参照してください。  
  
## <a name="predefined-enumerations"></a>定義済みの列挙型  
 Visual Basic には、コードを作成しやすいように定義済みの列挙型が多数用意されています (`FirstDayOfWeek` や `MsgBoxResult` など)。 これらの一覧については、[定数と列挙型](../../../language-reference/constants-and-enumerations.md)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [方法: 列挙型のメンバーを参照する](how-to-refer-to-an-enumeration-member.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [方法: Visual Basic で列挙型を反復処理する](how-to-iterate-through-an-enumeration.md)
- [方法: 列挙値に関連付けられている文字列を確認する](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [Enum ステートメント](../../../language-reference/statements/enum-statement.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
