---
title: '方法: EdmGen.exe を使用してモデル ファイルとマッピング ファイルを検証する'
ms.date: 03/30/2017
ms.assetid: 2641906a-971a-4d0b-8aee-13fabc02a1cc
ms.openlocfilehash: 4495ff3c5d55779e9db113a2a59361b643841382
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251373"
---
# <a name="how-to-use-edmgenexe-to-validate-model-and-mapping-files"></a>方法: EdmGen.exe を使用してモデル ファイルとマッピング ファイルを検証する
このトピックでは、[EDM ジェネレーター (EdmGen.exe)](edm-generator-edmgen-exe.md) ツールを使用してモデル ファイルとマッピング ファイルを検証する方法を示します。 詳細については、「[Entity Data Model](../entity-data-model.md)」を参照してください。  
  
### <a name="to-validate-the-school-model-using-edmgenexe"></a>EdmGen.exe を使用して School モデルを検証するには  
  
1. School データベースを作成します。 詳細については、「[School サンプル データベースの作成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))」を参照してください。  
  
2. School モデルを生成します。 詳細については、[EdmGen.exe を使用してモデル ファイルとマッピング ファイルを生成する](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)」を参照してください。  
  
3. コマンド プロンプトで、次のコマンド (改行なし) を実行します。  
  
    ```console
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:ValidateArtifacts /inssdl:.\School.ssdl /inmsl:.\School.msl /incsdl:.\School.csdl  
    ```  
  
## <a name="see-also"></a>関連項目

- [方法: Entity Framework プロジェクトを手動で構成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))
- [ADO.NET Entity Data Model ツール](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [方法: ビューを事前に生成してクエリ パフォーマンスを向上させる](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))
- [方法: EdmGen.exe を使用してオブジェクトレイヤー コードを生成する](how-to-use-edmgen-exe-to-generate-object-layer-code.md)
