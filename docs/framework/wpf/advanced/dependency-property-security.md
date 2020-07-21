---
title: 依存関係プロパティのセキュリティ
ms.date: 03/30/2017
helpviewer_keywords:
- wrappers [WPF], access
- wrappers [WPF], security
- dependency properties [WPF], security
- security [WPF], wrappers
- validation [WPF], dependency properties
- dependency properties [WPF], access
- security [WPF], dependency properties
ms.assetid: d10150ec-90c5-4571-8d35-84bafa2429a4
ms.openlocfilehash: f5640b348ccd68819052f58756489489371862d0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186392"
---
# <a name="dependency-property-security"></a>依存関係プロパティのセキュリティ
依存関係プロパティは、一般に、パブリック プロパティと考える必要があります。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のプロパティ システムの性質のため、依存関係プロパティの値に関してセキュリティを保証することはできません。  

<a name="AccessSecurity"></a>
## <a name="access-and-security-of-wrappers-and-dependency-properties"></a>ラッパーと依存関係プロパティのアクセスとセキュリティ  
 通常、依存関係プロパティは、インスタンスからのプロパティの取得または設定を簡素化する "ラッパー" 共通言語ランタイム (CLR) プロパティと共に実装されます。 ただし、ラッパーは実際には、依存関係プロパティとの対話時に使われる下位レベルの <xref:System.Windows.DependencyObject.GetValue%2A> および <xref:System.Windows.DependencyObject.SetValue%2A> の静的な呼び出しを実装する簡易メソッドにすぎません。 別の考え方をすれば、プロパティは、プライベート フィールドではなくたまたま依存関係プロパティが基になっている共通言語ランタイム (CLR) プロパティとして公開されます。 ラッパーに適用されるセキュリティ メカニズムでは、プロパティ システムの動作と基になっている依存関係プロパティのアクセスは並列化されません。 ラッパーにセキュリティを要求すると、簡易メソッドの使用が防がれるだけで、<xref:System.Windows.DependencyObject.GetValue%2A> または <xref:System.Windows.DependencyObject.SetValue%2A> の呼び出しを防ぐことはできません。 同様に、保護されたアクセス レベルまたはプライベート アクセス レベルをラッパーに適用しても、効果的なセキュリティは提供されません。  
  
 依存関係プロパティを独自に作成する場合は、呼び出し元がそのプロパティの真のアクセス レベルについて誤解しないように、ラッパーと <xref:System.Windows.DependencyProperty> 識別子フィールドをパブリック メンバーとして宣言する必要があります (そのストアが依存関係プロパティとして実装されているため)。  
  
 カスタム依存関係プロパティの場合は、プロパティを読み取り専用の依存関係プロパティとして登録できます。そうすることで、そのプロパティの <xref:System.Windows.DependencyPropertyKey> に対する参照を保持しないでプロパティを設定するのを防ぐ、有効な手段になります。 詳細については、「[読み取り専用の依存関係プロパティ](read-only-dependency-properties.md)」を参照してください。  
  
> [!NOTE]
> <xref:System.Windows.DependencyProperty> 識別子フィールドをプライベートとして宣言することは禁止されておらず、カスタム クラスのすぐに公開される名前空間を減らすのに役立つ場合があるかもしれませんが、次のセクションで説明するように共通言語ランタイム (CLR) 言語の定義でそのアクセス レベルが定義されているのと同じ意味で、そのようなプロパティを "プライベート" と考えるべきではありません。  
  
<a name="PropertySystemExposure"></a>
## <a name="property-system-exposure-of-dependency-properties"></a>プロパティ システムによる依存関係プロパティの公開  
 <xref:System.Windows.DependencyProperty> をパブリック以外のアクセス レベルとして宣言することは、一般に意味のないことであり、誤解を招くおそれがあります。 このようなアクセス レベルの設定は、宣言しているクラスからインスタンスへの参照を取得できるのを防ぐだけです。 しかし、特定のプロパティがクラスまたは派生クラスのインスタンスに存在することを示す手段としてプロパティ システムが <xref:System.Windows.DependencyProperty> を返すことには複数の側面があり、元の静的識別子が非パブリックと宣言されている場合であっても、この識別子を <xref:System.Windows.DependencyObject.SetValue%2A> の呼び出しで使用できます。 また、<xref:System.Windows.DependencyObject.OnPropertyChanged%2A> 仮想メソッドは、値が変化した既存の依存関係プロパティの情報を受け取ります。 さらに、<xref:System.Windows.DependencyObject.GetLocalValueEnumerator%2A> メソッドは、値がローカルに設定されたインスタンスのプロパティに対する識別子を返します。  
  
### <a name="validation-and-security"></a>検証とセキュリティ  
 <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> に対して要求を適用し、要求の失敗で検証エラーになってプロパティが設定されないことを期待するのは、適切なセキュリティ メカニズムではありません。 悪意のある呼び出し元がアプリケーション ドメイン内で動作している場合、<xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> によって適用される値設定の無効化も、そのような呼び出し元によって抑制される可能性があります。  
  
## <a name="see-also"></a>関連項目

- [カスタム依存関係プロパティ](custom-dependency-properties.md)
