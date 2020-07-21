---
ms.openlocfilehash: 3aafb14b65f7c0f9e5d77927809547f9d4b96e1c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620370"
---
### <a name="error-codes-for-maxrequestlength-or-maxreceivedmessagesize-are-different"></a>maxRequestLength または maxReceivedMessageSize のエラー コードが異なる

#### <a name="details"></a>説明

Internet Information Services (IIS) または ASP.NET 開発サーバーでホストされており、maxRequestLength (ASP.NET の場合) または maxReceivedMessageSize (WCF の場合) を超える WCF Web サービスのメッセージに異なるエラー コードがあります。HTTP 状態コードは 400 (正しくない要求) から 413 (要求したエンティティが大きすぎます) に変更され、maxRequestLength または maxReceivedMessageSize 設定を超えるメッセージでは <xref:System.ServiceModel.ProtocolException?displayProperty=fullName> 例外がスローされます。 これには、転送モードが Streamed である場合も含まれます。

#### <a name="suggestion"></a>提案される解決策

この変更により、メッセージ長が ASP.NET または WCF で許可されている制限を超えたときのデバッグが簡単になります。HTTP 400 状態コードに基づいて処理を実行するコードはすべて変更する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
