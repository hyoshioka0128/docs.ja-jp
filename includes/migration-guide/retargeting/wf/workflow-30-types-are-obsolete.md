---
ms.openlocfilehash: 358103d5816eb61c88738e9626fb02c563b507f8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617249"
---
### <a name="workflow-30-types-are-obsolete"></a>WorkFlow 3.0 タイプは廃止されました

#### <a name="details"></a>説明

Windows Workflow Foundation (WWF) 3.0 API (System.Workflow 名前空間からのもの) は廃止されました。

#### <a name="suggestion"></a>提案される解決策

新しい WWF 4.0 API (System.Activities) を代わりに使用する必要があります。 新しい API の使用例は[ここ](~/docs/framework/windows-workflow-foundation/how-to-update-the-definition-of-a-running-workflow-instance.md)にあり、詳しいガイダンスは[ここ](https://docs.microsoft.com/archive/blogs/workflowteam/wf3-types-marked-obsolete-in-net-4-5)にあります。 または、WWF 3.0 API はまだサポートされているので、使用でき、ビルド時の警告は、警告を抑制することによって、または以前のコンパイラを使用することによって回避できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |
