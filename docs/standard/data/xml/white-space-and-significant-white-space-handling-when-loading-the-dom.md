---
title: DOM を読み込むときの空白および有意の空白の処理
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
ms.openlocfilehash: 520d965737b82fda082aa44029f2a4042d948deb
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281775"
---
# <a name="white-space-and-significant-white-space-handling-when-loading-the-dom"></a>DOM を読み込むときの空白および有意の空白の処理
ドキュメントを読み込むときには、空白を保持するオプションを設定して、ドキュメント ツリーに **XmlWhitespace** ノードを作成できます。 空白ノードを作成するには、**PreserveWhitespace** プロパティを true に設定します。 このプロパティが既定の **false** に設定されている場合、空白ノードは作成されません。 **PreserveWhitespace** フラグの設定に関係なく、有意の空白ノードは常に保持され、そのデータを表す **XmlSignificantWhitespace** ノードが常にメモリ内に作成されます。  
  
 ドキュメントがリーダーから読み込まれた場合は、**XmlTextReader** の **WhitespaceHandling** プロパティが **WhitespaceHandling.None** に設定されていない場合にのみ、**XmlDocument** クラスの **PreserveWhitespace** フラグ プロパティの設定が **XmlWhitespace** ノードの作成に影響を及ぼします。 リーダーの **WhitespaceHandling** プロパティの値の方が **XmlDocument** のこのフラグの設定より優先されます。 **XmlSignificantWhitespace** の詳細については、「<xref:System.Xml.XmlSignificantWhitespace>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XML ドキュメント オブジェクト モデル (DOM)](xml-document-object-model-dom.md)
