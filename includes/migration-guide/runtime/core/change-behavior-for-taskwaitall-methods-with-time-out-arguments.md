---
ms.openlocfilehash: 94fad6fe910da6c528c5e13f529a6db274e07d5c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235099"
---
### <a name="change-in-behavior-for-taskwaitall-methods-with-time-out-arguments"></a>Mudança no comportamento de métodos Task.WaitAll com argumentos de tempo limite

|   |   |
|---|---|
|Detalhes|O comportamento de <xref:System.Threading.Tasks.Task.WaitAll%2A?displayProperty=nameWithType> ficou mais consistente no .NET Framework 4.5. No .NET Framework 4, esses métodos se comportavam de forma inconsistente. Quando o tempo limite expirou, se uma ou mais tarefas foram concluídas ou canceladas antes da chamada de método, o método lançou uma exceção <xref:System.AggregateException?displayProperty=name>. Quando o tempo limite expirava, se nenhuma tarefa tivesse sido concluída ou cancelada antes da chamada de método, mas uma ou mais tarefas tivessem entrado nesses estados após a chamada de método, o método retornava false.<br/><br/>No .NET Framework 4.5, essas sobrecargas de método agora retornam false se alguma tarefa ainda está em execução quando o intervalo de tempo limite expira e geram uma exceção <xref:System.AggregateException?displayProperty=name> somente se uma tarefa de entrada é cancelada (não importa se antes ou depois da chamada de método) e nenhuma outra tarefa ainda está em execução.|
|Sugestão|Se um <xref:System.AggregateException?displayProperty=name> era capturado como um meio de detectar uma tarefa cancelada antes da invocação da chamada de <xref:System.Threading.Tasks.Task.WaitAll%2A>, esse código deverá fazer a mesma detecção por meio da propriedade <xref:System.Threading.Tasks.Task.IsCanceled%2A> [por exemplo: .Any(t =&gt; t.IsCanceled)], porque o .NET Framework 4.6 acionará esse caso apenas se todas as tarefas esperadas forem concluídas antes do tempo limite.|
|Escopo|Secundário|
|Versão|4.5|
|Tipo|Tempo de execução|
|APIs afetadas|<ul><li><xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.Int32,System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.WaitAll(System.Threading.Tasks.Task[],System.TimeSpan)?displayProperty=nameWithType></li></ul>|
