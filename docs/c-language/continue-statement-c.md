---
title: continue ステートメント (C)
ms.date: 11/04/2016
f1_keywords:
- continue
helpviewer_keywords:
- loop structures, continue keyword
- continue keyword [C]
ms.assetid: 969f293a-45fe-48a7-b4c6-287ba27a631d
ms.openlocfilehash: 27d1d0aa0e49c5c46e4ea4e010635ca0057c3f85
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90684834"
---
# <a name="continue-statement-c"></a>continue ステートメント (C)

**`continue`** ステートメントは、それを囲む最も近い **`do`** 、 **`for`** 、または **`while`** ステートメントの次の反復処理に制御を渡し、 **`do`** 、 **`for`** 、または **`while`** ステートメント本体の残りのステートメントをバイパスします。

## <a name="syntax"></a>構文

*jump-statement*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**continue ;**

**`do`** 、 **`for`** 、または **`while`** ステートメントの次の反復処理は次のように決定されます。

- **`do`** または **`while`** ステートメント内では、次の繰り返しは **`do`** または **`while`** ステートメントの式の再評価によって開始されます。

- **`for`** ステートメントの **`continue`** ステートメントは、 **`for`** ステートメントのループ式を評価します。 その後、コンパイラは条件式を再評価し、その結果に応じて、ステートメント本体を終了または反復処理します。 **`for`** ステートメントおよびその非終端要素の詳細については、「[for ステートメント](../c-language/for-statement-c.md)」を参照してください。

**`continue`** ステートメントの例を次に示します。

```C
while ( i-- > 0 )
{
    x = f( i );
    if ( x == 1 )
        continue;
    y += x * x;
}
```

この例では、ステートメント本体は、`i` が 0 を超える場合に実行されます。 最初に、`f(i)` は `x` に割り当てられています。次に、`x` が 1 に等しい場合は、 **`continue`** ステートメントが実行されます。 本体のステートメントの残りの部分は無視され、ループ テストの評価がループの先頭から再び実行されます。

## <a name="see-also"></a>関連項目

[continue ステートメント](../cpp/continue-statement-cpp.md)
