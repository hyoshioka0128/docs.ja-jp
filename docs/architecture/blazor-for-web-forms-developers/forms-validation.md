---
title: フォームと検証
description: でクライアント側の検証を使用してフォームを構築する方法について説明 Blazor します。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- Blazor WebAssembly
ms.date: 09/19/2019
ms.openlocfilehash: 1a99719f59415872510aef051d1f3c73daf53e15
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173277"
---
# <a name="forms-and-validation"></a>フォームと検証

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

ASP.NET Web Forms framework には、フォーム (、、など) に入力されたユーザー入力の検証を処理する一連の検証サーバーコントロールが含まれてい `RequiredFieldValidator` `CompareValidator` `RangeValidator` ます。 ASP.NET Web Forms framework では、モデルのバインドと、データ注釈 (、、など) に基づくモデルの検証もサポートされて `[Required]` `[StringLength]` `[Range]` います。 検証ロジックは、控えめな JavaScript ベースの検証を使用して、サーバーとクライアントの両方に適用できます。 `ValidationSummary`サーバーコントロールは、検証エラーの概要をユーザーに表示するために使用されます。

Blazorでは、クライアントとサーバーの間の検証ロジックの共有がサポートされています。 ASP.NET には、多くの一般的なサーバー検証の事前構築済みの JavaScript 実装が用意されています。 多くの場合、開発者は、アプリ固有の検証ロジックを完全に実装するために JavaScript を作成する必要があります。 サーバーとクライアントの両方で、同じモデル型、データ注釈、および検証ロジックを使用できます。

Blazor入力コンポーネントのセットを提供します。 入力コンポーネントは、モデルへのフィールドデータのバインドを処理し、フォームが送信されたときにユーザー入力を検証します。

|入力コンポーネント|レンダリングされた HTML 要素    |
|---------------|-------------------------|
|`InputCheckbox`|`<input type="checkbox">`|
|`InputDate`    |`<input type="date">`    |
|`InputNumber`  |`<input type="number">`  |
|`InputSelect`  |`<select>`               |
|`InputText`    |`<input>`                |
|`InputTextArea`|`<textarea>`             |

コンポーネントは、 `EditForm` これらの入力コンポーネントをラップし、を使用して検証プロセスを調整し `EditContext` ます。 を作成するときは `EditForm` 、パラメーターを使用して、バインドするモデルインスタンスを指定し `Model` ます。 通常、検証はデータ注釈を使用して行われ、拡張可能です。 データ注釈に基づく検証を有効にするには、コンポーネントをの `DataAnnotationsValidator` 子として追加し `EditForm` ます。 コンポーネントには、 `EditForm` 有効な ( `OnValidSubmit` ) および無効な () 送信を処理するための便利なイベントが用意されて `OnInvalidSubmit` います。 また `OnSubmit` 、検証を自分でトリガーして処理できるようにする、より汎用的なイベントもあります。

検証エラーの概要を表示するには、コンポーネントを使用し `ValidationSummary` ます。 特定の入力フィールドの検証メッセージを表示するには、コンポーネントを使用して、 `ValidationMessage` `For` 適切なモデルメンバーを指すパラメーターのラムダ式を指定します。

次の種類のモデルでは、データ注釈を使用して複数の検証規則を定義しています。

```csharp
using System;
using System.ComponentModel.DataAnnotations;

public class Starship
{
    [Required]
    [StringLength(16,
        ErrorMessage = "Identifier too long (16 character limit).")]
    public string Identifier { get; set; }

    public string Description { get; set; }

    [Required]
    public string Classification { get; set; }

    [Range(1, 100000,
        ErrorMessage = "Accommodation invalid (1-100000).")]
    public int MaximumAccommodation { get; set; }

    [Required]
    [Range(typeof(bool), "true", "true",
        ErrorMessage = "This form disallows unapproved ships.")]
    public bool IsValidatedDesign { get; set; }

    [Required]
    public DateTime ProductionDate { get; set; }
}
```

次のコンポーネントは Blazor 、モデルの種類に基づいて、でフォームを構築する方法を示してい `Starship` ます。

```razor
<h1>New Ship Entry Form</h1>

<EditForm Model="@starship" OnValidSubmit="@HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />

    <p>
        <label for="identifier">Identifier: </label>
        <InputText id="identifier" @bind-Value="starship.Identifier" />
        <ValidationMessage For="() => starship.Identifier" />
    </p>
    <p>
        <label for="description">Description (optional): </label>
        <InputTextArea id="description" @bind-Value="starship.Description" />
    </p>
    <p>
        <label for="classification">Primary Classification: </label>
        <InputSelect id="classification" @bind-Value="starship.Classification">
            <option value="">Select classification ...</option>
            <option value="Exploration">Exploration</option>
            <option value="Diplomacy">Diplomacy</option>
            <option value="Defense">Defense</option>
        </InputSelect>
        <ValidationMessage For="() => starship.Classification" />
    </p>
    <p>
        <label for="accommodation">Maximum Accommodation: </label>
        <InputNumber id="accommodation" @bind-Value="starship.MaximumAccommodation" />
        <ValidationMessage For="() => starship.MaximumAccommodation" />
    </p>
    <p>
        <label for="valid">Engineering Approval: </label>
        <InputCheckbox id="valid" @bind-Value="starship.IsValidatedDesign" />
        <ValidationMessage For="() => starship.IsValidatedDesign" />
    </p>
    <p>
        <label for="productionDate">Production Date: </label>
        <InputDate id="productionDate" @bind-Value="starship.ProductionDate" />
        <ValidationMessage For="() => starship.ProductionDate" />
    </p>

    <button type="submit">Submit</button>
</EditForm>

@code {
    private Starship starship = new Starship();

    private void HandleValidSubmit()
    {
        // Save the data
    }
}
```

フォームの送信後、モデルバインドデータは、データベースのようなデータストアに保存されていません。 アプリでは、 Blazor WebAssembly データをサーバーに送信する必要があります。 たとえば、HTTP POST 要求を使用します。 Blazorサーバーアプリでは、データはサーバーに既に存在していますが、保存する必要があります。 アプリでのデータアクセス Blazor の処理は、データの処理に[関する](data.md)セクションの対象です。

## <a name="additional-resources"></a>その他の技術情報

アプリの[フォームと検証](/aspnet/core/blazor/forms-validation)の詳細につい Blazor ては、のドキュメントを参照してください Blazor 。

>[!div class="step-by-step"]
>[前へ](state-management.md)
>[次へ](data.md)
