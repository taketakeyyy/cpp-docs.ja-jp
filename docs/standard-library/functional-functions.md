---
title: '&lt;functional&gt; 関数'
ms.date: 02/21/2019
f1_keywords:
- functional/std::bind
- functional/std::bind1st
- functional/std::bind2nd
- functional/std::bit_and
- functional/std::bit_not
- functional/std::bit_or
- functional/std::bit_xor
- functional/std::cref
- type_traits/std::cref
- functional/std::mem_fn
- functional/std::mem_fun_ref
- functional/std::not1
- functional/std::not2
- functional/std::not_fn
- functional/std::ptr_fun
- functional/std::ref
- functional/std::swap
helpviewer_keywords:
- std::bind [C++]
- std::bind1st
- std::bind2nd
- std::bit_and [C++]
- std::bit_not [C++]
- std::bit_or [C++]
- std::bit_xor [C++]
- std::cref [C++]
ms.assetid: c34d0b45-50a7-447a-9368-2210d06339a4
ms.openlocfilehash: 5e3aa35395c8fd5a42d7127d0b6072a3edf4ace5
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88838088"
---
# <a name="ltfunctionalgt-functions"></a>&lt;functional&gt; 関数

これらの関数は C++ 11 で非推奨とされ、C++ 17 では削除されています。

[bind1st](#bind1st)\
[bind2nd](#bind2nd)\
[mem_fun](#mem_fun)\
[mem_fun_ref](#mem_fun_ref)\
[ptr_fun](#ptr_fun)

これらの関数は C++ 17 では非推奨とされます。

[not1](#not1)\
[not2](#not2)

## <a name="bind"></a><a name="bind"></a> 束縛

呼び出し可能オブジェクトに引数をバインドします。

```cpp
template <class FT, class T1, class T2, ..., class TN>
    unspecified bind(FT fn, T1 t1, T2 t2, ..., TN tN);

template <class RTy, class FT, class T1, class T2, ..., class TN>
    unspecified bind(FT fn, T1 t1, T2 t2, ..., TN tN);
```

### <a name="parameters"></a>パラメーター

*Fey*\
呼び出すオブジェクトの型。

*TN5250*\
N 番目の引数の型。

*1億*\
呼び出すオブジェクト。

*Tn5250*\
N 番目の呼び出しの引数。

### <a name="remarks"></a>解説

型は、 `FT, T1, T2, ..., TN` コピーによって構築可能である必要があり、 `INVOKE(fn, t1, ..., tN)` 一部の値に対して有効な式である必要があり `w1, w2, ..., wN` ます。

1 つ目のテンプレート関数は、転送呼び出しラッパー `g` と弱い結果型を返します。 の効果は `g(u1, u2, ..., uM)` `INVOKE(f, v1, v2, ..., vN,` [invoke_result](../standard-library/invoke-result-class.md)です `<FT cv (V1, V2, ..., VN)>::type)` 。ここで、はの cv 修飾子であり、バインドされる `cv` `g` 引数の値と型は `v1, v2, ..., vN` 以下のように決定されます。 引数を呼び出し可能なオブジェクトにバインドしてカスタマイズされた引数リストを使用する呼び出し可能なオブジェクトを作成するためにそれを使用します。

2 つ目のテンプレート関数は、転送呼び出しラッパー `g` と入れ子になった型 `result_type` を返します。これは `RTy` のシノニムです。 `g(u1, u2, ..., uM)` の効果は `INVOKE(f, v1, v2, ..., vN, RTy)` です。`cv` は、`g` の cv 修飾子であり、バインドされる引数 `v1, v2, ..., vN` の値と型は以下のように決定されます。 引数を呼び出し可能なオブジェクトにバインドしてカスタマイズされた引数リストと指定された戻り値の型を使用する呼び出し可能なオブジェクトを作成しするためにそれを使用します。

バインドされている引数 `v1, v2, ..., vN` の値およびそれらの対応する型 `V1, V2, ..., VN` は、次のように、`bind` の呼び出しの型 `Ti` の対応する引数 `ti`、および呼び出しラッパー `g` の cv 修飾子 `cv` に依存します。

`ti` が型 `reference_wrapper<T>` である場合、引数 `vi` は `ti.get()` であり、型 `Vi` は `T&` です。

の値がの場合、引数はであり、 `std::is_bind_expression<Ti>::value` **`true`** `vi` `ti(u1, u2, ..., uM)` 型 `Vi` はです `result_of<Ti` `cv` `(U1&, U2&, ..., UN&>::type` 。

の値が `j` `std::is_placeholder<Ti>::value` 0 でない場合、引数はで、 `vi` `uj` 型 `Vi` はです `Uj&` 。

それ以外の場合、引数 `vi` は `ti` で、型 `Vi` は `Ti` `cv` `&` です。

たとえば、関数 `f(int, int)` を指定した場合、式 `bind(f, _1, 0)` は、`cw(x)` が `f(x, 0)` を呼び出すように、転送呼び出しラッパー `cw` を返します。 式 `bind(f, 0, _1)` は、`cw(x)` が `f(0, x)` を呼び出すように、転送呼び出しラッパー `cw` を返します。

の呼び出しの引数の数 `bind` と引数は、 `fn` 呼び出し可能オブジェクトに渡すことができる引数の数と同じである必要があり `fn` ます。 たとえば、 `bind(cos, 1.0)` が正しく、との両方 `bind(cos)` `bind(cos, _1, 0.0)` が正しくありません。

`bind` によって返される呼出ラッパーに対する関数呼び出し内の引数の数は、`bind` に対する呼び出し内のすべてのプレースホルダー引数の `is_placeholder<PH>::value` の最高の数値以上になっている必要があります。 たとえば、 `bind(cos, _2)(0.0, 1.0)` は正しい (とを返し `cos(1.0)` ます)、 `bind(cos, _2)(0.0)` は正しくありません。

### <a name="example"></a>例

```cpp
// std__functional__bind.cpp
// compile with: /EHsc
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std::placeholders;

void square(double x)
{
    std::cout << x << "^2 == " << x * x << std::endl;
}

void product(double x, double y)
{
    std::cout << x << "*" << y << " == " << x * y << std::endl;
}

int main()
{
    double arg[] = { 1, 2, 3 };

    std::for_each(&arg[0], arg + 3, square);
    std::cout << std::endl;

    std::for_each(&arg[0], arg + 3, std::bind(product, _1, 2));
    std::cout << std::endl;

    std::for_each(&arg[0], arg + 3, std::bind(square, _1));

    return (0);
}
```

```Output
1^2 == 1
2^2 == 4
3^2 == 9

1*2 == 2
2*2 == 4
3*2 == 6

1^2 == 1
2^2 == 4
3^2 == 9
```

## <a name="bind1st"></a><a name="bind1st"></a> bind1st

二項関数オブジェクトを単項関数オブジェクトに変換するアダプターを作成するヘルパーテンプレート関数。 このメソッドは、二項関数の最初の引数を指定された値にバインドします。 C++ 11 では非推奨となりました。 C++ 17 では削除されています。

```cpp
template <class Operation, class Type>
    binder1st <Operation> bind1st (const Operation& func, const Type& left);
```

### <a name="parameters"></a>パラメーター

*func*\
単項関数オブジェクトに変換する二項関数オブジェクト。

*左側*\
二項関数オブジェクトの最初の引数がバインドされている値。

### <a name="return-value"></a>戻り値

二項関数オブジェクトの最初の引数を *左*の値にバインドした結果として生成される単項関数オブジェクト。

### <a name="remarks"></a>解説

関数バインダーは、関数アダプターの一種です。 関数オブジェクトを返すため、特定の型の関数構成で使用して、より複雑で強力な式を作成できます。

*Func*が型のオブジェクトで、 `Operation` `c` が定数である場合、 `bind1st( func, c )` は[binder1st](../standard-library/binder1st-class.md)クラスコンストラクターと同じであり、を `binder1st<Operation>(func, c)` 使用すると便利です。

### <a name="example"></a>例

```cpp
// functional_bind1st.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

// Creation of a user-defined function object
// that inherits from the unary_function base class
class greaterthan5: unary_function<int, bool>
{
public:
    result_type operator()(argument_type i)
    {
        return (result_type)(i > 5);
    }
};

int main()
{
    vector<int> v1;
    vector<int>::iterator Iter;

    int i;
    for (i = 0; i <= 5; i++)
    {
        v1.push_back(5 * i);
    }

    cout << "The vector v1 = ( " ;
    for (Iter = v1.begin(); Iter != v1.end(); Iter++)
        cout << *Iter << " ";
    cout << ")" << endl;

    // Count the number of integers > 10 in the vector
    vector<int>::iterator::difference_type result1a;
    result1a = count_if(v1.begin(), v1.end(), bind1st(less<int>(), 10));
    cout << "The number of elements in v1 greater than 10 is: "
         << result1a << "." << endl;

    // Compare: counting the number of integers > 5 in the vector
    // with a user defined function object
    vector<int>::iterator::difference_type result1b;
    result1b = count_if(v1.begin(), v1.end(), greaterthan5());
    cout << "The number of elements in v1 greater than 5 is: "
         << result1b << "." << endl;

    // Count the number of integers < 10 in the vector
    vector<int>::iterator::difference_type result2;
    result2 = count_if(v1.begin(), v1.end(), bind2nd(less<int>(), 10));
    cout << "The number of elements in v1 less than 10 is: "
         << result2 << "." << endl;
}
```

```Output
The vector v1 = ( 0 5 10 15 20 25 )
The number of elements in v1 greater than 10 is: 3.
The number of elements in v1 greater than 5 is: 4.
The number of elements in v1 less than 10 is: 2.
```

## <a name="bind2nd"></a><a name="bind2nd"></a> bind2nd

二項関数オブジェクトを単項関数オブジェクトに変換するアダプターを作成するヘルパーテンプレート関数。 二項関数の2番目の引数を指定された値にバインドします。 C++ 11 では非推奨となりました。 C++ 17 では削除されています。

```cpp
template <class Operation, class Type>
    binder2nd <Operation> bind2nd(const Operation& func, const Type& right);
```

### <a name="parameters"></a>パラメーター

*func*\
単項関数オブジェクトに変換する二項関数オブジェクト。

*そうです*\
二項関数オブジェクトの 2 つ目の引数がバインドされている値。

### <a name="return-value"></a>戻り値

二項関数オブジェクトの2番目の引数を *right*にバインドした単項関数オブジェクトの結果。

### <a name="remarks"></a>解説

関数バインダーは、関数アダプターの一種です。 関数オブジェクトを返すため、特定の型の関数構成で使用して、より複雑で強力な式を作成できます。

*Func*が型のオブジェクトで、 `Operation` `c` が定数である場合、 `bind2nd(func, c)` は[binder2nd](../standard-library/binder2nd-class.md)クラスコンストラクターと同じであり、を `binder2nd<Operation>(func, c)` 使用すると便利です。

### <a name="example"></a>例

```cpp
// functional_bind2nd.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

// Creation of a user-defined function object
// that inherits from the unary_function base class
class greaterthan15: unary_function<int, bool>
{
public:
    result_type operator()(argument_type i)
    {
        return (result_type)(i > 15);
    }
};

int main()
{
    vector<int> v1;
    vector<int>::iterator Iter;

    int i;
    for (i = 0; i <= 5; i++)
    {
        v1.push_back(5 * i);
    }

    cout << "The vector v1 = ( ";
    for (Iter = v1.begin(); Iter != v1.end(); Iter++)
        cout << *Iter << " ";
    cout << ")" << endl;

    // Count the number of integers > 10 in the vector
    vector<int>::iterator::difference_type result1a;
    result1a = count_if(v1.begin(), v1.end(), bind2nd(greater<int>(), 10));
    cout << "The number of elements in v1 greater than 10 is: "
         << result1a << "." << endl;

    // Compare counting the number of integers > 15 in the vector
    // with a user-defined function object
    vector<int>::iterator::difference_type result1b;
    result1b = count_if(v1.begin(), v1.end(), greaterthan15());
    cout << "The number of elements in v1 greater than 15 is: "
         << result1b << "." << endl;

    // Count the number of integers < 10 in the vector
    vector<int>::iterator::difference_type result2;
    result2 = count_if(v1.begin(), v1.end(), bind1st(greater<int>(), 10));
    cout << "The number of elements in v1 less than 10 is: "
         << result2 << "." << endl;
}
```

```Output
The vector v1 = ( 0 5 10 15 20 25 )
The number of elements in v1 greater than 10 is: 3.
The number of elements in v1 greater than 15 is: 2.
The number of elements in v1 less than 10 is: 2.
```

## <a name="bit_and"></a><a name="bit_and"></a> bit_and

引数に対してビットごとの AND 演算 (二項) を実行する定義済みの関数オブジェクト `operator&` 。

```cpp
template <class Type = void>
struct bit_and : public binary_function<Type, Type, Type> {
    Type operator()(
    const Type& Left,
    const Type& Right) const;
};

// specialized transparent functor for operator&
template <>
struct bit_and<void>
{
    template <class T, class U>
    auto operator()(T&& Left, U&& Right) const  ->
        decltype(std::forward<T>(Left) & std::forward<U>(Right));
};
```

### <a name="parameters"></a>パラメーター

*型*、 *T*、 *U*\
指定または推論された型のオペランドを受け取る `operator&` をサポートする任意の型。

*左側*\
ビットごとの AND 演算の左オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *T*の左辺値および右辺値参照引数の完全転送を行います。

*そうです*\
ビットごとの AND 演算の右オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *U*の左辺値および右辺値参照引数の完全転送を行います。

### <a name="return-value"></a>戻り値

`Left & Right` の結果。 特殊化されたテンプレートは、結果の完全転送を行います。結果には `operator&` によって返された型が含まれます。

### <a name="remarks"></a>解説

`bit_and` ファンクターは、基本データ型の整数型、または二項 `operator&` を実装しているユーザー定義型に制限されます。

## <a name="bit_not"></a><a name="bit_not"></a> bit_not

引数に対してビットごとの補数 (NOT) 演算 (単項) を実行する定義済みの関数オブジェクト `operator~` 。 C++ 14 で追加されました。

```cpp
template <class Type = void>
struct bit_not : public unary_function<Type, Type>
{
    Type operator()(const Type& Right) const;
};

// specialized transparent functor for operator~
template <>
struct bit_not<void>
{
    template <class Type>
    auto operator()(Type&& Right) const -> decltype(~std::forward<Type>(Right));
};
```

### <a name="parameters"></a>パラメーター

*各種*\
単項 `operator~` をサポートする型。

*そうです*\
ビットごとの補数演算の右オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型の *型*の左辺値または右辺値参照引数の完全転送を行います。

### <a name="return-value"></a>戻り値

`~ Right` の結果。 特殊化されたテンプレートは、結果の完全転送を行います。結果には `operator~` によって返された型が含まれます。

### <a name="remarks"></a>解説

`bit_not` ファンクターは、基本データ型の整数型、または二項 `operator~` を実装しているユーザー定義型に制限されます。

## <a name="bit_or"></a><a name="bit_or"></a> bit_or

引数に対してビットごとの OR 演算 () を実行する定義済みの関数オブジェクト `operator|` 。

```cpp
template <class Type = void>
struct bit_or : public binary_function<Type, Type, Type> {
    Type operator()(
    const Type& Left,
    const Type& Right) const;
};

// specialized transparent functor for operator|
template <>
struct bit_or<void>
{
    template <class T, class U>
    auto operator()(T&& Left, U&& Right) const
        -> decltype(std::forward<T>(Left) | std::forward<U>(Right));
};
```

### <a name="parameters"></a>パラメーター

*型*、 *T*、 *U*\
指定または推論された型のオペランドを受け取る `operator|` をサポートする任意の型。

*左側*\
ビットごとの OR 演算の左オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *T*の左辺値および右辺値参照引数の完全転送を行います。

*そうです*\
ビットごとの OR 演算の右オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *U*の左辺値および右辺値参照引数の完全転送を行います。

### <a name="return-value"></a>戻り値

`Left | Right` の結果。 特殊化されたテンプレートは、結果の完全転送を行います。結果には `operator|` によって返された型が含まれます。

### <a name="remarks"></a>解説

`bit_or` ファンクターは、基本データ型の整数型、または `operator|` を実装しているユーザー定義型に制限されます。

## <a name="bit_xor"></a><a name="bit_xor"></a> bit_xor

引数に対してビットごとの XOR 演算 (二項) を実行する定義済みの関数オブジェクト `operator^` 。

```cpp
template <class Type = void>
struct bit_xor : public binary_function<Type, Type, Type> {
    Type operator()(
    const Type& Left,
    const Type& Right) const;
};

// specialized transparent functor for operator^
template <>
struct bit_xor<void>
{
    template <class T, class U>
    auto operator()(T&& Left, U&& Right) const
        -> decltype(std::forward<T>(Left) ^ std::forward<U>(Right));
};
```

### <a name="parameters"></a>パラメーター

*型*、 *T*、 *U*\
指定または推論された型のオペランドを受け取る `operator^` をサポートする任意の型。

*左側*\
ビットごとの XOR 演算の左オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *T*の左辺値および右辺値参照引数の完全転送を行います。

*そうです*\
ビットごとの XOR 演算の右オペランド。 非特殊テンプレートは、type *型*の左辺値参照引数を受け取ります。 特殊化されたテンプレートは、推論された型 *U*の左辺値および右辺値参照引数の完全転送を行います。

### <a name="return-value"></a>戻り値

`Left ^ Right` の結果。 特殊化されたテンプレートは、結果の完全転送を行います。結果には `operator^` によって返された型が含まれます。

### <a name="remarks"></a>解説

`bit_xor` ファンクターは、基本データ型の整数型、または二項 `operator^` を実装しているユーザー定義型に制限されます。

## <a name="cref"></a><a name="cref"></a> cref

引数から const の `reference_wrapper` を構築します。

```cpp
template <class Ty>
reference_wrapper<const Ty> cref(const Ty& arg);

template <class Ty>
reference_wrapper<const Ty> cref(const reference_wrapper<Ty>& arg);
```

### <a name="parameters"></a>パラメーター

*~*\
ラップする引数の型。

*arg*\
ラップする引数。

### <a name="remarks"></a>解説

最初の関数は `reference_wrapper<const Ty>(arg.get())` を返します。 定数参照をラップするために使用します。 2 番目の関数は `reference_wrapper<const Ty>(arg)` を返します。 ラップされた参照を定数参照として再ラップするために使用します。

### <a name="example"></a>例

```cpp
// std__functional__cref.cpp
// compile with: /EHsc
#include <functional>
#include <iostream>

int neg(int val)
    {
    return (-val);
    }

int main()
    {
    int i = 1;

    std::cout << "i = " << i << std::endl;
    std::cout << "cref(i) = " << std::cref(i) << std::endl;
    std::cout << "cref(neg)(i) = "
        << std::cref(&neg)(i) << std::endl;

    return (0);
    }
```

```Output
i = 1
cref(i) = 1
cref(neg)(i) = -1
```

## <a name="invoke"></a><a name="invoke"></a> スタンド

指定された引数を使用して、呼び出し可能なオブジェクトを呼び出します。 C++ 17 で追加されました。

```cpp
template <class Callable, class... Args>
invoke_result_t<Callable, Args...>
    invoke(Callable&& fn, Args&&... args) noexcept(/* specification */);
```

### <a name="parameters"></a>パラメーター

*呼び出し可能*\
呼び出すオブジェクトの型。

*Value*\
呼び出し引数の型。

*1億*\
呼び出すオブジェクト。

*value*\
呼び出しの引数。

*スペシフィケーション*\
**`noexcept`** 仕様 `std::is_nothrow_invocable_v<Callable, Args>)` 。

### <a name="remarks"></a>解説

パラメーター*引数*を使用して、呼び出し可能オブジェクト*fn*を呼び出します。 実際には、 `INVOKE(std::forward<Callable>(fn), std::forward<Args>(args)...)` 擬似関数は `INVOKE(f, t1, t2, ..., tN)` 次のいずれかを意味します。

- `(t1.*f)(t2, ..., tN)`。`f` がクラス `T` のメンバー関数へのポインターであり、`t1` が型 `T` のオブジェクト、型 `T` のオブジェクトへの参照、`T` から派生した型のオブジェクトへの参照のいずれかである場合。 つまり、 `std::is_base_of<T, std::decay_t<decltype(t1)>>::value` が true の場合。

- `(t1.get().*f)(t2, ..., tN)``f`がクラスのメンバー関数へのポインターで `T` あり、が特殊化されている場合 `std::decay_t<decltype(t1)>` `std::reference_wrapper` 。

- `((*t1).*f)(t2, ..., tN)``f`がクラスのメンバー関数へのポインターで `T` `t1` あり、以前の型の1つではない場合。

- `t1.*f`。N == 1 で、`f` がクラス `T` のメンバー データへのポインターであり、`t1` が型 `T` のオブジェクト、型 `T` のオブジェクトへの参照、`T` から派生した型のオブジェクトへの参照のいずれかである場合。  つまり、 `std::is_base_of<T, std::decay_t<decltype(t1)>>::value` が true の場合。

- `t1.get().*f` N = = 1 で、 `f` がクラスのメンバーデータへのポインターで `T` あり、が特殊化されている場合 `std::decay_t<decltype(t1)>` `std::reference_wrapper` 。

- `(*t1).*f` N = = 1 で、 `f` がクラスのメンバーデータへのポインターで `T` `t1` あり、以前の型の1つではない場合。

- 他のすべての場合は `f(t1, t2, ..., tN)`。

呼び出し可能オブジェクトの結果の型の詳細については、「 [invoke_result](invoke-result-class.md)」を参照してください。 呼び出し可能な型の述語については、「 [is_invocable、is_invocable_r、is_nothrow_invocable、is_nothrow_invocable_r クラス](is-invocable-classes.md)」を参照してください。

### <a name="example"></a>例

```cpp
// functional_invoke.cpp
// compile using: cl /EHsc /std:c++17 functional_invoke.cpp
#include <functional>
#include <iostream>

struct Demo
{
    int n_;

    Demo(int const n) : n_{n} {}

    void operator()( int const i, int const j ) const
    {
        std::cout << "Demo operator( " << i << ", "
            << j << " ) is " << i * j << "\n";
    }

    void difference( int const i ) const
    {
        std::cout << "Demo.difference( " << i << " ) is "
            << n_ - i << "\n";
    }
};

void divisible_by_3(int const i)
{
    std::cout << i << ( i % 3 == 0 ? " is" : " isn't" )
        << " divisible by 3.\n";
}

int main()
{
    Demo d{ 42 };
    Demo * pd{ &d };
    auto pmf = &Demo::difference;
    auto pmd = &Demo::n_;

    // Invoke a function object, like calling d( 3, -7 )
    std::invoke( d, 3, -7 );

    // Invoke a member function, like calling
    // d.difference( 29 ) or (d.*pmf)( 29 )
    std::invoke( &Demo::difference, d, 29 );
    std::invoke( pmf, pd, 13 );

    // Invoke a data member, like access to d.n_ or d.*pmd
    std::cout << "d.n_: " << std::invoke( &Demo::n_, d ) << "\n";
    std::cout << "pd->n_: " << std::invoke( pmd, pd ) << "\n";

    // Invoke a stand-alone (free) function
    std::invoke( divisible_by_3, 42 );

    // Invoke a lambda
    auto divisible_by_7 = []( int const i ) {
        std::cout << i << ( i % 7 == 0 ? " is" : " isn't" )
            << " divisible by 7.\n";
        };
    std::invoke( divisible_by_7, 42 );
}
```

```Output
Demo operator( 3, -7 ) is -21
Demo.difference( 29 ) is 13
Demo.difference( 13 ) is 29
d.n_: 42
pd->n_: 42
42 is divisible by 3.
42 is divisible by 7.
```

## <a name="mem_fn"></a><a name="mem_fn"></a> mem_fn

単純な呼び出しラッパーを生成します。

```cpp
template <class RTy, class Ty>
unspecified mem_fn(RTy Ty::*pm);
```

### <a name="parameters"></a>パラメーター

*なり*\
ラップされた関数の戻り値の型。

*~*\
メンバー関数ポインターの型。

### <a name="remarks"></a>解説

このテンプレート関数は、 `cw` 式がと同じになるように、弱い結果型を持つ単純な呼び出しラッパーを返し `cw(t, a2, ..., aN)` `INVOKE(pm, t, a2, ..., aN)` ます。 例外はスローされません。

返された呼び出しラッパーは、 `std::unary_function<cv Ty*, RTy>` `result_type` *RTy* `argument_type` `cv Ty*` 型*Ty*が引数を取らない cv 修飾子を持つメンバー関数へのポインターである場合にのみ、から派生します (入れ子にされた型を rty のシノニムとして、入れ子にされた型をのシノニムとして定義し `cv` ます)。

返された呼び出しラッパーは、型 `std::binary_function<cv Ty*, T2, RTy>` `result_type` *RTy* `first argument_type` `cv Ty*` `second argument_type` `T2` *Ty* `cv` の引数を受け取る cv 修飾子を持つメンバー関数へのポインター `T2` である場合にのみ、(または、入れ子にされた型をのシノニムとして、入れ子にされた型をのシノニムとして定義する) に対してのみ派生します。

### <a name="example"></a>例

```cpp
// std__functional__mem_fn.cpp
// compile with: /EHsc
#include <functional>
#include <iostream>

class Funs
    {
public:
    void square(double x)
        {
        std::cout << x << "^2 == " << x * x << std::endl;
        }

    void product(double x, double y)
        {
        std::cout << x << "*" << y << " == " << x * y << std::endl;
        }
    };

int main()
    {
    Funs funs;

    std::mem_fn(&Funs::square)(funs, 3.0);
    std::mem_fn(&Funs::product)(funs, 3.0, 2.0);

    return (0);
    }
```

```Output
3^2 == 9
3*2 == 6
```

## <a name="mem_fun"></a><a name="mem_fun"></a> mem_fun

ポインター引数による初期化を行うときに、メンバー関数の関数オブジェクト アダプターを作成するために使用されるヘルパー テンプレート関数。 C++ 11 で [mem_fn](#mem_fn) および [バインド](#bind)用に非推奨となり、c++ 17 で削除されました。

```cpp
template <class Result, class Type>
mem_fun_t<Result, Type> mem_fun (Result(Type::* pMem)());

template <class Result, class Type, class Arg>
mem_fun1_t<Result, Type, Arg> mem_fun(Result (Type::* pMem)(Arg));

template <class Result, class Type>
const_mem_fun_t<Result, Type> mem_fun(Result (Type::* pMem)() const);

template <class Result, class Type, class Arg>
const_mem_fun1_t<Result, Type, Arg> mem_fun(Result (Type::* pMem)(Arg) const);
```

### <a name="parameters"></a>パラメーター

*pMem*\
関数オブジェクトに変換されるクラス `Type` のメンバー関数へのポインター。

### <a name="return-value"></a>戻り値

また **`const`** は **non_const** 型または型の関数オブジェクト `mem_fun_t` `mem_fun1_t` 。

### <a name="example"></a>例

```cpp
// functional_mem_fun.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

class StoreVals
{
    int val;
public:
    StoreVals() { val = 0; }
    StoreVals(int j) { val = j; }

    bool display() { cout << val << " "; return true; }
    int squareval() { val *= val; return val; }
    int lessconst(int k) {val -= k; return val; }
};

int main( )
{
    vector<StoreVals *> v1;

    StoreVals sv1(5);
    v1.push_back(&sv1);
    StoreVals sv2(10);
    v1.push_back(&sv2);
    StoreVals sv3(15);
    v1.push_back(&sv3);
    StoreVals sv4(20);
    v1.push_back(&sv4);
    StoreVals sv5(25);
    v1.push_back(&sv5);

    cout << "The original values stored are: " ;
    for_each(v1.begin(), v1.end(), mem_fun<bool, StoreVals>(&StoreVals::display));
    cout << endl;

    // Use of mem_fun calling member function through a pointer
    // square each value in the vector using squareval ()
    for_each(v1.begin(), v1.end(), mem_fun<int, StoreVals>(&StoreVals::squareval));
    cout << "The squared values are: " ;
    for_each(v1.begin(), v1.end(), mem_fun<bool, StoreVals>(&StoreVals::display));
    cout << endl;

    // Use of mem_fun1 calling member function through a pointer
    // subtract 5 from each value in the vector using lessconst ()
    for_each(v1.begin(), v1.end(),
        bind2nd (mem_fun1<int, StoreVals,int>(&StoreVals::lessconst), 5));
    cout << "The squared values less 5 are: " ;
    for_each(v1.begin(), v1.end(), mem_fun<bool, StoreVals>(&StoreVals::display));
    cout << endl;
}
```

## <a name="mem_fun_ref"></a><a name="mem_fun_ref"></a> mem_fun_ref

参照引数を使用して初期化を行うときに、メンバー関数の関数オブジェクト アダプターを作成するために使用されるヘルパー テンプレート関数。 C++ 11 では非推奨となりました。 C++ 17 では削除されています。

```cpp
template <class Result, class Type>
mem_fun_ref_t<Result, Type> mem_fun_ref(Result (Type::* pMem)());

template <class Result, class Type, class Arg>
mem_fun1_ref_t<Result, Type, Arg> mem_fun_ref(Result (Type::* pMem)(Arg));

template <class Result, class Type>
const_mem_fun_ref_t<Result, Type> mem_fun_ref(Result Type::* pMem)() const);

template <class Result, class Type, class Arg>
const_mem_fun1_ref_t<Result, Type, Arg> mem_fun_ref(Result (T::* pMem)(Arg) const);
```

### <a name="parameters"></a>パラメーター

*pMem*\
関数オブジェクトに変換されるクラス `Type` のメンバー関数へのポインター。

### <a name="return-value"></a>戻り値

**`const`** `non_const` 型または型の関数 `mem_fun_ref_t` オブジェクト `mem_fun1_ref_t` 。

### <a name="example"></a>例

```cpp
// functional_mem_fun_ref.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

class NumVals
   {
   int val;
   public:
   NumVals ( ) { val = 0; }
   NumVals ( int j ) { val = j; }

   bool display ( ) { cout << val << " "; return true; }
   bool isEven ( ) { return ( bool )  !( val %2 ); }
   bool isPrime( )
   {
      if (val < 2) { return true; }
      for (int i = 2; i <= val / i; ++i)
      {
         if (val % i == 0) { return false; }
      }
      return true;
   }
};

int main( )
{
   vector <NumVals> v1 ( 13 ), v2 ( 13 );
   vector <NumVals>::iterator v1_Iter, v2_Iter;
   int i, k;

   for ( i = 0; i < 13; i++ ) v1 [ i ] = NumVals ( i+1 );
   for ( k = 0; k < 13; k++ ) v2 [ k ] = NumVals ( k+1 );

   cout << "The original values stored in v1 are: " ;
   for_each( v1.begin( ), v1.end( ),
   mem_fun_ref ( &NumVals::display ) );
   cout << endl;

   // Use of mem_fun_ref calling member function through a reference
   // remove the primes in the vector using isPrime ( )
   v1_Iter = remove_if ( v1.begin( ),  v1.end( ),
      mem_fun_ref ( &NumVals::isPrime ) );
   cout << "With the primes removed, the remaining values in v1 are: " ;
   for_each( v1.begin( ), v1_Iter,
   mem_fun_ref ( &NumVals::display ) );
   cout << endl;

   cout << "The original values stored in v2 are: " ;
   for_each( v2.begin( ), v2.end( ),
   mem_fun_ref ( &NumVals::display ) );
   cout << endl;

   // Use of mem_fun_ref calling member function through a reference
   // remove the even numbers in the vector v2 using isEven ( )
   v2_Iter = remove_if ( v2.begin( ),  v2.end( ),
      mem_fun_ref ( &NumVals::isEven ) );
   cout << "With the even numbers removed, the remaining values are: " ;
   for_each( v2.begin( ),  v2_Iter,
   mem_fun_ref ( &NumVals::display ) );
   cout << endl;
}
```

```Output
The original values stored in v1 are: 1 2 3 4 5 6 7 8 9 10 11 12 13
With the primes removed, the remaining values in v1 are: 4 6 8 9 10 12
The original values stored in v2 are: 1 2 3 4 5 6 7 8 9 10 11 12 13
With the even numbers removed, the remaining values are: 1 3 5 7 9 11 13
```

## <a name="not1"></a><a name="not1"></a> not1

単項述語の補数を返します。 C++ 17 の [not_fn](#not_fn) では非推奨とされます。

```cpp
template <class UnaryPredicate>
unary_negate<UnaryPredicate> not1(const UnaryPredicate& predicate);
```

### <a name="parameters"></a>パラメーター

*述語*\
符号が反転される単項述語。

### <a name="return-value"></a>戻り値

変更される単項述語の否定である単項述語。

### <a name="remarks"></a>解説

`unary_negate`が単項述語から構築されている場合は、 `predicate(x)` を返し `!predicate(x)` ます。

### <a name="example"></a>例

```cpp
// functional_not1.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

int main()
{
    vector<int> v1;
    vector<int>::iterator Iter;

    int i;
    for (i = 0; i <= 7; i++)
    {
        v1.push_back(5 * i);
    }

    cout << "The vector v1 = ( ";
    for (Iter = v1.begin(); Iter != v1.end(); Iter++)
        cout << *Iter << " ";
    cout << ")" << endl;

    vector<int>::iterator::difference_type result1;
    // Count the elements greater than 10
    result1 = count_if(v1.begin(), v1.end(), bind2nd(greater<int>(), 10));
    cout << "The number of elements in v1 greater than 10 is: "
         << result1 << "." << endl;

    vector<int>::iterator::difference_type result2;
    // Use the negator to count the elements less than or equal to 10
    result2 = count_if(v1.begin(), v1.end(),
        not1(bind2nd(greater<int>(), 10)));

    cout << "The number of elements in v1 not greater than 10 is: "
         << result2 << "." << endl;
}
```

```Output
The vector v1 = ( 0 5 10 15 20 25 30 35 )
The number of elements in v1 greater than 10 is: 5.
The number of elements in v1 not greater than 10 is: 3.
```

## <a name="not2"></a><a name="not2"></a> not2

二項述語の補数を返します。 C++ 17 の [not_fn](#not_fn) では非推奨とされます。

```cpp
template <class BinaryPredicate>
binary_negate<BinaryPredicate> not2(const BinaryPredicate& func);
```

### <a name="parameters"></a>パラメーター

*func*\
符号が反転される二項述語。

### <a name="return-value"></a>戻り値

変更される二項述語の否定である二項述語。

### <a name="remarks"></a>解説

`binary_negate`が二項述語から構築されている場合は、 `binary_predicate(x, y)` を返し `!binary_predicate(x, y)` ます。

### <a name="example"></a>例

```cpp
// functional_not2.cpp
// compile with: /EHsc
#include <vector>
#include <algorithm>
#include <functional>
#include <cstdlib>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator Iter1;

   int i;
   v1.push_back( 6262 );
   v1.push_back( 6262 );
   for ( i = 0 ; i < 5 ; i++ )
   {
      v1.push_back( rand( ) );
   }

   cout << "Original vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   // To sort in ascending order,
   // use default binary predicate less<int>( )
   sort( v1.begin( ), v1.end( ) );
   cout << "Sorted vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   // To sort in descending order,
   // use the binary_negate helper function not2
   sort( v1.begin( ), v1.end( ), not2(less<int>( ) ) );
   cout << "Resorted vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;
}
```

```Output
Original vector v1 = ( 6262 6262 41 18467 6334 26500 19169 )
Sorted vector v1 = ( 41 6262 6262 6334 18467 19169 26500 )
Resorted vector v1 = ( 26500 19169 18467 6334 6262 6262 41 )
```

## <a name="not_fn"></a><a name="not_fn"></a> not_fn

`not_fn`関数テンプレートは、呼び出し可能オブジェクトを受け取り、呼び出し可能オブジェクトを返します。 返された呼び出し可能オブジェクトは、後でいくつかの引数を使用して呼び出されると、元の呼び出し可能オブジェクトに渡され、結果は論理的に否定されます。 このメソッドは、ラップされた呼び出し可能オブジェクトの const 修飾子と値カテゴリの動作を保持します。 `not_fn` は c++ 17 で新しく追加されたもので、非推奨の、 `std::not1` `std::not2` 、 `std::unary_negate` 、およびを置き換え `std::binary_negate` ます。

```cpp
template <class Callable>
/* unspecified */ not_fn(Callable&& func);
```

### <a name="parameters"></a>パラメーター

*func*\
転送呼び出しラッパーを構築するために使用される呼び出し可能オブジェクト。

### <a name="remarks"></a>解説

このテンプレート関数は `return call_wrapper(std::forward<Callable>(func))` 、この exposition のみのクラスに基づいて、のような呼び出しラッパーを返します。

```cpp
class call_wrapper
{
   using FD = decay_t<Callable>;
   explicit call_wrapper(Callable&& func);

public:
   call_wrapper(call_wrapper&&) = default;
   call_wrapper(call_wrapper const&) = default;

   template<class... Args>
     auto operator()(Args&&...) & -> decltype(!declval<invoke_result_t<FD&(Args...)>>());

   template<class... Args>
     auto operator()(Args&&...) const& -> decltype(!declval<invoke_result_t<FD const&(Args...)>>());

   template<class... Args>
     auto operator()(Args&&...) && -> decltype(!declval<invoke_result_t<FD(Args...)>>());

   template<class... Args>
     auto operator()(Args&&...) const&& -> decltype(!declval<invoke_result_t<FD const(Args...)>>());

private:
  FD fd;
};
```

呼び出し可能オブジェクトの *func* の明示的なコンストラクターは、 `std::decay_t<Callable>` の要件を満たす型を必要 `MoveConstructible` とし、 `is_constructible_v<FD, Callable>` true である必要があります。 このメソッドは、ラップされた呼び出し可能オブジェクトを `fd` から初期化 `std::forward<Callable>(func)` し、の構築によってスローされた例外をスローし `fd` ます。

ラッパーは、次に示すように、左辺値または右辺値参照カテゴリおよび const 修飾子によって識別される呼び出し演算子を公開します。

```cpp
template<class... Args> auto operator()(Args&&... args) & -> decltype(!declval<invoke_result_t<FD&(Args...)>>());
template<class... Args> auto operator()(Args&&... args) const& -> decltype(!declval<invoke_result_t<FD const&(Args...)>>());
template<class... Args> auto operator()(Args&&... args) && -> decltype(!declval<invoke_result_t<FD(Args...)>>());
template<class... Args> auto operator()(Args&&... args) const&& -> decltype(!declval<invoke_result_t<FD const(Args...)>>());
```

最初の2つは、と同じ `return !std::invoke(fd, std::forward<Args>(args)...)` です。 2つ目はと同じ `return !std::invoke(std::move(fd), std::forward<Args>(args)...)` です。

### <a name="example"></a>例

```cpp
// functional_not_fn_.cpp
// compile with: /EHsc /std:c++17
#include <vector>
#include <algorithm>
#include <functional>
#include <iostream>

int main()
{
    std::vector<int> v1 = { 99, 6264, 41, 18467, 6334, 26500, 19169 };
    auto divisible_by_3 = [](int i){ return i % 3 == 0; };

    std::cout << "Vector v1 = ( " ;
    for (const auto& item : v1)
    {
        std::cout << item << " ";
    }
    std::cout << ")" << std::endl;

    // Count the number of vector elements divisible by 3.
    int divisible =
        std::count_if(v1.begin(), v1.end(), divisible_by_3);
    std::cout << "Elements divisible by three: "
        << divisible << std::endl;

    // Count the number of vector elements not divisible by 3.
    int not_divisible =
        std::count_if(v1.begin(), v1.end(), std::not_fn(divisible_by_3));
    std::cout << "Elements not divisible by three: "
        << not_divisible << std::endl;
}
```

```Output
Vector v1 = ( 99 6264 41 18467 6334 26500 19169 )
Elements divisible by three: 2
Elements not divisible by three: 5
```

## <a name="ptr_fun"></a><a name="ptr_fun"></a> ptr_fun

単項関数ポインターと二項関数ポインターをそれぞれ適応性のある単項関数および二項関数に変換するために使用されるヘルパー テンプレート関数。 C++ 11 では非推奨となりました。 C++ 17 では削除されています。

```cpp
template <class Arg, class Result>
pointer_to_unary_function<Arg, Result, Result (*)(Arg)> ptr_fun(Result (*pfunc)(Arg));

template <class Arg1, class Arg2, class Result>
pointer_to_binary_function<Arg1, Arg2, Result, Result (*)(Arg1, Arg2)> ptr_fun(Result (*pfunc)(Arg1, Arg2));
```

### <a name="parameters"></a>パラメーター

*pfunc*\
アダプター関数に変換される単項関数ポインターまたは二項関数ポインター。

### <a name="return-value"></a>戻り値

1つ目のテンプレート関数は、単項関数[pointer_to_unary_function](../standard-library/pointer-to-unary-function-class.md)  < `Arg` 、 **Result**> () を返し \* `pfunc` ます。

2番目のテンプレート関数は、バイナリ関数 [pointer_to_binary_function](../standard-library/pointer-to-binary-function-class.md) \<**Arg1**, **Arg2**, **Result**> () を返し \* `pfunc` ます。

### <a name="remarks"></a>解説

関数ポインターは関数オブジェクトです。 パラメーターとして関数を想定している任意のアルゴリズムに渡すことができますが、適応性はありません。 その入れ子になった型に関する情報は、アダプターと共に使用するために必要です。たとえば、値をバインドしたり、それを否定したりすることができます。 `ptr_fun` ヘルパー関数による単項関数ポインターと二項関数ポインターの変換では、関数アダプターと共に単項関数ポインターおよび二項関数ポインターを使用できます。

### <a name="example"></a>例

[!code-cpp[functional_ptr_fun#1](../standard-library/codesnippet/CPP/functional-functions_1.cpp)]

## <a name="ref"></a><a name="ref"></a> リファレンス

引数から `reference_wrapper` を構築します。

```cpp
template <class Ty>
    reference_wrapper<Ty> ref(Ty& arg);

template <class Ty>
    reference_wrapper<Ty> ref(reference_wrapper<Ty>& arg);
```

### <a name="return-value"></a>戻り値

`arg`への参照。具体的には、 `reference_wrapper<Ty>(arg)`。

### <a name="example"></a>例

次の例では、2 つの関数を定義します。1 つは文字列変数にバインドされます。もう 1 つは、 `ref`の呼び出しによって計算された文字列変数の参照にバインドされます。 変数の値が変わると、1 つ目の関数では元の値が使用され続けますが、2 つ目の関数では新しい値が使用されます。

```cpp
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <ostream>
#include <string>
#include <vector>
using namespace std;
using namespace std;
using namespace std::placeholders;

bool shorter_than(const string& l, const string& r) {
    return l.size() < r.size();
}

int main() {
    vector<string> v_original;
    v_original.push_back("tiger");
    v_original.push_back("cat");
    v_original.push_back("lion");
    v_original.push_back("cougar");

    copy(v_original.begin(), v_original.end(), ostream_iterator<string>(cout, " "));
    cout << endl;

    string s("meow");

    function<bool (const string&)> f = bind(shorter_than, _1, s);
    function<bool (const string&)> f_ref = bind(shorter_than, _1, ref(s));

    vector<string> v;

    // Remove elements that are shorter than s ("meow")

    v = v_original;
    v.erase(remove_if(v.begin(), v.end(), f), v.end());

    copy(v.begin(), v.end(), ostream_iterator<string>(cout, " "));
    cout << endl;

    // Now change the value of s.
    // f_ref, which is bound to ref(s), will use the
    // new value, while f is still bound to the old value.

    s = "kitty";

    // Remove elements that are shorter than "meow" (f is bound to old value of s)

    v = v_original;
    v.erase(remove_if(v.begin(), v.end(), f), v.end());

    copy(v.begin(), v.end(), ostream_iterator<string>(cout, " "));
    cout << endl;

    // Remove elements that are shorter than "kitty" (f_ref is bound to ref(s))

    v = v_original;
    v.erase(remove_if(v.begin(), v.end(), f_ref), v.end());

    copy(v.begin(), v.end(), ostream_iterator<string>(cout, " "));
    cout << endl;
}
```

```Output
tiger cat lion cougar
tiger lion cougar
tiger lion cougar
tiger cougar
```

## <a name="swap"></a><a name="swap"></a> フォト

2 つの `function` オブジェクトを交換します。

```cpp
template <class FT>
    void swap(function<FT>& f1, function<FT>& f2);
```

### <a name="parameters"></a>パラメーター

*CM*\
関数オブジェクトによって制御される型。

*f1*\
最初の関数オブジェクト。

*bios*\
2 番目の関数オブジェクト。

### <a name="remarks"></a>解説

`f1.swap(f2)` が返されます。

### <a name="example"></a>例

```cpp
// std__functional__swap.cpp
// compile with: /EHsc
#include <functional>
#include <iostream>

int neg(int val)
    {
    return (-val);
    }

int main()
    {
    std::function<int (int)> fn0(neg);
    std::cout << std::boolalpha << "empty == " << !fn0 << std::endl;
    std::cout << "val == " << fn0(3) << std::endl;

    std::function<int (int)> fn1;
    std::cout << std::boolalpha << "empty == " << !fn1 << std::endl;
    std::cout << std::endl;

    swap(fn0, fn1);
    std::cout << std::boolalpha << "empty == " << !fn0 << std::endl;
    std::cout << std::boolalpha << "empty == " << !fn1 << std::endl;
    std::cout << "val == " << fn1(3) << std::endl;

    return (0);
    }
```

```Output
empty == false
val == -3
empty == true

empty == true
empty == false
val == -3
```
