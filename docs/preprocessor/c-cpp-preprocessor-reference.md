---
title: C/C++ のプリプロセッサ リファレンス
description: Visual Studio での Microsoft C/C++ コンパイラプリプロセッサのリファレンスです。
ms.date: 09/10/2020
helpviewer_keywords:
- preprocessor
- preprocessor, reference overview
ms.assetid: e4a52843-7016-4f6d-8b40-cb1ace18f805
ms.openlocfilehash: e72146d8b88f5a4bffcaaa121f6851d740ec948b
ms.sourcegitcommit: b492516cc65120250b9ea23f96f7f63f37f99fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2020
ms.locfileid: "90075635"
---
# <a name="cc-preprocessor-reference"></a>C/C++ のプリプロセッサ リファレンス

『 *C/C++ のプリプロセッサリファレンス* 』では、Microsoft C/C++ で実装されているプリプロセッサについて説明しています。 プリプロセッサは C および C++ ファイルをコンパイラに渡す前の準備的な処理を実行します。 プリプロセッサを使用して、コードの条件付きコンパイル、ファイルの挿入、コンパイル時のエラー メッセージの指定、コード セクションへのコンピューター固有の規則の適用を行うことができます。

Visual Studio 2019 では、 [/Zc: preprocessor](../build/reference/zc-preprocessor.md) コンパイラオプションは完全に準拠した C11 および C17 プリプロセッサを提供します。 これは、コンパイラフラグ `/std:c11` または `/std:c17` を使用する場合の既定値です。

## <a name="in-this-section"></a>このセクションの内容

[プリプロセッサ](preprocessor.md)\
従来のプリプロセッサと新しく準拠するプリプロセッサの概要について説明します。

[プリプロセッサ ディレクティブ](../preprocessor/preprocessor-directives.md)\
異なる実行環境でソース プログラムの変更やコンパイルを容易にするために通常使用される、ディレクティブについて説明します。

[プリプロセッサ演算子](../preprocessor/preprocessor-operators.md)\
`#define` ディレクティブのコンテキストで使用される、4 つのプリプロセッサ固有の演算子について説明します。

[定義済みマクロ](../preprocessor/predefined-macros.md)\
C および C++ 標準および Microsoft C++ によって指定された定義済みマクロについて説明します。

[プラグマ](../preprocessor/pragma-directives-and-the-pragma-keyword.md)\
各コンパイラが C 言語および C++ 言語の全体的な互換性を維持しながら、コンピューター固有の機能およびオペレーティング システム固有の機能を提供するために使用される、プラグマについて説明します。

## <a name="related-sections"></a>関連項目

[C++ 言語リファレンス](../cpp/cpp-language-reference.md)\
C++ 言語の Microsoft 実装に関するリファレンス ドキュメントを紹介します。

[C 言語リファレンス](../c-language/c-language-reference.md)\
C 言語の Microsoft 実装に関するリファレンス ドキュメントを紹介します。

[C/C++ ビルドリファレンス](../build/reference/c-cpp-building-reference.md)\
コンパイラとリンカーのオプション関するトピックへのリンクを示します。

[Visual Studio プロジェクト - C++](../build/creating-and-managing-visual-cpp-projects.md)\
プロジェクト システムが C++ プロジェクトのファイルを見つけるために検索するディレクトリを指定できる、Visual Studio のユーザー インターフェイスについて説明します。
