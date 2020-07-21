---
title: '方法: イメージ メタデータを読み取る'
desription: Learn how to read the Windows Forms PropertyItems property of an Image object to retrieve all the metadata from a file.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- metadata [Windows Forms], property item
- metadata [Windows Forms], reading image
ms.assetid: 72ec0b31-0be7-444a-9575-1dbcb864e0be
ms.openlocfilehash: 814cb17feba1e1e3a42b2bc403b0b4c828caf90e
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174667"
---
# <a name="how-to-read-image-metadata"></a>方法: イメージ メタデータを読み取る

一部のイメージファイルには、イメージの機能を確認するために読み取ることができるメタデータが含まれています。 たとえば、デジタル写真には、イメージのキャプチャに使用されるカメラのメーカーとモデルを決定するために読み取ることができるメタデータが含まれている場合があります。 GDI + を使用すると、既存のメタデータを読み取ることができます。また、イメージファイルに新しいメタデータを書き込むこともできます。

GDI + は、オブジェクトに個々のメタデータを格納 <xref:System.Drawing.Imaging.PropertyItem> します。 <xref:System.Drawing.Image.PropertyItems%2A>オブジェクトのプロパティを読み取って <xref:System.Drawing.Image> 、ファイルからすべてのメタデータを取得できます。 プロパティは、 <xref:System.Drawing.Image.PropertyItems%2A> オブジェクトの配列を返し <xref:System.Drawing.Imaging.PropertyItem> ます。

<xref:System.Drawing.Imaging.PropertyItem>オブジェクトには、、、 `Id` `Value` `Len` 、およびの4つのプロパティがあります `Type` 。

## <a name="id"></a>Id

メタデータ項目を識別するタグ。 次の表に、に割り当てることができる値をいくつか <xref:System.Drawing.Imaging.PropertyItem.Id%2A> 示します。

|16 進数値|説明|
|-----------------------|-----------------|
|0x0320<br /><br /> 0x010F<br /><br /> 0x0110<br /><br /> 0x9003<br /><br /> 0x829A<br /><br /> 0x5090<br /><br /> 0x5091|イメージのタイトル<br /><br /> 装置の製造元<br /><br /> 装置モデル<br /><br /> ExifDTOriginal<br /><br /> Exif 公開時間<br /><br /> 輝度テーブル<br /><br /> クロミナンステーブル|

## <a name="value"></a>値

値の配列です。 値の形式は、プロパティによって決まり <xref:System.Drawing.Imaging.PropertyItem.Type%2A> ます。

## <a name="len"></a>Len

プロパティが指す値の配列の長さ (バイト単位) <xref:System.Drawing.Imaging.PropertyItem.Value%2A> 。

## <a name="type"></a>種類

プロパティが指す配列内の値のデータ型 `Value` 。 次の表に、プロパティ値によって示される形式を `Type` 示します。

|数値|説明|
|-------------------|-----------------|
|1|`Byte`|
|2|`Byte`ASCII としてエンコードされたオブジェクトの配列|
|3|16ビット整数|
|4|32ビット整数|
|5|有理数を表す2つのオブジェクトの配列 `Byte`|
|6|使用されていない|
|7|未定義|
|8|使用されていない|
|9|`SLong`|
|10|`SRational`|

## <a name="example"></a>例
  
次のコード例では、ファイル内の7つのメタデータを読み取り、表示し `FakePhoto.jpg` ます。 リスト内の2番目の (インデックス 1) プロパティ項目には、 <xref:System.Drawing.Imaging.PropertyItem.Id%2A> 0x010F (装置の製造元) と <xref:System.Drawing.Imaging.PropertyItem.Type%2A> 2 (ASCII エンコードされたバイト配列) があります。 このコード例では、そのプロパティ項目の値を表示します。

[!code-csharp[System.Drawing.WorkingWithImages#51](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#51)]
[!code-vb[System.Drawing.WorkingWithImages#51](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#51)]

このコードでは、次のような出力が生成されます。

```output
 Property Item 0
  
 id: 0x320
  
 type: 2

 length: 16 bytes
  
 Property Item 1
  
 id: 0x10f
  
 type: 2
  
 length: 17 bytes
  
 Property Item 2
  
 id: 0x110
  
 type: 2
  
 length: 7 bytes
  
 Property Item 3
  
 id: 0x9003
  
 type: 2
  
 length: 20 bytes
  
 Property Item 4
  
 id: 0x829a
  
 type: 5
  
 length: 8 bytes
  
 Property Item 5
  
 id: 0x5090
  
 type: 3
  
 length: 128 bytes
  
 Property Item 6
  
 id: 0x5091
  
 type: 3
  
 length: 128 bytes
  
 The equipment make is Northwind Camera.
 ```

## <a name="compiling-the-code"></a>コードのコンパイル

前の例は、Windows フォームで使用するように設計されてい <xref:System.Windows.Forms.PaintEventArgs> `e` ます。これは、イベントハンドラーのパラメーターであるを必要とし <xref:System.Windows.Forms.Control.Paint> ます。 フォームのイベントを処理 <xref:System.Windows.Forms.Control.Paint> し、このコードを描画イベントハンドラーに貼り付けます。 を `FakePhoto.jpg` システム上で有効なイメージ名とパスに置き換えて、名前空間をインポートする必要があり `System.Drawing.Imaging` ます。

## <a name="see-also"></a>関連項目

- [イメージ、ビットマップ、およびメタファイル](images-bitmaps-and-metafiles.md)
- [イメージ、ビットマップ、アイコン、およびメタファイルの操作](working-with-images-bitmaps-icons-and-metafiles.md)
