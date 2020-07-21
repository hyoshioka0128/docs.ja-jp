---
title: -langversion (C# コンパイラ オプション)
ms.date: 05/20/2020
f1_keywords:
- /langversion
helpviewer_keywords:
- /langversion compiler option [C#]
- -langversion compiler option [C#]
- langversion compiler option [C#]
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
ms.openlocfilehash: 408b2fb1f19f872db675321601ebc1b0c921044b
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83802945"
---
# <a name="-langversion-c-compiler-options"></a>-langversion (C# コンパイラ オプション)

コンパイラが、選択した C# 言語仕様に含まれている構文のみを受け入れるようにします。

## <a name="syntax"></a>構文

```console
-langversion:option
```

## <a name="arguments"></a>引数

`option`

有効な値は、次のとおりです。

[!INCLUDE [lang-versions-table](../includes/langversion-table.md)]

既定の言語バージョンは、アプリケーションのターゲット フレームワークやインストールされている SDK または Visual Studio のバージョンに依存します。 これらの規則は、[言語バージョンの構成](../configure-language-version.md#defaults)に関する記事の中で定義されています。

## <a name="remarks"></a>Remarks

C# アプリケーションで参照されるメタデータは、 **-langversion** コンパイラ オプションの対象になりません。

C# コンパイラのバージョンごとに言語仕様の拡張機能が含まれているため、 **-langversion** は、コンパイラの以前のバージョンと同じ機能を提供しません。

さらに、C# バージョンの更新は、一般的に主要な .NET Framework のリリースと一致しますが、新しい構文および機能は必ずしも特定のフレームワーク バージョンに関連付けられていません。 新機能では、C# リビジョンと共にリリースされる新しいコンパイラの更新プログラムを確実に必要としますが、各特定機能には、独自の最小の .NET API または共通言語ランタイムの要件があり、この要件によって、NuGet パッケージやその他のライブラリを含めることで下位レベルのフレームワークで実行できるようになります。

使用する **-langversion** の設定に関係なく、現在のバージョンの共通言語ランタイムを使用して .exe や .dll を作成します。 1 つの例外は、 **-langversion:ISO-1** の下で機能する、フレンド アセンブリと [-moduleassemblyname (C# コンパイラ オプション)](./moduleassemblyname-compiler-option.md) です。

C# 言語バージョンを指定するその他の方法については、[C# 言語のバージョンの選択](../configure-language-version.md)に関するトピックを参照してください。

このコンパイラ オプションをプログラムで設定する方法については、「<xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>」を参照してください。

## <a name="c-language-specification"></a>C# 言語仕様

| バージョン          | Link                       | 説明                                                             |
|------------------|----------------------------|-------------------------------------------------------------------------|
| C# 7.0 以降 |                            | 現在、利用できません                                                 |
| C# 6.0           | [リンク][csharp-6]           | C# 言語仕様バージョン 6 - 非公式ドラフト: .NET Foundation |
| C# 5.0           | [PDF のダウンロード][csharp-5]   | Standard ECMA-334 5th Edition                                           |
| C# 3.0           | [DOC のダウンロード][csharp-3]   | C# 言語仕様バージョン 3.0:Microsoft Corporation            |
| C# 2.0           | [PDF のダウンロード][csharp-2]   | Standard ECMA-334 4th Edition                                           |
| C# 1.2           | [DOC のダウンロード][csharp-1.2] | C# 言語仕様バージョン 1.2:Microsoft Corporation            |
| C# 1.0           | [DOC のダウンロード][csharp-1]   | C# 言語仕様バージョン 1.0:Microsoft Corporation            |

[csharp-6]: /dotnet/csharp/language-reference/language-specification/introduction
[csharp-5]: https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf
[csharp-3]: https://download.microsoft.com/download/3/8/8/388e7205-bc10-4226-b2a8-75351c669b09/CSharp%20Language%20Specification.doc
[csharp-2]: https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%204th%20edition%20June%202006.pdf
[csharp-1.2]: https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%202nd%20edition%20December%202002.pdf
[csharp-1]: https://www.ecma-international.org/publications/files/ECMA-ST-ARCH/ECMA-334%201st%20edition%20December%202001.pdf

## <a name="minimum-sdk-version-needed-to-support-all-language-features"></a>すべての言語機能をサポートするために必要な SDK の最小バージョン

次の表は、SDK の最小バージョンに対応する言語バージョンをサポートする C# コンパイラを示しています。

| C# バージョン | SDK の最小バージョン                                                                  |
|------------|--------------------------------------------------------------------------------------|
| C# 8.0     | Microsoft Visual Studio/Build Tools 2019、バージョン 16.3 または .NET Core 3.0 SDK         |
| C# 7.3     | Microsoft Visual Studio/Build Tools 2017、バージョン 15.7                               |
| C# 7.2     | Microsoft Visual Studio/Build Tools 2017、バージョン 15.5                               |
| C# 7.1     | Microsoft Visual Studio/Build Tools 2017、バージョン 15.3                               |
| C# 7.0     | Microsoft Visual Studio/Build Tools 2017                                             |
| C# 6       | Microsoft Visual Studio/Build Tools 2015                                             |
| C# 5       | Microsoft Visual Studio/Build Tools 2012、またはバンドルされている .Net Framework 4.5 コンパイラ      |
| C# 4       | Microsoft Visual Studio/Build Tools 2010、またはバンドルされている .Net Framework 4.0 コンパイラ      |
| C# 3       | Microsoft Visual Studio/Build Tools 2008、またはバンドルされている .Net Framework 3.5 コンパイラ      |
| C# 2       | Microsoft Visual Studio/Build Tools 2005、またはバンドルされている .Net Framework 2.0 コンパイラ      |
| C# 1.0/1.2 | Microsoft Visual Studio/Build Tools .NET 2002 またはバンドルされている .NET Framework 1.0 コンパイラ |

## <a name="see-also"></a>関連項目

- [C# コンパイラ オプション](index.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
