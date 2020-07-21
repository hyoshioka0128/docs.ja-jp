---
title: 定数と列挙体
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
- constants [Visual Basic]
- constants [Visual Basic], list of
ms.assetid: 309c0ad5-83e4-4f96-99ea-83cd95107417
ms.openlocfilehash: 60cd1ddac9bca685ddc5778e7d289710245a183e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374487"
---
# <a name="constants-and-enumerations-visual-basic"></a>定数と列挙型 (Visual Basic)

Visual Basic には、開発者向けの定義済み定数と列挙型が多数用意されています。 定数に格納された値は、アプリケーションの実行中に変わることはありません。 一連の関連する定数を操作する場合や、定数値に名前を関連付ける場合は、列挙型を使うと便利です。  
  
## <a name="constants"></a>定数  
  
### <a name="conditional-compilation-constants"></a>条件付きコンパイル定数  

 次の表は、条件付きコンパイルで使用できる定義済み定数の一覧を示しています。  
  
|**定数**|**説明**|  
|---|---|  
|`CONFIG`|**構成マネージャー**の **[アクティブ ソリューション構成]** ボックスの現在の設定に対応する文字列。|  
|`DEBUG`|**[プロジェクト プロパティ]** ダイアログ ボックスで設定できる `Boolean` 値。 既定では、プロジェクトのデバッグ構成によって `DEBUG` が定義されます。 `DEBUG` を定義すると、<xref:System.Diagnostics.Debug> クラスのメソッドは **[出力]** ウィンドウに出力を生成します。 これを定義しない場合、<xref:System.Diagnostics.Debug> クラスのメソッドはコンパイルされず、デバッグ出力も生成されません。|  
|`TARGET`|プロジェクトの出力の種類、またはコマンド ラインの **-target** オプションの設定を表す文字列。 `TARGET` に指定できる値は次のとおりです。<br /><br /> - Windows アプリケーションの場合は "winexe"。<br />- コンソール アプリケーションの場合は "exe"。<br />- クラス ライブラリの場合は "library"。<br />- モジュールの場合は "module"。<br />- **-target** オプションは、Visual Studio 統合開発環境で設定できます。 詳細については、「[-target (Visual Basic)](../reference/command-line-compiler/target.md)」を参照してください。|  
|`TRACE`|**[プロジェクト プロパティ]** ダイアログ ボックスで設定できる `Boolean` 値。 既定では、プロジェクトのすべての構成で `TRACE` が定義されます。 `TRACE` を定義すると、<xref:System.Diagnostics.Trace> クラスのメソッドは **[出力]** ウィンドウに出力を生成します。 これを定義しない場合、<xref:System.Diagnostics.Trace> クラスのメソッドはコンパイルされず、`Trace` 出力も生成されません。|  
|`VBC_VER`|Visual Basic のバージョンを "*major*.*minor*" のフォーマットで表す番号。|  
  
### <a name="print-and-display-constants"></a>印刷定数と表示定数  

 印刷と表示の関数を呼び出す場合、実際の値の代わりに、次の定数をコードで使用できます。  
  
|**定数**|**説明**|  
|---|---|  
|`vbCrLf`|復帰/ラインフィード文字の組み合わせ。|  
|`vbCr`|復帰文字。|  
|`vbLf`|ラインフィード文字。|  
|`vbNewLine`|改行文字。|  
|`vbNullChar`|NULL 文字。|  
|`vbNullString`|長さ 0 の文字列 ("") と同じではありません。外部プロシージャの呼び出しに使用します。|  
|`vbObjectError`|エラー番号。 ユーザー定義のエラー番号は、この値より大きい必要があります。 次に例を示します。<br /><br /> `Err.Raise(Number) = vbObjectError + 1000`|  
|`vbTab`|タブ文字。|  
|`vbBack`|バックスペース文字。|  
|`vbFormFeed`|Microsoft Windows では使用されません。|  
|`vbVerticalTab`|Microsoft Windows では有用ではありません。|  
  
## <a name="enumerations"></a>列挙  

 次の表に、Visual Basic によって提供される列挙の一覧とその説明を示します。  
  
|列挙|説明|  
|---|---|  
|<xref:Microsoft.VisualBasic.AppWinStyle>|<xref:Microsoft.VisualBasic.Interaction.Shell%2A> 関数の呼び出し時に起動されるプログラムに使用するウィンドウ スタイルを示します。|  
|<xref:Microsoft.VisualBasic.AudioPlayMode>|オーディオ メソッドを呼び出すときにサウンドを再生する方法を示します。|  
|<xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole>|<xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A> メソッドを呼び出すときに確認するロールの種類を示します。|  
|<xref:Microsoft.VisualBasic.CallType>|<xref:Microsoft.VisualBasic.Interaction.CallByName%2A> 関数を呼び出すときに呼び出されるプロシージャの種類を示します。|  
|<xref:Microsoft.VisualBasic.CompareMethod>|比較関数を呼び出すときの文字列の比較方法を示します。|  
|<xref:Microsoft.VisualBasic.DateFormat>|<xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A> 関数を呼び出すときの日付の表示方法を示します。|  
|<xref:Microsoft.VisualBasic.DateInterval>|日付関連の関数を呼び出すときに使用する、日付の間隔の決定方法と形式の設定方法を示します。|  
|<xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption>|削除するディレクトリにファイルまたはディレクトリが含まれている場合に実行する操作を指定します。|  
|<xref:Microsoft.VisualBasic.DueDate>|財務メソッドを呼び出すときの支払期日を示します。|  
|<xref:Microsoft.VisualBasic.FileIO.FieldType>|テキスト フィールドを区切って指定するか、固定幅にするかを示します。|  
|<xref:Microsoft.VisualBasic.FileAttribute>|ファイル アクセス関数を呼び出すときに使用するファイル属性を示します。|  
|<xref:Microsoft.VisualBasic.FirstDayOfWeek>|日付関連の関数を呼び出すときに使用する週の最初の曜日を示します。|  
|<xref:Microsoft.VisualBasic.FirstWeekOfYear>|日付関連の関数を呼び出すときに使用する年の最初の週を示します。|  
|<xref:Microsoft.VisualBasic.MsgBoxResult>|<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 関数によって返され、メッセージ ボックスのどのボタンが押されたかを示します。|  
|<xref:Microsoft.VisualBasic.MsgBoxStyle>|<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 関数を呼び出すときに表示するボタンを示します。|  
|<xref:Microsoft.VisualBasic.OpenAccess>|ファイル アクセス関数を呼び出すときにファイルを開く方法を示します。|  
|<xref:Microsoft.VisualBasic.OpenMode>|ファイル アクセス関数を呼び出すときにファイルを開く方法を示します。|  
|<xref:Microsoft.VisualBasic.OpenShare>|ファイル アクセス関数を呼び出すときにファイルを開く方法を示します。|  
|<xref:Microsoft.VisualBasic.FileIO.RecycleOption>|ファイルを完全に削除するか、ごみ箱に移動するかを指定します。|  
|<xref:Microsoft.VisualBasic.FileIO.SearchOption>|すべてのディレクトリを検索するか最上位ディレクトリのみを検索するかを指定します。|  
|<xref:Microsoft.VisualBasic.TriState>|数値書式指定関数を呼び出すときに、`Boolean` 値を示すか、または既定値を使用する必要があるかどうかを示します。|  
|<xref:Microsoft.VisualBasic.FileIO.UICancelOption>|操作中にユーザーが **[キャンセル]** をクリックした場合の処理を指定します。|  
|<xref:Microsoft.VisualBasic.FileIO.UIOption>|ファイルまたはディレクトリをコピー、削除、移動するときに進行状況ダイアログを表示するかどうかを指定します。|  
|<xref:Microsoft.VisualBasic.VariantType>|<xref:Microsoft.VisualBasic.Information.VarType%2A> 関数によって返されるバリアント オブジェクトの型を示します。|  
|<xref:Microsoft.VisualBasic.VbStrConv>|<xref:Microsoft.VisualBasic.Strings.StrConv%2A> 関数の呼び出しで実行する変換の種類を示します。|  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の言語リファレンス](index.md)
- [定数の概要](../programming-guide/language-features/constants-enums/constants-overview.md)
- [列挙型の概要](../programming-guide/language-features/constants-enums/enumerations-overview.md)
