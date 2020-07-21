---
title: XML シリアライザー ジェネレーター ツール (Sgen.exe)
description: XML シリアライザー ジェネレーター ツールは、アセンブリ内の型の XML シリアル化アセンブリを生成します。これにより、XmlSerializer の起動パフォーマンスが向上します。
ms.date: 03/30/2017
ms.assetid: cc1d1f1c-fb26-4be9-885a-3fe84c81cec6
ms.openlocfilehash: b6d9406ca6a69f7bdff3129b55c89dd5d1589d3f
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84288941"
---
# <a name="xml-serializer-generator-tool-sgenexe"></a>XML シリアライザー ジェネレーター ツール (Sgen.exe)

XML シリアライザー ジェネレーターは、指定されたアセンブリの種類に対応する XML シリアル化アセンブリを作成します。 シリアル化アセンブリは、指定された型のオブジェクトのシリアル化または逆シリアル化の際に、<xref:System.Xml.Serialization.XmlSerializer> の起動パフォーマンスを向上させます。
  
## <a name="syntax"></a>構文

コマンド ラインでツールを実行します。
  
```console  
sgen [options]  
```
  
> [!TIP]
> .NET Framework ツールが適切に機能するには、 `Path`、`Include`、および `Lib` の各環境変数を正しく設定する必要があります。 これらの環境変数を設定するには、\<SDK>\v2.0\Bin ディレクトリにある SDKVars.bat を実行します。 SDKVars.bat は、コマンド シェルごとに実行する必要があります。
  
## <a name="parameters"></a>パラメーター  
  
|オプション|説明|  
|------------|-----------------|  
|**/a\[ssembly\]:** _filename_|アセンブリ、または *filename* によって指定される実行可能ファイルに含まれるすべての型に対して、シリアル化コードを生成します。 指定できるファイル名は 1 つのみです。 この引数を複数指定した場合は、最後のファイル名が使用されます。|  
|**/c\[ompiler\]:** _options_|オプションを C# コンパイラに渡すように指定します。 csc.exe のすべてのオプションがサポートされ、コンパイラに渡されます。 このオプションを使用して、アセンブリに署名してキー ファイルを指定するように指定できます。|  
|**/d\[ebug\]**|デバッガーで使用できるイメージを生成します。|  
|**/f\[orce\]**|同じ名前の既存のアセンブリに上書きします。 既定値は **false** です。|  
|**/help または /?**|このツールのコマンド構文とオプションを表示します。|  
|**/k\[eep\]**|生成されたソース ファイルとその他の一時ファイルをシリアル化アセンブリにコンパイルした後、元のファイルを削除しません。 このオプションを使用して、ツールが特定の型に対してシリアル化コードを生成するかどうかを指定できます。|  
|**/n\[ologo\]**|Microsoft の著作権情報を表示しません。|  
|**/o\[ut\]:** _path_|生成されたアセンブリの保存先のディレクトリを指定します。 **注:** 生成されたアセンブリの名前は、入力アセンブリの名前と "xmlSerializers.dll" で構成されます。|  
|**/p\[roxytypes\]**|XML Web サービス プロキシ型に対してのみシリアル化コードを生成します。|  
|**/r\[eference\]:** _assemblyfiles_|XML シリアル化が必要な型によって参照されるアセンブリを指定します。 コンマで区切られた複数のアセンブリ ファイルを受け入れます。|  
|**/s\[ilent\]**|成功メッセージを表示しません。|  
|**/t\[ype\]:** _type_|指定された型に対してのみ、シリアル化コードを生成します。|  
|**/v\[erbose\]**|デバッグに関する詳細出力を表示します。 <xref:System.Xml.Serialization.XmlSerializer> でシリアル化できない対象アセンブリの型を一覧表示します。|  
|**/?**|このツールのコマンド構文とオプションを表示します。|  
  
## <a name="remarks"></a>Remarks  
 XML シリアライザー ジェネレーターを使用しない場合、<xref:System.Xml.Serialization.XmlSerializer> はアプリケーションを実行するたびに、各型に対してシリアル化コードとシリアル化アセンブリを生成します。 XML シリアル化起動のパフォーマンスを向上させるには、Sgen.exe ツールを使用して、あらかじめこれらのアセンブリを生成します。 生成したアセンブリは、アプリケーションで配置できます。  
  
 XML シリアライザー ジェネレーターは、サーバーとの通信に XML Web サービス プロキシを使用するクライアントのパフォーマンスも向上させますが、これは型が初めて読み込まれるとき、シリアル化プロセスによってパフォーマンスが低下しないためです。  
  
 これらの生成されたアセンブリは、Web サービスのサーバー側では使用できません。 このツールは、Web サービス クライアントと手動シリアル化シナリオに対してのみ使用できます。  
  
 シリアル化する型を含むアセンブリの名前が MyType.dll の場合、関連するシリアル化アセンブリの名前は MyType.XmlSerializers.dll となります。  
  
## <a name="examples"></a>使用例  
 次のコマンドは、Data.dll という名前のアセンブリに含まれるすべての型をシリアル化するために、Data.XmlSerializers.dll という名前のアセンブリを作成します。  
  
```console  
sgen Data.dll
```  
  
 Data.XmlSerializers.dll アセンブリは、Data.dll の型をシリアル化および逆シリアル化する必要のあるコードから参照できます。  
  
## <a name="see-also"></a>関連項目

- [ツール](../../framework/tools/index.md)
- [Visual Studio 用開発者コマンド プロンプト](../../framework/tools/developer-command-prompt-for-vs.md)
