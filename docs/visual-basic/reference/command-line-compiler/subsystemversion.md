---
title: -subsystemversion
ms.date: 03/13/2018
helpviewer_keywords:
- /subsystemversion compiler option [Visual Basic]
- -subsystemversion compiler option [Visual Basic]
- subsystemversion compiler option [Visual Basic]
ms.assetid: 08be22b2-f447-4cd3-8203-120b1b920b54
ms.openlocfilehash: a977bc4cff822de551bf82d0f31707e9b2b6ea41
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348533"
---
# <a name="-subsystemversion-visual-basic"></a>-subsystemversion (Visual Basic)

生成された実行可能ファイルが動作できるサブシステムの最小バージョンを指定します。これにより、実行可能ファイルが動作できる Windows のバージョンが決まります。 通常、このオプションを指定することで、実行可能ファイルが、Windows の以前のバージョンでは使用できない特定のセキュリティ機能を利用できるようになります。

> [!NOTE]
> サブシステム自体を指定するには、[-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) のコンパイラ オプションを使用します。

## <a name="syntax"></a>構文

```vb
-subsystemversion:major.minor
```

## <a name="parameters"></a>パラメーター

`major.minor`

サブシステムに必要な最小バージョン。メジャー バージョンおよびマイナー バージョンのドット表記で表されます。 たとえば、このオプションの値を 6.01 に設定すると、Windows 7 より古いオペレーティング システムではアプリケーションを実行できないように指定できます (このトピックの以下の表を参照)。 `major` と `minor` の値を整数で指定する必要があります。

`minor` バージョンでは、前に配置されるゼロによってバージョンが変更されることはありませんが、後ろにゼロが付くとバージョンが変わります。 たとえば、6.1 と 6.01 は同じバージョンを示しますが、6.10 は異なるバージョンを示します。 混乱を避けるため、マイナー バージョンには 2 桁の数値を使用することをお勧めします。

## <a name="remarks"></a>コメント

次の表は、Windows の一般的なサブシステムのバージョンを示しています。

|Windows のバージョン|サブシステムのバージョン|
|---------------------|-----------------------|
|Windows 2000|5.00|
|Windows XP|5.01|
|Windows Server 2003|5.02|
|Windows Vista|6.00|
|Windows 7|6.01|
|Windows Server 2008|6.01|
|[!INCLUDE[win8](~/includes/win8-md.md)]|6.02|

## <a name="default-values"></a>既定の値

**-subsystemversion** コンパイラ オプションの既定値は条件によって異なります。その条件を次に示します。

- 次のコンパイラ オプションのいずれかが設定されている場合、既定値は 6.02 です。

  - [/target:appcontainerexe](../../../visual-basic/reference/command-line-compiler/target.md)

  - [/target:winmdobj](../../../visual-basic/reference/command-line-compiler/target.md)

  - [-platform:arm](../../../visual-basic/reference/command-line-compiler/platform.md)

- MSBuild を使用しており、.NET Framework 4.5 が対象で、さらにこの一覧で前に指定したコンパイラ オプションを設定していない場合、既定値は 6.00 です。

- 上記の条件がどれも当てはまらない場合、既定値は 4.00 です。

## <a name="setting-this-option"></a>このオプションを設定する

Visual Studio で **-subsystemversion**コンパイラオプションを設定するには、.vbproj ファイルを開き、MSBuild XML で `SubsystemVersion` プロパティの値を指定する必要があります。 Visual Studio IDE でこのオプションを設定することはできません。 詳細については、このトピックの「既定値」または「[MSBuild プロジェクトの共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)」を参照してください。

## <a name="see-also"></a>参照

- [Visual Basic のコマンド ライン コンパイラ](../../../visual-basic/reference/command-line-compiler/index.md)

- [MSBuild プロパティ](/visualstudio/msbuild/msbuild-properties)
