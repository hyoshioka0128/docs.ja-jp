---
title: クラスがオートメーションをサポートしていないか、必要なインターフェイスをサポートしていません。
ms.date: 07/20/2015
f1_keywords:
- vbrID430
ms.assetid: d985bb7e-e48e-443e-86f2-ddb86758757c
ms.openlocfilehash: 856c3f5ef503a7e5919e9e602532c56d9557482f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415402"
---
# <a name="class-does-not-support-automation-or-does-not-support-expected-interface"></a>クラスがオートメーションをサポートしていないか、必要なインターフェイスをサポートしていません。
`GetObject` 関数呼び出しまたは `CreateObject` 関数呼び出しで指定したクラスが外部からプログラム可能なインターフェイスを公開していません。あるいは、.dll から .exe へ、または .exe から .dll へプロジェクトを変更しました。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. オブジェクトを作成したアプリケーションのドキュメントを参照して、このクラスのオブジェクトでオートメーションを使用する上での制限を確認します。  
  
2. .dll から .exe へ、または .exe から .dll へプロジェクトを変更した場合は、古い .dll または .exe を手動で登録解除する必要があります。  
  
## <a name="see-also"></a>関連項目

- [エラーの種類](../../programming-guide/language-features/error-types.md)
- [ご意見](/visualstudio/ide/feedback-options)
