---
title: "CDCRenderTarget クラス |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-windows
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- CDCRenderTarget
- AFXRENDERTARGET/CDCRenderTarget
- AFXRENDERTARGET/CDCRenderTarget::CDCRenderTarget
- AFXRENDERTARGET/CDCRenderTarget::Attach
- AFXRENDERTARGET/CDCRenderTarget::BindDC
- AFXRENDERTARGET/CDCRenderTarget::Create
- AFXRENDERTARGET/CDCRenderTarget::Detach
- AFXRENDERTARGET/CDCRenderTarget::GetDCRenderTarget
- AFXRENDERTARGET/CDCRenderTarget::m_pDCRenderTarget
dev_langs:
- C++
helpviewer_keywords:
- CDCRenderTarget [MFC], CDCRenderTarget
- CDCRenderTarget [MFC], Attach
- CDCRenderTarget [MFC], BindDC
- CDCRenderTarget [MFC], Create
- CDCRenderTarget [MFC], Detach
- CDCRenderTarget [MFC], GetDCRenderTarget
- CDCRenderTarget [MFC], m_pDCRenderTarget
ms.assetid: aa8059c9-08e6-49e4-9b8c-00fa54077a61
caps.latest.revision: 16
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 4a770b6508067913aec51b8b3878f33e30eed4bb
ms.openlocfilehash: e195979967ac5422be67b634d44e2f5d1afa9263
ms.contentlocale: ja-jp
ms.lasthandoff: 10/09/2017

---
# <a name="cdcrendertarget-class"></a>CDCRenderTarget クラス
ID2D1DCRenderTarget のラッパーです。  
  
## <a name="syntax"></a>構文  
  
```  
class CDCRenderTarget : public CRenderTarget;  
```  
  
## <a name="members"></a>メンバー  
  
### <a name="public-constructors"></a>パブリック コンストラクター  
  
|名前|説明|  
|----------|-----------------|  
|[CDCRenderTarget::CDCRenderTarget](#cdcrendertarget)|CDCRenderTarget オブジェクトを構築します。|  
  
### <a name="public-methods"></a>パブリック メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[CDCRenderTarget::Attach](#attach)|既存の接続オブジェクトを対象のインターフェイスを表示します。|  
|[CDCRenderTarget::BindDC](#binddc)|描画コマンドを発行先デバイス コンテキスト レンダー ターゲットにバインドします。|  
|[CDCRenderTarget::Create](#create)|CDCRenderTarget を作成します。|  
|[CDCRenderTarget::Detach](#detach)|レンダー ターゲット インターフェイス オブジェクトからのデタッチします。|  
|[CDCRenderTarget::GetDCRenderTarget](#getdcrendertarget)|返します ID2D1DCRenderTarget インターフェイス|  
  
### <a name="public-operators"></a>パブリック演算子  
  
|名前|説明|  
|----------|-----------------|  
|[CDCRenderTarget::operator ID2D1DCRenderTarget *](#operator_id2d1dcrendertarget_star)|返します ID2D1DCRenderTarget インターフェイス|  
  
### <a name="protected-data-members"></a>プロテクト データ メンバー  
  
|名前|説明|  
|----------|-----------------|  
|[CDCRenderTarget::m_pDCRenderTarget](#m_pdcrendertarget)|ID2D1DCRenderTarget オブジェクトへのポインター。|  
  
## <a name="inheritance-hierarchy"></a>継承階層  
 [CObject](../../mfc/reference/cobject-class.md)  
  
 [CRenderTarget](../../mfc/reference/crendertarget-class.md)  
  
 [CDCRenderTarget](../../mfc/reference/cdcrendertarget-class.md)  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** afxrendertarget.h  
  
##  <a name="attach"></a>CDCRenderTarget::Attach  
 既存の接続オブジェクトを対象のインターフェイスを表示します。  
  
```  
void Attach(ID2D1DCRenderTarget* pTarget);
```  
  
### <a name="parameters"></a>パラメーター  
 `pTarget`  
 既存のレンダー ターゲット インターフェイスです。 NULL をすることはできません。  
  
##  <a name="binddc"></a>CDCRenderTarget::BindDC  
 描画コマンドを発行先デバイス コンテキスト レンダー ターゲットにバインドします。  
  
```  
BOOL BindDC(
    const CDC& dc,  
    const CRect& rect);
```  
  
### <a name="parameters"></a>パラメーター  
 `dc`  
 デバイス コンテキスト レンダー ターゲットが描画コマンドを発行するには  
  
 `rect`  
 レンダー ターゲットがバインドされているデバイス コンテキスト (HDC) へのハンドルのサイズ  
  
### <a name="return-value"></a>戻り値  
 メソッドが成功した場合は TRUE を返します。 それ以外の場合、FALSE を返します。  
  
##  <a name="cdcrendertarget"></a>CDCRenderTarget::CDCRenderTarget  
 CDCRenderTarget オブジェクトを構築します。  
  
```  
CDCRenderTarget();
```  
  
##  <a name="create"></a>CDCRenderTarget::Create  
 CDCRenderTarget を作成します。  
  
```  
BOOL Create(const D2D1_RENDER_TARGET_PROPERTIES& props);
```  
  
### <a name="parameters"></a>パラメーター  
 `props`  
 表示モード、ピクセル形式、リモート処理オプション、DPI 情報、およびハードウェアのレンダリングに必要な最小の DirectX サポートします。  
  
### <a name="return-value"></a>戻り値  
 メソッドが成功した場合は TRUE を返します。 それ以外の場合、FALSE を返します。  
  
##  <a name="detach"></a>CDCRenderTarget::Detach  
 レンダー ターゲット インターフェイス オブジェクトからのデタッチします。  
  
```  
ID2D1DCRenderTarget* Detach();
```  
  
### <a name="return-value"></a>戻り値  
 デタッチされたへのポインターは、対象のインターフェイスをレンダリングします。  
  
##  <a name="getdcrendertarget"></a>CDCRenderTarget::GetDCRenderTarget  
 返します ID2D1DCRenderTarget インターフェイス  
  
```  
ID2D1DCRenderTarget* GetDCRenderTarget();
```  
  
### <a name="return-value"></a>戻り値  
 ID2D1DCRenderTarget インターフェイスまたはオブジェクトがまだ初期化されていない場合は、NULL へのポインター。  
  
##  <a name="m_pdcrendertarget"></a>CDCRenderTarget::m_pDCRenderTarget  
 ID2D1DCRenderTarget オブジェクトへのポインター。  
  
```  
ID2D1DCRenderTarget* m_pDCRenderTarget;  
```  
  
##  <a name="operator_id2d1dcrendertarget_star"></a>CDCRenderTarget::operator ID2D1DCRenderTarget *  
 返します ID2D1DCRenderTarget インターフェイス  
  
```  
operator ID2D1DCRenderTarget*();
```   
  
### <a name="return-value"></a>戻り値  
 ID2D1DCRenderTarget インターフェイスまたはオブジェクトがまだ初期化されていない場合は、NULL へのポインター。  
  
## <a name="see-also"></a>関連項目  
 [クラス](../../mfc/reference/mfc-classes.md)
