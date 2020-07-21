---
title: シャドウとオーバーライドの違い
ms.date: 07/20/2015
helpviewer_keywords:
- shadowing, vs. overriding
- overriding, vs. shadowing
ms.assetid: 2d014a0b-7630-407d-8f4e-24bd87987923
ms.openlocfilehash: a6ea83fadf18ef3be778e6de31c0eb4e65e74824
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392871"
---
# <a name="differences-between-shadowing-and-overriding-visual-basic"></a>シャドウとオーバーライドの違い (Visual Basic)
基底クラスから継承するクラスを定義する場合、派生クラスの 1 つ以上の基底クラス要素を再定義する必要があることがあります。 この目的では、シャドウとオーバーライドの両方を使用できます。  
  
## <a name="comparison"></a>比較  
 シャドウとオーバーライドは、どちらも派生クラスが基底クラスから継承されるときに使用し、どちらも一方の宣言された要素を他方の要素で再定義します。 しかし、この 2 つには、大きな違いがあります。  
  
 次の表で、シャドウとオーバーライドを比較しています。  
  
||||  
|---|---|---|  
|比較のポイント|シャドウ|オーバーライド|  
|目的|既に派生クラスに定義しているメンバーを取り込む、基底クラスの後続の変更から保護します|同じ呼び出しシーケンス<sup>1</sup>で、プロシージャまたはプロパティの異なる実装を定義することによって、ポリモーフィズムを実現します|  
|再定義された要素|任意の宣言された要素型|プロシージャ (`Function`、`Sub`、または `Operator`) またはプロパティのみ|  
|再定義する要素|任意の宣言された要素型|同じ呼び出しシーケンス<sup>1</sup> のプロシージャまたはプロパティのみ|  
|再定義する要素のアクセス レベル|任意のアクセス レベル|オーバーライドされた要素のアクセス レベルは変更できません|  
|再定義する要素の読みやすさと記述のしやすさ|任意の組み合わせ|オーバーライドされたプロパティの読みやすさと記述のしやすさを変更することはできません|  
|再定義の制御|基底クラス要素ではシャドウを強制または禁止できません|基底クラス要素では、`MustOverride`、`NotOverridable`、または `Overridable` を指定できます|  
|キーワードの使用方法|派生クラスでは `Shadows` が推奨されます。`Shadows` も `Overrides` も指定されていない場合<sup>2</sup>、`Shadows` と見なされます|基底クラスでは `Overridable` または `MustOverride` が必要です。派生クラスでは `Overrides` が必要です|  
|派生クラスから派生するクラスによる再定義する要素の継承|さらに派生したクラスによって継承された要素のシャドウ。シャドウされた要素は引き続き非表示になります<sup>3</sup>|さらに派生したクラスによって継承された要素のオーバーライド。オーバーライドされた要素は引き続きオーバーライドされます|  
  
 <sup>1</sup> *呼び出しシーケンス* は、要素の型 (`Function`、`Sub`、`Operator`、または `Property`)、名前、パラメーター リスト、および戻り値の型から構成されます。 プロパティでプロシージャをオーバーライドすることはできません。また、その逆もできません。 ある種類のプロシージャ (`Function`、`Sub`、または `Operator`) を別の種類でオーバーライドすることはできません。  
  
 <sup>2</sup> `Shadows` または `Overrides` を指定しない場合、使用する再定義の種類を確認できるように、コンパイラによって警告メッセージが発行されます。 警告を無視すると、シャドウ メカニズムが使用されます。  
  
 <sup>3</sup> さらに派生したクラスから、シャドウする要素にアクセスできない場合、シャドウは継承されません。 たとえば、シャドウする要素を `Private` として宣言した場合、派生クラスから派生したクラスでは、シャドウする要素ではなく元の要素が継承されます。  
  
## <a name="guidelines"></a>ガイドライン  
 通常、オーバーライドは次の場合に使用します。  
  
- ポリモーフィックな派生クラスを定義している。  
  
- コンパイラに同一の要素型と呼び出しシーケンスを適用させる安全性が必要である。  
  
 通常、シャドウは次の場合に使用します。  
  
- 基底クラスが変更される可能性があると予想し、自分の要素と同じ名前を使用して要素を定義する。  
  
- 要素の型や呼び出しシーケンスを自由に変更したいと考えている。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic におけるシャドウ](shadowing.md)
- [方法: 自分で宣言した変数と同じ名前の変数を隠す](how-to-hide-a-variable-with-the-same-name-as-your-variable.md)
- [方法: 継承された変数を隠す](how-to-hide-an-inherited-variable.md)
- [方法: 派生クラスによって非表示になっている変数にアクセスする](how-to-access-a-variable-hidden-by-a-derived-class.md)
- [Shadows](../../../language-reference/modifiers/shadows.md)
- [Overrides](../../../language-reference/modifiers/overrides.md)
