---
title: 'チュートリアル: Windows API の呼び出し (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- DLLs, calling
- Windows API, walkthroughs
- platform invoke, walkthroughs
- API calls [Visual Basic], walkthroughs [Visual Basic]
- Windows API, calling
- walkthroughs [Visual Basic], API calls
- DllImport attribute, calling Windows API
- Declare statement [Visual Basic], declaring DLL functions
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
ms.openlocfilehash: 59c316ccb3a35a650ac11b96717a3ad729e777a3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54657975"
---
# <a name="walkthrough-calling-windows-apis-visual-basic"></a>チュートリアル: Windows API の呼び出し (Visual Basic)
Windows API は、Windows オペレーティング システムの一部であるダイナミック リンク ライブラリ (Dll) です。 それらを使用するには、独自の同等のプロシージャを記述するのにことは困難である場合は、タスクを実行します。 たとえば、という名前の関数は、Windows`FlashWindowEx`を可能にすること、アプリケーションのタイトル バーを薄いおよび濃い網掛けを切り替える。  
  
 Windows API を使用して、コード内の利点は、数十個は既に書き込まれている便利な関数の使用を待機しているが含まれているため、開発時間を保存することができます。 欠点は、問題が生じた場合、および晙の処理が難しくなって Windows API であることができます。  
  
 Windows API では、相互運用性の特殊なカテゴリを表します。 Windows API では、マネージ コードを使用しないでください、タイプ ライブラリ、および Visual Studio で使用されるものとは異なるデータ型を使用して、組み込みはありません。 これらの違いにより、Windows API は COM オブジェクト、Windows API との相互運用ではなく、[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]プラットフォームを使用して実行されます呼び出すには、pinvoke です。 プラットフォーム呼び出しはマネージ Dll で実装されたアンマネージ関数を呼び出すコードを有効するサービスです。 詳細については、次を参照してください。[アンマネージ DLL 関数の処理](../../../framework/interop/consuming-unmanaged-dll-functions.md)します。 Visual Basic で PInvoke を使用するにはいずれかを使用して、`Declare`ステートメントまたは適用する、`DllImport`属性を空のプロシージャです。  
  
 Windows API の呼び出しでは、Visual Basic では、以前は、プログラミングの重要な部分をされたが、Visual Basic .NET を使用して必要なことはほとんどありません。 可能であればからマネージ コードを使用する必要があります、 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] Windows API の呼び出しではなく、タスクを実行します。 このチュートリアルは、使用する必要のある状況についての情報を提供します。 Windows API が必要です。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="api-calls-using-declare"></a>使用して API 呼び出しを宣言します。  
 Windows API を呼び出すための最も一般的な方法を使用して、`Declare`ステートメント。  
  
#### <a name="to-declare-a-dll-procedure"></a>DLL のプロシージャを宣言するには  
  
1.  を呼び出そうと関数とその引数、引数の型の名前を特定し、値だけでなく、名前とそれを含んでいる DLL の場所を返します。  
  
    > [!NOTE]
    >  Windows API については、プラットフォーム SDK の Windows API で Win32 SDK ドキュメントを参照してください。 Windows API を使用する定数の詳細については、Windows.h、Platform SDK に含まれているなどのヘッダー ファイルを調べてください。  
  
2.  クリックして、新しい Windows アプリケーション プロジェクトを開く**新規**上、**ファイル** メニューのをクリックして**プロジェクト**します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  選択**Windows アプリケーション**Visual Basic プロジェクト テンプレートの一覧から。 新しいプロジェクトが表示されます。  
  
4.  次の追加`Declare`クラスまたはモジュールの DLL を使用するのいずれかの機能します。  
  
     [!code-vb[VbVbalrInterop#9](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_1.vb)]  
  
### <a name="parts-of-the-declare-statement"></a>部分、Declare ステートメント  
 `Declare`ステートメントには、次の要素が含まれています。  
  
#### <a name="auto-modifier"></a>Auto 修飾子  
 `Auto`修飾子に共通言語ランタイムの規則 (または別名が指定されている場合) に従ってメソッド名に基づく文字列を変換するようランタイムに指示します。  
  
#### <a name="lib-and-alias-keywords"></a>Lib およびエイリアス キーワード  
 名以下、`Function`キーワードは、プログラムをインポートした関数へのアクセスに使用する名前。 を呼び出す関数の実際の名前と同じことができます、または任意の有効なプロシージャの名前と採用しを使用することができます、`Alias`キーワードを呼び出している関数の実際の名前を指定します。  
  
 指定、`Lib`キーワードの後ろに呼び出している関数を含んでいる DLL の場所と名前。 Windows システムのディレクトリにあるファイルのパスを指定する必要はありません。  
  
 使用して、`Alias`キーワード、関数の名前を呼び出している場合は、有効な Visual Basic プロシージャ名、またはアプリケーションの他のアイテムの名前と競合します。 `Alias` 呼び出される関数の場合は true。 名前を示します。  
  
#### <a name="argument-and-data-type-declarations"></a>引数とデータ型の宣言  
 引数とそのデータ型を宣言します。 この部分は、Windows を使用するデータ型は、Visual Studio のデータ型に対応していないために、困難な場合がします。 Visual Basic では、多くの作業は、互換性のあるデータ型と呼ばれるプロセスの引数を変換することで*マーシャ リング*します。 使用して引数をマーシャ リングする方法を明示的に制御できる、<xref:System.Runtime.InteropServices.MarshalAsAttribute>属性で定義されている、<xref:System.Runtime.InteropServices>名前空間。  
  
> [!NOTE]
>  以前のバージョンの Visual Basic では、パラメーターを宣言できる`As Any`、つまり、任意のデータのデータ型を使用できます。 Visual Basic では、すべての特定のデータ型を使用することが必要です`Declare`ステートメント。  
  
#### <a name="windows-api-constants"></a>Windows API の定数  
 いくつかの引数は、定数の組み合わせです。 たとえば、`MessageBox`このチュートリアルで示すように API と呼ばれる整数の引数を受け入れる`Typ`メッセージ ボックスを表示する方法を制御します。 調べることで、これらの定数の数値の値を指定できます、 `#define` WinUser.h ファイル内のステートメント。 数値の値は、電卓を使用してそれらを追加して 10 進数に変換するために一般的に 16 進数で表示されます。 感嘆符のスタイルの定数を結合する場合など`MB_ICONEXCLAMATION`0x00000030 し、はい/スタイルなし`MB_YESNO`0x00000004, 番号を追加でき、10 進数、0x00000034 または 52 の結果を取得します。 これらの値をアプリケーションで定数として宣言し、それらを結合することをお勧め、10 進数の結果を直接使用できますを使用して、`Or`演算子。  
  
###### <a name="to-declare-constants-for-windows-api-calls"></a>Windows API 呼び出しのための定数を宣言するには  
  
1.  Windows 関数の呼び出しと、ドキュメントを参照してください。 使用されている定数の名前と、これらの定数の数値を含む .h ファイルの名前を決定します。  
  
2.  メモ帳などのテキスト エディターを使用して、ヘッダー (.h) ファイルの内容を表示、使用する定数に関連付けられている値を見つけてください。 たとえば、 `MessageBox` API は、定数を使用して`MB_ICONQUESTION`メッセージ ボックスに疑問符を表示します。 定義を`MB_ICONQUESTION`WinUser.h では、次のように表示されます。  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3.  同等の追加`Const`ステートメントをクラスまたはモジュールがアプリケーションで利用できるこれらの定数を確認します。 例:  
  
     [!code-vb[VbVbalrInterop#11](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_2.vb)]  
  
###### <a name="to-call-the-dll-procedure"></a>DLL のプロシージャを呼び出す  
  
1.  という名前のボタンを追加`Button1`の起動時に、プロジェクトの形式し、すると、そのコードの表示をダブルクリックします。 ボタンのイベント ハンドラーが表示されます。  
  
2.  コードを追加して、`Click`プロシージャを呼び出すし、適切な引数を提供する、追加したボタンのイベント ハンドラー。  
  
     [!code-vb[VbVbalrInterop#12](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_3.vb)]  
  
3.  F5 キーを押してプロジェクトを実行します。 両方のメッセージ ボックスが表示されます**はい**と**いいえ**返信ボタン。 いずれかをクリックします。  
  
#### <a name="data-marshaling"></a>データのマーシャ リング  
 Visual Basic では、パラメーターと、Windows API 呼び出しの戻り値のデータ型に自動的に変換しますが、使用することができます、 `MarshalAs` API が必要とするアンマネージ データ型を明示的に指定する属性。 相互運用マーシャ リングの詳細については、次を参照してください。[相互運用マーシャ リング](../../../framework/interop/interop-marshaling.md)します。  
  
###### <a name="to-use-declare-and-marshalas-in-an-api-call"></a>API 呼び出しで宣言して MarshalAs を使用するには  
  
1.  データの型を引数、呼び出そうと関数の名前を特定し、値を返します。  
  
2.  アクセスを簡略化する、`MarshalAs`属性を追加、`Imports`クラスまたはモジュールの次の例のように、コードの先頭にステートメント。  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
3.  クラスまたはモジュールを使用しているし、適用するにインポートした関数の関数プロトタイプを追加、`MarshalAs`属性をパラメーターまたは戻り値。 次の例では、型を要求する API 呼び出しで`void*`としてマーシャ リング`AsAny`:  
  
     [!code-vb[VbVbalrInterop#14](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_5.vb)]  
  
## <a name="api-calls-using-dllimport"></a>DllImport を使用して API 呼び出し  
 `DllImport`属性がタイプ ライブラリを持たない Dll で関数を呼び出す 2 番目の方法を提供します。 `DllImport` 使用するとほぼ同じです、`Declare`ステートメントが関数を呼び出す方法より詳細に制御を提供します。  
  
 使用することができます`DllImport`ほとんどの Windows API を使用した呼び出しの呼び出しは、共有を参照している限り (とも呼ばれる*静的*) メソッドです。 クラスのインスタンスを必要とするメソッドを使用することはできません。 異なり`Declare`ステートメント、`DllImport`呼び出しが使用することはできません、`MarshalAs`属性。  
  
#### <a name="to-call-a-windows-api-using-the-dllimport-attribute"></a>DllImport 属性を使用して Windows API を呼び出す  
  
1.  クリックして、新しい Windows アプリケーション プロジェクトを開く**新規**上、**ファイル** メニューのをクリックして**プロジェクト**します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  選択**Windows アプリケーション**Visual Basic プロジェクト テンプレートの一覧から。 新しいプロジェクトが表示されます。  
  
3.  という名前のボタンを追加`Button2`スタートアップ フォームにします。  
  
4.  ダブルクリック`Button2`フォームのコード ビューを開きます。  
  
5.  アクセスを簡略化する`DllImport`、追加、`Imports`スタートアップ フォーム クラスのコードの先頭にステートメント。  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
6.  空の関数を前の宣言、`End Class`フォーム、および名、関数のステートメント`MoveFile`します。  
  
7.  適用、`Public`と`Shared`関数宣言とパラメーターを設定する修飾子`MoveFile`Windows API 関数を使用して、引数に基づいた。  
  
     [!code-vb[VbVbalrInterop#16](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_6.vb)]  
  
     関数は、任意の有効なプロシージャ名前を持つことができます。`DllImport`属性は、DLL の名前を指定します。 パラメーターのマーシャ リングの相互運用性も処理して、データに類似した Visual Studio のデータ型を選択できるように、戻り値の型 API では。  
  
8.  適用、`DllImport`属性を空の関数。 最初のパラメーターを呼び出している関数を含む DLL の場所と名前です。 Windows システムのディレクトリにあるファイルのパスを指定する必要はありません。 2 番目のパラメーターは、Windows api 関数の名前を指定する名前付き引数です。 この例で、`DllImport`属性への呼び出しを強制する`MoveFile`に転送される`MoveFileW`KERNEL32 でします。DLL です。 `MoveFileW`メソッドは、パスからファイルをコピー`src`パスに`dst`します。  
  
     [!code-vb[VbVbalrInterop#17](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_7.vb)]  
  
9. コードを追加して、`Button2_Click`関数を呼び出すイベント ハンドラー。  
  
     [!code-vb[VbVbalrInterop#18](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_8.vb)]  
  
10. Test.txt という名前のファイルを作成し、ハード ドライブの C:\Tmp ディレクトリに配置します。 必要な場合は、Tmp ディレクトリを作成します。  
  
11. F5 キーを押してアプリケーションを起動します。 メイン フォームが表示されます。  
  
12. クリックして**Button2**します。 ファイルを移動できる場合は、「ファイルが正常に移動されました」メッセージが表示されます。  
  
## <a name="see-also"></a>関連項目
- <xref:System.Runtime.InteropServices.DllImportAttribute>
- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Declare ステートメント](../../../visual-basic/language-reference/statements/declare-statement.md)
- [Auto](../../../visual-basic/language-reference/modifiers/auto.md)
- [Alias](../../../visual-basic/language-reference/statements/alias-clause.md)
- [COM 相互運用](../../../visual-basic/programming-guide/com-interop/index.md)
- [マネージド コードでのプロトタイプの作成](../../../framework/interop/creating-prototypes-in-managed-code.md)
- [コールバック メソッドとしてのデリゲートのマーシャ リング](../../../framework/interop/marshaling-a-delegate-as-a-callback-method.md)
