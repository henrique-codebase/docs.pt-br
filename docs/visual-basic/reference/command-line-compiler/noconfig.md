---
title: -noconfig
ms.date: 03/13/2018
helpviewer_keywords:
- noconfig compiler option [Visual Basic]
- -noconfig compiler option [Visual Basic]
- /noconfig compiler option [Visual Basic]
ms.assetid: a7405067-bd21-4171-adf4-a126fa3ad6c3
ms.openlocfilehash: c57ed1699d110959e9faf3dc3d43bcc200851c1c
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005440"
---
# <a name="-noconfig"></a>-noconfig
Especifica que o compilador não deve referenciar automaticamente os assemblies de .NET Framework usados com frequência `System` ou `Microsoft.VisualBasic` importar os namespaces e.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-noconfig  
```  
  
## <a name="remarks"></a>Comentários  
 A `-noconfig` opção informa o compilador para não compilar com o arquivo Vbc. rsp, que está localizado no mesmo diretório que o arquivo Vbc. exe. O arquivo Vbc. rsp faz referência aos assemblies de .NET Framework usados com frequência `System` e `Microsoft.VisualBasic` importa os namespaces e. O compilador referencia implicitamente o assembly System. dll, a `-nostdlib` menos que a opção seja especificada. A `-nostdlib` opção informa o compilador para não compilar com Vbc. rsp ou referenciar automaticamente o assembly System. dll.  
  
> [!NOTE]
> Os assemblies mscorlib. dll e Microsoft. VisualBasic. dll são sempre referenciados.  
  
 Você pode modificar o arquivo Vbc. rsp para especificar opções adicionais do compilador que devem ser incluídas em cada compilação do Vbc. exe (exceto ao `-noconfig` especificar a opção). Para obter mais informações, confira [@ (Especificar de arquivo de resposta)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md).  
  
 O compilador processa as opções passadas para `vbc` o comando por último. Portanto, qualquer opção na linha de comando substitui a configuração da mesma opção no arquivo Vbc. rsp.  
  
> [!NOTE]
> A `-noconfig` opção não está disponível no ambiente de desenvolvimento do Visual Studio; Ele está disponível somente durante a compilação na linha de comando.  
  
## <a name="see-also"></a>Veja também

- [-nostdlib (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nostdlib.md)
- [Compilador de linha de comando do Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [Em (Especificar arquivo de resposta)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)
- [-referência (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
