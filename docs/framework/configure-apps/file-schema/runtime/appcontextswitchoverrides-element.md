---
title: AppContextSwitchOverrides 要素
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- AppContextSwitchOverrides
- compatibility switches
- configuration switches
- configuration
ms.assetid: 4ce07f47-7ddb-4d91-b067-501bd8b88752
ms.openlocfilehash: 8d5cd73bb9393533cb669581420e24297cb5ff71
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "82102932"
---
# <a name="appcontextswitchoverrides-element"></a>\<AppContextSwitchOverrides> 要素

<xref:System.AppContext> クラスで使用される、新機能に対するオプトアウト メカニズムを指定するスイッチを 1 つまたは複数定義します。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<AppContextSwitchOverrides>**

## <a name="syntax"></a>構文

```xml
<AppContextSwitchOverrides value="name1=value1[[;name2=value2];...]" />
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`value`|必須の属性です。<br /><br /> 1つ以上のスイッチ名とそれに関連付けられたブール値を定義します。|

### <a name="value-attribute"></a>value 属性

|値|Description|
|-----------|-----------------|
|"name = value"|定義済みのスイッチ名とその値 ( `true` または `false` )。 複数のスイッチの名前と値のペアは、セミコロン (";") で区切られます。 .NET Framework でサポートされている定義済みスイッチ名の一覧については、「解説」を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|

## <a name="remarks"></a>解説
 .NET Framework 4.6 以降では、 `<AppContextSwitchOverrides>` API の呼び出し元は、アプリが新しい機能を利用できるか、ライブラリの以前のバージョンとの互換性を維持できるかを判断するために、API の呼び出し元によって、API の呼び出し元に許可されます。 たとえば、API の動作がライブラリの2つのバージョン間で変更されている場合、要素を使用すると、 `<AppContextSwitchOverrides>` その api の呼び出し元は、新しい機能をサポートするライブラリのバージョンで新しい動作を無効にすることができます。 .NET Framework で Api を呼び出すアプリの場合、要素は、アプリ `<AppContextSwitchOverrides>` がその機能を含むバージョンの .NET Framework で実行されている場合に、アプリが以前のバージョンの .NET Framework をターゲットにして新しい機能をオプトインできるようにすることもできます。

 `value`要素の属性は、 `<AppContextSwitchOverrides>` セミコロンで区切られた1つ以上の名前と値のペアで構成される1つの文字列で構成されます。  各名前は互換性スイッチを識別し、対応する値は、 `true` `false` スイッチが設定されているかどうかを示すブール値 (または) です。 既定では、スイッチは `false` で、ライブラリは新しい機能を提供します。 スイッチが設定されている場合 (つまり、値がである場合) にのみ、以前の機能が提供され `true` ます。 これにより、ライブラリは既存の API に新しい動作を提供できるようになり、以前の動作に依存する呼び出し元は新しい機能を無効にすることができます。

.NET Framework では、次のスイッチがサポートされています。

|スイッチ名|Description|導入時期|
|-----------------|-----------------|----------------|
|`Switch.MS.Internal.`<br/>`DoNotApplyLayoutRoundingToMarginsAndBorderThickness`|コントロールレイアウトのために Windows Presentation Foundation レガシアルゴリズムを使用するかどうかを制御します。 詳細については、「[軽減策: WPF レイアウト](../../../migration-guide/mitigation-wpf-layout.md)」を参照してください。|.NET Framework 4.6|
|`Switch.MS.Internal.`<br/>`UseSha1AsDefaultHashAlgorithmForDigitalSignatures`|PackageDigitalSignatureManager によってパッケージの部分に署名するために使用される既定のアルゴリズムが SHA1 と SHA256 のどちらであるかを制御します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.1|
|`Switch.System.Activities.`<br/>`UseMD5CryptoServiceProviderForWFDebugger`|に設定すると `false` 、FIPS が有効になっている場合に、Visual Studio で XAML ベースのワークフロープロジェクトをデバッグできるようになります。 これを使用しない場合、は、system.object <xref:System.NullReferenceException> アセンブリ内のメソッドの呼び出しでスローされます。|.NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseMD5ForWFDebugger`|デバッガーのワークフローインスタンスのチェックサムで MD5 と SHA1 のどちらを使用するかを制御します。 | .NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseSHA1HashForDebuggerSymbols`|ワークフローチェックサムハッシュで、.NET Framework 4.7 () の既定値として導入された SHA1 アルゴリズムを使用するか `true` 、.NET Framework 4.8 () で既定値として導入された既定の SHA256 アルゴリズムを使用するかどうかを制御 `false` します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.8|
|`Switch.System.Diagnostics.`<br/>`IgnorePortablePDBsInStackTraces`|移植可能な Pdb を使用するときにスタックトレースが取得するかどうかを制御します。ソースファイルと行情報を含めることができます。 `false`ソースファイルと行情報を含める場合は。それ以外の場合は `true` 。|.NET Framework 4.7.2|
|`Switch.System.Drawing.`<br/>`DontSupportPngFramesInIcons`|<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> <xref:System.Drawing.Icon> オブジェクトに PNG フレームが含まれている場合に、メソッドが例外をスローするかどうかを制御します。 詳細については、「[軽減策: Icon オブジェクトの PNG フレーム](../../../migration-guide/mitigation-png-frames-in-icon-objects.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Drawing.Text.`<br/>`DoNotRemoveGdiFontsResourcesFromFontCollection`|<xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType>メソッドによってコレクションに追加されたときにオブジェクトが正しく破棄されるかどうかを判断し <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType> ます。 `true`従来の動作を維持するには`false`すべてのプライベートフォントオブジェクトを破棄する場合は。 |.NET Framework 4.7.2|
|`Switch.System.Drawing.Printing.`<br>`OptimizePrintPreview`|のパフォーマンスを <xref:System.Windows.Forms.PrintPreviewDialog> ネットワークプリンター用に最適化するかどうかを制御します。 詳細については、「 [Printプレビューダイアログコントロールの概要](../../../winforms/controls/printpreviewdialog-control-overview-windows-forms.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Globalization.EnforceJapaneseEraYearRanges`|日本語の暦の時代 (年号) をチェックするかどうかを制御します。 `true`年範囲のチェックを強制する場合は `false` 。それを無効にする場合は (既定の動作)。 詳細については、「[カレンダーの操作](../../../../standard/datetime/working-with-calendars.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Globalization.EnforceLegacyJapaneseDateParsing`|解析操作で、"1" だけを日本語の暦時代 (年号) の最初の年として認識するかどうかを制御します。 `true`"1" だけを認識する場合は。`false`"1" またはガント (既定の動作) のいずれかを認識します。 詳細については、「[カレンダーの操作](../../../../standard/datetime/working-with-calendars.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Globalization.FormatJapaneseFirstYearAsANumber`|日本語の暦時代 (年号) の最初の年を、書式設定操作で "1" または "ガント" として表示するかどうかを制御します。 `true`時代 (年号) の最初の年を "1" として書式設定するには、`false`(既定の動作) として書式設定します。 詳細については、「[カレンダーの操作](../../../../standard/datetime/working-with-calendars.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Globalization.NoAsyncCurrentCulture`|非同期操作が呼び出し元スレッドのコンテキストからフローされないかどうかを制御します。 詳細については、「[タスク間の CurrentCulture と CurrentUICulture flow](../../../migration-guide/retargeting/4.5.2-4.6.md#currentculture-and-currentuiculture-flow-across-tasks)」を参照してください。|.NET Framework 4.6|
|`Switch.System.IdentityModel.`<br/>`DisableMultipleDNSEntriesInSANCertificate`|<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType>メソッドが要求の種類と最後の DNS エントリのみを照合するかどうかを制御します。 詳細については、「[軽減策: X509CertificateClaimSet.FindClaims メソッド](../../../migration-guide/mitigation-x509certificateclaimset-findclaims-method.md)」を参照してください。|.NET Framework 4.6.1|
|`Switch.System.IdentityModel.`<br/>`EnableCachedEmptyDefaultAuthorizationContext`|AuthorizationContext. Empty を使用して変更可能なオブジェクトを返すかどうかを制御します。|.NET Framework 4.6|
|`Switch.System.IO.BlockLongPaths`|よりも長いパス `MAX_PATH` (260 文字) がをスローするかどうかを制御 <xref:System.IO.PathTooLongException> します。 詳細については、「[長いパスのサポート](../../../migration-guide/retargeting/4.6.1-4.6.2.md#long-path-support)」を参照してください。|.NET Framework 4.6.2|
|`Switch.System.IO.Compression.`<br/>`DoNotUseNativeZipLibraryForDecompression`|クラスによる展開にネイティブ OS ルーチンを使用するかどうかを制御 <xref:System.IO.Compression.DeflateStream> します。 `false`ネイティブ Api を使用するには`true`実装を使用する場合は <xref:System.IO.Compression.DeflateStream> 。|.NET Framework 4.7.2|
|`Switch.System.IO.Compression.ZipFile.`<br/>`UseBackslash`|は、スラッシュ (" \\ /") ではなく円記号 ("") をプロパティのパス区切り記号として使用し <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> ます。 詳細については、「[軽減策: ZipArchiveEntry パス区切り記号](../../../migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md)」を参照してください。|.NET Framework 4.6.1|
|`Switch.System.IO.Ports.`<br/>`DoNotCatchSerialStreamThreadExceptions`|ストリームで作成されたバックグラウンドスレッドでスローされるオペレーティングシステムの例外がプロセスを終了するかどうかを制御 <xref:System.IO.Ports.SerialPort> します。|.NET Framework 4.7.1|
|`Switch.System.IO.`<br/>`UseLegacyPathHandling`|従来のパスの正規化を使用するかどうか、およびメソッドとメソッドで URI パスをサポートするかどうかを制御し <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> ます。 詳細については、「[軽減策: パスの正規化](../../../migration-guide/mitigation-path-normalization.md)と[軽減策: パスのコロンチェック](../../../migration-guide/mitigation-path-colon-checks.md)」を参照してください。|.NET Framework 4.6.2|
|`Switch.System.`<br/>`MemberDescriptorEqualsReturnsFalseIfEquivalent`|等しいかどうかのテストが、 <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=nameWithType> 1 つのオブジェクトのプロパティを <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=nameWithType> 2 番目のオブジェクトのプロパティと比較するかどうかを制御します。 詳細については、「 [MemberDescriptor の不適切な実装](../../../migration-guide/retargeting/4.6.1-4.6.2.md#incorrect-implementation-of-memberdescriptorequals)」を参照してください。|.NET Framework 4.6.2|
 `Switch.System.Net.`<br/>`DontCheckCertificateEKUs`|証明書の拡張キー使用法 (EKU) の検証を無効にします。 EKU (拡張キー使用法) 拡張は、キーを使用するアプリケーションを示すオブジェクト識別子 (OID) の集まりです。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchSendAuxRecord`|SCH_SEND_AUX_RECORD の使用を無効にすることで、SSL/TLS (利用) の軽減策に対する TLS 1.0 ブラウザーの悪用を無効にします。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchUseStrongCrypto`|<xref:System.Net.ServicePointManager?displayProperty=nameWithType>および <xref:System.Net.Security.SslStream?displayProperty=nameWithType> クラスが SSL 3.0 プロトコルを使用できるかどうかを制御します。 詳細については、「[軽減策: TLS プロトコル](../../../migration-guide/mitigation-tls-protocols.md)」を参照してください。|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSystemDefaultTlsVersions`|既定の Tls12、Tls11、Tls に戻す SystemDefault TLS のバージョンを無効にします。|.NET Framework 4.7|
|`Switch.System.Net.`<br/>`DontEnableTlsAlerts`|System.net.security.sslstream TLS サーバー側アラートを無効にします。|.NET Framework 4.7|
|`Switch.System.Runtime.InteropServices.`<br/>`DoNotMarshalOutByrefSafeArrayOnInvoke`|COM 相互運用イベントの ByRef SafeArray パラメーターがネイティブコードにマーシャリング `false` されるか ()、またはネイティブコードへのマーシャリングが無効になるか () を制御 `true` します。|.NET Framework 4.8|
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseECMAScriptV6EscapeControlCharacter` |[DataContractJsonSerializer](xref:System.Runtime.Serialization.Json.DataContractJsonSerializer)が ECMAScript V6 と V8 標準に基づいて一部の制御文字をシリアル化するかどうかを制御します。 詳細については、「[軽減策: DataContractJsonSerializer での制御文字のシリアル化](../../../migration-guide/mitigation-serialization-control-characters.md)」を参照してください。| .NET Framework 4.7 |
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseTimeZoneInfo`|で複数の調整をサポートするか、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> タイムゾーンに対して1つの調整のみをサポートするかを制御します。 `true`の場合、型を使用して <xref:System.TimeZoneInfo> 日付と時刻のデータをシリアル化および逆シリアル化します。それ以外の場合は、 <xref:System.TimeZone> 複数の調整規則をサポートしていない型を使用します。|.NET Framework 4.6.2|
|`Switch.System.Runtime.Serialization.UseNewMaxArraySize`|が <xref:System.Runtime.Serialization.ObjectManager?displayProperty=nameWithType> オブジェクトのシリアル化と逆シリアル化の間に、より大きな配列サイズを使用するかどうかを制御します。 `true`などの型によってラージオブジェクトグラフのシリアル化と逆シリアル化のパフォーマンスを向上させるには、このスイッチをに設定し <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> ます。 |.NET Framework 4.7.2|
|`Switch.System.Security.ClaimsIdentity.`<br/>`SetActorAsReferenceWhenCopyingClaimsIdentity`|<xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29>コンストラクターが新しいオブジェクトのプロパティに既存のオブジェクト参照を設定するかどうか <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=nameWithType> を制御します。 詳細については、「[軽減策: ClaimsIdentity コンストラクター](../../../migration-guide/retargeting/4.6.1-4.6.2.md)」を参照してください。|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`AesCryptoServiceProvider.DontCorrectlyResetDecryptor`|復号化を再利用しようとしたがをスローするかどうかを制御 <xref:System.Security.Cryptography.AesCryptoServiceProvider> <xref:System.Security.Cryptography.CryptographicException> します。 詳細については、「 [AesCryptoServiceProvider の復号化による再利用可能な変換の提供](../../../migration-guide/retargeting/4.6.1-4.6.2.md#aescryptoserviceprovider-decryptor-provides-a-reusable-transform)」を参照してください。|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`DoNotAddrOfCspParentWindowHandle`|[Cspparameters.parentwindowhandle](xref:System.Security.Cryptography.CspParameters.ParentWindowHandle)プロパティの値が、ウィンドウハンドルのメモリ位置を表す[IntPtr](xref:System.IntPtr)であるか、またはウィンドウハンドル (HWND) であるかを制御します。 詳細については、「[Mitigation: CspParameters.ParentWindowHandle Expects an HWND](../../../migration-guide/retargeting/4.6.2-4.7.md#cspparametersparentwindowhandle-now-expects-hwnd-value)」 (軽減策: CspParameters.ParentWindowHandle で HWND を受け取る) を参照してください。 |.NET Framework 4.7|
|`Switch.System.Security.Cryptography.`<br/>`UseLegacyFipsThrow`|FIPS モードでマネージ暗号化クラスを使用するかどうかを制御し <xref:System.Security.Cryptography.CryptographicException> `true` ます ()。または、システムライブラリ () の実装に依存し `false` ます。|.NET Framework 4.8|
|`Switch.System.Security.Cryptography.Pkcs.`<br/>`UseInsecureHashAlgorithms`|一部の SignedCMS 操作の既定値が SHA1 または SHA256 であるかどうかを判断します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.1|
|`Switch.System.Security.Cryptography.X509Certificates.`<br/>`ECDsaCertificateExtensions.UseLegacyPublicKeyReader`|<xref:System.Security.Cryptography.X509Certificates.ECDsaCertificateExtensions.GetECDsaPublicKey%2A?displayProperty=nameWithType>オペレーティングシステムでサポートされているすべての名前付き曲線 () を正しく処理するか、 `false` レガシ動作に戻すかを制御します。|.NET Framework 4.8|
|`Switch.System.Security.Cryptography.Xml.`<br/>`UseInsecureHashAlgorithms`|一部の SignedXML 操作の既定値が SHA1 または SHA256 であるかどうかを判断します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`AllowUnsignedToHeader`|`TransportWithMessageCredential`セキュリティモードで、署名されていない "to" ヘッダーを持つメッセージを許可するかどうかを決定します。 これはオプトインスイッチです。 詳細については、「 [.NET Framework 4.6.1 におけるランタイムの変更点](../../../migration-guide/runtime/4.5.2-4.6.1.md#windows-communication-foundation-wcf)」を参照してください。|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableAddressHeaderCollectionValidation`>|<xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})>要素のいずれかがの場合に、コンストラクターがをスローするかどうかを制御 <xref:System.ArgumentException> `null` します。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br />`DisableCngCertificates`|.CSG キー記憶域プロバイダーで X509 証明書を使用しようとしたときに例外がスローされるかどうかを判断します。 詳細については、「 [WCF トランスポートセキュリティで CNG を使用して格納される証明書をサポート](../../../migration-guide/retargeting/4.6.1-4.6.2.md#wcf-transport-security-supports-certificates-stored-using-cng)する」を参照してください|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableExplicitConnectionCloseHeader`|自己ホスト型サービスで HTTP トランスポートを使用する場合、この値をに設定すると、 `true` `Connection: close` 要求の応答ヘッダーにヘッダーを追加するアプリケーションが WCF によって無視されます。 この値をに設定すると、 `false` 応答ヘッダーにヘッダーを追加できるようになります。これにより `Connection: close` 、応答の送信後に要求ソケットが閉じられます。|.NET Framework 4.6|
|`Switch.System.ServiceModel.`<br/>`DisableOperationContextAsyncFlow`|再入可能サービスのインスタンスを一度に1つの実行スレッドに制限することによって発生するデッドロックを処理します。|.NET Framework 4.6.2|
|`Switch.System.ServiceModel.`<br/>`DisableUsingServicePointManagerSecurityProtocols`|と共に `Switch.System.Net.DontEnableSchUseStrongCrypto` 、WCF メッセージセキュリティが tls 1.1 と tls 1.2 を使用するかどうかを決定します。|.NET Framework 4.7 |
|`Switch.System.ServiceModel.`<br/>`DontEnableSystemDefaultTlsVersions`|の値は、 `false` オペレーティングシステムがプロトコルを選択できるようにするための既定の構成を設定します。 値をに設定すると、 `true` 既定値が使用可能な最も高いプロトコルに設定されます。 (以前のバージョンの framework のサービスブランチでも利用可能)|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InMsmqEncryptionAlgorithm`|WCF の MSMQ メッセージの既定のメッセージ署名アルゴリズムが SHA1 であるか SHA256 であるかを判断します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InPipeConnectionGetHashAlgorithm`|WCF が SHA1 または SHA256 ハッシュを使用して名前付きパイプのランダムな名前を生成するかどうかを制御します。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.Internals`<br/>`IncludeNullExceptionMessageInETWTrace`|例外メッセージが null の場合に[NullReferenceException](xref:System.NullReferenceException)をスローするかどうかを制御します。|.NET Framework 4.7|
|`Switch.System.ServiceProcess.`<br/>`DontThrowExceptionsOnStart`|サービスの起動時にスローされる例外がメソッドの呼び出し元に反映されるかどうかを制御 <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> します。|.NET Framework 4.7.1|
|`Switch.System.Threading.UseNetCoreTimer`|<xref:System.Threading.Timer>インスタンスが大規模な環境でパフォーマンスの向上を利用できるかどうかを制御します。 の場合、 `true` パフォーマンスの向上が有効になります。 `false` (既定値) の場合は無効になります。|.NET Framework 4.8|
|`Switch.System.Uri.`<br/>`DontEnableStrictRFC3986ReservedCharacterSets`|デコードされた可能性がある特定のパーセントエンコード文字が一貫してエンコードされているかどうかを判断します。 `true`の場合は、デコードされます。それ以外の場合は `false` 。|.NET Framework 4.7.2|
|`Switch.System.Uri.`<br/>`DontKeepUnicodeBidiFormattingCharacters`|Uri での Unicode の双方向文字の処理を決定します。 `true`Uri から削除するには`false`を保持し、パーセントエンコードします。|.NET Framework 4.7.2|
|`Switch.System.Windows.Controls.Grid.`<br/>`StarDefinitionsCanExceedAvailableSpace` |Windows Presentation Foundation が古いアルゴリズム () を適用するか `true` 、または新しいアルゴリズム () を適用して `false` 領域を列に割り当てるかを決定し \* ます。 詳細については、「[Mitigation: Grid Control's Space Allocation to Star-columns](../../../migration-guide/retargeting/4.6.2-4.7.md#wpf-grid-allocation-of-space-to-star-columns)」 (軽減策: グリッド コントロールの *-column へのディスク領域の割り当て) を参照してください。 |.NET Framework 4.7 |
|`Switch.System.Windows.Controls.TabControl.`<br/>`SelectionPropertiesCanLagBehindSelectionChangedEvent`|選択変更イベントを発生させる前に、セレクターまたはタブコントロールが、選択した値プロパティの値を常に更新するかどうかを制御します。|.NET Framework 4.7.1|
|`Switch.System.Windows.Controls.Text.`<br/>`UseAdornerForTextboxSelectionRendering`|Occluded text () を防ぐために、コントロールおよびコントロールに対して非装飾ベースの選択のレンダリングを使用できるかどうかを決定し <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.PasswordBox> `false` ます。または、テキストを装飾層 () でのみ表示するかどうかを指定し `true` ます。|.NET Framework 4.7.2|
|`Switch.System.Windows.Data.Binding.`<br/>`IListIndexerHidesCustomIndexer`|カスタム IList インデクサーをクラスによって正しく使用しない ( `true` ) か、または正しく () 使用するかを制御し `false` <xref:System.Windows.Data.Binding?displayProperty=nameWithType> ます。|.NET Framework 4.8|
|`Switch.System.Windows.DoNotScaleForDpiChanges`|DPI の変更がシステムごと (の値 `false` ) またはモニター単位 (の値) のどちらで行われるかを決定し `true` ます。|.NET Framework 4.6.2|
|`Switch.System.Windows.`<br/>`DoNotUsePresentationDpiCapabilityTier2OrGreater`|WPF がモニターごとに認識されるモードで実行されるときに、内のコントロールのサイズ変更を改善するかどうかを制御 <xref:System.Windows.Interop.HwndHost?displayProperty=nameWithType> `true` します () または有効 ( `false` )。|.NET Framework 4.8|
|`Switch.System.Windows.Forms.`<br/>`DomainUpDown.UseLegacyScrolling`|コントロールテキストが存在する場合に、開発者がアクションを特別に処理する必要があるかどうかを判断し <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> ます。 `true`アクションを処理する <xref:System.Windows.Forms.DomainUpDown.UpButton> 場合は。 `false` <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> と <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> アクションが適切に同期される場合は。|.NET Framework 4.7.2|
|`Switch.System.Windows.Forms.`<br />`DontSupportReentrantFilterMessage`|<xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType>メソッドが呼び出されたときに例外がスローされることなく、カスタム実装がメッセージを安全にフィルター処理できるようにするコードを選択し <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> ます。 詳細については、[「軽減策: カスタムの IMessageFilter.PreFilterMessage 実装」](../../../migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md)を参照してください。|.NET Framework 4.6.1|
|`Switch.System.Windows.Forms.`<br/>`UseLegacyContextMenuStripSourceControlValue`|<xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType>ユーザーが入れ子になったコントロールからメニューを開いたときに、プロパティがソース管理を返すかどうかを決定し <xref:System.Windows.Forms.ToolStripMenuItem> ます。 `true``null`従来の動作を返す場合は。 `false` ソース管理を返す場合は。|.NET Framework 4.7.2|
|`Switch.System.Windows.Forms.UseLegacyToolTipDisplay`|ツールヒントの呼び出しサポートを無効 ( `true` ) または有効 () にするかどうかを制御 `false` します。 ツールヒントの呼び出しサポートを有効にするには、、、およびで定義されている従来のユーザー補助機能も必要 `Switch.UseLegacyAccessibilityFeatures` `Switch.UseLegacyAccessibilityFeatures.2` となり `Switch.UseLegacyAccessibilityFeatures.3` ます (に設定 `false` )。|.NET Framework 4.8|
|`Switch.System.Windows.Input.Stylus.`<br/>`EnablePointerSupport`|`WM_POINTER`WPF アプリケーションでオプションベースのタッチ/スタイラススタックを有効にするかどうかを決定します。 詳細については、「[軽減策: ポインターベースのタッチおよびスタイラスのサポート](../../../migration-guide/mitigation-pointer-based-touch-and-stylus-support.md)」を参照してください。|.NET Framework 4.7|
|`Switch.System.Windows.Markup.`<br/>`DoNotUseSha256ForMarkupCompilerChecksumAlgorithm`|チェックサムに使用される既定のハッシュアルゴリズムが SHA256 () または SHA1 () であるかどうかを判断し `false` `true` ます。<br>SHA1 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.7.2|
|`Switch.System.Windows.Media.ImageSourceConverter.`<br/>`OverrideExceptionWithNullReferenceException`|例外の原因 ( [DirectoryNotFoundException](xref:System.IO.DirectoryNotFoundException)や[FileNotFoundException](xref:System.IO.FileNotFoundException)など) をより具体的に示す例外の代わりに、レガシ[NullReferenceException](xref:System.NullReferenceException)をスローするかどうかを制御します。 これは、 [NullReferenceException](xref:System.NullReferenceException)の処理に依存するコードによって使用されることを意図しています。 | .NET Framework 4.7 |
|`Switch.System.Workflow.ComponentModel.`<br/>`UseLegacyHashForXomlFileChecksum`|ワークフロープロジェクトビルド内の XOML ファイルのチェックサムハッシュが MD5 アルゴリズム () を使用するかどうか `true` 、または .NET Framework 4.8 で既定値として導入された SHA256 アルゴリズムを使用するかどうかを制御します。<br>MD5 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.8|
|`Switch.System.Workflow.Runtime.`<br/>`UseLegacyHashForSqlTrackingCacheKey`|SqlTrackingService によるチェックサムハッシュで、キャッシュされた文字列に MD5 アルゴリズム () を使用するか `true` 、.NET Framework 4.8 で既定値として導入される SHA256 アルゴリズムを使用するかどうかを制御します。<br>MD5 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.8|
|`Switch.System.Workflow.Runtime.`<br/>`UseLegacyHashForWorkflowDefinitionDispenserCacheKey`|ワークフローランタイムによるチェックサムハッシュが、キャッシュされたワークフロー定義に MD5 アルゴリズム () を使用するかどうか `true` 、または .NET Framework 4.8 で既定値として導入された SHA256 アルゴリズムを使用するかどうかを制御します。<br>MD5 との競合問題のため、Microsoft では SHA256 を推奨しています。|.NET Framework 4.8|
|`Switch.UseLegacyAccessibilityFeatures`|.NET Framework 4.7.1 で使用できるユーザー補助機能を有効にするか無効にするかを制御します。 | .NET Framework 4.7.1 |
|`Switch.UseLegacyAccessibilityFeatures.2`|.NET Framework 4.7.2 で使用できるユーザー補助機能を有効にするかどうかを制御 `false` します () または disabled ( `true` )。 の場合は `true` 、 `Switch.UseLegacyAccessibilityFeatures` `true` .NET Framework 4.7.1 アクセシビリティ機能も有効にする必要があります。|.NET Framework 4.7.2|
|`Switch.UseLegacyAccessibilityFeatures.3`|.NET Framework 4.8 で導入されたユーザー補助機能が有効かどうかを制御 `false` します ()。または disabled ( `true` )。 `true`の場合、 `Switch.UseLegacyAccessibilityFeatures` および `Switch.UseLegacyAccessibilityFeatures.2` もである必要があり `true` ます。|.NET Framework 4.8|
|`Switch.UseLegacyToolTipDisplay`|WPF コントロール () の上にマウスカーソルを置いたときにツールヒントを表示するか `true` 、キーボードフォーカスとキーボードショートカットキー (既定の動作) の両方に表示するかを制御 `false` します。 .NET Framework 4.8 で実行され、以前のバージョンの .NET Framework を対象とするアプリケーションでは、キーボードフォーカスとショートカットキーのサポートの両方を有効にするには `Switch.UseLegacyAccessibilityFeatures` 、、 `Switch.UseLegacyAccessibilityFeatures.2` 、および `Switch.UseLegacyAccessibilityFeatures.3` すべてをに設定する必要があり `false` ます。|.NET Framework 4.8|
|`Switch.System.Xml.`<br />`IgnoreEmptyKeySequences`|複合キーの空のキーシーケンスが XSD スキーマ検証によって無視されるかどうかを制御します。 詳細については、「[軽減策: XML スキーマ検証](../../../migration-guide/mitigation-xml-schema-validation.md)」を参照してください。|.NET Framework 4.6|

> [!NOTE]
> アプリケーション構成ファイルに要素を追加する代わりに、 `AppContextSwitchOverrides` `static` (C# の場合) または `Shared` (Visual Basic) メソッドを呼び出すことによって、スイッチをプログラムで設定することもでき <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> ます。

 ライブラリ開発者はカスタムスイッチを定義して、新しいバージョンのライブラリで導入された機能の変更を呼び出し元がオプトアウトできるようにすることもできます。 詳細については、<xref:System.AppContext> クラスを参照してください。

## <a name="switches-in-aspnet-apps"></a>ASP.NET アプリのスイッチ

Web.config [\<Add>](../appsettings/add-element-for-appsettings.md) ファイルのセクションに要素を追加することにより、互換性設定を使用するように ASP.NET アプリケーションを構成でき [\<appSettings>](../appsettings/index.md) ます。

次の例では、要素を使用して、web.config `<add>` ファイルのセクションに2つの設定を追加して `<appSettings>` います。

```xml
<appSettings>
  <add key="AppContext.SetSwitch:Switch.System.Globalization.NoAsyncCurrentCulture" value="true" />
  <add key="AppContext.SetSwitch:Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets" value="true" />
</appSettings>
```

## <a name="example"></a>例

 次の例では、要素を使用して `AppContextSwitchOverrides` 単一のアプリケーション互換性スイッチを定義し `Switch.System.Globalization.NoAsyncCurrentCulture` ています。これにより、非同期メソッド呼び出しのスレッド間でカルチャをフローできなくなります。

```xml
<configuration>
   <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />
   </runtime>
</configuration>
```

 次の例では、要素を使用し `AppContextSwitchOverrides` て、とという2つのアプリケーション互換性スイッチを定義し `Switch.System.Globalization.NoAsyncCurrentCulture` `Switch.System.IO.BlockLongPaths` ます。 2つの名前と値のペアはセミコロンで区切られます。

```xml
<configuration>
    <runtime>
       <AppContextSwitchOverrides
          value="Switch.System.Globalization.NoAsyncCurrentCulture=true;Switch.System.IO.BlockLongPaths=true" />
    </runtime>
</configuration>
```

## <a name="see-also"></a>関連項目

- [.NET Framework 4.6 以降の新しい動作を抑制する](../../../migration-guide/mitigations.md)
- <xref:System.AppContext?displayProperty=nameWithType>
- [\<runtime>Element](runtime-element.md)
- [\<configuration>Element](../configuration-element.md)
