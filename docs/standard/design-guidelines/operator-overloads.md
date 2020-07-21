---
title: 演算子のオーバーロード
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- operators [.NET Framework], overloads
- names [.NET Framework], overloaded operators
- member design guidelines, operators
- overloaded operators
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
ms.openlocfilehash: 893b7d1f76dfb059a0ddca77dfd8654812e9ae12
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289734"
---
# <a name="operator-overloads"></a>演算子のオーバーロード
演算子のオーバーロードでは、フレームワーク型を組み込みの言語プリミティブとして表示できます。

 一部の状況では許可および便利ですが、演算子のオーバーロードは慎重に使用する必要があります。 多くの場合、演算子のオーバーロードは不正使用されています。たとえば、framework デザイナーが、単純なメソッドである必要がある操作に対して演算子の使用を開始した場合などです。 次のガイドラインは、演算子のオーバーロードを使用するタイミングと方法を決定するのに役立ちます。

 ❌プリミティブ (組み込み) 型のように感じられる型以外は、演算子のオーバーロードを定義しないようにします。

 プリミティブ型のように感じられる型に演算子のオーバーロードを定義する✔️ます。

 たとえば、に <xref:System.String?displayProperty=nameWithType> はがあり、が `operator==` `operator!=` 定義されています。

 数値を表す構造体 (など) では、演算子のオーバーロードを定義✔️ <xref:System.Decimal?displayProperty=nameWithType> ます。

 ❌演算子のオーバーロードを定義する場合は、かわいらしいしないでください。

 演算子のオーバーロードは、操作の結果がすぐにわかる場合に便利です。 たとえば、ある型を <xref:System.DateTime> 別のから減算してを取得できるようにすることは理にかなって `DateTime` <xref:System.TimeSpan> います。 ただし、2つのデータベースクエリを結合する場合や、shift 演算子を使用してストリームに書き込む場合は、論理和演算子を使用するのは適切ではありません。

 ❌少なくとも1つのオペランドがオーバーロードを定義する型でない限り、演算子のオーバーロードを指定しないでください。

 ✔️は、対称方式で演算子をオーバーロードします。

 たとえば、をオーバーロードする場合は、 `operator==` もオーバーロードする必要があり `operator!=` ます。 同様に、をオーバーロードする場合は、も同様に `operator<` オーバーロードする必要があり `operator>` ます。

 オーバーロードされた各演算子に対応するフレンドリ名を使用して、メソッドを指定する✔️ます。

 多くの言語では、演算子のオーバーロードはサポートされていません。 このため、オーバーロード演算子には、同等の機能を提供するドメイン固有の適切な名前を持つ二次的なメソッドが含まれていることをお勧めします。

 次の表に、演算子とそれに対応するわかりやすいメソッド名の一覧を示します。

|C# 演算子シンボル|メタデータ名|フレンドリ名|
|-------------------------|-------------------|-------------------|
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|
|`+ (binary)`|`op_Addition`|`Add`|
|`- (binary)`|`op_Subtraction`|`Subtract`|
|`* (binary)`|`op_Multiply`|`Multiply`|
|`/`|`op_Division`|`Divide`|
|`%`|`op_Modulus`|`Mod or Remainder`|
|`^`|`op_ExclusiveOr`|`Xor`|
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|
|<code>&#124;</code>|`op_BitwiseOr`|`BitwiseOr`|
|`&&`|`op_LogicalAnd`|`And`|
|<code>&#124;&#124;</code>|`op_LogicalOr`|`Or`|
|`=`|`op_Assign`|`Assign`|
|`<<`|`op_LeftShift`|`LeftShift`|
|`>>`|`op_RightShift`|`RightShift`|
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|
|`==`|`op_Equality`|`Equals`|
|`!=`|`op_Inequality`|`Equals`|
|`>`|`op_GreaterThan`|`CompareTo`|
|`<`|`op_LessThan`|`CompareTo`|
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|
|`<=`|`op_LessThanOrEqual`|`CompareTo`|
|`*=`|`op_MultiplicationAssignment`|`Multiply`|
|`-=`|`op_SubtractionAssignment`|`Subtract`|
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|
|`%=`|`op_ModulusAssignment`|`Mod`|
|`+=`|`op_AdditionAssignment`|`Add`|
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|
|<code>&#124;=</code>|`op_BitwiseOrAssignment`|`BitwiseOr`|
|`,`|`op_Comma`|`Comma`|
|`/=`|`op_DivisionAssignment`|`Divide`|
|`--`|`op_Decrement`|`Decrement`|
|`++`|`op_Increment`|`Increment`|
|`- (unary)`|`op_UnaryNegation`|`Negate`|
|`+ (unary)`|`op_UnaryPlus`|`Plus`|
|`~`|`op_OnesComplement`|`OnesComplement`|

### <a name="overloading-operator-"></a>オーバーロード演算子 = =
 オーバーロード `operator ==` は非常に複雑です。 演算子のセマンティクスは、など、他のいくつかのメンバーと互換性がある必要があり <xref:System.Object.Equals%2A?displayProperty=nameWithType> ます。

### <a name="conversion-operators"></a>変換演算子
 変換演算子は、ある型から別の型への変換を可能にする単項演算子です。 演算子は、オペランドまたは戻り値の型のいずれかの静的メンバーとして定義する必要があります。 変換演算子には、暗黙的と明示的の2種類があります。

 ❌エンドユーザーがこのような変換を明確に想定していない場合は、変換演算子を指定しないでください。

 ❌型のドメインの外に変換演算子を定義しないでください。

 たとえば、、 <xref:System.Int32> 、 <xref:System.Double> およびは <xref:System.Decimal> すべて数値型ですが、 <xref:System.DateTime> はではありません。 したがって、をに変換する変換演算子は存在しない必要があり `Double(long)` `DateTime` ます。 このような場合は、コンストラクターを使用することをお勧めします。

 ❌変換が損失する可能性がある場合は、暗黙的な変換演算子を指定しないでください。

 たとえば、からへの暗黙の型変換を行うことはできません `Double` `Int32` 。の `Double` 範囲がより大きくなるため `Int32` です。 変換が損失する可能性がある場合でも、明示的な変換演算子を指定できます。

 ❌暗黙のキャストから例外をスローしないでください。

 変換が行われていることを認識していない可能性があるため、エンドユーザーは何が起こっているかを理解することは非常に困難です。

 キャスト演算子の呼び出しによって損失を伴う変換が発生 <xref:System.InvalidCastException?displayProperty=nameWithType> し、演算子のコントラクトでは損失が生じない変換が許可されていない場合、✔️スローします。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [メンバーデザインのガイドライン](member.md)
- [フレームワークデザインのガイドライン](index.md)
