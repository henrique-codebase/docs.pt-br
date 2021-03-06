---
title: 'Como: Valores de data e hora de viagem de ida e volta'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- round-trip date and time values
- dates [.NET Framework], round-trip values
- time zones [.NET Framework], round-trip date and time values
- time [.NET Framework], round-trip values
- formatting strings [.NET Framework], round-trip values
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
ms.openlocfilehash: 3aa615dc7d7d1d49dce4897f8508b5210b364fc0
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635132"
---
# <a name="how-to-round-trip-date-and-time-values"></a>Como: Valores de data e hora de viagem de ida e volta

Em muitos aplicativos, um valor de data e hora destina-se a identificar sem ambiguidade um único ponto no tempo. Este artigo mostra como salvar <xref:System.DateTime> e <xref:System.DateTimeOffset> restaurar um valor, um valor e um valor de data e hora com informações de fuso horário para que o valor restaurado identifique o mesmo tempo que o valor salvo.

## <a name="round-trip-a-datetime-value"></a>Ida e volta um valor datetime

1. Converta o valor <xref:System.DateTime> em sua representação de cadeia de caracteres chamando o método <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> com o especificador de formato "o".

2. Salve a representação de cadeia de caracteres do valor <xref:System.DateTime> em um arquivo ou passe-a por um processo, domínio de aplicativo ou limite de computador.

3. Recupere a cadeia de caracteres que representa o valor <xref:System.DateTime>.

4. Chame o método <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> e passe <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> como o valor do parâmetro `styles`.

O exemplo a seguir mostra como fazer a viagem de ida e volta de um valor <xref:System.DateTime>.

[!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
[!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]

Fazendo a viagem de ida e volta de um valor <xref:System.DateTime>, essa técnica consegue preservar o horário para todos os horários locais e universais. Por exemplo, se <xref:System.DateTime> um valor local é salvo em um sistema no fuso horário padrão do Pacífico dos EUA e é restaurado em um sistema no fuso horário padrão padrão dos EUA, a data e hora restauradas serão duas horas mais tarde do que o horário original, o que reflete a diferença de tempo entre os dois fusos horários. No entanto, essa técnica não é necessariamente exata para horários não especificados. Todos os valores <xref:System.DateTime> cuja propriedade <xref:System.DateTime.Kind%2A> é <xref:System.DateTimeKind.Unspecified> são tratados como se fossem horários locais. Se não for uma hora <xref:System.DateTime> local, não identificará com sucesso o ponto correto no tempo. A solução alternativa para essa limitação é acoplar rigorosamente um valor de data e hora com seu fuso horário para salvar e restaurar a operação.

## <a name="round-trip-a-datetimeoffset-value"></a>Ida e volta um valor DateTimeOffset

1. Converta o valor <xref:System.DateTimeOffset> em sua representação de cadeia de caracteres chamando o método <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> com o especificador de formato "o".

2. Salve a representação de cadeia de caracteres do valor <xref:System.DateTimeOffset> em um arquivo ou passe-a por um processo, domínio de aplicativo ou limite de computador.

3. Recupere a cadeia de caracteres que representa o valor <xref:System.DateTimeOffset>.

4. Chame o método <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> e passe <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> como o valor do parâmetro `styles`.

O exemplo a seguir mostra como fazer a viagem de ida e volta de um valor <xref:System.DateTimeOffset>.

[!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
[!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]

Essa técnica sempre identifica sem ambiguidade um valor <xref:System.DateTimeOffset> como um único momento. O valor pode ser convertido em UTC (Tempo Universal Coordenado) chamando o método <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> ou pode ser convertido em determinado fuso horário chamando o método <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> ou <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType>. A principal limitação dessa técnica é que a aritmética de data e hora, quando executada em um valor <xref:System.DateTimeOffset> que representa o horário em determinado fuso horário, talvez não produza resultados precisos para esse fuso horário. Isso ocorre porque, quando um valor <xref:System.DateTimeOffset> é instanciado, é dissociado do fuso horário. Portanto, as regras de ajuste do fuso horário não podem mais ser aplicadas quando você executa cálculos de data e hora. É possível solucionar esse problema definindo um tipo personalizado que inclui um valor de data e hora e o respectivo fuso horário.

## <a name="round-trip-a-date-and-time-value-with-its-time-zone"></a>Ida e volta um valor de data e hora com seu fuso horário

1. Defina uma classe ou uma estrutura com dois campos. O primeiro campo é um objeto <xref:System.DateTime> ou <xref:System.DateTimeOffset>, e o segundo é um objeto <xref:System.TimeZoneInfo>. O exemplo a seguir é uma versão simples desse tipo.

    [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
    [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]

2. Marcar a classe com o atributo <xref:System.SerializableAttribute>.

3. Serialize o objeto usando o método <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>.

4. Restaure o objeto usando o método <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A>.

5. Transmita (em C#) ou converta (em Visual Basic) o objeto desserializado em um objeto do tipo apropriado.

O exemplo a seguir ilustra como fazer uma viagem de ida e volta a um objeto que armazena tanto o fuso horário quanto as informações de data e hora.

[!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
[!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]

Essa técnica deve refletir sempre inequivocamente o ponto no tempo correto, antes e depois de ser salvo e restaurado, desde que a implementação do objeto combinado de data e hora e fuso horário não permita que o valor de data fique fora de sincronia com o valor de fuso horário.

## <a name="compile-the-code"></a>Compilar o código

Esses exemplos exigem que:

- Os seguintes namespaces serão `using` importados com `Imports` diretivas C# ou instruções Básicas Visuais:

  - <xref:System>(Somente C)

  - <xref:System.Globalization?displayProperty=nameWithType>

  - <xref:System.IO?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=nameWithType>

- Cada exemplo de código, diferente da `DateInTimeZone` classe, será incluído em uma classe ou `Main` módulo Visual Basic, embrulhado em métodos, e chamado a partir do método.

## <a name="see-also"></a>Confira também

- [Escolhendo entre DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)
- [Cadeias de caracteres de formato de data e hora padrão](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
