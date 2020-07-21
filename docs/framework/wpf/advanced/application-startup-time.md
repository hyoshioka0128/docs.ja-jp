---
title: アプリケーションの起動時間
ms.date: 03/30/2017
helpviewer_keywords:
- splash screen [WPF], startup time
- WPF [WPF], startup time
- startup time [WPF]
- application startup [WPF]
- performance [WPF], startup time
ms.assetid: f0ec58d8-626f-4d8a-9873-c20f95e08b96
ms.openlocfilehash: 0fae3ac1769163101dcdb183f4c5c2135354b1fc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79145424"
---
# <a name="application-startup-time"></a>アプリケーションの起動時間
WPF アプリケーションの起動に必要な時間には、かなりばらつきがあります。 このトピックでは、Windows Presentation Foundation (WPF) アプリケーションの認識される起動時間と実際の起動時間を短縮する方法について説明します。  
  
## <a name="understanding-cold-startup-and-warm-startup"></a>コールド スタートとウォーム スタートについて  
 コールド スタートは、システムの再起動後にアプリケーションを初めて起動するとき、またはアプリケーションを起動して閉じた後、時間をおいて再び起動するときに発生します。 アプリケーションが起動するときに、必要なページ (コード、静的データ、レジストリなど) が Windows メモリ マネージャーのスタンバイ リストに存在しない場合、ページ フォールトが発生します。 そのページをメモリに読み込むには、ディスクにアクセスする必要があります。  
  
 ウォーム スタートは、主要な共通言語ランタイム (CLR) コンポーネント用のページのほとんどが、既にメモリに読み込まれているときに発生し、貴重なディスク アクセス タイムを節約できます。 このため、マネージド アプリケーションを再度実行すると、初回よりも短い時間で起動します。  
  
## <a name="implement-a-splash-screen"></a>スプラッシュ スクリーンの実装  
 アプリケーションを起動してから最初の UI が表示されるまでに、どうしても多大な時間がかかる場合は、"*スプラッシュ スクリーン*" を使用して、認識される起動時間を最適化します。 この方法により、ユーザーがアプリケーションを起動すると、すぐにイメージが表示されます。 アプリケーションが最初の UI を表示する準備が整うと、スプラッシュ スクリーンはフェード アウトします。 スプラッシュ スクリーンは、.NET Framework 3.5 SP1 以降、<xref:System.Windows.SplashScreen> クラスを使用して実装することができます。 詳細については、[WPF アプリケーションへのスプラッシュ スクリーンの追加](../app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)に関するページをご覧ください。  
  
 ネイティブな Win32 グラフィックスを使用して、独自のスプラッシュ スクリーンを実装することもできます。 独自の実装は、<xref:System.Windows.Application.Run%2A> メソッドが呼び出される前に表示してください。  
  
## <a name="analyze-the-startup-code"></a>スタートアップ コードの分析  
 コールド スタートに時間がかかる理由を特定します。 ディスク I/O が原因である可能性がありますが、常にそうとは限りません。 通常、ネットワーク、Web サービス、ディスクなどの外部リソースの使用は最小限に抑えてください。  
  
 テストを始める前に、実行中のアプリケーションやサービスが、マネージド コードまたは WPF コードを使用していないことを確認してください。  
  
 再起動の直後に WPF アプリケーションを起動し、表示されるまでの時間を計測します。 その後アプリケーションを何回か起動し (ウォーム スタート)、各回の起動時間が初回よりも短ければ、コールド スタートの問題の原因は I/O であると判断できます。  
  
 アプリケーションのコールド スタートの問題に I/O が無関係である場合は、アプリケーションが長時間かかる初期化や計算を実行しているか、イベントの完了を待機しているか、起動時に大量の JIT コンパイルを必要としている可能性があります。 以下のセクションでは、こうした状況のいくつかについてさらに詳しく説明します。  
  
## <a name="optimize-module-loading"></a>モジュールの読み込みの最適化  
 プロセス エクスプローラー (Procexp.exe)、Tlist.exe などのツールを使用して、アプリケーションがどのモジュールを読み込むかを調べます。 `Tlist <pid>` コマンドを実行すると、プロセスによって読み込まれるすべてのモジュールが表示されます。  
  
 たとえば、Web に接続しないにもかかわらず System.Web.dll が読み込まれている場合は、アプリケーション内にこのアセンブリを参照するモジュールが含まれています。 この参照が本当に必要かどうかを検討してください。  
  
 アプリケーションに複数のモジュールがある場合は、それをマージして単一のモジュールにします。 この方法により、CLR によるアセンブリ読み込みのオーバーヘッドが減少します。 アセンブリ数が減少すると、CLR の管理対象となる状態も少なくなります。  
  
## <a name="defer-initialization-operations"></a>初期化処理の延期  
 メイン アプリケーション ウィンドウが表示されるまで、初期化コードの実行を延期することを検討します。  
  
 初期化はクラス コンストラクター内で実行される場合があり、初期化コードが他のクラスを参照していと、多数のクラス コンストラクターが次々に実行される可能性があることに注意してください。  
  
## <a name="avoid-application-configuration"></a>アプリケーション構成の回避  
 アプリケーション構成を回避することを検討してください。 たとえば、アプリケーションの構成要件がシンプルで、起動時間の目標が非常に厳しい場合は、構成の代わりに、レジストリ エントリまたはシンプルな INI ファイルを使って起動時間を短縮できます。  
  
## <a name="utilize-the-gac"></a>GAC の活用  
 アセンブリがグローバル アセンブリ キャッシュ (GAC) にインストールされていない場合、厳密な名前付きアセンブリのハッシュ検証と NGen イメージ検証 (コンピューター上でそのアセンブリのネイティブ イメージを使用できる場合) が原因で遅延が発生します。 厳密な名前の検証は、GAC にインストールされているアセンブリに対してはスキップされます。 詳細については、「[Gacutil.exe (グローバル アセンブリ キャッシュ ツール)](../../tools/gacutil-exe-gac-tool.md)」を参照してください。  
  
## <a name="use-ngenexe"></a>Ngen.exe の使用  
 アプリケーションでネイティブ イメージ ジェネレーター (Ngen.exe) を使用することを検討してください。 Ngen.exe を使用すると、CPU 消費は減少しますが、Ngen.exe によって生成されるネイティブ イメージの方が MSIL イメージよりも大きいことが多いため、ディスク アクセスが増えます。  
  
 ウォーム スタートの起動時間を短縮するには、アプリケーションでは必ず Ngen exe を使用します。これにより、アプリケーション コードの JIT コンパイルにかかる CPU コストを回避できます。  
  
 コールド スタートでも、Ngen.exe を使用すると有効なことがあります。 これは、JIT コンパイラ (mscorjit.dll) を読み込む必要がないためです。  
  
 NGen と JIT モジュールを併用すると、最悪の影響がもたらされる可能性があります。 mscorjit.dll を読み込む必要があるほか、JIT コンパイラは、アプリケーション コードを処理するとき、アセンブリのメタデータを読み込む際に NGen イメージ内の多数のページにアクセスする必要があるためです。  
  
### <a name="ngen-and-clickonce"></a>NGen と ClickOnce  
 アプリケーションの配置方法が、読み込み時間に影響することもあります。 ClickOnce によるアプリケーションのデプロイでは、NGen がサポートされていません。 アプリケーションで Ngen.exe を使用する場合は、Windows インストーラーなど、他の配置機構を使用する必要があります。  
  
 詳細については、「[Ngen.exe (ネイティブ イメージ ジェネレーター)](../../tools/ngen-exe-native-image-generator.md)」を参照してください。  
  
### <a name="rebasing-and-dll-address-collisions"></a>ベース変更と DLL アドレスの競合  
 Ngen.exe を使用する場合は、ネイティブ イメージがメモリに読み込まれる際にベース変更が発生する可能性があることに注意してください。 希望のベース アドレスのアドレス範囲が既に割り当て済みであることが原因で、そのベース アドレスに DLL を読み込めない場合、Windows ローダーは、その DLL を別のアドレスに読み込みますが、これには時間がかかることがあります。  
  
 仮想アドレス ダンプ (Vadump.exe) ツールを使用すると、すべてのページがプライベートであるモジュールが存在するかどうかを調べることができます。 存在する場合、そのモジュールは、別のアドレスにベース変更されている可能性があります。 したがって、そのページは共有できません。  
  
 ベース アドレスを設定する方法の詳細については、「[Ngen.exe (ネイティブ イメージ ジェネレーター)](../../tools/ngen-exe-native-image-generator.md)」を参照してください。  
  
## <a name="optimize-authenticode"></a>Authenticode の最適化  
 Authenticode 検証によって起動時間は長くなります。 Authenticode 署名があるアセンブリは、証明機関 (CA: Certification Authority) を使用して検証する必要があります。 この検証では、最新の証明書失効リストをダウンロードするためにネットワークに複数回接続する必要があるので、時間がかかる可能性があります。 また、信頼できるルートへのパスに、有効な証明書すべてが存在することも確認します。 これにより、アセンブリの読み込み中に、数秒間の遅延が発生する場合があります。  
  
 CA 証明書をクライアント コンピューターにインストールするか、可能な場合は Authenticode の使用を避けることを検討してください。 アプリケーションが発行者の証拠を必要としないことがわかっている場合は、署名を検証する手間をかける必要はありません。  
  
 .NET Framework 3.5 以降、Authenticode 検証のバイパスを可能にする構成オプションが用意されています。 これを行うには、次の設定を app.exe.config ファイルに追加します。  
  
```xml  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>
    </runtime>  
</configuration>  
```  
  
 詳細については、「[\<generatePublisherEvidence> 要素](../../configure-apps/file-schema/runtime/generatepublisherevidence-element.md)」を参照してください。  
  
## <a name="compare-performance-on-windows-vista"></a>Windows Vista でのパフォーマンスの比較  
 Windows Vista のメモリ マネージャーには、SuperFetch というテクノロジが組み込まれています。 SuperFetch は、一定期間内のメモリ使用パターンを分析して、そのユーザーに適したメモリの内容を判断します。 そして、その内容が維持されるよう継続的に動作します。  
  
 これは、Windows XP で使用されているプリフェッチ手法とは異なります。プリフェッチでは、使用パターンを分析せずに、データをメモリにプリロードします。 ユーザーが WPF アプリケーションを Windows Vista で頻繁に使用すると、アプリケーションのコールド スタートの起動時間は次第に短くなる可能性があります。  
  
## <a name="use-appdomains-efficiently"></a>AppDomains の効率的な使用  
 可能な場合はアセンブリをドメイン中立コード領域に読み込み、アプリケーションで作成されるすべての AppDomains でネイティブ イメージが使用されるようにします (ネイティブ イメージが存在する場合)。  
  
 パフォーマンスを最大限に高めるには、ドメイン間呼び出しを減らしてドメイン間の通信を効率化します。 可能な場合は、引数のない呼び出し、または引数がプリミティブ型である呼び出しを使用します。  
  
## <a name="use-the-neutralresourceslanguage-attribute"></a>NeutralResourcesLanguage 属性の使用  
 <xref:System.Resources.NeutralResourcesLanguageAttribute> を使用して、<xref:System.Resources.ResourceManager> のニュートラル カルチャを指定します。 この方法を使用すると、アセンブリのルックアップの失敗が回避されます。  
  
## <a name="use-the-binaryformatter-class-for-serialization"></a>シリアル化での BinaryFormatter クラスの使用  
 シリアル化を使用する必要がある場合は、<xref:System.Xml.Serialization.XmlSerializer> クラスの代わりに <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> クラスを使用します。 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> クラスは、mscorlib.dll アセンブリの基本クラス ライブラリ (BCL) に実装されます。 <xref:System.Xml.Serialization.XmlSerializer> は System.Xml.dll アセンブリに実装されますが、これは、読み込まれる追加 DLL である場合があります。  
  
 <xref:System.Xml.Serialization.XmlSerializer> クラスを使用する必要がある場合は、シリアル化アセンブリを事前に生成すると、パフォーマンスを向上させることができます。  
  
## <a name="configure-clickonce-to-check-for-updates-after-startup"></a>起動後に更新プログラムをチェックする ClickOnce の構成  
 アプリケーションで ClickOnce を使用する場合は、アプリケーションの起動後にデプロイ サイトの更新プログラムをチェックするように ClickOnce を構成することで、ネットワーク アクセスを回避します。  
  
 XAML ブラウザー アプリケーション (XBAP) モデルを使用する場合、ClickOnce は、XBAP が既に ClickOnce キャッシュに存在する場合でも、デプロイ サイトの更新プログラムのチェックが行われることに注意してください。 詳細については、「 [ClickOnce Security and Deployment](/visualstudio/deployment/clickonce-security-and-deployment)」を参照してください。  
  
## <a name="configure-the-presentationfontcache-service-to-start-automatically"></a>PresentationFontCache サービスの自動起動の構成  
 再起動後に最初に実行される WPF アプリケーションは PresentationFontCache サービスです。 このサービスは、システム フォントをキャッシュし、フォント アクセスを高速化して、パフォーマンス全体を向上させます。 このサービスの起動にはオーバーヘッドが伴うため、一部の制御された環境では、システムの再起動時にこのサービスを自動起動するように構成することを検討してください。  
  
## <a name="set-data-binding-programmatically"></a>データ バインディングのプログラムによる設定  
 XAML を使用してメイン ウィンドウの <xref:System.Windows.FrameworkElement.DataContext%2A> を宣言によって設定するのではなく、<xref:System.Windows.Application.OnActivated%2A> メソッドでプログラムによって設定することを検討します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.SplashScreen>
- <xref:System.AppDomain>
- <xref:System.Resources.NeutralResourcesLanguageAttribute>
- <xref:System.Resources.ResourceManager>
- [スプラッシュ スクリーンを WPF アプリケーションに追加する](../app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)
- [Ngen.exe (ネイティブ イメージ ジェネレーター)](../../tools/ngen-exe-native-image-generator.md)
- [\<generatePublisherEvidence> 要素](../../configure-apps/file-schema/runtime/generatepublisherevidence-element.md)
