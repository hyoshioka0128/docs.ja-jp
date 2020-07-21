---
title: "'<constructorname>' の基本クラス '<baseclassname>' にある '<derivedclassname>' が古い形式に設定されているため、この 'Sub New' の最初のステートメントは、明示的な 'MyBase.New' または 'MyClass.New' への呼び出しでなければなりません: '<errormessage>'"
ms.date: 07/20/2015
f1_keywords:
- vbc30920
- bc30920
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
ms.openlocfilehash: 33dd15e3f5f5538963597f2b00f4214895e1f47a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403006"
---
# <a name="first-statement-of-this-sub-new-must-be-an-explicit-call-to-mybasenew-or-myclassnew-because-the-constructorname-in-the-base-class-baseclassname-of-derivedclassname-is-marked-obsolete-errormessage"></a>'\<constructorname>' の基本クラス '\<baseclassname>' にある '\<derivedclassname>' が古い形式に設定されているため、この 'Sub New' の最初のステートメントは、明示的な 'MyBase.New' または 'MyClass.New' への呼び出しでなければなりません: '\<errormessage>'
クラス コンストラクターが基底クラスのコンストラクターを明示的に呼び出さず、暗黙的な基底クラスのコンストラクターが <xref:System.ObsoleteAttribute> 属性およびエラーとして扱うことを示すディレクティブでマークされています。  
  
 派生クラスのコンストラクターが基底クラスのコンストラクターを呼び出さない場合、Visual Basic では、パラメーターなしの基底クラスのコンストラクターの暗黙的な呼び出しを生成しようとします。 引数を指定せずに呼び出すことができるアクセス可能なコンストラクターが基底クラスにない場合、Visual Basic では暗黙的な呼び出しを生成できません。 この場合、必要なコンストラクターが <xref:System.ObsoleteAttribute> 属性でマークされるため、Visual Basic では呼び出すことができません。  
  
 どのプログラミング要素でも、 <xref:System.ObsoleteAttribute> を適用すれば、もう使用しなくなったものとしてマークを付けることができます。 これを行う場合、この属性の <xref:System.ObsoleteAttribute.IsError%2A> プロパティを `True` または `False`のどちらかに設定できます。 `True`に設定した場合、この要素を使用しようとすると、コンパイラはエラーとして処理します。 `False`に設定した場合、または既定値の `False`を使用した場合、コンパイラはこの要素の使用が試行されると、警告を発行します。  
  
 **エラー ID:** BC30920  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 引用符で囲まれたエラー メッセージを確認し、適切な処理を行います。  
  
2. `MyBase.New()` または `MyClass.New()` の呼び出しを `Sub New` の最初のステートメントとして派生クラスに含めます。  
  
## <a name="see-also"></a>関連項目

- [属性の概要](../../programming-guide/concepts/attributes/index.md)
