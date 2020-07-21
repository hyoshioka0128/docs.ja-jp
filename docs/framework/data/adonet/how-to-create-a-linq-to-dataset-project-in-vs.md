---
title: Visual Studio で LINQ to DataSet プロジェクトを作成する
ms.date: 08/15/2018
ms.assetid: 49ba6cb0-cdd2-4571-aeaa-25bf0f40e9b3
ms.openlocfilehash: 91032766248b11e51b90aa788b1c64c140347c25
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74802027"
---
# <a name="how-to-create-a-linq-to-dataset-project-in-visual-studio"></a>方法: Visual Studio で LINQ to DataSet プロジェクトを作成する

さまざまな種類の LINQ プロジェクトでは、特定のアセンブリ参照と、インポートされる名前空間 (Visual Basic) または [using](../../../csharp/language-reference/keywords/using-directive.md) ディレクティブ (C#) が必要です。 LINQ の場合の最小要件は、*System.Core.dll* への参照と、<xref:System.Linq> に対する `using` ディレクティブです。

Visual Studio 2017 以降のバージョンで新しい C# コンソール アプリ プロジェクトを作成した場合、これらの要件は既定で提供されます。 以前のバージョンの Visual Studio のプロジェクトをアップグレードする場合、これらの LINQ 関連の参照を手動で追加する必要がある場合があります。

LINQ to DataSet では、さらに *System.Data.dll* と *System.Data.DataSetExtensions.dll* に対する 2 つの参照が必要です。

> [!NOTE]
> コマンド プロンプトからビルドする場合、 *%ProgramFiles%\Reference Assemblies\Microsoft\Framework\v3.5* 内の LINQ 関連 DLL を、手動で参照する必要があります。

## <a name="to-enable-linq-to-dataset-functionality"></a>LINQ to DataSet 機能を有効にするには

既存のプロジェクトで LINQ to DataSet 機能を有効にするには、次の手順のようにします。

1. **System.Core**、**System.Data**、**System.Data.DataSetExtensions** に対する参照を追加します。

   **ソリューション エクスプローラー**で、 **[参照]** ノードを右クリックし、 **[参照の追加]** を選択します。 **[参照マネージャー]** ダイアログ ボックスで、**System.Core**、**System.Data**、**System.Data.DataSetExtensions** を選択します。 **[OK]** を選択します。

1. **System.Data** と **System.Linq** に対する [using](../../../csharp/language-reference/keywords/using-directive.md) ディレクティブ (Visual Basic では [Imports ステートメント](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)) を追加します。

   ```csharp
   using System.Data;
   using System.Linq;
   ```

1. データベースへの接続方法に基づき、必要に応じて、**System.Data.Common** または **System.Data.SqlClient** に対する `using` ディレクティブ (または `Imports` ステートメント) を追加します。

## <a name="see-also"></a>関連項目

- [LINQ to DataSet の概要](getting-started-linq-to-dataset.md)
