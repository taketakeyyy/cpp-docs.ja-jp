---
title: '&lt;filesystem&gt; 関数'
ms.date: 03/27/2019
f1_keywords:
- FILESYSTEM/std::experimental::filesystem::absolute
- FILESYSTEM/std::experimental::filesystem::canonical
- FILESYSTEM/std::experimental::filesystem::copy
- FILESYSTEM/std::experimental::filesystem::copy_file
- FILESYSTEM/std::experimental::filesystem::copy_symlink
- FILESYSTEM/std::experimental::filesystem::create_directories
- FILESYSTEM/std::experimental::filesystem::create_directory
- FILESYSTEM/std::experimental::filesystem::create_directory_symlink
- FILESYSTEM/std::experimental::filesystem::create_hard_link
- FILESYSTEM/std::experimental::filesystem::create_symlink
- FILESYSTEM/std::experimental::filesystem::current_path
- FILESYSTEM/std::experimental::filesystem::equivalent
- FILESYSTEM/std::experimental::filesystem::exists
- FILESYSTEM/std::experimental::filesystem::file_size
- FILESYSTEM/std::experimental::filesystem::hard_link_count
- FILESYSTEM/std::experimental::filesystem::hash_value
- FILESYSTEM/std::experimental::filesystem::is_block_file
- FILESYSTEM/std::experimental::filesystem::is_character_file
- FILESYSTEM/std::experimental::filesystem::is_directory
- FILESYSTEM/std::experimental::filesystem::is_empty
- FILESYSTEM/std::experimental::filesystem::is_fifo
- FILESYSTEM/std::experimental::filesystem::is_other
- FILESYSTEM/std::experimental::filesystem::is_regular_file
- FILESYSTEM/std::experimental::filesystem::is_socket
- FILESYSTEM/std::experimental::filesystem::is_symlink
- FILESYSTEM/std::experimental::filesystem::last_write_time
- FILESYSTEM/std::experimental::filesystem::permissions
- FILESYSTEM/std::experimental::filesystem::read_symlink
- FILESYSTEM/std::experimental::filesystem::remove
- FILESYSTEM/std::experimental::filesystem::remove_all
- FILESYSTEM/std::experimental::filesystem::rename
- FILESYSTEM/std::experimental::filesystem::resize_file
- FILESYSTEM/std::experimental::filesystem::space
- FILESYSTEM/std::experimental::filesystem::status
- FILESYSTEM/std::experimental::filesystem::status_known
- FILESYSTEM/std::experimental::filesystem::swap
- FILESYSTEM/std::experimental::filesystem::symlink_status
- FILESYSTEM/std::experimental::filesystem::system_complete
- FILESYSTEM/std::experimental::filesystem::temp_directory_path
- FILESYSTEM/std::experimental::filesystem::u8path
ms.assetid: be3cb821-4728-4d47-ab78-858fa8aa5045
helpviewer_keywords:
- std::experimental::filesystem::absolute
- std::experimental::filesystem::canonical
- std::experimental::filesystem::copy
- std::experimental::filesystem::copy_file
- std::experimental::filesystem::copy_symlink
- std::experimental::filesystem::create_directories
- std::experimental::filesystem::create_directory
- std::experimental::filesystem::create_directory_symlink
- std::experimental::filesystem::create_hard_link
- std::experimental::filesystem::create_symlink
- std::experimental::filesystem::current_path
- std::experimental::filesystem::equivalent
- std::experimental::filesystem::exists
- std::experimental::filesystem::file_size
- std::experimental::filesystem::hard_link_count
- std::experimental::filesystem::hash_value
- std::experimental::filesystem::is_block_file
- std::experimental::filesystem::is_character_file
- std::experimental::filesystem::is_directory
- std::experimental::filesystem::is_empty
- std::experimental::filesystem::is_fifo
- std::experimental::filesystem::is_other
- std::experimental::filesystem::is_regular_file
- std::experimental::filesystem::is_socket
- std::experimental::filesystem::is_symlink
- std::experimental::filesystem::last_write_time
- std::experimental::filesystem::permissions
- std::experimental::filesystem::read_symlink
- std::experimental::filesystem::remove
- std::experimental::filesystem::remove_all
- std::experimental::filesystem::rename
- std::experimental::filesystem::resize_file
- std::experimental::filesystem::space
- std::experimental::filesystem::status
- std::experimental::filesystem::status_known
- std::experimental::filesystem::swap
- std::experimental::filesystem::symlink_status
- std::experimental::filesystem::system_complete
- std::experimental::filesystem::temp_directory_path
- std::experimental::filesystem::u8path
ms.openlocfilehash: c637c4893a13df577fd6c083c8a4f2380c9c4cad
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87219158"
---
# <a name="ltfilesystemgt-functions"></a>&lt;filesystem&gt; 関数

ヘッダーに含まれるこれらの free 関数 [\<filesystem>](../standard-library/filesystem.md) は、パス、ファイル、シンボリックリンク、ディレクトリ、およびボリュームに対する操作を変更し、クエリを実行します。 詳細とコード例については、「[ファイルシステムのナビゲーション (C++)](../standard-library/file-system-navigation.md)」を参照してください。

## <a name="absolute"></a><a name="absolute"></a>絶対

```cpp
path absolute(const path& pval, const path& base = current_path());
```

関数は、パス名に対して相対的な*pval*に対応する絶対パス名を返し `base` ます。

1. `pval.has_root_name() && pval.has_root_directory()`関数が*pval*を返す場合は。

1. `pval.has_root_name() && !pval.has_root_directory()`関数がを返す場合は `pval.root_name()`  /  `absolute(base).root_directory()`  /  `absolute(base).relative_path()`  /  `pval.relative_path()` 。

1. `!pval.has_root_name() && pval.has_root_directory()`関数が pval を返す場合は `absolute(base).root_name()`  /  *pval*。

1. `!pval.has_root_name() && !pval.has_root_directory()`関数が pval を返す場合は `absolute(base)`  /  *pval*。

## <a name="begin"></a><a name="begin"></a>初め

```cpp
const directory_iterator& begin(const directory_iterator& iter) noexcept;
const recursive_directory_iterator&
    begin(const recursive_directory_iterator& iter) noexcept;
```

どちらの関数も、 *iter*を返します。

## <a name="canonical"></a><a name="canonical"></a>標準

```cpp
path canonical(const path& pval, const path& base = current_path());
path canonical(const path& pval, error_code& ec);
path canonical(const path& pval, const path& base, error_code& ec);
```

これらの関数はすべて絶対パス名 `pabs = absolute(pval, base)` (または `pabs = absolute(pval)` 、基本パラメーターのないオーバーロード) を形成してから、次の一連の手順で正規の形式に縮小します。

1. がに置換されるすべてのパスコンポーネント `X` `is_symlink(X)` **`true`** `read_symlink(X)` 。

1. すべてのパスコンポーネント `.` (ドットは、前のパスコンポーネントによって確立された現在のディレクトリ) が削除されます。

1. パスコンポーネントのすべてのペア `X` / `..` (ドットドットは、前のパスコンポーネントによって確立された親ディレクトリ) が削除されます。

次に、関数はを返し `pabs` ます。

## <a name="copy"></a><a name="copy"></a>copy

```cpp
void copy(const path& from, const path& to);
void copy(const path& from, const path& to, error_code& ec) noexcept;
void copy(const path& from, const path& to, copy_options opts);
void copy(const path& from, const path& to, copy_options opts, error_code& ec) noexcept;
```

これら*の関数*では、指定されていない1つ以上のファイルを*から**にコピー*またはリンクすることが `copy_options::none` できます*opts* 。 *opts* 1 つのを含めることができます:

- `skip_existing`、`overwrite_existing`、または `update_existing`

- `copy_symlinks` または `skip_symlinks`

- `directories_only`、`create_symlinks`、または `create_hard_links`

これらの関数は、最初に `f` の*from*との file_status 値を次の `t` *ように*決定します。

- `opts & (copy_options::create_symlinks | copy_options::skip_symlinks)`の場合、を呼び出します。`symlink_status`

- それ以外の場合は、を呼び出します。`status`

- それ以外の場合は、エラーを報告します。

の場合は `!exists(f) || equivalent(f, t) || is_other(f) || is_other(t) || is_directory(f)&& is_regular_file(t)` 、エラーを報告します (他の操作は何も行いません)。

それ以外の場合は、次の `is_symlink(f)` ようになります。

- の場合は `options & copy_options::skip_symlinks` 、何も行いません。

- それ以外の場合は、の場合は `!exists(t)&& options & copy_options::copy_symlinks` `copy_symlink(from, to, opts)` です。

- それ以外の場合は、エラーを報告します。

それ以外の場合、の場合は `is_regular_file(f)` 次のようになります。

- の場合は `opts & copy_options::directories_only` 、何も行いません。

- それ以外の場合は、の場合は `opts & copy_options::create_symlinks` `create_symlink(to, from)` です。

- それ以外の場合は、の場合は `opts & copy_options::create_hard_links` `create_hard_link(to, from)` です。

- それ以外の場合は、の場合は `is_directory(f)` `copy_file(from, to`  /  `from.filename(), opts)` です。

- それ以外の場合は `copy_file(from, to, opts)`。

それ以外の場合、の場合は `is_directory(f) && (opts & copy_options::recursive || !opts)` 次のようになります。

```cpp
if (!exists(t))
{  // copy directory contents recursively
    create_directory(to, from, ec);

    for (directory_iterator next(from), end; ec == error_code() && next != end; ++next)
    {
        copy(next->path(), to / next->path().filename(), opts, ec);
    }
}
```

それ以外の場合は、何もしません。

## <a name="copy_file"></a><a name="copy_file"></a>copy_file

```cpp
bool copy_file(const path& from, const path& to);
bool copy_file(const path& from, const path& to, error_code& ec) noexcept;
bool copy_file(const path& from, const path& to, copy_options opts);
bool copy_file(const path& from, const path& to, copy_options opts, error_code& ec) noexcept;
```

これら*の関数*では、指定されていない場合は、を使用して*から**にファイル*をコピーすることが `copy_options::none` できます。 *opts* *opts*使用するに `skip_existing` は、、、またはのうち1つだけを含める必要があり `overwrite_existing` `update_existing` ます。

の場合は `exists(to) && !(opts & (copy_options::skip_existing | copy_options::overwrite_existing | copy_options::update_existing))` 、ファイルが既に存在することを示すエラーとして報告します。

それ以外の場合は、の場合は、 `!exists(to) || opts & copy_options::overwrite_existing || opts & copy_options::update_existing&& last_write_time(to) < last_write_time(from) || !(opts & (copy_options::skip_existing | copy_options::overwrite_existing | copy_options:update_existing))` ファイルの内容と属性を*から*ファイルに*to*コピーします。 このコピーの試行が失敗すると、エラーが報告されます。

**`true`** コピーが試行され、成功した場合、関数はを返します。それ以外の場合はを返し **`false`** ます。

## <a name="copy_symlink"></a><a name="copy_symlink"></a>copy_symlink

```cpp
void copy_symlink(const path& from, const path& to);
void copy_symlink(const path& from, const path& to, error_code& ec) noexcept;
```

の場合 `is_directory(from)` 、関数はを呼び出し `create_directory_symlink(from, to)` ます。 それ以外の場合は、を呼び出し `create_symlink(from, to)` ます。

## <a name="create_directories"></a><a name="create_directories"></a>create_directories

```cpp
bool create_directories(const path& pval);
bool create_directories(const path& pval, error_code& ec) noexcept;
```

B c などのパス名の場合、関数は必要に応じ \/ \/ てディレクトリ a と b を作成し、必要に応じ \/ てディレクトリ a b c を作成できるようにし \/ \/ ます。 このメソッドは **`true`** 、ディレクトリ*pval*を実際に作成した場合にのみを返します。

## <a name="create_directory"></a><a name="create_directory"></a>create_directory

```cpp
bool create_directory(const path& pval);

bool create_directory(const path& pval, error_code& ec) noexcept;
bool create_directory(const path& pval, const path& attr);
bool create_directory(const path& pval, const path& attr, error_code& ec) noexcept;
```

関数は、必要に応じてディレクトリ*pval*を作成します。 このメソッドは、実際にディレクトリ*pval*を作成する場合にのみ true を返します。この場合、既存のファイル*attr*からアクセス許可がコピーされるか、または `perms::all` *attr*パラメーターのないオーバーロードにを使用します。

## <a name="create_directory_symlink"></a><a name="create_directory_symlink"></a>create_directory_symlink

```cpp
void create_directory_symlink(const path& to, const path& link);
void create_directory_symlink(const path& to, const path& link, error_code& ec) noexcept;
```

関数は、ディレクトリへのシンボリックリンクとして*リンクを作成*します。

## <a name="create_hard_link"></a><a name="create_hard_link"></a>create_hard_link

```cpp
void create_hard_link(const path& to,  const path& link);
void create_hard_link(const path& to, const path& link, error_code& ec) noexcept;
```

関数は、*へ*のリンクをディレクトリまたはファイルへのハードリンクとして作成します。

## <a name="create_symlink"></a><a name="create_symlink"></a>create_symlink

```cpp
void create_symlink(const path& to, const path& link);

void create_symlink(const path& to, const path& link, error_code& ec) noexcept;
```

関数は、*へ*のリンクをファイルへのシンボリック*リンク*として作成します。

## <a name="current_path"></a><a name="current_path"></a>current_path

```cpp
path current_path();
path current_path(error_code& ec);
void current_path(const path& pval);
void current_path(const path& pval, error_code& ec) noexcept;
```

パラメーターのない関数*pval*は、現在のディレクトリのパス名を返します。 残りの関数は、現在のディレクトリを*pval*に設定します。

## <a name="end"></a><a name="end"></a>終わり

```cpp
directory_iterator& end(const directory_iterator& iter) noexcept;
recursive_directory_iterator& end(const recursive_directory_iterator& iter) noexcept;
```

最初の関数はを返し、 `directory_iterator()` 2 番目の関数はを返します。`recursive_directory_iterator()`

## <a name="equivalent"></a><a name="equivalent"></a> での同等機能

```cpp
bool equivalent(const path& left, const path& right);
bool equivalent(const path& left, const path& right, error_code& ec) noexcept;
```

これらの関数は、 **`true`** *left*と*right*が同じ filesystem エンティティを選択した場合にのみを返します。

## <a name="exists"></a><a name="exists"></a>あり

```cpp
bool exists(file_status stat) noexcept;
bool exists(const path& pval);
bool exists(const path& pval, error_code& ec) noexcept;
```

最初の関数は `status_known && stat.type() != file_not_found` を返します。 2番目と3番目の関数はを返し `exists(status(pval))` ます。

## <a name="file_size"></a><a name="file_size"></a>file_size

```cpp
uintmax_t file_size(const path& pval);
uintmax_t file_size(const path& pval, error_code& ec) noexcept;
```

関数は、 *pval*によって選択されたファイルのサイズ (バイト単位) を返し `exists(pval) && is_regular_file(pval)` ます。また、ファイルサイズを確認できる場合はを返します。 それ以外の場合は、エラーを報告してを返し `uintmax_t(-1)` ます。

## <a name="hard_link_count"></a><a name="hard_link_count"></a>hard_link_count

```cpp
uintmax_t hard_link_count(const path& pval);
uintmax_t hard_link_count(const path& pval, error_code& ec) noexcept;
```

関数は、 *pval*のハードリンクの数を返し \- ます。エラーが発生した場合は1を返します。

## <a name="hash_value"></a><a name="hash_value"></a>hash_value

```cpp
size_t hash_value(const path& pval) noexcept;
```

関数は、のハッシュ値を返し `pval.native()` ます。

## <a name="is_block_file"></a><a name="is_block_file"></a>is_block_file

```cpp
bool is_block_file(file_status stat) noexcept;
bool is_block_file(const path& pval);
bool is_block_file(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::block` を返します。 残りの関数は、 `is_block_file(status(pval))` を返します。

## <a name="is_character_file"></a><a name="is_character_file"></a>is_character_file

```cpp
bool is_character_file(file_status stat) noexcept;
bool is_character_file(const path& pval);
bool is_character_file(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::character` を返します。 残りの関数は、 `is_character_file(status(pval))` を返します。

## <a name="is_directory"></a><a name="is_directory"></a>is_directory

```cpp
bool is_directory(file_status stat) noexcept;
bool is_directory(const path& pval);
bool is_directory(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::directory` を返します。 残りの関数は、 `is_directory_file(status(pval))` を返します。

## <a name="is_empty"></a><a name="is_empty"></a>is_empty

```cpp
bool is_empty(file_status stat) noexcept;
bool is_empty(const path& pval);
bool is_empty(const path& pval, error_code& ec) noexcept;
```

の場合、 `is_directory(pval)` 関数はを返し `directory_iterator(pval) == directory_iterator()` ます。それ以外の場合はを返し `file_size(pval) == 0` ます。

## <a name="is_fifo"></a><a name="is_fifo"></a>is_fifo

```cpp
bool is_fifo(file_status stat) noexcept;
bool is_fifo(const path& pval);
bool is_fifo(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::fifo` を返します。 残りの関数は、 `is_fifo(status(pval))` を返します。

## <a name="is_other"></a><a name="is_other"></a>is_other

```cpp
bool is_other(file_status stat) noexcept;
bool is_other(const path& pval);
bool is_other(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::other` を返します。 残りの関数は、 `is_other(status(pval))` を返します。

## <a name="is_regular_file"></a><a name="is_regular_file"></a>is_regular_file

```cpp
bool is_regular_file(file_status stat) noexcept;
bool is_regular_file(const path& pval);
bool is_regular_file(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::regular` を返します。 残りの関数は、 `is_regular_file(status(pval))` を返します。

## <a name="is_socket"></a><a name="is_socket"></a>is_socket

```cpp
bool is_socket(file_status stat) noexcept;
bool is_socket(const path& pval);
bool is_socket(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::socket` を返します。 残りの関数は、 `is_socket(status(pval))` を返します。

## <a name="is_symlink"></a><a name="is_symlink"></a>is_symlink

```cpp
bool is_symlink(file_status stat) noexcept;
bool is_symlink(const path& pval);
bool is_symlink(const path& pval, error_code& ec) noexcept;
```

最初の関数は `stat.type() == file_type::symlink` を返します。 残りの関数は、 `is_symlink(status(pval))` を返します。

## <a name="last_write_time"></a><a name="last_write_time"></a>last_write_time

```cpp
file_time_type last_write_time(const path& pval);
file_time_type last_write_time(const path& pval, error_code& ec) noexcept;
void last_write_time(const path& pval, file_time_type new_time);
void last_write_time(const path& pval, file_time_type new_time, error_code& ec) noexcept;
```

最初の2つの関数は、 *pval*の最終データ変更の時刻を返し `file_time_type(-1)` ます。エラーが発生した場合は、を返します。 最後の2つの関数は、 *pval*に対して最後にデータを変更した時刻を*new_time*に設定します。

## <a name="permissions"></a><a name="permissions"></a>許可

```cpp
void permissions(const path& pval, perms mask);
void permissions(const path& pval, perms mask, error_code& ec) noexcept;
```

これらの関数は、 *pval*によって選択されたパス名に対するアクセス許可を `mask & perms::mask` の制御下に設定し `perms & (perms::add_perms | perms::remove_perms)` ます。 *mask*には、とのうち1つだけを含める必要が `perms::add_perms` `perms::remove_perms` あります。

の場合、これらの `mask & perms::add_perms` 関数はアクセス許可をに設定し `status(pval).permissions() | mask & perms::mask` ます。 それ以外の場合、の場合、これらの `mask & perms::remove_perms` 関数はアクセス許可をに設定し `status(pval).permissions() & ~(mask & perms::mask)` ます。 それ以外の場合、これらの関数はアクセス許可をに設定し `mask & perms::mask` ます。

## <a name="proximate"></a><a name="proximate"></a>近接

```cpp
path proximate(const path& p, error_code& ec);
path proximate(const path& p, const path& base = current_path());
path proximate(const path& p, const path& base, error_code& ec);
```

## <a name="read_symlink"></a><a name="read_symlink"></a>read_symlink

```cpp
path read_symlink(const path& pval);
path read_symlink(const path& pval, error_code& ec);
```

関数はエラーを報告し、の `path()` 場合はを返し `!is_symlink(pval)` ます。 それ以外の場合は、これらの関数はシンボリック リンクを格納している `path` 型のオブジェクトを返します。

## <a name="relative"></a><a name="relative"></a>点

```cpp
path relative(const path& p, error_code& ec);
path relative(const path& p, const path& base = current_path());
path relative(const path& p, const path& base, error_code& ec);
```

## <a name="remove"></a><a name="remove"></a>から

```cpp
bool remove(const path& pval);
bool remove(const path& pval, error_code& ec) noexcept;
```

関数は、 **`true`** `exists(symlink_status(pval))` とファイルが正常に削除された場合にのみを返します。 シンボリックリンク自体は削除され、選択されたファイルではなくなります。

## <a name="remove_all"></a><a name="remove_all"></a>remove_all

```cpp
uintmax_t remove_all(const path& pval);
uintmax_t remove_all(const path& pval, error_code& ec) noexcept;
```

*Pval*がディレクトリである場合、関数はすべてのディレクトリエントリを再帰的に削除してから、そのエントリ自体を削除します。 それ以外の場合、関数はを呼び出し `remove` ます。 これらの関数は、正常に削除した要素の合計数を返します。

## <a name="rename"></a><a name="rename"></a>リネーム

```cpp
void rename(const path& from, const path& to);
void rename(const path& from, const path& to, error_code& ec) noexcept;
```

関数は、*から*に*名前*を変更します。 シンボリックリンク自体は、選択したファイルではなく、名前が変更されています。

## <a name="resize_file"></a><a name="resize_file"></a>resize_file

```cpp
void resize(const path& pval, uintmax_t size);
void resize(const path& pval, uintmax_t size, error_code& ec) noexcept;
```

関数は、ファイルのサイズを変更します。`file_size(pval) == size`

## <a name="space"></a><a name="space"></a>行間

```cpp
space_info space(const path& pval);
space_info space(const path& pval, error_code& ec) noexcept;
```

関数は、 *pval*によって選択されたボリュームに関する情報を型の構造体で返し `space_info` ます。 構造体には、特定できない値が含まれてい `uintmax_t(-1)` ます。

## <a name="status"></a><a name="status"></a>オンライン

```cpp
file_status status(const path& pval);
file_status status(const path& pval, error_code& ec) noexcept;
```

これらの関数は、 *pval*に関連付けられているパス名の状態、ファイルの種類、およびアクセス許可を返します。 シンボリックリンク自体はテストされませんが、選択されるファイルになります。

## <a name="status_known"></a><a name="status_known"></a>status_known

```cpp
bool status_known(file_status stat) noexcept;
```

関数はを返します。`stat.type() != file_type::none`

## <a name="swap"></a><a name="swap"></a>フォト

```cpp
void swap(path& left, path& right) noexcept;
```

関数は、 *left*と*right*の内容を交換します。

## <a name="symlink_status"></a><a name="symlink_status"></a>symlink_status

```cpp
file_status symlink_status(const path& pval);
file_status symlink_status(const path& pval, error_code& ec) noexcept;
```

これらの関数は、 *pval*に関連付けられているパス名のシンボリックリンクの状態、ファイルの種類、およびアクセス許可を返します。 関数はと同じように動作しますが、 `status(pval)` シンボリックリンク自体は、選択したファイルではなくテストされる点が異なります。

## <a name="system_complete"></a><a name="system_complete"></a>system_complete

```cpp
path system_complete(const path& pval);
path system_complete(const path& pval, error_code& ec);
```

これらの関数は、ルート名に関連付けられた現在のディレクトリを必要に応じて考慮に入れた絶対パス名を返します。 \(POSIX の場合、関数はを返し `absolute(pval)` ます。\)

## <a name="temp_directory_path"></a><a name="temp_directory_path"></a>temp_directory_path

```cpp
path temp_directory_path();
path temp_directory_path(error_code& ec);
```

これらの関数は、一時ファイルの格納に適したディレクトリのパス名を返します。

## <a name="u8path"></a><a name="u8path"></a>u8path

```cpp
template <class Source>
path u8path(const Source& source);

template <class InIt>
path u8path(InIt first, InIt last);
```

最初の関数はと同じように動作 `path(source)` し、2番目の関数はと同じように動作しますが、 `path(first, last)` 各ケースで選択されたソースは、ファイルシステムではなく utf-8 としてエンコードされた char 要素のシーケンスとして扱われる点が異なります。

## <a name="weakly_canonical"></a><a name="weakly_canonical"></a>weakly_canonical

```cpp
path weakly_canonical(const path& p);
path weakly_canonical(const path& p, error_code& ec);
```
