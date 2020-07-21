---
title: 一般的な名前付け規則
description: 単語の選択に関連する一般的な名前付け規則、略語と頭字語の使用に関するガイドライン、および言語固有の名前を回避するためのガイダンスを使用します。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], conflicts
- type names, conflicts
- language-specific type names
- names [.NET Framework], about naming guidelines
- names [.NET Framework], abbreviations
- abbreviation naming guidelines
- acronym naming guidelines
- Hungarian notation
- names [.NET Framework], type names
- names [.NET Framework], acronyms
ms.assetid: d3a77ea1-75d2-4969-a8c3-3e1e3e1aaedc
ms.openlocfilehash: b7f06a57c57800afcfa7febf9452094b4ad5ddc1
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769081"
---
# <a name="general-naming-conventions"></a>一般的な名前付け規則

ここでは、単語の選択に関連する一般的な名前付け規則、略語と頭字語の使用に関するガイドライン、および言語固有の名前の使用を回避するための推奨事項について説明します。

## <a name="word-choice"></a>単語の選択
 ✔️は、簡単に判読できる識別子名を選択します。

 たとえば、という名前のプロパティは、 `HorizontalAlignment` よりも英語で読みやすく `AlignmentHorizontal` なります。

 ✔️簡潔にするために読みやすさを優先します。

 プロパティ名 `CanScrollHorizontally` は、 `ScrollableX` (X 軸へのあいまいな参照) よりも優れています。

 ❌アンダースコア、ハイフン、またはその他の英数字以外の文字は使用しないでください。

 ❌ハンガリー表記法は使用しないでください。

 ❌広く使用されているプログラミング言語のキーワードと競合する識別子を使用しないようにします。

 共通言語仕様 (CLS) の規則4に従って、すべての準拠言語は、その言語のキーワードを識別子として使用する名前付き項目へのアクセスを許可する機構を提供する必要があります。 たとえば、C# では、この場合、エスケープメカニズムとして @ sign が使用されます。 ただし、エスケープシーケンスではなく1つのメソッドを使用する方がはるかに困難であるため、一般的なキーワードを避けることをお勧めします。

## <a name="using-abbreviations-and-acronyms"></a>省略形と頭字語の使用
 ❌識別子名の一部として省略形または短縮形を使用しないでください。

 たとえば、で `GetWindow` はなくを使用 `GetWin` します。

 ❌広く受け入れられていない頭字語は使用せず、必要な場合にのみ使用してください。

## <a name="avoiding-language-specific-names"></a>言語固有の名前の回避
 型名の言語固有のキーワードではなく、意味的に興味深い名前を使用する✔️ます。

 たとえば、 `GetLength` はよりもわかりやすい名前です `GetInt` 。

 通常は、言語固有の名前ではなく、汎用的な CLR 型名を使用します。これは、識別子が型以外のセマンティックの意味を持たない場合に、まれに発生します。✔️

 たとえば、に変換するメソッドは、では <xref:System.Int64> なくという名前にする必要があり `ToInt64` `ToLong` <xref:System.Int64> ます (は C# 固有のエイリアスの CLR 名であるため `long` )。 次の表は、CLR 型名を使用したいくつかの基本データ型 (C#、Visual Basic、および C++ の対応する型名) を示しています。

|C#|Visual Basic|C++|CLR|
|---------|------------------|-----------|---------|
|**sbyte**|**SByte**|**char**|**SByte**|
|**byte**|**Byte**|**unsigned char**|**Byte**|
|**short**|**短い**|**short**|**Int16**|
|**ushort**|**UInt16**|**unsigned short**|**UInt16**|
|**int**|**整数**|**int**|**Int32**|
|**uint**|**UInt32**|**unsigned int**|**UInt32**|
|**long**|**Long**|**__int64**|**Int64**|
|**ulong**|**UInt64**|**unsigned __int64**|**UInt64**|
|**float**|**Single**|**float**|**Single**|
|**double**|**Double**|**double**|**Double**|
|**bool**|**Boolean**|**bool**|**Boolean**|
|**char**|**Char**|**wchar_t**|**Char**|
|**string**|**String**|**String**|**String**|
|**object**|**Object**|**Object**|**Object**|

 一般的な名前 (やなど) は、型名を繰り返すのではなく、通常の名前を使用します。たとえば、識別子に意味が `value` `item` なく、パラメーターの型が重要でない場合には、型名を繰り返すのではなく、✔️ます。

## <a name="naming-new-versions-of-existing-apis"></a>既存の Api の新しいバージョンの命名
 既存の API の新しいバージョンを作成するときに、古い API に似た名前を使用✔️ます。

 これは、Api 間の関係を強調表示するのに役立ちます。

 ✔️は、既存の API の新しいバージョンを示すために、プレフィックスではなくサフィックスを追加することをお勧めします。

 これにより、ドキュメントを参照したり、IntelliSense を使用したりするときに検出がサポートされます。 以前のバージョンの API は、ほとんどのブラウザーや IntelliSense がアルファベット順に識別子を表示するため、新しい Api の近くに編成されます。

 サフィックスまたはプレフィックスを追加するのではなく、新しいがわかりやすい識別子を使用する✔️ます。

 ✔️は、既存の API の新しいバージョンを示すために数字のサフィックスを使用します。特に、API の既存の名前が意味のある唯一の名前 (業界標準の場合) であり、意味のあるサフィックス (または名前の変更) を追加することは適切ではありません。

 ❌同じ API の以前のバージョンと区別するために、識別子に "Ex" (または同様の) サフィックスを使用しないでください。

 ✔️は、32ビット整数ではなく64ビット整数 (long 整数) で動作する Api のバージョンを導入するときに、"64" サフィックスを使用します。 既存の32ビット API が存在する場合にのみ、このアプローチを行う必要があります。これは、64ビットバージョンのみの新しい Api では使用しないでください。

 *部分 &copy; 2005、2009 Microsoft Corporation。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワーク デザインのガイドライン](index.md)
- [名前付けのガイドライン](naming-guidelines.md)
- [EditorConfig での .NET の名前付け規則](/visualstudio/ide/editorconfig-naming-conventions)
