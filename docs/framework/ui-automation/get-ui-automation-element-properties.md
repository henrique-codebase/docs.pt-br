---
title: Obter propriedades de elemento da automação de interface do usuário
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties, retrieving
- UI Automation, retrieving properties of elements
ms.assetid: 09576b1a-291f-435c-980e-dee32d899ae1
ms.openlocfilehash: 1b82302ff89d2e8407871cbfba6c10e8322ac4e7
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74435505"
---
# <a name="get-ui-automation-element-properties"></a>Obter propriedades de elemento da automação de interface do usuário
> [!NOTE]
> Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico mostra como recuperar propriedades de um elemento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
### <a name="get-a-current-property-value"></a>Obter um valor da propriedade atual  
  
1. Obtenha o <xref:System.Windows.Automation.AutomationElement> cuja propriedade você deseja obter.  
  
2. Chame <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>ou recupere a estrutura da propriedade <xref:System.Windows.Automation.AutomationElement.Current%2A> e obtenha o valor de um de seus membros.  
  
### <a name="get-a-cached-property-value"></a>Obter um valor de propriedade em cache  
  
1. Obtenha o <xref:System.Windows.Automation.AutomationElement> cuja propriedade você deseja obter. A propriedade deve ter sido especificada no <xref:System.Windows.Automation.CacheRequest>.  
  
2. Chame <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>ou recupere a estrutura da propriedade <xref:System.Windows.Automation.AutomationElement.Cached%2A> e obtenha o valor de um de seus membros.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra várias maneiras de recuperar as propriedades atuais de um <xref:System.Windows.Automation.AutomationElement>.  
  
 [!code-csharp[UIAClient_snip#170](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#170)]
 [!code-vb[UIAClient_snip#170](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#170)]  
  
## <a name="see-also"></a>Consulte também

- [Propriedades de automação de interface do usuário para clientes](ui-automation-properties-for-clients.md)
- [Usar o cache em automação de interface do usuário](use-caching-in-ui-automation.md)
- [Armazenamento em cache em clientes de automação de interface do usuário](caching-in-ui-automation-clients.md)
