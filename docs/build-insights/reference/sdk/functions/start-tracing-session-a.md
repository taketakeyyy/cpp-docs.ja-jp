---
title: トレースセッションを開始する
description: C++ ビルド インサイト SDK 開始トレーシングセッション関数リファレンス。
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- StartTracingSessionA
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: 1c184e214c7f55bb7eaa6eb03f21e792ef90fa40
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81323767"
---
# <a name="starttracingsessiona"></a>トレースセッションを開始する

::: moniker range="<=vs-2015"

C++ ビルド インサイト SDK は、Visual Studio 2017 以降と互換性があります。 これらのバージョンのドキュメントを参照するには、この記事の Visual Studio**バージョン**セレクター コントロールを Visual Studio 2017 または Visual Studio 2019 に設定します。 このページの目次の上部に表示されます。

::: moniker-end
::: moniker range=">=vs-2017"

この`StartTracingSessionA`関数は、トレース セッションを開始します。 この関数を呼び出す実行可能ファイルには、管理者権限が必要です。

## <a name="syntax"></a>構文

```cpp
enum RESULT_CODE StartTracingSessionA(
    const char*                    sessionName,
    const TRACING_SESSION_OPTIONS* options);
```

### <a name="parameters"></a>パラメーター

*Sessionname*\
開始するトレース セッションの名前。 [StopTracingSessionA](stop-tracing-session.md)またはその他の停止トレース関数を呼び出すときに、同じ名前を使用します。

*オプション*\
[TRACING_SESSION_OPTIONS](../other-types/tracing-session-options-struct.md)オブジェクトへのポインター。 このオブジェクトを使用して、トレース セッションで収集するイベントを選択します。

### <a name="return-value"></a>戻り値

[RESULT_CODE](../other-types/result-code-enum.md)列挙型からの結果コード。

::: moniker-end
