---
ms.openlocfilehash: 9b184f54650d2efb31ec66f443198b19ceaeb5f3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614708"
---
### <a name="applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a>Application.FilterMessage は、IMessageFilter.PreFilterMessage の再入可能な実装についてスローしなくなりました

#### <a name="details"></a>説明

.NET Framework 4.6.1 以前は、<xref:System.Windows.Forms.Application.AddMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=fullName> または <xref:System.Windows.Forms.Application.RemoveMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=fullName> (さらに <xref:System.Windows.Forms.Application.DoEvents>) を呼び出す<xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> で <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> を呼び出すと、<xref:System.IndexOutOfRangeException?displayProperty=fullName> が発生していました。<p/>.NET Framework 4.6.1 以降を対象とするアプリケーションでは、この例外がスローされなくなり、上述の再入可能フィルターを使用できます。

#### <a name="suggestion"></a>提案される解決策

上述の再入可能な <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> の動作に対して <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> はスローされなくなります。 これは、.NET Framework 4.6.1 をターゲットとするアプリケーションにのみ影響します。 .NET Framework 4.6.1 を対象とするアプリは、[DontSupportReentrantFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md#mitigation) 互換性スイッチを使用することによって、この変更を解除できます (または、以前の Framework をターゲットとしているアプリは、変更を受け入れることができます)。

| 名前          | [値]       |
|:--------------|:------------|
| スコープ         | エッジ        |
| バージョン       | 4.6.1       |
| 種類          | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)?displayProperty=nameWithType>
