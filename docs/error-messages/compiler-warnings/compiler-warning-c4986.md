---
title: コンパイラの警告 C4986
ms.date: 11/04/2016
f1_keywords:
- C4986
helpviewer_keywords:
- C4986
ms.assetid: a3a7b008-29dd-4203-85f3-7740ab6790bb
ms.openlocfilehash: ae782ea0a11bd72c867ea9532a62d0b14cd98453
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90684393"
---
# <a name="compiler-warning-c4986"></a>コンパイラの警告 C4986

' function ': 例外指定が前の宣言と一致しません

この警告は、1つの宣言に例外指定があり、もう一方の宣言には存在しない場合に生成されることがあります。

既定では、C4986 はオフになっています。 詳細については、「 [Compiler Warnings That Are Off by Default](../../preprocessor/compiler-warnings-that-are-off-by-default.md)」を参照してください。

## <a name="examples"></a>例

次の例では、C4986 が生成されます。

```cpp
class X { };
void f1() throw (X*);
// ...
void f1()
{
    // ...
}
```

次の例では、この警告を解消します。

```cpp
class X { };
void f1() throw (X*);
// ...
void f1() throw (X*)
{
    // ...
}
```
