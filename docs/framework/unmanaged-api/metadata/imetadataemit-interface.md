---
title: IMetaDataEmit インターフェイス
ms.date: 03/30/2017
api_name:
- IMetaDataEmit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit
helpviewer_keywords:
- IMetaDataEmit interface [.NET Framework metadata]
ms.assetid: 3b48fd47-7397-4e2c-8bec-8157aa08978c
topic_type:
- apiref
ms.openlocfilehash: a2c2512abc28f0140fc261c5136c7e1255db96de
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009214"
---
# <a name="imetadataemit-interface"></a>IMetaDataEmit インターフェイス
現在定義されているスコープ内のアセンブリに関するメタデータを作成、変更、および保存するためのメソッドを提供します。 メタデータは、メモリに格納することも、ディスクに保存することもできます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ApplyEditAndContinue メソッド](imetadataemit-applyeditandcontinue-method.md)|指定したに加えられた変更を使用して、現在のアセンブリスコープを更新し `pImport` ます。|  
|[DefineCustomAttribute メソッド](imetadataemit-definecustomattribute-method.md)|指定したメタデータシグネチャを使用して、指定したオブジェクトにアタッチするカスタム属性の定義を作成し、そのカスタム属性定義へのトークンを取得します。|  
|[DefineEvent メソッド](imetadataemit-defineevent-method.md)|指定したメタデータシグネチャを持つイベントの定義を作成し、そのイベント定義へのトークンを取得します。|  
|[DefineField メソッド](imetadataemit-definefield-method.md)|指定したメタデータシグネチャを持つフィールドの定義を作成し、そのフィールド定義へのトークンを取得します。|  
|[DefineImportMember メソッド](imetadataemit-defineimportmember-method.md)|現在のスコープ外のモジュールで定義されている型のメンバーの定義を作成し、その参照定義のトークンを取得します。|  
|[DefineImportType メソッド](imetadataemit-defineimporttype-method.md)|現在のスコープ外のモジュールで定義されている型への参照の定義を作成し、その参照定義へのトークンを取得します。|  
|[DefineMemberRef メソッド](imetadataemit-definememberref-method.md)|現在のスコープ外のモジュールのメンバーへの参照の定義を作成し、その参照定義へのトークンを取得します。|  
|[DefineMethod メソッド](imetadataemit-definemethod-method.md)|指定したシグネチャを使用してメソッドの定義を作成し、そのメソッド定義に対するトークンを返します。|  
|[DefineMethodImpl メソッド](imetadataemit-definemethodimpl-method.md)|インターフェイスから継承されたメソッドの実装の定義を作成し、そのメソッド実装定義にトークンを返します。|  
|[DefineModuleRef メソッド](imetadataemit-definemoduleref-method.md)|指定された名前を持つモジュールのメタデータシグネチャを作成します。|  
|[DefineNestedType メソッド](imetadataemit-definenestedtype-method.md)|型定義のメタデータシグネチャを作成し、 `mdTypeDef` その型のトークンを返します。さらに、定義された型がによって参照される型のメンバーであることを指定し `tdEncloser` ます。|  
|[DefineParam メソッド](imetadataemit-defineparam-method.md)|指定したトークンによって参照されるメソッドに対して、指定したシグネチャを持つパラメーター定義を作成し、そのパラメーター定義のトークンを取得します。|  
|[DefinePermissionSet メソッド](imetadataemit-definepermissionset-method.md)|指定したメタデータシグネチャを持つアクセス許可セットの定義を作成し、そのアクセス許可セットの定義に対するトークンを取得します。|  
|[DefinePinvokeMap メソッド](imetadataemit-definepinvokemap-method.md)|指定したトークンによって参照されるメソッドの PInvoke 署名の特徴を設定します。|  
|[DefineProperty メソッド](imetadataemit-defineproperty-method.md)|指定したアクセサーとメソッドアクセサーを使用して、指定した型のプロパティ定義を作成 `get` `set` し、そのプロパティ定義へのトークンを取得します。|  
|[DefineSecurityAttributeSet メソッド](imetadataemit-definesecurityattributeset-method.md)|指定したトークンによって参照されるオブジェクトにアタッチするセキュリティアクセス許可のセットを作成します。|  
|[DefineTypeDef メソッド](imetadataemit-definetypedef-method.md)|共通言語ランタイム型の型定義を作成し、その型定義へのメタデータトークンを取得します。|  
|[DefineTypeRefByName メソッド](imetadataemit-definetyperefbyname-method.md)|現在のスコープ外の別のモジュールで定義されている型のメタデータトークンを取得します。|  
|[DefineUserString メソッド](imetadataemit-defineuserstring-method.md)|指定されたリテラル文字列のメタデータトークンを取得します。|  
|[DeleteClassLayout メソッド](imetadataemit-deleteclasslayout-method.md)|指定したトークンによって参照される型のクラスレイアウトメタデータシグネチャを破棄します。|  
|[DeleteFieldMarshal メソッド](imetadataemit-deletefieldmarshal-method.md)|指定したトークンによって参照されるオブジェクトの PInvoke マーシャリングメタデータ署名を破棄します。|  
|[DeletePinvokeMap メソッド](imetadataemit-deletepinvokemap-method.md)|指定したトークンによって参照されるオブジェクトの PInvoke マッピングメタデータを破棄します。|  
|[DeleteToken メソッド](imetadataemit-deletetoken-method.md)|現在のメタデータスコープから指定されたトークンを削除します。|  
|[GetSaveSize メソッド](imetadataemit-getsavesize-method.md)|現在のスコープ内のアセンブリの推定バイナリサイズを取得します。|  
|[GetTokenFromSig メソッド](imetadataemit-gettokenfromsig-method.md)|指定したメタデータシグネチャのトークンを取得します。|  
|[GetTokenFromTypeSpec メソッド](imetadataemit-gettokenfromtypespec-method.md)|指定したメタデータシグネチャを持つ型のメタデータトークンを取得します。|  
|[Merge メソッド](imetadataemit-merge-method.md)|マージするスコープの一覧に、指定したインポートされたスコープを追加します。|  
|[MergeEnd メソッド](imetadataemit-mergeend-method.md)|の1つ以上の前の呼び出しで指定されたすべてのメタデータスコープを現在のスコープにマージ `IMetaDataEmit::Merge` します。|  
|[Save メソッド](imetadataemit-save-method.md)|現在のスコープ内のすべてのメタデータを、指定したアドレスにあるファイルに保存します。|  
|[SaveToMemory メソッド](imetadataemit-savetomemory-method.md)|現在のスコープ内のすべてのメタデータを、指定したメモリ領域に保存します。|  
|[SaveToStream メソッド](imetadataemit-savetostream-method.md)|現在のスコープ内のすべてのメタデータを、指定したに保存し `IStream` ます。|  
|[SetClassLayout メソッド](imetadataemit-setclasslayout-method.md)|の前の呼び出しで定義された型のクラスレイアウト署名を設定または更新し `IMetaDataEmit::DefineTypeDef` ます。|  
|[SetCustomAttributeValue メソッド](imetadataemit-setcustomattributevalue-method.md)|の前の呼び出しで定義されたカスタム属性の値を設定または更新し `IMetaDataEmit::DefineCustomAttribute` ます。|  
|[SetEventProps メソッド](imetadataemit-seteventprops-method.md)|の前の呼び出しで定義されたイベントの指定された機能を設定または更新し `IMetaDataEmit::DefineEvent` ます。|  
|[SetFieldMarshal メソッド](imetadataemit-setfieldmarshal-method.md)|指定したトークンによって参照されるフィールド、メソッドの戻り値、またはメソッドパラメーターの PInvoke マーシャリング情報を設定します。|  
|[SetFieldProps メソッド](imetadataemit-setfieldprops-method.md)|指定したフィールドトークンによって参照されるフィールドの既定値を設定または更新します。|  
|[SetFieldRVA メソッド](imetadataemit-setfieldrva-method.md)|指定したトークンによって参照されるフィールドの相対仮想アドレスのグローバル変数値を設定します。|  
|[SetHandler メソッド](imetadataemit-sethandler-method.md)|指定したポインターによって参照されるメソッドを、 `IUnknown` トークンリマップの通知コールバックとして設定します。|  
|[SetMethodImplFlags メソッド](imetadataemit-setmethodimplflags-method.md)|指定したトークンによって参照される、継承されたメソッドの実装のメタデータシグネチャを設定または更新します。|  
|[SetMethodProps メソッド](imetadataemit-setmethodprops-method.md)|の前の呼び出しで定義されたメソッドの、指定した相対仮想アドレスに格納されている機能を設定または更新し `IMetaDataEmit::DefineMethod` ます。|  
|[SetModuleProps メソッド](imetadataemit-setmoduleprops-method.md)|の前の呼び出しで定義されているモジュールへの参照を更新 `IMetaDataEmit::DefineModuleRef` します。|  
|[SetParamProps メソッド](imetadataemit-setparamprops-method.md)|の前の呼び出しで定義されたメソッドパラメーターの機能を設定または変更 `IMetaDataEmit::DefineParam` します。|  
|[SetParent メソッド](imetadataemit-setparent-method.md)|の前の呼び出しで定義されているように、指定したメンバーが、の前の呼び出しで定義されている、指定した型のメンバーであることを確立し `IMetaDataEmit::DefineMemberRef` `IMetaDataEmit::DefineTypeDef` ます。|  
|[SetPermissionSetProps メソッド](imetadataemit-setpermissionsetprops-method.md)|の前の呼び出しで定義されたアクセス許可セットのメタデータ署名の機能を設定または更新 `IMetaDataEmit::DefinePermissionSet` します。|  
|[SetPinvokeMap メソッド](imetadataemit-setpinvokemap-method.md)|の前の呼び出しで定義されているように、メソッドの PInvoke 署名の機能を設定または変更し `IMetaDataEmit::DefinePinvokeMap` ます。|  
|[SetPropertyProps メソッド](imetadataemit-setpropertyprops-method.md)|の前の呼び出しで定義されたプロパティのメタデータに格納されている機能を設定し `IMetaDataEmit::DefineProperty` ます。|  
|[SetRVA メソッド](imetadataemit-setrva-method.md)|指定したメソッドの相対仮想アドレスを設定します。|  
|[SetTypeDefProps メソッド](imetadataemit-settypedefprops-method.md)|の前の呼び出しで定義された型の機能を設定 `IMetaDataEmit::DefineTypeDef` します。|  
|[TranslateSigWithScope メソッド](imetadataemit-translatesigwithscope-method.md)|現在のスコープにアセンブリをインポートし、マージされたスコープの新しいメタデータシグネチャを取得します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ インターフェイス](metadata-interfaces.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
