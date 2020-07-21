---
title: Azure Active Directory
description: Azure 向けのクラウドネイティブ .NET アプリの設計 |Azure Active Directory
ms.date: 06/30/2019
ms.openlocfilehash: 03f5ea8e84bc3c4a2a88a63d4b109aabf0c64f36
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614280"
---
# <a name="azure-active-directory"></a>Azure Active Directory

Microsoft Azure Active Directory (Azure AD) は、id およびアクセス管理をサービスとして提供します。 お客様は、ユーザーの所有者、情報の保存先、その情報にアクセスできるユーザー、その情報を管理できるユーザー、およびアプリにアクセスできる対象を構成および管理するために使用します。 AAD は、シングルサインオン (SSO) エクスペリエンスを提供して、ユーザーを使用するように構成されたアプリケーションに対してユーザーを認証できます。 独自に使用することも、オンプレミスで実行されている Windows AD と統合することもできます。

Azure AD はクラウド用に構築されています。 これは、LDAP を使用する Windows AD とは異なり、REST ベースの Graph API とクエリに OData 構文を使用するクラウドネイティブの id ソリューションです。 オンプレミス Active Directory では、Id 同期サービスを使用してユーザー属性をクラウドに同期させることができます。これにより、Azure AD を使用して、すべての認証をクラウドで行うことができます。 または、オンプレミスの Windows AD によって実行される ADFS 経由でローカル Active Directory に渡すために、Connect を使用して認証を構成することもできます。

Azure AD は、オンプレミスでホストされているアプリケーションに SSO を提供するために使用される会社ブランドのサインイン画面、マルチファクトリ認証、およびクラウドベースのアプリケーションプロキシをサポートしています。 さまざまな種類のセキュリティレポートとアラート機能を提供します。

## <a name="references"></a>References

- [Microsoft ID プラットフォーム](https://docs.microsoft.com/azure/active-directory/develop/)

>[!div class="step-by-step"]
>[前へ](authentication-authorization.md)
>[次へ](identity-server.md)
