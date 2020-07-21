---
title: データ型の概要
ms.date: 07/20/2015
helpviewer_keywords:
- Boolean data type [Visual Basic], supported types in Visual Basic
- storage [Visual Basic], order of storage
- data types [Visual Basic], Visual Basic
- Single data type [Visual Basic], supported types in Visual Basic
- notation [Visual Basic], scientific
- memory requirements, data types
- user-defined data types [Visual Basic], Visual Basic
- Date data type [Visual Basic], Visual Basic
- Visual Basic, data types
- storage [Visual Basic], allocation
- Integer data type [Visual Basic], Visual Basic data types
- storage [Visual Basic], space
- Variant data types [Visual Basic], supported types in Visual Basic
- Char data type [Visual Basic], Visual Basic data types
- intrinsic data types [Visual Basic]
- memory consumption [Visual Basic], data types
- single-precision numbers
- data types [Visual Basic], order of storage
- Long data type [Visual Basic], supported types in Visual Basic
- String data type [Visual Basic], Visual Basic data types
- storage order, data types
- StructLayoutAttribute class, Visual Basic data type storage
- scientific notation
- Double data type [Visual Basic], Visual Basic data types
- Byte data type [Visual Basic], Visual Basic data types
- Object data type [Visual Basic], supported types in Visual Basic
- data types [Visual Basic], storage allocation
- double-precision numbers
- data types [Visual Basic], summary
- dates [Visual Basic], data types
- strings [Visual Basic], data types
- memory consumption
- storage order, controlling in Visual Basic
- data types [Visual Basic], memory requirements
ms.assetid: e975cdb6-64d8-4a4a-ae27-f3b3ed198ae0
ms.openlocfilehash: 5eb52ef937a677c0b7498d058b5a39a375351ddc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "85503841"
---
# <a name="data-type-summary-visual-basic"></a>データ型の概要 (Visual Basic)

次の表に、Visual Basic のデータ型、サポートする共通言語ランタイム型、その公称ストレージ割り当て、およびそれらの値範囲を示します。  
  
|Visual Basic のデータ型|共通言語ランタイム型の構造|公称ストレージ割り当て|値の範囲|  
|-----------------------|--------------------------------------------|--------------------------------|-----------------|  
|[Boolean](boolean-data-type.md)|<xref:System.Boolean>|実装するプラットフォームに依存|`True` または `False`|  
|[Byte](byte-data-type.md)|<xref:System.Byte>|1 バイト|0 から 255 (符号なし)|  
|[Char](char-data-type.md) (1 文字)|<xref:System.Char>|2 バイト|0 から 65535 (符号なし)|  
|[Date](date-data-type.md)|<xref:System.DateTime>|8 バイト|0001 年 1 月 1 日 0:00:00 (午前 0 時) から 9999 年 12 月 31 日午後 11:59:59|  
|[Decimal](decimal-data-type.md)|<xref:System.Decimal>|16 バイト|0 から +/-79,228,162,514,264,337,593,543,950,335 (+/-7.9...E+28) <sup>†</sup> (小数点なし)、0 から +/-7.9228162514264337593543950335 (小数点の右側に 28 桁)<br /><br /> 0 以外の最小値は +/-0.0000000000000000000000000001 (+/-1E-28) <sup>†</sup>|  
|[Double](double-data-type.md) (倍精度浮動小数点)|<xref:System.Double>|8 バイト|-1.79769313486231570E+308 から -4.94065645841246544E-324 <sup>†</sup> (負の値の場合)<br /><br /> 4.94065645841246544E-324 から 1.79769313486231570E+308 <sup>†</sup> (正の値の場合)|  
|[Integer](integer-data-type.md)|<xref:System.Int32>|4 バイト|-2,147,483,648 から 2,147,483,647 (符号付き)|  
|[Long](long-data-type.md) (長整数)|<xref:System.Int64>|8 バイト|-9,223,372,036,854,775,808 から 9,223,372,036,854,775,807 (9.2...E+18 <sup>†</sup>) (符号付き)|  
|[オブジェクト](object-data-type.md)|<xref:System.Object> (クラス)|32 ビット プラットフォームでは 4 バイト<br /><br /> 64 ビット プラットフォームでは 8 バイト|`Object` 型の変数に任意の型を格納できる|  
|[SByte](sbyte-data-type.md)|<xref:System.SByte>|1 バイト|-128 から 127 (符号付き)|  
|[Short](short-data-type.md) (短整数)|<xref:System.Int16>|2 バイト|-32,768 から 32,767 (符号付き)|  
|[Single](single-data-type.md) (単精度浮動小数点)|<xref:System.Single>|4 バイト|-3.4028235E+38 から -1.401298E-45 <sup>†</sup> (負の値の場合)<br /><br /> 1.401298E-45 から 3.4028235E+38 <sup>†</sup> (正の値の場合)|  
|[String](string-data-type.md) (可変長)|<xref:System.String> (クラス)|実装するプラットフォームに依存|0 から約 20 億の Unicode 文字|  
|[UInteger](uinteger-data-type.md)|<xref:System.UInt32>|4 バイト|0 から 4,294,967,295 (符号なし)|  
|[ULong](ulong-data-type.md)|<xref:System.UInt64>|8 バイト|0 から 18,446,744,073,709,551,615 (1.8...E+19 <sup>†</sup>) (符号なし)|  
|[ユーザー定義](user-defined-data-type.md) (構造体)|(<xref:System.ValueType> から継承)|実装するプラットフォームに依存|構造体の各メンバーには、そのデータ型によって決定され、他のメンバーの範囲からは独立した範囲がある|  
|[UShort](ushort-data-type.md)|<xref:System.UInt16>|2 バイト|0 から 65,535 (符号なし)|  
  
 <sup>†</sup> *指数表記*では、"E" は 10 の累乗を表します。 したがって、3.56E+2 は 3.56 x 10<sup>2</sup> (356) を意味し、3.56E-2 は 3.56/10<sup>2</sup> (0.0356) を意味します。  
  
> [!NOTE]
> テキストを含む文字列の場合は、<xref:Microsoft.VisualBasic.Strings.StrConv%2A> 関数を使用してテキスト形式間で変換します。  
  
 宣言ステートメントでデータ型を指定するだけでなく、型文字を使用して一部のプログラミング要素のデータ型を強制的に指定することもできます。 「[型文字](../../programming-guide/language-features/data-types/type-characters.md)」を参照してください。  
  
## <a name="memory-consumption"></a>メモリの使用量  

 基本データ型を宣言する際に、メモリ消費量がその公称ストレージ割り当てと同じであると仮定するのは安全ではありません。 これは、次の考慮事項によるものです。  
  
- **ストレージの割り当て。** 共通言語ランタイムでは、アプリケーションが実行されているプラットフォームの現在の特性に基づいてストレージを割り当てることができます。 メモリがほぼ満杯の場合は、宣言された要素を可能な限り密に詰めることができます。 それ以外の場合は、パフォーマンスを最適化するために、メモリ アドレスを自然なハードウェア境界に合わせることができます。  
  
- **プラットフォームの幅。** 64 ビット プラットフォームでのストレージ割り当ては、32 ビット プラットフォームでの割り当てとは異なります。  
  
### <a name="composite-data-types"></a>複合データ型  

 構造体や配列など、複合データ型の各メンバーにも同じ考慮事項が適用されます。 型のメンバーの公称ストレージ割り当てを単純に追加することはできません。 さらに、次のようなその他の考慮事項があります。  
  
- **オーバーヘッド。** 一部の複合型には、追加のメモリ要件があります。 たとえば、配列では配列自体に、およびディメンションごとに追加のメモリが使用されます。 32 ビット プラットフォームでは、このオーバーヘッドは現在 12 バイトで、ディメンションごとに 8 バイトが追加されます。 64 ビット プラットフォームでは、この要件は 2 倍になります。  
  
- **ストレージ レイアウト。** メモリ内に格納される順序が宣言の順序と同じであると仮定するのは安全ではありません。 2 バイトや 4 バイトの境界など、バイトのアラインメントについても仮定することはできません。 クラスまたは構造体を定義していて、そのメンバーのストレージ レイアウトを制御する必要がある場合は、クラスまたは構造体に <xref:System.Runtime.InteropServices.StructLayoutAttribute> 属性を適用できます。  
  
### <a name="object-overhead"></a>オブジェクトのオーバーヘッド  

 任意の基本データ型または複合データ型を参照する `Object` では、データ型に含まれているデータに加えて 4 バイトが使用されます。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.StrConv%2A>
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [型文字](../../programming-guide/language-features/data-types/type-characters.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
