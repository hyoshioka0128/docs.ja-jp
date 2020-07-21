---
title: 新しいノードの作成時における XML 要素名および属性名の検証
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: b489f647-a175-4659-ada4-170058bb41d0
ms.openlocfilehash: 1da893261b35c6b57c4f08eb53b7701ec1d81fae
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289851"
---
# <a name="xml-element-and-attribute-name-verification-when-creating-new-nodes"></a>新しいノードの作成時における XML 要素名および属性名の検証
XML ドキュメント オブジェクト モデル (DOM) は、新しい要素ノードまたは属性ノードを作成するときに名前の有効性を確認します。 名前に無効な文字が含まれていると、例外がスローされます。 名前が正しくエンコードされ、有効であることを保証するには、**XmlConvert** クラスを使用して名前をエンコードし、アプリケーション レベルで名前をデコードする必要があります。 **XmlWriter** には、整形式の XML を生成するための追加の処理を行うメソッドが用意されています。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
