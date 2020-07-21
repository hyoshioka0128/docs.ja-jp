---
title: '方法: Windows API を呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- API calls [Visual Basic]
- Windows API, calling
- API calls [Visual Basic], platform invoke
- calls [Visual Basic], stored procedures
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
ms.openlocfilehash: 2c3bb599b79575180eb2b0ec89453f01901f94c0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396844"
---
# <a name="how-to-call-windows-apis-visual-basic"></a>方法: Windows API を呼び出す (Visual Basic)
この例では、`MessageBox` 関数を user32.dll に定義して呼び出し、文字列を関数に渡します。  
  
## <a name="example"></a>例  
 [!code-vb[VbVbalrInterop#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#1)]  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System> 名前空間への参照  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- メソッドが静的ではない、抽象である、または以前に定義されています。 親の型がインターフェイスであるか、*name* または *dllName* の長さが 0 です。 (<xref:System.ArgumentException>)  
  
- *name* または *dllName* が `Nothing` です。 (<xref:System.ArgumentNullException>)  
  
- 含んでいる型が `CreateType` を使用して以前に作成されています。 (<xref:System.InvalidOperationException>)  
  
## <a name="see-also"></a>関連項目

- [プラットフォーム呼び出しの詳細](../../../framework/interop/consuming-unmanaged-dll-functions.md#a-closer-look-at-platform-invoke)
- [プラットフォーム呼び出しの例](../../../framework/interop/platform-invoke-examples.md)
- [アンマネージ DLL 関数の処理](../../../framework/interop/consuming-unmanaged-dll-functions.md)
- [リフレクション出力によるメソッドの定義](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w63y4d4f(v=vs.100))
- [チュートリアル: Windows API の呼び出し](walkthrough-calling-windows-apis.md)
- [COM 相互運用](index.md)
