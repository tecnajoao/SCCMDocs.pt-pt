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
ROBOTS: NOINDEX
ms.openlocfilehash: 2f8843a5d4e3b49126e2d0898a5bd006422957d2
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898159"
---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1605 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1605. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 **Problemas conhecidos neste Technical Preview:**  

- Com o Technical Preview 1605, se atualizar as propriedades de um ponto de gestão após a instalação, poderá ver um erro de consola que força a consola para fechar.  Se isto acontecer, pode desinstalar o ponto de gestão e, em seguida, reinstalar o ponto de gestão utilizando as definições pretendidas. Em alternativa, pode modificar o ponto de gestão antes de instalar o Technical Preview 1605.  

- Quando utiliza a Windows Store para a funcionalidade de negócios com o 1604 de pré-visualização técnica e, em seguida, atualizar para o Technical Preview 1605, já não pode ver os dados de inclusão. Todos os outros funcionalmente continua a funcionar. Se efetuou com 1604 de pré-visualização técnica,-o a manter carregadas depois de instalar o Technical Preview 1605 e não tem de tomar nenhuma ação adicional.  

  **Seguem-se os novos recursos, que pode experimentar com esta versão.**  

##  <a name="BKMK_PerAppVPN"></a> Por aplicação VPN para dispositivos Windows 10  
 Para dispositivos do Windows 10 geridos com o Configuration Manager com o Intune, pode adicionar uma lista de aplicações que abra automaticamente uma ligação de VPN que tiver configurado através da consola de administração do Configuration Manager. Tem a opção de restringir o tráfego VPN para essas aplicações, ou pode continuar a permitir todo o tráfego através da ligação VPN.  

 **Requisitos de**:  

-   Configuration Manager com Intune  

-   Um perfil de VPN do Windows 10 que tenha sido implementado para, pelo menos, um dispositivo  

##  <a name="BKMK_InstallSU"></a> Melhorias para a sequência de tarefas instalar atualizações de software  
 Foram efetuadas as seguintes melhorias para a sequência de tarefas instalar atualizações de Software:  

-   Uma variável de sequência de tarefas nova, SMSTSSoftwareUpdateScanTimeout, está disponível para lhe dar a capacidade de controlar o tempo limite em análise de atualizações de software durante o passo de sequência de tarefas de atualizações de software de instalação. O valor predefinido é 30 minutos.  

-   Foram melhorias ao registo. O ficheiro smsts log contém novas entradas de log que fazem referência a outros ficheiros de registo que lhe ajudarão a resolver problemas durante o processo de instalação de atualizações de software.  

##  <a name="BKMK_PrepareConfigMgrClient"></a> Melhorias para o preparar ConfigMgr Client para o passo de sequência de tarefas de captura  
 O passo preparar ConfigMgr Client agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas implementa a imagem de sistema operativo capturada que irá instalar um novo cliente de Configuration Manager cada vez.  

##  <a name="BKMK_Grace"></a> Período de tolerância para implementações de aplicações necessárias  
 Em alguns casos, talvez queira dar aos utilizadores mais tempo para instalar as implementações de aplicações necessárias para além de quaisquer prazos configurados. Por exemplo, se um utilizador final acabou de voltar de férias, poderá ter de aguardar por um longo enquanto como aplicação em atraso implementações estão instaladas. No entanto, ainda imediatamente podem instalar a aplicação a qualquer momento que desejarem.  

 Para ajudar a resolver este problema, pode agora definir um **período de tolerância** ao implementar as definições de cliente do Configuration Manager para uma coleção.  

 Para configurar o período de tolerância, efetue as seguintes ações:  

1. Sobre o **agente do computador** página de definições de cliente, configurar a nova propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.  

2. Numa nova implementação de aplicação ou nas propriedades de uma implementação existente, sobre o **agendamento** , selecione a caixa de verificação **Trasar imposição para esta implementação, de acordo com as preferências do usuário**, até o período de tolerância definido nas definições do cliente.  

    Todas as implementações com esta caixa de verificação selecionada e que é direcionado para os dispositivos em que implementou também a definição de cliente utilizará o período de tolerância.  

   Nesta versão, o período de tolerância que configurar não é utilizado pelos dispositivos cliente. Se configurar um período de tolerância e selecionar a caixa de verificação, a aplicação será instalada na primeira janela não comerciais que o utilizador configurado após o prazo.  

   Foram adicionadas opções similares para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades. No entanto, estes não são atualmente implementadas neste technical Preview.  

##  <a name="BKMK_Remote"></a> Nova experiência para ações remotas de dispositivos  
 Foi melhorada a experiência para executar ações remotas de dispositivos a partir da consola do Configuration Manager.  
Ações comuns, como **extinguir/limpar**, **repor código de acesso**, **bloqueio remoto**, e **ignorar bloqueio de ativação** agora podem ser encontradas no  **Ações do dispositivo remoto** menu acedido a partir de **ativos e compatibilidade** área de trabalho.  

 ![Nova captura de ecrã de ações do dispositivo remoto](media/New-Remote-Device-Actions.png)  

 Pode encontrar o estado para cada uma destas operações nos seguintes locais:  

- No painel de detalhes ao selecionar um dispositivo a partir da **dispositivos** nó.  

- Sobre o **propriedades** página para um dispositivo.  

- Na página principal do **dispositivos** nó (nem todas as colunas podem ser visíveis por padrão).  

  Para obter mais informações sobre a desativação do bloqueio de ativação de iOS, veja [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando o para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock), em particular, o **atuais problemas conhecidos com o bloqueio de ativação, desativação no Configuration Manager Technical Preview** secção.  

##  <a name="BKMK_WSFB"></a> Windows Store para aplicações empresariais  
 O [Windows Store para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja para o Configuration Manager, pode gerir aplicações compradas em volume da consola do Configuration Manager, por exemplo:  

- Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

- As aplicações que são sincronizadas aparecem na consola do Configuration Manager e pode implementá-las como todas as outras aplicações  

- A cada 24 horas, Configuration Manager transfere as informações de licenciamento de aplicações da loja e pode rever o que isso na consola do Configuration Manager  

  Na versão 1604 technical preview, pode sincronizar e ver aplicações a partir da Windows Store para empresas na consola do Configuration Manager. Nesta versão, adicionámos a capacidade de criar e implementar aplicações do Configuration Manager a partir de aplicações da loja sincronizados.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a Windows Store para sincronização de negócios  

1.  No Azure Active Directory, registe-se o Configuration Manager, como uma ferramenta de gestão "Aplicação Web e/ou API Web". Isso lhe fornecerá uma ID de cliente que irá precisar mais tarde.  

    1.  No nó do Active Directory [ https://manage.windowsazure.com ](https://manage.windowsazure.com), selecione o Azure Active Directory, em seguida, clique em **aplicativos** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique nas **seguinte** seta.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudomínio > / sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Sob **chaves**, selecione uma duração a partir da lista e clique em **guardar**. Isto irá criar uma nova chave de cliente. Não saia desta página até ter com êxito integrado a Windows Store para empresas para o Configuration Manager.  

3.  O Store do Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de armazenamento.  

    1.  Open [ https://businessstore.microsoft.com/en-us/managementtools ](https://businessstore.microsoft.com/managementtools) e início de sessão se lhe for pedido.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Sob **ferramentas de gestão**, clique em **adicionar uma ferramenta de gerenciamento**.  

    4.  Na **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **Add**.  

    5.  Clique em **Activate** junto da aplicação que acabou de importar.  

    6.  Na **aplicações licenciadas** assistente, clique em **Sim** se pretender permitir que aplicações licenciadas offline ser adquirido.  

4.  Compre, pelo menos, uma aplicação a partir da Windows Store para empresas.  

5.  Na **administração** área de trabalho da consola do Configuration Manager, expanda **serviços Cloud**, em seguida, clique em **Windows Store para empresas.**  

6.  Na **home page** separador a **Create** , clique em **Add Windows Store para empresas conta**.  

7.  Adicionar o seu ID de inquilino, o id de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta que configurou no **Windows Store para empresas contas** lista na consola do Configuration Manager.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir a seguinte tarefa e, em seguida, queremos saber como ele funcionava com o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

 Criar e implementar uma aplicação do Configuration Manager a partir de um Store do Windows para empresas aplicação com licença offline.  

1. Na **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações de Store**.  

2. Escolha a aplicação que pretende implementar, em seguida, na **home page** separador a **Create** , clique em **Criar aplicação**.  

   Uma aplicação do Configuration Manager é criada que contém a Windows Store para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

> [!IMPORTANT]  
>  Quando cria uma aplicação do Configuration Manager com um tipo de implementação única de uma aplicação com licença offline, isto pode ser implementado a dispositivos MDM geridos e também geridos com o cliente do Configuration Manager. Se tentar implementar uma aplicação com vários tipos de implementação, a instalação irá falhar.  
>   
>  Atualmente não é possível implementar aplicações licenciadas online com o Configuration Manager.  

##  <a name="BKMK_VPP2"></a> Melhoramentos gerais para aplicações compradas em volume  

-   Nesta versão, aplicações compradas em volume a partir da Windows Store para empresas e a aplicação iOS store foram consolidados na mesma exibição **informações de licença para aplicações Store**.  

-   Para aplicações compradas em volume iOS, no separador de Apple Volume Purchase Program tiver sido removido dos **pacote de aplicação para iOS Browser** caixa de diálogo no Assistente para criar aplicação. Para criar uma aplicação comprada em volume para iOS, utilize estes passos:  

    1.  1.  Na **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações de Store**.  

    2.  2.  Escolha a aplicação que pretende implementar, em seguida, na **home page** separador a **Create** , clique em **Criar aplicação**.  

-   A localização a que se usar para obter e carregar um token de VPP da Apple para aplicações compradas em volume na consola do Configuration Manager foi alterada. Agora pode fazer isso do **administrador** área de trabalho sob a **serviços Cloud** > **Tokens do programa Apple Volume Purchase** nó.  

##  <a name="BKMK_VPP"></a> Proteção de dados empresariais (EDP)  
 Pode criar itens de configuração que permitem-lhe implementar as políticas de proteção (EDP) de dados empresarial, incluindo lhe permite escolher as suas aplicações protegidas, seu nível de proteção de EDP e como encontrar os dados empresariais na rede. Para obter mais informações sobre EDP, consulte os seguintes tópicos:  

-   [Proteger os dados empresariais com a proteção de dados empresariais (EDP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [Criar e implementar uma política de proteção (EDP) de dados empresariais com o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a> Os utilizadores finais podem instalar aplicações do Portal da empresa  
 No local MDM foi introduzido do System Center Configuration Manager versão 1511. Nas versões anteriores, pode implementar aplicações em dispositivos Windows 10 geridos por MDM com o objetivo de implementação **necessário** instalar para dispositivos de gerido por MDM no local.  

 Nesta versão, pode agora implementar aplicações com um objetivo de implementação **disponível** aos utilizadores no local geridos pela MDM computadores Windows 10 e os utilizadores podem agora instalar estes próprias aplicações do Portal da empresa.
Neste technical Preview, se o Portal da empresa está aberto por mais de 15 minutos, o utilizador final verá uma mensagem de erro. Para contornar o problema, reinicie o Portal da empresa.  

### <a name="before-you-start"></a>Antes de começar  

#### <a name="server-prerequisites"></a>Pré-requisitos do servidor  

-   .NET 4.5 ou superior (requer reinicialização)  

-   PowerShell 3.0 para o script de configuração (requer reinicialização)  

#### <a name="client-prerequisites"></a>Pré-requisitos do cliente  

-   Windows 10 Desktop 1511 (compilação 10586.218 de SO) ou posterior  

#### <a name="general-prerequisites"></a>Pré-requisitos gerais  

-   Certifique-se de que concluiu o [passos de preparação para gestão de dispositivos móveis no local](https://technet.microsoft.com/library/mt613153.aspx) e [inscrito os seus dispositivos](https://technet.microsoft.com/library/mt627870.aspx).  

-   Para o aplicativo melhor instalar a experiência quando utilizar o Portal da empresa, certifique-se de que o Configuration Manager possui uma conexão ativa com o Microsoft Intune.  

-   Se escolher a opção de inscrição em massa, configure a afinidade de dispositivo / utilizador para o dispositivo inscrito antes de tentar este cenário.  

### <a name="configuration-steps"></a>Passos de configuração  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instalar as funções de catálogo de aplicações e ativar o suporte de gestão de dispositivos móveis  

1.  Adicionar as funções do serviço de Web do catálogo de aplicações e Web Site  

    1.  Selecione **modo HTTPS** e o **permitir que os dispositivos móveis utilizem este ponto de serviço de Web do catálogo de aplicações** opção.  

    2.  Limitações neste Technical Preview:  

        -   Tem de desinstalar qualquer funções existentes do catálogo de aplicações antes de selecionar a opção para permitir que dispositivos móveis se liguem.  

        -   Certificar-se de que existe apenas um conjunto de funções de catálogo de aplicações e as funções são colocalizadas no mesmo sistema de sites com o ponto de registo e as funções de ponto de Proxy de registo.  

2.  Certifique-se de que os seguintes componentes estão operacionais a partir do nó Estado do componente na consola do Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar limites  
 Configure limites necessários para pontos de distribuição apenas de intranet.  

> [!NOTE]  
>  Limites de intervalo de IPv4 apenas são suportados neste momento para gestão de dispositivos móveis.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implementar a aplicação Portal da empresa e a configuração  

1. Utilize o script de configuração incluído com o technical preview para preparar a implementação do Portal da empresa e a configuração:  

   1. Abra uma janela de comando do PowerShell elevada.  

   2. Executar **set-executionPolicy RemoteSigned**  

   3. A partir da pasta  **&lt;diretório de instalação do SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM** executar **.\ConfigurationScript.ps1**  

      O script de configuração faz o seguinte:  

   4. Cria uma aplicação do Configuration Manager com um Windows aplicação pacote implementação tipo com **CompanyPortalOnPremisesMDM.appx** na mesma pasta.  

   5. Cria um item de configuração e a linha de base de configuração que configura o Portal da empresa.  

   6. Implementa a linha de base de configuração e a aplicação e adiciona o aplicativo para todos os pontos de distribuição.  

   > [!NOTE]
   >  Se as funções de catálogo de aplicações não estiverem localizadas conjuntamente com o site primário, efetue as seguintes ações:  
   > 
   > - Na **ativos e compatibilidade** área de trabalho, localize a **CI de configuração do Portal OnPremMDM - urls do servidor** item de configuração  
   >   -   Alteração da **regras de conformidade** valor para o nome de domínio completamente qualificado do sistema de sites onde estão localizadas as funções de catálogo de aplicações.  

2. Assim que a aplicação Portal da empresa e a respetiva configuração são implementadas, verifique se a linha de base de configuração e de aplicação estão em conformidade para a determinado dispositivo utilizando **implementações** secção da consola do Configuration Manager. O Portal da empresa irá aparecer como **Portal da empresa (pré-visualização técnica)** no menu Iniciar no dispositivo.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, queremos saber como ele funcionava com o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

1.  Implementar vários aplicativos com tipos de implementação suportado para uma coleção de utilizador com um objetivo de implementação **disponível**. Para esta pré-visualização técnica, os aplicativos que exigem a aprovação de administrador não são suportados e não serão apresentados no Portal da empresa.  

2.  Os utilizadores podem, em seguida, procurar e instalar aplicações a partir do Portal da empresa.  

     Depois de abrir o Portal da empresa, verá uma caixa de diálogo de autenticação com o nome **System Center Configuration Manager** especificar as credenciais do usuário do Active Directory (na forma de user@domain ou domínio \ utilizador) para iniciar sessão.  

##  <a name="BKMK_SW1"></a> Novos separadores para atualizações e sistemas operativos no Centro de Software  
 Nesta versão, as seguintes alterações foram feitas para melhorar o esquema da aplicação Centro de Software:  

-   O **aplicativos** separador foi dividido em três guias separados para **atualizações**, **sistemas operativos** (que ambos anteriormente encontradas no **filtros**  lista), e **aplicativos**.  

##  <a name="BKMK_ServerGroups"></a> Serviço de um grupo de servidores  
 Pré-visualização técnica do System Center Configuration Manager, versão 1511, incluímos a capacidade de criar uma coleção em que todos os dispositivos na coleção constituem um grupo de servidores. Em seguida, pode configurar as definições de grupo do servidor para utilizar quando implementa atualizações de software para o grupo de servidor, o controle a percentagem de computadores que são atualizados em qualquer momento, e configurar o pré e pós-implementação scripts do PowerShell para executar ações personalizadas.  

 Pré-visualização técnica do System Center Configuration Manager, versão 1605, adiciona a capacidade de atualizar os computadores no grupo de servidor numa ordem especificada que definir, adiciona a monitorização avançada para ver o estado para os computadores no grupo de servidor e que fornece a capacidade de limpar os bloqueios de implementação que é útil quando os clientes tiverem falhado instalar as atualizações de software e estão a impedir que outros clientes de instalar as atualizações de software.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, queremos saber como ele funcionava com o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Posso criar uma coleção que representa um grupo de servidores. Para este teste, pode configurar as regras de associação recolhidas para ter 2 computadores nesta coleção.   

-   Posso especificar que computadores no grupo de servidor instalam atualizações de software numa ordem específica, com base nas definições de grupo do servidor para a coleção. Utilize os scripts de exemplo no procedimento para especificar os scripts de pré e pós-implementação.  

-   Posso implantar uma atualização de software para esta coleção. Reveja os ficheiros txt e Start (criados a partir dos scripts de exemplo) em C:\temp e certifique-se de horas de início e de fim para a implementação nos computadores no grupo de servidor. Reveja o ficheiro Updatesdeployment log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  

1.  [Criar uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contenha os computadores no grupo de servidor.  

2.  Na **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, clique com o botão direito na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  Sobre o **gerais** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  Sobre o **definições do grupo de servidor** , especifique uma das seguintes definições:  

    -   **Permitir que uma porcentagem de computadores seja atualizada ao mesmo tempo**: Especifica que apenas uma determinada percentagem de clientes são atualizados num dado momento. Se, por exemplo, a coleção tem 10 clientes, e a coleção é configurada para atualização 30% de clientes ao mesmo tempo, os clientes apenas 3 irão instalar as atualizações de software em qualquer momento.  

    -   **Permitir um número de computadores seja atualizada ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado num dado momento.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção será atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar as atualizações de software depois do cliente que é um passo à frente-lo na lista concluiu a instalação suas atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem do nó) ou o script de pós-implementação (retoma do nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar em testes de pré-implantação e os scripts de pós-implementação escrevem a hora atual num arquivo de texto:  
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
    >  **Post-deployment**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implementar atualizações de software para o estado do monitor e o grupo de servidor  

1.  [Implementar atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) para a coleção de grupo do servidor.  

2.  [Monitorizar a implementação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx). As vistas de monitorização padrão para a implementação de atualizações de software, além de uma nova descrição de estado é apresentada quando um cliente está a aguardar por sua vez para instalar as atualizações de software. **À espera de bloqueio** é apresentado para o novo Estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para limpar os bloqueios de implementação para computadores num grupo de servidor  

1.  Na **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  Sobre o **home page** separador a **implementação** , clique em **bloqueios de implementação de grupo de servidor clara**. Quando os clientes tiverem falhado instalar as atualizações de software e estão a impedir que outros clientes de instalar as atualizações de software, os bloqueios de implementação podem ser removidos manualmente.  

##  <a name="BKMK_ATP"></a> Suporte para o serviço de proteção de ameaças avançada do Windows Defender  
 Windows Defender avançadas proteção contra ameaças (ATP) é um serviço novo que irá ajudar as empresas a detetar, investigar e responder a ataques avançados em suas redes. Saiba mais sobre [do Windows Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). O Configuration Manager pode ajudá-lo a integrar e monitorizar dispositivos de cliente do Windows 10 Anniversary Edition geridos.  

### <a name="try-it-now"></a>Experimente agora!  
 Experimente concluir as seguintes tarefas e, em seguida, queremos saber como ele funcionava com o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

- Carregar dispositivos para o serviço online da proteção de ameaças avançada do Windows Defender (ATP)  

- Monitorizar a implementação do Windows Defender ATP para dispositivos geridos  

  **Pré-requisitos**  

- Subscrição do serviço online da proteção de ameaças avançada do Windows Defender  

- Clientes que executam o Windows 10, Anniversary Edition (compilação 14328 e superior)  

- Criar um ficheiro de configuração de integração do cliente  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

  1.  Início de sessão para o serviço online do Windows Defender ATP  

  2.  Clique nas **cliente integração** item de menu  

  3.  Selecione **System Center Configuration Manager** e clique em **pacote de transferência**.  

  4.  Transfira o ficheiro de arquivo morto compactado (. zip) e extraia o conteúdo.  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para o Windows Defender ATP  

1. Na consola do Configuration Manager, navegue até **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection**  >  **Políticas do Windows Defender ATP** e clique em **criar o Windows Defender ATP política**. É aberto o Assistente de política do Windows Defender ATP.  

2. Tipo de **Name** e **Descrição** para a política do Windows Defender ATP e selecione **integração**. Clique em Seguinte.  

3. **Procurar** ao arquivo de configuração fornecido pelo inquilino de serviço cloud da sua organização do Windows Defender ATP. Clique em **Seguinte**.  

4. Especifique os exemplos de ficheiros que são recolhidos e partilhados dos dispositivos geridos para análise.  

   - **Nenhum** – não existem ficheiros de exemplo são recolhidos para análise  

   - **Ficheiros executáveis portáteis** – o programa de ficheiros, tais como ficheiros (.exe), arquivos de link de biblioteca dinâmico (. dll), arquivos de fonte, e que ficheiros semelhantes que podem ser explorados em ataques cibernéticos são recolhidos e partilhados para análise  

     Clique em **Seguinte**.  

5. Reveja o resumo e conclua o assistente.  

6. Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos ao clicar em **Deploy**.  

##### <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard de proteção de ameaças avançada do Windows Defender.  

    -   **Estado de implementação de agente do Windows Defender** – o número e percentagem de computadores de cliente gerenciado elegíveis com o Active Directory integrado de política do Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – porcentagem de computadores cliente comunicar o estado para o agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativo** -não existem dados enviados para o serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente no Windows não está em execução  

        -   **Não incluído** - política foi aplicada, mas o agente não comunicou carregar política  

##  <a name="BKMK_DHA"></a> Atestado de estado de funcionamento do dispositivo no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 agora pode ser configurado para comunicar com a infraestrutura no local. Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local. Se no local para o relatório de atestado de estado de funcionamento, em seguida, um URL pode ser especificado para o serviço. Isso permite que os computadores de cliente sem acesso à internet ativar e gerir dispositivos através do atestado de estado de funcionamento.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar o atestado de estado de funcionamento para dispositivos no local  
 Na versão 1605, Corrigimos alguns bugs descobertos no 1604 Technical Preview.  Para experimentá-lo, configure o serviço de atestado de estado de funcionamento no local com as definições de agente do cliente.  

1.  Na consola do Configuration Manager, navegue até **Administration** > **descrição geral** > **as definições de cliente**e, em seguida, defina **Utilizar no local o serviço de atestado de estado de funcionamento** para **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

##  <a name="BKMK_RestartOptions"></a> Novas opções para clientes Windows 10 de reinício após a instalação de atualização de software  
 Quando uma atualização de software que requer um reinício é implementado utilizando o Gestor de configuração e instalado num computador, é agendado um reinício pendente e é apresentada uma caixa de diálogo de reinício. Atualmente, para o Windows 8 e acima, se encerrar ou reiniciar o computador utilizando as opções de energia do Windows (em vez de na caixa de diálogo de reinício), o permanece de caixa de diálogo de reinício após os reinícios de computador e o computador será necessário reiniciar no prazo de configurado. Neste technical Preview, a opção para **atualizar e reiniciar** e **atualizar e encerrar** estará disponível em computadores Windows 10 nas opções de energia do Windows sempre que existe um reinício pendente para um Atualização de software do Configuration Manager. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será apresentada depois do reinício do computador.  

##  <a name="BKMK_IMEI"></a> Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS  
 Agora é possível identificar os dispositivos pertencentes ao importar os números de identidade (IMEI) de equipamento móvel internacional. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI de dispositivos ou pode introduzir manualmente as informações do dispositivo.  Também pode importar números de série para dispositivos iOS.  Informação importada definirá a propriedade dos dispositivos que inscrever como "Empresa".  Uma licença do Intune ainda é necessária para cada utilizador que acede ao serviço.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, queremos saber como ele funcionava com o nosso formulário de comentários no [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) página no site Microsoft Connect:  

-   Importe um conjunto de números IMEI num ficheiro. csv. Cada linha pode conter o número IMEI, seguido de um campo de detalhes.  

-   Importe números IMEI manualmente a partir da consola do Configuration Manager.  

-   Importe um conjunto de números de série iOS num ficheiro. csv. Novamente, cada linha contém um número seguido por todos os detalhes para o dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS  

1. Na consola do Configuration Manager, aceda **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos da empresa**  >  **Dispositivos pre-declared**e, em seguida, clique em **criar dispositivos de Pre-declared**. É aberto o assistente Pre-declared dispositivos.  

2. Especifique como pretende adicionar informações do dispositivo:  

   -   **Carregar um ficheiro. csv com números IMEI e os detalhes** - para carregar uma lista de números, veja o passo 3.  

   -   **Adicionar manualmente os números IMEI e os detalhes** - para introduzir manualmente as informações, escreva o número IMEI ou número de série iOS e os detalhes para os dispositivos e, em seguida, avance para a etapa 4.  

3. Para ficheiros carregados, navegue para o ficheiro. csv que contém informações de pré-declarar dispositivos pertencentes à empresa. O ficheiro tem de ter o seguinte formato, excluindo a linha superior (fornecida para obter orientações apenas):  

   |**IMEI N. º**|**Série do iOS**|**OS**|**Detalhes**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Dispositivo de Windows pertencentes à empresa|
   |123456789012|A0BCD0EFGH0J|IOS|Dispositivos iOS pertencentes à empresa|
   |123456789012346||ANDROID|Dispositivo Android pertencentes à empresa|

    **Colunas:**  

   - Coluna 1: Número IMEI – seja um número ou iOS série número IMEI é necessário para cada linha  

   - Coluna 2: número de série iOS – apenas os números de série do iOS pode ser declarados previamente. Utilize o número IMEI para outras plataformas de dispositivos  

   - Coluna 3: Sistema operativo do dispositivo (capitalização necessário):  

     -   IOS – todos os dispositivos iOS  

     -   WINDOWS – inclui Windows Phone, Windows 10 Mobile e Windows PCs  

     -   ANDROID – todos os dispositivos Android  

   - Coluna 4: Detalhes – informações de dispositivo adicionais que surge na consola do Configuration Manager  

     Clique em **Seguinte**.  

4. Reveja os resultados da importação de ficheiros. Anteriormente números de série ou IMEI importados terão seus detalhes atualizados com novos detalhes.  Clique em **próxima** para continuar ou **volta** para manter atualizados detalhes e, em seguida, conclua o assistente.  
