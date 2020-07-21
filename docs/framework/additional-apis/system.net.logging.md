---
title: Logging クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Logging
- System.Net.Logging.Associate
- System.Net.Logging.Enter
- System.Net.Logging.Exception
- System.Net.Logging.Exit
- System.Net.Logging.get_Http
- System.Net.Logging.get_On
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: ad85fdd41252ed147eb5fe1a9db029db046d720c
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990542"
---
# <a name="logging-class"></a>ログクラス

トレースログ機能を提供します。

```csharp
internal class Logging
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="associate-method"></a>関連付け方法

2つのオブジェクトが互いに関連付けられていることをログに記録します。

```csharp
internal static void Associate(TraceSource traceSource, object objA, object objB)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `objA` <xref:System.Object>

  関連付けるオブジェクト `objB` 。

- `objB` <xref:System.Object>

  関連付けるオブジェクト `objA` 。

## <a name="entertracesource-object-string-string-method"></a>Enter (TraceSource、object、string、string) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, object obj, string method, string param)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.Object>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  入力されているメソッド。

- `param` <xref:System.String>

  メソッドに渡されたパラメーター。

## <a name="entertracesource-object-string-object-method"></a>Enter (TraceSource、object、string、object) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, object obj, string method, object paramObject)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.Object>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  入力されているメソッド。

- `paramObject` <xref:System.Object>

  メソッドに渡されたパラメーター。

## <a name="entertracesource-string-string-string-method"></a>Enter (TraceSource、string、string、string) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, string obj, string method, string param)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.String>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  入力されているメソッド。

- `param` <xref:System.String>

  メソッドに渡されたパラメーター。

## <a name="entertracesource-string-string-object-method"></a>Enter (TraceSource、string、string、object) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, string obj, string method, object paramObject)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.String>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  入力されているメソッド。

- `paramObject` <xref:System.Object>

  メソッドに渡されたパラメーター。

## <a name="entertracesource-string-string-method"></a>Enter (TraceSource, string, string) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, string method, string parameters)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `method` <xref:System.String>

  入力されているメソッド。

- `parameters` <xref:System.String>

  メソッドに渡されたパラメーター。

## <a name="entertracesource-string-method"></a>Enter (TraceSource, string) メソッド

メソッドへの入り口をログに記録します。

```csharp
internal static void Enter(TraceSource traceSource, string msg)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `msg` <xref:System.String>

  トレースソースにログを記録するための開始メッセージ。

## <a name="exception-method"></a>Exception メソッド

例外をログに記録し、インデントを復元します。

```csharp
internal static void Exception(TraceSource traceSource, object obj, string method, Exception e)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.Object>

  例外をスローしたメソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  例外をスローしたメソッド。

- `e` <xref:System.Exception>

  スローされた例外。

## <a name="exittracesource-object-string-object-method"></a>Exit (TraceSource、object、string、object) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, object obj, string method, object retObject)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.Object>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  終了されているメソッド。

- `retObject` <xref:System.Object>

  メソッドによって返される値。

## <a name="exittracesource-string-string-object-method"></a>Exit (TraceSource、string、string、object) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, string obj, string method, object retObject)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.String>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  終了されているメソッド。

- `retObject` <xref:System.Object>

  メソッドによって返される値。

## <a name="exittracesource-object-string-string-method"></a>Exit (TraceSource、object、string、string) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, object obj, string method, string retValue)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.Object>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  終了されているメソッド。

- `retValue` <xref:System.String>

  メソッドによって返される値。

## <a name="exittracesource-string-string-string-method"></a>Exit (TraceSource、string、string、string) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, string obj, string method, string retValue)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `obj` <xref:System.String>

  メソッドが呼び出されたオブジェクト。

- `method` <xref:System.String>

  終了されているメソッド。

- `retValue` <xref:System.String>

  メソッドによって返される値。

## <a name="exittracesource-string-string-method"></a>Exit (TraceSource, string, string) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, string method, string parameters)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `method` <xref:System.String>

  終了されているメソッド。

- `parameters` <xref:System.String>

  終了されるメソッドに渡されたパラメーター。

## <a name="exittracesource-string-method"></a>Exit (TraceSource, string) メソッド

ログは関数から終了します。

```csharp
internal static void Exit(TraceSource traceSource, string msg)
```

### <a name="parameters"></a>パラメーター

- `traceSource` <xref:System.Diagnostics.TraceSource>

  イベントのログを記録するトレースソース。

- `msg` <xref:System.String>

  トレースソースに記録する終了メッセージ。

## <a name="http-property"></a>Http プロパティ

"System .Net. Http" のトレースソースを取得します。

```csharp
internal static TraceSource Http { get; }
```

### <a name="property-value"></a>プロパティ値

<xref:System.Diagnostics.TraceSource>\
"System .Net. Http" のトレースソース `null` 。ログ記録が有効になっていない場合は。

## <a name="on-property"></a>On プロパティ

ログが有効になっているかどうかを示す値を取得します。

```csharp
internal static bool On { get; }
```

### <a name="property-value"></a>プロパティ値

<xref:System.Boolean>\
ログが可能な場合は `true`、それ以外の場合は `false` です。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
