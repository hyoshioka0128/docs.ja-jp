---
title: '方法: アプリケーション ドメインをアンロードする'
description: 指定されたアプリケーション ドメインを適切にシャットダウンするために AppDomain.Unload メソッドを使用して .NET のアプリケーション ドメインをアンロードする方法について確認します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Unload method
- application domains, unloading
- unloading application domains
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
ms.openlocfilehash: b64a9553f63aa4a8deb57f23a97fa464edd64fee
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104672"
---
# <a name="how-to-unload-an-application-domain"></a>方法: アプリケーション ドメインをアンロードする
アプリケーション ドメインの使用が完了したら、<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> メソッドを使用してアプリケーション ドメインをアンロードします。 **Unload** メソッドは、指定したアプリケーション ドメインを正常にシャットダウンします。 アンロード プロセス中は、新たなスレッドがアプリケーション ドメインにアクセスすることはできません。また、アプリケーション ドメイン固有のデータ構造はすべて解放されます。  
  
 アプリケーション ドメインに読み込まれたアセンブリは、削除され、以後は使用できません。 アプリケーション ドメイン内のアセンブリが、ドメインに中立である場合、アセンブリのデータは、プロセス全体がシャットダウンされるまでメモリに残ります。 プロセス全体をシャットダウンする以外に、ドメインに中立なアセンブリをアンロードする機構はありません。 アプリケーション ドメインのアンロード要求が機能しない場合は、<xref:System.CannotUnloadAppDomainException> が生成されます。  
  
 次の例では、`MyDomain` という新しいアプリケーション ドメインを作成し、情報をコンソールに出力してから、アプリケーション ドメインをアンロードします。 このコードは、アンロードされたアプリケーション ドメインのフレンドリ名をコンソールに出力しようとすることに注意してください。 このアクションでは、例外が生成されます。この例外は、プログラムの最後の try ステートメントまたは catch ステートメントで処理されます。  
  
## <a name="example"></a>例  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)]
 [!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)]
 [!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [アプリケーション ドメインを使用したプログラミング](application-domains.md#programming-with-application-domains)
- [方法: アプリケーション ドメインを作成する](how-to-create-an-application-domain.md)
- [アプリケーション ドメインの使用](use.md)
