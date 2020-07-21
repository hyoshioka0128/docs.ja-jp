---
title: アセンブリと DLL の名前
description: アセンブリとダイナミックリンクライブラリ (Dll) の名前付けのガイドラインについて説明します。 アセンブリは1つ以上のファイルにまたがることができますが、通常は1対1のファイルを DLL とマップします。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], DLLs
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
- DLLs, names
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
ms.openlocfilehash: de7ce3ee774d4598521d7156d0d660c3fe30154c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594479"
---
# <a name="names-of-assemblies-and-dlls"></a>アセンブリと DLL の名前
アセンブリは、マネージコードプログラムの配置と id の単位です。 アセンブリは1つ以上のファイルにまたがることができますが、通常、アセンブリは1対1のを DLL とマップします。 したがって、このセクションでは DLL の名前付け規則についてのみ説明し、次にアセンブリの名前付け規則にマップできます。

 アセンブリ Dll の名前を選択して、システムデータなどの大量の機能を提案する✔️ます。

 アセンブリ名と DLL 名は、名前空間名に対応する必要はありませんが、アセンブリに名前を付けるときは、名前空間名に従うことをお勧めします。 経験則として、アセンブリに含まれる名前空間の共通のプレフィックスに基づいて DLL の名前を指定することをお勧めします。 たとえば、との2つの名前空間を持つアセンブリを `MyCompany.MyTechnology.FirstFeature` `MyCompany.MyTechnology.SecondFeature` 呼び出すことができ `MyCompany.MyTechnology.dll` ます。

 ✔️ Dll には、次のパターンに従って名前を付けることを検討してください。

 `<Company>.<Component>.dll`

 に `<Component>` は1つ以上のドット区切り句が含まれています。 次に例を示します。

 `Litware.Controls.dll`.

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [名前付けのガイドライン](naming-guidelines.md)
