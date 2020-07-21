---
title: ISOSDacInterface インターフェイス
ms.date: 02/01/2019
api.name:
- ISOSDacInterface Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface Interface
helpviewer.keywords:
- ISOSDacInterface Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: c9b4e6e5b36fe38b6c0ea78f6d1848d155008bcc
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420969"
---
# <a name="isosdacinterface-interface"></a>ISOSDacInterface インターフェイス

からデータにアクセスするためのヘルパーメソッドを提供 `SOS` します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>メソッド

| メソッド                                                                                                               | 説明                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [GetMethodDescData](isosdacinterface-getmethoddescdata-method.md) | 指定された MethodDesc ポインターのデータを取得します。 |
| [GetMethodDescPtrFromIP](isosdacinterface-getmethoddescptrfromip-method.md) | 指定されたネイティブ命令アドレスを格納しているメソッドに対応する MethodDesc のポインターを取得します。 |
| [GetModuleData](isosdacinterface-getmoduledata-method.md)| 指定したアドレスに読み込まれたモジュールに対応するデータをフェッチします。 |

## <a name="remarks"></a>解説

このインターフェイスはランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 ただし、これは、 `IUnknown` `436f00f2-b42a-4b9f-870c-e73db66ae930` 通常の com 機構を通じて取得できる GUID を使用してから派生する com インターフェイスです。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
