---
title: Migrar objetos
titleSuffix: Configuration Manager
description: Saiba como planear a migração de objetos entre hierarquias num ambiente do System Center Configuration Manager.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e42b7c8db3ef8c6d645d29f371fd6da475159bd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>Planear a migração de objetos do Configuration Manager para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, é possível migrar muitos dos diversos objetos associados às diferentes funcionalidades presentes num site de origem. Utilize as secções seguintes para o ajudar a planear a migração de objetos entre hierarquias.  

-   [Planear a migração de atualizações de software](#Plan_migrate_Software_updates)  

-   [Planear a migração de conteúdo](#Plan_Migrate_content)  

-   [Planear a migração de coleções](#BKMK_MigrateCollections)  

-   [Planear a migração de implementações do sistema operativo](#Plan_migrate_OSD)  

-   [Planear a migração da gestão de configuração pretendida](#Plan_Migrate_Compliance_settings)  

-   [Planear a migração de limites](#Plan_migrate_Boundaries)  

-   [Planear a migração de relatórios](#Plan_Migrate_reports)  

-   [Planear a migração organizacionais e pastas de procura](#Plan_Migrate_Org_Folders)  

-   [Planear a migração de personalizações do Asset Intelligence](#Plan_Migrate_AI)  

-   [Planear a migração de personalizações de regras de medição de software](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a> Planear a migração de atualizações de software  
 Pode migrar objetos de atualização de software, como implementações de atualizações de software e os pacotes de atualização de software.  

 Para migrar com êxito objetos de atualização de software, tem de configurar primeiro a hierarquia de destino com configurações que correspondam ao ambiente da hierarquia de origem. Isso requer as seguintes ações:  

-   Implementar um ponto de atualização de software ativo na hierarquia de destino  

-   Configurar o catálogo de produtos e idiomas para corresponderem à configuração da hierarquia de origem  

-   Sincronizar o ponto de atualização de software na hierarquia de destino com o Windows Server Update Services (WSUS)  

Ao migrar atualizações de software, tenha em consideração:  

-   Migração de objetos de atualização de software pode falhar quando não tiver sincronizado informações na sua hierarquia de destino para corresponderem à configuração da hierarquia de origem.  

    > [!WARNING]  
    >  O Configuration Manager não suporta a utilização da ferramenta WSUSutil para sincronizar os dados entre uma hierarquia de origem e de destino.  

-   Não é possível migrar atualizações personalizadas que tenham sido publicadas utilizando o System Center Updates Publisher. Em vez disso, as atualizações personalizadas devem ser republicadas na hierarquia de destino.  

Quando migra de uma hierarquia de origem do Configuration Manager 2007, o processo de migração modifica alguns objetos de atualização de software para o formato utilizado pela hierarquia de destino. Utilize a tabela seguinte para ajudar a planear a migração de objetos de atualização de software do Configuration Manager 2007.  

|Objeto do Configuration Manager 2007|Nome do objeto após a migração|  
|-----------------------------------|---------------------------------|  
|Listas de atualização de software|As listas de atualização de software são convertidas em grupos de atualização de software.|  
|Implementações de atualizações de software|As implementações de atualização de software são convertidas em implementações e grupos de atualização.<br /><br /> Depois de migrar uma implementação de atualização de software do Configuration Manager 2007, tem de ativá-la na hierarquia de destino antes de poder implementá-la.|  
|Pacotes de atualização de software|Os pacotes de atualização de software mantêm a mesma designação.|  
|Modelos de atualização de software|Os modelos de atualização de software mantêm a sua designação.<br /><br /> O **duração** valor em modelos de implementação do Configuration Manager 2007 não são migrados.|  

Quando migra objetos de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, os objetos de atualizações de software não são modificados.  

##  <a name="Plan_Migrate_content"></a> Planear a migração de conteúdo  
 É possível migrar conteúdo de uma hierarquia de origem suportada para a hierarquia de destino. Para uma hierarquia de origem do Configuration Manager 2007, este conteúdo inclui pacotes de distribuição de software, programas e aplicações virtuais, como o Microsoft Application Virtualization (App-V). Para hierarquias de origem do System Center 2012 Configuration Manager e o System Center Configuration Manager, este conteúdo inclui aplicações e aplicações virtuais App-V. Ao migrar conteúdo entre hierarquias, os ficheiros de origem comprimidos migrar para a hierarquia de destino.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Ao migrar pacotes e programas, estes não são modificados pela migração. No entanto, antes de as migrar, tem de configurar cada pacote para utilizar um caminho de convenção de Nomenclatura Universal (UNC) para a localização do ficheiro de origem. Como parte da configuração para migrar pacotes e programas, terá de atribuir um site na hierarquia de destino para gerir este conteúdo. O conteúdo não é migrado do site atribuído, mas após a migração, o site atribuído acede a localização do ficheiro de origem original utilizando o mapeamento UNC.  

 Depois de migrar um pacote e programa para a hierarquia de destino e enquanto a migração da hierarquia de origem permanece ativa, é possível disponibilizar o conteúdo aos clientes dessa hierarquia utilizando um ponto de distribuição partilhado. Para utilizar um ponto de distribuição partilhado, o conteúdo terá de permanecer acessível no ponto de distribuição do site de origem. Para mais informações sobre pontos de distribuição partilhados, consulte [partilhar pontos de distribuição entre hierarquias de origem e destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) no [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Para o conteúdo que tenha migrado, se as alterações de versão do conteúdo na hierarquia de origem ou a hierarquia de destino, os clientes já não podem aceder ao conteúdo a partir do ponto de distribuição partilhado na hierarquia de destino. Neste cenário, terá de migrar novamente o conteúdo para restaurar uma versão consistente do pacote entre a hierarquia de origem e a hierarquia de destino. Estas informações sincroniza-se durante o ciclo de recolha de dados.  

> [!TIP]  
>  Por cada pacote que migrar, atualize o pacote na hierarquia de destino. Esta ação pode evitar problemas na implementação do pacote nos pontos de distribuição na hierarquia de destino. No entanto, quando atualizar um pacote no ponto de distribuição na hierarquia de destino, os clientes nessa hierarquia deixarão de ser capaz de obter esse pacote a partir de um ponto de distribuição partilhado. Para atualizar um pacote na hierarquia de destino, na consola do Configuration Manager, vá para a biblioteca de Software, faça duplo clique no pacote e, em seguida, selecione **atualizar pontos de distribuição**. Execute esta ação para cada pacote que migrar.  

> [!TIP]  
>  Pode utilizar a conversão de pacote de Gestor do Microsoft System Center Configuration Manager para converter pacotes e programas em aplicações do System Center Configuration Manager. Transfira o Package Conversion Manager a partir do site do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=212950). Para obter mais informações, veja [Gestor de Conversão de Pacotes do Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### <a name="virtual-applications"></a>Aplicações virtuais  
Quando migra pacotes de App-V de um site suportado do Configuration Manager 2007, o processo de migração converte-os em aplicações na hierarquia de destino. Além disso, com base nos anúncios existentes para o pacote de App-V, são criados os seguintes tipos de implementação na hierarquia de destino:  

-   Se não existirem anúncios, é criado um tipo de implementação que utilize as predefinições do tipo de implementação.  

-   Se existir um anúncio, é criado um tipo de implementação que utiliza as mesmas definições como o anúncio do Configuration Manager 2007.  

-   Se existirem vários anúncios, é criado um tipo de implementação para cada anúncio do Configuration Manager 2007, utilizando as definições desse anúncio.  

> [!IMPORTANT]  
>  Se migrar um pacote de Configuration Manager 2007 App-V anteriormente migrado, a migração falhará porque os pacotes de aplicações virtuais não suportam o comportamento de migração de substituição. Neste cenário, terá de eliminar o pacote de aplicação virtual migrado da hierarquia de destino e, em seguida, criar uma nova tarefa de migração para migrar a aplicação virtual.  

> [!NOTE]  
>  Depois de migrar um pacote de App-V, pode utilizar o Assistente de atualização de conteúdo para alterar o caminho de origem para os tipos de implementação de App-V. Para obter mais informações sobre como atualizar conteúdo para um tipo de implementação, consulte como gerir tipos de implementação [tarefas de gestão do System Center Configuration Manager aplicações](../../apps/deploy-use/management-tasks-applications.md).  

Quando migra de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, pode migrar objetos do ambiente virtual de App-V, além dos tipos de implementação de App-V e aplicações. Para obter mais informações sobre os ambientes App-V, consulte [aplicações virtuais do App-V implementar com o System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Anúncios  
Pode migrar anúncios a partir de um site de origem suportado do Configuration Manager 2007 para a hierarquia de destino utilizando a migração baseada em coleções. Se atualizar um cliente, este manterá o histórico dos anúncios anteriormente executados, para impedir que o cliente volte a executar os anúncios migrados.  

> [!NOTE]  
>  Não é possível migrar anúncios para pacotes virtuais. Esta é uma exceção à migração de anúncios.  

### <a name="applications"></a>Aplicações  
 Pode migrar aplicações de uma hierarquia de origem suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager para uma hierarquia de destino. Se reatribuir um cliente da hierarquia de origem para a hierarquia de destino, o cliente manterá o histórico das aplicações anteriormente instaladas, para impedir que o cliente volte a executar as aplicações migradas.  

##  <a name="BKMK_MigrateCollections"></a> Planear a migração de coleções  
 Pode migrar os critérios de coleções de uma hierarquia de origem suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager. Para tal, utilize uma tarefa de migração baseada em objetos. Ao migrar uma coleção migrará as respetivas regras, e não as informações sobre os membros da coleção nem as informações ou objetos relacionados com os membros da coleção.  

 Migração de objeto da coleção não é suportada ao migrar a partir de uma hierarquia de origem do Configuration Manager 2007.  

##  <a name="Plan_migrate_OSD"></a> Planear a migração de implementações do sistema operativo  
É possível migrar os seguintes objetos de implementação de sistemas operativos a partir de uma hierarquia de origem suportada:  

-   Imagens e pacotes de sistemas operativos. O caminho de origem das imagens de arranque é atualizado para a localização da imagem predefinida para o Windows Administrative Installation Kit (Windows AIK) no site de destino. Eis os requisitos e limitações da migração de imagens e pacotes de sistemas operativos:  

    -   Para migrar com êxito os ficheiros de imagem, a conta de computador do servidor do fornecedor de SMS para o site de nível superior da hierarquia de destino tem de ter **leitura** e **escrever** permissão para os ficheiros de origem da imagem da localização do Windows AIK do site de origem.  

    -   Quando migra um pacote de instalação do sistema operativo, certifique-se de que a configuração do pacote nos pontos de site de origem para a pasta que tenha o ficheiro WIM e não no próprio ficheiro WIM. Se o pacote de instalação apontar para o ficheiro WIM, a migração do pacote de instalação falhará.  

    -   Quando migra um pacote de imagem de arranque a partir de um site de origem do Configuration Manager 2007, o ID de pacote do pacote não será mantido no site de destino. O resultado é que os clientes da hierarquia de destino não poderão utilizar pacotes de imagens de arranque que estejam disponíveis em pontos de distribuição partilhados.  

-   Sequências de tarefas. Quando migra uma sequência de tarefas que contém uma referência a um pacote de instalação de cliente, esse referência é substituída por uma referência ao pacote de instalação de cliente da hierarquia de destino.  

    > [!NOTE]  
    >  Quando migra uma sequência de tarefas, o Configuration Manager poderá migrar objetos que não sejam necessários na hierarquia de destino. Tais objetos incluem imagens de arranque e pacotes de instalação de cliente do Configuration Manager 2007.  

-   Controladores e pacotes de controladores. Quando migra pacotes de controladores, a conta de computador do fornecedor de SMS da hierarquia de destino tem de ter controlo total para a origem do pacote.

##  <a name="Plan_Migrate_Compliance_settings"></a> Planear a migração da gestão de configuração pretendida  
É possível migrar itens de configuração e linhas de base de configuração.  

> [!NOTE]  
>  Itens de configuração não interpretados a partir de hierarquias de origem do Configuration Manager 2007 não são suportadas para migração. Não é possível migrar nem importar estes itens de configuração para a hierarquia de destino. Para mais informações sobre itens de configuração não interpretados, consulte itens de configuração não interpretados a [sobre itens de configuração de gestão de configuração pretendida](http://go.microsoft.com/fwlink/?LinkId=103846) tópico da biblioteca de documentação do Configuration Manager 2007.  

Pode importar pacotes de configuração do Configuration Manager 2007. O processo de importação converte automaticamente os pacotes de configuração para ser compatível com o System Center Configuration Manager.  

##  <a name="Plan_migrate_Boundaries"></a> Planear a migração de limites  
 É possível migrar limites entre hierarquias. Quando migra limites do Configuration Manager 2007, cada limite do site de origem migrada em simultâneo e é adicionada ao novo grupo de limites que é criado na hierarquia de destino. Quando migra limites de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager, cada limite selecionado é adicionado a um novo grupo de limites na hierarquia de destino.  

 Cada grupo de limites criado automaticamente está ativado para localização de conteúdo, mas não para atribuição de site. Deste modo, é evitada a sobreposição de limites para atribuição de sites entre as hierarquias de origem e de destino. Quando migra a partir de um site de origem do Configuration Manager 2007, isto ajuda a impedir que novos clientes do Configuration Manager 2007 que instale a partir de incorretamente à hierarquia de destino. Por predefinição, os clientes do System Center Configuration Manager não são automaticamente atribuídos a sites do Configuration Manager 2007.  

 Durante a migração, se partilhar um ponto de distribuição com a hierarquia de destino, todos os limites associados a essa distribuição migram automaticamente para a hierarquia de destino. Na hierarquia de destino, a migração cria um novo grupo de limites de só de leitura para cada ponto de distribuição partilhado. Se alterar os limites do ponto de distribuição da hierarquia de destino, o grupo de limites da hierarquia de destino será atualizado com estas alterações durante o próximo ciclo de recolha de dados.  

##  <a name="Plan_Migrate_reports"></a> Planear a migração de relatórios  
O Configuration Manager não suporta a migração de relatórios. Em alternativa, utilize o SQL Server Reporting Services Report Builder para exportar relatórios da hierarquia de origem e, em seguida, importá-los para a hierarquia de destino.  

> [!NOTE]  
>  Como existem alterações de esquema para os relatórios entre o Configuration Manager 2007 e o System Center Configuration Manager, teste todos os relatórios importados de uma hierarquia do Configuration Manager 2007 para garantir que funciona conforme esperado.  

Para obter mais informações sobre os relatórios, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="Plan_Migrate_Org_Folders"></a> Planear a migração organizacionais e pastas de procura  
 É possível migrar pastas organizacionais e pastas de procura de uma hierarquia de origem suportada para uma hierarquia de destino. Além disso, de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, pode migrar os critérios para uma pesquisa guardada para uma hierarquia de destino.  

 Por predefinição, o processo de migração mantém as estruturas de pastas de procura e de pastas administrativas de objetos e coleções. No entanto, no Assistente Criar tarefa de migração, no **definições** página, pode configurar uma tarefa de migração para não migrar a estrutura organizacional de objetos desmarcando a caixa para esta opção. As estruturas organizacionais das coleções são sempre mantidas.  

 Uma exceção a esta regra é uma pasta de procura com aplicações virtuais. Quando é migrado um pacote de App-V, o pacote de App-V é transformado numa aplicação no System Center Configuration Manager. Após a migração da pasta de pesquisa, encontram-se apenas os pacotes restantes e a pasta de pesquisa não é possível localizar um pacote de App-V devido a esta conversão para uma aplicação quando migra o pacote de App-V.  

 Quando migra uma procura guardada de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, migrar os critérios de pesquisa e não as informações sobre os resultados da pesquisa. Migração de uma procura guardada não se aplica a partir de um site de origem do Configuration Manager 2007.  

##  <a name="Plan_Migrate_AI"></a> Planear a migração de personalizações do Asset Intelligence  
 É possível migrar personalizações do Asset Intelligence de uma hierarquia de origem suportada para uma hierarquia de destino. Não foram efetuadas alterações significativas a estrutura de personalizações do Asset Intelligence entre o Configuration Manager 2007 e o System Center Configuration Manager.  

> [!NOTE]  
>  System Center Configuration Manager não suporta a migração de objetos do Asset Intelligence de um site do Configuration Manager 2007 que está a utilizar o Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="Plan_Migrate_SWM_Rules"></a> Planear a migração de personalizações de regras de medição de software  
 Não existem não existem alterações significativas na medição de software entre o Configuration Manager 2007 e o System Center Configuration Manager. É possível migrar as regras de medição de software de uma hierarquia de origem suportada para uma hierarquia de destino.  

 Por predefinição, as regras de medição de software que migra para uma hierarquia de destino não estão associadas a um site específico da hierarquia de destino e, em vez disso, aplicam-se a todos os clientes da hierarquia. Para aplicar uma regra de medição de software a clientes de um site específico, tem de editar a regra de medição após a respetiva migração.  
