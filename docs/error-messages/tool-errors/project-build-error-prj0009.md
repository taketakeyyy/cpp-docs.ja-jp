﻿---
title: プロジェクト ビルド エラー PRJ0009
ms.date: 11/04/2016
f1_keywords:
- PRJ0009
helpviewer_keywords:
- PRJ0009
ms.assetid: 89291778-cda4-495d-983f-ddcc06dfc98b
ms.openlocfilehash: d02325504b04a13cd15dee0bd70891bf5a63b62e
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80192965"
---
# <a name="project-build-error-prj0009"></a>プロジェクト ビルド エラー PRJ0009

ビルドログを書き込み用に開けませんでした。

**ファイルが別のプロセスによって開かれていないこと、および書き込み禁止になっていないことを確認してください。**

ビルド**ログ**のプロパティを **[はい]** に設定し、ビルドまたはリビルドC++を実行した後、Visual はビルドログを排他モードで開くことができませんでした。

**[オプション]** ダイアログボックスを開いて ( **[ツール]** メニューの **[オプション]** をクリック)、 **[プロジェクト]** フォルダーで **[VC + + ビルド]** を選択して、**ビルドのログ**設定を調べます。 ビルドファイルは Buildlog.htm ファイルという名前で、中間ディレクトリ $ (IntDir) に書き込まれます。

このエラーの考えられる原因:

- 2つのビジュアルC++プロセスを実行していて、同じプロジェクトの同じ構成を同時にビルドしようとしています。

- ビルドログファイルは、ファイルをロックするプロセスで開かれます。

- ユーザーに、ファイルを作成するためのアクセス許可がありません。

- 現在のユーザーには、Buildlog.htm ファイルファイルへの書き込みアクセス権がありません。
