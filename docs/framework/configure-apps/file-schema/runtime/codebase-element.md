---
title: <codeBase> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#codeBase
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/codeBase
helpviewer_keywords:
- <codeBase> element
- container tags, <codeBase> element
- codeBase element
ms.assetid: d48a3983-2297-43ff-a14d-1f29d3995822
ms.openlocfilehash: 475b7df55ed509157c1da0aeb8f979de238c72b5
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70971883"
---
# <a name="codebase-element"></a>\<codeBase> 要素

共通言語ランタイムがアセンブリを検索できる場所を指定します。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<dependentAssembly>**](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<codeBase>**

## <a name="syntax"></a>構文

```xml
   <codeBase
        version="Assembly version"
        href="URL of assembly"/>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`href`|必須の属性です。<br /><br /> ランタイムが指定されたバージョンのアセンブリを検索できる URL を指定します。|
|`version`|必須の属性です。<br /><br /> コードベースが適用されるアセンブリのバージョンを指定します。 アセンブリバージョン番号の形式は major. *minor. build. revision*です。|

## <a name="version-attribute"></a>version 属性

|値|Description|
|-----------|-----------------|
|バージョン番号の各部分の有効な値は 0 ~ 65535 です。|適用不可。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|`buildproviders`|カスタム リソース ファイルをコンパイルするためのビルド プロバイダーのコレクションを定義します。 ビルド プロバイダーの数は任意です。|
|`compilation`|ASP.NET が使用するすべてのコンパイル設定を構成します。|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`System.web`|ASP.NET 構成セクションのルート要素を指定します。|

## <a name="remarks"></a>解説

ランタイムで **\<codeBase>** コンピューター構成ファイルまたは発行者ポリシーファイルの設定を使用するには、アセンブリのバージョンもリダイレクトする必要があります。 アプリケーション構成ファイルには、アセンブリのバージョンをリダイレクトせずにコードベースを設定できます。 使用するアセンブリバージョンを決定した後、ランタイムは、バージョンを決定するファイルのコードベース設定を適用します。 コードベースが指定されていない場合、ランタイムは通常の方法でアセンブリをプローブします。

アセンブリに厳密な名前が付いている場合、コードベースの設定は、ローカルイントラネットまたはインターネット上の任意の場所に置くことができます。 アセンブリがプライベートアセンブリの場合、コードベースの設定は、アプリケーションのディレクトリに対する相対パスである必要があります。

厳密な名前のないアセンブリの場合、バージョンは無視され、ローダーは内部の最初の外観を使用し \<codebase> \<dependentAssembly> ます。 バインドを別のアセンブリにリダイレクトするエントリがアプリケーション構成ファイルにある場合、アセンブリのバージョンがバインド要求と一致しない場合でも、リダイレクトが優先されます。

## <a name="example"></a>例

次の例は、ランタイムがアセンブリを検索する場所を指定する方法を示しています。

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly"
                              publicKeyToken="32ab4ba45e0a69a1"
                              culture="neutral" />
            <codeBase version="2.0.0.0"
                      href="http://www.litwareinc.com/myAssembly.dll"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイルスキーマ](../index.md)
- [アセンブリの場所を指定します](../../../../standard/assembly/location.md)
- [ランタイムがアセンブリを検索する方法](../../../deployment/how-the-runtime-locates-assemblies.md)
