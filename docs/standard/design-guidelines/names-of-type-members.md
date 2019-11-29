---
title: 型のメンバーの名前
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], names
- methods [.NET Framework], names
- type members
- properties [.NET Framework], names
- fields, names
- field names
- names [.NET Framework], type members
- members [.NET Framework], type
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
author: KrzysztofCwalina
ms.openlocfilehash: b4da14575d29582814d32a3050087b7acc0da802
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353704"
---
# <a name="names-of-type-members"></a>型のメンバーの名前
型は次のメンバーで構成されています: メソッド、プロパティ、イベント、コンストラクター、フィールド。 次のセクションは、型のメンバーに名前を付けるためのガイドラインを示しています。  
  
## <a name="names-of-methods"></a>メソッドの名前  
 メソッドはアクションを実行する手段であるため、デザインのガイドラインでは、メソッド名を動詞または動詞句にする必要があります。 また、このガイドラインに従うと、名詞句または形容詞句であるプロパティ名および型名と、メソッド名を区別するためにも機能します。  
  
 **✓ DO**: 動詞または動詞句のメソッド名を指定します。  
  
```csharp  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
```  
  
## <a name="names-of-properties"></a>プロパティの名前  
 他のメンバーとは異なり、プロパティには名詞句または形容詞の名前を指定する必要があります。 つまり、プロパティはデータを参照するため、プロパティの名前にはデータが反映されます。 プロパティ名には、常に Pascal 形式が使用されます。  
  
 **✓ DO**: 名詞、名詞句、または形容詞を使用してプロパティに名前を付けます。  
  
 **X DO NOT**: 次の例のように、"Get" メソッドの名前と一致するプロパティを使用しないでください。  
  
 `public string TextWriter { get {...} set {...} }`  
 `public string GetTextWriter(int value) { ... }`  
  
 通常、このパターンは、プロパティが実際にメソッドであることを示します。  
  
 **✓ DO**: "List" または "Collection" が続く単数形の語句を使用する代わりに、コレクション内のアイテムを示す複数形の語句で、コレクション プロパティに名前を付けます。  
  
 **✓ DO**: 肯定の語句 (`CanSeek` ではなく `CantSeek`) を使用して、ブール値のプロパティに名前を付けます。 また、ブール値のプロパティに "Is"、"Can"、または "Has" のプレフィックスを使用することもできますが、値を追加する場所のみです (オプション)。  
  
 **✓ CONSIDER**: プロパティの型と同じ名前をプロパティに指定します。  
  
 たとえば、次のプロパティは、`Color` という名前の列挙値を適切に取得および設定するため、プロパティは `Color` という名前になります。  
  
```csharp  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## <a name="names-of-events"></a>イベントの名前  
 イベントは常に、発生中のアクションまたは発生したアクションのいずれかのアクションを参照します。 そのため、メソッドと同様、イベントには動詞の名前が付けられ、イベントが発生した時刻を示すために動詞の時制が使用されます。  
  
 **✓ DO**: 動詞または動詞句を使ってイベントに名前を付けます。  
  
 例として、`Clicked`、`Painting`、`DroppedDown` などがあります。  
  
 **✓ DO**: 現在形や過去形を使って、イベント名に前と後の概念を指定します。  
  
 たとえば、ウィンドウを閉じる前に発生するクローズ イベントは `Closing` と呼ばれ、ウィンドウを閉じた後に発生するクローズ イベントは `Closed` と呼ばれます。  
  
 **X DO NOT**: プリイベントとポストイベントを示すために、"Before" や "After" の接頭辞または接尾辞を使用しないでください。 前述のように、現在形と過去形を使用します。  
  
 **✓ DO**: 次の例に示すように、イベント ハンドラー (イベントの型として使用されるデリゲート) に "EventHandler" サフィックスを使って名前を付けます。  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ DO**: イベント ハンドラーに `sender` と `e` という名前の 2 つのパラメーターを使用します。  
  
 sender パラメーターは、イベントを発生させたオブジェクトを表します。 より具体的な型を使用できる場合も、通常、sender パラメーターの型は `object` になります。  
  
 **✓ DO**: "EventArgs" サフィックスを使ってイベントの引数クラスに名前を付けます。  
  
## <a name="names-of-fields"></a>フィールドの名前  
 フィールドの名前付けのガイドラインは、静的パブリック フィールドと保護されたフィールドを対象とします。 内部フィールドとプライベート フィールドは、ガイドラインの対象ではありません。また、パブリック インスタンス フィールドや保護されたインスタンス フィールドは、「[メンバーのデザインのガイドライン](../../../docs/standard/design-guidelines/member.md)」で許可されていません。  
  
 **✓ DO**: フィールド名に Pascal 形式を使用します。  
  
 **✓ DO**: 名詞、名詞句、または形容詞を使用してフィールドに名前を付けます。  
  
 **X DO NOT**: フィールド名にプレフィックスを使用しないでください。  
  
 たとえば、静的フィールドを示すために、"g_" や "s_" を使用しないでください。  
  
 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*  
  
 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*  
  
## <a name="see-also"></a>参照

- [フレームワーク デザインのガイドライン](../../../docs/standard/design-guidelines/index.md)
- [名前付けのガイドライン](../../../docs/standard/design-guidelines/naming-guidelines.md)
