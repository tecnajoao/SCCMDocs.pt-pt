---
title: "Capacidades na pré-visualização técnica 1605 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1605."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 8b3d472c586e704ee48e9825138c72f655d89492
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1605 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1605. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 **Problemas conhecidos neste pré-visualização técnica:**  

-   Com 1605 pré-visualização técnica, se atualizar as propriedades de um ponto de gestão após a respetiva instalação, poderá ver um erro de consola que obriga a consola para a fechar.  Se isto acontecer, pode desinstalar o ponto de gestão e, em seguida, reinstalar o ponto de gestão utilizando as definições pretendidas. Em alternativa, pode modificar o ponto de gestão antes de instalar 1605 de pré-visualização técnica.  

-   Quando utilizar a loja Windows para a funcionalidade de negócio com o 1604 de pré-visualização técnica e, em seguida, atualizar para 1605 de pré-visualização técnica, já não pode ver os dados de integração. Todos os outros funcionalmente continua a funcionar. Se onboarded com o 1604 de pré-visualização técnica, permanecerá onboarded depois de instalar 1605 de pré-visualização técnica e não precisa de tomar nenhuma ação adicional.  

 **Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="BKMK_PerAppVPN"></a>Dispositivos de VPN para o Windows 10 por aplicação  
 Para dispositivos Windows 10 geridos através do Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola do administrador do Configuration Manager. Tem a opção de restringir o tráfego VPN a essas aplicações ou, pode continuar a permitir que todo o tráfego através da ligação VPN.  

 **Requisitos de**:  

-   Configuration Manager com o Intune  

-   Um perfil VPN do Windows 10 que tenha sido implementado pelo menos um dispositivo  

##  <a name="BKMK_InstallSU"></a>Melhoramentos à sequência de tarefas de atualizações de software de instalação  
 Foram efetuadas as seguintes melhorias à sequência de tarefas instalar atualizações de Software:  

-   Uma variável de sequência de tarefas novas, SMSTSSoftwareUpdateScanTimeout, está disponível para dar-lhe a capacidade de controlar o tempo limite na análise de atualizações de software durante o passo de sequência de tarefas de atualizações de software de instalação. O valor predefinido é 30 minutos.  

-   Foram melhorias efetuadas ao registo. O ficheiro de registo smsts irá conter novas entradas de registo que fazem referência a outros ficheiros de registo que irão ajudá-lo a resolver problemas durante o processo de instalação de atualizações de software.  

##  <a name="BKMK_PrepareConfigMgrClient"></a>Melhoramentos para preparar ConfigMgr Client para captura passo de sequência de tarefas  
 O passo de preparar ConfigMgr Client agora irá remover completamente o cliente do Configuration Manager, em vez de apenas remoção de informações da chave. Quando a sequência de tarefas, implementa a imagem de sistema operativo capturada irá instalar um novo cliente de Configuration Manager cada vez.  

##  <a name="BKMK_Grace"></a>Período de tolerância para implementações de aplicações necessárias  
 Em alguns casos, poderá conceder aos utilizadores mais tempo a instalar implementações de aplicações necessárias, para além de qualquer prazos que configurou. Por exemplo, se um utilizador final apenas tiver devolvido de férias, poderá ter de aguardar por uma longa enquanto como uma aplicação em atraso implementações estão instaladas. No entanto, pode ainda imediatamente instalarem a aplicação em qualquer altura que queiram.  

 Para ajudar a resolver este problema, agora pode definir um **período de tolerância** implementando definições de cliente do Configuration Manager a uma coleção.  

 Para configurar o período de tolerância, execute as ações seguintes:  

1.  No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.  

2.  Uma nova implementação de aplicação ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar a imposição desta implementação, de acordo com as preferências do utilizador**, até o período de tolerância definido nas definições de cliente.  

     Todas as implementações que tenham esta caixa de verificação selecionada e são direcionadas para dispositivos em que também implementada a definição de cliente irão utilizar o período de tolerância.  

 Nesta versão, o período de tolerância que configurar não é utilizado por dispositivos cliente. Se configurar um período de tolerância e selecione a caixa de verificação, a aplicação será instalada na primeira janela de negócio não que o utilizador configurado após o prazo.  

 Foram adicionadas opções semelhantes ao Assistente de regras de implementação automática, o Assistente de implementação de atualizações de software e páginas de propriedades. No entanto, estes não foram atualmente implementadas neste technical preview.  

##  <a name="BKMK_Remote"></a>Nova experiência de ações de remota do dispositivo  
 A experiência para realizar ações de remota do dispositivo a partir da consola do Configuration Manager foi melhorada.  
Ações comuns, tais como **extinguir/apagar**, **repor o código de acesso**, **bloqueio remoto**, e **omissão de bloqueio de ativação** agora pode ser encontrado no **ações de dispositivo remotas** acedido a partir do menu a **ativos e compatibilidade** área de trabalho.  

 ![Captura de ecrã de ações de dispositivo remotas novo](media/New-Remote-Device-Actions.png)  

 Pode encontrar o estado para cada uma destas operações nas seguintes locais:  

-   No painel de detalhes ao selecionar um dispositivo a partir de **dispositivos** nó.  

-   No **propriedades** página para um dispositivo.  

-   Na página principal do **dispositivos** nó (nem todas as colunas podem estar visíveis por predefinição).  

 Para mais informações sobre iOS omissão de bloqueio de ativação, consulte o artigo [ajudar a proteger os dispositivos com o bloqueio de ativação ignorar para o Configuration Manager de iOS](/sccm/mdm/deploy-use/manage-ios-activation-lock), em particular, o **atuais problemas conhecidos com o bloqueio de ativação ignorar no Configuration Manager Technical Preview** secção.  

##  <a name="BKMK_WSFB"></a>Para aplicações de empresas da loja Windows  
 O [da loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar-se no arquivo do Configuration Manager, pode gerir as aplicações adquirido o volume a partir da consola do Configuration Manager, por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

-   As aplicações que são sincronizadas são apresentados na consola do Configuration Manager e é possível implementar estas como todas as outras aplicações  

-   A cada 24 horas, Configuration Manager transfere as informações de licenciamento de aplicação da loja e pode rever esta na consola do Configuration Manager  

 A versão de pré-visualização técnica 1604, pode sincronizar e ver as aplicações da loja Windows para empresas na consola do Configuration Manager. Nesta versão, adicionámos a possibilidade de criar e implementar aplicações do Configuration Manager a partir de aplicações da loja sincronizados.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a loja Windows para a sincronização de negócio  

1.  No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Web aplicação and/or Web API". Isto irá dar-lhe um ID de cliente que irá precisar mais tarde.  

    1.  No nó do Active Directory da [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique a **seguinte** seta.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser nada e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudominio > / sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registado.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Em **chaves**, selecione uma duração a partir da lista e clique em **guardar**. Esta ação cria uma nova chave de cliente. Não sai desta página até ter com êxito onboarded da loja Windows para empresas para o Configuration Manager.  

3.  Na loja Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de arquivo.  

    1.  Abrir [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) e início de sessão se lhe for solicitado.  

    2.  Aceite os termos de utilização se necessário.  

    3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.  

    4.  No **pesquisa para a ferramenta de por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.  

    5.  Clique em **ativar** junto da aplicação que acabou de importar.  

    6.  No **Show Offline-Licensed aplicações** assistente, clique em **Sim** se pretender permitir que as aplicações offline licenciado ser comprado.  

4.  Compre pelo menos uma aplicação da loja Windows para empresas.  

5.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **da loja Windows para empresas.**  

6.  No **base** separador o **criar** grupo, clique em **para conta de empresas da loja Windows adicionar**.  

7.  Adicionar o seu ID de inquilino, o id de cliente e a chave de cliente a partir do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta configurada no **da loja Windows para empresas** lista na consola do Configuration Manager.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a tarefa seguinte e, em seguida, gostou como trabalhou utilizando o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

 Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação licenciada offline de negócio.  

1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença de aplicações da loja**.  

2.  Escolha a aplicação que pretende implementar, em seguida, no **base** separador o **criar** grupo, clique em **Criar aplicação**.  

 Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Pode, em seguida, implementar e monitorizar esta aplicação, tal como faria com qualquer outra aplicação do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria uma aplicação do Configuration Manager com um tipo de implementação única a partir de uma aplicação licenciado offline, isto pode ser implementado em dispositivos que tenham MDM geridos e também são geridos com o cliente do Configuration Manager. Se tentar implementar uma aplicação com vários tipos de implementação, a instalação irá falhar.  
>   
>  Atualmente não é possível implementar aplicações licenciadas online com o Configuration Manager.  

##  <a name="BKMK_VPP2"></a>Melhoramentos gerais para aplicações adquirido de volume  

-   Nesta versão, adquirido volume aplicações da loja Windows para empresas e a aplicação iOS arquivo ter sido consolidados na mesma vista, **informações de licença para armazenar aplicações**.  

-   Comprou o volume para aplicações para iOS, no separador de programa de compra da Apple Volume tenha sido removido do **pacote de aplicações para o iOS Browser** caixa de diálogo no Assistente para criar aplicação. Para criar uma aplicação adquirido o volume para iOS, utilize estes passos:  

    1.  1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença de aplicações da loja**.  

    2.  2.  Escolha a aplicação que pretende implementar, em seguida, no **base** separador o **criar** grupo, clique em **Criar aplicação**.  

-   A localização que utiliza para obter e carregue um token de Apple VPP adquirido volume aplicações na consola do Configuration Manager foi alterada. Agora pode fazer isto no **Admin** área o **serviços em nuvem** > **Apple Volume compra programa Tokens** nó.  

##  <a name="BKMK_VPP"></a>Proteção de dados de empresa (por EDP)  
 Pode criar itens de configuração que permitem-lhe implementar as políticas de proteção (por EDP) de dados empresarial, incluindo permitindo que a escolher as suas aplicações protegidas, o nível de proteção por EDP e como localizar dados empresariais na rede. Para mais informações sobre por EDP, consulte os seguintes tópicos:  

-   [Proteger os dados de empresa através da proteção de dados de empresa (por EDP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [Criar e implementar uma política de proteção (por EDP) de dados de empresa com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a>Os utilizadores finais podem instalar aplicações a partir do Portal da empresa  
 No local MDM foi introduzida do System Center Configuration Manager versão 1511. Em versões anteriores, pode implementar aplicações em dispositivos Windows 10 geridos por MDM com um objetivo de implementação de **necessário** instalar no local dispositivos geridos pela MDM.  

 Nesta versão, pode agora implementar aplicações com um objetivo de implementação de **disponível** aos utilizadores no local MDM computadores geridos pelo Windows 10, e os utilizadores agora podem instalar estas aplicações próprios no Portal da empresa.
Nesta pré-visualização técnica, se o Portal da empresa está aberto por mais de 15 minutos, o utilizador final verá uma mensagem de erro. Para contornar este problema, reinicie o Portal da empresa.  

### <a name="before-you-start"></a>Antes de começar  

#### <a name="server-prerequisites"></a>Pré-requisitos do  

-   .NET 4.5 ou superior (necessita de reinicialização)  

-   O PowerShell 3.0 para o script de configuração (necessita de reinicialização)  

#### <a name="client-prerequisites"></a>Pré-requisitos de cliente  

-   1511 de ambiente de trabalho do Windows 10 (SO compilação 10586.218) ou posterior  

#### <a name="general-prerequisites"></a>Pré-requisitos gerais  

-   Certifique-se de que concluiu a [passos de preparação para gestão de dispositivos móveis no local](https://technet.microsoft.com/library/mt613153.aspx) e [os seus dispositivos inscritos](https://technet.microsoft.com/library/mt627870.aspx).  

-   Para a aplicação melhor instalar experiência ao utilizar o Portal da empresa, certifique-se do Configuration Manager tem uma ligação ativa para o Microsoft Intune.  

-   Se escolher a opção de inscrição em massa, configure a afinidade de dispositivo / utilizador para o dispositivo inscrito antes de tentar este cenário.  

### <a name="configuration-steps"></a>Passos de configuração  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instale as funções de catálogo de aplicações e ativar o suporte de gestão de dispositivos móveis  

1.  Adicionar as funções de serviço de Web do catálogo de aplicações e Web Site  

    1.  Selecione **modo HTTPS** e **permitir que os dispositivos móveis utilizem este ponto de serviço de Web do catálogo de aplicações** opção.  

    2.  Limitações este pré-visualização técnica:  

        -   Tem de desinstalar quaisquer funções de catálogo de aplicações existentes antes de selecionar a opção para permitir que os dispositivos móveis estabelecer a ligação.  

        -   Certificar-se de que existe apenas um conjunto de funções de catálogo de aplicações e as funções são localizadas conjuntamente no mesmo sistema de sites com as funções de ponto de Proxy de inscrição e o ponto de inscrição.  

2.  Certifique-se de que os seguintes componentes estão operacionais a partir do nó Estado do componente na consola do Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar limites  
 Configure limites necessários para pontos de distribuição apenas de intranet.  

> [!NOTE]  
>  Limites de intervalo IPv4 apenas são suportadas neste momento para gestão de dispositivos móveis.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implementar a aplicação de Portal da empresa e a configuração  

1.  Utilize o script de configuração incluído com a pré-visualização técnica para preparar a implementação do Portal da empresa e a configuração:  

    1.  Abra uma janela de comandos elevada do PowerShell.  

    2.  Executar **set-executionPolicy RemoteSigned**  

    3.  A partir da pasta  **&lt;diretório de instalação do SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM** executar **.\ConfigurationScript.ps1**  

     O script de configuração faz o seguinte:  

    1.  Cria uma aplicação do Configuration Manager com um Windows app pacote implementação tipo utilizando **CompanyPortalOnPremisesMDM.appx** na mesma pasta.  

    2.  Cria um item de configuração e a linha de base de configuração que configura o Portal da empresa.  

    3.  Implemente a linha de base de configuração e a aplicação e adiciona a aplicação para todos os pontos de distribuição.  

    > [!NOTE]  
    >  Se as funções de catálogo de aplicações não estão localizadas conjuntamente com o site primário, execute as ações seguintes:  
    >   
    >  -   No **ativos e compatibilidade** área de trabalho, localize o **CI de configuração do Portal OnPremMDM - servidor urls** item de configuração  
    > -   Alterar o **regras de compatibilidade** valor para o nome de domínio totalmente qualificado do sistema de sites onde se encontram as funções de catálogo de aplicações.  

2.  Depois da aplicação de Portal da empresa e a respetiva configuração são implementados, verifique se a linha de base de configuração e aplicações são compatíveis para o dispositivo especificado a utilizar **implementações** secção da consola do Configuration Manager. O Portal da empresa irá aparecer como **Portal da empresa (pré-visualização técnica)** no menu Iniciar no dispositivo.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as seguintes tarefas e, em seguida, gostou como trabalhou utilizando o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

1.  Implementar várias aplicações com tipos de implementação suportado para uma coleção de utilizadores com um objetivo de implementação de **disponível**. Para este pré-visualização técnica, as aplicações que exigem a aprovação do administrador não são suportadas e não serão apresentadas no Portal da empresa.  

2.  Os utilizadores podem, em seguida, procurar e instalar aplicações a partir do Portal da empresa.  

     Depois de abrir o Portal da empresa, verá uma caixa de diálogo de autenticação com o nome **System Center Configuration Manager** especificar as credenciais do utilizador do Active Directory (quer sob a forma de user@domain ou domínio \ utilizador) para iniciar sessão.  

##  <a name="BKMK_SW1"></a>Novos separadores para as atualizações e sistemas operativos no Centro de Software  
 Nesta versão, as seguintes alterações foram efetuadas para melhorar o esquema da aplicação Centro de Software:  

-   O **aplicações** separador foi dividido em três separadores individuais para **atualizações**, **sistemas operativos** (que foram ambas anteriormente encontradas no **filtros** lista), e **aplicações**.  

##  <a name="BKMK_ServerGroups"></a>Serviço de um grupo de servidores  
 Pré-visualização técnica do System Center Configuration Manager, versão 1511, incluídas a capacidade para criar uma coleção onde todos os dispositivos da coleção de constituem um grupo de servidores. Em seguida, pode configurar as definições de grupo do servidor para utilizar quando implementa atualizações de software para o grupo do servidor, o controlo a percentagem de computadores que são atualizadas em qualquer momento, e configurar implementação pré e pós-implementação de scripts do PowerShell para executar as ações personalizadas.  

 Pré-visualização técnica do System Center Configuration Manager, versão 1605, adiciona a capacidade de atualizar os computadores no grupo de servidor numa ordem especificada que definir, adiciona monitorização avançada para ver o estado para os computadores no grupo de servidor e fornece a capacidade para limpar os bloqueios de implementação que é útil quando os clientes falharam ao instalar as atualizações de software e estão a impedir a outros clientes de instalar as atualizações de software.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as seguintes tarefas e, em seguida, gostou como trabalhou utilizando o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Posso pode criar uma coleção que representa um grupo de servidores. Para este teste, pode configurar as regras de associação de recolher com 2 máquinas nesta coleção.   

-   Posso pode especificar que os computadores no grupo de servidores de instalar as atualizações de software por uma ordem específica, com base nas definições de grupo do servidor para a coleção. Utilize os scripts de exemplo no procedimento para especificar os scripts de pré-implementação e pós-implementação.  

-   Pode implementar uma atualização de software desta coleção. Consulte os ficheiros de start.txt e end.txt (criados a partir dos scripts de exemplo) em C:\temp e verifique se as horas de início e fim para a implementação nos computadores no grupo de servidor. Reveja o ficheiro de UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  

1.  [Criar uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contém os computadores no grupo de servidor.  

2.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, faça duplo clique na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  No **geral** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  No **definições de grupo do servidor** página, especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem das máquinas para sejam atualizadas ao mesmo tempo**: Especifica que são atualizados apenas numa determinada percentagem de clientes em qualquer momento. Se, por exemplo, a coleção tem 10 clientes e a coleção é configurada para atualização 30% do clientes ao mesmo tempo, em seguida, apenas 3 clientes irão instalar atualizações de software num determinado momento.  

    -   **Permitir que um número de máquinas para sejam atualizadas ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado ao mesmo tempo.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção serão atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar atualizações de software após o cliente que está adiantada-lo na lista terminar a atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem de nó) ou scripts pós-implementação (currículo de nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar testes de pré-implementação e scripts pós-implementação que escreverem a hora atual para um ficheiro de texto:  
    >   
    >  **Pré-implementação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implementar atualizações de software para o estado de grupo e o monitor de servidor  

1.  [Implementar atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) na coleção de grupo do servidor.  

2.  [Monitorizar a implementação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx). Para além das vistas de monitorização padrão para a implementação de atualizações de software, uma nova descrição de estado é apresentada quando um cliente está a aguardar o desativar instalar as atualizações de software. **Aguardar pelo bloqueio** é apresentada para este novo Estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para limpar os bloqueios de implementação para computadores de um grupo de servidores  

1.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  No **base** separador o **implementação** grupo, clique em **bloqueia de implementação de grupo de servidor limpar**. Quando os clientes falharam ao instalar as atualizações de software e estão a impedir a outros clientes de instalar as atualizações de software, os bloqueios de implementação podem ser desmarcados manualmente.  

##  <a name="BKMK_ATP"></a>Suporte para o serviço de proteção de ameaça avançada do Windows Defender  
 Windows Defender avançadas ameaça proteção (ATP) é um novo serviço que o irá ajudar empresas para detetar, analisar e responder a ataques avançadas nos redes deles. Saiba mais sobre [Windows Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Gestor de configuração pode ajudá-lo carregar e monitorizar dispositivos de cliente do Windows 10 aniversário Edition geridos.  

### <a name="try-it-now"></a>Experimente agora!  
 Tente concluir as seguintes tarefas e, em seguida, gostou como trabalhou utilizando o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Carregar dispositivos ao serviço online do Windows Defender avançadas ameaça proteção (ATP)  

-   Monitorizar a implementação do Windows Defender ATP para dispositivos geridos  

 **Pré-requisitos**  

-   Subscrição do serviço do Windows Defender avançadas ameaça proteção online  

-   Clientes a executar o Windows 10, edição de aniversário (compilação 14328 e maior)  

-   Criar um ficheiro de configuração de integração do cliente  

    ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um ficheiro de configuração de integração  

    1.  Início de sessão para o serviço do Windows Defender ATP online  

    2.  Clique no **no cliente típico** item de menu  

    3.  Selecione **System Center Configuration Manager** e clique em **transferir o pacote**.  

    4.  Transfira o ficheiro de arquivo comprimido (. zip) e extrair os conteúdos.  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP política**. O Assistente de política do Windows Defender ATP abre.  

2.  Tipo de **nome** e **Descrição** para a política do Windows Defender ATP e selecione **integração**. Clique em Seguinte.  

3.  **Procurar** ao ficheiro de configuração fornecido pelo inquilino do serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

4.  Especifique os exemplos de ficheiros que são recolhidos e partilhados a partir de dispositivos geridos para análise.  

    -   **Nenhum** – não existem ficheiros de exemplo são recolhidos para uma análise  

    -   **Ficheiros executáveis Portable** – ficheiros, tais como ficheiros (.exe), ficheiros de ligação dinâmica biblioteca (. dll), ficheiros de tipo de letra, de programas e ficheiros semelhantes que podem ser explorados no cyberattacks são recolhidos e partilhados para uma análise  

     Clique em **Seguinte**.  

5.  Reveja o resumo e conclua o assistente.  

6.  Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos clicando **implementar**.  

##### <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard de proteção de ameaça avançada do Windows Defender.  

    -   **Estado de implementação de agente do Windows Defender** – o número e a percentagem de computadores elegíveis cliente gerido com o Active Directory onboarded de política do Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – percentagem de clientes de computador a comunicar o estado para o agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativo** -não existem dados enviados ao serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente do Windows não está em execução  

        -   **Nenhum onboarded** - foi aplicada a política, mas o agente não comunicou carregar política  

##  <a name="BKMK_DHA"></a>Atestado de estado de funcionamento do dispositivo no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 agora pode ser configurado para comunicar utilizando a infraestrutura no local. Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local. Se estiver selecionada no local para fins de atestado de estado de funcionamento de relatórios, um URL pode ser especificado para o serviço. Isto permite que o cliente PCs sem acesso à internet ativar e gerir dispositivos através de atestado de estado de funcionamento.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar atestado de estado de funcionamento de dispositivos no local  
 No 1605, podemos ter corrigido alguns erros detetados no 1604 Technical Preview.  Para experimentá-lo, configure serviço de atestado de estado de funcionamento no local utilizando as definições de agente do cliente.  

1.  Na consola do Configuration Manager, navegue **administração** > **descrição geral** > **definições de cliente**e, em seguida, defina **utilização no local serviço de integridade de atestado** para **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

##  <a name="BKMK_RestartOptions"></a>Reiniciar novas opções para os clientes Windows 10 após a instalação de atualização de software  
 Quando uma atualização de software que requer um reinício é implementado utilizando o Configuration Manager e instalado num computador, um reinício pendente é agendado e é apresentada uma caixa de diálogo de reinício. Atualmente, para o Windows 8 e acima, se é encerrado ou reiniciar o computador utilizando as opções de energia do Windows (em vez da partir da caixa de diálogo de reinício), a permanece de caixa de diálogo de reinício após o computador seja reiniciado e o computador terá de reiniciar no prazo de configurado. Nesta pré-visualização técnica, a opção de **atualização e reinicie** e **atualização e encerramento** estará disponível em computadores Windows 10 nas opções do Windows Power sempre que existe um reinício pendente para uma atualização de software do Configuration Manager. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será apresentada depois do reinício do computador.  

##  <a name="BKMK_IMEI"></a>Pré-declarar os dispositivos da empresa com o número de série IMEI ou iOS  
 Agora pode identificar dispositivos pertencentes ao importar os seus números de identidade (IMEI) do estação internacional do equipamento móvel. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI do dispositivo ou pode introduzir manualmente as informações de dispositivo.  Também pode importar os números de série para dispositivos iOS.  Informação importada definirá a propriedade dos dispositivos inscritos como "Empresa".  Uma licença do Intune é ainda necessária para cada utilizador que aceda ao serviço.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as seguintes tarefas e, em seguida, gostou como trabalhou utilizando o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Importe um conjunto de números IMEI num ficheiro. csv. Cada linha pode conter o número IMEI seguido de um campo de detalhes.  

-   Importe manualmente os números IMEI a partir da consola do Configuration Manager.  

-   Importe um conjunto de números de série iOS num ficheiro. csv. Novamente, cada linha contém um número seguido de quaisquer detalhes para o dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS  

1.  Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **Pre-declared dispositivos**e, em seguida, clique em **criar dispositivos Pre-declared**. O Assistente de dispositivos de Pre-declared abre.  

2.  Especifique como pretende adicionar informações do dispositivo:  

    -   **Carregar um ficheiro. csv que contém números IMEI e os detalhes** - para carregar uma lista de números, consulte o passo 3.  

    -   **Adicionar manualmente IMEI números e os detalhes** - para introduzir manualmente as informações, escreva o número IMEI ou número de série iOS e detalhes para os dispositivos e, em seguida, prossiga para o passo #4.  

3.  Para ficheiros carregados, navegue até ao ficheiro. csv que contém informações para declarar previamente os dispositivos da empresa. O ficheiro tem de ter o seguinte formato, excluindo a linha de cima (fornecida para obter orientações sobre apenas):  

    |**IMEI #**|**iOS série**|**SO**|**Detalhes**|
    |---|---|---|---|
    |123456789012345||WINDOWS|Dispositivo de Windows pertencentes à empresa|
    |123456789012|A0BCD0EFGH0J|IOS|Dispositivos iOS pertencentes à empresa|
    |123456789012346||ANDROID|Dispositivo Android pertencentes à empresa|

     **Colunas:**  

    -   Coluna 1: O número IMEI – qualquer um de um IMEI número ou iOS número de série é obrigatório para cada linha  

    -   A coluna 2: número de série iOS – apenas os números de série iOS pode ser declarados previamente. Utilize o número IMEI para outras plataformas de dispositivo  

    -   Coluna 3: Sistema operativo do dispositivo (capitalização necessário):  

        -   IOS – todos os dispositivos iOS  

        -   WINDOWS – inclui o Windows Phone, janela 10 móveis e Windows PCs  

        -   ANDROID – todos os dispositivos Android  

    -   Coluna 4: Detalhes – informações de dispositivo adicionais que é apresentado na consola do Configuration Manager  

     Clique em **Seguinte**.  

4.  Reveja os resultados da importação de ficheiro. Anteriormente importados IMEI ou números de série terão os respetivos detalhes atualizados com detalhes de novo.  Clique em **seguinte** para continuar ou **novamente** manter atualizados detalhes e, em seguida, conclua o assistente.  

