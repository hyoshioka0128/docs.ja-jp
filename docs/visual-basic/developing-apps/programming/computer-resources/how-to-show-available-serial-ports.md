---
title: '方法 : 利用可能なシリアル ポートを表示する'
ms.date: 07/20/2015
helpviewer_keywords:
- serial ports, availability
- My.Computer.Ports.SerialPortNames property
- My.Computer.Ports object
- ports, serial port availability
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
ms.openlocfilehash: e7a9166f1879ed0850ca893bed307a0318298bbb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401824"
---
# <a name="how-to-show-available-serial-ports-in-visual-basic"></a>方法 : Visual Basic で利用可能なシリアル ポートを表示する

このトピックでは、`My.Computer.Ports` を使用して、コンピューターで利用可能なシリアルポートを Visual Basic で表示する方法について説明します。  
  
 使用するポートをユーザーが選択可能とするために、シリアル ポートの名前を <xref:System.Windows.Forms.ListBox> コントロールに格納します。  
  
## <a name="example"></a>例  

 次の例では、`My.Computer.Ports.SerialPortNames` プロパティが返す文字列のすべてについてループします。 これらの文字列は、コンピューターで利用可能なシリアル ポートの名前です。  
  
 通常、利用可能なポートの一覧から、アプリケーションで使用するシリアル ポートをユーザーが選択します。 この例では、シリアル ポート名は <xref:System.Windows.Forms.ListBox> コントロールに格納されます。 詳細については、「[ListBox コントロール](../../../../framework/winforms/controls/listbox-control-windows-forms.md)」を参照してください。  
  
 [!code-vb[VbVbalrMyComputer#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#45)]  
  
 このコード例は IntelliSense コード スニペットとしても利用できます。 コード スニペット ピッカーでは、これは **[接続とネットワーク]** にあります。 詳細については、「 [Code Snippets](/visualstudio/ide/code-snippets)」を参照してください。  
  
## <a name="compiling-the-code"></a>コードのコンパイル  

 この例で必要な要素は次のとおりです。  
  
- System.Windows.Forms.dll へのプロジェクト参照が必要です。  
  
- <xref:System.Windows.Forms> 名前空間のメンバーへのアクセス許可。 コード内でメンバー名を完全修飾していない場合は、`Imports` ステートメントを追加します。 詳細については、「[Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)」を参照してください。  
  
- `ListBox1` という名前の <xref:System.Windows.Forms.ListBox> コントロールを持つフォーム。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  

 利用可能なシリアル ポートの名前を表示するために、<xref:System.Windows.Forms.ListBox> コントロールを使用する必要はありません。 代わりに、<xref:System.Windows.Forms.ComboBox> やその他のコントロールを使用できます。 ユーザーからの応答が不要なアプリケーションの場合、<xref:System.Windows.Forms.TextBox> コントロールを使用して情報を表示できます。  
  
> [!NOTE]
> Windows 98 の実行時には、`My.Computer.Ports.SerialPortNames` が返すポート名が正しくない場合があります。 アプリケーション エラーを防ぐには、ポート名を使用してポートを開くときに、`Try...Catch...Finally` ステートメントや `Using` ステートメントなどの例外処理を使用します。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [方法 : シリアル ポートに接続されているモデムをダイヤルする](how-to-dial-modems-attached-to-serial-ports.md)
- [方法 : シリアル ポートに文字列を送信する](how-to-send-strings-to-serial-ports.md)
- [方法 : シリアル ポートから文字列を受信する](how-to-receive-strings-from-serial-ports.md)
