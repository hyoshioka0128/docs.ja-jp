---
title: スタートアップ設定スキーマ
ms.date: 03/30/2017
helpviewer_keywords:
- startup settings schema
- schema startup settings
- configuration schema [.NET Framework], startup settings
ms.assetid: 03de6972-442a-4648-9f3e-efa654e3b949
ms.openlocfilehash: e5f9c9af64ff38e7c0f1f26ccab039261b052e30
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "61701516"
---
# <a name="startup-settings-schema"></a>スタートアップ設定スキーマ

スタートアップ設定は、アプリケーションを実行する必要のある共通言語ランタイムのバージョンを指定します。  
  
|要素|説明|  
|-------------|-----------------|  
|[\<requiredRuntime>](requiredruntime-element.md)|バージョン 1.0 の共通言語ランタイムのみがアプリケーションでサポートされることを指定します。 ランタイムバージョン1.1 でビルドされたアプリケーションでは、要素を使用する必要があり **\<supportedRuntime>** ます。|  
|[\<supportedRuntime>](supportedruntime-element.md)|アプリケーションでサポートされる共通言語ランタイムのバージョンを指定します。|  
|[\<startup>](startup-element.md)|要素と要素が含まれてい **\<requiredRuntime>** **\<supportedRuntime>** ます。|  
  
## <a name="see-also"></a>関連項目

- [構成ファイル スキーマ](../index.md)
- [方法: .NET Framework 4 以降のバージョンをサポートするアプリを構成する](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
