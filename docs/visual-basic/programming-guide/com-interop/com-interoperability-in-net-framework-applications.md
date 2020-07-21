---
title: .NET Framework アプリケーションにおける COM 相互運用性
ms.date: 07/20/2015
helpviewer_keywords:
- interoperability, COM and .NET Framework objects
- COM interop [Visual Basic]
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
ms.openlocfilehash: 377958a21886fe0257633ea19417f9a19bd51ff3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396870"
---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>.NET Framework アプリケーションにおける COM 相互運用性 (Visual Basic)

COM オブジェクトと .NET Framework オブジェクトを同じアプリケーションで使用する場合は、オブジェクトがメモリ内にどのように存在するかの違いに対処する必要があります。 .NET Framework オブジェクトはマネージド メモリ (共通言語ランタイムによって制御されるメモリ) 内にあり、必要に応じてランタイムによって移動される場合があります。 COM オブジェクトはアンマネージ メモリ内にあり、別のメモリの場所に移動することは想定されていません。 Visual Studio と .NET Framework には、これらのマネージド コンポーネントとアンマネージ コンポーネントの相互作用を制御するためのツールが用意されています。 詳細については、[共通言語ランタイム](../../../standard/clr.md)に関するページを参照してください。

.NET アプリケーションで COM オブジェクトを使用するだけでなく、Visual Basic を使用して、COM を介してアンマネージ コードからアクセスできるオブジェクトを開発することもできます。

このページのリンクを使用すると、COM オブジェクトと .NET Framework オブジェクトの間の相互作用についての詳細が表示されます。

## <a name="related-sections"></a>関連項目

| | |
|---------|---------|
| [COM 相互運用](index.md) | COM オブジェクト、ActiveX コントロール、Win32 DLL、マネージド オブジェクト、COM オブジェクトの継承など、Visual Basic の COM 相互運用性に関するトピックへのリンクが掲載されています。 |
| [アンマネージ コードとの相互運用](../../../framework/interop/index.md) | マネージド コードとアンマネージ コードの間の相互作用の問題について簡単に説明し、さらに学習するためのリンクを掲載しています。 |
| [COM ラッパー](../../../standard/native-interop/com-wrappers.md) | マネージド コードが COM メソッドを呼び出すことができるようにするランタイム呼び出し可能ラッパー、および COM クライアントが .NET オブジェクトのメソッドを呼び出すことができるようにする COM 呼び出し可能ラッパーについて説明しています。 |
| [高度な COM 相互運用性](../../../framework/interop/index.md) | ラッパー、例外、継承、スレッド処理、イベント、変換、およびマーシャリングに関して、COM の相互運用性に関するトピックへのリンクを掲載しています。 |
| [Tlbimp.exe (タイプ ライブラリ インポーター)](../../../framework/tools/tlbimp-exe-type-library-importer.md) | COM タイプ ライブラリにある型定義を共通言語ランタイム アセンブリで等価な定義に変換するために使用できるツールについて説明しています。 |
