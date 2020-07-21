---
title: ホストするための Direct3D9 コンテンツを作成する
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 847ee74da5b295c2c9d3824b3df74f94bc98a4db
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76727916"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>チュートリアル: WPF でホストするための Direct3D9 コンテンツの作成
このチュートリアルでは、Windows Presentation Foundation (WPF) アプリケーションでのホスティングに適した Direct3D9 コンテンツを作成する方法について説明します。 WPF アプリケーションで Direct3D9 コンテンツをホストする方法の詳細については、「[WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)」を参照してください。

 このチュートリアルでは次のタスクを実行します。

- Direct3D9 プロジェクトを作成する。

- WPF アプリケーションでホストするための Direct3D9 プロジェクトを構成する。

 完了すると、WPF アプリケーションで使用する Direct3D9 コンテンツを含む DLL が作成されます。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2010。

- DirectX SDK 9 以降。

## <a name="creating-the-direct3d9-project"></a>Direct3D9 プロジェクトの作成
 最初の手順は、Direct3D9 プロジェクトを作成して構成することです。

#### <a name="to-create-the-direct3d9-project"></a>Direct3D9 プロジェクトを作成するには

1. C++ で `D3DContent` という新しい Win32 プロジェクトを作成します。

     Win32 アプリケーション ウィザードが開き、ようこそ画面が表示されます。

2. **[次へ]** をクリックします。

     [アプリケーションの設定] 画面が表示されます。

3. **[アプリケーションの種類]** セクションで、 **[DLL]** オプションを選択します。

4. **[完了]** をクリックします。

     D3DContent プロジェクトが生成されます。

5. ソリューション エクスプローラーで、D3DContent プロジェクトを右クリックし、 **[プロパティ]** をクリックします。

     **[D3DContent プロパティ ページ]** ダイアログ ボックスが開きます。

6. **[C/C++]** ノードを選択します。

7. **[追加のインクルード ディレクトリ]** フィールドで、DirectX インクルード フォルダーの場所を指定します。 このフォルダーの既定の場所は、%ProgramFiles%\Microsoft DirectX SDK (*version*)\Include です。

8. **[リンカー]** ノードをダブルクリックして展開します。

9. **[追加のライブラリ ディレクトリ]** フィールドで、DirectX ライブラリ フォルダーの場所を指定します。 このフォルダーの既定の場所は、%ProgramFiles%\Microsoft DirectX SDK (*version*)\Lib\x86 です。

10. **[入力]** ノードを選択します。

11. **[追加の依存ファイル]** フィールドに、`d3d9.lib` ファイルと `d3dx9.lib` ファイルを追加します。

12. ソリューション エクスプローラーで、`D3DContent.def` という新しいモジュール定義ファイル (.def) をプロジェクトに追加します。

## <a name="creating-the-direct3d9-content"></a>Direct3D9 コンテンツの作成
 最適なパフォーマンスを得るには、Direct3D9 コンテンツで特定の設定を使用する必要があります。 次のコードは、最適なパフォーマンス特性を持つ Direct3D9 サーフェイスを作成する方法を示しています。 詳細については、「[Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)」を参照してください。

#### <a name="to-create-the-direct3d9-content"></a>Direct3D9 コンテンツを作成するには

1. ソリューション エクスプローラーを使用して、次のような名前のプロジェクトに 3 つの C++ クラスを追加します。

     `CRenderer` (仮想デストラクターを使用)

     `CRendererManager`

     `CTriangleRenderer`

2. コード エディターで Renderer.h を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3. コード エディターで Renderer.cpp を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4. コード エディターで RendererManager.h を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5. コード エディターで RendererManager.cpp を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6. コード エディターで TriangleRenderer.h を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7. コード エディターで TriangleRenderer.cpp を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8. コード エディターで stdafx.h を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. コード エディターで dllmain.cpp を開き、自動生成されたコードを次のコードに置き換えます。

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. コード エディターで D3DContent.def を開きます。

11. 自動生成されたコードを次のコードに置き換えます。

    ```cpp
    LIBRARY "D3DContent"

    EXPORTS

    SetSize
    SetAlpha
    SetNumDesiredSamples
    SetAdapter

    GetBackBufferNoRef
    Render
    Destroy
    ```

12. プロジェクトをビルドします。

## <a name="next-steps"></a>次の手順

- WPF アプリケーションで Direct3D9 コンテンツをホストします。 詳細については、「[チュートリアル:WPF での Direct3D9 コンテンツのホスト](walkthrough-hosting-direct3d9-content-in-wpf.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [チュートリアル: WPF での Direct3D9 コンテンツのホスト](walkthrough-hosting-direct3d9-content-in-wpf.md)
