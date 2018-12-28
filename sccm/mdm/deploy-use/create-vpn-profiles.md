---
title: Perfis VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre os perfis VPN em dispositivos móveis no Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c90525b20107cbc926e3775f10d75b7c7083cac
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424566"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfis de VPN em dispositivos móveis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize perfis VPN no Configuration Manager para implementar definições VPN em utilizadores de dispositivos móveis na sua organização. Ao implementar estas definições, estará a minimizar o esforço do utilizador final para se ligar aos recursos na rede da empresa.  

Por exemplo, que pretende configurar todos os dispositivos iOS para se ligarem a uma partilha de ficheiros na rede empresarial. Crie um perfil VPN que tem as definições de ligação necessárias. Em seguida, implemente este perfil em todos os utilizadores com dispositivos iOS. Estes utilizadores veem a ligação de VPN na lista de redes disponíveis e podem ligar a esta rede com pouco esforço.  

Quando cria um perfil VPN, pode incluir uma grande variedade de definições de segurança. Por exemplo, pode especificar certificados para autenticação de cliente e de validação de servidor que foi configurados com perfis de certificado do Configuration Manager. Para obter mais informações, consulte [perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis VPN, ao utilizar o Gestor de configuração em conjunto com o Intune

Para implementar perfis de iOS, Android, Windows Phone e dispositivos Windows 8.1, tem de ser inscritos no Microsoft Intune. Dispositivos em outras plataformas também podem ser inscritos no Intune. Para obter informações sobre como inscrever, consulte [inscrever dispositivos no Microsoft Intune](/intune/device-enrollment). 

Esta tabela mostra o tipo de ligação suportado para cada plataforma de dispositivo:  

 |Tipo de ligação|iOS e macOS X|Android|Windows 8,1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|Sim<sup>1</sup>|Sim|Não|Não|Não|Não|Não|
 |Cisco (IPSec)|apenas em iOS|Não|Não|Não|Não|Não|Não|  
 |Pulse Secure|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |F5 Edge Client|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Dell SonicWALL Mobile Connect|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |VPN Móvel do Ponto de Verificação|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Microsoft SSL (SSTP)|Não|Não|Sim|Sim|Sim|Não|Não|  
 |Microsoft Automatic|Não|Não|Sim|Sim|Sim|Não|Sim|  
 |IKEv2|Sim (política personalizada, iOS 9 e posteriores)|Não|Sim|Sim|Sim|Sim|Sim|  
 |PPTP|Sim|Não|Sim|Sim|Sim|Não|Sim|  
 |L2TP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  

<sup>1</sup> a partir da versão 1802, varia de utilização do tipo de ligação do Cisco AnyConnect.<!--1357393-->  
   - Utilize o **Cisco Legacy AnyConnect** opção para VPN, perfis nas seguintes versões:
       - iOS com o Cisco AnyConnect versão 4.0.5 ou anterior
       - macOS com qualquer versão do Cisco AnyConnect
   - Utilize o **Cisco AnyConnect** opção para VPN, perfis nas seguintes versões:
       - iOS com o Cisco AnyConnect versão 4.0.7 ou posterior

     > [!Tip]  
     > Cisco AnyConnect 4.0.07x e versões posteriores para iOS foi introduzido pela primeira vez na versão 1802 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir [atualizar 4163547](https://support.microsoft.com/help/4163547) para versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  
  
  
> [!Note]  
> Versões de acesso de F5 3.0 e posteriores para iOS não são suportadas para perfis VPN no hybrid MDM. Este produto também é denominado F5 acesso 2018. Se precisar de criar perfis VPN para este cliente VPN, utilize o Intune autónomo. Versões futuras do iOS, incluindo a versão 12, não oferecem suporte ao acesso de F5 a versões 2.1 ou anterior. Para obter mais informações, consulte a [blogue de equipa de suporte do Microsoft Intune](https://aka.ms/iOS12_and_VPN).


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funcionalidades de VPN do Windows 10 estão disponíveis ao utilizar o Configuration Manager com o Intune  

As seguintes opções estão disponíveis para todos os tipos de ligação no Windows 10:

- **Ignorar VPN quando ligado à rede Wi-Fi da empresa**: A ligação VPN não é utilizada quando o dispositivo estiver ligado à rede Wi-Fi da empresa. Introduza o nome de rede fidedigna, que é utilizado para determinar se o dispositivo está ligado à rede da empresa.  

- **As regras de tráfego de rede**: Defina os protocolos, portas locais, porta remota e intervalos de endereços para ativar para a ligação VPN.  

     > [!Note]  
     > Se não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços estarão ativados. Depois de criar uma regra, apenas os protocolos, portas e intervalos de endereços que especificar nessa regra ou nas regras adicionais são utilizados pela ligação VPN.  
  
- **Rotas**: Rotas que utilizem a ligação VPN. Criação de mais de 60 rotas pode fazer com que a política de falha.  

- **Servidores DNS**: Servidores DNS que são utilizados pela ligação VPN, depois da ligação foi estabelecida.  

- **Aplicações que ligam automaticamente à VPN**: Pode adicionar aplicações ou importar listas de aplicações que utilizam automaticamente a ligação VPN. O tipo de aplicação determina o identificador de aplicação. Para uma aplicação de ambiente de trabalho, forneça o caminho do ficheiro da aplicação. Para uma aplicação universal, forneça o nome de família de pacotes (PFN). Para saber como localizar o PFN para uma aplicação, veja [localizar um nome de família de pacotes para VPN por aplicação](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md).  

     > [!IMPORTANT]  
     > Proteção de todas as listas de aplicações associadas que compilar para utilização na configuração da VPN por aplicação. Se um utilizador não autorizado altera sua lista e importá-lo para a lista de aplicações VPN por aplicação, irá autorizar potencialmente acesso VPN para aplicações que não devem ter acesso. Uma forma de proteger as listas de aplicações é através de uma lista de controlo de acesso (ACL).  



## <a name="create-vpn-profiles"></a>Criar perfis VPN


1. Na consola do Configuration Manager, no **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**, expanda **acesso a recursos da empresa**e selecione  **Perfis VPN**. 

2. Clique em **criar perfil VPN** na faixa de opções.  

3. Na **gerais** , especifique um **nome**e, em seguida, selecione o **tipo de perfil VPN**.   
     > [!NOTE]  
     > O nome de um perfil VPN que utiliza as funcionalidades de VPN do Windows 10 não pode estar em Unicode ou incluir caracteres especiais.


4. Se o **plataformas suportadas** página está disponível, selecione as versões de SO para o tipo de perfil VPN especificado anteriormente. Escolher **Selecionar tudo** para instalar o perfil VPN em todas as versões disponíveis do sistema operacional.  

5. Configurar a ligação VPN no **ligação** página. Para obter mais informações sobre estas opções, consulte o passo na página de ligação [criar um perfil VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6. Sobre o **método de autenticação** página, especifique as seguintes definições:  

   - **Método de autenticação**: Selecione o método de autenticação que utiliza a ligação VPN. Métodos disponíveis dependem do tipo de ligação, conforme mostrado nesta tabela.  

     |Método de Autenticação|Suportado&nbsp;ligação&nbsp;tipos|  
     |---------------------------|--------------------------------|  
     |**Certificados**<br /><br /> **Notas:**<ul><li>Se o certificado de cliente é autenticado num servidor RADIUS, como um servidor de políticas de rede, defina o nome alternativo do requerente no certificado para o nome do Principal de utilizador.</li><li>Para implementações de Android, selecione o identificador EKU e o valor de hash de thumbprint de emissor do certificado. Caso contrário, os utilizadores devem selecionar o certificado apropriado manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN Móvel do Ponto de Verificação</li></ul>|  
     |**Nome de Utilizador e Palavra-passe**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN Móvel do Ponto de Verificação</li></ul>|  
     |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
     |**Microsoft EAP protegido (PEAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Microsoft palavra-passe segura (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Smart Card ou outro certificado**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**RSA SecurID** (apenas para iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Utilizar certificados de computador**|<ul><li>IKEv2</li></ul>|  

      Dependendo das opções selecionadas, poderá ser-lhe pedido para especificar a obter mais informações, como:  

     - **Lembrar as credenciais de utilizador em cada início de sessão**: As credenciais de utilizador são memorizadas, para que os utilizadores não têm de introduzi-las sempre que se ligam.  

     - **Selecione um certificado de cliente para autenticação de cliente**: Selecione o cliente criado anteriormente [certificado SCEP](create-pfx-certificate-profiles.md) que é utilizado para autenticar a ligação VPN.   

       > [!NOTE]  
       >  Para dispositivos iOS, o perfil SCEP que selecionar é incorporado no perfil da VPN. Para outras plataformas, uma regra de aplicabilidade é adicionada para se certificar de que o perfil VPN não está instalado, se o certificado não estiver presente ou não estiver em conformidade.  
       >   
       >  Se o certificado SCEP que especificar não estiver em conformidade ou não tenha sido implantado, em seguida, o perfil VPN não está instalado no dispositivo.
       >  
       >  Os dispositivos que executam o iOS suportam apenas SecurID de RSA e MSCHAP v2 para o método de autenticação quando o tipo de ligação é PPTP. Para evitar erros de relatório, implemente um perfil VPN PPTP separado para dispositivos com iOS.   

     - **Acesso condicional**  
         - Escolher **ativar o acesso condicional para esta ligação VPN** para garantir que os dispositivos que estabelecem ligação à VPN são testados para compatibilidade de acesso condicional antes de ligar. Para obter mais informações, consulte [políticas de conformidade do dispositivo](/sccm/protect/deploy-use/device-compliance-policies).  

         - Escolher **ativar o início de sessão único (SSO) com certificado alternativo** escolher um certificado que não seja o certificado de autenticação VPN para a conformidade do dispositivo. Se escolher esta opção, forneça o **EKU** (lista separada por vírgulas) e **Hash de emissor**, para o correto de certificado que o cliente VPN deve localizar.  

       - Para **Windows Information Protection**, forneça a geridas por empresas identidade empresarial, que é normalmente domínio primário da sua organização, por exemplo, *contoso.com*. É possível especificar vários domínios que sua organização é proprietária, separando-as com o "|" caráter. Por exemplo, *contoso.com|newcontoso.com*. Para obter mais informações, consulte [criar e implementar uma política de proteção de aplicações do Windows Information Protection com o Intune](/intune/windows-information-protection-policy-create).   

       ![Criar Assistente de perfil de VPN, página de método de autenticação](media/vpn-conditional-access.png)

       Quando a versão de cliente do Windows oferece suporte a ele, a opção para **configurar** o método de autenticação está disponível. Esta opção abre a caixa de diálogo de propriedades do Windows para configurar o método de autenticação. Se **configurar** é desativada, a utilizar um modo diferente para configurar as propriedades do método de autenticação.  

7. Na **definições de Proxy** página do **criar Assistente de perfil de VPN**, verifique o **configurar definições de proxy para este perfil VPN** caixa se a ligação VPN utilizar um servidor proxy. Em seguida, forneça o proxy de informações do servidor. Para obter mais informações, consulte a documentação do Windows Server.  

   > [!NOTE]  
   >  Em computadores Windows 8.1, o perfil VPN não irá mostrar as informações de proxy até que se liga à VPN utilizando esse computador.  


8. Configure definições DNS adicionais, se necessário.  

9. Conclua o assistente. O **perfis de VPN** nó a **ativos e compatibilidade** área de trabalho mostra o novo perfil VPN.  



## <a name="next-steps"></a>Passos seguintes  
Para obter mais informações sobre como implementar perfis VPN, consulte [implementar Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Utilize os seguintes artigos para o ajudar a planear, configurar, operar e manter perfis VPN:  

-   [Pré-requisitos para perfis VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
