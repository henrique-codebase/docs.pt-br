---
title: 'Como: criar um verificador de identidade de cliente personalizado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f2d34e43-fa8b-46d2-91cf-d2960e13e16b
ms.openlocfilehash: 86e7869efdba50d72cc61a1aebb767cf43927546
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795638"
---
# <a name="how-to-create-a-custom-client-identity-verifier"></a>Como: criar um verificador de identidade de cliente personalizado
O recurso de *identidade* do Windows Communication Foundation (WCF) permite que um cliente especifique com antecedência a identidade esperada do serviço. Sempre que um servidor se autentica no cliente, a identidade é verificada em relação à identidade esperada. (Para obter uma explicação de identidade e como ela funciona, consulte [identidade e autenticação de serviço](../feature-details/service-identity-and-authentication.md).)  
  
 Se necessário, a verificação pode ser personalizada usando um verificador de identidade personalizado. Por exemplo, você pode executar verificações de verificação de identidade de serviço adicionais. Neste exemplo, o verificador de identidade personalizado verifica declarações adicionais no certificado X. 509 retornado do servidor. Para um aplicativo de exemplo, consulte [exemplo de identidade de serviço](../samples/service-identity-sample.md).  
  
### <a name="to-extend-the-endpointidentity-class"></a>Para estender a classe EndpointIdentity  
  
1. Defina uma nova classe derivada da <xref:System.ServiceModel.EndpointIdentity> classe. Este exemplo nomeia a extensão `OrgEndpointIdentity`.  
  
2. Adicione membros privados junto com as propriedades que serão usadas pela classe estendida <xref:System.ServiceModel.Security.IdentityVerifier> para executar a verificação de identidade em declarações no token de segurança retornado do serviço. Este exemplo define uma propriedade: a `OrganizationClaim` propriedade.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
     [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
### <a name="to-extend-the-identityverifier-class"></a>Para estender a classe IdentityVerifier  
  
1. Defina uma nova classe derivada de <xref:System.ServiceModel.Security.IdentityVerifier>. Este exemplo nomeia a extensão `CustomIdentityVerifier`.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#7)]
     [!code-vb[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#7)]  
  
2. Substituir o método <xref:System.ServiceModel.Security.IdentityVerifier.CheckAccess%2A>. O método determina se a verificação de identidade foi bem-sucedida ou falhou.  
  
3. O `CheckAccess` método tem dois parâmetros. A primeira é uma instância da <xref:System.ServiceModel.EndpointIdentity> classe. A segunda é uma instância da <xref:System.IdentityModel.Policy.AuthorizationContext> classe.  
  
     Na implementação do método, examine a coleção de declarações retornada pela <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> propriedade <xref:System.IdentityModel.Policy.AuthorizationContext> da classe e execute as verificações de autenticação conforme necessário. Este exemplo começa encontrando qualquer declaração que seja do tipo "nome distinto" e, em seguida, compara o nome com a extensão <xref:System.ServiceModel.EndpointIdentity> do`OrgEndpointIdentity`().  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#1)]
     [!code-vb[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#1)]  
  
### <a name="to-implement-the-trygetidentity-method"></a>Para implementar o método TryGetIdentity  
  
1. Implemente <xref:System.ServiceModel.Security.IdentityVerifier.TryGetIdentity%2A> o método, que determina se uma instância <xref:System.ServiceModel.EndpointIdentity> da classe pode ser retornada pelo cliente. A infraestrutura do WCF chama a implementação do `TryGetIdentity` método primeiro para recuperar a identidade do serviço da mensagem. Em seguida, a infraestrutura chama `CheckAccess` a implementação com o `EndpointIdentity` retornado <xref:System.IdentityModel.Policy.AuthorizationContext>e.  
  
2. `TryGetIdentity` No método, coloque o seguinte código:  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#2)]
     [!code-vb[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#2)]  
  
### <a name="to-implement-a-custom-binding-and-set-the-custom-identityverifier"></a>Para implementar uma associação personalizada e definir o IdentityVerifier personalizado  
  
1. Crie um método que retorne <xref:System.ServiceModel.Channels.Binding> um objeto. Este exemplo começa a criar uma instância da <xref:System.ServiceModel.WSHttpBinding> classe e define seu modo de segurança <xref:System.ServiceModel.SecurityMode.Message>como, e <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> seu <xref:System.ServiceModel.MessageCredentialType.None>para.  
  
2. Crie um <xref:System.ServiceModel.Channels.BindingElementCollection> usando o <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A> método.  
  
3. Retorne <xref:System.ServiceModel.Channels.SecurityBindingElement> o da coleção e converta-o <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> em uma variável.  
  
4. Defina a <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.IdentityVerifier%2A> propriedade <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> da classe como `CustomIdentityVerifier` uma nova instância da classe criada anteriormente.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#3)]
     [!code-vb[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#3)]  
  
5. A associação personalizada retornada é usada para criar uma instância do cliente e da classe. O cliente pode, então, executar uma verificação de verificação de identidade personalizada do serviço, conforme mostrado no código a seguir.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#4)]
     [!code-vb[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#4)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma implementação completa da <xref:System.ServiceModel.Security.IdentityVerifier> classe.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#5)]
 [!code-vb[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#5)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma implementação completa da <xref:System.ServiceModel.EndpointIdentity> classe.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
 [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- <xref:System.ServiceModel.EndpointIdentity>
- <xref:System.ServiceModel.Security.IdentityVerifier>
- [Exemplo de identidade de serviço](../samples/service-identity-sample.md)
- [Política de autorização](../samples/authorization-policy.md)
