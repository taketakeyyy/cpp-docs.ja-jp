---
title: '&lt;list&gt; 演算子'
ms.date: 11/04/2016
f1_keywords:
- list/std::operator!=
- list/std::operator&gt;
- list/std::operator&gt;=
- list/std::operator&lt;
- list/std::operator&lt;=
- list/std::operator==
ms.assetid: 8103d8f2-c30f-49ad-ac50-b3ba6a907ebe
helpviewer_keywords:
- std::operator!= (list)
- std::operator&gt; (list)
- std::operator&gt;= (list)
- std::operator&lt; (list)
- std::operator&lt;= (list)
- std::operator== (list)
ms.openlocfilehash: 8648258f17bff577ba1c0dde5016f5f284b82e25
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87224839"
---
# <a name="ltlistgt-operators"></a>&lt;list&gt; 演算子

## <a name="operator"></a><a name="op_neq"></a>operator! =

演算子の左辺の list オブジェクトが右辺の list オブジェクトと等しくないかどうかを調べます。

```cpp
bool operator!=(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** リストが等しくない場合は。**`false`** リストが等しい場合は。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つの list は、同じ数の要素を持ち、各要素の値が同じである場合に等しくなります。 それ以外の場合は等しくありません。

### <a name="example"></a>例

```cpp
// list_op_ne.cpp
// compile with: /EHsc
#include <list>
#include <iostream>

int main( )
{
using namespace std;
list <int> c1, c2;
c1.push_back( 1 );
c2.push_back( 2 );

if ( c1 != c2 )
cout << "Lists not equal." << endl;
else
cout << "Lists equal." << endl;
}
/* Output:
Lists not equal.
*/
```

## <a name="operatorlt"></a><a name="op_lt"></a>operator&lt;

演算子の左辺の list オブジェクトが右辺の list オブジェクトより小さいかどうかを調べます。

```cpp
bool operator<(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** 演算子の左辺のリストが演算子の右辺のリストより小さい場合は、それ以外の場合は。それ以外の場合は **`false`** 。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つのオブジェクト間の小なり関係は、最初の等しくない要素のペアの比較に基づいています。

### <a name="example"></a>例

```cpp
// list_op_lt.cpp
// compile with: /EHsc
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   list <int> c1, c2;
   c1.push_back( 1 );
   c1.push_back( 2 );
   c1.push_back( 4 );

   c2.push_back( 1 );
   c2.push_back( 3 );

   if ( c1 < c2 )
      cout << "List c1 is less than list c2." << endl;
   else
      cout << "List c1 is not less than list c2." << endl;
}
/* Output:
List c1 is less than list c2.
*/
```

## <a name="operatorlt"></a><a name="op_lt_eq"></a>operator&lt;=

演算子の左辺の list オブジェクトが右辺の list オブジェクト以下かどうかを調べます。

```cpp
bool operator<=(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** 演算子の左辺のリストが演算子の右辺の list 以下である場合は、を返します。それ以外の場合は **`false`** 。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つのオブジェクト間の "以下" 関係は、最初の等しくない要素のペアの比較に基づいています。

### <a name="example"></a>例

```cpp
// list_op_le.cpp
// compile with: /EHsc
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   list <int> c1, c2;
   c1.push_back( 1 );
   c1.push_back( 2 );
   c1.push_back( 4 );

   c2.push_back( 1 );
   c2.push_back( 3 );

   if ( c1 <= c2 )
      cout << "List c1 is less than or equal to list c2." << endl;
   else
      cout << "List c1 is greater than list c2." << endl;
}
/* Output:
List c1 is less than or equal to list c2.
*/
```

## <a name="operator"></a><a name="op_eq_eq"></a>operator = =

演算子の左辺の list オブジェクトが右辺の list オブジェクトと等しいかどうかを調べます。

```cpp
bool operator==(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** 演算子の左辺のリストが演算子の右辺にあるリストと等しい場合は、。それ以外の場合は **`false`** 。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つの list は、同じ数の要素を持ち、各要素の値が同じである場合に等しくなります。 それ以外の場合は等しくありません。

### <a name="example"></a>例

```cpp
// list_op_eq.cpp
// compile with: /EHsc
#include <list>
#include <iostream>
int main( )
{
   using namespace std;

   list <int> c1, c2;
   c1.push_back( 1 );
   c2.push_back( 1 );

   if ( c1 == c2 )
      cout << "The lists are equal." << endl;
   else
      cout << "The lists are not equal." << endl;
}
/* Output:
The lists are equal.
*/
```

## <a name="operatorgt"></a><a name="op_gt"></a>operator&gt;

演算子の左辺の list オブジェクトが右辺の list オブジェクトより大きいかどうかを調べます。

```cpp
bool operator>(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** 演算子の左辺のリストが演算子の右辺の list より大きい場合は、です。それ以外の場合は **`false`** 。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つのオブジェクト間の大なり関係は、最初の等しくない要素のペアの比較に基づいています。

### <a name="example"></a>例

```cpp
// list_op_gt.cpp
// compile with: /EHsc
#include <list>
#include <iostream>
int main( )
{
   using namespace std;
   list <int> c1, c2;
   c1.push_back( 1 );
   c1.push_back( 3 );
   c1.push_back( 1 );

   c2.push_back( 1 );
   c2.push_back( 2 );
   c2.push_back( 2 );

   if ( c1 > c2 )
      cout << "List c1 is greater than list c2." << endl;
   else
      cout << "List c1 is not greater than list c2." << endl;
}
/* Output:
List c1 is greater than list c2.
*/
```

## <a name="operatorgt"></a><a name="op_gt_eq"></a>operator&gt;=

演算子の左辺の list オブジェクトが右辺の list オブジェクト以上かどうかを調べます。

```cpp
bool operator>=(
    const list<Type, Allocator>& left,
    const list<Type, Allocator>& right);
```

### <a name="parameters"></a>パラメーター

*左側*\
`list` 型オブジェクト。

*そうです*\
`list` 型オブジェクト。

### <a name="return-value"></a>戻り値

**`true`** 演算子の左辺のリストが演算子の右辺のリスト以上である場合は、を返します。それ以外の場合は **`false`** 。

### <a name="remarks"></a>解説

list オブジェクト間の比較は、要素のペアの比較に基づいています。 2 つのオブジェクト間の "以上" 関係は、最初の等しくない要素のペアの比較に基づいています。

### <a name="example"></a>例

```cpp
// list_op_ge.cpp
// compile with: /EHsc
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   list <int> c1, c2;
   c1.push_back( 1 );
   c1.push_back( 3 );
   c1.push_back( 1 );

   c2.push_back( 1 );
   c2.push_back( 2 );
   c2.push_back( 2 );

   if ( c1 >= c2 )
      cout << "List c1 is greater than or equal to list c2." << endl;
   else
      cout << "List c1 is less than list c2." << endl;
}
/* Output:
List c1 is greater than or equal to list c2.
*/
```
