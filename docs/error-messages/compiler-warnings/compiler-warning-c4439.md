---
title: コンパイラの警告 C4439
ms.date: 11/04/2016
f1_keywords:
- C4439
helpviewer_keywords:
- C4439
ms.assetid: 9449958f-f407-4824-829b-9e092f2af97d
ms.openlocfilehash: baf74733c94fdb03f130d2300d0918845cc4de4c
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87223331"
---
# <a name="compiler-warning-c4439"></a>コンパイラの警告 C4439

' function ': シグネチャのマネージ型を持つ関数定義には __clrcall の呼び出し規約が必要です

コンパイラは、呼び出し規約をに暗黙的に置き換えました [`__clrcall`](../../cpp/clrcall.md) 。 この警告を解決するに **`__cdecl`** は、またはの呼び出し規約を削除し **`__stdcall`** ます。

C4439 は常にエラーとして発行されます。 この警告は、またはで無効にできます `#pragma warning` 。詳細については、 **`/wd`** 「 [warning](../../preprocessor/warning.md) or [/w、/W0、/W1、/W2、/W3、/W4、/W1、/W2、/W3、/W4、/Wall、/wd、/we、/wo、/Wv、/wx (警告レベル)](../../build/reference/compiler-option-warning-level.md) 」を参照してください。

## <a name="example"></a>例

次の例では、C4439 が生成されます。

```cpp
// C4439.cpp
// compile with: /clr
void __stdcall f( System::String^ arg ) {}   // C4439
void __clrcall f2( System::String^ arg ) {}   // OK
void f3( System::String^ arg ) {}   // OK
```
