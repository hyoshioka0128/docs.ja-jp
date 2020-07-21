---
title: パス/ファイル アクセス エラー
ms.date: 07/20/2015
f1_keywords:
- vbrID75
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
ms.openlocfilehash: dfe96cd6eaa673438849fe8f799d46fa2617bfdd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387258"
---
# <a name="pathfile-access-error"></a>パス/ファイル アクセス エラー
ファイル アクセス操作またはディスク アクセス操作中に、オペレーティング システムがパスとファイル名の間の接続を作成できませんでした。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. ファイルの指定が正しく書式設定されていることを確認します。 ファイル名には、完全修飾パス (絶対パスまたは相対パス) を含めることができます。 完全修飾パスは、ドライブ名 (パスが別のドライブにある場合) で始まり、ルートからファイルへの明示的なパスを一覧表示します。 完全修飾されていないパスは、現在のドライブとディレクトリに対する相対パスです。  
  
2. 既存の読み取り専用ファイルを置き換えるファイルを保存しようとしていないことを確認します。 この場合は、ターゲット ファイルの読み取り専用属性を変更するか、別のファイル名でファイルを保存します。  
  
3. シーケンシャル `Output` モードまたは `Append` モードで読み取り専用ファイルを開こうとしていないことを確認します。 この場合は、ファイルを `Input` モードで開くか、ファイルの読み取り専用属性を変更します。  
  
4. データベースまたはドキュメント内の Visual Basic プロジェクトを変更しようとしていないことを確認します。  
  
## <a name="see-also"></a>関連項目

- [エラーの種類](../../programming-guide/language-features/error-types.md)
