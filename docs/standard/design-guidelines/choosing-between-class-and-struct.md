---
title: クラスまたは構造体の選択
description: 型をクラスとしてデザインするか、構造体として型をデザインするかを決定する方法について説明します。 .NET での参照型と値型の違いについて説明します。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- class library design guidelines [.NET Framework], classes
- structures [.NET Framework], vs. classes
- classes [.NET Framework], design guidelines
- type design guidelines, structures
- structures [.NET Framework], design guidelines
- classes [.NET Framework], vs. structures
- type design guidelines, classes
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
ms.openlocfilehash: 9d757e77292c1226fbe2328cce082033ae8f7003
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662603"
---
# <a name="choosing-between-class-and-struct"></a>クラスまたは構造体の選択
すべてのフレームワークデザイナーの面で基本的な設計上の決定事項の1つは、型をクラスとしてデザインするか (参照型)、または構造体 (値型) として設計するかということです。 この選択を行うには、参照型と値型の動作の違いをよく理解していることが重要です。

 参照型と値型の間の最初の違いは、参照型がヒープに割り当てられ、ガベージコレクトされるのに対し、値型はスタックまたはインラインの型に割り当てられ、スタックのアンワインドまたはそれを含んでいる型の割り当てが解除されるときに割り当てが解除されるという点です。 したがって、値型の割り当てと割り当て解除は、参照型の割り当てと割り当て解除よりも一般的に低コストです。

 次に、参照型の配列はアウトオブラインで割り当てられます。つまり、配列要素は、ヒープに存在する参照型のインスタンスへの参照にすぎません。 値型の配列はインラインで割り当てられます。つまり、配列要素は値型の実際のインスタンスです。 したがって、値型の配列の割り当てと割り当て解除は、参照型の配列の割り当てと割り当て解除よりもはるかに安価です。 また、ほとんどの場合、値型の配列は参照の局所性が大幅に向上します。

 次の相違点は、メモリ使用量に関連します。 参照型または実装するインターフェイスのいずれかにキャストすると、値型はボックス化されます。 値型にキャストされると、ボックス化が解除されます。 ボックスはヒープに割り当てられ、ガベージコレクトされるオブジェクトであるため、ボックス化とボックス化解除が過剰になると、ヒープ、ガベージコレクター、および最終的にアプリケーションのパフォーマンスに悪影響を及ぼす可能性があります。  これに対し、参照型がキャストされると、このようなボックス化は行われません。 (詳細については、「[ボックス化とボックス化解除](../../csharp/programming-guide/types/boxing-and-unboxing.md)」を参照してください)。

 次に、参照型の割り当てによって参照がコピーされます。一方、値型の割り当てでは、値全体がコピーされます。 したがって、大きな参照型の割り当ては、大きな値型の割り当てよりもコストが高くなります。

 最後に、参照型は参照によって渡されるのに対し、値型は値によって渡されます。 参照型のインスタンスへの変更は、そのインスタンスを指すすべての参照に影響します。 値型のインスタンスは、値によって渡されるときにコピーされます。 値型のインスタンスが変更された場合、当然、そのインスタンスのコピーには影響しません。 コピーはユーザーによって明示的に作成されるのではなく、引数が渡されるときに暗黙的に作成されるため、または戻り値が返される場合、変更可能な値型は多くのユーザーに混乱を招く可能性があります。 したがって、値型は不変である必要があります。

 経験則として、フレームワークのほとんどの型はクラスである必要があります。 ただし、場合によっては、値型の特性によって、構造体を使用する方が適切であることがあります。

 型のインスタンスが小さく、通常は短い有効期間であるか、または他のオブジェクトに埋め込まれている場合は、クラスではなく構造体を定義する✔️ます。

 ❌型に次の特性がすべて含まれている場合を除き、構造体を定義しないでください。

- プリミティブ型 (、など) と同様に、論理的には単一の値を表し `int` `double` ます。

- インスタンスのサイズは16バイト未満です。

- 変更できません。

- 頻繁にボックス化する必要はありません。

 それ以外の場合は、型をクラスとして定義する必要があります。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [型デザインのガイドライン](type.md)
- [フレームワークデザインのガイドライン](index.md)
