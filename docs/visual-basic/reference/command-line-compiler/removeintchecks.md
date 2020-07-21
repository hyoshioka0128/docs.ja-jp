---
title: -removeintchecks
ms.date: 03/13/2018
f1_keywords:
- removeintchecks
- -removeintchecks
helpviewer_keywords:
- removeintchecks compiler option [Visual Basic]
- /removeintchecks compiler option [Visual Basic]
- -removeintchecks compiler option [Visual Basic]
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
ms.openlocfilehash: ec4722cb7088819dae95ca1b7cbc1469d957a7aa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400475"
---
# <a name="-removeintchecks"></a>-removeintchecks
整数演算のオーバーフロー エラー チェックをオンまたはオフにします。  
  
## <a name="syntax"></a>構文  
  
```console  
-removeintchecks[+ | -]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`+` &#124; `-`|任意。 `-removeintchecks-` オプションを指定すると、すべての整数計算について、オーバーフロー エラーの有無がコンパイラでチェックされます。 既定値は、`-removeintchecks-` です。<br /><br /> `-removeintchecks` または `-removeintchecks+` を指定すると、エラー チェックが行われず、整数計算を高速にすることができます。 ただし、エラー チェックが行われず、データ型の容量がオーバーフローした場合は、エラーが発生することなく誤った結果が格納される可能性があります。|  
  
|Visual Studio 統合開発環境で -removeintchecks を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3. **[詳細設定]** ボタンをクリックします。<br />4. **[整数オーバーフローのチェックを解除]** ボックスの値を変更します。|  
  
## <a name="example"></a>例  
 次のコードでは、`Test.vb` がコンパイルされ、整数オーバーフロー エラーのチェックがオフにされます。  
  
```console
vbc -removeintchecks+ test.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
