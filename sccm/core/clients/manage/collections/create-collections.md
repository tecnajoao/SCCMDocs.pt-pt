---
title: "Criar coleções | Documentos do Microsoft"
description: "Crie coleções no System Center Configuration Manager, para gerir mais facilmente os grupos de utilizadores e dispositivos."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: dee63826d8e6100f5b8402952175106076585030
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Como criar coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções consistem em agrupamentos de utilizadores ou dispositivos. Utilize coleções para tarefas como a gestão de aplicações, implementação de definições de compatibilidade, ou instalar atualizações de software. Também pode utilizar coleções para gerir grupos de definições de cliente ou utilizá-las com a administração baseada em funções para especificar os recursos aos quais um utilizador administrativo pode aceder. Gestor de configuração contém várias coleções incorporadas. Para obter mais informações, consulte o artigo [introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Uma coleção pode conter utilizadores ou dispositivos, mas não ambos.  

 A tabela seguinte lista as regras que pode utilizar para configurar os membros de uma coleção no Configuration Manager.  

|Tipo de regra de associação|Mais informações|  
|--------------------------|----------------------|  
|Regra direta|Utilize para escolher os utilizadores ou computadores que pretende adicionar a uma coleção. Associação a este não se altera, exceto se remover um recurso do Configuration Manager. O Configuration Manager têm de ter detetados os recursos ou tem importou os recursos antes de poder adicioná-los para uma coleção de regra direta. Coleções de regra direta tem um overhead administrativo mais elevado de coleções de regra de consulta porque requerem alterações manuais.|  
|Regra de consulta|Atualize dinamicamente a associação de uma coleção com uma consulta que o Configuration Manager é executado com base numa agenda. Por exemplo, pode criar uma coleção de utilizadores que são membros da unidade organizacional Recursos Humanos nos Serviços de Domínio do Active Directory. Esta coleção é automaticamente atualizada quando novos utilizadores são adicionados ou removidos da unidade organizacional de recursos humanos.<br /><br /> Por exemplo consultas que pode utilizar para criar coleções, consulte o artigo [como criar consultas no System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regra de inclusão de coleção|Inclua membros de outra coleção numa coleção do Configuration Manager que a associação da coleção de atual é atualizada com base numa agenda, se alterar a coleção incluída.<br /><br /> Pode adicionar várias regras de inclusão de coleção a uma coleção.<br /> |  
|Regra de exclusão de coleção|A regra de recolha de exclusão permitem-lhe excluir membros de outra coleção de uma coleção do Configuration Manager. A associação da coleção de atual é atualizada com base numa agenda, se a coleção excluída as alterações.<br /><br /> Pode adicionar várias regras de exclusão de coleção a uma coleção. Se uma coleção inclui ambos de coleção de inclusão e exclusão regras de recolha e existe um conflito, a regra de recolha de exclusão tem prioridade.<br />              **Exemplo:** Criar uma coleção que tenha uma incluem regra de recolha e uma excluir regra de recolha. A regra de inclusão de coleção destina-se a uma coleção de computadores de secretária Dell. A regra de exclusão de coleção destina-se a uma coleção de computadores que têm menos de 4 GB de RAM. A nova coleção irá conter os computadores de secretária Dell que tenham, pelo menos, 4 GB de RAM.|  

 Utilize os procedimentos seguintes para o ajudar a criar coleções no Configuration Manager. Também pode importar coleções que foram criadas este ou de outro site do Configuration Manager. Para obter informações sobre como exportar e importar coleções, consulte o artigo [como gerir coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Para obter informações sobre a criação de coleções para computadores que executam o Linux e UNIX, consulte o artigo [como gerir os clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="BKMK_1"></a> Para criar uma coleção de dispositivos  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de dispositivos**.  

3.  No **base** separador o **criar** grupo, selecione **criar coleção de dispositivos**.  

4.  No **geral** página fornecem uma **nome** e um **comentário**. Em seguida, no **a limitação da coleção**, escolha **procurar** para selecionar uma coleção restritiva. A coleção irá conter apenas membros da coleção restritiva.  

5.  No **regras de associação** página do **criar Assistente de coleção de dispositivos**, no **Adicionar regra** lista, selecione o tipo de regra de associação que pretende utilizar para esta coleção. Pode configurar várias regras para cada coleção.  

        
        ##### To configure a direct rule  

        1.  Na página **Procurar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as seguintes informações:  

            -   **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Selecione entre os valores **Recurso do Sistema** para procurar dados de inventário devolvidos de computadores cliente ou **Computador Desconhecido** para selecionar entre os valores devolvidos por computadores desconhecidos.  

            -   **Nome do atributo**: Selecione o atributo associado com a classe de recursos selecionado que pretende procurar. Por exemplo, se pretender selecionar computadores pelo respetivo nome NetBIOS, selecione **Recurso do Sistema** na lista **Classe de recursos** e **Nome NetBIOS** na lista **Nome do atributo** .  

            -   **Excluir recursos marcados como obsoletos** - se um computador cliente está marcado como obsoleto, não incluir este valor nos resultados da pesquisa.  

            -   **Excluir recursos que não tenham o cliente do Configuration Manager instalado** -estes não serão apresentadas nos resultados da pesquisa.  

            -   **Valor:** Introduza um valor para o qual pretende procurar o nome de atributo selecionado. Pode utilizar o caráter de percentagem **%** como caráter universal. Por exemplo, para procurar computadores que tenham um início de nome de NetBIOS com "M", introduza **M %** neste campo.  

        2.  No **selecione recursos** página, selecione os recursos que pretende adicionar à coleção no **recursos** lista e, em seguida, selecione **seguinte**.  


        ##### To configure a query rule  

        1.  Na caixa de diálogo **Propriedades da Regra de Consulta** , especifique as seguintes informações:  

            -   **Nome**: Especifique um nome exclusivo.  

            -   **Importar declaração de consulta** -abre a **procurar consulta** caixa de diálogo onde pode selecionar um [do Configuration Manager consulta](../../../../core/servers/manage/create-queries.md) para utilizar como a regra de consulta para a coleção.   

            -   **Classe de recursos:** Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Selecione um valor entre os valores de **Recurso do Sistema** para procurar dados de inventário devolvidos de computadores cliente ou **Computador Desconhecido** para selecionar entre os valores devolvidos por computadores desconhecidos.  

            -   **Editar a instrução de consulta** -abre a **propriedades da instrução de consulta** caixa de diálogo onde pode criar uma consulta para utilizar como a regra para a coleção. Para obter mais informações sobre consultas, veja [Referência técnica para consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

    
        ##### To configure an include collection rule  

        In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  

        ##### To configure an exclude collection rule  

        In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  

    -   **Utilizar atualizações incrementais para esta coleção** - Selecione esta opção para verificar periodicamente e atualizar apenas novos ou alterados recursos desde a anterior avaliação de coleção, independentemente de uma avaliação de coleção completa. As atualizações incrementais ocorrem em intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  As coleções configuradas através de regras de consulta que utilizem as classes seguintes não suportam atualizações incrementais:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Agendar uma atualização completa desta coleção** -agendar uma avaliação completa regular da associação à coleção.  

6.  Conclua o assistente para criar a nova coleção. A nova coleção é apresentada no nó **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** .  

> [!NOTE]  
>  Tem de atualizar ou recarregar a consola do Configuration Manager para ver os membros da coleção. No entanto, os membros não aparecerão na coleção até após a atualização agendada primeiro, ou se selecionou manualmente **atualizar associação** para a coleção. Poderá demorar alguns minutos para que uma atualização da coleção concluir.  

##  <a name="BKMK_2"></a> Para criar uma coleção de utilizadores  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de utilizadores**.  

3.  No **base** separador o **criar** grupo, selecione **criar coleção de utilizadores**.  

4.  No **geral** página do wizardprovide um **nome** e um **comentário**. Em seguida, no **a limitação da coleção**, escolha **procurar** para selecionar uma coleção restritiva. A coleção só irá conter os membros da coleção restritiva.  

5.  No **regras de associação** página, especifique o seguinte:  

    -   Na lista **Adicionar Regra** , selecione o tipo de regra de associação que pretende utilizar para esta coleção. Pode configurar várias regras para cada coleção.  

         ##### <a name="to-configure-a-direct-rule"></a>Para configurar uma regra direta  

        1.  No **procurar recursos** página do **criar Assistente de regra de associação direta**, especificar:  

            -   **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Selecione a partir de **recursos de utilizador** valores para procurar informações do utilizador recolhidas pelo Configuration Manager ou **recurso do grupo de utilizador** para procurar informações do grupo de utilizador recolhidas pelo Configuration Manager.  

            -   **Nome do atributo**: Selecione o atributo associado com a classe de recursos que pretende procurar. Por exemplo, se pretender selecionar utilizadores pelo respetivo nome de Unidade Organizacional (UO), selecione **Recurso de Utilizador** na lista **Classe de recursos** e **Nome da UO de Utilizadores** na lista **Nome do atributo** .  

            -   **Valor:** Introduza um valor que pretende procurar. Pode utilizar o caráter de percentagem **%** como caráter universal. Por exemplo, para localizar utilizadores no Contoso OU, introduza **Contoso** neste campo.  

        2.  No **selecione recursos** página, selecione os recursos que pretende adicionar à coleção no **recursos** lista.  

        ##### <a name="to-configure-a-query-rule"></a>Para configurar uma regra de consulta  

        1.  No **propriedades da regra de consulta** caixa de diálogo, fornecer:  

            -   **Nome**: Um nome exclusivo.  

            -   **Importar declaração de consulta** -abre a **procurar consulta** caixa de diálogo onde pode selecionar um [do Configuration Manager consulta](../../../../core/servers/manage/queries-technical-reference.md) para utilizar como a regra de consulta para a coleção.  

            -   **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Selecione a partir de **recursos de utilizador** valores para procurar informações do utilizador recolhidas pelo Configuration Manager ou **recurso do grupo de utilizador** para procurar informações do grupo de utilizador recolhidas pelo Configuration Manager.  

            -   **Editar a instrução de consulta** -abre a **propriedades da instrução de consulta** caixa de diálogo onde poderá [uma consulta de autor](../../../../core/servers/manage/queries-technical-reference.md) para utilizar como a regra para a coleção.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Para configurar uma regra de inclusão de coleção  

        No **selecionar coleções** diálogo caixa, selecione as coleções que pretende incluir na nova coleção, em seguida, escolha **OK**.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Para configurar uma regra de exclusão de coleção  

        No **selecionar coleções** diálogo caixa, selecione as coleções que pretende excluir da nova coleção, em seguida, escolha **OK**.  


    -   **Utilizar atualizações incrementais para esta coleção** - Selecione esta opção para verificar periodicamente e atualizar apenas novos ou alterados recursos desde a anterior avaliação de coleção, independentemente de uma avaliação de coleção completa. As atualizações incrementais ocorrem em intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  As coleções configuradas através de regras de consulta que utilizem as classes seguintes não suportam atualizações incrementais:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Agendar uma atualização completa desta coleção** -agendar uma avaliação completa regular da associação à coleção.  

6.  Conclua o assistente. A nova coleção é apresentada no nó **Coleções de Utilizadores** da área de trabalho **Ativos e Compatibilidade** .  

> [!NOTE]  
>  Tem de atualizar ou recarregar a consola do Configuration Manager para ver os membros da coleção. No entanto, os membros só irão aparecer na coleção após a primeira atualização agendada ou se selecionar manualmente a opção **Atualizar Associação** para a coleção. Poderá demorar alguns minutos para que uma atualização da coleção concluir.  

##  <a name="BKMK_3"></a> Para importar uma coleção  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de utilizadores** ou **coleções de dispositivos**.  

3.  No **base** separador o **criar** grupo, selecione **importar coleções**.  

4.  No **geral** página do **Assistente Importar coleções**, escolha **seguinte**.  

5.  No **nome do ficheiro MOF** página, selecione **procurar** e, em seguida, procure o ficheiro MOF que contém as informações de recolha que pretende importar.  

    > [!NOTE]  
    >  O ficheiro que pretende importar tem sido exportado a partir de um site com a mesma versão do Configuration Manager como este. Para obter mais informações acerca da exportação de coleções, consulte o artigo [como gerir coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Conclua o assistente para importar a coleção. A nova coleção é apresentada no nó **Coleções de Utilizadores** ou **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** . Atualize ou recarregue a consola do Configuration Manager para ver os membros da coleção para a coleção recentemente importado.  

