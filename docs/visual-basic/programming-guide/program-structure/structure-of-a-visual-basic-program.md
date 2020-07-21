---
title: Visual Basic プログラムの構造
ms.date: 07/20/2015
helpviewer_keywords:
- conditional compilation [Visual Basic], Visual Basic
- program structure [Visual Basic], Visual Basic
- procedures [Visual Basic], structure
- Visual Basic code, program structure
ms.assetid: ad0c6531-d762-4c77-a700-de16b07b6119
ms.openlocfilehash: dc6b38d78f02a42c8e7cc2aa964e9f3f74996f44
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408765"
---
# <a name="structure-of-a-visual-basic-program"></a>Visual Basic プログラムの構造
Visual Basic プログラムは、標準の構成要素から構築します。 "*ソリューション*" は、1 つ以上のプロジェクトで構成します。 "*プロジェクト*" には、1 つ以上のアセンブリを含めることができます。 各 "*アセンブリ*" は、1 つ以上のソース ファイルからコンパイルします。 "*ソース ファイル*" では、クラス、構造体、モジュール、インターフェイスの定義と実装が提供され、最終的にはすべてのコードが含まれます。  
  
 Visual Basic プログラムのこれらの構成要素の詳細については、[ソリューションとプロジェクト](/visualstudio/ide/solutions-and-projects-in-visual-studio)および [.NET のアセンブリ](../../../standard/assembly/index.md)に関する記事をご覧ください。  
  
## <a name="file-level-programming-elements"></a>ファイルレベルのプログラミング要素  
 プロジェクトまたはファイルを起動してコード エディターを開くと、いくつかのコードが既に配置され、正しい順序で表示されていることがわかります。 記述するすべてのコードで、次のシーケンスに従う必要があります。  
  
1. `Option` ステートメント  
  
2. `Imports` ステートメント  
  
3. `Namespace` ステートメントと名前空間レベルの要素  
  
 ステートメントを異なる順序で入力すると、コンパイル エラーが発生する可能性があります。  
  
 プログラムには、条件付きコンパイル ステートメントを含めることもできます。 ソース ファイル内で、前のシーケンスのステートメントの間にこれらを挿入することができます。  
  
### <a name="option-statements"></a>Option ステートメント  
 `Option` ステートメントを使用すると、後続のコードに対して基本ルールを確立し、構文エラーと論理エラーを防ぐことができます。 [Option Explicit ステートメント](../../language-reference/statements/option-explicit-statement.md)を使用すると、すべての変数の宣言とスペルが正しいことを保証できるため、デバッグ時間が短縮されます。 [Option Strict ステートメント](../../language-reference/statements/option-strict-statement.md)を使用すると、データ型が異なる変数間の処理で発生する可能性がある論理エラーとデータ損失を最小限に抑えることができます。 [Option Compare ステートメント](../../language-reference/statements/option-compare-statement.md)では、文字列を `Binary` または `Text` の値に基づいて相互比較する方法を指定します。  
  
### <a name="imports-statements"></a>Imports ステートメント  
 [Imports ステートメント (.NET 名前空間および型)](../../language-reference/statements/imports-statement-net-namespace-and-type.md) を含めて、プロジェクトの外部で定義されている名前をインポートすることができます。 `Imports` ステートメントを使用すると、インポートする名前空間内で定義されているクラスやその他の型を、修飾することなくコード内で参照できます。 `Imports` ステートメントは必要な数だけ使用できます。 詳細については、「[参照と Imports ステートメント](references-and-the-imports-statement.md)」を参照してください。  
  
### <a name="namespace-statements"></a>Namespace ステートメント  
 名前空間を使用すると、プログラミング要素を編成、分類でき、グループ化とアクセスが容易になります。 [Namespace ステートメント](../../language-reference/statements/namespace-statement.md)を使用すると、特定の名前空間内の後続のステートメントを分類できます。 詳細については、「[Visual Basic における名前空間](namespaces.md)」を参照してください。  
  
### <a name="conditional-compilation-statements"></a>条件付きコンパイル ステートメント  
 条件付きコンパイル ステートメントは、ソース ファイル内のほぼどこにでも記述できます。 コンパイル時に、特定の条件に応じて、コードの一部を含める、または除外することができます。 条件付きコードはデバッグ モードでのみ実行されるため、アプリケーションのデバッグにも使用できます。 詳細については、[条件付きコンパイル](conditional-compilation.md)に関するページを参照してください。  
  
## <a name="namespace-level-programming-elements"></a>名前空間レベルのプログラミング要素  
 ソース ファイル内のすべてのコードは、クラス、構造体、モジュールに含まれます。 これらは "*名前空間レベル*" の要素であり、名前空間内またはソース ファイル レベルで記述することができます。 他のすべてのプログラミング要素の宣言が保持されます。 また、要素シグネチャを定義するが実装を提供しないインターフェイスは、モジュール レベルで記述します。 モジュールレベルの要素の詳細については、次を参照してください。  
  
- [Class ステートメント](../../language-reference/statements/class-statement.md)  
  
- [Structure ステートメント](../../language-reference/statements/structure-statement.md)  
  
- [Module ステートメント](../../language-reference/statements/module-statement.md)  
  
- [Interface ステートメント](../../language-reference/statements/interface-statement.md)  
  
 名前空間レベルのデータ要素は、列挙型とデリゲートです。  
  
## <a name="module-level-programming-elements"></a>モジュールレベルのプログラミング要素  
 プロシージャ、演算子、プロパティ、イベントは、実行可能コード (実行時にアクションを実行するステートメント) を保持できる唯一のプログラミング要素です。 これらは、プログラムの "*モジュールレベル*" の要素です。 プロシージャレベルの要素の詳細については、次を参照してください。  
  
- [Function ステートメント](../../language-reference/statements/function-statement.md)  
  
- [Sub ステートメント](../../language-reference/statements/sub-statement.md)  
  
- [Declare ステートメント](../../language-reference/statements/declare-statement.md)  
  
- [Operator ステートメント](../../language-reference/statements/operator-statement.md)  
  
- [Property ステートメント](../../language-reference/statements/property-statement.md)  
  
- [Event ステートメント](../../language-reference/statements/event-statement.md)  
  
 モジュール レベルのデータ要素は、変数、定数、列挙型、デリゲートです。  
  
## <a name="procedure-level-programming-elements"></a>プロシージャレベルのプログラミング要素  
 "*プロシージャレベル*" の要素の内容の大部分は実行可能なステートメントであり、プログラムの実行時コードを構成します。 すべての実行可能コードは、何らかのプロシージャ (`Function`、`Sub`、`Operator`、`Get`、`Set`、`AddHandler`、`RemoveHandler`、`RaiseEvent`) 内にある必要があります。 詳細については、「[ステートメント](../language-features/statements.md)」を参照してください。  
  
 プロシージャ レベルのデータ要素は、ローカル変数と定数に制限されます。  
  
## <a name="the-main-procedure"></a>Main プロシージャ  
 `Main` プロシージャは、アプリケーションが読み込まれたときに実行される最初のコードです。 `Main` は、アプリケーションの開始点および全体的な制御として機能します。 `Main` には、次の 4 種類があります。  
  
- `Sub Main()`  
  
- `Sub Main(ByVal cmdArgs() As String)`  
  
- `Function Main() As Integer`  
  
- `Function Main(ByVal cmdArgs() As String) As Integer`  
  
 このプロシージャの中で最も一般的なものは `Sub Main()` です。 詳細については、「[Visual Basic の Main プロシージャ](main-procedure.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の Main プロシージャ](main-procedure.md)
- [Visual Basic の名前付け規則](naming-conventions.md)
- [Visual Basic の制限事項](limitations.md)
