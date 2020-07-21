---
title: 'アセンブリ マニフェストを作成中にエラーが発生しました : <error message>'
ms.date: 07/20/2015
f1_keywords:
- bc30140
- vbc30140
helpviewer_keywords:
- BC30140
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
ms.openlocfilehash: 7ccfb970a0e471b4a7e6808f041dfea2f386e7e9
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197126"
---
# <a name="error-creating-assembly-manifest-error-message"></a>アセンブリ マニフェストを作成中にエラーが発生しました: \<error message>
Visual Basic コンパイラはアセンブリ リンカー (Al.exe、Alink とも呼ばれる) を呼び出し、マニフェストを伴うアセンブリを生成します。 リンカーが、アセンブリの生成前の段階でのエラーを報告しています。  
  
 指定したキー ファイルまたはキー コンテナーに原因がある場合があります。 アセンブリに完全署名するには、公開キーと秘密キーに関する情報を含む有効なキー ファイルを提供する必要があります。 アセンブリに遅延署名するには、 **[遅延署名のみ]** チェック ボックスをオンにし、公開キー情報を含む有効なキー ファイルを提供する必要があります。 アセンブリに遅延署名する場合、秘密キーは必要ありません。 詳細については、[厳密な名前でアセンブリに署名する](../../../standard/assembly/sign-strong-name.md)」を参照してください。  
  
 **エラー ID:** BC30140  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 引用符で囲まれたエラー メッセージを調べ、トピック「[Al.exe](../../../framework/tools/al-exe-assembly-linker.md)」で エラー AL1019 の詳細な説明とアドバイスを参照してください  
  
2. エラーが続く場合は、状況に関する情報を収集し、マイクロソフト プロダクト サポート サービスに通知してください。  
  
## <a name="see-also"></a>関連項目

- [方法: 厳密な名前でアセンブリに署名する](../../../standard/assembly/sign-strong-name.md)
- [[署名] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/signing-page-project-designer)
- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [ご意見](/visualstudio/ide/feedback-options)
