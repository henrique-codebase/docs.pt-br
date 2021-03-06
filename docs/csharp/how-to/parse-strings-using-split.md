---
title: Como analisar strings usando String.Split (Guia C#)
description: O String.Split retorna uma matriz de divisão de cadeias de caracteres com base em um conjunto de delimitadores. Esta á uma maneira fácil de analisar cadeias de caracteres.
ms.date: 01/03/2018
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
ms.custom: mvc
ms.openlocfilehash: cf8307517213b54041b272843232eb595660b2e9
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389498"
---
# <a name="how-to-parse-strings-using-stringsplit-in-c"></a>Como analisar strings usando String.Split em C\#

O método <xref:System.String.Split%2A?displayProperty=nameWithType> cria uma matriz de subcadeias, dividindo a cadeia de caracteres de entrada com base em um ou mais delimitadores. Geralmente essa é a maneira mais fácil de separar uma cadeia de caracteres em limites de palavra. Ele também é usado para dividir cadeias de caracteres em outros caracteres específicos ou cadeias de caracteres.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

O código a seguir divide uma frase comum em uma matriz de cadeias de caracteres para cada palavra.

[!code-csharp-interactive[split strings on word boundaries](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#1)]

Cada instância de um caractere separador produz um valor na matriz retornada. Caracteres separadores consecutivos produzem a cadeia de caracteres vazia como um valor na matriz retornada. Você pode ver como uma seqüência de caracteres vazia é criada no exemplo a seguir, que usa o caractere espaço como um separador.

[!code-csharp-interactive[split strings with repeated separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#2)]

Esse comportamento facilita para formatos como arquivos csv (valores separados por comma) que representam dados tabulares. Vírgulas consecutivas representam uma coluna em branco.

Você pode passar um parâmetro <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> opcional para excluir as cadeias de caracteres vazias da matriz retornada. Para um processamento mais complicado da coleção retornada, você pode usar o [LINQ](../programming-guide/concepts/linq/index.md) para manipular a sequência de resultado.

O <xref:System.String.Split%2A?displayProperty=nameWithType> pode usar vários caracteres separadores.
O exemplo a seguir utiliza espaços, vírgulas, pontos, dois-pontos e tabulações, todos passados em uma matriz que contém esses caracteres de separação para <xref:System.String.Split%2A>.
O loop, na parte inferior do código, exibe cada uma das palavras na matriz retornada.  

[!code-csharp-interactive[split strings using multiple separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#3)]

As instâncias consecutivas de qualquer separador produzem a cadeia de caracteres vazia na matriz de saída:

[!code-csharp-interactive[split strings using multiple consecutive separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#4)]

O <xref:System.String.Split%2A?displayProperty=nameWithType> pode receber uma matriz de cadeias de caracteres (sequências de caracteres que atuam como separadores para analisar a cadeia de caracteres de destino, em vez de um único caractere).  
  
[!code-csharp-interactive[split strings using strings as separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#5)]

Você pode experimentar essas amostras olhando para o código em nosso [repositório GitHub](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings). Ou então, você pode baixar os exemplos [como um arquivo zip](../../../samples/snippets/csharp/how-to/strings.zip).

## <a name="see-also"></a>Confira também

- [C# Guia de Programação](../programming-guide/index.md)
- [Cadeias de caracteres](../programming-guide/strings/index.md)
- [Expressões regulares do .NET](../../standard/base-types/regular-expressions.md)
