---
ms.openlocfilehash: 986b647047aaa4a185c1403e96e499ae587bea98
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617538"
---
### <a name="httpruntimeappdomainapppath-throws-a-nullreferenceexception"></a>HttpRuntime.AppDomainAppPath で NullReferenceException がスローされる

#### <a name="details"></a>説明

ランタイムによってスローされる、.NET Framework 4.6.2、`T:System.NullReferenceException`取得するときに、 `P:System.Web.HttpRuntime.AppDomainAppPath` null 文字を含む値です。 .NET Framework 4.6.1 と以前のバージョンでは、ランタイムによってスローされる、`T:System.ArgumentNullException`です。

#### <a name="suggestion"></a>提案される解決策

次のいずれかでこの変更に対応できます。

- アプリケーションが .NET Framework 4.6.2 で実行されている場合には `T:System.NullReferenceException` を処理します。
- .NET Framework 4.7 にアップグレードします。以前の動作が復元され、`T:System.ArgumentNullException` がスローされます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Web.HttpRuntime.AppDomainAppPath?displayProperty=nameWithType>
