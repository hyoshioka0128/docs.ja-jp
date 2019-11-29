---
title: 数値演算関数
ms.date: 07/20/2015
helpviewer_keywords:
- math functions, Visual Basic
- arithmetic operations, math functions
- math routines
- Atn function
ms.assetid: 4d2d82e7-6924-42fe-a4a7-b4dd5bebbd0c
ms.openlocfilehash: b1cd6a846a7dc1dddcf6bdb5eb99ebc1c57a012c
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348074"
---
# <a name="math-functions-visual-basic"></a>数値演算関数 (Visual Basic)
<xref:System.Math?displayProperty=nameWithType> クラスのメソッドは、三角関数、対数、およびその他の一般的な数学関数を提供します。  
  
## <a name="remarks"></a>コメント  
 <xref:System.Math?displayProperty=nameWithType> クラスのメソッドの一覧を次の表に示します。 これらは、Visual Basic プログラムで使用できます。  
  
|.NET メソッド|説明|  
|---------------------------|-----------------|  
|<xref:System.Math.Abs%2A>|数値の絶対値を返します。|  
|<xref:System.Math.Acos%2A>|コサインが指定数となる角度を返します。|  
|<xref:System.Math.Asin%2A>|サインが指定数となる角度を返します。|  
|<xref:System.Math.Atan%2A>|タンジェントが指定数となる角度を返します。|  
|<xref:System.Math.Atan2%2A>|タンジェントが 2 つの指定された数の商である角度を返します。|  
|<xref:System.Math.BigMul%2A>|2 32 ビットの数値の完全な積を返します。|  
|<xref:System.Math.Ceiling%2A>|指定された `Decimal` または `Double`以上の最小の整数値を返します。|  
|<xref:System.Math.Cos%2A>|指定された角度のコサインを返します。|  
|<xref:System.Math.Cosh%2A>|指定された角度のハイパーボリック コサインを返します。|  
|<xref:System.Math.DivRem%2A>|2 32 ビットまたは64ビット符号付き整数の商を返し、出力パラメーターの剰余も返します。|  
|<xref:System.Math.Exp%2A>|E (自然対数の底) を指定された指数で累乗した値を返します。|  
|<xref:System.Math.Floor%2A>|指定された `Decimal` または `Double` 数値以下の最大の整数を返します。|  
|<xref:System.Math.IEEERemainder%2A>|指定された数を別の指定数だけ除算した結果の剰余を返します。|  
|<xref:System.Math.Log%2A>|指定した数値または指定した底の指定した数値の対数を示す自然対数 (底 e) を返します。|  
|<xref:System.Math.Log10%2A>|指定した数の底 10 の対数を返します。|  
|<xref:System.Math.Max%2A>|2つの数値のうち、大きい方を返します。|  
|<xref:System.Math.Min%2A>|2 つの数のうち、小さい方を返します。|  
|<xref:System.Math.Pow%2A>|指定の数値を指定した値で累乗した値を返します。|  
|<xref:System.Math.Round%2A>|最も近い整数値または指定した小数部の桁数に丸められた `Decimal` または `Double` の値を返します。|  
|<xref:System.Math.Sign%2A>|数値の符号を示す `Integer` 値を返します。|  
|<xref:System.Math.Sin%2A>|指定された角度のサインを返します。|  
|<xref:System.Math.Sinh%2A>|指定された角度のハイパーボリック サインを返します。|  
|<xref:System.Math.Sqrt%2A>|指定された数値の平方根を返します。|  
|<xref:System.Math.Tan%2A>|指定された角度のタンジェントを返します。|  
|<xref:System.Math.Tanh%2A>|指定された角度のハイパーボリック タンジェントを返します。|  
|<xref:System.Math.Truncate%2A>|指定した `Decimal` または `Double` 数値の整数部を計算します。|  
  
 これらの関数を修飾なしで使用するには、ソースファイルの先頭に次のコードを追加して、<xref:System.Math?displayProperty=nameWithType> 名前空間をプロジェクトにインポートします。  
  
```vb
Imports System.Math  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Abs%2A> メソッドを使用して、数値の絶対値を計算します。  
  
```vb
' Returns 50.3.  
Dim MyNumber1 As Double = Math.Abs(50.3)  
' Returns 50.3.  
Dim MyNumber2 As Double = Math.Abs(-50.3)  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Atan%2A> メソッドを使用して、pi の値を計算します。  
  
```vb
Public Function GetPi() As Double  
    ' Calculate the value of pi.  
    Return 4.0 * Math.Atan(1.0)  
End Function  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Cos%2A> メソッドを使用して、角度のコサインを返します。  
  
```vb
Public Function Sec(ByVal angle As Double) As Double  
    ' Calculate the secant of angle, in radians.  
    Return 1.0 / Math.Cos(angle)  
End Function  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Exp%2A> メソッドを使用して、e の累乗を返します。  
  
```vb
Public Function Sinh(ByVal angle As Double) As Double  
    ' Calculate hyperbolic sine of an angle, in radians.  
    Return (Math.Exp(angle) - Math.Exp(-angle)) / 2.0  
End Function  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Log%2A> メソッドを使用して、数値の自然対数を返します。  
  
```vb
Public Function Asinh(ByVal value As Double) As Double  
    ' Calculate inverse hyperbolic sine, in radians.  
    Return Math.Log(value + Math.Sqrt(value * value + 1.0))  
End Function  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Round%2A> メソッドを使用して、数値を最も近い整数に丸めます。  
  
```vb
' Returns 3.  
Dim MyVar2 As Double = Math.Round(2.8)  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Sign%2A> メソッドを使用して、数値の符号を決定します。  
  
```vb
' Returns 1.  
Dim MySign1 As Integer = Math.Sign(12)  
' Returns -1.  
Dim MySign2 As Integer = Math.Sign(-2.4)  
' Returns 0.  
Dim MySign3 As Integer = Math.Sign(0)  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Sin%2A> メソッドを使用して、角度のサインを返します。  
  
```vb
Public Function Csc(ByVal angle As Double) As Double  
    ' Calculate cosecant of an angle, in radians.  
    Return 1.0 / Math.Sin(angle)  
End Function  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Sqrt%2A> メソッドを使用して、数値の平方根を計算します。  
  
```vb
' Returns 2.  
Dim MySqr1 As Double = Math.Sqrt(4)  
' Returns 4.79583152331272.  
Dim MySqr2 As Double = Math.Sqrt(23)  
' Returns 0.  
Dim MySqr3 As Double = Math.Sqrt(0)  
' Returns NaN (not a number).  
Dim MySqr4 As Double = Math.Sqrt(-4)  
```  
  
## <a name="example"></a>例  
 この例では、<xref:System.Math> クラスの <xref:System.Math.Tan%2A> メソッドを使用して、角度のタンジェントを返します。  
  
```vb
Public Function Ctan(ByVal angle As Double) As Double  
    ' Calculate cotangent of an angle, in radians.  
    Return 1.0 / Math.Tan(angle)  
End Function  
```  
  
## <a name="requirements"></a>要件  
 **クラス:** <xref:System.Math>  
  
 **名前空間:** <xref:System>  
  
 **アセンブリ:** mscorlib (mscorlib.dll 内)  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.VBMath.Rnd%2A>
- <xref:Microsoft.VisualBasic.VBMath.Randomize%2A>
- <xref:System.Double.NaN>
- [数値演算関数の導出](../../../visual-basic/language-reference/keywords/derived-math-functions.md)
- [算術演算子](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
