---
title: 名前空間プレフィックス プロパティの変更
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: d5c87cbe-4d69-429f-aad5-3103c2ca2770
ms.openlocfilehash: b817a68ff9789be414118ff4c1a3d88ca3ea9f01
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290916"
---
# <a name="changing-namespace-prefix-properties"></a>名前空間プレフィックス プロパティの変更
**XmlNode** クラスを使用すると、特定のノードに関連付けられた名前空間プレフィックスを変更できます。 たとえば、要素のプレフィックスを変更するコードを次に示します。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "b"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "b";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **出力**  
  
```xml  
<b:test xmlns:a="123" xmlns:b="456" />  
```  
  
 ノードのプレフィックスを変更しても、名前空間は変更されません。 名前空間を設定できるのは、ノードを作成するときだけです。 ツリーを永続化するときには、設定したプレフィックスに適合するように新しい名前空間の属性も永続化されます。 新しい名前空間を作成できない場合は、プレフィックスが変更され、ノードにはそのローカル名と名前空間が保持されます。 名前空間の属性を追加する例を次に示します。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<test xmlns='123'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "a"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<test xmlns='123'/>");  
XmlElement e = doc.DocumentElement;
e.Prefix = "a";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **出力**  
  
```xml  
<a:test xmlns="123" xmlns:a="123" />  
```  
  
 **doc.InnerXml** の呼び出しの結果としてツリーが文字列に永続化されるとき、`test` 要素の名前空間を保持するために `xmlns:a='123'` という属性が追加されます。 `'123'` の元の値は `'123'` だったので、そのまま  として残ります。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
