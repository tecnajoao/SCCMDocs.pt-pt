---
title: Pré-visualização técnica 1805
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades disponíveis na versão 1805 Configuration Manager Technical Preview.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 24cb16ab17475bdd063949c7e3e2961b53341026
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/21/2018
ms.locfileid: "34450156"
---
# <a name="capabilities-in-technical-preview-1805-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1805 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview para o Configuration Manager, versão 1805. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica. 

Reveja o [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Criar uma implementação faseada fases configurados manual de uma sequência de tarefas
<!--1358148--> Agora, pode [criar uma implementação faseada](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) fases configurados manual de uma sequência de tarefas. Pode adicionar até 10 fases adicionais do **fases** separador do assistente criar implementação fases. 


### <a name="try-it-out"></a>Experimente!
Siga as instruções para criar uma implementação faseada em que configura manualmente todas as fases. Enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu. 

1. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Faça duplo clique na sequência de tarefas existente e selecione **criar implementação fases**.  

3. No **geral** separador, atribua a implementação faseada um nome, descrição (opcional) e selecione **configurar manualmente todas as fases**.  

4. No **fases** separador, clique em **adicionar**.  

5. Especifique um **nome** para a fase e, em seguida, navegue para o destino **fase coleção**.  

6. No **fase definições** separador, escolha uma opção para cada uma das definições de agendamento e selecione **seguinte** quando concluir.  

    - Critérios de êxito da fase anterior (esta opção está desativada para a primeira fase.)
        - **Percentagem de êxito da implementação**: Especifique a percentagem de dispositivos que concluem com êxito a implementação para os critérios de êxito da fase anterior.  

    - Condições para iniciar esta fase da implementação, após o êxito da fase anterior  
        - **Iniciar automaticamente nesta fase após um período de diferimento por (em dias)**: Escolha o número de dias a aguardar antes de iniciar a fase seguinte após o êxito da fase anterior. 
        - **Iniciar manualmente a nesta fase da implementação**: Não iniciar esta fase automaticamente após êxito da fase anterior.  

    - Depois de um dispositivo é direcionado, instalar o software
        - **Logo que possível**: Define o prazo de instalação no dispositivo, assim que o dispositivo é visado.
        - **Prazo de tempo (em relação à hora de dispositivo é direcionado)**: Define o prazo de instalação de um determinado número de dias após o dispositivo é direcionado.  
     
7. Conclua o Assistente de definições de fase.

8. No **fases** separador do assistente criar implementação fases que agora pode adicionar, remover, reordenar ou editar as fases para esta implementação.  

9. Conclua o Assistente de implementação de fases criar.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte de ponto de distribuição de nuvem do Azure Resource Manager
<!--1322209--> Quando criar uma instância do [ponto de distribuição de nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure), o assistente fornece agora a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementar um ponto de distribuição na nuvem com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos de nuvem necessário. Esta implementação modernized não necessita que o certificado de gestão do Azure clássico.  

O Assistente de ponto de distribuição de nuvem fornece ainda a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, recomendamos que utilize o modelo de implementação Azure Resource Manager para todos os novos pontos de distribuição de nuvem. Se for possível, volte a implementar pontos de distribuição existente na nuvem através do Resource Manager.

O Configuration Manager não migra pontos de distribuição de nuvem clássico existentes para o modelo de implementação Azure Resource Manager. Criar nuvem nova pontos de distribuição com implementações do Azure Resource Manager e, em seguida, remova pontos de distribuição de nuvem clássico. 

> [!IMPORTANT]  
> Esta capacidade não ative o suporte para fornecedores de serviços de nuvem do Azure (CSP). A implementação de ponto de distribuição de nuvem com o Azure Resource Manager continua a utilizar o serviço de nuvem clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Pré-requisitos  
- Integração com [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Não é necessária a deteção de utilizadores do Azure AD.  

- O mesmo [requisitos para um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_PrereqsCloudDP), exceto o certificado de gestão do Azure.  


### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho, expanda **serviços em nuvem**e selecione **pontos de distribuição de nuvem**. Clique em **criar ponto de distribuição na nuvem** no Friso.   

2. No **geral** página, selecione **implementação Azure Resource Manager**. Clique em **sessão** para autenticar com uma conta de administrador de subscrição do Azure. O Assistente de auto-preenche os campos restantes das informações de subscrição do Azure AD armazenados durante o pré-requisito de integração. Se tiver várias subscrições, selecione a subscrição pretendida a utilizar. Clique em **Seguinte**.  

3. No **definições** , indique o servidor de PKI **ficheiro de certificado** como habitualmente. Este certificado define o ponto de distribuição de nuvem **FQDN de serviço** utilizados pelo Azure. Selecione o **região**e, em seguida, selecione uma opção de grupo de recursos para qualquer **criar nova** ou **utilizar existente**. Introduza o nome do novo grupo de recursos ou selecione um grupo de recursos existente na lista pendente.  

4. Conclua o assistente.  

> [!NOTE]  
> Para o Azure AD selecionado aplicação de servidor, o Azure atribui a subscrição **contribuinte** permissão.  

Monitorizar o progresso da implementação de serviço com **cloudmgr.log** no ponto de ligação de serviço.



## <a name="take-actions-based-on-management-insights"></a>Executar ações com base nas informações de gestão
<!--1357930--> Alguns [insights gestão](/sccm/core/servers/manage/management-insights) tem agora a opção de efetuar uma ação. Consoante a regra, esta ação exhibits um dos seguintes comportamentos:  

- Navegar automaticamente na consola para o nó em que pode qualquer ação adicional. Por exemplo, se as informações de gestão recomenda alterar uma definição de cliente, efetuar ação navega para o nó de definições de cliente. -Pode qualquer ação adicional ao modificar a predefinição ou um objeto de definições personalizadas de cliente.  

- Navegue para uma vista filtrada com base numa consulta. Por exemplo, efetuar a ação na regra coleções vazias mostra apenas a estes coleções na lista de coleções. Aqui, pode qualquer ação adicional, tal como eliminar uma coleção ou modificar as suas regras de associação.  

As seguintes regras de informações de gestão têm ações nesta versão:
- Segurança
    - Versões de cliente antimalware não suportado
- Centro de software
    - Utilize a versão nova do Centro de Software
- Aplicações
    - Aplicações sem implementações
- Gestão simplificada
    - Versões de cliente não CB
- Coleções
    - Coleções vazias 
- Serviços cloud
    - Atualizar clientes para a versão mais recente do Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Transição dispositivo configuração carga de trabalho utilizando a gestão de coadministrador do Intune
<!--1357903-->

Pode agora efetuar a transição carga de trabalho de configuração dispositivo do Configuration Manager para o Intune depois de ativar a gestão conjunta. Transição esta carga de trabalho permite-lhe utilizar o Intune para implementar MDM políticas, ao continuar a utilizar o Configuration Manager para implementar aplicações. 

A transição esta carga de trabalho, vá para a página de propriedades de gestão conjunta e desloque o cursor de controlo do Configuration Manager para **piloto** ou **todos os**. Para obter mais informações, consulte [conjunta management para Windows 10 dispositivos](/sccm/core/clients/manage/co-management-overview).

> [!Note]  
> Mover esta carga de trabalho também move o **acesso a recursos** e **Endpoint Protection** cargas de trabalho, que são um subconjunto da carga de trabalho de configuração do dispositivo.

Quando efetuar a transição esta carga de trabalho, ainda pode implementar as definições do Configuration Manager para dispositivos geridos conjuntamente, apesar do Intune é a autoridade de configuração do dispositivo. Esta exceção pode ser utilizada para configurar as definições que são necessárias pela sua organização, mas ainda não está disponível no Intune. Especifique esta exceção uma linha de base de configuração do Configuration Manager. Ativar a opção para **sempre aplicar esta linha de base, mesmo para clientes conjuntamente geridos** ao criar a linha de base ou no **geral** separador das propriedades de uma linha de base existente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ative pontos de distribuição para utilizar o controlo de congestionamento de rede
<!--1358112-->

Windows baixa Extra atraso em segundo plano transporte (LEDBAT) é uma funcionalidade do Windows Server para ajudar a gerir as transferências de rede em segundo plano. Para pontos de distribuição em execução em versões suportadas do Windows Server, pode ativar uma opção ajudar a ajustar o tráfego de rede. Os clientes utilizam apenas a largura de banda de rede quando estiver disponível. 

Para obter mais informações sobre LEDBAT do Windows, consulte o [avanços de transporte do novo](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) blogue.


### <a name="prerequisites"></a>Pré-requisitos
- Um ponto de distribuição no Windows Server, versão 1709.  

- Um dispositivo de cliente em execução, pelo menos, Windows 10, versão 1607.


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Selecione o **pontos de distribuição** nós. Selecione o ponto de distribuição de destino e clique em **propriedades** no Friso.  

2. No **geral** separador, ative a opção para **ajustar a velocidade de transferência para utilizar a largura de banda de rede não utilizados (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Dashboard de gestão de nuvem
<!--1358461--> A nova **dashboard de gestão de nuvem** fornece uma vista centralizada para utilização do gateway (CMG) de gestão de nuvem. Quando o site é integrado com o Azure AD, também apresenta os dados sobre dispositivos e utilizadores de nuvem.  

Captura de ecrã seguinte é uma parte do dashboard de gestão de nuvem que mostra dois os mosaicos disponíveis:  
![Tráfego de CMG de mosaicos do dashboard do gestão de nuvem e de clientes online atuais](media/1358461-cmg-dashboard.png)

Esta funcionalidade também inclui o **analisador da ligação de CMG** para a verificação em tempo real ajudar a resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através da ligação de CMG aponte para quaisquer pontos de gestão que permitam o tráfego CMG.


### <a name="prerequisites"></a>Pré-requisitos
- Um Active Directory [gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) utilizado por clientes baseados na internet.  

- Simplificar o site para [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão de nuvem.  


### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

#### <a name="cloud-management-dashboard"></a>Dashboard de gestão de nuvem

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho. Selecione o **gestão de nuvem** nós e ver o dashboard os mosaicos.  

#### <a name="cmg-connection-analyzer"></a>Analisador da ligação de CMG

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços em nuvem** e selecione **gateway de gestão de nuvem**.  

2. Selecione a instância CMG de destino e, em seguida, selecione **analisador da ligação** no Friso.  

3. Na janela de analisador da ligação de CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Utilizador do Azure AD**: Utilize esta opção para simular o mesmo que uma identidade de utilizador baseadas na nuvem com sessão iniciado num dispositivo do Azure Windows 10 associados a um AD de comunicação. Clique em **sessão** em segurança, introduza as credenciais para esta conta de utilizador do Azure AD.  

     2. **Certificado de cliente**: Utilize esta opção para simular a comunicação o mesmo que um cliente de Configuration Manager com um [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Clique em **iniciar** para iniciar a análise. Os resultados são apresentados na janela do analisador. Selecione uma entrada para ver mais detalhes no campo de descrição.  



## <a name="cmpivot"></a>CMPivot
<!--1358456--> O Configuration Manager sempre forneceu um arquivo centralizado grande de dados de dispositivo, os clientes utilizam para efeitos de relatórios. No entanto, a que dados são apenas como boas como a última vez que foi recolhido a partir de clientes. 

CMPivot é um utilitário de na consola novo que fornece acesso ao Estado em tempo real dos dispositivos no seu ambiente. Imediatamente executa uma consulta em todos os dispositivos atualmente ligados na coleção de destino e devolve os resultados. Pode filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real a partir de clientes online, pode mais rapidamente responder a perguntas de negócio, resolver problemas e responder a incidentes de segurança.

Por exemplo, no [mitigar vulnerabilidades de canal de lado de execução speculative](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Pode utilizar CMPivot para consultar rapidamente nas informações de BIOS do sistema e localizar os clientes que não estejam em conformidade. 

Nesta captura de ecrã, CMPivot apresenta duas versões de BIOS separadas com uma contagem de dispositivos de cada. Pode utilizar este exemplo de consulta quando experimentar CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Janela de CMPivot com exemplo fro consultar BIOSVersion](media/1358456-cmpivot-biosversion.png)

Pode clicar na contagem de dispositivos para desagregar para ver os dispositivos específicos. Quando se apresenta dispositivos no CMPivot, pode utilizar para um dispositivo com o botão direito e selecione o seguinte [ações de notificação de cliente](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode):
- Executar Script
- Controlo Remoto
- Explorador de recursos

Ao clicar num dispositivo específico, também pode dinâmico a vista do dispositivo específico a um dos seguintes atributos:
- Comandos de início automático
- Produtos instalados
- Processos
- Serviços
- Utilizadores
- Ligações ativas
- Atualizações em falta

### <a name="prerequisites"></a>Pré-requisitos
- Os clientes de destino tem de ser atualizados para a versão mais recente.  

- O administrador do Configuration Manager necessita de permissões para executar scripts. Para obter mais informações, consulte [funções de segurança para os scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione **coleções de dispositivos**. Selecione uma coleção de destino e clique em **iniciar CMPivot** no friso para iniciar a ferramenta.  

2. A interface fornece mais informações sobre como utilizar a ferramenta. 
     - Manualmente pode introduzir as cadeias de consulta na parte superior, ou clique nas hiperligações na documentação em linha.
     - Clique do **entidades** adicioná-lo para a cadeia de consulta. 
     - As ligações para **operadores de tabela**, **funções de agregação**, e **escalar funções** abrir documentação de referência de linguagem do browser. CMPivot utiliza a mesma linguagem de consulta como [Log Analytics do Azure](https://docs.loganalytics.io/docs/Language-Reference/Change-log).



## <a name="improved-secure-client-communications"></a>Melhorado comunicações de cliente seguras
<!--1356889,1358228,1358460--> Utilizar a comunicação HTTPS é recomendada para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido ao overhead inerente à gestão de certificados PKI. A introdução do Azure Active Directory integração (Azure AD) reduz algumas, mas não todos os requisitos de certificado. 

Esta versão inclui melhoramentos à forma como os clientes comunicam com sistemas de sites. Existem dois objetivos principais para estas melhorias:  

- Pode proteger a comunicação de cliente sem a necessidade de certificados de autenticação de servidor PKI.  

- Os clientes podem aceder de forma segura conteúdos dos pontos de distribuição sem a necessidade de uma conta de acesso à rede.  

> [!Note]  
> Os certificados PKI são ainda uma opção válida para clientes que quiser utilizá-la.  


### <a name="bkmk_token"></a> Cenários
Os seguintes cenários beneficiam estas melhorias:  

#### <a name="bkmk_token1"></a> Cenário 1: Cliente para ponto de gestão
<!--1356889-->
[Dispositivos associados ao Azure AD](/azure/active-directory/device-management-introduction#azure-ad-joined-devices) pode comunicar através de um gateway de gestão de nuvem (CMG) com um ponto de gestão configurado para HTTP. O servidor de site gera um certificado para o ponto de gestão, permitindo que comunicar através de um canal seguro.   

> [!Note]  
> Este comportamento é alterado do Configuration Manager versão atual do ramo 1802, que necessita de um ponto de gestão ativado para HTTPS para este cenário. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

#### <a name="bkmk_token2"></a> Cenário 2: Cliente para ponto de distribuição
<!--1358228--> Grupo de trabalho ou do Azure AD associados a um cliente pode transferir o conteúdo através de um canal seguro de um ponto de distribuição configurado para HTTP.   

#### <a name="bkmk_token3"></a> Identidade de dispositivo do cenário 3 do Azure AD 
<!--1358460--> Associado a um Azure AD ou [dispositivos do Azure AD híbrido](/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um Azure AD utilizador com sessão iniciada pode comunicar de forma segura com o respetivo site atribuído. Agora é suficiente para autenticar com o ponto de gestão e CMG a identidade de dispositivo baseado na nuvem.  


### <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gestão configurado para ligações de cliente HTTP. Defina esta opção no **geral** separador de propriedades de função do sistema de sites.  

- Um ponto de distribuição configurado para ligações de cliente HTTP. Defina esta opção no **geral** separador de propriedades de função do sistema de sites. Não ative a opção de **permitir a ligação anónima dos clientes**.  

- Um gateway de gestão de nuvem.  

- Carregar o site para o Azure AD para gestão de nuvem.  

    - Se já tiver cumprido nesta pré-requisitos para o seu site, terá de atualizar a aplicação do Azure AD. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços em nuvem**e selecione **do Azure Active Directory inquilinos**. Selecione o inquilino do Azure AD, selecione a aplicação web no **aplicações** painel e, em seguida, clique em **atualizar a definição de aplicação** no Friso.  

- Um cliente com o Windows 10 versão 1803 e associados para o Azure AD. (Este requisito é tecnicamente apenas para [cenário 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Selecione o site e clique em **propriedades** no Friso.  

2. Mudar para o **comunicação com o computador cliente** separador. Selecione a opção para **HTTPS ou HTTP** e, em seguida, ative a nova opção **sistemas de sites de certificados gerados-utilize o Gestor de configuração para HTTP**.  

Consulte o anteriormente [lista dos cenários](#bkmk_token) para validar.

> [!Tip]
> Nesta versão, aguarde até 30 minutos para o ponto de gestão receber e configurar o novo certificado a partir do site.

Pode ver estes certificados, na consola do Configuration Manager. Vá para o **administração** área de trabalho, expanda **segurança**e selecione o **certificados** nó. Procure o **SMS emitir** certificado de raiz, bem como os certificados de função de servidor de site emitidos por raiz emitir de SMS.


### <a name="known-issues"></a>Problemas conhecidos
- O utilizador não é possível ver no Centro de Software quaisquer aplicações direcionadas para-los como disponível.  

- Cenários de implementação de SO requerem ainda a conta de acesso de rede.  

- Rapidamente e repetidamente ativar e desativar a opção de **sistemas de sites de certificados gerados-utilize o Gestor de configuração para HTTP** pode fazer com que o certificado para o enlace não está corretamente para as funções de sistema de sites. Não existem certificados emitidos pelo certificado de "Emitir de SMS" estão vinculados a um site no Windows Server informações de serviços Internet (IIS). Para contornar este problema, elimine todos os certificados emitidos por "Emitir de SMS" do **SMS** certificado loja do Windows e, em seguida, reinicie o serviço smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Melhoramentos para ativar o suporte de atualização de software de terceiros
<!--1357605--> Como resultado da sua comentários do UserVoice no [suporte de atualização de software de terceiros](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), esta versão ainda mais itera na integração com o System Center atualizações publicador (SCUP). Pré-visualização técnica do Configuration Manager [versão 1803](/sccm/core/get-started/capabilities-in-technical-preview-1803#enable-third-party-software-update-support-on-clients) foi adicionada a capacidade para ler o certificado do WSUS para atualizações de terceiros e, em seguida, implementar esse certificado em clientes. No entanto, pode ainda necessários para utilizar a ferramenta SCUP para criar e gerir o certificado de assinatura de atualizações de software de terceiros.

Nesta versão, pode ativar o site do Configuration Manager configurar automaticamente o certificado. O site comunica com o WSUS para gerar um certificado para esta finalidade. O Configuration Manager, em seguida, continua a implementar se o certificado em clientes. Este iteração remove a necessidade de utilizar a ferramenta SCUP para criar e gerir o certificado. 

Para obter mais informações sobre a utilização geral da ferramenta SCUP, consulte [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

### <a name="prerequisites"></a>Pré-requisitos
- Ativar e implementar a definição de cliente **ativar atualizações de software de terceiros** no **atualizações de Software** grupo.
- Se o WSUS é num servidor separado do ponto de atualização de software, terá de efetuar uma das seguintes opções num servidor remoto do WSUS:
    - Ativar o serviço registo remoto no Windows  
    ou
    - Na chave do registo `HKLM\Software\Microsoft\Update Services\Server\Setup`, criar um novo DWORD denominado **EnableSelfSignedCertificates** com um valor de `1`. 

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Selecione o site de nível superior, clique em **configurar componentes do Site** no Friso e selecione **ponto de atualização de Software**.  

2. Mudar para o **atualizações de terceiros** separador. Selecione a opção para **ativar atualizações de software de terceiros**e, em seguida, selecione a opção para **do Configuration Manager gere automaticamente o certificado**.

3. Continuar com o resto do fluxo de trabalho SCUP típico para importar um catálogo de atualização de software de terceiros e, em seguida, implementar as atualizações para os clientes.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização no local do Windows 10
<!--1358500-->

O modelo de sequência de tarefas predefinido para a atualização do Windows 10 no local agora inclui a outro grupo novo com as ações recomendadas para adicionar no caso de falha o processo de atualização. Estas ações facilitam a resolução de problemas.

### <a name="new-groups-under-run-actions-on-failure"></a>Novos grupos em **executar ações em caso de falha**
- **Recolher registos**: Para recolher registos de cliente, adicione os passos neste grupo. 
    - É uma prática comum copiar os ficheiros de registo para uma partilha de rede. Para estabelecer esta ligação, utilize o [ligar à pasta de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) passo. 
    - Para efetuar a operação de cópia, utilize um script personalizado ou o utilitário com uma o [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [executar Script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript) passo.
    - Ficheiros a recolher podem incluir os seguintes registos:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Para obter mais informações sobre os ficheiros setupact.log e outros registos de configuração do Windows, consulte [ficheiros de registo de configuração do Windows](/windows/deployment/upgrade/log-files).
    - Para obter mais informações sobre os registos de cliente do Configuration Manager, consulte [registos de cliente do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)
    - Para obter mais informações sobre smstslogpath e outras variáveis útil, consulte [variáveis incorporadas de sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables)

- **Executar as ferramentas de diagnóstico**: Para executar as ferramentas de diagnóstico adicionais, adicione os passos neste grupo. Devem ser automatizadas estas ferramentas para recolher informações adicionais do sistema como logo após a falha quanto possível.
    - Uma ferramenta deste tipo é Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico autónoma que pode utilizar para obter detalhes sobre o motivo pelo qual uma atualização do Windows 10 foi bem-sucedida.
         - No Configuration Manager, [criar um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para a ferramenta.
         - Adicionar um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo para este grupo de sequência de tarefas. Utilize o **pacote** opção para fazer referência a ferramenta. A seguinte cadeia é um exemplo **linha de comandos**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace instalado com o cliente
<!--1357971-->

Agora, o ferramenta de visualização de registos de CMTrace é instalado automaticamente, juntamente com o cliente do Configuration Manager. É adicionado para o diretório de instalação do cliente, que, por predefinição, é `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace é *não* automaticamente registado com o Windows para abrir a extensão de ficheiro. log.



## <a name="improvement-to-the-configuration-manager-console"></a>Melhoria da consola do Configuration Manager
<!--1358202--> Fizemos como a melhoria seguinte na consola do Configuration Manager:

- Apresenta uma lista de dispositivos em ativos e compatibilidade, dispositivos, agora por predefinição apresenta o utilizador atualmente com sessão iniciado. Este valor é como atual como o [estado do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). O valor será eliminado quando o utilizador termina a sessão. Se nenhum utilizador é iniciado, o valor está em branco. 

### <a name="known-issues"></a>Problemas conhecidos
Atualmente registados no utilizador valor está em branco no nó dispositivos ou ao visualizar uma lista de dispositivos do nó coleções de dispositivos. Para contornar este problema, transferir este [SQL script](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Execute sp_BgbUpdateLiveData.sql no servidor de base de dados do site e, em seguida, reinicie os serviços smsexec e sms_notification_server no ponto de gestão.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Melhoramentos a comentários de consola
<!--1357542--> Esta versão inclui os seguintes melhoramentos para o novo [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) mecanismo na consola do Configuration Manager:  

- A caixa de diálogo de comentários memorizou agora as definições anteriores, tais como as opções selecionadas e o seu endereço de e-mail.  

- Agora suporta comentários offline. Guarde os seus comentários a partir da consola e, em seguida, carregue para a Microsoft a partir de um sistema ligado à internet. Utilize a ferramenta de /carregador comentários offline novo localizada na `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Para ver as opções da linha de comandos disponíveis e necessárias, execute a ferramenta com o `--help` opção. O sistema ligado precisa de acesso à **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problemas conhecidos
Quando utilizar **enviar um smile** ou **enviar um negativos** partir da consola num computador com ligação à internet, podem devolver com a seguinte mensagem: "Erro ao enviar comentários." Se clicar em **mais detalhes**, mostra o seguinte texto: `{"Message":""}`. Este erro é devido a um problema conhecido com a resposta do sistema de comentários do back-end. Pode ignorar o erro. Microsoft recebeu ainda os seus comentários. (Se os detalhes apresentam uma mensagem diferente, utilize a opção de comentários offline para repetir a enviar os seus comentários numa altura posterior.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhoramentos para pontos de distribuição com PXE ativado
<!--1357580-->

Esta versão inclui os seguintes melhoramentos adicionais ao utilizar a opção de [ **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows** ](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points) num ponto de distribuição:  

- Regras de Firewall do Windows são criadas automaticamente no ponto de distribuição quando a ativação desta opção  
- Melhoramentos ao registo de componentes



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Melhoria do inventário de hardware para os valores de número inteiro grande
<!--1357880--> Inventário de hardware tem atualmente um limite de números inteiros superiores 4,294,967,296 (2 ^ 32). Este limite pode ser contactado para atributos como tamanhos de disco rígido em bytes. O ponto de gestão não processar valores inteiros acima este limite, deste modo, nenhum valor é armazenado na base de dados. Agora nesta versão, o limite é aumentado para 18,446,744,073,709,551,616 (2 ^ 64). 

Para uma propriedade com um valor que não irá alterar, como o tamanho total do disco, poderá não imediatamente ver o valor após a atualização do site. A maioria das inventário de hardware é um relatório de diferenças. O cliente envia apenas valores alterarem. Para contornar este comportamento, adicione outra propriedade à mesma classe. Esta ação faz com que o cliente atualizar todas as propriedades na classe que foi alterado. 



## <a name="improvement-to-wsus-maintenance"></a>Melhoria da manutenção do WSUS
<!--1357898-->

O Assistente de limpeza do WSUS agora recusar atualizações que estão expiradas ou substituídas, de acordo com as regras de substituição. Estas regras estão definidas em Propriedades de componente de ponto de atualização de software.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Selecione o site de nível superior, clique em **configurar componentes do Site** no Friso e selecione **ponto de atualização de Software**.  

2. Mudar para o **regras de substituição** separador. Ativar a opção para **Assistente de limpeza do WSUS executar**. Especifique o comportamento de substituição pretendido.  

3. Consulte o ficheiro WSyncMgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Melhoria para suportar em certificados CNG
<!--1357314--> Nesta versão, utilize [certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview) para as seguintes funções de servidor adicionais ativadas por HTTPS:  
- Ponto de registo de certificados, incluindo o servidor do NDES com o módulo de política do Configuration Manager



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
