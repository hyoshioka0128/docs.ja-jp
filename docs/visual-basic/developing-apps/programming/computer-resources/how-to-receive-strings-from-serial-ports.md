---
title: '方法 : シリアル ポートから文字列を受信する'
ms.date: 07/20/2015
helpviewer_keywords:
- serial ports, retrieving strings
- strings [Visual Basic], retrieving from serial ports
- My.Resources object
ms.assetid: 8371ce2c-e1c7-476b-a86d-9afc2614b6b7
ms.openlocfilehash: 93b6b47d89d05331c85a6459bba7d6fd5e2e3377
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401837"
---
# <a name="how-to-receive-strings-from-serial-ports-in-visual-basic"></a>方法 : Visual Basic でシリアル ポートから文字列を受信する

このトピックでは、Visual Basic で `My.Computer.Ports` を使用して、コンピューターのシリアル ポートから文字列を受信する方法について説明します。  
  
### <a name="to-receive-strings-from-the-serial-port"></a>シリアル ポートから文字列を受信する  
  
1. 戻り値の文字列を初期化します。  
  
     [!code-vb[VbVbalrMyComputer#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#38)]  
  
2. どのシリアル ポートから文字列を取得するのかを決定します。 この例では、`COM1` です。  
  
3. `My.Computer.Ports.OpenSerialPort` メソッドを使用して、ポートへの参照を取得します。 詳細については、<xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> を参照してください。  
  
     `Try...Catch...Finally` ブロックを使用すると、アプリケーションが例外を生成した場合でも、シリアル ポートを閉じることができます。 シリアル ポートを操作するコードはすべて、このブロック内に記述する必要があります。  
  
     [!code-vb[VbVbalrMyComputer#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#39)]  
  
4. 利用可能な行がなくなるまでテキスト行を読み取るための `Do` ループを作成します。  
  
     [!code-vb[VbVbalrMyComputer#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#40)]  
  
5. <xref:System.IO.Ports.SerialPort.ReadLine> メソッドを使用して、次に利用可能なテキスト行をシリアル ポートから読み取ります。  
  
     [!code-vb[VbVbalrMyComputer#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#41)]  
  
6. `If` ステートメントを使用して、<xref:System.IO.Ports.SerialPort.ReadLine> メソッドが `Nothing` を返す (つまり、利用可能なテキストがこれ以上ない) かどうかを確認します。 `Nothing` を返した場合は、`Do` ループを終了します。  
  
     [!code-vb[VbVbalrMyComputer#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#42)]  
  
7. `If` ステートメントに `Else` ブロックを追加して、文字列が実際に読み取られた場合のケースを処理します。 このブロックによって、シリアル ポートからの文字列を戻り値の文字列に追加します。  
  
     [!code-vb[VbVbalrMyComputer#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#43)]  
  
8. 文字列を返します。  
  
     [!code-vb[VbVbalrMyComputer#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#44)]  
  
## <a name="example"></a>例  

 [!code-vb[VbVbalrMyComputer#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#37)]  
  
 このコード例は IntelliSense コード スニペットとしても利用できます。 コード スニペット ピッカーでは、これは **[接続とネットワーク]** にあります。 詳細については、「 [Code Snippets](/visualstudio/ide/code-snippets)」を参照してください。  
  
## <a name="compiling-the-code"></a>コードのコンパイル  

 この例では、コンピューターが `COM1` を使用しているものと想定しています。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  

 この例では、コンピューターが `COM1` を使用しているものと想定しています。 柔軟性を高めるためには、利用可能なポートの一覧から目的のシリアル ポートを選択できるようにコードを作成する必要があります。 詳細については、「[方法: 利用可能なシリアル ポートを表示する](how-to-show-available-serial-ports.md)」を参照してください。  
  
 この例では、アプリケーションによってポートが閉じられ、タイムアウト例外がキャッチされるようにするために、`Try...Catch...Finally` ブロックを使用しています。 詳しくは、「[Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)」をご覧ください。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Devices.Ports>
- <xref:System.IO.Ports.SerialPort?displayProperty=nameWithType>
- [方法 : シリアル ポートに接続されているモデムをダイヤルする](how-to-dial-modems-attached-to-serial-ports.md)
- [方法 : シリアル ポートに文字列を送信する](how-to-send-strings-to-serial-ports.md)
- [方法 : 利用可能なシリアル ポートを表示する](how-to-show-available-serial-ports.md)
