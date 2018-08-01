---
title: Planear e configurar a gestão de aplicações
titleSuffix: Configuration Manager
description: Implementar e configurar as dependências necessárias para implantar aplicativos no System Center Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 626fbb8d431857b1b672fffd9f3ba0df8b2a3da0
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385206"
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planear e configurar a gestão de aplicações no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para ajudar a implementar as dependências necessárias para implementar aplicações no System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|------------------|----------------------|  
|Serviços de informação Internet (IIS) é necessário nos servidores de sistema de sites que executam o ponto de sites do catálogo de aplicações, o ponto de serviço web do catálogo de aplicações, o ponto de gestão e o ponto de distribuição.|Para obter mais informações sobre este requisito, consulte [configurações suportadas](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivos móveis inscritos pelo Configuration Manager|Quando os aplicativos de código de início de sessão para implementá-las em dispositivos móveis, não utiliza um certificado que tenha sido criado com um modelo de versão 3 (**Windows Server 2008, Enterprise Edition**). Este modelo de certificado cria um certificado que é incompatível com aplicações do Configuration Manager para dispositivos móveis.<br /><br /> Se utilizar os serviços de certificados do Active Directory a aplicações de código de início de sessão para aplicações para dispositivos móveis, não utilize um modelo de certificado da versão 3.|  
|Os clientes devem ser configurados para auditar eventos de início de sessão, se pretender criar automaticamente afinidades de dispositivo do utilizador.|O cliente do Configuration Manager lê eventos de início de sessão do tipo **êxito** de registo de eventos de segurança do PC para determinar afinidades dispositivo / utilizador automáticas.  Estes eventos estão ativados pelas políticas de auditoria de duas seguintes:<br>**Auditar eventos de início de sessão de conta**<br>**Auditar eventos de início de sessão**<br>Para criar automaticamente relações entre utilizadores e dispositivos, certifique-se de que estas duas definições estão ativadas nos computadores cliente. Pode utilizar a Política de Grupo do Windows para configurar estas definições.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager   

|Dependência|Mais informações|  
|------------------|----------------------|  
|Ponto de gestão|Os clientes contactar um ponto de gestão para transferir a política de cliente, para localizar os conteúdos e para ligar ao catálogo de aplicações.<br /><br /> Se os clientes não é possível aceder um ponto de gestão, estes não podem utilizar o catálogo de aplicações.|  
|Ponto de distribuição|Antes da implementação das aplicações nos clientes, tem de ter pelo menos um ponto de distribuição na hierarquia. Por predefinição, durante uma instalação padrão, o servidor do site tem uma função de site do ponto de distribuição ativada. O número e a localização dos pontos de distribuição são variam de acordo com os requisitos específicos da sua empresa.<br /><br /> Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Definições do cliente|Muitas definições de cliente controlam a forma como as aplicações são instaladas no cliente e o utilizador a experiência do cliente. Estas definições do cliente incluem o seguinte:<br /><br /><ul><li>Agente do computador</li><li>Reinício do computador</li><li>Implementação de software</li><li>Afinidade dispositivo / utilizador</li></ul> Para obter mais informações sobre estas definições de cliente, consulte [sobre as definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para obter mais informações sobre como configurar as definições de cliente, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).|  
|Contas de utilizador detetadas para catálogo de aplicações |Primeiro tem do Configuration Manager detetar contas de utilizador antes dos utilizadores podem ver e pedir aplicações a partir do catálogo de aplicações. Para obter mais informações, consulte [executar a deteção](/sccm/core/servers/deploy/configure/run-discovery).|  
|Cliente de App-V 4.6 SP1 ou posterior para executar aplicações virtuais|Para criar aplicações virtuais no Configuration Manager, computadores cliente têm de ter o App-V 4.6 SP1 ou o cliente mais recente instalado.<br /><br /> Tem também de atualizar o cliente de App-V com a correção descrita no [Knowledge Base artigo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) antes de poder implementar aplicações virtuais.|  
|Ponto de serviço Web do Catálogo de Aplicações|O ponto de serviço Web do Catálogo de Aplicações é uma função do sistema de sites que fornece informações sobre software disponível na Biblioteca de Software para o Web site do Catálogo de Aplicações.<br /><br /> Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software e o catálogo de aplicações (apenas para PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto de site do Catálogo de Aplicações|O ponto do Web site do Catálogo de Aplicações é uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível.<br /><br /> Para obter mais informações sobre como configurar esta função de sistema de sites, consulte [configurar o Centro de Software e o catálogo de aplicações (apenas para PCs Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) neste artigo.|  
|Ponto do Reporting Services|Para utilizar os relatórios no Configuration Manager para gestão de aplicações, tem primeiro de instalar e configurar um ponto do reporting services.<br /><br /> Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gestão de aplicações|Tem de ter as seguintes permissões de segurança para gestão de aplicações:<br /><br /> O **autor da aplicação** função de segurança inclui as permissões listadas anteriormente que são necessárias para criar, alterar e extinguir aplicações no Configuration Manager.<br /><br /> **Para implementar aplicações:**<br /><br /> O **Gestor de implementação de aplicação** função de segurança inclui as permissões listadas anteriormente que são necessários para implementar aplicações no Configuration Manager.<br /><br /> O **administrador da aplicação** função de segurança tem todas as permissões de ambas as **autor da aplicação** e o **Gestor de implementação de aplicação** funções de segurança.<br /><br /> Para obter mais informações, consulte [configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurar o Centro de Software e o Catálogo de Aplicações (apenas PCs Windows)  

 No System Center Configuration Manager, tem agora duas opções para os utilizadores alterar as definições, procurar as aplicações e instalar aplicações:  

-   **O novo Centro de Software**: O novo Centro de Software tem uma aparência moderna. Aplicações que eram apresentadas apenas no catálogo de aplicações dependente do Silverlight (aplicações disponíveis ao utilizador) agora aparecer no Centro de Software no **aplicativos** separador. O catálogo de aplicações ainda podem ser acedido através da ligação no **estado de instalação** separador do Centro de Software.  

     Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**.  

    > [!IMPORTANT]  
    >  Apesar de já não precisar de ligar ao catálogo de aplicações, tem ainda de configurar o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações conforme detalhado na secção seguinte.  

-   **O Centro de Software anterior e o catálogo de aplicações**: Por predefinição, os utilizadores continuam a ligar-se para a versão anterior do Centro de Software e ligue-se ao catálogo de aplicações (com capacidade para Silverlight necessário um browser) para procurar as aplicações disponíveis.  

 Qualquer versão que opte por utilizar, o Centro de Software é instalado automaticamente quando instala o cliente do Configuration Manager em Windows PCs.  

    > [!TIP]  
    >  A versão do Centro de Software que os utilizadores visualizam baseia-se nas definições de cliente do Configuration Manager. Isso lhe dá a flexibilidade para controlar a versão que está a ser utilizada com base nas definições de cliente personalizadas que implementa para uma coleção. 

    > [!IMPORTANT]
    > Nos próximos meses, removeremos a versão anterior do Centro de Software e já não estará disponível.
    > Para configurar clientes para que utilizem o novo Centro de Software, ative a definição de cliente **Agente do Computador** > **Utilizar o novo Centro de Software**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Passos para instalar e configurar o Catálogo de Aplicações e o Centro de Software  

> [!IMPORTANT]  
>  Antes de efetuar estes passos, certifique-se de que cumpriu todos os pré-requisitos listados anteriormente.  

|Passos|Detalhes|Mais informações|  
|-----------|-------------|----------------------|  
|**Passo 1:** Se utilizar ligações HTTPS, certifique-se de que implementou um certificado de servidor web nos servidores do sistema de sites.|Implemente um certificado do servidor Web nos servidores do sistema de sites que executarão o ponto do Web site do Catálogo de Aplicações e o ponto de serviço Web do Catálogo de Aplicações.<br /><br /> Além disso, se pretender que os clientes para utilizarem o catálogo de aplicações a partir da internet, implemente um certificado de servidor de web para o servidor do sistema de sites de ponto de gestão, pelo menos, um e configurá-la para ligações de cliente a partir da internet.|Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 2:** Se utilizar um certificado PKI de cliente para ligações a pontos de gestão, implemente um certificado de autenticação de cliente para computadores cliente.|Embora os clientes não utilizam um certificado PKI de cliente para ligar ao catálogo de aplicações, deve ligar um ponto de gestão antes de poderem utilizar o catálogo de aplicações. Tem de implementar um certificado de autenticação de cliente nos computadores cliente nos seguintes cenários:<br /><br /><ul><li>Todos os pontos de gestão na intranet aceitam apenas ligações de cliente HTTPS.</li><li>Os clientes ligam ao catálogo de aplicações a partir da internet.</li></ul>|Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passo 3:** Instalar e configurar o ponto de serviço web do catálogo de aplicações e o site do catálogo de aplicações.|Tem de instalar ambas as funções de sistema de sites no mesmo site. Não tem de instalá-los no mesmo servidor de sistema do site ou na mesma floresta do Active Directory. No entanto, o ponto de serviço web do catálogo de aplicações tem de ser na mesma floresta que o banco de dados do site.|Para obter mais informações sobre o posicionamento de funções de sistema de sites, consulte [planear servidores de sistema de sites e funções de sistema de sites](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Para configurar o ponto de serviço web do catálogo de aplicações e o ponto de Web site do catálogo de aplicações, consulte **passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações**.|  
|**Passo 4:** Configure definições de cliente para o catálogo de aplicações e o Centro de Software.|Se pretender que todos os utilizadores tenham a mesma definição, configure as predefinições do cliente. Caso contrário, configure definições do cliente personalizadas para coleções específicas.|Para obter mais informações sobre definições de cliente, consulte [sobre as definições de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para obter mais informações sobre como configurar estas definições de cliente, consulte **passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software**.|  
|**Passo 5:** Certifique-se de que o catálogo de aplicações está operacional.|Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou do Centro de Software.|Consulte **passo 5: Certifique-se de que o catálogo de aplicações está operacional**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedimentos suplementares para instalar e configurar o Catálogo de Aplicações e o Centro de Software  
 Utilize as informações seguintes quando os passos da tabela anterior exigirem procedimentos adicionais.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Passo 3: Instalar e configurar as funções de sistema de sites do catálogo de aplicações  
 Estes procedimentos configuram as funções do sistema de sites do Catálogo de Aplicações. Escolha um dos dois procedimentos seguintes consoante pretenda instalar um servidor de sistema de sites novo ou utilizar um servidor de sistema de sites existente:  

> [!NOTE]  
>  Não é possível instalar o Catálogo de Aplicações num site secundário ou num site de administração central.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Novo servidor de sistema de sites  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração do Site** > **servidores e funções de sistema de sites**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar servidor do sistema de sites**.  

4.  Sobre o **gerais** página, especifique as definições gerais do sistema de sites e, em seguida, escolha **próxima**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente utilizarem o catálogo de aplicações através da internet, especifique a internet (FQDN) de nome de domínio completamente qualificado.  

5.  Sobre o **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web sites do catálogo de aplicações** na lista de funções disponíveis e, em seguida, escolher **seguinte**.  

6.  Conclua os passos restantes.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Para instalar e configurar os sistemas de sites do catálogo de aplicações: Servidor de sistema de sites existente  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, Selecione o servidor a utilizar para o catálogo de aplicações.  

3.  Sobre o **home page** separador o **servidor** de grupo, selecione **adicionar funções de sistema de sites**.  

4.  Sobre o **gerais** página, especifique as definições gerais do sistema de sites e, em seguida, escolha **próxima**.  

    > [!TIP]  
    >  Se pretender que os computadores cliente utilizarem o catálogo de aplicações através da internet, especifique a internet (FQDN) de nome de domínio completamente qualificado.  

5.  Sobre o **seleção da função do sistema** página, selecione **ponto de serviço web do catálogo de aplicações** e **ponto de Web sites do catálogo de aplicações** na lista de funções disponíveis e, em seguida, escolher **seguinte**.  

6.  Conclua os passos restantes.  

7. Verifique a instalação destas funções do sistema de sites utilizando as mensagens de estado e revendo os ficheiros de registo:  

    Mensagens de estado: Utilize os componentes **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por exemplo, o ID de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que o Gestor de componentes do Site instalou com êxito o ponto de sites do catálogo de aplicações.  

    Ficheiros de registo: Procure **smsawebsvcsetup. log** e **Smsportalwebsetup**.  

    Para obter mais informações, procure o **awebsvcmsi. log** e **Portlwebmsi** ficheiros de registo.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Passo 4: Configurar as definições de cliente para o catálogo de aplicações e o Centro de Software  
 Este procedimento configura as predefinições de cliente para o catálogo de aplicações e o Centro de Software que se aplicam a todos os dispositivos na hierarquia. Se pretender que estas definições se apliquem apenas a alguns dispositivos, pode criar uma definição de cliente personalizada e implementá-la para uma coleção que tenha os dispositivos com as definições específicas. Para obter mais informações sobre como criar uma definição de dispositivo personalizado, consulte a [como criar e implementar definições personalizadas do cliente](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) secção [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

3.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

4.  Reveja e configure as definições relacionadas com as notificações do utilizador, o Catálogo de Aplicações e o Centro de Software. Por exemplo:  

    1.  Grupo**Agente do Computador** :  

        -   **Padrão de ponto de Web sites do catálogo de aplicações**.  

        -   **Adicionar Web site predefinido do catálogo de aplicações à zona de sites fidedignos do Internet Explorer**.  

        -   **Nome da organização apresentada no Centro de Software**.  

            > [!TIP]  
            >  Para especificar o nome da organização que é apresentado no catálogo de aplicações e configurar o tema do Web site, utilize o **personalização** separador nas propriedades do Web site do catálogo de aplicações.  

        -   **Utilizar o novo Centro de Software**. Defina como **Sim** se pretender utilizar o novo Centro de Software, que permite aos utilizadores procurar e instalar as aplicações disponíveis sem a necessidade de acessar o catálogo de aplicações (que necessita de um navegador da web habilitado para Silverlight).  

        -   **Permissões de instalação**.  

        -   **Mostrar notificações para novas implementações**.  

    2.  Grupo**Gestão de Energia** :  

        -   **Permitir que os utilizadores excluam o seu dispositivo da gestão de energia**.  

    3.  Grupo**Ferramentas Remotas** :  

        -   **Os utilizadores podem alterar as definições de notificação ou da política no Centro de Software**.  

    4.  Grupo**Afinidade de Dispositivo e Utilizador** :  

        -   **Permitir que os usuários definam seus dispositivos primários**.  

    > [!NOTE]  
    >  Para obter mais informações sobre as definições de cliente, veja [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Escolher **OK** para fechar a **predefinições de cliente** caixa de diálogo.  

Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [como gerir clientes](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Para personalizar a imagem corporativa do Centro de Software

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, o Centro de Software apresentará o nome da organização especificado na **agente do computador** definição do cliente **nome da organização** apresentada no Centro de Software. Para obter instruções, consulte [como configurar as definições de cliente](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de site catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração do ponto de Web sites do catálogo de aplicações](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Se uma subscrição do Microsoft Intune é configurada e ligada para o Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

#### <a name="to-manually-set-software-center-branding"></a>Para definir manualmente a imagem corporativa do Centro de Software
<!-- 1351224 --> Com a versão 1710, pode adicionar elementos de marca corporativa e especificar a visibilidade dos separadores no Centro de Software manualmente. Pode adicionar o seu nome de empresa específico do Centro de Software, defina um tema de cores de configuração do Centro de Software, defina um logótipo de empresa e definir as guias visíveis para os dispositivos de cliente.

1. Na **Configuration Manager** da consola, escolha **administração** > **definições de cliente**. Clique na sua instância de definição de cliente pretendido.
2. Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.
3. Na **predefinições** caixa de diálogo caixa, escolha **Centro de Software**.
4. Selecione **Sim** ao **selecione definições para especificar as informações da empresa** para ativar as definições de personalização do Centro de Software.
5. Tipo de sua **nome da empresa**.
6. Selecione seu **esquema para o Centro de Software de cor**.
7. Clique em **procurar** para navegar para o seu logótipo para o Centro de Software. O logótipo tem de ser um JPEG ou PNG de 400 x 100 pixéis com um tamanho máximo de 750 KB.
8. Selecione **Sim** para tornar os guias visíveis no Centro de Software para dispositivos cliente. Pelo menos um separador tem de estar visível:

    -  Ativar separador aplicações
    -  Ativar separador atualizações
    -  Ativar separador Sistemos operativos
    -  Ativar separador de estado da instalação
    -  Ativar separador conformidade de dispositivo
    -  Ativar separador Opções
    -  Especifique um separador personalizado para o Centro de Software (a partir da versão 1806) <!--1358132 -->
        - Nome do separador
        - URL de conteúdo

> [!IMPORTANT]  
> - Algumas funcionalidades do Web site poderão não funcionar quando utilizá-lo como uma guia personalizada no Centro de Software. Lembre-se de que os resultados de teste antes de implementar isso para os clientes. <!--519659--> 
> - Imagem corporativa do Centro de software está sincronizada com o serviço do Intune a cada 14 dias. Por conseguinte, pode haver um atraso antes das alterações que fizer no Intune são apresentadas no Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passo 5: Certifique-se de que o catálogo de aplicações está operacional  
 Utilize os procedimentos seguintes para verificar se o Catálogo de Aplicações está operacional. Pode utilizar o catálogo de aplicações diretamente a partir de um browser ou do Centro de Software.  

> [!NOTE]  
>  O catálogo de aplicações requer o Microsoft Silverlight, o que é instalado automaticamente como um pré-requisito de cliente do Configuration Manager. Se utilizar o catálogo de aplicações diretamente a partir de um browser utilizando um computador que não tenha o cliente do Configuration Manager instalado, primeiro certifique-se de que o Microsoft Silverlight está instalado no computador.  

> [!TIP]  
>  Os pré-requisitos em falta estão entre as razões mais habituais para o catálogo de aplicações a funcionar incorretamente após a instalação. Confirme os pré-requisitos das funções do sistema de sites do Catálogo de Aplicações. Pode fazê-lo utilizando o [configurações suportadas](../../core/plan-design/configs/supported-configurations.md) artigo.  

> [!NOTE]  
>  Se tiver iniciado sessão com uma conta de administrador de domínio, mensagens de notificação do cliente do Configuration Manager (por exemplo, mensagens a indicar que está disponível novo software) não serão apresentadas.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Para utilizar o catálogo de aplicações diretamente a partir de um browser  

-   Num browser, introduza o endereço do site do catálogo de aplicações e confirme que a página Web mostra os três separadores: **Catálogo de aplicações**, **os meus pedidos de aplicação**, e **os meus dispositivos**.  

     Selecione e utilize o endereço apropriado na lista seguinte para o catálogo de aplicações, onde &lt;servidor&gt; é o nome do computador, intranet, FQDN ou o FQDN de internet:  

    -   Definições de função do sistema de sites de ligações de cliente HTTPS e predefinições: **https://&lt;server&gt;/CMApplicationCatalog**  

    -   Ligações de cliente HTTP e predefinições de definições de função do sistema de sites: **http://&lt;server&gt;/CMApplicationCatalog**  

    -   HTTPS ligações de cliente e definições de função do sistema de site personalizada: **https://&lt;server&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

    -   Ligações de cliente HTTP e definições de função do sistema de site personalizada: **http://&lt;server&gt;:&lt;porta&gt;/&lt;nome da aplicação web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Para utilizar o catálogo de aplicações a partir do Centro de Software (não é aplicável para a nova versão do Centro de Software)  

1.  Num computador cliente, escolha **começar** > **todos os programas** > **Microsoft System Center 2012**  >   **O Configuration Manager** > **Centro de Software**.  

2.  Se tiver configurado previamente um nome da organização para o Centro de Software como uma definição do cliente, certifique-se de que este é apresentado conforme especificado.  

3.  Escolher **localizar aplicações adicionais no catálogo de aplicações** e confirme que a página mostra os três separadores: **Catálogo de aplicações**, **os meus pedidos de aplicação**, e **os meus dispositivos**.  

> [!WARNING]  
>  Depois de instalar as funções de sistema de sites do catálogo de aplicações, conseguirá não ver de imediato o catálogo de aplicações ao escolher o **localizar aplicações adicionais no catálogo de aplicações** ligação a partir do Centro de Software. O Catálogo de Aplicações fica disponível do Centro de Software quando o cliente transferir a respetiva política do cliente ou num período máximo de 25 horas após a instalação das funções do sistema de sites do Catálogo de Aplicações.  
