---
ms.openlocfilehash: fabbc9a51f61a703ce97db50ab251e7a13ffe348
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144483"
---
### <a name="countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists"></a>インスタンスが既に存在する場合、CounterSet.CreateCounterSetInstance は InvalidOperationException をスローするようになった

.NET 5.0 以降では、カウンター セットが既に存在する場合、<xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance(System.String)?displayProperty=nameWithType> は <xref:System.ArgumentException> ではなく <xref:System.InvalidOperationException> をスローします。

#### <a name="change-description"></a>変更の説明

.NET Framework と .NET Core 1.0 から 3.1 では、<xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> を呼び出すことによって、カウンター セットのインスタンスを作成できます。 ただし、カウンター セットが既に存在する場合、このメソッドは <xref:System.ArgumentException> 例外をスローします。

.NET 5.0 以降のバージョンでは、<xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> を呼び出したときにカウンター セットが存在すると、<xref:System.InvalidOperationException> 例外がスローされます。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 5

#### <a name="recommended-action"></a>推奨アクション

<xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A> を呼び出すときにアプリで <xref:System.ArgumentException> 例外をキャッチする場合は、<xref:System.InvalidOperationException> 例外もキャッチすることを検討してください。

> [!NOTE]
> <xref:System.ArgumentException> 例外をキャッチすることは推奨されません。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Diagnostics.PerformanceData.CounterSet.CreateCounterSetInstance(System.String)`

-->
