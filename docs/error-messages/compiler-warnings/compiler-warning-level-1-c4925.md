---
title: コンパイラの警告 (レベル 1) C4925
ms.date: 11/04/2016
f1_keywords:
- C4925
helpviewer_keywords:
- C4925
ms.assetid: a4b206c0-016a-4f28-873a-bb8bb41bad50
ms.openlocfilehash: defd60d02a8725b114b3901f8d70af87e27445c4
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80174636"
---
# <a name="compiler-warning-level-1-c4925"></a>コンパイラの警告 (レベル 1) C4925

'method': dispinterface メソッドはスクリプトから呼び出すことはできません

スクリプト言語は VT_BYREF 'in' パラメーターを作成することはできません。VT_BYREF 'out' パラメーターのみ作成できます。

この警告を解決する別の方法としては、(定義と実装の) パラメーターをポインター型にしないようにします。

次の例では C4925 が生成されます。

```cpp
// C4925.cpp
// compile with: /LD /W1
#define _ATL_ATTRIBUTES 1
#include <atlbase.h>
#include <atlcom.h>
[ module(name="Test")];

[ dispinterface, uuid("00000000-0000-0000-0000-000000000001") ]
__interface IDisp {
   [id(9)] void f([in] int*);
};

[ coclass, uuid("00000000-0000-0000-0000-000000000002")  ]
struct CDisp : IDisp {   // C4925
   void f(int*) {}
};
```
