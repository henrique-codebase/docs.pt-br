---
title: Como concatenar várias strings (Guia C#)
description: Há várias maneiras para concatenar cadeias de caracteres em C#. Conheça as opções e os motivos subjacentes por trás de diferentes escolhas.
ms.date: 02/20/2018
helpviewer_keywords:
- joining strings [C#]
- concatenating strings [C#]
- strings [C#], concatenation
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
ms.openlocfilehash: bbdeba4ee3526140de29ac0d7c97e9a593729d47
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389529"
---
# <a name="how-to-concatenate-multiple-strings-c-guide"></a>Como concatenar várias strings (Guia C#)

*Concatenação* é o processo de acrescentar uma cadeia de caracteres ao final de outra cadeia de caracteres. Você concatena cadeias de caracteres usando o operador `+`. Para literais de cadeia de caracteres e constantes de cadeia de caracteres, a concatenação ocorre em tempo de compilação; não ocorre nenhuma concatenação de tempo de execução. Para variáveis de cadeia de caracteres, a concatenação ocorre somente em tempo de execução.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

O exemplo a seguir usa a concatenação para dividir um literal de cadeia de caracteres longo em cadeias de caracteres menores, a fim de melhorar a legibilidade no código-fonte. Essas partes são concatenadas em uma única cadeia de caracteres em tempo de compilação. Não há custos de desempenho em tempo de execução, independentemente da quantidade de cadeias de caracteres envolvidas.  
  
 [!code-csharp-interactive[Combining strings at compile time](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#1)]  

Para concatenar variáveis de seqüência, você pode usar <xref:System.String.Format%2A?displayProperty=nameWithType> <xref:System.String.Concat%2A?displayProperty=nameWithType>os <xref:System.String.Join%2A?displayProperty=nameWithType> `+` ou `+=` operadores, [interpolação de cordas](../language-reference/tokens/interpolated.md) ou os métodos ou <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> métodos. O operador `+` é fácil de usar e torna o código intuitivo. Mesmo ao usar vários operadores `+` em uma instrução, o conteúdo da cadeia de caracteres será copiado apenas uma vez. O código a seguir mostra dois exemplos de como usar os operadores `+` e `+=` para concatenar cadeias de caracteres:

[!code-csharp-interactive[combining strings using +](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#2)]  

Em algumas expressões, é mais fácil concatenar cadeias de caracteres usando a interpolação de cadeia de caracteres, conforme mostra o seguinte código:
  
[!code-csharp-interactive[building strings using string interpolation](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#3)]  
  
> [!NOTE]
> Em operações de concatenação de cadeia de caracteres, o compilador C# trata uma cadeia de caracteres nula da mesma maneira que uma cadeia de caracteres vazia.

Outro método para concatenar cadeias de caracteres é o <xref:System.String.Format%2A?displayProperty=nameWithType>. Esse método funciona bem quando você está criando uma cadeia de caracteres com base em um pequeno número de cadeias de caracteres de componente.

Em outros casos, você pode estar combinando strings em um loop onde você não sabe quantas strings de origem você está combinando, e o número real de strings de origem pode ser grande. A classe <xref:System.Text.StringBuilder> foi projetada para esses cenários. O código a seguir usa o método <xref:System.Text.StringBuilder.Append%2A> da classe <xref:System.Text.StringBuilder> para concatenar cadeias de caracteres.  
  
[!code-csharp-interactive[string concatenation using string builder](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#4)]  

Você pode ler mais sobre as [razões `StringBuilder` para escolher a concatenação de cordas ou a classe](xref:System.Text.StringBuilder#StringAndSB).

Outra opção para unir cadeias de caracteres de uma coleção é usar o método <xref:System.String.Concat%2A?displayProperty=nameWithType>. Use <xref:System.String.Join%2A?displayProperty=nameWithType> o método se as seqüências de origem devem ser separadas por um delimitador. O código a seguir combina uma matriz de palavras usando os dois métodos:

[!code-csharp-interactive[concatenation of string collection](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#5)]

Por fim, você pode usar [LINQ](../programming-guide/concepts/linq/index.md) e o método <xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=nameWithType> para unir cadeias de caracteres de uma coleção. Esse método combina as cadeias de caracteres de origem usando uma expressão lambda. A expressão lambda faz o trabalho de adicionar cada cadeia de caracteres ao acúmulo existente. O exemplo a seguir combina uma matriz de palavras, adicionando um espaço entre cada palavra na matriz:

[!code-csharp-interactive[string concatenation using LINQ expressions](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#6)]  

Você pode experimentar essas amostras olhando para o código da [amostra](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings). Ou, você pode baixar as amostras [como um arquivo zip](../../../samples/snippets/csharp/how-to/strings.zip).

## <a name="see-also"></a>Confira também

- <xref:System.String>
- <xref:System.Text.StringBuilder>
- [C# Guia de Programação](../programming-guide/index.md)
- [Cadeias de caracteres](../programming-guide/strings/index.md)
