---
title: 安全なクライアント アプリケーション
ms.date: 03/30/2017
ms.assetid: 6239592e-fa7d-4dea-9f00-d296d0048b01
ms.openlocfilehash: 15d2b2199344644392be0e9a530c046a77db8523
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794382"
---
# <a name="secure-client-applications"></a>安全なクライアント アプリケーション
通常、アプリケーションは多数の要素で構成されており、それぞれをデータの損失やシステムのセキュリティ侵害を招く脆弱性から確実に保護する必要があります。 安全なユーザー インターフェイスを作成し、攻撃者によるデータやシステム リソースへのアクセスを未然に阻止することで、多くの問題を防ぐことができます。  
  
## <a name="validate-user-input"></a>ユーザー入力の検証  
 データにアクセスするアプリケーションを構築する場合、ユーザーの入力はすべて悪意のあるものと想定しない限り、 攻撃に対する脆弱性をアプリケーションから取り除くことはできません。 .NET Framework には、入力できる文字数の制限など、入力コントロールの値の範囲を設定するクラスが用意されています。 イベントを捕捉することによって、値の有効性を確認するプロシージャを作成できます。 ユーザーによって入力されるデータを検証し、厳密に型指定することで、アプリケーションをスクリプト インジェクションや SQL インジェクションなどの攻撃にさらす機会を制限できます。  
  
> [!IMPORTANT]
> クライアント アプリケーションだけでなく、データ ソース側でもユーザー入力を検証する必要があります。 攻撃者がアプリケーションを迂回し、データ ソースを直接攻撃してくる可能性もあります。  
  
 [セキュリティとユーザー入力](../../../standard/security/security-and-user-input.md)  
 発見が難しく大きな危険を招く可能性のあるユーザー入力に関連したバグへの対処方法を説明します。  
  
 [ASP.NET Web ページにおけるユーザー入力の検証](https://docs.microsoft.com/previous-versions/aspnet/7kh55542(v=vs.100))  
 ASP.NET の検証コントロールを使ったユーザー入力の検証について概要を説明します。  
  
 [Windows フォームでのユーザー入力](../../winforms/user-input-in-windows-forms.md)  
 Windows フォーム アプリケーションにおけるマウス入力およびキーボード入力の検証に関連したリンクや情報を提供します。  
  
 [.NET Framework 正規表現](../../../standard/base-types/regular-expressions.md)  
 <xref:System.Text.RegularExpressions.Regex> クラスを使用してユーザー入力の有効性を確認する方法について説明します。  
  
## <a name="windows-applications"></a>Windows アプリケーション  
 これまで、Windows アプリケーションは、アクセスがすべて許可された状態で実行されていました。 .NET Framework は、コード アクセス セキュリティ (CAS) を使用して Windows アプリケーションで実行されるコードを制限するインフラストラクチャを提供します。 ただし、CAS だけでは、アプリケーションを保護するには不十分です。  
  
 [Windows フォームのセキュリティ](../../winforms/windows-forms-security.md)  
 Windows フォーム アプリケーションをセキュリティで保護する方法について説明します。また、関連項目へのリンクがあります。  
  
 [Windows Forms and Unmanaged Applications](../../winforms/advanced/windows-forms-and-unmanaged-applications.md)  
 Windows フォーム アプリケーションでアンマネージ アプリケーションと対話する方法について説明します。  
  
 [Windows フォームの ClickOnce 配置](../../winforms/clickonce-deployment-for-windows-forms.md)  
 Windows フォーム アプリケーションでの `ClickOnce` 配置の使用方法およびセキュリティへの影響について説明します。  
  
## <a name="aspnet-and-xml-web-services"></a>ASP.NET と XML Web サービス  
 通常、ASP.NET アプリケーションは、アクセスを Web サイトの一部に制限し、データ保護およびサイト セキュリティのための他のメカニズムを提供する必要があります。 以下のリンクにアクセスすると、ASP.NET アプリケーションをセキュリティで保護するための有益な情報を見つけることができます。  
  
 XML Web サービスは、ASP.NET アプリケーション、Windows フォーム アプリケーション、またはその他の Web サービスが使用できるデータを提供します。 クライアント アプリケーションのセキュリティだけでなく、Web サービスそのもののセキュリティを管理する必要があります。  
  
 詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[ASP.NET Web サイトのセキュリティ保護](https://docs.microsoft.com/previous-versions/aspnet/91f66yxt(v=vs.100))|ASP.NET アプリケーションをセキュリティで保護する方法について説明します。|  
|[ASP.NET を使用して作成した XML Web サービスのセキュリティ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w67h0dw7(v=vs.100))|ASP.NET Web サービスへのセキュリティの実装方法について説明します。|  
|[スクリプト攻略の概要](https://docs.microsoft.com/previous-versions/aspnet/w1sw53ds(v=vs.100))|Web ページに悪意のある文字の挿入を試みるスクリプト攻略攻撃を阻止する方法について説明します。|  
|[Web アプリケーションのセキュリティに関する基本的な対策](https://docs.microsoft.com/previous-versions/aspnet/zdh19h94(v=vs.100))|一般的なセキュリティ情報のほか、より詳細なページへのリンクも掲載されています。|  
  
## <a name="remoting"></a>リモート処理  
 .NET リモート処理を使用すると、広範囲の分散アプリケーションを簡単に構築できます。その場合、アプリケーションのコンポーネントを、すべて 1 台のコンピューターに置くことも、遠隔地のコンピューターに分散させることもできます。 同じコンピューター上、またはネットワークを経由してアクセスできる他の任意のコンピューター上にある他のプロセスのオブジェクトを使用するクライアント アプリケーションを構築できます。 また、.NET リモート処理を使用すると、同じプロセスの他のアプリケーション ドメインと通信できます。  
  
|リソース|説明|  
|--------------|-----------------|  
|[リモート アプリケーションの構成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/b8tysty8(v=vs.100))|一般的な問題を回避するためのリモート処理アプリケーションの構成方法について説明します。|  
|[リモート処理でのセキュリティ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/9hwst9th(v=vs.100))|認証と暗号化のほか、リモート処理に関連したその他のセキュリティ トピックについて説明します。|  
|[セキュリティとリモート処理の考慮事項](../../misc/security-and-remoting-considerations.md)|保護されたオブジェクトやアプリケーション ドメインの境界越えに伴うセキュリティの問題について説明します。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](securing-ado-net-applications.md)
- [データ アクセス戦略に関する推奨事項](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))
- [アプリケーションの保護](/visualstudio/ide/securing-applications)
- [接続情報の保護](protecting-connection-information.md)
- [ADO.NET の概要](ado-net-overview.md)
