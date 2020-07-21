---
title: Property プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- Set statement [Visual Basic], Property procedures
- Visual Basic code, procedures
- return values [Visual Basic], Property procedures
- syntax [Visual Basic], Property procedures
- procedures [Visual Basic], property
- Visual Basic code, properties
- procedures [Visual Basic], calling
- properties [Visual Basic], custom
- property procedures
- Get statement [Visual Basic], property procedures
ms.assetid: 46a98379-e1a2-45dd-a48c-b51213f5ab07
ms.openlocfilehash: cb5b0e12512e476b7c96bbfb19f8e4f470f6b498
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363734"
---
# <a name="property-procedures-visual-basic"></a>Property プロシージャ (Visual Basic)

プロパティ プロシージャは、モジュール、クラス、または構造体のカスタム プロパティを操作する一連の Visual Basic ステートメントです。 プロパティ プロシージャは、"*プロパティ アクセサー*" とも呼ばれます。

Visual Basic には、次のプロパティ プロシージャが用意されています。

- `Get` プロシージャは、プロパティの値を返します。 式でプロパティにアクセスするときに呼び出されます。
- `Set` プロシージャは、プロパティを値 (オブジェクト参照を含む) に設定します。 プロパティに値を割り当てるときに呼び出されます。

通常は、`Get` および `Set` ステートメントを使用して、プロパティ プロシージャをペアで定義しますが、プロパティが読み取り専用 ([Get ステートメント](../../../language-reference/statements/get-statement.md)) または書き込み専用 ([Set ステートメント](../../../language-reference/statements/set-statement.md)) の場合は、いずれかのプロシージャだけを定義できます。

自動実装プロパティを使用する場合は、`Get` および `Set` プロシージャを省略できます。 詳細については、「[自動実装プロパティ](./auto-implemented-properties.md)」を参照してください。

プロパティは、クラス、構造体、モジュールで定義できます。 プロパティは既定で `Public` であるため、プロパティのコンテナーにアクセスできるアプリケーション内のどこからでも呼び出すことができます。

プロパティと変数の比較については、「[Differences Between Properties and Variables in Visual Basic (Visual Basic のプロパティと変数の違い)](differences-between-properties-and-variables.md)」をご覧ください。

## <a name="declaration-syntax"></a>宣言の構文

プロパティ自体は、[Property ステートメント](../../../language-reference/statements/property-statement.md)と `End Property` ステートメントで囲まれたコード ブロックによって定義されます。 このブロック内では、各プロパティ プロシージャは、宣言ステートメント (`Get` または `Set`) と、対応する `End` 宣言で囲まれた内部ブロックとして表示されます。

プロパティとそのプロシージャを宣言するための構文は次のとおりです。

```vb
[Default] [Modifiers] Property PropertyName[(ParameterList)] [As DataType]
    [AccessLevel] Get
        ' Statements of the Get procedure.
        ' The following statement returns an expression as the property's value.
        Return Expression
    End Get
    [AccessLevel] Set[(ByVal NewValue As DataType)]
        ' Statements of the Set procedure.
        ' The following statement assigns newvalue as the property's value.
        LValue = NewValue
    End Set
End Property
' - or -
[Default] [Modifiers] Property PropertyName [(ParameterList)] [As DataType]
```

`Modifiers` では、アクセス レベルと、オーバーロード、オーバーライド、共有、シャドウに関する情報、およびプロパティが読み取り専用または書き込み専用かどうかを指定できます。 `Get` または `Set` プロシージャの `AccessLevel` には、プロパティ自体に指定されたアクセス レベルよりも制限の厳しい任意のレベルを指定できます。 詳細については、「[Property Statement (Property ステートメント)](../../../language-reference/statements/property-statement.md)」をご覧ください。

### <a name="data-type"></a>データの種類

プロパティのデータ型とプリンシパル アクセス レベルは、プロパティ プロシージャではなく、`Property` ステートメントで定義されます。 プロパティはデータ型を 1 つだけ持つことができます。 たとえば、`Decimal` 値を格納し、`Double` 値を取得するプロパティを定義することはできません。

### <a name="access-level"></a>アクセス レベル

プロパティのプリンシパル アクセス レベルを定義し、プロパティ プロシージャの 1 つでアクセス レベルをさらに制限できます。 たとえば、`Public` プロパティを定義し、`Private Set` プロシージャを定義できます。 `Get` プロシージャは `Public` のままです。 アクセス レベルは、プロパティのプロシージャの 1 つでのみ変更することができ、プリンシパル アクセス レベルよりも厳しい制限にすることだけが可能です。 詳細については、「[方法:方法: 複数のアクセス レベルを持つプロパティを宣言する](how-to-declare-a-property-with-mixed-access-levels.md) をご覧ください。

## <a name="parameter-declaration"></a>パラメーターの宣言

引渡し方法に `ByVal` を指定する必要がある点を除き、[Sub プロシージャ](sub-procedures.md)の場合と同様に各パラメーターを宣言します。

パラメーター リストの各パラメーターの構文は次のとおりです。

```vb
[Optional] ByVal [ParamArray] parametername As datatype
```

パラメーターが省略可能な場合は、宣言の一部として既定値も指定する必要があります。 既定値を指定するための構文は次のとおりです。

```vb
Optional ByVal parametername As datatype = defaultvalue
```

## <a name="property-value"></a>プロパティ値

`Get` プロシージャでは、戻り値は呼び出し元の式にプロパティの値として指定されます。

`Set` プロシージャでは、新しいプロパティ値が `Set` ステートメントのパラメーターに渡されます。 パラメーターを明示的に宣言する場合は、プロパティと同じデータ型で宣言する必要があります。 パラメーターを宣言していない場合、コンパイラは暗黙的な `Value` パラメーターを使用して、プロパティに割り当てられる新しい値を表します。

## <a name="calling-syntax"></a>呼び出しの構文

プロパティを参照することにより、プロパティ プロシージャを暗黙的に呼び出します。 プロパティの名前は、変数の名前を使用する場合と同様に使用します。ただし、省略可能ではないすべての引数に値を指定する必要があり、引数リストをかっこで囲む必要があります。 引数を指定しない場合は、必要に応じてかっこを省略できます。

`Set` プロシージャの暗黙的な呼び出しの構文は次のとおりです。

```vb
propertyname[(argumentlist)] = expression
```

`Get` プロシージャの暗黙的な呼び出しの構文は次のとおりです。

```vb
lvalue = propertyname[(argumentlist)]
Do While (propertyname[(argumentlist)] > expression)
```

### <a name="illustration-of-declaration-and-call"></a>宣言と呼び出しの実例

次のプロパティは、フル ネームを 2 つの構成要素名 (名と姓) として格納します。 呼び出し元のコードが `fullName` を読み取ると、`Get` プロシージャが 2 つの構成要素名を結合し、フル ネームを返します。 呼び出し元のコードが新しいフル ネームを割り当てると、`Set` プロシージャがそれを 2 つの構成要素名に分割することを試みます。 スペースが見つからない場合は、すべてが名として格納されます。

[!code-vb[VbVbcnProcedures#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#8)]

次の例は、`fullName` のプロパティ プロシージャの一般的な呼び出しを示しています。

[!code-vb[VbVbcnProcedures#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#9)]

## <a name="see-also"></a>関連項目

- [手順](index.md)
- [Function プロシージャ](function-procedures.md)
- [演算子プロシージャ](operator-procedures.md)
- [プロシージャのパラメーターと引数](procedure-parameters-and-arguments.md)
- [Visual Basic のプロパティと変数の違い](differences-between-properties-and-variables.md)
- [方法: プロパティを作成する](how-to-create-a-property.md)
- [方法: プロパティ プロシージャを呼び出す](how-to-call-a-property-procedure.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](how-to-get-a-value-from-a-property.md)
