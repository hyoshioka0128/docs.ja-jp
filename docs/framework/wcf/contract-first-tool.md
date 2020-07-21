---
title: コントラクト優先ツール
ms.date: 03/30/2017
ms.assetid: 0a880690-f460-4475-a5f4-9f91ce08fcc6
ms.openlocfilehash: 36e1a3e19f802ca5b74cf50f5bcd57c167e31e33
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291701"
---
# <a name="contract-first-tool"></a>コントラクト優先ツール
サービス コントラクトは、多くの場合、既存のサービスから作成する必要があります。 .NET Framework 4.5 以降では、データ コントラクト クラスは、コントラクト優先ツールを使用して既存のサービスから自動的に作成できます。 コントラクト優先ツールを使用するには、XML スキーマ定義ファイル (XSD) をローカルにダウンロードする必要があります。ツールは、HTTP 経由でリモート データ コントラクトをインポートすることはできません。

 コントラクトファースト ツールは、ビルド タスクとして Visual Studio 2012 に統合されています。 ビルド タスクによって生成されるコード ファイルは、基になるサービス コントラクトの変更をプロジェクトが簡単に取り込むことができるように、プロジェクトがビルドされるたびに作成されます。

 コントラクト優先ツールがインポートできるスキーマ型には、次のようなものがあります。

```xml
<xsd:complexType>
 <xsd:simpleType>
 </xsd:simpleType>
</xsd:complexType>
```

 単純型は、`Int16` または `String` のようなプリミティブである場合は生成されません。複合型は、`Collection` 型である場合は生成されません。 他の `xsd:complexType` の一部である型も、生成されません。 これらのすべての場合に、型はプロジェクト内の既存の型を参照するようになります。

## <a name="adding-a-data-contract-to-a-project"></a>プロジェクトへのデータ コントラクトの追加
 コントラクト優先ツールを使用する前に、サービス コントラクト (XSD) をプロジェクトに追加する必要があります。 この概要説明では、コントラクト優先機能を示すために、次のコントラクトを使用します。 このサービス定義は、Bingの検索 API で使用されるサービス コントラクトの小さなサブセットです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema id="ServiceSchema"
    targetNamespace="http://tempuri.org/ServiceSchema.xsd"
    elementFormDefault="qualified"
    xmlns="http://tempuri.org/ServiceSchema.xsd"
    xmlns:mstns="http://tempuri.org/ServiceSchema.xsd"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
>
  <xs:complexType name="SearchRequest">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Version" type="xs:string" default="2.2" />
      <xs:element minOccurs="0" maxOccurs="1" name="Market" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UILanguage" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="Query" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="AppId" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:double" />
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:double" />
      <xs:element minOccurs="0" maxOccurs="1" name="Radius" type="xs:double" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="WebSearchOption">
    <xs:restriction base="xs:string">
      <xs:enumeration value="DisableHostCollapsing" />
      <xs:enumeration value="DisableQueryAlterations" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

 上記のサービス契約をプロジェクトに追加するには、プロジェクトを右クリックし、[**新規追加....**] を選択します。 [テンプレート] ダイアログ ボックスの [WCF] ペインで [スキーマ定義] を選択し、新しいファイルの名前を SampleContract.xsd にします。 上のコードをコピーし、新しいファイルのコード ビューに貼り付けます。

## <a name="configuring-contract-first-options"></a>コントラクト優先のオプションの構成
 コントラクト優先オプションは、WCF プロジェクトの [プロパティ] メニューで構成できます。 コントラクト優先開発を有効にするには、プロジェクトプロパティ ウィンドウの [WCF] ページで **[XSD を型定義言語として有効**にする] チェック ボックスをオンにします。

 ![コントラクト優先開発が有効になっている WCF オプションのスクリーンショット。](./media/contract-first-tool/contract-first-options.png)

 高度なプロパティを構成するには、[詳細設定] をクリックします。

 ![[契約コード生成の詳細設定] ダイアログ ボックス](./media/contract-first-tool/advanced-contract-settings.png)

 次の詳細設定は、コントラクトからコードを生成するために構成できます。 設定は、プロジェクト内のすべてのファイルに対してのみ構成できます。現時点では、ファイルごとの構成はできません。

- **シリアライザー モード**: この設定は、サービス コントラクト ファイルの読み取りに使用するシリアライザーを決定します。 **XML シリアライザー**を選択すると、**コレクションの種類**と**再利用の種類のオプション**は無効になります。 これらのオプションは、データ**コントラクト シリアライザー**にのみ適用されます。

- **型の再利用**: この設定では、型の再利用に使用するライブラリを指定します。 この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **コレクション型**: この設定では、コレクション データ型に使用する完全修飾型またはアセンブリ修飾型を指定します。 この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **ディクショナリ型**: この設定では、ディクショナリ データ型に使用する完全修飾型またはアセンブリ修飾型を指定します。

- **EnableDataBinding**: この設定は、データ<xref:System.ComponentModel.INotifyPropertyChanged>バインディングを実装するすべてのデータ型にインターフェイスを実装するかどうかを指定します。

- **除外型**: この設定では、参照アセンブリから除外する完全修飾型またはアセンブリ修飾型の一覧を指定します。 この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **内部型の生成**: 内部としてマークされたクラスを生成するかどうかを指定します。 この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **この**設定では、属性を持つクラスを生成するかどうかを指定します<xref:System.SerializableAttribute>。 この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **ImportXMLTypes**: この設定では、<xref:System.SerializableAttribute>属性を持たないクラスに属性を適用するようにデータ コントラクト<xref:System.Runtime.Serialization.DataContractAttribute>シリアライザーを構成するかどうかを指定します。  この設定は **、[シリアライザー モード] が** **[データ コントラクト シリアライザー**] に設定されている場合にのみ適用されます。

- **この設定では**、.NET Framework 3.5 用に作成された型指定されたデータ セットに追加機能を提供するかどうかを指定します。 **シリアライザー モード**を**XML シリアライザー**に設定<xref:System.Data.Design.TypedDataSetSchemaImporterExtensionFx35>すると、この値が True に設定されている場合、拡張機能が XML スキーマ インポーターに追加されます。 **シリアライザー モード**をデータ**コントラクト シリアライザー**に設定すると<xref:System.DateTimeOffset>、この値が False に設定されている場合、型は参照から除外され<xref:System.DateTimeOffset>、古いフレームワーク バージョンでは a が常に生成されます。

- **入力XsdFiles**: この設定では、入力ファイルの一覧を指定します。 各ファイルは、有効な XML スキーマを含んでいる必要があります。

- **言語**: この設定では、生成されるコントラクト コードの言語を指定します。 設定は、<xref:System.CodeDom.Compiler.CodeDomProvider> が認識できるものである必要があります。

- **名前空間マッピング**: この設定では、XSD ターゲット名前空間から CLR 名前空間へのマッピングを指定します。 各マッピングは、次の形式を使用する必要があります。

    ```xml
    "Schema Namespace, CLR Namespace"
    ```

     XML シリアライザーは、次の形式の 1 つのマッピングだけを受け取ります。

    ```xml
    "*, CLR Namespace"
    ```

- **OutputDirectory**: この設定では、コード ファイルが生成されるディレクトリを指定します。

 設定は、プロジェクトのビルド時に、サービス コントラクト ファイルからサービス コントラクト型を生成するために使用されます。

## <a name="using-contract-first-development"></a>コントラクト優先の開発の使用
 プロジェクトにサービスコントラクトを追加し、ビルド設定を確認したら **、F6**キーを押してプロジェクトをビルドします。 これで、サービス コントラクトで定義された型が、プロジェクト内で利用できるようになります。

 サービス コントラクトで定義した型を使用するには、現在の名前空間に `ContractTypes` への参照を追加します。

```csharp
using MyProjectNamespace.ContractTypes;
```

 サービスコントラクトで定義された型は、次に示すように、プロジェクトで解決可能になります。

 ![最初の数文字を入力した後に IntelliSense で表示される検索要求クラス。](./media/contract-first-tool/service-contract-types.png)

 ツールによって生成された型は、GeneratedXSDTypes.cs ファイル内に作成されます。 ファイルは、プロジェクト ディレクトリ\<>/obj/\<ビルド構成>/XSDGeneratedCode/ ディレクトリに既定で作成されます。 この資料の冒頭にあるサンプル スキーマは、次のように変換されます。

```csharp
//------------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by a tool.
//     Runtime Version:4.0.30319.17330
//
//     Changes to this file may cause incorrect behavior and will be lost if
//     the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------

namespace TestXSD3.ContractTypes
{
    using System.Xml.Serialization;

    /// <remarks/>
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]
    [System.SerializableAttribute()]
    [System.Diagnostics.DebuggerStepThroughAttribute()]
    [System.ComponentModel.DesignerCategoryAttribute("code")]
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=true)]
    public partial class SearchRequest
    {

        private string versionField;

        private string marketField;

        private string uILanguageField;

        private string queryField;

        private string appIdField;

        private double latitudeField;

        private bool latitudeFieldSpecified;

        private double longitudeField;

        private bool longitudeFieldSpecified;

        private double radiusField;

        private bool radiusFieldSpecified;

        public SearchRequest()
        {
            this.versionField = "2.2";
        }

        /// <remarks/>
        [System.ComponentModel.DefaultValueAttribute("2.2")]
        public string Version
        {
            get
            {
                return this.versionField;
            }
            set
            {
                this.versionField = value;
            }
        }

        /// <remarks/>
        public string Market
        {
            get
            {
                return this.marketField;
            }
            set
            {
                this.marketField = value;
            }
        }

        /// <remarks/>
        public string UILanguage
        {
            get
            {
                return this.uILanguageField;
            }
            set
            {
                this.uILanguageField = value;
            }
        }

        /// <remarks/>
        public string Query
        {
            get
            {
                return this.queryField;
            }
            set
            {
                this.queryField = value;
            }
        }

        /// <remarks/>
        public string AppId
        {
            get
            {
                return this.appIdField;
            }
            set
            {
                this.appIdField = value;
            }
        }

        /// <remarks/>
        public double Latitude
        {
            get
            {
                return this.latitudeField;
            }
            set
            {
                this.latitudeField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool LatitudeSpecified
        {
            get
            {
                return this.latitudeFieldSpecified;
            }
            set
            {
                this.latitudeFieldSpecified = value;
            }
        }

        /// <remarks/>
        public double Longitude
        {
            get
            {
                return this.longitudeField;
            }
            set
            {
                this.longitudeField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool LongitudeSpecified
        {
            get
            {
                return this.longitudeFieldSpecified;
            }
            set
            {
                this.longitudeFieldSpecified = value;
            }
        }

        /// <remarks/>
        public double Radius
        {
            get
            {
                return this.radiusField;
            }
            set
            {
                this.radiusField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool RadiusSpecified
        {
            get
            {
                return this.radiusFieldSpecified;
            }
            set
            {
                this.radiusFieldSpecified = value;
            }
        }
    }

    /// <remarks/>
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]
    [System.SerializableAttribute()]
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=false)]
    public enum WebSearchOption
    {

        /// <remarks/>
        DisableHostCollapsing,

        /// <remarks/>
        DisableQueryAlterations,
    }
}
```

## <a name="errors-and-warnings"></a>エラーと警告
 XSD スキーマの解析中に発生したエラーと警告は、ビルドのエラーと警告として表示されます。

## <a name="interface-inheritance"></a>インターフェイスの継承
 コントラクト優先の開発でインターフェイスの継承を使用することはできません。これは、他の操作におけるインターフェイスの動作と一致しています。 基底インターフェイスを継承するインターフェイスを使用するには、2 つの別個のエンドポイントを使用します。 最初のエンドポイントは継承されるコントラクトを使用し、2 番目のエンドポイントは基底インターフェイスを実装します。
