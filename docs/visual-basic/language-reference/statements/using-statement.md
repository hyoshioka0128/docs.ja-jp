---
title: Using ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.using
helpviewer_keywords:
- resource disposal
- Try...Catch...Finally statements, equivalent to Using statement
- resources [Visual Basic], disposing
- Using statement [Visual Basic]
ms.assetid: 665d1580-dd54-4e96-a9a9-6be2a68948f1
ms.openlocfilehash: 6ec0e228b3898f66f27e322b5db2dd7f3bf3d7d6
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352756"
---
# <a name="using-statement-visual-basic"></a>Using ステートメント (Visual Basic)

`Using` ブロックの開始を宣言し、必要に応じて、ブロックで制御するシステム リソースを取得します。

## <a name="syntax"></a>構文

```vb
Using { resourcelist | resourceexpression }
    [ statements ]
End Using
```

## <a name="parts"></a>指定項目

|用語|定義|  
|---|---|  
|`resourcelist`|`resourceexpression` を指定しない場合は必須です。 この `Using` ブロックで制御する、コンマで区切られた 1 つまたは複数のシステム リソースの一覧。|  
|`resourceexpression`|`resourcelist` を指定しない場合は必須です。 この `Using` ブロックによって制御されるシステム リソースを参照する、参照変数または式。|  
|`statements`|任意。 `Using` ブロックで実行されるステートメントのブロック。|  
|`End Using`|必須です。 `Using` ブロックの定義を終了し、それによって制御されているすべてのリソースを破棄します。|  

 `resourcelist` 部分の各リソースには、次の構文と指定項目があります。

 `resourcename As New resourcetype [ ( [ arglist ] ) ]`

 \- または -

 `resourcename As resourcetype = resourceexpression`

## <a name="resourcelist-parts"></a>resourcelist の指定項目

|用語|定義|  
|---|---|  
|`resourcename`|必須です。 `Using` ブロックで制御されるシステム リソースを参照する参照変数。|  
|`New`|`Using` ステートメントでリソースを取得する場合は必須です。 リソースを既に取得している場合は、2 番目の代替構文を使用します。|  
|`resourcetype`|必須です。 リソースのクラス。 クラスでは、<xref:System.IDisposable> インターフェイスを実装している必要があります。|  
|`arglist`|任意。 `resourcetype` のインスタンスを作成するためにコンストラクターに渡す引数の一覧。 「[パラメーター リスト](parameter-list.md)」を参照してください。|  
|`resourceexpression`|必須です。 `resourcetype` の要件を満たすシステム リソースを参照する変数または式。 2 番目の代替構文を使用する場合は、`Using` ステートメントに制御を渡す前にリソースを取得する必要があります。|  
  
## <a name="remarks"></a>Remarks

 コードに、ファイル ハンドル、COM ラッパー、SQL 接続などのアンマネージド リソースが必要な場合があります。 `Using` ブロックによって、コードでそのようなリソースを使い終わったときに、それらの 1 つまたは複数が確実に破棄されます。 これにより、それらを他のコードで使用できるようになります。

 管理対象リソースは、.NET Framework ガベージ コレクター (GC) によって、ユーザー側の追加のコーディングなしで破棄されます。 管理対象リソースには `Using` ブロックは必要ありません。 ただし、`Using` ブロックを使用して、ガベージ コレクターを待つことなく、管理対象リソースを強制的に破棄することもできます。

 `Using` ブロックには、取得、使用、破棄という 3 つの部分があります。

- *取得*とは、変数を作成して、システム リソースを参照するようにそれを初期化することを意味します。 `Using` ステートメントでは 1 つ以上のリソースを取得できます。または、ブロックに入る前にリソースを 1 つだけ取得し、それを `Using` ステートメントに指定することもできます。 `resourceexpression` を指定する場合は、`Using` ステートメントに制御を渡す前にリソースを取得する必要があります。

- *使用*とは、リソースにアクセスし、それらによってアクションを実行することを意味します。 `Using` と `End Using` の間のステートメントは、リソースの使用を表します。

- *破棄*は、`resourcename` 内のオブジェクトに対して <xref:System.IDisposable.Dispose%2A> メソッドを呼び出すことを意味します。 これにより、オブジェクトでそのリソースを完全に終了させることができます。 `End Using` ステートメントでは、`Using` ブロックの制御下にあるリソースが破棄されます。

## <a name="behavior"></a>動作

 `Using` ブロックは、`Try`...`Finally` コンストラクションのように動作します。そのコンストラクションでは、`Try` ブロックでリソースを使用し、`Finally` ブロックでそれらを破棄します。 このため、`Using` ブロックでは、ブロックを終了する方法に関係なく、確実にリソースが破棄されます。 これは、<xref:System.StackOverflowException> を除いて、ハンドルされない例外が発生した場合でも当てはまります。

 `Using` ステートメントによって取得されるすべてのリソース変数のスコープは、`Using` ブロックに制限されます。

 `Using` ステートメントで複数のシステム リソースを指定した場合、その効果は、`Using` ブロックを別のブロック内に入れ子にした場合と同じになります。

 `resourcename` が `Nothing` の場合、<xref:System.IDisposable.Dispose%2A> の呼び出しは行われず、例外はスローされません。

## <a name="structured-exception-handling-within-a-using-block"></a>Using ブロック内の構造化例外処理

 `Using` ブロック内で発生する可能性のある例外を処理する必要がある場合は、完全な `Try`...`Finally` コンストラクションをこれに追加できます。 `Using` ステートメントでリソースの取得に失敗した状況に対処する必要がある場合は、`resourcename` が `Nothing` であるかどうかをテストして確認できます。

## <a name="structured-exception-handling-instead-of-a-using-block"></a>Using ブロックの代わりの構造化例外処理

 リソースの取得をより詳細に制御する必要がある場合、または `Finally` ブロックに追加のコードが必要な場合は、`Using` ブロックを `Try`...`Finally` コンストラクションとして書き換えることができます。 次の例では、`resource` の取得と破棄において同等であるスケルトン `Try` と `Using` のコントラクションを示しています。

```vb
Using resource As New resourceType
    ' Insert code to work with resource.
End Using

' For the acquisition and disposal of resource, the following  
' Try construction is equivalent to the Using block.
Dim resource As New resourceType
Try
    ' Insert code to work with resource.
Finally
    If resource IsNot Nothing Then
        resource.Dispose()
    End If
End Try
```

> [!NOTE]
> `Using` ブロック内のコードでは、`resourcename` 内のオブジェクトを別の変数に割り当てることはできません。 `Using` ブロックを終了すると、リソースが破棄され、他の変数はそれが指すリソースにアクセスできなくなります。

## <a name="example"></a>例

 次の例では、log.txt という名前のファイルを作成し、ファイルに 2 行のテキストを書き込んでいます。 さらに、この例では、同じファイルを読み取って、テキスト行を表示しています。

 <xref:System.IO.TextWriter> クラスと <xref:System.IO.TextReader> クラスでは <xref:System.IDisposable> インターフェイスを実装するため、コードでは `Using` ステートメントを使用して、書き込み操作と読み取り操作の後でファイルが正しく閉じられるようにすることができます。

 [!code-vb[VbVbalrStatements#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#50)]

## <a name="see-also"></a>関連項目

- <xref:System.IDisposable>
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
- [方法: システム リソースを破棄する](../../programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)
