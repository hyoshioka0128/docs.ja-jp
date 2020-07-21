---
title: XML シリアル化および SOAP シリアル化
description: この概要では、SOAP 仕様に準拠する XML ストリームにオブジェクトをシリアル化することもできる XML シリアル化について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
- serialization, about serialization
- XML serialization
- serialization
ms.assetid: 832ac524-21bc-419a-a27b-ca8bfc45840f
ms.openlocfilehash: 6b7d6f59694a28207758fa7772781eed073917e4
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379541"
---
# <a name="xml-and-soap-serialization"></a>XML シリアル化および SOAP シリアル化

XML シリアル化とは、オブジェクトのパブリック フィールドやパブリック プロパティ、およびメソッドのパラメーターや戻り値を、特定の XML スキーマ定義言語 (XSD: XML Schema Definition Language) ドキュメントに準拠する XML ストリームに変換 (シリアル化) する処理です。 XML シリアル化によって、パブリック プロパティおよびパブリック フィールドを含むクラスの型が厳密に指定され、それらのパブリック メンバーは格納または転送できるようにシリアル形式 (この場合は XML) に変換されます。

XML はオープン標準であるため、XML ストリームは、プラットフォームに関係なく、必要に応じて任意のアプリケーションで処理できます。 たとえば、ASP.NET を使用して作成された XML Web サービスは、<xref:System.Xml.Serialization.XmlSerializer> クラスを使用して、インターネット全体またはイントラネット上の XML Web サービス アプリケーション間でデータを受け渡しする XML ストリームを作成します。 一方、逆シリアル化は、このような XML ストリームからデータを取得して、元のオブジェクトを再構築します。

XML シリアル化を使用して、SOAP 仕様に準拠する XML ストリームにオブジェクトをシリアル化することもできます。 SOAP は、XML を使用してプロシージャ呼び出しを転送するために特別にデザインされた、XML に基づくプロトコルです。

オブジェクトをシリアル化または逆シリアル化するには、<xref:System.Xml.Serialization.XmlSerializer> クラスを使用します。 また、シリアル化する対象のクラスを作成するには、XML スキーマ定義ツールを使用します。

## <a name="see-also"></a>関連項目

- [バイナリ シリアル化](binary-serialization.md)
- [ASP.NET と XML Web サービス クライアントを使用して作成した XML Web サービス](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))
