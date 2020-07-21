---
title: '方法: アセンブリを読み込み、アンロードする'
description: CLR では、プログラムによって参照される .NET アセンブリが自動的に読み込まれます。 また、特定のアセンブリを現在のアプリケーション ドメインに動的に読み込むこともできます。
ms.date: 08/19/2019
ms.assetid: 6a4f490f-3576-471f-9533-003737cad4a3
ms.openlocfilehash: e6f1ede055dd3f68bced4eba527b2fc65f7d5715
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378680"
---
# <a name="how-to-load-and-unload-assemblies"></a>方法: アセンブリを読み込み、アンロードする
プログラムから参照されるアセンブリは、共通言語ランタイムによって自動的に読み込まれますが、特定のアセンブリを現在のアプリケーション ドメインに動的に読み込むこともできます。 詳細については、[アプリケーション ドメインにアセンブリを読み込む](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)」を参照してください。

.NET Framework では、アセンブリが含まれるすべてのアプリケーション ドメインをアンロードせずに、個々のアセンブリをアンロードする方法はありません。 アセンブリがスコープの外にある場合であっても、実際のアセンブリ ファイルは、これらのアセンブリ ファイルを含むすべてのアプリケーション ドメインがアンロードされるまでは読み込まれたままになります。 .Net Core では、<xref:System.Runtime.Loader.AssemblyLoadContext?displayProperty=nameWithType> クラスによってアセンブリのアンロードが処理されます。 詳細については、「[.NET Core でアセンブリのアンローダビリティを使用およびデバッグする方法](unloadability.md)」を参照してください。

## <a name="load-and-unload-assemblies"></a>アセンブリを読み込み、アンロードする

アセンブリをアプリケーション ドメインに読み込むには、<xref:System.AppDomain> クラスと <xref:System.Reflection.Assembly> クラスに含まれるいくつかの読み込みメソッドのいずれかを使用します。 詳細については、[アプリケーション ドメインにアセンブリを読み込む](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)」を参照してください。 .NET Core でサポートされるアプリケーション ドメインは 1 つだけであることに注意してください。

.NET Framework でアセンブリをアンロードするには、アセンブリを含まれるすべてのアプリケーション ドメインをアンロードする必要があります。 アプリケーション ドメインをアンロードするには、<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> メソッドを使用します。 詳細については、[アプリケーション ドメインをアンロードする](../../framework/app-domains/how-to-unload-an-application-domain.md)」を参照してください。

.NET Framework アプリケーションで、一部のアセンブリだけをアンロードする場合は、新しいアプリケーション ドメインを作成し、そのドメイン内でコードを実行した後、そのアプリケーション ドメインをアンロードします。 詳細については、[アプリケーション ドメインをアンロードする](../../framework/app-domains/how-to-unload-an-application-domain.md)」を参照してください。  

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../../csharp/programming-guide/index.md)
- [プログラミングの概念 (Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
- [.NET のアセンブリ](index.md)
- [方法: アプリケーション ドメインにアセンブリを読み込む](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)
