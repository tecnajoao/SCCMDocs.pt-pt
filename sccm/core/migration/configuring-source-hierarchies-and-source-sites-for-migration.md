---
title: "Hierarquias de origem de migração"
titleSuffix: Configuration Manager
description: Configure uma hierarquia de origem e sites de origem, pelo que pode migrar dados para o seu ambiente do System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 7977f66c71da300c59c7781f09975ca08ddea0b9
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para permitir a migração de dados para o seu ambiente do System Center Configuration Manager, tem de configurar uma hierarquia de origem suportada do Configuration Manager e um ou mais sites de origem nessa hierarquia que contenham dados que pretende migrar.  

> [!NOTE]  
>  As operações de migração são executadas no site de nível superior na hierarquia de destino. Se configurar a migração quando utilizar uma consola do Configuration Manager que está ligada a um site primário subordinado, tem de dar tempo para a configuração para replicar para o site de administração central, o início e, em seguida, replicar o estado para o site primário ao qual estão ligados.  

 Utilize as informações e procedimentos das secções seguintes para especificar hierarquia de origem e adicionar outros sites de origem. Depois de concluir estes procedimentos, pode criar tarefas de migração e começar a migrar dados da hierarquia de origem para a hierarquia de destino.  

-   [Especificar uma hierarquia de origem para migração](#BKBM_ConfigSrcHierarchy)  

-   [Identificar sites de origem adicionais da hierarquia de origem](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a>Especificar uma hierarquia de origem para migração  
 Para migrar dados para a hierarquia de destino, tem de especificar uma hierarquia de origem suportada que tem os dados que pretende migrar. Por predefinição, no site de nível superior dessa hierarquia torna-se um site de origem da hierarquia de origem. Se migrar de uma hierarquia do Configuration Manager 2007, pode, em seguida, configurar sites de origem adicionais para migração após a recolha de dados do site de origem inicial. Se migrar de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager, não terá de configurar sites de origem adicionais para migrar os dados da hierarquia de origem. Isto acontece porque estas versões do Configuration Manager utilizarem uma base de dados partilhada que está disponível no site de nível superior da hierarquia de origem. A base de dados partilhado tem todas as informações que pode migrar.  

 Utilize os procedimentos seguintes para especificar uma hierarquia de origem para migração e para identificar sites de origem adicionais numa hierarquia do Configuration Manager 2007.  

 Execute este procedimento com uma consola do Configuration Manager que está ligada à hierarquia de destino:  

### <a name="to-configure-a-source-hierarchy"></a>Para configurar uma hierarquia de origem   

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  No **home page** separador o **migração** , clique em **especificar hierarquia de origem**.  

4.  No **especificar hierarquia de origem** caixa de diálogo, para **hierarquia de origem**, selecione **nova hierarquia de origem**.  

5.  Para **servidor do site de nível superior Configuration Manager**, introduza o nome ou endereço IP do site de nível superior de uma hierarquia de origem suportada.  

6.  Especificar contas de acesso de site de origem tem as seguintes permissões:  

    -   Conta de Site de origem: **Leitura** permissão para o fornecedor de SMS para o site de nível superior especificado na hierarquia de origem. A partilha do ponto de distribuição e atualizações requerem **modificar** e **eliminar** permissões para o site na hierarquia de origem.

    -   Conta de base de dados do Site de origem: **Leitura** e **executar** permissão para a base de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

     Se especificar a utilização da conta de computador, o Configuration Manager utiliza a conta de computador do site de nível superior da hierarquia de destino. Para esta opção, certifique-se de que esta conta é um membro do grupo de segurança **utilizadores COM distribuídos** no domínio onde reside o site de nível superior da hierarquia de origem.  

7.  Para partilhar pontos de distribuição entre as hierarquias de origem e de destino, selecione o **ativar partilha do servidor do site de origem do ponto de distribuição** caixa de verificação. Se não ativar o ponto de distribuição de partilha neste momento, pode efetuar para que editando as credenciais do site de origem após dados recolha terminou.  

8.  Clique em **OK** para guardar a configuração. Esta ação abre o **estado de recolha de dados** caixa de diálogo e recolha de dados é iniciada automaticamente.  

9. Quando estiver concluída, a recolha de dados clique **fechar** para fechar o **estado de recolha de dados** diálogo caixa e concluir a configuração.  

##  <a name="BKBM_ConfigSrcSites"></a>Identificar sites de origem adicionais da hierarquia de origem  
 Quando configura uma hierarquia de origem suportada, o site de nível superior dessa hierarquia é automaticamente configurado como um site de origem e dados são recolhidos automaticamente a partir desse site. A próxima ação que tomar depende da versão do Configuration Manager que é executada pela hierarquia de origem:  

-   Para uma hierarquia de origem do Configuration Manager 2007, pode começar a migração a partir desse site de origem inicial ou configurar sites de origem adicionais da hierarquia de origem após a conclusão da recolha de dados para o site de origem inicial. Para migrar os dados que estão disponíveis apenas de um site subordinado, configure sites de origem adicionais para uma hierarquia do Configuration Manager 2007. Por exemplo, pode configurar sites de origem adicionais para recolher dados sobre o conteúdo que pretende migrar quando é criado um site subordinado na hierarquia de origem e não está disponível no site de nível superior da hierarquia de origem.  

-   Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, não terá de configurar sites de origem adicionais. Isto acontece porque estas versões do Configuration Manager utilizarem uma base de dados partilhada que está disponível no site de nível superior da hierarquia de origem. A base de dados partilhado tem todas as informações que pode migrar de todos os sites dessa hierarquia de origem. Isto disponibiliza os dados que pode migrar do site de nível superior da hierarquia de origem.  

Quando configura sites de origem adicionais para uma hierarquia de origem do Configuration Manager 2007, tem de configurar sites de origem adicionais do nível superior da hierarquia de origem para a parte inferior. Tem de configurar um site principal como um site de origem antes de configurar qualquer um dos respetivos sites subordinados como sites de origem.  

Utilize o procedimento seguinte para configurar sites de origem adicionais para hierarquias de origem do Configuration Manager 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar sites de origem adicionais numa hierarquia de origem 

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Escolha o site que pretende configurar como site de origem.  

4.  No separador **Home Page** , no grupo **Site de Origem** , clique em **Configurar**.  

5.  No **credenciais do Site de origem** caixa de diálogo, para as contas de acesso do site de origem, especifique contas com as seguintes permissões:  

    -   Conta de Site de origem: **Leitura** permissão para o fornecedor de SMS para o site de nível superior especificado na hierarquia de origem. A partilha do ponto de distribuição e atualizações requerem **modificar** e **eliminar** permissões para o site na hierarquia de origem.  

    -   Conta de base de dados do Site de origem: **Leitura** e **executar** permissão para a base de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

    Se especificar a utilização da conta de computador, o Configuration Manager utiliza a conta de computador do site de nível superior da hierarquia de destino. Para esta opção, certifique-se de que esta conta é um membro do grupo de segurança **utilizadores COM distribuídos** no domínio onde reside o site de nível superior da hierarquia de origem.  

6.  Para partilhar pontos de distribuição entre as hierarquias de origem e de destino, selecione o **ativar partilha do servidor do site de origem do ponto de distribuição** caixa de verificação. Se não ativar o ponto de distribuição de partilha neste momento, pode efetuar para que editando as credenciais para o site de origem após dados recolha terminou.  

7. Clique em **OK** para guardar a configuração. Esta ação abre o **estado de recolha de dados** caixa de diálogo e recolha de dados é iniciada automaticamente.  

8.  Quando estiver concluída, a recolha de dados clique **fechar** para concluir a configuração.  
