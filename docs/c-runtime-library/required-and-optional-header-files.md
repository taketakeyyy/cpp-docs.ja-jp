---
title: 必須ヘッダー ファイルと省略可能ヘッダー ファイル
description: Microsoft C ランタイムライブラリの必須ヘッダーファイルと省略可能ヘッダーファイルを使用する場合。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- c.headers
helpviewer_keywords:
- include files, required in run time
- header files, required in run time
ms.assetid: f64d0bf5-e2c3-4b42-97d0-443b3d901d9f
ms.openlocfilehash: 79a45aaba5e2872b23e70f3fd276d6f3cae11167
ms.sourcegitcommit: 9451db8480992017c46f9d2df23fb17b503bbe74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91589810"
---
# <a name="required-and-optional-header-files"></a>必須ヘッダー ファイルと省略可能ヘッダー ファイル

各ランタイム ルーチンの説明には、そのルーチンで必須および省略可能なインクルード ファイル、またはヘッダー (.H) ファイルの一覧が含まれています。 内部で呼び出される別のルーチンで使用されるルーチンまたは定義の関数の宣言を取得するには、必須ヘッダー ファイルを含める必要があります。 省略可能ヘッダー ファイルは通常、定義済みの定数、型定義、インライン マクロを活用するために含まれます。 次の表では、省略可能ヘッダー ファイルの内容の例をいくつか示します。

|定義|例|
|----------------|-------------|
|マクロ定義|ライブラリ ルーチンがマクロとして実装されている場合、マクロ定義が元のルーチンのヘッダー ファイル以外のヘッダー ファイルに存在する場合があります。 たとえば、`_toupper` マクロはヘッダー ファイル CTYPE.H に定義されますが、関数 `toupper` は STDLIB.H に宣言されています。|
|定義済みの定数|ライブラリ ルーチンの多くは、ヘッダー ファイルで定義されている定数を参照します。 たとえば、`_open` ルーチンは、ヘッダー ファイル FCNTL.H に定義されている `_O_CREAT` などの定数を使用します。|
|型定義|一部のライブラリ ルーチンは構造体を返すか、引数として構造体を受け取ります。 たとえば、ストリーム入出力ルーチンは、STDIO.H で定義されている型 `FILE` の構造体を使用します。|

ランタイム ライブラリのヘッダー ファイルは、ANSI/ISO C 標準で推奨されるスタイルで関数の宣言を提供します。 コンパイラは、その関連する関数の宣言より後に発生するすべてのルーチン参照に対して型チェックを実行します。 関数宣言は、既定である以外の型の値を返すルーチンに特に重要です **`int`** 。 宣言内で適切な戻り値を指定していないルーチンは、コンパイラによってが返されるため **`int`** 、予期しない結果が発生する可能性があります。 詳細については、「[型チェック](../c-runtime-library/type-checking-crt.md)」を参照してください。

## <a name="see-also"></a>関連項目

[CRT ライブラリの機能](../c-runtime-library/crt-library-features.md)
