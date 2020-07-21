---
title: セキュリティとシリアル化
description: 「セキュリティとシリアル化」を参照してください。 オブジェクトインスタンスデータを表示または変更するには、SecurityPermission を SerializationFormatter フラグを指定して使用します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, serialization
- serialization, security
- secure coding, serialization
- security [.NET Framework], serialization
ms.assetid: b921bc94-bd3a-4c91-9ede-2c8d4f78ea9a
ms.openlocfilehash: f19641ad2154631b4eab5104252c12b73b9084fd
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309275"
---
# <a name="security-and-serialization"></a>セキュリティとシリアル化

シリアル化によって、他の方法ではアクセスできないオブジェクト インスタンス データを他のコードから参照または変更できるようになるため、シリアル化を実行するコードには、特殊なアクセス許可として、 <xref:System.Security.Permissions.SecurityPermission> フラグが指定された <xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter> が必要です。 既定のポリシーでは、インターネットからダウンロードしたコードまたはイントラネット コードにはこのアクセス許可は与えられず、ローカル コンピューター上のコードにだけ付与されます。  
  
 通常、オブジェクト インスタンスのすべてのフィールドはシリアル化されます。つまり、データは、インスタンスのシリアル化されたデータで表されます。 形式を解釈できるコードでは、メンバーのアクセシビリティとは関係なく、データ値を判断できます。 同様に、逆シリアル化でもアクセシビリティ規則に関係なく、シリアル化された表現からデータを抽出し、オブジェクトの状態を直接設定します。  
  
 機密データを含む可能性のあるオブジェクトは、可能であれば、シリアル化できないようにしてください。 そのようなオブジェクトをシリアル化しなければならない場合、機密データを保持する特定のフィールドは、シリアル化できないように維持してください。 これらのフィールドをシリアル化にできない場合、機密データは、シリアル化のアクセス許可を持つすべてのコードに公開されます。 悪意のあるコードがこのアクセス許可を取得できないことを確認してください。  
  
 <xref:System.Runtime.Serialization.ISerializable> インターフェイスは、シリアル化インフラストラクチャでのみ使用するためのものです。 ただし、保護されていない場合、機密情報をリリースする可能性があります。 **ISerializable**を実装してカスタムのシリアル化を提供する場合は、必ず次の予防措置を取ってください。  
  
- <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> SerializationFormatter **アクセス許可を指定した** SecurityPermission **を要求するか、メソッドの出力で機密情報がリリースされないことを確実にして、** メソッドを明示的に保護します。 次に例を示します。  
  
    ```vb  
    Public Overrides<SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)>  _  
    Sub GetObjectData(info As SerializationInfo, context As StreamingContext)  
    End Sub  
    ```  
  
    ```csharp  
    [SecurityPermissionAttribute(SecurityAction.Demand,SerializationFormatter
    =true)]  
    public override void GetObjectData(SerializationInfo info,
    StreamingContext context)  
    {  
    }  
    ```  
  
- シリアル化に使用する特殊なコンストラクターでも徹底的な入力検証を行い、悪質なコードによる悪用を防ぐために、コンストラクターを保護するか、またはプライベートにする必要があります。 また、クラスを明示的に作成したり、ある種のファクトリで間接的に作成したりするなど、他の方法でこのようなクラスのインスタンスを取得する場合にも、同じセキュリティ チェックとアクセス許可を適用してください。  
  
## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](../../standard/security/secure-coding-guidelines.md)
