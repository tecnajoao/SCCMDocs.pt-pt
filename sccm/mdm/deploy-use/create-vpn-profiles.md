---
title: Perfis da VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre perfis da VPN em dispositivos móveis no Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9409b6cc71ea238755f40baf75e6211c447b547f
ms.sourcegitcommit: 826e9ec385d6a1c1f3aa86ac202883154e0c1285
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/29/2018
ms.locfileid: "37116516"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfis da VPN em dispositivos móveis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize perfis VPN no Configuration Manager para implementar definições VPN em utilizadores de dispositivos móveis na sua organização. Ao implementar estas definições, minimiza o esforço do utilizador final necessárias para ligar a recursos na rede da empresa.  

Por exemplo, pretende configurar todos os dispositivos iOS para ligar a uma partilha de ficheiros na rede empresarial. Crie um perfil VPN com as definições de ligação necessárias. Em seguida, implemente este perfil em todos os utilizadores com dispositivos iOS. Estes utilizadores veem a ligação VPN na lista de redes disponíveis e podem ligar a esta rede com pouca esforço.  

Quando cria um perfil da VPN, pode incluir um vasto leque de definições de segurança. Por exemplo, pode especificar certificados para autenticação de cliente e validação do servidor que configurou através da utilização de perfis de certificado do Configuration Manager. Para obter mais informações, consulte [perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis VPN, ao utilizar o Gestor de configuração com o Intune

Para implementar perfis em dispositivos Windows 8.1, Windows Phone, Android e iOS, tem de estar inscritos no Microsoft Intune. Dispositivos em outras plataformas também podem ser inscritos no Intune. Para obter informações sobre como inscrever, consulte [inscrever dispositivos no Microsoft Intune](/intune/device-enrollment). 

Esta tabela mostra o tipo de ligação que é suportado para cada plataforma de dispositivo:  

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

<sup>1</sup> a partir de versão 1802, varia de utilização do tipo de ligação Cisco AnyConnect.<!--1357393-->  
   - Utilize o **Cisco AnyConnect de legado** opção para VPN, perfis nas seguintes versões:
       - iOS com o Cisco AnyConnect versão 4.0.5 ou anterior
       - macOS com qualquer versão do Cisco AnyConnect
   - Utilize o **Cisco AnyConnect** opção para VPN, perfis nas seguintes versões:
       - iOS com o Cisco AnyConnect versão 4.0.7 ou posterior

     > [!Tip]  
     > Cisco AnyConnect 4.0.07x e posterior para iOS foi introduzida pela primeira vez na versão 1802 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Começando com [atualizar 4163547](https://support.microsoft.com/help/4163547) para versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  
  
  
> [!Note]  
> F5 acesso 2018 não é suportada para perfis VPN no híbrida MDM.  


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funcionalidades de VPN do Windows 10 estão disponíveis ao utilizar o Configuration Manager com o Intune  

As seguintes opções estão disponíveis para todos os tipos de ligação no Windows 10:

- **Ignorar VPN quando ligado à rede Wi-Fi da empresa**: A ligação VPN não é utilizada quando o dispositivo estiver ligado à rede Wi-Fi da empresa. Introduza o nome de rede fidedigna, que é utilizado para determinar se o dispositivo está ligado à rede da empresa.  

- **As regras de tráfego de rede**: Defina os protocolos, portas locais, porta remota e intervalos de endereços para ativar para a ligação VPN.  

     > [!Note]  
     > Se não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços estarão ativados. Depois de criar uma regra, apenas os protocolos, portas e intervalos de endereços que especificar nessa regra ou nas regras adicionais são utilizados pela ligação VPN.  
  
- **Rotas**: Rotas que utilizem a ligação VPN. Criação de mais de 60 rotas pode fazer com que a política de falha.  

- **Servidores DNS**: Servidores DNS que são utilizados pela ligação VPN, depois da ligação for estabelecida.  

- **Aplicações que ligam automaticamente à VPN**: Pode adicionar aplicações ou importar listas de aplicações que utilizam automaticamente a ligação VPN. O tipo de aplicação determina o identificador da aplicação. Para uma aplicação de ambiente de trabalho, forneça o caminho do ficheiro da aplicação. Para uma aplicação universal, forneça o nome de família de pacotes (PFN). Para saber como encontrar o PFN para uma aplicação, consulte [localizar um nome de família de pacotes para VPN por aplicação](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md).  

     > [!IMPORTANT]  
     > Proteção de todas as listas de aplicações associadas que compilar para utilização na configuração da VPN por aplicação. Se a sua lista de alterações de um utilizador não autorizado e importe-o à lista de aplicações VPN por aplicação, autorizar potencialmente acesso VPN para aplicações que não devem ter acesso. Uma forma de proteger as listas de aplicação é utilizar uma lista de controlo de acesso (ACL).  



## <a name="create-vpn-profiles"></a>Criar perfis de VPN


1. Na consola do Configuration Manager, no **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade**, expanda **acesso a recursos da empresa**e selecione  **Perfis da VPN**. 

2. Clique em **criar perfil VPN** no Friso.  

3. No **geral** página, especifique um **nome**e, em seguida, selecione o **tipo de perfil VPN**.   
     > [!NOTE]  
     > O nome de um perfil VPN que utiliza funcionalidades de VPN do Windows 10 não pode estar em Unicode ou incluir carateres especiais.


4. Se o **plataformas suportadas** página se encontra disponível, selecione as versões de SO para o tipo de perfil VPN especificado anteriormente. Escolha **Selecionar tudo** para instalar o perfil da VPN em todas as versões do SO disponíveis.  

5. Configurar a ligação VPN no **ligação** página. Para obter mais informações sobre estas opções, consulte o passo na página de ligação de [criar um perfil VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6.  No **método de autenticação** página, especifique as seguintes definições:  

    -   **Método de autenticação**: Selecione o método de autenticação que utiliza a ligação VPN. Métodos disponíveis dependem do tipo de ligação conforme mostrado nesta tabela.  

        |Método de Autenticação|Suportado&nbsp;ligação&nbsp;tipos|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Notas:**<ul><li>Se o certificado de cliente efetua a autenticação para um servidor RADIUS, como um servidor de políticas de rede, defina nome alternativo do requerente no certificado para o nome Principal de utilizador.</li><li>Para implementações de Android, selecione o identificador EKU e o valor de hash de thumbprint do certificado emissor. Caso contrário, os utilizadores tem de selecionar o certificado adequado manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco AnyConnect de legado</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN Móvel do Ponto de Verificação</li></ul>|  
        |**Nome de Utilizador e Palavra-passe**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN Móvel do Ponto de Verificação</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**EAP (PEAP) protegido da Microsoft**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Microsoft protegida por palavra-passe (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Smart Card ou outro certificado**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (apenas para iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Utilizar certificados de computador**|<ul><li>IKEv2</li></ul>|  

         Consoante as opções selecionadas, poderá ser-lhe pedido para especificar a obter mais informações, como:  

        -   **Lembrar as credenciais de utilizador em cada início de sessão**: As credenciais de utilizador são memorizadas, para que os utilizadores não têm introduzi-las sempre que se ligam.  

        -   **Selecione um certificado de cliente para autenticação de cliente**: Selecione o cliente criado anteriormente [certificado de SCEP](create-pfx-certificate-profiles.md) que é utilizado para autenticar a ligação VPN.   

            > [!NOTE]  
            >  Para dispositivos iOS, o perfil SCEP que selecionar é incorporado no perfil da VPN. Para outras plataformas, é adicionada uma regra de aplicabilidade para assegurar que o perfil VPN não está instalado se o certificado não está presente ou não é compatível.  
            >   
            >  Se o certificado SCEP que especificou não está em conformidade ou ainda não tenha sido implementado, o perfil VPN não está instalado no dispositivo.
            >  
            >  Os dispositivos que executam o iOS suportam apenas SecurID de RSA e MSCHAP v2 para o método de autenticação quando o tipo de ligação for PPTP. Para evitar erros de relatório, implemente um perfil VPN PPTP separado para dispositivos com iOS.   

        - **Acesso condicional**  
            - Escolha **ativar o acesso condicional para esta ligação VPN** para se certificar de que os dispositivos que ligam à VPN são testados para compatibilidade de acesso condicional, antes de ligar. Para obter mais informações, consulte [políticas de conformidade do dispositivo](/sccm/protect/deploy-use/device-compliance-policies).  

            - Escolha **ativar início de sessão único (SSO) com certificado alternativo** para escolher um certificado que não seja o certificado de autenticação VPN para conformidade do dispositivo. Se escolher esta opção, forneça o **EKU** (lista de valores separados por vírgulas) e **Hash de emissor**, para o certificado correto que o cliente VPN deve localizar.  

         - Para **Windows Information Protection**, forneça a geridas por empresas identidade empresarial, que é normalmente domínio principal da sua organização, por exemplo, *contoso.com*. Pode especificar vários domínios que a sua organização é proprietária, separando-as com o "|" carateres. Por exemplo, *contoso.com|newcontoso.com*. Para obter mais informações, consulte [criar e implementar uma política de proteção de aplicações do Windows Information Protection com o Intune](/intune/windows-information-protection-policy-create).   

         ![Criar Assistente de perfil de VPN, página de método de autenticação](media/vpn-conditional-access.png)

         Quando a versão do cliente Windows suporta, a opção de **configurar** o método de autenticação está disponível. Esta opção abre a caixa de diálogo de propriedades do Windows para configurar o método de autenticação. Se **configurar** está desativada, utilize um meio diferente para configurar as propriedades do método de autenticação.  

3.  No **as definições de Proxy** página do **VPN Assistente para criar perfil**, verifique o **configurar definições de proxy para este perfil VPN** caixa se a ligação VPN utilizar um servidor proxy. Em seguida, forneça o proxy de informações do servidor. Para obter mais informações, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Em computadores Windows 8.1, o perfil VPN não irá mostrar as informações de proxy até que o se ligar à VPN utilizando esse computador.  


4. Configure definições DNS adicionais, se necessário.  

5. Conclua o assistente. O **perfis VPN** no nó de **ativos e compatibilidade** área de trabalho mostra o novo perfil VPN.  



## <a name="next-steps"></a>Passos seguintes  
Para obter mais informações sobre como implementar perfis VPN, consulte [implementar Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Utilize os artigos seguintes para o ajudar a planear, configurar, operar e manter perfis VPN:  

-   [Pré-requisitos para perfis VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
