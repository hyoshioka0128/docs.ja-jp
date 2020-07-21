---
title: XML からのデータ型クラスの生成
ms.date: 03/30/2017
ms.assetid: e4e5e4e8-527f-44d1-92fa-8904a08784ea
ms.openlocfilehash: d66cbd1806b90d21a483d0c470f953ddfb9c4fca
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184130"
---
# <a name="generating-data-type-classes-from-xml"></a>XML からのデータ型クラスの生成
.NET Framework 4.5 には、XML からデータ型クラスを生成する新しい機能が含まれています。 このトピックでは、.NET ブログ RSS フィードのデータ型を自動的に生成する方法について説明します。  
  
### <a name="obtaining-the-xml-from-the-net-blog-rss-feed"></a>.NET ブログ RSS フィードからの XML の取得  
  
1. インターネット エクスプローラで[、.NET ブログ RSS フィード](https://devblogs.microsoft.com/dotnet/feed/)に移動します。  
  
2. ページを右クリックし、[**ソースの表示 ]** を選択します。  
  
3. **Ctrl キーを押しながら A キー**を押してすべてのテキストを選択し **、Ctrl + C キーを押**してコピーしてフィードのテキストをコピーします。  
  
### <a name="creating-the-data-types"></a>データ型の作成  
  
1. プロキシが使用されるコード ファイルを開きます。 このファイルは.NET Framework 4.5 プロジェクトの一部である必要があります。  
  
2. 既存のクラスの外部にあるファイルの場所にカーソルを置きます。  
  
3. [**編集]、[****形式の貼り付け****]、[XML をクラスとして貼り付け] を選択**します。  
  
4. 、 `link`、 `rss` `rssChannel`、`rssChannelImage``rssChannelItem`と`rssChannelItemGuid`呼ばれるクラスは、RSS フィード内の要素にアクセスするために必要なメンバーを使用して作成されます。  
  
### <a name="using-the-generated-classes"></a>生成されたクラスの使用  
  
1. クラスが生成されると、他のクラスのコードなどで使用できます。 次のコード例では、`rssChannelImage` クラスの新しいインスタンスが返されます。  
  
    ```csharp
    var channelImage = new rssChannelImage()
    {
        title = "MyImage",
        link = "http://www.contoso.com/images/channelImage.jpg",
        url = "http://www.contoso.com/entries/myEntry.html"
    };  
    ```
