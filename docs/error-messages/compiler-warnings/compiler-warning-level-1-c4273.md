---
title: コンパイラの警告 (レベル 1) C4273
ms.date: 11/04/2016
f1_keywords:
- C4273
helpviewer_keywords:
- C4273
ms.assetid: cc18611d-9454-40a4-ad73-69823d5888fb
ms.openlocfilehash: 08508ce11943605e3a7432491f8c4dd1d1175e2f
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90686536"
---
# <a name="compiler-warning-level-1-c4273"></a>コンパイラの警告 (レベル 1) C4273

' function ': DLL リンケージが一致しません

ファイル内の2つの定義は、 [dllimport](../../cpp/dllexport-dllimport.md)の使用方法が異なります。

## <a name="examples"></a>例

次の例では、C4273 が生成されます。

```cpp
// C4273.cpp
// compile with: /W1 /c
char __declspec(dllimport) c;
char c;   // C4273, delete this line or the line above to resolve
```

次の例では、C4273 が生成されます。

```cpp
// C4273_b.cpp
// compile with: /W1 /clr /c
#include <stdio.h>
extern "C" int printf_s(const char *, ...);   // C4273
```
