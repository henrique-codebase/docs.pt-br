---
title: Método ISymUnmanagedScope::GetParent
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetParent
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetParent
helpviewer_keywords:
- GetParent method [.NET Framework debugging]
- ISymUnmanagedScope::GetParent method [.NET Framework debugging]
ms.assetid: c7963c87-6ec5-49b3-a5cd-e0fe0c43f9b4
topic_type:
- apiref
ms.openlocfilehash: 95ae081d61200e4fd020609a4d23783f265d2cc6
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615352"
---
# <a name="isymunmanagedscopegetparent-method"></a>Método ISymUnmanagedScope::GetParent
Obtém o escopo pai deste escopo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetParent(  
    [out, retval] ISymUnmanagedScope** pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 fora Um ponteiro para a interface [ISymUnmanagedScope](isymunmanagedscope-interface.md) retornada.  
  
## <a name="return-value"></a>Valor retornado  
 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Veja também

- [Interface ISymUnmanagedScope](isymunmanagedscope-interface.md)
- [Método GetChildren](isymunmanagedscope-getchildren-method.md)
