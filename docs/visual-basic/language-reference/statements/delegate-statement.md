---
title: Delegate ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Delegate
helpviewer_keywords:
- delegate keyword [Visual Basic]
- Delegate statement [Visual Basic]
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
ms.openlocfilehash: 8dec28620b0409f05007b2c0b1c1fd4494c2d7c8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404759"
---
# <a name="delegate-statement"></a>Delegate ステートメント
デリゲートの宣言に使用します。 デリゲートは、型の `Shared` メソッドまたはオブジェクトのインスタンス メソッドを参照する参照型です。 パラメーターおよび戻り値の型が一致するプロシージャを使用すると、このデリゲート クラスのインスタンスを作成できます。 このプロシージャは、後でデリゲート インスタンスを使用して呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```vb  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`attrlist`|任意。 このデリゲートに適用される属性の一覧です。 複数の属性を指定するときは、コンマで区切ります。 [属性リスト](attribute-list.md)は山かっこ ("`<`" および "`>`") で囲む必要があります。|  
|`accessmodifier`|任意。 どのようなコードからデリゲートにアクセスできるのかを指定します。 次のいずれかの値を指定します。<br /><br /> - [Public](../modifiers/public.md)。 このデリゲートを宣言している要素にアクセス可能なすべてのコードからアクセスできます。<br />-   [Protected](../modifiers/protected.md)。 デリゲートのクラスまたは派生クラス内のコードからのみアクセスできます。<br />-   [Friend](../modifiers/friend.md)。 デリゲートには同じアセンブリ内のコードからのみアクセスできます。<br />- [Private](../modifiers/private.md)。 このデリゲートを宣言している要素内のコードからのみアクセスできます。<br /><br /> - [Protected Friend](../modifiers/protected-friend.md) デリゲートのクラス、派生クラス、または同じアセンブリ内のコードからのみ、デリゲートにアクセスできます。 <br />- [Private Protected](../modifiers/private-protected.md) 同じアセンブリ内のデリゲートのクラスまたは派生クラス内のコードからのみ、デリゲートにアクセスできます。 |  
|`Shadows`|任意。 このデリゲートが、基底クラスにある、同じ名前を持つプログラミング要素、またはオーバーロードされる要素のセットを宣言し直して非表示にすることを示します。 宣言された要素は、他の任意の種類の要素でシャドウできます。<br /><br /> シャドウされた要素は、その要素をシャドウする派生クラスからは使用できません。ただし、シャドウする要素がアクセスできない要素の場合は例外です。 たとえば、`Private` 要素が基底クラスの要素をシャドウすると、`Private` 要素へのアクセス許可を持たないコードが、代わりに基底クラスの要素にアクセスします。|  
|`Sub`|省略可能ですが、`Sub` または `Function` のいずれかを指定する必要があります。 このプロシージャを、値を返さないデリゲート `Sub` プロシージャとして宣言します。|  
|`Function`|省略可能ですが、`Sub` または `Function` のいずれかを指定する必要があります。 このプロシージャを、値を返すデリゲート `Function` プロシージャとして宣言します。|  
|`name`|必須です。 デリゲート型の名前です。変数の標準的な名前付け規則に従います。|  
|`typeparamlist`|任意。 このデリゲートの型パラメーターのリスト。 複数の型パラメーターはコンマで区切ります。 必要に応じて、`In` および `Out` ジェネリック修飾子を使用して、各型パラメーターをバリアントとして宣言できます。 [型リスト](type-list.md)をかっこで囲み、`Of` キーワードと共に導入する必要があります。|  
|`parameterlist`|任意。 呼び出されたときにプロシージャに渡されるパラメーターのリスト。 [パラメーター リスト](parameter-list.md)はかっこで囲む必要があります。|  
|`type`|`Function` プロシージャを指定する場合は、必ず指定します。 戻り値のデータ型。|  
  
## <a name="remarks"></a>Remarks  
 `Delegate` ステートメントでは、デリゲート クラスのパラメーターと戻り値の型を定義します。 パラメーターおよび戻り値の型が一致するプロシージャを使用すると、このデリゲート クラスのインスタンスを作成できます。 このプロシージャは、デリゲートの `Invoke` メソッドを呼び出すことによって、後でデリゲート インスタンスを使用して呼び出すことができます。  
  
 デリゲートは、名前空間、モジュール、クラス、または構造体レベルで宣言できますが、プロシージャ内では宣言できません。  
  
 各デリゲート クラスでは、オブジェクト メソッドの仕様を渡すコンストラクターを定義します。 デリゲート コンス トラクターに渡す引数は、メソッドへの参照、またはラムダ式である必要があります。  
  
 メソッドへの参照を指定するには、次の構文を使用します。  
  
 `AddressOf` [`expression`.]`methodname`  
  
 コンパイル時の `expression` の型は、シグネチャがデリゲート クラスのシグネチャと同じで、指定された名前のメソッドを持つクラスまたはインターフェイスである必要があります。 `methodname` は、共有メソッドまたはインスタンス メソッドのいずれかにできます。 クラスの既定メソッドに対してデリゲートを作成する場合も、`methodname` は省略できません。  
  
 ラムダ式を指定するには、次の構文を使用します。  
  
 `Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`  
  
 関数のシグネチャは、デリゲート型のシグネチャと一致している必要があります。 ラムダ式について詳しくは、「[ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)」をご覧ください。  
  
 デリゲートの詳細については、「[デリゲート](../../programming-guide/language-features/delegates/index.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Delegate` ステートメントを使用して、2 つの数値を演算して 1 つの数値を返すためのデリゲートを宣言します。 `DelegateTest` メソッドは、この型のデリゲートのインスタンスを受け取り、それを使用して数値のペアを演算します。  
  
 [!code-vb[VbVbalrDelegates#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#14)]  
  
## <a name="see-also"></a>関連項目

- [AddressOf 演算子](../operators/addressof-operator.md)
- [Of](of-clause.md)
- [デリゲート](../../programming-guide/language-features/delegates/index.md)
- [方法: ジェネリック クラスを使用する](../../programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [共変性と反変性](../../programming-guide/concepts/covariance-contravariance/index.md)
- [In](../modifiers/in-generic-modifier.md)
- [Out](../modifiers/out-generic-modifier.md)
