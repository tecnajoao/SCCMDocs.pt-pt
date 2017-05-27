---
title: "Planear e configurar a gestão de aplicações | Documentos do Microsoft"
description: "Implementar e configurar as dependências necessárias para implementar aplicações no System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1c43c4968f93985515249ddb117269f8ed61302a
ms.openlocfilehash: 46cc3fcfd9516cf1c124e24b50d0aac0cb0025dc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planear e configurar a gestão de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a implementar as dependências necessárias para implementar aplicações no System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|------------------|----------------------|  
|Os Serviços de Informação Internet (IIS) são necessários nos servidores do sistema de sites que executam o ponto de sites do Catálogo de Aplicações, o ponto de serviço Web do Catálogo de Aplicações, o ponto de gestão e o ponto de distribuição.|Para mais informações sobre este requisito, consulte o artigo [configurações suportadas](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivos móveis que são inscritos pelo Configuration Manager|Quando as aplicações de início de sessão de código para implementá-las em dispositivos móveis, não utiliza um certificado que foi criado utilizando um modelo da versão 3 (**Windows Server 2008, Enterprise Edition**). Este modelo de certificado cria um certificado que não é compatível com aplicações do Configuration Manager para dispositivos móveis.<br /><br /> Se utilizar serviços de certificados do Active Directory para assinar código para aplicações para dispositivos móveis, não utilize um modelo de certificado de versão 3.|  
|Os clientes devem ser configurados para auditar eventos de início de sessão se pretender criar automaticamente afinidades de dispositivo do utilizador.|O cliente do Configuration Manager lê eventos de início de sessão do tipo **êxito** a partir do registo de eventos de segurança de PCs para determinar as afinidades de dispositivo do utilizador automática.  Estes eventos estão ativados através das políticas de duas auditoria seguintes: "<br>**Auditar eventos de início de sessão de conta**<br>**Auditar eventos de início de sessão**<br>Para criar automaticamente relações entre utilizadores e dispositivos, certifique-se de que estas duas definições estão ativadas nos computadores cliente. Pode utilizar a Política de Grupo do Windows para configurar estas definições.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   

|Dependência|Mais informações|  
|------------------|----------------------|  
|Ponto de gestão|Os clientes contactar um ponto de gestão para transferir a política de cliente, localizar o conteúdo e estabelecer ligação ao catálogo de aplicações.<br /><br /> Se os clientes não conseguirem aceder a um ponto de gestão, não poderão utilizar o Catálogo de Aplicações.|  
|Ponto de distribuição|Antes da implementação das aplicações nos clientes, tem de ter pelo menos um ponto de distribuição na hierarquia. Por predefinição, durante uma instalação padrão, o servidor do site tem uma função de site do ponto de distribuição ativada. O número e a localização dos pontos de distribuição varia consoante os requisitos específicos da sua empresa.<br /><br /> Para mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Definições do cliente|Muitas definições de cliente controlam a forma como as aplicações são instaladas no cliente e o utilizador experiência do cliente. Estas definições do cliente incluem o seguinte:<br /><br /><ul><li>Agente do computador</li><li>Reinício do computador</li><li>Implementação de software</li><li>Afinidade de dispositivo e utilizador</li></ul> Para mais informações sobre estas definições de cliente, consulte o artigo [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para sobre como configurar definições de cliente, consulte o artigo [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).|  
|Para o Catálogo de Aplicações:<br /><br /> Contas de utilizador detetadas|O Configuration Manager primeiro tem de detetar utilizadores antes de poderem ver e pedir aplicações a partir do catálogo de aplicações. Para obter mais informações, consulte o artigo [executar a deteção](/sccm/core/servers/deploy/configure/run-discovery).|  
|Cliente de App-V 4.6 SP1 ou posterior para executar aplicações virtuais|Para poder criar aplicações virtuais no Configuration Manager, computadores cliente têm de ter o App-V 4.6 SP1 cliente ou posterior instalado.<br /><br /> Tem também de atualizar o cliente de App-V com a correção descrita no Base de dados de conhecimento [artigo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) antes de poder implementar aplicações virtuais.|  
|Ponto de serviço Web do Catálogo de Aplicações|O ponto de serviço Web do Catálogo de Aplicações é uma função do sistema de sites que fornece informações sobre software disponível na Biblioteca de Software para o Web site do Catálogo de Aplicações.<br /><br /> Para mais informações sobre como configurar esta função do sistema de sites, consulte o artigo [configurar o Centro de Software e o catálogo de aplicações (apenas para PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto de site do Catálogo de Aplicações|O ponto do Web site do Catálogo de Aplicações é uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível.<br /><br /> Para mais informações sobre como configurar esta função do sistema de sites, consulte o artigo [configurar o Centro de Software e o catálogo de aplicações (apenas para PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto do Reporting Services|Para poder utilizar os relatórios no Configuration Manager para gestão de aplicações, tem primeiro de instalar e configurar um ponto do reporting services.<br /><br /> Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gestão de aplicações|Tem de ter as seguintes permissões de segurança para gerir aplicações.<br /><br /> O **autor da aplicação** função de segurança inclui as permissões listadas anteriormente que são necessárias para criar, alterar e extinguir aplicações no Configuration Manager.<br /><br /> **Para implementar aplicações:**<br /><br /> O **Gestor de implementação de aplicação** função de segurança inclui as permissões listadas anteriormente que são necessárias para implementar aplicações no Configuration Manager.<br /><br /> O **administrador da aplicação** função de segurança tem todas as permissões de ambas as **autor da aplicação** e o **Gestor de implementação de aplicação** funções de segurança.<br /><br /> Para obter mais informações, consulte o artigo [configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurar o Centro de Software e o Catálogo de Aplicações (apenas PCs Windows)  

 No System Center Configuration Manager, tem agora duas opções para os utilizadores alterar as definições, procurar as aplicações e instalar aplicações:  

-   **O novo Centro de Software** -o novo Centro de Software tem um aspeto Moderno. As aplicações que poderiam ter apareceu apenas no catálogo de aplicações de dependentes do Silverlight (aplicações disponíveis para o utilizador) agora apresentada no Centro de Software no **aplicações** separador. O catálogo de aplicações ainda podem ser acedido utilizando a ligação no **estado da instalação** separador do Centro de Software.  

     Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**.  

    > [!IMPORTANT]  
    >  Embora já não é necessário estabelecer ligação ao catálogo de aplicações, tem ainda de configurar o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações como detalhadas na secção seguinte.  

-   **O Centro de Software anterior e o Catálogo de Aplicações** - Por predefinição, os utilizadores continuam a ligar-se à versão anterior do Centro de Software e a ligar-se ao Catálogo de Aplicações (é necessário um browser com capacidade para Silverlight) para procurar as aplicações disponíveis.  

 Qualquer versão optar por utilizar, Centro de Software é instalado automaticamente quando instala o cliente do Configuration Manager em Windows PCs.  

    > [!TIP]  
    >  A versão do Centro de Software que os utilizadores visualizam baseia-se definições de cliente do Configuration Manager. Isto dá-lhe a flexibilidade para controlar a versão que está a ser utilizada com base nas definições de cliente personalizadas que implementa para uma coleção. 

    > [!IMPORTANT]
    > Nos próximos meses, iremos irá remover a versão anterior do Centro de Software e já não estará disponível para ser utilizada.
    > Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Passos para instalar e configurar o Catálogo de Aplicações e o Centro de Software  

> [!IMPORTANT]  
>  Antes de efetuar estes passos, certifique-se de que cumpriu todos os pré-requisitos listados anteriormente.  

|Passos|Detalhes|Mais informações|  
|-----------|-------------|----------------------|  
|**Passo 1:** Se pretender utilizar ligações HTTPS, certifique-se de que implementou um certificado de servidor web nos servidores do sistema de sites.|Implemente um certificado do servidor Web nos servidores do sistema de sites que executarão o ponto do Web site do Catálogo de Aplicações e o ponto de serviço Web do Catálogo de Aplicações.<br /><br /> Além disso, se pretender que os clientes para utilizar o catálogo de aplicações a partir da Internet, implemente um certificado de servidor web para servidor de sistema de sites de ponto de gestão pelo menos um e configure-o para ligações de cliente a partir da Internet.|Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 2:** Se pretender utilizar um certificado PKI de cliente para ligações a pontos de gestão, implemente um certificado de autenticação de cliente para computadores cliente.|Embora os clientes não utilizarem um certificado PKI de cliente para estabelecer ligação ao catálogo de aplicações, precisam de estabelecer ligação ao ponto de gestão antes de poderem utilizar o catálogo de aplicações. Tem de implementar um certificado de autenticação de cliente nos computadores cliente nos seguintes cenários:<br /><br /><ul><li>Todos os pontos de gestão na intranet aceitam apenas ligações de cliente HTTPS.</li><li>Os clientes estabelecerão ligação ao catálogo de aplicações a partir da Internet.</li></ul>|Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 3:** Instalar e configurar o ponto de serviço web do catálogo de aplicações e o Web site do catálogo de aplicações.|Tem de instalar ambas as funções de sistema de sites no mesmo site. Não necessita de as instalar no mesmo servidor do sistema de sites nem na mesma floresta do Active Directory. Contudo, o ponto de serviço web do catálogo de aplicações têm de estar na mesma floresta que a base de dados do site.|Para mais informações sobre o posicionamento de funções de sistema de sites, consulte o artigo [planear servidores de sistema de sites e funções do sistema de sites](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Para configurar o ponto de serviço web do catálogo de aplicações e o ponto de Web site do catálogo de aplicações, consulte o artigo **passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações**.|  
|**Passo 4:** Configure definições de cliente para o catálogo de aplicações e o Centro de Software.|Se pretender que todos os utilizadores tenham a mesma definição, configure as predefinições do cliente. Caso contrário, configure definições do cliente personalizadas para coleções específicas.|Para mais informações sobre as definições de cliente, consulte o artigo [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para mais informações sobre como configurar estas definições de cliente, consulte o artigo **passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software**.|  
|**Passo 5:** Certifique-se de que o catálogo de aplicações está operacional.|Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou a partir do Centro de Software.|Consulte o artigo **passo 5: Certifique-se de que o catálogo de aplicações está operacional**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedimentos suplementares para instalar e configurar o Catálogo de Aplicações e o Centro de Software  
 Utilize as informações seguintes quando os passos da tabela anterior exigirem procedimentos adicionais.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações  
 Estes procedimentos configuram as funções do sistema de sites do Catálogo de Aplicações. Escolha um dos seguintes dois procedimentos consoante pretenda instalar um servidor de sistema de sites novo ou utilizar um servidor de sistema de sites existente:  

> [!NOTE]  
>  Não é possível instalar o Catálogo de Aplicações num site secundário ou num site de administração central.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Novo servidor de sistema de sites  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.  

3.  No **base** separador o **criar** grupo, selecione **criar servidor do sistema de sites**.  

4.  No **geral** página, especifique as definições gerais para o sistema de sites e, em seguida, selecione **seguinte**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente para utilizar o catálogo de aplicações através da Internet, especifique a Internet completamente qualificado (FQDN) do nome de domínio.  

5.  No **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web site do catálogo de aplicações** da lista de funções disponíveis e, em seguida, escolha **seguinte**.  

6.  Conclua o assistente.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Servidor de sistema de sites existente  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor a utilizar para o catálogo de aplicações.  

3.  No **base** separador o **servidor** grupo, selecione **adicionar funções do sistema de sites**.  

4.  No **geral** página, especifique as definições gerais para o sistema de sites e, em seguida, selecione **seguinte**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente para utilizar o catálogo de aplicações através da Internet, especifique a Internet completamente qualificado (FQDN) do nome de domínio.  

5.  No **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web site do catálogo de aplicações** da lista de funções disponíveis e, em seguida, escolha **seguinte**.  

6.  Conclua o assistente.  

7. Verifique a instalação destas funções do sistema de sites utilizando as mensagens de estado e revendo os ficheiros de registo:  

    Mensagens de estado: Utilize os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, o ID de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que o Gestor de componentes do Site instalou com êxito o ponto de Web site do catálogo de aplicações.  

    Ficheiros de registo: Procurar **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Para obter mais informações, procure o **awebsvcMSI.log** e **portlwebMSI.log** ficheiros de registo.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software  
 Este procedimento configura as predefinições de cliente do Catálogo de Aplicações e do Centro de Software que serão aplicadas em todos os dispositivos da hierarquia. Se pretender que estas definições aplicam-se apenas nalguns dispositivos, pode criar uma definição de cliente personalizada e implementá-la para uma coleção que tenha os dispositivos que terão definições específicas. Para mais informações sobre como criar uma definição personalizada do dispositivo, consulte o [como criar e implementar definições personalizadas do cliente](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) secção a [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) artigo.  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

3.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

4.  Reveja e configure as definições relacionadas com as notificações do utilizador, o Catálogo de Aplicações e o Centro de Software. Por exemplo:  

    1.  Grupo**Agente do Computador** :  

        -   **Ponto de Web sites Predefinido do Catálogo de Aplicações**  

        -   **Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer**  

        -   **Nome da organização apresentada no Centro de Software**  

            > [!TIP]  
            >  Para especificar o nome da organização que é apresentado no catálogo de aplicações e configurar o tema do Web site, utilize o **personalização** separador nas propriedades do Web site de catálogo de aplicações.  

        -   **Utilizar o Centro de Software novo** -definido como **Sim** se pretender utilizar o novo Centro de Software, que permite aos utilizadores procurar e instalar as aplicações disponíveis sem a necessidade de aceder ao catálogo de aplicações (o que necessita de um browser ativado para Silverlight).  

        -   **Permissões de instalação**  

        -   **Mostrar notificações para novas implementações**  

    2.  Grupo**Gestão de Energia** :  

        -   **Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia**  

    3.  Grupo**Ferramentas Remotas** :  

        -   **Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software**  

    4.  Grupo**Afinidade de Dispositivo e Utilizador** :  

        -   **Permitir ao utilizador a definição dos seus dispositivos primários**  

    > [!NOTE]  
    >  Para mais informações sobre as definições de cliente, consulte o artigo [sobre definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Escolher **OK** para fechar o **predefinições de cliente** caixa de diálogo.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção de política para um único cliente, consulte o artigo [como gerir clientes](../../core/clients/manage/manage-clients.md).

#### <a name="how-to-customize-software-center-branding"></a>Como personalizar uma imagem corporativa do Centro de Software

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresentará o nome da organização especificado no **agente do computador** definição de cliente **nome da organização** apresentada no Centro de Software. Para obter instruções, consulte o artigo [como configurar as definições de cliente](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/configure-client-settings).
2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações é instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificado nas propriedades de função de servidor de site do catálogo de aplicações Web site ponto. Para obter mais informações, consulte o artigo [opções de configuração de ponto de Web site do catálogo de aplicações](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Se uma subscrição do Microsoft Intune é configurada e ligada ao Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, cor e a empresa logótipo especificado nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

> [!IMPORTANT]  
>  Uma imagem corporativa do Centro de software está sincronizada com o serviço Intune que cada nos últimos 14 dias, por isso, poderá haver um atraso antes das alterações que fizer no Intune são apresentadas no Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passo 5: Certifique-se de que o catálogo de aplicações está operacional  
 Utilize os procedimentos seguintes para verificar se o Catálogo de Aplicações está operacional. Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou a partir do Centro de Software.  

> [!NOTE]  
>  O catálogo de aplicações requer o Microsoft Silverlight, o que é instalado automaticamente como um pré-requisito de cliente do Configuration Manager. Se utilizar o catálogo de aplicações diretamente a partir de um browser utilizando um computador que não tenha o cliente do Configuration Manager, primeiro certifique-se de que o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos em falta são uma das principais razões para o catálogo de aplicações funcionar incorretamente após a instalação. Confirme os pré-requisitos das funções do sistema de sites do Catálogo de Aplicações. Pode fazê-lo utilizando o [configurações suportadas](../../core/plan-design/configs/supported-configurations.md) artigo.  

> [!NOTE]  
>  Se iniciar sessão utilizando uma conta de administrador de domínio, as mensagens de notificação do cliente do Configuration Manager (por exemplo, mensagens com a indicação de que está disponível novo software) não serão apresentadas.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Para utilizar o catálogo de aplicações diretamente a partir de um browser  

-   Num browser, introduza o endereço do Web site do catálogo de aplicações e confirme que a página web mostra os três separadores: **Catálogo de aplicações**, **meus pedidos de aplicações**, e **meus dispositivos**.  

     Selecione e utilize o endereço adequado na lista seguinte de catálogo de aplicações, onde &lt;servidor&gt; é o nome do computador, o FQDN da intranet ou o FQDN de Internet:  

    -   Ligações de cliente HTTPS e predefinições definições da função do sistema de sites: **https://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Ligações de cliente HTTP e predefinições definições da função do sistema de sites: **http://&lt;servidor&gt;/CMApplicationCatalog**  

    -   HTTPS ligações de cliente e definições de função do sistema de site personalizado: **https://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

    -   Ligações de cliente HTTP e definições de função de sistema de sites personalizada: **http://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Para utilizar o catálogo de aplicações a partir do Centro de Software (não se aplica a nova versão do Centro de Software)  

1.  Num computador cliente, escolha **iniciar** > **todos os programas** > **Microsoft System Center 2012** > **do Configuration Manager** > **Centro de Software**.  

2.  Se tiver configurado previamente um nome da organização para o Centro de Software como uma definição do cliente, certifique-se de que este é apresentado conforme especificado.  

3.  Escolher **localizar aplicações adicionais no catálogo de aplicações**e confirme que a página mostra os três separadores: **Catálogo de aplicações**, **meus pedidos de aplicações**, e **meus dispositivos**.  

> [!WARNING]  
>  Depois de instalar as funções de sistema de sites do catálogo de aplicações, serão não ver de imediato o catálogo de aplicações quando escolhe o **localizar aplicações adicionais no catálogo de aplicações** ligação a partir do Centro de Software. O Catálogo de Aplicações fica disponível do Centro de Software quando o cliente transferir a respetiva política do cliente ou num período máximo de 25 horas após a instalação das funções do sistema de sites do Catálogo de Aplicações.  

