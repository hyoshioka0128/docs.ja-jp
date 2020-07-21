---
title: CBC 復号化の脆弱性
description: パディングを使用した暗号ブロックチェーン (CBC) モード対称復号化を使用してタイミングの脆弱性を検出し、軽減する方法を説明します。
ms.date: 06/12/2018
author: blowdart
ms.openlocfilehash: 47520ea4c9c7d0ef4d79378c93c6ce1f2ba7dd6d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186094"
---
# <a name="timing-vulnerabilities-with-cbc-mode-symmetric-decryption-using-padding"></a>パディングを使用した CBC モードの対称復号化に関するタイミングの脆弱性

マイクロソフトは、検証可能なパディングが適用された場合、暗号化テキストの整合性を最初に確保せずに、対称暗号化の暗号ブロックチェーン (CBC) モードで暗号化されたデータを復号化することはもはや安全ではないと考えています。状況。 この判断は、現在知られている暗号研究に基づいています。

## <a name="introduction"></a>はじめに

パディング Oracle 攻撃は、暗号化されたデータに対する攻撃の一種であり、攻撃者はキーを知らなくてもデータの内容を解読できます。

オラクルとは、実行しているアクションが正しいかどうかに関する情報を攻撃者に提供する「tell」を指します。 子供と一緒にボードやカードゲームをプレイ想像してみてください。 彼らが良い動きをしようとしていると思うので、彼らの顔が満面の笑みで点灯するとき、それはオラクルです。 対戦相手として、このオラクルを使用して次の動きを適切に計画することができます。

パディングは特定の暗号用語です。 データの暗号化に使用されるアルゴリズムである暗号の中には、各ブロックが固定サイズのデータブロックで機能するものもあります。 暗号化するデータがブロックを埋めるのに適切なサイズでない場合、データは埋め込まれます。 多くの形式のパディングでは、元の入力が適切なサイズであった場合でも、常に埋め込みが必要です。 これにより、暗号化解除時にパディングを常に安全に削除できます。

2 つの事項を組み合わせると、Oracle を埋め込むソフトウェア実装によって、暗号化解除されたデータに有効なパディングがあるかどうかが明らかになります。 oracle は、「無効な埋め込み」と言う値を返す単純なものや、無効なブロックではなく、有効なブロックを処理するのに、測定可能な異なる時間を取るような複雑な何かである可能性があります。

ブロックベースの暗号には、モードと呼ばれる別のプロパティがあり、最初のブロックのデータと 2 番目のブロックのデータとの関係が決定されます。 最も一般的に使用されるモードの 1 つは CBC です。 CBC は初期化ベクトル (IV) と呼ばれる初期のランダム ブロックを導入し、前のブロックと静的暗号化の結果を組み合わせて、同じキーで同じメッセージを暗号化しても必ずしも同じ暗号化出力が生成されないようになっています。

攻撃者は、パディング オラクルと CBC データの構造を組み合わせて使用して、わずかに変更されたメッセージを Oracle を公開するコードに送信し、Oracle からデータが正しいことを伝えるまでデータを送信し続けることができます。 この応答から、攻撃者はメッセージバイトをバイト単位で解読できます。

最近のコンピュータ ネットワークは、攻撃者がリモート システムでの実行時間の差を非常に小さく (0.1 ミリ秒未満) 検出できるような高品質のネットワークです。データが改ざんされていない場合にのみ、正常な復号化が発生すると想定されているアプリケーションは、復号化の成功と失敗の違いを観察するように設計されたツールからの攻撃に対して脆弱である可能性があります。 このタイミングの違いは、他の言語やライブラリよりも重要な場合もありますが、アプリケーションの障害への対応を考慮すると、すべての言語とライブラリにとって、これは実用的な脅威であると考えられています。

この攻撃は、暗号化されたデータを変更し、Oracle で結果をテストする機能に依存します。 攻撃を完全に軽減する唯一の方法は、暗号化されたデータに対する変更を検出し、そのデータに対する操作の実行を拒否することです。 これを行う標準的な方法は、データの署名を作成し、操作が実行される前にその署名を検証することです。 署名は検証可能でなければならず、攻撃者が作成することはできません。 適切な署名の一般的な種類の 1 つは、キー付きハッシュ メッセージ認証コード (HMAC) と呼ばれます。 HMAC は、HMAC を作成するユーザーと検証するユーザーにのみ知られている秘密キーを受け取るという点で、チェックサムとは異なります。 キーを所有していない場合、正しい HMAC を生成することはできません。 データを受信したら、暗号化されたデータを取得し、自分と送信者の共有を使用して HMAC を個別に計算し、送信した HMAC を計算したデータと比較します。 この比較は一定の時間である必要があり、それ以外の場合は別の検出可能な oracle を追加して、別の種類の攻撃を許可します。

要約すると、埋め込まれた CBC ブロック暗号を安全に使用するには、データの復号化を試みる前に、一定の時間比較を使用して検証する HMAC (または別のデータ整合性チェック) と組み合わせる必要があります。 変更されたすべてのメッセージは応答を生成するのに同じ時間がかかるため、攻撃は防止されます。

## <a name="who-is-vulnerable"></a>脆弱なユーザー

この脆弱性は、独自の暗号化と復号化を実行しているマネージ アプリケーションとネイティブ アプリケーションの両方に適用されます。 これには、たとえば次のものが含まれます。

- サーバーで後で復号化するために Cookie を暗号化するアプリケーション。
- 後で列を復号化するテーブルにデータを挿入する機能をユーザーに提供するデータベース アプリケーション。
- 転送中のデータを保護するために共有キーを使用した暗号化に依存するデータ転送アプリケーション。
- TLS トンネル内でメッセージを暗号化および復号化するアプリケーション。

TLS を単独で使用しても、これらのシナリオでは保護されない場合があることに注意してください。

脆弱なアプリケーション:

- PKCS#7 や ANSI X.923 などの検証可能なパディング モードを使用して、CBC 暗号モードを使用してデータを復号化します。
- (MAC または非対称デジタル署名を介して) データ整合性チェックを実行せずに、復号化を実行します。

これは、暗号化メッセージ構文 (PKCS#7/CMS) EnvelopedData 構造体など、これらのプリミティブの上に抽象化の上に構築されたアプリケーションにも当てはまります。

## <a name="related-areas-of-concern"></a>関連する懸念事項

調査により、マイクロソフトは、メッセージが既知または予測可能なフッター構造を持つ場合に、ISO 10126 相当のパディングで埋め込まれた CBC メッセージについてさらに懸念を抱いています。 たとえば、W3C XML 暗号化の構文と処理の推奨事項 (xmlenc、EncryptedXml) の規則に従って作成されたコンテンツ。 メッセージに署名するための W3C ガイダンスでは、暗号化が適切であると考えられていたが、マイクロソフトでは、常に暗号化してから署名を行うことをお勧めします。

アプリケーション開発者は、非対称キーと任意のメッセージの間に固有の信頼関係がないため、非対称署名キーの適用性を常に確認する必要があります。

## <a name="details"></a>詳細

従来、HMAC や RSA 署名などの手段を使用して、重要なデータの暗号化と認証の両方が重要であるというコンセンサスがありました。 ただし、暗号化と認証操作の順序付け方法に関する明確なガイダンスは少なくてすんでいます。 この資料で詳しく説明している脆弱性のため、マイクロソフトのガイダンスでは、常に "暗号化して署名する" パラダイムを使用します。 つまり、最初に対称キーを使用してデータを暗号化し、次に暗号文(暗号化されたデータ)上で MAC または非対称署名を計算します。 データを復号化する場合は、逆の操作を行います。 まず、暗号文の MAC または署名を確認してから、暗号化を解除します。

「パディングオラクル攻撃」と呼ばれる脆弱性のクラスは、10年以上前から存在することが知られています。 これらの脆弱性により、攻撃者は、AES や 3DES などの対称ブロック アルゴリズムで暗号化されたデータを、データ ブロックあたり 4096 回を超える試行を使用して復号化できます。 これらの脆弱性は、ブロック暗号が最も頻繁に使用され、最後にデータをパディングする検証が可能であるという事実を利用します。 攻撃者が暗号化テキストを改ざんし、改ざんによって最後のパディングの形式でエラーが発生したかどうかを突き出した場合、攻撃者はデータを解読できることが判明しました。

最初は、パディングが有効かどうかに基づいて異なるエラー コードを返すサービスに基づいて攻撃ASP.NET攻撃を受[けた MS10-070](/security-updates/SecurityBulletins/2010/ms10-070)。 しかし、マイクロソフトは現在、有効なパディングと無効なパディングのタイミングの違いだけを使用して同様の攻撃を行うことを現実的であると考えています。

暗号化スキームが署名を採用し、(内容に関係なく) 所定の長さのデータの固定ランタイムで署名検証が実行されることを知って、データの整合性は[、サイドチャネル](https://en.wikipedia.org/wiki/Side-channel_attack)を介して攻撃者に情報を送信することなく検証することができます。 整合性チェックは改ざんされたメッセージを拒否するため、パディング Oracle の脅威は軽減されます。

## <a name="guidance"></a>ガイダンス

まず第一に、機密性を持つデータは、セキュア ソケット レイヤ (SSL) の後継であるトランスポート層セキュリティ (TLS) を介して送信する必要があります。

次に、アプリケーションを分析して次の処理を行います。

- 実行している暗号化と、使用しているプラットフォームと API によって提供される暗号化を正確に把握します。
- CBC モードでの AES や 3DES などの対称[ブロック暗号アルゴリズム](https://en.wikipedia.org/wiki/Block_cipher#Notable_block_ciphers)の各層での各使用法には、秘密鍵によるデータ整合性チェック (非対称署名、HMAC、または認証済み暗号化モードを GCM や CCM などの[認証済み暗号化](https://en.wikipedia.org/wiki/Authenticated_encryption)(AE) モードに変更する) が組み込まれているかどうか確認してください。

現在の調査によると、認証と暗号化の手順が非AE暗号化モードに対して独立して実行される場合、暗号文(暗号化してから署名)を認証することが最良の一般的な選択肢であると一般的に考えられています。 しかし、暗号化に対する万能の正解はなく、この一般化はプロの暗号学者からの指示されたアドバイスほど良くありません。

メッセージング形式を変更できないが、認証されていない CBC 復号化を実行するアプリケーションは、次のような緩和策を組み込むことをお勧めします。

- 復号化を許可せずに復号化し、パディングを検証または削除する:
  - 適用されたパディングは、アプリケーションに負担を移す必要があります。
  - 利点は、パディングの検証と削除を他のアプリケーション データ検証ロジックに組み込むことができるという利点があります。 パディング検証とデータ検証が一定時間で行える場合、脅威は減少します。
  - パディングの解釈は、知覚されるメッセージの長さを変更するので、このアプローチから発されるタイミング情報がまだあるかもしれません。
- 復号化パディング モードを ISO10126 に変更します。
  - ISO10126 復号化パディングは、PKCS7 暗号化パディングと ANSIX923 暗号化パディングの両方と互換性があります。
  - モードを変更すると、パディング・オラクルの知識がブロック全体ではなく 1 バイトに減ります。 ただし、コンテンツに XML 要素の終了など、既知のフッターがある場合、関連する攻撃は引き続きメッセージの残りの部分を攻撃できます。
  - また、攻撃者が同じプレーンテキストを異なるメッセージ オフセットで複数回暗号化する可能性がある場合でも、プレーンテキストの回復を防止することはできません。
- タイミング信号を減衰させるために復号化コールの評価をゲートします。
  - ホールド時間の計算は、埋め込みを含むデータ セグメントに対して、復号化操作が必要とする最大時間を超える最小時間を持つ必要があります。
  - 時間の計算は[、(](/windows/desktop/sysinfo/acquiring-high-resolution-time-stamps)ロールオーバー/オーバーフローの対象となる)または2つのシステムタイムスタンプ(NTP調整エラー<xref:System.Environment.TickCount?displayProperty=nameWithType>の影響を受ける)を使用してではなく、高解像度タイムスタンプの取得のガイダンスに従って行う必要があります。
  - 時間計算には、マネージ アプリケーションまたは C++ アプリケーションで発生する可能性のあるすべての例外を含む、最後に埋め込まれたもの以外に、復号化操作を含める必要があります。
  - 成功または失敗がまだ決定されている場合、タイミング ゲートは、期限が切れたときに失敗を返す必要があります。
- 認証されていない復号化を実行しているサービスでは、"無効な" メッセージが大量に送信されたことを検出するために監視を行う必要があります。
  - このシグナルは、誤検知(正当に破損したデータ)と偽陰性(検出を回避するために十分に長い時間にわたって攻撃を広げる)の両方を運ぶことを覚えておいてください。

## <a name="finding-vulnerable-code---native-applications"></a>脆弱なコードを見つける - ネイティブ アプリケーション

Windows 暗号化: 次世代 (CNG) ライブラリに対してビルドされたプログラムの場合:

- 復号化の呼び出しは、フラグを指定する[BCryptDecrypt](/windows/desktop/api/bcrypt/nf-bcrypt-bcryptdecrypt)に対する呼び出しです`BCRYPT_BLOCK_PADDING`。
- キー ハンドルは[、BCryptSetProperty を](/windows/desktop/api/bcrypt/nf-bcrypt-bcryptsetproperty)呼び出して初期化`BCRYPT_CHAIN_MODE_CBC`[BCRYPT_CHAINING_MODE。](/windows/desktop/SecCNG/cng-property-identifiers#BCRYPT_CHAINING_MODE)
  - 既定`BCRYPT_CHAIN_MODE_CBC`では、影響を受けるコードに 対`BCRYPT_CHAINING_MODE`して値が割り当てられていない可能性があります。

古い Windows 暗号化 API に対してビルドされたプログラムの場合:

- 復号化の呼び出しは[、CryptDecrypt](/windows/desktop/api/wincrypt/nf-wincrypt-cryptdecrypt)とを使用します`Final=TRUE`。
- キー ハンドルは`CRYPT_MODE_CBC`[、cryptSetKeyParam](/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetkeyparam)を呼び出して初期化[KP_MODE](/windows/desktop/api/wincrypt/nf-wincrypt-cryptgetkeyparam)に設定されています。
  - 既定`CRYPT_MODE_CBC`では、影響を受けるコードに 対`KP_MODE`して値が割り当てられていない可能性があります。

## <a name="finding-vulnerable-code---managed-applications"></a>脆弱なコードを検出する - マネージ アプリケーション

- 復号化の呼び出しは、 <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor> <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor(System.Byte[],System.Byte[])>または<xref:System.Security.Cryptography.SymmetricAlgorithm?displayProperty=nameWithType>のメソッドに対して呼び出されます。
  - これには、.NET 内の次の派生型が含まれますが、サードパーティの型も含まれる場合があります。
    - <xref:System.Security.Cryptography.Aes>
    - <xref:System.Security.Cryptography.AesCng>
    - <xref:System.Security.Cryptography.AesCryptoServiceProvider>
    - <xref:System.Security.Cryptography.AesManaged>
    - <xref:System.Security.Cryptography.DES>
    - <xref:System.Security.Cryptography.DESCryptoServiceProvider>
    - <xref:System.Security.Cryptography.RC2>
    - <xref:System.Security.Cryptography.RC2CryptoServiceProvider>
    - <xref:System.Security.Cryptography.Rijndael>
    - <xref:System.Security.Cryptography.RijndaelManaged>
    - <xref:System.Security.Cryptography.TripleDES>
    - <xref:System.Security.Cryptography.TripleDESCng>
    - <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>
- プロパティ<xref:System.Security.Cryptography.SymmetricAlgorithm.Padding?displayProperty=nameWithType>は、 、 <xref:System.Security.Cryptography.PaddingMode.PKCS7?displayProperty=nameWithType> <xref:System.Security.Cryptography.PaddingMode.ANSIX923?displayProperty=nameWithType>、または<xref:System.Security.Cryptography.PaddingMode.ISO10126?displayProperty=nameWithType>に設定されています。
  - デフォルト<xref:System.Security.Cryptography.PaddingMode.PKCS7?displayProperty=nameWithType>であるため、影響を受けるコードがプロパティを<xref:System.Security.Cryptography.SymmetricAlgorithm.Padding?displayProperty=nameWithType>割り当てなかった可能性があります。
- プロパティ<xref:System.Security.Cryptography.SymmetricAlgorithm.Mode?displayProperty=nameWithType>は次の値に設定されました。<xref:System.Security.Cryptography.CipherMode.CBC?displayProperty=nameWithType>
  - デフォルト<xref:System.Security.Cryptography.CipherMode.CBC?displayProperty=nameWithType>であるため、影響を受けるコードがプロパティを<xref:System.Security.Cryptography.SymmetricAlgorithm.Mode?displayProperty=nameWithType>割り当てなかった可能性があります。

## <a name="finding-vulnerable-code---cryptographic-message-syntax"></a>脆弱なコードを見つける - 暗号メッセージの構文

暗号化されたコンテンツが AES の CBC モードを使用する認証されていない CMS EnvelopedData メッセージ (2.16.840.1.101.3.4.1.2,2.16.840.1.101.3.4.1.22、 2.16.840.1.101.3.4.4.42、DES (1.3.14.3.2.7)、3DES (1.2.840.113549.3.7)またはRC2 (1.2.840.113549.3.2)また、CBC モードで他のブロック暗号アルゴリズムを使用するメッセージも含まれます。

ストリーム暗号はこの特定の脆弱性の影響を受けにくいですが、マイクロソフトでは ContentEncryptionAlgorithm 値の検査を行う際に常にデータを認証することをお勧めします。

マネージ アプリケーションの場合、CMS EnvelopedData BLOB は、 に<xref:System.Security.Cryptography.Pkcs.EnvelopedCms.Decode(System.Byte[])?displayProperty=fullName>渡される任意の値として検出できます。

ネイティブ アプリケーションの場合、CMS EnvelopedData BLOB は、結果として[得られるCMSG_TYPE_PARAM](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsggetparam)`CMSG_ENVELOPED`が CryptMsgControl を介して命令を送信される[CryptMsgUpdate](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsgupdate) `CMSG_CTRL_DECRYPT`を介[CryptMsgControl](/windows/desktop/api/wincrypt/nf-wincrypt-cryptmsgcontrol)して CMS ハンドルに提供される任意の値として検出できます。

## <a name="vulnerable-code-example---managed"></a>脆弱なコード例 - マネージ

このメソッドは、Cookie を読み取って復号化しますが、データ整合性チェックは表示されません。 したがって、このメソッドによって読み取られる Cookie の内容は、その Cookie を受け取ったユーザー、または暗号化された Cookie 値を取得した攻撃者によって攻撃される可能性があります。

```csharp
private byte[] DecryptCookie(string cookieName)
{
    HttpCookie cookie = Request.Cookies[cookieName];

    if (cookie == null)
    {
        return null;
    }

    using (ICryptoTransform decryptor = _aes.CreateDecryptor())
    using (MemoryStream memoryStream = new MemoryStream())
    using (CryptoStream cryptoStream =
        new CryptoStream(memoryStream, decryptor, CryptoStreamMode.Write))
    {
        byte[] readCookie = Convert.FromBase64String(cookie.Value);
        cryptoStream.Write(readCookie, 0, readCookie.Length);
        cryptoStream.FlushFinalBlock();
        return memoryStream.ToArray();
    }
}
```

## <a name="example-code-following-recommended-practices---managed"></a>推奨されるプラクティスに従ったコード例 - マネージド

次のサンプル コードでは、標準以外のメッセージ形式を使用しています。

`cipher_algorithm_id || hmac_algorithm_id || hmac_tag || iv || ciphertext`

ここで、`cipher_algorithm_id`および`hmac_algorithm_id`アルゴリズム識別子は、それらのアルゴリズムのアプリケーションローカル (非標準) 表現です。 これらの識別子は、既存のメッセージング プロトコルの他の部分では、専用の連結バイト ストリームとしてではなく意味を持つ場合があります。

また、この例では、暗号化キーと HMAC キーの両方を派生させるために、単一のマスター キーを使用します。 これは、1 つのキーを使用したアプリケーションをデュアルキーアプリケーションに変換する場合と、2 つのキーを異なる値として保持することを推奨する利便性の両方として提供されます。 さらに、HMAC キーと暗号化キーが同期から外れることができないことを保証します。

このサンプルでは、暗号化または復号化<xref:System.IO.Stream>のどちらも受け入れません。 現在のデータ形式では、値が暗号化テキストの前`hmac_tag`にあるため、1 回の暗号化が困難になります。 ただし、この形式は、パーサーをシンプルにするために、固定サイズの要素をすべて最初に保持するため選択されました。 このデータ形式では、1 パス復号化が可能ですが、実装者は GetHashAndReset を呼び出し、TransformFinalBlock を呼び出す前に結果を検証するように注意してください。 ストリーミング暗号化が重要な場合は、別の AE モードが必要になる場合があります。

```csharp
// ==++==
//
//   Copyright (c) Microsoft Corporation.  All rights reserved.
//
//   Shared under the terms of the Microsoft Public License,
//   https://opensource.org/licenses/MS-PL
//
// ==--==

using System;
using System.Diagnostics;
using System.IO;
using System.Runtime.CompilerServices;
using System.Security.Cryptography;

namespace Microsoft.Examples.Cryptography
{
    public enum AeCipher : byte
    {
        Unknown,
        Aes256CbcPkcs7,
    }

    public enum AeMac : byte
    {
        Unknown,
        HMACSHA256,
        HMACSHA384,
    }

    /// <summary>
    /// Provides extension methods to make HashAlgorithm look like .NET Core's
    /// IncrementalHash
    /// </summary>
    internal static class IncrementalHashExtensions
    {
        public static void AppendData(this HashAlgorithm hash, byte[] data)
        {
            hash.TransformBlock(data, 0, data.Length, null, 0);
        }

        public static void AppendData(
            this HashAlgorithm hash,
            byte[] data,
            int offset,
            int length)
        {
            hash.TransformBlock(data, offset, length, null, 0);
        }

        public static byte[] GetHashAndReset(this HashAlgorithm hash)
        {
            hash.TransformFinalBlock(Array.Empty<byte>(), 0, 0);
            return hash.Hash;
        }
    }

    public static partial class AuthenticatedEncryption
    {
        /// <summary>
        /// Use <paramref name="masterKey"/> to derive two keys (one cipher, one HMAC)
        /// to provide authenticated encryption for <paramref name="message"/>.
        /// </summary>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <param name="message">The message to encrypt</param>
        /// <returns>
        /// A concatenation of
        /// [cipher algorithm+chainmode+padding][mac algorithm][authtag][IV][ciphertext],
        /// suitable to be passed to <see cref="Decrypt"/>.
        /// </returns>
        /// <remarks>
        /// <paramref name="masterKey"/> should be a 128-bit (or bigger) value generated
        /// by a secure random number generator, such as the one returned from
        /// <see cref="RandomNumberGenerator.Create()"/>.
        /// This implementation chooses to block deficient inputs by length, but does not
        /// make any attempt at discerning the randomness of the key.
        ///
        /// If the master key is being input by a prompt (like a password/passphrase)
        /// then it should be properly turned into keying material via a Key Derivation
        /// Function like PBKDF2, represented by Rfc2898DeriveBytes. A 'password' should
        /// never be simply turned to bytes via an Encoding class and used as a key.
        /// </remarks>
        public static byte[] Encrypt(byte[] masterKey, byte[] message)
        {
            if (masterKey == null)
                throw new ArgumentNullException(nameof(masterKey));
            if (masterKey.Length < 16)
                throw new ArgumentOutOfRangeException(
                    nameof(masterKey),
                    "Master Key must be at least 128 bits (16 bytes)");
            if (message == null)
                throw new ArgumentNullException(nameof(message));

            // First, choose an encryption scheme.
            AeCipher aeCipher = AeCipher.Aes256CbcPkcs7;

            // Second, choose an authentication (message integrity) scheme.
            //
            // In this example we use the master key length to change from HMACSHA256 to
            // HMACSHA384, but that is completely arbitrary. This mostly represents a
            // "cryptographic needs change over time" scenario.
            AeMac aeMac = masterKey.Length < 48 ? AeMac.HMACSHA256 : AeMac.HMACSHA384;

            // It's good to be able to identify what choices were made when a message was
            // encrypted, so that the message can later be decrypted. This allows for
            // future versions to add support for new encryption schemes, but still be
            // able to read old data. A practice known as "cryptographic agility".
            //
            // This is similar in practice to PKCS#7 messaging, but this uses a
            // private-scoped byte rather than a public-scoped Object IDentifier (OID).
            // Please note that the scheme in this example adheres to no particular
            // standard, and is unlikely to survive to a more complete implementation in
            // the .NET Framework.
            //
            // You may be well-served by prepending a version number byte to this
            // message, but may want to avoid the value 0x30 (the leading byte value for
            // DER-encoded structures such as X.509 certificates and PKCS#7 messages).
            byte[] algorithmChoices = { (byte)aeCipher, (byte)aeMac };
            byte[] iv;
            byte[] cipherText;
            byte[] tag;

            // Using our algorithm choices, open an HMAC (as an authentication tag
            // generator) and a SymmetricAlgorithm which use different keys each derived
            // from the same master key.
            //
            // A custom implementation may very well have distinctly managed secret keys
            // for the MAC and cipher, this example merely demonstrates the master to
            // derived key methodology to encourage key separation from the MAC and
            // cipher keys.
            using (HMAC tagGenerator = GetMac(aeMac, masterKey))
            {
                using (SymmetricAlgorithm cipher = GetCipher(aeCipher, masterKey))
                using (ICryptoTransform encryptor = cipher.CreateEncryptor())
                {
                    // Since no IV was provided, a random one has been generated
                    // during the call to CreateEncryptor.
                    //
                    // But note that it only does the auto-generation once. If the cipher
                    // object were used again, a call to GenerateIV would have been
                    // required.
                    iv = cipher.IV;

                    cipherText = Transform(encryptor, message, 0, message.Length);
                }

                // The IV and ciphertest both need to be included in the MAC to prevent
                // tampering.
                //
                // By including the algorithm identifiers, we have technically moved from
                // simple Authenticated Encryption (AE) to Authenticated Encryption with
                // Additional Data (AEAD). By including the algorithm identifiers in the
                // MAC, it becomes harder for an attacker to change them as an attempt to
                // perform a downgrade attack.
                //
                // If you've added a data format version field, it can also be included
                // in the MAC to further inhibit an attacker's options for confusing the
                // data processor into believing the tampered message is valid.
                tagGenerator.AppendData(algorithmChoices);
                tagGenerator.AppendData(iv);
                tagGenerator.AppendData(cipherText);
                tag = tagGenerator.GetHashAndReset();
            }

            // Build the final result as the concatenation of everything except the keys.
            int totalLength =
                algorithmChoices.Length +
                tag.Length +
                iv.Length +
                cipherText.Length;

            byte[] output = new byte[totalLength];
            int outputOffset = 0;

            Append(algorithmChoices, output, ref outputOffset);
            Append(tag, output, ref outputOffset);
            Append(iv, output, ref outputOffset);
            Append(cipherText, output, ref outputOffset);

            Debug.Assert(outputOffset == output.Length);
            return output;
        }

        /// <summary>
        /// Reads a message produced by <see cref="Encrypt"/> after verifying it hasn't
        /// been tampered with.
        /// </summary>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <param name="cipherText">
        /// The output of <see cref="Encrypt"/>: a concatenation of a cipher ID, mac ID,
        /// authTag, IV, and cipherText.
        /// </param>
        /// <returns>The decrypted content.</returns>
        /// <exception cref="ArgumentNullException">
        /// <paramref name="masterKey"/> is <c>null</c>.
        /// </exception>
        /// <exception cref="ArgumentNullException">
        /// <paramref name="cipherText"/> is <c>null</c>.
        /// </exception>
        /// <exception cref="CryptographicException">
        /// <paramref name="cipherText"/> identifies unknown algorithms, is not long
        /// enough, fails a data integrity check, or fails to decrypt.
        /// </exception>
        /// <remarks>
        /// <paramref name="masterKey"/> should be a 128-bit (or larger) value
        /// generated by a secure random number generator, such as the one returned from
        /// <see cref="RandomNumberGenerator.Create()"/>. This implementation chooses to
        /// block deficient inputs by length, but doesn't make any attempt at
        /// discerning the randomness of the key.
        ///
        /// If the master key is being input by a prompt (like a password/passphrase),
        /// then it should be properly turned into keying material via a Key Derivation
        /// Function like PBKDF2, represented by Rfc2898DeriveBytes. A 'password' should
        /// never be simply turned to bytes via an Encoding class and used as a key.
        /// </remarks>
        public static byte[] Decrypt(byte[] masterKey, byte[] cipherText)
        {
            // This example continues the .NET practice of throwing exceptions for
            // failures. If you consider message tampering to be normal (and thus
            // "not exceptional") behavior, you may like the signature
            // bool Decrypt(byte[] messageKey, byte[] cipherText, out byte[] message)
            // better.
            if (masterKey == null)
                throw new ArgumentNullException(nameof(masterKey));
            if (masterKey.Length < 16)
                throw new ArgumentOutOfRangeException(
                    nameof(masterKey),
                    "Master Key must be at least 128 bits (16 bytes)");
            if (cipherText == null)
                throw new ArgumentNullException(nameof(cipherText));

            // The format of this message is assumed to be public, so there's no harm in
            // saying ahead of time that the message makes no sense.
            if (cipherText.Length < 2)
            {
                throw new CryptographicException();
            }

            // Use the message algorithm headers to determine what cipher algorithm and
            // MAC algorithm are going to be used. Since the same Key Derivation
            // Functions (KDFs) are being used in Decrypt as Encrypt, the keys are also
            // the same.
            AeCipher aeCipher = (AeCipher)cipherText[0];
            AeMac aeMac = (AeMac)cipherText[1];

            using (SymmetricAlgorithm cipher = GetCipher(aeCipher, masterKey))
            using (HMAC tagGenerator = GetMac(aeMac, masterKey))
            {
                int blockSizeInBytes = cipher.BlockSize / 8;
                int tagSizeInBytes = tagGenerator.HashSize / 8;
                int headerSizeInBytes = 2;
                int tagOffset = headerSizeInBytes;
                int ivOffset = tagOffset + tagSizeInBytes;
                int cipherTextOffset = ivOffset + blockSizeInBytes;
                int cipherTextLength = cipherText.Length - cipherTextOffset;
                int minLen = cipherTextOffset + blockSizeInBytes;

                // Again, the minimum length is still assumed to be public knowledge,
                // nothing has leaked out yet. The minimum length couldn't just be calculated
                // without reading the header.
                if (cipherText.Length < minLen)
                {
                    throw new CryptographicException();
                }

                // It's very important that the MAC be calculated and verified before
                // proceeding to decrypt the ciphertext, as this prevents any sort of
                // information leaking out to an attacker.
                //
                // Don't include the tag in the calculation, though.

                // First, everything before the tag (the cipher and MAC algorithm ids)
                tagGenerator.AppendData(cipherText, 0, tagOffset);

                // Skip the data before the tag and the tag, then read everything that
                // remains.
                tagGenerator.AppendData(
                    cipherText,
                    tagOffset + tagSizeInBytes,
                    cipherText.Length - tagSizeInBytes - tagOffset);

                byte[] generatedTag = tagGenerator.GetHashAndReset();

                // The time it took to get to this point has so far been a function only
                // of the length of the data, or of non-encrypted values (e.g. it could
                // take longer to prepare the *key* for the HMACSHA384 MAC than the
                // HMACSHA256 MAC, but the algorithm choice wasn't a secret).
                //
                // If the verification of the authentication tag aborts as soon as a
                // difference is found in the byte arrays then your program may be
                // acting as a timing oracle which helps an attacker to brute-force the
                // right answer for the MAC. So, it's very important that every possible
                // "no" (2^256-1 of them for HMACSHA256) be evaluated in as close to the
                // same amount of time as possible. For this, we call CryptographicEquals
                if (!CryptographicEquals(
                    generatedTag,
                    0,
                    cipherText,
                    tagOffset,
                    tagSizeInBytes))
                {
                    // Assuming every tampered message (of the same length) took the same
                    // amount of time to process, we can now safely say
                    // "this data makes no sense" without giving anything away.
                    throw new CryptographicException();
                }

                // Restore the IV into the symmetricAlgorithm instance.
                byte[] iv = new byte[blockSizeInBytes];
                Buffer.BlockCopy(cipherText, ivOffset, iv, 0, iv.Length);
                cipher.IV = iv;

                using (ICryptoTransform decryptor = cipher.CreateDecryptor())
                {
                    return Transform(
                        decryptor,
                        cipherText,
                        cipherTextOffset,
                        cipherTextLength);
                }
            }
        }

        private static byte[] Transform(
            ICryptoTransform transform,
            byte[] input,
            int inputOffset,
            int inputLength)
        {
            // Many of the implementations of ICryptoTransform report true for
            // CanTransformMultipleBlocks, and when the entire message is available in
            // one shot this saves on the allocation of the CryptoStream and the
            // intermediate structures it needs to properly chunk the message into blocks
            // (since the underlying stream won't always return the number of bytes
            // needed).
            if (transform.CanTransformMultipleBlocks)
            {
                return transform.TransformFinalBlock(input, inputOffset, inputLength);
            }

            // If our transform couldn't do multiple blocks at once, let CryptoStream
            // handle the chunking.
            using (MemoryStream messageStream = new MemoryStream())
            using (CryptoStream cryptoStream =
                new CryptoStream(messageStream, transform, CryptoStreamMode.Write))
            {
                cryptoStream.Write(input, inputOffset, inputLength);
                cryptoStream.FlushFinalBlock();
                return messageStream.ToArray();
            }
        }

        /// <summary>
        /// Open a properly configured <see cref="SymmetricAlgorithm"/> conforming to the
        /// scheme identified by <paramref name="aeCipher"/>.
        /// </summary>
        /// <param name="aeCipher">The cipher mode to open.</param>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <returns>
        /// A SymmetricAlgorithm object with the right key, cipher mode, and padding
        /// mode; or <c>null</c> on unknown algorithms.
        /// </returns>
        private static SymmetricAlgorithm GetCipher(AeCipher aeCipher, byte[] masterKey)
        {
            SymmetricAlgorithm symmetricAlgorithm;

            switch (aeCipher)
            {
                case AeCipher.Aes256CbcPkcs7:
                    symmetricAlgorithm = Aes.Create();
                    // While 256-bit, CBC, and PKCS7 are all the default values for these
                    // properties, being explicit helps comprehension more than it hurts
                    // performance.
                    symmetricAlgorithm.KeySize = 256;
                    symmetricAlgorithm.Mode = CipherMode.CBC;
                    symmetricAlgorithm.Padding = PaddingMode.PKCS7;
                    break;
                default:
                    // An algorithm we don't understand
                    throw new CryptographicException();
            }

            // Instead of using the master key directly, derive a key for our chosen
            // HMAC algorithm based upon the master key.
            //
            // Since none of the symmetric encryption algorithms currently in .NET
            // support key sizes greater than 256-bit, we can use HMACSHA256 with
            // NIST SP 800-108 5.1 (Counter Mode KDF) to derive a value that is
            // no smaller than the key size, then Array.Resize to trim it down as
            // needed.

            using (HMAC hmac = new HMACSHA256(masterKey))
            {
                // i=1, Label=ASCII(cipher)
                byte[] cipherKey = hmac.ComputeHash(
                    new byte[] { 1, 99, 105, 112, 104, 101, 114 });

                // Resize the array to the desired keysize. KeySize is in bits,
                // and Array.Resize wants the length in bytes.
                Array.Resize(ref cipherKey, symmetricAlgorithm.KeySize / 8);

                symmetricAlgorithm.Key = cipherKey;
            }

            return symmetricAlgorithm;
        }

        /// <summary>
        /// Open a properly configured <see cref="HMAC"/> conforming to the scheme
        /// identified by <paramref name="aeMac"/>.
        /// </summary>
        /// <param name="aeMac">The message authentication mode to open.</param>
        /// <param name="masterKey">The master key from which other keys derive.</param>
        /// <returns>
        /// An HMAC object with the proper key, or <c>null</c> on unknown algorithms.
        /// </returns>
        private static HMAC GetMac(AeMac aeMac, byte[] masterKey)
        {
            HMAC hmac;

            switch (aeMac)
            {
                case AeMac.HMACSHA256:
                    hmac = new HMACSHA256();
                    break;
                case AeMac.HMACSHA384:
                    hmac = new HMACSHA384();
                    break;
                default:
                    // An algorithm we don't understand
                    throw new CryptographicException();
            }

            // Instead of using the master key directly, derive a key for our chosen
            // HMAC algorithm based upon the master key.
            // Since the output size of the HMAC is the same as the ideal key size for
            // the HMAC, we can use the master key over a fixed input once to perform
            // NIST SP 800-108 5.1 (Counter Mode KDF):
            hmac.Key = masterKey;

            // i=1, Context=ASCII(MAC)
            byte[] newKey = hmac.ComputeHash(new byte[] { 1, 77, 65, 67 });

            hmac.Key = newKey;
            return hmac;
        }

        // A simple helper method to ensure that the offset (writePos) always moves
        // forward with new data.
        private static void Append(byte[] newData, byte[] combinedData, ref int writePos)
        {
            Buffer.BlockCopy(newData, 0, combinedData, writePos, newData.Length);
            writePos += newData.Length;
        }

        /// <summary>
        /// Compare the contents of two arrays in an amount of time which is only
        /// dependent on <paramref name="length"/>.
        /// </summary>
        /// <param name="a">An array to compare to <paramref name="b"/>.</param>
        /// <param name="aOffset">
        /// The starting position within <paramref name="a"/> for comparison.
        /// </param>
        /// <param name="b">An array to compare to <paramref name="a"/>.</param>
        /// <param name="bOffset">
        /// The starting position within <paramref name="b"/> for comparison.
        /// </param>
        /// <param name="length">
        /// The number of bytes to compare between <paramref name="a"/> and
        /// <paramref name="b"/>.</param>
        /// <returns>
        /// <c>true</c> if both <paramref name="a"/> and <paramref name="b"/> have
        /// sufficient length for the comparison and all of the applicable values are the
        /// same in both arrays; <c>false</c> otherwise.
        /// </returns>
        /// <remarks>
        /// An "insufficient data" <c>false</c> response can happen early, but otherwise
        /// a <c>true</c> or <c>false</c> response take the same amount of time.
        /// </remarks>
        [MethodImpl(MethodImplOptions.NoInlining | MethodImplOptions.NoOptimization)]
        private static bool CryptographicEquals(
            byte[] a,
            int aOffset,
            byte[] b,
            int bOffset,
            int length)
        {
            Debug.Assert(a != null);
            Debug.Assert(b != null);
            Debug.Assert(length >= 0);

            int result = 0;

            if (a.Length - aOffset < length || b.Length - bOffset < length)
            {
                return false;
            }

            unchecked
            {
                for (int i = 0; i < length; i++)
                {
                    // Bitwise-OR of subtraction has been found to have the most
                    // stable execution time.
                    //
                    // This cannot overflow because bytes are 1 byte in length, and
                    // result is 4 bytes.
                    // The OR propagates all set bytes, so the differences are only
                    // present in the lowest byte.
                    result = result | (a[i + aOffset] - b[i + bOffset]);
                }
            }

            return result == 0;
        }
    }
}
```
