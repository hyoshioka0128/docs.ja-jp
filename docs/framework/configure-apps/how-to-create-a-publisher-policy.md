---
title: '方法: 発行者ポリシーを作成する'
description: アセンブリベンダーが、.NET でアップグレードされたアセンブリを使用して発行者ポリシーファイルを作成し、アプリケーションが新しいバージョンを使用する必要があることを規定する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- publisher policy assembly
- publisher policy files
- GAC (global assembly cache), publisher policy assembly
- global assembly cache, publisher policy assembly
ms.assetid: 8046bc5d-2fa9-4277-8a5e-6dcc96c281d9
ms.openlocfilehash: 23e9d8144ec5742e0371d566b7af59dc9dd30c9b
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85105404"
---
# <a name="how-to-create-a-publisher-policy"></a>方法: 発行者ポリシーを作成する

アセンブリのベンダーは、アップグレードされたアセンブリに発行者ポリシーファイルを含めることによって、アプリケーションが新しいバージョンのアセンブリを使用する必要があることを示すことができます。 発行者ポリシーファイルは、アセンブリリダイレクトとコードベース設定を指定し、アプリケーション構成ファイルと同じ形式を使用します。 発行者ポリシーファイルは、アセンブリにコンパイルされ、グローバルアセンブリキャッシュに配置されます。

発行者ポリシーを作成するには、次の3つの手順が必要です。

1. 発行者ポリシーファイルを作成します。

2. 発行者ポリシーアセンブリを作成します。

3. 発行者ポリシーアセンブリをグローバルアセンブリキャッシュに追加します。

発行元ポリシーのスキーマについては、「[アセンブリバージョンのリダイレクト](redirect-assembly-versions.md)」を参照してください。 次の例は、の1つのバージョンを別のバージョンにリダイレクトする発行者ポリシーファイルを示して `myAssembly` います。

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
       <dependentAssembly>
         <assemblyIdentity name="myAssembly"
                           publicKeyToken="32ab4ba45e0a69a1"
                           culture="en-us" />
         <!-- Redirecting to version 2.0.0.0 of the assembly. -->
         <bindingRedirect oldVersion="1.0.0.0"
                          newVersion="2.0.0.0"/>
       </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

コードベースを指定する方法については、「[アセンブリの場所の指定](specify-assembly-location.md)」を参照してください。

## <a name="creating-the-publisher-policy-assembly"></a>発行者ポリシーアセンブリを作成しています

[アセンブリリンカー (Al.exe)](../tools/al-exe-assembly-linker.md)を使用して、発行者ポリシーアセンブリを作成します。

#### <a name="to-create-a-publisher-policy-assembly"></a>発行者ポリシーアセンブリを作成するには

コマンド プロンプトに、次のコマンドを入力します。

```console
al /link:publisherPolicyFile /out:publisherPolicyAssemblyFile /keyfile:keyPairFile /platform:processorArchitecture
```

このコマンドの説明:

- `publisherPolicyFile`引数は発行者ポリシーファイルの名前です。

- `publisherPolicyAssemblyFile`引数は、このコマンドの結果として生成される発行者ポリシーアセンブリの名前です。 アセンブリファイル名は、次の形式に従う必要があります。

  'policy.majorNumber.minorNumber.mainAssemblyName.dll '

- `keyPairFile`引数は、キーペアを含むファイルの名前です。 アセンブリと発行者ポリシーアセンブリには、同じキーペアで署名する必要があります。

- 引数は、 `processorArchitecture` プロセッサ固有のアセンブリの対象となるプラットフォームを識別します。

  > [!NOTE]
  > 特定のプロセッサアーキテクチャを対象とする機能は、.NET Framework 2.0 以降で使用できます。

特定のプロセッサアーキテクチャを対象とする機能は、.NET Framework 2.0 以降で使用できます。 次のコマンドは、という発行者ポリシーファイルからという発行者ポリシーアセンブリを作成し `policy.1.0.myAssembly` `pub.config` 、ファイルのキーペアを使用してアセンブリに厳密な名前を割り当て、 `sgKey.snk` アセンブリが x86 プロセッサアーキテクチャを対象とすることを指定します。

```console
al /link:pub.config /out:policy.1.0.myAssembly.dll /keyfile:sgKey.snk /platform:x86
```

発行者ポリシーアセンブリは、適用されるアセンブリのプロセッサアーキテクチャと一致している必要があります。 したがって、アセンブリの値がの場合は、 <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A> <xref:System.Reflection.ProcessorArchitecture.MSIL> そのアセンブリの発行者ポリシーアセンブリをで作成する必要があり `/platform:anycpu` ます。 プロセッサ固有のアセンブリごとに個別の発行者ポリシーアセンブリを指定する必要があります。

このルールの結果として、アセンブリのプロセッサアーキテクチャを変更するには、バージョン番号のメジャーまたはマイナーコンポーネントを変更して、正しいプロセッサアーキテクチャを持つ新しい発行者ポリシーアセンブリを指定できるようにする必要があります。 アセンブリに異なるプロセッサアーキテクチャがある場合、古い発行者ポリシーアセンブリはアセンブリを処理できません。

また、バージョン2.0 リンカーを使用して、以前のバージョンの .NET Framework を使用してコンパイルされたアセンブリの発行者ポリシーアセンブリを作成することはできません。これは、常にプロセッサアーキテクチャを指定するためです。

## <a name="adding-the-publisher-policy-assembly-to-the-global-assembly-cache"></a>発行者ポリシーアセンブリをグローバルアセンブリキャッシュに追加する

グローバル[アセンブリキャッシュツール (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md)を使用して、発行者ポリシーアセンブリをグローバルアセンブリキャッシュに追加します。

### <a name="to-add-the-publisher-policy-assembly-to-the-global-assembly-cache"></a>発行者ポリシーアセンブリをグローバルアセンブリキャッシュに追加するには

コマンド プロンプトに、次のコマンドを入力します。

```console
gacutil /i publisherPolicyAssemblyFile
```

次のコマンドは、 `policy.1.0.myAssembly.dll` をグローバルアセンブリキャッシュに追加します。

```console
gacutil /i policy.1.0.myAssembly.dll
```

> [!IMPORTANT]
> 引数で指定された元の発行者ポリシーファイル `/link` がアセンブリと同じディレクトリにある場合を除き、発行者ポリシーアセンブリをグローバルアセンブリキャッシュに追加することはできません。

## <a name="see-also"></a>関連項目

- [アセンブリを使用したプログラミング](../../standard/assembly/index.md)
- [ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)
- [構成ファイルを使用してアプリを構成する方法](index.md)
- [ランタイム設定スキーマ](./file-schema/runtime/index.md)
- [構成ファイル スキーマ](./file-schema/index.md)
- [アセンブリ バージョンのリダイレクト](redirect-assembly-versions.md)
