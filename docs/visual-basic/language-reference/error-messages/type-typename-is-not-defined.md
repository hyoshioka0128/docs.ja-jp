---
title: 型 '<typename>' が定義されていません。
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: 89e2d1d18b456c96f62d6b9ee1dd8dc9d41bf665
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84386933"
---
# <a name="type-typename-is-not-defined"></a>型 '\<typename>' が定義されていません。
ステートメントで、定義されていない型の参照が行われました。 `Enum`、`Structure`、`Class`、`Interface` などの宣言ステートメントで型を定義できます。  
  
 **エラー ID:** BC30002  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 型定義とその参照の両方で同じスペルが使用されていることを確認します。  
  
- 参照から型定義にアクセスできることを確認してください。 たとえば、型が別のモジュールにあり、`Private` と宣言されている場合は、型定義を参照元のモジュールに移動するか、それを `Public` と宣言します。  
  
- 型の名前空間がプロジェクト内で再定義されていないことを確認します。 その場合は、`Global` キーワードを使用して、型名を完全修飾します。 たとえば、プロジェクトで `System` という名前の名前空間を定義している場合、`Global` キーワード: `Global.System.Object` で完全修飾していない限り、<xref:System.Object?displayProperty=nameWithType> 型にアクセスできません。  
  
- 型が定義されていても、それが定義されているオブジェクト ライブラリまたはタイプ ライブラリが Visual Basic に登録されていない場合は、 **[プロジェクト]** メニューの **[参照の追加]** クリックし、該当するオブジェクト ライブラリまたはタイプ ライブラリを選択します。  
  
- 型が、対象の .NET Framework プロファイルの一部であるアセンブリに含まれていることを確認してください。 詳細については、「[.NET Framework を対象とするエラーのトラブルシューティング](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)
- [Enum ステートメント](../statements/enum-statement.md)
- [Structure ステートメント](../statements/structure-statement.md)
- [Class ステートメント](../statements/class-statement.md)
- [Interface ステートメント](../statements/interface-statement.md)
- [プロジェクト内の参照の管理](/visualstudio/ide/managing-references-in-a-project)
