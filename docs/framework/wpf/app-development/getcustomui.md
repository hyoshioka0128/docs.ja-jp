---
title: GetCustomUI
ms.date: 03/30/2017
helpviewer_keywords:
- custom error messages [WPF]
ms.assetid: e55180fc-35bb-4f80-a136-772b5eb3e4e5
ms.openlocfilehash: e9ef32912c2afb3c99e46e1e14bb3daa5a2e99af
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005710"
---
# <a name="getcustomui"></a>GetCustomUI
実装されている場合、ホストから進行状況とエラーのカスタム メッセージを取得するために、PresentationHost.exe によって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCustomUI( [out] BSTR* pwzProgressAssemblyName, [out] BSTR* pwzProgressClassName, [out] BSTR* pwzErrorAssemblyName, [out] BSTR* pwzErrorClassName );  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzProgressAssemblyName`  
  
 [out] ホストから提供された進行状況ユーザー インターフェイスが格納されているアセンブリへのポインター。  
  
 `pwzProgressClassName`  
  
 [out] ホストから提供された進行状況ユーザー インターフェイスであるクラスの名前。可能であれば、<xref:System.Windows.Controls.Page> を含む XAML ファイルが最上位の要素です。 このクラスは、`pwzProgressAssemblyName` によって指定されているアセンブリに存在します。  
  
 `pwzErrorAssemblyName`  
  
 [out] ホストから提供されたエラー ユーザー インターフェイスが格納されているアセンブリへのポインター。  
  
 `pwzErrorClassName`  
  
 [out] ホストから提供されたエラー ユーザー インターフェイスであるクラスの名前。可能であれば、<xref:System.Windows.Controls.Page> を含む XAML ファイルが最上位の要素です。 このクラスは、`pwzErrorAssemblyName` によって指定されているアセンブリに存在します。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 HRESULT:無視されます。  
  
## <a name="remarks"></a>コメント  
 ホスト アプリケーションには、PresentationHost.exe の既定のユーザー インターフェイスが準拠していない可能性がある特定のテーマが含まれる場合があります。 その場合は、ホスト アプリケーションで [GetCustomUI](getcustomui.md) を実装して、進行状況とエラーのユーザー インターフェイスを PresentationHost.exe に返すことができます。 [GetCustomUI](getcustomui.md) は、既定のユーザーインターフェイスを使用する前に、常にを呼び出します。  
  
 この関数は、PresentationHost の初期化の間に 1 回呼び出されます。  
  
## <a name="see-also"></a>関連項目

- [IWpfHostSupport](iwpfhostsupport.md)
