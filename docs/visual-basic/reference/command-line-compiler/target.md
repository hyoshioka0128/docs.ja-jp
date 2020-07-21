---
title: -target
ms.date: 03/13/2018
helpviewer_keywords:
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
ms.openlocfilehash: 0ab28d55b2426a4efda112ab84da5e790909d565
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403071"
---
# <a name="-target-visual-basic"></a>-target (Visual Basic)

コンパイラ出力の形式を指定します。

## <a name="syntax"></a>構文

```console
-target:{exe | library | module | winexe | appcontainerexe | winmdobj}
```

## <a name="remarks"></a>Remarks

次の表は、`-target` オプションの効果をまとめたものです。

|**オプション**|**Behavior**|
|----------------|------------------|
|`-target:exe`|実行可能なコンソール アプリケーションがコンパイラによって作成されます。<br /><br /> これは、`-target` オプションが指定されていない場合の既定のオプションです。 実行可能ファイルは、.exe 拡張子を使用して作成されます。<br /><br /> `-out` オプションで特に指定しない限り、出力ファイル名は `Sub Main` プロシージャを含む入力ファイルの名前となります。<br /><br /> `Sub Main` プロシージャは、.exe ファイルにコンパイルされるソースコード ファイル内に 1 つだけ必要になります。 `-main` コンパイラ オプションを使用して、`Sub Main` プロシージャを含むクラスを指定します。|
|`-target:library`|ダイナミックリンク ライブラリ (DLL) がコンパイラによって作成されます。<br /><br /> ダイナミックリンク ライブラリ ファイルは、.dll 拡張子を使用して作成されます。<br /><br /> `-out` オプションで特に指定しない限り、出力ファイル名は最初の入力ファイルの名前となります。<br /><br /> DLL をビルドする場合、`Sub Main` プロシージャは必要ありません。|
|`-target:module`|アセンブリに追加できるモジュールがコンパイラによって生成されます。<br /><br /> 出力ファイルは、.netmodule の拡張子を使用して作成されます。<br /><br /> .NET 共通言語ランタイムでは、アセンブリのないファイルを読み込むことはできません。 しかし、このようなファイルは、`-reference` を使用して、アセンブリのアセンブリ マニフェストに組み込むことができます。<br /><br /> あるモジュールのコードで別のモジュールの内部型を参照する場合は、`-reference` を使用して、両方のモジュールをアセンブリ マニフェストに組み込む必要があります。<br /><br /> [-addmodule](addmodule.md) オプションでは、モジュールからメタデータをインポートします。|
|`-target:winexe`|実行可能な Windows ベースのアプリケーションがコンパイラによって作成されます。<br /><br /> 実行可能ファイルは、.exe 拡張子を使用して作成されます。 Windows ベースのアプリケーションは、.NET Framework クラス ライブラリまたは Windows API のユーザー インターフェイスを提供するものです。<br /><br /> `-out` オプションで特に指定しない限り、出力ファイル名は `Sub Main` プロシージャを含む入力ファイルの名前となります。<br /><br /> `Sub Main` プロシージャは、.exe ファイルにコンパイルされるソースコード ファイル内に 1 つだけ必要になります。 コードに `Sub Main` プロシージャを持つクラスが複数ある場合は、`-main` コンパイラ オプションを使用して、`Sub Main` プロシージャを含むクラスを指定します。|
|`-target:appcontainerexe`|アプリ コンテナーで実行する必要がある実行可能な Windows ベースのアプリケーションが、コンパイラによって作成されます。 この設定は、Windows 8.x ストア アプリケーションで使用するように設計されています。<br /><br /> **appcontainerexe** 設定では、[移植可能な実行可能](/windows/desktop/Debug/pe-format)ファイルの Characteristics フィールドにビットを設定します。 このビットは、アプリ コンテナーでアプリが実行される必要があることを示します。 このビットが設定されている場合、`CreateProcess` メソッドでアプリケーション コンテナー外のアプリケーションを起動しようとすると、エラーが発生します。 このビット設定を除けば、 **-target:appcontainerexe** は **-target:winexe** と同じです。<br /><br /> 実行可能ファイルは、.exe 拡張子を使用して作成されます。<br /><br /> `-out` オプションを使用して特に指定しない限り、出力ファイル名は `Sub Main` プロシージャを含む入力ファイルの名前となります。<br /><br /> `Sub Main` プロシージャは、.exe ファイルにコンパイルされるソースコード ファイル内に 1 つだけ必要になります。 コードに `Sub Main` プロシージャを持つクラスが複数含まれている場合は、`-main` コンパイラ オプションを使用して、`Sub Main` プロシージャを含むクラスを指定します。|
|`-target:winmdobj`|Windows ランタイム バイナリ (.winmd) ファイルに変換できる中間ファイルが、コンパイラによって作成されます。 .winmd ファイルは、マネージド言語プログラムだけでなく、JavaScript および C++ プログラムでも使用できます。<br /><br /> 中間ファイルは、.winmdobj 拡張子を使用して作成されます。<br /><br /> `-out` オプションを使用して特に指定しない限り、出力ファイル名は最初の入力ファイルの名前になります。 `Sub Main` プロシージャは必要ありません。<br /><br /> .winmdobj ファイルは、Windows メタデータ (WinMD) ファイルを生成するために <xref:Microsoft.Build.Tasks.WinMDExp> エクスポート ツールの入力として使用されるように設計されています。 WinMD ファイルには、.winmd 拡張子が付いており、元のライブラリのコードと、JavaScript、C++、および Windows ランタイムで使用される WinMD 定義の両方が含まれています。|

`-target:module` を指定しない限り、`-target` を使用すると、.NET Framework のアセンブリ マニフェストが出力ファイルに追加されます。

Vbc.exe の各インスタンスで生成される出力ファイルは、多くても 1 つです。 `-out` または `-target` などのコンパイラ オプションを複数回指定した場合、コンパイラで処理される最後のものが有効になります。 コンパイルにおけるすべてのファイルに関する情報は、マニフェストに追加されます。 `-target:module` で作成されたもの以外のすべての出力ファイルには、マニフェストのアセンブリ メタデータが含まれます。 [Ildasm.exe (IL 逆アセンブラー)](../../../framework/tools/ildasm-exe-il-disassembler.md) を使用して、出力ファイル内のメタデータを表示します。

`-target` の省略形は `-t` です。

### <a name="to-set--target-in-the-visual-studio-ide"></a>Visual Studio IDE で -target を設定するには

1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[アプリケーション]** タブをクリックします。

3. **[アプリケーションの種類]** ボックスで値を変更します。

## <a name="example"></a>例

次のコードでは、`in.vb` がコンパイルされ、`in.dll` が作成されます。

```console
vbc -target:library in.vb
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-main](main.md)
- [-out (Visual Basic)](out.md)
- [-reference (Visual Basic)](reference.md)
- [-addmodule](addmodule.md)
- [-moduleassemblyname](moduleassemblyname.md)
- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
