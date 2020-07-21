---
title: -codepage
ms.date: 03/09/2018
helpviewer_keywords:
- -codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
ms.openlocfilehash: 34dbf36cc79a8c4715cf6a07c57d559e14f40030
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363631"
---
# <a name="-codepage-visual-basic"></a>-codepage (Visual Basic)
コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`id`|必須です。 コンパイラは、`id` で指定されたコード ページを使用して、ソース ファイルのエンコードを解釈します。|  
  
## <a name="remarks"></a>Remarks  
 特定のエンコードを使用して保存されたソース コードをコンパイルするには、`-codepage` を使用して、使用するコード ページを指定します。 `-codepage` オプションは、コンパイル時にすべてのソース コード ファイルに適用されます。 詳細については、[.NET Framework での文字エンコード](../../../standard/base-types/character-encoding.md)に関する記事を参照してください。  
  
 ソース コード ファイルが現在の ANSI コード ページ、Unicode、または UTF-8 を使用して保存されている場合、`-codepage` オプションは必要ありません。 Visual Studio では、ユーザーが **[エンコード]** ダイアログ ボックスで別のエンコードを指定しない限り、既定ですべてのソース コード ファイルが現在の ANSI コード ページで保存されます。 Visual Studio では、 **[エンコード]** ダイアログ ボックスを使用して、別のコード ページで保存されたソースコード ファイルが開かれます。  
  
> [!NOTE]
> `-codepage` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
