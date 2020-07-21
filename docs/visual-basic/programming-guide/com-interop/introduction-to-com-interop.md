---
title: COM 相互運用の概要
ms.date: 07/20/2015
helpviewer_keywords:
- interop assemblies
- COM interop [Visual Basic], about COM interop
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
ms.openlocfilehash: 6c7caf266514c43e40135b33d848a688546acf1c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396780"
---
# <a name="introduction-to-com-interop-visual-basic"></a>COM 相互運用の概要 (Visual Basic)
コンポーネント オブジェクト モデル (COM) により、オブジェクトがその機能を他のコンポーネントに公開し、アプリケーションをホストできます。 COM オブジェクトは長年にわたって Windows プログラミングの基本となってきましたが、共通言語ランタイム (CLR) 用に設計されたアプリケーションには多くの利点があります。  
  
 .NET Framework アプリケーションによって、最終的に COM で開発されたものが置き換えられます。 それまでは、Visual Studio を使用して COM オブジェクトを使用するか、作成する必要がある可能性があります。 COM との相互運用性、つまり *COM 相互運用*により、自分のペースで .NET Framework に移行しながら、既存の COM オブジェクトを使用できます。  
  
 .NET Framework を使用して COM コンポーネントを作成することにより、登録を必要としない COM 相互運用を使用できます。 これにより、コンピューターに複数のバージョンがインストールされている場合に有効にする DLL バージョンを制御でき、エンド ユーザーは、XCOPY または FTP を使用して、アプリケーションを、それが実行可能なコンピューター上の適切なディレクトリにコピーできます。 詳細については、「[登録を必要としない COM 相互運用機能](../../../framework/interop/registration-free-com-interop.md)」を参照してください。  
  
## <a name="managed-code-and-data"></a>マネージド コードとデータ  
 .NET Framework 用に開発されたコードは*マネージド コード*と呼ばれ、CLR によって使用されるメタデータが含まれます。 .NET Framework アプリケーションによって使用されるデータは、*マネージド データ*と呼ばれます。ランタイムによって、メモリの割り当てや解放、型チェックの実行などのデータ関連タスクが管理されるためです。 既定で Visual Basic .NET ではマネージド コードとデータが使用されますが、相互運用アセンブリを使用して、COM オブジェクトのアンマネージド コードとデータにアクセスできます (このページで後述しています)。  
  
## <a name="assemblies"></a>アセンブリ  
 アセンブリは、.NET Framework アプリケーションの主な構成要素です。 これは、1 つ以上のファイルを含む 1 つの実装単位として、ビルド、バージョン管理、およびデプロイされる機能のコレクションです。 各アセンブリには、アセンブリ マニフェストが含まれます。  
  
## <a name="type-libraries-and-assembly-manifests"></a>タイプ ライブラリとアセンブリ マニフェスト  
 タイプ ライブラリは、メンバー名やデータ型など、COM オブジェクトの特性を記述します。 アセンブリ マニフェストは、.NET Framework アプリケーションに対して同じ機能を実行します。 それらには、次に関する情報が含まれます。  
  
- アセンブリ ID、バージョン、カルチャ、およびデジタル署名。  
  
- アセンブリ実装を構成するファイル。  
  
- アセンブリを構成する型とリソース。 これには、そこからエクスポートされたものも含まれます。  
  
- 他のアセンブリに対するコンパイル時の依存関係。  
  
- アセンブリを正常に実行するために必要なアクセス許可。  
  
 アセンブリとアセンブリ マニフェストの詳細については、「[.NET のアセンブリ](../../../standard/assembly/index.md)」を参照してください。  
  
### <a name="importing-and-exporting-type-libraries"></a>タイプ ライブラリのインポートとエクスポート  
 Visual Studio には、Tlbimp というユーティリティが含まれており、これにより、タイプ ライブラリから .NET Framework アプリケーションに情報をインポートできます。 アセンブリからタイプ ライブラリを生成するには、Tlbexp ユーティリティを使用します。  
  
 Tlbimp と Tlbexp の詳細については、「[Tlbimp.exe (タイプ ライブラリ インポーター)](../../../framework/tools/tlbimp-exe-type-library-importer.md)」と「[Tlbexp.exe (タイプ ライブラリ エクスポーター)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)」を参照してください。  
  
## <a name="interop-assemblies"></a>相互運用機能アセンブリ  
 相互運用機能アセンブリは、マネージド コードとアンマネージド コードの間を橋渡しし、COM オブジェクト メンバーを同等の .NET Framework マネージド メンバーにマップする .NET Framework アセンブリです。 Visual Basic .NET によって作成された相互運用機能アセンブリは、相互運用マーシャリングなど、COM オブジェクトの操作に関する多くの詳細を処理します。  
  
## <a name="interoperability-marshaling"></a>相互運用マーシャリング  
 すべての .NET Framework アプリケーションでは、使用するプログラミング言語に関係なく、オブジェクトの相互運用性を実現する一連の共通型を共有します。 COM オブジェクトのパラメーターと戻り値に、マネージド コードで使用されているものと異なるデータ型が使われている場合があります。 *相互運用マーシャリング*は、パラメーターと戻り値を、COM オブジェクトとの間で移動するときと同等のデータ型にパッケージ化するプロセスです。 詳細については、「[相互運用マーシャリング](../../../framework/interop/interop-marshaling.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [COM 相互運用](index.md)
- [チュートリアル: COM オブジェクトによる継承の実装](walkthrough-implementing-inheritance-with-com-objects.md)
- [アンマネージ コードとの相互運用](../../../framework/interop/index.md)
- [相互運用性のトラブルシューティング](troubleshooting-interoperability.md)
- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [Tlbimp.exe (タイプ ライブラリ インポーター)](../../../framework/tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe (タイプ ライブラリ エクスポーター)](../../../framework/tools/tlbexp-exe-type-library-exporter.md)
- [相互運用マーシャリング](../../../framework/interop/interop-marshaling.md)
- [登録を必要としない COM 相互運用機能](../../../framework/interop/registration-free-com-interop.md)
