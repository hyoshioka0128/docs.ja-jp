---
ms.openlocfilehash: 9a2d6a25a8ab1b8bf65b947557802e0805a7f826
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617200"
---
### <a name="foreach-iterator-variable-is-now-scoped-within-the-iteration-so-closure-capturing-semantics-are-different-in-c5"></a>foreach 反復子変数は、イテレーション内をスコープとするようになったため、クロージャ キャプチャのセマンティクスが (C#5 では) 異なります。

#### <a name="details"></a>説明

C#5 (Visual Studio 2012) 以降では、`foreach` 反復子変数は、イテレーション内をスコープとします。 このため、変数が `foreach` のクロージャに含まれないことに依存していたコードは機能しなくなります。 この変更による症状は、デリゲートに渡された反復子変数が、デリゲートが呼び出された時点での値ではなく、デリゲートの作成時点での値として扱われることです。

#### <a name="suggestion"></a>提案される解決策

理想的には、新しいコンパイラの動作を予期するように、コードを更新する必要があります。 古いセマンティクスが必要な場合は、反復子変数を、ループのスコープ外に明示的に配置される別の変数に置き換えることができます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |
