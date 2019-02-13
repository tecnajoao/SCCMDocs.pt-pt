---
title: Pré-requisitos para sites
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a56739eee4d116014f89b3a7e7835e3e87a62ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124593"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Pré-requisitos para instalar sites do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de iniciar uma instalação de site, saiba mais sobre os pré-requisitos para instalar os diferentes tipos de sites do Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Sites primários e o site de administração central

Os seguintes pré-requisitos aplicam-se para instalar um dos seguintes tipos:
- Um site de administração central como o primeiro site de uma hierarquia
- Um site primário autónomo
- Um site primário subordinado

Se estiver a instalar um site de administração central como parte de uma expansão da hierarquia, consulte [expandir um site primário autónomo](#bkmk_expand).


###  <a name="bkmk_PrereqPri"></a> Pré-requisitos para instalar um site primário ou site de administração central  

- A conta de utilizador que instala o site tem de ter os seguintes direitos de:  

    - **Administrador** nos seguintes servidores:  
        - O servidor do site  
        - Cada servidor que aloja o **base de dados do site**  
        - Cada instância do **fornecedor de SMS** para o site  

    - **Administrador do sistema** na instância do SQL Server que aloja a base de dados do site  

        > [!IMPORTANT]  
        >  Quando concluir a configuração do Configuration Manager, tanto a conta de utilizador que executa a configuração e a conta de computador do servidor de site têm de reter os direitos de administrador do sistema no SQL Server. Não remova os direitos de administrador do sistema a estas contas.  

- Se estiver a instalar um site primário, tem os seguintes direitos adicionais:  

    - **Administrador** em servidores adicionais em que instalar o ponto de gestão inicial e o ponto de distribuição; caso contrário, no servidor do site  

- Se estiver a instalar um novo site primário subordinado abaixo de um site de administração central, terá os direitos adicionais seguintes:  

    - **Administrador** no servidor que aloja o site de administração central  

    - Direitos de administração baseada em funções dentro do Configuration Manager que são equivalentes à função de segurança de **administrador de infraestrutura** ou **administrador total**  

- Utilize os ficheiros de origem de instalação correta e executar a configuração a partir dessa localização. Para obter informações sobre os ficheiros de origem correto a utilizar para instalar vários tipos de sites, consulte [opções para instalar vários tipos de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

- O servidor do site tem de ter acesso aos ficheiros de configuração atualizados da Microsoft, de uma das seguintes formas:  

    - Antes de iniciar a instalação, transferir e armazenar uma cópia desses arquivos na sua rede local. Para obter mais informações, consulte [programa de configuração](/sccm/core/servers/deploy/install/setup-downloader).  

    - Se uma cópia local destes ficheiros não estiver disponível, o servidor do site tem de ter acesso à internet. Estes ficheiros são transferidas da Microsoft durante a instalação.  

- O servidor do site e o servidor de base de dados do site tem de cumprir todas as configurações de pré-requisitos. Antes de iniciar a configuração do Configuration Manager, [executar manualmente o Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) para identificar e corrigir problemas.  


### <a name="bkmk_expand"></a> Pré-requisitos para expandir um site primário autónomo

Pode expandi-lo para uma hierarquia com um site de administração central, um site primário autónomo tem de cumprir os seguintes pré-requisitos:

#### <a name="source-file-version-matches-site-version"></a>Versão do ficheiro de origem corresponde à versão do site
Instale o novo site de administração central com suportes de dados de um CD. Pasta mais recente que corresponde à versão do site primário autónomo. Para certificar-se de que as versões correspondem, utilize os ficheiros de origem encontrados no [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) no site primário autónomo. 

Para obter mais informações acerca dos ficheiros de origem correta a utilizar para instalar sites diferentes, consulte [opções para instalar vários tipos de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Parar a migração ativa de outra hierarquia
Não é possível configurar o site primário autónomo para migrar dados de outra hierarquia do Configuration Manager. Parar a migração ativa para o site primário autónomo de outras hierarquias do Configuration Manager e remova todas as configurações para a migração. Estas configurações incluem: 
- Tarefas de migração que ainda não foi concluída  
- Recolha de dados  
- A configuração da hierarquia de origem Ativa  

Esta configuração é necessária porque o Configuration Manager efetua a migração de dados do site de nível superior da hierarquia. Quando expande um site primário autónomo, não se transferem as configurações de migração para o site de administração central.  

Depois de expandir o site primário autónomo, se reconfigurar a migração no site primário, o site de administração central realiza as operações de migração. 

Para obter mais informações sobre como configurar a migração, consulte [configurar hierarquias de origem e sites de origem para migração](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration).  

#### <a name="computer-account-as-administrator"></a>Conta de computador como administrador
A conta de computador do servidor que aloja o novo site de administração central tem de ser um membro do **administrador** grupo no servidor do site primário autónomo. 

Para expandir com êxito o site primário autónomo, a conta de computador do novo site de administração central tem de ter **administrador** direitos no site primário autónomo. Isto é necessário apenas durante a expansão do site. Quando é concluída a expansão do site, pode remover a conta do grupo de utilizadores no site primário.  

#### <a name="installation-account-permissions"></a>Permissões de conta de instalação
A conta de utilizador que executa a configuração do Configuration Manager para instalar o novo site de administração central tem de ter direitos de administração baseada em funções no site primário autónomo.

Para instalar um site de administração central como parte de uma expansão do site, a conta de utilizador que executa a configuração para instalar o site de administração central tem de ser definida na administração baseada em funções no site primário autónomo como um **completo Administrador** ou uma **administrador de infraestrutura**.  

#### <a name="top-level-site-roles"></a>Funções de site de nível superior
Antes de expandir o site, desinstale as seguintes funções de sistema de sites do site primário autónomo:

- Ponto de sincronização do Asset Intelligence  
- Ponto de Endpoint Protection  
- Ponto de ligação de serviço  

O Configuration Manager só suporta estas funções no site de nível superior da hierarquia. Desinstale estas funções de sistema de sites antes de expandir o site primário autónomo. Depois de expandir o site, reinstale estas funções de sistema de sites no site de administração central.  

Todas as outras funções do sistema de site podem permanecer instaladas no site primário.  

#### <a name="open-the-sql-server-service-broker-port"></a>Abra a porta do SQL Server Service Broker
A porta de rede tem de estar aberta para o SQL Server Service Broker (SSB) entre o site primário autónomo e o servidor do site de administração central.  

Para replicar com êxito os dados entre um site de administração central e um site primário, o Configuration Manager requer uma porta aberta entre os dois sites para SSB a utilizar. Quando instala um site de administração central e expandir um site primário autónomo, a verificação de pré-requisitos não verifica que a porta especificada para o SSB está aberta no site primário.  

#### <a name="known-issues-with-azure-services"></a>Problemas conhecidos com serviços do Azure
Quando utiliza um dos seguintes serviços do Azure com o Configuration Manager, depois de expandir o site, remover e, em seguida, recriar a ligação a esse serviço.

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [Preparação para atualização](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

Utilize os seguintes passos para resolver este problema:
 1. Na consola do Configuration Manager, eliminar o serviço do Azure a partir da **dos serviços do Azure** nó.  

 2. No portal do Azure, elimine o inquilino que está associada com o serviço a partir do nó de inquilinos do Azure Active Directory. Esta ação também elimina a aplicação web do Azure AD que tenha associado ao serviço.  

 3. Reconfigure a ligação ao serviço do Azure para utilização com o Configuration Manager.  



## <a name="bkmk_secondary"></a> Sites secundários

Seguem-se os pré-requisitos para instalar sites secundários:

- O administrador que configura a instalação do site secundário na consola do Configuration Manager tem de ter direitos de administração baseada em funções que são equivalentes à função de segurança de **administrador de infraestrutura** ou **Administrador total**.  

- A conta de computador do site primário principal tem de ser um **administrador** no servidor do site secundário.  

- Quando o site secundário utiliza uma instância anteriormente instalada do SQL Server para alojar a base de dados do site secundário:  

    - A conta de computador do site primário principal tem de ter **sysadmin** direitos na instância do SQL Server no servidor do site secundário.  

    - O **Sistema Local** conta de computador do servidor do site secundário tem de ter **sysadmin** direitos na instância do SQL Server no servidor do site secundário.  

        > [!IMPORTANT]  
        >  Quando concluir a configuração do Configuration Manager, ambas as contas têm de reter os direitos de administrador do sistema no SQL Server. Não remova os direitos de administrador do sistema a estas contas.  

- Servidor do site secundário tem de cumprir todas as configurações de pré-requisitos. Estas configurações incluem o SQL Server e as funções de sistema de sites predefinidas do ponto de gestão e ponto de distribuição.  
