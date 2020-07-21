---
title: デバッグのインターフェイス
ms.date: 02/07/2019
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: b6297c26-7624-4431-8af4-14112d07bcd5
ms.openlocfilehash: c4b9cdc2bc90096ab7c3b041bd8aa2742b48c35c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179161"
---
# <a name="debugging-interfaces"></a>デバッグのインターフェイス
ここでは、共通言語ランタイム (CLR: Common Language Runtime) で実行するプログラムのデバッグを処理するアンマネージ インターフェイスについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [インターフェイス](iclrdataenummemoryregions-interface.md)\
 呼び出し元が指定したメモリ範囲を列挙するメソッドを提供します。  
  
 [コールバック インターフェイス](iclrdataenummemoryregionscallback-interface.md)\
 メモリの指定された領域を列挙した結果の `EnumMemoryRegions` をデバッガーにレポートするコールバック メソッドを提供します。  
  
 [インターフェイス](iclrdatatarget-interface.md)\
 対象の CLR プロセスと対話するためのメソッドを提供します。  
  
 [インターフェイス](iclrdatatarget2-interface.md)\
 データ アクセス サービス層で使用して対象プロセスの仮想メモリ領域を操作する、`ICLRDataTarget` のサブクラスです。  
  
 [インターフェイス](iclrdatatarget3-interface.md)\
 例外情報へのアクセスを提供する[ICLRDataTarget2](iclrdatatarget2-interface.md)のサブクラス。  
  
 [インターフェイスのデバッグ](iclrdebugging-interface.md)\
 デバッグ用にモジュールの読み込みとアンロードを処理するメソッドを提供します。  
  
 [インターフェイス](iclrdebugginglibraryprovider-interface.md)\
 メソッドを含む[、 ProvideLibrary メソッド](iclrdebugginglibraryprovider-providelibrary-method.md)は、共通言語ランタイムのバージョン固有のデバッグ ライブラリを配置し、要求に応じて読み込むライブラリ プロバイダーのコールバック インターフェイスを取得します。  
  
 [ICLR メタデータ ロケーター インターフェイス](iclrmetadatalocator-interface.md)\
 データ アクセス サービス層で使用して、対象プロセス内のアセンブリのメタデータを見つけるためのインターフェイスです。  
  
 [インターフェイス](icordebug-interface.md)\
 開発者が CLR 環境でアプリケーションをデバッグできるようにするメソッドを提供します。  
  
 [インターフェイス](icordebugappdomain-interface.md)\
 アプリケーション ドメインをデバッグするためのメソッドを提供します。  
  
 [インターフェイス](icordebugappdomain2-interface.md)\
 配列、ポインター、関数ポインター、および ByRef 型を使用するメソッドを提供します。 これは、`ICorDebugAppDomain` インターフェイスの機能を拡張するインターフェイスです。  
  
 [インターフェイス](icordebugappdomain3-interface.md)\
 アプリケーション ドメイン内の Windows ランタイム型を操作するメソッドを提供します。 このインターフェイスは、`ICorDebugAppDomain` インターフェイスと `ICorDebugAppDomain2` インターフェイスを拡張します。  
  
 [インターフェイス](icordebugappdomain4-interface.md)\
 COM 呼び出し可能ラッパーからマネージ オブジェクトを取得する[ICorDebugAppDomain](icordebugappdomain-interface.md)インターフェイスを論理的に拡張します。  
  
 [インターフェイス](icordebugappdomainenum-interface.md)\
 列挙体の次の位置から、指定した数の `ICorDebugAppDomain` の値を返すメソッドを提供します。  
  
 [インターフェイス](icordebugarrayvalue-interface.md)\
 1 次元または多次元の配列を表す `ICorDebugHeapValue` のサブクラスです。  
  
 [インターフェイスを指定します。](icordebugassembly-interface.md)\
 アセンブリを表します。  
  
 [インターフェイス](icordebugassembly2-interface.md)\
 アセンブリを表します。 これは、`ICorDebugAssembly` インターフェイスの機能を拡張するインターフェイスです。  
  
 [インターフェイス](icordebugassembly3-interface.md)\
 コンテナー アセンブリとその含まれているアセンブリをサポートするために[、ICorDebugAssembly](icordebugassembly-interface.md)インターフェイスを論理的に拡張します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスを作成します。](icordebugassemblyenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugAssembly` 配列を列挙します。  
  
 [インターフェイスをブロックします。](icordebugblockingobjectenum-interface.md)\
 [構造体の](cordebugblockingobject-structure.md)一覧の列挙子を提供します。  
  
 [インターフェイスを返します。](icordebugboxvalue-interface.md)\
 ボックス化された値クラスのオブジェクトを表す `ICorDebugHeapValue` のサブクラス。  
  
 [インターフェイスのデバッグのデバッグ](icordebugbreakpoint-interface.md)\
 関数のブレークポイント、または値のウォッチ ポイントを表します。  
  
 [インターフェイスをデバッグします。](icordebugbreakpointenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugBreakpoint` 配列を列挙します。  
  
 [インターフェイス](icordebugchain-interface.md)\
 物理呼び出し履歴または論理呼び出し履歴のセグメントを表します。  
  
 [インターフェイスをデバッグします。](icordebugchainenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugChain` 配列を列挙します。  
  
 [インターフェイス](icordebugclass-interface.md)\
 基本型または複合型 (つまり、ユーザー定義) のいずれかの型を表します。 型がジェネリックの場合、`ICorDebugClass` はインスタンス化されないジェネリック型を表します。  
  
 [インターフェイス](icordebugclass2-interface.md)\
 ジェネリック、または <xref:System.Type> 型のメソッド パラメーターを持つクラスを表します。 このインターフェイスは、`ICorDebugClass` の機能を拡張します。  
  
 [インターフェイスを指定します。](icordebugcode-interface1.md)\
 Microsoft Intermediate Language (MSIL) コードまたはネイティブ コードのセグメントを表します。  
  
 [インターフェイス](icordebugcode2-interface.md)\
 `ICorDebugCode` の機能を拡張するメソッドを提供します。  
  
 [インターフェイス](icordebugcode3-interface.md)\
 マネージ戻り値に関する情報を提供するために[ICorDebugCode](icordebugcode-interface1.md)と[ICorDebugCode2](icordebugcode2-interface.md)を拡張するメソッドを提供します。  
  
 [インターフェイス](icordebugcode4-interface.md)\
 デバッガーが関数のローカル変数と引数を列挙できるようにするメソッドを提供します。  
  
 [インターフェイスをデバッグします。](icordebugcodeenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugCode` 配列を列挙します。  
  
 [インターフェイスを指定します。](icordebugcomobjectvalue-interface.md)\
 キャッシュされたインターフェイス オブジェクトを取得するメソッドを提供します。  
  
 [インターフェイス](icordebugcontext-interface.md)\
 コンテキストのオブジェクトを表します。 このインターフェイスはまだ実装されていません。  
  
 [インターフェイスを使用します。](icordebugcontroller-interface.md)\
 コードの実行コンテキストを制御できる <xref:System.Diagnostics.Process> または <xref:System.AppDomain> のスコープを表します。  
  
 [インターフェイスを指定します。](icordebugdatatarget-interface.md)\
 特定のターゲット プロセスにアクセスするためのコールバック インターフェイスが用意されています。  
  
 [インターフェイス](icordebugdatatarget2-interface.md)\
 [インターフェイス](icordebugdatatarget-interface.md)を論理的に拡張します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebugdatatarget3-interface.md)\
 読み込まれたモジュールに関する情報を提供する[ICorDebugDataTarget](icordebugdatatarget-interface.md)インターフェイスを論理的に拡張します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスをデバッグします。](icordebugdebugevent-interface.md)\
 すべての `ICorDebug` デバッグ イベントを派生させる基本インターフェイスを定義します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスをデバッグします。](icordebugeditandcontinueerrorinfo-interface.md)\
 互換性のために残されています。 このインターフェイスは使用しないでください。  
  
 [インターフェイスを継続します。](icordebugeditandcontinuesnapshot-interface.md)\
 互換性のために残されています。 このインターフェイスは使用しないでください。  
  
 [インターフェイス](icordebugenum-interface1.md)\
 デバッグ中の列挙子の抽象基底インターフェイスとして機能します。  
  
 [インターフェイスをデバッグします。](icordebugerrorinfoenum-interface.md)\
 互換性のために残されています。 このインターフェイスは使用しないでください。  
  
 [インターフェイス](icordebugeval-interface.md)\
 デバッガーが、デバッグ中のコードのコンテキスト内でコードを実行できるメソッドを提供します。  
  
 [インターフェイス](icordebugeval2-interface.md)\
 ジェネリック型をサポートできるように `ICorDebugEval` を拡張します。  
  
 [インターフェイスを呼び出します。](icordebugexceptiondebugevent-interface.md)\
 例外イベントをサポートするために[インターフェイス](icordebugdebugevent-interface.md)を拡張します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスを呼び出します。](icordebugexceptionobjectcallstackenum-interface.md)\
 例外オブジェクトに埋め込まれているコール スタックの情報の列挙子を提供します。  
  
 [インターフェイスを呼び出します。](icordebugexceptionobjectvalue-interface.md)\
 [マネージ例外](icordebugobjectvalue-interface.md)オブジェクトからスタック トレース情報を提供するインターフェイスを拡張します。  
  
 [インターフェイスを指定します。](icordebugframe-interface.md)\
 現在のスタックのフレームを表します。  
  
 [インターフェイスをデバッグします。](icordebugframeenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugFrame` 配列を列挙します。  
  
 [インターフェイス](icordebugfunction-interface1.md)\
 マネージド関数またはマネージド メソッドを表します。  
  
 [インターフェイス](icordebugfunction2-interface.md)\
 `ICorDebugFunction` を論理的に拡張して、"マイ コードのみ" ステップ実行によるデバッグをサポートします。  
  
 [インターフェイス](icordebugfunction3-interface.md)\
 論理的に、ReJIT 要求からコードへのアクセスを提供する[ICorDebugFunction](icordebugfunction-interface1.md)インターフェイスを拡張します。  
  
 [インターフェイスを関数のブレークポイントのインターフェイスを使用します。](icordebugfunctionbreakpoint-interface.md)\
 関数内のブレークポイントをサポートするように `ICorDebugBreakpoint` を拡張します。  
  
 [インターフェイスを指定します。](icordebuggcreferenceenum-interface.md)\
 ガベージ コレクトされるオブジェクトの列挙子を提供します。  
  
 [インターフェイスを使用します。](icordebuggenericvalue-interface.md)\
 すべての値に適用する `ICorDebugValue` のサブクラスです。 このインターフェイスは、値に対して Get メソッドと Set メソッドを提供します。  
  
 [インターフェイスを使用します。](icordebugguidtotypeenum-interface.md)\
 GUID およびその対応する `ICorDebugType` オブジェクトをマップするオブジェクトの列挙子を提供します。  
  
 [インターフェイスを処理します。](icordebughandlevalue-interface.md)\
 デバッガーが作成したガベージ コレクションのハンドルへの参照値を表す `ICorDebugReferenceValue` のサブクラスです。  
  
 [インターフェイス](icordebugheapenum-interface.md)\
 マネージド ヒープのオブジェクトの列挙子を提供します。  
  
 [インターフェイスを指定します。](icordebugheapsegmentenum-interface.md)\
 マネージド ヒープのメモリ領域の列挙子を提供します。  
  
 [インターフェイスを指定します。](icordebugheapvalue-interface.md)\
 CLR ガベージ コレクターによって収集されたオブジェクトを表す `ICorDebugValue` のサブクラスです。  
  
 [インターフェイス](icordebugheapvalue2-interface1.md)\
 ランタイム ハンドルのサポートを提供する `ICorDebugHeapValue` の拡張機能です。  
  
 [インターフェイス](icordebugheapvalue3-interface.md)\
 オブジェクトのモニター ロック プロパティを公開します。  
  
 [インターフェイス](icordebugilcode-interface.md)\
 中間言語 (IL) コードのセグメントを表します。  
  
 [インターフェイス](icordebugilcode2-interface.md)\
 関数のローカル変数シグネチャのトークンを返すメソッドを提供するために[ICorDebugILCode](icordebugilcode-interface.md)インターフェイスを論理的に拡張し、プロファイラーのインストルメント化された中間言語 (IL) オフセットを元のメソッドの IL オフセットにマップします。  
  
 [インターフェイス](icordebugilframe-interface.md)\
 MSIL コードのスタック フレームを表します。  
  
 [インターフェイス](icordebugilframe2-interface.md)\
 `ICorDebugILFrame` の論理拡張機能です。  
  
 [インターフェイス](icordebugilframe3-interface.md)\
 関数の戻り値をカプセル化するメソッドを提供します。  
  
 [インターフェイス](icordebugilframe4-interface.md)\
 ローカル変数にアクセスできるようにするメソッドおよび中間言語 (IL) コードのスタック フレームのコードを提供します。 パラメーターは、プロファイラーの ReJIT インストルメンテーションに追加される変数およびコードへデバッガーがアクセスできるかどうかを指定します。  
  
 [フィールド インターフェイス](icordebuginstancefieldsymbol-interface.md)\
 インスタンス フィールドのデバッグ シンボル情報を表します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebuginternalframe-interface.md)\
 デバッガーのフレーム種類を識別します。  
  
 [インターフェイス](icordebuginternalframe2-interface.md)\
 [ICorDebugFrame](icordebugframe-interface.md)オブジェクトに関連するスタック アドレスと位置を含む、内部フレームに関する情報を提供します。  
  
 [インターフェイスを使用します。](icordebugloadedmodule-interface.md)\
 読み込まれたモジュールについての情報を提供します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスをデバッグします。](icordebugmanagedcallback-interface.md)\
 デバッガーのコールバックを処理するメソッドを提供します。  
  
 [インターフェイスをマネージ デバッグします。](icordebugmanagedcallback2-interface.md)\
 デバッガーの例外処理およびマネージド デバッグ アシスタント (MDA: Managed Debugging Assistants) をサポートするメソッドを提供します。 `ICorDebugManagedCallback2` は、`ICorDebugManagedCallback` の論理拡張機能です。  
  
 [インターフェイスをデバッグします。](icordebugmanagedcallback3-interface.md)\
 有効なカスタムのデバッガー通知が発生したことを示すコールバック メソッドを提供します。  
  
 [インターフェイス](icordebugmda-interface.md)\
 マネージド デバッグ アシスタント (MDA) メッセージを表します。  
  
 [インターフェイスをデバッグします。](icordebugmemorybuffer-interface.md)\
 メモリ内のバッファーを表します。 **.NET ネイティブのみで使用できます。**  
  
 [レコード インターフェイスをマージしました。](icordebugmergedassemblyrecord-interface.md)\
 マージされたアセンブリに関する情報を提供します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスをデバッグします。](icordebugmetadatalocator-interface.md)\
 デバッガーにメタデータ情報を提供します。  
  
 [インターフェイス](icordebugmodule-interface.md)\
 実行可能ファイルまたはダイナミック リンク ライブラリ (DLL: Dynamic-Link Library) のいずれかの CLR モジュールを表します。  
  
 [インターフェイス](icordebugmodule2-interface.md)\
 `ICorDebugModule` の論理的な拡張機能として動作します。  
  
 [インターフェイス](icordebugmodule3-interface.md)\
 動的モジュールのシンボル リーダーを作成します。  
  
 [インターフェイスをデバッグモジュールのブレークポイント](icordebugmodulebreakpoint-interface.md)\
 特定のモジュールにアクセスできるように `ICorDebugBreakpoint` を拡張します。  
  
 [インターフェイスをデバッグします。](icordebugmoduledebugevent-interface.md)\
 モジュール レベルの[イベント](icordebugdebugevent-interface.md)をサポートするようにインターフェイスを拡張します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスを使用します。](icordebugmoduleenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugModule` 配列を列挙します。  
  
 [インターフェイスを変更します。](icordebugmutabledatatarget-interface.md)\
 変更可能なデータ[ターゲット](icordebugdatatarget-interface.md)をサポートするインターフェイスを拡張します。  
  
 [インターフェイス](icordebugnativeframe-interface.md)\
 ネイティブ フレームで使用される `ICorDebugFrame` の特化された実装。  
  
 [インターフェイス](icordebugnativeframe2-interface.md)\
 子と親のフレームの関係をテストするメソッドを提供します。  
  
 [インターフェイス](icordebugobjectenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、オブジェクトの配列を相対仮想アドレス (RVA: Relative Virtual Address) で列挙します。  
  
 [インターフェイスを指定します。](icordebugobjectvalue-interface.md)\
 オブジェクトが含まれた値を表す `ICorDebugValue` のサブクラスです。  
  
 [インターフェイス](icordebugobjectvalue2-interface.md)\
 継承およびオーバーライドをサポートするように `ICorDebugObjectValue` を拡張します。  
  
 [インターフェイス](icordebugprocess-interface.md)\
 マネージド コードを実行しているプロセスを表します。  
  
 [インターフェイス](icordebugprocess2-interface1.md)\
 `ICorDebugProcess` の論理拡張機能です。  
  
 [インターフェイス](icordebugprocess3-interface.md)\
 カスタムのデバッガー通知を制御します。

 [インターフェイス](icordebugprocess4-interface.md)\
 プロセスの実行制御のサポートを提供します。
  
 [インターフェイス](icordebugprocess5-interface.md)\
 マネージ ヒープへのアクセスをサポートし、マネージ オブジェクトのガベージ コレクションに関する情報を提供し、デバッガーがアプリケーションのローカル ネイティブ イメージ キャッシュからイメージを読み込むかどうかを判断するために[、ICorDebugProcess](icordebugprocess-interface.md)インターフェイスを拡張します。  
  
 [インターフェイス](icordebugprocess6-interface.md)\
 [ICorDebugProcess](icordebugprocess-interface.md)インターフェイスを論理的に拡張して、ネイティブ例外デバッグ イベントでエンコードされたマネージ デバッグ イベントのデコードや仮想モジュール分割などの機能を有効にします。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebugprocess7-interface.md)\
 ターゲット プロセスでメモリ内のメタデータ更新を処理するようにデバッガーを構成するメソッドを提供します。  
  
 [インターフェイス](icordebugprocess8-interface.md)\
 特定の種類の[ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)例外コールバックを有効または無効にするインターフェイスを論理的に拡張します。 [ICorDebugProcess](icordebugprocess-interface.md)  
  
 [インターフェイスを処理します。](icordebugprocessenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugProcess` 配列を列挙します。  
  
 [インターフェイスを指定します。](icordebugreferencevalue-interface.md)\
 参照型をサポートする `ICorDebugValue` のサブクラス。  
  
 [インターフェイスを設定します。](icordebugregisterset-interface.md)\
 現在コードを実行しているマシン上で使用できるレジスタ セットを表します。  
  
 [インターフェイス](icordebugregisterset2-interface.md)\
 64 を超えるレジスタを持つハードウェア プラットフォーム用に `ICorDebugRegisterSet` の機能を拡張します。  
  
 [リモート インターフェイス](icordebugremote-interface.md)\
 リモート ターゲット プロセスに対してマネージド デバッガーを起動または接続する機能を提供します。  
  
 [インターフェイスをデバッグします。](icordebugremotetarget-interface.md)\
 開発者が CLR 環境で Silverlight ベース アプリケーションをデバッグできるようにするメソッドを提供します。  
  
 [アンワインドブルフレームインターフェイス](icordebugruntimeunwindableframe-interface.md)\
 共通言語ランタイム (CLR: Common Language Runtime) でフレームをアンワインドする必要のあるアンマネージ メソッドに対してサポートを提供します。  
  
 [インターフェイス](icordebugstackwalk-interface.md)\
 スレッドのスタック上のマネージド メソッド (フレーム) を取得するメソッドを提供します。  
  
 [インターフェイスを呼び出します。](icordebugstaticfieldsymbol-interface.md)\
 静的フィールドのデバッグ シンボル情報を表します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイスをデバッグします。](icordebugstepper-interface.md)\
 デバッガーが実行するコード実行内のステップを表します。コマンドの発行から完了までの間は識別子として機能します。これを使用するとステップをキャンセルできます。  
  
 [インターフェイス](icordebugstepper2-interface1.md)\
 マイ コードのみ (JMC: Just My Code) デバッグのサポートを提供します。  
  
 [インターフェイスをデバッグします。](icordebugstepperenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugStepper` 配列を列挙します。  
  
 [インターフェイスを返します。](icordebugstringvalue-interface.md)\
 文字列値に適用する `ICorDebugHeapValue` のサブクラスです。  
  
 [インターフェイスを指定します。](icordebugsymbolprovider-interface.md)\
 デバッグ シンボル情報を取得するために使用できるメソッドを提供します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebugsymbolprovider2-interface.md)\
 [ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md)インターフェイスを論理的に拡張して、追加のデバッグ シンボル情報を取得します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebugthread-interface.md)\
 プロセス内のスレッドを表します。 `ICorDebugThread` インスタンスの有効期間は、それが表しているスレッドの有効期間と同じです。  
  
 [インターフェイス](icordebugthread2-interface.md)\
 `ICorDebugThread` の論理的な拡張機能として動作します。  
  
 [インターフェイス](icordebugthread3-interface.md)\
 [エントリ](icordebugstackwalk-interface.md)ポイントを提供します。  
  
 [インターフェイス](icordebugthread4-interface.md)\
 スレッドのブロック情報を提供します。  
  
 [インターフェイス](icordebugthreadenum-interface1.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugThread` 配列を列挙します。  
  
 [インターフェイス](icordebugtype-interface.md)\
 基本型または複合型 (つまり、ユーザー定義) のいずれかの型を表します。 型がジェネリックの場合、`ICorDebugType` はインスタンス化されたジェネリック型を表します。  
  
 [インターフェイス](icordebugtype2-interface.md)\
 基本型または複合 (ユーザー定義) 型の型識別子を取得する[ICorDebugType](icordebugtype-interface.md)インターフェイスを拡張します。  
  
 [インターフェイス](icordebugtypeenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugType` 配列を列挙します。  
  
 [インターフェイスをデバッグします。](icordebugunmanagedcallback-interface.md)\
 CLR に直接関連していないネイティブ イベントについて通知します。  
  
 [を指定します。](icordebugvalue-interface.md)\
 デバッグ中のプロセス内の読み取り値または書き込み値を表します。  
  
 [2](icordebugvalue2-interface.md)\
 `ICorDebugValue` をサポートできるように `ICorDebugType` を拡張します。  
  
 [インターフェイス](icordebugvalue3-interface.md)\
 2 GB を超える配列をサポートするために、"ICorDebugValue" インターフェイスと "ICorDebugValue2" インターフェイスを拡張します。  
  
 [値ブレークポイントを指定します。](icordebugvaluebreakpoint-interface.md)\
 特定の値にアクセスできるように `ICorDebugBreakpoint` を拡張します。  
  
 [を返します。](icordebugvalueenum-interface.md)\
 `ICorDebugEnum` メソッドを実装し、`ICorDebugValue` 配列を列挙します。  
  
 [インターフェイスを変更します。](icordebugvariablehome-interface.md)\
 関数のローカル変数または引数を表します。  
  
 [インターフェイスを変数として使用します。](icordebugvariablehomeenum-interface.md)\
 関数のローカル変数と引数に列挙子を提供します。  
  
 [インターフェイスを使用します。](icordebugvariablesymbol-interface.md)\
 変数のデバッグ シンボル情報を取得します。 **.NET ネイティブのみで使用できます。**  
  
 [インターフェイス](icordebugvirtualunwinder-interface.md)\
 スタック アンワインドを支援するメソッドを提供します。 **.NET ネイティブのみで使用できます。**  
  
 [ICorパブリッシュインターフェイス](icorpublish-interface.md)\
 発行プロセスの汎用インターフェイスとして機能します。  
  
 [インターフェイス](icorpublishappdomain-interface.md)\
 アプリケーション ドメインの情報を表し、提供します。  
  
 [インターフェイスを発行します。](icorpublishappdomainenum-interface.md)\
 現在プロセス内に存在する `ICorPublishAppDomain` オブジェクトのコレクションを走査するメソッドを提供します。  
  
 [インターフェイス](icorpublishenum-interface.md)\
 発行する列挙子の抽象ベースとして機能します。  
  
 [インターフェイスを発行します。](icorpublishprocess-interface.md)\
 プロセスの情報にアクセスするメソッドを適用します。  
  
 [インターフェイスを発行します。](icorpublishprocessenum-interface.md)\
 `ICorPublishProcess` オブジェクトのコレクションを走査するメソッドを提供します。  

 [インターフェイス](isosdacinterface-interface.md)\
 から`SOS`データにアクセスするためのヘルパー メソッドを提供します。

 [インターフェイスを定義します。](ixclrdatamethoddefinition-interface.md)\
 メソッド定義に関する情報を照会するためのメソッドを提供します。

 [インターフェイス](ixclrdatamethodinstance-interface.md)\
 メソッド インスタンスに関する情報を照会するためのメソッドを提供します。

 [インターフェイス](ixclrdatamodule-interface.md)\
 読み込まれたモジュールに関する情報を照会するためのメソッドを提供します。

 [インターフェイス](ixclrdataprocess-interface.md)\
 プロセスに関する情報を照会するためのメソッドを提供します。
  
## <a name="related-sections"></a>関連項目  
 [コクラスのデバッグ](debugging-coclasses.md)\
 [グローバル静的関数のデバッグ](debugging-global-static-functions.md)\
 [列挙体のデバッグ](debugging-enumerations.md)\
 [構造体のデバッグ](debugging-structures.md)\
