---
title: 型 '<typename1>' の値を '<typename2>' に変換できません。
ms.date: 07/20/2015
f1_keywords:
- vbc30955
- bc30955
helpviewer_keywords:
- BC30955
ms.assetid: 966b61eb-441e-48b0-bedf-ca95384ecb8b
ms.openlocfilehash: f6b35efbc445887c537b94dd299b317a28e5f689
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406561"
---
# <a name="value-of-type-typename1-cannot-be-converted-to-typename2"></a>型 '\<typename1>' の値を '\<typename2>' に変換できません。
型 '\<typename1>' の値を '\<typename2>' に変換できません。 ファイル参照とアセンブリ '\<assemblyname>' へのプロジェクト参照との混在により、型の不一致が生じた可能性があります。 プロジェクト '\<projectname1>' の '\<filepath>' へのファイル参照を '\<projectname2>' へのプロジェクト参照で置き換えてください。  
  
 プロジェクトがプロジェクト参照とファイル参照の両方を行う場合、コンパイラは、1 つの型を別の型に変換できることを保証できません。  
  
 次の擬似コードは、このエラーを生成する可能性がある状況を示しています。  
  
 `' ================ Visual Basic project P1 ================`  
  
 `'        P1 makes a PROJECT REFERENCE to project P2`  
  
 `'        and a FILE REFERENCE to project P3.`  
  
 `Public commonObject As P3.commonClass`  
  
 `commonObject = P2.getCommonClass()`  
  
 `' ================ Visual Basic project P2 ================`  
  
 `'        P2 makes a PROJECT REFERENCE to project P3`  
  
 `Public Function getCommonClass() As P3.commonClass`  
  
 `Return New P3.commonClass`  
  
 `End Function`  
  
 `' ================ Visual Basic project P3 ================`  
  
 `Public Class commonClass`  
  
 `End Class`  
  
 プロジェクト `P1` は、プロジェクト `P2` からプロジェクト `P3` への間接プロジェクト参照と、`P3` への直接ファイル参照を行います。 `commonObject` の宣言は `P3` へのファイル参照を使用しますが、`P2.getCommonClass` の呼び出しは `P3` へのプロジェクト参照を使用します。  
  
 この場合の問題は、ファイル参照が `P3` (通常は p3.dll) の出力ファイルのファイル パスと名前を指定する一方、プロジェクト参照はプロジェクト名でソース プロジェクト (`P3`) を識別することです。 このため、コンパイラは、型 `P3.commonClass` が 2 つの異なる参照を使用した同じソース コードからのものであることを保証できません。  
  
 この状況は通常、プロジェクト参照とファイル参照が混在している場合に発生します。 前の図の、`P1` でファイル参照ではなく `P3` への直接プロジェクト参照が行われた場合、この問題は発生しません。  
  
 **エラー ID:** BC30955  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ファイル参照をプロジェクト参照に変更します。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における型変換](../../programming-guide/language-features/data-types/type-conversions.md)
- [プロジェクト内の参照の管理](/visualstudio/ide/managing-references-in-a-project)
