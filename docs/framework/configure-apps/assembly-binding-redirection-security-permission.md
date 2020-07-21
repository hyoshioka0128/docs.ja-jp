---
title: アセンブリ バインディング リダイレクトのセキュリティ アクセス許可
description: .NET のアプリケーション構成ファイルで、明示的なアセンブリバインドリダイレクトに必要なセキュリティアクセス許可について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, assembly binding redirection
- assemblies [.NET Framework], binding redirection
ms.assetid: 24a5cdff-7ed9-4195-93f3-edf6899019fc
ms.openlocfilehash: a8596bcac4efb0aea07efcfde6726d8bbf148c24
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85105091"
---
# <a name="assembly-binding-redirection-security-permission"></a>アセンブリ バインディング リダイレクトのセキュリティ アクセス許可
アプリケーション構成ファイルで明示的にアセンブリ バインディングをリダイレクトするには、セキュリティ アクセス許可が必要です。 これは、.NET Framework アセンブリおよびサードパーティ製アセンブリに適用されます。 権限は、にフラグを設定することによって付与され <xref:System.Security.Permissions.SecurityPermissionFlag> <xref:System.Security.Permissions.SecurityPermission> ます。 マネージアセンブリには、既定ではアクセス許可がありません。  
  
 セキュリティアクセス許可は、信頼済みゾーン (ローカルコンピューター) およびイントラネットゾーンで実行されているアプリケーションに付与されます。 インターネットゾーンで実行されているアプリケーションは、アセンブリバインディングのリダイレクトを実行できません。  
  
 アセンブリのリダイレクトが、コンポーネントの発行者によって制御される発行者ポリシーファイル、または管理者によって制御されるコンピューター構成ファイルで実行される場合、このアクセス許可は必要ありません。 ただし、アプリケーションでアプリケーション構成ファイルの要素を使用して発行者ポリシーを明示的に無視するには、アプリケーションのアクセス許可が必要です [\<publisherPolicy apply="no"/>](./file-schema/runtime/publisherpolicy-element.md) 。  
  
 次の表は、 **bindingredirects**フラグの既定のセキュリティ設定を示しています。  
  
|ゾーン|BindingRedirects フラグの設定|  
|----------|-----------------------------------|  
|信頼済みゾーン (ローカルコンピューター)|**ON**|  
|イントラネット ゾーン|**ON**|  
|インターネット ゾーン|**OFF**|  
|信頼されていないゾーン|**OFF**|  
  
 管理者は、これらのセキュリティ設定を変更して、特定のコンピューター上の特定のシナリオをサポートまたは制限することができます。 既定値から**Bindingredirects**フラグ設定を変更するためのツールはありません。管理者は、ユーザーのコンピューターの Security.config ファイルを手動で編集する必要があります。  
  
## <a name="see-also"></a>関連項目

- [発行者ポリシー ファイルと side-by-side 実行](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/06d2bae3(v=vs.100))
- [方法: 自動バインディング リダイレクトを有効/無効にする](how-to-enable-and-disable-automatic-binding-redirection.md)
- [Side-by-side 実行](../deployment/side-by-side-execution.md)
