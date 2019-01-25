---
title: Pré-visualização técnica 1807
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis no Configuration Manager versão de ramificação de pré-visualização técnica 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c443f561392f95d875a681319ebb9db4ff3fb66b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898482"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Recursos do Configuration Manager technical preview versão 1807 

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no technical preview no Configuration Manager, versão 1807. Instale esta versão para atualizar e adicionar novas funcionalidades para o seu site de pré-visualização técnica. 

Reveja os [pré-visualização técnica](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problemas conhecidos 

### <a name="ki_o365"></a> Problemas com atualizações de software do Office 365
<!--521365--> Se gerir atualizações do Office 365 com as versões do ramo de pré-visualização técnica 1806 e 1806.2, eles podem não conseguir instalar nos clientes. 

#### <a name="workaround"></a>Solução
- Elimine pacotes de implementação existentes e grupos de atualização de software para o Office 365.  

- A partir de 31 de Julho de 2018, a sincronização do Office 365 atualizações de software e implementar apenas as atualizações mais recentes.  



</br>

**As secções seguintes descrevem os novos recursos para experimentar o nesta versão:**  


## <a name="bkmk_hub"></a> Hub de Comunidade
<!--1357766-->

O Hub de Comunidade é uma localização centralizada para objetos do Configuration Manager úteis de partilha com outras pessoas. Ver a nova **Comunidade** área de trabalho na consola do Configuration Manager e selecione o **Hub** nó. Utilize o Hub de Comunidade para transferir os seguintes tipos de objetos do Configuration Manager: 
- Scripts
- Itens de configuração

![Consola do Configuration Manager, área de trabalho da Comunidade, nó de Hub](media/1357766-hub.png)

Para ver mais detalhes sobre um item disponível, clique no mesmo no hub. A partir da página de detalhes, clique em **transferir** para adquirir o item. Ao baixar um item a partir do hub, é automaticamente adicionado ao seu site. 

![Página de detalhes da consola do Configuration Manager, área de trabalho da Comunidade, nó de Hub,](media/1357766-hub-details.png)

O **Comunidade** área de trabalho também inclui os seguintes nós:

- **Documentação**: Apresenta o Gestor de configuração [biblioteca de documentação](https://docs.microsoft.com/sccm/)  

- **Comentários**: Apresenta o Gestor de configuração [site do UserVoice](https://configurationmanager.uservoice.com/)  


### <a name="prerequisites"></a>Pré-requisitos

- Utilize a consola do Configuration Manager num sistema operacional cliente.  

    - Em alternativa, mas não recomendado: num servidor de sistema operacional, desativar [do Internet Explorer: Configuração de segurança avançada](https://go.microsoft.com/fwlink/?LinkId=253461).  

- O computador com a consola requer acesso à internet e a conectividade com os seguintes sites:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problema conhecido

Contribuir itens para o hub não está atualmente disponível nesta versão. 



## <a name="bkmk_osd"></a> Especifique a unidade para a manutenção da imagem de SO offline  
<!--1358924-->

Com base no seu [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive), agora, especifique a unidade que o Configuration Manager utiliza durante a manutenção offline de imagens do sistema operacional. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários, para que esta opção dá-lhe flexibilidade para selecionar a unidade a utilizar. 


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com suas idéias sobre a funcionalidade.

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. No Friso, clique em **configurar componentes do Site** e selecione **ponto de atualização de Software**.  

2. Mude para o **fornecimento Offline** separador e especificar a opção para **uma unidade local a ser utilizado pelo fornecimento offline de imagens**.  

Por predefinição, esta definição é **automática**. Com este valor, o Configuration Manager seleciona a unidade onde está instalado. 

Durante a manutenção offline, o Configuration Manager armazena ficheiros temporários na pasta, `<drive>:\ConfigMgr_OfflineImageServicing`. Ele também monta as imagens do sistema operacional nesta pasta. 

Reveja os **OfflineServicingMgr.log** ficheiro de registo. 



## <a name="bkmk_comgmt"></a> Atividade de sincronização de dispositivos cogeridos do Intune
<!--1358565-->

Apresentar na consola do Configuration Manager se um dispositivo cogerido está ativo com o Microsoft Intune. Este estado baseia-se a dados a partir da [armazém de dados do Intune](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). O **estado do cliente** dashboard na mostra de consola do Configuration Manager **clientes Inativos com o Intune**. Esta nova categoria destina-se a dispositivos cogeridos que estão inativos com o Configuration Manager, mas foram sincronizados com o serviço do Intune na última semana.


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com suas idéias sobre a funcionalidade.

Se já tiver configurado a seu site para a cogestão: 

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó. Clique em **propriedades** na faixa de opções.  

2. Mude para o **relatórios** separador. Clique em **sessão** e autenticar. Em seguida, clique em **atualização** para ativar as permissões de leitura para o armazém de dados do Intune.  

3. Depois das sincronizações de site com o Intune, vá para o **monitorização** área de trabalho e selecione o **estado do cliente** nó. Na **estado geral do cliente** secção, consulte a linha para **clientes Inativos com o Intune**.  

Para obter mais informações sobre como ativar a cogestão, consulte [cogestão para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).



## <a name="bkmk_app-repair"></a> Aplicativos de reparação
<!--1357866-->

Com base no seu [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application), agora, especifique uma linha de comando de reparo para tipos de implementação do Windows Installer e o instalador de Script. 


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com suas idéias sobre a funcionalidade.

1. Na consola do Configuration Manager, abra as propriedades de um tipo de implementação do Windows Installer ou instalador de Script.  

2. Mude para o **programas** separador. Especifique a **programa de reparação** comando.  

3. Implemente a aplicação. Sobre o **definições de implementação** separador da implementação, ative a opção para **permitir que os utilizadores finais tentam reparar esta aplicação**.  


### <a name="known-issue"></a>Problema conhecido

O novo botão no Centro de Software para que os usuários **reparação** a aplicação não está visível nesta versão.  



## <a name="bkmk_email-approve"></a> Aprovar pedidos de aplicações através de e-mail
<!--1321550-->

Configure notificações por e-mail para pedidos de aprovação de aplicações. Quando um utilizador solicita uma aplicação, receberá uma mensagem de e-mail. Clique em ligações no e-mail para aprovar ou negar o pedido, sem a necessidade de consola do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

#### <a name="to-send-email-notifications"></a>Enviar notificações por e-mail
- Ativar a [funcionalidade opcional](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **aprovar pedidos de aplicações para utilizadores por dispositivo**.  

- Configurar [notificação por e-mail para alertas](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Para aprovar ou recusar pedidos de e-mail
Se não configurar estes pré-requisitos, o site envia notificações por e-mail para pedidos de aplicações sem ligações para aprovar ou negar o pedido.  

- Nas propriedades do site, **ativar o ponto final REST para todas as funções de fornecedores neste site e permitir o tráfego de gateway de gestão de nuvem do Configuration Manager**. Para obter mais informações, consulte [acesso a dados do ponto de extremidade OData](/sccm/core/get-started/capabilities-in-technical-preview-1612#odata-endpoint-data-access).  

    - Reinicie o serviço SMS_EXEC depois de ativar o ponto final REST

- [Gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Carregar o site para [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão na Cloud**  

    - Ativar [deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Configure manualmente as seguintes definições para esta aplicação nativa no Azure AD:  

        - **URI de redirecionamento**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Utilize o nome de domínio completamente qualificado (FQDN) do serviço de gateway (CMG) de gestão na cloud, por exemplo, GraniteFalls.Contoso.com.   

        - **Manifesto**: defina **oauth2AllowImplicitFlow** como true: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com suas idéias sobre a funcionalidade.

1. Na consola do Configuration Manager, implemente uma aplicação como disponível para uma coleção de utilizadores. Sobre o **definições de implementação** página, ativá-la para aprovação. Em seguida, introduza um *único* endereço de e-mail para receber a notificação.  

     > [!Note]  
     > Qualquer pessoa na sua organização do Azure AD que recebe o e-mail pode aprovar o pedido. Não reencaminhe o e-mail para outras pessoas, a menos que deseja que eles para tomar medidas.  

2. Como um utilizador, solicite a aplicação no Centro de Software.  

3. Receber uma notificação por e-mail semelhante ao seguinte exemplo:  

![Notificação de e-mail de exemplo para aprovação de aplicação](media/1321550-email.png)

> [!Note]  
> O link para aprovar ou recusar destina-se a utilização de uma única vez. Por exemplo, configurar um alias de grupo para receber notificações. MB aprova o pedido. Agora, Bruce não é possível negar o pedido.  



## <a name="bkmk_script"></a> Melhoria à saída do script
<!--1236459-->

Agora pode ver a saída do script detalhadas no formato JSON não processado ou não estruturado. Essa formatação torna a saída mais fácil de ler e analisar. Se o script retorna texto formatado em JSON válido, em seguida, veja a saída detalhada dado **saída JSON** ou **saída brutos**. Caso contrário, a única opção é **saída de Script**. 

#### <a name="example-script-output-is-valid-json"></a>Exemplo: Saída do script é um JSON válido
Comando: `$PSVersionTable.PSVersion`  

Saída:  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Exemplo: Saída do script não é um JSON válido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

Saída:  
```
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Experimente!

Experimente concluir as tarefas. Em seguida, envie [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) com suas idéias sobre a funcionalidade.

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione o **coleções de dispositivos** nó. Uma coleção com o botão direito e selecione **executar Script**. Para obter mais informações sobre como criar e executar scripts, consulte [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).  

2. Execute um script na coleção de destino.  

3. Sobre o **monitorização de estado de Script** página do Assistente para executar o Script, selecione a **resumo** separador na parte inferior. Alterar as duas listas de lista pendente na parte superior para **saída de Script** e **tabela de dados**. Em seguida, faça duplo clique na linha de resultados para abrir o **detalhada saída** caixa de diálogo.  

4. Sobre o **monitorização de estado do Script** página do Assistente para executar o Script, selecione a **detalhes da execução** separador na parte inferior. Faça duplo clique numa linha de resultados para abrir a caixa de diálogo de saída detalhada desse dispositivo.  



## <a name="bkmk_3pupdate"></a> Melhoria para atualizações de software de terceiros
<!--1358714-->

Agora, pode modificar as propriedades de catálogos personalizados.

Para obter mais informações, consulte [suportam de atualizações de software de terceiros para catálogos personalizados](/sccm/core/get-started/capabilities-in-technical-preview-1806-2#bkmk_3pupdate).



## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [pré-visualização técnica](/sccm/core/get-started/technical-preview).    

Para obter mais informações sobre as ramificações diferentes do Configuration Manager, consulte [o ramo do Configuration Manager devo utilizar?](/sccm/core/understand/which-branch-should-i-use)