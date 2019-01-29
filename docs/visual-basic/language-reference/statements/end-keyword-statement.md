---
title: End<keyword>ステートメント (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.EndDefinition
helpviewer_keywords:
- End keyword [Visual Basic]
ms.assetid: 42d6e088-ab0f-4cda-88e8-fdce3e5fcf4f
ms.openlocfilehash: d65c921a1631cd38c4d0d1ab9b34db3d7e43a97e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54654842"
---
# <a name="end-ltkeywordgt-statement-visual-basic"></a>End<keyword>ステートメント (Visual Basic)

その他のキーワードの後に、そのキーワードによって導入されるステートメント ブロックの定義を終了します。

## <a name="syntax"></a>構文

```vb
End AddHandler
End Class
End Enum
End Event
End Function
End Get
End If
End Interface
End Module
End Namespace
End Operator
End Property
End RaiseEvent  
End RemoveHandler  
End Select
End Set
End Structure
End Sub
End SyncLock
End Try
End While
End With  
```  
  
## <a name="parts"></a>指定項目

|パーツ|説明|
|---|---|
|`End`|必須。 プログラミング要素の定義を終了します。|
|`AddHandler`|終了するために必要な`AddHandler`アクセサーを照合することによって開始された`AddHandler`カスタム ステートメント[Event ステートメント](event-statement.md)します。|
|`Class`|照合することによって開始されたクラス定義を終了するために必要な[Class ステートメント](class-statement.md)します。|
|`Enum`|照合することによって開始された列挙の定義を終了するために必要な[Enum ステートメント](enum-statement.md)します。|
|`Event`|終了するために必要な`Custom`を照合することによって開始されたイベント定義[Event ステートメント](event-statement.md)します。|  
|`Function`|終了するために必要な`Function`プロシージャの定義を照合することによって開始された[Function ステートメント](function-statement.md)します。 実行されると、`End Function`ステートメントでは、呼び出し元のコードに制御が戻ります。|
|`Get`|終了するために必要な`Property`プロシージャの定義を照合することによって開始された[Get ステートメント](get-statement.md)します。 実行されると、`End Get`ステートメントでは、プロパティの値を要求するステートメントに制御が戻ります。|
|`If`|終了するために必要な`If`.`Then`...`Else`ブロックを照合することによって開始された定義`If`ステートメント。 参照してください[If...Then...Else ステートメント](if-then-else-statement.md)です。|
|`Interface`|照合することによって開始されたインターフェイス定義を終了するために必要な[Interface ステートメント](interface-statement.md)します。|
|`Module`|照合することによって開始されたモジュールの定義を終了するために必要な[モジュール ステートメント](module-statement.md)します。|
|`Namespace`|照合することによって開始された名前空間の定義を終了するために必要な[Namespace ステートメント](namespace-statement.md)します。|
|`Operator`|照合することによって開始された演算子の定義を終了するために必要な[Operator Statement](operator-statement.md)します。|
|`Property`|照合することによって開始されたプロパティの定義を終了するために必要な[Property ステートメント](property-statement.md)します。|
|`RaiseEvent`|終了するために必要な`RaiseEvent`アクセサーを照合することによって開始された`RaiseEvent`カスタム ステートメント[Event ステートメント](event-statement.md)します。|
|`RemoveHandler`|終了するために必要な`RemoveHandler`アクセサーを照合することによって開始された`RemoveHandler`カスタム ステートメント[Event ステートメント](event-statement.md)します。|
|`Select`|終了するために必要な`Select`.`Case`ブロックを照合することによって開始された定義`Select`ステートメント。 参照してください[Select...Case ステートメント](select-case-statement.md)します。  
|`Set`|終了するために必要な`Property`プロシージャの定義を照合することによって開始された[Set ステートメント](set-statement.md)します。 実行されると、`End Set`ステートメントでは、プロパティの値を設定するステートメントに制御が戻ります。  
|`Structure`|照合することによって開始された構造体の定義を終了するために必要な[Structure ステートメント](structure-statement.md)します。  
|`Sub`|終了するために必要な`Sub`プロシージャの定義を照合することによって開始された[Sub ステートメント](sub-statement.md)します。 実行されると、`End Sub`ステートメントでは、呼び出し元のコードに制御が戻ります。  
|`SyncLock`|終了するために必要な`SyncLock`ブロックを照合することによって開始された定義`SyncLock`ステートメント。 参照してください[SyncLock ステートメント](synclock-statement.md)します。  
|`Try`|終了するために必要な`Try`.`Catch`...`Finally`ブロックを照合することによって開始された定義`Try`ステートメント。 [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)を参照してください。  
|`While`|終了するために必要な`While`ループの定義を照合することによって開始された`While`ステートメント。 参照してください[While...End While ステートメント](while-end-while-statement.md)を参照してください。  
|`With`| 終了するために必要な`With`ブロックを照合することによって開始された定義`With`ステートメント。 [With...End With ステートメント](with-end-with-statement.md)を参照してください。  
|||
  
## <a name="directives"></a>ディレクティブ

シャープ記号に続く場合 (`#`)、`End`キーワードに対応するディレクティブによって導入されるプリプロセッサ ブロックが終了します。  

```vb
#End ExternalSource
#End If
#End Region
```

|パーツ|説明|
|---|---|
|`#End`|必須。 処理前のブロックの定義を終了します。|
|`ExternalSource`|照合することによって開始された、外部ソース ブロックを終了するために必要な[#ExternalSource ディレクティブ](../directives/externalsource-directive.md)します。|
|`If`|照合することによって開始された条件付きコンパイル ブロックを終了するために必要な`#If`ディレクティブ。 参照してください[#If.Then... #Else ディレクティブ](../directives/if-then-else-directives.md)します。|
|`Region`|照合することによって開始されたソース リージョンのブロックを終了するために必要な[#Region ディレクティブ](../directives/region-directive.md)します。|
|||

## <a name="remarks"></a>Remarks

[End ステートメント](end-statement.md)をその他のキーワードを使用せずにすぐに実行を終了します。

## <a name="smart-device-developer-notes"></a>スマート デバイスの開発者向け注意事項  

`End`その他のキーワードを使用せず、ステートメントはサポートされていません。  
  
## <a name="see-also"></a>関連項目

- [End ステートメント](end-statement.md)
