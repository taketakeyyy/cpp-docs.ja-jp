---
title: '&lt;スパン&gt;'
description: 標準テンプレートライブラリ (STL) スパン名前空間の API リファレンス。連続した一連のオブジェクトに対して簡易ビューを提供します。
ms.date: 05/28/2020
f1_keywords:
- <span>
helpviewer_keywords:
- span header
ms.openlocfilehash: f4c6b141dfea6464e58d06e221a39a693469d31c
ms.sourcegitcommit: 6280a4c629de0f638ebc2edd446de2a9b11f0406
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90039873"
---
# <a name="ltspangt"></a>&lt;スパン&gt;

は、 `span` 連続した一連のオブジェクトに対するビューです。 高速および境界の安全なアクセスを提供します。 またはとは異なり `vector` `array` 、アクセスを提供する要素を "所有" することはできません。

詳細については、 [span クラス](span-class.md) を参照してください。 スパンを使用する方法の例を次に示します。

```cpp
#include <span>
#include <iostream>

void Show(std::span<int> someValues)
{
    // show values in reverse
    for (auto rIt = someValues.rbegin(); rIt != someValues.rend(); ++rIt)
    {
        std::cout << *rIt;
    }

    // show a subspan
    for (auto& i : someValues.subspan(1, 2))
    {
        std::cout << i;
    }
}

int main()
{
    int numbers[]{ 0,1,2,3,4 };
    Show(numbers); // note conversion from array to span
}
```

## <a name="requirements"></a>要件

**ヘッダー:**\<span>

**名前空間:** std

**コンパイラオプション:** [/std: c + + latest](../build/reference/std-specify-language-standard-version.md)

## <a name="members"></a>メンバー

### <a name="classes"></a>クラス

|名前|説明|
|-|:-|
|[スパン](span-class.md)| 連続した一連のオブジェクトに対するビューを提供します。 |

### <a name="operators"></a>オペレーター

|Name|説明|
|-|:-|
|[operator =](span-class.md#op_eq)| スパンの割り当て |
|[operator\[\]](span-class.md#op_at)| 要素アクセス |

### <a name="functions"></a>機能

|Name|説明|
|-|:-|
| [as_bytes](span-functions.md#as_bytes)| スパンの基になる読み取り専用のバイトを取得します。 |
| [as_writable_bytes](span-functions.md#as_writable_bytes) | スパンの基になるバイトを取得します。 |

### <a name="constants"></a>定数

|Name|説明|
|-|:-|
| **dynamic_extent** | スパンサイズがコンパイル時ではなく実行時に決定されることを示します。 スパン内の要素の数がコンパイル時にわかっている場合は、テンプレートパラメーターとして指定され `Extent` ます。 ランタイムまでの数値がわからない場合は、代わりにを指定し `dynamic_extent` ます。 |

## <a name="see-also"></a>参照

[ヘッダー ファイル リファレンス](../standard-library/cpp-standard-library-header-files.md)
