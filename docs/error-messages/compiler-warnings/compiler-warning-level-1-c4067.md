---
title: コンパイラの警告 (レベル 1) C4067
ms.date: 11/04/2016
f1_keywords:
- C4067
helpviewer_keywords:
- C4067
ms.assetid: 1d10353e-8cd5-4b01-9184-a06189b965a4
ms.openlocfilehash: 8bdd16f5c3182e4217e195475bdb4a9a0f60fa6f
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80164119"
---
# <a name="compiler-warning-level-1-c4067"></a>コンパイラの警告 (レベル 1) C4067

> プリプロセッサディレクティブの後に予期しないトークンがあります-改行が必要です

## <a name="remarks"></a>解説

コンパイラは、プリプロセッサディレクティブの後に余分な文字を検出し、無視しました。 これは、予期しない文字によって発生することがありますが、一般的な原因としては、ディレクティブの後にセミコロンが使用されます。 コメントは、この警告を発生させません。 **/Za**コンパイラオプションでは、既定の設定よりも多くのプリプロセッサディレクティブに対してこの警告が有効になります。

## <a name="example"></a>例

```cpp
// C4067a.cpp
// compile with: cl /EHsc /DX /W1 /Za C4067a.cpp
#include <iostream>
#include <string> s     // C4067
#if defined(X);         // C4067
std::string s{"X is defined"};
#else
std::string s{"X is not defined"};
#endif;                 // C4067 only under /Za
int main()
{
    std::cout << s << std::endl;
}
```

この警告を解決するには、余分な文字を削除するか、コメントブロックに移動します。 **/Za**コンパイラオプションを削除すると、特定の C4067 の警告が無効になる場合があります。

```cpp
// C4067b.cpp
// compile with: cl /EHsc /DX /W1 C4067b.cpp
#include <iostream>
#include <string>
#if defined(X)
std::string s{"X is defined"};
#else
std::string s{"X is not defined"};
#endif
int main()
{
    std::cout << s << std::endl;
}
```
