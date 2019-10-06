---
title: <httpListener> 要素 (ネットワーク設定)
ms.date: 03/30/2017
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
ms.openlocfilehash: 3f75096681ab07dd6d4788fbded5ca5c4a024aef
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698193"
---
# <a name="httplistener-element-network-settings"></a>\<httpListener> 要素 (ネットワーク設定)
<xref:System.Net.HttpListener>クラスで使用されるパラメータをカスタマイズします。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t 47 >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t @ no__t @no__t @ no__t-3[ **-6 設定 >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 **\<httpListener >** を行います。  
  
## <a name="syntax"></a>構文  
  
```xml  
<httpListener  
  unescapeRequestUrl="true|false"  
/>  
```  
  
## <a name="type"></a>種類  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|unescapeRequestUrl|@No__t 0 のインスタンスが、変換後の URI ではなく、生のエスケープされていない URI を使用するかどうかを示すブール値。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**[説明]**|  
|-----------------|---------------------|  
|[settings](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>コメント  
 **UnescapeRequestUrl**属性は、パーセントでエンコードされた値が変換され、その他の正規化ステップが実行される場合に、<xref:System.Net.HttpListener> では、変換後の uri ではなく、生のエスケープされない uri を使用するかどうかを示します。  
  
 @No__t 0 のインスタンスが @no__t 1 のサービスを介して要求を受信すると、`http.sys` によって提供される URI 文字列のインスタンスが作成され、<xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=nameWithType> プロパティとして公開されます。  
  
 @No__t-0 サービスは、次の2つの要求 URI 文字列を公開します。  
  
- 未加工の URI  
  
- 変換された URI  
  
 未加工 URI は、HTTP 要求の要求行に指定された @no__t 0 です。  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 上記の要求で `http.sys` によって指定された未加工の URI は、"/path/" です。 これは、ネットワーク経由で送信された HTTP 動詞に続く文字列を表します。  
  
 @No__t-0 サービスは、HTTP 要求行に指定された URI とホストヘッダーを使用して、要求に指定された情報から変換された URI を作成し、要求の転送先となる配信元サーバーを決定します。 これは、要求の情報を一連の登録済み URI プレフィックスと比較することによって行われます。 HTTP Server SDK ドキュメントは、この変換後の URI を HTTP_COOKED_URL 構造体として参照します。  
  
 要求を登録済みの URI プレフィックスと比較できるようにするには、要求の正規化を行う必要があります。 上記のサンプルの場合、変換後の URI は次のようになります。  
  
 `http://www.contoso.com/path/`  
  
 @No__t-0 サービスは、<xref:System.Uri.Host%2A?displayProperty=nameWithType> プロパティ値と要求行の文字列を組み合わせて、変換された URI を作成します。 さらに、`http.sys` と <xref:System.Uri?displayProperty=nameWithType> クラスも、次のことを行います。  
  
- パーセントでエンコードされたすべての値をエスケープ解除します。  
  
- パーセントでエンコードされた非 ASCII 文字を UTF-16 文字表現に変換します。 UTF-8 および ANSI/DBCS 文字は、Unicode 文字 (% uXXXX 形式を使用した Unicode エンコード) でもサポートされています。  
  
- パスの圧縮など、その他の正規化手順を実行します。  
  
 パーセントでエンコードされた値に使用されるエンコーディングに関する情報が要求に含まれていないため、パーセントでエンコードされた値を解析するだけで、正しいエンコーディングを判断できない場合があります。  
  
 したがって、`http.sys` は、プロセスを変更するための2つのレジストリキーを提供します。  
  
|レジストリ キー|既定値|説明|  
|------------------|-------------------|-----------------|  
|EnableNonUTF8|1|0の場合、`http.sys` は UTF-8 でエンコードされた Url のみを受け入れます。<br /><br /> 0以外の場合、`http.sys` は、要求で ANSI エンコードまたは DBCS でエンコードされた Url も受け入れます。|  
|FavorUTF8|1|0以外の場合、`http.sys` は常に UTF-8 として URL をデコードしようとします。この変換が失敗し、EnableNonUTF8 が0以外の場合は、http.sys は ANSI または DBCS としてデコードしようとします。<br /><br /> 0 (および EnableNonUTF8 が0以外) の場合、`http.sys` は ANSI または DBCS としてデコードしようとします。これが成功しなかった場合は、UTF-8 変換が試行されます。|  
  
 @No__t-0 が要求を受け取ると、`http.sys` の変換された URI を <xref:System.Net.HttpListenerRequest.Url%2A> プロパティへの入力として使用します。  
  
 Uri の文字と数字以外の文字をサポートする必要があります。 例として、次の URI があります。これは、顧客番号 "1/3812" の顧客情報を取得するために使用されます。  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 Uri (% 2F) のパーセントでエンコードされたスラッシュに注意してください。 この場合は、スラッシュ文字がパス区切り記号ではなく、データを表すために必要です。  
  
 文字列を Uri コンストラクターに渡すと、次の URI になります。  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 パスをセグメントに分割すると、次の要素が生成されます。  
  
 `Customer('1`  
  
 `3812')`  
  
 これは、要求の送信者の意図ではありません。  
  
 **UnescapeRequestUrl**属性が**false**に設定されている場合、@no__t 2 は要求を受信すると、`http.sys` の変換された uri ではなく、生の uri を使用して <xref:System.Net.HttpListenerRequest.Url%2A> プロパティに入力します。  
  
 **UnescapeRequestUrl**属性の既定値は**true**です。  
  
 @No__t-0 プロパティを使用して、適用可能な構成ファイルから**unescapeRequestUrl**属性の現在の値を取得できます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Net.HttpListenerRequest.Url%2A> プロパティへの入力として `http.sys` の変換された URI ではなく、未加工 URI の使用を要求を受け取ったときに <xref:System.Net.HttpListener> クラスを構成する方法を示します。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpListener  
        unescapeRequestUrl="false"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="element-information"></a>要素情報  
  
|||
|-|-|  
|Namespace|System.Net|  
|[スキーマ名]||  
|検証ファイル||  
|空にすることができます||  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Configuration.HttpListenerElement>
- <xref:System.Net.HttpListener>
- <xref:System.Net.HttpListenerRequest.Url%2A>
- [ネットワーク設定スキーマ](index.md)
