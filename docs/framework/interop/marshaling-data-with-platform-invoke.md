---
title: プラットフォーム呼び出しによるデータのマーシャリング
description: .NET でプラットフォーム呼び出しを使用してデータをマーシャリングします。 Windows API および C スタイルの関数で使用されるデータ型の一覧を参照し、対応する .NET マネージド型を検索します。
ms.date: 03/20/2019
dev_langs:
- cpp
helpviewer_keywords:
- platform invoke, marshaling data
- data marshaling, platform invoke
- marshaling, platform invoke
ms.assetid: dc5c76cf-7b12-406f-b79c-d1a023ec245d
ms.openlocfilehash: 27045790780c1eef9537bdf7e52deb579e2b467c
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904105"
---
# <a name="marshaling-data-with-platform-invoke"></a>プラットフォーム呼び出しによるデータのマーシャリング

アンマネージド ライブラリからエクスポートされた関数を呼び出すには、.NET Framework アプリケーションで、マネージド コード内にアンマネージド 関数を表す関数プロトタイプが必要です。 プラットフォーム呼び出しがデータを正しくマーシャリングできるようにするプロトタイプを作成するには、次のことを実行する必要があります。

- <xref:System.Runtime.InteropServices.DllImportAttribute> 属性をマネージド コード内の静的関数またはメソッドに適用します。

- アンマネージド データ型をマネージド データ型に置き換えます。

アンマネージド 関数に付属のドキュメントを使用して、属性とその省略可能なフィールドを適用し、アンマネージド型をマネージド データ型に置き換えることによって、同等のマネージド プロトタイプを作成できます。 <xref:System.Runtime.InteropServices.DllImportAttribute> を適用する方法の詳細については、「[アンマネージ DLL 関数の処理](consuming-unmanaged-dll-functions.md)」を参照してください。

このセクションでは、アンマネージド ライブラリによってエクスポートされた関数に引数を渡し、その関数からの戻り値を受け取るための、マネージド関数のプロトタイプを作成する方法を示すサンプルを示します。 サンプルではまた、いつ <xref:System.Runtime.InteropServices.MarshalAsAttribute> 属性と <xref:System.Runtime.InteropServices.Marshal> クラスを使用して明示的にデータをマーシャリングするかをも示しています。

## <a name="platform-invoke-data-types"></a>プラットフォーム呼び出しのデータ型

次の表は、Windows API と C スタイルの関数で使用されるデータ型を一覧で示しています。 多くのアンマネージ ライブラリには、これらのデータ型をパラメーターや戻り値として渡す関数が含まれています。 3 番目の列には、マネージド コードで使用する、対応する .NET Framework の組み込みの値型またはクラスを一覧で示します。 場合によっては、表にリストされた型を、同じサイズの型に置き換えることができます。

|Windows API でのアンマネージ型|アンマネージ C 言語型|マネージド型|説明|
|--------------------------------|-------------------------------|------------------------|-----------------|
|`VOID`|`void`|<xref:System.Void?displayProperty=nameWithType>|値を返さない関数に適用されます。|
|`HANDLE`|`void *`|<xref:System.IntPtr?displayProperty=nameWithType> または <xref:System.UIntPtr?displayProperty=nameWithType>|32 ビット Windows オペレーティング システム、64 ビット Windows オペレーティング システムで 64 ビットに 32 ビットです。|
|`BYTE`|`unsigned char`|<xref:System.Byte?displayProperty=nameWithType>|8 ビット|
|`SHORT`|`short`|<xref:System.Int16?displayProperty=nameWithType>|16 ビット|
|`WORD`|`unsigned short`|<xref:System.UInt16?displayProperty=nameWithType>|16 ビット|
|`INT`|`int`|<xref:System.Int32?displayProperty=nameWithType>|32 ビット|
|`UINT`|`unsigned int`|<xref:System.UInt32?displayProperty=nameWithType>|32 ビット|
|`LONG`|`long`|<xref:System.Int32?displayProperty=nameWithType>|32 ビット|
|`BOOL`|`long`|<xref:System.Boolean?displayProperty=nameWithType> または <xref:System.Int32?displayProperty=nameWithType>|32 ビット|
|`DWORD`|`unsigned long`|<xref:System.UInt32?displayProperty=nameWithType>|32 ビット|
|`ULONG`|`unsigned long`|<xref:System.UInt32?displayProperty=nameWithType>|32 ビット|
|`CHAR`|`char`|<xref:System.Char?displayProperty=nameWithType>|ANSI で装飾します。|
|`WCHAR`|`wchar_t`|<xref:System.Char?displayProperty=nameWithType>|Unicode で装飾します。|
|`LPSTR`|`char *`|<xref:System.String?displayProperty=nameWithType> または <xref:System.Text.StringBuilder?displayProperty=nameWithType>|ANSI で装飾します。|
|`LPCSTR`|`const char *`|<xref:System.String?displayProperty=nameWithType> または <xref:System.Text.StringBuilder?displayProperty=nameWithType>|ANSI で装飾します。|
|`LPWSTR`|`wchar_t *`|<xref:System.String?displayProperty=nameWithType> または <xref:System.Text.StringBuilder?displayProperty=nameWithType>|Unicode で装飾します。|
|`LPCWSTR`|`const wchar_t *`|<xref:System.String?displayProperty=nameWithType> または <xref:System.Text.StringBuilder?displayProperty=nameWithType>|Unicode で装飾します。|
|`FLOAT`|`float`|<xref:System.Single?displayProperty=nameWithType>|32 ビット|
|`DOUBLE`|`double`|<xref:System.Double?displayProperty=nameWithType>|64 ビット|

Visual Basic、C#、および C++ での対応する型については、「[.NET Framework クラス ライブラリの概要](../../standard/class-library-overview.md#system-namespace)」を参照してください。

## <a name="pinvokelibdll"></a>PinvokeLib.dll

次のコードでは、Pinvoke.dll によって提供されるライブラリ関数を定義します。 このセクションで説明される多くのサンプルでは、このライブラリを呼び出します。

### <a name="example"></a>例

[!code-cpp[PInvokeLib#1](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.cpp#1)]

[!code-cpp[PInvokeLib#2](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.h#2)]
