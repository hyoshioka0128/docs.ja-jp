---
title: '方法: エンティティをシリアル化可能にする'
ms.date: 03/30/2017
ms.assetid: a6c5bf6e-064a-4f77-b74c-76b3a5dec309
ms.openlocfilehash: 5e9d078ed2daacfa48b09693f533e9aade613281
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002713"
---
# <a name="how-to-make-entities-serializable"></a>方法: エンティティをシリアル化可能にする
コードを作成するときに、エンティティをシリアル化可能にできます。 エンティティ クラスは <xref:System.Runtime.Serialization.DataContractAttribute> 属性で装飾し、列は <xref:System.Runtime.Serialization.DataMemberAttribute> 属性で装飾します。  
  
 Visual Studio を使用している開発者は、オブジェクト リレーショナル デザイナーをこの目的に使用できます。  
  
 SQLMetal コマンド ライン ツールを使用する場合は、`unidirectional` 引数を指定して **/serialization** オプションを使用します。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の SQLMetal コマンド ラインでは、シリアル化可能なエンティティを持つファイルが作成されます。  
  
```console  
sqlmetal /code:nwserializable.vb /language:vb "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
```console  
sqlmetal /code:nwserializable.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
## <a name="see-also"></a>関連項目

- [シリアル化](serialization.md)
- [オブジェクト モデルの作成](creating-the-object-model.md)
