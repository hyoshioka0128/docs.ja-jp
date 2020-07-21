---
title: x:Property ディレクティブ
ms.date: 03/30/2017
ms.assetid: 618555a8-c893-455c-810f-ac54cd24ef10
ms.openlocfilehash: 2804ec935d0626cba9ef050f70a3266cf23bcce0
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432678"
---
# <a name="xproperty-directive"></a>x:Property ディレクティブ

マークアップで XAML プロパティを宣言します。

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<object x:Class="className">
  <x:Members>
    <x:Property Name="propertyName" Type="propertyType"/>
    additionalProperties
  </x:Members>
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`className`|XAML 運用環境のバッキング クラスまたは部分クラスの名前。|
|`propertyName`|定義されるプロパティのメンバーの名前。|
|`propertyType`|このプロパティの型を指定する型名 (またはその他の文字列の形式、フレームワーク固有)。|

## <a name="remarks"></a>解説

NET XAML サービスの実装では、. `x:Property` には直接の型のバッキングはありませんが、<xref:System.Windows.Markup.PropertyDefinition> クラスによってサポートされています。 XAML ノード ストリームでは、`x:Property` 要素は、XAML 言語の XAML 名前空間から `Property` という名前のメンバーとして表されます。 メンバー `Property` は、マークアップによって宣言された属性を保持します。

の意味`Name`と`Type`は 、.NET XAML サービス レベルでは割り当てられません。 これらは、特定のフレームワークによって課される可能性がある規則の下で後に解釈される文字列の値として、初期の XAML ノード ストリームに格納されます。 意味は、実装によって、XAML の名前および XAML 型の意味と揃えるか、バッキング型のシステムでのみ有効になることがあります。

マークアップでメンバーの定義を指定する手段として `x:Members` の実用的な使用法をサポートするため、メンバーを変更可能なクラスに関連付ける必要があります。 目的とするモデルは、`x:Members` が `x:Class` を指定する型のメンバーとして存在することです。 ただし、型とメンバーを関連付けたり、動的メンバー定義を生成するためのメカニズムは、.NET XAML サービス レベルではサポートされていません。 これは、XAML のメンバーの定義をサポートするアプリケーション モデルがある個々のフレームワークに残されています。 一般に、XAML をマークアップ コンパイルするとともに、XAML と分離コードの統合または純粋な XAML からのアセンブリの生成を行う MSBUILD のビルド操作が、この機能をサポートするために必要です。

## <a name="xproperty-for-windows-workflow-foundation"></a>Windows Workflow Foundation の x:Property

Windows Workflow Foundation では、 `x:Property` は、全体が XAML で構成されるカスタム アクティビティのメンバーや、分離コードを含むアクティビティ デザイナーの XAML で定義された動的メンバーを定義します。 `x:Class` は、XAML の運用環境のルート要素にも指定する必要があります。 これは .NET XAML サービス レベルでは必須ではありませんが、カスタム アクティビティと Windows ワークフローファウンデーション XAML 全般をサポートする MSBUILD ビルド アクションによって XAML の運用環境が読み込まれる場合に必要になります。 Windows ワークフロー ファンデーションは、`x:Property``Type`純粋な XAML 型名を属性の目的の値として使用せず、ここでは説明していない規則を使用します。 詳細については、「[動的アクティビティの作成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd807392(v=vs.100))」を参照してください。
