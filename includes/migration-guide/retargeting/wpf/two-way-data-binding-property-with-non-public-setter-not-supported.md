---
ms.openlocfilehash: 5f1a8af37a305ab0904801002dd99e17e8eca62e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616123"
---
### <a name="two-way-data-binding-to-a-property-with-a-non-public-setter-is-not-supported"></a>非パブリック セッターを持つプロパティへの双方向データ バインドはサポートされません

#### <a name="details"></a>説明

パブリック セッターを持たないプロパティへのデータ バインドを試みることは、サポートされるシナリオではありません。 .NET framework 4.5.1 以降では、このシナリオでは <xref:System.InvalidOperationException?displayProperty=fullName> がスローされます。 この新しい例外は、具体的に .NET Framework 4.5.1 を対象とするアプリでのみスローされることに注意してください。 アプリが .NET Framework 4.5 をターゲットとしている場合、この呼び出しは許されます。 アプリが特定のバージョンの .NET Framework をターゲットにしていない場合、バインドは一方向として扱われます。

#### <a name="suggestion"></a>提案される解決策

一方向のバインドを使用するか、プロパティのセッターを公開するように、アプリを更新する必要があります。 または、.NET Framework 4.5 をターゲットにすると、アプリは以前の動作を示すようになります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Data.BindingMode.TwoWay?displayProperty=nameWithType>
