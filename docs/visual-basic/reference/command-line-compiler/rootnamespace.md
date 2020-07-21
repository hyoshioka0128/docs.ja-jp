---
title: -rootnamespace
ms.date: 03/13/2018
f1_keywords:
- /rootnamespace
- rootnamespace
helpviewer_keywords:
- /rootnamespace compiler option [Visual Basic]
- -rootnamespace compiler option [Visual Basic]
- rootnamespace compiler option [Visual Basic]
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
ms.openlocfilehash: b6a2f3ba0772d8f8c8c6a762a1be01703d21b778
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403136"
---
# <a name="-rootnamespace"></a>-rootnamespace
すべての型宣言に対して名前空間を指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-rootnamespace:namespace  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`namespace`|現在のプロジェクトのすべての型宣言を囲む名前空間の名前。|  
  
## <a name="remarks"></a>Remarks  
 Visual Studio 統合開発環境で作成したプロジェクトをコンパイルするのに Visual studio の実行可能ファイル (Devenv.exe) を使用する場合は、`-rootnamespace` を使用して <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> プロパティの値を指定します。 詳細については、「[Devenv コマンド ライン スイッチ](/visualstudio/ide/reference/devenv-command-line-switches)」を参照してください。  
  
 共通言語ランタイムの MSIL 逆アセンブラー (`Ildasm.exe`) を使用して、出力ファイル内に名前空間の名前を示します。  
  
|Visual Studio 統合開発環境で -rootnamespace を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[アプリケーション]** タブをクリックします。<br />3. **[ルート名前空間]** ボックス内の値を変更します。|  
  
## <a name="example"></a>例  
 次のコードでは、`In.vb` がコンパイルされ、すべての型宣言が名前空間 `mynamespace` で囲まれます。  
  
```console
vbc -rootnamespace:mynamespace in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [Ildasm.exe (IL 逆アセンブラー)](../../../framework/tools/ildasm-exe-il-disassembler.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
