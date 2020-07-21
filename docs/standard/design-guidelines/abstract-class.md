---
title: 抽象クラスのデザイン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, abstract classes
- abstract classes, design guidelines
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], abstract
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
ms.openlocfilehash: e6a5923f293ed536fb272f6fe6c805067aede0ab
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280778"
---
# <a name="abstract-class-design"></a>抽象クラスのデザイン

❌抽象型では、パブリックまたはプロテクトの内部コンストラクターを定義しないでください。

 コンストラクターは、ユーザーが型のインスタンスを作成する必要がある場合にのみ、パブリックにする必要があります。 抽象型のインスタンスを作成することはできないため、パブリックコンストラクターを持つ抽象型は誤って設計され、ユーザーに対して誤解が生じることになります。

 ✔️は、抽象クラスで protected コンストラクターまたは internal コンストラクターを定義します。

 プロテクトコンストラクターはより一般的であり、サブタイプの作成時に基底クラスが独自の初期化を実行できるようにするだけです。

 内部コンストラクターを使用すると、抽象クラスの具象実装を、クラスを定義するアセンブリに限定できます。

 ✔️は、出荷する各抽象クラスから継承される具象型を少なくとも1つ指定する必要があります。

 これにより、抽象クラスの設計を検証できます。 たとえば、 <xref:System.IO.FileStream?displayProperty=nameWithType> は抽象クラスの実装です <xref:System.IO.Stream?displayProperty=nameWithType> 。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [型デザインのガイドライン](type.md)
- [フレームワークデザインのガイドライン](index.md)
