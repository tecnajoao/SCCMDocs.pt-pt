---
title: Pré-requisitos para sites
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do System Center Configuration Manager.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e45ec9aca5ee1a14f9058453497003814b2fdb0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Pré-requisitos de instalação de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de iniciar uma instalação de site, é uma boa ideia para saber mais sobre os pré-requisitos para instalar os diferentes tipos de sites do System Center Configuration Manager.

## <a name="primary-sites-and-the-central-administration-site"></a>Sites primários e o site de administração central
Os seguintes pré-requisitos aplicam-se a instalação de um site de administração central como o primeiro site numa hierarquia, instalar um site primário autónomo ou instalar um site primário subordinado. Se estiver a instalar um site de administração central como parte de uma expansão da hierarquia, consulte o artigo [expandir um site primário autónomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) neste tópico.

###  <a name="bkmk_PrereqPri"></a> Pré-requisitos para instalar um site primário ou site de administração central  

-   A conta de utilizador que instala o site tem de ter os seguintes direitos de:  

    -   **Administrador** no computador do servidor do site  
    -   **Administrador** em cada computador que alojará o **base de dados do site** ou uma instância do **fornecedor de SMS** para o site  
    -   **Sysadmin** na instância do SQL Server que aloja a base de dados do site  

        > [!IMPORTANT]  
        >  Quando a conclusão da configuração, a conta de utilizador que executa a configuração e a conta de computador do servidor de site têm de reter os direitos de administrador do sistema no SQL Server. Não remova os direitos de administrador do sistema destas contas.  

-   Se estiver a instalar um site primário, terá os seguintes direitos adicionais:  
    -  **Administrador** em computadores adicionais onde irá instalar o ponto de gestão inicial e o ponto de distribuição; caso contrário no servidor do site  

-   Se estiver a instalar um novo site primário subordinado abaixo de um site de administração central, terá os seguintes direitos adicionais:  

    -   **Administrador** no computador que aloja o site de administração central  

    -   Direitos de administração baseada em funções dentro do Gestor de configuração que sejam equivalentes à função de segurança de **administrador de infraestrutura** ou **administrador total**  

-   Tem de utilizar o suporte de dados de instalação correta (ficheiros de origem) e executar a configuração a partir dessa localização. Para obter informações sobre os ficheiros de origem correta a utilizar para instalar os diferentes tipos de sites, consulte [opções para a instalação de diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) no [preparar para instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) tópico.

-   O computador de servidor do site tem de ter acesso aos ficheiros de configuração atualizados da Microsoft, de uma das seguintes formas:
    -  Antes de iniciar a instalação, pode transferir e armazenar uma cópia destes ficheiros na sua rede local utilizando [dispositivo de transferência da configuração](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Se copiar uma local destes ficheiros não estão disponível, o servidor do site tem de ter acesso à Internet, de modo que pode transferir estes ficheiros da Microsoft durante a instalação.

- Antes de poder expandir um site primário autónomo que tenha uma ligação ponto site função do sistema serviço instalada, terá de desinstalar o ponto de ligação de serviço. Apenas uma instância desta função é permitida numa hierarquia e só é permitida no site de nível superior da hierarquia. Terá a oportunidade de reinstalar a função durante a instalação do site de administração central.
- O servidor do site e computadores de base de dados do site tem de cumprir todas as configurações de pré-requisitos. Antes de iniciar a configuração, pode [executar manualmente o Verificador de pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar e corrigir problemas.  


### <a name="bkmk_expand"></a> Pré-requisitos para expandir um site primário autónomo
Pode expandi-lo para uma hierarquia com um site de administração central, um site primário autónomo tem de cumprir os seguintes pré-requisitos:

-   **Tem de instalar a nova instalação de site de administração central utilizando suportes de dados de um CD. Pasta mais recente (que contém os ficheiros de origem) que corresponde à versão do site primário autónomo**

 Para garantir uma correspondência de versão, utilize os ficheiros de origem localizado no [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) no site primário autónomo.

 Para obter mais informações sobre os ficheiros de origem correta a utilizar para instalar sites diferentes, consulte [opções para a instalação de diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) no [preparar para instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) tópico.


-   **O site primário autónomo não pode ser configurado para migrar dados a partir de outra hierarquia do Configuration Manager**  

     Tem de parar a migração ativa para o site primário autónomo de outras hierarquias do Configuration Manager e remover todas as configurações de migração. Isto inclui tarefas de migração que ainda não estão concluídas, a recolha de dados e a configuração da hierarquia de origem ativa.  

     Isto é necessário porque as operações de migração são efetuadas pelo site de nível superior da hierarquia, as configurações de migração, não sendo transferem para o site de administração central quando expande um site primário autónomo.  

     Depois de expandir o site primário autónomo, se reconfigurar a migração no site primário, o site de administração central executa as operações relacionadas com a migração. Para obter mais informações sobre como configurar a migração, consulte [configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **A conta de computador do computador que irá alojar o novo site de administração central tem de ser um membro do grupo de utilizador administrador no site primário standa única**  

     Para expandir com êxito o site primário autónomo, a conta de computador do novo site de administração central tem de ter **administrador** direitos no site primário autónomo. Isto é necessário apenas durante a expansão do site. A conta pode ser removida do grupo de utilizador no site primário quando a expansão do site for concluída.  

-   **A conta de utilizador que executa o programa de configuração para instalar o novo site de administração central tem de ter direitos de administração baseada em funções no site primário autónomo**  

     Para instalar um site de administração central como parte da expansão do site, a conta de utilizador que executa a configuração para instalar o site de administração central tem de ser definida na administração baseada em funções no site primário autónomo como um **administrador total** ou um **administrador de infraestrutura**.  

-   **Tem de desinstalar as seguintes funções do sistema de sites do site primário autónomo antes de poder expandir o site:**  

    -   Ponto de sincronização do Asset Intelligence  
    -   Ponto de Endpoint Protection  
    -   Ponto de ligação de serviço  

   Estas funções de sistema de sites são suportadas apenas no site de nível superior da hierarquia. Por conseguinte, tem de desinstalar estas funções de sistema de sites antes de expandir o site primário autónomo. Depois de expandir o site, pode reinstalar estas funções de sistema de sites no site de administração central.  

    Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

-   **A porta para o SQL Server Service Broker (SSB) entre o site primário autónomo e o computador que vai instalar o site de administração central tem de estar aberta**  

     Para replicar com êxito os dados entre um site de administração central e um site primário, o Configuration Manager requer uma porta aberta entre os dois sites para SSB a utilizar. Quando instala um site de administração central e expandir um site primário autónomo, a verificação de pré-requisitos não Certifique-se de que a porta especificada para o SSB está aberta no site primário.  

**Problemas conhecidos quando tiver configurado os serviços do Azure:**  
Quando utilizar um dos seguintes serviços do Azure com o Configuration Manager e se pretende expandir um site, depois de expandir o site tem de remover e, em seguida, recrie a ligação a esse serviço.

Serviços:  
-       [Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS)
-       [Preparação para a atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics)
-       [Microsoft loja para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

Utilize os seguintes passos para resolver este problema:
 1.    Na consola do Configuration Manager, elimine o serviço do Azure a partir do nó de serviços do Azure.
 2.    No portal do Azure, elimine o inquilino que estão associado com o serviço a partir do nó do Azure Active Directory inquilinos.  Isto também elimina a aplicação web do Azure AD que estão associada com o serviço.  
 3.   Reconfigure a ligação ao serviço do Azure para utilização com o Configuration Manager.


## <a name="bkmk_secondary"></a> Sites secundários
Seguem-se os pré-requisitos para instalar sites secundários:
-   O administrador configura a instalação do site secundário na consola do Configuration Manager tem de ter direitos de administração baseada em funções que sejam equivalentes à função de segurança de **administrador de infraestrutura** ou **administrador total**.  
-   A conta de computador do site primário principal tem de ser um **administrador** no computador do servidor de site secundário.  
-   Quando o site secundário utiliza uma instância anteriormente instalada do SQL Server para alojar a base de dados do site secundário:  

    -   O **conta de computador** de principal tem de ter primário **sysadmin** direitos na instância do SQL Server no computador do servidor de site secundário.  

    -   O **Sistema Local** conta de computador do servidor do site secundário tem de ter **sysadmin** direitos na instância do SQL Server no computador do servidor de site secundário.  

        > [!IMPORTANT]  
        >  Quando a conclusão da configuração, ambas as contas têm de reter os direitos de administrador do sistema no SQL Server. Não remova os direitos de administrador do sistema destas contas.  

-   O computador do servidor do site secundário tem de cumprir todas as configurações de pré-requisitos, que inclui o SQL Server e as funções do sistema de sites predefinido do ponto de gestão e ponto de distribuição.  
