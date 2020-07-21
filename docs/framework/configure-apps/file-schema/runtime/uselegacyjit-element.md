---
title: <useLegacyJit> 要素
ms.date: 04/26/2017
ms.assetid: c2cf97f0-9262-4f1f-a754-5568b51110ad
ms.openlocfilehash: a126b8c0050a8d1fd96a3d090f9b018a9faa07a7
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73968852"
---
# <a name="uselegacyjit-element"></a>\<useLegacyJit> 要素

共通言語ランタイムが Just-In-Time コンパイルの従来の 64 ビット JIT コンパイラを使用するかどうかを決定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<useLegacyJit>**  
  
## <a name="syntax"></a>構文  
  
```xml
<useLegacyJit enabled=0|1 />
```

要素名 `useLegacyJit` は大文字と小文字が区別されます。
  
## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
| 属性 | 説明                                                                                   |  
| --------- | --------------------------------------------------------------------------------------------- |  
| `enabled` | 必須の属性です。<br><br>ランタイムがレガシ64ビット JIT コンパイラを使用するかどうかを指定します。 |  
  
### <a name="enabled-attribute"></a>enabled 属性  
  
| 値 | 説明                                                                                                         |  
| ----- | ------------------------------------------------------------------------------------------------------------------- |  
| 0     | 共通言語ランタイムは、.NET Framework 4.6 以降のバージョンに含まれる新しい64ビット JIT コンパイラを使用します。 |  
| 1     | 共通言語ランタイムは、古い64ビット JIT コンパイラを使用します。                                                     |  
  
### <a name="child-elements"></a>子要素

なし
  
### <a name="parent-elements"></a>親要素  
  
| 要素         | Description                                                                                                       |  
| --------------- | ----------------------------------------------------------------------------------------------------------------- |  
| `configuration` | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |  
| `runtime`       | ランタイム初期化オプションに関する情報を含んでいます。                                                        |  
  
## <a name="remarks"></a>解説  

.NET Framework 4.6 以降、共通言語ランタイムは、Just-in-time (JIT) コンパイルに新しい64ビットコンパイラを既定で使用します。 場合によっては、以前のバージョンの64ビット JIT コンパイラによって JIT コンパイルされたアプリケーションコードとの動作が異なる場合があります。 `enabled`要素の属性をに設定 `<useLegacyJit>` する `1` と、新しい64ビット jit コンパイラを無効にし、代わりに従来の64ビット jit コンパイラを使用してアプリをコンパイルできます。  
  
> [!NOTE]
> 要素は、 `<useLegacyJit>` 64 ビットの JIT コンパイルのみに影響します。 32ビットの JIT コンパイラでのコンパイルは影響を受けません。  
  
構成ファイルの設定を使用する代わりに、次の2つの方法で従来の64ビット JIT コンパイラを有効にすることができます。  
  
- 環境変数の設定

  `COMPLUS_useLegacyJit`環境変数を、 `0` (新しい64ビット jit コンパイラを使用) または `1` (古い64ビット jit コンパイラを使用) のいずれかに設定します。
  
  ```env  
  COMPLUS_useLegacyJit=0|1  
  ```  
  
  環境変数には*グローバルスコープ*があります。これは、コンピューター上で実行されるすべてのアプリケーションに影響を与えることを意味します。 設定されている場合は、アプリケーション構成ファイルの設定によって上書きできます。 環境変数の名前では大文字と小文字は区別されません。
  
- レジストリキーの追加

  `REG_DWORD` `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` レジストリ内のまたはキーのいずれかに値を追加することで、レガシ64ビット JIT コンパイラを有効にすることができ `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` ます。 値にはという名前が付けられ `useLegacyJit` ます。 値が0の場合は、新しいコンパイラが使用されます。 値が1の場合、レガシ64ビット JIT コンパイラが有効になります。 レジストリ値の名前では大文字と小文字は区別されません。
  
  キーに値を追加すると `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework` 、コンピューター上で実行されているすべてのアプリに影響します。 キーに値を追加すると、 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework` 現在のユーザーが実行しているすべてのアプリに影響します。 コンピューターに複数のユーザーアカウントが構成されている場合、その値が他のユーザーのレジストリキーにも追加されない限り、現在のユーザーが実行しているアプリのみが影響を受けます。 `<useLegacyJit>`構成ファイルに要素を追加すると、レジストリ設定が存在する場合はその設定が上書きされます。  
  
## <a name="example"></a>例  

次の構成ファイルは、新しい64ビット JIT コンパイラでのコンパイルを無効にし、代わりに従来の64ビット JIT コンパイラを使用します。  
  
```xml  
<?xml version ="1.0"?>  
<configuration>  
  <runtime>  
    <useLegacyJit enabled="1" />  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [\<runtime>Element](runtime-element.md)
- [\<configuration>Element](../configuration-element.md)
- [軽減策: 新しい 64 ビット JIT コンパイラ](../../../migration-guide/mitigation-new-64-bit-jit-compiler.md)
