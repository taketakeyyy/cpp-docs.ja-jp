---
title: コンパイラの警告 (レベル 1) C4944
ms.date: 11/04/2016
f1_keywords:
- C4944
helpviewer_keywords:
- C4944
ms.assetid: e2905eb1-2e3b-4fab-a48b-c0cae0fd997f
ms.openlocfilehash: 72280bf19d50b0fc1f4c0738d5fc7d7b8a478e5c
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90684314"
---
# <a name="compiler-warning-level-1-c4944"></a>コンパイラの警告 (レベル 1) C4944

'symbol': 'assembly1' からシンボルをインポートできません: 'symbol' は既に現在のスコープに存在します

シンボルがソース コード ファイル内で定義されています。#using ステートメントはアセンブリを参照しますが、そのアセンブリもシンボルを定義しています。 アセンブリ内のシンボルは無視されます。

## <a name="examples"></a>例

ClassA という型を使用してコンポーネントを作成する例を次に示します。

```csharp
// C4944.cs
// compile with: /target:library
// C# source code to create a dll
public class ClassA {
   public int i;
}
```

次の例では C4944 が生成されます。

```cpp
// C4944b.cpp
// compile with: /clr /W1
class ClassA {
public:
   int u;
};

#using "C4944.dll"   // C4944 ClassA also defined C4944.dll

int main() {
   ClassA * x = new ClassA();
   x->u = 9;
   System::Console::WriteLine(x->u);
}
```
