---
title: Perfis VPN no System Center Configuration Manager | Microsoft Docs
description: "Perfis da VPN em dispositivos móveis no System Center Configuration Manager."
ms.custom: na
ms.date: 07/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: "18"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: e4a53caab7d76b604a3fee7dcfc4dc48f22b0fb0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfis da VPN em dispositivos móveis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize perfis VPN no System Center Configuration Manager para implementar definições VPN em utilizadores de dispositivos móveis na sua organização. Ao implementar estas definições, minimiza o esforço do utilizador final necessárias para ligar a recursos na rede da empresa.  

 Por exemplo, pretende configurar todos os dispositivos que executam o sistema operativo iOS, utilizando as definições que são necessárias para ligar a uma partilha de ficheiros na rede empresarial. Pode criar um perfil da VPN com as definições necessárias para ligar à rede empresarial e, em seguida, implementar este perfil em todos os utilizadores com dispositivos que executam o iOS na sua hierarquia. Os utilizadores de dispositivos com iOS veem a ligação VPN na lista de redes disponíveis e podem estabelecer ligação com esta rede com o mínimo de esforço.  

 Quando cria um perfil da VPN, pode incluir um vasto leque de definições de segurança. Por exemplo, pode especificar certificados para autenticação de cliente e validação do servidor que configurou através da utilização de perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [no System Center Configuration Manager de perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis VPN, ao utilizar o Gestor de configuração com o Intune

 Para implementar perfis em dispositivos Windows 8.1, Windows Phone, Android e iOS, estes dispositivos têm de estar inscritos no Microsoft Intune. Dispositivos em outras plataformas também podem ser inscritos no Intune. Para obter informações sobre como inscrever, consulte [gerir dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Esta tabela mostra o tipo de ligação que é suportado para cada plataforma de dispositivo:  

 |Tipo de ligação|iOS e macOS X|Android|Windows 8,1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sim|Sim|Não|Não|Não|Não|Sim (OMA-URI)|
 |Cisco (IPSec)|apenas em iOS|Não|Não|Não|Não|Não|Não|  
 |Pulse Secure|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |F5 Edge Client|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Dell SonicWALL Mobile Connect|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |VPN Móvel do Ponto de Verificação|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Microsoft SSL (SSTP)|Não|Não|Sim|Sim|Sim|Não|Não|  
 |Microsoft Automatic|Não|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
 |IKEv2|Sim (política personalizada)|Não|Sim|Sim|Sim|Sim|Sim (OMA-URI)|  
 |PPTP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
 |L2TP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Criar perfis de VPN
[Como criar perfis VPN no System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) fornece informações gerais sobre como creat perfis VPN.

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funcionalidades de VPN do Windows 10 estão disponíveis ao utilizar o Configuration Manager com o Intune  


> [!NOTE]  
> O nome de um perfil VPN que utiliza funcionalidades de VPN do Windows 10 não pode estar em Unicode ou incluir carateres especiais.


|Opção|Mais informações|Tipo de ligação|  
    |------------|----------------------|---------------------|  
    |**Ignorar a VPN quando ligado à rede Wi-Fi da empresa**|A ligação VPN não será utilizada quando o dispositivo estiver ligado à rede Wi-Fi da empresa. Introduza o nome de rede fidedigna, que é utilizado para determinar se o dispositivo está ligado à rede da empresa.|Todas|  
    |**Regras network traffic (de tráfego de rede)**|Defina os protocolos, portas locais, porta remota e intervalos de endereços que irão estar ativados para a ligação VPN.<br /><br /> **Nota:** Se não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços estarão ativados. Depois de criar uma regra, apenas os protocolos, portas e intervalos de endereços que especificar nessa regra ou nas regras adicionais serão utilizados pela ligação VPN.|Todas|  
    |**Rotas**|Rotas que utilizarão a ligação VPN. Tenha em atenção que a criação de mais de 60 rotas pode fazer com que a política de falha. |Todas|  
    |**Servidores DNS**|Servidores DNS que são utilizados pela ligação VPN, depois da ligação for estabelecida.|Todas|  
    |**Aplicações que ligam automaticamente à VPN**|Pode adicionar aplicações ou importar listas de aplicações que irão utilizar automaticamente a ligação VPN. O tipo de aplicação irá determinar o identificador de aplicação. Para uma aplicação de ambiente de trabalho, forneça o caminho do ficheiro da aplicação. Para uma aplicação universal, forneça o nome de família de pacotes (PFN). Para saber como encontrar o PFN para uma aplicação, consulte [localizar um nome de família de pacotes para VPN por aplicação](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Todas|

> [!IMPORTANT]
> Recomendamos que proteja todas as listas de aplicações associadas que compilar para utilização na configuração da VPN por aplicação. Se a sua lista de alterações de um utilizador não autorizado e importe-o à lista de aplicações VPN por aplicação, irá autorizar potencialmente o acesso VPN para aplicações que não devem ter acesso. Uma forma de proteger as listas de aplicação é utilizar uma lista de controlo de acesso (ACL).


1.  No **método de autenticação** página do assistente, especifique:  

    -   **Método de autenticação**: Selecione o método de autenticação que será utilizado pela ligação VPN. Métodos disponíveis dependem do tipo de ligação conforme mostrado nesta tabela.  

        |Método de Autenticação|Suportado&nbsp;ligação&nbsp;tipos|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Notas:**<ul><li>Se o certificado de cliente efetua a autenticação para um servidor RADIUS, como um servidor de políticas de rede, tem de definir o nome alternativo do requerente no certificado para o nome Principal de utilizador.</li><li>Para implementações de Android, selecione o identificador EKU e o valor de hash de thumbprint do certificado emissor.  Caso contrário, os utilizadores tem de selecionar o certificado adequado manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN Móvel do Ponto de Verificação</li></ul>|  
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

        -   **Selecione um certificado de cliente para autenticação de cliente**: Selecione o cliente criado anteriormente [certificado de SCEP](create-pfx-certificate-profiles.md) que será utilizado para autenticar a ligação VPN.   

            > [!NOTE]  
            >  Para dispositivos iOS, o perfil SCEP que selecionar será incorporado no perfil da VPN. Para outras plataformas, é adicionada uma regra de aplicabilidade para assegurar que o perfil VPN não está instalado se o certificado não está presente ou não está em conformidade.  
            >   
            >  Se o certificado SCEP que especificou não está em conformidade ou não foi implementado, em seguida, o perfil VPN não será instalado no dispositivo.
            >  
            >  Os dispositivos que executam o iOS suportam apenas SecurID de RSA e MSCHAP v2 para o método de autenticação quando o tipo de ligação for PPTP. Para evitar erros de relatório, implemente um perfil VPN PPTP separado para dispositivos com iOS.  

        - **Acesso condicional**
            - Escolha **ativar o acesso condicional para esta ligação VPN** para se certificar de que os dispositivos que ligam à VPN são testados para compatibilidade de acesso condicional, antes de ligar. Políticas de conformidade são descritas nas [políticas de conformidade de dispositivos no System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Escolha **ativar início de sessão único (SSO) com certificado alternativo** para escolher um certificado que não seja o certificado de autenticação VPN para conformidade do dispositivo. Se escolher esta opção, forneça o **EKU** (lista de valores separados por vírgulas) e **Hash de emissor**, para o certificado correto que o cliente VPN deve localizar.

         - Para **Windows Information Protection**, forneça a geridas por empresas identidade empresarial, que é normalmente domínio principal da sua organização, por exemplo, *contoso.com*. Pode especificar vários domínios que a organização é proprietária, separando-as com o "|" carateres. Por exemplo, *contoso.com|newcontoso.com*.   
            Para mais informações sobre o Windows Information Protection, consulte [criar uma política de proteção de informações do Windows (WIP) através do Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar o acesso condicional para VPN](media/vpn-conditional-access.png)

         Quando suportado pela versão do Windows que executa o Configuration Manager _e_ o método de autorização selecionada, pode escolher **configurar** para abrir a caixa de diálogo de propriedades do Windows e configurar as propriedades do método de autenticação.  Se **configurar** está desativada, utilize um meio diferente para configurar as propriedades do método de autenticação.

2.  No **as definições de Proxy** página do **VPN Assistente para criar perfil**, verifique o **configurar definições de proxy para este perfil VPN** caixa se a ligação VPN utilizar um servidor proxy. Em seguida, forneça o proxy de informações do servidor. Para obter mais informações, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Em computadores Windows 8.1, o perfil VPN não irá mostrar as informações de proxy até que o se ligar à VPN utilizando esse computador.  


3. Configure definições DNS adicionais (se necessário).  
 No **configurar ligação VPN automática** página, pode configurar o seguinte:  

    -   **Ativar VPN a pedido**: Utilize se pretender configurar mais definições de DNS para dispositivos Windows Phone 8.1. Esta definição só se aplica a dispositivos Windows Phone 8.1 e só deve ser ativada em perfis VPN que vão ser implementado em dispositivos Windows Phone 8.1.

    -   **Lista de sufixos DNS** (apenas para dispositivos Windows Phone 8.1): Configura domínios que irão estabelecer uma ligação VPN. Para cada domínio que especificar, adicione o sufixo DNS, o endereço do servidor DNS e uma das seguintes ações a pedido:  

        -   **Nunca estabelecer**: Nunca abra uma ligação VPN.  

        -   **Estabelecer se necessário**: Apenas abra uma ligação VPN se o dispositivo tem de se ligar aos recursos.  

        -   **Estabelecer sempre**: Abra sempre a ligação VPN.  

    -   **Intercalar**: Copia todos os sufixos DNS que configurou para o **lista de redes fidedignas**.  

    -   **Lista de redes fidedignas** (apenas para dispositivos Windows Phone 8.1): Especifique um sufixo DNS em cada linha. Se o dispositivo estiver numa rede fidedigna, a ligação VPN não será aberta.  

    -   **Lista de pesquisa de sufixos** (apenas para dispositivos Windows Phone 8.1): Especifique um sufixo DNS em cada linha. Cada sufixo DNS será procurado ao ligar a um Web site utilizando um nome abreviado.  

     Por exemplo, pode especificar os sufixos DNS, **dominio1.contoso.com** e **dominio2.contoso.com**e, em seguida, avance para o URL **http://mywebsite**. Serão procurados os seguintes endereços:  

    -   **http://omeusite.dominio1.contoso.com**  

    -   **http://omeusite.dominio2.contoso.com**  

    > [!NOTE]  
    >  Apenas para dispositivos Windows Phone 8.1  
    >   
    >  Quando o *enviar fego de rede através da ligação VPN* opção está selecionada *e* a ligação VPN utiliza túneis completos, a ligação VPN abre automaticamente com o primeiro perfil de dispositivo. Para abrir uma ligação com um perfil diferente, defina o perfil pretendido como predefinição.  
    >   
    >  Quando o *enviar fego de rede através da ligação VPN* opção é *não* selecionado *e* a ligação VPN utiliza a divisão de túnel, as ligações VPN aberta automaticamente para rotas configuradas ou sufixos DNS específico da ligação.  


4. No **plataformas suportadas** página do **VPN Assistente para criar perfil**, selecione os sistemas operativos nos quais o perfil VPN será instalado ou escolha **Selecionar tudo** para instalar o perfil da VPN em todos os sistemas operativos disponíveis.  

5. Conclua o assistente. O **perfis VPN** no nó de **ativos e compatibilidade** área de trabalho mostra o novo perfil VPN.  


**Implementar**: Consulte [implementar Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para obter mais informações sobre como implementar perfis VPN.

### <a name="next-steps"></a>Passos seguintes  
 Utilize os tópicos seguintes para o ajudar a planear, configurar, operar e manter perfis VPN no Configuration Manager.  

-   [Pré-requisitos para perfis VPN no System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis VPN no System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
