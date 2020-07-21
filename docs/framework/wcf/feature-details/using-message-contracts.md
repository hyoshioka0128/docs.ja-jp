---
title: メッセージ コントラクトの使用
description: メッセージコントラクト属性を使用して、WFC で SOAP メッセージの構造を指定するメッセージコントラクトを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- message contracts [WCF]
ms.assetid: 1e19c64a-ae84-4c2f-9155-91c54a77c249
ms.openlocfilehash: 0a75298b50df74ddf15904af43a0eb62c5ba8496
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244713"
---
# <a name="using-message-contracts"></a>メッセージ コントラクトの使用
通常、Windows Communication Foundation (WCF) アプリケーションを構築する場合、開発者はデータ構造とシリアル化の問題に細心の注意を払って、データが格納されるメッセージの構造を考慮する必要はありません。 このようなアプリケーションでは、パラメーターまたは戻り値用にデータ コントラクトを作成するのは簡単です  (詳細については、「[サービスコントラクトでのデータ転送の指定](specifying-data-transfer-in-service-contracts.md)」を参照してください)。  
  
 ただし、SOAP メッセージの構造を完全に制御することがメッセージの内容の制御と同様に重要となる場合があります。 これが特に当てはまるのは、相互運用性が重要である場合、具体的にはメッセージまたはメッセージ部分のレベルでセキュリティの問題を制御する場合です。 このような場合は、必要な正確な SOAP メッセージの構造を指定できるようにする*メッセージコントラクト*を作成できます。  
  
 ここでは、メッセージ コントラクトの各種属性を使用して、ユーザー操作に専用のメッセージ コントラクトを作成する方法について説明します。  
  
## <a name="using-message-contracts-in-operations"></a>処理におけるメッセージ コントラクトの使用  
 WCF は、*リモートプロシージャコール (RPC) スタイル*または*メッセージングスタイル*でモデル化された操作をサポートします。 RPC スタイルの操作では、シリアル化可能な任意の型を使用できます。複数のパラメーター、`ref` パラメーターと `out` パラメーターなど、ローカル呼び出しで使用できる機能を利用できます。 このスタイルでは、選択したシリアル化の形式によって基になるメッセージのデータ構造が制御され、WCF ランタイムによって、操作をサポートするメッセージが作成されます。 これにより、SOAP や SOAP メッセージに不慣れな開発者でも、サービス アプリケーションを迅速かつ容易に作成し、使用できます。  
  
 RPC スタイルでモデル化されたサービス操作のコード例を次に示します。  
  
```csharp  
[OperationContract]  
public BankingTransactionResponse PostBankingTransaction(BankingTransaction bt);  
```  
  
 通常は、データ コントラクトだけでメッセージのスキーマを定義することができます。 たとえば、前の例では、`BankingTransaction` と `BankingTransactionResponse` にデータ コントラクトがあれば、ほとんどのアプリケーションで基になる SOAP メッセージの内容を定義できます。 データコントラクトの詳細については、「[データコントラクトの使用](using-data-contracts.md)」を参照してください。  
  
 ただし、場合によっては、SOAP メッセージの構造がネットワーク経由でどのように転送されるかを厳密に制御する必要があります。 最も一般的なシナリオは、カスタム SOAP ヘッダーの挿入です。 もう 1 つの一般的なシナリオは、メッセージのヘッダーと本文のセキュリティ プロパティを定義すること、つまり、これらの要素にデジタル署名し、要素を暗号化するかどうかを決定することです。 最後に、一部のサードパーティの SOAP スタックでは、メッセージが特定の形式である必要があります。 この制御は、メッセージング スタイルの操作によって行うことができます。  
  
 メッセージング スタイルの操作には、最大で 1 つのパラメーターと 1 つの戻り値があります。これらはいずれもメッセージ型です。つまり、パラメーターと戻り値は、指定された SOAP メッセージ構造に直接シリアル化されます。 これは、<xref:System.ServiceModel.MessageContractAttribute> 型、または <xref:System.ServiceModel.Channels.Message> 型としてマークされた任意の型を使用できます。 次のコード例は前の RPC スタイルと同様の操作を示していますが、この例ではメッセージング スタイルを使用しています。  
  
 たとえば、`BankingTransaction` と `BankingTransactionResponse` がいずれもメッセージ コントラクト型である場合、次の操作のコードは有効です。  
  
```csharp  
[OperationContract]  
BankingTransactionResponse Process(BankingTransaction bt);  
[OperationContract]  
void Store(BankingTransaction bt);  
[OperationContract]  
BankingTransactionResponse GetResponse();  
```  
  
 ただし、次のコードは無効です。  
  
```csharp  
[OperationContract]  
bool Validate(BankingTransaction bt);  
// Invalid, the return type is not a message contract.  
[OperationContract]  
void Reconcile(BankingTransaction bt1, BankingTransaction bt2);  
// Invalid, there is more than one parameter.  
```  
  
 メッセージ コントラクト型を含み、有効なパターンのいずれにも従わないすべての操作に対して例外がスローされます。 もちろん、メッセージ コントラクト型を含まない処理にはこのような制限はありません。  
  
 1 つの型にメッセージ コントラクトとデータ コントラクトの両方が含まれる場合は、処理でその型が使用されたときにはメッセージ コントラクトだけが考慮されます。  
  
## <a name="defining-message-contracts"></a>メッセージ コントラクトの定義  
 型のメッセージ コントラクトを定義する (つまり、型と SOAP エンベロープ間のマッピングを定義する) には、<xref:System.ServiceModel.MessageContractAttribute> を型に適用します。 次に、SOAP ヘッダーにする型のメンバーに <xref:System.ServiceModel.MessageHeaderAttribute> を適用し、メッセージの SOAP 本文の一部にするメンバーに <xref:System.ServiceModel.MessageBodyMemberAttribute> を適用します。  
  
 メッセージ コントラクトの使用例を次のコードに示します。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader] public DateTime transactionDate;  
  [MessageBodyMember] private Account sourceAccount;  
  [MessageBodyMember] private Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 この型を操作パラメーターとして使用すると、次の SOAP エンベロープが生成されます。  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
    <h:transactionDate xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">2012-02-16T16:10:00</h:transactionDate>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <BankingTransaction xmlns="http://tempuri.org/">  
      <amount>0</amount>  
      <sourceAccount xsi:nil="true"/>  
      <targetAccount xsi:nil="true"/>  
    </BankingTransaction>  
  </s:Body>  
</s:Envelope>  
```  
  
 `operation` と `transactionDate` が SOAP ヘッダーとして表示され、SOAP 本体は `BankingTransaction`、`sourceAccount`、および `targetAccount` を含むラッパー要素 `amount` から成ることに注意してください。  
  
 パブリック、プライベート、保護、または内部のいずれであるかに関係なく、<xref:System.ServiceModel.MessageHeaderAttribute> と <xref:System.ServiceModel.MessageBodyMemberAttribute> は、すべてのフィールド、プロパティ、およびイベントに適用できます。  
  
 <xref:System.ServiceModel.MessageContractAttribute> を使用すると、SOAP メッセージの本文のラッパー要素の名前を制御する WrapperName および WrapperNamespace 属性を指定できます。 既定では、メッセージ コントラクト型の名前はラッパー用に使用され、メッセージ コントラクトが定義されている名前空間 (`http://tempuri.org/`) は既定の名前空間として使用されます。  
  
> [!NOTE]
> <xref:System.Runtime.Serialization.KnownTypeAttribute> 属性は、メッセージ コントラクトでは無視されます。 <xref:System.Runtime.Serialization.KnownTypeAttribute> が必要な場合は、対象のメッセージ コントラクトを使用している処理でそれを設定します。  
  
## <a name="controlling-header-and-body-part-names-and-namespaces"></a>ヘッダー名、本文名、および名前空間の制御  
 メッセージ コントラクトの SOAP 表現では、各ヘッダーと本文の各部分が名前と名前空間を持つ XML 要素にマップされます。  
  
 既定では、名前空間はメッセージが参加しているサービス コントラクトの名前空間と同じであり、その名前は <xref:System.ServiceModel.MessageHeaderAttribute> 属性または <xref:System.ServiceModel.MessageBodyMemberAttribute> 属性が割り当てられたメンバー名によって決定されます。  
  
 (<xref:System.ServiceModel.MessageContractMemberAttribute.Name%2A?displayProperty=nameWithType> 属性と <xref:System.ServiceModel.MessageContractMemberAttribute.Namespace%2A?displayProperty=nameWithType> 属性の親クラスの) <xref:System.ServiceModel.MessageHeaderAttribute> および <xref:System.ServiceModel.MessageBodyMemberAttribute> を操作することによって、これらの既定値を変更できます。  
  
 次のコード例のクラスについて考えてみます。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader(Namespace="http://schemas.contoso.com/auditing/2005")] public bool IsAudited;  
  [MessageBodyMember(Name="transactionData")] public BankingTransactionData theData;  
}  
```  
  
 この例では、`IsAudited` ヘッダーがコードで指定された名前空間に存在し、`theData` メンバーを表す本文が `transactionData` という名前の XML 要素によって表現されます。 次に、このメッセージ コントラクト用に生成された XML を示します。  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:IsAudited xmlns:h="http://schemas.contoso.com/auditing/2005" xmlns="http://schemas.contoso.com/auditing/2005">false</h:IsAudited>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <AuditedBankingTransaction xmlns="http://tempuri.org/">  
      <transactionData/>  
    </AuditedBankingTransaction>  
  </s:Body>  
</s:Envelope>  
```  
  
## <a name="controlling-whether-the-soap-body-parts-are-wrapped"></a>SOAP 本文の各部分のラップの制御  
 SOAP 本文は、既定で、ラップされた要素内にシリアル化されます。 たとえば、`HelloGreetingMessage` メッセージのメッセージ コントラクトに含まれる <xref:System.ServiceModel.MessageContractAttribute> 型の名前から生成される `HelloGreetingMessage` ラッパー要素を次のコードに示します。  
  
[!code-csharp[MessageHeaderAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/messageheaderattribute/cs/services.cs#3)]
[!code-vb[MessageHeaderAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/messageheaderattribute/vb/services.vb#3)]  
  
 ラッパー要素を抑制するには、<xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> プロパティを `false` に設定します。 ラッパー要素の名前と名前空間を制御するには、<xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> プロパティと <xref:System.ServiceModel.MessageContractAttribute.WrapperNamespace%2A> プロパティを使用します。  
  
> [!NOTE]
> ラップされていないメッセージにメッセージ本文の複数の部分を含めることは、WS-I Basic Profile 1.1 規格に反するため、新しいメッセージ コントラクトを設計する場合はお勧めできません。 ただし、特定の相互運用シナリオでは、複数のラップされていないメッセージ本文が必要な場合もあります。 1 つのメッセージ本文で複数のデータを転送する場合は、既定の (ラップされた) モードを使用することをお勧めします。 ラップされていないメッセージで複数のメッセージ ヘッダーを使用しても、何の問題もありません。  
  
## <a name="using-custom-types-inside-message-contracts"></a>メッセージ コントラクト内部でのカスタム型の使用  
 メッセージが使用されるサービス コントラクト用に選択されたシリアル化エンジンを使用して、個々のメッセージ ヘッダーとメッセージ本文がシリアル化されます (XML に変換されます)。 既定のシリアル化エンジンである `XmlFormatter` は、データ コントラクトを持つ任意の型を (<xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> を持つことによって) 明示的に処理することも、(プリミティブ型にしたり、<xref:System.SerializableAttribute?displayProperty=nameWithType> を持ったりすることなどによって) 暗黙的に処理することもできます。 詳細については、「[データコントラクトの使用](using-data-contracts.md)」を参照してください。  
  
 前の例では、`Operation` 型と `BankingTransactionData` 型は、データ コントラクトを持つ必要があります。また、`transactionDate` がプリミティブである (したがって、暗黙のデータ コントラクトを持つ) ため、<xref:System.DateTime> はシリアル化可能です。  
  
 ただし、別のシリアル化エンジンである `XmlSerializer` に切り替えることができます。 このような切り替えを行う場合は、メッセージ ヘッダーと本文の各部分に使用されているすべての型が `XmlSerializer` を使用してシリアル化可能であることを確認する必要があります。  
  
## <a name="using-arrays-inside-message-contracts"></a>メッセージ コントラクト内部での配列の使用  
 メッセージ コントラクトでは、反復要素の配列を 2 とおりの方法で使用できます。  
  
 最初の方法は、配列上で <xref:System.ServiceModel.MessageHeaderAttribute> または <xref:System.ServiceModel.MessageBodyMemberAttribute> を直接使用する方法です。 この場合は、配列全体が複数の子要素を含む 1 つの要素 (つまり、1 つのヘッダーまたは 1 つの本文) としてシリアル化されます。 次の例のクラスについて考えてみます。  
  
```csharp  
[MessageContract]  
public class BankingDepositLog  
{  
  [MessageHeader] public int numRecords;  
  [MessageHeader] public DepositRecord[] records;  
  [MessageHeader] public int branchID;  
}  
```  
  
 これは、次のような SOAP ヘッダーになります。  
  
```xml  
<BankingDepositLog>  
<numRecords>3</numRecords>  
<records>  
  <DepositRecord>Record1</DepositRecord>  
  <DepositRecord>Record2</DepositRecord>  
  <DepositRecord>Record3</DepositRecord>  
</records>  
<branchID>20643</branchID>  
</BankingDepositLog>  
```  
  
 もう 1 つの方法は、<xref:System.ServiceModel.MessageHeaderArrayAttribute> を使用する方法です。 この場合、各配列要素が個別にシリアル化されるため、次のように配列要素ごとに 1 つのヘッダーが付加されます。  
  
```xml  
<numRecords>3</numRecords>  
<records>Record1</records>  
<records>Record2</records>  
<records>Record3</records>  
<branchID>20643</branchID>  
```  
  
 配列エントリの既定の名前は、<xref:System.ServiceModel.MessageHeaderArrayAttribute> 属性が適用されたメンバーの名前になります。  
  
 <xref:System.ServiceModel.MessageHeaderArrayAttribute> 属性は、<xref:System.ServiceModel.MessageHeaderAttribute> から継承されます。 この属性は、非配列属性と同じ機能セットを持ちます。たとえば、単一のヘッダーに設定するのと同様に、ヘッダーの配列に順序、名前、および名前空間を設定できます。 配列で `Order` プロパティを使用すると、その配列全体に適用されます。  
  
 <xref:System.ServiceModel.MessageHeaderArrayAttribute> を適用できるのは配列だけであり、コレクションには適用できません。  
  
## <a name="using-byte-arrays-in-message-contracts"></a>メッセージ コントラクトでのバイト配列の使用  
 バイト配列を非配列属性 (<xref:System.ServiceModel.MessageBodyMemberAttribute> と <xref:System.ServiceModel.MessageHeaderAttribute>) で使用した場合は、配列としてではなく、生成された XML 内で Base64 でエンコードされたデータとして表現される特殊なプリミティブ型として扱われます。  
  
 <xref:System.ServiceModel.MessageHeaderArrayAttribute> 配列属性でバイト配列を使用した場合、結果は使用しているシリアライザーによって異なります。 既定のシリアライザーでは、配列が個々のバイト エントリとして表されます。 ただし、(サービス コントラクトの `XmlSerializer` を使用して) <xref:System.ServiceModel.XmlSerializerFormatAttribute> を選択した場合は、配列属性と非配列属性のどちらを使用しているかに関係なく、バイト配列は Base64 データとして扱われます。  
  
## <a name="signing-and-encrypting-parts-of-the-message"></a>メッセージの一部の署名と暗号化  
 メッセージ コントラクトでは、メッセージのヘッダーまたは本文にデジタル署名し、暗号化するかどうかを示すことができます。  
  
 この操作は、<xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A?displayProperty=nameWithType> 属性と <xref:System.ServiceModel.MessageHeaderAttribute> 属性の <xref:System.ServiceModel.MessageBodyMemberAttribute> プロパティを設定することによって実行されます。 このプロパティは、<xref:System.Net.Security.ProtectionLevel?displayProperty=nameWithType> 型の列挙体であり、<xref:System.Net.Security.ProtectionLevel.None> (暗号化と署名を行わない)、<xref:System.Net.Security.ProtectionLevel.Sign> (デジタル署名だけを行う)、または <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> (暗号化とデジタル署名の両方を行う) に設定できます。 既定値は、<xref:System.Net.Security.ProtectionLevel.EncryptAndSign> です。  
  
 これらのセキュリティ機能を使用するには、バインディングと動作を適切に構成する必要があります。 適切な構成を行わずにこれらのセキュリティ機能を使用した場合 (資格情報を指定せずにメッセージに署名しようとした場合など)、検証時に例外がスローされます。  
  
 メッセージ ヘッダーの場合、ヘッダーごとに保護レベルが設定されます。  
  
 メッセージ本文の各部分の場合は、保護レベルを "最小保護レベル" と見なすことができます。 本文には、その数に関係なく 1 つの保護レベルしか設定できません。 本文の保護レベルは、本文の全部分の中の最も高い <xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A> プロパティの設定によって決定されます。 ただし、本文の各部分の保護レベルを必要最小限の保護レベルに設定することをお勧めします。  
  
 次のコード例のクラスについて考えてみます。  
  
```csharp  
[MessageContract]  
public class PatientRecord  
{  
   [MessageHeader(ProtectionLevel=None)] public int recordID;  
   [MessageHeader(ProtectionLevel=Sign)] public string patientName;  
   [MessageHeader(ProtectionLevel=EncryptAndSign)] public string SSN;  
   [MessageBodyMember(ProtectionLevel=None)] public string comments;  
   [MessageBodyMember(ProtectionLevel=Sign)] public string diagnosis;  
   [MessageBodyMember(ProtectionLevel=EncryptAndSign)] public string medicalHistory;  
}  
```  
  
 この例では、`recordID` ヘッダーは保護されず、`patientName` は署名`signed`され、`SSN` は暗号化および署名されます。 本文の comments と diagnosis の各部分では低い保護レベルを指定していても、本文の少なくとも 1 つの部分 (`medicalHistory`) に <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> が適用されているため、メッセージ本文全体が暗号化され、署名されます。  
  
## <a name="soap-action"></a>SOAP アクション  
 SOAP 標準と関連する Web サービス標準では、送信されるすべての SOAP メッセージに設定可能な `Action` という名前のプロパティが定義されます。 このプロパティの値は、操作の <xref:System.ServiceModel.OperationContractAttribute.Action%2A?displayProperty=nameWithType> プロパティと <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A?displayProperty=nameWithType> プロパティによって制御されます。  
  
## <a name="soap-header-attributes"></a>SOAP ヘッダーの属性  
 SOAP 標準では、ヘッダーに設定可能な次の属性が定義されます。  
  
- `Actor/Role` (SOAP 1.1 では `Actor`、SOAP 1.2 では `Role`)  
  
- `MustUnderstand`  
  
- `Relay`  
  
 `Actor` 属性または `Role` 属性は、指定のヘッダーが対象とするノードの URI (Uniform Resource Identifier) を指定します。 `MustUnderstand` 属性は、ヘッダー処理ノードがヘッダーを認識する必要があるかどうかを指定します。 `Relay` 属性は、ダウンストリーム ノードにヘッダーを中継する必要があるかどうかを指定します。 WCF では、 `MustUnderstand` このトピックで後述する「メッセージコントラクトのバージョン管理」セクションで指定されている属性を除き、受信メッセージに対してこれらの属性の処理は実行されません。 ただし、後述するように、必要に応じてこれらの属性を読み書きすることができます。  
  
 既定では、メッセージの送信時にこれらの属性は出力されません。 これは、2 とおりの方法で変更できます。 1 つ目の方法として、次のコード例に示すように、<xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A?displayProperty=nameWithType>、<xref:System.ServiceModel.MessageHeaderAttribute.MustUnderstand%2A?displayProperty=nameWithType>、および <xref:System.ServiceModel.MessageHeaderAttribute.Relay%2A?displayProperty=nameWithType> の各プロパティを変更することによって、属性を必要な値に静的に設定できます  (`Role` プロパティが存在しないことに注意してください。SOAP 1.2 を使用している場合は、<xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A> プロパティを設定すると `Role` 属性が出力されます)。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader(Actor="http://auditingservice.contoso.com", MustUnderstand=true)] public bool IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
```  
  
 これらの属性を制御する 2 番目の方法は、コードを通して動的に行う方法です。 これを行うには、必要なヘッダーの型を <xref:System.ServiceModel.MessageHeader%601> 型にラップし (この型と非ジェネリック バージョンを混同しないようにしてください)、その型を <xref:System.ServiceModel.MessageHeaderAttribute> と共に使用します。 これで、次のコード例に示すように、<xref:System.ServiceModel.MessageHeader%601> のプロパティを使用して SOAP 属性を設定できるようになります。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public MessageHeader<bool> IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
// application code:  
BankingTransaction bt = new BankingTransaction();  
bt.IsAudited = new MessageHeader<bool>();  
bt.IsAudited.Content = false; // Set IsAudited header value to "false"  
bt.IsAudited.Actor="http://auditingservice.contoso.com";  
bt.IsAudited.MustUnderstand=true;  
```  
  
 動的制御機構と静的制御機構の両方を使用する場合、静的な設定が既定で使用されますが、次のコードに示すように、後で動的機構を使用して静的な設定をオーバーライドできます。  
  
```csharp  
[MessageHeader(MustUnderstand=true)] public MessageHeader<Person> documentApprover;  
// later on in the code:  
BankingTransaction bt = new BankingTransaction();  
bt.documentApprover = new MessageHeader<Person>();  
bt.documentApprover.MustUnderstand = false; // override the static default of 'true'  
```  
  
 次のコードに示すように、属性を動的に制御して繰り返すヘッダーを作成できます。  
  
```csharp  
[MessageHeaderArray] public MessageHeader<Person> documentApprovers[];  
```  
  
 受信側で、<xref:System.ServiceModel.MessageHeader%601> クラスがこの型のヘッダーで使用されている場合にのみ、これらの SOAP 属性の読み取りを実行できます。 受信メッセージの属性設定を明らかにするために、`Actor` 型のヘッダーの `Relay`、`MustUnderstand`、または <xref:System.ServiceModel.MessageHeader%601> の各プロパティを調べます。  
  
 メッセージを受信して返信するときに、これらの SOAP 属性設定は <xref:System.ServiceModel.MessageHeader%601> 型のヘッダーとして往復するだけです。  
  
## <a name="order-of-soap-body-parts"></a>SOAP 本文の順序  
 状況によっては、本文の各部分の順序を制御する必要があります。 本文要素の既定の順序はアルファベット順ですが、<xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=nameWithType> プロパティで制御できます。 このプロパティのセマンティクスは、継承シナリオにおける動作を除き、<xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A?displayProperty=nameWithType> プロパティのセマンティクスと同じです (メッセージ コントラクトでは、派生型の本文メンバーの前に基本型の本文メンバーが並べ替えられることはありません)。 詳細については、「[データメンバーの順序](data-member-order.md)」を参照してください。  
  
 次の例では、通常はアルファベット順で最初である `amount` が先頭にきますが、 <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A> プロパティによって 3 番目の位置に挿入されます。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember(Order=1)] public Account sourceAccount;  
  [MessageBodyMember(Order=2)] public Account targetAccount;  
  [MessageBodyMember(Order=3)] public int amount;  
}  
```  
  
## <a name="message-contract-versioning"></a>メッセージ コントラクトのバージョン管理  
 場合によっては、メッセージ コントラクトを変更する必要があります。 たとえば、新しいバージョンのアプリケーションによってメッセージに余分なヘッダーが追加された場合です。 この場合、新しいバージョンから古いバージョンに送信するときは、システムは余分なヘッダーを処理し、逆方向に送信するときは不足しているヘッダーを処理する必要があります。  
  
 ヘッダーのバージョン管理には、次のルールが適用されます。  
  
- WCF では、不足しているヘッダーにはオブジェクトが存在しません。対応するメンバーは既定値のままになります。  
  
- WCF では、予期しない余分なヘッダーも無視されます。 このルールの 1 つの例外は、入力 SOAP メッセージ内の余分なヘッダーの `MustUnderstand` 属性が `true` に設定されている場合です。この場合、認識する必要のあるヘッダーを処理できないため、例外がスローされます。  
  
 メッセージ本文にも同様のバージョン管理ルールがあります。メッセージ本文の不足している部分と追加された部分はいずれも無視されます。  
  
## <a name="inheritance-considerations"></a>継承に関する留意点  
 メッセージ コントラクト型は、基本型がメッセージ コントラクトを持っている限り、他の型から継承することができます。  
  
 他のメッセージ コントラクト型から継承したメッセージ コントラクト型を使用して、メッセージを作成したり、メッセージにアクセスしたりする場合、次のルールが適用されます。  
  
- 継承階層内のすべてのメッセージ ヘッダーが収集され、そのメッセージの完全なヘッダー セットが形成されます。  
  
- 継承階層内のすべてのメッセージ本文が収集され、完全なメッセージ本文が形成されます。 本文の各部分は、継承階層内での位置に関係なく、通常の順序ルール (<xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=nameWithType> プロパティ順、続いてアルファベット順) に従って並べられます。 メッセージ本文が継承ツリーの複数レベルに存在するメッセージ コントラクト継承の使用は、あまりお勧めできません。 基本クラスと派生クラスでヘッダーまたは本文に同じ名前が定義されている場合は、base-most クラスからのメンバーがそのヘッダーまたは本文の値を保存するために使用されます。  
  
 次のコード例のクラスについて考えてみます。  
  
```csharp  
[MessageContract]  
public class PersonRecord  
{  
  [MessageHeader(Name="ID")] public int personID;  
  [MessageBodyMember] public string patientName;  
}  
  
[MessageContract]  
public class PatientRecord : PersonRecord  
{  
  [MessageHeader(Name="ID")] public int patientID;  
  [MessageBodyMember] public string diagnosis;  
}  
```  
  
 `PatientRecord` クラスは、`ID` という名前の 1 つのヘッダーを持つメッセージを記述します。 このヘッダーは、base-most メンバーが選択されたことによって、`personID` メンバーには対応しますが、`patientID` メンバーには対応しません。 そのため、この場合は `patientID` フィールドは使用されません。 メッセージ本文には、アルファベット順で、`diagnosis` 要素の次に `patientName` 要素が含まれます。 この例は、基本メッセージ コントラクトと派生メッセージ コントラクトの両方にメッセージ本文が含まれ、あまりお勧めできないパターンを示していることに注意してください。  
  
## <a name="wsdl-considerations"></a>WSDL に関する留意点  
 メッセージ コントラクトを使用するサービスから Web サービス記述言語 (WSDL: Web Services Description Language) コントラクトを生成するときには、メッセージ コントラクトのすべての機能が結果の WSDL に反映されるわけではないことに留意してください。 次の点を考慮してください。  
  
- WSDL では、ヘッダー配列の概念を表現することができません。 <xref:System.ServiceModel.MessageHeaderArrayAttribute> を使用してヘッダー配列を含むメッセージを作成した場合、結果の WSDL は配列ではなく 1 つのヘッダーだけに反映されます。  
  
- 結果の WSDL ドキュメントに一部の保護レベル情報が反映されない場合があります。  
  
- WSDL で生成されたメッセージ型が、メッセージ コントラクト型のクラスと同じ名前になります。  
  
- 複数の処理で同じメッセージ コントラクトを使用すると、WSDL ドキュメント内に複数のメッセージ型が生成されます。 以降も使用できるように、"2"、"3" などの番号を付加することで名前を一意にします。 WSDL をインポートし直すと、名前以外は同一の複数のメッセージ コントラクト型が作成されます。  
  
## <a name="soap-encoding-considerations"></a>SOAP エンコードに関する留意点  
 WCF では XML の従来の SOAP エンコードスタイルを使用できますが、その使用は推奨されません。 (サービス コントラクトに適用されている `Use` で、`Encoded` プロパティを <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType> に設定して) このスタイルを使用する場合、次の追加の考慮事項が適用されます。  
  
- メッセージ ヘッダーはサポートされません。つまり、<xref:System.ServiceModel.MessageHeaderAttribute> 属性と <xref:System.ServiceModel.MessageHeaderArrayAttribute> 配列属性は、SOAP エンコーディングと互換性がありません。  
  
- メッセージ コントラクトがラップされていない場合、つまり、<xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> プロパティが `false` に設定されている場合は、メッセージ コントラクトが持つことのできる本文の部分は 1 つに限られます。  
  
- 要求メッセージ コントラクトのラッパー要素の名前は、操作の名前と一致する必要があります。 この場合、メッセージ コントラクトの `WrapperName` プロパティを使用します。  
  
- 応答メッセージ コントラクトのラッパー要素の名前は、操作の名前にサフィックスとして "Response" を付けたものと同じである必要があります。 この場合、メッセージ コントラクトの <xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> プロパティを使用します。  
  
- SOAP エンコードはオブジェクト参照を保存します。 次に例を示します。  
  
    ```csharp  
    [MessageContract(WrapperName="updateChangeRecord")]  
    public class ChangeRecordRequest  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    [MessageContract(WrapperName="updateChangeRecordResponse")]  
    public class ChangeRecordResponse  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    // application code:  
    ChangeRecordRequest cr = new ChangeRecordRequest();  
    Person p = new Person("John Doe");  
    cr.changedBy=p;  
    cr.changedFrom=p;  
    cr.changedTo=p;  
    ```  
  
 SOAP エンコーディングを使用してメッセージをシリアル化した後、`changedFrom` と `changedTo` には `p` のコピーは保存されませんが、代わりに、`changedBy` 要素内部のコピーがポイントされます。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項  
 すべてのメッセージ ヘッダーとメッセージ本文が個別にシリアル化されます。 したがって、ヘッダーおよび本文ごとに同じ名前空間が繰り返し宣言される可能性があります。 特に、回線上のメッセージ サイズに関して、パフォーマンスを向上させるには、複数のヘッダーと本文を単一のヘッダーまたは本文に統合します。 たとえば、次のコードの代わりに  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public Account sourceAccount;  
  [MessageBodyMember] public Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 次のコードを使用します。  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public OperationDetails details;  
}  
  
[DataContract]  
public class OperationDetails  
{  
  [DataMember] public Account sourceAccount;  
  [DataMember] public Account targetAccount;  
  [DataMember] public int amount;  
}  
```  
  
### <a name="event-based-asynchronous-and-message-contracts"></a>イベント ベースの非同期とメッセージ コントラクト  
 イベント ベースの非同期モデルのデザイン ガイドラインには、複数の値を返す場合に、1 つの値を `Result` プロパティとして返し、残りの値を <xref:System.EventArgs> オブジェクトのプロパティとして返すことが記載されています。 この 1 つの結果として、クライアントがイベント ベースの非同期コマンド オプションを使用してメタデータをインポートし、操作から複数の値が返される場合、既定の <xref:System.EventArgs> オブジェクトは 1 つの値を `Result` プロパティとして返し、残りの値は <xref:System.EventArgs> オブジェクトのプロパティになります。  
  
 メッセージ オブジェクトを `Result` プロパティとして受け取り、返された値をそのオブジェクトのプロパティとして取得する場合は、`/messageContract` コマンド オプションを使用します。 これにより、`Result` オブジェクトの <xref:System.EventArgs> プロパティとして応答メッセージを返すシグネチャが生成されます。 すべての内部戻り値は、応答メッセージ オブジェクトのプロパティになります。  
  
## <a name="see-also"></a>関連項目

- [データ コントラクトの使用](using-data-contracts.md)
- [サービスの設計と実装](../designing-and-implementing-services.md)
