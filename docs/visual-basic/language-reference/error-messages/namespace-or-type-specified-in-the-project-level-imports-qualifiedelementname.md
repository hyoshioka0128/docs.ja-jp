---
title: プロジェクト レベルのインポート '<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。
ms.date: 07/20/2015
f1_keywords:
- vbc40057
- bc40057
helpviewer_keywords:
- BC40057
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
ms.openlocfilehash: 0ee235252d69e6f77ce53b048f45e73d0969e864
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409453"
---
# <a name="namespace-or-type-specified-in-the-project-level-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a>プロジェクト レベルのインポート '\<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。
プロジェクト レベルのインポート '\<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。 名前空間または型が定義されており、少なくとも 1 つのパブリック メンバーが含まれていることを確認してください。 別名の名前に他の別名が含まれていないことを確認してください。  
  
 プロジェクトの import プロパティが、見つからないか、`Public` メンバーを定義しないコンテナー要素を指定しています。  
  
 *コンテナー要素*は、名前空間、クラス、構造体、モジュール、インターフェイス、または列挙型にすることができます。 コンテナー要素には、変数、プロシージャ、その他のコンテナー要素などのメンバーが含まれています。  
  
 インポートの目的は、コードによって名前空間または型のメンバーに、それらを修飾しなくてもアクセスできるようにすることです。 また、プロジェクトで名前空間や型への参照を追加する必要がある場合もあります。 詳細については、「[宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)」の "コンテナー要素のインポート" に関するセクションを参照してください。  
  
 コンパイラは、指定したコンテナー要素が見つからない場合、それを使用する参照を解決できません。 要素が見つかったが、要素が `Public` のメンバーを公開していない場合、参照を正常に実行できません。 どちらの場合も、要素をインポートしても意味がありません。  
  
 インポートする要素を指定するには、**プロジェクト デザイナー**を使用します。 **[参照]** ページの **[インポートされた名前空間]** セクションを使用します。 **プロジェクト デザイナー**には、**ソリューション エクスプローラー**の **[マイ プロジェクト]** アイコンをダブルクリックするとアクセスできます。  
  
 **エラー ID:** BC40057  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. **プロジェクト デザイナー**を開き、 **[参照]** ページに切り替えます。  
  
2. **[インポートされた名前空間]** セクションで、コンテナー要素がプロジェクトからアクセス可能であることを確認します。  
  
3. コンテナー要素が少なくとも 1 つの `Public` メンバーを公開していることを確認します。  
  
## <a name="see-also"></a>関連項目

- [[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
- [Public](../modifiers/public.md)
- [Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)
- [宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
