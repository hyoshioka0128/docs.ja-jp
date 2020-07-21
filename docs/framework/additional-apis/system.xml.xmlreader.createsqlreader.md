---
title: メソッドを作成します。
ms.date: 10/17/2019
topic_type:
- apiref
api_name:
- System.Xml.XmlReader.CreateSqlReader
api_location:
- system.xml.dll
api_type:
- Assembly
ms.openlocfilehash: 7bd2ef5158516acede47f73f9937d06159bc16c9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79155740"
---
# <a name="xmlreadercreatesqlreader-method"></a>XmlReader.CreateSqlReader  メソッド

解析のために指定されたストリーム、設定、およびコンテキスト情報を使用して、新しい <xref:System.Xml.XmlReader> インスタンスを作成します。

```csharp
internal static XmlReader CreateSqlReader(Stream input,
  XmlReaderSettings settings, XmlParserContext inputContext)
```

## <a name="parameters"></a>パラメーター

- `input` <xref:System.IO.Stream>  
  XML データを格納しているストリーム。

- `settings` <xref:System.Xml.XmlReaderSettings>  
  新しい <xref:System.Xml.XmlReader> インスタンスの設定。 この値には `null` を指定できます。

- `inputContext` <xref:System.Xml.XmlParserContext>  
  XML フラグメントの解析に必要なコンテキスト情報。 この値には `null` を指定できます。

## <a name="returns"></a>戻り値

<xref:System.Xml.XmlReader>  
ストリーム内の XML データの読み取りに使用するオブジェクト。

## <a name="remarks"></a>解説

> [!WARNING]
> メソッド`XmlReader.CreateSqlReader`は内部であり、コード内で直接使用するためのものではありません。
>
> マイクロソフトでは、どのような状況でも、本稼動アプリケーションでこの方法の使用をサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:**<xref:System.Xml>

**アセンブリ:** システム.Xml.dll

**.NET フレームワークのバージョン:** 2.0 以降で利用可能。
