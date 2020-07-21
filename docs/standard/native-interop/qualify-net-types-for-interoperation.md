---
title: COM 相互運用のための .NET 型の要件
description: この記事では、COM 相互運用のために .NET アセンブリの型を COM アプリケーションに公開する際に役立つガイドラインを示します。
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- COM interop, qualifying .NET types
- qualifying .NET types for interoperation
- interoperation with unmanaged code, qualifying .NET types
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
ms.assetid: 4b8afb52-fb8d-4e65-b47c-fd82956a3cdd
ms.openlocfilehash: 5e8d604c8152d37475bf93e3b5687f24cfebfa02
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84285964"
---
# <a name="qualifying-net-types-for-com-interoperation"></a>COM 相互運用のための .NET 型の要件
COM アプリケーションにアセンブリ内の型を公開する場合は、設計時に COM 相互運用の要件を検討する必要があります。 以下のガイドラインに従うと、マネージド型 (クラス、インターフェイス、構造体、列挙型) は COM の型とシームレスに統合します。  
  
- クラスは、インターフェイスを明示的に実装する必要があります。  
  
     COM 相互運用は、クラスのすべてのメンバーとその基底クラスのメンバーを含むインターフェイスを自動的に生成するメカニズムを備えていますが、明示的なインターフェイスを提供する方がはるかによい方法です。 自動的に生成されるインターフェイスは、クラス インターフェイスと呼ばれます。 ガイドラインについては、「[クラス インターフェイスの概要](com-callable-wrapper.md#introducing-the-class-interface)」を参照してください。  
  
     インターフェイス定義言語 (IDL) またはそれと同等のものを使う代わりに、Visual Basic、C#、C++ を使ってコードにインターフェイス定義を組み込むことができます。 構文の詳細については、言語のドキュメントを参照してください。  
  
- マネージド型はパブリックにする必要があります。  
  
     アセンブリ内のパブリック型のみが登録されて、タイプ ライブラリにエクスポートされます。 その結果、パブリック型のみが COM に表示されます。  
  
     マネージド型は、COM に公開されない可能性がある他のマネージド コードに機能を公開します。 たとえば、パラメーター化されたコンストラクター、静的メソッド、および定数フィールドは、COM クライアントに公開されません。 さらに、ランタイムが、ある型に、またはある型からデータをマーシャリングすると、データがコピーまたは変換される可能性があります。  
  
- メソッド、プロパティ、フィールド、イベントは、パブリックである必要があります。  
  
     また、パブリック型のメンバーを COM に表示させる場合は、メンバーもパブリックにする必要があります。 アセンブリ、パブリック型、またはパブリック型のパブリック メンバーの可視性は、<xref:System.Runtime.InteropServices.ComVisibleAttribute> を適用することにより制限できます。 既定では、すべてのパブリック型とメンバーが可視になります。  
  
- 型では、パラメーターなしのパブリック コンストラクターを COM からアクティブ化する必要があります。  
  
     マネージド パブリック型のみが COM に表示されます。 ただし、パラメーターなしのパブリック コンストラクター (引数のないコンストラクター) がないと、COM クライアントでは型を作成できません。 その場合でも、型が他の方法でアクティブ化されると、COM クライアントは型を使うことができます。  
  
- 型を抽象にすることはできません。  
  
     COM クライアントも .NET クライアントも、抽象型は作成できません。  
  
 COM にエクスポートされるとき、マネージド型の継承階層はフラット化されます。 マネージド環境とアンマネージド環境では、バージョン管理も異なります。 COM に公開された型は、他のマネージド型とバージョン管理特性が異なります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.ComVisibleAttribute>
- [COM への .NET Framework コンポーネントの公開](../../framework/interop/exposing-dotnet-components-to-com.md)
- [クラス インターフェイスの概要](com-callable-wrapper.md#introducing-the-class-interface)
- [相互運用固有の属性の適用](apply-interop-attributes.md)
- [COM 用の .NET Framework アセンブリのパッケージ化](../../framework/interop/packaging-an-assembly-for-com.md)
