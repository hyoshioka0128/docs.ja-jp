---
title: リソースに名前を付ける
description: .NET でのリソースの名前付けガイドラインを確認します。これは、プロパティの名前付けのガイドラインに似ています。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], localized resources
- localization, naming guidelines
- resource names
- global applications, naming guidelines
- international applications, naming guidelines
ms.assetid: 8b0e97f3-7877-44fd-bc76-e05d36d5d79c
ms.openlocfilehash: 765337bcf9fad4f9a8c9272a15b5c77d02770471
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768249"
---
# <a name="naming-resources"></a>リソースに名前を付ける
ローカライズ可能なリソースは、プロパティのように特定のオブジェクトを介して参照できるので、リソースの名前付けガイドラインはプロパティガイドラインに似ています。

 リソースキーでは、✔️の大文字と小文字の区別を使用します。

 ✔️は、短い識別子ではなく説明を入力します。

 ❌メインの CLR 言語の言語固有のキーワードは使用しないでください。

 ✔️リソースには英数字とアンダースコアのみを使用します。

 ✔️例外メッセージリソースには、次の名前付け規則を使用します。

 リソース識別子は、例外の種類の名前に例外の短い識別子を加えたものにする必要があります。

 `ArgumentExceptionIllegalCharacters` `ArgumentExceptionInvalidName`
 `ArgumentExceptionFileNameIsMalformed`

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [名前付けのガイドライン](naming-guidelines.md)
