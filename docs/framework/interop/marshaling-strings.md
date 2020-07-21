---
title: 文字列のマーシャリング
description: 文字列をマーシャリングする方法を確認します。 文字列をマーシャリングするためのオプション (値渡しまたは参照渡し、結果として、構造体またはクラスで値渡しまたは参照渡し、その他) について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- marshaling, samples
- platform invoke, marshaling data
- data marshaling, strings
- data marshaling, samples
- data marshaling, platform invoke
- marshaling. strings
- marshaling, platform invoke
- sample applications [.NET Framework], marshaling strings
ms.assetid: e21b078b-70fb-4905-be26-c097ab2433ff
ms.openlocfilehash: 0be5a5817bd92c5be6b701200a74650ef9de1955
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621484"
---
# <a name="marshaling-strings"></a>文字列のマーシャリング
プラットフォーム呼び出しは、文字列のパラメーターをコピーし、必要な場合は、.NET Framework 形式 (Unicode) からアンマネージ形式 (ANSI) に変換します。 マネージド文字列は変更できないため、プラットフォーム呼び出しでは、関数から戻るときに、アンマネージド メモリからマネージド メモリに文字列がコピーされて戻されることはありません。  
  
 次の表では、文字列のマーシャリング オプションの一覧、それぞれの使用方法の説明、対応する .NET Framework サンプルへのリンクを示します。  
  
|String|説明|サンプル|  
|------------|-----------------|------------|  
|値渡し。|In パラメーターとして文字列を渡します。|[MsgBox](msgbox-sample.md)|  
|結果として。|アンマネージ コードから文字列を返します。|[文字列](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e765dyyy(v=vs.100))|  
|参照渡し。|<xref:System.Text.StringBuilder> を使って In/Out パラメーターとして文字列を渡します。|[バッファー](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/x3txb6xc(v=vs.100))|  
|構造体で値渡し。|In パラメーターである構造体で文字列を渡します。|[構造体](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/eadtsekz(v=vs.100))|  
|構造体で参照渡し **(char\*)** 。|In/Out パラメーターである構造体で文字列を渡します。 アンマネージ関数は文字バッファーへのポインターを必要とし、バッファー サイズは構造体のメンバーです。|[文字列](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e765dyyy(v=vs.100))|  
|構造体で参照渡し **(char[])** 。|In/Out パラメーターである構造体で文字列を渡します。 アンマネージ関数は、埋め込み文字バッファーを必要とします。|[OSInfo](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/795sy883(v=vs.100))|  
|クラスで値渡し **(char\*)** 。|クラスで文字列を渡します (クラスは In/Out パラメーターです)。 アンマネージ関数は、文字バッファーへのポインターを必要とします。|[OpenFileDlg](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w5tyztk9(v=vs.100))|  
|クラスで値渡し **(char[])** 。|クラスで文字列を渡します (クラスは In/Out パラメーターです)。 アンマネージ関数は、埋め込み文字バッファーを必要とします。|[OSInfo](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/795sy883(v=vs.100))|  
|文字列の配列として値渡し。|値によって渡される文字列の配列を作成します。|[配列](marshaling-different-types-of-arrays.md)|  
|文字列を含む構造体の配列として値渡し。|文字列を含む構造体の配列を作成し、配列を値で渡します。|[配列](marshaling-different-types-of-arrays.md)|  
  
## <a name="see-also"></a>関連項目

- [文字列に対する既定のマーシャリング](default-marshaling-for-strings.md)
- [プラットフォーム呼び出しによるデータのマーシャリング](marshaling-data-with-platform-invoke.md)
- [クラス、構造体、および共用体のマーシャリング](marshaling-classes-structures-and-unions.md)
- [さまざまな型の配列のマーシャリング](marshaling-different-types-of-arrays.md)
- [各種のマーシャリングのサンプル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ss9sb93t(v=vs.100))
