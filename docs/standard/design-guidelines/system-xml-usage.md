---
title: System.Xml の使用法
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 82302f0d-a621-4c6f-b57d-999bd61f21a6
ms.openlocfilehash: 07828219f2e17be925d060fa3bb33a9209ecb62b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291670"
---
# <a name="systemxml-usage"></a>System.Xml の使用法
このセクションでは、 <xref:System.Xml?displayProperty=nameWithType> XML データを表すために使用できる名前空間に存在するいくつかの型の使用方法について説明します。

 ❌<xref:System.Xml.XmlNode> <xref:System.Xml.XmlDocument> XML データを表すためにまたはを使用しないでください。 <xref:System.Xml.XPath.IXPathNavigable> <xref:System.Xml.XmlReader> <xref:System.Xml.XmlWriter> 代わりにの、、、またはの各サブタイプのインスタンスの使用を優先し <xref:System.Xml.Linq.XNode> ます。 `XmlNode`と `XmlDocument` は、パブリック api で公開するように設計されていません。

 ✔️は `XmlReader` 、 `IXPathNavigable` XML を `XNode` 受け入れるか返すメンバーの入力または出力として、、、またはの各サブタイプを使用します。

 、、またはではなく、これらの抽象化を使用し `XmlDocument` `XmlNode` <xref:System.Xml.XPath.XPathDocument> ます。これは、メモリ内の xml ドキュメントの特定の実装からメソッドを分離し、、、またはを公開する仮想 XML データソースとの連携を可能にするため `XNode` `XmlReader` <xref:System.Xml.XPath.XPathNavigator> です。

 ❌`XmlDocument`基になるオブジェクトモデルまたはデータソースの XML ビューを表す型を作成する場合は、サブクラス化しないでください。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [使用に関するガイドライン](usage-guidelines.md)
