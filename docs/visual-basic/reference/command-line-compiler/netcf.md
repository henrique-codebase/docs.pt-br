---
title: -netcf
ms.date: 03/13/2018
f1_keywords:
- /netcf
- -netcf
helpviewer_keywords:
- -netcf compiler option [Visual Basic]
- netcf compiler option [Visual Basic]
- /netcf compiler option [Visual Basic]
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
ms.openlocfilehash: 7f14ce07a2928f4dbffd3aa57f8cdd514b75694c
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716710"
---
# <a name="-netcf"></a>-netcf

Define o compilador para o .NET Compact Framework de destino.

## <a name="syntax"></a>Sintaxe

```console
-netcf
```

## <a name="remarks"></a>Comentários

A `-netcf` opção faz com que o compilador de Visual Basic direcione o .NET Compact Framework em vez do .NET Framework completo. A funcionalidade de idioma que está presente somente no .NET Framework completo está desabilitada.

A `-netcf` opção foi projetada para ser usada com [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md). Os recursos de idioma desabilitados pelo `-netcf` são os mesmos recursos de linguagem que não estão presentes `-sdkpath`nos arquivos de destino com o.

> [!NOTE]
> A `-netcf` opção não está disponível no ambiente de desenvolvimento do Visual Studio; Ele está disponível somente durante a compilação na linha de comando. A `-netcf` opção é definida quando um projeto de dispositivo Visual Basic é carregado.

A `-netcf` opção altera os seguintes recursos de idioma:

- A [palavra \<-chave end keyword>](../../../visual-basic/language-reference/statements/end-keyword-statement.md) palavra-chave Statement, que encerra a execução de um programa, está desabilitada. O programa a seguir compila e executa sem `-netcf` , mas falha no momento da compilação `-netcf`com.

  [!code-vb[VbVbalrCompiler#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/netcf.vb#34)]

- A associação tardia, em todos os formulários, está desabilitada. Erros de tempo de compilação são gerados quando cenários de ligação tardia reconhecidos são encontrados. O programa a seguir compila e executa sem `-netcf` , mas falha no momento da compilação `-netcf`com.

  [!code-vb[VbVbalrCompiler#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#35)]

- Os modificadores [auto](../../../visual-basic/language-reference/modifiers/auto.md), [ANSI](../../../visual-basic/language-reference/modifiers/ansi.md)e [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) estão desabilitados. A sintaxe da [instrução Declare](../../../visual-basic/language-reference/statements/declare-statement.md) também é modificada para `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`. O código a seguir mostra o efeito `-netcf` de em uma compilação.

  [!code-vb[VbVbalrCompiler#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#36)]

- Usar as palavras-chave Visual Basic 6,0 que foram removidas do Visual Basic gera um `-netcf` erro diferente quando é usado. Isso afeta as mensagens de erro para as seguintes palavras-chave:

  - `Open`

  - `Close`

  - `Put`

  - `Print`

  - `Write`

  - `Input`

  - `Lock`

  - `Unlock`

  - `Seek`

  - `Width`

  - `Name`

  - `FreeFile`

  - `EOF`

  - `Loc`

  - `LOF`

  - `Line`

## <a name="example"></a>Exemplo

O código a seguir é compilado `Myfile.vb` com o .NET Compact Framework, usando as versões de mscorlib. dll e Microsoft. VisualBasic. dll encontrados no diretório de instalação padrão do .NET Compact Framework na unidade C. Normalmente, você usaria a versão mais recente do .NET Compact Framework.

```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb
```

## <a name="see-also"></a>Veja também

- [Compilador de linha de comando do Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [Linhas de Comando de Compilação de Exemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
