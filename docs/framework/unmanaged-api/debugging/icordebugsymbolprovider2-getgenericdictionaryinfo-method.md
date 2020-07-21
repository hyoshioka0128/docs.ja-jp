---
title: ICorDebugSymbolProvider2::GetGenericDictionaryInfo メソッド
ms.date: 03/30/2017
ms.assetid: ba28fe4e-5491-4670-bff7-7fde572d7593
ms.openlocfilehash: a6c32b72c5924399aeb13d56ddf9242fe7990f35
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379321"
---
# <a name="icordebugsymbolprovider2getgenericdictionaryinfo-method"></a>ICorDebugSymbolProvider2::GetGenericDictionaryInfo メソッド

汎用のディクショナリ マップを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetGenericDictionaryInfo(
   [out] ICorDebugMemoryBuffer** ppMemoryBuffer
);
```

## <a name="parameters"></a>パラメーター

`ppMemoryBuffer`\
入出力ジェネリックディクショナリマップを格納している、[のオブジェクトの](icordebugmemorybuffer-interface.md)アドレスへのポインター。 詳細については、「解説」を参照してください。

## <a name="remarks"></a>Remarks

> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。

このマップは最上位レベルの 2 つのセクションで構成されています。

- このマップに含まれるすべてのディクショナリの相対仮想アドレス (RVA) を格納している[ディレクトリ](#Directory)。

- オブジェクトのインスタンス化情報を格納するバイト固定[ヒープ](#Heap)。 最後のディレクトリ エントリの直後から開始します。

<a name="Directory"></a>

## <a name="the-directory"></a>ディレクトリ

ディレクトリ内の各エントリは、ヒープ内のオフセットを参照します。つまり、これは、ヒープの開始位置を基準としたオフセットです。 個々のエントリの値が一意とは限りません。このため、複数のディクショナリ エントリがヒープ内の同一オフセットを指すことがあります。

汎用のディクショナリ マップのディレクトリ部分の構造は次のとおりです。

- 最初の 4 バイトには、ディクショナリのエントリ数 (ディクショナリ内の相対仮想アドレスの数) が格納されています。 この値は*N*として参照されます。上位ビットが設定されている場合、エントリは相対仮想アドレスで昇順に並べ替えられます。

- *N*ディレクトリエントリは次のようになります。 各エントリは 8 バイトであり、次の 2 つの 4 バイト セグメントからなります。

  - バイト 0 ～ 3: RVA (ディクショナリの相対仮想アドレス)。

  - バイト 4 ～ 7: オフセット (ヒープの開始位置を基準としたオフセット)。

<a name="Heap"></a>

## <a name="the-heap"></a>ヒープ

ヒープのサイズは、ストリーム リーダーにより、ディレクトリ サイズ + 4 の値からストリームの長さを差し引くことで算出されます。 つまり、以下の要件が適用されます。

```csharp
Heap Size = Stream.Length – (Directory Size + 4)
```

ディレクトリのサイズが `N * 8` であるとします。

ヒープの各インスタンス化情報項目の形式は次のとおりです。

- このインスタンス化情報項目のバイト単位の長さ。圧縮 ECMA メタデータ形式です。 値では、この長さ情報が除外されます。

- 圧縮された ECMA メタデータ形式のジェネリックインスタンス化型 ( *T*) の数。

- *T*型はそれぞれ ECMA 型シグネチャ形式で表されます。

各ヒープ要素の長さを含めることで、ヒープに影響を与えずに、ディレクトリ セクションの単純な並べ替えを実行できるようになります。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]

## <a name="see-also"></a>関連項目

- [ICorDebugSymbolProvider2 インターフェイス](icordebugsymbolprovider2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
