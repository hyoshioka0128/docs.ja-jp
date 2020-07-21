---
title: ICorDebugClass2::GetParameterizedType メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.GetParameterizedType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::GetParameterizedType
helpviewer_keywords:
- GetParameterizedType method [.NET Framework debugging]
- ICorDebugClass2::GetParameterizedType method [.NET Framework debugging]
ms.assetid: 94b591c4-9302-4af2-a510-089496afb036
topic_type:
- apiref
ms.openlocfilehash: 329bcee441b395982a8a8b539c0a938fa8170b14
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894054"
---
# <a name="icordebugclass2getparameterizedtype-method"></a>ICorDebugClass2::GetParameterizedType メソッド
このクラスの型宣言を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetParameterizedType (  
    [in] CorElementType                      elementType,  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType  *ppTypeArgs[],  
    [out] ICorDebugType                    **ppType  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `elementType`  
 からこのクラスの要素の型を指定する CorElementType 列挙体の値。この ICorDebugClass2 が値の型を表す場合は、この値を ELEMENT_TYPE_VALUETYPE に設定します。 この`ICorDebugClass2`が複合型を表す場合は、この値を ELEMENT_TYPE_CLASS に設定します。  
  
 `nTypeArgs`  
 から型がジェネリックの場合は、型パラメーターの数。 型パラメーターの数 (存在する場合) は、クラスで必要な数と一致する必要があります。  
  
 `ppTypeArgs`  
 からポインターの配列。各ポインターは、型パラメーターを表す、テキスト型のオブジェクトを指します。 クラスが非ジェネリックの場合、この値は null になります。  
  
 `ppType`  
 入出力型宣言を表す`ICorDebugType`オブジェクトのアドレスへのポインター。 このオブジェクトは、 <xref:System.Type>マネージコード内のオブジェクトに相当します。  
  
## <a name="remarks"></a>解説  
 クラスが非ジェネリックの場合、つまり、型パラメーターがない場合は、 `GetParameterizedType`クラスに対応するランタイム型オブジェクトを取得します。 クラス`elementType`が値型の場合、パラメーターは、クラスの正しい要素型に設定する必要があります: ELEMENT_TYPE_VALUETYPE。それ以外の場合は、ELEMENT_TYPE_CLASS ます。  
  
 クラスが型パラメーター (など`ArrayList<T>`) を受け入れる場合は、を使用`GetParameterizedType`して`ArrayList<int>`、インスタンス化された型 (など) の型オブジェクトを構築できます。  
  
## <a name="background-information"></a>背景情報  
 .NET Framework バージョン1.0 および1.1 では、メタデータ内のすべての型を、実行中のプロセスの型に直接マップすることができます。 したがって、メタデータ型とランタイム型には、実行中のプロセスで1つの表現が含まれていました。 ただし、メタデータ内の1つのジェネリック型は、実行中のプロセスの型のさまざまなインスタンス化にマップできます。 たとえば、 `SortedList<K,V>`メタデータ型は、 `SortedList<String, EmployeeRecord>` `SortedList<Int32, String>`、、 `SortedList<String,Array<Int32>>`などにマップできます。 そのため、型のインスタンス化を処理する方法が必要です。  
  
 .NET Framework バージョン2.0 では、 `ICorDebugType`インターフェイスが導入されています。 ジェネリック型の場合、オブジェクト`ICorDebugClass`また`ICorDebugClass2`はオブジェクトはインスタンス type (`SortedList<K,V>`) を表し、 `ICorDebugType`オブジェクトはインスタンス化されたさまざまな型を表します。 オブジェクト`ICorDebugClass`または`ICorDebugClass2`オブジェクトを指定した場合`ICorDebugType`は、 `ICorDebugClass2::GetParameterizedType`メソッドを呼び出すことによって、インスタンス化の対象となるオブジェクトを作成できます。 また、Int32 などの`ICorDebugType`単純型のオブジェクト、または非ジェネリック型のオブジェクトを作成することもできます。  
  
 型の実行時`ICorDebugType`の概念を表すオブジェクトの導入は、API 全体で波及効果を持ちます。 以前に`ICorDebugClass`または`ICorDebugClass2`オブジェクトを取得した関数`CorElementType` 、または値を使用`ICorDebugType`した関数は、オブジェクトを取得するために一般化されています。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
