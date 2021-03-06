---
title: IExecutionResource 構造体
ms.date: 11/04/2016
f1_keywords:
- IExecutionResource
- CONCRTRM/concurrency::IExecutionResource
- CONCRTRM/concurrency::IExecutionResource::IExecutionResource::CurrentSubscriptionLevel
- CONCRTRM/concurrency::IExecutionResource::IExecutionResource::GetExecutionResourceId
- CONCRTRM/concurrency::IExecutionResource::IExecutionResource::GetNodeId
- CONCRTRM/concurrency::IExecutionResource::IExecutionResource::Remove
helpviewer_keywords:
- IExecutionResource structure
ms.assetid: 6b27042b-b98c-4f7f-b831-566950af84cd
ms.openlocfilehash: af6b10d1552770c776762ed195f5efceab30a3d5
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87215791"
---
# <a name="iexecutionresource-structure"></a>IExecutionResource 構造体

ハードウェア スレッドの抽象化です。

## <a name="syntax"></a>構文

```cpp
struct IExecutionResource;
```

## <a name="members"></a>メンバー

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[IExecutionResource:: CurrentSubscriptionLevel](#currentsubscriptionlevel)|この実行リソースが表す、基になるハードウェアスレッドに現在関連付けられている、アクティブ化された仮想プロセッサルートとサブスクライブされた外部スレッドの数を返します。|
|[IExecutionResource:: GetExecutionResourceId](#getexecutionresourceid)|この実行リソースが表すハードウェアスレッドの一意の識別子を返します。|
|[IExecutionResource:: GetNodeId](#getnodeid)|この実行リソースが属するプロセッサノードの一意の識別子を返します。|
|[IExecutionResource:: Remove](#remove)|この実行リソースをリソースマネージャーに返します。|

## <a name="remarks"></a>解説

実行リソースは、スタンドアロンにすることも、仮想プロセッサルートに関連付けることもできます。 アプリケーションのスレッドがスレッドサブスクリプションを作成すると、スタンドアロンの実行リソースが作成されます。 メソッド[ISchedulerProxy:: SubscribeThread](ischedulerproxy-structure.md#subscribecurrentthread)と[ISchedulerProxy:: RequestInitialVirtualProcessors](ischedulerproxy-structure.md#requestinitialvirtualprocessors)は、スレッドサブスクリプションを作成し、 `IExecutionResource` サブスクリプションを表すインターフェイスを返します。 スレッドサブスクリプションの作成は、リソースマネージャーに対して、指定されたスレッドがスケジューラに対してキューに登録された作業に参加すること、およびリソースマネージャーがスケジューラに割り当てる仮想プロセッサルートを通知する方法です。 リソースマネージャーは、この情報を使用して、可能な場所にハードウェアスレッドのオーバーサブスクライブを回避します。

## <a name="inheritance-hierarchy"></a>継承階層

`IExecutionResource`

## <a name="requirements"></a>必要条件

**ヘッダー:** concrtrm. h

**名前空間:** concurrency

## <a name="iexecutionresourcecurrentsubscriptionlevel-method"></a><a name="currentsubscriptionlevel"></a>IExecutionResource:: CurrentSubscriptionLevel メソッド

この実行リソースが表す、基になるハードウェアスレッドに現在関連付けられている、アクティブ化された仮想プロセッサルートとサブスクライブされた外部スレッドの数を返します。

```cpp
virtual unsigned int CurrentSubscriptionLevel() const = 0;
```

### <a name="return-value"></a>戻り値

現在のサブスクリプションレベルです。

### <a name="remarks"></a>解説

サブスクリプションレベルは、ハードウェアスレッドに関連付けられている実行中のスレッドの数を示します。 これには、サブスクライブされたスレッドの形式でリソースマネージャーが認識しているスレッドと、スレッドプロキシをアクティブに実行している仮想プロセッサルートだけが含まれます。

パラメーターを値に設定してメソッド[ISchedulerProxy:: SubscribeCurrentThread](ischedulerproxy-structure.md#subscribecurrentthread)またはメソッド[ISchedulerProxy:: RequestInitialVirtualProcessors](ischedulerproxy-structure.md#requestinitialvirtualprocessors)を呼び出すと、 `doSubscribeCurrentThread` **`true`** ハードウェアスレッドのサブスクリプションレベルが1ずつ増加します。 また、サブスクリプションを `IExecutionResource` 表すインターフェイスも返されます。 [Iexecutionresource:: Remove](#remove)を呼び出すと、ハードウェアスレッドのサブスクリプションレベルが1ずつ減少します。

[Ivirtualprocessorroot:: Activate](ivirtualprocessorroot-structure.md#activate)メソッドを使用して仮想プロセッサルートをアクティブ化すると、ハードウェアスレッドのサブスクリプションレベルが1ずつ増加します。 [Ivirtualprocessorroot::D eactivate](ivirtualprocessorroot-structure.md#deactivate)または[iexecutionresource:: Remove](#remove)のメソッドは、アクティブ化された仮想プロセッサルートで呼び出されると、サブスクリプションレベルを1ずつデクリメントします。

リソースマネージャーは、スケジューラ間でリソースを移動するタイミングを決定する方法の1つとして、サブスクリプションレベル情報を使用します。

## <a name="iexecutionresourcegetexecutionresourceid-method"></a><a name="getexecutionresourceid"></a>IExecutionResource:: GetExecutionResourceId メソッド

この実行リソースが表すハードウェアスレッドの一意の識別子を返します。

```cpp
virtual unsigned int GetExecutionResourceId() const = 0;
```

### <a name="return-value"></a>戻り値

この実行リソースの基になるハードウェアスレッドの一意の識別子。

### <a name="remarks"></a>解説

各ハードウェアスレッドには、同時実行ランタイムによって一意の識別子が割り当てられます。 複数の実行リソースがハードウェアスレッドに関連付けられている場合、それらはすべて同じ実行リソース識別子を持ちます。

## <a name="iexecutionresourcegetnodeid-method"></a><a name="getnodeid"></a>IExecutionResource:: GetNodeId メソッド

この実行リソースが属するプロセッサノードの一意の識別子を返します。

```cpp
virtual unsigned int GetNodeId() const = 0;
```

### <a name="return-value"></a>戻り値

プロセッサノードの一意の識別子。

### <a name="remarks"></a>解説

同時実行ランタイムは、システム上のハードウェアスレッドをプロセッサノードのグループ単位で表します。 通常、ノードはシステムのハードウェアトポロジから派生します。 たとえば、特定のソケットまたは特定の NUMA ノードのすべてのプロセッサが、同じプロセッサノードに属している場合があります。 リソースマネージャーでは、これらのノードに一意の識別子が割り当てられ `0` `nodeCount - 1` ます。ここで、は、 `nodeCount` システム上のプロセッサノードの合計数を表します。

ノードの数は、関数[GetProcessorNodeCount](concurrency-namespace-functions.md)から取得できます。

## <a name="iexecutionresourceremove-method"></a><a name="remove"></a>IExecutionResource:: Remove メソッド

この実行リソースをリソースマネージャーに返します。

```cpp
virtual void Remove(_Inout_ IScheduler* pScheduler) = 0;
```

### <a name="parameters"></a>パラメーター

*pScheduler*<br/>
この実行リソースを削除する要求を行うスケジューラへのインターフェイス。

### <a name="remarks"></a>解説

このメソッドを使用して、スタンドアロンの実行リソースだけでなく、仮想プロセッサのルートに関連付けられている実行リソースをリソースマネージャーに返すこともできます。

[ISchedulerProxy:: SubscribeCurrentThread](ischedulerproxy-structure.md#subscribecurrentthread)メソッドまたは[ISchedulerProxy:: RequestInitialVirtualProcessors](ischedulerproxy-structure.md#requestinitialvirtualprocessors)メソッドのいずれかから受け取ったスタンドアロンの実行リソースの場合、メソッドを呼び出すと、リソースが作成された `Remove` スレッドサブスクリプションが終了します。 スケジューラプロキシをシャットダウンする前に、すべてのスレッドサブスクリプションを終了する必要があり、サブスクリプションを作成したスレッドからを呼び出す必要があり `Remove` ます。

`Remove`インターフェイスはインターフェイスから継承するため、仮想プロセッサのルートも、メソッドを呼び出すことによってリソースマネージャーに返すことができ `IVirtualProcessorRoot` `IExecutionResource` ます。 [IScheduler:: RemoveVirtualProcessors](ischeduler-structure.md#removevirtualprocessors)メソッドの呼び出しへの応答として、または[ISchedulerProxy:: createoversubscriber](ischedulerproxy-structure.md#createoversubscriber)メソッドから取得したオーバーサブスクライブ仮想プロセッサルートを使用して完了した場合は、仮想プロセッサルートを返す必要がある場合があります。 仮想プロセッサルートの場合、どのスレッドがメソッドを呼び出すことができるかに制限はありません `Remove` 。

`invalid_argument`パラメーターがに設定されている場合は、がスローされ `pScheduler` `NULL` ます。

`invalid_operation`パラメーター `pScheduler` が、この実行リソースが作成されたスケジューラと異なる場合、またはスタンドアロンの実行リソースを使用して、現在のスレッドがスレッドサブスクリプションを作成したスレッドと異なる場合は、がスローされます。

## <a name="see-also"></a>関連項目

[concurrency 名前空間](concurrency-namespace.md)<br/>
[IVirtualProcessorRoot 構造体](ivirtualprocessorroot-structure.md)
