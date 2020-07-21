---
title: MissingRuntimeArtifactException クラス (.NET ネイティブ)
ms.date: 03/30/2017
ms.assetid: d5b3d13e-689f-4584-8ba6-44f5167a8590
ms.openlocfilehash: 7a69add45202b3ad838de592fadc82a84fa0ba5d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79180966"
---
# <a name="missingruntimeartifactexception-class-net-native"></a>MissingRuntimeArtifactException クラス (.NET ネイティブ)
**Windows アプリ用 .NET (Windows 10 用)、.NET ネイティブのみ**  
  
 この例外は、型または型のメンバーのメタデータは使用可能だが、その実装が削除されている場合にスローされます。  
  
 **名前空間:** System.Reflection  
  
> [!IMPORTANT]
> クラスは、 `MissingRuntimeArtifactException` .NET ネイティブツールチェーンによる内部使用のみを目的としています。 サード パーティのコードで使用することを目的としていません。また、アプリケーション コードで、例外を処理する必要はありません。 代わりに、[ランタイム ディレクティブ ファイル](runtime-directives-rd-xml-configuration-file-reference.md)にエントリを追加することにより、例外を除去します。 詳細については、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
 [!code-csharp[ProjectN#22](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingruntimeartifactexception_syntax1.cs#22)]  
  
 `MissingRuntimeArtifactException` クラスは、<xref:System.MemberAccessException> から派生しています。  
  
 `MissingRuntimeArtifactException` クラスには次のメンバーがあります。  
  
## <a name="constructors"></a>コンストラクター  
  
|コンストラクター|説明|  
|-----------------|-----------------|  
|`public MissingRuntimeArtifactException()`|エラーを説明するシステム提供のメッセージを使用して、`MissingRuntimeArtifactException` クラスの新しいインスタンスを初期化します。<br /><br /> このコンストラクターは、.NET ネイティブツールチェーンのみによって内部で使用されます。|  
|`public MissingRuntimeArtifactException(String message)`|指定したエラー メッセージを使用して、`MissingRuntimeArtifactException` クラスの新しいインスタンスを初期化します。<br /><br /> このコンストラクターは、.NET ネイティブツールチェーンのみによって内部で使用されます。|  
  
## <a name="properties"></a>Properties  
  
|プロパティ|Description|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|例外に関する追加のユーザー定義情報を提供する、キーと値のペアのコレクションを取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public string HelpLink { get; set; }`|この例外に関連付けられているヘルプ ファイルへのリンクを取得または設定します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public int HResult { get; protected set; }`|特定の例外に割り当てられた、コード化された数値である、`HRESULT` を取得または設定します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public Exception InnerException { get; }`|現在の例外を引き起こした例外を取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public string Message { get; }`|現在の例外を説明するメッセージを取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public string Source { get; set; }`|エラーの原因になったアプリケーションまたはオブジェクトの名前を取得または設定します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public string StackTrace { get; }`|呼び出し履歴で直前のフレームの文字列形式を取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public MethodBase TargetSite { get; }`|現在の例外をスローしたメソッドを取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
  
## <a name="methods"></a>メソッド  
  
|メソッド|Description|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|指定されたオブジェクトが現在のオブジェクトと等しいかどうかを判断します。  (<xref:System.Object> から継承。)|  
|`protected void Finalize()`|オブジェクトが、ガベージ コレクションによって収集される前に、リソースの解放とその他のクリーンアップ操作の実行を試みることができるようにします。 (<xref:System.Object> から継承。)|  
|`public Exception GetBaseException()`|1 つ以上の後続の例外の根本原因である例外を返します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public int GetHashCode()`|`MissingRuntimeArtifactException` インスタンスのハッシュ コードを返します。   (<xref:System.Object> から継承。)|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|例外に関する情報を使用して、<xref:System.Runtime.Serialization.SerializationInfo> オブジェクトを設定します。  (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`public Type GetType()`|現在のインスタンスのランタイム型を取得します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
|`protected Object MemberwiseClone()`|現在のオブジェクトの簡易コピーを作成します。 (<xref:System.Object> から継承。)|  
|`public string ToString()`|現在の例外の文字列形式を返します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
  
## <a name="events"></a>events  
  
|Event|Description|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|例外がシリアル化され、例外に関するシリアル化されたデータを含む例外状態オブジェクトが作成されたときに発生します。 (<xref:System.Exception?displayProperty=nameWithType> から継承。)|  
  
## <a name="usage-details"></a>Usage Details  
 `MissingRuntimeArtifactException` 例外は、型のインスタンス化または型のメンバーの呼び出しが試行され、その型またはメンバーのメタデータは存在するが、実装が削除されている場合にスローされます。  
  
 メソッドを動的に実行するためのメタデータと実装コードを実行時にアプリで使用できるようにするかどうかは、ランタイムディレクティブ (XML 構成) ファイル (.xml) によって定義されます。 \* アプリからこの例外がスローされないようにするには、\*.rd.xml を変更して、型または型のメンバーが必要とするメタデータが実行時に確実に存在するようにする必要があります。 \*.rd.xml ファイルの形式の詳細については、「[Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md)」(ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス) を参照してください。  
  
> [!IMPORTANT]
> この例外はアプリケーションで必要な実装コードを実行時に使用できないことを示しているため、この例外を `try`/`catch` ブロックで処理しないでください。 代わりに、ランタイム ディレクティブ ファイルを使用して、例外の原因を診断して排除する必要があります。 通常、この例外を回避するには、 `Activate` `Dynamic` ランタイムディレクティブファイル (. .xml ファイル) 内のプログラム要素に適切なまたはポリシーを指定し \* ます。 例外を除去するためにランタイム ディレクティブ ファイルに追加できるエントリを取得するには、次の 2 つのトラブルシューティング ツールのいずれかを使用できます。  
>
> - [MissingMetadataException トラブルシューティング ツール](https://dotnet.github.io/native/troubleshooter/type.html) (型の場合)。  
> - [MissingMetadataException トラブルシューティング ツール](https://dotnet.github.io/native/troubleshooter/method.html) (メソッドの場合)。  
  
 `MissingRuntimeArtifactException` クラスには一意のメンバーは含まれていません。メンバーはすべて基底クラスの <xref:System.MemberAccessException> から継承されます。  
  
## <a name="see-also"></a>関連項目

- [ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス](runtime-directives-rd-xml-configuration-file-reference.md)
- [ランタイム ディレクティブ ポリシーの設定](runtime-directive-policy-settings.md)
