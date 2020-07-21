---
title: 破壊的変更 - .NET Framework から .NET Core
titleSuffix: ''
description: .NET Framework から .NET Core への破壊的変更を一覧表示します。
ms.date: 05/05/2020
ms.openlocfilehash: f830d4571f21752900b35a7462bf0881673d6d2e
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420449"
---
# <a name="breaking-changes-for-migration-from-net-framework-to-net-core"></a>.NET Framework から .NET Core への移行の破壊的変更

.NET Framework から .NET Core にアプリを移行する場合、この記事の一覧にある破壊的変更による影響を受ける可能性があります。 破壊的変更はカテゴリ別に分類され、そのカテゴリ内では、導入された .NET Core のバージョンによってグループ化されます。

> [!NOTE]
> この記事は、.NET Framework と .NET Core の間の破壊的変更の完全な一覧ではありません。 最も重要な破壊的変更が認識されると、こちらに追加されます。

## <a name="core-net-libraries"></a>Core .NET ライブラリ

- [UseShellExecute の既定値の変更](#change-in-default-value-of-useshellexecute)
- [FileSystemInfo.Attributes によってスローされる UnauthorizedAccessException](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes)
- [プロセス破損状態例外の処理がサポートされない](#handling-corrupted-state-exceptions-is-not-supported)
- [UriBuilder のプロパティでは今後、先頭に文字が付加されない](#uribuilder-properties-no-longer-prepend-leading-characters)
- [開始されなかったプロセスについて Process.StartInfo が InvalidOperationException をスローする](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start)

### <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Process.Start changes](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

### <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

***

## <a name="cryptography"></a>暗号

- [SignedCms.ComputeSignature のブール型パラメーターの尊重](#boolean-parameter-of-signedcmscomputesignature-is-respected)

### <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE [Boolean parameter of SignedCms.ComputeSignature is respected](~/includes/core-changes/cryptography/2.1/compute-signature-silent-parameter.md)]

***

## <a name="msbuild"></a>MSBuild

- [リソース マニフェストのファイル名の変更](#resource-manifest-file-name-change)

### <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***

## <a name="networking"></a>ネットワーキング

- [WebClient.CancelAsync がすぐにキャンセルされない場合がある](#webclientcancelasync-doesnt-always-cancel-immediately)

### <a name="net-core-20"></a>.NET Core 2.0

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***

## <a name="windows-forms"></a>Windows フォーム

Windows フォームのサポートは、.NET Core にバージョン 3.0 で追加されました。 .NET Framework から .NET Core に Windows フォーム アプリを移行する場合、アプリがこの記事の一覧にある破壊的変更による影響を受ける可能性があります。

- [削除されたコントロール](#removed-controls)
- [ヒントが表示されていると CellFormatting が発生しない](#cellformatting-event-not-raised-if-tooltip-is-shown)
- [Control.DefaultFont を Segoe UI 9 pt に変更](#default-control-font-changed-to-segoe-ui-9-pt)
- [FolderBrowserDialog の最新化](#modernization-of-the-folderbrowserdialog)
- [一部の Windows フォーム型から SerializableAttribute を削除](#serializableattribute-removed-from-some-windows-forms-types)
- [AllowUpdateChildControlIndexForTabControls 互換性スイッチがサポートされない](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported)
- [DomainUpDown.UseLegacyScrolling 互換性スイッチがサポートされない](#domainupdownuselegacyscrolling-compatibility-switch-not-supported)
- [DoNotLoadLatestRichEditControl 互換性スイッチがサポートされない](#donotloadlatestricheditcontrol-compatibility-switch-not-supported)
- [DoNotSupportSelectAllShortcutInMultilineTextBox 互換性スイッチがサポートされない](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported)
- [DontSupportReentrantFilterMessage 互換性スイッチがサポートされない](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported)
- [EnableVisualStyleValidation 互換性スイッチがサポートされない](#enablevisualstylevalidation-compatibility-switch-not-supported)
- [UseLegacyContextMenuStripSourceControlValue 互換性スイッチがサポートされない](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported)
- [UseLegacyImages 互換性スイッチがサポートされない](#uselegacyimages-compatibility-switch-not-supported)
- [AccessibleObject.RuntimeIDFirstItem のアクセスに対する変更](#change-of-access-for-accessibleobjectruntimeidfirstitem)
- [Windows フォームからの重複する API の削除](#duplicated-apis-removed-from-windows-forms)

### <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

### <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9 pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

[!INCLUDE[Change of access for AccessibleObject.RuntimeIDFirstItem](~/includes/core-changes/windowsforms/3.0/changed-access-for-runtimeidfirstitem.md)]

***

[!INCLUDE[Duplicated APIs removed from Windows Forms](~/includes/core-changes/windowsforms/3.0/remove-duplicated-apis.md)]

***

## <a name="see-also"></a>関連項目

- [.NET Core で常に例外をスローする API](unsupported-apis.md)
- [.NET Core で使用できない .NET Framework テクノロジ](../porting/net-framework-tech-unavailable.md)
