---
title: "Cdynamicaccessor::getcolumnname |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ATL::CDynamicAccessor::GetColumnName
- GetColumnName
- ATL.CDynamicAccessor.GetColumnName
- CDynamicAccessor::GetColumnName
- CDynamicAccessor.GetColumnName
dev_langs: C++
helpviewer_keywords: GetColumnName method
ms.assetid: 96a7452a-1f5b-41e9-ab37-88dac026f961
caps.latest.revision: "8"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload:
- cplusplus
- data-storage
ms.openlocfilehash: 57d0a7b494fb2222db0a29b4fdc7def7a8aac057
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2017
---
# <a name="cdynamicaccessorgetcolumnname"></a>CDynamicAccessor::GetColumnName
指定された列の名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
      LPOLESTR GetColumnName(   
   DBORDINAL nColumn    
) const throw( );  
```  
  
#### <a name="parameters"></a>パラメーター  
 `nColumn`  
 [in]列番号。 列番号は、1 から始まります。 値 0 は、存在する場合に、ブックマーク列を参照します。  
  
## <a name="return-value"></a>戻り値  
 指定された列の名前。  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** atldbcli.h  
  
## <a name="see-also"></a>参照  
 [CDynamicAccessor クラス](../../data/oledb/cdynamicaccessor-class.md)