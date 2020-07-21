---
title: プロパティと変数の違い
ms.date: 07/20/2015
helpviewer_keywords:
- property values [Visual Basic]
- variables [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- variables [Visual Basic], definition
- Visual Basic code, variables
- Visual Basic code, properties
- properties [Visual Basic], values
- properties [Visual Basic], defined
- variables [Visual Basic], and properties
- properties [Visual Basic], and variables
ms.assetid: 7a03a8be-5381-431f-bd7c-16e887e4e07b
ms.openlocfilehash: 162bd71eaebdf55f6be89e0c5dce7acc1b975d79
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403305"
---
# <a name="differences-between-properties-and-variables-in-visual-basic"></a>Visual Basic のプロパティと変数の違い
変数とプロパティはどちらも、アクセスできる値を表します。 ただし、ストレージと実装には相違点があります。  
  
## <a name="variables"></a>変数  
 "*変数*" は、メモリ位置に直接対応します。 変数は、1 つの宣言ステートメントで定義します。 変数は "*ローカル変数*" (プロシージャ内で定義され、そのプロシージャ内でのみ使用できる) とすることも、"*メンバー変数*" (モジュール、クラス、または構造体内で定義されるが、プロシージャ内では定義されない) とすることもできます。 メンバー変数は "*フィールド*" とも呼ばれます。  
  
## <a name="properties"></a>プロパティ  
 "*プロパティ*" は、モジュール、クラス、または構造体上で定義されたデータ要素です。 `Property` と `End Property` のステートメント間のコード ブロックを使用してプロパティを定義します。 コード ブロックには、`Get` プロシージャまたは `Set` プロシージャのいずれか、またはその両方が含まれます。 これらのプロシージャは、"*プロパティ プロシージャ*" または "*プロパティ アクセサー*" と呼ばれています。 プロパティの値を取得または格納するだけでなく、アクセス カウンターの更新などのカスタム アクションを実行することもできます。  
  
## <a name="differences"></a>相違点  
 次の表に変数とプロパティのいくつかの重要な相違点を示します。  
  
|相違点|変数|プロパティ|  
|-------------------------|--------------|--------------|  
|宣言|単一の宣言ステートメント|コード ブロック内の一連のステートメント|  
|実装|単一のストレージ場所|実行可能なコード (プロパティ プロシージャ)|  
|記憶域|変数の値に直接関連付けられる|通常、プロパティの包含クラスまたはモジュールの外部では使用できない内部ストレージがあります。<br /><br /> プロパティの値は格納された要素として存在する場合と存在しない場合があります <sup>1</sup>|  
|実行可能なコード|None|少なくとも 1 つのプロシージャが必要です。|  
|読み書きアクセス|読み書き、または読み取り専用|読み書き、読み取り専用、または書き込み専用|  
|カスタム アクション (値を受け入れ、または返すことに加えて)|サポートできません|プロパティ値の設定または取得の一部として実行できます。|  
  
 <sup>1</sup> 変数とは異なり、プロパティの値はストレージの単一の項目に直接対応しない場合があります。 利便性やセキュリティを高めるためにストレージが各ピースに分割される場合や、値が暗号化された形式で格納される場合があります。 このような場合、`Get` プロシージャによって各ピースの組み立てまたは格納されている値の暗号化の解除が行われ、`Set` プロシージャによって新しい値の暗号化または構成ストレージへの分割が行われます。 プロパティ値は時刻のように一時的なものである可能性があります。その場合は、プロパティにアクセスするたびに `Get` プロシージャによってそれが即座に計算されます。  
  
## <a name="see-also"></a>関連項目

- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Property ステートメント](../../../language-reference/statements/property-statement.md)
- [Dim ステートメント](../../../language-reference/statements/dim-statement.md)
- [方法: プロパティを作成する](./how-to-create-a-property.md)
- [方法: 複数のアクセス レベルを持つプロパティを宣言する](./how-to-declare-a-property-with-mixed-access-levels.md)
- [方法: プロパティ プロシージャを呼び出す](./how-to-call-a-property-procedure.md)
- [方法: 既定のプロパティを宣言して呼び出す (Visual Basic)](./how-to-declare-and-call-a-default-property.md)
- [方法: プロパティに値を格納する](./how-to-put-a-value-in-a-property.md)
- [方法: プロパティから値を取得する](./how-to-get-a-value-from-a-property.md)
