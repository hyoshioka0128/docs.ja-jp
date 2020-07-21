---
title: '方法: オーバーロードされたプロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], overloading
- procedures [Visual Basic], calling
- procedures [Visual Basic], multiple versions
- procedure calls [Visual Basic], overloaded
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
ms.openlocfilehash: de101309fa1edaaddc3defc5759d9293fbef684c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388544"
---
# <a name="how-to-call-an-overloaded-procedure-visual-basic"></a>方法: オーバーロードされたプロシージャを呼び出す (Visual Basic)
プロシージャをオーバーロードする利点は、呼び出しの柔軟性にあります。 呼び出し元のコードは、プロシージャに渡す必要がある情報を取得し、渡す引数に関係なく、1 つのプロシージャ名を呼び出すことができます。  
  
### <a name="to-call-a-procedure-that-has-more-than-one-version-defined"></a>複数のバージョンが定義されているプロシージャを呼び出すには  
  
1. 呼び出し元のコードで、プロシージャに渡すデータを決定します。  
  
2. 引数リストにデータを提示して、通常の方法でプロシージャ呼び出しを記述します。 引数が、プロシージャに対して定義されているいずれかのバージョンのパラメーター リストと一致していることを確認してください。  
  
3. 呼び出すプロシージャのバージョンを決定する必要はありません。 Visual Basic によって、引数リストと一致するバージョンに制御が渡されます。  
  
     次の例では、`post` プロシージャを呼び出します。これは「[方法:プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)」で定義されています。 顧客 ID を取得し、それが `String` か `Integer` かを判断して、どちらの場合でも同じプロシージャを呼び出します。  
  
     [!code-vb[VbVbcnProcedures#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#56)]  
  
     [!code-vb[VbVbcnProcedures#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#57)]  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)
- [オーバーロードの解決](./overload-resolution.md)
- [Overloads](../../../language-reference/modifiers/overloads.md)
