---
title: My.Resources オブジェクト
ms.date: 07/20/2015
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
ms.openlocfilehash: 2b7c82c31d2e31ccbf573cf1dfa138af2d99ce29
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372461"
---
# <a name="myresources-object"></a>My.Resources オブジェクト
アプリケーションのリソースにアクセスするためのプロパティとクラスを提供します。  
  
## <a name="remarks"></a>Remarks  
 `My.Resources` オブジェクトは、アプリケーションのリソースへのアクセスを提供し、アプリケーションのリソースを動的に取得できるようにします。 詳細については、「[アプリケーション リソースの管理 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)」を参照してください。  
  
 `My.Resources` オブジェクトは、グローバル リソースのみを公開します。 フォームに関連付けられたリソース ファイルへのアクセスは提供しません。 フォームのリソースには、フォームからアクセスする必要があります。  
  
 `My.Resources` オブジェクトから、アプリケーションのカルチャ固有のリソース ファイルにアクセスできます。 既定では、`My.Resources` オブジェクトは、<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> プロパティのカルチャに一致するリソース ファイルからリソースを検索します。 ただし、この動作をオーバーライドして、リソースに使用する特定のカルチャを指定することができます。 詳細については、「[デスクトップ アプリケーションのリソース](../../../framework/resources/index.md)」を参照してください。  
  
## <a name="properties"></a>プロパティ  
 `My.Resources` オブジェクトのプロパティは、アプリケーションのリソースへの読み取り専用アクセスを提供します。 リソースを追加または削除するには、**プロジェクト デザイナー**を使用します。 `My.Resources.`*resourceName* を使用することで、**プロジェクト デザイナー**を使用して追加されたリソースにアクセスできます。  
  
 また、**ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[新しい項目の追加]** または **[既存項目の追加]** をクリックして、リソース ファイルを追加または削除することもできます。 この方法で追加されたリソースには、`My.Resources.`*resourceFileName*`.`*resourceName* を使用してアクセスできます。  
  
 各リソースには名前、カテゴリ、および値が含まれ、これらのリソース設定によって、リソースにアクセスするためのプロパティが `My.Resources` オブジェクトにどのように表示されるかが決まります。 **プロジェクト デザイナー**で追加したリソースの場合:  
  
- 名前はプロパティの名前を決定します。  
  
- リソース データはプロパティの値です。  
  
- カテゴリはプロパティの型を決定します。  
  
|カテゴリ|プロパティのデータ型|  
|---|---|  
|**文字列**|[String](../data-types/string-data-type.md)|  
|**イメージ**|<xref:System.Drawing.Bitmap>|  
|**アイコン**|<xref:System.Drawing.Icon>|  
|**オーディオ**|<xref:System.IO.UnmanagedMemoryStream><br /><br /> <xref:System.IO.UnmanagedMemoryStream> クラスは <xref:System.IO.Stream> クラスから導出されるため、<xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> メソッドなどのストリームを受け取るメソッドで使用できます。|  
|**ファイル**|-   [String](../data-types/string-data-type.md) (テキスト ファイルの場合)。<br />-   <xref:System.Drawing.Bitmap> (イメージ ファイルの場合)。<br />-   <xref:System.Drawing.Icon> (アイコン ファイルの場合)。<br />-   <xref:System.IO.UnmanagedMemoryStream> (音声ファイルの場合)。|  
|**その他**|デザイナーの **[型]** 列の情報によって決まります。|  
  
## <a name="classes"></a>クラス  
 `My.Resources` オブジェクトは、各リソース ファイルを共有プロパティを持つクラスとして公開します。 クラス名は、リソース ファイルの名前と同じです。 前のセクションで説明したように、リソース ファイル内のリソースはクラスのプロパティとして公開されます。  
  
## <a name="example"></a>例  
 この例では、フォームのタイトルを、アプリケーション リソース ファイル内の `Form1Title` という名前の文字列リソースに設定します。 この例を機能させるには、アプリケーションのリソース ファイルに `Form1Title` という名前の文字列が必要です。  
  
 [!code-vb[VbVbalrMyResources#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#1)]  
  
## <a name="example"></a>例  
 この例では、フォームのアイコンを、アプリケーションのリソース ファイルに格納されている `Form1Icon` という名前のアイコンに設定します。 この例を機能させるには、アプリケーションのリソース ファイルに `Form1Icon` という名前のアイコンが必要です。  
  
 [!code-vb[VbVbalrMyResources#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#2)]  
  
## <a name="example"></a>例  
 この例では、フォームの背景イメージを、アプリケーション リソース ファイル内にある `Form1Background` という名前のイメージ リソースに設定します。 この例を機能させるには、アプリケーションのリソース ファイルに `Form1Background` という名前のイメージ リソースが必要です。  
  
 [!code-vb[VbVbalrMyResources#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#3)]  
  
## <a name="example"></a>例  
 この例では、アプリケーションのリソースファイルに `Form1Greeting` という名前のオーディオ リソースとして格納されているサウンドを再生します。 この例を機能させるには、アプリケーションのリソース ファイルに `Form1Greeting` という名前のオーディオ リソースが必要です。 `My.Computer.Audio.Play` は、Windows フォーム アプリケーションでのみ使用できます。  
  
 [!code-vb[VbVbalrMyResources#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#4)]  
  
## <a name="example"></a>例  
 この例では、フランス語のカルチャ バージョンのアプリケーションの文字列リソースを取得します。 リソースには `Message` という名前が付けられます。 `My.Resources` オブジェクトが使用するカルチャを変更するために、この例では <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A> を使用しています。  
  
 この例を機能させるには、アプリケーションのリソース ファイルに `Message` という名前の文字列が必要であり、アプリケーションには、そのリソース ファイルのフランス語のカルチャ バージョン、Resources.fr-FR.resx が必要です。 アプリケーションにフランス語のカルチャ バージョンのリソース ファイルがない場合、`My.Resource` オブジェクトは、既定のカルチャ リソース ファイルからリソースを取得します。  
  
 [!code-vb[VbVbalrMyResources#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#10)]  
  
## <a name="see-also"></a>関連項目

- [アプリケーション リソースの管理 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)
- [デスクトップ アプリケーションのリソース](../../../framework/resources/index.md)
