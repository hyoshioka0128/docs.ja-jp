---
title: OpenType フォント パックのサンプル
ms.date: 03/30/2017
helpviewer_keywords:
- OpenType font pack [WPF]
- fonts [WPF], OpenType font pack
- typography [WPF], OpenType font pack
ms.assetid: 56b46fa1-a44e-419b-8f14-25ad51c715c3
ms.openlocfilehash: 30cb69fcf05108822e8f3e2d45c9e79dbced26ca
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181906"
---
# <a name="sample-opentype-font-pack"></a>OpenType フォント パックのサンプル
このトピックでは、Windows SDK で配布されている OpenType フォントのサンプルの概要を説明します。 サンプル フォントは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションで使用可能な拡張 OpenType 機能をサポートしています。  

<a name="overview"></a>
## <a name="fonts-in-the-opentype-font-pack"></a>OpenType フォント パックのフォント  
 Windows SDK には、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションの作成に使用できる OpenType フォント サンプルのセットが用意されています。 サンプル フォントは、Ascender Corporation のライセンスを受けて提供されています。 これらのフォントには、OpenType フォーマットで定義されている機能全体のサブセットだけが実装されています。 サンプルの OpenType フォント名の一覧を次の表に示します。  
  
|**Name**|**ファイル**|  
|--------------|--------------|  
|Kootenay|Kooten.ttf|  
|Lindsey|Linds.ttf|  
|Miramonte|Miramo.ttf|  
|Miramonte Bold|Miramob.ttf|  
|Pericles|Peric.ttf|  
|Pericles Light|Pericl.ttf|  
|Pescadero|Pesca.ttf|  
|Pescadero Bold|Pescab.ttf|  
  
 次の図は OpenType フォントのサンプルが、どのように表示されるかを示しています。  
  
 ![サンプル フォント パック内のフォント名の一覧](./media/sample-opentype-font-pack/font-names-sample-pack.gif)  
  
 サンプル フォントは、Ascender Corporation のライセンスを受けて提供されています。 Ascender は、高度なフォント製品を提供する企業です。 サンプル フォントの拡張版またはカスタム版のライセンスを受けるには、[Ascender Corporation の Web サイト](https://www.monotype.com/)を参照してください。  
  
> [!NOTE]
> アプリケーションに埋め込む、または別の方法で再頒布するフォントについて、必要なライセンス権限を取得することは、開発者であるユーザーの責任で行ってください。  
  
<a name="installing_the_fonts"></a>
## <a name="installing-the-fonts"></a>フォントのインストール  
 サンプルの OpenType フォントを、既定の Windows フォント ディレクトリである **\WINDOWS\Fonts** にインストールできます。 フォントをインストールするには、コントロール パネルの [フォント] を使用します。 これらのフォントをコンピューターにインストールすると、既定の Windows フォントを参照するすべてのアプリケーションからアクセスできるようになります。 フォント ファイルをダブルクリックして、各フォントの文字を異なるいくつかのフォント サイズで表示できます。 次のスクリーン ショットは、Lindsey フォント ファイル (Linds.ttf) を表示したものです。  
  
 ![Lindsey フォント &#40;OpenType&#41;](./media/typographyinwpf-04.png "TypographyInWPF_04")  
Lindsey フォントの表示  
  
<a name="using_the_fonts"></a>
## <a name="using-the-fonts"></a>フォントの使用  
 アプリケーションでフォントを使用するには、2 とおりの方法があります。 アセンブリ内にリソースとして埋め込まれていないプロジェクト コンテンツ項目として、フォントをアプリケーションに追加できます。 あるいは、アプリケーションのアセンブリ ファイル内に埋め込まれたプロジェクト リソース項目として、フォントをアプリケーションに追加できます。 詳細については、「[アプリケーションでのフォントのパッケージング](packaging-fonts-with-applications.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Documents.Typography>
- [OpenType フォントの機能](opentype-font-features.md)
- [アプリケーションでのフォントのパッケージング](packaging-fonts-with-applications.md)
