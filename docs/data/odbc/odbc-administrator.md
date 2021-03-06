---
title: ODBC データ ソース アドミニストレーター
ms.date: 11/04/2016
helpviewer_keywords:
- installing ODBC
- ODBC data sources [C++], ODBC Administrator
- ODBC drivers [C++], installing
- ODBC [C++], ODBC Administrator
- Administrator in ODBC
- administration ODBC Administrator
- ODBC Administrator [C++]
- drivers [C++], ODBC
ms.assetid: b8652790-3437-4e7d-bc83-6ea6981f008b
ms.openlocfilehash: 9e88492919eac80a4f3db2f94202d49011aa69de
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80213180"
---
# <a name="odbc-administrator"></a>ODBC データ ソース アドミニストレーター

ODBC 管理者は、ローカルまたはネットワーク経由で使用できる[データソース](../../data/odbc/data-source-odbc.md)を登録して構成します。 ウィザードは、ODBC データ ソース アドミニストレーターの提供する情報を利用して、データ ソースに接続するコードを生成します。

MFC ODBC クラスまたは MFC DAO (データ アクセス オブジェクト) クラスで使用する ODBC データ ソースをセットアップするには、最初にデータ ソースの登録と設定を行う必要があります。 データ ソースの追加や削除には ODBC データ ソース アドミニストレーターを使います。 使用する ODBC ドライバーによっては、新しいデータ ソースも作成できます。

ODBC データ ソース アドミニストレーターは、セットアップ時にインストールされます。 **[カスタム]** インストール を選択し、 **[データベースのオプション]** ダイアログボックスで ODBC ドライバーを選択しなかった場合は、セットアップを再度実行して、必要なファイルをインストールする必要があります。

ODBC ドライバーは、セットアップ時に選択してインストールします。 また、セットアップ後に、Visual C++ セットアップ プログラムを使って、Visual C++ に添付されているドライバーをインストールすることもできます。

Visual C++ に添付されていない ODBC ドライバーをインストールする場合は、そのドライバーのセットアップ プログラムを実行してください。

#### <a name="to-install-odbc-drivers-that-ship-with-visual-c"></a>Visual C++ に添付されている ODBC ドライバーをインストールするには

1. Visual C++ の CD からセットアップ プログラムを起動します。

   セットアップ プログラムの最初のダイアログ ボックスが表示されます。

1. 各ダイアログボックスで **[次へ]** をクリックすると、 **[インストールオプション]** ダイアログボックスが表示されます。 **[カスタム]** を選択し、 **[次へ]** をクリックします。

1. **[ C++ Microsoft Visual セットアップ]** ダイアログボックスのすべてのチェックボックスをオフにします ( **[データベースのオプション]** チェックボックスを除く)。次に、 **[詳細]** をクリックして、 **[データベースのオプション]** ダイアログボックスを表示します。

1. **[Microsoft Data Access Objects]** チェックボックスをオフにし、 **[microsoft ODBC ドライバー]** チェックボックスをオンにして、 **[詳細]** をクリックします。

   **[MICROSOFT ODBC ドライバー]** ダイアログボックスが表示されます。

1. インストールするドライバーを選択し、 **[OK]** を2回クリックします。

1. 残りのダイアログボックスで **[次へ]** をクリックして、インストールを開始します。 インストールが完了すると、セットアップ プログラムが知らせます。

ドライバーをインストールしたら、ODBC データ ソース アドミニストレーターを使用してデータ ソースを設定できます。 ODBC アイコンはコントロール パネルにあります。

## <a name="see-also"></a>参照

[ODBC (Open Database Connectivity)](../../data/odbc/open-database-connectivity-odbc.md)<br/>
[データ ソース (ODBC)](../../data/odbc/data-source-odbc.md)
