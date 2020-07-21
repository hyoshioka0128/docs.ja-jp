---
title: シリアル化 - .NET
description: この記事では、バイナリ シリアル化、XML および SOAP シリアル化、JSON シリアル化など、.NET シリアル化テクノロジに関する情報を提供します。
ms.date: 09/02/2019
helpviewer_keywords:
- JSON serialization
- XML serialization, defined
- binary serialization
- serializing objects
- serialization
- objects, serializing
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
ms.openlocfilehash: b3d76c14dc9180a5f19781122d1a42bcae603e76
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "85840381"
---
# <a name="serialization-in-net"></a>.NET でのシリアル化

シリアル化とは、オブジェクトの状態を永続化または転送できる形式に変換するプロセスのことです。 シリアル化を補完するプロセスとして、ストリームをオブジェクトに変換する逆シリアル化があります。 これらのプロセスを共に使用することで、データを格納および転送できます。  
  
.NET では、次のシリアル化テクノロジが提供されています。  
  
- [バイナリ シリアル化](binary-serialization.md)では、型そのものが正確に維持されるため、アプリケーションを次回起動するまでの間、オブジェクトの状態を維持するのに役立ちます。 たとえば、クリップボードを出力先としてオブジェクトをシリアル化することによって、そのオブジェクトを異なるアプリケーション間で共有できます。 オブジェクトをシリアル化して、ストリーム、ディスク、メモリ、ネットワーク上などに出力できます。 リモート処理では、シリアル化を使用して、コンピューター間やアプリケーション ドメイン間でオブジェクトを "値渡し" します。  
  
- [XML および SOAP シリアル化](xml-and-soap-serialization.md)では、パブリック プロパティとフィールドのみがシリアル化され、型そのものは維持されません。 これは、データを使用するアプリケーションに制限を加えずに、データを提供または処理する場合に有効です。 XML はオープン標準であるため、Web 経由でデータを共有する場合には有用な選択肢となります。 SOAP も同様のオープン標準であるため、有用な選択肢です。  
  
- [JSON シリアル化](system-text-json-overview.md)では、パブリック プロパティのみがシリアル化され、型そのものは維持されません。 JSON はオープン標準です。Web 経由でデータを共有する場合には有用な選択肢となります。

## <a name="reference"></a>関連項目

<xref:System.Runtime.Serialization>  
オブジェクトのシリアル化と逆シリアル化に使用できるクラスが含まれています。
  
<xref:System.Xml.Serialization>  
オブジェクトを XML 形式のドキュメントまたはストリームにシリアル化するために使用できるクラスが含まれています。

<xref:System.Text.Json>  
オブジェクトを JSON 形式のドキュメントまたはストリームにシリアル化するために使用できるクラスが含まれています。
