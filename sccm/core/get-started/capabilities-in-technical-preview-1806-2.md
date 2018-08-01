---
title: Pré-visualização técnica 1806.2
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis na versão do Configuration Manager Technical Preview 1806.2.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5183b30d9184f7119d1423b5773da2b692026ab7
ms.sourcegitcommit: 64b343906afdd442189559119eea8e933642cbf8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342819"
---
# <a name="capabilities-in-technical-preview-18062-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1806.2 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview no Configuration Manager, versão 1806.2. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

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

### <a name="ki_sqlncli"></a> Os clientes não atualizar automaticamente
<!--518760--> Ao atualizar para versão 1806.2, o site também atualiza o SQL Native Client, que pode fazer com que um reinício pendente no servidor do site. Este atraso faz com que alguns arquivos para não atualização, o que tem impacto sobre a atualização automática de cliente.

#### <a name="workarounds"></a>Soluções alternativas
Evitar este problema atualizando manualmente o SQL Native Client *antes de atualizar* versão 1806.2 o Configuration Manager. Para obter mais informações, consulte a [manutenção mais recente atualização para o SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Se já atualizado o seu site, atualização automática de cliente e a instalação push do cliente não funcionará. Tem de atualizar os clientes para testar totalmente a maior parte das novas funcionalidades. Atualize manualmente os clientes de pré-visualização técnica com o seguinte processo:  

1. Localizar os ficheiros de origem do cliente no **CMUClient** pasta do diretório de instalação do Configuration Manager no servidor do site. Por exemplo, `C:\Program Files\Configuration Manager\CMUClient`  

2. Copie a pasta de CMUClient completa para o dispositivo cliente. Por exemplo, `C:\Temp\CMUClient`  

    Esta localização pode ser uma partilha de rede que é acessível a partir de clientes.  

3. Execute a seguinte linha de comando da linha de comandos elevada: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Se estiver a instalar um novo cliente no seu site 1806.2 da versão de pré-visualização técnica, utilize esse mesmo processo. 

> [!Important]  
> Não utilize o `/MP` parâmetro da linha de comandos neste cenário. Este parâmetro tem prioridade sobre `/source` e faz com que o ccmsetup transferir o conteúdo de cliente a partir do ponto de gestão ou ponto de distribuição.
> 
> Propriedades da linha de comandos, como SMSSITECODE ou CCMLOGLEVEL=3, estão ok para utilizar, mas não deve ser necessário quando atualizar um cliente existente. 


### <a name="ki_version"></a> Versão 1806.2 mostra 1806 de versão no acerca do Configuration Manager
<!--518148--> Depois de atualizar para versão de pré-visualização técnica 1806.2, se abrir o **sobre o Configuration Manager** janela no canto superior esquerdo da consola, ele continua a mostrar **versão 1806**. 

#### <a name="workaround"></a>Solução
Utilize o **versão do Site** propriedade para determinar a diferença entre 1806 e 1806.2:

| Versão do site  | Versão
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  


## <a name="bkmk_pod"></a> Melhorias para as implementações faseadas

Esta versão inclui as seguintes melhorias às [faseada implementações](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence):
- [Estado de implementação por fases](#bkmk_pod-monitor)
- [Implementação faseada de aplicações](#bkmk_pod-app)
- [Implementação gradual durante as implementações faseadas](#bkmk_pod-throttle)


### <a name="bkmk_pod-monitor"></a> Estado de implementação por fases
<!--1358577--> As implementações faseadas agora tem uma experiência de monitorização nativa. Do **implementações** nó a **monitorização** área de trabalho, selecione uma implementação faseada e, em seguida, clique em **estado da implementação por fases** na faixa de opções.

![Dashboard de estado de implementação por fases que mostra o estado de duas fases](media/1358577-phased-deployment-status.png)

Este dashboard mostra as seguintes informações para cada fase da implementação:  

- **Total de dispositivos**: O número de dispositivos visado por esta fase.  

- **Estado**: O estado atual desta fase. Cada fase pode ter um dos seguintes Estados:  

    - **Implementação criada**: A implementação faseada criou uma implementação do software para a coleção para esta fase. Os clientes são direcionados ativamente com este software.  

    - **A aguardar**: Fase anterior ainda não tiver atingido os critérios de êxito para a implementação continuar para esta fase.  

    - **Suspenso**: Um administrador suspensa a implementação.  

- **Curso**: Os Estados de implementação codificados por cores de clientes. Por exemplo: Êxito no curso, erro, requisitos não cumpridos e desconhecido. 


#### <a name="known-issue"></a>Problema conhecido
O dashboard de estado de implementação por fases pode mostrar várias linhas para a mesma fase.<!--518510-->


### <a name="bkmk_pod-app"></a> Implementação faseada de aplicações
<!--1358147--> Crie implementações faseadas para aplicações. As implementações faseadas permitem-lhe organizar uma implementação coordenada e sequenciada de software com base em critérios personalizáveis e grupos.

Na consola do Configuration Manager, vá para o **biblioteca de Software**, expanda **gestão de aplicações**e selecione **aplicativos**. Selecione uma aplicação e, em seguida, clique em **criar implementação faseada** na faixa de opções. 

O comportamento de implementação de uma aplicação por fases é igual de sequências de tarefas. Para obter mais informações, consulte [criar implementações faseadas para uma sequência de tarefas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="prerequisite"></a>Pré-requisito
Distribua o conteúdo da aplicação para um ponto de distribuição antes de criar a implementação faseada.<!--518293-->

#### <a name="known-issue"></a>Problema conhecido
Não é possível criar manualmente fases para uma aplicação. O assistente cria automaticamente duas fases para implementações de aplicações.


### <a name="bkmk_pod-throttle"></a> Implementação gradual durante as implementações faseadas
<!--1358578--> Durante uma implementação faseada, a implementação de cada fase pode agora acontecer gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implantação e diminui a carga na rede causada pela distribuição de conteúdo aos clientes. O site pode gradualmente disponibilizar o software dependendo da configuração para cada fase. Todos os clientes numa fase têm um prazo em relação ao tempo que o software é disponibilizado. A janela de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. 

Ao criar uma implementação faseada e configurar manualmente uma fase no **definições da fase** página do Assistente para adicionar fase ou no **definições** página do assistente criar implementação faseada, configure o opção: **Gradualmente tornar este software disponível durante este período de tempo (em dias)**. O valor predefinido desta definição é **0**, por isso, por predefinição não está limitada a implementação.

> [!Note]  
> Esta opção só está atualmente disponível para implementações faseadas de sequências de tarefas.  



## <a name="bkmk_msix"></a> Suporte para novos formatos de pacote de aplicação Windows
<!--1357427--> O Configuration Manager suporta agora a implementação de novo pacote de aplicação do Windows 10 (.msix) e formatos de pacote (.msixbundle) da aplicação. A versão mais recente [Windows Insider Preview](https://insider.windows.com/) compilações atualmente suportam estes novos formatos.

Para uma descrição geral MSIX, consulte [atentamente MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Para saber como criar uma nova aplicação MSIX, consulte [introduzido no Insider 17682 de criar o suporte MSIX](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Pré-requisitos
- Um cliente do Windows 10, pelo menos, Windows Insider Preview build 17682
- Um pacote de aplicação do Windows no formato MSIX

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, [criar uma aplicação](/sccm/apps/deploy-use/create-applications). 
2. Selecione o ficheiro de instalação do aplicativo **tipo** como **pacote de aplicação do Windows (\*. AppX, \*. appxbundle, \*.msix, \*.msixbundle)**.
3. [Implementar a aplicação](/sccm/apps/deploy-use/deploy-applications) para o cliente a executar a compilação mais recente do Windows Insider Preview.



## <a name="bkmk_client-push"></a> Melhoria de segurança de push de cliente
<!--1358204--> Ao utilizar o [push de cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation) método de instalação do cliente do Configuration Manager, o servidor do site cria uma ligação remota para o cliente para iniciar a instalação. A partir desta versão, o site pode exigir a autenticação mútua do Kerberos, não permitindo fallback para NTLM antes de estabelecer a ligação. Esta melhoria ajuda a proteger a comunicação entre o servidor e o cliente. 

Consoante as políticas de segurança, o seu ambiente já pode preferir ou requerem Kerberos através de autenticação de NTLM mais antiga. Para obter mais informações sobre as considerações de segurança, os protocolos de autenticação, consulte a [definição de política de segurança de Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Pré-requisito

Para utilizar esta funcionalidade, os clientes devem ser numa floresta do Active Directory fidedigna. Kerberos no Windows depende do Active Directory para autenticação mútua. 


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

Ao atualizar o site, o comportamento existente persiste. Uma vez que *abra* as propriedades de instalação de push de cliente, o site ativa automaticamente a verificação de Kerberos. Se necessário, pode permitir a ligação de reversão para utilizar uma ligação de NTLM menos segura, que não é recomendada. 

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Selecione o site de destino. No Friso, clique em **definições de instalação de cliente** e selecione **instalação Push do cliente**.  

2. O site agora ativou a verificação de Kerberos para instalação push do cliente. Clique em **OK** para fechar a janela.  

3. Se for necessário para o seu ambiente, na janela de propriedades de instalação de Push de cliente, sobre o **gerais** separador, consulte a opção de **permitir ligação fallback para NTLM**. Esta opção está desativada por predefinição. 



## <a name="bkmk_insights"></a> Informações de gestão para a manutenção proativa
<!--1352184,et al--> Informações de gestão adicionais estão disponíveis nesta versão, para realçar os potenciais problemas de configuração. Reveja as seguintes regras no novo **manutenção pró-ativa** grupo:  

- **Itens de configuração não utilizados**: Itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias.  

- **Imagens de arranque não utilizados**: Imagens de arranque não referenciadas para utilização de sequência de arranque ou a tarefa PXE.  

- **Grupos de limites com nenhuma sistemas de site atribuído**: Sem sistemas de site atribuído, só podem ser utilizados grupos de limites para atribuição de sites.  

- **Grupos de limites com nenhum membro**: Grupos de limites não são aplicáveis para a atribuição de site ou pesquisa de conteúdo se eles não têm nenhum membro.  

- **Pontos de distribuição não servir conteúdo aos clientes**: Pontos de distribuição que ainda não o conteúdo servido para clientes nos últimos 30 dias. Estes dados baseia-se em relatórios de clientes do respetivo histórico de transferências.  

- **Expirado atualizações encontradas**: Atualizações expiradas não são aplicáveis para a implementação.   



## <a name="bkmk_comgmt"></a> Carga de trabalho de aplicações móveis de transição para dispositivos cogeridos
<!--1357892--> Gerir aplicações móveis com o Microsoft Intune e continuar a utilizar o Configuration Manager para implementar aplicações de ambiente de trabalho do Windows. Para fazer a transição da carga de trabalho de aplicações modernas, vá para a página de propriedades de cogestão. Mova a barra de controlo de deslize do Configuration Manager para piloto ou todos. 

Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software. 

Para obter mais informações, consulte os artigos seguintes:  

- [Cogestão para os dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview)  

- [O que é a gestão de aplicações do Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="bkmk_bgoptions"></a> Opções de grupos de limites para configurar o peering downloads
<!--1356193--> Agora, os grupos de limites incluem definições adicionais para lhe dar mais controle sobre a distribuição de conteúdo no seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir transferências de ponto a ponto neste grupo de limites**: Esta definição está ativada por predefinição. O ponto de gestão fornece aos clientes uma lista de localizações de conteúdo que inclui a origens de ponto a ponto. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Existem dois cenários comuns nos quais deve considerar a desativar esta opção:  

    - Se tiver um grupo de limites que inclui os limites de geograficamente dispersos localizações, como uma VPN. Dois clientes possível no mesmo grupo de limites que estão ligados através de VPN, mas em diferentes locais que não apropriadas para o mesmo nível de partilha de conteúdo.  

    - Se utilizar um grupo de limites única e grandes para a atribuição de sites que não façam referência a quaisquer pontos de distribuição.  

- **Durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede**: Esta definição é dependente de um acima. Se ativar esta opção, o ponto de gestão inclui apenas nas fontes de mesmo nível de lista de localização de conteúdo que estão na mesma sub-rede que o cliente.

    Cenários comuns para ativar esta opção:

    - A estrutura de grupo de limites para distribuição de conteúdos inclui um grupo de limites de grandes dimensões que sobrepõe-se a outros grupos de limites mais pequenos. Com esta nova definição, a lista de fontes de conteúdo que o ponto de gestão fornece aos clientes inclui apenas as origens de ponto a ponto da mesma sub-rede.

    - Tem um grupo de limites de grandes único para todas as localizações de escritórios remotos. Ative esta opção e os clientes apenas de partilhar conteúdos dentro da sub-rede na localização do escritório remoto, em vez de correr o risco de partilha de conteúdo entre localizações.


### <a name="known-issue"></a>Problema conhecido
Se o cliente de origem do elemento de rede tiver mais de um endereço IP (IPv4, IPv6 ou ambos), colocação em cache de elemento de rede não funciona. A nova opção **durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede**, não tem qualquer efeito se a origem de item de mesmo nível tem mais de um endereço IP.<!--518661-->   



## <a name="bkmk_3pupdate"></a> Suporte para catálogos personalizados de atualizações de software de terceiros
<!--1358714--> Esta versão ainda mais itera sobre o suporte para atualizações de software de terceiros, como resultado de sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [Versão de pré-visualização técnica 1806](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate) foi fornecido suporte para *catálogos de parceiros*, que são registados catálogos de fornecedores de software. Catálogos fornecidas por si, que não são registados na Microsoft, são chamados *catálogos personalizados*. Adicione catálogos personalizados na consola do Configuration Manager.  


### <a name="prerequisites"></a>Pré-requisitos 

- Configurar [atualizações de software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate). Concluir a primeira fase 1: Ativar e configurar a funcionalidade.   

- Um catálogo personalizado assinado digitalmente que contém digitalmente assinado atualizações de software.  

- O administrador requer as seguintes permissões:  

    - Site: Criar, modificar  


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione o **catálogos de atualizações de Software de terceiros** nó. Clique em **catálogo de personalizado adicionar** na faixa de opções.  

2. Sobre o **gerais** , especifique os seguintes detalhes:  

    - **URL de transferência**: Um endereço HTTPS válido do catálogo personalizado.  

    - **Publicador**: O nome da organização que publica o catálogo.  

    - **Nome**: O nome do catálogo, para apresentar na consola do Configuration Manager.  

    - **Descrição**: Uma descrição do catálogo.  

    - **URL de suporte** (opcional): Um endereço HTTPS válido de um Web site para obter ajuda com o catálogo.  

    - **Contacto de suporte** (opcional): Informações de contacto para obter ajuda com o catálogo.  

3. Conclua o assistente. O assistente adiciona o novo catálogo num Estado de funcionamento anulou a subscrição receber.  

4. Subscrever o catálogo personalizado com a atual **subscrever catálogo** ação. Para obter mais informações, consulte [fase 2: Subscrever um catálogo de terceiros e sincronizar as atualizações](/sccm/core/get-started/capabilities-in-technical-preview-1806#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Não é possível adicionar catálogos com o mesmo URL de transferência, e não é possível editar propriedades do catálogo. Se especificar propriedades incorretas para um catálogo personalizado, de eliminar o catálogo antes de adicioná-lo novamente.  


#### <a name="unsubscribe-from-a-catalog"></a>Anular a subscrição de um catálogo
Para anular a subscrição de um catálogo, selecione o catálogo pretendido na lista e clique em **catálogo de anular a subscrição** na faixa de opções. Se cancelar a inscrição a partir de um catálogo, os comportamentos e ações seguintes ocorrem: 
- O site deixa de sincronização de atualizações novas 
- O site bloqueia os certificados associados para o conteúdo de assinatura e a atualização do catálogo. 
- Atualizações existentes não são removidas, mas poderá não conseguir publicar ou implementá-las.

#### <a name="delete-a-custom-catalog"></a>Eliminar um catálogo personalizado
Elimine catálogos personalizados do mesmo nó da consola. Selecione um catálogo personalizado num *anulou a subscrição receber* de estado e clique em **Eliminar catálogo personalizado**. Se já inscrito para o catálogo, primeiro anular a subscrição antes de o eliminar. Não é possível eliminar catálogos de parceiros. A eliminar um catálogo personalizado, remove-o na lista de catálogos. Esta ação não afeta quaisquer atualizações de software que tenham publicado para o seu ponto de atualização de software.


### <a name="known-issue"></a>Problema conhecido
A ação de eliminação no catálogos personalizados de está a cinzento, portanto, não é possível eliminar o catálogos personalizados a partir da consola. Para resolver este problema, utilize o **wbemtest** ferramenta no servidor do site. Consulta para a instância que pretende eliminar com o nome ou transferir URL, por exemplo: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Na janela de resultados da consulta, selecione o objeto e clique em **eliminar**.<!--518676-->  



## <a name="bkmk_cloud"></a> Melhorias para a cloud de funcionalidades de gestão

Esta versão inclui as seguintes melhorias:  

- As seguintes funcionalidades agora suportam a utilização do Azure dos EUA Nuvem de governo:<!--511980-->  

    - Integração do site para **gestão na Cloud** através de [dos serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  

    - Implementar um [gateway de gestão na cloud com o Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)  

    - Implementar um [ponto de distribuição com o Azure Resource Manager da nuvem](/sccm/core/get-started/capabilities-in-technical-preview-1805#cloud-distribution-point-support-for-azure-resource-manager)  

- Os clientes estão usando o Windows AutoPilot para aprovisionar o Windows 10 em dispositivos associados ao Azure Active Directory que estão ligadas à rede no local. Para instalar ou atualizar o cliente do Configuration Manager nestes dispositivos, agora não precisa de um ponto de distribuição em nuvem ou ponto de distribuição no local configurado para **permitir a ligação anónima dos clientes**. Em vez disso, ative a opção de site para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**, que permite que um cliente associado a um domínio de nuvem comunicar com um ponto de distribuição ativado por HTTP no local. Para obter mais informações, consulte [comunicações de cliente seguras melhorado](https://docs.microsoft.com/en-us/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="bkmk_report"></a> Novo relatório de conformidade de atualizações de software
<!--1357775--> Visualizar relatórios para atualizações de software conformidade tradicionalmente inclui os dados de clientes que ainda não recentemente a contactar o site. Um novo relatório permite-lhe filtrar os resultados de compatibilidade para um grupo de atualização de software específico por clientes de "integridade". Este relatório mostra o estado de conformidade mais realista dos clientes ativos no seu ambiente. 
 
Para ver o relatório, vá para o **monitorização** área de trabalho, expanda **Reporting**, expanda **relatórios**, expanda **atualizações de Software - conformidade**e selecione **conformidade 9 - estado de funcionamento geral e a conformidade**. Especifique a **grupo de atualização**, **nome da coleção**, e **estado de funcionamento do cliente** estado.

O relatório inclui as seguintes partes:
- **Bom estado de funcionamento clientes vs Total de clientes**: Este gráfico de barras compara os clientes de "integridade" que comunicaram com o site no período de tempo especificado com o número total de clientes na coleção especificada.
- **Descrição geral de conformidade**: Este gráfico circular mostra o estado de conformidade geral para o grupo de atualização de software específico em clientes ativos na coleção especificada.
- **5 principais em não conformidades por ID de artigo**: Este gráfico de barras mostra as atualizações de software de cinco principais no grupo especificado que estão em não conformidades em clientes ativos na coleção especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
