---
title: コンパイラの警告 (レベル 1) C4364
ms.date: 11/04/2016
f1_keywords:
- C4364
helpviewer_keywords:
- C4364
ms.assetid: 1477634c-d60f-4570-ad16-1aaeae24ac7f
ms.openlocfilehash: 7f1c71cb3cd6a99d4ed9960032813e7cebca7591
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90685080"
---
# <a name="compiler-warning-level-1-c4364"></a>コンパイラの警告 (レベル 1) C4364

\#as_friend 属性のない場所 (line_number) で以前に検出されたアセンブリ ' file ' に対してを使用しています。as_friend 適用されていません

`#using`指定されたメタデータファイルに対してディレクティブが繰り返されましたが、この **`as_friend`** 修飾子は最初の発生時には使用されませんでした。コンパイラは2番目のを無視 **`as_friend`** します。

詳細については、「 [フレンドアセンブリ (C++)](../../dotnet/friend-assemblies-cpp.md)」を参照してください。

## <a name="examples"></a>例

コンポーネントを作成する例を次に示します。

```cpp
// C4364.cpp
// compile with: /clr /LD
ref class A {};
```

次の例では、C4364 が生成されます。

```cpp
// C4364_b.cpp
// compile with: /clr /W1 /c
#using " C4364.dll"
#using " C4364.dll" as_friend   // C4364
```
