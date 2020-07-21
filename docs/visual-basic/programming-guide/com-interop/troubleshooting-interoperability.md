---
title: 相互運用性のトラブルシューティング
ms.date: 07/20/2015
helpviewer_keywords:
- interop, deploying assemblies
- assemblies [Visual Basic]
- interop, installing assemblies that share components
- COM objects, troubleshooting
- interop, sharing components
- troubleshooting interoperability [Visual Basic]
- interoperability, troubleshooting
- COM interop [Visual Basic], troubleshooting
- assemblies [Visual Basic], deploying
- troubleshooting Visual Basic, interoperability
- interop assemblies
- interoperability, sharing components
- shared components, using with assemblies
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
ms.openlocfilehash: 0890bac80396feaf37d4ba917c1e3fafb8579981
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396767"
---
# <a name="troubleshooting-interoperability-visual-basic"></a>相互運用性のトラブルシューティング (Visual Basic)
COM と .NET Framework のマネージド コードとの間で相互運用を行うときに、以下に示した一般的な問題が発生することがあります。  
  
## <a name="interop-marshaling"></a><a name="vbconinteroperabilitymarshalinganchor1"></a>相互運用マーシャリング  
 場合によっては、.NET Framework の一部ではないデータ型を使用しなければならないことがあります。 COM オブジェクトに関するほとんどの作業は相互運用アセンブリによって処理されますが、マネージド オブジェクトが COM に公開されるときに使用されるデータ型の制御が必要になる場合があります。 たとえば、クラス ライブラリ内の構造体では、Visual Basic 6.0 とそれ以前のバージョンで作成された COM オブジェクトに送信される文字列に対して、`BStr` アンマネージド型を指定する必要があります。 このような場合は、<xref:System.Runtime.InteropServices.MarshalAsAttribute> 属性を使用して、マネージド型がアンマネージド型として公開されるようにすることができます。  
  
## <a name="exporting-fixed-length-strings-to-unmanaged-code"></a><a name="vbconinteroperabilitymarshalinganchor2"></a>アンマネージド コードへの固定長文字列のエクスポート  
 Visual Basic 6.0 とそれ以前のバージョンでは、文字列は null 終端文字のないバイト シーケンスとして COM オブジェクトにエクスポートされます。 他の言語との互換性のために、Visual Basic .NET では文字列をエクスポートするときに終端文字が挿入されます。 この非互換性に対処する最良の方法は、終端文字のない文字列を `Byte` または `Char` の配列としてエクスポートすることです。  
  
## <a name="exporting-inheritance-hierarchies"></a><a name="vbconinteroperabilitymarshalinganchor3"></a>継承階層のエクスポート  
 マネージド クラスの階層は、COM オブジェクトとして公開されるとフラット化されます。 たとえば、メンバーを持つ基底クラスを定義し、COM オブジェクトとして公開されている派生クラスで基底クラスを継承した場合、COM オブジェクトの派生クラスを使用するクライアントは、継承されたメンバーを使用できません。 基底クラスのメンバーには、COM オブジェクトから基底クラスのインスタンスとしてのみアクセスでき、その後は、基底クラスも COM オブジェクトとして作成される場合にのみアクセスできます。  
  
## <a name="overloaded-methods"></a>オーバーロードされたメソッド  
 オーバーロードされたメソッドは Visual Basic で作成できますが、COM ではサポートされていません。 オーバーロードされたメソッドを含むクラスが COM オブジェクトとして公開されると、オーバーロードされたメソッドに対して新しいメソッド名が生成されます。  
  
 たとえば、`Synch` メソッドの 2 つのオーバーロードを持つクラスを考えてみます。 そのクラスが COM オブジェクトとして公開された場合、生成される新しいメソッド名は `Synch` と `Synch_2` のようになります。  
  
 この名前変更によって、COM オブジェクトのコンシューマーに 2 つの問題が発生する可能性があります。  
  
1. 生成されたメソッド名をクライアントが予期していない可能性があります。  
  
2. COM オブジェクトとして公開されるクラスに対して生成されたメソッド名は、クラスまたはその基底クラスに新しいオーバーロードが追加されたときに変更される可能性があります。 これにより、バージョン管理の問題が発生する可能性があります。  
  
 両方の問題を解決するには、COM オブジェクトとして公開されるオブジェクトを開発するときに、オーバーロードを使用するのではなく、各メソッドに一意の名前を指定します。  
  
## <a name="use-of-com-objects-through-interop-assemblies"></a><a name="vbconinteroperabilitymarshalinganchor4"></a>相互運用アセンブリによる COM オブジェクトの使用  
 相互運用アセンブリは、それらが表す COM オブジェクトをマネージド コードで置き換えた場合とほぼ同様に使用されます。 ただし、それらはラッパーであって実際の COM オブジェクトではないため、相互運用アセンブリの使用と標準アセンブリの使用にはいくつかの違いがあります。 そのような違いのある領域として、クラスの公開、パラメーターと戻り値のデータ型があります。  
  
## <a name="classes-exposed-as-both-interfaces-and-classes"></a><a name="vbconinteroperabilitymarshalinganchor5"></a>インターフェイスとクラスの両方として公開されるクラス  
 標準アセンブリのクラスとは異なり、相互運用アセンブリの COM クラスは、インターフェイスとクラス (COM クラスを表す) の両方として公開されます。 インターフェイスの名前は、COM クラスの名前と同じです。 相互運用クラスの名前は、元の COM クラスの名前と同じですが、"Class" という単語が追加されます。 たとえば、COM オブジェクトの相互運用アセンブリへの参照を持つプロジェクトがあるとします。 COM クラスに `MyComClass` という名前が付けられている場合、IntelliSense とオブジェクト ブラウザーには、`MyComClass` という名前のインターフェイスと、`MyComClassClass` という名前のクラスが表示されます。  
  
## <a name="creating-instances-of-a-net-framework-class"></a><a name="vbconinteroperabilitymarshalinganchor6"></a>.NET Framework クラスのインスタンスの作成  
 通常、.NET Framework クラスのインスタンスを作成するにはクラス名を指定した `New` ステートメントを使用します。 COM クラスが相互運用アセンブリによって表されるようにすることは、インターフェイスで `New` ステートメントを使用できるケースの 1 つです。 `Inherits` ステートメントで COM クラスを使用している場合を除き、クラスを使用するのと同様にインターフェイスを使用できます。 次のコードは、Microsoft ActiveX データ オブジェクト 2.8 ライブラリ COM オブジェクトへの参照を含むプロジェクト内に、`Command` オブジェクトを作成する方法を示しています。  
  
 [!code-vb[VbVbalrInterop#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#20)]  
  
 ただし、COM クラスを派生クラスのベースとして使用している場合は、次のコードのように、COM クラスを表す相互運用クラスを使用する必要があります。  
  
 [!code-vb[VbVbalrInterop#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#21)]  
  
> [!NOTE]
> 相互運用アセンブリにより、COM クラスを表すインターフェイスが暗黙的に実装されます。 これらのインターフェイスを実装するために `Implements` ステートメントを使用しないでください。使用すると、エラーが発生します。  
  
## <a name="data-types-for-parameters-and-return-values"></a><a name="vbconinteroperabilitymarshalinganchor7"></a>パラメーターと戻り値のデータ型  
 標準アセンブリのメンバーとは異なり、相互運用アセンブリのメンバーは、元のオブジェクト宣言で使用されているデータ型とは異なるデータ型を持つ場合があります。 COM の型は相互運用アセンブリによって互換性のある共通言語ランタイムの型に暗黙的に変換されますが、ランタイム エラーを防ぐために、双方で使用されているデータ型に注意する必要があります。 たとえば、Visual Basic 6.0 とそれ以前のバージョンで作成された COM オブジェクトでは、`Integer` 型の値は、.NET Framework での同等な型である `Short` と見なされます。 インポートしたメンバーを使用する前に、オブジェクト ブラウザーを使用して、それらの特性を確認することをお勧めします。  
  
## <a name="module-level-com-methods"></a><a name="vbconinteroperabilitymarshalinganchor8"></a>モジュール レベルの COM メソッド  
 ほとんどの COM オブジェクトは、`New` キーワードを使用して COM クラスのインスタンスを作成してから、そのオブジェクトのメソッドを呼び出すことによって使用します。 この規則の 1 つの例外として、COM クラス `AppObj` または `GlobalMultiUse` を含む COM オブジェクトがあります。 このようなクラスは Visual Basic .NET クラスのモジュール レベル メソッドに似ています。 Visual Basic 6.0 とそれ以前のバージョンでは、メソッドのいずれかを初めて呼び出すときに、これらのオブジェクトのインスタンスが暗黙的に作成されます。 たとえば、Visual Basic 6.0 では、Microsoft DAO 3.6 オブジェクト ライブラリへの参照を追加し、最初にインスタンスを作成することなく、`DBEngine` メソッドを呼び出すことができます。  
  
```vb  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 Visual Basic .NET では常に、COM オブジェクトのメソッドを使用する前に、まずインスタンスを作成する必要があります。 これらのメソッドを Visual Basic で使用するには、目的のクラスの変数を宣言し、new キーワードを使用してオブジェクトをオブジェクト変数に割り当てます。 `Shared` キーワードは、クラスのインスタンスが確実に 1 つだけ作成されるようにする場合に使用できます。  
  
 [!code-vb[VbVbalrInterop#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#23)]  
  
## <a name="unhandled-errors-in-event-handlers"></a><a name="vbconinteroperabilitymarshalinganchor9"></a>イベント ハンドラーでのハンドルされないエラー  
 一般的な相互運用の問題には、COM オブジェクトで発生したイベントを処理するイベント ハンドラーでのエラーが含まれます。 `On Error` または `Try...Catch...Finally` ステートメントを使用してエラーの有無を明示的にチェックしない限り、このようなエラーは無視されます。 たとえば、次の例は、Microsoft ActiveX データ オブジェクト 2.8 ライブラリ COM オブジェクトへの参照を含む Visual Basic .NET プロジェクトのものです。  
  
 [!code-vb[VbVbalrInterop#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#24)]  
  
 この例では、予期したとおりにエラーが発生します。 ただし、`Try...Catch...Finally` ブロックを指定せずに同じ例を試した場合、`OnError Resume Next` ステートメントを使用した場合と同様に、エラーは無視されます。 エラー処理がなければ、0 による除算は警告なく失敗します。 このようなエラーが原因でハンドルされない例外エラーが発生することはないため、COM オブジェクトからのイベントを処理する何らかの形式の例外処理をイベント ハンドラーで使用することが重要です。  
  
### <a name="understanding-com-interop-errors"></a>COM 相互運用エラーについて  
 エラー処理を行わないと、相互運用呼び出しによって、情報がほとんど提供されないエラーが頻繁に発生します。 可能な限り、構造化されたエラー処理を使用して、発生した問題に関する詳細情報を提供します。 これは、アプリケーションをデバッグするときに特に役立ちます。 次に例を示します。  
  
 [!code-vb[VbVbalrInterop#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#25)]  
  
 例外オブジェクトの内容を調べることによって、エラーの説明、HRESULT、COM エラーの発生源などの情報を確認できます。  
  
## <a name="activex-control-issues"></a><a name="vbconinteroperabilitymarshalinganchor10"></a>ActiveX コントロールの問題  
 Visual Basic 6.0 で動作するほとんどの ActiveX コントロールは、Visual Basic .NET で問題なく動作します。 主な例外は、コンテナー コントロール、または他のコントロールを視覚的に含むコントロールです。 Visual Studio で正しく動作しない古いコントロールの例を次に示します。  
  
- Microsoft Forms 2.0 Frame コントロール  
  
- アップダウン コントロール (スピン コントロールとも呼ばれます)  
  
- Sheridan タブ コントロール  
  
 サポートされていない ActiveX コントロールの問題には、いくつかの回避策しかありません。 元のソース コードを所有している場合は、既存のコントロールを Visual Studio に移行できます。 それ以外の場合は、.NET と互換性のある更新されたバージョンのコントロールの有無をソフトウェア ベンダーに確認し、サポートされていない ActiveX コントロールを置き換えます。  
  
## <a name="passing-readonly-properties-of-controls-byref"></a><a name="vbconinteroperabilitymarshalinganchor11"></a>コントロールの読み取り専用プロパティを ByRef で渡す  
 Visual Basic .NET では、一部の古い ActiveX コントロールの `ReadOnly` プロパティを他のプロシージャに `ByRef` パラメーターとして渡すと、"エラー 0x800A017F CTL_E_SETNOTSUPPORTED" などの COM エラーが発生することがあります。 Visual Basic 6.0 からの同様のプロシージャ呼び出しではエラーは発生せず、パラメーターは値渡しで渡されたものとして扱われます。 Visual Basic .NET のエラー メッセージは、プロパティの `Set` プロシージャを持たないプロパティを変更しようとしていることを示します。  
  
 呼び出されるプロシージャにアクセスできる場合は、`ByVal` キーワードを使用して、`ReadOnly` プロパティを受け取るパラメーターを宣言します。それにより、このエラーを回避できます。 次に例を示します。  
  
 [!code-vb[VbVbalrInterop#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#26)]  
  
 呼び出されるプロシージャのソース コードにアクセスできない場合は、呼び出し元プロシージャを囲むもう一組の角かっこを追加することで、プロパティを強制的に値渡しにすることができます。 たとえば、Microsoft ActiveX データ オブジェクト 2.8 ライブラリ COM オブジェクトへの参照があるプロジェクトでは、以下を使用できます。  
  
 [!code-vb[VbVbalrInterop#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#27)]  
  
## <a name="deploying-assemblies-that-expose-interop"></a><a name="vbconinteroperabilitymarshalinganchor12"></a>相互運用機能を公開するアセンブリの配置  
 COM インターフェイスを公開するアセンブリを配置する場合、いくつかの固有の課題が生じます。 たとえば、別のアプリケーションから同じ COM アセンブリを参照すると、問題が発生する可能性があります。 この状況は、新しいバージョンのアセンブリがインストールされていて、別のアプリケーションで以前のバージョンのアセンブリを引き続き使用している場合によく発生します。 DLL を共有するアセンブリをアンインストールすると、意図せずにそのアセンブリを他のアセンブリから使用できなくしてしまう可能性があります。  
  
 この問題を回避するには、共有アセンブリをグローバル アセンブリ キャッシュ (GAC) にインストールし、コンポーネントに MergeModule を使用する必要があります。 GAC にアプリケーションをインストールできない場合は、バージョン固有のサブディレクトリにある CommonFilesFolder にインストールする必要があります。  
  
 共有されていないアセンブリは、呼び出し元のアプリケーションと共にサイド バイ サイドでディレクトリに配置する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [COM 相互運用](index.md)
- [Tlbimp.exe (タイプ ライブラリ インポーター)](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe (タイプ ライブラリ エクスポーター)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [チュートリアル: COM オブジェクトによる継承の実装](walkthrough-implementing-inheritance-with-com-objects.md)
- [Inherits ステートメント](../../language-reference/statements/inherits-statement.md)
- [グローバル アセンブリ キャッシュ](../../../framework/app-domains/gac.md)
