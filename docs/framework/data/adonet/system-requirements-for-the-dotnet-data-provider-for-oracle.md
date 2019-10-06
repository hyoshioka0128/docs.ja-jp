---
title: .NET Framework Data Provider for Oracle のシステム要件
ms.date: 03/30/2017
ms.assetid: 054f76b9-1737-43f0-8160-84a00a387217
ms.openlocfilehash: 664357fb08a6100b8b69d2b4e11edc77cdb81ac7
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833638"
---
# <a name="system-requirements-for-the-net-framework-data-provider-for-oracle"></a>.NET Framework Data Provider for Oracle のシステム要件

.NET Framework Data Provider for Oracle を使用するには、MDAC (Microsoft Data Access Components) のバージョン 2.6 以降が必要です。 MDAC 2.8 SP1 をインストールすることをお勧めします。  
  
 Oracle 8i Release 3 (8.1.7) Client 以降もインストールする必要があります。  
  
 UTF16 は Oracle 9i の新機能なので、Oracle 9i 以前のバージョンの Oracle Client ソフトウェアでは UTF16 データベースにアクセスできません。 この機能を使用するには、お使いのクライアント ソフトウェアを Oracle 9i 以降にアップグレードする必要があります。  
  
## <a name="working-with-the-data-provider-for-oracle-and-unicode-data"></a>Data Provider for Oracle と Unicode データの使用  
 
次に、Oracle および Oracle クライアントライブラリの .NET Framework Data Provider を使用する場合に考慮する必要がある、Unicode 関連の問題の一覧を示します。 詳細については、Oracle のドキュメントを参照してください。  
  
### <a name="setting-the-unicode-value-in-a-connection-string-attribute"></a>接続文字列の属性に Unicode 値を設定する  

Oracle を操作する場合、接続文字列の属性を使用し、  
  
`Unicode=True`
  
UTF-16 モードで Oracle クライアント ライブラリを初期化することができます。 これにより、Oracle クライアント ライブラリで、マルチバイト文字列の代わりに UTF-16 (UCS-2 とよく似ています) が使用できるようになります。 新たに変換作業を行わなくても、Data Provider for Oracle で Oracle のコード ページを常に使用できます。 この構成は、Oracle 9i クライアントを使用して、AL16UTF16 の代替文字セットを持つ Oracle 9i データベースと通信する場合に動作します。 Oracle 9i クライアントが Oracle 9i サーバーと通信する場合、Unicode の**CommandText**値を、Oracle9i サーバーが使用する適切なマルチバイト文字セットに変換するために、追加のリソースが必要になります。 安全な構成が確保されていることがわかっている場合は、`Unicode=True` を接続文字列に追加することにより回避することができます。  
  
### <a name="mixing-versions-of-oracle-client-and-oracle-server"></a>Oracle クライアントと Oracle サーバーのバージョンの混在  

Oracle 8i クライアントは、サーバーの national character set が AL16UTF16 (Oracle 9i の既定の設定) として指定されている場合、Oracle 9i データベースの**NCHAR**、 **NVARCHAR2**、または**NCLOB**データにアクセスできません。 UTF-16 文字セットのサポートは Oracle 9i まで導入されなかったため、Oracle 8i クライアントでは読み取れません。  
  
### <a name="working-with-utf-8-data"></a>UTF-8 データの使用  

代替文字セットを設定するには、レジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE\HOMEID\NLS_LANG を UTF8 に設定します。 詳細については、ご使用のプラットフォームに関する Oracle のインストール ノートを参照してください。 既定の設定は、Oracle Client ソフトウェアのインストールに使用する言語の基本文字セットになっています。 接続するデータベースの各国語文字セットと言語が一致するように設定されていないと、パラメーターと列の組み合わせは、各国語文字セットではなくプライマリ データベースの文字セットでデータを送受信します。  
  
### <a name="oraclelob-can-only-update-full-characters"></a>OracleLob で更新できるのは Full 文字列のみです。  

ユーザビリティ上の理由から<xref:System.Data.OracleClient.OracleLob> 、オブジェクトは .NET Framework ストリームクラスから継承され、 **readbyte**メソッドと**writebyte**メソッドを提供します。 また、Oracle **LOB**オブジェクトのセクションに対して機能する**CopyTo**や**Erase**などのメソッドも実装しています。 これに対し、Oracle クライアントソフトウェアには、文字**LOB**s (**CLOB**および**NCLOB**) で動作する多くの api が用意されています。 ただし、これらの API は full 文字列でのみ動作します。 この違いにより、Oracle の Data Provider では、UTF-16 データをバイト単位で操作するための**Read**および**readbyte**のサポートが実装されています。 ただし、 **OracleLob**オブジェクトの他のメソッドでは、フル文字操作のみが許可されます。  
  
## <a name="see-also"></a>関連項目

- [Oracle および ADO.NET](oracle-and-adonet.md)
- [ADO.NET の概要](ado-net-overview.md)
