---
title: "Planear e configurar a gestão de aplicações"
titleSuffix: Configuration Manager
description: "Implementar e configurar as dependências necessárias para implementar aplicações no System Center Configuration Manager."
ms.custom: na
ms.date: 11/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: "13"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: cd06d3ee2ea14c9ff1b9cf09980c2b25a5263db9
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planear e configurar a gestão de aplicações no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a implementar as dependências necessárias para implementar aplicações no System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|------------------|----------------------|  
|Serviços de informação Internet (IIS) é necessário nos servidores de sistema de sites que executam o ponto de Web site do catálogo de aplicações, o ponto de serviço web do catálogo de aplicações, o ponto de gestão e o ponto de distribuição.|Para obter mais informações sobre este requisito, consulte [configurações suportadas](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivos móveis que são inscritos pelo Configuration Manager|Quando as aplicações de assinar com código para implementá-las em dispositivos móveis, não utilize um certificado que foi gerado utilizando um modelo da versão 3 (**Windows Server 2008, Enterprise Edition**). Este modelo de certificado cria um certificado que é incompatível com aplicações do Configuration Manager para dispositivos móveis.<br /><br /> Se utilizar o Active Directory Certificate Services para aplicações de assinar com código para aplicações para dispositivos móveis, não utilize um modelo de certificado da versão 3.|  
|Os clientes devem ser configurados para auditar eventos de início de sessão, se pretender criar automaticamente afinidades de dispositivo do utilizador.|O cliente do Configuration Manager lê os eventos de início de sessão do tipo **êxito** do registo de eventos de segurança do computador para determinar afinidades dispositivo / utilizador automáticas.  Estes eventos estão ativados pelas políticas de dois auditoria seguintes:<br>**Auditar eventos de início de sessão de conta**<br>**Auditar eventos de início de sessão**<br>Para criar automaticamente relações entre utilizadores e dispositivos, certifique-se de que estas duas definições estão ativadas nos computadores cliente. Pode utilizar a Política de Grupo do Windows para configurar estas definições.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   

|Dependência|Mais informações|  
|------------------|----------------------|  
|Ponto de gestão|Os clientes contactar um ponto de gestão para transferir a política de cliente, para localizar os conteúdos e para estabelecer ligação ao catálogo de aplicações.<br /><br /> Se os clientes não é possível aceder a um ponto de gestão, estes não podem utilizar o catálogo de aplicações.|  
|Ponto de distribuição|Antes da implementação das aplicações nos clientes, tem de ter pelo menos um ponto de distribuição na hierarquia. Por predefinição, durante uma instalação padrão, o servidor do site tem uma função de site do ponto de distribuição ativada. O número e a localização dos pontos de distribuição variam de acordo com os requisitos específicos da sua empresa.<br /><br /> Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Definições do cliente|Muitas definições de cliente controlam a forma como as aplicações são instaladas no cliente e o utilizador experiência no cliente. Estas definições do cliente incluem o seguinte:<br /><br /><ul><li>Agente do computador</li><li>Reinício do computador</li><li>Implementação de software</li><li>Afinidade dispositivo / utilizador</li></ul> Para obter mais informações sobre estas definições de cliente, consulte [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para obter mais informações sobre como configurar as definições de cliente, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).|  
|Contas de utilizador detetadas para o catálogo de aplicações |O Configuration Manager primeiro tem de detetar contas de utilizador, antes dos utilizadores podem ver e solicitar aplicações a partir do catálogo de aplicações. Para obter mais informações, consulte [executar a deteção](/sccm/core/servers/deploy/configure/run-discovery).|  
|Cliente de App-V 4.6 SP1 ou posterior para executar aplicações virtuais|Para criar aplicações virtuais no Configuration Manager, computadores cliente tem de ter o App-V 4.6 SP1 cliente ou posterior instalado.<br /><br /> Tem também de atualizar o cliente de App-V com a correção descrita no [Base de dados de conhecimento artigo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) antes de poder implementar aplicações virtuais.|  
|Ponto de serviço Web do Catálogo de Aplicações|O ponto de serviço Web do Catálogo de Aplicações é uma função do sistema de sites que fornece informações sobre software disponível na Biblioteca de Software para o Web site do Catálogo de Aplicações.<br /><br /> Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software e o catálogo de aplicações (apenas PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto de site do Catálogo de Aplicações|O ponto do Web site do Catálogo de Aplicações é uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível.<br /><br /> Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software e o catálogo de aplicações (apenas PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto do Reporting Services|Para utilizar os relatórios no Configuration Manager para gestão de aplicações, tem primeiro de instalar e configurar um ponto do Reporting Services.<br /><br /> Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gestão de aplicações|Tem de ter as seguintes permissões de segurança para gerir aplicações:<br /><br /> O **autor da aplicação** função de segurança inclui as permissões listadas anteriormente que são necessárias para criar, alterar e extinguir aplicações no Configuration Manager.<br /><br /> **Para implementar aplicações:**<br /><br /> O **Gestor de implementação de aplicação** função de segurança inclui as permissões listadas anteriormente que são necessários para implementar aplicações no Configuration Manager.<br /><br /> O **administrador da aplicação** função de segurança tem todas as permissões de ambas as **autor da aplicação** e o **Gestor de implementação de aplicação** funções de segurança.<br /><br /> Para obter mais informações, consulte [configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurar o Centro de Software e o Catálogo de Aplicações (apenas PCs Windows)  

 No System Center Configuration Manager, tem agora duas opções para os utilizadores alterar as definições, procurar as aplicações e instalar aplicações:  

-   **O novo Centro de Software**: O novo Centro de Software tem um aspeto Moderno. As aplicações que eram apenas no catálogo de aplicações dependente do Silverlight (aplicações disponíveis ao utilizador) agora apresentadas no Centro de Software no **aplicações** separador. O catálogo de aplicações ainda podem ser acedido utilizando a hiperligação sob o **estado da instalação** separador do Centro de Software.  

     Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**.  

    > [!IMPORTANT]  
    >  Apesar de já não precisam de estabelecer ligação ao catálogo de aplicações, tem ainda de configurar o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações conforme especificado na secção seguinte.  

-   **O Centro de Software anterior e o catálogo de aplicações**: Por predefinição, os utilizadores continuam a ligar para a versão anterior do Centro de Software e ligar ao catálogo de aplicações (é necessário um browser ativado para Silverlight) para procurar as aplicações disponíveis.  

 Independentemente da versão optar por utilizar, o Centro de Software é instalado automaticamente quando instala o cliente do Configuration Manager em Windows PCs.  

    > [!TIP]  
    >  A versão do Centro de Software que os utilizadores visualizam baseia-se nas definições de cliente do Configuration Manager. Isto dá-lhe a flexibilidade para a versão que está a ser utilizada com base nas definições de cliente personalizadas que implementa para uma coleção de controlo. 

    > [!IMPORTANT]
    > Nos próximos meses, iremos irá remover a versão anterior do Centro de Software e já não estará disponível.
    > Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Passos para instalar e configurar o Catálogo de Aplicações e o Centro de Software  

> [!IMPORTANT]  
>  Antes de efetuar estes passos, certifique-se de que cumpriu todos os pré-requisitos listados anteriormente.  

|Passos|Detalhes|Mais informações|  
|-----------|-------------|----------------------|  
|**Passo 1:** Se utilizar ligações HTTPS, certifique-se de que implementou um certificado de servidor web nos servidores do sistema de sites.|Implemente um certificado do servidor Web nos servidores do sistema de sites que executarão o ponto do Web site do Catálogo de Aplicações e o ponto de serviço Web do Catálogo de Aplicações.<br /><br /> Além disso, se pretender que os clientes para utilizarem o catálogo de aplicações da internet, implemente um certificado de servidor web para o servidor do sistema de sites de ponto de gestão, pelo menos, um e configurá-la para ligações de cliente a partir da internet.|Para obter mais informações sobre os requisitos de certificado, consulte [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 2:** Se utilizar um certificado PKI de cliente para ligações a pontos de gestão, implemente um certificado de autenticação de cliente para computadores cliente.|Embora os clientes não utilizam um certificado PKI de cliente para estabelecer ligação ao catálogo de aplicações, precisam de estabelecer ligação ao ponto de gestão antes de poderem utilizar o catálogo de aplicações. Tem de implementar um certificado de autenticação de cliente nos computadores cliente nos seguintes cenários:<br /><br /><ul><li>Todos os pontos de gestão na intranet aceitam apenas ligações de cliente HTTPS.</li><li>Os clientes ligam ao catálogo de aplicações da internet.</li></ul>|Para obter mais informações sobre os requisitos de certificado, consulte [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 3:** Instalar e configurar o ponto de serviço web do catálogo de aplicações e o Web site do catálogo de aplicações.|Tem de instalar ambas as funções de sistema de sites no mesmo site. Não tem de instalá-los no mesmo servidor de sistema do site ou na mesma floresta do Active Directory. No entanto, o ponto de serviço web do catálogo de aplicações tem de ser na mesma floresta que a base de dados do site.|Para mais informações sobre o posicionamento de funções de sistema de sites, consulte [planear servidores de sistema de sites e funções de sistema de sites](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Para configurar o ponto de serviço web do catálogo de aplicações e o ponto de Web site do catálogo de aplicações, consulte **passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações**.|  
|**Passo 4:** Configure definições de cliente para o catálogo de aplicações e o Centro de Software.|Se pretender que todos os utilizadores tenham a mesma definição, configure as predefinições do cliente. Caso contrário, configure definições do cliente personalizadas para coleções específicas.|Para obter mais informações sobre definições de cliente, consulte [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para obter mais informações sobre como configurar estas definições de cliente, consulte **passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software**.|  
|**Passo 5:** Certifique-se de que o catálogo de aplicações está operacional.|Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou a partir do Centro de Software.|Consulte **passo 5: Verifique se o catálogo de aplicações está operacional**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedimentos suplementares para instalar e configurar o Catálogo de Aplicações e o Centro de Software  
 Utilize as informações seguintes quando os passos da tabela anterior exigirem procedimentos adicionais.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações  
 Estes procedimentos configuram as funções do sistema de sites do Catálogo de Aplicações. Escolha um dos dois procedimentos seguintes, dependendo se irá instalar um servidor de sistema de sites novo ou utilizar um servidor de sistema de sites existente:  

> [!NOTE]  
>  Não é possível instalar o Catálogo de Aplicações num site secundário ou num site de administração central.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Novo servidor do sistema de sites  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.  

3.  No **home page** separador o **criar** grupo, escolha **criar servidor do sistema de sites**.  

4.  No **geral** página, especifique as definições gerais para o sistema de sites e, em seguida, escolha **seguinte**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente para utilizar o catálogo de aplicações através da internet, especifique internet totalmente qualificado (FQDN) do nome de domínio.  

5.  No **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web site do catálogo de aplicações** da lista de funções disponíveis e, em seguida, escolha **seguinte**.  

6.  Conclua os restantes passos.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Servidor do sistema de sites existente  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor a utilizar para o catálogo de aplicações.  

3.  No **home page** separador o **servidor** grupo, escolha **adicionar funções do sistema de sites**.  

4.  No **geral** página, especifique as definições gerais para o sistema de sites e, em seguida, escolha **seguinte**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente para utilizar o catálogo de aplicações através da internet, especifique internet totalmente qualificado (FQDN) do nome de domínio.  

5.  No **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web site do catálogo de aplicações** da lista de funções disponíveis e, em seguida, escolha **seguinte**.  

6.  Conclua os restantes passos.  

7. Verifique a instalação destas funções do sistema de sites utilizando as mensagens de estado e revendo os ficheiros de registo:  

    Mensagens de estado: Utilize os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, ID de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que o Gestor de componentes do Site instalou com êxito o ponto de Web site do catálogo de aplicações.  

    Ficheiros de registo: Procurar **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Para obter mais informações, procure o **awebsvcMSI.log** e **portlwebMSI.log** ficheiros de registo.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software  
 Este procedimento configura as predefinições de cliente para o catálogo de aplicações e o Centro de Software que se aplicam a todos os dispositivos na hierarquia. Se pretender que estas definições se apliquem apenas a alguns dispositivos, pode criar uma definição de cliente personalizada e implementá-la para uma coleção que tenha os dispositivos com as definições específicas. Para obter mais informações sobre como criar uma definição de dispositivo personalizada, consulte o [como criar e implementar definições personalizadas do cliente](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) secção [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  Reveja e configure as definições relacionadas com as notificações do utilizador, o Catálogo de Aplicações e o Centro de Software. Por exemplo:  

    1.  Grupo**Agente do Computador** :  

        -   **Ponto de Web site do catálogo de aplicações de predefinido**.  

        -   **Adicionar Web site predefinido do catálogo de aplicações à zona de sites fidedignos do Internet Explorer**.  

        -   **Nome da organização apresentada no Centro de Software**.  

            > [!TIP]  
            >  Para especificar o nome da organização que é apresentado no catálogo de aplicações e configurar o tema do Web site, utilize o **personalização** separador nas propriedades do Web site de catálogo de aplicações.  

        -   **Utilizar o novo Centro de Software**. Definido como **Sim** se pretender utilizar o novo Centro de Software, que permite aos utilizadores procurar e instalar as aplicações disponíveis sem a necessidade de aceder ao catálogo de aplicações (o que necessita de um browser com capacidade para Silverlight web).  

        -   **Permissões de instalação**.  

        -   **Mostrar notificações para novas implementações**.  

    2.  Grupo**Gestão de Energia** :  

        -   **Permitir que os utilizadores excluam o seu dispositivo da gestão de energia**.  

    3.  Grupo**Ferramentas Remotas** :  

        -   **Os utilizadores podem alterar as definições de notificação ou da política no Centro de Software**.  

    4.  Grupo**Afinidade de Dispositivo e Utilizador** :  

        -   **Permitir que os utilizadores definir os seus dispositivos primários**.  

    > [!NOTE]  
    >  Para obter mais informações sobre as definições de cliente, veja [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Escolha **OK** para fechar o **predefinições de cliente** caixa de diálogo.  

Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [como gerir clientes](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Para personalizar a imagem corporativa do Centro de Software

Uma imagem corporativa personalizado para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresentará o nome da organização especificado no **agente do computador** definição de cliente **nome da organização** apresentada no Centro de Software. Para obter instruções, consulte [como configurar as definições de cliente](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de sites catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração para o ponto de Web site do catálogo de aplicações](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Se uma subscrição do Microsoft Intune estiver configurada e ligada ao Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

#### <a name="to-manually-set-software-center-branding"></a>Definir manualmente a imagem corporativa do Centro de Software
<!-- 1351224 -->
Com o lançamento 1710, pode manualmente adicionar enterprise elementos de imagem corporativa e especificar a visibilidade dos separadores no Centro de Software. Pode adicionar o seu nome de empresa específica do Centro de Software, definir um tema de cor de configuração de centro de Software, defina um logótipo de empresa e definir os separadores visíveis para os dispositivos cliente.

1. No **do Configuration Manager** consola, escolha **administração** > **as definições de cliente**. Clique na sua instância de definição de cliente pretendidos.
2. No **home page** separador o **propriedades** grupo, escolha **propriedades**.
3. No **predefinições** diálogo caixa, escolha **Centro de Software**.
4. Selecione **Sim** para **Selecione as novas definições para especificar as informações da empresa** para ativar as definições de personalização do Centro de Software.
5. Tipo sua **nome da empresa**.
6. Selecione o **cor esquema no Centro de Software**.
7. Clique em **procurar** para navegar para o logótipo no Centro de Software. O logótipo tem de ser um JPEG ou PNG de 400 x 100 pixéis com um tamanho máximo de 750 KB.
8. Selecione **Sim** para tornar os separadores visível no Centro de Software para dispositivos cliente. Pelo menos um separador tem de estar visível:

    -  Ativar o separador aplicações
    -  Ativar o separador de atualizações
    -  Ativar o separador de sistemas operativos
    -  Ativar o separador de estado da instalação
    -  Ativar o separador de conformidade do dispositivo
    -  Ativar o separador Opções

> [!IMPORTANT]  
>  Imagem corporativa do Centro de software está sincronizada com o serviço do Intune a cada 14 dias. Por conseguinte, poderá haver um atraso antes das alterações efetuadas no Intune são apresentadas no Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passo 5: Verifique se o catálogo de aplicações está operacional  
 Utilize os procedimentos seguintes para verificar se o Catálogo de Aplicações está operacional. Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou a partir do Centro de Software.  

> [!NOTE]  
>  O catálogo de aplicações requer o Microsoft Silverlight, o que é instalado automaticamente como um pré-requisito de cliente do Configuration Manager. Se utilizar o catálogo de aplicações diretamente a partir de um browser utilizando um computador que não tenham o cliente de Configuration Manager instalado, verifique primeiro se o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos em falta são uma das principais razões para o catálogo de aplicações funcionar incorretamente após a instalação. Confirme os pré-requisitos das funções do sistema de sites do Catálogo de Aplicações. Pode fazê-lo utilizando o [configurações suportadas](../../core/plan-design/configs/supported-configurations.md) artigo.  

> [!NOTE]  
>  Se tiver iniciado com uma conta de administrador de domínio, mensagens de notificação do cliente do Configuration Manager (por exemplo, mensagens que indica que está disponível novo software) não serão apresentadas.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Para utilizar o catálogo de aplicações diretamente a partir de um browser  

-   Num browser, introduza o endereço do Web site catálogo de aplicações e confirme que a página Web apresenta os três separadores: **Catálogo de aplicações**, **os meus pedidos de aplicação**, e **os meus dispositivos**.  

     Selecione e utilize o endereço adequado na lista seguinte para o catálogo de aplicações, onde &lt;servidor&gt; é o nome do computador, intranet FQDN ou o FQDN de internet:  

    -   Ligações de cliente HTTPS e predefinições definições de função do sistema de sites: **https://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Ligações de cliente HTTP e predefinições definições de função do sistema de sites: **http://&lt;servidor&gt;/CMApplicationCatalog**  

    -   HTTPS ligações de cliente e definições de função do sistema de site personalizado: **https://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

    -   Ligações de cliente HTTP e definições de função do sistema de site personalizado: **http://&lt;servidor&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Para utilizar o catálogo de aplicações a partir do Centro de Software (não é aplicável para a nova versão do Centro de Software)  

1.  Num computador cliente, escolha **iniciar** > **todos os programas** > **Microsoft System Center 2012** > **do Configuration Manager** > **Centro de Software**.  

2.  Se tiver configurado previamente um nome da organização para o Centro de Software como uma definição do cliente, certifique-se de que este é apresentado conforme especificado.  

3.  Escolha **localizar aplicações adicionais no catálogo de aplicações** e confirme que a página mostra os três separadores: **Catálogo de aplicações**, **os meus pedidos de aplicação**, e **os meus dispositivos**.  

> [!WARNING]  
>  Depois de instalar as funções de sistema de sites do catálogo de aplicações, conseguirá não ver de imediato o catálogo de aplicações quando escolhe o **localizar aplicações adicionais no catálogo de aplicações** ligação a partir do Centro de Software. O Catálogo de Aplicações fica disponível do Centro de Software quando o cliente transferir a respetiva política do cliente ou num período máximo de 25 horas após a instalação das funções do sistema de sites do Catálogo de Aplicações.  
