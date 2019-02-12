---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis na versão do Configuration Manager Technical Preview 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 086f7aa4062ee62a2ee8aaf28df3a1e6e389bdf0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139209"
---
# <a name="capabilities-in-technical-preview-1805-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1805 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview no Configuration Manager, versão 1805. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja os [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Criar uma implementação faseada com fases configurados manualmente para uma sequência de tarefas
<!--1358148--> Agora, pode [criar uma implementação faseada](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) com fases configurados manualmente para uma sequência de tarefas. Pode adicionar até 10 fases adicionais do **fases** separador do Assistente para criar implementação por fases. 


### <a name="try-it-out"></a>Experimente!
Siga as instruções para criar uma implementação faseada onde são configuradas manualmente todas as fases. Envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu. 

1. Na **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Com o botão direito na sequência de tarefas existente e selecione **criar implementação faseada**.  

3. Sobre o **gerais** separador, dê um nome, descrição (opcional), à implementação faseada e selecione **configurar manualmente todas as fases**.  

4. Sobre o **fases** separador, clique em **Add**.  

5. Especifique um **Name** para a fase e, em seguida, navegue para o destino **fase de coleção**.  

6. Sobre o **definições da fase** separador, escolher uma opção para cada uma das definições de agendamento e selecione **próxima** quando terminar.  

    - Critérios para o êxito da fase anterior (esta opção está desativada para a primeira fase.)
        - **Percentagem de êxito da implementação**: Especifique a percentagem de dispositivos que concluir a implementação para os critérios de êxito da fase anterior com êxito.  

    - Condições para iniciar esta fase de implementação após o êxito da fase anterior  
        - **Iniciar automaticamente esta fase após um período de diferimento (em dias)**: Escolha o número de dias a aguardar antes de iniciar a fase seguinte após o êxito da fase anterior. 
        - **Iniciar manualmente esta fase de implantação**: Não iniciar esta fase automaticamente após o êxito da fase anterior.  

    - Assim que um dispositivo é direcionado, instale o software
        - **Assim que possível**: Define o prazo de instalação do dispositivo assim que o dispositivo é direcionado.
        - **Hora (relativo à hora de dispositivo é direcionado) do prazo**: Define o prazo de instalação de um determinado número de dias após o dispositivo é direcionado.  
     
7. Conclua o Assistente de definições da fase.

8. Sobre o **fases** separador do Assistente para criar implementação por fases agora pode adicionar, remover, reordenar ou editar fases para esta implementação.  

9. Conclua o assistente criar implementação faseada.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte de ponto de distribuição de nuvem para o Azure Resource Manager
<!--1322209--> Ao criar uma instância do [ponto de distribuição da nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure), o assistente fornece agora a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implementar um ponto de distribuição de nuvem com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não requer o certificado de gestão clássico do Azure.  

O Assistente de ponto de distribuição de nuvem ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, recomendamos que utilize o modelo de implementação Azure Resource Manager para todos os novos pontos de distribuição de nuvem. Se possível, volte a implementar pontos de distribuição existentes na cloud através do Resource Manager.

O Configuration Manager não migra pontos de distribuição de cloud clássica existentes para o modelo de implementação Azure Resource Manager. Criar nova nuvem pontos de distribuição com implementações do Azure Resource Manager e, em seguida, remova os pontos de distribuição de cloud clássica. 

> [!IMPORTANT]  
> Esta capacidade não ativa o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação de ponto de distribuição em nuvem com o Azure Resource Manager continua a utilizar o serviço cloud clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Pré-requisitos  
- Integração com o [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Deteção de utilizadores do Azure AD não é necessária.  

- O mesmo [os requisitos para um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_PrereqsCloudDP), exceto para o certificado de gestão do Azure.  


### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, **Administration** área de trabalho, expanda **serviços Cloud**e selecione **pontos de distribuição de nuvem**. Clique em **criar ponto de distribuição na nuvem** na faixa de opções.   

2. Sobre o **gerais** página, selecione **implementação Azure Resource Manager**. Clique em **iniciar sessão** para autenticar com uma conta de administrador de subscrição do Azure. O assistente é preenchido automaticamente os campos restantes das informações de subscrição do Azure AD armazenados durante a pré-requisitos de integração. Se tiver várias subscrições, selecione a subscrição pretendida a utilizar. Clique em **Seguinte**.  

3. Sobre o **definições** , indique o servidor de PKI **ficheiro de certificado** como de costume. Este certificado define o ponto de distribuição de nuvem **FQDN de serviço** utilizados pelo Azure. Selecione o **região**e, em seguida, selecione uma opção de grupo de recursos de **criar nova** ou **utilizar existente**. Introduza o nome do grupo de recursos novo ou selecione um grupo de recursos existente na lista pendente.  

4. Conclua o assistente.  

> [!NOTE]  
> Para o Azure AD selecionado aplicação de servidor, o Azure atribui a subscrição **contribuinte** permissão.  

Monitorizar o progresso da implementação de serviço com **cloudmgr** no ponto de ligação de serviço.



## <a name="take-actions-based-on-management-insights"></a>Executar ações com base nas informações de gestão
<!--1357930--> Algumas [informações de gestão](/sccm/core/servers/manage/management-insights) agora tem a opção de adotar uma ação. Consoante a regra, esta ação exibe um dos seguintes comportamentos:  

- Navegar automaticamente na consola para o nó em que pode qualquer ação adicional. Por exemplo, se as informações de gestão recomenda alterar uma definição de cliente, tomar navega para o nó de definições de cliente. Agir ainda mais ao modificar o padrão ou um objeto de definições de cliente personalizadas.  

- Navegue para uma exibição filtrada com base numa consulta. Por exemplo, realizar a ação na regra de coleções vazias mostra apenas essas coleções na lista de coleções. Aqui pode qualquer ação adicional, como a eliminação de uma coleção ou modificar as suas regras de associação.  

As seguintes regras de informações de gestão têm ações nesta versão:
- Segurança
    - Versões de cliente de antimalware não suportadas
- Software Center
    - Utilizar a nova versão do Centro de Software
- Aplicações
    - Aplicações sem implementações
- Gestão simplificada
    - Versões de cliente não CB
- Coleções
    - Coleções vazias 
- Serviços cloud
    - Atualizar clientes para a versão mais recente do Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Carga de trabalho do transição dispositivo configuração Intune com a cogestão
<!--1357903-->

Pode realizar a transição carga de trabalho de configuração dispositivo do Configuration Manager para o Intune depois de ativar a cogestão. Transição esta carga de trabalho permite-lhe políticas de utilização do Intune para implementar o MDM, enquanto continua a utilizar o Configuration Manager para implantar aplicativos. 

Para fazer a transição esta carga de trabalho, vá para a página de propriedades de cogestão e mova a barra de controlo de deslize do Configuration Manager para **piloto** ou **todos os**. Para obter mais informações, consulte [cogestão para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).

> [!Note]  
> Mover esta carga de trabalho também move os **acesso a recursos** e **Endpoint Protection** cargas de trabalho, que são um subconjunto da carga de trabalho de configuração do dispositivo.

Faça a transição esta carga de trabalho, pode continuar a implementar as definições do Configuration Manager para dispositivos cogeridos, mesmo que o Intune é a autoridade de configuração do dispositivo. Essa exceção pode ser utilizada para configurar as definições que são necessárias pela sua organização, mas ainda não está disponível no Intune. Especifique esta exceção numa linha de base de configuração do Configuration Manager. Ativar a opção para **sempre aplicam-se esta linha de base, mesmo para clientes cogeridos** ao criar a linha de base ou no **geral** separador das propriedades de uma linha de base existente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ativar pontos de distribuição para utilizar o controlo de congestionamento de rede
<!--1358112-->

Windows baixa Extra atraso em segundo plano transporte (LEDBAT) é uma funcionalidade do Windows Server para o ajudar a gerir as transferências de rede em segundo plano. Para pontos de distribuição em execução em versões suportadas do Windows Server, pode ativar uma opção para o ajudar a ajustar o tráfego de rede. Os clientes utilizam apenas a largura de banda de rede quando estiver disponível. 

Para obter mais informações sobre LEDBAT do Windows, consulte a [avanços de transporte de New](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) postagem de blog.


### <a name="prerequisites"></a>Pré-requisitos
- Um ponto de distribuição na versão 1709 do Windows Server.  

- Não há nenhum pré-requisito do cliente.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Selecione o **pontos de distribuição** nó. Selecione o ponto de distribuição de destino e clique em **propriedades** na faixa de opções.  

2. Sobre o **gerais** separador, ative a opção de **ajustar a velocidade de transferência para utilizar a largura de banda de rede não utilizadas (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Dashboard de gestão da cloud
<!--1358461--> A nova **dashboard de gestão da cloud** fornece uma visão centralizada para utilização de gateway (CMG) de gestão na cloud. Quando o site está integrado com o Azure AD, também apresenta dados sobre os utilizadores da nuvem e dispositivos.  

Captura de ecrã seguinte é uma parte do dashboard de gestão na cloud, que mostra dois dos mosaicos disponíveis:  
![Tráfego de CMG de mosaicos de dashboard de gestão de nuvem e de clientes online atuais](media/1358461-cmg-dashboard.png)

Esta funcionalidade também inclui a **analisador de ligação do CMG** para a verificação em tempo real ajudar a resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através da ligação do CMG aponte para pontos de gestão que permitam o tráfego CMG.


### <a name="prerequisites"></a>Pré-requisitos
- Um ativo [gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) utilizado por clientes baseados na internet.  

- A integração de site para [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão na cloud.  


### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

#### <a name="cloud-management-dashboard"></a>Dashboard de gestão da cloud

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho. Selecione o **gestão na Cloud** mosaicos do nó e ver o dashboard.  

#### <a name="cmg-connection-analyzer"></a>Analisador de ligação do CMG

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud** e selecione **gateway de gestão da nuvem**.  

2. Selecione a instância CMG de destino e, em seguida, selecione **analisador da ligação** na faixa de opções.  

3. Na janela de analisador da ligação do CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Utilizador do Azure AD**: Utilize esta opção para simular communication o mesmo que uma identidade de utilizador baseadas na cloud conectado a um dispositivo do Azure Windows 10 associados ao AD. Clique em **sessão** em segurança, introduza as credenciais para esta conta de utilizador do Azure AD.  

     2. **Certificado de cliente**: Utilize esta opção para simular communication o mesmo que um cliente do Configuration Manager com um [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Clique em **iniciar** para iniciar a análise. Os resultados são exibidos na janela do analyzer. Selecione uma entrada para ver mais detalhes no campo Descrição.  



## <a name="cmpivot"></a>CMPivot
<!--1358456--> O Configuration Manager sempre forneceu um armazenamento centralizado grandes de dados de dispositivo, que os clientes utilizam para fins de relatórios. No entanto, a que dados apenas são o melhor a última vez que foi recolhido dos clientes. 

CMPivot é um novo utilitário de na consola, que fornece acesso ao Estado em tempo real de dispositivos no seu ambiente. Ele imediatamente, executa uma consulta em todos os dispositivos atualmente ligados na coleção de destino e retorna os resultados. Pode, em seguida, filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode mais rapidamente responder às perguntas sobre, resolver problemas e responder a incidentes de segurança.

Por exemplo, no [mitigar vulnerabilidades de canal de lado a execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Pode utilizar CMPivot para consultar rapidamente nas informações de BIOS do sistema e encontrar os clientes que não estejam em conformidade. 

Nesta captura de ecrã, CMPivot apresenta duas versões do BIOS separadas com uma contagem de dispositivos de um cada. Pode usar esta consulta de exemplo, quando experimentar CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Janela de CMPivot com o exemplo de consulta do BIOSVersion](media/1358456-cmpivot-biosversion.png)

Pode clicar na contagem de dispositivos para desagregar para ver os dispositivos específicos. Quando visualizar dispositivos em CMPivot, pode utilizar para um dispositivo com o botão direito e selecione as seguintes [ações de notificação de cliente](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode):
- Executar Script
- Controlo Remoto
- Explorador de recursos

Quando clicar com o botão direito num dispositivo específico, também pode dinamizar a vista do dispositivo específico a um dos seguintes atributos:
- Comandos de início automático
- Produtos instalados
- Processos
- Serviços
- Utilizadores
- Ligações ativas
- Atualizações em falta

### <a name="prerequisites"></a>Pré-requisitos
- Os clientes de destino têm de ser atualizados para a versão mais recente.  

- Administrador do Configuration Manager necessita de permissões para executar scripts. Para obter mais informações, consulte [funções de segurança para os scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione **coleções de dispositivos**. Selecione uma coleção de destino e clique em **CMPivot iniciar** na faixa de opções para iniciar a ferramenta.  

2. A interface fornece mais informações sobre como utilizar a ferramenta. 
     - Manualmente pode introduzir cadeias de caracteres de consulta na parte superior, ou clique nas ligações na documentação do inline.
     - Clique da **entidades** para adicioná-lo para a cadeia de consulta. 
     - As ligações para **operadores de tabela**, **funções de agregação**, e **funções escalares** abrir documentação de referência de idioma no navegador da web. O mesmo idioma de consulta que utiliza o CMPivot [do Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Melhorada a comunicações de cliente seguras
<!--1356889,1358228,1358460--> Utilizar a comunicação HTTPS é recomendada para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução do Azure Active Directory integration (Azure AD) reduz alguns, mas nem todos os requisitos de certificado. 

Esta versão inclui melhoramentos para a forma como os clientes comunicam com sistemas de sites. Existem dois objetivos principais para esses aprimoramentos:  

- Pode proteger a comunicação de cliente sem a necessidade de certificados de autenticação de servidor PKI.  

- Os clientes com segurança podem aceder a conteúdo de pontos de distribuição sem a necessidade de uma conta de acesso de rede.  

> [!Note]  
> Certificados PKI ainda são uma opção válida para os clientes que desejam usá-lo.  


### <a name="bkmk_token"></a> Cenários
Os cenários seguintes se beneficiar desses aprimoramentos:  

#### <a name="bkmk_token1"></a> Cenário 1: Cliente para ponto de gestão
<!--1356889-->
[Dispositivos associados ao Azure AD](/azure/active-directory/device-management-introduction#azure-ad-joined-devices) pode comunicar através de um gateway de gestão da cloud (CMG) com um ponto de gestão configurado para HTTP. O servidor de site gera um certificado para o ponto de gestão que lhe permite comunicar através de um canal seguro.   

> [!Note]  
> Este comportamento é alterado a partir do Gestor de configuração atual versão do ramo 1802, que requer um ponto de gestão que suporte HTTPS para este cenário. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

#### <a name="bkmk_token2"></a> Cenário 2: Cliente para ponto de distribuição
<!--1358228--> Grupo de trabalho ou do Azure AD associado a um cliente pode transferir o conteúdo através de um canal seguro de um ponto de distribuição configurado para HTTP.   

#### <a name="bkmk_token3"></a> Identidade de dispositivo do cenário 3 do Azure AD 
<!--1358460--> Associado um Azure AD ou [dispositivos do Azure AD híbrido](/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um Azure AD utilizador iniciada sessão pode comunicar de forma segura com o respetivo site atribuído. A identidade de dispositivo com base na cloud agora é suficiente para se autenticar com o ponto de gestão e CMG.  


### <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gestão configurado para ligações de cliente HTTP. Defina esta opção no **gerais** separador de propriedades de função do sistema de sites.  

- Um ponto de distribuição configurado para ligações de cliente HTTP. Defina esta opção no **gerais** separador de propriedades de função do sistema de sites. Não ative a opção para **permitir a ligação anónima dos clientes**.  

- Um gateway de gestão na cloud.  

- Carregar o site para o Azure AD para gestão na cloud.  

    - Se já tiver cumprido este pré-requisito para o seu site, tem de atualizar a aplicação do Azure AD. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione **inquilinos do Azure Active Directory do**. Selecione o inquilino do Azure AD, selecione a aplicação web no **aplicativos** painel e, em seguida, clique **atualização da definição de aplicação** na faixa de opções.  

- Um cliente com o Windows 10 versão 1803 e associado ao Azure AD. (Este requisito é tecnicamente apenas para [cenário 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Selecione o site e clique em **propriedades** na faixa de opções.  

2. Mude para o **comunicação do computador cliente** separador. Selecione a opção para **HTTPS ou HTTP** e, em seguida, ative a nova opção **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**.  

Veja quanto mais cedo [lista de cenários](#bkmk_token) para validar.

> [!Tip]
> Nesta versão, aguarde até 30 minutos para o ponto de gestão receber e configurar o novo certificado do site.

Pode ver estes certificados na consola do Configuration Manager. Vá para o **administração** área de trabalho, expanda **Security**e selecione o **certificados** nó. Procure o **SMS emitir** certificado de raiz, bem como os certificados de função de servidor de site emitidos por raiz emissora de SMS.


### <a name="known-issues"></a>Problemas conhecidos
- O utilizador não pode ver, no Centro de Software, todas as aplicações direcionadas aos mesmos como disponível.  

- Cenários de implementação do sistema operacional ainda exigem a conta de acesso de rede.  

- Forma rápida e repetida ativar e desativar a opção para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP** pode fazer com que o certificado a ligação não está corretamente com as funções de sistema de sites. Não existem certificados emitidos pelo certificado "Emissão de SMS" são vinculados a um Web site no Windows Server Internet serviços de informação (IIS). Para contornar este problema, elimine todos os certificados emitidos emitindo"SMS" dos **SMS** arquivo no Windows de certificados e, em seguida, reinicie o serviço smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Melhorias para ativar o suporte de atualização de software de terceiros
<!--1357605--> Como resultado de comentários no UserVoice [suporte de atualização de software de terceiros](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), esta versão ainda mais itera sobre a integração com o System Center atualiza Publisher (SCUP). Pré-visualização técnica do Configuration Manager [versão 1803](/sccm/core/get-started/capabilities-in-technical-preview-1803#enable-third-party-software-update-support-on-clients) adicionada a capacidade de ler o certificado do WSUS para atualizações de terceiros e, em seguida, implementar esse certificado em clientes. Mas ainda precisava de utilizar a ferramenta SCUP para criar e gerir o certificado de assinatura de atualizações de software de terceiros.

Nesta versão, pode ativar o site do Configuration Manager configurar automaticamente o certificado. O site se comunica com o WSUS para gerar um certificado para esta finalidade. O Configuration Manager, em seguida, continua a implementar o certificado em clientes. Essa iteração remove a necessidade de usar a ferramenta SCUP para criar e gerir o certificado. 

Para obter mais informações sobre a utilização geral da ferramenta SCUP, consulte [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

### <a name="prerequisites"></a>Pré-requisitos
- Ativar e implementar a definição de cliente **ativar as atualizações de software de terceiros** no **atualizações de Software** grupo.
- Se for WSUS num servidor separado do ponto de atualização de software, terá de efetuar uma das opções seguintes no servidor WSUS remoto:
    - Ativar o serviço de registo remoto no Windows  
    ou
    - Na chave do registo `HKLM\Software\Microsoft\Update Services\Server\Setup`, crie uma nova DWORD denominada **EnableSelfSignedCertificates** com um valor de `1`. 

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Selecione o site de nível superior, clique em **configurar componentes do Site** na faixa de opções e selecione **ponto de atualização de Software**.  

2. Mude para o **atualizações de terceiros** separador. Selecione a opção para **ativar atualizações de software de terceiros**e, em seguida, selecione a opção para **Configuration Manager gere automaticamente o certificado**.

3. Continuar com o resto do fluxo de trabalho típico do SCUP para a importação de um catálogo de atualização de software de terceiros e, em seguida, implementar as atualizações para os clientes.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização in-loco do Windows 10
<!--1358500-->

O modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui, agora, outro grupo novo com as ações recomendadas para adicionar no caso do processo de atualização falha. Estas ações facilitam a resolução de problemas.

### <a name="new-groups-under-run-actions-on-failure"></a>Novos grupos em **executar ações em caso de falha**
- **Recolher registos**: Para recolher os registos do cliente, adicione passos neste grupo. 
    - Uma prática comum é copiar os ficheiros de registo para uma partilha de rede. Para estabelecer esta ligação, utilize o [ligar à pasta de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) passo. 
    - Para efetuar a operação de cópia, usar um utilitário ou um script personalizado com o [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [executar Script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript) passo.
    - Ficheiros a recolher podem incluir os seguintes registos:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Para obter mais informações no log e outros registos de configuração do Windows, consulte [ficheiros de registo de configuração do Windows](/windows/deployment/upgrade/log-files).
    - Para obter mais informações sobre registos de cliente do Configuration Manager, consulte [registos de cliente do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)
    - Para obter mais informações sobre smstslogpath e outras variáveis útil, consulte [variáveis incorporadas de sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables)

- **Executar as ferramentas de diagnóstico**: Para executar as ferramentas de diagnóstico adicionais, adicione passos neste grupo. Essas ferramentas devem ser automatizadas para recolher informações adicionais do sistema logo após a falha possível.
    - Uma dessas ferramentas é o Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico autónomo que pode utilizar para obter detalhes sobre o motivo pelo qual uma atualização do Windows 10 foi concluída com êxito.
         - No Configuration Manager, [criar um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para a ferramenta.
         - Adicionar uma [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo para este grupo da sequência de tarefas. Utilize o **pacote** opção para fazer referência a ferramenta. A seguinte cadeia de caracteres é um exemplo **linha de comandos**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace instalado com o cliente
<!--1357971-->

Agora, o ferramenta de visualização de registos de CMTrace é instalado automaticamente, juntamente com o cliente do Configuration Manager. Este é adicionado ao diretório de instalação do cliente, que, por predefinição, é `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> É a ferramenta CMTrace *não* automaticamente registado com o Windows para abrir a extensão de ficheiro. log.



## <a name="improvement-to-the-configuration-manager-console"></a>Melhoria na consola do Configuration Manager
<!--1358202--> Fizemos a melhoria seguinte na consola do Configuration Manager:

- Listas de dispositivos em ativos e compatibilidade, dispositivos, por predefinição apresentam agora o usuário atualmente conectado. Este valor é as mais atual a [estado do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). O valor será eliminado quando o usuário fizer Logoff. Se nenhum usuário está conectado, o valor está em branco. 

### <a name="known-issues"></a>Problemas conhecidos
Atualmente conectado no utilizador estiver em branco no nó dispositivos ou ao visualizar uma lista de dispositivos no nó coleções de dispositivos. Para contornar este problema, transfira este [SQL script](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Execute sp_BgbUpdateLiveData.sql no servidor de base de dados do site e, em seguida, reinicie os serviços smsexec e sms_notification_server no ponto de gestão.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Melhorias aos comentários de consola
<!--1357542--> Esta versão inclui as seguintes melhorias para o novo [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) mecanismo na consola do Configuration Manager:  

- A caixa de diálogo de comentários lembra agora as definições anteriores, por exemplo, as opções selecionadas e o seu endereço de e-mail.  

- Ele agora suporta comentários offline. Guarde os seus comentários a partir da consola e, em seguida, carregar para a Microsoft a partir de um sistema de ligação à internet. Utilize a nova ferramenta de carregador de comentários offline localizada na `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Para ver as opções de linha de comandos disponíveis e necessárias, execute a ferramenta com o `--help` opção. O sistema ligado precisa de aceder a **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problemas conhecidos
Ao usar **enviar um sorriso** ou **enviar comentários negativos** partir da consola num computador com ligação à internet, ele pode retornar com a seguinte mensagem: "Erro ao enviar comentários." Se clicar em **mais detalhes**, mostra o seguinte texto: `{"Message":""}`. Este erro é devido a um problema conhecido com a resposta do sistema de comentários de back-end. Pode ignorar o erro. Microsoft ainda receber seus comentários. (Se os detalhes de exibem uma mensagem diferente, utilize a opção de comentários de offline para repetir a enviar seus comentários num momento posterior.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias aos pontos de distribuição com PXE ativado
<!--1357580-->

Esta versão inclui as seguintes melhorias adicionais quando utiliza a opção para [ **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows** ](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points) num ponto de distribuição:  

- Regras de Firewall do Windows são criadas automaticamente no ponto de distribuição quando ativa esta opção  
- Melhorias ao registo de componentes



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Melhoria para o inventário de hardware para valores inteiros grandes
<!--1357880--> Inventário de hardware tem atualmente um limite de números inteiros maiores do que 4,294,967,296 (2 ^ 32). Este limite pode ser contatado para atributos, como tamanhos de disco rígido em bytes. O ponto de gestão não processa os valores de número inteiro acima desse limite, portanto, nenhum valor é armazenado na base de dados. Agora, nesta versão, o limite foi aumentado para 18,446,744,073,709,551,616 (2 ^ 64). 

Para uma propriedade com um valor que não é alterado, como o tamanho total do disco, poderá não ver de imediato o valor depois de atualizar o site. A maioria dos inventário de hardware é um relatório de delta. O cliente envia apenas valores que alterarem. Para contornar este comportamento, adicione outra propriedade para a mesma classe. Esta ação faz com que o cliente atualizar todas as propriedades na classe que foi alterado. 



## <a name="improvement-to-wsus-maintenance"></a>Melhoria para manutenção WSUS
<!--1357898-->

O Assistente de limpeza do WSUS agora recusa atualizações expiradas ou substituídas, de acordo com as regras de substituição. Estas regras são definidas em Propriedades de componente do ponto de atualização de software.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Selecione o site de nível superior, clique em **configurar componentes do Site** na faixa de opções e selecione **ponto de atualização de Software**.  

2. Mude para o **regras de substituição** separador. Ativar a opção para **Assistente de limpeza do WSUS executar**. Especifique o comportamento de substituição pretendido.  

3. Reveja o ficheiro Wsyncmgr log.



## <a name="improvement-to-support-for-cng-certificates"></a>Melhoria para o suporte para certificados CNG
<!--1357314--> Nesta versão, utilize [certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview) para as seguintes funções de servidor adicionais de suporte HTTPS:  
- Ponto de registo de certificados, incluindo o servidor do NDES com o módulo de política do Configuration Manager



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
