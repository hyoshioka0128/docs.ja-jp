---
title: ICorPublish::EnumProcesses メソッド
ms.date: 03/30/2017
api_name:
- ICorPublish.EnumProcesses
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::EnumProcesses
helpviewer_keywords:
- ICorPublish::EnumProcesses method [.NET Framework debugging]
- EnumProcesses method [.NET Framework debugging]
ms.assetid: 4ae765f0-93b2-4b6f-aea1-7b0cf44e04a7
topic_type:
- apiref
ms.openlocfilehash: 70255a89cee13abfe63b01351f8ffba51e54665a
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396404"
---
# <a name="icorpublishenumprocesses-method"></a>ICorPublish::EnumProcesses メソッド
このコンピューター上で実行されているマネージプロセスの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumProcesses (  
    [in] COR_PUB_ENUMPROCESS       Type,  
    [out] ICorPublishProcessEnum   **ppIEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `Type`  
 取得するプロセスの種類を指定する[COR_PUB_ENUMPROCESS](cor-pub-enumprocess-enumeration.md)列挙体の値。 現在のバージョンでは、COR_PUB_MANAGEDONLY のみが有効です。  
  
 `ppIEnum`  
 プロセスの列挙子である[ICorPublishProcessEnum](icorpublishprocessenum-interface.md)インスタンスのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 列挙子のプロセスのコレクションは、メソッドが呼び出されたときに実行されているプロセスのスナップショットに基づいてい `EnumProcesses` ます。 列挙子には、の呼び出しの前または後に終了するプロセスは含まれません `EnumProcesses` 。  
  
 `EnumProcesses`この[ICorPublish](icorpublish-interface.md)インスタンスでメソッドを複数回呼び出して、新しい最新のプロセスコレクションを作成することができます。 既存のコレクションは、メソッドの後続の呼び出しの影響を受けません `EnumProcesses` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublish インターフェイス](icorpublish-interface.md)
