---
title: "Pré-requisitos para sites | Documentos do Microsoft"
description: "Saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager do System Center."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ff89d4aea6be871e64e0a788f054ba4cadb3e51d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Pré-requisitos para a instalação de sites do Configuration Manager do System Center

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de iniciar uma instalação de site, é uma boa ideia para saber mais sobre os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager do System Center.

## <a name="primary-sites-and-the-central-administration-site"></a>Sites primários e o site de administração central
Os pré-requisitos seguintes aplicam-se a instalação de um site de administração central como o primeiro site numa hierarquia, instalar um site primário autónomo ou instalar um site primário subordinado. Se estiver a instalar um site de administração central como parte de uma expansão da hierarquia, consulte o artigo [expandir um site primário autónomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) neste tópico.

###  <a name="bkmk_PrereqPri"></a>Pré-requisitos para instalar um site primário ou um site de administração central  

-   A conta de utilizador que instala o site tem de ter os seguintes direitos de:  

    -   **Administrador** no computador do servidor de site  
    -   **Administrador** em cada computador que alojará o **base de dados do site** ou uma instância do **fornecedor de SMS** para o site  
    -   **Sysadmin** na instância do SQL Server que aloja a base de dados do site  

        > [!IMPORTANT]  
        >  Após a conclusão do programa de configuração, a conta de utilizador que executa a configuração e a conta de computador do servidor de site têm de reter os direitos sysadmin no SQL Server. Não remova os direitos sysadmin destas contas.  

-   Se estiver a instalar um site primário, terá dos seguintes direitos de adicionais:  
    -  **Administrador** em computadores adicionais onde irá instalar o ponto de gestão inicial e o ponto de distribuição if not no servidor do site  

-   Se estiver a instalar um novo site primário subordinado abaixo de um site de administração central, terá dos seguintes direitos de adicionais:  

    -   **Administrador** no computador que aloja o site de administração central  

    -   Direitos de administração baseada em funções no Configuration Manager que sejam equivalentes à função de segurança de **administrador de infraestrutura** ou **administrador total**  

-   Tem de utilizar o suporte de dados de instalação correto (ficheiros de origem) e execute a configuração a partir dessa localização. Para obter informações sobre os ficheiros de origem correta a utilizar para instalar diferentes tipos de sites, consulte o artigo [opções para a instalação diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) no [preparar a instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) tópico.

-   Computador do servidor do site tem de ter acesso a ficheiros de configuração atualizados da Microsoft, de uma das seguintes formas:
    -  Antes de iniciar a instalação, pode transferir e armazenar uma cópia destes ficheiros na rede local utilizando [dispositivo de transferência da configuração](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Se copiar um local destes ficheiros não está disponível, o servidor do site tem de ter acesso à Internet, de modo que pode transferir estes ficheiros da Microsoft durante a instalação.

- Antes de poder expandir um site primário autónomo que tenha uma ligação função ponto de serviço site system instalada, terá de desinstalar o ponto de ligação de serviço. Apenas uma instância desta função é permitida numa hierarquia e apenas é permitida no site de nível superior da hierarquia. Terá a oportunidade de reinstalar a função durante a instalação do site de administração central.
- O servidor do site e computadores de base de dados do site tem de cumprir todas as configurações de pré-requisitos. Antes de iniciar o programa de configuração, pode [executar manualmente o Verificador de pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar e corrigir problemas.  


### <a name="bkmk_expand"></a>Pré-requisitos para expandir um site primário autónomo
Pode expandi-lo para uma hierarquia com um site de administração central, um site primário autónomo tem de cumprir os seguintes pré-requisitos:

-   **Tem de instalar da nova instalação de site de administração central utilizando suportes de dados a partir de um CD. Pasta mais recente (que contém os ficheiros de origem) que corresponde à versão do site primário autónomo**

 Para garantir uma correspondência de versão, utilize os ficheiros de origem localizado no [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) no site primário autónomo.

 Para obter mais informações acerca dos ficheiros de origem correta a utilizar para instalar vários sites, consulte o artigo [opções para a instalação diferentes tipos de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) no [preparar a instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) tópico.


-   **O site primário autónomo não pode ser configurado para migrar dados a partir de outra hierarquia do Configuration Manager**  

     Tem de parar a migração ativa para o site primário autónomo a partir de outras hierarquias do Configuration Manager e remover todas as configurações de migração. Isto inclui tarefas de migração que ainda não estão concluídas, a recolha de dados e a configuração da hierarquia de origem ativa.  

     Isto é necessário pois operações de migração são realizadas pelo site de nível superior da hierarquia e as configurações de migração não são transferidas para o site de administração central quando expande um site primário autónomo.  

     Depois de expandir o site primário autónomo, se reconfigurar a migração no site primário, o site de administração central executará as operações relacionadas com a migração. Para obter mais informações sobre como configurar a migração, consulte o artigo [configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **A conta de computador do computador que alojará o novo site de administração central tem de ser um membro do grupo de utilizador administrador no site primário standa lone**  

     Para expandir com êxito o site primário autónomo, a conta de computador do novo site de administração central tem de ter **administrador** direitos no site primário autónomo. Isto é necessário apenas durante a expansão do site. A conta pode ser removida do grupo de utilizador no site primário quando a expansão do site estiver concluída.  

-   **A conta de utilizador que executa o programa de configuração para instalar o novo site de administração central tem de ter direitos de administração baseada em funções no site primário autónomo**  

     Para instalar um site de administração central como parte de uma expansão do site, a conta de utilizador que executa a configuração para instalar o site de administração central tem de ser definida na administração baseada em funções no site primário autónomo como um **administrador total** ou uma **administrador de infraestrutura**.  

-   **Tem de desinstalar as seguintes funções de sistema de sites a partir do site primário autónomo antes de poder expandir o site:**  

    -   Ponto de sincronização do Asset Intelligence  
    -   Ponto de Endpoint Protection  
    -   Ponto de ligação de serviço  

   Estas funções de sistema de sites são suportadas apenas no site de nível superior da hierarquia. Por conseguinte, tem de desinstalar estas funções de sistema de sites antes de expandir o site primário autónomo. Depois de expandir o site, pode reinstalar estas funções de sistema de sites no site de administração central.  

    Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

-   **A porta para o SQL Server Service Broker (SSB) entre o site primário autónomo e o computador que irá instalar o site de administração central tem de estar aberta**  

     Para replicar com êxito os dados entre um site de administração central e um site primário, o Configuration Manager requer uma porta abra entre os dois sites para SSB a utilizar. Quando instala um site de administração central e expandir um site primário autónomo, a verificação dos pré-requisitos não verifica que a porta especificada para o SSB está aberta no site primário.  


## <a name="bkmk_secondary"></a>Sites secundários
Seguem-se os pré-requisitos para instalar os sites secundários:
-   O administrador que configura a instalação do site secundário na consola do Configuration Manager tem de ter direitos de administração baseada em funções que sejam equivalentes à função de segurança de **administrador de infraestrutura** ou **administrador total**.  
-   A conta de computador do site primário principal tem de ser um **administrador** no computador do servidor de site secundário.  
-   Quando o site secundário utiliza uma instância anteriormente instalada do SQL Server para alojar a base de dados do site secundário:  

    -   O **conta de computador** do elemento principal site primário tem de ter **sysadmin** direitos a instância do SQL Server no computador do servidor do site secundário.  

    -   O **Sistema Local** conta de computador do servidor do site secundário tem de ter **sysadmin** direitos a instância do SQL Server no computador do servidor do site secundário.  

        > [!IMPORTANT]  
        >  Após a conclusão do programa de configuração, ambas as contas têm de reter os direitos sysadmin no SQL Server. Não remova os direitos sysadmin destas contas.  

-   Computador do servidor do site secundário tem de cumprir todas as configurações de pré-requisitos, que inclui o SQL Server e as funções de sistema de sites predefinidas do ponto de gestão e ponto de distribuição.  

