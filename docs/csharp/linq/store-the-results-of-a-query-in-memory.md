---
title: Armazenar os resultados de uma consulta na memória
description: Como armazenar os resultados.
ms.date: 11/30/2016
ms.assetid: 5b863961-1750-4cf9-9607-acea5054d15a
ms.openlocfilehash: 66a7a95c74db4062e76c54d4339ccb7343f44067
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2020
ms.locfileid: "65633562"
---
# <a name="store-the-results-of-a-query-in-memory"></a>Armazenar os resultados de uma consulta na memória

Uma consulta é basicamente um conjunto de instruções sobre como recuperar e organizar os dados. As consultas são executadas lentamente, conforme cada item subsequente no resultado é solicitado. Quando você usa `foreach` para iterar os resultados, os itens são retornados conforme acessado. Para avaliar uma consulta e armazenar os resultados sem executar um loop `foreach`, basta chamar um dos métodos a seguir na variável de consulta:

- <xref:System.Linq.Enumerable.ToList%2A>

- <xref:System.Linq.Enumerable.ToArray%2A>

- <xref:System.Linq.Enumerable.ToDictionary%2A>

- <xref:System.Linq.Enumerable.ToLookup%2A>

 Recomendamos que ao armazenar os resultados da consulta, você atribua o objeto da coleção retornado a uma nova variável conforme mostrado no exemplo a seguir:

## <a name="example"></a>Exemplo

[!code-csharp[csProgGuideLINQ#25](~/samples/snippets/csharp/concepts/linq/how-to-store-the-results-of-a-query-in-memory_1.cs)]

## <a name="see-also"></a>Confira também

- [Consulta Integrada ao Idioma (LINQ)](index.md)
