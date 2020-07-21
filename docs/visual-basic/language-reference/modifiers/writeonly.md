---
title: WriteOnly
ms.date: 07/20/2015
f1_keywords:
- WriteOnly
- vb.WriteOnly
helpviewer_keywords:
- write-only properties
- WriteOnly keyword [Visual Basic]
- sensitive data, protecting
- properties [Visual Basic], write-only
- sensitive data
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
ms.openlocfilehash: a9fa0a3a23561215d6ff122bc8e609b68ca6fc30
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84386635"
---
# <a name="writeonly-visual-basic"></a>WriteOnly (Visual Basic)
プロパティを書き込めるが、読み込みはできないことを示します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="rules"></a>ルール  
 **宣言コンテキスト。** `WriteOnly` は、モジュール レベルでのみ使用できます。 つまり、`WriteOnly` プロパティの宣言コンテキストは、クラス、構造体、またはモジュールにする必要があり、ソース ファイル、名前空間、またはプロシージャにすることはできません。  
  
 プロパティは、変数ではなく `WriteOnly` として宣言できます。  
  
## <a name="when-to-use-writeonly"></a>WriteOnly を使用するタイミング  
 場合によっては、使用しているコードで値を設定できても、それが何であるかを検出できないようにする必要があります。 たとえば、社会登録番号やパスワードなどの機密データは、それが設定されていないコンポーネントからはアクセスできないようにする必要があります。 このような場合は、`WriteOnly` プロパティを使用して値を設定できます。  
  
> [!IMPORTANT]
> `WriteOnly` プロパティを定義して使用する場合は、次の追加の保護対策を検討してください。  
  
- **オーバーライド。** プロパティがクラスのメンバーである場合は、既定値の [NotOverridable](notoverridable.md) に設定できます。`Overridable` または `MustOverride` としては宣言しないでください。 これにより、派生クラスがオーバーライドによって不要なアクセスを行うのを防ぐことができます。  
  
- **アクセス レベル。** プロパティの機密データを 1 つ以上の変数に保持する場合は、他のコードがアクセスできないように、[Private](private.md) として宣言してください。  
  
- **暗号化。** すべての機密データを、プレーンテキストではなく暗号化された形式で保存します。 悪意のあるコードが何らかの方法でメモリ領域にアクセスできた場合は、そのデータを使用するのが難しくなります。 暗号化は、機密データをシリアル化する必要がある場合にも役立ちます。  
  
- **リセット。** プロパティを定義するクラス、構造体、またはモジュールが終了しているときに、機密データを既定値またはその他の意味のない値にリセットします。 これにより、メモリの領域が一般的なアクセス用に解放されているときに、追加の保護が提供されます。  
  
- **永続性。** 機密データは、ディスクなどにはなるべく保存しないでください。 また、機密データをクリップボードに書き込まないでください。  
  
 `WriteOnly` 修飾子は、次のコンテキストで使用できます。  
  
 [Property ステートメント](../statements/property-statement.md)  
  
## <a name="see-also"></a>関連項目

- [ReadOnly](readonly.md)
- [Private](private.md)
- [キーワード](../keywords/index.md)
