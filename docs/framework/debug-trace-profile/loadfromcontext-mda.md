---
title: loadFromContext MDA
description: .NET の loadFromContext マネージデバッグアシスタント (MDA) について説明します。これは、アセンブリが LoadFrom コンテキストに読み込まれた場合にアクティブ化されます。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), LoadFrom context
- managed debugging assistants (MDAs), LoadFrom context
- LoadFrom context
- LoadFromContext MDA
ms.assetid: a9b14db1-d3a9-4150-a767-dcf3aea0071a
ms.openlocfilehash: 8d55268f2b2106dde4e488a6f0271fd3b17349da
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051650"
---
# <a name="loadfromcontext-mda"></a>loadFromContext MDA
アセンブリが `LoadFrom` コンテキストに読み込まれると、`loadFromContext` マネージド デバッグ アシスタント (MDA) がアクティブになります。 このような状況は、<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> または他の同様のメソッドを呼び出した結果として発生する可能性があります。  
  
## <a name="symptoms"></a>現象  
 一部のローダー メソッドは、使用すると、`LoadFrom` コンテキストでアセンブリが呼び出される結果になる可能性があります。 このコンテキストを使用すると、シリアル化、キャスティング、依存関係の解決について予期しない結果になる可能性があります。 一般的に、このような問題を回避するために、アセンブリを `Load` コンテキストに読み込むことをお勧めします。 この MDA を使用せずに、アセンブリが読み込まれたコンテキストを判断することは困難です。  
  
## <a name="cause"></a>原因  
 一般的に、アセンブリは `Load` コンテキスト以外のパス (グローバル アセンブリ キャッシュや <xref:System.AppDomainSetup.ApplicationBase%2A?displayProperty=nameWithType> プロパティなど) から読み込まれた場合、`LoadFrom` コンテキストに読み込まれていました。  
  
## <a name="resolution"></a>解決方法  
 <xref:System.Reflection.Assembly.LoadFrom%2A> の呼び出しが不要になるようにアプリケーションを構成します。 そのためには、次の手法を使用できます。  
  
- グローバル アセンブリ キャッシュにアセンブリをインストールします。  
  
- アセンブリを <xref:System.AppDomain> の <xref:System.AppDomainSetup.ApplicationBase%2A> ディレクトリに配置します。 既定のドメインの場合、<xref:System.AppDomainSetup.ApplicationBase%2A> ディレクトリは、プロセスを開始した実行可能ファイルを含むディレクトリです。 また、アセンブリを移動したくない場合は、必要に応じて新しい <xref:System.AppDomain> を作成します。  
  
- 依存するアセンブリが、実行可能ファイルの相対的な子ディレクトリ内にある場合、アプリケーション構成 (.config) ファイルまたはセカンダリ アプリケーション ドメインのプローブ パスを追加します。  
  
 いずれの場合でも、<xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> メソッドを使用するようにコードを変更できます。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 MDA は、CLR にまったく影響がありません。 MDA では、読み込み要求の結果として使用されたコンテキストが報告されます。  
  
## <a name="output"></a>出力  
 MDA では、アセンブリが `LoadFrom` コンテキストに読み込まれたことが報告されます。 また、アセンブリの簡易名とパスが指定されます。 `LoadFrom` コンテキストの使用を回避する軽減策も提案されます。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <loadFromContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>例  
 次のコードの例は、この MDA がアクティブ化されることのある状況を示しています。  
  
```csharp
using System.Reflection;  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // The following call caused the LoadFrom context to be used  
            // because the assembly is loaded using LoadFrom and the path is
            // located outside of the Load context probing path.
            Assembly.LoadFrom(@"C:\Text\Test.dll");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
