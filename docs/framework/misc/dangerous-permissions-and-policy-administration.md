---
title: 危険なアクセス許可とポリシー管理
description: 「.NET でのさまざまな危険なアクセス許可へのリンク」を参照してください。 これらのアクセス許可は、信頼できるコードにのみ付与し、必要な場合にのみ指定する必要があります。
ms.date: 03/30/2017
helpviewer_keywords:
- permissions [.NET Framework], policy administration
- security [.NET Framework], dangerous permissions
- code security, dangerous permissions
- secure coding, dangerous permissions
- permissions [.NET Framework], dangerous
ms.assetid: 1929e854-23a0-4bb1-94be-e8aa3b609e32
ms.openlocfilehash: ba3d47dc445e4b368f57d59d735fc331f5d6de81
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281616"
---
# <a name="dangerous-permissions-and-policy-administration"></a>危険なアクセス許可とポリシー管理
.NET Framework がアクセス許可を提供する保護された操作のいくつかで、セキュリティ システムが回避されてしまう可能性があります。 これらの危険なアクセス許可は信頼できるコードにのみ付与し、その付与は必要な場合に限る必要があります。 これらのアクセス許可が付与されると、通常、悪意のあるコードに対する防御策はありません。  
  
> [!NOTE]
> .NET Framework 4 では、.NET Framework セキュリティモデルと用語に重要な変更が加えられています。 これらの変更の詳細については、「[セキュリティの変更](https://docs.microsoft.com/previous-versions/dotnet/framework/security/security-changes)」を参照してください。  
  
 危険なアクセス許可については、次の表で説明します。  
  
|権限|潜在的なリスク|  
|----------------|--------------------|  
|<xref:System.Security.Permissions.SecurityPermission>||  
|<xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode>|マネージド コードからアンマネージド コードを呼び出せるようにしますが、これは大抵リスクを伴います。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SkipVerification>|検証なしで、コードは何でも実行できます。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlEvidence>|無効な証拠でセキュリティ ポリシーをかいくぐることができます。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPolicy>|セキュリティ ポリシーを変更する機能によって、セキュリティを無効にできます。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter>|シリアル化を使用して、ユーザー補助機能のメカニズムを回避できます。 詳細については、「 [セキュリティとシリアル化](security-and-serialization.md)」を参照してください。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPrincipal>|現行プリンシパルを設定する機能によって、ロール ベースのセキュリティを欺くことができます。|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlThread>|スレッドにはセキュリティ状態が関連付けられているため、スレッドの操作は危険です。|  
|<xref:System.Security.Permissions.ReflectionPermission>||  
|<xref:System.MemberAccessException>|プライベート メンバーを使用して、ユーザー補助機能のメカニズムを無効にすることができます。|  
  
## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](../../standard/security/secure-coding-guidelines.md)
