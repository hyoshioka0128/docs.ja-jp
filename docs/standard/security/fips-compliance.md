---
title: FIPS 準拠-.NET Core
description: .NET Core Federal Information Processing Standards (FIPS) 準拠について説明します。
ms.date: 11/20/2019
author: Rick-Anderson
ms.author: riande
ms.openlocfilehash: cf640c857e79ae811dd38d57a0e5301b7bc96572
ms.sourcegitcommit: 81ad1f09b93f3b3e6706a7f2e4ddf50ef229ea3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74205078"
---
# <a name="net-core-federal-information-processing-standard-fips-compliance"></a>.NET Core Federal Information Processing Standards (FIPS) 準拠

Federal Information Processing Standards (FIPS) 公開140-2 は、情報技術製品の暗号化モジュールに最低限必要なセキュリティ要件を規定する米国政府の標準です。詳細については、「」のセクション5131で定義されています。1996のテクノロジ管理の改善。

.NET Core:

* は、基になるオペレーティングシステムが提供する標準モジュールに暗号化プリミティブの呼び出しを渡します。
* では、.NET Core アプリで FIPS 承認アルゴリズムまたはキーサイズを使用することは強制**されません**。

システム管理者は、オペレーティングシステムの FIPS 準拠を構成する役割を担います。

コードが FIPS 準拠環境用に記述されている場合、開発者は準拠していない FIPS アルゴリズムが使用されていないことを確認する責任があります。

FIPS 準拠の詳細については、次の記事を参照してください。

* [Windows FIPS 準拠](/windows/security/threat-protection/fips-140-validation)
* [FIPS 準拠のための Windows の構成](/windows/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing)
* [10.2. 連邦情報処理標準 (FIPS)](https://access.redhat.com/documentation/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-federal_standards_and_regulations-federal_information_processing_standard)
