---
title: "テンプレートと名前解決 |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: C++
ms.assetid: 519ba7b5-cd25-4549-865a-9a7b9dffdc28
caps.latest.revision: "6"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: 7cb6708a8b7631551a6e245c0777bcc6c9fb1a92
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2017
---
# <a name="templates-and-name-resolution"></a>テンプレートと名前解決

テンプレート定義では、3 種類の名前があります。  
  
-   ローカルに宣言された名前。これには、テンプレート自体の名前や、テンプレート定義内で宣言されている名前も含まれます。  
  
-   テンプレート定義の外側のスコープ内の名前。  
  
-   テンプレート引数になんらかの形で依存する名前 (依存名とも呼ばれます)。  
  
 最初の 2 つの名前もクラスと関数のスコープに関係しますが、テンプレート定義では、依存名によって高まる複雑さに対処するために、名前解決の特別な規則が必要になります。 これは、使用されるテンプレート引数によって依存名の型がまったく異なることがあるので、テンプレートがインスタンス化されるまで、コンパイラにはこれらの名前についての情報がほとんどないことによります。 非依存名は、通常の規則に従って、テンプレートの定義時点で検索されます。 これらの名前は、テンプレートの引数に依存しないので、テンプレートの特殊化すべてに対して 1 回参照されます。 依存名はテンプレートがインスタンス化されるまで検索されず、特殊化ごとに個別に検索されます。  
  
 型がテンプレート引数に依存する場合、その型は依存する型です。 具体的には、以下に当てはまるものは依存する型になります。  
  
-   テンプレート引数自体。  
  
    ```cpp
    T  
    ```  
  
-   依存する型を含む修飾を持つ修飾名。  
  
    ```cpp
    T::myType  
    ```  
  
-   非修飾部で依存する型が特定される場合の修飾名。  
  
    ```cpp
    N::T  
    ```  
  
-   基本型が依存する型である const または volatile 型。  
  
    ```cpp
    const T  
    ```  
  
-   依存する型に基づくポインター、参照、配列、または関数ポインター型。  
  
    ```cpp
    T *, T &, T [10], T (*)()  
    ```  
  
-   サイズがテンプレート パラメーターに基づく配列。  
  
    ```cpp
    template <int arg> class X {  
    int x[arg] ; // dependent type  
    }  
    ```  
  
-   テンプレート パラメーターから構築されたテンプレート型。  
  
    ```cpp
    T<int>, MyTemplate<T>  
    ```  
  
## <a name="type-dependence-and-value-dependence"></a>型の依存性と値の依存性

 テンプレート パラメーターに依存する名前と式は、テンプレート パラメーターが型パラメーターであるか値パラメーターであるかによって、型依存か値依存かに分類されます。 また、テンプレート内で宣言された、テンプレート引数に依存する型を持つ識別子は、整数型や列挙型が値に依存する式で初期化されるのと同様に、値依存であると見なされます。  
  
 型に依存する式と値に依存する式は、型依存または値依存である変数が関係する式です。 これらの式は、テンプレートに使用されたパラメーターに応じて異なるセマンティクスを持つことができます。  
  
## <a name="see-also"></a>参照

 [テンプレート](../cpp/templates-cpp.md)