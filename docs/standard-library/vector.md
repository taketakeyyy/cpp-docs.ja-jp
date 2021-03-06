---
title: '&lt;vector&gt;'
ms.date: 11/04/2016
f1_keywords:
- <vector>
helpviewer_keywords:
- vector header
ms.assetid: c1431ad8-c0b6-4dbb-89c4-5f651e432d7f
ms.openlocfilehash: 7cecff1e5e0014c4f1a4294a5c6ba25c5d38da67
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88840012"
---
# <a name="ltvectorgt"></a>&lt;vector&gt;

コンテナークラステンプレートベクターといくつかのサポートテンプレートを定義します。

`vector` 指定された型の要素を直線上のシーケンスに編成するコンテナーです。 このシーケンスでは、任意の要素を高速にランダム アクセスしたり、動的に追加および削除したりできます。 `vector` は、ランダム アクセスのパフォーマンスを重視するシーケンスに適したコンテナーです。

> [!NOTE]
> ライブラリは、 \<vector> ステートメントも使用し `#include <initializer_list>` ます。

クラス `vector` の詳細については、「[vector クラス](../standard-library/vector-class.md)」をご覧ください。 特殊化の詳細については `vector<bool>` 、「 [vector \<bool> クラス](../standard-library/vector-bool-class.md)」を参照してください。

## <a name="syntax"></a>構文

```cpp
namespace std {
template <class Type, class Allocator>
class vector;
template <class Allocator>
class vector<bool>;

template <class Allocator>
struct hash<vector<bool, Allocator>>;

// TEMPLATE FUNCTIONS
template <class Type, class Allocator>
bool operator== (
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
bool operator!= (
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
bool operator<(
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
bool operator> (
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
bool operator<= (
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
bool operator>= (
    const vector<Type, Allocator>& left,
    const vector<Type, Allocator>& right);

template <class Type, class Allocator>
void swap (
    vector<Type, Allocator>& left,
    vector<Type, Allocator>& right);

}  // namespace std
```

### <a name="parameters"></a>パラメーター

*各種*\
ベクター内に格納されるデータ型に対するテンプレート パラメーター。

*アロケーター*\
メモリの割り当てと解放を担当する格納されたアロケーター オブジェクトのテンプレート パラメーター。

*左側*\
比較演算の最初の (左辺の) ベクター

*そうです*\
比較演算の 2 つ目の (右辺の) ベクター。

## <a name="members"></a>メンバー

### <a name="operators"></a>演算子

|名前|説明|
|-|-|
|[operator!=](../standard-library/vector-operators.md#op_neq)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクトと等しくないかどうかを調べます。|
|[<演算子 ](../standard-library/vector-operators.md#op_lt)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクトより小さいかどうかを調べます。|
|[operator\<=](../standard-library/vector-operators.md#op_gt_eq)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクト以下かどうかを調べます。|
|[operator = =](../standard-library/vector-operators.md#op_eq_eq)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクトと等しいかどうかを調べます。|
|[>演算子 ](../standard-library/vector-operators.md#op_gt)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクトより大きいかどうかを調べます。|
|[operator>=](../standard-library/vector-operators.md#op_gt_eq)|演算子の左辺のベクター オブジェクトが右辺のベクター オブジェクト以上かどうかを調べます。|

### <a name="classes"></a>クラス

|名前|説明|
|-|-|
|[vector クラス](../standard-library/vector-class.md)|指定された型の要素を直線上に配置し、任意の要素に対する高速なランダム アクセスを可能にするシーケンス コンテナーのクラス テンプレートです。|

### <a name="specializations"></a>特殊化

|名前|説明|
|-|-|
|hash|ベクターのハッシュを返します。|
|[vector \<bool> クラス](../standard-library/vector-bool-class.md)|**`bool`** 特殊化で使用される基になる型のアロケーターを持つ型の要素に対するクラステンプレートベクターの完全な特殊化。|

## <a name="requirements"></a>必要条件

**ヘッダー:**\<vector>

**名前空間:** std

## <a name="see-also"></a>関連項目

[ヘッダーファイルのリファレンス](../standard-library/cpp-standard-library-header-files.md)\
[C++ 標準ライブラリのスレッドセーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C++ 標準ライブラリリファレンス](../standard-library/cpp-standard-library-reference.md)
