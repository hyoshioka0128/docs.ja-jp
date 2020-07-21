---
title: '方法: クエリを使用してモデル定義関数を呼び出す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c804e4d-f348-4afd-9f63-d3f0f24bc6a9
ms.openlocfilehash: 33f26896dd0d4ff08beb4a011fa6bd468cba7207
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250756"
---
# <a name="how-to-call-model-defined-functions-in-queries"></a>方法: クエリを使用してモデル定義関数を呼び出す
このトピックでは、概念モデルで定義されている関数を LINQ to Entities クエリから呼び出す方法について説明します。  
  
 以下に示す手順は、モデル定義関数を LINQ to Entities クエリから呼び出す方法をまとめたものです。 各手順の詳しい説明は、その後の例で示します。 この手順では、関数を概念モデルで定義済みであると想定します。 詳細については、[概念モデルでカスタム関数を定義する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))」を参照してください。  
  
### <a name="to-call-a-function-defined-in-the-conceptual-model"></a>概念モデルで定義された関数を呼び出すには  
  
1. 概念モデルで定義された関数にマップされているアプリケーションに、共通言語ランタイム (CLR) メソッドを追加します。 メソッドをマップするには、ユーザーが <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> をメソッドに適用する必要があります。 属性の <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> パラメーターと <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> パラメーターが、それぞれ概念モデルの名前空間名と関数名であることに注意してください。 LINQ の関数名解決では、大文字と小文字が区別されます。  
  
2. LINQ to Entities クエリから関数を呼び出します。  
  
## <a name="example"></a>例  
 次の例は、概念モデルで定義されている関数を LINQ to Entities クエリから呼び出す方法を示しています。 この例では、School モデルを使用します。 School モデルの詳細については、「[School サンプル データベースの作成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))」と「[School .edmx ファイルの生成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100))」を参照してください。  
  
 次の概念モデル関数は、あるインストラクターが雇用されてから経過した年数を返します。 関数を概念モデルに追加する方法については、「[方法:概念モデルでカスタム関数を定義する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))」を参照してください。)  
  
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp conceptualmodelfunctions/xml/school.edmx#1)]
  
## <a name="example"></a>例  
 次に、次のメソッドをアプリケーションに追加し、<xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> を使用して概念モデル関数にマップします。  
  
 [!code-csharp[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#2)]
 [!code-vb[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#2)]  
  
## <a name="example"></a>例  
 これで、LINQ to Entities クエリから概念モデル関数を呼び出すことができます。 次のコードは、雇用年数が 10 年を超えるすべてのインストラクターを表示するメソッドを呼び出します。  
  
 [!code-csharp[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#3)]
 [!code-vb[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [.edmx ファイルの概要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
- [LINQ to Entities クエリ内の関数の呼び出し](calling-functions-in-linq-to-entities-queries.md)
- [方法: モデル定義関数をオブジェクト メソッドとして呼び出す](how-to-call-model-defined-functions-as-object-methods.md)
