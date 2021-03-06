---
title: const_seg プラグマ
ms.date: 08/29/2019
f1_keywords:
- vc-pragma.const_seg
- const_seg_CPP
helpviewer_keywords:
- pragmas, const_seg
- const_seg pragma
ms.assetid: 1eb58ee2-fb0e-4a39-9621-699c8f5ef957
ms.openlocfilehash: 04467df1205bd6d4c70687422572aef898d46f68
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87231625"
---
# <a name="const_seg-pragma"></a>const_seg プラグマ

[Const](../cpp/const-cpp.md)変数がオブジェクト (.obj) ファイルに格納されるセクション (セグメント) を指定します。

## <a name="syntax"></a>構文

> **#pragma const_seg (** ["*section-name*" [ **,** "*section-class*"]] **)**\
> **#pragma const_seg (** { **push**  |  **pop** } [ **,** *identifier* ] [ **,** "*section-name*" [ **,** "*section-class*"]] **)**

### <a name="parameters"></a>パラメーター

**押し付け**\
Optional内部コンパイラスタックにレコードを格納します。 **プッシュ**は*識別子*と*セクション名*を持つことができます。

**ショート**\
Optional内部コンパイラスタックの先頭からレコードを削除します。 **Pop**は*識別子*と*セクション名*を持つことができます。 *識別子*を使用して、 **pop**コマンドを1つだけ使用して複数のレコードをポップできます。 *セクション名*は、pop の後のアクティブな const セクション名になります。

*identifier*\
Optional**Push**と共に使用すると、内部コンパイラスタックのレコードに名前が割り当てられます。 **Pop**と共に使用する場合、ディレクティブは、*識別子*が削除されるまで、レコードを内部スタックからポップします。 *識別子*が内部スタックで見つからない場合は、何もポップされません。

"*section-name*" \
Optionalセクションの名前。 **Pop**と共に使用すると、スタックがポップされ、*セクション名*がアクティブな const セクション名になります。

"*セクションクラス*" \
Optionalは無視されますが、バージョン2.0 より前のバージョンの Microsoft C++ との互換性のために含まれています。

## <a name="remarks"></a>解説

オブジェクトファイルの*セクション*は、1つの単位としてメモリに読み込まれるデータの名前付きブロックです。 *Const セクション*は、定数データを含むセクションです。 この記事では、*セグメント*と*セクション*は同じ意味を持ちます。

**Const_seg** pragma ディレクティブは、翻訳単位のすべての定数データ項目を、*セクション名*という名前の const セクションに配置するようコンパイラに指示します。 変数のオブジェクトファイルの既定のセクション **`const`** は `.rdata` です。 スカラーなどの一部の **`const`** 変数は、コードストリームに自動的にインライン化されます。 インラインコードはには表示されません `.rdata` 。 *Section-name*パラメーターを指定せずに**const_seg**プラグマディレクティブを使用すると、後続のデータ項目のセクション名がにリセットされ **`const`** `.rdata` ます。

で動的な初期化を必要とするオブジェクトを定義した場合、 `const_seg` 結果は未定義の動作になります。

セクションの作成に使用しない名前の一覧については、「 [/SECTION](../build/reference/section-specify-section-attributes.md)」を参照してください。

初期化されたデータのセクション ([data_seg](../preprocessor/data-seg.md))、初期化されていないデータ ([bss_seg](../preprocessor/bss-seg.md))、および関数 ([code_seg](../preprocessor/code-seg.md)) を指定することもできます。

[DUMPBIN.EXE](../build/reference/dumpbin-command-line.md)アプリケーションを使用して、オブジェクトファイルを表示できます。 サポートされている各ターゲットアーキテクチャの DUMPBIN のバージョンは、Visual Studio に含まれています。

## <a name="example"></a>例

```cpp
// pragma_directive_const_seg.cpp
// compile with: /EHsc
#include <iostream>

const int i = 7;               // inlined, not stored in .rdata
const char sz1[]= "test1";     // stored in .rdata

#pragma const_seg(".my_data1")
const char sz2[]= "test2";     // stored in .my_data1

#pragma const_seg(push, stack1, ".my_data2")
const char sz3[]= "test3";     // stored in .my_data2

#pragma const_seg(pop, stack1) // pop stack1 from stack
const char sz4[]= "test4";     // stored in .my_data1

int main() {
    using namespace std;
   // const data must be referenced to be put in .obj
   cout << sz1 << endl;
   cout << sz2 << endl;
   cout << sz3 << endl;
   cout << sz4 << endl;
}
```

```Output
test1
test2
test3
test4
```

## <a name="see-also"></a>関連項目

[プラグマ ディレクティブと __pragma キーワード](../preprocessor/pragma-directives-and-the-pragma-keyword.md)
