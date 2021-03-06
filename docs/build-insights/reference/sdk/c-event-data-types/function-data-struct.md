---
title: FUNCTION_DATA 構造体
description: C++ Build Insights SDK FUNCTION_DATA 構造体のリファレンス。
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- FUNCTION_DATA
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: 1034ce01bba6422d0c47fc34b308cafcc113e32b
ms.sourcegitcommit: 6280a4c629de0f638ebc2edd446de2a9b11f0406
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90041745"
---
# <a name="function_data-structure"></a>FUNCTION_DATA 構造体

::: moniker range="<=vs-2015"

C++ Build Insights SDK は、Visual Studio 2017 以降と互換性があります。 これらのバージョンのドキュメントを表示するには、この記事の Visual Studio **Version** セレクター コントロールを Visual Studio 2017 または Visual Studio 2019 に設定します。 このページの目次の一番上にあります。

::: moniker-end
::: moniker range=">=vs-2017"

`FUNCTION_DATA` 構造体は関数を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct FUNCTION_DATA_TAG
{
    const char*         Name;

} FUNCTION_DATA;
```

## <a name="members"></a>メンバー

| 名前 | [説明] |
|--|--|
| `Name` | UTF-8 でエンコードされる関数の名前。 |

::: moniker-end
