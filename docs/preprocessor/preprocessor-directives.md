---
title: プリプロセッサ ディレクティブ
ms.date: 08/29/2019
helpviewer_keywords:
- directives, preprocessor
- preprocessor, directives
ms.assetid: e0fc4564-b6cf-4a36-bf51-6ccd7abd0a94
ms.openlocfilehash: ac765d33aec4795e94866c097d6c453dbd0e4a08
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88845329"
---
# <a name="preprocessor-directives"></a>プリプロセッサ ディレクティブ

`#define` や `#ifdef` などのプリプロセッサ ディレクティブは、通常、ソースプログラムの変更を容易にし、異なる実行環境で簡単にコンパイルできるようにするために使用されます。 ソースファイル内のディレクティブは、特定のアクションを実行するようにプリプロセッサに指示します。 たとえば、プリプロセッサは、テキストのトークンを置き換えたり、ソース ファイルに他のファイルの内容を挿入したり、テキストのセクションの削除によりファイルの一部のコンパイルを中止したりできます。 プリプロセッサ行は、マクロの展開の前に認識され、実行されます。 したがって、マクロがプリプロセッサコマンドのようなものを展開すると、プリプロセッサによって認識されません。

プリプロセッサ ステートメントは、ソースファイル ステートメントと同じ文字セットを使用しますが、エスケープシーケンスはサポートされていません。 プリプロセッサ ステートメントで使用される文字セットは、実行文字セットと同じです。 プリプロセッサは、負の文字値も認識します。

プリプロセッサは次のディレクティブを認識します。

:::row:::
   :::column span="":::
      [`#define`](../preprocessor/hash-define-directive-c-cpp.md)\
      [`#elif`](../preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp.md)\
      [`#else`](../preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp.md)\
      [`#endif`](../preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp.md)
   :::column-end:::
   :::column span="":::
      [`#error`](../preprocessor/hash-error-directive-c-cpp.md)\
      [`#if`](../preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp.md)\
      [`#ifdef`](../preprocessor/hash-ifdef-and-hash-ifndef-directives-c-cpp.md)\
      [`#ifndef`](../preprocessor/hash-ifdef-and-hash-ifndef-directives-c-cpp.md)
   :::column-end:::
   :::column span="":::
      [`#import`](../preprocessor/hash-import-directive-cpp.md)\
      [`#include`](../preprocessor/hash-include-directive-c-cpp.md)\
      [`#line`](../preprocessor/hash-line-directive-c-cpp.md)
   :::column-end:::
   :::column span="":::
      [`#pragma`](../preprocessor/pragma-directives-and-the-pragma-keyword.md)\
      [`#undef`](../preprocessor/hash-undef-directive-c-cpp.md)\
      [`#using`](../preprocessor/hash-using-directive-cpp.md)
   :::column-end:::
:::row-end:::

番号記号 (`#`) は、ディレクティブを含む行の最初の非空白文字である必要があります。 番号記号とディレクティブの最初の文字の間に空白文字を含めることができます。 一部のディレクティブには、引数または値が含まれます。 ディレクティブ (ディレクティブの一部である引数または値を除く) の後に続くテキストは、前に単一行コメント区切り記号 (`//`) を付けるか、コメント区切り記号 (`/* */`) で囲む必要があります。 プリプロセッサ ディレクティブを含む行は、行末のマーカーの直前に円記号 (`\`) を付けて続けることができます。

プリプロセッサ ディレクティブは、ソースファイル内の任意の場所で使用できますが、使用されたあとのソースファイルの残りの部分にのみ適用されます。

## <a name="see-also"></a>関連項目

[プリプロセッサ演算子](../preprocessor/preprocessor-operators.md)\
[定義済みマクロ](../preprocessor/predefined-macros.md)\
[C/C++ プリプロセッサ リファレンス](../preprocessor/c-cpp-preprocessor-reference.md)
