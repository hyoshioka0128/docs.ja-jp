---
ms.openlocfilehash: 4a65e721e5639f12445a9a44f46baa0d26898a88
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615673"
---
### <a name="il-ret-not-allowed-in-a-try-region"></a>try 領域で IL ret が許可されない

#### <a name="details"></a>説明

JIT64 Just-In-Time コンパイラとは異なり、(.NET Framework 4.6 で使用される) RyuJIT では、try 領域で IL ret 命令が許可されません。 ECMA-335 仕様により try 領域から戻ることは許可されておらず、そうした IL を生成する既知のマネージド コンパイラはありません。 ただし、JIT64 コンパイラは、リフレクション出力を使用して生成される場合にはこうした IL を実行します。

#### <a name="suggestion"></a>提案される解決策

try 領域に ret オペコードを含む IL をアプリが生成する場合、そのアプリでは .NET Framework 4.5 を対象にして以前の JIT を使用し、この中断を回避できます。 あるいは、try 領域の後に戻るように生成後の IL を更新できます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |
