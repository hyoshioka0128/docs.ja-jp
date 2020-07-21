---
ms.openlocfilehash: e9d34465970287ed94c0f0373ee4ae94d55aa1ff
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617179"
---
### <a name="machinekeyencode-and-machinekeydecode-methods-are-now-obsolete"></a>MachineKey.Encode メソッドと MachineKey.Decode メソッドが廃止に

#### <a name="details"></a>説明

これらのメソッドは今後使用しません。 これらのメソッドを呼び出すコードをコンパイルすると、コンパイラ警告が生成されます。

#### <a name="suggestion"></a>提案される解決策

別の方法として、<xref:System.Web.Security.MachineKey.Protect(System.Byte[],System.String[])> および <xref:System.Web.Security.MachineKey.Unprotect(System.Byte[],System.String[])> を使用することをお勧めします。 または、ビルド警告を抑制するか、古いコンパイラを使用して警告を回避できます。 API は、まだサポートされています。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Web.Security.MachineKey.Encode(System.Byte[],System.Web.Security.MachineKeyProtection)?displayProperty=nameWithType>
- <xref:System.Web.Security.MachineKey.Decode(System.String,System.Web.Security.MachineKeyProtection)?displayProperty=nameWithType>
