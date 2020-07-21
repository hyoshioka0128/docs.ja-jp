---
title: '方法: 式ツリーを変更する'
ms.date: 07/20/2015
ms.assetid: d1309fff-28bd-4d8e-a2cf-75725999e8f2
ms.openlocfilehash: 1f052120a2e7e12f5a985adce3ae193afec0e9af
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410993"
---
# <a name="how-to-modify-expression-trees-visual-basic"></a>方法: 式ツリーを変更する (Visual Basic)

このトピックでは、式ツリーを変更する方法について説明します。 式ツリーは変更不可であるため、直接変更を加えることができません。 式ツリーを変更するには、既存の式ツリーのコピーを作成する必要があります。コピーを作成する際に、必要な変更を加えます。 <xref:System.Linq.Expressions.ExpressionVisitor> クラスを使用して、既存の式ツリーを走査し、走査した各ノードをコピーすることができます。

## <a name="to-modify-an-expression-tree"></a>式ツリーを変更するには

1. 新しい**コンソール アプリケーション** プロジェクトを作成します。

2. ファイルに `System.Linq.Expressions` 名前空間の `Imports` ステートメントを追加します。

3. `AndAlsoModifier` クラスをプロジェクトに追加します。

    ```vb
    Public Class AndAlsoModifier
        Inherits ExpressionVisitor

        Public Function Modify(ByVal expr As Expression) As Expression
            Return Visit(expr)
        End Function

        Protected Overrides Function VisitBinary(ByVal b As BinaryExpression) As Expression
            If b.NodeType = ExpressionType.AndAlso Then
                Dim left = Me.Visit(b.Left)
                Dim right = Me.Visit(b.Right)

                ' Make this binary expression an OrElse operation instead
                ' of an AndAlso operation.
                Return Expression.MakeBinary(ExpressionType.OrElse, left, right, _
                                             b.IsLiftedToNull, b.Method)
            End If

            Return MyBase.VisitBinary(b)
        End Function
    End Class
    ```

    このクラスは、`AND` 条件演算を表す式を変更するための特別なクラスで、<xref:System.Linq.Expressions.ExpressionVisitor> クラスを継承します。 このクラスによって条件 `AND` が条件 `OR` に変更されます。 そのために、クラスは基本データ型の <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> メソッドをオーバーライドします。`AND` 条件式は二項式で表されるためです。 `VisitBinary` メソッドでは、渡される式が `AND` 条件演算を表す場合、`AND` 条件演算子ではなく `OR` 条件演算子を含む新しい式がコードによって作成されます。 `VisitBinary` に渡される式が `AND` 条件演算を表さない場合は、基底クラスの実装が延期されます。 基底クラスのメソッドによって、渡された式ツリーに似たノードが作成されますが、そのノードのサブツリーは、ビジターによって再帰的に作成される式ツリーに置き換えられます。

4. ファイルに `System.Linq.Expressions` 名前空間の `Imports` ステートメントを追加します。

5. 式ツリーを作成し、それをメソッドに渡して変更するコードを、Module1.vb ファイルの `Main` メソッドに追加します。

    ```vb
    Dim expr As Expression(Of Func(Of String, Boolean)) = _
        Function(name) name.Length > 10 AndAlso name.StartsWith("G")

    Console.WriteLine(expr)

    Dim modifier As New AndAlsoModifier()
    Dim modifiedExpr = modifier.Modify(CType(expr, Expression))

    Console.WriteLine(modifiedExpr)

    ' This code produces the following output:
    ' name => ((name.Length > 10) && name.StartsWith("G"))
    ' name => ((name.Length > 10) || name.StartsWith("G"))
    ```

    次のコードは、`AND` 条件演算を含む式を作成し、 `AndAlsoModifier` クラスのインスタンスを作成して、このクラスの `Modify` メソッドにその式を渡します。 元の式ツリーと変更された式ツリーの両方が出力され、変更内容が表示されます。

6. アプリケーションをコンパイルして実行します。

## <a name="see-also"></a>関連項目

- [方法: 式ツリーを実行する (Visual Basic)](how-to-execute-expression-trees.md)
- [式ツリー (Visual Basic)](index.md)
