---
title: 属性リスト
ms.date: 07/20/2015
helpviewer_keywords:
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
ms.openlocfilehash: f2400334182d373ea49c130fd17bc4f9943248d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408446"
---
# <a name="attribute-list-visual-basic"></a>属性リスト (Visual Basic)
宣言されたプログラミング要素に適用する属性を指定します。 複数の属性を指定するときは、コンマで区切ります。 次に 1 つの属性の構文を示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a>指定項目  
|||
|---|---|
|`attributemodifier`|ソース ファイルの先頭で適用される属性の場合は必須です。 [Assembly](../modifiers/assembly.md) または [Module](../modifiers/module-keyword.md) を指定できます。|
|`attributename`| 必須です。 属性の名前。|
|`attributearguments`|任意。 この属性の位置引数の一覧です。 複数の引数はコンマで区切ります。|
|`attributeinitializer`|任意。 この属性の変数またはプロパティ初期化子の一覧です。 複数の初期化子を指定するときは、コンマで区切ります。|
  
## <a name="remarks"></a>Remarks  
 1 つまたは複数の属性を、ほぼすべてのプログラミング要素 (型、プロシージャ、プロパティなど) に適用できます。 属性は、アセンブリのメタデータに指定され、コードに注釈を付けたり、特定のプログラミング要素の使用方法を指定したりするのに役立ちます。 Visual Basic と .NET Framework で定義された属性を適用したり、独自の属性を定義したりできます。  

 属性を使用するタイミングの詳細については、[属性の概要](../../programming-guide/concepts/attributes/index.md)に関するページを参照してください。 属性名については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。  
  
## <a name="rules"></a>ルール  
  
- **配置。** ほとんどの宣言されたプログラミング要素に属性を適用できます。 1 つまたは複数の属性を適用するには、要素宣言の先頭に*属性ブロック*を配置します。 属性リストの各エントリは、適用する属性、および属性のこの呼び出しに使用する修飾子と引数を指定します。  
  
- **山かっこ。** 属性リストを指定する場合は、山かっこ ("`<`" および "`>`") で囲む必要があります。  
  
- **宣言の一部。** 属性は、個別のステートメントではなく、要素宣言の一部である必要があります。 行連結シーケンス ("`_`") を使用して、宣言ステートメントを複数のソースコード行に拡張することができます。  
  
- **修飾子。** ソース ファイルの先頭でプログラミング要素に適用されるすべての属性に対して、属性修飾子 (`Assembly` または `Module`) が必要です。 ソース ファイルの先頭にない要素に適用される属性では、属性修飾子は使用できません。  
  
- **引数。** 属性のすべての位置引数は、変数またはプロパティ初期化子の前に記述する必要があります。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Runtime.InteropServices.DllImportAttribute> 属性を `Function` プロシージャのスケルトン定義に適用しています。  
  
 [!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute> は、属性付きプロシージャがアンマネージ ダイナミックリンク ライブラリ (DLL) のエントリ ポイントを表していることを示します。 属性は、DLL 名を位置引数として指定し、その他の情報を変数初期化子として指定しています。  
  
## <a name="see-also"></a>関連項目

- [Assembly](../modifiers/assembly.md)
- [Module \<keyword>](../modifiers/module-keyword.md)
- [属性の概要](../../programming-guide/concepts/attributes/index.md)
- [方法: コード内でステートメントを分割および連結する](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
