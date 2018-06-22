---
title: Funcionalidades no Technical Preview 1605
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 05d87b253f2387dd8428f4b9fadea3fe5f3a48e8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342533"
---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1605 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1605. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.  

 **Problemas conhecidos neste Technical Preview:**  

-   Com o Technical Preview 1605, se atualizar as propriedades de um ponto de gestão depois de ser instalado, poderá ver um erro de consola que força a consola para fechar.  Se isto acontecer, pode desinstalar o ponto de gestão e, em seguida, reinstalar o ponto de gestão utilizando as definições pretendidas. Em alternativa, pode modificar o ponto de gestão antes de instalar 1605 de pré-visualização técnica.  

-   Quando utilizar a loja Windows para a funcionalidade de negócio com 1604 de pré-visualização técnica e, em seguida, atualizar para o Technical Preview 1605, já não pode ver os dados de integração. Todos os outros funcionalmente continua a trabalhar. Se integrado com o 1604 de pré-visualização técnica, permanecem integrado depois de instalar 1605 de pré-visualização técnica e não precisa de tomar nenhuma ação adicional.  

 **Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="BKMK_PerAppVPN"></a> Dispositivos de VPN para Windows 10 por aplicação  
 Para dispositivos do Windows 10 geridos com o Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola de administração do Configuration Manager. Tem a opção de restringir o tráfego VPN para essas aplicações, ou pode continuar a permitir todo o tráfego através da ligação VPN.  

 **Requisitos**:  

-   Configuration Manager com Intune  

-   Um perfil de VPN do Windows 10 que tenha sido implementado, pelo menos, um dispositivo  

##  <a name="BKMK_InstallSU"></a> Melhoramentos para a sequência de tarefas instalar atualizações de software  
 Foram efetuadas as seguintes melhorias à sequência de tarefas instalar atualizações de Software:  

-   Uma variável de sequência de tarefas novo, SMSTSSoftwareUpdateScanTimeout, está disponível para lhe fornecer a capacidade para controlar o tempo limite a análise de atualizações de software durante o passo de sequência de tarefas de atualizações de software de instalação. O valor predefinido é 30 minutos.  

-   Foram melhoramentos ao registo. O ficheiro de registo smsts.log irá conter novas entradas de registo referenciam outros ficheiros de registo que o irão ajudar a resolver problemas durante o processo de instalação de atualizações de software.  

##  <a name="BKMK_PrepareConfigMgrClient"></a> Melhoramentos ao preparar ConfigMgr Client para captura de passo de sequência de tarefas  
 O passo de preparar ConfigMgr Client agora removerá totalmente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas, implementa a imagem do sistema operativo capturada, instalará um novo cliente de Configuration Manager cada vez.  

##  <a name="BKMK_Grace"></a> Período de tolerância para implementações de aplicações necessárias  
 Em alguns casos, poderá conceder aos utilizadores mais tempo a instalar as implementações de aplicações necessárias, para além de qualquer prazos que configurou. Por exemplo, se um utilizador final tiver apenas devolvido de férias, poderá ter de aguardar algum enquanto como uma aplicação em atraso implementações estão instaladas. No entanto, ainda imediatamente podem instalar a aplicação em qualquer altura em que pretende.  

 Para ajudar a resolver este problema, agora pode definir um **período de tolerância** ao implementar as definições de cliente do Configuration Manager para uma coleção.  

 Para configurar o período de tolerância, efetuar as seguintes ações:  

1.  No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para a imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.  

2.  Numa nova implementação de aplicação ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador**, até ao período de tolerância definido nas definições do cliente.  

     Todas as implementações que tenham esta caixa de verificação selecionada e são os que são direcionadas para os dispositivos nos quais tiver implementado também a definição de cliente utilizará o período de tolerância.  

 Nesta versão, o período de tolerância que configurar não é utilizado pelos dispositivos cliente. Se configurar um período de tolerância e selecione a caixa de verificação, a aplicação será instalada na primeira janela de empresa-empresa que o utilizador configurado após o prazo.  

 Foram adicionadas opções semelhantes para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades. No entanto, estes não estão implementados nesta pré-visualização técnica.  

##  <a name="BKMK_Remote"></a> Nova experiência para as ações do dispositivo remoto  
 A experiência para efetuar ações do dispositivo remoto a partir da consola do Configuration Manager foi melhorada.  
Ações comuns, tais como **extinguir/limpar**, **repor código de acesso**, **bloqueio remoto**, e **ignorar bloqueio de ativação** agora podem ser encontrados no **ações do dispositivo remoto** acedido a partir do menu de **ativos e compatibilidade** área de trabalho.  

 ![Captura de ecrã de ações do dispositivo remoto novo](media/New-Remote-Device-Actions.png)  

 Pode encontrar o estado para cada uma destas operações nos seguintes locais:  

-   No painel de detalhes, quando seleciona um dispositivo a partir do **dispositivos** nós.  

-   No **propriedades** página para um dispositivo.  

-   Na página principal do **dispositivos** nó (nem todas as colunas poderão ser visíveis por predefinição).  

 Para obter mais informações sobre a desativação do bloqueio de ativação de iOS, consulte [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock), em particular, a **ignorar atuais problemas conhecidos com o bloqueio de ativação no Configuration Manager Technical Preview** secção.  

##  <a name="BKMK_WSFB"></a> Loja Windows para as aplicações da empresa  
 O [loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode gerir aplicações compradas em volume da consola do Configuration Manager, por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

-   As aplicações que são sincronizadas aparecem na consola do Configuration Manager e pode implementá-las como todas as outras aplicações  

-   A cada 24 horas, Configuration Manager transfere as informações de licenciamento de aplicações da loja e pode rever este na consola do Configuration Manager  

 Na versão 1604 technical preview, pode sincronizar e ver as aplicações da loja Windows para empresas na consola do Configuration Manager. Nesta versão, foi adicionado a capacidade de criar e implementar aplicações do Configuration Manager a partir de aplicações da loja sincronizados.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a loja Windows para a sincronização de negócio  

1.  No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web". Isto irá dar-lhe um ID de cliente que irá precisar mais tarde.  

    1.  No nó do Active Directory da [ https://manage.windowsazure.com ](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique o **seguinte** seta.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudomínio > / sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Em **chaves**, selecione uma duração da lista e clique em **guardar**. Isto irá criar uma nova chave de cliente. Não saia desta página até ter com êxito integrado da loja Windows para empresas para o Configuration Manager.  

3.  Na loja Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de armazenamento.  

    1.  Abra [ https://businessstore.microsoft.com/en-us/managementtools ](https://businessstore.microsoft.com/managementtools) e início de sessão se lhe for pedido.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.  

    4.  No **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.  

    5.  Clique em **ativar** junto da aplicação que acabou de importar.  

    6.  No **aplicações licenciadas offline** assistente, clique em **Sim** se pretender permitir que as aplicações licenciadas offline sejam compradas.  

4.  Compre pelo menos uma aplicação da loja Windows para empresas.  

5.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **loja Windows para empresas.**  

6.  No **home page** separador o **criar** , clique em **adicionar da loja Windows para empresas conta**.  

7.  Adicione o ID do inquilino, o id de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta configurada no **da loja Windows para empresas contas** lista na consola do Configuration Manager.  

### <a name="try-it-out"></a>Experimente!  
 Tentar concluir a seguinte tarefa e, em seguida, informe-nos como correu utilizando o nosso formulário de comentários no [programa de feedback do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

 Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para empresas as aplicações licenciadas offline.  

1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.  

2.  Escolha a aplicação que pretende implementar, em seguida, no **home page** separador o **criar** , clique em **Criar aplicação**.  

 Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria uma aplicação do Configuration Manager com um tipo de implementação única a partir de uma aplicação com licença offline, isto pode ser implementado em dispositivos que tenham MDM gerida e também são geridos com o cliente do Configuration Manager. Se tentar implementar uma aplicação com vários tipos de implementação, a instalação irá falhar.  
>   
>  Atualmente não é possível implementar as aplicações licenciadas online com o Configuration Manager.  

##  <a name="BKMK_VPP2"></a> Melhoramentos gerais para as aplicações compradas em volume  

-   Nesta versão, as aplicações compradas na loja Windows para empresas e a aplicação iOS arquivo ter sido consolidados na mesma vista, **informações de licença para armazenar aplicações**.  

-   Para aplicações compradas em volume do iOS, no separador de Apple Volume Purchase Program foi removido do **pacote de aplicação para o iOS Browser** caixa de diálogo no Assistente para criar aplicação. Para criar uma aplicação comprada em volume para iOS, utilize estes passos:  

    1.  1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.  

    2.  2.  Escolha a aplicação que pretende implementar, em seguida, no **home page** separador o **criar** , clique em **Criar aplicação**.  

-   A localização que utilizar para obter e carregar um token VPP da Apple para aplicações compradas em volume na consola do Configuration Manager foi alterada. Agora pode fazer isto no **Admin** área de trabalho no **serviços Cloud** > **Tokens do Apple Volume Purchase Program** nós.  

##  <a name="BKMK_VPP"></a> Proteção de dados empresariais (EDP)  
 Pode criar itens de configuração que permitem-lhe implementar as políticas de proteção (EDP) de dados empresariais, incluindo, permitindo-lhe escolher as aplicações protegidas, o nível de proteção de EDP e como dados empresariais são localizados na rede. Para obter mais informações sobre EDP, consulte os tópicos seguintes:  

-   [Proteger os dados de enterprise através de proteção de dados empresariais (EDP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [Criar e implementar uma política de proteção (EDP) de dados empresariais com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a> Os utilizadores finais podem instalar aplicações a partir do Portal da empresa  
 No local MDM foi introduzida do System Center Configuration Manager versão 1511. Em versões anteriores, pode implementar aplicações em dispositivos Windows 10 geridos por MDM com um objetivo de implementação **necessário** instalar para dispositivos de geridos por MDM no local.  

 Nesta versão, pode agora implementar aplicações com um objetivo de implementação **disponível** MDM utilizadores no local geridas computadores Windows 10 e os utilizadores podem agora instalar estas aplicações próprios no Portal da empresa.
Nesta pré-visualização técnica, se o Portal da empresa está aberto durante mais de 15 minutos, o utilizador final verá uma mensagem de erro. Para contornar este problema, reinicie o Portal da empresa.  

### <a name="before-you-start"></a>Antes de começar  

#### <a name="server-prerequisites"></a>Pré-requisitos do  

-   .NET 4.5 ou superior (necessita de reinicialização)  

-   PowerShell 3.0 para o script de configuração (necessita de reinicialização)  

#### <a name="client-prerequisites"></a>Pré-requisitos do cliente  

-   Windows 10 Desktop 1511 (compilação 10586.218 SO) ou posterior  

#### <a name="general-prerequisites"></a>Pré-requisitos gerais  

-   Certifique-se de que concluiu o [passos de preparação para gestão de dispositivos móveis no local](https://technet.microsoft.com/library/mt613153.aspx) e [inscrito os seus dispositivos](https://technet.microsoft.com/library/mt627870.aspx).  

-   Para a aplicação melhor instalar a experiência de utilização ao utilizar o Portal da empresa, certifique-se de que o Configuration Manager tem uma ligação ativa para o Microsoft Intune.  

-   Se escolher a opção de inscrição em massa, configure a afinidade de dispositivo / utilizador para o dispositivo inscrito antes de tentar este cenário.  

### <a name="configuration-steps"></a>Passos de configuração  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instalar as funções de catálogo de aplicações e ativar o suporte de gestão de dispositivos móveis  

1.  Adicione as funções do serviço de Web do catálogo de aplicações e Web Site  

    1.  Selecione **modo HTTPS** e **permitir que os dispositivos móveis utilizem este ponto de serviço de Web do catálogo de aplicações** opção.  

    2.  Limitações nesta pré-visualização técnica:  

        -   Tem de desinstalar quaisquer funções de catálogo de aplicações existentes antes de selecionar a opção para permitir que dispositivos móveis se liguem.  

        -   Certifique-se de que existe apenas um conjunto de funções de catálogo de aplicações e as funções estão colocalizadas no mesmo sistema de sites com o ponto de registo e as funções de ponto de Proxy de registo.  

2.  Certifique-se de que os seguintes componentes estão operacionais nó Estado do componente na consola do Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar limites  
 Configure limites necessários apenas de intranet para pontos de distribuição.  

> [!NOTE]  
>  Limites de intervalo IPv4 apenas são suportados neste momento para gestão de dispositivos móveis.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implementar a aplicação Portal da empresa e a configuração  

1.  Utilize o script de configuração incluído com o technical preview para preparar a implementação do Portal da empresa e a configuração:  

    1.  Abra uma janela de comandos elevada do PowerShell.  

    2.  Executar **set-executionPolicy RemoteSigned**  

    3.  Na pasta  **&lt;diretório de instalação do SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM** executar **.\ConfigurationScript.ps1**  

     O script de configuração faz o seguinte:  

    1.  Cria uma aplicação do Configuration Manager com um Windows aplicação pacote implementação tipo utilizando **CompanyPortalOnPremisesMDM.appx** na mesma pasta.  

    2.  Cria um item de configuração e a linha de base de configuração configura o Portal da empresa.  

    3.  Implementa a linha de base de configuração e a aplicação e adiciona a aplicação por todos os pontos de distribuição.  

    > [!NOTE]  
    >  Se as funções de catálogo de aplicações não estão colocalizadas com o site primário, execute as ações seguintes:  
    >   
    >  -   No **ativos e compatibilidade** área de trabalho, localize o **CI de configuração do Portal OnPremMDM - urls do servidor** item de configuração  
    > -   Alterar o **regras de compatibilidade** valor para o nome de domínio completamente qualificado do sistema de sites onde estão localizadas as funções de catálogo de aplicações.  

2.  Depois da aplicação Portal da empresa e a respetiva configuração são implementados, certifique-se a linha de base de configuração e aplicações são compatíveis para utilizar o dispositivo determinado **implementações** secção da consola do Configuration Manager. O Portal da empresa irá aparecer como **Portal da empresa (pré-visualização técnica)** no menu Iniciar no dispositivo.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, informe-nos como correu utilizando o nosso formulário de comentários no [programa de feedback do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

1.  Implementar várias aplicações com tipos de implementação suportado para uma coleção de utilizadores com um objetivo de implementação **disponível**. Para esta pré-visualização técnica, as aplicações que necessitem de aprovação do admin não são suportadas e não serão apresentadas no Portal da empresa.  

2.  Os utilizadores podem, em seguida, procurar e instalar aplicações a partir do Portal da empresa.  

     Depois de abrir o Portal da empresa, verá uma caixa de diálogo de autenticação com o nome **System Center Configuration Manager** especificar as credenciais do utilizador do Active Directory (no formato user@domain ou domínio \ utilizador) para iniciar sessão.  

##  <a name="BKMK_SW1"></a> Separadores novas atualizações e sistemas operativos no Centro de Software  
 Nesta versão, as seguintes alterações foram efetuadas para melhorar o esquema da aplicação Centro de Software:  

-   O **aplicações** separador foi foi dividido em três separadores separados para **atualizações**, **sistemas operativos** (que foram ambos anteriormente encontradas no **filtros** lista), e **aplicações**.  

##  <a name="BKMK_ServerGroups"></a> Um grupo de servidores de serviço  
 Pré-visualização técnica do System Center Configuration Manager, versão 1511, incluída a capacidade de criar uma coleção em que todos os dispositivos na coleção constituem um grupo de servidor. Em seguida, pode configurar as definições do grupo de servidor para utilizar quando implementa atualizações de software para o grupo de servidor, o controlo a percentagem de computadores que são atualizadas em qualquer momento, e configurar scripts do PowerShell de pré-implementação e pós-implementação para executar ações personalizadas.  

 Pré-visualização técnica do System Center Configuration Manager, versão 1605, adiciona a capacidade para atualizar os computadores no grupo de servidor por uma ordem especificada definir, adiciona a monitorização avançada para ver o estado para os computadores no grupo de servidor e fornece a capacidade de limpar os bloqueios de implementação que é útil quando os clientes não tem conseguido instalar as atualizações de software e estão a impedir outros clientes instalar as atualizações de software.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, informe-nos como correu utilizando o nosso formulário de comentários no [programa de feedback do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Pode criar uma coleção que representa um grupo de servidor. Para este teste, pode configurar as regras de associação recolhidas para ter 2 computadores nesta coleção.   

-   Consigo especificar que os computadores no grupo de servidor instalar atualizações de software por uma ordem específica, com base nas definições do grupo de servidor para a coleção. Utilize os scripts de exemplo no procedimento para especificar os scripts de pré-implementação e pós-implementação.  

-   Pode implementar uma atualização de software desta coleção. Consulte os ficheiros de hora e end.txt (criados a partir os scripts de exemplo) em C:\temp e verifique se os tempos de início e de fim para a implementação nos computadores no grupo de servidor. Reveja o ficheiro UpdatesDeployment.log para mais informações.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  

1.  [Criar uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contenha os computadores no grupo de servidor.  

2.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, faça duplo clique na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  No **geral** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  No **as definições do grupo de servidor** página, especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem das máquinas seja atualizada ao mesmo tempo**: Especifica que apenas determinada percentagem de clientes são atualizadas ao mesmo tempo. Se, por exemplo, a coleção tem 10 clientes, e a coleção é configurada para atualização 30% de clientes ao mesmo tempo, em seguida, apenas 3 clientes irão instalar atualizações de software em qualquer momento.  

    -   **Permitir que um número de máquinas seja atualizada ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado ao mesmo tempo.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção será atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar atualizações de software depois do cliente que está à frente das-la na lista concluiu a instalação respetivas atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem do nó) ou um script de pós-implementação (retoma do nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar no teste de pré-implementação e pós-implementação scripts que escrevem a hora atual para um ficheiro de texto:  
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

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implementar atualizações de software para o estado do monitor e o grupo de servidor  

1.  [Implementar atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) na coleção de grupo do servidor.  

2.  [Monitorizar a implementação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx). Para além das vistas de monitorização padrão para a implementação de atualizações de software, uma nova descrição de estado é apresentada quando um cliente está a aguardar a ativar instalar as atualizações de software. **À espera de bloqueio** é apresentada para este novo Estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para limpar os bloqueios de implementação para computadores num grupo de servidor  

1.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  No **home page** separador o **implementação** , clique em **bloqueia de implementação de grupo de servidor limpar**. Quando os clientes não tem conseguido instalar as atualizações de software e estão a impedir outros clientes instalar as atualizações de software, os bloqueios de implementação podem ser eliminados manualmente.  

##  <a name="BKMK_ATP"></a> Suporte para o serviço do Windows Defender Advanced Threat Protection  
 Avançadas Threat Protection (ATP do Windows Defender) é um novo serviço que o irão ajudar as empresas para detetar, analisar e responder a ataques avançados nas respetivas redes. Saiba mais sobre [Windows Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). O Configuration Manager pode ajudá-lo com a sua integração e monitorizar dispositivos de cliente de edição do Windows 10 Anniversary geridos.  

### <a name="try-it-now"></a>Experimente agora!  
 Experimente concluir as seguintes tarefas e, em seguida, informe-nos como correu utilizando o nosso formulário de comentários no [programa de feedback do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Carregar dispositivos para o serviço online do Windows Defender Advanced Threat Protection (ATP)  

-   Monitorizar a implementação do Windows Defender ATP em dispositivos geridos  

 **Pré-requisitos**  

-   Subscrição do serviço online do Windows Defender Advanced Threat Protection  

-   Clientes que executam o Windows 10, aniversário da edição (compilação 14328 e superior)  

-   Criar um ficheiro de configuração de integração do cliente  

    ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um ficheiro de configuração de integração  

    1.  Início de sessão para o serviço online do Windows Defender ATP  

    2.  Clique em de **cliente Dependency** item de menu  

    3.  Selecione **System Center Configuration Manager** e clique em **pacote de transferência**.  

    4.  Transfira o ficheiro de arquivo comprimido (. zip) e extraia os conteúdos.  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP Policy**. É aberto o Assistente de política do Windows Defender ATP.  

2.  Tipo de **nome** e **Descrição** para o Windows Defender ATP policy selecione **integração**. Clique em Seguinte.  

3.  **Procurar** para o ficheiro de configuração fornecido pelo inquilino de serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

4.  Especifique os exemplos de ficheiros que são recolhidos e partilhados a partir dos dispositivos geridos para análise.  

    -   **Nenhum** – não existem ficheiros de exemplo são recolhidos para análise  

    -   **Ficheiros executáveis portátil** – ficheiros, tais como programas (.exe), ficheiros de ligação dinâmica de biblioteca (. dll), ficheiros de tipo de letra e se os ficheiros semelhantes que podem ser forem explorados no cyberattacks são recolhidos e partilhados para análise  

     Clique em **Seguinte**.  

5.  Reveja o resumo e conclua o assistente.  

6.  Agora pode implementar a política Windows Defender ATP para os computadores cliente geridos clicando **implementar**.  

##### <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard do Windows Defender Advanced Threat Protection.  

    -   **Estado de implementação de agente do Windows Defender** – o número e a percentagem de computadores elegíveis cliente gerido com o Active Directory integrado de política Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – percentagem de clientes de computador a comunicar o estado para os respetivos agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativa** -não existem dados enviados ao serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente do Windows não está em execução  

        -   **Não existem integrado** - foi aplicada a política, mas o agente não comunicou carregar política  

##  <a name="BKMK_DHA"></a> Atestado de estado de funcionamento de dispositivos no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 pode agora ser configurado para comunicar utilizando a infraestrutura no local. Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local. Se estiver selecionada no local para fins de atestado de estado de funcionamento de relatórios, um URL pode ser especificado para o serviço. Isto permite que os computadores cliente sem acesso à internet ativar e gerir dispositivos através de atestado de estado de funcionamento.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar o atestado de estado de funcionamento de dispositivos no local  
 No 1605, iremos tiver fixo alguns erros detetados no 1604 Technical Preview.  Para experimentá-lo, configure o serviço de atestado de estado de funcionamento no local utilizando as definições de agente do cliente.  

1.  Na consola do Configuration Manager, navegue **administração** > **descrição geral** > **as definições de cliente**e, em seguida, defina **utilizar no local o serviço de atestado de estado de funcionamento** para **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

##  <a name="BKMK_RestartOptions"></a> Novo as opções para clientes Windows 10 de reinício após a instalação de atualização de software  
 Quando uma atualização de software que requer um reinício é implementado utilizando o Gestor de configuração e instalado num computador, um reinício pendente está agendado e é apresentada uma caixa de diálogo de reinício. Atualmente, para o Windows 8 e superior, se lhe encerrar ou reiniciar o computador utilizando as opções de energia do Windows (em vez da caixa de diálogo de reinício), os permanecem de caixa de diálogo de reinício após os reinícios de computador e o computador serão necessário reiniciar no prazo de configurado. Nesta pré-visualização técnica, a opção de **atualizar e reinicie** e **Update e no encerramento** estará disponível em computadores Windows 10 opções de energia do Windows sempre que há um reinício pendente para uma atualização de software do Configuration Manager. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será apresentada depois do reinício do computador.  

##  <a name="BKMK_IMEI"></a> Pré-declarar dispositivos pertencentes à empresa com o número de série iOS ou IMEI  
 Agora pode identificar dispositivos pertencentes ao importar os respetivos números de identidade (IMEI) estação internacional do equipamento móvel. Pode carregar um ficheiro de valores separados por vírgulas (. csv) contendo os números IMEI de dispositivo ou pode introduzir manualmente as informações do dispositivo.  Também pode importar os números de série para dispositivos iOS.  Informação importada definirá a propriedade dos dispositivos inscritos como "Empresa".  Uma licença do Intune é ainda necessária para cada utilizador que acede ao serviço.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, informe-nos como correu utilizando o nosso formulário de comentários no [programa de feedback do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Importe um conjunto de números IMEI num ficheiro. csv. Cada linha pode conter o número IMEI seguido de um campo de detalhes.  

-   Importe os números IMEI manualmente a partir da consola do Configuration Manager.  

-   Importe um conjunto de números de série iOS num ficheiro. csv. Novamente, cada linha contém um número seguido por quaisquer detalhes para o dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS  

1.  Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **Pre-declared dispositivos**e, em seguida, clique em **criar dispositivos de Pre-declared**. É aberto o Assistente de Pre-declared dispositivos.  

2.  Especifique como pretende adicionar informações do dispositivo:  

    -   **Carregar um ficheiro. csv contendo os números IMEI e os detalhes** - para carregar uma lista de números, consulte o passo 3.  

    -   **Adicionar manualmente os números IMEI e os detalhes** - para introduzir manualmente as informações, escreva o número IMEI ou número de série iOS e os detalhes para os dispositivos e, em seguida, avance para o passo n. º 4.  

3.  Para os ficheiros carregados, procure o ficheiro. csv que contém informações de pré-declarar dispositivos pertencentes à empresa. O ficheiro tem de ter o seguinte formato, excluindo a linha superior (fornecida para obter orientações sobre apenas):  

    |**IMEI N. º**|**Série de iOS**|**OS**|**Detalhes**|
    |---|---|---|---|
    |123456789012345||WINDOWS|Dispositivo de Windows pertencentes à empresa|
    |123456789012|A0BCD0EFGH0J|IOS|Dispositivos iOS pertencentes à empresa|
    |123456789012346||ANDROID|Dispositivo Android da empresa|

     **Colunas:**  

    -   Coluna 1: Número IMEI – ou um número ou iOS série número IMEI é necessário para cada linha  

    -   A coluna 2: número de série iOS – apenas os números de série iOS pode ser declarados previamente. Utilize o número IMEI para outras plataformas de dispositivos  

    -   Coluna 3: Sistema operativo do dispositivo (maiúsculas/minúsculas necessário):  

        -   IOS – todos os dispositivos iOS  

        -   WINDOWS – inclui Windows Phone, Windows 10 Mobile e Windows PCs  

        -   ANDROID – todos os dispositivos Android  

    -   Coluna 4: Detalhes – informações de dispositivo adicionais que aparece na consola do Configuration Manager  

     Clique em **Seguinte**.  

4.  Reveja os resultados da importação de ficheiro. Anteriormente os números de série ou IMEI importados terão os respetivos detalhes atualizados com detalhes de novo.  Clique em **seguinte** para continuar ou **novamente** para manter atualizados detalhes e, em seguida, conclua o assistente.  
