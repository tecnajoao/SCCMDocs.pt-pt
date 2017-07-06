---
title: "Pré-requisitos de migração | Documentos do Microsoft"
description: "Compreenda as versões suportadas do Configuration Manager, idiomas suportados do site de origem e as configurações necessárias para a migração."
ms.custom: na
ms.date: 3/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ee7f69bd65152deffb2456d9807e1e8fee8802ec
ms.openlocfilehash: cd90f5462ac4bb4c0a2021e6d5dde65161b9c5f6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>Pré-requisitos de migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para migrar de uma hierarquia de origem suportada, tem de ter acesso a cada site de origem aplicável do Configuration Manager e as permissões no site de destino do System Center Configuration Manager para configurar e executar operações de migração.  

 Utilize as informações nas secções seguintes para ajudar a compreender as versões do Configuration Manager que são suportadas para migração e as configurações necessárias.  

-   [Versões do Configuration Manager que são suportadas para migração](#BKMK_SupportedMigrationVersions)  

-   [Idiomas do site de origem que são suportados para migração](#BKMK_SorceSiteLanguage)  

-   [Configurações necessárias para a migração](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> Versões do Configuration Manager que são suportadas para migração  
 Pode migrar dados a partir de uma hierarquia de origem que execute qualquer uma das seguintes versões do Configuration Manager:  

-   Configuration Manager 2007 SP2 (para efeitos de migração, Configuration Manager 2007 R2 ou R3 no site de origem não são uma consideração significativa. Desde que a origem site é executada SP2, sites com o suplemento a R2 ou R3 instalado é suportada para migração para o System Center Configuration Manager).  

-   System Center 2012 Configuration Manager SP2 ou System Center 2012 R2 Configuration Manager SP1.  

    > [!TIP]  
    >  Além de migração, pode utilizar uma atualização direta de sites que executam o System Center 2012 Configuration Manager para System Center Configuration Manager.  

-   Uma hierarquia do System Center Configuration Manager de versão igual ou menor do System Center Configuration Manager.  

  Por exemplo, se tiver uma hierarquia de destino que executa o System Center Configuration Manager 1606, pode utilizar a migração para copiar dados de uma hierarquia de origem que é executado versão 1606 ou 1602. No entanto não foi possível migrar dados a partir de uma hierarquia de origem que é executado 1610.  


##  <a name="BKMK_SorceSiteLanguage"></a> Idiomas do site de origem que são suportados para migração  
 Ao migrar dados entre hierarquias do Configuration Manager, os dados são armazenados na hierarquia de destino no formato independente de idiomas para o System Center Configuration Manager. Porque Manager2007 de configuração não armazena dados num formato independente de idiomas, o processo de migração deve converter objetos nesse formato durante a migração do Configuration Manager 2007. Por conseguinte, apenas do Configuration Manager 2007 sites de origem que são instalados com os seguintes idiomas são suportados para migração:  

-   Inglês  

-   Francês  

-   Alemão  

-   Japonês  

-   Coreano  

-   Russo  

-   Chinês Simplificado  

-   Chinês Tradicional  

Ao migrar dados a partir de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager, não existem sem limitações de idioma do site de origem. Os objetos da base de dados do site de origem já estão num formato independente de idiomas.  

##  <a name="BKMK_Required_Configurations"></a> Configurações necessárias para a migração  
Seguem-se as configurações necessárias para utilizar a migração e as operações de migração:  

-   **Para configurar, executar e monitorizar a migração na consola do Configuration Manager:**  

     No site de destino, deve ser atribuída à sua conta a função de segurança de administração baseada em funções do **Administrador de Infraestrutura**. Esta função de segurança concede permissões para gestão de todas as operações de migração, incluindo a criação de tarefas de migração, limpeza e monitorização e a ação de partilhar e atualizar pontos de distribuição.  

-   **Recolha de Dados:**  

     Para ativar o site de destino para a recolha de dados, é necessário configurar as duas contas de acesso ao site de origem indicadas a seguir para utilização com cada site de origem:  

    -   **Conta de Site de origem:** Esta conta é utilizada para aceder ao fornecedor de SMS do site de origem.  

        -   Para um site de origem de configuração Manager2007 SP2, esta conta requer **leitura** permissão para todos os objetos de site de origem.  

        -   Para um site de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, esta conta requer **leitura** permissão para todos os objetos de site de origem, pode conceder esta permissão à conta utilizando a administração baseada em funções. Para obter mais informações sobre como utilizar a administração baseada em funções, veja [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    -   **Conta de base de dados do Site de origem:** Esta conta é utilizada para aceder à base de dados do SQL Server do site de origem e necessita **ligar**, **executar**, e **selecione** permissões para a base de dados do site de origem.  

    Pode configurar estas contas durante a configuração de uma nova hierarquia de origem, a recolha de dados de um site de origem adicional ou a reconfiguração das credenciais de um site de origem. Estas contas podem utilizar uma conta de utilizador de domínio ou o utilizador pode especificar a conta de computador do site de nível superior da hierarquia de destino.  

    > [!IMPORTANT]  
    >  Se utilizar a conta de computador do Configuration Manager para nenhuma das contas de acesso, certifique-se de que esta conta é membro do grupo de segurança **utilizadores COM distribuídos** no domínio onde reside o site de origem.  

    Durante a recolha de dados, são utilizados os protocolos de rede e as portas seguintes:  

    -   NetBIOS/SMB - 445 (TCP)  

    -   RPC (WMI) - 135 (TCP)  

    -   SQL Server - As portas TCP utilizadas pelas bases de dados dos sites de origem e de destino.  

-   **Migrar Atualizações de Software:**  

     Para poder migrar as atualizações de software, é necessário configurar a hierarquia de destino com um ponto de atualização de software. Para obter mais informações, veja [Planear a migração de atualizações de software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

-   **Partilhar pontos de distribuição:**  

     Para partilhar pontos de distribuição com sucesso a partir de um site de origem, pelo menos um site primário ou o site de administração central da hierarquia de destino deve utilizar os mesmos números da porta que os do site de origem para os pedidos do cliente. Para obter informações sobre as portas de pedidos de cliente, veja [How to configure client communication ports in System Center Configuration Manager (Como configurar portas de comunicação de cliente no System Center Configuration Manager)](../../core/clients/deploy/configure-client-communication-ports.md).  

     Em cada site de origem, são partilhados apenas os pontos de distribuição que estão instalados em servidores do sistema de sites configurados com um FQDN.  

     Além disso, para partilhar um ponto de distribuição a partir de um site de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, o **conta Site de origem** (que acede ao fornecedor de SMS para o servidor de site de origem), tem de ter **modificar** permissões para o **Site** objeto no site de origem. Esta permissão é concedida à conta utilizando a administração baseada em funções. Para obter mais informações sobre como utilizar a administração baseada em funções, veja [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


-   **Atualizar ou reatribuir pontos de distribuição:**  

     A **Conta de Acesso ao Site de Origem** configurada para recolher dados a partir de um Fornecedor de SMS do site de origem tem de ter as seguintes permissões:  

    -   Para atualizar um ponto de distribuição Manager2007 de configuração, a conta necessita de **leitura**, **executar**, e **eliminar** permissões para o **Site** classe no servidor do site Manager2007 de configuração para remover com sucesso o ponto de distribuição do site de origem de configuração Manager2007  

    -   Para reatribuir um ponto de distribuição do System Center 2012 Configuration Manager ou System Center Configuration Manager, a conta deve ter **modificar** permissão para o **Site** objeto no site de origem. Esta permissão é concedida à conta utilizando a administração baseada em funções. Para obter mais informações sobre como utilizar a administração baseada em funções, veja [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

     Para atualizar ou reatribuir com sucesso um ponto de distribuição a uma nova hierarquia, as portas configuradas para pedidos de cliente no site que efetua a gestão do ponto de distribuição na hierarquia de origem devem ser iguais às portas configuradas para pedidos de cliente no site de destino que efetuará a gestão do ponto de distribuição. Para obter informações sobre as portas de pedidos de cliente, veja [How to configure client communication ports in System Center Configuration Manager (Como configurar portas de comunicação de cliente no System Center Configuration Manager)](../../core/clients/deploy/configure-client-communication-ports.md).  
