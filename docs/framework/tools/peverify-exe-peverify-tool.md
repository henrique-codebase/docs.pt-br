---
title: Peverify.exe (Ferramenta PEVerify)
ms.date: 03/30/2017
helpviewer_keywords:
- portable executable files, PEVerify
- verifying MSIL and metadata
- PEVerify tool
- type safety requirements
- MSIL
- PEverify.exe
- PE files, PEVerify
ms.assetid: f4f46f9e-8d08-4e66-a94b-0c69c9b0bbfa
ms.openlocfilehash: 9d5f8c80937c36e975d42d6efb0a83295cb28be9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "73104975"
---
# <a name="peverifyexe-peverify-tool"></a>Peverify.exe (Ferramenta PEVerify)
A ferramenta PEVerify ajuda desenvolvedores que geram MSIL (Microsoft Intermediate Language) (como gravadores de compiladores, desenvolvedores de mecanismos de script etc.) a determinar se o código MSIL e os metadados associados atendem aos requisitos de segurança de tipo. Alguns compiladores só gerarão código fortemente tipado verificável se você evitar usar determinados constructos de linguagem. Se, como desenvolvedor, estiver usando um compilador assim, você talvez queira verificar se não comprometeu a segurança de tipo do código. Nessa situação, é possível executar a ferramenta PEVerify nos arquivos para verificar MSIL e metadados.  
  
 Essa ferramenta é instalada automaticamente com o Visual Studio. Para executar a ferramenta, use o Prompt de Comando do Desenvolvedor para Visual Studio (ou o Prompt de Comando do Visual Studio no Windows 7). Para obter mais informações, consulte [Prompts de Comando](developer-command-prompt-for-vs.md).  
  
 No prompt de comando, digite o seguinte:  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
peverify filename [options]  
```  
  
## <a name="parameters"></a>parâmetros  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|*Filename*|O arquivo PE (Portable Executable) para o qual MSIL e metadados devem ser verificados.|  
  
|Opção|Descrição|  
|------------|-----------------|  
|**/break=** *maxErrorCount*|Anula a verificação depois de erros *maxErrorCount*.<br /><br /> Esse parâmetro não é compatível no .NET Framework versão 2.0 ou posterior.|  
|**/relógio**|Mede e relata os seguintes tempos de verificação em milissegundos:<br /><br /> **MD Val. cycle**<br /> Ciclo de validação dos metadados<br /><br /> **MD Val. pure**<br /> Validação dos metadados pura<br /><br /> **IL Ver. cycle**<br /> Ciclo de verificação MSIL<br /><br /> **IL Ver pure**<br /> Verificação MSIL pura<br /><br /> Os tempos de **MD Val. cycle** e **IL Ver. cycle** incluem o tempo necessário para a realização de procedimentos de inicialização e desligamento necessários. Os tempos de **MD Val. pure** e **IL Ver pure** refletem o tempo necessário para a realização da validação ou apenas da verificação.|  
|**/help**|Exibe sintaxe de comando e opções para a ferramenta.|  
|**/hresult**|Exibe códigos de erro em formato hexadecimal.|  
|**/ignore=** *hex.code* [, *hex.code*]|Ignora os códigos de erro especificados.|  
|**/ignore=@** *responseFile*|Ignora os códigos de erro listados no arquivo de resposta especificado.|  
|**(iI).**|Realiza verificação de segurança do tipo MSIL dos métodos implementados no assembly especificado por *filename*. A ferramenta retorna descrições detalhadas para cada problema encontrado, a menos que você especifique a opção **/quiet**.|  
|**/md**|Realiza verificações de validação de metadados no assembly especificado por *filename*. Isso analisa a estrutura de metadados completa dentro do arquivo e relata todos os problemas de validação encontrados.|  
|**/nologo**|Suprime a exibição da versão do produto e as informações de direitos autorais.|  
|**/nosymbols**|No .NET Framework versão 2.0, suprime números de linha para compatibilidade com versões anteriores.|  
|**/quiet**|Especifica o modo silencioso; suprime saída dos relatórios de problema de verificação. Peverify.exe ainda relata se o arquivo é fortemente tipado, mas não relata informações sobre problemas que impeçam a verificação de segurança do tipo.|  
|`/transparent`|Verifique apenas os métodos transparentes.|  
|**/único**|Ignora códigos de erro repetidos.|  
|**/verbose**|No .NET Framework versão 2.0, exibe informações adicionais em mensagens de verificação MSIL.|  
|**/?**|Exibe sintaxe de comando e opções para a ferramenta.|  
  
## <a name="remarks"></a>Comentários  
 O Common Language Runtime depende na execução fortemente tipada do código de aplicativo para ajudar a impor mecanismos de segurança e isolamento. Normalmente, o código que não é [fortemente tipado verificável](../../standard/security/key-security-concepts.md#type-safety-and-security) não pode ser executado, embora seja possível definir a política de segurança para permitir a execução de código confiável, mas não verificável.  
  
 Se as opções **/md** ou **/il** não forem especificadas, Peverify.exe realizará ambos os tipos de verificações. Peverify.exe realiza as verificações de **/md** primeiro. Se não houver erros, as verificações de **/il** serão feitas. Se você especificar **/md** e **/il**, as verificações de **/il** serão feitas mesmo se houver erros nos metadados. Por isso, se não houver erros de metadados, **peverify** *filename* equivalerá a **peverify** *filename* **/md** **/il**.  
  
 Peverify.exe realiza verificações MSIL abrangentes com base na análise do fluxo de dados mais uma lista de várias centenas de regras em metadados válidos. Saiba mais sobre as verificações realizadas por Peverify.exe em "Especificação de Validação dos Metadados" e em "Especificação do Conjunto de Instruções MSIL" na pasta Guia de Desenvolvedores de Ferramentas no SDK do Windows.  
  
 Observe que o .NET Framework versão 2.0 ou posterior dá suporte a retornos de `byref` verificáveis usando as seguintes instruções MSIL: `dup`, `ldsflda`, `ldflda`, `ldelema`, `call` e `unbox`.  
  
## <a name="examples"></a>Exemplos  
 O comando a seguir realiza verificações de validação dos metadados e verificações de segurança fortemente tipada MSIL para métodos implementados no assembly `myAssembly.exe`.  
  
```console  
peverify myAssembly.exe /md /il  
```  
  
 Mediante a conclusão bem-sucedida da solicitação acima, Peverify.exe exibe a mensagem a seguir.  
  
```output
All classes and methods in myAssembly.exe Verified  
```  
  
 O comando a seguir realiza verificações de validação dos metadados e verificações de segurança fortemente tipada MSIL para métodos implementados no assembly `myAssembly.exe`. A ferramenta exibe o tempo necessário à realização dessas verificações.  
  
```console  
peverify myAssembly.exe /md /il /clock  
```  
  
 Mediante a conclusão bem-sucedida da solicitação acima, Peverify.exe exibe a mensagem a seguir.  
  
```output
All classes and methods in myAssembly.exe Verified  
Timing: Total run     320 msec  
        MD Val.cycle  40 msec  
        MD Val.pure   10 msec  
        IL Ver.cycle  270 msec  
        IL Ver.pure   230 msec  
```  
  
 O comando a seguir realiza verificações de validação dos metadados e verificações de segurança fortemente tipada MSIL para métodos implementados no assembly `myAssembly.exe`. Peverify.exe para, no entanto, quando alcança a contagem de erros máxima de 100. A ferramenta também ignora os códigos de erro especificados.  
  
```console  
peverify myAssembly.exe /break=100 /ignore=0x12345678,0xABCD1234  
```  
  
 O comando a seguir produz o mesmo resultado que o exemplo anterior acima, mas especifica os códigos de erro que serão ignorados no arquivo de resposta `ignoreErrors.rsp`.  
  
```console  
peverify myAssembly.exe /break=100 /ignore@ignoreErrors.rsp  
```  
  
 O arquivo de resposta pode conter uma lista separada por vírgulas de códigos de erro.  
  
```text
0x12345678, 0xABCD1234  
```  
  
 O arquivo de resposta também pode ser formatado com um código de erro por linha.  
  
```text
0x12345678  
0xABCD1234  
```  
  
## <a name="see-also"></a>Confira também

- [Ferramentas](index.md)
- [Escrevendo um código fortemente tipado verificável](../misc/code-access-security-basics.md#typesafe_code)
- [Segurança de tipos e proteção](../../standard/security/key-security-concepts.md#type-safety-and-security)
- [Prompts de Comando](developer-command-prompt-for-vs.md)
