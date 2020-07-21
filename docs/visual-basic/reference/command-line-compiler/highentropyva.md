---
title: -highentropyva
ms.date: 03/10/2018
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
ms.openlocfilehash: 9501ea46eb13baa171208e20d0c9645d118c4301
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408622"
---
# <a name="-highentropyva-visual-basic"></a>-highentropyva (Visual Basic)
64 ビットの実行可能ファイルまたは [platform:anycpu](platform.md) コンパイラ オプションによってマークされた実行可能ファイルが、高エントロピ Address Space Layout Randomization (ASLR) をサポートするかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```console  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>引数  
 `+` &#124; `-`  
 任意。 このオプションは、既定でまたは `-highentropyva-` を指定した場合はオフになっています。 `-highentropyva` または `-highentropyva+` を指定した場合、オプションはオンになります。  
  
## <a name="remarks"></a>Remarks  
 このオプションを指定すると、適合するバージョンの Windows カーネルで、ASLR の一環としてプロセスのアドレス空間レイアウトをカーネルでランダム化する際、より高いエントロピを使用できるようになります。 カーネルでより高いエントロピが使用される場合は、スタックやヒープなどのメモリ領域により多くのアドレスを割り当てることができます。 これによって特定のメモリ領域の位置を推測しづらくなる効果が得られます。  
  
 このオプションがオンになっている場合、ターゲットの実行可能ファイルとそれが依存するモジュールは、これらのモジュールが 64 ビット プロセスとして実行されている際に、4 ギガバイト (GB) を超えるポインター値を処理できる必要があります。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
