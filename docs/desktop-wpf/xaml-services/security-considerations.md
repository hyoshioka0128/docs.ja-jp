---
title: XAML セキュリティの考慮事項
ms.date: 03/30/2017
helpviewer_keywords:
- security [XAML Services], .NET XAML services
- XAML security [XAML Services]
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
ms.openlocfilehash: 1864910b339c74e3033fb4d6d8baebffada1a4f8
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432918"
---
# <a name="xaml-security-considerations"></a>XAML のセキュリティに関する考慮事項

この記事では、XAML および .NET XAML サービス API を使用する場合のアプリケーションのセキュリティに関するベスト プラクティスについて説明します。

## <a name="untrusted-xaml-in-applications"></a>アプリケーションでの信頼されていない XAML

最も一般的な意味では、信頼されていない XAML は、アプリケーションが明示的に含めなかった XAML ソースです。

信頼済みで署名されたアセンブリ内で`resx`-type リソースにコンパイルまたは格納される XAML は、本質的に信頼されていません。 アセンブリ全体を信頼できるのと同じくらい XAML を信頼できます。 ほとんどの場合、ストリームまたはその他の I/O から読み込む XAML ソースである、緩い XAML の信頼の側面にのみ関心があります。 Loose XAML は、配置およびパッケージ化インフラストラクチャを備えたアプリケーション モデルの特定のコンポーネントや機能ではありません。 ただし、アセンブリは、loose XAML の読み込みを含む動作を実装する場合があります。

信頼されていない XAML の場合は、通常、信頼されていないコードと同じように扱う必要があります。 サンドボックスまたは他のメタファを使用して、信頼できない XAML から信頼されたコードにアクセスすることを防ぎます。

XAML 機能の性質により、XAML はオブジェクトを構築し、そのプロパティを設定する権限を与えます。 これらの機能には、型コンバーターへのアクセス、アプリケーション ドメイン内のアセンブリへのマッピングとアクセス、マークアップ拡張機能、`x:Code`ブロックなどを使用する機能も含まれます。

言語レベルの機能に加えて、多くのテクノロジで UI 定義に XAML が使用されます。 信頼されていない XAML を読み込むと、悪意のあるスプーフィング UI を読み込むことがあります。

## <a name="sharing-context-between-readers-and-writers"></a>読者とライターの間でコンテキストを共有する

XAML リーダーと XAML ライターの .NET XAML サービス アーキテクチャでは、XAML リーダーを XAML ライターまたは共有 XAML スキーマ コンテキストと共有する必要がよくあります。 XAML ノード ループ ロジックを記述する場合や、カスタムの保存パスを提供する場合は、オブジェクトまたはコンテキストの共有が必要になることがあります。 信頼されたコードと信頼されていないコードの間で XAML リーダー インスタンス、既定以外の XAML スキーマ コンテキスト、または XAML リーダー/ライター クラスの設定を共有しないでください。

CLR ベースの型バッキングに対する XAML オブジェクトの書き込みに関連するほとんどのシナリオと操作では、既定の XAML スキーマ コンテキストを使用できます。 既定の XAML スキーマ コンテキストには、完全な信頼を損なう可能性のある設定が明示的に含まれていません。 したがって、信頼できる XAML リーダー/ライター コンポーネント間でコンテキストを共有しても安全です。 ただし、これを行う場合でも、このようなリーダーとライターを別々<xref:System.AppDomain>のスコープに保持し、その 1 つを特に意図/サンドボックスして部分的な信頼を得ることをお勧めします。

## <a name="xaml-namespaces-and-assembly-trust"></a>XAML 名前空間とアセンブリの信頼

XAML がアセンブリにカスタム XAML 名前空間マッピングを解釈する方法に関する基本的な非修飾構文および定義では、信頼されたアセンブリと信頼されていないアセンブリがアプリケーション ドメインに読み込まれたアセンブリと区別されません。 したがって、信頼されていないアセンブリが、信頼されたアセンブリの目的の XAML 名前空間マッピングを偽装し、XAML ソースの宣言されたオブジェクトとプロパティ情報を取得することは技術的に可能です。 この状況を回避するためのセキュリティ要件がある場合は、次のいずれかの方法を使用して、目的の XAML 名前空間マッピングを行う必要があります。

- アプリケーションの XAML で作成された XAML 名前空間マッピングでは、厳密な名前を持つ完全修飾アセンブリ名を使用します。

- XAML リーダーと XAML オブジェクト ライターに固有<xref:System.Xaml.XamlSchemaContext>のアセンブリ マッピングを構築することで、固定の参照アセンブリ セットに制限します。 [https://docs.microsoft.com/azure/active-directory/develop/scenario-protected-web-api-overview](<xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29> ) をご覧ください。

## <a name="xaml-type-mapping-and-type-system-access"></a>XAML 型マッピングと型システム アクセス

XAML は独自の型システムをサポートしており、多くの点で CLR が基本的な CLR 型システムを実装する方法とは同じです。 ただし、型の情報に基づいて型に関する信頼の決定を行う型認識の特定の側面については、CLR バッキング型の型情報に従う必要があります。 これは、XAML 型システムの特定のレポート機能の一部が仮想メソッドとして開かれたままであるため、元の .NET XAML サービスの実装の制御下に完全にはないためです。 XAML 型システムは拡張可能であり、XAML 自体の拡張性と、既定の CLR で対応する実装と既定の XAML スキーマ コンテキストに対して、その代替型マッピング戦略に対応するため、これらの拡張ポイントが存在します。 詳細については、<xref:System.Xaml.XamlType>および<xref:System.Xaml.XamlMember>のいくつかのプロパティに関する注意事項を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Xaml.Permissions.XamlAccessLevel>
