---
title: x:FactoryMethod ディレクティブ
ms.date: 03/30/2017
helpviewer_keywords:
- XAML. x:FactoryMethod directive [XAML Services]
- FactoryMethod directive in XAML [XAML Services]
- x:FactoryMethod directive [XAML Services]
ms.assetid: 829bcbdf-5318-4afb-9a03-c310e0d2f23d
ms.openlocfilehash: 5e864b6f5d664b079036a5d915e2f6f81b83639f
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432786"
---
# <a name="xfactorymethod-directive"></a>x:FactoryMethod ディレクティブ
XAML プロセッサがバッキング型を解決した後にオブジェクトを初期化するために使用するコンストラクター以外のメソッドを指定します。  
  
## <a name="xaml-attribute-usage-no-xarguments"></a>XAML 属性の使用方法、x なし:引数  
  
```xaml  
<object x:FactoryMethod="methodname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-attribute-usage-xarguments-as-elements"></a>XAML 属性の使用方法、x: 要素としての引数  
  
```xaml  
<object x:FactoryMethod="methodname"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`methodname`|として`object`指定されたインスタンスを初期化するために XAML プロセッサが呼び出すメソッドの文字列メソッド名。 「解説」を参照してください。|  
|`oneOrMoreObjectElements`|ファクトリ メソッド のパラメーターを指定するオブジェクトの 1 つ以上のオブジェクト要素。 順序は重要です。これは、引数がファクトリメソッドに渡される順序を示します。|  
  
## <a name="remarks"></a>解説  
 インスタンス`methodname`メソッドの場合、修飾できません。  
  
 ファクトリ メソッドとしての静的メソッドがサポートされています。 静的`methodname`メソッドの場合は、`methodname`静的ファクトリ メソッド`typeName.methodName`を定義する`typeName`クラスを名前を指定する組み合わせとして提供されます。 `typeName`マップされた xmlns 内の型を参照する場合は、プレフィックス修飾できます。 `typeName`とは異なる型を`typeof(object)`指定できます。  
  
 ファクトリ メソッドは、関連するオブジェクト要素をバックする型の宣言済みのパブリック メソッドである必要があります。  
  
 ファクトリ メソッドは、関連オブジェクトに割り当て可能なインスタンスを返す必要があります。 ファクトリ メソッドは null を返しません。  
  
 `x:Arguments`ファクトリメソッドのシグネチャに最適な一致の原則に基づいて動作します。 一致は、最初にパラメーター数を評価します。 パラメーター数に対して複数の一致が可能な場合、パラメーターの型が評価され、最適な一致が判別されます。 この評価フェーズの後にあいまいな状態が続く場合、XAML プロセッサの動作は未定義です。  
  
 ディレクティブ`x:FactoryMethod`マークアップは、含んでいるオブジェクト要素の型を参照しないため、要素の使用法は、一般的な意味でのプロパティ要素の使用ではありません。 要素の使用は属性の使用よりも一般的ではないと予想されます。 `x:Arguments`(属性または要素の使用法) は、要素`x:FactoryMethod`の使用方法と共に使用できますが、これは Usage セクションに特に示されていません。  
  
 `x:FactoryMethod`要素は、他のプロパティ要素の前にする必要があり、要素`x:Arguments`としても指定される前に、コンテンツ/内部テキスト/初期化テキストの前にする必要があります。  
  
## <a name="see-also"></a>関連項目

- [x:Arguments ディレクティブ](xarguments-directive.md)
