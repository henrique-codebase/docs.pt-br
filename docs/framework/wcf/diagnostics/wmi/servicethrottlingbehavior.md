---
title: ServiceThrottlingBehavior
ms.date: 03/30/2017
ms.assetid: 37b9e517-1f1f-4ec4-9fcb-2b8016794f5b
ms.openlocfilehash: 572e458f08c4717207667db9940296c4a957199a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956865"
---
# <a name="servicethrottlingbehavior"></a>ServiceThrottlingBehavior
ServiceThrottlingBehavior  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp  
class ServiceThrottlingBehavior : Behavior  
{  
  sint32 MaxConcurrentCalls;  
  sint32 MaxConcurrentInstances;  
  sint32 MaxConcurrentSessions;  
};  
```  
  
## <a name="methods"></a>Métodos  
 A classe ServiceThrottlingBehavior não define quaisquer métodos.  
  
## <a name="properties"></a>Propriedades  
 A classe ServiceThrottlingBehavior tem as seguintes propriedades:  
  
### <a name="maxconcurrentcalls"></a>MaxConcurrentCalls  
 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de mensagens processando ativamente entre todos os objetos de dispatcher em um ServiceHost.  
  
### <a name="maxconcurrentinstances"></a>MaxConcurrentInstances  
 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de objetos de serviço que podem ser executadas ao mesmo tempo.  
  
### <a name="maxconcurrentsessions"></a>MaxConcurrentSessions  
 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de sessões que um host pode aceitar simultaneamente.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em Servicemodel.mof.|  
|---------|-----------------------------------|  
|Namespace|Definido no root\ServiceModel|  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
