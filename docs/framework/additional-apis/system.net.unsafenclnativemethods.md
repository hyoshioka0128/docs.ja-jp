---
title: UnsafeNclNativeMethods クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.UnsafeNclNativeMethods
- System.Net.UnsafeNclNativeMethods.NativePKI
- System.Net.UnsafeNclNativeMethods.NativePKI.FindClientCertificates
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 46756a0d1d69b4768dbb8dcdd7ab098d3f1849bf
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990533"
---
# <a name="unsafenclnativemethods-class"></a>UnsafeNclNativeMethods クラス

Unsafe ネイティブネットワークメソッドをインポートするクラスが含まれています。 このクラスは継承できません。

```csharp
internal static class UnsafeNclNativeMethods
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="nativepki-class"></a>Pipki クラス

crypt32.dll からインポートされたメソッドを格納します。 これらのメソッドは、ハイパーテキスト転送プロトコルセキュア (HTTPS) を使用する場合に証明書を処理します。 このクラスは継承できません。

```csharp
internal static class NativePKI
```

## <a name="nativepkifindclientcertificates-method"></a>Pipki. FindClientCertificates メソッド

サーバーに送信できる使用可能なクライアント証明書を検出します。

```csharp
internal static X509CertificateCollection FindClientCertificates
```

### <a name="return-value"></a>戻り値

<xref:System.Security.Cryptography.X509Certificates.X509CertificateCollection?displayProperty=nameWithType>

使用可能なクライアント証明書のコレクション。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
