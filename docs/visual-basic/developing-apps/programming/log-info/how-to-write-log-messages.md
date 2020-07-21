---
title: '方法: ログ メッセージを書き込む'
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application.Log object, writing log messages
ms.assetid: 972a3e0c-2996-4623-a7a9-d7ebc4d207f8
ms.openlocfilehash: 28c5fe77e2711dfcac96e621a90fb9506eb74775
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410050"
---
# <a name="how-to-write-log-messages-visual-basic"></a>方法: ログ メッセージを書き込む (Visual Basic)

`My.Application.Log` オブジェクトおよび `My.Log` オブジェクトを使用すると、アプリケーションに関する情報をログに記録できます。 この例では、 `My.Application.Log.WriteEntry` メソッドを使用してトレース情報をログに記録する方法を示します。

例外情報をログに記録するには、`My.Application.Log.WriteException` メソッドを使います。方法については、「[方法 : 例外をログに記録する](how-to-log-exceptions.md)」をご覧ください。

## <a name="example"></a>例

この例では、 `My.Application.Log.WriteEntry` メソッドを使用してトレース情報を書き込みます。

[!code-vb[VbVbalrMyApplicationLog#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#11)]

## <a name="net-framework-security"></a>.NET Framework のセキュリティ

ログに書き込むデータに、ユーザーのパスワードなどの機密情報が含まれないように注意してください。 詳しくは、「[アプリケーション ログの使用](working-with-application-logs.md)」をご覧ください。

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [アプリケーション ログの使用](working-with-application-logs.md)
- [方法 : 例外をログに記録する](how-to-log-exceptions.md)
- [チュートリアル : My.Application.Log による情報の書き込み先の確認](walkthrough-determining-where-my-application-log-writes-information.md)
- [チュートリアル : My.Application.Log による情報の書き込み先の変更](walkthrough-changing-where-my-application-log-writes-information.md)
- [チュートリアル : My.Application.Log の出力をフィルター処理する](walkthrough-filtering-my-application-log-output.md)
