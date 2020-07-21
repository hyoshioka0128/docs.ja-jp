---
title: ICorProfilerObjectEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum
helpviewer_keywords:
- ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: 13e1651c-9523-40ef-bfd7-87fb94519f8b
topic_type:
- apiref
ms.openlocfilehash: 5ebe99dd8d1d7ec73cd140991a4b13dfa381791d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494645"
---
# <a name="icorprofilerobjectenum-interface"></a>ICorProfilerObjectEnum インターフェイス
[Ngen.exe (ネイティブイメージジェネレーター)](../../tools/ngen-exe-native-image-generator.md)によって生成される固定されたオブジェクトのコレクションを順番に反復処理するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Clone メソッド](icorprofilerobjectenum-clone-method.md)|この `ICorProfilerObjectEnum` インターフェイスのコピーへのインターフェイス ポインターを取得します。|  
|[GetCount メソッド](icorprofilerobjectenum-getcount-method.md)|コレクション内の固定されたオブジェクトの合計数を取得します。|  
|[Next メソッド](icorprofilerobjectenum-next-method.md)|シーケンス内の列挙子の現在位置を開始位置として、オブジェクトのシーケンシャルコレクションから、指定された数の連続するオブジェクトを取得します。|  
|[Reset メソッド](icorprofilerobjectenum-reset-method.md)|この列挙子のカーソルをシーケンスの開始位置に移動します。|  
|[Skip メソッド](icorprofilerobjectenum-skip-method.md)|指定された数の要素がスキップされるように、この列挙子のカーソルを現在の位置から進めます。|  
  
## <a name="remarks"></a>解説  
 `ICorProfilerObjectEnum` インターフェイスは列挙子です。 このインターフェイスにより、配列の受信側は、受信側に適した速度で送信側から要素をプルできます。 つまり、受信側は配列要素のフローを明示的に制御できるため、大きな配列をメソッドパラメーターとして渡すことに関連する問題を回避できます。  
  
 インターフェイスへのポインターを取得するには、 [ICorProfilerInfo2:: EnumModuleFrozenObjects](icorprofilerinfo2-enummodulefrozenobjects-method.md)を使用し `ICorProfilerObjectEnum` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [EnumModuleFrozenObjects メソッド](icorprofilerinfo2-enummodulefrozenobjects-method.md)
