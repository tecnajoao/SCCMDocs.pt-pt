---
title: Pré-visualização técnica 1806.2
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades disponíveis na versão 1806.2 Configuration Manager Technical Preview.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13742fcbeefacd2183b26c5083d6f8b3ee0ef60f
ms.sourcegitcommit: d1bf26bcf0d78b37ac7598fab36eb58ca69b1dc5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37067640"
---
# <a name="capabilities-in-technical-preview-18062-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1806.2 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview para o Configuration Manager, versão 1806.2. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica. 

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

### <a name="ki_sqlncli"></a> Os clientes não atualizem automaticamente
<!--518760--> Quando atualizar para a versão 1806.2, o site também atualiza o SQL Native Client, que pode causar um reinício pendente no servidor do site. Este atraso faz com que determinados ficheiros a não atualização, o que tem impacto sobre a atualização automática de cliente.

#### <a name="workarounds"></a>Soluções
Evitar este problema atualizando manualmente o SQL Native Client *antes de atualizar* versão 1806.2 o Configuration Manager. Para obter mais informações, consulte o [manutenção mais recente atualização para SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Se já atualizado o seu site, a atualização automática de cliente e a instalação push do cliente não funcionará. Tem de atualizar os clientes para testar totalmente mais novas funcionalidades. Atualize manualmente os clientes de pré-visualização técnica utilizando o seguinte processo:  

1. Localizar os ficheiros de origem do cliente no **CMUClient** pasta do diretório de instalação do Configuration Manager no servidor do site. Por exemplo, `C:\Program Files\Configuration Manager\CMUClient`  

2. Copie a pasta de CMUClient completa para o dispositivo cliente. Por exemplo, `C:\Temp\CMUClient`  

    Esta localização pode ser uma partilha de rede que esteja acessível a partir de clientes.  

3. Execute a seguinte linha de comandos a partir de uma linha de comandos elevada: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Se estiver a instalar um novo cliente no seu site 1806.2 da versão de pré-visualização técnica, utilize este mesmo processo. 

> [!Important]  
> Não utilize o `/MP` parâmetro da linha de comandos neste cenário. Este parâmetro tem prioridade sobre `/source` e faz com que o ccmsetup transferir conteúdo de cliente a partir do ponto de gestão ou ponto de distribuição.
> 
> Propriedades da linha de comandos, tais como SMSSITECODE ou CCMLOGLEVEL, são ok a utilizar, mas não deve ser necessário quando atualizar um cliente existente. 


### <a name="ki_version"></a> Versão 1806.2 mostra 1806 de versão em sobre o Configuration Manager
<!--518148--> Após a atualização para a versão de pré-visualização técnica 1806.2, se abrir o **sobre o Configuration Manager** janela do canto superior esquerdo da consola, este continua a mostrar **versão 1806**. 

#### <a name="workaround"></a>Solução
Utilize o **versão do Site** propriedade para determinar a diferença entre 1806 e 1806.2:

| Versão do site  | Versão
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="bkmk_pod"></a> Melhoramentos às implementações faseadas

Esta versão inclui as seguintes melhorias para [fases implementações](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence):
- [Estado da implementação faseada](#bkmk_pod-monitor)
- [Implementação faseada de aplicações](#bkmk_pod-app)
- [Implementação gradual durante implementações faseadas](#bkmk_pod-throttle)


### <a name="bkmk_pod-monitor"></a> Estado da implementação faseada
<!--1358577--> Implementações faseadas tem agora uma experiência de monitorização nativa. Do **implementações** no nó de **monitorização** área de trabalho, selecione uma implementação faseada e, em seguida, clique em **fases estado da implementação** no Friso.

![Dashboard de estado de implementação faseada que mostra o estado de duas fases](media/1358577-phased-deployment-status.png)

Este dashboard mostra as seguintes informações para cada fase da implementação:  

- **Total de dispositivos**: Quantos dispositivos visados por esta fase.  

- **Estado**: O estado atual nesta fase. Cada fase pode ser um dos seguintes Estados:  

    - **Implementação criada**: A implementação faseada criou uma implementação de software para a coleção para esta fase. Ativamente são direcionados para os clientes com este software.  

    - **A aguardar**: A fase anterior ainda não atingiu os critérios de êxito para a implementação para continuar a nesta fase.  

    - **Suspenso**: Um administrador suspenso a implementação.  

- **Progresso**: Os Estados de implementação codificado por cores dos clientes. Por exemplo: Concluído com sucesso, em curso, erro, requisitos não cumpridos e desconhecido. 


#### <a name="known-issue"></a>Problema conhecido
O dashboard de estado de implementação faseada pode mostrar várias linhas para a fase de mesma.<!--518510-->


### <a name="bkmk_pod-app"></a> Implementação faseada de aplicações
<!--1358147--> Crie faseadas implementações de aplicações. Implementações faseadas permitem-lhe orquestrar uma coordenada, sequenciada implementação de software com base em critérios personalizáveis e grupos.

Na consola do Configuration Manager, vá para o **biblioteca de Software**, expanda **gestão de aplicações**e selecione **aplicações**. Selecione uma aplicação e, em seguida, clique em **criar implementação fases** no Friso. 

O comportamento de implementação de uma aplicação de fases é igual para sequências de tarefas. Para obter mais informações, consulte [criar implementações faseadas de uma sequência de tarefas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="prerequisite"></a>Pré-requisito
Distribua o conteúdo da aplicação para um ponto de distribuição antes de criar a implementação faseada.<!--518293-->

#### <a name="known-issue"></a>Problema conhecido
Não é possível criar manualmente fases para uma aplicação. O assistente cria automaticamente duas fases para implementações de aplicações.


### <a name="bkmk_pod-throttle"></a> Implementação gradual durante implementações faseadas
<!--1358578--> Durante uma implementação faseada, a implementação em cada fase pode agora acontecer gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implementação e reduz a carga na rede causada pela distribuição de conteúdo para clientes. O site pode gradualmente disponibilizar o software dependendo da configuração para cada fase. Todos os clientes numa fase tem um prazo em relação ao momento, que o software é disponibilizado. A janela de tempo entre a hora de disponibilização e o prazo é igual para todos os clientes numa fase. 

Quando criar uma implementação faseada e configurar manualmente uma fase no **fase definições** página do Assistente para adicionar fase ou no **definições** página do Assistente de implementação de fases criar, configurar o opção: **Gradualmente tornar este software disponível durante este período de tempo (em dias)**. O valor predefinido desta definição é **0**, por isso, por predefinição não está limitada a implementação.

> [!Note]  
> Esta opção só está atualmente disponível para implementações faseadas de sequências de tarefas.  



## <a name="bkmk_msix"></a> Suporte para formatos de pacote de aplicação do novo Windows
<!--1357427--> O Configuration Manager suporta agora a implementação de novo pacote de aplicação do Windows 10 (.msix) e formatos de grupo (.msixbundle) de aplicação. A versão mais recente [pré-visualização do Windows Insider](https://insider.windows.com/) compilações atualmente suportam estes formatos de novo.

Para obter uma descrição geral de MSIX, consulte [um olhar MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Para saber como criar uma nova aplicação MSIX, consulte [suporte MSIX introduzido no internas criar 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Pré-requisitos
- Um cliente do Windows 10 em execução, pelo menos, Windows Insider Preview criar 17682
- Um pacote de aplicações do Windows no formato MSIX

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, [criar uma aplicação](/sccm/apps/deploy-use/create-applications). 
2. Selecione o ficheiro de instalação da aplicação **tipo** como **pacote de aplicação do Windows (*. AppX, *. appxbundle, *.msix, *.msixbundle) * *.
3. [Implementar a aplicação](/sccm/apps/deploy-use/deploy-applications) para o cliente a executar o mais recente Windows Insider versão de pré-visualização.



## <a name="bkmk_client-push"></a> Melhoramento de segurança de push de cliente
<!--1358204--> Ao utilizar o [push de cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation) método de instalação do cliente do Configuration Manager, o servidor de site cria uma ligação remota para o cliente para iniciar a instalação. A partir desta versão, o site pode exigir a autenticação mútua Kerberos, não permitindo contingência para NTLM antes de estabelecer a ligação. Esta melhoria ajuda a proteger a comunicação entre o servidor e o cliente. 

Consoante as políticas de segurança, o seu ambiente já pode preferir ou exigir Kerberos através de autenticação de NTLM mais antiga. Para obter mais informações sobre as considerações de segurança estes protocolos de autenticação, consulte o [definição de política de segurança do Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Pré-requisito

Para utilizar esta funcionalidade, os clientes devem ser numa floresta do Active Directory fidedigna. Kerberos no Windows depende do Active Directory para autenticação mútua. 


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

Quando atualizar o site, mantém o comportamento existente. Uma vez que *abrir* as propriedades de instalação de push de cliente, o site ativa automaticamente a verificação de Kerberos. Se necessário, pode permitir a ligação a contingência para utilizar uma ligação de NTLM menos segura, que não é recomendada. 

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Selecione o site de destino. No Friso, clique em **definições de instalação de cliente** e selecione **instalação Push do cliente**.  

2. O site agora ativou a verificação de Kerberos para a instalação push do cliente. Clique em **OK** para fechar a janela.  

3. Se for necessário para o seu ambiente, na janela de propriedades de instalação de Push de cliente, no **geral** separador, consulte a opção de **permitir a ligação de contingência para NTLM**. Esta opção está desativada por predefinição. 



## <a name="bkmk_insights"></a> Informações de gestão para uma manutenção pró-ativa
<!--1352184,et al--> Informações de gestão adicionais estão disponíveis nesta versão para realçar potenciais problemas de configuração. Reveja as seguintes regras no novo **uma manutenção pró-ativa** grupo:  

- **Itens de configuração não utilizados**: Itens de configuração que não fazem parte de uma linha de base de configuração e são com mais de 30 dias.  

- **Imagens de arranque não utilizados**: Imagens de arranque referenciadas não para utilização de sequência de tarefas ou o arranque PXE.  

- **Grupos de limites com nenhuma sistemas de site atribuído**: Sem sistemas de site atribuído, só podem ser utilizados grupos de limites para atribuição de site.  

- **Grupos de limites sem membros**: Grupos de limites não são aplicáveis para a atribuição de site ou a pesquisa de conteúdo se não tiverem nenhum membro.  

- **Pontos de distribuição não servir conteúdo aos clientes**: Pontos de distribuição que ainda não o conteúdo servido em clientes nos últimos 30 dias. Estes dados baseia-se em relatórios a partir de clientes do respetivo histórico de transferências.  

- **Expirado atualizações encontradas**: As atualizações expiradas não são aplicáveis para a implementação.   



## <a name="bkmk_comgmt"></a> Carga de trabalho de aplicações móveis de transição para dispositivos geridos conjuntamente
<!--1357892--> Gerir aplicações móveis com o Microsoft Intune ao continuar a utilizar o Configuration Manager para implementar aplicações de ambiente de trabalho do Windows. A transição a carga de trabalho de aplicações modernas, vá para a página de propriedades de gestão conjunta. Desloque o cursor de controlo do Configuration Manager para piloto ou todos os. 

Depois de efetuar a transição esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa do Configuration Manager estão disponíveis no Centro de Software. 

Para obter mais informações, consulte os artigos seguintes:  

- [Cogestão para os dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview)  

- [O que é a gestão de aplicações do Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="bkmk_bgoptions"></a> Opções do grupo de limites para transferências de elemento
<!--1356193--> Grupos de limites incluem agora definições adicionais para lhe dar mais controlo sobre a distribuição de conteúdo no seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir transferências de elemento de rede neste grupo de limites**: Esta definição está ativada por predefinição. O ponto de gestão fornece aos clientes uma lista de localizações de conteúdo que inclui as origens de ponto a ponto. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Existem dois cenários comuns que deve considerar o desativar esta opção:  

    - Se tiver um grupo de limites que inclui os limites de geograficamente dispersos localizações, por exemplo, uma VPN. Dois clientes podem estar no mesmo grupo de limites porque estão ligados através de VPN, mas em localizações muito diferentes que estão inadequadas para elemento de rede de partilha de conteúdo.  

    - Se utilizar um grupo de limites único, grande para atribuição de sites que não fazer referência a quaisquer pontos de distribuição.  

- **Durante as transferências de ponto a ponto, utilize apenas elementos dentro da mesma sub-rede**: Esta definição está dependente dos acima. Se ativar esta opção, o ponto de gestão apenas inclui as origens de ponto a ponto de lista de localização de conteúdo que estão na mesma sub-rede que o cliente.

    Cenários comuns para a ativação desta opção:

    - A estrutura de grupo de limites para distribuição de conteúdos inclui um grupo de limites de grandes dimensões que sobreposições outros grupos de limites mais pequenos. Com esta nova definição, a lista de origens de conteúdo que o ponto de gestão fornece aos clientes inclui apenas origens de ponto a ponto da mesma sub-rede.

    - Tem um grupo de limites de grandes dimensões única para todas as localizações de escritórios remotos. Ative esta opção e os clientes apenas partilham conteúdo dentro da sub-rede na localização do escritório remoto, em vez de risking a partilha de conteúdo entre localizações.


### <a name="known-issue"></a>Problema conhecido
Se o cliente de origem do elemento de rede tiver mais do que um endereço IP (IPv4, IPv6 ou ambos), a colocação em cache ponto a ponto não funciona. A nova opção **durante as transferências de ponto a ponto, utilize apenas elementos dentro da mesma sub-rede**, não tem qualquer efeito se o elemento de rede de origem tiver mais do que um endereço IP.<!--518661-->   



## <a name="bkmk_3pupdate"></a> Suporte para catálogos personalizados de atualizações de software de terceiros
<!--1358714--> Esta versão ainda mais itera sobre o suporte para atualizações de software de terceiros, como resultado de sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [Versão de pré-visualização técnica 1806](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate) fornecido suporte para *parceiro catálogos*, que são registados catálogos fornecedores de software. Catálogos indicadas por si, que não estão registados com a Microsoft, são denominados *catálogos personalizados*. Adicione catálogos personalizados na consola do Configuration Manager.  


### <a name="prerequisites"></a>Pré-requisitos 

- Configurar [atualizações de software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate). Concluir a primeira fase 1: Ativar e configurar a funcionalidade.   

- Um catálogo personalizado assinado digitalmente que contém digitalmente assinado atualizações de software.  

- O administrador requer as seguintes permissões:  

    - Site: Criar, modificar  


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione o **catálogos de atualização de Software de terceiros** nós. Clique em **Adicionar catálogo de personalizado** no Friso.  

2. No **geral** página, especifique os seguintes detalhes:  

    - **URL de transferência**: Um endereço HTTPS válido do catálogo personalizado.  

    - **Publicador**: O nome da organização que publica o catálogo.  

    - **Nome**: O nome do catálogo a apresentar na consola do Configuration Manager.  

    - **Descrição**: Uma descrição do catálogo.  

    - **URL de suporte** (opcional): Um endereço HTTPS válido de um Web site para obter ajuda com o catálogo.  

    - **Suporta contacte** (opcional): Informações de contacto para obter ajuda com o catálogo.  

3. Conclua o assistente. O assistente adiciona o catálogo novo num Estado unsubscribed.  

4. Subscrever o catálogo personalizado utilizando existente **subscrever catálogo** ação. Para obter mais informações, consulte [fase 2: Subscrever um catálogo de terceiros e sincronizar as atualizações](/sccm/core/get-started/capabilities-in-technical-preview-1806#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Não é possível adicionar catálogos com o mesmo URL de transferência e não é possível editar propriedades do catálogo. Se especificar propriedades incorretas para um catálogo personalizado, elimine o catálogo antes de adicioná-lo novamente.  


#### <a name="unsubscribe-from-a-catalog"></a>Anular a subscrição a partir de um catálogo
Para anular a subscrição a partir de um catálogo, selecione o catálogo pretendido na lista e clique em **anular a subscrição catálogo** no Friso. Se anular a subscrição de um catálogo, as ações e comportamentos seguintes ocorrem: 
- O site deixa de sincronização de novas atualizações 
- O site bloqueia os certificados associados para o conteúdo de assinatura e atualização de catálogo. 
- Atualizações existentes não são removidas, mas poderá não conseguir publicar ou implementá-las.

#### <a name="delete-a-custom-catalog"></a>Eliminar um catálogo personalizado
Elimine catálogos personalizados do mesmo nó da consola. Selecione um catálogo personalizado num *unsubscribed* de estado e clique em **eliminar personalizado catálogo**. Se já subscreveu o catálogo, primeiro anular a subscrição antes de o eliminar. Não é possível eliminar catálogos de parceiro. Eliminar um catálogo personalizado remove-o da lista de catálogos. Esta ação não afeta quaisquer atualizações de software que tiver publicado para o ponto de atualização de software.


### <a name="known-issue"></a>Problema conhecido
A ação de eliminação nos catálogos personalizados fica a cinzento, por conseguinte, não é possível eliminar o catálogos personalizados a partir da consola do. Para resolver este problema, utilize o **wbemtest** ferramenta no servidor do site. Consulta para a instância que pretende eliminar com o nome ou transferir o URL, por exemplo: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Na janela de resultados da consulta, selecione o objeto e clique em **eliminar**.<!--518676-->  



## <a name="bkmk_cloud"></a> Melhoramentos às funcionalidades de gestão de nuvem

Esta versão inclui as seguintes melhorias:  

- As seguintes funcionalidades agora suportam a utilização dos EUA do Azure Nuvem pública:<!--511980-->  

    - Integração do site para **gestão de nuvem** através de [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  

    - Implementar um [gateway de gestão de nuvem com o Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)  

    - Implementar um [na nuvem de ponto de distribuição com o Azure Resource Manager](/sccm/core/get-started/capabilities-in-technical-preview-1805#cloud-distribution-point-support-for-azure-resource-manager)  

- Os clientes estão a utilizar AutoPilot do Windows para aprovisionar o Windows 10 em dispositivos associados ao Azure Active Directory que estão ligados à rede no local. Para instalar ou atualizar o cliente do Configuration Manager nestes dispositivos, agora não precisa de um ponto de distribuição em nuvem ou um ponto de distribuição no local configurado para **permitir a ligação anónima dos clientes**. Em vez disso, ative a opção de site para **sistemas de sites de certificados gerados-utilize o Gestor de configuração para HTTP**, que permite que um cliente de associados a um domínio de nuvem comunicar com um ponto de distribuição ativado por HTTP no local. Para obter mais informações, consulte [comunicações de cliente seguras Improved](https://docs.microsoft.com/en-us/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="bkmk_report"></a> Novo relatório de compatibilidade de atualizações de software
<!--1357775--> Conformidade tradicionalmente visualizar relatórios para atualizações de software inclui dados dos clientes que ainda não recentemente contactar o site. Um novo relatório permite-lhe filtrar os resultados de compatibilidade para um grupo de atualização de software específico por parte dos clientes "bom estado de funcionamento". Este relatório mostra o estado de conformidade mais realista dos clientes do Active Directory no seu ambiente. 
 
Para ver o relatório, vá para o **monitorização** área de trabalho, expanda **relatórios**, expanda **relatórios**, expanda **atualizações de Software - conformidade**e selecione **conformidade 9 - estado de funcionamento geral e compatibilidade**. Especifique o **grupo de atualização**, **nome da coleção**, e **estado de funcionamento do cliente** estado.

O relatório inclui as seguintes partes:
- **Bom estado de funcionamento clientes vs Total de clientes**: Este gráfico de barras compara os "bom estado de funcionamento" clientes que comunicaram com o site no período de tempo especificado com o número total de clientes na coleção especificada.
- **Descrição geral da compatibilidade**: Este gráfico circular mostra o estado de conformidade geral para o grupo de atualização de software específico nos clientes ativos na coleção especificada.
- **Parte superior 5 não conformes por ID de artigo**: Este gráfico de barras apresenta as atualizações de software cinco superior no grupo especificado não conformes em clientes ativos na coleção especificada.
- Na parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
