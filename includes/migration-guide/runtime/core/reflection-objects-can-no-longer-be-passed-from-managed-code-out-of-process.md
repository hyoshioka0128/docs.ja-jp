---
ms.openlocfilehash: a54b17b2002bd0f85b8b47c5e37e040470d6c494
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621332"
---
### <a name="reflection-objects-can-no-longer-be-passed-from-managed-code-to-out-of-process-dcom-clients"></a>リフレクション オブジェクトが、マネージド コードからアウト プロセス DCOM クライアントに渡されなくなった

#### <a name="details"></a>説明

リフレクション オブジェクトはマネージド コードからアウト プロセス DCOM クライアントに渡されなくなりました。 影響を受ける型は次のとおりです。<ul><li><xref:System.Reflection.Assembly?displayProperty=fullName></li><li><xref:System.Reflection.MemberInfo?displayProperty=fullName> (およびその派生型、<xref:System.Reflection.FieldInfo?displayProperty=fullName>、<xref:System.Reflection.MethodInfo?displayProperty=fullName>、<xref:System.Type?displayProperty=fullName>、<xref:System.Reflection.TypeInfo?displayProperty=fullName> など)</li><li><xref:System.Reflection.MethodBody?displayProperty=fullName></li><li><xref:System.Reflection.Module?displayProperty=fullName></li><li>[https://login.microsoftonline.com/consumers/](<xref:System.Reflection.ParameterInfo?displayProperty=fullName>)</li></ul>オブジェクトの <code>IMarshal</code> の呼び出しは <code>E_NOINTERFACE</code> を返します。

#### <a name="suggestion"></a>提案される解決策

非リフレクション オブジェクトで動作するように、マーシャリング コードを更新します。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6|
|種類|ランタイム|
