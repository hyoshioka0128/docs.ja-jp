---
title: アクセス レベル
ms.date: 05/10/2018
helpviewer_keywords:
- members [Visual Basic], accessing in Visual Basic
- Friend access modifier
- access levels, declared elements
- access levels
- access modifiers
- Public access modifier
- Protected access modifier
- Protected Friend access modifier
- Private Protected access modifier
- Private access modifier
- declared elements [Visual Basic], access level
ms.assetid: 6e06c1ab-fd78-47f0-83a8-1152780b5e1a
ms.openlocfilehash: 33a218a2acc3c876428d6c9a887280a559f84323
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348679"
---
# <a name="access-levels-in-visual-basic"></a>Visual Basic でのアクセス レベル

宣言された要素の*アクセス レベル*は、それにアクセスする機能の範囲、つまり、読み取りまたは書き込みのアクセス許可があるコードです。 これは、要素自体を宣言する方法だけでなく、要素のコンテナーのアクセス レベルによっても決定されます。 コンテナー要素にアクセスできないコードは、`Public` として宣言されていても、格納されている要素のいずれにもアクセスできません。 たとえば、`Private` 構造体の `Public` 変数は、構造体を含むクラス内からアクセスできますが、そのクラスの外部からはアクセスできません。

## <a name="public"></a>Public

宣言ステートメント内の [Public](../../../language-reference/modifiers/public.md) キーワードは、要素に、同じプロジェクト内の任意の場所のコードから、プロジェクトを参照する他のプロジェクトから、およびプロジェクトからビルドされた任意のアセンブリからアクセスできることを指定します。 次のコードは、サンプルの `Public` 宣言を示しています。

```vb
Public Class ClassForEverybody
```

`Public` は、モジュール、インターフェイス、または名前空間レベルでのみ使用できます。 つまり、Public 要素は、ソース ファイルまたは名前空間のレベルで、またはインターフェイス、モジュール、クラス、または構造体の内部で宣言できますが、プロシージャ内では宣言できません。
  
## <a name="protected"></a>Protected

宣言ステートメントの [Protected](../../../language-reference/modifiers/protected.md) キーワードは、要素にアクセスできるのは、同じクラス内から、またはこのクラスから派生したクラスからのみであることを指定します。 次のコードは、サンプルの `Protected` 宣言を示しています。

```vb
Protected Class ClassForMyHeirs
```

`Protected` は、クラス レベルでのみ、およびクラスのメンバーを宣言する場合にのみ使用できます。 つまり、Protected 要素はクラスで宣言できますが、ソース ファイルまたは名前空間のレベル、またはインターフェイス、モジュール、構造体、またはプロシージャの内部では宣言できません。

## <a name="friend"></a>Friend

宣言ステートメントの [Friend](../../../language-reference/modifiers/friend.md) キーワードは、要素には同じアセンブリ内からアクセスできますが、アセンブリの外部からはアクセスできないことを指定します。 次のコードは、サンプルの `Friend` 宣言を示しています。

```vb
Friend stringForThisProject As String
```

`Friend` は、モジュール、インターフェイス、または名前空間レベルでのみ使用できます。 つまり、Friend 要素は、ソース ファイルまたは名前空間のレベルで、またはインターフェイス、モジュール、クラス、または構造体の内部で宣言できますが、プロシージャ内では宣言できません。

## <a name="protected-friend"></a>Protected Friend

宣言ステートメントの [Protected Friend](../../../language-reference/modifiers/protected-friend.md) キーワードの組み合わせは、派生クラスまたは同じアセンブリ内、またはその両方から要素にアクセスできることを指定します。 次のコードは、サンプルの `Protected Friend` 宣言を示しています。

```vb
Protected Friend stringForProjectAndHeirs As String
```

`Protected Friend` は、クラス レベルでのみ、およびクラスのメンバーを宣言する場合にのみ使用できます。 つまり、Protected Friend 要素はクラスで宣言できますが、ソース ファイルまたは名前空間のレベル、またはインターフェイス、モジュール、構造体、またはプロシージャの内部では宣言できません。

## <a name="private"></a>Private

宣言ステートメントの [Private](../../../language-reference/modifiers/private.md) キーワードは、要素にアクセスできるのは、同じモジュール、クラス、または構造体内からのみであることを指定します。 次のコードは、サンプルの `Private` 宣言を示しています。

```vb
Private _numberForMeOnly As Integer
```

`Private` は、モジュール レベルでのみ使用できます。 つまり、Private 要素はモジュール、クラス、または構造体内で宣言できますが、ソース ファイルまたは名前空間のレベル、インターフェイス内、またはプロシージャ内では宣言できません。

モジュール レベルでは、アクセス レベルのキーワードのない `Dim` ステートメントは、`Private` 宣言に相当します。 ただし、`Private` キーワードを使用して、コードを読みやすくし、解釈しやすくすることもできます。

## <a name="private-protected"></a>Private Protected

宣言ステートメントで [Private Protected](../../../language-reference/modifiers/private-protected.md) キーワードの組み合わせを使用すると、要素には、同じクラス内からだけでなく、含まれているクラスと同じアセンブリ内にある派生クラスからもアクセスできることが指定されます。 `Private Protected` アクセス修飾子は Visual Basic 15.5 以降でサポートされています。

次の例は、`Private Protected` 宣言を示しています。

```vb
Private Protected internalValue As Integer
```

`Private Protected` 要素は、クラス内でのみ宣言できます。 インターフェイスまたは構造体内で宣言することはできません。また、ソース ファイルまたは名前空間のレベル、インターフェイスまたは構造体の内部、またはプロシージャ内で宣言することもできません。

`Private Protected` アクセス修飾子は Visual Basic 15.5 以降でサポートされています。 これを使用するには、次の要素を Visual Basic プロジェクト ( *\*.vbproj*) ファイルに追加します。 システムに Visual Basic 15.5 以降がインストールされている限り、Visual Basic コンパイラの最新バージョンでサポートされているすべての言語機能を利用できます。

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

`Private Protected` アクセス修飾子を使用するには、次の要素を Visual Basic プロジェクト ( *\*.vbproj*) ファイルに追加します。

```xml
<PropertyGroup>
   <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

詳細については、[Visual Basic 言語バージョンの設定](../../../language-reference/configure-language-version.md)に関するページを参照してください。

## <a name="access-modifiers"></a>アクセス修飾子

アクセス レベルを指定するキーワードは、*アクセス修飾子*と呼ばれます。 アクセス修飾子の比較を次の表に示します。

|アクセス修飾子|付与されたアクセス レベル|このアクセス レベルで宣言できる要素|この修飾子を使用できる宣言コンテキスト|
|---------------------|--------------------------|-----------------------------------------------------|----------------------------------------------------------------|
|`Public`|無制限:<br /><br /> Public 要素を参照できるすべてのコードが、これにアクセスできます|インターフェイス<br /><br /> モジュール<br /><br /> クラス<br /><br /> 構造体<br /><br /> 構造体メンバー<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|ソース ファイル<br /><br /> 名前空間<br /><br /> Interface<br /><br /> Module<br /><br /> クラス<br /><br /> 構造体|
|`Protected`|派生:<br /><br /> Protected 要素を宣言するクラス、またはそこから派生したクラスのコードが、要素にアクセスできます|インターフェイス<br /><br /> クラス<br /><br /> 構造体<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|クラス|
|`Friend`|アセンブリ:<br /><br /> Friend 要素を宣言するアセンブリ内のコードが、これにアクセスできます|インターフェイス<br /><br /> モジュール<br /><br /> クラス<br /><br /> 構造体<br /><br /> 構造体メンバー<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|ソース ファイル<br /><br /> 名前空間<br /><br /> Interface<br /><br /> Module<br /><br /> クラス<br /><br /> 構造体|
|`Protected` `Friend`|`Protected` と `Friend` の和集合:<br /><br /> Protected Friend 要素と同じクラスまたは同じアセンブリ、または要素のクラスから派生した任意のクラス内のコードが、これにアクセスできます|インターフェイス<br /><br /> クラス<br /><br /> 構造体<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|クラス|
|`Private`|宣言コンテキスト:<br /><br /> 含まれている型内のコードを含む、Private 要素を宣言する型のコードが、要素にアクセスできます|インターフェイス<br /><br /> クラス<br /><br /> 構造体<br /><br /> 構造体メンバー<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|Module<br /><br /> クラス<br /><br /> 構造体|
|`Private Protected`|Private Protected 要素を宣言するクラスのコード、または基底クラスと同じアセンブリ内に存在する派生クラスのコード。|インターフェイス<br /><br /> クラス<br /><br /> 構造体<br /><br /> プロシージャ<br /><br /> プロパティ<br /><br /> メンバー変数<br /><br /> 定数<br /><br /> 列挙<br /><br /> イベント<br /><br /> 外部宣言<br /><br /> デリゲート|クラス|

## <a name="see-also"></a>関連項目

- [Dim ステートメント](../../../language-reference/statements/dim-statement.md)
- [Static](../../../language-reference/modifiers/static.md)
- [宣言された要素の名前](declared-element-names.md)
- [宣言された要素の参照](references-to-declared-elements.md)
- [宣言された要素の特性](declared-element-characteristics.md)
- [Visual Basic における有効期間](lifetime.md)
- [Visual Basic におけるスコープ](scope.md)
- [方法: 変数の可用性を制御する](how-to-control-the-availability-of-a-variable.md)
- [変数](../variables/index.md)
- [変数宣言](../variables/variable-declaration.md)
