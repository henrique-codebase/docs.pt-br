---
title: Parallel Programming in .NET (Programação paralela no .NET)
ms.date: 09/12/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- parallel programming
ms.assetid: 4d83c690-ad2d-489e-a2e0-b85b898a672d
ms.openlocfilehash: 75f5ded48acfb82b0327ead3880ee23e6ef4bc2f
ms.sourcegitcommit: 961ec21c22d2f1d55c9cc8a7edf2ade1d1fd92e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80588157"
---
# <a name="parallel-programming-in-net"></a>Parallel Programming in .NET (Programação paralela no .NET)

Muitos computadores pessoais e estações de trabalho têm vários núcleos de CPU, o que permite a execução simultânea de vários threads. Para tirar proveito do hardware, é possível paralelizar seu código para distribuir o trabalho entre vários processadores.

No passado, a paralelização exigia a manipulação em baixo nível de threads e de bloqueios. O Visual Studio e o .NET Framework aprimoram o suporte à programação paralela ao fornecer um runtime, tipos de biblioteca de classes e ferramentas de diagnóstico. Esses recursos, que foram introduzidos com o .NET Framework 4, simplificam o desenvolvimento paralelo. É possível escrever código paralelo eficiente, refinado e dimensionável em uma linguagem natural sem precisar trabalhar diretamente com threads ou o pool de threads.

A ilustração a seguir oferece uma visão geral de alto nível da arquitetura de programação paralela do .NET Framework:

![Arquitetura de programação paralela .NET](./media/tpl-architecture.png)

## <a name="related-topics"></a>Tópicos Relacionados

|Tecnologia|Descrição|
|----------------|-----------------|
|[Biblioteca de tarefas paralelas (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|Fornece documentação para a classe <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>, a qual inclui versões paralelas de `For` e loops `ForEach`, e também para a classe <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>, a qual representa a forma preferencial de expressar operações assíncronas.|
|[PLINQ (LINQ paralelo)](../../../docs/standard/parallel-programming/introduction-to-plinq.md)|Uma implementação paralela do LINQ em Objects que melhora significativamente o desempenho em muitos cenários.|
|[Estruturas de dados para programação paralela](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)|Fornece links para a documentação de classes de coleta com threads seguros, tipos de sincronização leves e tipos para inicialização lenta.|
|[Ferramentas de diagnóstico paralelo](../../../docs/standard/parallel-programming/parallel-diagnostic-tools.md)|Fornece links para a documentação de janelas do depurador para tarefas e pilhas paralelas, e para a [Visualização Simultânea](/visualstudio/profiling/concurrency-visualizer) do Visual Studio.|
|[Particionadores personalizados para PLINQ e TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)|Descreve como os particionadores funcionam e como configurar os particionadores padrão ou criar um novo particionador.|
|[Agendadores de tarefas](xref:System.Threading.Tasks.TaskScheduler)|Descreve como os agendadores funcionam e como os agendadores padrão podem ser configurados.|
|[Expressões lambda em PLINQ e TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)|Fornece uma visão geral das expressões lambda em C# e Visual Basic e mostra como elas são usadas em PLINQ e na Biblioteca Paralela de Tarefas.|
|[Para mais leituras](../../../docs/standard/parallel-programming/for-further-reading-parallel-programming.md)|Fornece links para informações adicionais e recursos de exemplo para a programação paralela no .NET.|

## <a name="see-also"></a>Confira também

- [Visão geral de Async](../async.md)
- [Rosnado gerenciado](../threading/index.md)
