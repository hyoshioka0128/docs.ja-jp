---
title: -baseaddress
ms.date: 08/09/2018
f1_keywords:
- /baseaddress
- baseaddress
helpviewer_keywords:
- -baseaddress compiler option [Visual Basic]
- /baseaddress compiler option [Visual Basic]
- baseaddress compiler option [Visual Basic]
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
ms.openlocfilehash: d241584195da7d6f74b45b191c4f63204c200d45
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357181"
---
# <a name="-baseaddress"></a>-baseaddress
DLL を作成するときの既定のベース アドレスを指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-baseaddress:address  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`address`|必須です。 DLL のベース アドレス。 このアドレスは 16 進数として指定する必要があります。|  
  
## <a name="remarks"></a>Remarks  
 DLL の既定のベース アドレスは、.NET Framework により設定されます。  
  
 このアドレスの下位ワードは丸められることにご注意ください。 たとえば、0x11110001 と指定すると、丸められて 0x11110000 になります。  
  
 DLL の署名プロセスを完了するには、厳密名ツール (Sn.exe) の `–R` オプションを使用します。  
  
 ターゲットが DLL でない場合、このオプションは無視されます。  
  
|Visual Studio IDE で -baseaddress を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3. **[詳細設定]** をクリックします。<br />4. **[DLL ベース アドレス]** ボックスの値を変更します。 **注:**    **[DLL ベース アドレス]** ボックスは、ターゲットが DLL の場合を除き、読み取り専用です。|  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-target (Visual Basic)](target.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Sn.exe (厳密名ツール)](../../../framework/tools/sn-exe-strong-name-tool.md)
