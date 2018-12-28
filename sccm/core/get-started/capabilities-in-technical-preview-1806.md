---
title: Pré-visualização técnica 1806
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis na versão do Configuration Manager Technical Preview 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8914c9ff7a33d24b5d68893018edff8d8e0de444
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424318"
---
# <a name="capabilities-in-technical-preview-1806-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1806 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview no Configuration Manager, versão 1806. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja os [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview

### <a name="ki_contentlib"></a> Site não conseguir atualizar com a biblioteca de conteúdos remota
<!--514642--> O site não conseguir atualizar com os seguintes erros na **cmupdate. log**:  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Este problema ocorre nesta versão, quando a biblioteca de conteúdos está numa localização remota.

#### <a name="workaround"></a>Solução
Mova a biblioteca de conteúdos para uma unidade local para o servidor do site. Para obter mais informações, consulte [configurar uma biblioteca de conteúdos remota para o servidor de site](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server). 



</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  



## <a name="bkmk-3pupdate"></a> Atualizações de software de terceiros
<!--1352101--> Esta versão ainda mais itera sobre o suporte para atualizações de software de terceiros, como resultado de sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Já não precisa a utilização do System Center Updates Publisher (SCUP) para alguns cenários comuns. A nova **catálogos de atualização de Software de terceiros** nó na consola do Configuration Manager permite-lhe subscrever catálogos de terceiros, publicar suas atualizações para o seu ponto de atualização de software e, em seguida, implementá-las para os clientes. 

Os seguinte catálogos de atualizações de software de terceiros estão disponíveis nesta versão:

 | Fabricante | O nome do catálogo |
 |--------|---------------------|
 | HP | Catálogo de atualizações de cliente HP |

SCUP continua a suportar a outros catálogos e cenários. A lista de catálogos no nó de catálogos de atualizações de Software de terceiros da consola do Configuration Manager é dinâmica e será atualizada como catálogos adicionais estão disponíveis e suportam.


### <a name="prerequisites"></a>Pré-requisitos
- Configurar o software de gestão de atualizações de, com um ponto de atualização de software ativado para HTTPS. Para obter mais informações, consulte [gestão de atualizações de preparação para a software](/sccm/sum/get-started/prepare-for-software-updates-management).  
  - O ponto de atualização de software tem de ser no servidor do site para esta funcionalidade nesta versão. <!--515810--> 

    > [!Tip]  
    > O ponto de atualização de software requer o HTTPS, porque é um requisito para as APIs do WSUS usado para lidar com certificados de assinatura. Os clientes não precisam de ser ativado para HTTPS também. Para obter mais informações sobre como ativar o HTTPS no WSUS, consulte os artigos seguintes para obter assistência:  
    > - [WSUS seguro com o protocolo Secure Sockets Layer](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) 
    > - [Mensagem de blogue de suporte do WSUS](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- Ponto de espaço em disco suficiente sobre a atualização de software, pasta WSUSContent, para armazenar o conteúdo do binário de origem para atualizações de software de terceiros. A quantidade de armazenamento necessário varia consoante o fornecedor, os tipos de atualizações e atualizações específicas que publicar para a implementação. Se precisar de mover a pasta WSUSContent para outra unidade com mais espaço livre, consulte a mensagem de blogue da equipa de suporte do WSUS [como alterar a localização onde o WSUS armazena as atualizações localmente](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).  

- Ativar e implementar a definição de cliente [ativar as atualizações de software de terceiros](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates) no **atualizações de Software** grupo.  

- O servidor de site requer acesso à internet para download.microsoft.com através da porta HTTPS 443. O serviço de sincronização de atualização de software de terceiros atualmente é executado no servidor do site. Este serviço atualiza a lista de catálogos de terceiros disponíveis, transfere os catálogos quando subscrever e transfere as atualizações quando publicado. Configurar definições de proxy de internet, se necessário, sobre o **Proxy** guia das propriedades de função do sistema de sites do computador do servidor do site.  


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Ativar e configurar a funcionalidade
Execute os passos seguintes *uma vez por hierarquia* para ativar e configurar a funcionalidade para uso:  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nó.  

2. Selecione o site de nível superior na hierarquia. No Friso, clique em **configurar componentes do Site**e selecione **ponto de atualização de Software**.  

3. Mude para o **atualizações de terceiros** separador. Selecione a opção para **ativar atualizações de software de terceiros**. Para obter mais informações sobre as opções de certificado, consulte [suporte de atualização de melhorias para ativar o software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Se utilizar a opção predefinida para o Configuration Manager para gerir este certificado, um novo certificado do tipo **de terceiros de assinatura de WSUS** é criado na **certificados** no nó  **Segurança** no **administração** área de trabalho.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Subscrever um catálogo de terceiros e sincronização de atualizações
Execute os seguintes passos para *cada catálogo de terceiros* para que quisesse se inscrever:  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **catálogos de atualizações de Software de terceiros** nó.  

2. Selecione o catálogo para subscrever e clique em **subscrever catálogo** na faixa de opções.   

3. Rever e aprovar o certificado de catálogo.  

   > [!Note]  
   > Ao subscrever um catálogo de atualização de software de terceiros, o certificado que rever e aprovar no assistente é adicionado ao site. Este certificado é do tipo **catálogo de atualizações de Software de terceiros**. Pode gerenciá-lo a partir do **certificados** no nó **segurança** no **administração** área de trabalho.  

4. Conclua o assistente.  

   > [!Tip]  
   > Depois da subscrição inicial, o catálogo deve começar imediatamente a transferir. Ele, em seguida, sincroniza novamente a cada 24 horas nesta versão. Se não quiser aguardar que o catálogo para automaticamente baixar, clique em **sincronizar agora** na faixa de opções.  
   > 
   > Depois do catálogo é transferido, têm de ser sincronizados os metadados de produto para o ponto de atualização de software. Para obter mais informações sobre este processo, bem como para iniciar manualmente, consulte [sincronizar as atualizações de software](/sccm/sum/get-started/synchronize-software-updates). Neste ponto, pode ver as atualizações de terceiros a **todas as atualizações** nó. 

5. Em seguida, configure o ponto de atualização de software **produtos** para o catálogo de terceiros para o qual inscrito. Para obter mais informações, consulte [configurar classificações e produtos para sincronizar](/sccm/sum/get-started/configure-classifications-and-products). Depois das alterações de critérios de produto, sincronização de atualizações de software tem de ocorrer novamente.

Antes de pode ver os resultados de compatibilidade de clientes, eles precisam para analisar e avaliar as atualizações. Já pode acionar manualmente este ciclo do painel de controlo do Configuration Manager num cliente ao executar o **atualizações de Software de análise ciclo** ação. Para obter mais informações sobre o processo, consulte [introdução de atualizações de Software](/sccm/sum/understand/software-updates-introduction).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: Implementar atualizações de software de terceiros
Execute os seguintes passos para *quaisquer atualizações de software de terceiros* que pretende implementar em clientes:  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **todas as atualizações de Software** nó.  

   > [!Tip]  
   > Clique em **adicionar critérios** para filtrar a lista de atualizações. Por exemplo, adicione **fornecedor** para **Adobe Systems, Inc.** para ver todas as atualizações da Adobe.  

2. Selecione as atualizações que são solicitadas pelos clientes. Clique em **publicar de terceiros Software Update conteúdo** e reveja o progresso no SMS_ISVUPDATES_SYNCAGENT.log. Esta ação transfere os binários de atualização do fornecedor e armazena-os na pasta WSUSContent no ponto de atualização de software. Também altera o estado da atualização de apenas de metadados para com conteúdo e implantável.  

   > [!Note]  
   > Quando publica conteúdos de atualização de software de terceiros, são adicionados todos os certificados utilizados para assinar o conteúdo para o site. Estes certificados são do tipo **atualizações de Software de terceiros conteúdo**. Pode geri-los a partir do **certificados** no nó **segurança** no **administração** área de trabalho.  

3. Implemente as atualizações com o processo de gerenciamento de atualizações de software existente. Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates). Sobre o **transferir localizações** página do Assistente de atualizações de Software de implementação, selecione a opção padrão para **transferir atualizações de software a partir da internet**. Neste cenário, o conteúdo já está publicado para o ponto de atualização de software, o que é utilizado para transferir o conteúdo para o pacote de implementação.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorizar o progresso das atualizações de software de terceiros
Sincronização de atualizações de software de terceiros é processada pelo componente SMS_ISVUPDATES_SYNCAGENT no servidor do site. Pode ver mensagens de estado este componente, ou ver mais detalhadas de estado no SMS_ISVUPDATES_SYNCAGENT.log. Este registo é no servidor do site no **registos** subpasta do diretório de instalação do site. Por predefinição este caminho é `C:\Program Files\Microsoft Configuration Manager\Logs`. Para obter mais informações sobre como monitorizar o processo de gestão de atualizações de software geral, consulte [monitorizar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


### <a name="known-issues"></a>Problemas conhecidos
- O serviço de sincronização de atualização de software de terceiros não suporta o ponto de atualização de software configurado para utilizar um **conta de ligação do servidor WSUS**. Se esta conta está configurada no **definições de conta de Proxy e** separador da atualização de Software ponto a página de propriedades, verá o erro seguinte no SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Para obter mais informações sobre esta conta, consulte [conta de ligação de ponto de atualização de Software](/sccm/core/plan-design/hierarchy/accounts#software-update-point-connection-account).<!--515492-->  

- Não misture o uso de outras ferramentas, como SCUP com esta nova funcionalidade de atualização de software de terceiros integrado. O serviço de sincronização de atualização de software de terceiros não é possível publicar conteúdo para atualizações apenas de metadados que foram adicionadas ao WSUS por outro aplicativo, ferramenta ou script, como SCUP. O **publicar conteúdo de atualização de software de terceiros** ação falhar nestas atualizações. Se precisar de implementar as atualizações de terceiros que ainda não suporta esta funcionalidade, utilize o seu processo existente na totalidade para implementar essas atualizações.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar as definições do Windows Defender SmartScreen para o Microsoft Edge
<!--1353701--> Esta versão adiciona três configurações para [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) para o [política de definições de conformidade de browser Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). A política agora inclui as seguintes definições adicionais sobre o **definições de SmartScreen** página:
- **Permite ao SmartScreen**: Especifica se o Windows Defender SmartScreen tem permissão. Para obter mais informações, consulte a [política de browser AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Os utilizadores podem substituir a linha de comandos do SmartScreen para sites**: Especifica se os utilizadores podem substituir os avisos do filtro do Windows Defender SmartScreen sobre sites potencialmente maliciosos. Para obter mais informações, consulte a [política de browser PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Os utilizadores podem substituir a linha de comandos do SmartScreen para ficheiros**: Especifica se os utilizadores podem substituir os avisos do filtro do Windows Defender SmartScreen sobre transferir ficheiros não verificados. Para obter mais informações, consulte a [política de browser PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Política MDM de sincronização do Microsoft Intune para um dispositivo cogerido
<!--1357377--> A partir desta versão quando [mudar de uma carga de trabalho de cogestão](/sccm/core/clients/manage/co-management-switch-workloads), os dispositivos cogeridos sincronizar automaticamente a política MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação de notificações do cliente na consola do Configuration Manager. Para obter mais informações, consulte [iniciar a obtenção de política de cliente com a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Carga de trabalho de transição do Office 365 para o Intune através de cogestão
<!--1357841--> Pode realizar a transição do Office 365 carga de trabalho do Configuration Manager para o Microsoft Intune depois de ativar a cogestão. Para fazer a transição esta carga de trabalho, vá para a página de propriedades de cogestão e mova a barra de controlo de deslize do Configuration Manager para piloto ou todos. Para obter mais informações, consulte [cogestão para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).

Também existe uma nova condição global **aplicações do Office 365 são geridas pelo Intune no dispositivo**. Esta condição é adicionada por padrão, como um requisito para novos aplicativos do Office 365. Faça a transição esta carga de trabalho, clientes cogeridos não cumpre o requisito no aplicativo, assim, a não instalar o Office 365 implementado através do Configuration Manager.

### <a name="known-issue"></a>Problema conhecido
- Esta transição da carga de trabalho atualmente só se aplica às implementações do Office 365. O Configuration Manager continua a gerir atualizações do Office 365.<!--510876--> Para obter mais informações, incluindo uma solução, consulte o 1802 de versão do Configuration Manager nota de versão [definição de cliente do Office 365 a alteração não se aplica](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply).



## <a name="package-conversion-manager"></a>Gestor de conversão de pacotes 
<!--1357861--> Gestor de conversão de pacotes agora é uma ferramenta integrada que lhe permite converter pacotes do Configuration Manager 2007 herdados para o Configuration Manager aplicativos do ramo atual. Em seguida, pode utilizar funcionalidades de aplicativos, como dependências, regras de requisitos e afinidade dispositivo / utilizador.

> [!Tip]  
> Documentação herdada para a funcionalidade existente no Gestor de conversão de pacotes está disponível no [TechNet](https://technet.microsoft.com/library/hh531519.aspx). As informações relevantes estão em curso para migrar para a biblioteca do docs.microsoft.com.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

> [!Important]  
> Se instalou anteriormente uma versão mais antiga do Gestor de conversão de pacotes, primeiro desinstalá-lo antes de atualizar o seu site. A nova versão integrada não requer a instalação, mas poderá entrar em conflito com as versões existentes.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **gestão de aplicações** e selecione **pacotes**.  
2. Selecione um pacote. As três opções seguintes estão disponíveis no **conversão de pacote** grupo da faixa de opções:  
     - **Analisar pacote**: Inicie o processo de conversão ao analisar o pacote.
     - **Converter pacote**: Alguns pacotes podem ser facilmente convertidas em aplicações com esta ação.
     - **Corrigir e converter**: Alguns pacotes requerem problemas corrigidos antes de converter em aplicações.  

   Para obter mais informações sobre estas ações, consulte [como analisar e converter pacotes](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Vá para o **monitorização** área de trabalho e selecione **estado de conversão de pacote**. Este novo dashboard mostra o estado geral de análise e conversão de pacotes no site. Uma nova tarefa em segundo plano automaticamente resume os dados de análise.  

   > [!Tip]  
   > Gestor de conversão de pacotes não exige que agendar uma análise de pacotes. Esta ação é agora processada pela tarefa de resumo integrada.  

![Dashboard de captura de ecrã do Estado de conversão do pacote](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Implementar atualizações de software sem conteúdo
<!--1357933--> Agora pode implementar atualizações de software em dispositivos sem primeiro download e a distribuição de conteúdo de atualização de software para pontos de distribuição. Esta funcionalidade é benéfica ao lidar com conteúdo da atualização extremamente grandes ou quando pretender que sempre clientes a obter o conteúdo do serviço de nuvem do Microsoft Update. Os clientes neste cenário também podem transferir o conteúdo de elementos que já tenham o conteúdo necessário. O cliente continua a gerir a transferência do conteúdo, o Configuration Manager, portanto, pode utilizar a funcionalidade de cache ponto a ponto do Configuration Manager ou outras tecnologias, como a Otimização da entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Configuration Manager, incluindo o Windows e atualizações do Office. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Inicie uma implementação de atualização de software por normal. Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).
2. No Assistente de atualizações de Software de implementação, sobre o **pacote de implementação** página, selecione a nova opção para **nenhum pacote de implementação**.

### <a name="known-issues"></a>Problemas conhecidos
- O ícone de atualização implementado com incorretamente esta definição é apresentada com um X vermelho como se a atualização é inválida. Para obter mais informações, consulte [ícones utilizados para atualizações de software](/sccm/sum/understand/software-updates-icons). <!--515556-->  
- Esta definição só está integrada com o Assistente para implementar atualizações de Software. Não é atualmente disponível com regras de implementação automática. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração de ferramenta de personalização do Office com o instalador do Office 365
<!--1358149--> A ferramenta de personalização do Office está agora integrada com o instalador do Office 365 na consola do Configuration Manager. Ao criar uma implementação para o Office 365, pode agora configurar de forma dinâmica as definições de capacidade de gestão mais recentes do Office. A ferramenta de personalização do Office é atualizada ao mesmo tempo que o lançamento de novas compilações do Office 365. Pode agora tirar partido das novas definições de capacidade de gerenciamento no Office 365, assim que estiverem disponíveis. 

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola do Configuration Manager tem acesso à internet por meio da porta HTTPS 443. O Assistente de instalação de cliente do Office 365 utiliza um navegador da web padrão Windows API para abrir https://config.office.com. Se for utilizado um proxy de internet, o utilizador tem de ser capaz de aceder a este URL.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho e selecione o **gestão de clientes do Office 365** nó.
2. Clique nas **Office 365 instalador** peça de mosaico no dashboard para iniciar o Assistente de instalação de cliente do Office 365. Para obter mais informações, consulte [aplicações do Office 365/implementar](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).
3. Sobre o **definição do Office** página, clique em **Ir para página de Web do Office**. Utilize a ferramenta de personalização do Office online para especificar definições para esta implementação. 
4. Clique em **submeter** no canto superior direito quando terminar. Conclua o Assistente de instalação de cliente do Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Melhorias para a cloud do gateway de gestão
Esta versão inclui as seguintes melhorias para o gateway de gestão da cloud (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de arranque de configuração simplificada do cliente
<!--1358215--> Ao instalar o cliente do Configuration Manager na internet através de um CMG, menos propriedades da linha de comandos são agora necessária. Para obter mais informações sobre um exemplo deste cenário, consulte a [linha de comando para instalar o cliente do Configuration Manager](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) ao se preparar para a cogestão. 

As seguintes propriedades de linha de comandos são necessários em todos os cenários:
  - CCMHOSTNAME  
  - SMSSITECODE  

As seguintes propriedades são necessárias quando utilizar o Azure AD para autenticação de cliente em vez de certificados de autenticação de clientes baseada na PKI:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

A propriedade seguinte é necessária se o cliente forem se mover para a intranet:
  - SMSMP  

O exemplo seguinte inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="download-content-from-a-cmg"></a>Transferir conteúdo de um CMG
<!--1358651--> Anteriormente, era necessário implementar um ponto de distribuição de nuvem e CMG como funções separadas. Agora nesta versão, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para ativar esta funcionalidade, ative a nova opção para **permitir CMG para funcionar como um ponto de distribuição de nuvem e servir conteúdo a partir de armazenamento do Azure** sobre o **definições** guia das propriedades do CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Certificado de raiz fidedigna não é necessário com o Azure AD
<!--503899--> Quando cria um CMG, já não tem de fornecer um [certificado de raiz fidedigna](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) na página Definições. Este certificado não necessárias ao utilizar o Azure Active Directory (Azure AD) para autenticação de cliente, mas utilizado para ser necessário no assistente.

> [!Important]  
> Se estiver a utilizar certificados de autenticação de cliente PKI, em seguida, ainda tem de adicionar um certificado de raiz fidedigna para CMG.



## <a name="improvements-to-secure-client-communications"></a>Melhorias para proteger as comunicações de cliente
<!--1358278,1358279--> Esta versão continua a iterar [aprimorada de comunicações de cliente seguras](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications) removendo dependências adicionais na conta de acesso de rede. Quando ativa a nova opção de site para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**, os seguintes cenários não precisam de uma conta de acesso de rede para transferir o conteúdo de um ponto de distribuição:  

- Sequências de tarefas em execução a partir do suporte de dados ou PXE
- Sequências de tarefas em execução a partir do Centro de Software  

Estas sequências de tarefas podem ser para a implementação do sistema operacional ou personalizado. Também é suportada para computadores de grupo de trabalho.



## <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura de centro de software
<!--1358309--> Funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Esta alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. Centro de software baseia-se agora no ponto de gestão para obter essa informação, que ajuda a escala de ambientes de maior melhor ao atribuir-lhes [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Remova todas as funções de catálogo de aplicações a partir do site. Estas funções incluem o ponto de serviço da web de catálogo de aplicações e o ponto de Web site do catálogo de aplicações.
2. Implemente uma aplicação como disponível para uma coleção de utilizadores.
3. Utilize o Centro de Software como um utilizador visado para procurar, solicitar e instalar a aplicação.

### <a name="known-issue"></a>Problema conhecido
- Se utilizar um cliente associado ao Azure Active Directory com esta funcionalidade, não configure o site para **sistemas de sites de certificados gerados de utilizar o Configuration Manager para HTTP**. Está em conflito atualmente com esta funcionalidade.<!--515846--> Para obter mais informações sobre esta definição, consulte [aprimorada de comunicações de cliente seguras](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Aprovisionar os pacotes de aplicações do Windows para todos os utilizadores num dispositivo
<!--1358310--> Agora, pode aprovisionar uma aplicação com um pacote de aplicação do Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é aprovisionar uma aplicação a partir da Microsoft Store para empresas e educação, como o Minecraft: Edição de educação, para todos os dispositivos utilizados pelos alunos de uma instituição de ensino. Anteriormente, o Configuration Manager apenas suportada a instalar estas aplicações por utilizador. Depois de iniciar sessão para um novo dispositivo, um estudante teria de espera para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada no dispositivo para todos os utilizadores, eles podem ser produtivos mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, aprovisionamento e a atualizar versões diferentes do mesmo pacote de aplicação do Windows num dispositivo, que poderá provocar resultados inesperados. Esse comportamento pode ocorrer ao utilizar o Gestor de configuração para aprovisionar a aplicação, mas, em seguida, permitindo que os usuários atualizar a aplicação a partir da Microsoft Store. Para obter mais informações, consulte a documentação de orientação passo seguinte quando [gerir aplicações a partir da Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Quando aprovisionar uma aplicação com licença offline, o Configuration Manager não permite Windows automaticamente atualizá-la a partir da Microsoft Store.  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Crie uma nova aplicação. Esta aplicação tem de ter entre um pacote de aplicação do Windows ou uma aplicação licenciadas offline, o que já sincronizadas a partir da Microsoft Store para empresas e educação.  

2. Sobre o **informações gerais** página do Assistente para criar aplicação, ative a opção para **aprovisionar esta aplicação para todos os utilizadores no dispositivo**.  

   > [!Tip]  
   > Se pretender modificar uma aplicação existente, esta definição é sobre o **experiência de utilizador** separador das propriedades da aplicação.  

3. Implemente a aplicação para uma coleção de dispositivos.  

4. Inicie sessão para um dispositivo de destino com diferentes contas de usuário e iniciar o aplicativo.  

> [!Note]  
> Se precisar de desinstalar uma aplicação de aprovisionamento de dispositivos nas quais os utilizadores já tem iniciado sessão, tem de criar duas implementações de desinstalação. Destino a primeira implementação para uma coleção de dispositivos que contenha os dispositivos da desinstalação. O segundo de destino a implementação para uma coleção de utilizadores que contém os utilizadores que já tem sessão iniciada dispositivos com o aplicativo aprovisionado da desinstalação. Quando desinstalar uma aplicação aprovisionada num dispositivo, Windows atualmente não desinstale essa aplicação para os utilizadores também. 



## <a name="improvements-to-the-surface-dashboard"></a>Aprimoramentos no painel do Surface
<!--1358654--> Esta versão inclui as seguintes melhorias para o [painel do Surface](/sccm/core/clients/manage/surface-device-dashboard):
- O painel do Surface apresenta agora uma lista de dispositivos relevantes quando as secções do gráfico estão selecionadas.
   - Clicar no **por cento de dispositivos Surface** mosaico abre-se uma lista de dispositivos Surface.
   - Clicar numa barra no **principais cinco versões de Firmware** mosaico abre-se uma lista de dispositivos Surface com essa versão de firmware específico.
- Ao visualizar estas listas de dispositivo a partir do painel do Surface, pode um dispositivo com o botão direito e efetuar ações comuns.



## <a name="hardware-inventory-default-unit-revision"></a>Revisão de unidade de padrão de inventário de hardware
<!--514442--> Na [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), a unidade de padrão utilizada nas vistas de geração de relatórios muitos mudou de megabytes (MB) a gigabytes (GB). Devido a [melhorias ao inventário de hardware para valores inteiros grandes](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values), e com base nos comentários dos clientes, esta unidade padrão é agora MB novamente.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
