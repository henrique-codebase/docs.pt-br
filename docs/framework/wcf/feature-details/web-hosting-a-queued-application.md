---
title: Hospedando na Web um aplicativo em fila
ms.date: 03/30/2017
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
ms.openlocfilehash: 36c35fe0590ad9fc728641313d4175a432d7ccaa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951571"
---
# <a name="web-hosting-a-queued-application"></a>Hospedando na Web um aplicativo em fila
O WAS (serviço de ativação de processos do Windows) gerencia a ativação e o tempo de vida dos processos de trabalho que contêm aplicativos que hospedam serviços do Windows Communication Foundation (WCF). O modelo de processo WAS generaliza o modelo de processo do IIS 6,0 para o servidor HTTP removendo a dependência em HTTP. Isso permite que os serviços WCF usem protocolos HTTP e não HTTP, como net. MSMQ e MSMQ. FormatName, em um ambiente de hospedagem que ofereça suporte à ativação baseada em mensagem e ofereça a capacidade de hospedar um grande número de aplicativos em um determinado computador.  
  
 O WAS inclui um serviço de ativação de enfileiramento de mensagens (MSMQ) que ativa um aplicativo na fila quando uma ou mais mensagens são colocadas em uma das filas usadas pelo aplicativo. O serviço de ativação MSMQ é um serviço NT que é iniciado automaticamente por padrão.  
  
 Para obter mais informações sobre o WAS e seus benefícios, consulte [hospedagem no serviço de ativação de processos do Windows](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md). Para obter mais informações sobre o MSMQ, consulte [visão geral de filas](../../../../docs/framework/wcf/feature-details/queues-overview.md).
  
## <a name="queue-addressing-in-was"></a>O endereçamento de fila no foi  
 Os aplicativos WAS têm endereços Uniform Resource Identifier (URI). Os endereços de aplicativo têm duas partes: um prefixo de URI de base e um endereço relativo de aplicativo específico (caminho). Essas duas partes fornecem o endereço externo para um aplicativo quando Unidos. O prefixo URI de base é construído a partir da associação do site e é usado para todos os aplicativos no site, por exemplo, "net. MSMQ://localhost", "MSMQ. FormatName://localhost" ou "net. TCP://localhost". Os endereços de aplicativo são então construídos por meio de fragmentos de caminho específicos do aplicativo (como "/applicationOne") e os acrescentamos ao prefixo de URI de base para chegar ao URI completo do aplicativo, por exemplo, "net. MSMQ://localhost/applicationOne".  
  
 O serviço de ativação MSMQ usa o URI do aplicativo para corresponder à fila que o serviço de ativação MSMQ deve monitorar para mensagens. Quando o serviço de ativação MSMQ é iniciado, ele enumera todas as filas públicas e privadas no computador em que ele está configurado para receber e as monitora por mensagens. A cada 10 minutos, o serviço de ativação MSMQ atualiza a lista de filas a serem monitoradas. Quando uma mensagem é encontrada em uma fila, o serviço de ativação corresponde ao nome da fila para o URI de aplicativo correspondente mais longo para a associação net. MSMQ e ativa o aplicativo.  
  
> [!NOTE]
> O aplicativo que está sendo ativado deve corresponder (correspondência mais longa) ao prefixo do nome da fila.  
  
 Por exemplo, um nome de fila é: msmqWebHost/orderProcessing/Service. svc. Se o aplicativo 1 tiver um diretório virtual/msmqWebHost/orderProcessing com um Service. svc, e o aplicativo 2 tiver um diretório virtual/msmqWebHost com um orderProcessing. svc sob ele, o aplicativo 1 será ativado. Se o aplicativo 1 for excluído, o aplicativo 2 será ativado.  
  
> [!NOTE]
> Quando uma fila é criada, todas as mensagens enviadas a ela não ativam um aplicativo até que o serviço de ativação MSMQ atualize a lista de filas, que é, no máximo, 10 minutos a partir da hora em que a fila foi criada. Reiniciar o serviço de ativação também atualiza a lista de filas.  
  
### <a name="the-effect-of-private-and-public-queues-on-addressing"></a>O efeito de filas privadas e públicas no endereçamento  
 O serviço de ativação MSMQ não faz distinção entre o monitoramento de filas pública e privada. Assim, você não pode ter filas públicas e privadas com o mesmo nome. Se você fizer isso, um aplicativo hospedado na Web poderá ser ativado com a leitura de uma das filas.  
  
### <a name="queue-configuration-for-activation"></a>Configuração de fila para ativação  
 O serviço de ativação MSMQ é executado como serviço de rede. É o serviço que monitora as filas para ativar aplicativos. Para que ele ative aplicativos da fila, a fila deve fornecer acesso ao serviço de rede para inspecionar mensagens em sua ACL (lista de controle de acesso).  
  
### <a name="poison-messaging"></a>Mensagens suspeitas  
 O tratamento de mensagens suspeitas no WCF é manipulado pelo canal, o que detecta apenas que uma mensagem é inviabilizada, mas seleciona uma disposição com base na configuração do usuário. Como resultado, há uma única mensagem na fila. O aplicativo hospedado na Web aborta os tempos sucessivos e a mensagem é movida para uma fila de repetição. Em um ponto determinado pelo atraso do ciclo de repetição, a mensagem é movida da fila de repetição para a fila principal para tentar novamente. Mas isso requer que o canal enfileirado esteja ativo. Se o aplicativo for reciclado pelo WAS, a mensagem permanecerá na fila de repetição até que outra mensagem chegue na fila principal para ativar o aplicativo enfileirado. A solução alternativa, nesse caso, é mover a mensagem manualmente da fila de repetição de volta para a fila principal para reativar o aplicativo.  
  
### <a name="subqueue-and-system-queue-caveat"></a>Advertência da subfila e da fila do sistema  
 Um aplicativo WAS hospedado não pode ser ativado com base em mensagens em uma fila do sistema, como a fila de mensagens mortas de todo o sistema, ou subfilas, como subfilas suspeitas. Esta é uma limitação para esta versão do produto.  
  
## <a name="see-also"></a>Consulte também

- [Manipulação de mensagens suspeitas](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)
- [Pontos de extremidade de serviço e endereçamento de fila](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)
