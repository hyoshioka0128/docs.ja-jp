---
title: COR_IL_MAP 構造体
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
ms.openlocfilehash: 4c79d0e4e37f3f884651e49c8fff6db72fac4f50
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179294"
---
# <a name="cor_il_map-structure"></a>COR_IL_MAP 構造体
機能の相対オフセットでの変更を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;
    ULONG32 newOffset;
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`oldOffset`|関数の先頭を基準とした、古い Microsoft 中間言語 (MSIL) オフセット。|  
|`newOffset`|関数の先頭を基準とした新しい MSIL オフセット。|  
|`fAccurate`|`true`マッピングが正確であることがわかっている場合。それ以外`false`の場合は、 .|  
  
## <a name="remarks"></a>解説  
 マップの形式は次のとおりです: デバッガーは、元の変更されていない`oldOffset`MSIL コード内の MSIL オフセットを参照することを想定します。 パラメーター`newOffset`は、新しいインストルメント化されたコード内の対応する MSIL オフセットを参照します。  
  
 ステップが正しく機能するためには、次の要件を満たす必要があります。  
  
- マップは昇順で並べ替える必要があります。  
  
- インストルメント化された MSIL コードは並べ替えできません。  
  
- 元の MSIL コードは削除しないでください。  
  
- マップには、プログラム データベース (PDB) ファイルからのすべてのシーケンス ポイントをマップするエントリが含まれている必要があります。  
  
 マップは、欠落しているエントリを補間しません。 次の例は、マップとその結果を示しています。  
  
 マップ：  
  
- 0 古いオフセット、0 新しいオフセット  
  
- 5 古いオフセット、10 の新しいオフセット  
  
- 9 古いオフセット、20 の新しいオフセット  
  
 結果:  
  
- 古いオフセットが 0、1、2、3、または 4 の場合は、新しいオフセット 0 にマップされます。  
  
- 古いオフセットが 5、6、7、または 8 の場合は、新しいオフセット 10 にマップされます。  
  
- 9 以上の古いオフセットは、新しいオフセット 20 にマップされます。  
  
- 新しいオフセット 0、1、2、3、4、5、6、7、8、または 9 は、古いオフセット 0 にマップされます。  
  
- 10、11、12、13、14、15、16、17、18、または 19 の新しいオフセットは、古いオフセット 5 にマップされます。  
  
- 20 以上の新しいオフセットは、古いオフセット 9 にマップされます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** コルデバッグ.idl、コルプロフ.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
