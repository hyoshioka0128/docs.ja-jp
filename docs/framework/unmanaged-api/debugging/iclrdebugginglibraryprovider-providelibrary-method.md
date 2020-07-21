---
title: ICLRDebuggingLibraryProvider::ProvideLibrary メソッド
ms.date: 03/30/2017
api_name:
- ICLRDebuggingLibraryProvider.ProvideLibrary Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebuggingLibraryProvider::ProvideLibrary
helpviewer_keywords:
- ProvideLibrary method [.NET Framework debugging]
- ICLRDebuggingLibraryProvider::ProvideLibrary method [.NET Framework debugging]
ms.assetid: 86f06245-9517-49be-8d8c-ca5deaf34c02
topic_type:
- apiref
ms.openlocfilehash: 7bbb49dc6ee9b1d29dd61ccdcfdacb62740133ed
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860263"
---
# <a name="iclrdebugginglibraryproviderprovidelibrary-method"></a>ICLRDebuggingLibraryProvider::ProvideLibrary メソッド

共通言語ランタイム (CLR) のバージョン固有のデバッグライブラリをオンデマンドで検索して読み込むことができるようにする、ライブラリプロバイダーのコールバックインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT ProvideLibrary(
     [in] const WCHAR* pwszFileName,
     [in] DWORD dwTimestamp,
     [in] DWORD dwSizeOfImage,
     [out] HMODULE* hModule);
```

## <a name="parameters"></a>パラメーター

`pwszFilename` \
から要求されているモジュールの名前。

`dwTimestamp` \
からPE ファイルの COFF ファイルヘッダーに格納されている日付と時刻のタイムスタンプ。

`pLibraryProvider` \
からPE `SizeOfImage`ファイルの COFF オプションファイルヘッダーに格納されているフィールド。

`hModule` \
入出力要求されたモジュールへのハンドル。

## <a name="return-value"></a>戻り値

このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。

|HRESULT|説明|
|-------------|-----------------|
|S_OK|メソッドは正常に完了しました。|

## <a name="exceptions"></a>例外

## <a name="remarks"></a>解説

`ProvideLibrary`デバッガーが、mscordbi.dll や mscordacwks などの特定の CLR ファイルをデバッグするために必要なモジュールを提供できるようにします。 モジュールハンドルは、 [ICLRDebugging:: CanUnloadNow](iclrdebugging-canunloadnow-method.md)メソッドの呼び出しによって解放される可能性があることが示されるまで有効なままにしておく必要があります。その時点で、呼び出し元がハンドルを解放する必要があります。

デバッガーは、使用可能な任意の方法を使用して、デバッグモジュールを見つけたり調達したりすることができます。

> [!IMPORTANT]
> この機能により、API 呼び出し元は、実行可能ファイルや悪意のあるコードを含むモジュールを提供できます。 セキュリティ上の理由から、呼び出し元はを`ProvideLibrary`使用して、それ自体を実行しないコードを配布することはできません。
>
> Mscordbi.dll や mscordacwks など、既にリリースされているライブラリで深刻なセキュリティの問題が検出された場合、shim には、ファイルの不適切なバージョンを認識するように修正プログラムを適用できます。 その後、shim は、修正されたバージョンのファイルに対する要求を発行し、要求に応答して指定されている場合は無効なバージョンを拒否します。 これは、ユーザーが shim の新しいバージョンに修正プログラムを適用している場合にのみ発生します。 修正プログラム脆弱性のバージョンは脆弱なままです。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]

## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
