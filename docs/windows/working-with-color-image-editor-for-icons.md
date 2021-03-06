---
title: '方法: 色を操作する'
ms.date: 02/15/2019
f1_keywords:
- vc.editors.image.color
- vc.editors.customcolorselector
- vc.editors.loadcolorpalette
- vc.editors.colorswindow
helpviewer_keywords:
- images [C++], background colors
- Image editor [C++], Colors Palette
- colors [C++], image
- Colors Palette, Image editor
- palettes, Image editor colors
- foreground colors [C++], Image editor
- colors [C++]
- Image editor [C++], colors
- colors [C++], Image editor
- colors [C++], image
- images [C++], colors
- Image editor [C++], colors
- Fill tool
- colors [C++], image
- images [C++], colors
- colors [C++], selection tools
- Image editor [C++], colors
- Select Color tool
- dithered color, Image editor
- Custom Color Selector dialog box [C++]
- Image editor [C++], Colors Palette
- colors [C++], image
- bitmaps [C++], colors
- images [C++], colors
- HSL values
- Colors Palette, Image editor
- RGB color values
- Adjust Colors command [C++]
- Image editor [C++], dithered color
- Image editor [C++], Colors Palette
- Colors Palette, Image editor
- colors [C++], inverting
- colors [C++]
- Color Indicator
- colors [C++], Colors window
- Colors window, hiding colors
- Show Colors Window command
- Colors window, displaying colors
- color palettes [C++]
- palettes
- palettes, Image editor
- colors [C++], Image editor
- Image editor [C++], palettes
- color palettes
- Load Palette Colors dialog box [C++]
- opaque backgrounds [C++]
- colors [C++], image
- Image editor [C++], transparent or opague backgrounds
- images [C++], transparency
- images [C++], opaque background
- colors [C++], image
- Image editor [C++], color inversion
- images [C++], colors
- colors [C++], inverting
ms.assetid: d34ff96f-241d-494f-abdd-13811ada8cd3
ms.openlocfilehash: 3c9134fde9053f57f8848a37b1442728f6111c98
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91502951"
---
# <a name="how-to-work-with-color"></a>方法: 色を操作する

**イメージエディター**には、色を処理およびカスタマイズする多くの機能が含まれています。 前景色または背景色を設定したり、境界領域を色で塗りつぶすことができます。また、イメージの色を選択して、現在の前景色または背景色として使用することもできます。 [ [イメージエディター] ツールバー](./image-editor-for-icons.md) のツールと [ **色** ] ウィンドウのカラーパレットを使用すると、イメージを作成できます。

モノクロおよび16色の画像のすべての色は、[**色**] ウィンドウの [**色**] パレットに表示されます。 16の標準色と共に、独自のカスタムカラーを作成できます。 パレット内のいずれかの色を変更すると、イメージ内の対応する色が直ちに変更されます。

256カラーアイコンとカーソルイメージを使用する場合、[プロパティウィンドウ](/visualstudio/ide/reference/properties-window)の [**色**] プロパティが使用されます。 詳細については、「 [256 色のアイコンまたはカーソルの作成](./creating-an-icon-or-other-image-image-editor-for-icons.md)」を参照してください。

True-カラーイメージを作成することもできます。 ただし、[ **色** ] ウィンドウの完全なパレットには実際の色のサンプルが表示されません。これらは、前景色または背景色のインジケーター領域にのみ表示されます。 実際の色は、[ **カスタムカラーセレクター** ] ダイアログボックスを使用して作成されます。

カスタマイズしたカラーパレットをディスクに保存し、必要に応じて再度読み込むことができます。 最近使用したカラーパレットはレジストリに保存され、次回 Visual Studio を起動したときに自動的に読み込まれます。

[ **色** ] ウィンドウには、次の2つの部分があります。

- 色 **パレット**。使用できる色を表す色のサンプルの配列です。 このサンプルを選択すると、グラフィックスツールを使用しているときに、前景色と背景色を選択できます。

- **カラーインジケーター**。画面および反転色の前景色と背景色を示します。

   ![色ウィンドウ](../windows/media/vccolorswindow.gif "vcColorsWindow")<br/>
   **色** ウィンドウ

> [!NOTE]
> **画面の色**と**反転色**ツールは、アイコンとカーソルでのみ使用できます。

[ **色** ] ウィンドウは、[ [イメージエディター] ツールバー](./image-editor-for-icons.md)で使用できます。

- [**色**] ウィンドウを表示するには、**イメージエディター**ペイン内を右クリックし、[**色ウィンドウの表示**] を選択するか、メニュー[イメージ](./image-editor-for-icons.md)の [  >  **色の表示] ウィンドウ**を開きます。

- [ **色** ] ウィンドウを非表示にするには、ウィンドウの固定を解除します (この操作により、ウィンドウが使用されていないときに自動的に非表示になります)。または、[ **閉じる** ] ボタンを選択します。

**カラー**パレットには、初期状態で16個の標準色が表示されます。 色を表示した場合は、独自の色を作成することもできます。 カスタマイズした色パレットを保存し、読み込むことができます。

[ **カスタムカラーセレクター** ] ダイアログボックスでは、次のプロパティを使用して、イメージに使用する色をカスタマイズできます。

|プロパティ|説明|
|--------------------------|--------------------------|
|**グラデーションの色の表示**|選択した色の値を変更します。<br/><br/>変更する色に十字線を置き、スライダーを上下に移動して色の輝度または RGB 値を変更します。|
|**輝度バー**|**グラデーションの色の表示**ボックスで選択した色の明るさを設定します。<br/><br/>白の矢印を選択して、明るさを上げるにはバーの上にドラッグします。 **色**ボックスには、選択した色と、設定した輝度の効果が表示されます。|
|**色**|定義している色の色合い (カラーホイール値) を一覧表示します。 値の範囲は 0 ~ 240 です。0は赤、60は黄色、120は緑、180は水色、200はマゼンタ、240は青です。|
|**Hue**|定義している色の色合い (カラーホイール値) を一覧表示します。 値の範囲は 0 ~ 240 です。0は赤、60は黄色、120は緑、180は水色、200はマゼンタ、240は青です。|
|**[鮮やかさ]**|定義している色の鮮やかさの値を指定します。 鮮やかさは、指定された色合いの色の量です。 値の範囲は 0 ~ 240 です。|
|**[明るさ]**|定義している色の明るさ (明るさ) を一覧表示します。 値の範囲は 0 ~ 240 です。|
|**赤**|定義している色の赤の値を指定します。 値の範囲は 0 ~ 255 です。|
|**緑**|定義している色の緑の値を指定します。 値の範囲は 0 ~ 255 です。|
|**青**|定義している色の青の値を指定します。 値の範囲は 0 ~ 255 です。|

カスタマイズした色を含む **カラー** パレットを保存して読み込むことができます。 既定では、Visual Studio を起動すると、最近使用した **色** パレットが自動的に読み込まれます。

> [!TIP]
> **イメージエディター**には既定の**色**パレットを復元する手段がないため、既定の**色**パレットは、既定の設定を簡単に復元できるように、*標準の pal*や既定の*pal*などの名前で保存してください。

[ **パレットカラーの読み込み** ] ダイアログボックスを使用すると、C++ プロジェクトで使用する次のプロパティを持つ特殊なカラーパレットを読み込むことができます。

|プロパティ|説明|
|-----------------|-----------------|
|**Look in**|ファイルまたはフォルダーを検索する場所を指定します。<br/><br/>矢印を選択して別の場所を選択するか、ツールバーのフォルダーアイコンを選択してレベルを上へ移動します。|
|**[ファイル名]**|開こうとするファイルの名前を入力する場所です。<br/><br/>以前に開いたファイルをすばやく見つけるには、ドロップダウンリストでファイル名を選択します (使用可能な場合)。<br/><br/>ファイルを検索している場合は、アスタリスク (*) をワイルドカードとして使用できます。 たとえば、「」と入力すると、 \* \* すべてのファイルの一覧を表示できます。 ファイルの完全なパス (たとえば、 *C:\My Documents\MyColorPalette.pal*や* \\ \NetworkServer\MyFolder\MyColorPalette.pal*) を入力することもできます。|
|[**ファイルの種類**]|表示するファイルの種類を一覧表示します。<br/><br/>パレット (* pal) は、カラーパレットの既定のファイルの種類です。|

## <a name="how-to"></a>操作方法

### <a name="to-select-foreground-or-background-colors"></a>前景色または背景色を選択するには

**消しゴム**を除き、[**イメージエディター** ] ツールバーのツールは、左または右のマウスボタンを押すと、現在の前景色または背景色で描画されます。

- 前景色を選択するには、マウスの左ボタンを使用し **て、色パレットで** 目的の色を選択します。

- 背景色を選択するには、マウスの右ボタンで、 **色** パレットで目的の色を選択します。

### <a name="to-fill-a-bounded-area-of-an-image-with-a-color"></a>イメージの境界領域に色を設定するには

**イメージエディター**には、現在の描画色または現在の背景色で囲まれたイメージ領域を塗りつぶすための**塗りつぶし**ツールが用意されています。

### <a name="to-use-the-fill-tool"></a>Fill ツールを使用するには

1. [**イメージエディター** ] ツールバーを使用するか、[メニュー**イメージ**  >  **ツール**] にアクセスして [**塗りつぶし**] ツールを選択します。

1. 必要に応じて、[描画色] を選択します。 [色パレット](./image-editor-for-icons.md)で、マウスの左ボタンを選択して前景色を選択するか、マウスの右ボタンをクリックして背景色を選択します。

1. 塗りつぶしを行う領域に **塗りつぶし** ツールを移動します。

1. マウスの左ボタンまたは右ボタンを選択して、前景色または背景色をそれぞれ塗りつぶします。

### <a name="to-pick-up-a-color-from-an-image-to-use-elsewhere"></a>イメージから色を取得して他の場所で使用するには

**[色の選択**] または [カラーピックアップ] ツールは、左または右のマウスボタンを押すかどうかに応じて、画像の色を現在の前景色または背景色にします。 **[色の選択**] ツールを取り消すには、別のツールを選択します。

1. [**イメージエディター** ] ツールバーを使用するか、メニュー**イメージ**  >  **ツール**にアクセスして、[**色の選択**] ツールを選択します。

1. 画像から取得する色を選択します。

   > [!NOTE]
   > 色を選択すると、 **イメージエディター** によって、最近使用したツールが再アクティブ化されます。

1. 前景色にマウスの左ボタンを使用するか、背景色にマウスの右ボタンを使用して描画します。

### <a name="to-choose-the-background"></a>背景を選択するには

イメージから選択項目を移動またはコピーすると、現在の背景色に一致する選択範囲のピクセルは、既定では透明になり、ターゲットの場所のピクセルは見えなくなります。

透明な背景 (既定) から不透明な背景に切り替えて、もう一度戻ることができます。 選択ツールを使用すると、[**イメージエディター** ] ツールバーの**オプション**セレクターに [**透明な背景**] オプションと [**不透明な背景**] オプションが表示されます。

![背景オプション &#45; 不透明または透明](../windows/media/vcimageeditoropaqtranspback.gif "背景オプション &#45; 不透明または透明")<br/>
[**イメージエディター] ツールバー**の**透明なオプションと不透明なオプション**

#### <a name="to-switch-between-a-transparent-and-opaque-background"></a>透明な背景と不透明な背景を切り替えるには

[ **イメージエディター** ] ツールバーで、 **オプション** セレクターを選択し、適切な背景を選択します。

- **不透明な背景 (O)**: 既存のイメージは、選択範囲のすべての部分で隠されています。

- **透明な背景 (T)**: 既存のイメージは、現在の背景色に一致する選択範囲の一部を示します。

> [!TIP]
> ショートカットの場合は、[ **イメージ** ] メニューの [ **不透明な描画**] をオンまたはオフにします。

背景色は、選択が既に有効になっている間に変更して、画像のどの部分を透明にするかを変更できます。

### <a name="to-invert-the-colors-in-a-selection"></a>選択範囲の色を反転するには

イメージ **エディター** を使用すると、画像が反転色でどのように表示されるかを指定できるように、イメージの選択部分の色を反転することができます。

現在の選択範囲の色を反転するには、[メニュー**イメージ**の色の反転] にアクセスし  >  **Invert Colors**ます。

### <a name="to-customize-or-change-colors-on-the-colors-palette"></a>色パレットの色をカスタマイズまたは変更するには

1. メニュー**イメージ**の [  >  **色の調整**] にジャンプします。

1. [ **カスタムカラーセレクター** ] ダイアログボックスで、適切なテキストボックスに「RGB 値または HSL 値」と入力するか、[ **グラデーションの色] 表示** ボックスで色を選択して、色を定義します。

1. 輝度を設定するには、 **輝度** バーのスライダーを動かします。

1. 作成した色の多くは、ディザリングされます。 ディザーカラーに最も近い純色を使用する場合は、[ **色** ] ボックスをダブルクリックします。

   後でディザーカラーを使用する場合は、 **輝度** バーのスライダーを動かすか、[ **グラデーションの色] 表示** ボックスの十字線を再び移動して、ディザリングを復元します。

1. [ **OK** ] を選択して新しい色を追加します。

### <a name="to-save-a-custom-colors-palette"></a>カスタム カラー パレットを保存するには

1. メニュー**イメージ**の [  >  **パレットの保存**] を開きます。

1. パレットを保存するディレクトリに移動し、パレット名を入力します。

1. **[保存]** を選択します。

### <a name="to-load-a-custom-colors-palette"></a>カスタム カラー パレットを読み込むには

1. メニューイメージの**Image**  >  **読み込みパレット**にアクセスします。

1. [ **カラーパレットの読み込み** ] ダイアログボックスで、適切なディレクトリに移動し、読み込むパレットを選択します。 **カラー** パレットは、pal ファイル拡張子で保存されます。

## <a name="requirements"></a>必要条件

None

## <a name="see-also"></a>関連項目

[アイコン用イメージエディター](../windows/image-editor-for-icons.md)<br/>
[方法: アイコンまたはその他のイメージを作成する](../windows/creating-an-icon-or-other-image-image-editor-for-icons.md)<br/>
[方法: イメージを編集する](../windows/selecting-an-area-of-an-image-image-editor-for-icons.md)<br/>
[方法: 描画ツールを使用する](../windows/using-a-drawing-tool-image-editor-for-icons.md)<br/>
[アクセラレータキー](../windows/accelerator-keys-image-editor-for-icons.md)<br/>
