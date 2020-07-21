---
title: メタデータ インターフェイス
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], metadata
- metadata interfaces [.NET Framework]
- interfaces (.NET Framework metadata]
ms.assetid: f5cdac93-a28c-48ef-8a19-5773376e9e7c
ms.openlocfilehash: 4d947388afb8d7f8f935ae3b8e8aff81efaf2ee4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84489596"
---
# <a name="metadata-interfaces"></a>メタデータ インターフェイス
このセクションでは、.NET Framework の型、メソッド、フィールドなどによって公開されるメタデータにアクセスできるようにするアンマネージ インターフェイスについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ICeeGen インターフェイス](iceegen-interface.md)  
 動的なコード コンパイルのためのメソッドを提供します。  
  
 [IHostFilter インターフェイス](ihostfilter-interface.md)  
 ランタイム ホストがメタデータ トークンに処理済みのマークを付けるためのメソッドを提供します。  
  
 [IMapToken インターフェイス](imaptoken-interface.md)  
 インポートされたメタデータ署名と生成されたメタデータ署名との間の割り当て機能を提供します。  
  
 [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)  
 共通言語ランタイム (CLR) がリソースの解決および消費に使用する自己記述モデルをサポートするメソッドを提供します。  
  
 [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)  
 アセンブリ マニフェストの内容にアクセスして確認するメソッドを提供します。  
  
 [IMetaDataConverter インターフェイス](imetadataconverter-interface.md)  
 タイプ ライブラリをそれぞれのメタデータ署名にマップして、一方から他方に変換するメソッドを提供します。  
  
 [IMetaDataDispenser インターフェイス](imetadatadispenser-interface.md)  
 `IMetaDataDispenser` は互換性のために残されています。 代わりに、`IMetaDataDispenserEx` を使用してください。  
  
 [IMetaDataDispenserEx インターフェイス](imetadatadispenserex-interface.md)  
 メタデータを作成または変更するためのメモリ領域を割り当てるメソッドを提供します。  
  
 [IMetaDataEmit インターフェイス](imetadataemit-interface.md)  
 現在定義されているスコープ内のアセンブリについてのメタデータを作成、変更、格納するメソッドを提供します。  
  
 [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)  
 <xref:System.Type?displayProperty=nameWithType> 型のパラメーターを持つメソッドおよびコンストラクターのメタデータ署名を定義および変更するメソッドを提供します。  
  
 [IMetaDataError インターフェイス](imetadataerror-interface.md)  
 アセンブリのメタデータ署名の解決時のエラーを報告するためのコールバック機構を提供します。  
  
 [IMetaDataFilter インターフェイス](imetadatafilter-interface.md)  
 メタデータ トークンにマークを付け、フィルター処理をして、既に実行されたアクションが繰り返し行われないようにするメソッドを提供します。  
  
 [IMetaDataImport インターフェイス](imetadataimport-interface.md)  
 他のアセンブリの型をインポートおよび操作するメソッドを提供します。  
  
 [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)  
 `IMetaDataImport` を拡張して、ジェネリック型を使用できるようにします。  
  
 [IMetaDataInfo インターフェイス](imetadatainfo-interface.md)  
 ディスク上のファイルからメモリへのメタデータのマッピングに関する情報を取得するメソッドを提供します。  
  
 [IMetaDataTables インターフェイス](imetadatatables-interface.md)  
 テーブル内のメタデータ情報の格納と取得のためのメソッドを提供します。  
  
 [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)  
 `IMetaDataTables` を拡張して、メタデータ ストリームを使用するためのメソッドを含めます。  
  
 [IMetaDataValidate インターフェイス](imetadatavalidate-interface.md)  
 メタデータ署名の検証で使用するメソッドを提供します。  
  
## <a name="related-sections"></a>関連項目  
 [メタデータ グローバル静的関数](metadata-global-static-functions.md)  
  
 [メタデータ列挙体](metadata-enumerations.md)  
  
 [メタデータ構造体](metadata-structures.md)  
  
 [メタデータ共用体](metadata-unions.md)
