---
title: 'x:Code 組み込み XAML 型 '
ms.date: 03/30/2017
f1_keywords:
- Code
- x:Code
- xCode
helpviewer_keywords:
- Code directive in XAML [XAML Services]
- x:Code XAML directive element [XAML Services]
- XAML [XAML Services], x:Code directive element
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
ms.openlocfilehash: 4da72ed630c1df001e3fd6c7e55f866b94c4d9b1
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432804"
---
# <a name="xcode-intrinsic-xaml-type"></a>x:Code 組み込み XAML 型 
XAML 運用環境内でコードを配置できます。 このようなコードは、XAML をコンパイルする任意の XAML プロセッサ実装によってコンパイルすることも、ランタイムによる解釈など、後で使用するために XAML の運用環境に残してコンパイルすることもできます。

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xaml
<x:Code>
   // code instructions, usually enclosed by CDATA...
</x:Code>
```

## <a name="remarks"></a>解説

XAML ディレクティブ要素`x:Code`内のコードは、一般的な XML 名前空間と提供される XAML 名前空間内で解釈されます。 したがって、通常は、セグメント内で使用されるコードを`x:Code`囲む必要`CDATA`があります。

`x:Code`XAML の運用環境で可能なすべての展開メカニズムに対して許可されていません。 特定のフレームワーク (たとえば、WPF) では、コードをコンパイルする必要があります。 他のフレームワークでは、`x:Code`一般的に使用が許可されない場合があります。

マネージ`x:Code`コンテンツを許可するフレームワークでは、`x:Code`コンテンツに使用する適切な言語コンパイラは、アプリケーションのコンパイルに使用される、含まれているプロジェクトの設定とターゲットによって決定されます。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

WPF`x:Code`で宣言されたコードには、次のようないくつかの特大な制限があります。

- ディレクティブ`x:Code`要素は、XAML の運用環境のルート要素の直接の子要素である必要があります。

- [x:クラスディレクティブ](xclass-directive.md)は、親ルート要素に指定する必要があります。

- 内に`x:Code`配置されたコードは、その XAML ページに対して既に作成されている部分クラスのスコープ内に収まるように、コンパイルによって処理されます。 したがって、定義するすべてのコードは、その部分クラスのメンバーまたは変数である必要があります。

- 部分クラス内にクラスを入れ子にする以外に、追加のクラスを定義することはできません (入れ子は許可されますが、入れ子になったクラスは XAML では参照できないため、通常は使用できません)。 既存の部分クラスに使用される名前空間以外の CLR 名前空間を定義または追加することはできません。

- 部分クラス CLR 名前空間の外部にあるコード エンティティへの参照はすべて完全修飾されている必要があります。 宣言されるメンバーが部分クラスオーバーライド可能なメンバーのオーバーライドである場合は、言語固有の override キーワードを使用して指定する必要があります。 スコープで宣言された`x:Code`メンバーが XAML から作成された部分クラスのメンバーと競合する場合、コンパイラが競合を報告するような方法で、XAML ファイルをコンパイルまたは読み込むことができません。

## <a name="see-also"></a>関連項目

- [x:Class ディレクティブ](xclass-directive.md)
- [WPF における分離コードと XAML](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
