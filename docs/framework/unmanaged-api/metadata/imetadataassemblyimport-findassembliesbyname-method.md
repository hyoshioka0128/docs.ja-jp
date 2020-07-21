---
title: IMetaDataAssemblyImport::FindAssembliesByName メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.FindAssembliesByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::FindAssembliesByName
helpviewer_keywords:
- FindAssembliesByName method [.NET Framework metadata]
- IMetaDataAssemblyImport::FindAssembliesByName method [.NET Framework metadata]
ms.assetid: 4db97cf9-e4c1-4233-8efa-cbdc0e14a8e4
topic_type:
- apiref
ms.openlocfilehash: d2693a94f02214df6d7265b26e3d70d91adcf8a7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503836"
---
# <a name="imetadataassemblyimportfindassembliesbyname-method"></a>IMetaDataAssemblyImport::FindAssembliesByName メソッド
`szAssemblyName`参照を解決するために共通言語ランタイム (CLR) によって採用されている標準規則を使用して、指定したパラメーターを持つアセンブリの配列を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindAssembliesByName (  
    [in]  LPCWSTR     szAppBase,
    [in]  LPCWSTR     szPrivateBin,
    [in]  LPCWSTR     szAssemblyName,
    [out] IUnknown    *ppIUnk[],
    [in]  ULONG       cMax,
    [out] ULONG       *pcAssemblies  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szAppBase`  
 から指定されたアセンブリを検索するルートディレクトリ。 この値がに設定されている場合 `null` 、 `FindAssembliesByName` はアセンブリのグローバルアセンブリキャッシュ内だけを検索します。  
  
 `szPrivateBin`  
 からルートディレクトリの下のセミコロンで区切られたサブディレクトリ (たとえば、"bin; bin2") の一覧。このディレクトリで、アセンブリを検索します。 これらのディレクトリは、既定のプローブルールで指定されているものに加えてプローブされます。  
  
 `szAssemblyName`  
 から検索するアセンブリの名前。 この文字列の形式は、のクラス参照ページで定義されてい <xref:System.Reflection.AssemblyName> ます。  
  
 `ppIUnk`  
 からインターフェイスポインターを格納する[IUnknown](/cpp/atl/iunknown)型の配列 `IMetadataAssemblyImport` 。  
  
 `cMax`  
 入出力に配置できるインターフェイスポインターの最大数 `ppIUnk` 。  
  
 `pcAssemblies`  
 入出力返されたインターフェイスポインターの数。 つまり、実際に配置されたインターフェイスポインターの数 `ppIUnk` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`FindAssembliesByName`正常に返されました。|  
|`S_FALSE`|アセンブリがありません。|  
  
## <a name="remarks"></a>解説  
 アセンブリ名が指定されている場合、メソッドは、 `FindAssembliesByName` アセンブリ参照を解決するための標準の規則に従って、アセンブリを検索します。 (詳細については、「[ランタイムがアセンブリを検索する方法](../../deployment/how-the-runtime-locates-assemblies.md)」を参照してください)。`FindAssembliesByName`呼び出し元は、アプリケーションベースやプライベート検索パスなど、アセンブリリゾルバーコンテキストのさまざまな側面を構成できます。  
  
 `FindAssembliesByName`メソッドでは、アセンブリ解決ロジックを呼び出すために、プロセスで CLR を初期化する必要があります。 したがって、を呼び出す前に[Coinitializeee](../hosting/coinitializeee-function.md) (COINITEE_DEFAULT を渡す) を呼び出してから、CoUninitializeCor の呼び出しを実行する必要があり `FindAssembliesByName` [CoUninitializeCor](../hosting/couninitializecor-function.md)ます。  
  
 `FindAssembliesByName`渡されたアセンブリ名のアセンブリマニフェストを格納しているファイルへの[IMetaDataImport](imetadataimport-interface.md)ポインターを返します。 指定したアセンブリ名が完全に指定されていない場合 (たとえば、バージョンが含まれていない場合) は、複数のアセンブリが返されることがあります。  
  
 `FindAssembliesByName`は、コンパイル時に参照アセンブリの検索を試行するコンパイラによって一般的に使用されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ランタイムがアセンブリを検索する方法](../../deployment/how-the-runtime-locates-assemblies.md)
- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
