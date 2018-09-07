---
title: Plano de gestão de aplicações
titleSuffix: Configuration Manager
description: Implementar e configurar as dependências necessárias para implantar aplicativos no Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df936f3ab5567840560497edd60a32f3bbb9c74d
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893606"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planear e configurar a gestão de aplicações no Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para ajudar a implementar as dependências necessárias para implementar aplicações no Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  


### <a name="internet-information-services-iis"></a>Serviços de Informação de Internet (IIS)

IIS é necessário nos servidores que execute o seguinte site funções de sistema: 
- Ponto de site do Catálogo de Aplicações  
- Ponto de serviço Web do Catálogo de Aplicações  
- Ponto de gestão  
- Ponto de distribuição  

Para obter mais informações sobre este requisito, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificados no assinada por código aplicações para dispositivos móveis

Quando os aplicativos de código de início de sessão para implementá-las em dispositivos móveis, não utiliza um certificado que tenha sido criado com um modelo de versão 3 (**Windows Server 2008, Enterprise Edition**). Este modelo de certificado cria um certificado que é incompatível com aplicações do Configuration Manager para dispositivos móveis.

Se utilizar os serviços de certificados do Active Directory a aplicações de código de início de sessão para aplicações para dispositivos móveis, não utilize um modelo de certificado da versão 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditar eventos de início de sessão para a afinidade dispositivo / utilizador  

Se pretender criar automaticamente afinidades dispositivo / utilizador, configure-os para auditar eventos de início de sessão.

Para determinar afinidades dispositivo / utilizador automáticas, o cliente do Configuration Manager lê eventos de início de sessão do tipo **êxito** do registo de eventos de segurança do Windows. Ative estes eventos com as políticas de auditoria de duas seguintes:
- **Auditar eventos de início de sessão de conta**
- **Auditar eventos de início de sessão**

Para criar automaticamente relações entre utilizadores e dispositivos, certifique-se de que estas duas definições estão ativadas nos computadores cliente. Pode utilizar a Política de Grupo do Windows para configurar estas definições.

Para obter mais informações sobre a afinidade dispositivo / utilizador, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   


### <a name="management-point"></a>Ponto de gestão

Os clientes contactar um ponto de gestão para transferir a política de cliente, para localizar os conteúdos e para ligar ao catálogo de aplicações. Se os clientes não é possível aceder um ponto de gestão, estes não podem utilizar o catálogo de aplicações.

> [!Note]  
> A partir da versão 1806, funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Para obter mais informações, consulte [configurar o Centro de Software](#bkmk_userex).<!--1358309-->  
  

### <a name="distribution-point"></a>Ponto de distribuição

Antes de poder implementar aplicações para os clientes, tem de, pelo menos, uma distribuição ponto na hierarquia. Por predefinição, durante uma instalação padrão, o servidor do site tem uma função de site do ponto de distribuição ativada. O número e a localização dos pontos de distribuição são variam de acordo com os requisitos específicos do seu ambiente. 

Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services

Para utilizar os relatórios no Configuration Manager para gestão de aplicações, primeiro instale e configure um ponto do reporting services.

Para obter mais informações, consulte [relatórios no Configuration Manager](/sccm/core/servers/manage/reporting).  


### <a name="client-settings"></a>Definições do cliente

Muitas definições de cliente controlam como o cliente instala aplicativos e a experiência de utilizador no dispositivo. Estas definições de cliente incluem os seguintes grupos:
- Agente do computador  
- Reinício do computador  
- Centro de software  
- Implementação de software  
- Afinidade dispositivo / utilizador  

Para obter mais informações, consulte os artigos seguintes:
- [Acerca das definições de cliente](/sccm/core/clients/deploy/about-client-settings)  
- [Como configurar as definições do cliente](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>Permissões de segurança para gestão de aplicações

- O **autor da aplicação** função de segurança inclui as permissões necessárias para criar, alterar e extinguir aplicações.  

- O **Gestor de implementação de aplicação** função de segurança inclui as permissões necessárias para implementar aplicações.  

- O **administrador da aplicação** função de segurança tem todas as permissões de ambas as **autor da aplicação** e o **Gestor de implementação de aplicação** funções de segurança.  

Para obter mais informações, consulte [configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Cliente de App-V 4.6 SP1 ou posterior para executar aplicações virtuais

Para criar aplicações virtuais no Configuration Manager, instale o App-V 4.6 SP1 ou posterior no dispositivos.

Antes de implementar aplicações virtuais, também de atualizar o cliente de App-V com a correção descrita no [artigo do Microsoft Support 2645225](https://support.microsoft.com/help/2645225).  


### <a name="discovered-user-accounts-for-application-catalog"></a>Contas de utilizador detetadas para catálogo de aplicações

Primeiro tem do Configuration Manager detetar contas de utilizador antes dos utilizadores podem ver e pedir aplicações a partir do catálogo de aplicações. Para obter mais informações, consulte [executar a deteção](/sccm/core/servers/deploy/configure/run-discovery).  


### <a name="application-catalog-web-service-point"></a>Ponto de serviço Web do Catálogo de Aplicações

O ponto de serviço web do catálogo de aplicações é uma função de sistema de sites que fornece informações sobre software disponível a partir de sua biblioteca de software para o site do catálogo de aplicações que o acesso aos utilizadores.

Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software](#bkmk_userex).  

> [!Note]  
> A partir da versão 1806, a função de ponto de serviço de web de catálogo de aplicações não se encontra *necessária*, mas ainda *suportado*.<!--1358309-->  
> 
> O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="application-catalog-website-point"></a>Ponto de site do Catálogo de Aplicações

O ponto do Web site do Catálogo de Aplicações é uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível.
"Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software](#bkmk_userex).

> [!Note]  
> A partir da versão 1806, a função de ponto de Web site de catálogo de aplicações não se encontra *necessária*, mas ainda *suportado*.<!--1358309-->  
> 
> O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="bkmk_userex"></a> Configurar o Centro de Software  

Os utilizadores alteram as definições, procurarem as aplicações e instalam aplicações a partir do Centro de Software. Quando instala o cliente do Configuration Manager num dispositivo Windows, ele instala automaticamente o Centro de Software também. O novo Centro de Software tem uma aparência moderna. Aplicações que eram apresentadas apenas no catálogo de aplicações dependente do Silverlight (aplicações disponíveis ao utilizador) agora aparecer no Centro de Software no **aplicativos** separador. Para obter mais informações sobre os outros recursos do Centro de Software, consulte a [guia de utilizador do Centro de Software](/sccm/core/understand/software-center).  

Reveja os seguintes melhoramentos ao centro de Software: 

#### <a name="starting-in-version-1802"></a>A partir da versão 1802

- A definição de cliente **utilizar o novo Centro de Software** no **agente do computador** grupo está ativado por predefinição. A versão anterior do Centro de Software já não é suportada. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Os utilizadores podem procurar e instalar aplicações disponíveis para o utilizador no Azure Active Directory (Azure AD)-dispositivos associados a um. Para obter mais informações, consulte [implementar aplicações disponíveis para o utilizador em dispositivos associados ao AD Azure](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

#### <a name="starting-in-version-1806"></a>A partir da versão 1806

- Especifique a visibilidade da ligação de site do catálogo de aplicações no **estado de instalação** separador do Centro de Software. Para obter mais informações, consulte [Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center) as definições de cliente.  

- Funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Esta alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. Centro de software baseia-se agora no ponto de gestão para obter essa informação, que ajuda a escala de ambientes de maior melhor ao atribuir-lhes [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Se estiver a utilizar atualmente o catálogo de aplicações e atualizar o Configuration Manager para a versão 1806, continuam a funcionar. Os catálogo site web e de ponto de serviço ponto funções da aplicação já não estão *necessária*, mas ainda *suportado*. O **experiência de usuário do Silverlight** para o catálogo de aplicações *ponto do Web site* já não é suportada. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). 
    > 
    > Comece a planejar a remover as funções do catálogo de aplicações da sua infraestrutura no futuro. Tire partido das melhorias do Centro de Software para utilizar o ponto de gestão e simplificar seu ambiente do Configuration Manager.  

Utilize a tabela seguinte para ajudar a compreender os requisitos para o Centro de Software, consoante a versão específica do Configuration Manager:

| Tipo de Dispositivo | Versão do site | Infraestrutura | 
|-----------------|--------------|----------------|
| Dispositivo associado ao AD do Azure</br>(ou "cloud associados a um domínio") | 1802 ou 1806 | Ponto de gestão para todas as implementações de aplicações | 
| [Azure híbrido associado ao AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) dispositivos na internet | 1802 ou 1806 | Gateway de gestão e ponto de gestão para todas as implementações de aplicações na cloud |
| Dispositivo de associados a um domínio no local do Active Directory | 1802 | Catálogo de aplicações necessário para as aplicações disponíveis ao utilizador através do Centro de Software |
| Dispositivo de associados a um domínio no local do Active Directory | 1806 | Ponto de gestão para todas as implementações de aplicações |


> [!Important]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.



## <a name="branding-software-center"></a>Imagem corporativa do Centro de Software

Alterar a aparência do Centro de Software para satisfazer a sua organização a imagem corporativa da requisitos. Esta configuração ajuda os utilizadores confiança Centro de Software. 

Gestor de configuração aplica-se de marca personalizada para o Centro de Software, de acordo com as prioridades seguintes:  

- Se ainda não instalou o catálogo de aplicações (recomendado):  

    1. **Centro de software** as definições de cliente. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. **Nome da organização** definição cliente **agente do computador** grupo. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Se instalou o catálogo de aplicações:  

    1. **Centro de software** as definições de cliente. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Se liga uma subscrição do Microsoft Intune ao Configuration Manager, o Centro de Software apresenta os *nome da organização*, *cor*, e *logótipo da empresa* que Especifique as propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. O *nome da organização* e *cor* que especificou nas propriedades do ponto de Web site de catálogo de aplicações. Para obter mais informações, consulte [opções de configuração do ponto de Web sites do catálogo de aplicações](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. **Nome da organização** definição cliente **agente do computador** grupo. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

#### <a name="configure-software-center-branding"></a>Configurar a imagem corporativa do Centro de Software
<!-- 1351224 --> Personalize a aparência do Centro de Software ao adicionar a sua organização de elementos de marca e especificando a visibilidade dos separadores. 

Para obter mais informações, consulte os artigos seguintes:
- [Centro de software](/sccm/core/clients/deploy/about-client-settings#software-center) grupo de definições de cliente  
- [Como configurar as definições do cliente](/sccm/core/clients/deploy/configure-client-settings)  



## <a name="bkmk_appcat"></a> Instalar e configurar o catálogo de aplicações  

> [!Note]  
> A partir da versão 1806, os catálogo site web e de ponto de serviço ponto funções da aplicação já não estão *necessária*, mas ainda *suportado*. Para obter mais informações, consulte [configurar o Centro de Software](#bkmk_userex).  
> 
> O **experiência de usuário do Silverlight** para o catálogo de aplicações *ponto do Web site* já não é suportada. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

> [!IMPORTANT]  
>  Antes de efetuar estes passos, certifique-se de que todas as dependências estão em vigor. Para obter mais informações, consulte as seguintes secções neste artigo:
> - [Dependências externas ao Configuration Manager](#dependencies-external-to-configuration-manager)  
> - [Dependências do Configuration Manager](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>Passo 1: Certificado de servidor Web para HTTPS

Se utilizar ligações HTTPS, implemente um certificado de servidor web para os servidores de sistema de sites para o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações. 

Se pretender que os clientes para utilizarem o catálogo de aplicações da internet, implemente um certificado de servidor web, pelo menos, um ponto de gestão. Configure ligações de cliente através da internet.

Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Passo 2: Certificado de autenticação de cliente para HTTPS

Se utilizar um certificado PKI de cliente para ligações a pontos de gestão, implemente um certificado de autenticação de cliente para computadores cliente. Embora os clientes não utilizam um certificado PKI de cliente para ligar ao catálogo de aplicações, deve ligar um ponto de gestão antes de poderem utilizar o catálogo de aplicações. 

Implemente um certificado de autenticação de cliente nos computadores de cliente nos seguintes cenários:
- Todos os pontos de gestão na intranet aceitam apenas ligações de cliente HTTPS.
- Os clientes ligam ao catálogo de aplicações a partir da internet.

Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Passo 3: Instalar e configurar as funções de catálogo de aplicações

Instale o ponto de serviço web do catálogo de aplicações e as funções de Web site do catálogo de aplicações no mesmo site. Não tem de instalá-los no mesmo servidor ou na mesma floresta do Active Directory. No entanto, o ponto de serviço web do catálogo de aplicações tem de ser na mesma floresta que o banco de dados do site.

Para obter mais informações sobre posicionamento do servidor, consulte [planear servidores de sistema de sites e funções de sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

> [!NOTE]  
> Instale o catálogo de aplicações num site primário. Não é possível instalá-lo num site secundário ou o site de administração central.  

Instale o catálogo de aplicações num servidor de sistema de sites novo ou um servidor existente no site. Para obter mais informações sobre o procedimento geral, consulte [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). No Assistente para adicionar uma função de sistema de sites ou criar um servidor de sistema de sites, selecione as seguintes funções a partir da lista:  
- **Ponto de serviço da web de catálogo de aplicações**  
- **Ponto de Web site do catálogo de aplicações**  

> [!TIP]  
>  Se pretender que os computadores cliente utilizarem o catálogo de aplicações através da internet, especifique a internet (FQDN) de nome de domínio completamente qualificado.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verificar a instalação destas funções de sistema de sites  

- Mensagens de estado: Utilize os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, o ID de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que o Gestor de componentes do Site instalou com êxito o ponto de sites do catálogo de aplicações.  

- Ficheiros de registo: Procure **smsawebsvcsetup. log** e **Smsportalwebsetup**.  

    Para obter mais informações, procure o **awebsvcmsi. log** e **Portlwebmsi** ficheiros de registo.  


### <a name="step-4-configure-client-settings"></a>Passo 4: Configurar definições de cliente

Se pretender que todos os utilizadores tenham as mesmas definições, configure as predefinições de cliente. Caso contrário, configure definições do cliente personalizadas para coleções específicas.

Para obter mais informações, consulte os artigos seguintes:
- [Acerca das definições de cliente](/sccm/core/clients/deploy/about-client-settings)  
    - Agente do computador  
    - Reinício do computador  
    - Centro de software  
    - Implementação de software  
    - Afinidade dispositivo / utilizador  
- [Como configurar as definições do cliente](/sccm/core/clients/deploy/configure-client-settings)  

O cliente do Configuration Manager configura os dispositivos com estas definições quando a próxima vez que transferir política do cliente. Para acionar a obtenção de política para um único cliente, consulte [como gerir clientes](/sccm/core/clients/manage/manage-clients).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passo 5: Certifique-se de que o catálogo de aplicações está operacional

Utilize os procedimentos seguintes para verificar se o Catálogo de Aplicações está operacional. 

> [!NOTE]  
>  A experiência de utilizador do catálogo de aplicações requer o Microsoft Silverlight. Se utilizar o catálogo de aplicações diretamente a partir de um browser, primeiro certifique-se de que o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos em falta estão entre as razões mais habituais para o catálogo de aplicações a funcionar incorretamente após a instalação. Confirme os pré-requisitos para as funções de sistema de sites do catálogo de aplicações. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

Num browser, introduza o endereço do site do catálogo de aplicações. Confirme que a página da web mostra os três separadores: **Catálogo de aplicações**, **os meus pedidos de aplicação**, e **os meus dispositivos**.  

Utilize o endereço apropriado ao catálogo de aplicações na lista seguinte, onde &lt;servidor&gt; é o nome do computador, intranet, FQDN ou o FQDN de internet:  

- Definições de função do sistema de sites de ligações de cliente HTTPS e predefinições: **https://&lt;server&gt;/CMApplicationCatalog**  

- Ligações de cliente HTTP e predefinições de definições de função do sistema de sites: **http://&lt;server&gt;/CMApplicationCatalog**  

- HTTPS ligações de cliente e definições de função do sistema de site personalizada: **https://&lt;server&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

- Ligações de cliente HTTP e definições de função do sistema de site personalizada: **http://&lt;server&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

> [!NOTE]  
>  Se tiver iniciado sessão no dispositivo com uma conta de administrador de domínio, o cliente do Configuration Manager não apresenta as mensagens de notificação. Por exemplo, as mensagens que indica esse novo software estão disponíveis.  

