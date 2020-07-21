---
title: jitCompilationStart マネージデバッグアシスタント (MDA)
description: JitCompilationStart managed デバッグアシスタント (MDA) は、just-in-time (JIT) コンパイラが .NET 関数のコンパイルを開始したときに報告します。
ms.date: 03/30/2017
helpviewer_keywords:
- JIT compilation
- MDAs (managed debugging assistants), JIT compilation
- JitCompilationStart MDA
- managed debugging assistants (MDAs), JIT compilation
ms.assetid: 5ffd2857-d0ba-4342-9824-9ffe04ec135d
ms.openlocfilehash: 13e20c1a940b7bfa777245ba35f3cc1b003d15b2
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325538"
---
# <a name="jitcompilationstart-mda"></a>jitCompilationStart MDA

`jitCompilationStart` マネージド デバッグ アシスタント (MDA: Managed Debugging Assistant) が起動すると、Just-In-Time (JIT) コンパイラが関数のコンパイルを開始した時刻が報告されます。  
  
## <a name="symptoms"></a>現象  
 mscorjit.dll がプロセスに読み込まれるため、既にネイティブイメージ形式のプログラムでワーキングセットサイズが増加します。  
  
## <a name="cause"></a>原因  
プログラムが依存しているアセンブリがネイティブ形式で生成されていないか、アセンブリが正しく登録されていません。  

## <a name="resolution"></a>解決策  
 この MDA を有効にすると、どの関数が JIT コンパイルされているかを識別できます。 関数を含むアセンブリが、ネイティブ形式に生成され、適切に登録されていることを確認します。
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は、メソッドが JIT コンパイルされる前にメッセージをログに記録します。そのため、この MDA を有効にすると、パフォーマンスに大きな影響が出ます。 メソッドがインラインである場合、この MDA は別のメッセージを生成しません。  
  
## <a name="output"></a>出力  
 次のコード サンプルでは、サンプル出力を確認できます。 この場合、出力には、アセンブリテストで、クラス "ns2.CO" のメソッド "m" が JIT でコンパイルされたことが示されています。  
  
```output
method name="Test!ns2.C0::m"  
```  
  
## <a name="configuration"></a>構成  
 次の構成ファイルでは、最初に JIT コンパイルされたときに報告されるメソッドを絞り込むためのさまざまなフィルターを確認できます。 Name 属性の値をに設定することによって、すべてのメソッドを報告するように指定でき \* ます。  
  
```xml  
<mdaConfig>  
  <assistants>  
    <jitCompilationStart>  
      <methods>  
        <match name="C0::m" />  
        <match name="MyMethod" />  
        <match name="C2::*" />  
        <match name="ns0::*" />  
        <match name="ns1.C0::*" />  
        <match name="ns2.C0::m" />  
        <match name="ns2.C0+N0::m" />  
      </methods>  
    </jitCompilationStart >  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>例  
 次のコード サンプルは、先の構成ファイルとの併用を意図しています。  
  
```csharp
using System;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public static void Main(string[] args)  
    {  
        C0.m();  
        C1.MyMethod();  
        C2.m();  
  
        ns0.C0.m();  
        ns0.C0.N0.m();  
        ns0.C1.m();  
  
        ns1.C0.m();  
        ns1.C0.N0.m();  
  
        ns2.C0.m();  
        ns2.C0.N0.m();  
    }  
}  
  
public class C0  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
public class C1  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void MyMethod() { }  
}  
  
public class C2  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
namespace ns0  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
  
    public class C1  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
    }  
}  
  
namespace ns1  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
  
namespace ns2  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../interop/interop-marshaling.md)
