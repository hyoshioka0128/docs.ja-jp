---
title: ICorDebugClass インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass
helpviewer_keywords:
- ICorDebugClass interface [.NET Framework debugging]
ms.assetid: 03a6facb-f12f-49be-9839-e73b9c791cd5
topic_type:
- apiref
ms.openlocfilehash: d7417e8dc193172c77d23fe3fa72c8298d802b5c
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894039"
---
# <a name="icordebugclass-interface"></a>ICorDebugClass インターフェイス

基本型または複合型 (つまり、ユーザー定義) のいずれかの型を表します。 型がジェネリックの場合、`ICorDebugClass` はインスタンス化されないジェネリック型を表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetModule メソッド](icordebugclass-getmodule-method.md)|このクラスを定義するモジュールを取得します。|  
|[GetStaticFieldValue メソッド](icordebugclass-getstaticfieldvalue-method.md)|指定された静的フィールドの値を取得します。|  
|[GetToken メソッド](icordebugclass-gettoken-method.md)|このクラス`TypeDef`のメタデータトークンを取得します。|  
  
## <a name="remarks"></a>解説  
 インターフェイス`ICorDebugClass`は、インスタンスジェネリック型を表します。 は、インスタンス化されたジェネリック型を表します。 たとえば、 `Hashtable<K, V>`はで`ICorDebugClass` `Hashtable<Int32, String>`表されますが、はによっ`ICorDebugType`て表されます。  
  
 非ジェネリック型は、と`ICorDebugClass` `ICorDebugType`の両方で表されます。 後者のインターフェイスは、型のインスタンス化を処理するために .NET Framework バージョン2.0 で導入されました。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
