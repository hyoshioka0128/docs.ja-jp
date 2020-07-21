---
title: 構造体のデザイン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- deallocating structures
- allocating structures
- value types, structures
- structure design
- type design guidelines, structures
- structures [.NET Framework], design guidelines
ms.assetid: 1f48b2d8-608c-4be6-9ba4-d8f203ed9f9f
ms.openlocfilehash: c6ac53014e048da3a90dd7b8e961176f61e90355
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290812"
---
# <a name="struct-design"></a>構造体のデザイン
汎用値型は、ほとんどの場合、構造体である C# キーワードと呼ばれます。 このセクションでは、一般的な構造体のデザインに関するガイドラインを示します。

 ❌構造体にパラメーターなしのコンストラクターを指定しないでください。

 このガイドラインに従うことで、配列の各項目に対してコンストラクターを実行しなくても、構造体の配列を作成できます。 C# では、構造体にパラメーターなしのコンストラクターを含めることはできないことに注意してください。

 ❌変更可能な値の型は定義しないでください。

 変更可能な値の型にはいくつかの問題があります。 たとえば、プロパティ getter が値型を返す場合、呼び出し元はコピーを受け取ります。 コピーは暗黙的に作成されるため、開発者は元の値ではなくコピーを変更することを認識していない可能性があります。 また、一部の言語 (特に動的言語) では、変更可能な値型を使用した場合に問題が発生します。これは、ローカル変数でも逆参照した場合にコピーが作成されるためです。

 ✔️、すべてのインスタンスデータが0、false、または null (必要に応じて) に設定されている状態であることを確認します。

 これにより、構造体の配列が作成されたときに無効なインスタンスが誤って作成されるのを防ぐことができます。

 ✔️ <xref:System.IEquatable%601> 値型に実装します。

 <xref:System.Object.Equals%2A?displayProperty=nameWithType>値型のメソッドではボックス化が行われますが、リフレクションを使用するため、既定の実装はあまり効率的ではありません。 <xref:System.IEquatable%601.Equals%2A>パフォーマンスを大幅に向上させることができ、ボックス化が行われないように実装できます。

 ❌を明示的に拡張しないで <xref:System.ValueType> ください。 実際、ほとんどの言語ではこれを回避できます。

 一般に、構造体は非常に便利ですが、頻繁にボックス化されない小さな単一の変更できない値に対してのみ使用してください。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [型デザインのガイドライン](type.md)
- [フレームワークデザインのガイドライン](index.md)
- [クラスまたは構造体の選択](choosing-between-class-and-struct.md)
