---
title: セキュリティとパブリックの読み取り専用配列フィールド
description: アプリケーションの境界動作またはセキュリティを定義するために、読み取り専用のパブリック配列フィールドの使用を避ける必要がある理由をお読みください。
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
ms.openlocfilehash: 0a6a82c2c88fe61bd34c0accb831f018cf8702fc
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281434"
---
# <a name="security-and-public-read-only-array-fields"></a>セキュリティとパブリックの読み取り専用配列フィールド
読み取り専用のパブリック配列フィールドを変更できるため、マネージライブラリから読み取り専用パブリック配列フィールドを使用して、アプリケーションの境界動作またはセキュリティを定義しないでください。  
  
## <a name="remarks"></a>解説  

一部の .NET クラスには、プラットフォーム固有の境界パラメーターを含む読み取り専用のパブリックフィールドが含まれています。 たとえば、 <xref:System.IO.Path.InvalidPathChars> フィールドは、ファイルパス文字列で許可されていない文字を記述する配列です。 多くの同様のフィールドが .NET 全体に存在します。  
  
 のようなパブリック読み取り専用フィールドの値は、コード <xref:System.IO.Path.InvalidPathChars> またはコードのアプリケーションドメインを共有するコードによって変更できます。  アプリケーションの境界動作を定義するには、このような読み取り専用パブリック配列フィールドを使用しないでください。  そうすると、悪意のあるコードが境界の定義を変更し、予期しない方法でコードを使用できるようになります。  
  
 .NET Framework のバージョン2.0 以降では、パブリック配列フィールドを使用する代わりに、新しい配列を返すメソッドを使用する必要があります。  たとえば、フィールドを使用する代わりに、 <xref:System.IO.Path.InvalidPathChars> メソッドを使用する必要があり <xref:System.IO.Path.GetInvalidPathChars%2A> ます。  
  
 .NET Framework 型では、内部的に境界の種類を定義するためにパブリックフィールドが使用されないことに注意してください。  代わりに、.NET Framework は個別のプライベートフィールドを使用します。  これらのパブリックフィールドの値を変更しても、.NET Framework 型の動作は変更されません。  
  
## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](../../standard/security/secure-coding-guidelines.md)
