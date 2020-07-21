---
title: IXCLRDataMethodDefinition インターフェイス
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodDefinition Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodDefinition Interface
helpviewer.keywords:
- IXCLRDataMethodDefinition Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: ebb689eee4a89a70e81d8f9d958e7826c3b3421b
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420956"
---
# <a name="ixclrdatamethoddefinition-interface"></a>IXCLRDataMethodDefinition インターフェイス

メソッド定義に関する情報を照会するためのメソッドを提供します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>メソッド

次のメソッドは、インターフェイスで使用できるメソッドの一部です。

| メソッド                                                                                                                          | 説明                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [StartEnumInstances](ixclrdatamethoddefinition-startenuminstances-method.md) | 指定されたのメソッドインスタンスの列挙体のハンドルを提供 `IXCLRDataAppDomain` します。 |
| [EnumInstance](ixclrdatamethoddefinition-enuminstance-method.md)             | このメソッド定義のインスタンスを列挙します。                                         |
| [EndEnumInstances](ixclrdatamethoddefinition-endenuminstances-method.md)     | インスタンスの列挙中に使用される内部反復子によって使用されるリソースを解放します。         |

## <a name="remarks"></a>解説

このインターフェイスはランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 ただし、これは、 `IUnknown` `AAF60008-FB2C-420b-8FB1-42D244A54A97` 通常の com 機構を通じて取得できる GUID を使用してから派生する com インターフェイスです。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
