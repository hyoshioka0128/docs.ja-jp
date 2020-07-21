---
title: -moduleassemblyname
ms.date: 03/13/2018
helpviewer_keywords:
- moduleassemblyname compiler option [Visual Basic]
- /moduleassemblyname compiler option [Visual Basic]
- -moduleassemblyname compiler option [Visual Basic]
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
ms.openlocfilehash: 99f2b9d65f3c2a128e026666c5efb384e22643f9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403149"
---
# <a name="-moduleassemblyname"></a>-moduleassemblyname
このモジュールが一部となるアセンブリの名前を指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`assembly_name`|このモジュールが一部となるアセンブリの名前。|  
  
## <a name="remarks"></a>Remarks  
 `-target:module` オプションが指定されている場合にのみ、コンパイラで `-moduleassemblyname` オプションが処理されます。 これにより、コンパイラでモジュールが作成されます。 コンパイラによって作成されたモジュールは、`-moduleassemblyname` オプションで指定されたアセンブリに対してのみ有効です。 モジュールを別のアセンブリに配置すると、実行時エラーが発生します。  
  
 `-moduleassemblyname` オプションは、次の条件に該当する場合にのみ必要です。  
  
- モジュール内のデータ型が、参照アセンブリの `Friend` 型にアクセスする必要がある場合。  
  
- 参照アセンブリに、モジュールをビルドするアセンブリへのフレンド アセンブリのアクセス権が付与されている場合。  
  
 モジュールの作成の詳細については、「[-target (Visual Basic)](target.md)」を参照してください。 フレンド アセンブリの詳細については、「[フレンド アセンブリ](../../../standard/assembly/friend.md)」を参照してください。  
  
> [!NOTE]
> `-moduleassemblyname` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド プロンプトからコンパイルするときにのみ使用できます。  
  
## <a name="see-also"></a>関連項目

- [方法: マルチファイル アセンブリをビルドする](../../../framework/app-domains/build-multifile-assembly.md)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-target (Visual Basic)](target.md)
- [-main](main.md)
- [-reference (Visual Basic)](reference.md)
- [-addmodule](addmodule.md)
- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [フレンド アセンブリ](../../../standard/assembly/friend.md)
