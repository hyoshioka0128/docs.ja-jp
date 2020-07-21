---
title: Windows フォーム上のコントロールのユーザー補助情報の提供
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, accessibility
- controls [Windows Forms], accessibility
- accessibility [Windows Forms], Windows Forms controls
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 887dee6f-5059-4d57-957d-7c6fcd4acb10
ms.openlocfilehash: 672104db94826cfbe113a7ae0ea29546b0c3b9da
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181997"
---
# <a name="providing-accessibility-information-for-controls-on-a-windows-form"></a>Windows フォーム上のコントロールのユーザー補助情報の提供
ユーザー補助機能は専用のプログラムおよびデバイスで、障碍を持つユーザーがコンピューターをより効果的に使用するよう助けます。 たとえば、視覚障碍者のためのスクリーン リーダーや、マウスまたはキーボードではなく音声コマンド入力を利用するユーザーのための音声入力ユーティリティがあります。 これらのユーザー補助機能は、Windows フォーム コントロールによって公開されているアクセシビリティのプロパティと連携します。 それらのプロパティは以下のとおりです。  
  
- **AccessibilityObject**  
  
- **AccessibleDefaultActionDescription**  
  
- **AccessibleDescription**  
  
- **AccessibleName**  
  
- **AccessibleRole**  
  
## <a name="accessibilityobject-property"></a>AccessibilityObject プロパティ  
 この読み取り専用プロパティには <xref:System.Windows.Forms.AccessibleObject> インスタンスが含まれます。 **AccessibleObject** は、コントロールの説明、画面上の位置、ナビゲーション能力、および値に関する情報を提供する <xref:Accessibility.IAccessible> インターフェイスを実装します。 デザイナーは、コントロールがフォームに追加されたときにこの値を設定します。  
  
## <a name="accessibledefaultactiondescription-property"></a>AccessibleDefaultActionDescription プロパティ  
 この文字列は、コントロールの操作について説明します。 [プロパティ] ウィンドウには表示されず、コードでのみ設定できます。 次の例では、このプロパティをボタン コントロールに設定します。  
  
```vb  
Button1.AccessibleDefaultActionDescription = _  
   "Closes the application."  
```

```csharp  
Button1.AccessibleDefaultActionDescription =
   "Closes the application.";  
```

```cpp  
button1->AccessibleDefaultActionDescription =  
   "Closes the application.";  
```  
  
## <a name="accessibledescription-property"></a>AccessibleDescription プロパティ  
 この文字列はコントロールについて説明します。 これは、[プロパティ] ウィンドウで、または次のようにコードで設定できます。  
  
```vb  
Button1.AccessibleDescription = "A button with text 'Exit'."  
```

```csharp  
Button1.AccessibleDescription = "A button with text 'Exit'";  
```

```cpp  
button1->AccessibleDescription = "A button with text 'Exit'";  
```  
  
## <a name="accessiblename-property"></a>AccessibleName プロパティ  
 これは、ユーザー補助機能に報告されたコントロールの名前です。 これは、[プロパティ] ウィンドウで、または次のようにコードで設定できます。  
  
```vb  
Button1.AccessibleName = "Order"  
```

```csharp  
Button1.AccessibleName = "Order";  
```

```cpp  
button1->AccessibleName = "Order";  
```  
  
## <a name="accessiblerole-property"></a>AccessibleRole プロパティ  
 このプロパティには <xref:System.Windows.Forms.AccessibleRole> 列挙型が含まれており、コントロールのユーザー インターフェイスの役割について説明します。 新しいコントロールは値が `Default` に設定されています。 つまり、 **ボタン** コントロールは既定値では **ボタン**として機能します。 コントロールに別の役割がある場合、このプロパティをリセットできます。 たとえば、 **PictureBox** コントロールを **Chart**として使用する場合、 **PictureBox**ではなく **Chart**としてユーザー補助機能が役割を報告するようにできます。 また、開発したカスタム コントロールにこのプロパティを指定することもできます。 このプロパティは、[プロパティ] ウィンドウで、または次のようにコードで設定できます。  
  
```vb
PictureBox1.AccessibleRole = AccessibleRole.Chart  
```

```csharp  
PictureBox1.AccessibleRole = AccessibleRole.Chart;  
```

```cpp  
pictureBox1->AccessibleRole = AccessibleRole::Chart;  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.AccessibleObject>
- <xref:System.Windows.Forms.Control.AccessibilityObject%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.AccessibleDefaultActionDescription%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.AccessibleDescription%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.AccessibleName%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.AccessibleRole%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.AccessibleRole>
