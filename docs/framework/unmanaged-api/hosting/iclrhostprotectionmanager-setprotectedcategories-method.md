---
title: ICLRHostProtectionManager::SetProtectedCategories メソッド
ms.date: 03/30/2017
api_name:
- ICLRHostProtectionManager.SetProtectedCategories
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostProtectionManager::SetProtectedCategories
helpviewer_keywords:
- SetProtectedCategories method [.NET Framework hosting]
- ICLRHostProtectionManager::SetProtectedCategories method [.NET Framework hosting]
ms.assetid: fa21dc7b-5da7-440b-b59e-9180e5181f9d
topic_type:
- apiref
ms.openlocfilehash: 5cf6f942add3d090cf830e71a545b9f4d4f69f00
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703163"
---
# <a name="iclrhostprotectionmanagersetprotectedcategories-method"></a>ICLRHostProtectionManager::SetProtectedCategories メソッド
部分信頼コードでの実行をブロックする必要があるマネージ型およびメンバーのカテゴリを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetProtectedCategories (  
    [in] EApiCategories  categories  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `categories`  
 から部分信頼コードでの実行をブロックする必要があるマネージ型およびメンバーのカテゴリを示す、 [EApiCategories](eapicategories-enumeration.md)値の組み合わせ。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetProtectedCategories`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 各 `EApiCategories` 値は、マネージ型とメンバーのリストを参照します。 `EApiCategories`列挙体と `SetProtectedCategories` メソッドは、マネージクラスに直接関連付けられ <xref:System.Security.Permissions.HostProtectionAttribute> ます。これは、マネージ型と、によって記述されたカテゴリに対応する機能を公開するメンバーをマークするために使用され `EApiCategories` ます。 詳細については、「」および列挙を参照してください <xref:System.Security.Permissions.HostProtectionAttribute> <xref:System.Security.Permissions.HostProtectionResource> 。これは、に直接対応 `EApiCategories` します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Security.Permissions.HostProtectionAttribute>
- <xref:System.Security.Permissions.HostProtectionResource>
- [EApiCategories 列挙型](eapicategories-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRHostProtectionManager インターフェイス](iclrhostprotectionmanager-interface.md)
