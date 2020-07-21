---
title: ICorDebugILFrame4::EnumerateLocalVariablesEx メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.EnumerateLocalVariablesEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6f60aae6-70ec-4c4c-963a-138df98c4668
topic_type:
- apiref
ms.openlocfilehash: aef28af3eff6aba03003f156b9226b61a8e72d5b
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213752"
---
# <a name="icordebugilframe4enumeratelocalvariablesex-method"></a>ICorDebugILFrame4::EnumerateLocalVariablesEx メソッド
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 フレームのローカル変数の列挙子を取得し、プロファイラー ReJIT インストルメンテーションに追加される変数も含みます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT EnumerateLocalVariablesEx(  
   [in] ILCodeKind flags,
   [out] ICorDebugValueEnum **ppValueEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `flags`  
 からプロファイラー ReJIT インストルメンテーションに追加された変数がフレームに含まれるかどうかを指定する[Ilcodekind](ilcodekind-enumeration.md)列挙型のメンバー。  
  
 `ppValueEnum`  
 入出力このフレーム内のローカル変数の列挙子である "テキスト" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、 [EnumerateLocalVariables](icordebugilframe-enumeratelocalvariables-method.md)メソッドに似ていますが、プロファイラー rejit インストルメンテーションに追加された変数にオプションでアクセスする点が異なります。 をに設定すること `flags` `ILCODE_ORIGINAL_IL` は、 [EnumerateLocalVariables](icordebugilframe-enumeratelocalvariables-method.md)を呼び出した場合と同じです。 `flags` を `ILCODE_REJIT_IL` に設定することにより、デバッガは プロファイラー ReJIT インストルメンテーションに追加されるローカル変数にアクセスできるようになります。 中間言語 (IL) がインストルメント化されていない場合は、列挙子は空になり、メソッドは `S_OK` を返します。  
  
 実行中のメソッドにあるすべてのローカル変数が列挙子に含まれない場合がありますが、それは一部のローカル変数が非アクティブである可能性があるためです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugILFrame4 インターフェイス](icordebugilframe4-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [ReJIT: ハウツーガイド](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)
