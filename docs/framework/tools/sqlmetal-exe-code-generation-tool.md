---
title: SqlMetal.exe (コード生成ツール)
ms.date: 03/30/2017
helpviewer_keywords:
- SQLMetal [LINQ to SQL]
- code generation tool
- SQLMetal.exe
- LINQ to SQL, serialization
- LINQ to SQL, DBML files
- LINQ to SQL, SQLMetal
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
ms.openlocfilehash: d5b4c2b59b585b3d3a3584ef9055e70c9d998e85
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2020
ms.locfileid: "71044075"
---
# <a name="sqlmetalexe-code-generation-tool"></a>SqlMetal.exe (コード生成ツール)
SqlMetal コマンドライン ツールは、.NET Framework の [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] コンポーネント用のコードとマッピングを生成します。 このトピックで後述するオプションを適用することにより、次のようなアクションを SqlMetal で実行できます。  
  
- データベースから、ソース コードとマッピング属性またはマッピング ファイルを生成する。  
  
- データベースから、カスタマイズ用の中間的なデータベース マークアップ言語 (.dbml) ファイルを生成する。  
  
- .dbml ファイルから、コードとマッピング属性またはマッピング ファイルを生成する。  
  
 このツールは、Visual Studio と共に自動的にインストールされます。 既定では、このファイルは `drive`:\Program Files\Microsoft SDKs\Windows\v`n.nn`\bin にあります。 Visual Studio をインストールしない場合は、 [Windows SDK](https://go.microsoft.com/fwlink/?LinkId=142225)をダウンロードすることによって SQLMetal ファイルを入手することもできます。  
  
> [!NOTE]
> Visual Studio を使用する開発者は、オブジェクト リレーショナル デザイナーを使用してエンティティ クラスを生成することもできます。 コマンド ライン方式は、大きなデータベースにも適切に対応できます。 SqlMetal はコマンド ライン ツールであるため、ビルド プロセスでこれを使用できます。  
  
 このツールを実行するには、Visual Studio 用開発者コマンド プロンプト (または Windows 7 の Visual Studio コマンド プロンプト) を使用します。 詳細については、「[Visual Studio 用開発者コマンド プロンプト](developer-command-prompt-for-vs.md)」を参照してください。コマンド プロンプトで、次のように入力します。  
  
## <a name="syntax"></a>構文  
  
```console  
sqlmetal [options] [<input file>]  
```  
  
## <a name="options"></a>オプション  
 最新のオプションの一覧を確認するには、コマンド プロンプトでインストール場所に移動し、「 `sqlmetal /?` 」と入力します。  
  
 **接続オプション**  
  
|オプション|説明|  
|------------|-----------------|  
|**/server:** *\<name>*|データベース サーバーの名前を指定します。|  
|**/database:** *\<name>*|サーバー上のデータベース カタログを指定します。|  
|**/user:** *\<name>*|ログオン ユーザー ID を指定します。既定値:Windows 認証の使用。|  
|**/password:** *\<password>*|ログオン パスワードを指定します。 既定値:Windows 認証の使用。|  
|**/conn:** *\<connection string>*|データベース接続文字列を指定します。 **/server**、 **/database**、 **/user**、または **/password** オプションと共に使用することはできません。<br /><br /> 接続文字列にファイル名は含めないでください。 代わりに、コマンド ラインにファイル名を入力ファイルとして追加します。 たとえば、 **sqlmetal /code:"c:\northwind.cs" /language:csharp "c:\northwnd.mdf"** というコマンド ラインは、入力ファイルとして "c:\northwnd.mdf" を指定します。|  
|**/timeout:** *\<seconds>*|SqlMetal がデータベースにアクセスする際のタイムアウト値を指定します。 既定値:0 (時間制限なし)。|  
  
 **抽出オプション**  
  
|オプション|説明|  
|------------|-----------------|  
|**/views**|データベース ビューを抽出します。|  
|**/functions**|データベース関数を抽出します。|  
|**/sprocs**|ストアド プロシージャを抽出します。|  
  
 **出力オプション**  
  
|オプション|説明|  
|------------|-----------------|  
|**/dbml** *[:file]*|出力を .dbml として送ります。 **/map** オプションと共に使用することはできません。|  
|**/code** *[:file]*|出力をソース コードとして送ります。 **/dbml** オプションと共に使用することはできません。|  
|**/map** *[:file]*|属性ではなく XML マッピング ファイルを生成します。 **/dbml** オプションと共に使用することはできません。|  
  
 **その他**  
  
|オプション|説明|  
|------------|-----------------|  
|**/language:** *\<language>*|ソース コードの言語を指定します。<br /><br /> Valid *\<language>* : vb, csharp.<br /><br /> 既定値:コード ファイル名の拡張子から派生します。|  
|**/namespace:** *\<name>*|生成されるコードの名前空間を指定します。 既定値は、名前空間なしです。|  
|**/context:** *\<type>*|データ コンテキスト クラスの名前を指定します。 既定値:データベース名から派生します。|  
|**/entitybase:** *\<type>*|生成されるコード内のエンティティ クラスの基本クラスを指定します。 既定値:エンティティの基本クラスなしです。|  
|**/pluralize**|クラスとメンバーの名前を自動的に複数化または単数化します。<br /><br /> このオプションは、米国英語バージョンでのみ使用できます。|  
|**/serialization:** *\<option>*|シリアル化可能なクラスを生成します。<br /><br /> 有効な *\<オプション>* :None と Unidirectional。 既定値:なし。<br /><br /> 詳細については、「[Serialization](../data/adonet/sql/linq/serialization.md)」 (シリアル化) を参照してください。|  
  
 **入力ファイル**  
  
|オプション|説明|  
|------------|-----------------|  
|**\<入力ファイル>**|SQL Server Express .mdf ファイル、SQL Server Compact 3.5 .sdf ファイル、または .dbml 中間ファイルを指定します。|  
  
## <a name="remarks"></a>Remarks  
 SqlMetal の実際の機能には、次の 2 つの段階が含まれています。  
  
- データベースのメタデータを .dbml ファイルに抽出する。  
  
- コード出力ファイルを生成する。  
  
     適切なコマンド ライン オプションを使用することで、Visual Basic または C# ソース コードを生成するか、XML マッピング ファイルを生成できます。  
  
 メタデータを .mdf ファイルから抽出するには、他のすべてのオプションの後に .mdf ファイルの名前を指定する必要があります。  
  
 **/server** を指定しない場合、 **localhost/sqlexpress** と見なされます。  
  
 Microsoft SQL Server 2005 は、次の条件が少なくとも 1 つ満たされる場合に例外をスローします。  
  
- 自身を呼び出すストアド プロシージャを SqlMetal が抽出しようとした。  
  
- ストアド プロシージャ、関数、またはビューの入れ子レベルが 32 を超える。  
  
     SqlMetal はこの例外をキャッチして、それを警告として報告します。  
  
 入力ファイル名を指定するには、その名前をコマンド ラインに入力ファイルとして追加します。 ( **/conn** オプションを使用して) 接続文字列にファイル名を含める操作は、サポートされていません。  
  
## <a name="examples"></a>使用例  
 抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml**  
  
 SQL Server Express を使用して .mdf ファイルから抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal /dbml:mymeta.dbml mydbfile.mdf**  
  
 SQL Server Express から抽出された SQL メタデータを格納する .dbml ファイルを生成します。  
  
 **sqlmetal /server:.\sqlexpress /dbml:mymeta.dbml /database:northwind**  
  
 .dbml メタデータ ファイルからソース コードを生成します。  
  
 **sqlmetal /namespace:nwind /code:nwind.cs /language:csharp mymetal.dbml**  
  
 SQL メタデータからソース コードを直接生成します。  
  
 **sqlmetal /server:myserver /database:northwind /namespace:nwind /code:nwind.cs /language:csharp**  
  
> [!NOTE]
> サンプル データベース Northwind で **/pluralize** オプションを使用する場合には、注意を必要とする動作があります。 SqlMetal がテーブルのために行型の名前を生成するとき、テーブル名は単数形です。 テーブルに関する <xref:System.Data.Linq.DataContext> プロパティを生成するときには、テーブル名は複数形です。 偶然にも、サンプル データベース Northwind 内のテーブルには既に複数形が使われています。 このため、この部分はうまく機能しません。 データベース テーブルの名前は単数形にするのが一般的ですが、.NET では、コレクションの名前を複数形にすることも一般的です。  
  
## <a name="see-also"></a>関連項目

- [方法: Visual Basic または C# でオブジェクト モデルを生成する](../data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
- [LINQ to SQL でのコード生成](../data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [外部マップ](../data/adonet/sql/linq/external-mapping.md)
