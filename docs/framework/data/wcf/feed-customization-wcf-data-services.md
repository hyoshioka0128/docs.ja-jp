---
title: フィードのカスタマイズ (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, feeds
- WCF Data Services, Atom protocol
- Atom Publishing Protocol [WCF Data Services]
- WCF Data Services, customizing feeds
ms.assetid: 0d1a39bc-6462-4683-bd7d-e74e0fd28a85
ms.openlocfilehash: f34ee198ba49a168ed8b56785bea68beee2eb214
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75348119"
---
# <a name="feed-customization-wcf-data-services"></a>フィードのカスタマイズ (WCF Data Services)
WCF Data Services では、Open Data Protocol (OData) を使用してデータがフィードとして公開されます。 OData では、データ フィード用に Atom 形式と JavaScript Object Notation (JSON) 形式の両方がサポートされています。 Atom フィードを使用する場合、OData では、エンティティやリレーションシップなどのデータを XML 形式にシリアル化する標準の方法が提供されます。この XML 形式は、HTTP メッセージの本文に含めることができます。 OData では、エンティティに含まれるデータと Atom 要素間のエンティティとプロパティの既定のマッピングが定義されています。 詳細については、[OData のAtom 形式](https://www.odata.org/documentation/odata-version-2-0/atom-format/)に関するページを参照してください。  
  
 場合によっては、データ サービスから返されるプロパティのデータを、標準のフィードの形式ではなくカスタマイズした方法でシリアル化する必要があります。 OData を使用すると、データ フィードのシリアル化をカスタマイズして、エントリの未使用の要素と属性、またはフィードのエントリのカスタム要素にエンティティのプロパティをマップできます。  
  
> [!NOTE]
> フィードのカスタマイズは、Atom フィードでのみサポートされます。 返されたフィードに対して JSON 形式が要求されたときは、カスタム フィードが返されません。  
  
 WCF Data Services を使用すると、Atom ペイロードに対するエンティティとプロパティの代替マッピングは、属性をデータ モデルのエンティティ型に手動で適用することによって定義できます。 これらの属性の適用方法は、データ サービスのデータ ソース プロバイダーによって決定されます。  
  
> [!IMPORTANT]
> カスタム フィードを定義する場合、カスタム マッピングが定義されているすべてのエンティティ プロパティが投影に含まれることを保証する必要があります。 マップされているエンティティ プロパティがこの射影に含まれていない場合、データの損失が発生することがあります。 詳しくは、「[クエリ射影](query-projections-wcf-data-services.md)」をご覧ください。  
  
## <a name="customizing-feeds-with-the-entity-framework-provider"></a>Entity Framework プロバイダーを使用したフィードのカスタマイズ  
 Entity Framework プロバイダーで使用されるデータ モデルは、.edmx ファイルの XML として表現されます。 この場合、カスタム フィードを定義する属性が、データ モデルのエンティティ型とプロパティを表現する `EntityType` および `Property` 要素に追加されます。 これらのフィードのカスタマイズ属性は、「[\[MC-CSDL\]: 概念スキーマ定義ファイル形式](https://docs.microsoft.com/openspecs/windows_protocols/mc-csdl/c03ad8c3-e8b7-4306-af96-a9e52bb3df12)」では定義されていません。これは、データ モデルを定義するために Entity Framework プロバイダーで使用される形式です。 したがって、フィードのカスタマイズ属性を特定のスキーマ名前空間で宣言する必要があります。これは、`m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"` として定義されます。 次の XML フラグメントは、`Property`、`Products`、および `ProductName` プロパティを定義する `ReorderLevel` エンティティ型の `UnitsInStock` 要素に適用されたフィードのカスタマイズ属性を示します。  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedAttributes](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedattributes)]  
  
 これらの属性によって `Products` エンティティ セットに対して次のカスタム データ フィードが生成されます。 このカスタム データ フィードでは、`ProductName` プロパティ値が `author` 要素内に加えて、`ProductName` プロパティ要素としても表示されます。`UnitsInStock` プロパティは、一意の名前空間、および属性としての `ReorderLevel` プロパティと共にカスタム要素に表示されます。  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResultProduct](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresultproduct)]  
  
 詳細については、[Entity Framework プロバイダーでフィードをカスタマイズする](how-to-customize-feeds-with-ef-provider-wcf-data-services.md)」を参照してください。  
  
> [!NOTE]
> データ モデルへの拡張はエンティティ デザイナーでサポートされていないので、データ モデルを含む XML ファイルを手動で変更する必要があります。 Entity Data Model ツールによって生成される .edmx ファイルの詳細については、「[.edmx ファイルの概要 (Entity Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))」を参照してください。  
  
### <a name="custom-feed-attributes"></a>カスタム フィード属性  
 次の表に、データ モデルを定義する概念スキーマ定義言語 (CSDL) に追加できるフィードをカスタマイズする XML 属性を示します。 これらの属性は、<xref:System.Data.Services.Common.EntityPropertyMappingAttribute> のプロパティと同等です。  
  
|属性名|説明|  
|--------------------|-----------------|  
|`FC_ContentKind`|コンテンツの種類を示します。 次のキーワードは、配信コンテンツの種類を定義します。<br /><br /> `text:` プロパティ値はフィード内でテキストとして表示されます。<br /><br /> `html:` プロパティ値はフィード内で HTML として表示されます。<br /><br /> `xhtml:` プロパティ値はフィード内で XML 形式の HTML として表示されます。<br /><br /> これらのキーワードは、リフレクション プロバイダーと共に使用する <xref:System.Data.Services.Common.SyndicationTextContentKind> 列挙の値と同等です。<br /><br /> この属性は、`FC_NsPrefix` および `FC_NsUri` 属性が使用されているときはサポートされません。<br /><br /> `xhtml` 属性の値として `FC_ContentKind` を指定する場合、そのプロパティ値に正しい形式の XML が含まれることを確認する必要があります。 データ サービスは、変換を行わずに値を返します。 さらに、返された XML 内の XML 要素のプレフィックスに名前空間 URI、およびマップされたフィード内で定義されたプレフィックスが含まれている必要があります。|  
|`FC_KeepInContent`|参照されたプロパティ値をフィードのコンテンツ セクションおよびマップされた場所の両方に含める必要があることを示します。 有効値は `true` または `false` です。 結果のフィードで WCF Data Services の以前のバージョンとの下位互換性を維持するには、`true` の値を指定して、フィードのコンテンツ セクションに含めます。|  
|`FC_NsPrefix`|非配信マッピング内の XML 要素の名前空間プレフィックス。 この属性は、`FC_NsUri` 属性と一緒に使用する必要があります。この属性は、`FC_ContentKind` 属性と一緒に使用できません。|  
|`FC_NsUri`|非配信マッピング内の XML 要素の名前空間 URI。 この属性は、`FC_NsPrefix` 属性と一緒に使用する必要があります。この属性は、`FC_ContentKind` 属性と一緒に使用できません。|  
|`FC_SourcePath`|このフィード マッピング規則が適用されるエンティティのプロパティのパス。 この属性は、`EntityType` 要素で使用されている場合にのみサポートされます。<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> プロパティは、複合型を直接参照できません。 複合型の場合は、プロパティ名が円記号 (`/`) で区切られたパス式を使用する必要があります。 たとえば、以下の値は、整数プロパティ `Age` と複合プロパティを含むエンティティ型 `Person` で使用できます<br /><br /> `Address`:<br /><br /> `Age`<br /><br /> `Address/Street`<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> プロパティは、プロパティ名で無効な文字 (スペースなど) を含む値に設定することはできません。|  
|`FC_TargetPath`|プロパティのマップ先となる結果のフィードのターゲット要素の名前。 この要素は、Atom 仕様またはカスタム要素によって定義された要素である場合があります。<br /><br /> 次のキーワードは、OData フィードの特定の場所をポイントする定義済みの配信ターゲット パス値です。<br /><br /> `SyndicationAuthorEmail:` `atom:author` 要素の `atom:email` 子要素。<br /><br /> `SyndicationAuthorName:` `atom:author` 要素の `atom:name` 子要素。<br /><br /> `SyndicationAuthorUri:` `atom:author` 要素の `atom:uri` 子要素。<br /><br /> `SyndicationContributorEmail:` `atom:contributor` 要素の `atom:email` 子要素。<br /><br /> `SyndicationContributorName:` `atom:contributor` 要素の `atom:name` 子要素。<br /><br /> `SyndicationContributorUri:` `atom:contributor` 要素の `atom:uri` 子要素。<br /><br /> `SyndicationCustomProperty:` カスタム プロパティ要素。 カスタム要素にマップする際、ターゲットは、ネストされた要素が円記号 (`/`) で区切られ、属性がアンパサンド (`@`) で指定されたパス式である必要があります。 次の例では、文字列 `UnitsInStock/@ReorderLevel` によってプロパティ値がルート エントリ要素の `ReorderLevel` という子要素の `UnitsInStock` という属性にマップされます。<br /><br /> `<Property Name="ReorderLevel" Type="Int16"               m:FC_TargetPath="UnitsInStock/@ReorderLevel"               m:FC_NsPrefix="Northwind"               m:FC_NsUri="http://schemas.examples.microsoft.com/dataservices"               m:FC_KeepInContent="false"               />`<br /><br /> ターゲットがカスタム要素名の場合、`FC_NsPrefix` および `FC_NsUri` 属性も指定する必要があります。<br /><br /> `SyndicationPublished:` `atom:published` 要素。<br /><br /> `SyndicationRights:` `atom:rights` 要素。<br /><br /> `SyndicationSummary:` `atom:summary` 要素。<br /><br /> `SyndicationTitle:` `atom:title` 要素。<br /><br /> `SyndicationUpdated:` `atom:updated` 要素。<br /><br /> これらのキーワードは、リフレクション プロバイダーと共に使用する <xref:System.Data.Services.Common.SyndicationItemProperty> 列挙の値と同等です。|  
  
> [!NOTE]
> 属性名および値では、大文字と小文字が区別されます。 属性は、`EntityType` 要素または 1 つ以上の `Property` 要素に適用されます (両方には適用されません)。  
  
## <a name="customizing-feeds-with-the-reflection-provider"></a>リフレクション プロバイダーを使用したフィードのカスタマイズ  
 リフレクション プロバイダーを使用して実装されたデータ モデル用にフィードをカスタマイズするには、<xref:System.Data.Services.Common.EntityPropertyMappingAttribute> 属性の 1 つ以上のインスタンスをデータ モデル内でエンティティ型を表現するクラスに追加します。 <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> クラスのプロパティは、前のセクションで説明したフィードのカスタマイズ属性に対応します。 両方のプロパティに対して定義されたカスタム フィード マッピングと共に `Order` 型の宣言の例を次に示します。  
  
> [!NOTE]
> 次の例のデータ モデルは、トピック「[方法: リフレクション プロバイダーを使用してデータ サービスを作成する](create-a-data-service-using-rp-wcf-data-services.md)」で定義されています。  
  
 [!code-csharp[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_custom_feeds/cs/orderitems.svc.cs#customorderfeed)]
 [!code-vb[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_custom_feeds/vb/orderitems.svc.vb#customorderfeed)]  
  
 これらの属性によって `Orders` エンティティ セットに対して次のカスタム データ フィードが生成されます。 このカスタム フィードでは、`OrderId` プロパティの値は `entry` の `title` 要素内にのみ表示され、`Customer` プロパティの値は `author` 要素内だけでなく、`Customer` プロパティ要素としても表示されます。  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/iqueryablefeedresult.xml#iqueryablefeedresult)]  
  
 詳細については、[リフレクション プロバイダーでフィードをカスタマイズする](how-to-customize-feeds-with-the-reflection-provider-wcf-data-services.md)」を参照してください。  
  
## <a name="customizing-feeds-with-a-custom-data-service-provider"></a>カスタム データ サービス プロバイダーを使用したフィードのカスタマイズ  
 カスタム データ サービス プロバイダーを使用して定義されたデータ モデル用のフィードのカスタマイズは、データ モデル内でエンティティ型を表現する <xref:System.Data.Services.Providers.ResourceType.AddEntityPropertyMappingAttribute%2A> で <xref:System.Data.Services.Providers.ResourceType> を呼び出すことによってリソース型に対して定義されます。 詳しくは、「[カスタム データ サービス プロバイダー](custom-data-service-providers-wcf-data-services.md)」をご覧ください。  
  
## <a name="consuming-custom-feeds"></a>カスタム フィードの処理  
 OData フィードをアプリケーションで直接処理する場合、アプリケーションでは、返されたフィード内のカスタム要素および属性を処理できる必要があります。 データ サービス プロバイダーに関係なく、データ モデルにカスタム フィードを実装した場合、`$metadata` エンドポイントは、データ サービスによって返される CSDL のカスタム フィード属性としてカスタム フィード情報を返します。 **[サービス参照の追加]** ダイアログまたは [datasvcutil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) ツールを使用してクライアント データ サービス クラスを生成する場合、データ サービスへの要求および応答を正しく処理するためにカスタム フィード属性が使用されます。  
  
## <a name="feed-customization-considerations"></a>フィードのカスタマイズに関する考慮事項  
 カスタム フィードのマッピングを定義する場合は、以下を検討してください。  
  
- WCF Data Services クライアントでは、フィード内のマップされた要素に含まれているのが空白のみの場合、その要素は空であると見なされます。 そのため、空白のみを含むマップされた要素は、同じ空白を使用するクライアントで具体化されません。 この空白をクライアントで維持するには、フィード マッピング属性で `KeepInContext` の値を `true` に設定する必要があります。  
  
## <a name="versioning-requirements"></a>バージョン管理の要件  
 フィードのカスタマイズには、次に示す OData プロトコルのバージョン管理の要件があります。  
  
- フィードのカスタマイズを行う場合は、クライアントとデータ サービスの両方でバージョン 2.0 以降の OData プロトコルがサポートされている必要があります。  
  
 詳細については、「[データ サービスのバージョン管理](data-service-versioning-wcf-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [リフレクション プロバイダー](reflection-provider-wcf-data-services.md)
- [Entity Framework プロバイダー](entity-framework-provider-wcf-data-services.md)
