---
title: メンバー '<membername>' の型は CLS に準拠していません。
ms.date: 07/20/2015
f1_keywords:
- bc40025
- vbc40025
helpviewer_keywords:
- BC40025
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
ms.openlocfilehash: 030cb31b8f1ba0e8eaa82eeb8e37153411a53404
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400306"
---
# <a name="type-of-member-membername-is-not-cls-compliant"></a>メンバー '\<membername>' の型は CLS に準拠していません。
このメンバーに指定されたデータ型は、[言語への非依存性、および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) の一部ではありません。 .NET Framework と Visual Basic では、このデータ型をサポートしているため、コンポーネント内でエラーにはなりません。 ただし、厳密に CLS に準拠しているコードで記述された別のコンポーネントでは、このデータ型をサポートしていない可能性があります。 そのようなコンポーネントでは、使用しているコンポーネントと正常にやり取りできない場合があります。  
  
 次の Visual Basic データ型は CLS に準拠していません。  
  
- [SByte データ型](../data-types/sbyte-data-type.md)  
  
- [UInteger データ型](../data-types/uinteger-data-type.md)  
  
- [ULong データ型](../data-types/ulong-data-type.md)  
  
- [UShort データ型](../data-types/ushort-data-type.md)  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」を参照してください。  
  
 **エラー ID:** BC40025  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- コンポーネントが他の .NET Framework コンポーネントとのみやり取りする場合、または他のコンポーネントとやり取りしない場合は、何も変更する必要はありません。  
  
- .NET Framework 用に記述されていないコンポーネントとやり取りする場合は、リフレクションを通じて、またはドキュメントからこのデータ型がサポートされているかどうかを判断できます。 サポートされている場合は、何も変更する必要はありません。  
  
- このデータ型をサポートしていないコンポーネントとやり取りする場合は、それを最も近い CLS 準拠の型に置き換える必要があります。 たとえば、2,147,483,647 を超える値の範囲が不要な場合は、 `UInteger` の代わりに `Integer` を使用できます。 拡張範囲が必要な場合は、 `UInteger` の代わりに `Long`を使用できます。  
  
- オートメーション オブジェクトや COM オブジェクトとやり取りする場合は、一部の型のデータ幅が .NET Framework とは異なることに注意してください。 たとえば、他の多くの環境では `uint` は 16 ビットです。 そのようなコンポーネントに 16 ビットの引数を渡す場合は、Visual Basic のマネージド コードで、`UInteger` ではなく `UShort` として宣言します。  
  
## <a name="see-also"></a>関連項目

- [リフレクション](../../../framework/reflection-and-codedom/reflection.md)
