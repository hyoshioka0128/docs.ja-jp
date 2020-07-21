---
title: Me、My、MyBase、および MyClass
ms.date: 07/20/2015
f1_keywords:
- MyClass
- vb.Me
- MyBase
- vb.MyBase
- Me
- vb.MyClass
- vb.This
- vb.My
helpviewer_keywords:
- My object
- self-reference [Visual Basic], Me keyword
- MyClass keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], referring to the current instance of an object
- Me keyword [Visual Basic]
- self-reference
- current instance [Visual Basic], Me keyword
- MyBase keyword [Visual Basic], relationship to similar programming elements
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
ms.openlocfilehash: b4470e5c178c0f66dc33956ea0131d4eabc51d46
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397468"
---
# <a name="me-my-mybase-and-myclass-in-visual-basic"></a>Visual Basic における Me、My、MyBase、MyClass
Visual Basic の `Me`、`My`、`MyBase`、`MyClass` は、名前は似ていますが目的が異なります。 このトピックでは、これらのエンティティを区別するために、それぞれについて説明します。  
  
## <a name="me"></a>Me  
 `Me` キーワードを使用すると、コードが現在実行されている、クラスまたは構造体の特定のインスタンスを参照できます。 `Me` は、現在のインスタンスを参照するオブジェクト変数または構造体変数と同様に動作します。 `Me` の使用は、クラスまたは構造体の現在実行されているインスタンスに関する情報を、別のクラス、構造体、またはモジュールのプロシージャに渡す際に特に役立ちます。  
  
 たとえば、モジュールに次のプロシージャがあるとします。  
  
```vb  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 このプロシージャを呼び出し、次のステートメントを使用して、<xref:System.Windows.Forms.Form> クラスの現在のインスタンスを引数として渡すことができます。  
  
```vb  
ChangeFormColor(Me)  
```  
  
## <a name="my"></a>My  
 `My` 機能を使用すると、多数の .NET Framework クラスに簡単かつ直感的にアクセスできるので、Visual Basic ユーザーはコンピューター、アプリケーション、設定、リソースなどを操作できます。  
  
## <a name="mybase"></a>MyBase  
 `MyBase` キーワードは、クラスの現在のインスタンスの基底クラスを参照するオブジェクト変数と同様に動作します。 `MyBase` は、派生クラスでオーバーライドまたはシャドウされた基底クラスのメンバーにアクセスするためによく使用されます。 `MyBase.New` は、派生クラスのコンストラクターから基底クラスのコンストラクターを明示的に呼び出すために使用されます。  
  
## <a name="myclass"></a>MyClass  
 `MyClass` キーワードは、もともと実装されているクラスの現在のインスタンスを参照するオブジェクト変数と同様に動作します。 `MyClass` は `Me` に似ていますが、これに対するすべてのメソッド呼び出しは、メソッドが `NotOverridable` であるかのように扱われます。  
  
## <a name="see-also"></a>関連項目

- [継承の基本](../language-features/objects-and-classes/inheritance-basics.md)
