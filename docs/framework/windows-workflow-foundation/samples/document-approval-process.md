---
title: Processo de aprovação de documento
description: Este exemplo demonstra muitos recursos de Windows Workflow Foundation e Windows Communication Foundation em um cenário de processo de aprovação de documentos.
ms.date: 03/30/2017
ms.assetid: 9b240937-76a7-45cd-8823-7f82c34d03bd
ms.openlocfilehash: 18b4f978e9234daf22395f0d2f6f0889d0edf966
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421404"
---
# <a name="document-approval-process"></a>Processo de aprovação de documento

Este exemplo demonstra o uso de muitos recursos Windows Workflow Foundation (WF) e Windows Communication Foundation (WCF) juntos. Junto implementam um cenário do processo de aprovação do documento. Um aplicativo cliente pode enviar documentos para a aprovação e aprovar documentos. Um aplicativo do gerenciador de aprovação existe para facilitar comunicação entre clientes e para aplicar as regras do processo de aprovação. O processo de aprovação é um fluxo de trabalho que pode executar vários tipos de aprovação. As atividades existem para obter uma única aprovação, uma aprovação de quorum (uma porcentagem do conjunto de approvers), e um processo de aprovação complexo que consiste em um quorum e em uma única aprovação em uma sequência.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\DocumentApprovalProcess`

## <a name="sample-details"></a>Detalhes de exemplo

O gráfico a seguir demonstra o fluxo de trabalho do processo de aprovação de documentos:

![Um fluxo de trabalho do processo de aprovação do documento](./media/document-approval-process/document-approval-process.jpg)

Da perspectiva de cliente, o processo de aprovação funciona como segue:

1. Um cliente assina para ser um usuário no sistema do processo de aprovação.

2. Um cliente WCF envia para um serviço WCF hospedado pelo aplicativo Gerenciador de aprovação.

3. Um usuário exclusivo - a identificação é retornada para o cliente. O cliente agora pode participar em processos de aprovação.

4. Uma vez que unido, um cliente pode enviar um documento para usar a aprovação única, o quorum ou processos de aprovação complexos.

5. Um botão na interface de cliente é clicado, começando uma instância de fluxo de trabalho em um host de Serviço de Fluxo de Trabalho do cliente.

6. O fluxo de trabalho envia uma solicitação de aprovação o aplicativo gerenciador da aprovação.

7. O gerenciador de fluxo de trabalho inicia um fluxo de trabalho em seu próprio lado para representar um processo de aprovação.

8. Uma vez que o fluxo de trabalho de aprovação do aplicativo é executado, os resultados são novamente enviado ao cliente.

9. O cliente exibe os resultados.

10. Um cliente pode receber uma solicitação de aprovação e responder à solicitação em qualquer ponto no tempo.

11. Um serviço WCF hospedado no cliente pode receber uma solicitação de aprovação do aplicativo Gerenciador de aprovação.

12. Informações de documento é apresentada no cliente para revisão.

13. O usuário pode aprovar ou descartar o documento.

14. Um cliente WCF é usado para enviar uma resposta de aprovação de volta para o aplicativo Gerenciador de aprovação.

Do ponto de vista de aplicativo do gerenciador de aprovação, o processo de aprovação funciona como segue:

1. Solicitações de cliente participar do sistema do processo de aprovação.

2. Um serviço WCF no Gerenciador de aprovação recebe uma solicitação para fazer parte do sistema de processo de aprovação.

3. Uma identificação exclusiva é gerada para o cliente. Informações de usuário é armazenado em uma base de dados.

4. A identificação exclusiva é enviada para o usuário.

5. Uma solicitação de aprovação é receber. O gerenciador de aprovação executa um processo de aprovação.

6. Uma solicitação de aprovação é recebida pelo gerenciador de aprovação, iniciando um novo fluxo de trabalho.

7. Dependendo do tipo de solicitação (simples, quorum, ou complexo) uma atividade diferente é executada.

8. Enviar e receber atividades com correlação são usados para enviar a solicitação aprovação do cliente para a revisão e para receber a resposta.

9. O resultado de fluxo de trabalho do processo de aprovação é enviada para o cliente.

## <a name="using-the-sample"></a>Usando o exemplo

##### <a name="to-set-up-the-database"></a>Para configurar o base de dados

1. Em um prompt de comando do Visual Studio 2010 aberto com privilégios de administrador, navegue até essa pasta DocumentApprovalProcess e execute Setup. cmd.

##### <a name="to-set-up-the-application"></a>Para configurar o aplicativo

1. Usando o Visual Studio 2010, abra o arquivo de solução DocumentApprovalProcess. sln.

2. Para criar a solução, pressione CTRL+SHIFT+B.

3. Para executar a solução, inicie o aplicativo Gerenciador de aprovação clicando com o botão direito do mouse no projeto de aprovação no **Gerenciador de soluções** e clicando em **depurar** -> **Iniciar** nova instância no menu do clique com o botão direito do mouse.

    Espera para que a saída do gerenciador deixem-no saber que estão prontas.

##### <a name="to-run-the-single-approval-scenario"></a>Para executar o único cenário de aprovação

1. Abra um prompt de comando com permissão de administrador.

2. Navegue até a pasta que contém a solução.

3. Navegue até a pasta de ApprovalClient \ bin \ debug e executar duas instâncias de ApprovalClient.exe.

4. Clique em **descobrir**, aguarde até que o botão **assinar** esteja habilitado.

5. Digite qualquer nome de usuário e clique em **assinar**. Para um cliente, use `UserType1` e o outro tipo `UserType2`.

6. No cliente de `UserType1` , selecione o único tipo de aprovação do menu suspenso e digite um nome e um conteúdo do documento. Clique em **solicitar aprovação**.

7. No cliente de `UserType2` , um documento aguardando a aprovação aparece. Selecione-o e pressione **aprovar** ou **rejeitar**. Os resultados devem mostrar no cliente de `UserType1` .

##### <a name="to-run-the-quorum-approval-scenario"></a>Para executar o cenário de aprovação de quorum

1. Abra um prompt de comando com permissão de administrador.

2. Navegue até a pasta que contém a solução.

3. Navegue até a pasta de ApprovalClient \ bin \ debug e executar três instâncias de ApprovalClient.exe.

4. Clique em **descobrir**, aguarde até que o botão **assinar** esteja habilitado.

5. Digite qualquer nome de usuário e clique em **assinar**. Para um uso `UserType1` de cliente e outros dois tipo `UserType2`.

6. No cliente de `UserType1` , selecione o tipo de aprovação de quorum no menu suspenso e digite um nome e um conteúdo do documento. Clique em **solicitar aprovação**. Isso requer que os dois clientes de `UserType2` aprovam ou rejeitam o documento. Quando ambos os clientes de `UserType2` devem responder, somente um cliente deve aprovar o documento para que esteja certo.

7. Os clientes de `UserType2` , um documento aguardando a aprovação aparece. Selecione-o e pressione **aprovar** ou **rejeitar**. Os resultados devem mostrar no cliente de `UserType1` .

##### <a name="to-run-the-complex-approval-scenario"></a>Para executar o cenário complexo de aprovação

1. Abra um prompt de comando com permissão de administrador.

2. Navegue até a pasta que contém a solução.

3. Navegue até a pasta de ApprovalClient \ bin \ debug e executar quatro instâncias de ApprovalClient.exe.

4. Clique em **descobrir**, aguarde até que o botão **assinar** esteja habilitado.

5. Digite qualquer nome de usuário e clique em **assinar**. Para um cliente, use `UserType1`no tipo `UserType2`de dois usos, e o uso mais recente `UserType3`.

6. No cliente de `UserType1` , selecione o único tipo de aprovação do menu suspenso e digite um nome e um conteúdo do documento. Clique em **solicitar aprovação**.

7. Os clientes de `UserType2` , um documento aguardando a aprovação aparece. Selecione-o e pressione **aprovar**, o documento é passado para o `UserType3` cliente.

    Se o documento é certo pela primeira quorum de `UserType2` , o documento é passado para o cliente de `UserType3` .

8. Aprove ou rejeite o documento de cliente de `UserType3` . Os resultados devem mostrar no cliente de `UserType1` .

##### <a name="to-clean-up"></a>Para limpar

1. Em um prompt de comando do Visual Studio 2010, navegue até a pasta DocumentApprovalProcess e execute Cleanup. cmd.
