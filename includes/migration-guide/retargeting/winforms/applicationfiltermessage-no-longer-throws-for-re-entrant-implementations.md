---
ms.openlocfilehash: 8a1e2ca0790cb62e3c2c879f2ba0bb169ef07d77
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67804316"
---
### <a name="applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a>Application.FilterMessage não é mais gerada para implementações de reentrância de IMessageFilter.PreFilterMessage

|   |   |
|---|---|
|Detalhes|Antes do .NET Framework 4.6.1, a chamada a uma <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> com uma <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> que chamava <xref:System.Windows.Forms.Application.AddMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> ou <xref:System.Windows.Forms.Application.RemoveMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> (ao chamar <xref:System.Windows.Forms.Application.DoEvents> também) causava uma <xref:System.IndexOutOfRangeException?displayProperty=name>.<p/>A partir dos aplicativos destinados ao .NET Framework 4.6.1, essa exceção não é mais gerada e filtros reentrantes, conforme descrito acima, podem ser usados.|
|Sugestão|Lembre-se de que <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)> não será mais gerado para o comportamento <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> reentrante descrito acima. Isso afeta somente os aplicativos destinados ao .NET Framework 4.6.1. Os aplicativos destinados ao .NET Framework 4.6.1 podem recusar essa alteração (ou os aplicativos de Frameworks mais antigos podem aceitar) usando a opção de compatibilidade [DontSupportReentrantFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md#mitigation).|
|Escopo|Microsoft Edge|
|Versão|4.6.1|
|Type|Redirecionando|
|APIs afetadas|<ul><li><xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)?displayProperty=nameWithType></li></ul>|
