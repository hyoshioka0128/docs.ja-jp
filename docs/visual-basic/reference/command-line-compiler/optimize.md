---
title: -optimize
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: 337cb794ef9a405a178f1998cbe27b5da7709382
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397442"
---
# <a name="-optimize"></a>-optimize
コンパイラ最適化を有効または無効にします。  
  
## <a name="syntax"></a>構文  
  
```console  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`+` &#124; `-`|任意。 `-optimize-` オプションにより、コンパイラ最適化が無効になります。 `-optimize+` オプションにより、最適化が有効になります。 既定では、最適化が無効になります。|  
  
## <a name="remarks"></a>Remarks  
 コンパイラを最適化すると、出力ファイルのサイズが小さくなり、動作が速くなり、処理の効率が向上します。 ただし、最適化によって出力ファイル内のコードの配置が変更されるため、`-optimize+` を使用するとデバッグが困難になる可能性があります。  
  
 `-target:module` で生成されるアセンブリのすべてのモジュールには、アセンブリと同じ `-optimize` 設定を使用する必要があります。 詳細については、「[-target (Visual Basic)](target.md)」を参照してください。  
  
 `-optimize` オプションと `-debug` オプションを組み合わせることができます。  
  
|Visual Studio 統合開発環境で -optimize を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。<br />     <br />2. **[コンパイル]** タブをクリックします。<br />3. **[詳細設定]** ボタンをクリックします。<br />4. **[最適化を有効にする]** チェック ボックスを変更します。|  
  
## <a name="example"></a>例  
 次のコードでは、`T2.vb` がコンパイルされ、コンパイラの最適化が有効になります。  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-debug (Visual Basic)](debug.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [-target (Visual Basic)](target.md)
