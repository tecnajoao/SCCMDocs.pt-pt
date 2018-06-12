---
title: Pré-visualização técnica 1806
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades disponíveis na versão 1806 Configuration Manager Technical Preview.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4933e4e6d9037edd01d80c9535627287275f7462
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814302"
---
# <a name="capabilities-in-technical-preview-1806-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1806 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview para o Configuration Manager, versão 1806. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica. 

Reveja o [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos nesta pré-visualização técnica

### <a name="ki_contentlib"></a> Site não conseguir atualizar com biblioteca de conteúdos remota
<!--514642-->
O site não consegue atualizar com os seguintes erros no **cmupdate.log**:  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Este problema ocorre nesta versão, quando a biblioteca de conteúdos numa localização remota.

#### <a name="workaround"></a>Solução
Mova a biblioteca de conteúdos para uma unidade local para o servidor do site. Para obter mais informações, consulte [configurar uma biblioteca de conteúdos remota para o servidor de site](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server). 



</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



## <a name="bkmk-3pupdate"></a> Atualizações de software de terceiros
<!--1352101-->
Esta versão ainda mais itera sobre o suporte para atualizações de software de terceiros, como resultado de sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Já não requerem a utilização do System Center atualizações publicador (SCUP) para alguns cenários comuns. A nova **catálogos de atualização de Software de terceiros** nó na consola do Configuration Manager permite-lhe subscrever catálogos de terceiros, publicar as atualizações para o ponto de atualização de software e, em seguida, implementá-las para os clientes. 

Os seguinte catálogos de atualização de software de terceiros estão disponíveis nesta versão:
 | Fabricante | Nome do catálogo |
 |--------|---------------------|
 | HP | Catálogo de atualizações de cliente do HP |

SCUP continua a suportar outros cenários e catálogos. A lista de catálogos no nó de catálogos de atualização de Software de terceiros da consola do Configuration Manager for dinâmica e será atualizada conforme catálogos adicionais estão disponíveis e suportam.


### <a name="prerequisites"></a>Pré-requisitos
- Configurar o software de atualizações de gestão, com um ponto de atualização de software ativadas por HTTPS. Para obter mais informações, consulte [preparar para o software de gestão de atualizações](/sccm/sum/get-started/prepare-for-software-updates-management).  
   - O ponto de atualização de software tem de ser no servidor do site para esta funcionalidade nesta versão. <!--515810--> 

- Ponto de espaço em disco suficiente na atualização de software, pasta WSUSContent, para armazenar o conteúdo do binário de origem para atualizações de software de terceiros. A quantidade de armazenamento necessário varia consoante o fornecedor, os tipos de atualizações e atualizações específicas que publicar para a implementação. Se precisar de mover a pasta WSUSContent para outra unidade com mais espaço livre, consulte a mensagem de blogue da equipa de suporte do WSUS [como alterar a localização onde o WSUS armazena as atualizações localmente](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).  

- Ativar e implementar a definição de cliente [ativar atualizações de software de terceiros](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates) no **atualizações de Software** grupo.  

- O servidor de site requer acesso à internet para download.microsoft.com através da porta HTTPS 443. O serviço de sincronização de atualização de software de terceiros atualmente é executado no servidor do site. Este serviço atualiza a lista de catálogos de terceiros disponíveis, transfere os catálogos quando subscrever e transfere as atualizações quando publicado. Configurar definições de proxy de internet, se necessário, no **Proxy** separador das propriedades da função de sistema de sites do computador do servidor do site.  


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Ativar e configurar a funcionalidade
Execute os seguintes passos *uma vez por hierarquia* para ativar e configurar a funcionalidade para ser utilizado:  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nós.  

2. Selecione o site de nível superior na hierarquia. No Friso, clique em **configurar componentes do Site**e selecione **ponto de atualização de Software**.  

3. Mudar para o **atualizações de terceiros** separador. Selecione a opção para **ativar atualizações de software de terceiros**. Para obter mais informações sobre as opções de certificado, consulte [melhoramentos para ativar o software de terceiros atualizar suporte](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Se utilizar a opção predefinida para o Configuration Manager para gerir este certificado, um novo certificado do tipo **terceiros WSUS assinatura** é criado no **certificados** nó  **Segurança** no **administração** área de trabalho.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Subscrever um catálogo de terceiros e sincronização de atualizações
Execute os seguintes passos para *cada catálogo de terceiros* para que pretende subscrever:  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **catálogos de atualização de Software de terceiros** nós.  

2. Selecione o catálogo para subscrever e clique em **subscrever catálogo** no Friso.   

3. Reveja e aprove o certificado de catálogo.  

   > [!Note]  
   > Ao subscrever um catálogo de atualização de software de terceiros, o certificado que rever e aprovar no assistente é adicionado ao site. Este certificado é do tipo **catálogo de atualizações de Software de terceiros**. Pode gerir ao **certificados** nó **segurança** no **administração** área de trabalho.  

4. Conclua o assistente.  

   > [!Tip]  
   > Após a subscrição inicial, o catálogo deve começar imediatamente a transferir. -Resyncs, em seguida, a cada 24 horas nesta versão. Se não pretender aguardar que o catálogo automaticamente transferir, clique em **sincronizar agora** no Friso.  
   > 
   > Depois do catálogo é transferido, têm de ser sincronizados os metadados de produto para o ponto de atualização de software. Para obter mais informações sobre este processo, bem como para iniciar manualmente, consulte o artigo [sincronizar atualizações de software](/sccm/sum/get-started/synchronize-software-updates). Neste momento, pode ver as atualizações de terceiros a **todas as atualizações** nós. 

5. Em seguida, configure o ponto de atualização de software **produtos** para o catálogo de terceiros para o qual subscrito. Para obter mais informações, consulte [configurar classificações e produtos para sincronizar](/sccm/sum/get-started/configure-classifications-and-products). Depois das alterações de critérios de produto, sincronização de atualizações de software tem de ocorrer novamente.

Antes de poder ver os resultados de compatibilidade de clientes, que precisam de analisar e avaliar as atualizações. Pode acionar este ciclo do painel de controlo do Configuration Manager num cliente manualmente executando o **Software atualizações analisar ciclo** ação. Para obter mais informações sobre o processo, consulte [introdução de atualizações de Software](/sccm/sum/understand/software-updates-introduction).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Passo 3: Implementar atualizações de software de terceiros
Execute os seguintes passos para *quaisquer atualizações de software de terceiros* que pretende implementar em clientes:  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **todas as atualizações de Software** nós.  

   > [!Tip]  
   > Clique em **adicionar critérios** para filtrar a lista de atualizações. Por exemplo, adicionar **fornecedor** para **Adobe Systems, Inc.** para ver todas as atualizações do Adobe.  

2. Selecione as atualizações que são necessárias por parte dos clientes. Clique em **publicar independente Software conteúdo de atualização** e rever o progresso no SMS_ISVUPDATES_SYNCAGENT.log. Esta ação transfere os binários da atualização do fornecedor e armazena-os na pasta WSUSContent no ponto de atualização de software. Também altera o estado da atualização de apenas de metadados para com o conteúdo e implementável.  

   > [!Note]  
   > Quando publica os conteúdos de atualização de software de terceiros, todos os certificados utilizados para assinar o conteúdo são adicionados ao site. Estes certificados são do tipo **conteúdo de atualizações de Software do terceiros**. Pode geri-los do **certificados** nó **segurança** no **administração** área de trabalho.  

3. Implemente as atualizações utilizando o processo de gestão de atualizações de software existente. Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates). No **transferir localizações** página do Assistente de atualização de Software implementar, selecione a opção predefinida para **transferir atualizações de software a partir da internet**. Neste cenário, o conteúdo já está publicado para o ponto de atualização de software, o que é utilizado para transferir o conteúdo para o pacote de implementação.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorizar o progresso das atualizações de software de terceiros
A sincronização de atualizações de software de terceiros é processada pelo componente SMS_ISVUPDATES_SYNCAGENT no servidor do site. Pode ver mensagens de estado deste componente ou ver mais detalhadas de estado no SMS_ISVUPDATES_SYNCAGENT.log. Este registo é no servidor do site no **registos** subpasta do diretório de instalação do site. Por predefinição este caminho é `C:\Program Files\Microsoft Configuration Manager\Logs`. Para obter mais informações sobre como monitorizar o processo de gestão de atualizações de software geral, consulte [monitorizar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


### <a name="known-issues"></a>Problemas conhecidos
- O serviço de sincronização de atualização de software de terceiros não suporta o ponto de atualização de software configurado para utilizar um **conta de ligação do servidor WSUS**. Se esta conta está configurada no **definições de conta de Proxy e** separador página de propriedades do ponto de atualização de Software, verá o erro seguinte no SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Para obter mais informações sobre esta conta, consulte [conta de ligação de ponto de atualização de Software](/sccm/core/plan-design/hierarchy/accounts#software-update-point-connection-account).<!--515492-->  

- Não misture a utilização de outras ferramentas, como SCUP com esta nova funcionalidade de atualização de software de terceiros integrado. O serviço de sincronização de atualização de software de terceiros não é possível publicar conteúdo apenas de metadados de atualizações que foram adicionadas ao WSUS por outra aplicação, ferramenta ou script, como SCUP. O **publicar conteúdo de atualização de software de terceiros** ação falhar nestas atualizações. Se precisar de implementar as atualizações de terceiros que ainda não suporta esta funcionalidade, utilize o processo existente no completo para implementar essas atualizações.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar as definições do Windows Defender SmartScreen para Microsoft Edge
<!--1353701-->
Esta versão adiciona três definições para [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) para o [política de definições de compatibilidade de browser Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). A política agora inclui as seguintes definições adicionais no **SmartScreen definições** página:
- **Permite ao SmartScreen**: Especifica se o Windows Defender SmartScreen é permitido. Para obter mais informações, consulte o [política de browser AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Os utilizadores podem ignorar pedido de SmartScreen para sites**: Especifica se os utilizadores podem substituir os avisos do Filtro SmartScreen do Windows Defender sobre sites potencialmente maliciosos. Para obter mais informações, consulte o [política de browser PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Os utilizadores podem ignorar pedido de SmartScreen para ficheiros**: Especifica se os utilizadores podem substituir os avisos do Filtro SmartScreen do Windows Defender sobre a transferência de ficheiros não verificados. Para obter mais informações, consulte o [política de browser PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Política MDM de sincronização do Microsoft Intune para um dispositivo gerido conjuntamente
<!--1357377-->
Isto partir da versão quando [mudar de uma carga de trabalho de gestão conjunta](/sccm/core/clients/manage/co-management-switch-workloads), os dispositivos geridos conjuntamente sincronizar automaticamente políticas MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação de notificações do cliente na consola do Configuration Manager. Para obter mais informações, consulte [iniciar a obtenção de política de cliente utilizando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Transição do Office 365 carga de trabalho utilizando a gestão de coadministrador do Intune
<!--1357841-->
Pode agora efetuar a transição do Office 365 carga de trabalho do Configuration Manager para o Microsoft Intune depois de ativar a gestão conjunta. A transição esta carga de trabalho, vá para a página de propriedades de gestão conjunta e desloque o cursor de controlo do Configuration Manager piloto ou todos os. Para obter mais informações, consulte [conjunta management para Windows 10 dispositivos](/sccm/core/clients/manage/co-management-overview).

Também é uma nova condição global, **aplicações do Office 365 são geridas pelo Intune no dispositivo**. Esta condição é adicionada por predefinição como um requisito para novas aplicações do Office 365. Quando efetuar a transição esta carga de trabalho, clientes conjuntamente geridos não cumpre o requisito da aplicação, assim, não instale do Office 365 implementado através do Configuration Manager.

### <a name="known-issue"></a>Problema conhecido
- Esta transição de carga de trabalho atualmente só se aplica às implementações do Office 365. O Configuration Manager continua a gerir atualizações do Office 365.<!--510876--> Para obter mais informações, incluindo uma solução possíveis, consulte o artigo 1802 de versão do Configuration Manager versão nota [não aplica a definição de cliente do Office 365 alterar](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply).



## <a name="package-conversion-manager"></a>Gestor de conversão de pacotes 
<!--1357861-->
Gestor de conversão de pacotes agora é uma ferramenta integrada que lhe permite converter pacotes legados do Configuration Manager 2007 para o Configuration Manager que as aplicações de sucursais atuais. Em seguida, pode utilizar funcionalidades das aplicações, tais como dependências, regras de requisitos e afinidade dispositivo / utilizador.

> [!Tip]  
> Documentação legada para a funcionalidade existente no Gestor de conversão de pacotes está disponível no [TechNet](https://technet.microsoft.com/library/hh531519.aspx). Informações relevantes estão no processo de migrar para a biblioteca de docs.microsoft.com.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

> [!Important]  
> Se instalou anteriormente uma versão mais antiga do Gestor de conversão de pacotes, primeiro desinstale antes de atualizar o seu site. A nova versão integrada não requer a instalação, mas poderá entrar em conflito com versões existentes.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **gestão de aplicações** e selecione **pacotes**.  
2. Selecione um pacote. As três opções seguintes estão disponíveis no **conversão de pacote** do Friso:  
     - **Analisar pacote**: Inicie o processo de conversão ao analisar o pacote.
     - **Converter pacote**: Alguns pacotes podem facilmente ser convertidos em aplicações com esta ação.
     - **Corrigir e converter**: Alguns pacotes necessitam de problemas para ser corrigidos antes de converter em aplicações.  

   Para obter mais informações sobre estas ações, consulte [como analisar e converter pacotes](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Vá para o **monitorização** área de trabalho e selecione **estado de conversão de pacote**. Este novo dashboard mostra o estado geral de análise e conversão de pacotes no site. Uma nova tarefa em segundo plano automaticamente resume os dados de Analysis Services.  

   > [!Tip]  
   > Gestor de conversão de pacotes não requerem a agendar análises ou pacotes. Agora, esta ação é processada pela tarefa de resumo integrada.  

![Dashboard de captura de ecrã do Estado de conversão do pacote](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Implementar atualizações de software sem conteúdo
<!--1357933-->
Agora pode implementar atualizações de software em dispositivos sem primeiro a transferir e a distribuição de conteúdo de atualização de software para pontos de distribuição. Esta funcionalidade é vantajoso ao lidar com o conteúdo da atualização extremamente grandes ou quando pretender que sempre clientes ao obter o conteúdo do serviço de nuvem do Microsoft Update. Os clientes neste cenário também podem transferir o conteúdo de elementos de rede que já tenham o conteúdo necessário. O Gestor de configuração de cliente continua a gerir a transferência do conteúdo, deste modo, pode utilizar a funcionalidade de cache ponto a ponto do Configuration Manager ou outras tecnologias, como a otimização de entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Configuration Manager, incluindo o Windows e atualizações do Office. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Inicie uma implementação de atualização de software por normal. Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).
2. No Assistente de atualizações de Software implementar, no **pacote de implementação** página, selecione a opção nova para **nenhum pacote de implementação**.

### <a name="known-issues"></a>Problemas conhecidos
- O ícone de atualização implementado com esta definição incorretamente apresentada com um X vermelho como se a atualização é inválida. Para obter mais informações, consulte [ícones utilizados para atualizações de software](/sccm/sum/understand/software-updates-icons). <!--515556-->  
- Esta definição só está integrada com o Assistente para implementar atualizações de Software. Não se encontra atualmente disponível com regras de implementação automática. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração de ferramenta de personalização do Office com o instalador do Office 365
<!--1358149-->
A ferramenta de personalização do Office agora está integrada com o programa de instalação do Office 365 na consola do Configuration Manager. Ao criar uma implementação para o Office 365, pode agora dinamicamente configurar as definições de capacidade de gestão mais recentes do Office. A ferramenta de personalização do Office é atualizada ao mesmo tempo que a versão do novo compilações do Office 365. Agora, pode tirar partido de novas definições de capacidade de gestão do Office 365, assim que estiverem disponíveis. 

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola do Configuration Manager necessita de acesso à internet através de porta HTTPS 443. O Assistente de instalação de cliente do Office 365 utiliza um Windows padrão browser API para abrir https://config.office.com. Se for utilizado um proxy de internet, o utilizador tem de ser capaz de aceder este URL.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho e selecione o **gestão de clientes do Office 365** nós.
2. Clique em de **instalador do Office 365** mosaico no dashboard para iniciar o Assistente de instalação de cliente do Office 365. Para obter mais informações, consulte [aplicações de implementar o Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).
3. No **Office definição** página, clique em **vá para o Office Web página**. Utilize a ferramenta de personalização do Office online para especificar definições para esta implementação. 
4. Clique em **submeter** no canto superior direito quando terminar. Conclua o Assistente de instalação de cliente do Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Melhoramentos ao gateway de gestão de nuvem
Esta versão inclui os seguintes melhoramentos para o gateway de gestão de nuvem (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Linha de comandos de arranque do sistema cliente simplificada
<!--1358215-->
Ao instalar o cliente do Configuration Manager na internet através de um CMG, menos propriedades da linha de comandos são agora necessárias. Para obter mais informações sobre um exemplo deste cenário, consulte o [linha de comandos para instalar o cliente do Configuration Manager](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) quando preparar para o management conjunta. 

São necessárias as seguintes propriedades da linha de comandos em todos os cenários:
  - CCMHOSTNAME  
  - SMSSITECODE  

As seguintes propriedades são necessárias quando utilizar o Azure AD para autenticação de cliente em vez de certificados de autenticação de clientes baseada na PKI:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

A seguinte propriedade é necessária se o cliente irá se movem para voltar à intranet:
  - SMSMP  

O exemplo seguinte inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [as propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="download-content-from-a-cmg"></a>Transferir conteúdo de um CMG
<!--1358651-->
Anteriormente, era necessário implementar um ponto de distribuição de nuvem e CMG como funções separadas. Agora nesta versão, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo de VMs do Azure. Para ativar esta funcionalidade, ative a nova opção **permitir CMG para funcionar como um ponto de distribuição de nuvem e a servir conteúdo do armazenamento do Azure** no **definições** separador das propriedades da CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Certificado de raiz fidedigna não é necessário com o Azure AD
<!--503899-->
Quando cria um CMG, está a já não é necessário fornecer um [certificado de raiz fidedigna](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) na página de definições. Este certificado não é necessário quando utilizar o Azure Active Directory (Azure AD) para autenticação de cliente, mas utilizado para ser necessário no assistente.

> [!Important]  
> Se estiver a utilizar certificados de autenticação de cliente PKI, em seguida, ainda tem de adicionar um certificado de raiz fidedigna para o CMG.



## <a name="improvements-to-secure-client-communications"></a>Melhoramentos para proteger as comunicações de cliente
<!--1358278,1358279-->
Esta versão continua iterar [melhorada comunicações de cliente seguras](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications) removendo dependências adicionais na conta de acesso de rede. Quando ativa a nova opção de site para **sistemas de sites de certificados gerados-utilize o Gestor de configuração para HTTP**, os cenários seguintes não necessitam de uma conta de acesso de rede ao transferir o conteúdo a partir de um ponto de distribuição:  

- Sequências de tarefas em execução a partir do suporte de dados de arranque ou PXE
- Sequências de tarefas em execução a partir do Centro de Software  

Estas sequências de tarefas podem ser para implementação do SO ou personalizado. Também é suportada para computadores de grupo de trabalho.



## <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura de centro de software
<!--1358309-->
Funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Esta alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicações aos utilizadores. Centro de software baseia-se agora na ponto de gestão para obter estas informações, que ajuda a escala de ambientes maior melhor ao atribuir-lhes [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Remova todas as funções de catálogo de aplicações do site. Estas funções incluem o ponto de serviço web do catálogo de aplicações e o ponto de Web site do catálogo de aplicações.
2. Implemente uma aplicação disponível como uma coleção de utilizadores.
3. Utilize o Centro de Software como um utilizador direcionado para procurar, solicitar e instalar a aplicação.

### <a name="known-issue"></a>Problema conhecido
- Se utilizar um cliente associado ao Azure Active Directory com esta funcionalidade, não configure o site para **sistemas de sites de certificados gerados de utilizar o Configuration Manager para HTTP**. Está em conflito atualmente com esta funcionalidade.<!--515846--> Para obter mais informações sobre esta definição, consulte [melhorada comunicações de cliente seguras](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Aprovisionar pacotes de aplicações do Windows para todos os utilizadores num dispositivo
<!--1358310-->
Agora pode aprovisionar uma aplicação com um pacote de aplicação do Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é aprovisionamento de uma aplicação da Microsoft Store para empresas e as educação, como Minecraft: Edição de educação para todos os dispositivos utilizados pelo estudantes num profissional. Anteriormente, o Configuration Manager só suportada a instalar estas aplicações por utilizador. Depois de iniciarem sessão para um novo dispositivo, um estudante teria de espera para aceder a uma aplicação. Agora quando a aplicação é aprovisionada no dispositivo para todos os utilizadores, estes podem ser produtivos mais rapidamente.

> [!Important]  
> Seja cuidadoso com a instalação, o aprovisionamento e atualizar versões diferentes do mesmo pacote de aplicação do Windows, um dispositivo, o que poderá provocar resultados inesperados. Este comportamento pode ocorrer quando utilizar o Configuration Manager para aprovisionar a aplicação, mas, em seguida, permitindo que os utilizadores atualizar a aplicação da Microsoft Store. Para obter mais informações, consulte a documentação de orientação passo seguinte quando que [gerir aplicações a partir do Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Quando aprovisionar uma aplicação com licença offline, o Configuration Manager não permitir que o Windows automaticamente a atualização da Microsoft Store.  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Crie uma nova aplicação. Esta aplicação tem de ser de um pacote de aplicações do Windows ou uma aplicação licenciadas offline, o que tiver sincronizado da Microsoft Store para empresas e Education.  

2. No **informações gerais** página do Assistente para criar aplicação, ative a opção para **aprovisionar esta aplicação para todos os utilizadores no dispositivo**.  

   > [!Tip]  
   > Se estiver a modificar uma aplicação existente, esta definição está ativada a **experiência de utilizador** separador das propriedades da aplicação.  

3. Implemente a aplicação para uma coleção de dispositivos.  

4. Inicie sessão no dispositivo com contas de utilizador diferente e iniciar a aplicação.  

> [!Note]  
> Se precisar de desinstalar uma aplicação de aprovisionamento de dispositivos para que os utilizadores já se inscreveu no, terá de criar dois desinstalar implementações. Destino primeiro a implementação para uma coleção de dispositivos que contenha os dispositivos da desinstalação. Destino a segunda implementação para uma coleção de utilizador que contenha os utilizadores que já tenham sessão iniciada dispositivos com a aplicação de aprovisionamento da desinstalação. Quando desinstalar uma aplicação num dispositivo aprovisionada, Windows atualmente não desinstale essa aplicação para utilizadores bem. 



## <a name="improvements-to-the-surface-dashboard"></a>Melhoramentos ao dashboard superfície
<!--1358654-->
Esta versão inclui os seguintes melhoramentos para o [dashboard superfície](/sccm/core/clients/manage/surface-device-dashboard):
- O dashboard de superfície agora apresenta uma lista de dispositivos relevantes quando estão selecionadas secções de gráfico.
   - Clicar no **percentagem de dispositivos Surface** mosaico, abre-se uma lista de dispositivos superfície.
   - Clicar numa barra no **superior a cinco de versões de Firmware** mosaico abre-se uma lista de dispositivos superfície com essa versão de firmware específico.
- Ao visualizar estas listas de dispositivo a partir do dashboard superfície, pode um dispositivo com o botão direito e efetuar ações comuns.



## <a name="hardware-inventory-default-unit-revision"></a>Revisão de unidade da predefinição de inventário de hardware
<!--514442-->
No [do Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), a unidade de predefinição utilizada nas vistas de relatórios muitos mudou de megabytes (MB) para gigabytes (GB). Devido a [melhoramentos ao inventário de hardware para os valores de número inteiro grande](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values), e com base nos comentários de clientes, esta unidade predefinido é agora MB novamente.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
