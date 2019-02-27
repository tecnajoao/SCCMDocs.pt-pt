---
title: Novidades na versão 1810
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1810 do Configuration Manager current branch.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc4fb762e39680dfb9a9894bc19e929b8ff3d7ed
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838825"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>O que há de novo na versão 1810 do Configuration Manager current branch

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1810 para o ramo atual do Configuration Manager está disponível como uma atualização na consola. Aplica esta atualização de sites que executam a versão 1710, 1802 ou 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Reveja sempre a lista de verificação mais recente para instalar esta atualização. Para obter mais informações, consulte [lista de verificação para a instalação de atualização 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). Depois de atualizar um site, reveja também os [lista de verificação de pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

> [!Note]  
> Este artigo lista atualmente todas as funcionalidades significativas nesta versão. No entanto, nem todas as seções ainda uma ligação para o conteúdo atualizado com informações adicionais sobre os novos recursos. Continuar a verificar esta página regularmente a existência de atualizações. As alterações são indicadas com o ***[atualizado]*** marca. Esta nota será removida quando o conteúdo é finalizado.  

> [!Important]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.

Este artigo resume as alterações e novos recursos no Configuration Manager, versão 1810.  



## <a name="bkmk_deprecated"></a> Funcionalidades preteridas e sistemas operativos

Saiba mais sobre as alterações de suporte antes de eles são implementados no [removidas e preteridas itens](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A partir de 14 de Agosto de 2018, a funcionalidade de gestão de dispositivos móveis híbrida foi preterida. Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

Suporte para o System Center Endpoint Protection (SCEP) para Mac e Linux (todas as versões) termina a 31 de Dezembro de 2018. Disponibilidade da nova definição de vírus para o SCEP para Mac e o SCEP para Linux pode ser interrompida após o fim do suporte. Para obter mais informações, consulte [final de mensagem de blogue de suporte](https://go.microsoft.com/fwlink/?linkid=870182).

Implementações de serviço clássico no Azure estão agora preteridas no Configuration Manager. Começar a utilizar implementações do Azure Resource Manager para o gateway de gestão de nuvem e o ponto de distribuição de nuvem. Para obter mais informações, consulte [planear CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a> Infraestrutura do site

### <a name="support-for-windows-server-2019"></a>Suporte para o Windows Server de 2019
<!--1359195--> O Configuration Manager suporta agora 2019 do Windows Server e no Windows Server, versão 1809, como sistemas de sites. 

Para obter mais informações, consulte [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Suporte de hierarquia para disponibilidade elevada do servidor de site
<!--1358224--> Sites de administração central e sites primários subordinados agora podem ter um servidor de sites adicionais em modo passivo. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>Melhorias para configurar os pré-requisitos

Ao instalar ou atualizar para versão 1810, configuração do Configuration Manager inclui agora ou melhora as verificações de pré-requisitos seguintes:

- **Reinício de sistema pendente**: Esta verificação de pré-requisitos agora é mais resiliente. Verifica a chaves de registo adicionais para funcionalidades do Windows. Para obter mais informações, consulte [reinício de sistema pendente](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Limpeza de controlo de alteração de SQL**: Uma nova verificação se a base de dados do site tem um registo de segurança de dados de controlo de alterações do SQL. Para obter mais informações, incluindo um procedimento para verificar e desmarque este registo de segurança, consulte [SQL Alterar controlo limpeza](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Versão do SQL Native Client**: Esta verificação de pré-requisitos foi atualizada com versões do SQL Native Client que suportam o TLS 1.2. A versão mínima é [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Para obter mais informações, consulte [versão do SQL Native Client](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094-->  

- **No nó de cluster do Windows do sistema de sites**: O processo de configuração do Configuration Manager já não bloqueia a instalação da função de servidor de site num computador com a função do Windows para o Clustering de ativação pós-falha. SQL Always On requer esta função, por isso, anteriormente não foi possível colocar a base de dados no servidor do site. Com esta alteração, pode criar um site de elevada disponibilidade com menos servidores com o SQL Always On e um servidor de site em modo passivo. Para obter mais informações, consulte [Cluster de ativação pós-falha do Windows](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>Nova permissão para ações de notificação do cliente
<!--SCCMDocs-pr issue #2972--> Ações de notificação do cliente agora exigem a **notificar recursos** permissão na classe SMS_Collection. As seguintes funções incorporadas têm esta permissão, por predefinição:
- Administrador total  
- Administrador de infraestrutura  

Adicione esta permissão para quaisquer funções personalizadas que tem de utilizar as ações de notificação do cliente. 

Para obter mais informações, consulte [notificações do cliente](/sccm/core/clients/manage/client-notification).



## <a name="bkmk_content"></a>Gestão de conteúdo

### <a name="new-boundary-group-options"></a>Novas opções de grupo de limites
<!--1358749--> Grupos de limites agora incluem as seguintes definições adicionais para lhe dar mais controle sobre a distribuição de conteúdo no seu ambiente:

- **Prefira pontos de distribuição através de protocolos de mesmo nível com a mesma sub-rede**: Por predefinição, o ponto de gestão, atribui prioridades aos origens da cache ponto a ponto na parte superior da lista de localizações de conteúdo. Esta definição reverte essa prioridade para clientes que estejam na mesma sub-rede que a origem de cache ponto a ponto.  

- **Prefira pontos de distribuição de cloud através de pontos de distribuição**: Se tiver uma filial com um link da internet mais rápida, agora pode priorizar o conteúdo em nuvem.  

Para obter mais informações, consulte [opções de grupos de limites para as transferências de ponto a ponto](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regra de informações de gestão para a versão de cliente de origem de cache ponto a ponto
<!-- 1358008 --> O **informações de gestão** nó tem uma nova regra para identificar os clientes que servem como uma origem de cache ponto a ponto, mas ainda não tiver atualizado a partir de uma versão de cliente de pré-1806. É a nova regra **atualizar origens de cache ponto a ponto para a versão mais recente do cliente do Configuration Manager**, e faz parte da nova **manutenção pró-ativa** grupo de regras. Pré-1806 clientes não podem servir como uma origem de cache ponto a ponto para clientes que executam a versão 1806 ou posterior. Selecione **agir** para abrir uma vista de dispositivo que apresenta a lista de clientes. 

Para obter mais informações, consulte [informações de gestão](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Gestão de clientes

### <a name="new-client-notification-action-to-wake-up-device"></a>Nova ação de notificação de cliente para reativar o dispositivo
<!--1317364--> Agora pode reativar os clientes a partir da consola do Configuration Manager, mesmo que o cliente não está na mesma sub-rede que o servidor do site. Se precisar de fazer a manutenção ou consulta de dispositivos, não está limitado pelos clientes remotos que estão em modo de suspensão. O servidor de site utiliza o canal de notificação de cliente para identificar a outro cliente está ativo na mesma sub-rede remota. O cliente ativo, em seguida, envia uma reativação no pedido de LAN (Pacote mágico).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nova opção para efetuar a notificação do cliente a partir do nó dispositivos
<!--1317364--> Até 1810, o **notificação do cliente** opção só estava disponível a partir do nó de coleção de dispositivos ou quando visualizado a associação de uma coleção de dispositivos. Agora, é possível efetuar uma **notificação do cliente** da **dispositivos** nó diretamente. Já não é um requisito para estar dentro de uma vista de associação de coleção. 

Para obter mais informações, consulte [notificações do cliente](/sccm/core/clients/manage/client-notification).


### <a name="improvements-to-collection-evaluation"></a>Melhorias à avaliação de coleção
<!--1358981--> As seguintes alterações no comportamento de avaliação de coleção podem melhorar o desempenho do site:  
 
- Anteriormente, quando tiver configurado uma agenda numa coleção com base na consulta, o site continuaria a avaliar a consulta quer ou não tiver ativado a definição de coleção para **agendar uma atualização completa para esta coleção**. Para desabilitar totalmente a agenda, era necessário que alterar a agenda para **None**. Agora o site limpa a agenda quando desativar esta definição. Para especificar uma agenda para avaliação de coleção, ative a opção para **agendar uma atualização completa para esta coleção**.  

- Não é possível desativar a avaliação de coleções incorporadas, como **todos os sistemas**, mas agora pode configurar a agenda. Este comportamento permite-lhe personalizar esta ação ao mesmo tempo que cumpra os requisitos de negócio. 

<!--For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).-->


### <a name="improvement-to-client-installation"></a>Melhoria para instalação do cliente
<!--1358840--> Ao instalar o cliente do Configuration Manager, o processo de ccmsetup entra em contacto com o ponto de gestão para localizar os conteúdos necessários. Anteriormente o ponto de gestão nesse processo devolve apenas os pontos de distribuição no grupo de limite atual do cliente. Se nenhum conteúdo estiver disponível, o processo de configuração é retrocede para transferir o conteúdo do ponto de gestão. Não existe nenhuma opção para reverter para pontos de distribuição em outros grupos de limites que podem ter o conteúdo necessário. Agora o ponto de gestão devolve pontos de distribuição com base na configuração do grupo de limites. 

Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).


### <a name="improvements-to-internet-based-client-setup"></a>Melhorias à configuração de clientes baseada na internet
<!--1359181-->
<!--move this under co-management?-->  
Esta versão ainda mais simplifica o processo de configuração de cliente do Configuration Manager para clientes na internet. O site publica informações adicionais do Azure Active Directory (Azure AD) para o gateway de gestão da cloud (CMG). Um cliente do Azure AD associado obtém essas informações de CMG, durante o processo de ccmsetup, utilizar o mesmo inquilino ao qual está associado. Este comportamento ainda mais simplifica a inscrição de dispositivos para a cogestão num ambiente com mais do que um inquilino do Azure AD. Agora, as propriedades de ccmsetup necessárias apenas duas são **CCMHOSTNAME** e **SMSSiteCode**.

<!--For more information, see [Prepare Windows 10 devices for co-management](https://docs.microsoft.com/en-us/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).-->



## <a name="bkmk_comgmt"></a> Cogestão

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Necessária a política de conformidade de aplicações para dispositivos cogeridos
<!--1358196--> Defina as regras de política de conformidade no Configuration Manager para as aplicações necessárias. Esta avaliação de aplicação faz parte do Estado de conformidade geral enviado para o Microsoft Intune para dispositivos cogeridos.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>Melhoria para o dashboard de cogestão
<!--1358980--> O dashboard de cogestão foi melhorado com as seguintes informações mais detalhadas:  

- O **estado de inscrição de cogestão** mosaico inclui Estados adicionais

- Um novo **estado de cogestão** mosaico com um gráfico de funil mostra os Estados do processo de inscrição

- Um novo mosaico com as contagens de **erros de inscrição**

![Captura de ecrã do dashboard de cogestão com os mosaicos de quatro principais](media/1358980-comgmt-dashboard.png)

Para obter mais informações, consulte [dashboard de cogestão](/sccm/comanage/how-to-monitor#co-management-dashboard).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gestão de aplicações

### <a name="convert-applications-to-msix"></a>Converter aplicações para MSIX
<!--3607729, fka 1359029-->
 ***[Atualizado] *** a partir da versão 1806, o Configuration Manager suporta a implementação do novo formato de pacote (.msix) de aplicação com o Windows 10. Agora, pode converter seus aplicativos existentes do Windows Installer (MSI) para o formato MSIX.

Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications#bkmk_msix).  


### <a name="repair-applications"></a>Aplicativos de reparação
<!--1357866--> Especifique uma linha de comando de reparo para tipos de implementação do Windows Installer e o instalador de Script. Em seguida, se habilitar a opção na implementação, um novo botão está disponível no Centro de Software para **reparação** o aplicativo. Quando configura uma aplicação com um programa de reparação, os usuários possam iniciar o comando do Centro de Software. 

Para obter mais informações, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) e [implementar aplicações](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Aprovar pedidos de aplicações através de e-mail
<!--1321550--> Configure notificações por e-mail para pedidos de aprovação de aplicações. Quando um utilizador solicita uma aplicação, receberá uma mensagem de e-mail. Clique em ligações no e-mail para aprovar ou negar o pedido, sem a necessidade de consola do Configuration Manager.

Para obter mais informações, consulte [aprovar aplicações](/sccm/apps/deploy-use/app-approval).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Métodos de deteção não carregam perfis do Windows PowerShell
<!--1359239--> Pode utilizar scripts do Windows PowerShell para métodos de Deteção em aplicativos e configurações nos itens de configuração. Quando estes scripts são executados nos clientes, o cliente do Configuration Manager chama agora PowerShell com o `-NoProfile` parâmetro. Esta opção inicia PowerShell sem perfis. 

Um perfil de PowerShell é um script que é executada quando o PowerShell é iniciado. Pode criar um perfil de PowerShell para personalizar o seu ambiente e para adicionar elementos específicos da sessão para cada sessão do PowerShell que começar. 

> [!Note]  
> Esta alteração no comportamento não se aplica a [Scripts](/sccm/apps/deploy-use/create-deploy-scripts) ou [CMPivot](/sccm/core/servers/manage/cmpivot). Esses dois recursos já utilizam este parâmetro de PowerShell.    

<!--For more information, see []().-->


## <a name="bkmk_osd"></a> Implementação do SO

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Suporte de sequência de tarefas do Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333-->

***[Atualizado]***  [Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está agora disponível com o Windows 10, versão 1809 ou posterior. Esta nova funcionalidade permite-lhe criar uma nova imagem e aprovisionar um dispositivo Windows 7 para [modo de controlada pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma sequência de tarefas do Configuration Manager única e nativo. 

Para obter mais informações, consulte [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Especifique a unidade para a manutenção da imagem de SO offline  
<!--1358924--> Agora, especifique a unidade que o Configuration Manager utiliza ao adicionar as atualizações de software para imagens do sistema operacional e pacotes de atualização do sistema operacional. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários, para que esta opção dá-lhe flexibilidade para selecionar a unidade a utilizar. 

Para obter mais informações, consulte [imagens do sistema operacional gerenciar](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) ou [pacotes de atualização de SO gerir](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Suporte de sequência de tarefas para grupos de limites
<!--1359025--> Quando um dispositivo é executada uma sequência de tarefas e precisa de adquirir o conteúdo, ele usa agora comportamentos de grupo de limites semelhantes para o cliente do Configuration Manager.   

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Melhoramentos à manutenção do controlador
<!--1358270--> Pacotes de controladores agora têm campos de metadados adicionais para **fabricante** e **modelo**. Utilize estes campos para os pacotes de controladores de etiqueta com informações para auxiliar na manutenção geral ou para identificar controladores antigos e duplicados, que pode eliminar.


### <a name="new-task-sequence-variable-for-last-action-name"></a>Nova variável de sequência de tarefas para o último nome de ação
<!--SCCMDocs-pr issue #2964--> Juntamente com a tarefa sequência variável _SMSTSLastActionRetCode, a sequência de tarefas também define uma nova variável **_SMSTSLastActionName**. Ele também registra este valor para o ficheiro smsts log. Esta nova variável é útil quando uma sequência de tarefas de resolução de problemas. Quando um passo falhar, um script personalizado pode incluir o nome de passo juntamente com o código de retorno.

Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a>Atualizações de software

### <a name="phased-deployment-of-software-updates"></a>Implementação faseada de atualizações de software
<!--1358146--> Crie implementações faseadas para atualizações de software. As implementações faseadas permitem-lhe organizar uma implementação coordenada e sequenciada de software com base em critérios personalizáveis e grupos.

Para obter mais informações, consulte [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Melhoria para janelas de manutenção para atualizações de software
<!--vso2839307--> A seguinte definição de cliente está no **atualizações de Software** grupo para controlar o comportamento de instalação de atualizações de software de janelas de manutenção: 

**Ativar a instalação de atualizações na janela de manutenção de "Todas as implementações" quando a janela de manutenção "Atualização de Software" está disponível**

Por predefinição, esta opção está **não** para manter consistente com o comportamento existente. Altere-o para **Sim** para permitir aos clientes utilizar outras janelas de manutenção disponíveis para instalar atualizações de software.

<!--For more information, see []().-->

### <a name="improvement-to-software-updates-maintenance"></a>Manutenção de atualizações de melhoria para o software
<!--2839349--> Agora executam as tarefas de limpeza do WSUS em sites secundários. Limpeza do WSUS para atualizações expiradas é executada e as atualizações substituídas, serão recusadas no WSUS para sites secundários.

Para obter mais informações, consulte [o comportamento de limpeza WSUS a partir da versão 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810)

## <a name="bkmk_report"></a>Relatórios

### <a name="improvement-to-lifecycle-dashboard"></a>Melhoria para o dashboard do ciclo de vida
<!--1358702--> O dashboard de ciclo de vida do produto agora inclui informações sobre **System Center 2012 Configuration Manager e versões posteriores**. 

Também há um novo relatório **ciclo de vida 05A - dashboard de ciclo de vida do produto**. Ele inclui informações semelhantes, como o dashboard na consola.

Para obter mais informações sobre este dashboard, consulte [utilize o dashboard do ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="improvement-to-data-warehouse"></a>Melhoria para o armazém de dados
<!--1358870--> Agora pode sincronizar mais tabelas da base de dados do site para o armazém de dados. Esta alteração permite-lhe criar relatórios mais com base nos seus requisitos empresariais.

Para obter mais informações, consulte [armazém de dados](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Consola do Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Autenticação de administrador do Configuration Manager
<!--1357013--> Agora pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. Para configurar esta definição, localize a **autenticação** separador **definições de hierarquia**. 

Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth).


### <a name="support-center"></a>Centro de Suporte
<!--1357489--> Utilize o Centro de suporte para resolução de problemas e em tempo real registo de cliente visualizando ou capturar o estado de um computador de cliente do Configuration Manager para análise posterior. Centro de suporte é uma ferramenta única para combinar administrador muitas ferramentas de resolução de problemas. Localizar o instalador do Support Center no servidor do site no **cd.latest\SMSSETUP\Tools\SupportCenter** pasta.

Para obter mais informações, consulte [Support Center](/sccm/core/support/support-center).


### <a name="management-insights-dashboard"></a>Dashboard de conhecimentos de gestão
<!--1357979-->

O **informações de gestão** nó agora inclui um dashboard gráfico. Este dashboard mostra uma descrição geral dos Estados de regra, que torna mais fácil para que possa mostrar o progresso. O dashboard inclui os seguintes mosaicos:

- **Índice de informações de gestão**: Controla o progresso global em regras de informações de gestão. O índice é uma média ponderada. Regras críticas valem o máximo. Esse índice oferece o peso, pelo menos, a regras opcionais.  

- **Grupos de informações de gestão**: Mostra a percentagem de regras em cada grupo.  

- **Prioridade de informações de gestão**: Mostra a percentagem de regras por prioridade.  

- **Todas as informações**: Uma tabela de informações, incluindo a prioridade e estado.  

![Captura de ecrã do dashboard de conhecimentos de gestão](media/1357979-management-insights-dashboard.png)

Para obter mais informações, consulte [informações de gestão](/sccm/core/servers/manage/management-insights).


### <a name="improvements-to-cmpivot"></a>Melhorias à CMPivot
<!--1359068--> CMPivot inclui os seguintes aprimoramentos:

- Guarde **favorito** consultas  

- No separador Resumo de consulta, selecione a contagem de dispositivos Offline ou de falha e, em seguida, selecione a opção para **criar coleção**. 

Para obter mais informações sobre o desempenho adicional e resolução de problemas melhorias CMPivot, consulte [melhorias para scripts](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Melhorias aos scripts
<!--1358239--> Agora pode ver a saída do script detalhadas no formato JSON não processado ou não estruturado. Essa formatação torna a saída mais fácil de ler e analisar. 

O desempenho seguintes e resolução de problemas de melhorias de aplicam a CMPivot e scripts:

- Devolvem saídos menos do que 80 KB atualizados de clientes para o site através de um canal de comunicação rápida. Esta alteração aumenta o desempenho da saída do script ou consulta de visualização.  

- Registos adicionais para resolução de problemas  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>API do fornecedor de SMS
<!--1321523--> O fornecedor de SMS agora fornece acesso de interoperabilidade de API só de leitura ao WMI através de HTTPS. O **fornecedor de SMS** aparece como uma função com uma opção para permitir a comunicação através do gateway de gestão na cloud. A utilização atual para esta definição é ativar aprovações de aplicação através de e-mail a partir de um dispositivo remoto. Para obter mais informações, consulte [aprovar pedidos de aplicações através de e-mail](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> MDM no local

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Uma ligação do Intune já não é necessária para novas implementações de MDM no local
<!--1359124--> O pré-requisito MDM no local para configurar uma subscrição do Microsoft Intune já não é necessário para novas implementações. Sua organização ainda requer licenças do Intune para utilizar esta funcionalidade. Atualmente não é possível remover a ligação do Intune a partir de implementações de MDM no local existentes. Para obter mais informações, consulte a [mensagem de blogue de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Outras atualizações

Além das novas funcionalidades, esta versão também inclui alterações adicionais, como correções de erros. Para obter mais informações, consulte [resumo das alterações no ramo atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4482169).

Para obter mais informações sobre as alterações aos cmdlets do Windows PowerShell para o Configuration Manager, consulte [notas de versão do PowerShell versão 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

O update rollup seguintes (4486457) está disponível na consola a partir de 25 de Janeiro de 2019: [Update rollup para o ramo atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4486457).


### <a name="hotfixes"></a>Correções

As seguintes correções adicionais estão disponíveis para resolver problemas específicos:

| ID | Título | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Certificado de conector do Microsoft Intune não renovar no Configuration Manager | 18 de Janeiro de 2019 | Sim |


## <a name="next-steps"></a>Passos seguintes

Quando estiver pronto para instalar esta versão, consulte [instalação de atualizações para o Configuration Manager](/sccm/core/servers/manage/updates) e [lista de verificação para a instalação de atualização 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalar novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para problemas conhecidos e significativos, consulte a [notas de versão](/sccm/core/servers/deploy/install/release-notes).

Depois de atualizar um site, reveja também os [lista de verificação de pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).
