---
title: XML スキーマ定義ツールと XML シリアル化
description: XML スキーマ定義ツールは、XSD スキーマについて C# または Visual Basic クラス ファイルを生成し、ライブラリまたは実行可能ファイルから XML スキーマを生成します。
ms.date: 03/30/2017
helpviewer_keywords:
- Xsd.exe
- XML serialization, XML Schema Definition tool
- XML Schema Definition tool
- serialization, XML Schema Definition tool
ms.assetid: 3c03f855-f931-47ff-bbc6-50c0367a16e4
ms.openlocfilehash: c88770403d4c2abfb5ce99f44ea1bec1f8337545
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84279777"
---
# <a name="the-xml-schema-definition-tool-and-xml-serialization"></a>XML スキーマ定義ツールと XML シリアル化

XML スキーマ定義ツール ([XML Schema Definition Tool (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)) は、Windows&reg; Software Development Kit (SDK) の一部として、.NET Framework ツールと共にインストールされます。 このツールは、主に次の 2 つの目的を実現するためにデザインされています。  
  
- 特定の XML スキーマ定義言語 (XSD) スキーマに準拠する C# クラス ファイルまたは Visual Basic クラス ファイルの生成。 このツールは、XML スキーマを引数として受け取り、<xref:System.Xml.Serialization.XmlSerializer> を使用したシリアル化時にそのスキーマに準拠している多数のクラスを含むファイルを出力します。 このツールを使用して、特定のスキーマに準拠するクラスを生成する方法については、「[方法:XML スキーマ定義ツールを使用してクラスと XML スキーマ ドキュメントを生成する](xml-schema-def-tool-gen.md)」を参照してください。  
  
- .dll ファイルまたは .exe ファイルからの XML スキーマ ドキュメントの生成。 作成済み、または属性を使用して変更済みの一連のファイルのスキーマを確認するには、このツールに DLL または EXE を引数として渡し、その XML スキーマを生成します。 このツールを使用して、一連のクラスから XML スキーマ ドキュメントを生成する方法については、「[方法:XML スキーマ定義ツールを使用してクラスと XML スキーマ ドキュメントを生成する](xml-schema-def-tool-gen.md)」を参照してください。  
  
ツールの使用の詳細については、「[XML スキーマ定義ツール (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataSet>
- [XML シリアル化の概要](introducing-xml-serialization.md)
- [XML スキーマ定義ツール (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [方法: オブジェクトをシリアル化する](how-to-serialize-an-object.md)
- [方法: オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)
- [方法: XML スキーマ定義ツールを使用してクラスと XML スキーマ ドキュメントを生成する](xml-schema-def-tool-gen.md)
- [XML スキーマのバインディング サポート](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sh1e66zd(v=vs.100))
