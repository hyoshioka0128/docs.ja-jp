---
title: DataGridView コントロールと DataGrid コントロールの違い
description: Windows フォーム DataGridView と DataGrid コントロールの機能のさまざまな相違点と、アーキテクチャの違いについて説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms
- DataGrid control [Windows Forms], DataGridView control compared
- DataGridView control [Windows Forms], DataGrid control compared
ms.assetid: d412c786-140e-4210-8a56-a68467530a55
ms.openlocfilehash: 1438182d764097ae4f8fd7df046ad72c9213da19
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174589"
---
# <a name="differences-between-the-windows-forms-datagridview-and-datagrid-controls"></a>Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて
コントロールは、 <xref:System.Windows.Forms.DataGridView> コントロールを置き換える新しいコントロールです <xref:System.Windows.Forms.DataGrid> 。 コントロール <xref:System.Windows.Forms.DataGridView> には、コントロールに不足している基本的な機能と高度な機能が多数用意されてい <xref:System.Windows.Forms.DataGrid> ます。 さらに、コントロールのアーキテクチャに <xref:System.Windows.Forms.DataGridView> より、コントロールよりもはるかに簡単に拡張およびカスタマイズ <xref:System.Windows.Forms.DataGrid> できます。  
  
 次の表では、コントロールで使用できない主な機能のいくつかについて説明し <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.DataGrid> ます。  
  
|DataGridView コントロール機能|説明|  
|----------------------------------|-----------------|  
|複数の列の型|コントロールには、 <xref:System.Windows.Forms.DataGridView> コントロールよりも多くの組み込み列型が用意されて <xref:System.Windows.Forms.DataGrid> います。 これらの列の型は、最も一般的なシナリオのニーズを満たしますが、コントロール内の列の型よりも拡張または置換が簡単です <xref:System.Windows.Forms.DataGrid> 。 詳細については、「 [Windows フォーム DataGridView コントロールの列の型](column-types-in-the-windows-forms-datagridview-control.md)」を参照してください。|  
|データを表示する複数の方法|<xref:System.Windows.Forms.DataGrid>コントロールは、外部データソースのデータの表示に限定されます。 ただし、コントロールには、 <xref:System.Windows.Forms.DataGridView> コントロールに格納されているバインドされていないデータ、バインドされたデータソースのデータ、またはバインドされたデータとバインドされていないデータが表示されます。 コントロールに仮想モードを実装して、 <xref:System.Windows.Forms.DataGridView> カスタムデータ管理を提供することもできます。 詳細については、「 [Windows フォーム DataGridView コントロールのデータ表示モード](data-display-modes-in-the-windows-forms-datagridview-control.md)」を参照してください。|  
|データの表示をカスタマイズする複数の方法|コントロールには、 <xref:System.Windows.Forms.DataGridView> データの書式設定方法と表示方法を指定できる多数のプロパティとイベントが用意されています。 たとえば、格納されているデータに応じてセル、行、および列の外観を変更することや、あるデータ型のデータを別の型の同等のデータに置き換えることができます。 詳細については、「 [Windows フォーム DataGridView コントロールでのデータの書式設定](data-formatting-in-the-windows-forms-datagridview-control.md)」を参照してください。|  
|セル、行、列、およびヘッダーの外観と動作を変更するための複数のオプション|コントロールを使用すると、 <xref:System.Windows.Forms.DataGridView> さまざまな方法で個々のグリッドコンポーネントを操作できます。 たとえば、行と列を固定してスクロールできないようにすることができます。行、列、およびヘッダーを非表示にします。行、列、およびヘッダーのサイズを調整する方法を変更します。ユーザーが選択する方法を変更します。とには、個々のセル、行、および列のツールヒントとショートカットメニューが用意されています。|  
  
 コントロールは、 <xref:System.Windows.Forms.DataGrid> 旧バージョンとの互換性を維持し、特別なニーズに対応するために残されています。 ほぼすべての目的で、コントロールを使用する必要があり <xref:System.Windows.Forms.DataGridView> ます。 コントロールで使用できない唯一の機能は、 <xref:System.Windows.Forms.DataGrid> <xref:System.Windows.Forms.DataGridView> 1 つのコントロール内の2つの関連テーブルの情報を階層的に表示することです。 <xref:System.Windows.Forms.DataGridView>マスター/詳細リレーションシップに含まれる2つのテーブルの情報を表示するには、2つのコントロールを使用する必要があります。  
  
## <a name="upgrading-to-the-datagridview-control"></a>DataGridView コントロールへのアップグレード  
 カスタマイズのない単純なデータバインドシナリオでコントロールを使用する既存のアプリケーションがある場合は、単純に <xref:System.Windows.Forms.DataGrid> 古いコントロールを新しいコントロールに置き換えることができます。 どちらのコントロールも標準の Windows フォームデータバインディングアーキテクチャを使用します。そのため、コントロールは、 <xref:System.Windows.Forms.DataGridView> 追加の構成を必要とせずに、バインドされたデータを表示します。 ただし、データバインディングの機能強化を利用する場合は、データをコンポーネントにバインドして、コントロールにバインドできるようにすることをお勧めし <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.DataGridView> ます。 詳細については、「 [BindingSource コンポーネント](bindingsource-component.md)」を参照してください。  
  
 コントロールには <xref:System.Windows.Forms.DataGridView> まったく新しいアーキテクチャがあるため、 <xref:System.Windows.Forms.DataGrid> コントロールでカスタマイズを使用できるようにするための単純な変換パスはありません <xref:System.Windows.Forms.DataGridView> 。 ただし、コントロールには多く <xref:System.Windows.Forms.DataGrid> のカスタマイズが不要です <xref:System.Windows.Forms.DataGridView> 。これは、新しいコントロールで使用できる組み込みの機能があるためです。 コントロールで使用するコントロールに対してカスタムの列の型を作成した場合 <xref:System.Windows.Forms.DataGrid> <xref:System.Windows.Forms.DataGridView> は、新しいアーキテクチャを使用してもう一度実装する必要があります。 詳細については、「 [Windows フォーム DataGridView コントロールのカスタマイズ](customizing-the-windows-forms-datagridview-control.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGrid>
- <xref:System.Windows.Forms.BindingSource>
- [DataGridView コントロール](datagridview-control-windows-forms.md)
- [DataGrid コントロール](datagrid-control-windows-forms.md)
- [BindingSource コンポーネント](bindingsource-component.md)
- [Windows フォーム DataGridView コントロールの列型](column-types-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールでのセルのスタイル](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールでのデータ表示モード](data-display-modes-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールでのデータの書式設定](data-formatting-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールのサイズ変更オプション](sizing-options-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロール内の列の並べ替えモード](column-sort-modes-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールの選択モード](selection-modes-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールのカスタマイズ](customizing-the-windows-forms-datagridview-control.md)
