---
title: Signed Bitwise Operations (符号付きビット処理演算)
ms.date: 11/04/2016
helpviewer_keywords:
- bitwise operations
- signed bitwise operations
ms.assetid: 1e5cf65b-ee32-41a0-a5c2-82c1854091f6
ms.openlocfilehash: 43f65fd5d1ea14ef5e15f18d9c8516ccf5fb1e08
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62158320"
---
# <a name="signed-bitwise-operations"></a>Signed Bitwise Operations (符号付きビット処理演算)

**ANSI 3.3** 符号付き整数のビットごとの演算の結果

符号付き整数のビットごとの演算は、符号なし整数のビットごとの演算と同じように動作します。 たとえば、`-16 & 99` は、バイナリでは次のように表されます。

```
  11111111 11110000
& 00000000 01100011
  _________________
  00000000 01100000
```

ビットごとの AND の結果は 96 です。

## <a name="see-also"></a>関連項目

[整数](../c-language/integers.md)
