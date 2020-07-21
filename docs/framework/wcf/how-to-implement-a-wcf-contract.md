---
title: 'チュートリアル: Windows Communication Foundation サービスコントラクトの実装'
description: Wcf アプリケーションの作成を開始する際に役立つ一連の記事の一部として、WCF サービスインターフェイスを実装するコードを追加する方法について説明します。
ms.date: 03/19/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], implementing
ms.assetid: d5ab51ba-61ae-403e-b3c8-e2669e326806
ms.openlocfilehash: 89f97610cccd42c2a5d298baa667327d077fd472
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244648"
---
# <a name="tutorial-implement-a-windows-communication-foundation-service-contract"></a>チュートリアル: Windows Communication Foundation サービスコントラクトの実装

このチュートリアルでは、基本的な Windows Communication Foundation (WCF) アプリケーションを作成するために必要な5つのタスクについて説明します。 チュートリアルの概要については、「[チュートリアル: Windows Communication Foundation アプリケーションの](getting-started-tutorial.md)概要」を参照してください。

WCF アプリケーションを作成するための次の手順では、前の手順で作成した WCF サービスインターフェイスを実装するコードを追加します。 この手順では、ユーザー定義のインターフェイスを実装するという名前のクラスを作成し `CalculatorService` `ICalculator` ます。 次のコードの各メソッドは、電卓操作を呼び出し、テキストをコンソールに書き込んでテストします。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
>
> - WCF サービスコントラクトを実装するコードを追加します。
> - ソリューションをビルドします。

## <a name="add-code-to-implement-the-wcf-service-contract"></a>WCF サービスコントラクトを実装するコードを追加する

**Service1.cs**または**Service1**ファイルを**開き、その**コードを次のコードに置き換えます。

```csharp
using System;
using System.ServiceModel;

namespace GettingStartedLib
{
    public class CalculatorService : ICalculator
    {
        public double Add(double n1, double n2)
        {
            double result = n1 + n2;
            Console.WriteLine("Received Add({0},{1})", n1, n2);
            // Code added to write output to the console window.
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Subtract(double n1, double n2)
        {
            double result = n1 - n2;
            Console.WriteLine("Received Subtract({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Multiply(double n1, double n2)
        {
            double result = n1 * n2;
            Console.WriteLine("Received Multiply({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Divide(double n1, double n2)
        {
            double result = n1 / n2;
            Console.WriteLine("Received Divide({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }
    }
}
```

```vb
Imports System.ServiceModel

Namespace GettingStartedLib

    Public Class CalculatorService
        Implements ICalculator

        Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add
            Dim result As Double = n1 + n2
            ' Code added to write output to the console window.
            Console.WriteLine("Received Add({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result
        End Function

        Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract
            Dim result As Double = n1 - n2
            Console.WriteLine("Received Subtract({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function

        Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply
            Dim result As Double = n1 * n2
            Console.WriteLine("Received Multiply({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function

        Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide
            Dim result As Double = n1 / n2
            Console.WriteLine("Received Divide({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function
    End Class
End Namespace
```

## <a name="edit-appconfig"></a>App.config の編集

**Gettingon lib**で**App.config**を編集して、コードに加えた変更を反映します。

- Visual C# プロジェクトの場合:
  - 14行目をに変更します。`<service name="GettingStartedLib.CalculatorService">`
  - 17行目をに変更します。`<add baseAddress = "http://localhost:8000/GettingStarted/CalculatorService" />`
  - 22行目をに変更します。`<endpoint address="" binding="wsHttpBinding" contract="GettingStartedLib.ICalculator">`

- Visual Basic プロジェクトの場合は、次の操作を行います。
  - 14行目をに変更します。`<service name="GettingStartedLib.GettingStartedLib.CalculatorService">`
  - 17行目をに変更します。`<add baseAddress = "http://localhost:8000/GettingStarted/CalculatorService" />`
  - 22行目をに変更します。`<endpoint address="" binding="wsHttpBinding" contract="GettingStartedLib.GettingStartedLib.ICalculator">`

## <a name="compile-the-code"></a>コードのコンパイル

ソリューションをビルドして、コンパイルエラーがないことを確認します。 Visual Studio を使用している場合は、[**ビルド**] メニューの [**ソリューションのビルド**] を選択します (または、 **Ctrl** + **Shift** + **B**キーを押します)。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
>
> - WCF サービスコントラクトを実装するコードを追加します。
> - ソリューションをビルドします。

次のチュートリアルに進み、WCF サービスを実行する方法を学習してください。

> [!div class="nextstepaction"]
> [チュートリアル: 基本的な WCF サービスをホストして実行する](how-to-host-and-run-a-basic-wcf-service.md)
