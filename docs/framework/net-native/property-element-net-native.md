---
title: <Property>要素 (.NET ネイティブ)
ms.date: 03/30/2017
ms.assetid: ad4ba56d-3bcb-4c10-ba90-1cc66e2175a1
ms.openlocfilehash: b9bc89804a872dddf1a56c2a3dadc9c3df4f5fd1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128208"
---
# <a name="property-element-net-native"></a>\<Property>要素 (.NET ネイティブ)
プロパティにランタイム リフレクション ポリシーを適用します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<Property Name="property_name"  
          Browse="policy_type"  
          Dynamic="policy_type"  
          Serialize="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|属性の型|Description|  
|---------------|--------------------|-----------------|  
|`Name`|全般|必須の属性です。 プロパティ名を指定します。|  
|`Browse`|リフレクション|省略可能な属性です。 プロパティに関する情報の照会やプロパティの列挙を制御しますが、実行時の動的アクセスは有効にしません。|  
|`Dynamic`|リフレクション|省略可能な属性です。 プロパティへの実行時アクセスを制御して、動的プログラミングを有効にします。 このポリシーによって、実行時にプロパティを動的に設定または取得できるようになります。|  
|`Serialize`|シリアル化|省略可能な属性です。 プロパティへの実行時アクセスを制御して、型インスタンスを Newtonsoft の JSON シリアライザーなどのライブラリによってシリアル化できるようにしたり、データ バインディングで使用できるようにしたりします。|  
  
## <a name="name-attribute"></a>Name 属性  
  
|値|[説明]|  
|-----------|-----------------|  
|*method_name*|プロパティ名。 プロパティの型は、親要素または要素によって定義され [\<Type>](type-element-net-native.md) [\<TypeInstantiation>](typeinstantiation-element-net-native.md) ます。|  
  
## <a name="all-other-attributes"></a>その他すべての属性  
  
|値|[説明]|  
|-----------|-----------------|  
|*policy_setting*|プロパティのこのポリシーの種類に適用する設定です。 指定できる値は、`Auto`、`Excluded`、`Included`、および `Required` です。 詳細については、「[ランタイム ディレクティブのポリシー設定](runtime-directive-policy-settings.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|型とそのすべてのメンバーにリフレクション ポリシーを適用します。|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|構築されたジェネリック型とそのすべてのメンバーにリフレクション ポリシーを適用します。|  
  
## <a name="remarks"></a>解説  
 プロパティのポリシーが明示的に定義されていない場合は、親要素の実行時ポリシーを継承します。  
  
## <a name="example"></a>例  
 次の例では、リフレクションを使用して、`Book` オブジェクトをインスタンス化し、そのプロパティ値を表示します。 プロジェクトの既定の default.rd.xml ファイルは、次のように示されます。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Namespace Name="LibraryApplications"  Browse="Required Public" >  
         <Type Name="Book"   Activate="All" />  
      </Namespace>  
   </Application>  
</Directives>  
```  
  
 このファイルは、`All` クラスの `Activate` ポリシーに `Book` 値を適用します。これにより、リフレクションを介してクラス コンストラクターにアクセスできるようになります。 `Browse` クラスの `Book` ポリシーは、その親名前空間から継承されます。 これは `Required Public` に設定され、メタデータが実行時に使用できるようになります。  
  
 この例のソース コードを次に示します。 変数は、 `outputBlock` コントロールを表し <xref:Windows.UI.Xaml.Controls.TextBlock> ます。  
  
 [!code-csharp[ProjectN_Reflection#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/property1.cs#6)]  
  
 ただし、この例をコンパイルして実行すると、[MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外がスローされます。 `Book` 型のメタデータは使用可能になりましたが、プロパティの getter の実装は動的に使用可能になりませんでした。 このエラーは、次の 2 つの方法のいずれかを使用して修正できます。  
  
- `Dynamic` `Book` 要素内の型のポリシーを定義し [\<Type>](type-element-net-native.md) ます。  
  
- [\<Property>](property-element-net-native.md)次の既定の .xml ファイルのように、呼び出す getter を持つ各プロパティに対して、入れ子になった要素を追加します。  
  
    ```xml  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
       <Application>  
          <Namespace Name="LibraryApplications"  Browse="Required Public" >  
             <Type Name="Book"   Activate="All" >  
                <Property Name="Title" Dynamic="Required" />  
                <Property Name="Author" Dynamic="Required" />  
                  <Property Name="ISBN" Dynamic="Required" />  
             </Type>  
          </Namespace>  
       </Application>  
    </Directives>  
    ```  
  
## <a name="see-also"></a>関連項目

- [ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス](runtime-directives-rd-xml-configuration-file-reference.md)
- [ランタイム ディレクティブ要素](runtime-directive-elements.md)
- [ランタイム ディレクティブ ポリシーの設定](runtime-directive-policy-settings.md)
