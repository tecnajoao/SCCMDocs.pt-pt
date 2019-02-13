---
title: Hierarquias de origem de migração
titleSuffix: Configuration Manager
description: Configure uma hierarquia de origem e sites de origem para que possa migrar dados para o seu ambiente do System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a2b336173df72a2b54bd92cda4477df58e4dac5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125998"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para ativar a migração de dados ao seu ambiente do System Center Configuration Manager, tem de configurar uma hierarquia de origem suportadas do Configuration Manager e um ou mais sites de origem nessa hierarquia que contenham dados que pretende migrar.  

> [!NOTE]  
>  As operações de migração são executadas no site de nível superior na hierarquia de destino. Se configurar a migração quando utiliza uma consola do Configuration Manager que está ligada a um site primário subordinado, tem de dar tempo para que a configuração seja replicada para o site de administração central, o início e, em seguida, replicar o estado de volta para o site primário para que está ligado.  

 Utilize as informações e procedimentos nas secções seguintes para especificar a hierarquia de origem e adicionar outros sites de origem. Depois de concluir estes procedimentos, pode criar tarefas de migração e começar a migrar os dados da hierarquia de origem à hierarquia de destino.  

-   [Especificar uma hierarquia de origem para migração](#BKBM_ConfigSrcHierarchy)  

-   [Identificar sites de origem adicionais da hierarquia de origem](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a> Especificar uma hierarquia de origem para migração  
 Para migrar dados para a hierarquia de destino, tem de especificar uma hierarquia de origem suportada que tenha os dados que pretende migrar. Por predefinição, o site de nível superior dessa hierarquia torna-se um site de origem da hierarquia de origem. Se migrar de uma hierarquia do Configuration Manager 2007, pode, em seguida, configurar sites de origem adicionais para a migração após a recolha de dados do site de origem inicial. Se migrar de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager, não precisa de configurar sites de origem adicionais para migrar os dados da hierarquia de origem. Isto acontece porque essas versões do Configuration Manager utilizam uma base de dados partilhada que está disponível no site de nível superior da hierarquia de origem. A base de dados partilhado tem todas as informações que pode migrar.  

 Utilize os procedimentos seguintes para especificar uma hierarquia de origem para migração e para identificar sites de origem adicionais numa hierarquia do Configuration Manager 2007.  

 Execute este procedimento com uma consola do Configuration Manager que está ligada à hierarquia de destino:  

### <a name="to-configure-a-source-hierarchy"></a>Para configurar uma hierarquia de origem   

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3. Sobre o **home page** separador a **migração** , clique em **especificar hierarquia de origem**.  

4. Na **especificar hierarquia de origem** caixa de diálogo, para **hierarquia de origem**, selecione **nova hierarquia de origem**.  

5. Para **servidor do site de nível superior Configuration Manager**, introduza o nome ou endereço IP do site de nível superior de uma hierarquia de origem suportada.  

6. Especifica contas de acesso de site de origem que tenham as seguintes permissões:  

   - Conta de Site de origem: **Leitura** permissão ao fornecedor de SMS para o site de nível superior especificado na hierarquia de origem. Partilha do ponto de distribuição e as atualizações requerem **Modify** e **eliminar** permissões para o site na hierarquia de origem.

   - Conta de base de dados do Site de origem: **Leia** e **Execute** permissão para a base de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

     Se especificar a utilização da conta de computador, o Configuration Manager utiliza a conta de computador do site de nível superior da hierarquia de destino. Para esta opção, certifique-se de que esta conta é membro do grupo de segurança **Distributed COM-usuários** no domínio onde reside o site de nível superior da hierarquia de origem.  

7. Para partilhar pontos de distribuição entre as hierarquias de origem e de destino, selecione o **ativar partilha para o servidor de site de origem do ponto de distribuição** caixa de verificação. Se não ativar o ponto de distribuição de partilha neste momento, pode fazê-lo, editando as credenciais do site de origem depois de dados a recolher foi concluída.  

8. Clique em **OK** para guardar a configuração. Esta ação abre o **estado de recolha de dados** caixa de diálogo e dados de coleta é iniciada automaticamente.  

9. Quando os dados de recolha estiver concluído, clique em **feche** para fechar a **estado de recolha de dados** diálogo caixa e concluir a configuração.  

##  <a name="BKBM_ConfigSrcSites"></a> Identificar sites de origem adicionais da hierarquia de origem  
 Quando configura uma hierarquia de origem suportada, o site de nível superior dessa hierarquia é automaticamente configurado como um site de origem e dados são recolhidos automaticamente a partir desse site. A próxima ação que tomar depende da versão do Configuration Manager que é executada pela hierarquia de origem:  

-   Para uma hierarquia de origem do Configuration Manager 2007, pode começar a migração a partir desse site de origem inicial ou configurar sites de origem adicionais da hierarquia de origem após a conclusão da recolha de dados para o site de origem inicial. Para migrar os dados que só estão disponíveis de um site subordinado, configure sites de origem adicionais para uma hierarquia do Configuration Manager 2007. Por exemplo, pode configurar sites de origem adicionais para recolher dados sobre o conteúdo que pretende migrar quando ele é criado num site subordinado na hierarquia de origem e não está disponível no site superior da hierarquia de origem.  

-   Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, não terá de configurar sites de origem adicionais. Isto acontece porque essas versões do Configuration Manager utilizam uma base de dados partilhada que está disponível no site de nível superior da hierarquia de origem. A base de dados partilhado tem todas as informações que pode migrar de todos os sites dessa hierarquia de origem. Isso faz com que os dados que podem ser migrados disponíveis do site de nível superior da hierarquia de origem.  

Quando configurar sites de origem adicionais para uma hierarquia de origem do Configuration Manager 2007, tem de configurar sites de origem adicionais da parte superior da hierarquia de origem para a parte inferior. Tem de configurar um site principal como site de origem antes de configurar qualquer um dos respetivos sites subordinados como sites de origem.  

Utilize o procedimento seguinte para configurar sites de origem adicionais para hierarquias de origem do Configuration Manager 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar sites de origem adicionais na hierarquia de origem 

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Escolha o site que pretende configurar como site de origem.  

4.  No separador **Home Page** , no grupo **Site de Origem** , clique em **Configurar**.  

5.  Na **credenciais do Site de origem** caixa de diálogo, para as contas de acesso do site de origem, especifique as contas que têm as seguintes permissões:  

    -   Conta de Site de origem: **Leitura** permissão ao fornecedor de SMS para o site de nível superior especificado na hierarquia de origem. Partilha do ponto de distribuição e as atualizações requerem **Modify** e **eliminar** permissões para o site na hierarquia de origem.  

    -   Conta de base de dados do Site de origem: **Leia** e **Execute** permissão para a base de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

    Se especificar a utilização da conta de computador, o Configuration Manager utiliza a conta de computador do site de nível superior da hierarquia de destino. Para esta opção, certifique-se de que esta conta é membro do grupo de segurança **Distributed COM-usuários** no domínio onde reside o site de nível superior da hierarquia de origem.  

6.  Para partilhar pontos de distribuição entre as hierarquias de origem e de destino, selecione o **ativar partilha para o servidor de site de origem do ponto de distribuição** caixa de verificação. Se não ativar o ponto de distribuição de partilha neste momento, pode fazê-lo, editando as credenciais para o site de origem depois de dados a recolher foi concluída.  

7. Clique em **OK** para guardar a configuração. Esta ação abre o **estado de recolha de dados** caixa de diálogo e dados de coleta é iniciada automaticamente.  

8.  Quando os dados de recolha estiver concluído, clique em **fechar** para concluir a configuração.  
