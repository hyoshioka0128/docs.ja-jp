---
ms.openlocfilehash: 2d0798917b639bc90bf3f78f6fb9f19d0eaf2c71
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614821"
---
### <a name="incorrect-implementation-of-memberdescriptorequals"></a>MemberDescriptor.Equals の不適切な実装

#### <a name="details"></a>説明

<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> メソッドの元の実装によって、比較対象のオブジェクトからの 2 つの異なる文字列プロパティである、カテゴリ名と説明文字列が比較されます。 この修正は、最初のオブジェクトの <xref:System.ComponentModel.MemberDescriptor.Category> と 2 番目のオブジェクトの <xref:System.ComponentModel.MemberDescriptor.Category> を比較し、最初のオブジェクトの <xref:System.ComponentModel.MemberDescriptor.Description> と 2 番目のオブジェクトの <xref:System.ComponentModel.MemberDescriptor.Description> を比較するものです。

#### <a name="suggestion"></a>提案される解決策

記述子が等しいときに `false` を返すことがある <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> にアプリケーションが依存しているとき、.NET Framework のバージョン 4.6.2 以降を対象とする場合、いくつかの選択肢があります。

- コードを変更し、<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> メソッドの呼び出しに加え、<xref:System.ComponentModel.MemberDescriptor.Category> フィールドと <xref:System.ComponentModel.MemberDescriptor.Description> フィールドを手動で比較します。
- app.config ファイルに次の値を追加し、この変更を無効にします。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true" />
</runtime>
```

アプリケーションの対象が .NET Framework 4.6.1 以前であるが .NET Framework 4.6.2 以降で実行しているとき、この変更を有効にする場合、app.config ファイルに次の値を追加することで互換性スイッチを `false` に設定します。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.ComponentModel.MemberDescriptor.Equals(System.Object)?displayProperty=nameWithType>
