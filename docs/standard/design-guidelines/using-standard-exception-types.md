---
title: 標準例外型の使用
description: .NET での標準の例外の種類について説明します。 SystemException、ApplicationException、ArgumentException、ComException などについて説明します。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- throwing exceptions, standard types
- catching exceptions
- exceptions, catching
- exceptions, throwing
ms.assetid: ab22ce03-78f9-4dca-8824-c7ed3bdccc27
ms.openlocfilehash: f95529eabd87d9ec7c379b9f790e039e1192ac53
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663058"
---
# <a name="using-standard-exception-types"></a>標準例外型の使用
このセクションでは、フレームワークによって提供される標準の例外とその使用法の詳細について説明します。 リストは、完全な手段ではありません。 他のフレームワークの例外の種類の使用方法については、.NET Framework リファレンスドキュメントを参照してください。

## <a name="exception-and-systemexception"></a>Exception および SystemException
 ❌<xref:System.Exception?displayProperty=nameWithType>またはをスローしないで <xref:System.SystemException?displayProperty=nameWithType> ください。

 ❌を再 `System.Exception` `System.SystemException` スローする場合を除き、フレームワークコードでまたはをキャッチしないでください。

 ❌`System.Exception` `System.SystemException` 最上位レベルの例外ハンドラーを除き、またはをキャッチしないでください。

## <a name="applicationexception"></a>ApplicationException
 ❌をスローしたり、から派生させたりしないで <xref:System.ApplicationException> ください。

## <a name="invalidoperationexception"></a>InvalidOperationException
 <xref:System.InvalidOperationException>オブジェクトが不適切な状態にある場合は、✔️スローされます。

## <a name="argumentexception-argumentnullexception-and-argumentoutofrangeexception"></a>ArgumentException、System.argumentnullexception、ArgumentOutOfRangeException
 <xref:System.ArgumentException>無効な引数がメンバーに渡された場合、✔️、またはそのサブタイプの1つをスローします。 最も派生した例外の種類を優先します (該当する場合)。

 ✔️は、 `ParamName` のサブクラスの1つをスローするときに、プロパティを設定し `ArgumentException` ます。

 このプロパティは、例外がスローされる原因となったパラメーターの名前を表します。 プロパティは、コンストラクターのオーバーロードのいずれかを使用して設定できます。

 ✔️は `value` 、プロパティ setter の暗黙的な値パラメーターの名前にを使用します。

## <a name="nullreferenceexception-indexoutofrangeexception-and-accessviolationexception"></a>NullReferenceException、IndexOutOfRangeException、および Access Ationexception
 ❌パブリックに呼び出し可能な Api が、、、またはを明示的または暗黙的にスローすることを許可しないでください <xref:System.NullReferenceException> <xref:System.AccessViolationException> <xref:System.IndexOutOfRangeException> 。 これらの例外は、実行エンジンによって予約およびスローされ、ほとんどの場合、バグを示します。

 これらの例外をスローしないように引数をチェックします。 これらの例外をスローすると、時間の経過と共に変化する可能性のあるメソッドの実装の詳細が表示されます。

## <a name="stackoverflowexception"></a>StackOverflowException
 ❌明示的にスローしないで <xref:System.StackOverflowException> ください。 例外は、CLR によってのみ明示的にスローされる必要があります。

 ❌キャッチしないで `StackOverflowException` ください。

 任意のスタックオーバーフローの有無に一貫性を持たせるマネージコードを記述することはほとんど不可能です。 CLR のアンマネージ部分は、プローブを使用してスタックオーバーフローを適切に定義された場所に移動することによって一貫性を保ちます。これは、任意のスタックオーバーフローからのバックアップではありません。

## <a name="outofmemoryexception"></a>OutOfMemoryException
 ❌明示的にスローしないで <xref:System.OutOfMemoryException> ください。 この例外は、CLR インフラストラクチャによってのみスローされます。

## <a name="comexception-sehexception-and-executionengineexception"></a>ComException、SEHException、および System.executionengineexception
 ❌、、およびを明示的にスローしないでください <xref:System.Runtime.InteropServices.COMException> <xref:System.ExecutionEngineException> <xref:System.Runtime.InteropServices.SEHException> 。 これらの例外は、CLR インフラストラクチャによってのみスローされます。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [例外のデザインのガイドライン](exceptions.md)
