---
title: '方法: Point4D 構造体が等価かどうかをテストする'
ms.date: 03/30/2017
helpviewer_keywords:
- inequality [WPF], testing Point4D structures for
- equality [WPF], testing Point4D structures for
- testing [WPF], Point4D structures for equality
- Point4D structures [WPF], testing for inequality
- testing [WPF], Point4D structures for inequality
- Point4D structures [WPF], testing for equality
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
ms.openlocfilehash: ce1188e99ef2b0682427cc2e227aaccd27f7c4f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62050637"
---
# <a name="how-to-test-point4d-structures-for-equality-and-inequality"></a>方法: Point4D 構造体が等価かどうかをテストする
この例では、<xref:System.Windows.Media.Media3D.Point4D> 構造体の等価性と非等価性をテストする方法を示します。  
  
 次のコードは、<xref:System.Windows.Media.Media3D.Point4D> 等価性メソッドを利用し、<xref:System.Windows.Media.Media3D.Point4D> 構造体の等価性と非等価性をテストする方法を示すものです。  <xref:System.Windows.Media.Media3D.Point4D> 構造体の等価性がオーバーロードされた等価性 (`==`) 演算子でテストされ、その後、オーバーロードされた非等価性 (`!=`) 演算子で非等価性がテストされ、最後に、静的 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A> メソッドを利用し、<xref:System.Windows.Media.Media3D.Point3D> 構造体と <xref:System.Windows.Media.Media3D.Point4D> 構造体の等価性が確認されます。  
  
## <a name="example"></a>例  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>
