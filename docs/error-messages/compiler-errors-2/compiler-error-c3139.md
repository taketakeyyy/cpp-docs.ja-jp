---
title: コンパイラエラー C3139
ms.date: 11/04/2016
f1_keywords:
- C3139
helpviewer_keywords:
- C3139
ms.assetid: 95c92263-10ac-4ff3-b385-6312dd92adbc
ms.openlocfilehash: 86f905653c6e1574a1d1c0a1225294b3a4dc5f3e
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91506178"
---
# <a name="compiler-error-c3139"></a>コンパイラエラー C3139

' struct ': メンバーのない UDT をエクスポートすることはできません

空の UDT (ユーザー定義型) に [エクスポート](../../windows/attributes/export.md) 属性を適用しようとしました。 次に例を示します。

```cpp
// C3139.cpp
#include "unknwn.h"
[emitidl];
[module(name=xx)];

[export] struct MyStruct {   // C3139 empty type
};
int main(){}
```
