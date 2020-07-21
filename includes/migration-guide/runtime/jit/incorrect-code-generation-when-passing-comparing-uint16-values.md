---
ms.openlocfilehash: c20d5fb3d700ba7649e423a79e4598b327c50a00
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622254"
---
### <a name="incorrect-code-generation-when-passing-and-comparing-uint16-values"></a>UInt16 値を渡して比較する場合にコード生成が正しく行われません

#### <a name="details"></a>説明

.NET Framework 4.7 で変更が導入されたため、.NET Framework 4.7 で実行されているアプリケーションの JIT コンパイラによって生成されたコードが 2 つの <code>T:System.UInt16</code> 値を正しく比較しない場合があります。 詳細については、GitHub.com の「[Issue #11508: Silent bad codegen when passing and comparing ushort args](https://github.com/dotnet/coreclr/issues/11508)」 (問題 #11508: ushort の引数を渡して比較する場合のサイレントかつ不適切な codegen ) を参照してください。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 で 16 ビットの符号なし値を比較したときに問題が検出された場合は、.NET Framework 4.7.1 にアップグレードしてください。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7|
|種類|ランタイム|
