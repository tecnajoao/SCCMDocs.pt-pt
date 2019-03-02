---
title: Versões Technical preview
titleSuffix: Configuration Manager
description: Saiba mais sobre o ramo de pré-visualização técnica a testarem novas funcionalidades e capacidades no Configuration Manager.
ms.date: 02/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9dee0aa39454d41f217cbe646845bf42076d3af
ms.sourcegitcommit: 56ec6933cf7bfc93842f55835ad336ee3a1c6ab5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57211623"
---
# <a name="technical-preview-for-configuration-manager"></a>Pré-visualização técnica do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo fornece detalhes sobre o ramo mensal de pré-visualização técnica do Configuration Manager. O technical preview introduz novas funcionalidades que a Microsoft está trabalhando. Ele introduz novas funcionalidades que ainda não estão incluídas no ramo atual do Configuration Manager. Estas funcionalidades poderão eventualmente ser incluídas numa atualização para o current branch. Antes de vamos finalizar os recursos, queremos a experimentá-las e envie-nos comentários.  

Uma vez que esta versão é uma pré-visualização técnica, detalhes e a funcionalidade estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do ramo de pré-visualização técnica do Configuration Manager. Este artigo apresenta uma lista de cada funcionalidade nova juntamente com a versão de pré-visualização técnica em que ele aparece pela primeira vez. Por exemplo, a versão **1901** para Janeiro (01) de 2019 (19). Artigos separados dedicados para cada detalhe da versão de pré-visualização, os recursos individuais.  

Para obter informações sobre o que há de novo no *ramo atual* do Configuration Manager, consulte [o que há de novo no Configuration Manager versões incrementais](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> Para ser notificado quando esta página é atualizada, copie e cole o URL seguinte no seu feed de leitor de RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`


##  <a name="bkmk_reqs"></a> Requisitos e limitações  

> [!IMPORTANT]     
>  O technical preview é licenciado apenas para utilização num ambiente de laboratório. A Microsoft não pode fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software de pré-visualização. Além disso, o software de pré-visualização, pode ter reduzido ou diferentes padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade relação ao software disponibilizado comercialmente.  

Para a maioria dos pré-requisitos de produto, utilize as informações no [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations). As exceções seguintes aplicam-se para o ramo de pré-visualização técnica:  

-   Cada instalação está ativa por 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma suportado.  

-   Ela oferece suporte apenas os seguintes parâmetros de linha de comandos de configuração:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   Instala o ponto de ligação de serviço para o modo online. Ele não suporta o modo offline.  

-   Os artigos separados para cada versão específica do technical preview incluem requisitos, conforme aplicável ou limitações adicionais.

-   As seguintes funcionalidades não são suportadas com o ramo de pré-visualização técnica:  

    - [Migração](/sccm/core/migration/migrate-data-between-hierarchies) de ou para este ramo de pré-visualização.  

    - [Atualizar](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) para este ramo de pré-visualização.  

    - [Recuperação de sites](/sccm/core/servers/manage/recover-sites) da pasta CD. Latest.  <!--507106-->

-   Não há suporte para a atualização para o ramo atual do ramo pré-visualização.  

    > [!Note]  
    > Quando as atualizações estiverem disponíveis para uma versão de pré-visualização, ainda encontrar e instalá-los a partir da **atualizações e manutenção** nó da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, consulte [pacotes de atualização de instalar o Configuration Manager](https://www.youtube.com/embed/KBd_EGFbUT8) em youtube.com.  

-   Ela oferece suporte apenas um site primário autónomo. Não há suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

O ramo de pré-visualização técnica do Configuration Manager suporta os seguintes produtos e tecnologias: 

-   Ele só suporta as seguintes versões do **SQL Server**:  

    -   SQL Server 2017 (com a atualização cumulativa 2 ou posterior) 
    -   SQL Server 2016 (sem service pack ou posterior)
    -   SQL Server 2014 (sem service pack 1 ou posterior)
    -   SQL Server 2012 (sem service pack 3 ou posterior)  


-   O site suporta até 10 clientes, que tem de executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 7  

> [!Note]  
> A inclusão desses produtos neste conteúdo não implica uma extensão de suporte para uma versão que está além do seu ciclo de vida de suporte. O Configuration Manager não suporta produtos que estejam fora do respetivo ciclo de vida de suporte. Para obter mais informações, consulte [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Instalação e atualização  

O ramo de pré-visualização técnica do Configuration Manager para utilização do laboratório é diferente do Configuration Manager current branch para utilização em produção.  

Primeiro de instalar uma versão de linha de base do ramo de pré-visualização técnica. Depois de instalar uma versão de linha de base, em seguida, utilize atualizações na consola para atualizar sua instalação atualizada com a versão de pré-visualização mais recente. Normalmente, as novas versões do technical preview estão disponíveis mensalmente.

A Microsoft suporta a cada versão de pré-visualização técnica até que existem três versões sucessivas. Por exemplo, quando versão 1708 lançado, versão 1704 não era mais suporte. Versões 1705, 1706 e versão 1707 permaneceram em suporte. Quando uma linha de base sai do suporte, ainda é suportado para a instalação de um novo site de pré-visualização técnica, partindo do princípio de que atualizar imediatamente para uma versão suportada. A linha de base mais antiga é suportada até que uma nova versão de linha de base está disponível. Atualize para a versão mais recente disponível da linha de base e, em seguida, repita o processo de atualização até que instale a versão de pré-visualização técnica mais recente.

> [!TIP]  
>  Quando instala uma atualização para o technical preview, atualizar sua instalação de visualização para essa nova versão de pré-visualização técnica. Uma instalação de pré-visualização técnica nunca tem a opção de atualizar para uma instalação do ramo atual. Também nunca recebe atualizações da versão do ramo atual. 
> 
> Várias vezes ao longo do ano, existem pré-visualização técnica e as versões atuais do ramo com o mesmo número de versão. Por exemplo, existe uma versão de pré-visualização técnica 1802 e uma versão de ramificação 1802 atual. 


### <a name="active-baseline-versions"></a>Versões de linha de Active Directory
   
Instale uma versão de linha de base para até um ano após o seu lançamento. Quando instala um novo site de pré-visualização técnica, se mais de uma versão de linha de base está atualmente disponível, utilize a versão de linha de base mais recente.

-  **Versão de pré-visualização técnica 1902.2**: A versão de pré-visualização técnica 1902.2 do Configuration Manager está disponível como uma atualização na consola e como uma nova versão de linha de base. Baixe versões de linha de base do [Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  

Adoramos ouvir os seus comentários sobre as novas funcionalidades no technical preview. Para obter mais informações, consulte [comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Se tiver ideias sobre novas funcionalidades que gostariam de ver, o que queremos saber que também. Para submeter novas ideias e votar em ideias submetidas por outras pessoas, [visite a nossa página UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> A versão mais recente  

As seguintes funcionalidades estão disponíveis com a versão de pré-visualização técnica mais recente do Configuration Manager: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-19022"></a>Pré-visualização técnica versão 1902.2

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID--> 

- [Idiomas adicionais para atualizações do Office 365](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365lang) <!--3555955--> 
- [Integração com análise de preparação para o Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365) <!--3735402--> 
- [Melhoria para os critérios de sucesso de implementação por fases](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_pod) <!--3555946--> 
- [Melhoria para HTTP avançado](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_ehttp) <!--3798957--> 


> [!Note]  
> Recursos que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, os recursos que são adicionados para o Configuration Manager current branch permanecem disponíveis no ramo de pré-visualização técnica.   



## <a name="features-in-recent-supported-technical-previews"></a>Recursos em technical previews recentes suportadas

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Configuration Manager que ainda são suportadas: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Funcionalidade | Versão de pré-visualização técnica | Versão do ramo atual |  
 |---------|---------------------------|------------------------|
 | Substitua as notificações de alerta com a janela caixa de diálogo <!--3555947--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact) | ![Não adicionado](media/Red_X.gif) | 
 | Estado do progresso durante a sequência de tarefas de atualização no local <!--3747129--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu) | ![Não adicionado](media/Red_X.gif) | 
 | Redirecionar Windows conhecido pastas no OneDrive <!--3556021--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb) | ![Não adicionado](media/Red_X.gif) | 
 | Primeiro ecrã da vista apenas durante o controlo remoto <!--3231732--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti) | ![Não adicionado](media/Red_X.gif) | 
 | Editar ou copiar scripts do PowerShell <!--3705507--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit) | ![Não adicionado](media/Red_X.gif) | 
 | Adicionar o gateway de gestão na cloud a grupos de limites <!--3640932--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg) | ![Não adicionado](media/Red_X.gif) | 
 | Configurar as vistas predefinidas no Centro de Software <!--3612112--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias ao dashboard de estado de funcionamento do cliente <!--3599209--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health) | ![Não adicionado](media/Red_X.gif) | 
 | Dashboard de estado de funcionamento do cliente <!--3599209--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | ![Não adicionado](media/Red_X.gif) | 
 | Especifique a prioridade para as atualizações de funcionalidade na manutenção do Windows 10 <!--3734525--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | ![Não adicionado](media/Red_X.gif) | 
 | Dedicado a monitorização para as implementações faseadas <!--3555949--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | ![Não adicionado](media/Red_X.gif) | 
 | Executar CMPivot do site de administração central <!--3610960--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias para o passo de sequência de tarefas executar Script do PowerShell <!--3556028--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | ![Não adicionado](media/Red_X.gif) | 
 | Produtos do Office no dashboard do ciclo de vida <!--3556026--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | ![Não adicionado](media/Red_X.gif) | 
 | Regras de informações de gestão para coleções <!--3555752--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | ![Não adicionado](media/Red_X.gif) | 
 | Modos de exibição do dispositivo de pesquisa com o endereço MAC <!--3600878--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | ![Não adicionado](media/Red_X.gif) | 
 | Modo de manutenção do ponto de distribuição <!--3555754--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | ![Não adicionado](media/Red_X.gif) | 
 | Manutenção de imagens otimizada <!--3555951--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | ![Não adicionado](media/Red_X.gif) | 
 | Importar um único índice de imagem do SO <!--3719699--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | ![Não adicionado](media/Red_X.gif) | 
 | Utilizar o Azure Resource Manager para os serviços cloud <!--3605704--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | ![Não adicionado](media/Red_X.gif) | 
 | Confirmação de comentários de consola <!--3556010--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | ![Não adicionado](media/Red_X.gif) | 
 | Criar um laboratório de pré-visualização técnica do Configuration Manager no Azure <!--3556017--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | ![Não adicionado](media/Red_X.gif) | 
 | Especifique uma porta personalizada para reativação de ponto a ponto <!--3605925--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | ![Não adicionado](media/Red_X.gif) | 
 | Modo de exibição ligado recentemente consolas <!--3699367--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | ![Não adicionado](media/Red_X.gif) | 
 | Parar serviço em nuvem quando exceder o limiar <!--3735092--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | ![Não adicionado](media/Red_X.gif) | 
 | Aprovisionamento modo tempo limite do cliente <!--3197824--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias para implementação do SO <!--3633146,3641475,3654172,3734270--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias para o passo de sequência de tarefas executar Script do PowerShell <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias para aprovações de aplicação através de e-mail <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![Não adicionado](media/Red_X.gif) | 
 | Configurar a afinidade dispositivo / utilizador no Centro de Software <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias à consola do Configuration Manager <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![Não adicionado](media/Red_X.gif) | 
 | Transferir relatórios a partir do Hub de Comunidade<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Não adicionado](media/Red_X.gif) | 
 | Não carregar perfis do Windows PowerShell <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Não adicionado](media/Red_X.gif) | 
 | Uma ligação do Intune já não é necessária para MDM no local <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Não adicionado](media/Red_X.gif) | 
 | Notificações de consola do Configuration Manager <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Não adicionado](media/Red_X.gif) | 
 | Melhorias na criação de suportes de dados de sequência de tarefas <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Não adicionado](media/Red_X.gif) | 
 | Melhoria para o passo de sequência de tarefas executar Script do PowerShell <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Não adicionado](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>Recursos do anteriores pré-visualizações técnicas

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Configuration Manager. Estas funcionalidades permanecem disponíveis nas versões posteriores, mas não ainda estão disponíveis no ramo atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Funcionalidade        | Versão de pré-visualização técnica |  
|----------------|---------------------------|
| Dashboard de documentação na consola <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| Hub de Comunidade <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Atividade de sincronização de dispositivos cogeridos com o Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Serviço de resposta PXE baseada no cliente <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Suporte de arranque de rede PXE para IPv6 <!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Utilizar o Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Avaliação de compatibilidade para o Windows Update para atualizações de negócios <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Melhorias ao Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Os utilizadores finais podem instalar aplicações do Portal da empresa <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Consulte também  

Para obter mais informações, veja os artigos seguintes:  

- [Avaliar o Configuration Manager num laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades das versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para obter mais informações sobre as funcionalidades de ramo atual que requerem o consentimento para ativar, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para obter mais informações sobre funcionalidades atuais do ramo que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
