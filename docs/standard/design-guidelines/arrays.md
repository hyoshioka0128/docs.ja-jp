---
title: 配列
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], arrays
- arrays [.NET Framework], usage guidelines
- empty arrays
ms.assetid: 66a1b3d8-6f3f-4715-b235-e1ff95e32d8e
ms.openlocfilehash: 30277507050091de6b1e9293401d61ac5e351a1f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280622"
---
# <a name="arrays"></a>配列
✔️は、パブリック Api で配列に対してコレクションを使用することをお勧めします。 コレクション[セクションで](guidelines-for-collections.md)は、コレクションと配列のどちらかを選択する方法について詳しく説明します。

 ❌読み取り専用の配列フィールドは使用しないでください。 フィールド自体は読み取り専用であり、変更することはできませんが、配列内の要素は変更できます。

 ✔️多次元配列の代わりにジャグ配列を使用することを検討してください。

 ジャグ配列は、配列でもある要素を含む配列です。 要素を構成する配列は、さまざまなサイズになることがあり、一部のデータセット (スパースマトリックスなど) では、多次元配列と比較して無駄になる領域が少なくなります。 さらに、CLR はジャグ配列に対するインデックス操作を最適化するため、一部のシナリオでは実行時のパフォーマンスが向上する可能性があります。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- <xref:System.Array>
- [フレームワークデザインのガイドライン](index.md)
- [使用に関するガイドライン](usage-guidelines.md)
