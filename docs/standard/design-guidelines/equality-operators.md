---
title: 等値演算子
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], Equals method
- class library design guidelines [.NET Framework], equality operator
- equality operator (==) [.NET Framework]
- Equals method
- == operator (equality) [.NET Framework]
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
ms.openlocfilehash: bd36b98af25db2921c164ac359188997d379a270
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280051"
---
# <a name="equality-operators"></a>等値演算子
このセクションでは、等値演算子のオーバーロードについて説明し、 `operator==` 等値演算子としてとを参照し `operator!=` ます。

 ❌等値演算子の1つをオーバーロードしないでください。

 ✔️、 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 等値演算子のセマンティクスと同様のパフォーマンス特性がまったく同じであることを確認します。

 これは多くの場合 `Object.Equals` 、等値演算子がオーバーロードされるときにをオーバーライドする必要があることを意味します。

 ❌等値演算子から例外をスローしないようにします。

 たとえば、引数のいずれかがスローではなく null の場合は、false を返し `NullReferenceException` ます。

## <a name="equality-operators-on-value-types"></a>値型の等値演算子
 等しい場合は、値型に対して等値演算子をオーバーロード✔️ます。

 ほとんどのプログラミング言語では、値型にの既定の実装はありません `operator==` 。

## <a name="equality-operators-on-reference-types"></a>参照型の等値演算子
 ❌変更可能な参照型に対する等値演算子のオーバーロードは避けてください。

 多くの言語には、参照型の等価演算子が組み込まれています。 これらの組み込み演算子は、通常、参照の等価性を実装します。多くの開発者は、既定の動作が値の等価性に変更されると驚かれます。

 不変性によって参照の等価性と値の等価性の違いが非常に困難になるため、この問題は変更できない参照型に対しては緩和されます。

 ❌実装が参照の等価性よりも大幅に遅くなる場合は、参照型に対する等値演算子のオーバーロードを避けてください。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [使用に関するガイドライン](usage-guidelines.md)
