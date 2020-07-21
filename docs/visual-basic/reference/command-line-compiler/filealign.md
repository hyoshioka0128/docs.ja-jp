---
title: -filealign
ms.date: 03/10/2018
helpviewer_keywords:
- sections compiler option [Visual Basic]
- alignment compiler option [Visual Basic]
- -filealign compiler option [Visual Basic]
- section alignment
- /filealign compiler option [Visual Basic]
- filealign compiler option [Visual Basic]
ms.assetid: cc61ec3d-ad38-4b28-9659-099d73cad099
ms.openlocfilehash: 3877757185030b0dba914a79d8c760fb8033ae5f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408648"
---
# <a name="-filealign"></a>-filealign
出力ファイルでセクションをアラインするサイズを指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>引数  
 `number`  
 必須です。 出力ファイルにセクションの配置を指定する値です。 有効値は 512、1024、2048、4096、および 8192 です。 これらの値はバイト単位です。  
  
## <a name="remarks"></a>Remarks  
 `-filealign` オプションは、ご自分の出力ファイルにセクションの配置を指定するときに使用します。 セクションは、コードまたはデータのいずれかを含む、移植可能な実行可能 (PE) ファイルの連続したメモリのブロックです。 `-filealign` オプションを使用すると、非標準の配置でご自分のアプリケーションをコンパイルできます。ほとんどの開発者は、このオプションを使用する必要はありません。  
  
 各セクションは、`-filealign` 値の倍数の境界上に配置されます。 固定の既定値はありません。 `-filealign` を指定しない場合、コンパイル時にコンパイラによって既定が選択されます。  
  
 セクションのサイズを指定すると、出力ファイルのサイズを変更できます。 セクションのサイズ変更は、比較的小さなデバイスで実行されるプログラムに対して有効な場合があります。  
  
> [!NOTE]
> `-filealign` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
