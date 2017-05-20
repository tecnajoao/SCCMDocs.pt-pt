---
title: "Pré-visualização técnica do System Center Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre a versão de pré-visualização técnica que permite-lhe test-drive novas funcionalidades e capacidades no System Center Configuration Manager."
ms.custom: na
ms.date: 4/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: 3a7370fedee417588d219dc7bff46205faf42929
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

**Bem-vindo à pré-visualização do System Center Technical do Configuration Manager**. Este tópico fornece detalhes sobre a versão de pré-visualização em desenvolvimento, que apresenta novas funcionalidades e capacidades nas quais estamos a trabalhar. Com cada versão da pré-visualização técnica, foram introduzidas novas funcionalidades que não estão incluídos no ramo atual do System Center Configuration Manager no momento que é disponibilizada a versão de pré-visualização técnica. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Como se trata de uma versão de pré-visualização técnica, os detalhes e a funcionalidade estão sujeitos a alterações.  

 Este tópico contém informações que se aplica a todas as versões do Technical Preview e também enumera cada nova capacidade de (ou funcionalidade) juntamente com a versão de pré-visualização técnica em que a capacidade de aparece em primeiro lugar, como versão 1701 de Janeiro de 2017. Os detalhes destas capacidades estão descritos em tópicos separados dedicados a cada versão de pré-visualização.  

 Para obter informações sobre o que há de novo o ramo atual do Configuration Manager, consulte o artigo [quais as novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório.  A Microsoft poderá não fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software da Preview. Além disso, o software da Preview poderá ter um nível reduzido ou diferente de padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade em relação ao software disponibilizado comercialmente.  

 Para a maioria dos pré-requisitos de produto, utilize as informações de [configurações suportadas para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções são aplicáveis apenas às versões do Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias até se tornar inativa.  

-   O inglês é o único idioma suportado.


-   Apenas os seguintes sinalizadores de instalação (comutadores) são suportados:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por predefinição, quando utilizar a pré-visualização técnica, o ponto de ligação de serviço está definido para o modo online quando é instalado e não suporta uma alteração ao modo offline.

-   Quando aplicável, são incluídos requisitos ou limitações adicionais com detalhes para cada versão específica do Technical Preview  

-   Não existe suporte para migração para ou a partir desta versão de pré-visualização.  

-   Não existe suporte para atualizar para esta versão de pré-visualização.  

-   Não existe suporte para atualizar para uma compilação de produção (ramo atual) a partir desta preview build. No entanto, quando as atualizações estão disponíveis para uma versão de pré-visualização, pode localizar e instalá-los a partir de **atualizações e a manutenção** nó da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, veja [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalar Pacotes de Atualização do ConfigMgr) em youtube.com.  
-   Apenas é suportado um site primário autónomo. Não existe suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, as respetivas inclusão neste conteúdo não implica uma extensão de suporte para um produto ou a versão que se não ultrapassa o ciclo de vida de suporte individuais desse produto. Produtos que se encontram para além do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Apenas são suportadas as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem nenhum Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3, ou posterior)


-   O site suporta até 10 clientes, que têm de estar a executar um dos seguintes sistemas operativos:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar o Technical Preview  
 O System Center Configuration Manager Technical Preview é distinta da versão atual do System Center Configuration Manager.  

 Para utilizar a versão de pré-visualização técnica, primeiro tem de instalar uma **versão de linha de base** da compilação da versão de pré-visualização técnica. Depois de instalar uma versão de linha de base, pode então utilizar as **atualizações na consola** para atualizar a sua instalação com a versão de pré-visualização mais recente.     Normalmente, existem novas versões mensais da Technical Preview.

Cada versão de pré-visualização é suportado até três versões sucessivos estão disponíveis. O que significa que, quando versão 1702 lançadas, versão 1610 já não seria no suporte, mas versões 1611, 1612 e 1701 permanecerá em suporte. Quando uma linha de base desce fora de suporte (como versão 1610), ainda é suportada para instalar um novo site de pré-visualização técnica até que uma nova versão de linha de base está disponível, desde que, em seguida, atualizar essa instalação para uma versão suportada. Ao atualizar, se não vir a versão mais recente disponível na sua consola, atualização da versão mais recente oferecidas e, em seguida, repita o processo até pode instalar a versão mais atual do pré-visualização técnica.

> [!TIP]  
>  Quando instala uma atualização da versão de pré-visualização técnica, atualiza a instalação de pré-visualização para essa nova versão de pré-visualização técnica.    Uma instalação de pré-visualização técnica nunca inclui a opção de atualizar para uma instalação do ramo atual, nem de receber atualizações da versão do ramo atual.  

**Versões de linha de base ativas da Technical Preview:**  
É possível instalar uma versão de linha de base para até 1 ano após a respetiva versão. No entanto, quando instala um novo site de pré-visualização técnica, recomendamos que utilize a versão mais recente do plano base que está disponível.
-  **1703 de pré-visualização técnica** -o Configuration Manager Technical pré-visualização 1703 está disponível como ambos os uma atualização na consola do Configuration Manager Technical Preview e como uma nova versão do plano base que está disponível a partir do Web site do Centro de avaliação TechNet.

-  **1610 de pré-visualização técnica** -o Configuration Manager Technical pré-visualização 1610 estava disponível como ambos os uma atualização na consola do Configuration Manager Technical Preview e como uma versão de linha de base. Se tiver suporte de dados para a instalação 1610, recomendamos a versão 1703 de transferir e instalar em vez disso, essa versão.




##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Gostaríamos de receber o seu feedback sobre as nossas versões de pré-visualização técnica. Para submeter comentários sobre as funcionalidades de cada versão de pré-visualização, siga a hiperligação para o nosso formulário de resposta na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 Se tiver ideias sobre novas funcionalidades que gostaria de ver, estamos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capacidades fornecidas em pré-visualizações técnicas  
 Seguem-se as capacidades fornecidas com cada versão de pré-visualização técnica do Configuration Manager.  As capacidades que estão disponíveis a partir de uma versão da Technical Preview permanecem disponíveis em versões posteriores. Do mesmo modo, as funcionalidades que foram adicionadas para a versão de Configuration Manager do System Center (ramo atual) permanecem disponíveis no pré-visualizações técnicas subsequentes.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

 |Funcionalidade |Versão de pré-visualização técnica |Versão atual do ramo|  
|----------------|---------------------|--------------------|
 |Configurar as aplicações Android com as políticas de configuração de aplicação  |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Não foram adicionadas](media/Red_X.gif)|
 |Inventário de hardware recolhe informações de arranque seguro |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![Não foram adicionadas](media/Red_X.gif)|
 |Adicionar sequências de tarefas do subordinado a uma sequência de tarefas|[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Não foram adicionadas](media/Red_X.gif)|
 |Recarregar imagens de arranque com a versão atual do Windows PE |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![Não foram adicionadas](media/Red_X.gif)|
 |Melhorias na implementação do sistema operativo|[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Não foram adicionadas](media/Red_X.gif)|
 |Implementar aplicações iOS adquiridos de volume em coleções de dispositivos|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versão 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Ligações diretas para aplicações no Centro de Software|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Não foram adicionadas](media/Red_X.gif)
 |Certificados PFX para computadores cliente do Windows do Configuration Manager|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Não foram adicionadas](media/Red_X.gif)|
 |Configurar o Assistente de serviços do Azure|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![Não foram adicionadas](media/Red_X.gif)|
 |Converter de BIOS para UEFI uma sequência de tarefas de atualização do sistema operativo| [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de sequências de tarefas expansíveis| [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Não foram adicionadas](media/Red_X.gif)|
 |Definições de cliente para configurar o Windows Analytics para a preparação da atualização | [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Não foram adicionadas](media/Red_X.gif)|
 |Novas definições de compatibilidade para dispositivos iOS|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versão 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Criar os certificados PFX com suporte S/MIME|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versão 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Verifique a existência de ficheiros executáveis a ser executado antes de instalar uma aplicação|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentários a partir da consola do Configuration Manager | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Alterações à atualizações e manutenção  | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Melhoramentos de Cache ponto a ponto  | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versão 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Utilizar o Azure Active Directory  | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Não foram adicionadas](media/Red_X.gif)|
 |Melhoramentos de política de conformidade de dispositivos de acesso condicional | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versão 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versão do cliente de proteção contra software maligno | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versão 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Avaliação de compatibilidade para o Windows Update para atualizações de negócio | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Não foram adicionadas](media/Red_X.gif)|
 |Foram introduzidos melhoramentos nas definições do Centro de Software e mensagens de notificação para sequências de tarefas de impacto elevado|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versão 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android para o suporte de trabalho| [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versão 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Pontos de atualização de melhorias de grupos de limites de software | [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versão 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |Inventário de hardware recolhe informações de UEFI | [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Melhorias na implementação do sistema operativo| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Atualizações de software do anfitrião em pontos de distribuição baseado na nuvem| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Não foram adicionadas](media/Red_X.gif) |
 |Validar dados de atestado de estado de funcionamento de dispositivos através de pontos de gestão| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versão 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector OMS para a nuvem do Microsoft Azure para a administração pública |[Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versão 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Versões do Android e iOS já não são targetable nos assistentes de criação |[Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Não foram adicionadas](media/Red_X.gif) |
 |Acesso de dados do ponto final de OData |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foram adicionadas](media/Red_X.gif)|
 |Ponto de serviço do armazém de dados |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versão 1702](/sccm/core/servers/manage/data-warehouse)|
 |Ferramenta de limpeza da biblioteca de conteúdos |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versão 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Melhoramentos na cópia de pesquisa na consola |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Evitar a instalação de uma aplicação, se um programa especificado está em execução|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Novo Windows Hello para notificação de negócio para os utilizadores finais|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Não foram adicionadas](media/Red_X.gif)|
 |Loja Windows para o suporte de negócio no Configuration Manager|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Não foram adicionadas](media/Red_X.gif)|
 |Regressar à página anterior, quando uma sequência de tarefas falhar|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Suporte para atualizações do Windows 10 de ficheiros de instalação rápida|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versão 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Integração do Azure Active Directory|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Não foram adicionadas](media/Red_X.gif)|
 |Alterar para configurar a autenticação multifator para a inscrição de dispositivos|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Não foram adicionadas](media/Red_X.gif)|
 |Conteúdo da cache de pré-lançamento para implementações e sequências de tarefas |[Pré-visualização do técnico 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Definições de configuração do Windows Defender|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Política de pedido de sincronização a partir da consola de administrador|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versão 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Suporte de função de segurança adicional para o nó de todos os dispositivos pertencentes|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versão 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acesso condicional para perfis VPN do Windows 10|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versão 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar por tamanho do conteúdo nas regras de implementação automática|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Melhoria da funcionalidade para caixas de diálogo de software necessárias|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negar pedidos de aplicações anteriormente aprovados|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir os clientes da atualização automática|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versão 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Melhoramentos no Endpoint Protection|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versão 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Aumento do número de dispositivos inscritos|[Pré-visualização do técnico 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versão 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Definições adicionais do DEP da Apple|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versão 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Melhoramentos à loja Windows para a integração de negócio com o Configuration Manager|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md)|[Versão 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Novas definições de compatibilidade para itens de configuração|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integração com a análise de atualização|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versão 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Perfis de VPN híbrida de tipos de ligação nativo do Windows 10|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Não foram adicionadas](media/Red_X.gif)|
 |Melhoramentos na cópia de grupos de limites|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versão 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Dashboard de gestão de clientes do Office 365|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versão 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implementar aplicações do Office 365 para clientes|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versão 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Melhorias BIOS para conversão de UEFI|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versão 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de conformidade do Intune|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versão 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Melhorias efetuadas ao centro de Software|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Melhorias do Asset Intelligence|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Não foram adicionadas](media/Red_X.gif)|
 |Tradução de teclado do controlo remoto|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Não foram adicionadas](media/Red_X.gif)|
 |Melhoramentos à Política de Atualização de Edição do Windows 10|[Pré-visualização do técnico 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versão 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software|[Pré-visualização do técnico 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Não foram adicionadas](media/Red_X.gif)|  
 |Vários pontos de gestão de dispositivos para Gestão de Dispositivos Móveis no Local|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizar automaticamente os dispositivos em coleções|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Versão 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Período de tolerância de imposição para implementações de atualizações de aplicações e de software|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Utilizar o Configuration Manager como um Instalador Gerido com Device Guard|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Não foram adicionadas](media/Red_X.gif)|
 |Gateway de gestão da nuvem (anteriormente serviço Proxy de nuvem)|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gerir o agente de cliente do Office 365 no Configuration Manager|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |A variável da sequência de tarefas OSDPreserveDriveLetter foi preterida|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versão 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Alterações do Nó Atualizações e Manutenção|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN por Aplicação para dispositivos Windows 10|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versão 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Melhoramentos à sequência de tarefas Instalar atualizações de software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Período de tolerância para implementações de aplicações necessárias |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Não foram adicionadas](media/Red_X.gif)|  
 |Nova experiência para ações de dispositivos remotos |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Aplicações da Loja Windows para Empresas |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhoramentos gerais para aplicações compradas em volume|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Proteção de Dados Empresariais (EDP)|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Os utilizadores finais podem instalar aplicações a partir do Portal da Empresa |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Não foram adicionadas](media/Red_X.gif)|  
 |Novos separadores para Atualizações e Sistemas Operativos no Centro de Software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Fazer manutenção a um grupo de servidores |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versão 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Suporte do serviço Proteção Avançada Contra Ameaças do Windows Defender |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versão 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Novas opções de reinício para clientes do Windows 10 após a instalação de atualizações de software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Atestado de Estado de Funcionamento no Local |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versão 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Gerir aplicações adquiridas em volume a partir da Loja Windows para Empresas| [Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhoramentos na gestão do Microsoft Passport for Work|[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Opção para os clientes mudarem para um novo ponto de atualização de software|[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Definições de cliente para gerir Definições de Cache do Cliente e Cache Ponto a Ponto do cliente |[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Definições de cliente: [Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Cache de elementos da: [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Suporte do Passport for Work como um KSP |[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Versão 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Atestado de Estado de Funcionamento no Local|[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Definição de SmartLock para dispositivos Android|[Pré-visualização do técnico 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Versão 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 <!--  TP 1603 Aged out of support and all features in Current Branch Builds:
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->
 Quando todas as funcionalidades de uma versão de pré-visualização técnica estão disponíveis na versão mínima suportada do mesmo atual, os detalhes para essa versão de pré-visualização são removidos desta tabela.


## <a name="see-also"></a>Consulte Também  
[O que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)

