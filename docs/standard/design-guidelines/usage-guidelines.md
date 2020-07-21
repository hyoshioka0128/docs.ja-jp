---
title: 使用ガイドライン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], usage guidelines
ms.assetid: 42215ffa-a099-4a26-b14e-fb2bdb6f95b7
ms.openlocfilehash: 03eaba3e52cb25619f65637efb4f414c22770440
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291345"
---
# <a name="usage-guidelines"></a>使用ガイドライン

このセクションでは、一般公開されている Api で共通型を使用するためのガイドラインを示します。 組み込みのフレームワーク型 (シリアル化属性など) の直接使用と、一般的な演算子のオーバーロードを扱っています。
  
<xref:System.IDisposable?displayProperty=nameWithType>このセクションでは、このインターフェイスについては説明しませんが、「 [Dispose Pattern](../garbage-collection/implementing-dispose.md) 」セクションで説明します。

> [!NOTE]
> その他の一般的な組み込み .NET Framework 型のガイドラインと追加情報については、「」、「」、「」、「」、「」、および「」のリファレンストピックを参照してください <xref:System.DateTime?displayProperty=nameWithType> <xref:System.DateTimeOffset?displayProperty=nameWithType> <xref:System.ICloneable?displayProperty=nameWithType> <xref:System.IComparable%601?displayProperty=nameWithType> <xref:System.IEquatable%601?displayProperty=nameWithType> <xref:System.Nullable%601?displayProperty=nameWithType> <xref:System.Object?displayProperty=nameWithType> <xref:System.Uri?displayProperty=nameWithType> 。

## <a name="in-this-section"></a>このセクションの内容

[配列](arrays.md)  
[属性](attributes.md)  
[コレクション](guidelines-for-collections.md)  
[シリアル化](serialization.md)  
[System.xml の使用法](system-xml-usage.md)  
[等値演算子](equality-operators.md)  

*©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

*2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*
  
## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
