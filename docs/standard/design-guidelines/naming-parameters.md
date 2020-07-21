---
title: パラメーターに名前を付ける
description: パラメーターの名前付けのガイドラインについて説明します。 たとえば、説明的なパラメーター名 & camel 形式で使用し、型ではなく意味に基づいて名前を付ける & を検討します。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: 54f37c4d6a0f9a6931fa69d612bf0e45bf1f2ce7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84583519"
---
# <a name="naming-parameters"></a>パラメーターに名前を付ける
読みやすくするために、パラメーター名のガイドラインに従うことが重要です。これは、ビジュアルデザインツールが Intellisense とクラス参照機能を提供する場合に、ドキュメントとデザイナーにパラメーターが表示されるためです。

 パラメーター名にキャメルを使用する✔️ます。

 ✔️、説明的なパラメーター名を使用します。

 パラメーターの型ではなく、パラメーターの意味に基づいて名前を使用することを✔️してください。

### <a name="naming-operator-overload-parameters"></a>演算子のオーバーロードパラメーターの名前付け
 `left` `right` パラメーターに意味がない場合は、二項演算子のオーバーロードパラメーター名に and を使用✔️ます。

 `value`パラメーターに意味がない場合は、単項演算子のオーバーロードパラメーター名には✔️を使用します。

 ✔️演算子を使用すると、有意な値が追加されます。

 ❌演算子のオーバーロードパラメーター名には、省略形または数値インデックスを使用しないでください。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [名前付けのガイドライン](naming-guidelines.md)
