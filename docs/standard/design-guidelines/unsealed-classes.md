---
title: シールされていないクラス
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- classes [.NET Framework], unsealed
- unsealed classes
- inheritance, classes
ms.assetid: 9a3bd505-90f5-4053-9f0d-3cf5fa3d3ebf
ms.openlocfilehash: 8e332a6382cf644c82d5e26cf5234cea08dcc693
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289552"
---
# <a name="unsealed-classes"></a>シールされていないクラス
シールされたクラスはから継承できません。また、拡張を防ぎます。 これに対し、から継承できるクラスは、シールされていないクラスと呼ばれます。

 仮想メンバーまたはプロテクトメンバーを追加せずに封印されていないクラスを使用することを検討してください。これは、フレームワークに対して非常に優れた拡張性を提供する優れた方法です。✔️

 開発者は、カスタムコンストラクター、新しいメソッド、メソッドオーバーロードなどの便利なメンバーを追加するために、シールされていないクラスから継承することがよくあります。 たとえば、 `System.Messaging.MessageQueue` は封印されていないので、ユーザーは特定のキューパスを既定とするカスタムキューを作成したり、特定のシナリオで API を簡略化するカスタムメソッドを追加したりできます。

 ほとんどのプログラミング言語では、クラスは既定で封印されていません。これは、フレームワークのほとんどのクラスで既定でも推奨されます。 封印されていない型によって実現される機能拡張は、フレームワークユーザーにとって非常に歓迎されており、封印されていない型に関連するテストコストが比較的低いため、非常に安価です

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [機能拡張のデザイン](designing-for-extensibility.md)
- [シール](sealing.md)
