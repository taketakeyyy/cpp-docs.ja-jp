---
title: コンパイラエラー C2723
ms.date: 11/04/2016
f1_keywords:
- C2723
helpviewer_keywords:
- C2723
ms.assetid: 86925601-2297-4cfd-94e2-2caf27c474c4
ms.openlocfilehash: f723fcc0a3d9626f01f2059a3d9363801221bca0
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87216051"
---
# <a name="compiler-error-c2723"></a>コンパイラエラー C2723

'function' : 'specifier' 指定子が関数の定義で誤って指定されています

この指定子は、クラス宣言の外側にある関数定義では使用できません。 指定 **`virtual`** 子は、クラス宣言内のメンバー関数宣言に対してのみ指定できます。

次の例では、C2723 を生成し、その修正方法を示しています。

```cpp
// C2723.cpp
struct X {
   virtual void f();
   virtual void g();
};

virtual void X::f() {}   // C2723

// try the following line instead
void X::g() {}
```
