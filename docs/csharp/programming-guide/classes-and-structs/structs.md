---
title: 構造体 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, structs
- structs [C#]
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
ms.openlocfilehash: df2a235651a2242ffe18df377dce9995af31e99f
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392450"
---
# <a name="structs-c-programming-guide"></a>構造体 (C# プログラミング ガイド)

構造体は [struct](../../language-reference/keywords/struct.md) キーワードを使って定義します。次はその例です。  
  
 [!code-csharp[csProgGuideObjects#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#39)]  
  
構造体の構文はクラスとほとんど同じです。 構造体の名前を、有効な C# の[識別子名](../inside-a-program/identifier-names.md)にする必要があります。 構造体は次の点でクラスよりも制限されています。  
  
- 構造体宣言内では、const または static と宣言されているフィールド以外は初期化できません。  
- 構造体では、パラメーターなしのコンストラクター (パラメーターを伴わないコンストラクター) やファイナライザーを宣言できません。  
- 構造体は、割り当て時にコピーされます。 構造体を新しい変数に割り当てると、すべてのデータがコピーされ、新しいコピーを変更しても、元のコピーのデータは変更されません。 これは、`Dictionary<string, myStruct>` などの値の型のコレクションを使用する際に重要です。  
- 参照型であるクラスとは異なり、構造体は値型です。  
- クラスとは異なり、構造体は `new` 演算子を使用せずにインスタンス化できます。  
- 構造体は、パラメーターのあるコンストラクターを宣言できます。
- 構造体は、他の構造体やクラスから継承できず、基本クラスになることはできません。 すべての構造体が <xref:System.ValueType> を直接継承し、System.ValueType は <xref:System.Object> を継承します。  
- 構造体は、インターフェイスを実装できます。
- 構造体は `null` にすることができません。変数が null 許容値型として宣言されない限り、構造体変数に `null` を割り当てることはできません。
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [クラスと構造体](index.md)
- [クラス](classes.md)
- [null 許容値型](../nullable-types/index.md)
- [識別子名](../inside-a-program/identifier-names.md)
- [構造体の使用](using-structs.md)
- [方法: メソッドに構造体を渡すこととクラス参照を渡すことの違いを理解する](how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)
