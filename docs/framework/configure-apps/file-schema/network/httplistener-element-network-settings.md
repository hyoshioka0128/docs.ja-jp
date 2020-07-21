---
title: <httpListener> 要素 (ネットワーク設定)
ms.date: 03/30/2017
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
ms.openlocfilehash: 0054be3d2002e4ea5247f25d8094386ac7242422
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "74088373"
---
# <a name="httplistener-element-network-settings"></a>\<httpListener> 要素 (ネットワーク設定)
クラスによって使用されるパラメーターをカスタマイズ <xref:System.Net.HttpListener> します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<httpListener>**

## <a name="syntax"></a>構文  
  
```xml  
<httpListener  
  unescapeRequestUrl="true|false"  
/>  
```  
  
## <a name="type"></a>Type  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|[説明]|  
|---------------|-----------------|  
|unescapeRequestUrl|インスタンスが、 <xref:System.Net.HttpListener> 変換後の uri ではなく、未加工のエスケープされていない uri を使用するかどうかを示すブール値。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[設定](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 **UnescapeRequestUrl**属性は、が変換された uri では <xref:System.Net.HttpListener> なく、生のエスケープされていない uri を使用するかどうかを示します。  
  
 インスタンスは、 <xref:System.Net.HttpListener> サービスを介して要求を受け取ると、 `http.sys` によって提供される URI 文字列のインスタンスを作成 `http.sys` し、プロパティとして公開し <xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=nameWithType> ます。  
  
 サービスは、 `http.sys` 次の2つの要求 URI 文字列を公開します。  
  
- 未加工の URI  
  
- 変換された URI  
  
 未加工 URI は、 <xref:System.Uri?displayProperty=nameWithType> HTTP 要求の要求行で指定されるです。  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 前述の要求に対してによって提供される未加工の URI `http.sys` は、"/path/" です。 これは、ネットワーク経由で送信された HTTP 動詞に続く文字列を表します。  
  
 サービスは、 `http.sys` HTTP 要求行に指定された uri とホストヘッダーを使用して、要求で提供される情報から変換された uri を作成し、要求の転送先となる配信元サーバーを決定します。 これは、要求の情報を一連の登録済み URI プレフィックスと比較することによって行われます。 HTTP Server SDK のドキュメントでは、この変換された URI を HTTP_COOKED_URL 構造として参照します。  
  
 要求を登録済みの URI プレフィックスと比較できるようにするには、要求の正規化を行う必要があります。 上記のサンプルの場合、変換後の URI は次のようになります。  
  
 `http://www.contoso.com/path/`  
  
 サービスは、 `http.sys` <xref:System.Uri.Host%2A?displayProperty=nameWithType> 要求行にプロパティ値と文字列を結合して、変換された URI を作成します。 さらに、 `http.sys` クラスは <xref:System.Uri?displayProperty=nameWithType> 次のことも行います。  
  
- パーセントでエンコードされたすべての値をエスケープ解除します。  
  
- パーセントでエンコードされた非 ASCII 文字を UTF-16 文字表現に変換します。 UTF-8 および ANSI/DBCS 文字は、Unicode 文字 (% uXXXX 形式を使用した Unicode エンコード) でもサポートされています。  
  
- パスの圧縮など、その他の正規化手順を実行します。  
  
 パーセントでエンコードされた値に使用されるエンコーディングに関する情報が要求に含まれていないため、パーセントでエンコードされた値を解析するだけで、正しいエンコーディングを判断できない場合があります。  
  
 このため `http.sys` 、プロセスを変更するには、次の2つのレジストリキーを使用します。  
  
|レジストリ キー|Default value|説明|  
|------------------|-------------------|-----------------|  
|EnableNonUTF8|1|ゼロの場合、は `http.sys` utf-8 でエンコードされた url のみを受け入れます。<br /><br /> 0以外の場合、 `http.sys` は、要求で ANSI エンコードまたは DBCS でエンコードされた url も受け入れます。|  
|FavorUTF8|1|0以外の場合、は `http.sys` 常に utf-8 として URL をデコードしようとします。変換に失敗し、EnableNonUTF8 が0以外の場合は、http.sys は ANSI または DBCS としてデコードしようとします。<br /><br /> ゼロ (および EnableNonUTF8 が0以外) の場合、は `http.sys` ANSI または DBCS としてデコードしようとします。成功しなかった場合は、utf-8 変換を試行します。|  
  
 は、要求を受信すると、変換された <xref:System.Net.HttpListener> URI をから `http.sys` プロパティへの入力として使用し <xref:System.Net.HttpListenerRequest.Url%2A> ます。  
  
 Uri の文字と数字以外の文字をサポートする必要があります。 例として、次の URI があります。これは、顧客番号 "1/3812" の顧客情報を取得するために使用されます。  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 Uri (% 2F) のパーセントでエンコードされたスラッシュに注意してください。 この場合は、スラッシュ文字がパス区切り記号ではなく、データを表すために必要です。  
  
 文字列を Uri コンストラクターに渡すと、次の URI になります。  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 パスをセグメントに分割すると、次の要素が生成されます。  
  
 `Customer('1`  
  
 `3812')`  
  
 これは、要求の送信者の意図ではありません。  
  
 **UnescapeRequestUrl**属性が**false**に設定されている場合、が要求を受信すると、から変換された uri ではなく、 <xref:System.Net.HttpListener> 未加工の uri が `http.sys` プロパティへの入力として使用され <xref:System.Net.HttpListenerRequest.Url%2A> ます。  
  
 **UnescapeRequestUrl**属性の既定値は**true**です。  
  
 プロパティは、 <xref:System.Net.Configuration.HttpListenerElement.UnescapeRequestUrl%2A> 適用可能な構成ファイルから**unescapeRequestUrl**属性の現在の値を取得するために使用できます。  
  
## <a name="example"></a>例  
 次の例は、変換され <xref:System.Net.HttpListener> た uri ではなく、未加工の uri を使用するように要求を受け取ったときに、プロパティへの入力としてクラスを構成する方法を示して `http.sys` <xref:System.Net.HttpListenerRequest.Url%2A> います。  
  
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
|名前空間|System.Net|  
|スキーマ名||  
|検証ファイル||  
|空にすることができます||  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Configuration.HttpListenerElement>
- <xref:System.Net.HttpListener>
- <xref:System.Net.HttpListenerRequest.Url%2A>
- [ネットワーク設定スキーマ](index.md)
