---
title: 配列のトラブルシューティング
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting arrays
- arrays [Visual Basic], initialization errors
- troubleshooting Visual Basic, arrays
- arrays [Visual Basic], compilation errors
- arrays [Visual Basic], declaration errors
- arrays [Visual Basic], troubleshooting
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
ms.openlocfilehash: e633c5a00693f188270b1610abaf2decb656b00a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414596"
---
# <a name="troubleshooting-arrays-visual-basic"></a>配列のトラブルシューティング (Visual Basic)
ここでは、配列を使用しているときに発生する可能性のある一般的な問題について説明します。  
  
## <a name="compilation-errors-declaring-and-initializing-an-array"></a>配列の宣言と初期化のコンパイル エラー  
 コンパイル エラーは、配列の宣言、作成、および初期化に関する規則の解釈の誤りが原因で発生する可能性があります。 エラーの最も一般的な原因は次のとおりです。  
  
- 配列変数宣言で、次元の長さを指定した後に [new 演算子](../../../language-reference/operators/new-operator.md)句を指定した。 次のコード行は、この型の無効な宣言を示しています。  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
- ジャグ配列の最上位の配列を超える次元の長さを指定した。 次のコード行は、この型の無効な宣言を示しています。  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
- 要素値を指定するときに `New` キーワードを省略した。 次のコード行は、この型の無効な宣言を示しています。  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
- 中かっこ (`{}`) を使用せずに `New` 句を指定した。 次のコード行は、この型の無効な宣言を示しています。  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## <a name="accessing-an-array-out-of-bounds"></a>範囲外の配列へのアクセス  
 配列を初期化するプロセスでは、各次元に上限と下限が割り当てられます。 配列の要素にアクセスする場合は必ず、有効なインデックス (添字) を次元ごとに指定する必要があります。 インデックスのいずれかが下限を下回るか上限を超えていると、<xref:System.IndexOutOfRangeException> 例外が発生します。 このようなエラーはコンパイラでは検出できないため、実行時にエラーが発生します。  
  
### <a name="determining-bounds"></a>境界の特定  
 配列が別のコンポーネントによってコードに渡される場合、たとえばプロシージャの引数として渡される場合、その配列のサイズやその次元の長さはわかりません。 どの要素でも、要素へのアクセスを試みる場合は必ず、配列のすべての次元の上限を事前に決めておく必要があります。 配列が Visual Basic の `New` 句以外の方法で作成された場合、下限は 0 以外の値になる可能性があるため、最も確実なのは下限も決めておくことです。  
  
### <a name="specifying-the-dimension"></a>次元の指定  
 多次元配列の境界を決めるときは、次元を指定する方法に注意してください。 <xref:System.Array.GetLowerBound%2A> メソッドと <xref:System.Array.GetUpperBound%2A> メソッドの `dimension` パラメーターは 0 から始まりますが、Visual Basic の <xref:Microsoft.VisualBasic.Information.LBound%2A> 関数と <xref:Microsoft.VisualBasic.Information.UBound%2A> 関数の `Rank` パラメーターは 1 から始まります。  
  
## <a name="see-also"></a>関連項目

- [配列](index.md)
- [方法: Visual Basic で配列変数を初期化する](how-to-initialize-an-array-variable.md)
