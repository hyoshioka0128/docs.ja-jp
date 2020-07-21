---
title: C# を使用した JSON のシリアル化と逆シリアル化 - .NET
description: この概要では、.NET で JSON との間でシリアル化または逆シリアル化を行うための System.Text.Json 名前空間機能について説明します。
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 909d979d46b30939e304af071de65d230febd92d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380137"
---
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a>.NET での JSON のシリアル化と逆シリアル化 (マーシャリングとマーシャリング解除) - 概要

`System.Text.Json` 名前空間は、JavaScript Object Notation (JSON) との間でのシリアル化と逆シリアル化の機能を提供します。

ライブラリの設計では、ハイ パフォーマンスと、高度な豊富なセットに対する少ないメモリ割り当てが強調されています。 組み込みの UTF-8 サポートによって、UTF-8 としてエンコードされた JSON テキストの読み取りと書き込みのプロセスが最適化されます。これは、web 上のデータおよびディスク上のファイルのための最も一般的なエンコードです。

ライブラリには、メモリ内のドキュメント オブジェクト モデル (DOM) を操作するためのクラスも用意されています。 この機能により、JSON ファイルまたは文字列内の要素に対する読み取り専用のランダムアクセスが可能になります。

## <a name="how-to-get-the-library"></a>ライブラリの入手方法

* このライブラリは [.NET Core 3.0](https://aka.ms/netcore3download) 共有フレームワークの一部として組み込まれています。
* その他のターゲット フレームワークの場合は、[System.Text.Json](https://www.nuget.org/packages/System.Text.Json) NuGet パッケージをインストールします。 このパッケージで以下がサポートされます。
  * .NET Standard 2.0 以降のバージョン
  * .NET Framework 4.7.2 以降のバージョン
  * .NET Core 2.0、2.1、および 2.2

## <a name="additional-resources"></a>その他の技術情報

* [ライブラリを使用する方法](system-text-json-how-to.md)
* [Newtonsoft.Json から移行する方法](system-text-json-migrate-from-newtonsoft-how-to.md)
* [コンバーターを記述する方法](system-text-json-converters-how-to.md)
* [System.Text.Json ソース コード](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json)
* [System.Text.Json API リファレンス](xref:System.Text.Json)
* [System.Text.Json.Serialization API リファレンス](xref:System.Text.Json.Serialization)
<!-- * [Roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
