---
title: ICorDebugDataTarget2 インターフェイス
ms.date: 03/30/2017
ms.assetid: 13f11388-2f91-48d8-98d6-6a4a63cb5746
ms.openlocfilehash: 1c598d23cac77e50cf302e6936b88b5eb6e558c2
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976435"
---
# <a name="icordebugdatatarget2-interface"></a>ICorDebugDataTarget2 インターフェイス
によって、"の" を論理的に[拡張します](icordebugdatatarget-interface.md)。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateVirtualUnwinder メソッド](icordebugdatatarget2-createvirtualunwinder-method.md)|初期コンテキストからアンワインドを開始する新しいスタック アンワインダーを作成します (これは、必ずしもスレッドのリーフではありません)。|  
|[EnumerateThreadIDs メソッド](icordebugdatatarget2-enumeratethreadids-method.md)|アクティブなスレッド ID の一覧を返します。|  
|[GetImageFromPointer メソッド](icordebugdatatarget2-getimagefrompointer-method.md)|モジュールのアドレスから、そのモジュールのベース アドレスとサイズを返します。|  
|[GetImageLocation メソッド](icordebugdatatarget2-getimagelocation-method.md)|モジュールのベース アドレスからモジュールのパスを返します。|  
|[GetSymbolProviderForImage メソッド](icordebugdatatarget2-getsymbolproviderforimage-method.md)|モジュールのベース アドレスからそのモジュールのシンボル プロバイダーを返します。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは .NET ネイティブでのみ使用可能です。 .NET ネイティブの外部で ICorDebug シナリオについてこのインターフェイスを実装する場合は、共通言語ランタイムはこのインターフェイスを無視します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
