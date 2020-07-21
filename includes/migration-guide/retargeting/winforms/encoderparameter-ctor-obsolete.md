---
ms.openlocfilehash: 4ad7c4c2781480c08ad4cf27e40de445b1c50671
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617244"
---
### <a name="encoderparameter-ctor-is-obsolete"></a>EncoderParameter ctor が廃止に

#### <a name="details"></a>説明

<xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)> コンストラクターは廃止され、使用された場合、ビルド警告が発生します。

#### <a name="suggestion"></a>提案される解決策

コンストラクター <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)> は引き続き動作しますが、.NET Framework 4.5 のツールでコードを再コンパイルするときに古いビルド警告を回避するには、コンストラクター <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Drawing.Imaging.EncoderParameterValueType,System.IntPtr)> を代わりに使用する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)>
