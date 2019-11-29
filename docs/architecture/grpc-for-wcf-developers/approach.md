---
title: GRPC が WCF 開発者向けの RPC-gRPC にアプローチする方法
description: WCF の主な機能を gRPC と比較します。
ms.date: 09/02/2019
ms.openlocfilehash: 1ebfd102217c9685c5ff5200386c642b2017e98f
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73968129"
---
# <a name="how-grpc-approaches-rpc"></a>gRPC でいかにして RPC に近づくか

Windows Communication Foundation (WCF) と gRPC はどちらも、*リモートプロシージャコール*(RPC) パターンの実装であり、別のコンピューターで実行されているサービスを呼び出すことを目的としています。また、別のプロセスでは、クライアントアプリケーションのメソッド呼び出しと同じようにシームレスに動作します。 WCF と gRPC の目的は同じですが、実装の詳細はまったく異なります。

次の表は、WCF の主要な機能が gRPC とどのように関連しているかを示しています。また、このブックの残りの部分では、より詳細な説明を参照できます。

| 機能 | WCF | gRPC |
| -------- | --- | ---- |
| 目標 | ネットワーク実装からビジネスコードを分離する | インターフェイス定義とネットワーク実装からビジネスコードを分離する |
| サービスとメッセージを定義する (章 3-4)  | サービスコントラクト、操作コントラクト、およびデータコントラクト | プロトコルファイルを使用して、サービスとメッセージを宣言します。 |
| 言語 (章 3-5) | または Visual Basic C#で記述されたコントラクト | プロトコルバッファー言語 |
| ワイヤ形式 (第3章) | SOAP/XML、Plain XML、JSON、.NET バイナリなどの構成が可能です。 | プロトコルバッファーバイナリ形式 (他の形式を使用することもできます)。
| 相互運用性 (第4章) | SOAP over HTTP を使用する場合 | 公式サポート: .NET、Java、Python、JavaScript、C/C++、ゴー、Rust、Ruby、Swift、DART、PHP。 コミュニティの他の言語を非公式にサポートします。 |
| ネットワーク (第4章) | 実行時に構成されます。 NetTCP、HTTP、MSMQ などを切り替えます。 | HTTP/2 (現時点では ASP.NET Core gRPC を使用した TCP のみ)。 |
| 方法 (第4章) | 基本クラスでのシリアル化/逆シリアル化とネットワークコードのランタイム生成 | 基本クラスでのシリアル化/逆シリアル化とネットワークコードのビルド時生成 |
| セキュリティ (第6章) | 認証、WS-SECURITY、メッセージの暗号化 | 資格情報、ASP.NET Core セキュリティ、TLS ネットワーク |

>[!div class="step-by-step"]
>[前へ](grpc-overview.md)
>[次へ](interface-definition-language.md)
