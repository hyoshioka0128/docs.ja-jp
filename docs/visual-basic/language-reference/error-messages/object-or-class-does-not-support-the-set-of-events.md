---
title: オブジェクトまたはクラスがこのイベント セットをサポートしていません。
ms.date: 07/20/2015
f1_keywords:
- vbrID459
ms.assetid: 785df3f3-2aae-4a25-af36-1f9879d4e5fd
ms.openlocfilehash: bc75e031c2d05bea3aa64774a9d3817756e51e8b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409362"
---
# <a name="object-or-class-does-not-support-the-set-of-events"></a>オブジェクトまたはクラスがこのイベント セットをサポートしていません。
指定されたイベント セットのイベント ソースとして機能しないコンポーネントで、`WithEvents` 変数を使用しようとしました。 たとえば、オブジェクトのイベントをシンクしてから、最初のオブジェクトを `Implements` する別のオブジェクトを作成するとします。 実装されたオブジェクトからイベントをシンクできると思うかもしれませんが、常にそうであるとは限りません。 `Implements` は、メソッドとプロパティのインターフェイスのみを実装します。 `WithEvents` は、`ObjectEvent` を発生させるために必要な型情報が実行時に使用できないため、非公開の `UserControls` ではサポートされていません。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. イベントを発生させないコンポーネントのイベントをシンクすることはできません。  
  
## <a name="see-also"></a>関連項目

- [WithEvents](../modifiers/withevents.md)
- [Implements ステートメント](../statements/implements-statement.md)
