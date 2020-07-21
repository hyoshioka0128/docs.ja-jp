---
title: My.Forms と My.WebServices が提供する既定のオブジェクト インスタンス
ms.date: 07/20/2015
helpviewer_keywords:
- My.WebServices object [Visual Basic], developing applications
- My.Forms object [Visual Basic], developing applications
- rapid application development (RAD), My.Forms
- rapid application development (RAD), My.WebServices
ms.assetid: de930027-9108-4f0c-b97c-5e7db4d6ef79
ms.openlocfilehash: 141f2f5f98499498d3c6732f7ae8d0abe6259ed9
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990239"
---
# <a name="default-object-instances-provided-by-myforms-and-mywebservices-visual-basic"></a>My.Forms および My.WebServices が提供する既定のオブジェクト インスタンス (Visual Basic)

[My.Forms](../../language-reference/objects/my-forms-object.md) オブジェクトと [My.WebServices](../../language-reference/objects/my-webservices-object.md) オブジェクトを使用すると、アプリケーションで使用されるフォーム、データ ソース、および XML Web サービスにアクセスできます。 アクセスは、各オブジェクトの "*既定のインスタンス*" のコレクションを通じて行われます。  
  
## <a name="default-instances"></a>既定のインスタンス  

 既定のインスタンスは、ランタイムによって提供されるクラスのインスタンスであり、`Dim` および `New` ステートメントを使用して宣言およびインスタンス化する必要はありません。 次の例では、`Form1` という名前の <xref:System.Windows.Forms.Form> クラスのインスタンスを宣言およびインスタンス化し、`My.Forms` を使用してこの <xref:System.Windows.Forms.Form> クラスの既定のインスタンスを取得できるようになった方法を示します。  
  
 [!code-vb[VbVbcnMy#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#5)]  
  
 [!code-vb[VbVbcnMy#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#6)]  
  
 `My.Forms` オブジェクトにより、プロジェクト内に存在するすべての `Form` クラスの既定のインスタンスのコレクションが返されます。 同様に、`My.WebServices` により、アプリケーション内で参照を作成したすべての Web サービスに対して、プロキシ クラスの既定のインスタンスが提供されます。  
  
## <a name="see-also"></a>関連項目

- [My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)
- [My.WebServices オブジェクト](../../language-reference/objects/my-webservices-object.md)
- [プロジェクトの種類に応じた My の機能](how-my-depends-on-project-type.md)
