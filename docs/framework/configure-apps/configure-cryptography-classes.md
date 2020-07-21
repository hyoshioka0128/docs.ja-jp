---
title: 暗号化クラスの設定
description: コンピューター管理者が、.NET とアプリケーションで使用する既定の暗号化アルゴリズムとアルゴリズムの実装を構成する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- configuration files [.NET Framework], cryptography
- cryptographic algorithms
- security [.NET Framework], encryption
- cryptography, classes
- .NET Framework application configuration, cryptography
- default cryptography
ms.assetid: eee3ccb8-2c0d-4f35-b38d-6892a46c14e5
ms.openlocfilehash: 5d12aae31ec78f80bea7df1bb0f37ac78dc37de2
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85105066"
---
# <a name="configuring-cryptography-classes"></a>暗号化クラスの設定
Windows SDK を使用すると、コンピューター管理者は、.NET Framework および適切に記述されたアプリケーションで使用される既定の暗号化アルゴリズムおよびアルゴリズムの実装を構成できます。  たとえば、暗号化アルゴリズムを独自に実装する企業は、Windows SDK に付属する実装ではなく、その実装を既定値にすることができます。 暗号化を使用するマネージアプリケーションは、常に特定の実装に明示的にバインドすることができますが、暗号化の構成システムを使用して暗号化オブジェクトを作成することをお勧めします。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [暗号化クラスへのアルゴリズム名の割り当て](map-algorithm-names-to-cryptography-classes.md)  
 アルゴリズム名を暗号クラスにマップする方法について説明します。  
  
 [暗号化アルゴリズムへのオブジェクト ID の割り当て](map-object-identifiers-to-cryptography-algorithms.md)  
 オブジェクト識別子を暗号アルゴリズムにマップする方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [Cryptographic Services](../../standard/security/cryptographic-services.md)  
 Windows SDK によって提供される暗号化サービスの概要について説明します。  
  
 [暗号設定スキーマ](./file-schema/cryptography/index.md)  
 アルゴリズムの表示名を、暗号化アルゴリズムを実装するクラスに割り当てる要素について説明します。
