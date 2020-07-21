---
ms.openlocfilehash: 4d410811095786b33580d25f6c6eab3ac2f27148
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616104"
---
### <a name="resolveassemblyreference-task-now-warns-of-dependencies-with-the-wrong-architecture"></a>ResolveAssemblyReference タスクは、正しくないアーキテクチャとの依存関係に関する警告を表示するようになりました

#### <a name="details"></a>説明

タスクは警告 MSB3270 を生成します。これは参照または依存関係がアプリのアーキテクチャと一致しないことを示します。 たとえば、`AnyCPU` オプションでコンパイルされたアプリに x86 参照が含まれる場合に発生します。 このようなシナリオは、実行時にアプリでエラーが起こった場合に発生することがあります (この場合は、アプリが x64 プロセスとして配置されている場合)。

#### <a name="suggestion"></a>提案される解決策

影響には 2 つの領域があります。

- 再コンパイルすると、アプリが MSBuild の以前のバージョンでコンパイルされたときには現れなかった警告が生成されます。 ただし、警告はランタイム エラーの可能性のある原因を特定するため、調査と対処が必要です。
- 警告がエラーとして扱われると、アプリはコンパイルされません。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5.1       |
| 種類    | 再ターゲット中 |
