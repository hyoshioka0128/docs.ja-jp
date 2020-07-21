---
title: 'チュートリアル: COM オブジェクトの作成'
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop [Visual Basic], creating COM objects
- COM objects, creating
- COM interop [Visual Basic], walkthroughs
- object creation [Visual Basic], COM objects
- COM objects, walkthroughs
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
ms.openlocfilehash: 6ff23f73af384a1440bcebd4b6bac21714e01756
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051481"
---
# <a name="walkthrough-creating-com-objects-with-visual-basic"></a>チュートリアル: Visual Basic での COM オブジェクトの作成
新しいアプリケーションまたはコンポーネントを作成する場合は、.NET Framework アセンブリを作成することをお勧めします。 ただし、Visual Basic を使用すると、COM への .NET Framework コンポーネントの公開も簡単になります。 これにより、COM コンポーネントを必要とする以前のアプリケーション スイートに対して新しいコンポーネントが提供できるようになります。 このチュートリアルでは、Visual Basic を使用して、COM クラス テンプレートを使用するかどうかにかかわらず、.NET Framework オブジェクトを COM オブジェクトとして公開する方法について説明します。  
  
 COM オブジェクトを公開する最も簡単な方法は、COM クラス テンプレートを使用することです。 このテンプレートでは、新しいクラスが作成され、クラスと相互運用性レイヤーを COM オブジェクトとして生成してオペレーティング システムに登録するようにプロジェクトが構成されます。  
  
> [!NOTE]
> Visual Basic で作成されたクラスをアンマネージド コードで使用できるように COM オブジェクトとして公開することもできますが、これは実際の COM オブジェクトではなく、Visual Basic では使用できません。 詳細については、「[.NET Framework アプリケーションにおける COM 相互運用性](com-interoperability-in-net-framework-applications.md)」を参照してください。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-com-object-by-using-the-com-class-template"></a>COM クラス テンプレートを使用して COM オブジェクトを作成するには  
  
1. **[新しいプロジェクト]** をクリックして、 **[ファイル]** メニューから新しい Windows アプリケーション プロジェクトを開きます。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** フィールドで、[Windows] が選択されていることを確認します。 **[テンプレート]** の一覧から **[クラス ライブラリ]** を選択し、 **[OK]** をクリックします。 新しいプロジェクトが表示されます。  
  
3. **[プロジェクト]** メニューの **[新しい項目の追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
4. **[テンプレート]** の一覧から **[COM クラス]** を選択し、 **[追加]** をクリックします。 Visual Basic は、新しいクラスを追加し、COM 相互運用のための新しいプロジェクトを構成します。  
  
5. プロパティ、メソッド、イベントなどのコードを COM クラスに追加します。  
  
6. **[ビルド]** メニューから **[ClassLibrary1 のビルド]** を選択します。 Visual Basic は、アセンブリをビルドし、オペレーティング システムに COM オブジェクトを登録します。  
  
## <a name="creating-com-objects-without-the-com-class-template"></a>COM クラス テンプレートを使用しない COM オブジェクトの作成  
 COM クラス テンプレートを使用する代わりに、手動で COM クラスを作成することもできます。 この手順は、コマンド ラインから作業する場合や、COM オブジェクトの定義方法をより細かく制御する必要がある場合に便利です。  
  
#### <a name="to-set-up-your-project-to-generate-a-com-object"></a>COM オブジェクトを生成するようにプロジェクトを設定するには  
  
1. **[新しいプロジェクト]** をクリックして、 **[ファイル]** メニューから新しい Windows アプリケーション プロジェクトを開きます。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** フィールドで、[Windows] が選択されていることを確認します。 **[テンプレート]** の一覧から **[クラス ライブラリ]** を選択し、 **[OK]** をクリックします。 新しいプロジェクトが表示されます。  
  
3. **ソリューション エクスプローラー**で、プロジェクトを右クリックして、 **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されます。  
  
4. **[コンパイル]** タブをクリックします。  
  
5. **[COM の相互運用機能に登録]** チェック ボックスをオンにします。  
  
#### <a name="to-set-up-the-code-in-your-class-to-create-a-com-object"></a>COM オブジェクトを作成するためにクラス内のコードを設定するには  
  
1. **ソリューション エクスプローラー**で、 **[Class1.vb]** をダブルクリックしてコードを表示します。  
  
2. クラスの名前を `ComClass1` に変更します。  
  
3. 次の定数を `ComClass1` に追加します。 これにより、COM オブジェクトに必要なグローバル一意識別子 (GUID) 定数が格納されます。  
  
     [!code-vb[VbVbalrInterop#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#2)]  
  
4. **[ツール]** メニューの **[GUID の作成]** をクリックします。 **[GUID の作成]** ダイアログ ボックスで、 **[レジストリ形式]** をクリックし、 **[コピー]** をクリックします。 **[終了]** をクリックします。  
  
5. `ClassId` の空の文字列を GUID に置き換え、先頭と末尾の中かっこを削除します。 たとえば、Guidgen によって提供された GUID が `"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"` の場合、コードは次のようになります。  
  
     [!code-vb[VbVbalrInterop#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#3)]  
  
6. 次の例に示すように、`InterfaceId` と `EventsId` の定数に対して前のステップを繰り返します。  
  
     [!code-vb[VbVbalrInterop#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#4)]  
  
    > [!NOTE]
    > GUID が新しく、一意であることを確認します。そうでない場合、COM コンポーネントは他の COM コンポーネントと競合する可能性があります。  
  
7. 次の例に示すように、`ComClass` 属性を `ComClass1` に追加して、クラス ID、インターフェイス ID、およびイベント ID の GUID を指定します。  
  
     [!code-vb[VbVbalrInterop#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#5)]  
  
8. COM クラスにはパラメーターなしの `Public Sub New()` コンストラクターが必要です。そうでない場合、クラスが正しく登録されません。 クラスにパラメーターなしのコンストラクターを追加します。  
  
     [!code-vb[VbVbalrInterop#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#6)]  
  
9. プロパティ、メソッド、およびイベントをクラスに追加し、`End Class` ステートメントで終了します。 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 Visual Basic は、アセンブリをビルドし、オペレーティング システムに COM オブジェクトを登録します。  
  
    > [!NOTE]
    > Visual Basic で生成した COM オブジェクトは、実際の COM オブジェクトではないため、他の Visual Basic アプリケーションでは使用できません。 そのような COM オブジェクトに参照を追加しようとすると、エラーが発生します。 詳細については、「[.NET Framework アプリケーションにおける COM 相互運用性](com-interoperability-in-net-framework-applications.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ComClassAttribute>
- [COM 相互運用](index.md)
- [チュートリアル: COM オブジェクトによる継承の実装](walkthrough-implementing-inheritance-with-com-objects.md)
- [#Region ディレクティブ](../../language-reference/directives/region-directive.md)
- [.NET Framework アプリケーションにおける COM 相互運用性](com-interoperability-in-net-framework-applications.md)
- [相互運用性のトラブルシューティング](troubleshooting-interoperability.md)
