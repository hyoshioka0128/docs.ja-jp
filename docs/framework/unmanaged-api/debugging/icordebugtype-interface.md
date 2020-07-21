---
title: ICorDebugType インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType
helpviewer_keywords:
- ICorDebugType interface [.NET Framework debugging]
ms.assetid: 94e02e31-67ea-4b00-8148-a46740a4571d
topic_type:
- apiref
ms.openlocfilehash: 5e88652ff75223e30e6abc454f1e1af91494c7b2
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396703"
---
# <a name="icordebugtype-interface"></a>ICorDebugType インターフェイス
基本または複合 (つまり、ユーザー定義) のいずれかの型を表します。 型がジェネリックの場合、`ICorDebugType` はインスタンス化されたジェネリック型を表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumerateTypeParameters メソッド](icordebugtype-enumeratetypeparameters-method.md)|このによって参照されるクラスのジェネリックパラメーターを参照する、ツールのインターフェイスポインターを取得し <xref:System.Type> `ICorDebugType` ます。|  
|[GetBase メソッド](icordebugtype-getbase-method.md)|`ICorDebugType`このによって参照されるクラス `ICorDebugType` (存在する場合) の基本クラスを参照するへのインターフェイスポインターを取得します。|  
|[GetClass メソッド](icordebugtype-getclass-method.md)|このの型指定されたコンストラクターを参照する、によるクラスへのインターフェイスポインターを取得し `ICorDebugType` ます。|  
|[GetFirstTypeParameter メソッド](icordebugtype-getfirsttypeparameter-method.md)|`ICorDebugType` <xref:System.Type> このによって参照されるクラスのコンストラクターの最初のジェネリックパラメーターを参照するへのインターフェイスポインターを取得し `ICorDebugType` ます。|  
|[GetRank メソッド](icordebugtype-getrank-method.md)|配列型の次元数を取得します。|  
|[GetStaticFieldValue メソッド](icordebugtype-getstaticfieldvalue-method.md)|指定したスタックフレーム内の指定したフィールドトークンによって参照される静的フィールドの値を格納する、ICorDebugValue へのインターフェイスポインターを取得します。|  
|[GetType メソッド](icordebugtype-gettype-method.md)|このによって参照される共通言語ランタイムのネイティブ型を記述する CorElementType 値を取得し <xref:System.Type> `ICorDebugType` ます。|  
  
## <a name="remarks"></a>解説  
 型がジェネリックの場合、は `ICorDebugClass` インスタンス型を表します。 インターフェイスは、 `ICorDebugType` インスタンス化されたジェネリック型を表します。 たとえば、ハッシュテーブル \< K、V> はで表さ `ICorDebugClass` れますが、hashtable \< Int32、String> はによって表さ `ICorDebugType` れます。  
  
 非ジェネリック型は、との両方で表され `ICorDebugClass` `ICorDebugType` ます。 後者のインターフェイスは、型のインスタンス化を処理するために .NET Framework バージョン2.0 で導入されました。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
