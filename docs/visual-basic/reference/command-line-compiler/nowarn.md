---
title: -nowarn
ms.date: 07/20/2015
helpviewer_keywords:
- nowarn compiler option [Visual Basic]
- /nowarn compiler option [Visual Basic]
- -nowarn compiler option [Visual Basic]
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
ms.openlocfilehash: 37851f99eb88543e939ce48995ded41958e57cc3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397489"
---
# <a name="-nowarn"></a>-nowarn
警告を生成するコンパイラの機能を無効にします。  
  
## <a name="syntax"></a>構文  
  
```console  
-nowarn[:numberList]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`numberList`|任意。 コンパイラにより非表示にされるべき警告 ID 番号のコンマ区切りの一覧。 警告 ID が指定されていない場合、すべての警告は非表示になります。|  
  
## <a name="remarks"></a>Remarks  
 `-nowarn` オプションを指定すると、コンパイラにより警告が生成されなくなります。 個々の警告を非表示にするには、`-nowarn` オプションの後にコロンを追加し、警告 ID を指定します。 警告が複数ある場合は、番号をコンマで区切ります。  
  
 警告 ID は、数値部分のみを指定します。 たとえば、BC42024 を非表示にする場合は、使用されていないローカル変数の警告に、`-nowarn:42024` を指定します。  
  
 警告 ID の番号の詳細については、「[Visual Basic での警告の構成](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
|Visual Studio 統合開発環境で -nowarn を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3.警告をすべて無効にするには、 **[すべての警告を表示しない]** チェック ボックスをオンにします。<br />     または<br />     特定の警告を無効にするには、その警告の隣のドロップダウン リストから **[なし]** をクリックします。|  
  
## <a name="example"></a>例  
 次のコードでは `T2.vb` がコンパイルされ、警告が表示されません。  
  
```console
vbc -nowarn t2.vb  
```  
  
## <a name="example"></a>例  
 次のコードでは `T2.vb` がコンパイルされ、使用されていないローカル変数 (42024) の警告が表示されません。  
  
```console
vbc -nowarn:42024 t2.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
