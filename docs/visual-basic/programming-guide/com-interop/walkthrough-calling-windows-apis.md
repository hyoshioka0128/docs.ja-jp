---
title: 'チュートリアル: Windows API の呼び出し'
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
ms.openlocfilehash: c7b84a3bb12329ae235e5ea03dc5e86f921112c4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396754"
---
# <a name="walkthrough-calling-windows-apis-visual-basic"></a>チュートリアル: Windows API の呼び出し (Visual Basic)
Windows API は、Windows オペレーティング システムの一部であるダイナミック リンク ライブラリ (DLL) です。 独自の同等のプロシージャを記述することが困難な場合は、これらを使用してタスクを実行します。 たとえば、Windows には `FlashWindowEx` という名前の関数が用意されていて、これを使用すると、アプリケーションのタイトル バーを交互に明るい色合いと暗い色合いにすることができます。  
  
 ご自身のコードで Windows API を使用する利点は、既に記述され、使用されるのを待っている便利な関数が多数含まれているため、開発時間を節約できることです。 欠点として、Windows API は処理が容易でなく、問題が発生したときに困難な状況になることがあります。  
  
 Windows API は、相互運用性の特別なカテゴリを表しています。 Windows API にマネージド コードは使用されておらず、組み込みのタイプ ライブラリはありません。また、使用するデータ型は Visual Studio で使用するものとは異なります。 これらの違いにより、また、Windows API は COM オブジェクトではないことから、Windows API および .NET Framework との相互運用性は、プラットフォーム呼び出し (PInvoke) を使用して実現されます。 プラットフォーム呼び出しは、DLL に実装されたアンマネージド関数をマネージド コードから呼び出すことを可能にするサービスです。 詳細については、「[アンマネージド DLL 関数の処理](../../../framework/interop/consuming-unmanaged-dll-functions.md)」を参照してください。 Visual Basic で PInvoke を使用するには、`Declare` ステートメントを使用するか、`DllImport` 属性を空のプロシージャに適用します。  
  
 Windows API 呼び出しは、過去においては Visual Basic プログラミングの重要な部分でしたが、Visual Basic .NET ではほとんど必要ありません。 可能な限り、Windows API 呼び出しではなく .NET Framework のマネージド コードを使用してタスクを実行するようにしてください。 このチュートリアルでは、Windows API を使用することが必要な場合のために、情報を示します。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="api-calls-using-declare"></a>Declare を使用した API 呼び出し  
 Windows API を呼び出す最も一般的な方法は、`Declare` ステートメントを使用することです。  
  
### <a name="to-declare-a-dll-procedure"></a>DLL プロシージャを宣言するには  
  
1. 呼び出す関数の名前と引数、引数の型、戻り値、さらに、その関数を含む DLL の名前と場所を特定します。  
  
    > [!NOTE]
    > Windows API の詳細については、プラットフォーム SDK Windows API の Win32 SDK ドキュメントを参照してください。 Windows API で使用する定数の詳細については、プラットフォーム SDK に付属している Windows.h などのヘッダー ファイルを調べてください。  
  
2. **[ファイル]** メニューの **[新規作成]** をクリックし、次に **[プロジェクト]** をクリックして、新しい Windows アプリケーション プロジェクトを開きます。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3. Visual Basic プロジェクト テンプレートの一覧から **[Windows アプリケーション]** を選択します。 新しいプロジェクトが表示されます。  
  
4. DLL を使用するクラスまたはモジュールに、次の `Declare` 関数を追加します。  
  
     [!code-vb[VbVbalrInterop#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#9)]  
  
### <a name="parts-of-the-declare-statement"></a>Declare ステートメントの各部  
 `Declare` ステートメントには、次の要素が含まれます。  
  
#### <a name="auto-modifier"></a>Auto 修飾子  
 `Auto` は、共通言語ランタイムの規則 (または、指定されている場合はエイリアス名) に従って、メソッド名に基づいて文字列を変換するようにランタイムに指示する修飾子です。  
  
#### <a name="lib-and-alias-keywords"></a>Lib キーワードと Alias キーワード  
 `Function` キーワードの後の名前は、インポートされた関数にアクセスするためにプログラムで使用する名前です。 これは、呼び出す関数の実際の名前と同じにすることができます。または、任意の有効なプロシージャ名を使用し、`Alias` キーワードを使って呼び出す関数の実際の名前を指定することもできます。  
  
 `Lib` キーワードを指定し、その後に、呼び出す関数を含む DLL の名前と場所を指定します。 Windows システム ディレクトリにあるファイルのパスを指定する必要はありません。  
  
 呼び出す関数の名前が有効な Visual Basic プロシージャ名ではない場合、またはアプリケーション内の他の項目の名前と競合する場合は、`Alias` キーワードを使用します。 呼び出す関数の名前を `Alias` で示します。  
  
#### <a name="argument-and-data-type-declarations"></a>引数とデータ型の宣言  
 引数とそのデータ型を宣言します。 Windows で使用されるデータ型は Visual Studio のデータ型に対応していないため、この部分は難しくなる可能性があります。 Visual Basic では、引数を互換性のあるデータ型に変換すること ("*マーシャリング*" と呼ばれるプロセス) によって、さまざまな処理が自動的に行われます。 <xref:System.Runtime.InteropServices> 名前空間に定義されている <xref:System.Runtime.InteropServices.MarshalAsAttribute> 属性を使用して、引数のマーシャリング方法を明示的に制御できます。  
  
> [!NOTE]
> 以前のバージョンの Visual Basic では、パラメーターを `As Any` と宣言することができました。これは、任意のデータ型のデータを使用できることを意味します。 Visual Basic では、すべての `Declare` ステートメントで特定のデータ型を使用する必要があります。  
  
#### <a name="windows-api-constants"></a>Windows API の定数  
 定数を組み合わせた引数もあります。 たとえば、このチュートリアルに示されている `MessageBox` API では、メッセージ ボックスの表示方法を制御する `Typ` という整数の引数を使用できます。 これらの定数の数値を確認するには、WinUser.h ファイルの `#define` ステートメントを調べます。 通常、数値は 16 進数で表示されるので、加算や 10 進数への変換には電卓を使用した方がよいかもしれません。 たとえば、感嘆符のスタイルを示す定数 `MB_ICONEXCLAMATION` 0x00000030 と、[はい] と [いいえ] のスタイルを示す定数 `MB_YESNO` 0x00000004 を組み合わせる場合は、これらの数値を加算して 0x00000034 または 10 進数の 52 という結果を得ることができます。 10 進数の結果を直接使用することもできますが、これらの値をアプリケーションで定数として宣言し、`Or` 演算子を使用して組み合わせることをお勧めします。  
  
##### <a name="to-declare-constants-for-windows-api-calls"></a>Windows API 呼び出しの定数を宣言するには  
  
1. 呼び出す Windows 関数のドキュメントを参照してください。 使用する定数の名前と、定数の数値が含まれている .h ファイルの名前を確認します。  
  
2. メモ帳などのテキスト エディターを使用してヘッダー (.h) ファイルの内容を表示し、使用する定数に関連付けられている値を見つけます。 たとえば、`MessageBox` API では、定数 `MB_ICONQUESTION` を使用して、メッセージ ボックスに疑問符を表示します。 `MB_ICONQUESTION` の定義は WinUser.h にあり、次のように表示されます。  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3. クラスまたはモジュールに同等の `Const` ステートメントを追加して、これらの定数をアプリケーションで使用できるようにします。 次に例を示します。  
  
     [!code-vb[VbVbalrInterop#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#11)]  
  
###### <a name="to-call-the-dll-procedure"></a>DLL プロシージャを呼び出すには  
  
1. `Button1` という名前のボタンをプロジェクトのスタートアップ フォームに追加し、それをダブルクリックしてコードを表示します。 そのボタンに対応するイベント ハンドラーが表示されます。  
  
2. 追加したボタンの `Click` イベント ハンドラーにコードを追加して、プロシージャを呼び出し、適切な引数を指定します。  
  
     [!code-vb[VbVbalrInterop#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#12)]  
  
3. F5 キーを押して、プロジェクトを実行します。 メッセージ ボックスに **Yes** と **No** の両方の応答ボタンが表示されます。 どちらかをクリックします。  
  
#### <a name="data-marshaling"></a>データ マーシャリング  
 Visual Basic では、パラメーターと戻り値のデータ型が Windows API 呼び出し用に自動的に変換されますが、`MarshalAs` 属性を使用すると、API で想定されるアンマネージド データ型を明示的に指定できます。 相互運用マーシャリングの詳細については、「[相互運用マーシャリング](../../../framework/interop/interop-marshaling.md)」を参照してください。  
  
##### <a name="to-use-declare-and-marshalas-in-an-api-call"></a>API 呼び出しで Declare と MarshalAs を使用するには  
  
1. 呼び出す関数の名前と引数、データ型、戻り値を特定します。  
  
2. `MarshalAs` 属性へのアクセスを簡単にするために、次の例に示すように、クラスまたはモジュールのコードの先頭に `Imports` ステートメントを追加します。  
  
     [!code-vb[VbVbalrInterop#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#13)]  
  
3. 使用するクラスまたはモジュールに、インポートされる関数の関数プロトタイプを追加し、`MarshalAs` 属性をパラメーターまたは戻り値に適用します。 次の例では、型 `void*` が想定される API 呼び出しを `AsAny` としてマーシャリングしています。  
  
     [!code-vb[VbVbalrInterop#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#14)]  
  
## <a name="api-calls-using-dllimport"></a>DllImport を使用した API 呼び出し  
 `DllImport` 属性により、タイプ ライブラリを使用せずに DLL 内の関数を呼び出す第 2 の方法が提供されます。 `DllImport` は `Declare` ステートメントを使用するのとほぼ同等ですが、関数の呼び出し方法をより詳細に制御できます。  
  
 `DllImport` は、ほとんどの Windows API 呼び出しで使用できます。ただし、その呼び出しで共有 ("*静的*" とも呼ばれる) メソッドを参照している場合に限ります。 クラスのインスタンスを必要とするメソッドは使用できません。 `Declare` ステートメントとは異なり、`DllImport` 呼び出しでは `MarshalAs` 属性を使用できません。  
  
### <a name="to-call-a-windows-api-using-the-dllimport-attribute"></a>DllImport 属性を使用して Windows API を呼び出すには  
  
1. **[ファイル]** メニューの **[新規作成]** をクリックし、次に **[プロジェクト]** をクリックして、新しい Windows アプリケーション プロジェクトを開きます。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2. Visual Basic プロジェクト テンプレートの一覧から **[Windows アプリケーション]** を選択します。 新しいプロジェクトが表示されます。  
  
3. `Button2` という名前のボタンをスタートアップ フォームに追加します。  
  
4. `Button2` をダブルクリックして、フォームのコード ビューを開きます。  
  
5. `DllImport` へのアクセスを簡単にするために、スタートアップ フォーム クラスのコードの先頭に `Imports` ステートメントを追加します。  
  
     [!code-vb[VbVbalrInterop#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#13)]  
  
6. フォームの `End Class` ステートメントの前に空の関数を宣言し、その関数に `MoveFile` という名前を指定します。  
  
7. 関数宣言に `Public` および `Shared` 修飾子を適用し、Windows API 関数で使用される引数に基づいて `MoveFile` のパラメーターを設定します。  
  
     [!code-vb[VbVbalrInterop#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#16)]  
  
     ご自身の関数には任意の有効なプロシージャ名を使用できます。`DllImport` 属性で、DLL 内の名前を指定します。 また、それによってパラメーターと戻り値の相互運用マーシャリングも処理されるため、API で使用されているデータ型に似た Visual Studio データ型を選択できます。  
  
8. 空のクラスに `DllImport` 属性を適用します。 最初のパラメーターは、呼び出す関数を含む DLL の名前と場所です。 Windows システム ディレクトリにあるファイルのパスを指定する必要はありません。 2 番目のパラメーターは、Windows API 内の関数の名前を指定する名前付き引数です。 この例では、`DllImport` 属性によって、`MoveFile` への呼び出しを KERNEL32.DLL 内の `MoveFileW` に強制的に転送しています。 `MoveFileW` メソッドにより、`src` パスから `dst` パスにファイルをコピーします。  
  
     [!code-vb[VbVbalrInterop#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#17)]  
  
9. 関数を呼び出すコードを `Button2_Click` イベント ハンドラーに追加します。  
  
     [!code-vb[VbVbalrInterop#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#18)]  
  
10. Test.txt という名前のファイルを作成し、ハード ドライブの C:\Tmp ディレクトリに配置します。 Tmp ディレクトリは、必要に応じて作成してください。  
  
11. F5 キーを押してアプリケーションを起動します。 メイン フォームが表示されます。  
  
12. **[Button2]** をクリックします。 ファイルを移動できた場合、"ファイルが正常に移動しました" というメッセージが表示されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Declare ステートメント](../../language-reference/statements/declare-statement.md)
- [Auto](../../language-reference/modifiers/auto.md)
- [Alias](../../language-reference/statements/alias-clause.md)
- [COM 相互運用](index.md)
- [マネージド コードでのプロトタイプの作成](../../../framework/interop/creating-prototypes-in-managed-code.md)
- [コールバック メソッドとしてのデリゲートのマーシャ リング](../../../framework/interop/marshaling-a-delegate-as-a-callback-method.md)
