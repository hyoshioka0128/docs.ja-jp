---
title: クラス、構造体、およびインターフェイスの名前
ms.date: 10/22/2008
helpviewer_keywords:
- type names, guidelines
- classes [.NET Framework], names
- enumerations [.NET Framework], names
- names [.NET Framework], interfaces
- common type names
- names [.NET Framework], type names
- names [.NET Framework], classes
- interfaces [.NET Framework], names
- generic type parameters
ms.assetid: 87a4b0da-ed64-43b1-ac43-968576c444ce
author: KrzysztofCwalina
ms.openlocfilehash: 2ecd708ccb8eb91270e8ef9c174b8d7e599a2629
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353703"
---
# <a name="names-of-classes-structs-and-interfaces"></a>クラス、構造体、およびインターフェイスの名前
次に示す名前付けのガイドラインは、一般的な型の名前付けに適用されます。  
  
 **✓ DO** 名前をクラスと構造体には名詞または名詞句を使用して pascal 表記を使用します。  
  
 これにより、動詞句を使用して名前が付けられたメソッドの型名が区別されます。  
  
 **✓ DO** 形容詞句、または場合によっては名詞または名詞句とインターフェイスの名前します。  
  
 名詞と名詞句を使用することはほとんどなく、型がインターフェイスではなく抽象クラスであることを示している可能性があります。  
  
 **X DO NOT** クラス名のプレフィックス ("C"など) を指定します。  
  
 **✓ CONSIDER** 基底クラスの名前のクラスを派生の名前を終了します。  
  
 これは非常に読みやすく、リレーションシップについて明確に説明しています。 このコードの例としては、`ArgumentOutOfRangeException`があります。これは `Exception`の一種であり、`SerializableAttribute`であり、`Attribute`です。 ただし、このガイドラインを適用するには、適切な判断を使用することが重要です。たとえば、`Button` クラスは `Control` イベントの一種ですが、名前に `Control` は表示されません。  
  
 **✓ DO** インターフェイス名のプレフィックス文字では、型がインターフェイスであることを示します。  
  
 たとえば、`IComponent` (わかりやすい名詞)、`ICustomAttributeProvider` (名詞句)、および `IPersistable` (形容詞) は、適切なインターフェイス名です。 他の型名と同様に、省略形を避けます。  
  
 **✓ DO** だけで、"I"プレフィックスのインターフェイスの名前、クラスがインターフェイスの標準的な実装であるクラス – インターフェイスのペアを定義するときに名前が異なることを確認してください。  
  
## <a name="names-of-generic-type-parameters"></a>ジェネリック型パラメーターの名前  
 ジェネリックが .NET Framework 2.0 に追加されました。 この機能では、*型パラメーター*と呼ばれる新しい種類の識別子が導入されました。  
  
 **✓ DO** 1 文字の名前が完全にわかり、わかりやすい名前と値を追加していない場合を除き、わかりやすい名前を持つジェネリック型パラメーターの名前します。  
  
 **✓ CONSIDER** を使用して`T`の 1 文字の型パラメーターを 1 つの種類の型パラメーター名として。  
  
```csharp  
public int IComparer<T> { ... }  
public delegate bool Predicate<T>(T item);  
public struct Nullable<T> where T:struct { ... }  
```  
  
 **✓ DO** 説明的な型パラメーター名をプレフィックス`T`です。  
  
```csharp  
public interface ISessionChannel<TSession> where TSession : ISession {  
    TSession Session { get; }  
}  
```  
  
 **✓ CONSIDER** 制約を示す名前、パラメーターの型パラメーター上に配置します。  
  
 たとえば、`ISession` に制約されたパラメーターは `TSession`と呼ばれる場合があります。  
  
## <a name="names-of-common-types"></a>共通型の名前  
 **✓ DO** から派生または特定の .NET Framework 型を実装する型の名前を付けるときは、次の表に説明されているガイドラインに従ってください。  
  
|基本型|派生/実装型のガイドライン|  
|---------------|------------------------------------------|  
|`System.Attribute`|**✓ DO** カスタム属性クラスの名前にサフィックス"Attribute"を追加します。|  
|`System.Delegate`|**✓ DO** イベントで使用されるデリゲートの名前にサフィックス"EventHandler"を追加します。<br /><br /> **✓ DO** 以外のイベント ハンドラーとして使用されているデリゲートの名前に"Callback"サフィックスを追加します。<br /><br /> **X DO NOT** 「代理」サフィックスをデリゲートに追加します。|  
|`System.EventArgs`|**✓ DO** "EventArgs です"というサフィックスを追加。|  
|`System.Enum`|**X DO NOT** 代わりに使用する言語でサポートされているキーワードを使用して; たとえば、C# の場合、次のように使用します。 このクラスから派生、`enum`キーワード。<br /><br /> **X DO NOT** 「列挙」または"Flag"サフィックスを追加|  
|`System.Exception`|**✓ DO** "Exception"サフィックスを追加|  
|`IDictionary` <br /> `IDictionary<TKey,TValue>`|**✓ DO** 「ディクショナリ」というサフィックスを追加。 `IDictionary` は特定の種類のコレクションであることに注意してくださいが、このガイドラインは、次に示す一般的なコレクションのガイドラインよりも優先されます。|  
|`IEnumerable` <br /> `ICollection` <br /> `IList` <br /> `IEnumerable<T>` <br /> `ICollection<T>` <br /> `IList<T>`|**✓ DO** 「コレクション」サフィックスを追加|  
|`System.IO.Stream`|**✓ DO** 「ストリームです」というサフィックスを追加。|  
|`CodeAccessPermission IPermission`|**✓ DO** 「権限」というサフィックスを追加。|  
  
## <a name="naming-enumerations"></a>列挙型の名前付け  
 一般的に、列挙型の名前 (列挙型とも呼ばれます) は、標準的な型の名前付け規則に従う必要があります。 ただし、列挙型に特に適用される追加のガイドラインがあります。  
  
 **✓ DO** ビット フィールドがその値がない限り、列挙体の単数形の型名を使用します。  
  
 **✓ DO** ビット フィールドを持つ列挙体の複数形の型名を使用して値として、フラグ列挙型とも呼ばれます。  
  
 **X DO NOT** 列挙型の型名で、「列挙」サフィックスを使用します。  
  
 **X DO NOT** 「フラグを設定」を使用して、または"Flags"サフィックス列挙型では、名前を入力します。  
  
 **X DO NOT** リッチ テキストの列挙型などの列挙値の名前 (例:"ad"ADO 列挙型の場合。)、"rtf"に対して、プレフィックスを使用します。  
  
 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*  
  
 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*  
  
## <a name="see-also"></a>参照

- [フレームワーク デザインのガイドライン](../../../docs/standard/design-guidelines/index.md)
- [名前付けのガイドライン](../../../docs/standard/design-guidelines/naming-guidelines.md)
