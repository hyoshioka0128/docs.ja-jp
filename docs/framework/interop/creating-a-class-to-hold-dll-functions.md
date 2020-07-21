---
title: DLL 関数を保持するクラスの作成
description: .NET で DLL 関数を保持するマネージド クラス ラッパーを作成します。これにより、プラットフォームの機能をカプセル化できます。
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, creating class for functions
- DLL functions
ms.assetid: e08e4c34-0223-45f7-aa55-a3d8dd979b0f
ms.openlocfilehash: b8aa0361ee5213cb947a102f903d1a7a35331f17
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622173"
---
# <a name="creating-a-class-to-hold-dll-functions"></a>DLL 関数を保持するクラスの作成
マネージド クラス内の頻繁に使用される DLL 関数をラップすることは、プラットフォームの機能をカプセル化するための効果的な方法です。 これはすべてのケースで必須であるわけではありませんが、DLL 関数の定義には手間がかかり、エラーが発生しやすくなるため、クラス ラッパーを用意しておくと便利です。 Visual Basic や C# でプログラミングしている場合は、DLL 関数をクラスまたは Visual Basic モジュール内で宣言する必要があります。  
  
 クラス内では、呼び出す DLL 関数ごとに静的メソッドを定義します。 この定義には、メソッド引数を渡すときに使用される呼び出し規則や文字セットなどの追加情報を含めることができます。この情報を省略すると、既定の設定が選択されます。 宣言のオプションと、既定の設定の完全なリストについては、「[Creating Prototypes in Managed Code](creating-prototypes-in-managed-code.md)」(マネージド コードでのプロトタイプの作成) を参照してください。  
  
 ラッピングが完了すると、他のクラスで静的メソッドを呼び出す場合と同じように、クラスでメソッドを呼び出すことができます。 プラットフォーム呼び出しでは、基になるエクスポートされた関数が自動的に処理されます。  
  
 プラットフォーム呼び出しのためにマネージド クラスをデザインする場合は、クラスと DLL 関数との関係を考慮してください。 たとえば、次のように操作できます。  
  
- 既存のクラス内で DLL 関数を宣言する。  
  
- 関数を分離し、検索しやすくするために、DLL 関数ごとに別のクラスを作成する。  
  
- 論理的なグループを形成し、オーバーヘッドを減らすため、一連の関連する DLL 関数に対して 1 つのクラスを作成する。  
  
 クラスおよびそのメソッドには、任意の名前を付けることができます。 プラットフォーム呼び出しで使用する .NET ベースの宣言を作成する方法を示す例については、「[プラットフォーム呼び出しによるデータのマーシャリング](marshaling-data-with-platform-invoke.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [アンマネージ DLL 関数の処理](consuming-unmanaged-dll-functions.md)
- [DLL 内の関数の識別](identifying-functions-in-dlls.md)
- [マネージド コードでのプロトタイプの作成](creating-prototypes-in-managed-code.md)
- [DLL 関数の呼び出し](calling-a-dll-function.md)
