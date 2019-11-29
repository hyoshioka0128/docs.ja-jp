---
title: '方法: Windows API を呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- API calls [Visual Basic]
- Windows API, calling
- API calls [Visual Basic], platform invoke
- calls [Visual Basic], stored procedures
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
ms.openlocfilehash: 6f3c53243d7aeb73be81796d5ca185c3a3c41c72
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348707"
---
# <a name="how-to-call-windows-apis-visual-basic"></a>方法: Windows API を呼び出す (Visual Basic)
この例では、user32.dll で `MessageBox` 関数を定義して呼び出し、その関数に文字列を渡します。  
  
## <a name="example"></a>例  
 [!code-vb[VbVbalrInterop#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System> 名前空間への参照  
  
## <a name="robust-programming"></a>堅牢性の高いプログラミング  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- メソッドが静的でない、または抽象メソッドである、または以前に定義されているメソッドの場合。 親の型がインターフェイスであるか、または*名前*または*dllName*の長さが0です。 (<xref:System.ArgumentException>)  
  
- *名前*または*dllName*が `Nothing`。 (<xref:System.ArgumentNullException>)  
  
- 含んでいる型が `CreateType` を使用して以前に作成されています。 (<xref:System.InvalidOperationException>)  
  
## <a name="see-also"></a>参照

- [プラットフォーム呼び出しの詳細](../../../framework/interop/consuming-unmanaged-dll-functions.md#a-closer-look-at-platform-invoke)
- [プラットフォーム呼び出しの例](../../../framework/interop/platform-invoke-examples.md)
- [アンマネージ DLL 関数の処理](../../../framework/interop/consuming-unmanaged-dll-functions.md)
- [リフレクション出力によるメソッドの定義](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w63y4d4f(v=vs.100))
- [チュートリアル : Windows API の呼び出し](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
- [COM 相互運用](../../../visual-basic/programming-guide/com-interop/index.md)
