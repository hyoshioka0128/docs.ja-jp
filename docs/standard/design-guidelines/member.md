---
title: メンバーのデザインのガイドライン
description: .NET のメンバーデザインガイドラインについて説明します。 メンバーには、メソッド、プロパティ、イベント、コンストラクター、およびフィールドが含まれます。
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], about member design guidelines
- members [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], members
- member design guidelines [.NET Framework]
ms.assetid: 0ce93180-1d7b-4f8c-9306-f828b2d66b8f
ms.openlocfilehash: a1f0c1d74e8bffa7cfef975c7dafb9fd01479470
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594492"
---
# <a name="member-design-guidelines"></a>メンバーのデザインのガイドライン
メソッド、プロパティ、イベント、コンストラクター、およびフィールドは、総称してメンバーと呼ばれます。 フレームワークのエンドユーザーに公開されるフレームワークの機能は、最終的にメンバーになります。  
  
 メンバーは、仮想または非仮想、具象または抽象、静的、またはインスタンスにすることができ、アクセシビリティの複数の異なるスコープを持つことができます。 これらはすべて、非常に優れた表現力を提供しますが、同時にフレームワークデザイナーの一部に注意する必要があります。  
  
 この章では、任意の型のメンバーを設計する際に従う必要がある基本的なガイドラインについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [メンバーのオーバーロード](member-overloading.md)  
 [プロパティのデザイン](property.md)  
 [コンストラクターのデザイン](constructor.md)  
 [イベントのデザイン](event.md)  
 [フィールドのデザイン](field.md)  
 [拡張メソッド](extension-methods.md)  
 [演算子のオーバーロード](operator-overloads.md)  
 [パラメーターのデザイン](parameter-design.md)  
 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*  
  
 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*  
  
## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
