---
title: '方法: Visual Basic から COM オブジェクトを参照する'
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop [Visual Basic], referencing COM objects
- referencing objects, COM objects from Visual Basic
- objects [Visual Basic], referencing
- COM objects, referencing
- interop assemblies
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
ms.openlocfilehash: 2e2cbac6fad5e1686b7383c44619b8c6f5326483
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396805"
---
# <a name="how-to-reference-com-objects-from-visual-basic"></a>方法: Visual Basic から COM オブジェクトを参照する
Visual Basic でタイプ ライブラリがある COM オブジェクトへの参照を追加するには、COM ライブラリ用の相互運用アセンブリを作成する必要があります。 COM オブジェクトのメンバーへの参照は相互運用アセンブリにルーティングされてから、実際の COM オブジェクトに転送されます。 COM オブジェクトからの応答は相互運用アセンブリにルーティングされてから、.NET Framework アプリケーションに転送されます。  
  
 .NET アセンブリに COM オブジェクトの型情報を埋め込むことによって、相互運用アセンブリを使用せずに COM オブジェクトを参照できます。 型情報を埋め込むには、COM オブジェクトへの参照の `Embed Interop Types` プロパティを `True` に設定します。 コマンド ライン コンパイラを使用してコンパイルする場合は、`/link` オプションを使用して COM ライブラリを参照します。 詳細については、「[-link (Visual Basic)](../../reference/command-line-compiler/link.md)」を参照してください。  
  
 統合開発環境 (IDE) からタイプ ライブラリへの参照を追加すると、Visual Basic によって相互運用アセンブリが自動的に作成されます。 コマンド ラインから作業する場合は、Tlbimp ユーティリティを使用して、相互運用アセンブリを手動で作成できます。  
  
### <a name="to-add-references-to-com-objects"></a>COM オブジェクトへの参照を追加するには  
  
1. **[プロジェクト]** メニューの **[参照の追加]** を選択し、次にダイアログ ボックスの **[COM]** タブをクリックします。  
  
2. COM オブジェクトの一覧から、使用するコンポーネントを選択します。  
  
3. 相互運用アセンブリへのアクセスを簡単にするために、COM オブジェクトを使用するクラスまたはモジュールの先頭に `Imports` ステートメントを追加します。 たとえば、次のコード例では、`Microsoft InkEdit Control 1.0` ライブラリで参照されているオブジェクトの `INKEDLib` 名前空間をインポートします。  
  
     [!code-vb[VbVbalrInterop#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#40)]  
  
### <a name="to-create-an-interop-assembly-using-tlbimp"></a>Tlbimp を使用して相互運用アセンブリを作成するには  
  
1. Tlbimp の場所がまだ検索パスに含まれておらず、現在のディレクトリに存在しない場合は、検索パスにそれを追加します。  
  
2. 次の情報を指定してコマンド プロンプトから Tlbimp を呼び出します。  
  
    - タイプ ライブラリを含む DLL の名前と場所  
  
    - 情報の配置先となる名前空間の名前と場所  
  
    - ターゲットとする相互運用アセンブリの名前と場所  
  
     次にコード例を示します。  
  
    ```console  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     登録されていない COM オブジェクトに対しても、Tlbimp.exe を使用してタイプ ライブラリの相互運用アセンブリを作成できます。 ただし、相互運用アセンブリによって参照される COM オブジェクトは、それらが使用されるコンピューターに適切に登録されている必要があります。 Windows オペレーティング システムに含まれている Regsvr32 ユーティリティを使用して、COM オブジェクトを登録できます。  
  
## <a name="see-also"></a>関連項目

- [COM 相互運用](index.md)
- [Tlbimp.exe (タイプ ライブラリ インポーター)](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe (タイプ ライブラリ エクスポーター)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [チュートリアル: COM オブジェクトによる継承の実装](walkthrough-implementing-inheritance-with-com-objects.md)
- [相互運用性のトラブルシューティング](troubleshooting-interoperability.md)
- [Imports ステートメント (.NET 名前空間および型)](../../language-reference/statements/imports-statement-net-namespace-and-type.md)
