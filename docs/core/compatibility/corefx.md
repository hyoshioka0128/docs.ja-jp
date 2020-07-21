---
title: 基本クラス ライブラリの破壊的変更
description: Core .NET ライブラリにおける破壊的変更の一覧を示します。
ms.date: 09/20/2019
ms.openlocfilehash: 1c56358e69d0dd6e8572a41229c1b9edbcdad795
ms.sourcegitcommit: 63bb83322814f5e5e5c5b69939b14a3139a6ca7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85365618"
---
# <a name="core-net-libraries-breaking-changes"></a>Core .NET ライブラリの破壊的変更

Core .NET ライブラリでは、.NET Core で使用されるプリミティブとその他の一般的な型が提供されます。

このページでは、次の破壊的変更について説明します。

| 互換性に影響する変更点 | 導入されたバージョン |
| - | :-: |
| [SSE および SSE2 の CompareGreaterThan メソッドで NaN 入力が正しく処理されるようになった](#sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs) | 5.0 |
| [インスタンスが既に存在する場合、CounterSet.CreateCounterSetInstance は InvalidOperationException をスローするようになった](#countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists) | 5.0 |
| [Microsoft.DotNet.PlatformAbstractions パッケージの削除](#microsoftdotnetplatformabstractions-package-removed) | 5.0 |
| [バージョンをレポートする API が、ファイル バージョンではなく製品をレポートするようになった](#apis-that-report-version-now-report-product-and-not-file-version) | 3.0 |
| [カスタム EncoderFallbackBuffer インスタンスが再帰的にフォールバックしない](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | 3.0 |
| [浮動小数点の書式設定と解析の動作の変更](#floating-point-formatting-and-parsing-behavior-changed) | 3.0 |
| [浮動小数点の解析操作が失敗したり OverflowException がスローされたりすることがなくなった](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | 3.0 |
| [InvalidAsynchronousStateException を別のアセンブリに移動](#invalidasynchronousstateexception-moved-to-another-assembly) | 3.0 |
| [Unicode のガイドラインに従って不適切な形式の UTF-8 バイト シーケンスを置き換える](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | 3.0 |
| [TypeDescriptionProviderAttribute を別のアセンブリに移動](#typedescriptionproviderattribute-moved-to-another-assembly) | 3.0 |
| [ZipArchiveEntry による、エントリ サイズに一貫性のないアーカイブ処理の中止](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | 3.0 |
| [JSON シリアライザーの例外の種類を JsonException から NotSupportedException に変更](#json-serializer-exception-type-changed-from-jsonexception-to-notsupportedexception) | 3.0 |
| [Utf8JsonWriter での (string)null のセマンティクスの変更](#change-in-semantics-of-stringnull-in-utf8jsonwriter) | 3.0 |
| [JsonEncodedText.Encode メソッドに JavaScriptEncoder 引数を追加](#jsonencodedtextencode-methods-have-an-additional-javascriptencoder-argument) | 3.0 |
| [JsonFactoryConverter.CreateConverter 署名の変更](#jsonfactoryconvertercreateconverter-signature-changed) | 3.0 |
| [JsonElement API の変更](#jsonelement-api-changes) | 3.0 |
| [FieldInfo.SetValue で、静的な初期化専用フィールドに対する例外がスローされる](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | 3.0 |
| [組み込みの構造体型に追加されたプライベート フィールド](#private-fields-added-to-built-in-struct-types) | 2.1 |
| [UseShellExecute の既定値の変更](#change-in-default-value-of-useshellexecute) | 2.1 |
| [macOS 上の OpenSSL バージョン](#openssl-versions-on-macos) | 2.1 |
| [FileSystemInfo.Attributes によってスローされる UnauthorizedAccessException](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | 1 |
| [プロセス破損状態例外の処理がサポートされない](#handling-corrupted-state-exceptions-is-not-supported) | 1 |
| [UriBuilder のプロパティでは今後、先頭に文字が付加されない](#uribuilder-properties-no-longer-prepend-leading-characters) | 1 |
| [開始されなかったプロセスについて Process.StartInfo が InvalidOperationException をスローする](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | 1 |

## <a name="net-50"></a>.NET 5.0

[!INCLUDE [sse-comparegreaterthan-intrinsics](../../../includes/core-changes/corefx/5.0/sse-comparegreaterthan-intrinsics.md)]

***

[!INCLUDE [createcountersetinstance-throws-invalidoperation](../../../includes/core-changes/corefx/5.0/createcountersetinstance-throws-invalidoperation.md)]

***

[!INCLUDE [platformabstractions-package-removed](../../../includes/core-changes/corefx/5.0/platformabstractions-package-removed.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

***

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

***

[!INCLUDE[JSON serializer exception type changed from JsonException to NotSupportedException](~/includes/core-changes/corefx/3.0/serializer-throws-notsupportedexception.md)]

***

[!INCLUDE[Change in semantics of (string)null in Utf8JsonWriter](~/includes/core-changes/corefx/3.0/change-in-null-in-utf8jsonwriter.md)]

***

[!INCLUDE[JsonEncodedText.Encode methods have an additional JavaScriptEncoder argument](~/includes/core-changes/corefx/3.0/jsonencodedtext-encode-has-additional-argument.md)]

***

[!INCLUDE[JsonFactoryConverter.CreateConverter signature changed](~/includes/core-changes/corefx/3.0/jsonfactoryconverter-createconverter.md)]

***

[!INCLUDE[JsonElement API changes](~/includes/core-changes/corefx/3.0/jsonelement-api-changes.md)]

***

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

***

## <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

***

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

***

## <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

***
