---
title: x:Members ディレクティブ
ms.date: 03/30/2017
ms.assetid: 155b393d-3b49-4c5a-8c9e-b3d9893af4e4
ms.openlocfilehash: c751a4f1cdea8dce7ef5165f5225ab3a825c7344
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432726"
---
# <a name="xmembers-directive"></a>x:Members ディレクティブ
親要素の x:Class に適用される、マークアップで定義されたメンバーのセットを保持します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Class="className">
<x:Members>
  oneOrMoreMembers
</x:Members
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`className`|XAML 運用環境のバッキング クラスまたは部分クラスの名前。 「解説」を参照してください。|
|`oneOrMoreMembers`|メンバ定義を表す 1 つ以上のオブジェクト要素。 通常、これらはオブジェクト`x:Property`要素です。 「解説」を参照してください。|

## <a name="remarks"></a>解説

NET XAML サービスの実装では、バッキング クラスや基になるメンバー`x:Members`の実装はありません。 `x:Members`は、任意の型のメンバーとして存在できる特殊な XAML メンバーです。 XAML ノード ストリームでは`x:Members`、XAML 言語 XAML`Members`名前空間からという名前のメンバーとして表されます。 メンバー`Members`には、オブジェクトの読み取り専用`Member`の汎用リストが含まれています。 一般的なマークアップでは、個々のメンバ`x:Property`はプロパティ要素として指定されます。 `x:Property`は、型のプロパティに特化したより正確な型であり、`x:Member`に割り当て可能です。 詳細については、「 [x: プロパティ ディレクティブ](xproperty-directive.md)」を参照してください。

マークアップでメンバーの定義を指定する手段として `x:Members` の実用的な使用法をサポートするため、メンバーを変更可能なクラスに関連付ける必要があります。 目的とするモデルは、`x:Members` が `x:Class` を指定する型のメンバーとして存在することです。 ただし、型とメンバーを関連付けたり、動的メンバー定義を生成するためのメカニズムは、.NET XAML サービス レベルではサポートされていません。 これは、XAML のメンバーの定義をサポートするアプリケーション モデルがある個々のフレームワークに残されています。 一般に、XAML をマークアップ コンパイルするとともに、XAML と分離コードの統合または純粋な XAML からのアセンブリの生成を行う MSBUILD のビルド操作が、この機能をサポートするために必要です。

## <a name="xmembers-for-windows-workflow-foundation"></a>x:Windows ワークフローファウンデーションのメンバー

Windows ワークフロー ファン`x:Members`デーションの場合、XAML で完全に構成されたカスタム アクティビティのメンバー、または分離コードを持つアクティビティ デザイナーの XAML 定義動的メンバーが含まれます。 `x:Class` は、XAML の運用環境のルート要素にも指定する必要があります。 これは .NET XAML サービス レベルでは必須ではありませんが、カスタム アクティビティと Windows ワークフローファウンデーション XAML 全般をサポートする MSBUILD ビルド アクションによって XAML の運用環境が読み込まれる場合に必要になります。 `x:Members`は、`x:Class`を宣言するオブジェクト要素のマークアップ内の最初の子要素である必要があります。
