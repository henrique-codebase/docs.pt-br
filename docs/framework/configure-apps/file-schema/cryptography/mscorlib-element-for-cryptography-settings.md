---
title: Elemento <mscorlib> para configurações de criptografia
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mscorlib
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib
helpviewer_keywords:
- mscorlib element
- <mscorlib> element
ms.assetid: d549668f-31f1-4b92-8021-a9135c09ca3c
ms.openlocfilehash: d1d805f7154c18dba2dcd4eb7228cc200d8da811
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79155175"
---
# <a name="mscorlib-element-for-cryptography-settings"></a>\<mscorlib> Element para configurações de criptografia
Contém [ \<o elemento> criptografiaConfigurações>](cryptographysettings-element.md).  
  
[**\<>de configuração**](../configuration-element.md)  
&nbsp;&nbsp;**\<mscorlib>**  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
      <mscorlib>
</mscorlib>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`cryptographySettings`|Contém configurações de criptografia.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o ** \<elemento mscorlib>** para referenciar uma classe de criptografia e configurar o tempo de execução. Em seguida, você pode passar a <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> string "RSA" para o método e usar o <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> método para retornar um `MyCryptoRSAClass` objeto.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCryptoRSA="MyCryptoRSAClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RSA" class="MyCryptoRSA"/>  
            <nameEntry name="System.Security.Cryptography.AsymmetricAlgorithm"  
                       class="MyCryptoRSA"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A>
- <xref:System.Security.Cryptography>
- [Esquema de arquivo de configuração](../index.md)
- [Esquema de configurações de criptografia](index.md)
- [Serviços criptográficos](../../../../standard/security/cryptographic-services.md)
- [Configurando classes de criptografia](../../configure-cryptography-classes.md)
