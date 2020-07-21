---
title: Azure HDInsight Spark クラスター上の Jupyter Notebook に .NET for Apache Spark をインストールする
description: Azure HDInsight の Jupyter Notebook に .NET for Apache Spark をインストールする方法について説明します。
ms.date: 06/25/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 14babf7a551192b286f309393e3bbff25d4745d5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617744"
---
# <a name="install-net-for-apache-spark-on-jupyter-notebooks-on-azure-hdinsight-spark-clusters"></a>Azure HDInsight Spark クラスター上の Jupyter Notebook に .NET for Apache Spark をインストールする

この記事では、Azure HDInsight Spark クラスター上の Jupyter Notebook に .NET for Apache Spark をインストールする方法について説明します。 コマンド ラインと Azure portal を組み合わせて、Azure HDInsight クラスターに .NET for Apache Spark をデプロイすることができます (詳しくは [Azure HDInsight に .NET for Apache Spark アプリケーションをデプロイする方法](../tutorials/hdinsight-deployment.md)に関する記事を参照)。ただし、ノートブックにはより対話的で反復的なエクスペリエンスが用意されています。

Azure HDInsight クラスターには既に Jupyter Notebook が付属しているため、.NET for Apache Spark を実行するように Jupyter Notebook を構成するだけで済みます。 Jupyter Notebook で .NET for Apache Spark を使用する場合、C# コードを 1 行ずつ実行し、必要に応じて実行状態を維持するために、C# REPL が必要です。 [Try .NET](https://github.com/dotnet/try) は、公式の .NET REPL として統合されています。

Jupyter Notebook のエクスペリエンスを通じて .NET for Apache Spark を有効にするには、[Ambari](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-manage-ambari) を使用したいくつかの手動の手順に従い、HDInsight Spark クラスターで[スクリプト アクション](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)を送信する必要があります。

> [!NOTE]
> この機能は "*試験段階*" であり、HDInsight Spark チームではサポートされていません。

[!INCLUDE [spark-preview-note](../../../includes/spark-preview-note.md)]

## <a name="prerequisites"></a>必須コンポーネント

まだお持ちでない場合は、[Azure HDInsight Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-apache-spark-cluster-in-hdinsight) クラスターを作成します。

1. [Azure portal](https://portal.azure.com) にアクセスし、 **[+ リソースの作成]** を選択します。

1. 新しい Azure HDInsight クラスターのリソースを作成します。 クラスターの作成中に、**Spark 2.4** と **HDI 4.0** を選択します。

## <a name="install-net-for-apache-spark"></a>.NET for Apache Spark のインストール

Azure portal で、前の手順で作成した **HDInsight Spark クラスター**を選択します。

### <a name="stop-the-livy-server"></a>Livy サーバーを停止する

1. ポータルで **[概要]** を選択した後、 **[Ambari ホーム]** を選択します。 入力を求められたら、クラスターのログイン資格情報を入力します。

   ![Livy サーバーを停止する](./media/hdinsight-notebook-installation/select-ambari.png)

2. 左側のナビゲーション メニューから **[Spark2]** を選択し、 **[LIVY FOR SPARK2 SERVER]\(Spark2 の Livy サーバー\)** を選択します。

   ![Livy サーバーを停止する](./media/hdinsight-notebook-installation/select-livyserver.png)

3. **hn0 で始まるホスト**を選択します。

   ![Livy サーバーを停止する](./media/hdinsight-notebook-installation/select-host.png)

4. **[Livy for Spark2 Server]\(Spark2 の Livy サーバー\)** の横にある省略記号を選択し、 **[停止]** を選択します。 メッセージが表示されたら、 **[OK]** を選択して続行します。

   Spark2 の Livy サーバーを停止します。
   ![Livy サーバーを停止する](./media/hdinsight-notebook-installation/stop-server.png)

5. **hn1 で始まるホスト**に対して前の手順を繰り返します。

### <a name="submit-an-hdinsight-script-action"></a>HDInsight スクリプト アクションを送信する

1. `install-interactive-notebook.sh` は、.NET for Apache Spark をインストールし、Apache Livy と sparkmagic に変更を加えるスクリプトです。 スクリプト アクションを HDInsight に送信する前に、`install-interactive-notebook.sh` を作成してアップロードする必要があります。

   ご自分のローカル コンピューターに **install-interactive-notebook.sh** という名前の新しいファイルを作成し、[install-interactive-notebook.sh の内容](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh)を貼り付けます。

   このスクリプトを、HDInsight クラスターからアクセスできる [URI](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) にアップロードします。 たとえば、`https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh` のようにします。

2. [HDInsight スクリプト アクション](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)を使用して、クラスターで `install-interactive-notebook.sh` を実行します。

   Azure portal で HDI クラスターに戻り、左側のオプションから **[スクリプト アクション]** を選択します。 HDInsight Spark クラスターに .NET for Apache Spark の REPL をデプロイするためのスクリプト アクションを 1 つ送信します。 次の設定を使用します。

   |プロパティ  |説明  |
   |---------|---------|
   | スクリプトの種類 | カスタム |
   | 名前 | " *.NET for Apache Spark 対話型 Notebook エクスペリエンスをインストールする*" |
   | Bash スクリプト URI | `install-interactive-notebook.sh` のアップロード先の URI。 |
   | ノードの種類| ヘッド、ワーカー |
   | パラメーター | .NET for Apache Spark のバージョン。 [.NET for Apache Spark のリリース](https://github.com/dotnet/spark/releases)を確認できます。 たとえば、Sparkdotnet バージョン 0.6.0 をインストールする場合は、`0.6.0` とします。

   スクリプト アクションの状態の横に緑色のチェックマークが表示されたら、次の手順に進みます。

### <a name="start-the-livy-server"></a>Livy サーバーを起動する

「[Livy サーバーを停止する](#stop-the-livy-server)」セクションの手順に従って、ホスト **hn0** と **hn1** に対して Spark2 の Livy サーバーを **[開始]** ( **[停止]** ではなく) します。

### <a name="set-up-spark-default-configurations"></a>Spark の既定の構成を設定する

1. ポータルで **[概要]** を選択した後、 **[Ambari ホーム]** を選択します。 入力を求められたら、クラスターのログイン資格情報を入力します。

2. **[Spark2]** 、 **[CONFIGS]\(構成\)** の順に選択します。 次に、 **[Custom spark2-defaults]\(カスタム Spark2 既定値\)** を選択します。

   ![構成の設定](./media/hdinsight-notebook-installation/spark-configs.png)

3. **[プロパティの追加...]** を選択して、Spark の既定の設定を追加します。

   ![プロパティの追加](./media/hdinsight-notebook-installation/add-property.png)

   個別のプロパティが 3 つあります。 単一プロパティの追加モードで、**TEXT** プロパティの型を使用して、一度に 1 つずつ追加します。 いずれのキーまたは値の前後にも、余分なスペースがないことを確認してください。

   * **プロパティ 1**
       * キー: &ensp;&ensp;`spark.dotnet.shell.command`
       * 値: `/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`

   * **プロパティ 2** 前のスクリプト アクションに含めた .NET for Apache Spark のバージョンを使用してください。
       * キー: &ensp;&ensp;`spark.dotnet.packages`
       * 値: `["nuget: Microsoft.Spark, 0.6.0", "nuget: Microsoft.Spark.Extensions.Delta, 0.6.0"]`

   * **プロパティ 3**
       * キー: &ensp;&ensp;`spark.dotnet.interpreter`
       * 値: `try`

   たとえば、次の画像は、プロパティ 1 を追加するための設定をキャプチャしたものです。

   ![構成の設定](./media/hdinsight-notebook-installation/add-sparkconfig.png)

   3 つのプロパティを追加したら、 **[保存]** を選択します。 構成の推奨事項に関する警告画面が表示された場合は、 **[PROCEED ANYWAY]\(警告を無視して続行\)** を選択します。

4. 影響を受けたコンポーネントを再起動します。

   新しいプロパティを追加したら、その変更の影響を受けたコンポーネントを再起動する必要があります。 上部にある **[再起動]** を選択して、ドロップダウンから **[影響を受けるものをすべて再起動する]** を選択します。

   ![構成の設定](./media/hdinsight-notebook-installation/restart-affected.png)

   メッセージが表示されたら、 **[CONFIRM RESTART ALL]\(すべて再起動\)** を選択して続行し、 **[OK]** をクリックして完了します。

## <a name="submit-jobs-through-a-jupyter-notebook"></a>Jupyter Notebook を使用してジョブを送信する

前の手順を完了したら、Jupyter Notebook を使用して .NET for Apache Spark ジョブを送信できるようになります。

1. 新しい .NET for Apache Spark ノートブックを作成します。 Azure portal で、HDI クラスターから Jupyter Notebook を起動します。

   ![Jupyter Notebook を起動する](./media/hdinsight-notebook-installation/launch-notebook.png)

   次に、 **[新規]**  >  **[.NET Spark (C#)]** の順に選択して、ノートブックを作成します。

   ![Jupyter Notebook](./media/hdinsight-notebook-installation/create-sparkdotnet-notebook.png)

2. .NET for Apache Spark を使用してジョブを送信します。

   次のコード スニペットを使用して、データフレームを作成します。

   ```csharp
   var df = spark.Range(0,5);
   df.Show();
   ```

   ![Spark ジョブを送信する](./media/hdinsight-notebook-installation/create-df.png)

   次のコード スニペットを使用して、ユーザー定義関数 (UDF) を登録し、データフレームを指定してその UDF を使用します。

   ```csharp
   var myawesomeudf = Udf<int, string>((id) => $"hello {id}");
   df.Select(myawesomeudf(df["id"])).Show();
   ```

   ![Spark ジョブを送信する](./media/hdinsight-notebook-installation/run-udf.png)

## <a name="next-steps"></a>次の手順

* [.NET for Apache Spark アプリケーションを Azure HDInsight にデプロイする](../tutorials/hdinsight-deployment.md)
* [HDInsight のドキュメント](https://docs.microsoft.com/azure/hdinsight/)
