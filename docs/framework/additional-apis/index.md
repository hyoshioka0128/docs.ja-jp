---
title: 追加のクラス ライブラリと API
description: 帯域外 (OOB) プロジェクト、プラットフォーム固有のライブラリ、プライベート Api など、.NET で追加のクラスライブラリと Api を探索します。
ms.date: 06/12/2020
helpviewer_keywords:
- Additional class libraries
- Additional managed libraries
- .NET Framework out-of-band releases
- out-of-band releases
ms.assetid: cf2d9006-b631-4e5d-81cd-20aab78c60f1
ms.topic: conceptual
ms.openlocfilehash: 0b888d2f0e80685ba993682b2f3067cf8aee15bc
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989738"
---
# <a name="additional-class-libraries-and-apis"></a>追加のクラス ライブラリと API

この記事では、帯域外でリリースされた Api、特定のプラットフォームを対象とする Api、またはプライベート型または内部型の Api .NET Framework を示します。

## <a name="oob-projects"></a>OOB プロジェクト

クロスプラットフォームの開発を改善し、新しい機能を早期に導入するために、一部の .NET Framework 機能がアウトオブバンド (OOB) でリリースされました。

| Project | 説明 |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | スレッド セーフであり、内容が変更されないことが保証されているコレクションを提供します。 |
| <xref:System.Net.Http.WinHttpHandler> | Windows の WinHTTP インターフェイスに基づいた <xref:System.Net.Http.HttpClient> のメッセージ ハンドラーを提供します。 |
| <xref:System.Numerics> | SIMD ハードウェア ベースのアクセラレータを利用できるベクター型のライブラリを提供します。|
| <xref:System.Threading.Tasks.Dataflow> | TPL データフロー ライブラリはデータ フロー コンポーネントを提供し、コンカレンシー対応アプリケーションの堅牢性を強化します。 |  

## <a name="platform-specific-libraries"></a>プラットフォーム固有のライブラリ

一部のライブラリは特定のプラットフォームを対象としています。 たとえば、クラスを <xref:System.Text.CodePagesEncodingProvider> 使用すると、.NET Framework を使用して開発された UWP アプリでコードページエンコーディングを使用できるようになります。
  
| Project | 説明 |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | クラスを拡張して <xref:System.Text.EncodingProvider> 、ユニバーサル Windows プラットフォームを対象とするアプリでコードページエンコーディングを使用できるようにします。 |  
  
## <a name="private-apis"></a>プライベート API  

これらの Api は製品インフラストラクチャをサポートします。コードから直接使用するためのものでも、サポートもされていません。  
  
* [SmiOrderProperty プロパティの値です。](microsoft.sqlserver.server.smiorderproperty.item.md)
* [PrepForRemoting メソッド](system.exception.prepforremoting.md)
* [SqlTypes プロパティ (system.object のプロパティ)](system.data.sqltypes.sqlchars.stream.md)
* [SqlTypes. SqlStreamChars コンストラクター](system.data.sqltypes.sqlstreamchars.-ctor.md)
* [SqlTypes プロパティの値を検索します。](system.data.sqltypes.sqlstreamchars.canseek.md)
* [SqlTypes プロパティの値を持つことができます。](system.data.sqltypes.sqlstreamchars.isnull.md)
* [SqlTypes プロパティ ("system.string" プロパティ)](system.data.sqltypes.sqlstreamchars.length.md)
* [SqlTypes メソッドを削除してください。](system.data.sqltypes.sqlstreamchars.close.md)
* [SqlTypes メソッド (system.object の置換メソッド)](system.data.sqltypes.sqlstreamchars.dispose.md)
* [System.string メソッド (SqlTypes...)](system.data.sqltypes.sqlstreamchars.flush.md)
* [SqlTypes メソッドを参照してください。](system.data.sqltypes.sqlstreamchars.read.md)
* [SqlTypes (システムのデータ. Seek メソッド)](system.data.sqltypes.sqlstreamchars.seek.md)
* [SetLength メソッドを SqlTypes しています。](system.data.sqltypes.sqlstreamchars.setlength.md)
* [SqlTypes メソッドを作成してください。](system.data.sqltypes.sqlstreamchars.write.md)
* [MemoryStream メソッドの呼び出しを行います。](system.io.memorystream.internalgetoriginandlength.md)
* [System .Net. ComNetOS クラス](system.net.comnetos.md)
* [System .Net. Connection クラス](connection.md)
* [System .Net. 接続. m \_ writelist フィールド](m_writelist.md)
* [システム .Net. ConnectionGroup クラス](connectiongroup.md)
* [System .Net. ConnectionGroup. m \_ connectiongroup フィールド](m_connectionlist.md)
* [System .Net. ConnectStream. 接続プロパティ](system.net.connectstream.connection.md)
* [CoreResponseData クラス](coreresponsedata.md)
* [System CoreResponseData \_ ResponseHeaders フィールド](coreresponsedata_m_responseheaders.md)
* [CoreResponseData の \_ StatusCode フィールド](coreresponsedata_m_statuscode.md)
* [System .Net. ExceptionHelper クラス](system.net.exceptionhelper.md)
* [System .Net. HttpStatusDescription クラス](system.net.httpstatusdescription.md)
* [HttpWebRequest。 \_AutoRedirects フィールド](_autoredirects.md)
* [HttpWebRequest。 \_CoreResponse フィールド](httpwebrequest__coreresponse.md)
* [HttpWebRequest。 \_Httpresponse.cache フィールド](_httpresponse.md)
* [System .Net. Logging クラス](system.net.logging.md)
* [System .Net. Mail. Mailaddressparc クラス](system.net.mail.mailaddressparser.md)
* [System QuotedPairReader クラス](system.net.mail.quotedpairreader.md)
* [System .Net (Mime) のヘルパークラス](system.net.mime.mailbnfhelper.md)
* [System .Net. PooledStream. NetworkStream プロパティ](system.net.pooledstream.networkstream.md)
* [システム .Net. RtcState クラス](system.net.rtcstate.md)
* [System .Net. Security. Sslstate プロパティ](system.net.security.sslstate.sslprotocol.md)
* [System .Net. ServicePoint. m \_ connectiongrouplist フィールド](m_connectiongrouplist.md)
* [System .Net. ServicePointManager. CloseConnectionGroups メソッド](system.net.servicepointmanager.closeconnectiongroups.md)
* [System .Net. ServicePointManager. s \_ servicepointmanager フィールド](s_servicepointtable.md)
* [M_Worker TlsStream (システム) フィールド](system.net.tlsstream.m_worker.md)
* [UnsafeNclNativeMethods クラス](system.net.unsafenclnativemethods.md)
* [System .Net. WebHeaderCollection. AddInternal メソッド](system.net.webheadercollection.addinternal.md)
* [System.servicemodel. Channels. Message. BodyToString メソッド](system.servicemodel.channels.message.bodytostring.md)
* [WriteStartHeaders メソッド (System.servicemodel.)](system.servicemodel.channels.message.writestartheaders.md)
* [IsDebuggerCheckDisabledForTestPurposes (システムの診断の \_ フィールド)](s-isdebuggercheckdisabledfortestpurposes-field.md)
* [System.string クラス (DataMemberFieldEditor クラス)](datamemberfieldeditor-class.md)
* [System.string クラス (DataMemberListEditor クラス)](datamemberlisteditor-class.md)
* [System.Xml.XmlReader メソッド](system.xml.xmlreader.createsqlreader.md)
* [adodb.recordset.接続インターフェイス](adodb.connection.md)
* [adodb.recordset.EventReason 列挙型](adodb.eventreasonenum.md)
* [adodb.recordset.EventStatus 列挙型](adodb.eventstatusenum.md)
* [stdole.DISPPARAMS 構造体](stdole.dispparams.md)
* [stdole.EXCEPINFO 構造体](stdole.excepinfo.md)
* [stdole.IFont.Name プロパティ](stdole.ifont.name.md)
* [stdole.IFontDisp インターフェイス](stdole.ifontdisp.md)
* [stdole.IPicture. Handle プロパティ](stdole.ipicture.handle.md)
* [stdole.IPictureDisp プロパティ](stdole.ipicturedisp.handle.md)
* [stdole.StdFont インターフェイス](stdole.stdfont.md)
* [stdole.StdPicture インターフェイス](stdole.stdpicture.md)
  
## <a name="see-also"></a>関連項目

* [.NET Framework および特別なリリース](../get-started/the-net-framework-and-out-of-band-releases.md)
