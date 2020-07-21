---
title: IXCLRDataProcess インターフェイス
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess Interface
helpviewer.keywords:
- IXCLRDataProcess Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 6a6def8fc10f04b89aa8d8c735025b01f9b6ddfb
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420761"
---
# <a name="ixclrdataprocess-interface"></a>IXCLRDataProcess インターフェイス

プロセスに関する情報を照会するためのメソッドを提供します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>メソッド

| メソッド                                                                                                                                               | 説明                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [GetAppDomainByUniqueId](ixclrdataprocess-getappdomainbyuniqueid-method.md)                       | `AppDomain`プロセス内のを一意の id で取得します。                                              |
| [StartEnumModules](ixclrdataprocess-startenummodules-method.md)                                   | プロセスのモジュールを列挙するハンドルを提供します。                                        |
| [EnumModule](ixclrdataprocess-enummodule-method.md)                                               | このプロセスのモジュールを列挙します。                                                         |
| [EndEnumModules](ixclrdataprocess-endenummodules-method.md)                                       | モジュールの列挙中に使用される内部反復子によって使用されるリソースを解放します。               |
| [StartEnumMethodInstancesByAddress](ixclrdataprocess-startenummethodinstancesbyaddress-method.md) | 指定されたアドレスから開始するのメソッドインスタンスを列挙するハンドルを提供し `AppDomain` ます。 |
| [EnumMethodInstanceByAddress](ixclrdataprocess-enummethodinstancebyaddress-method.md)             | このプロセスのメソッドインスタンスを、アドレスオフセットを開始位置として列挙します。                  |
| [EndEnumMethodInstancesByAddress](ixclrdataprocess-endenummethodinstancesbyaddress-method.md)     | インスタンスの列挙中に使用される内部反復子によって使用されるリソースを解放します。             |

## <a name="remarks"></a>解説

このインターフェイスはランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 ただし、これは、 `IUnknown` `5c552ab6-fc09-4cb3-8e36-22fa03c798b7` 通常の com 機構を通じて取得できる GUID を使用してから派生する com インターフェイスです。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
