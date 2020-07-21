---
title: '方法: MetadataLoadContext を使用してアセンブリの内容を検査する'
description: MetadataLoadContext を使用する方法について説明します。この API を使用すると、検査のために .NET アセンブリを読み込むことができます。
author: MSDN-WhiteKnight
ms.date: 03/10/2020
ms.technology: dotnet-standard
ms.openlocfilehash: 90c84147c52199afc42a2efc297bc7fe40658ec7
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141198"
---
# <a name="how-to-inspect-assembly-contents-using-metadataloadcontext"></a>方法: MetadataLoadContext を使用してアセンブリの内容を検査する

既定では、開発者は .NET のリフレクション API を使用して、メインの実行コンテキストに読み込まれたアセンブリの内容を検査することができます。 ただし、場合によってはアセンブリを実行コンテキストに読み込むことができないことがあります。その原因としては、それが別のプラットフォームやプロセッサ アーキテクチャ用にコンパイルされた場合や、[参照アセンブリ](reference-assemblies.md)である場合などが考えられます。 <xref:System.Reflection.MetadataLoadContext?displayProperty=fullName> API を使用すると、このようなアセンブリを読み込んで検査することができます。 <xref:System.Reflection.MetadataLoadContext> に読み込まれたアセンブリは、メタデータとしてのみ扱われます。つまり、アセンブリ内の型を調べることはできますが、そこに含まれるコードを実行することはできません。 メインの実行コンテキストとは異なり、<xref:System.Reflection.MetadataLoadContext> によって現在のディレクトリから自動的に依存関係が読み込まれることはありません。代わりに、これに渡された <xref:System.Reflection.MetadataAssemblyResolver> によって指定されるカスタム バインド ロジックが使用されます。

## <a name="prerequisites"></a>必須コンポーネント

<xref:System.Reflection.MetadataLoadContext> を使用するには、[System.Reflection.MetadataLoadContext](https://www.nuget.org/packages/System.Reflection.MetadataLoadContext) NuGet パッケージをインストールしてください。 これは、.NET Standard 2.0 に準拠している任意のターゲット フレームワーク (たとえば、.NET Core 2.0 や .NET Framework 4.6.1) でサポートされています。

## <a name="create-metadataassemblyresolver-for-metadataloadcontext"></a>MetadataLoadContext 用の MetadataAssemblyResolver を作成する

<xref:System.Reflection.MetadataLoadContext> を作成するには、<xref:System.Reflection.MetadataAssemblyResolver> のインスタンスを指定する必要があります。 その 1 つを指定するための最も簡単な方法は、<xref:System.Reflection.PathAssemblyResolver> を使用することです。これを使うと、指定したアセンブリ パス文字列のコレクションからアセンブリが解決されます。 直接検査したいアセンブリだけでなく、このコレクションにも、必要な依存関係がすべて含まれている必要があります。 たとえば、ある外部アセンブリに配置されているカスタム属性を読み取るには、そのアセンブリを含める必要があります。そうしないと、例外がスローされます。 ほとんどの場合は、少なくとも "*コア アセンブリ*"、つまり <xref:System.Object?displayProperty=nameWithType> などの組み込みのシステム型を含むアセンブリを含める必要があります。 次のコードでは、検査されるアセンブリと、現在のランタイムのコア アセンブリで構成されるコレクションを使用して <xref:System.Reflection.PathAssemblyResolver> を作成する方法が示されています。

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CoreAssembly)]

すべての BCL 型にアクセスする必要がある場合は、コレクションにすべてのランタイム アセンブリを含めることができます。 次のコードでは、検査されるアセンブリと、現在のランタイムのすべてのアセンブリで構成されるコレクションを使用して <xref:System.Reflection.PathAssemblyResolver> を作成する方法が示されています。

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#RuntimeAssemblies)]

## <a name="create-metadataloadcontext"></a>MetadataLoadContext の作成

<xref:System.Reflection.MetadataLoadContext> を作成するには、そのコンストラクター <xref:System.Reflection.MetadataLoadContext.%23ctor%28System.Reflection.MetadataAssemblyResolver%2CSystem.String%29> を呼び出します。その際、前に作成した <xref:System.Reflection.MetadataAssemblyResolver> を最初のパラメーターとして渡し、コア アセンブリの名前を 2 番目のパラメーターとして渡します。 コア アセンブリの名前は省略できます。そうした場合、コンストラクターでは、既定の名前 "mscorlib"、"System.Runtime"、または "netstandard" の使用が試みられます。

コンテキストを作成したら、<xref:System.Reflection.MetadataLoadContext.LoadFromAssemblyPath%2A> などのメソッドを使用して、そのコンテキストにアセンブリを読み込むことができます。 コードの実行に関連するアセンブリを除き、読み込まれたアセンブリに対してすべてのリフレクション API を使用できます。 <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A> メソッドにはコンストラクターの実行が含まれているため、<xref:System.Reflection.MetadataLoadContext> でカスタム属性を調べる必要がある場合は、代わりに <xref:System.Reflection.MemberInfo.GetCustomAttributesData%2A> メソッドを使用します。

次のコード サンプルでは、<xref:System.Reflection.MetadataLoadContext> が作成され、それにアセンブリが読み込まれ、コンソールにアセンブリ属性が出力されます。

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CreateContext)]

## <a name="example"></a>例

完全なコード例については、[MetadataLoadContext サンプルを使用したアセンブリ内容の検査](https://docs.microsoft.com/samples/dotnet/samples/inspect-assembly-contents-using-metadataloadcontext/)に関するページを参照してください。
