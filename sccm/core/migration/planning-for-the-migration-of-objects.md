---
title: Migrar objetos | Microsoft Docs
description: "Saiba como planejar a migração de objetos entre hierarquias em um ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 17f3955aa7c63a13bab03b46002f7de0b0ec38fe
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>Planejar a migração de objetos do Configuration Manager para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Com o System Center Configuration Manager, você pode migrar vários objetos diferentes associados a diferentes recursos encontrados em um site de origem. Utilize as secções seguintes para o ajudar a planear a migração de objetos entre hierarquias.  

-   [Planejar a migração de atualizações de software](#Plan_migrate_Software_updates)  

-   [Planejar a migração de conteúdo](#Plan_Migrate_content)  

-   [Planejar a migração de coleções](#BKMK_MigrateCollections)  

-   [Planejar a migração de implantações de sistema operacional](#Plan_migrate_OSD)  

-   [Planejar a migração de gerenciamento da configuração desejada](#Plan_Migrate_Compliance_settings)  

-   [Planejar a migração de limites](#Plan_migrate_Boundaries)  

-   [Planejar a migração de relatórios](#Plan_Migrate_reports)  

-   [Planejar a migração organizacionais e de pastas de pesquisa](#Plan_Migrate_Org_Folders)  

-   [Planejar a migração de personalizações do Asset Intelligence](#Plan_Migrate_AI)  

-   [Planejar a migração de personalizações das regras de medição de software](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a>Planejar a migração de atualizações de software  
 Você pode migrar objetos de atualização de software, como implantações de atualização de software e pacotes de atualização de software.  

 Para migrar com êxito os objetos de atualização de software, você deve primeiro configurar sua hierarquia de destino com configurações que correspondem ao ambiente da hierarquia de origem. Isso requer as seguintes ações:  

-   Implantar um ponto de atualização de software ativo na hierarquia de destino  

-   Configurar o catálogo de produtos e idiomas para corresponder à configuração de sua hierarquia de origem  

-   Sincronizar o ponto de atualização de software na hierarquia de destino com o Windows Server Update Services (WSUS)  

Ao migrar atualizações de software, tenha em consideração:  

-   Migração de objetos de atualização de software pode falhar quando você não sincronizou informações em sua hierarquia de destino para corresponder à configuração de sua hierarquia de origem.  

    > [!WARNING]  
    >  Gerenciador de configuração não suporta o uso da ferramenta WSUSutil para sincronizar dados entre a hierarquia de origem e de destino.  

-   Não é possível migrar atualizações personalizadas que tenham sido publicadas utilizando o System Center Updates Publisher. Em vez disso, as atualizações personalizadas devem ser republicadas na hierarquia de destino.  

Quando você migra de uma hierarquia de origem do Configuration Manager 2007, o processo de migração modifica alguns objetos de atualização de software para o formato em uso pela hierarquia de destino. Use a tabela a seguir para ajudá-lo a planejar a migração de objetos de atualização de software do Configuration Manager 2007.  

|Objeto do Configuration Manager 2007|Nome do objeto após a migração|  
|-----------------------------------|---------------------------------|  
|Listas de atualização de software|As listas de atualização de software são convertidas em grupos de atualização de software.|  
|Implementações de atualizações de software|As implementações de atualização de software são convertidas em implementações e grupos de atualização.<br /><br /> Depois de migrar uma implantação de atualização de software do Configuration Manager 2007, você deve habilitá-la na hierarquia de destino antes de implantá-lo.|  
|Pacotes de atualização de software|Os pacotes de atualização de software mantêm a mesma designação.|  
|Modelos de atualização de software|Os modelos de atualização de software mantêm a sua designação.<br /><br /> O **duração** valor em modelos de implantação do Configuration Manager 2007 não migra.|  

Quando você migra objetos de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, os objetos de atualizações de software não são modificados.  

##  <a name="Plan_Migrate_content"></a>Planejar a migração de conteúdo  
 É possível migrar conteúdo de uma hierarquia de origem suportada para a hierarquia de destino. Para uma hierarquia de origem do Configuration Manager 2007, esse conteúdo inclui pacotes de distribuição de software, programas e aplicativos virtuais, como o Microsoft Application Virtualization (App-V). Para hierarquias de origem do System Center 2012 Configuration Manager e o System Center Configuration Manager, esse conteúdo inclui aplicativos e aplicativos virtuais do App-V. Ao migrar conteúdo entre hierarquias, os arquivos de origem compactados migram para a hierarquia de destino.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Ao migrar pacotes e programas, estes não são modificados pela migração. No entanto, antes de serem migradas, você deve configurar cada pacote para usar um caminho de convenção de nomenclatura Universal (UNC) para seu local de arquivo de origem. Como parte da configuração para migrar pacotes e programas, terá de atribuir um site na hierarquia de destino para gerir este conteúdo. O conteúdo não é migrado de um site atribuído, mas após a migração, o site atribuído acessa o local do arquivo de origem original usando o mapeamento UNC.  

 Depois de migrar um pacote e programa para a hierarquia de destino e enquanto a migração da hierarquia de origem permanece ativa, você pode tornar o conteúdo disponível para clientes nessa hierarquia usando um ponto de distribuição compartilhado. Para utilizar um ponto de distribuição partilhado, o conteúdo terá de permanecer acessível no ponto de distribuição do site de origem. Para obter mais informações sobre pontos de distribuição compartilhados, consulte [compartilhar pontos de distribuição entre hierarquias de origem e destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) na [planejar uma estratégia de migração de implantação de conteúdo no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Para o conteúdo que foi migrado, se as alterações de versão do conteúdo na hierarquia de origem ou a hierarquia de destino, os clientes não podem acessar o conteúdo do ponto de distribuição compartilhado na hierarquia de destino. Nesse cenário, você deve migrar o conteúdo para restaurar uma versão consistente do pacote entre a hierarquia de origem e de destino novamente. Essas informações será sincronizado durante o ciclo de coleta de dados.  

> [!TIP]  
>  Por cada pacote que migrar, atualize o pacote na hierarquia de destino. Esta ação pode evitar problemas na implementação do pacote nos pontos de distribuição na hierarquia de destino. No entanto, quando você atualiza um pacote no ponto de distribuição na hierarquia de destino, os clientes nessa hierarquia não ser capaz de obter esse pacote de um ponto de distribuição compartilhado. Para atualizar um pacote na hierarquia de destino, no console do Configuration Manager, vá para a biblioteca de Software, clique com botão direito no pacote e, em seguida, selecione **atualizar pontos de distribuição**. Faça essa ação para cada pacote que você migrar.  

> [!TIP]  
>  Você pode usar o Microsoft System Center Configuration Manager Package Conversion Manager para converter pacotes e programas em aplicativos do System Center Configuration Manager. Transfira o Package Conversion Manager a partir do site do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=212950). Para obter mais informações, veja [Gestor de Conversão de Pacotes do Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### <a name="virtual-applications"></a>Aplicações virtuais  
Quando você migrar pacotes do App-V de um site do Configuration Manager 2007 com suporte, o processo de migração converte-os em aplicativos na hierarquia de destino. Além disso, os seguintes tipos de implantação com base nos anúncios existentes para o pacote do App-V, são criados na hierarquia de destino:  

-   Se não existirem anúncios, é criado um tipo de implementação que utilize as predefinições do tipo de implementação.  

-   Se existir um anúncio, é criado um tipo de implantação usa as mesmas configurações como o anúncio do Configuration Manager 2007.  

-   Se vários anúncios, um tipo de implantação é criado para cada anúncio do Configuration Manager 2007, usando as configurações para esse anúncio.  

> [!IMPORTANT]  
>  Se você migrar um pacote migrado anteriormente do Configuration Manager 2007 App-V, a migração falhará porque os pacotes de aplicativos virtuais não oferecem suporte para o comportamento de substituição da migração. Neste cenário, terá de eliminar o pacote de aplicação virtual migrado da hierarquia de destino e, em seguida, criar uma nova tarefa de migração para migrar a aplicação virtual.  

> [!NOTE]  
>  Depois de migrar um pacote do App-V, você pode usar o Assistente para atualização de conteúdo para alterar o caminho de origem para tipos de implantação do App-V. Para obter mais informações sobre como atualizar o conteúdo de um tipo de implantação, consulte como gerenciar tipos de implantação de [tarefas de gerenciamento para aplicativos do System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

Quando você migra de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, você pode migrar objetos para o ambiente virtual App-V Além de aplicativos e tipos de implantação do App-V. Para obter mais informações sobre ambientes do App-V, consulte [aplicativos virtuais do App-V implantando com o System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Anúncios  
É possível migrar anúncios de um site de origem do Configuration Manager 2007 com suporte para a hierarquia de destino usando a migração baseada em coleção. Se atualizar um cliente, este manterá o histórico dos anúncios anteriormente executados, para impedir que o cliente volte a executar os anúncios migrados.  

> [!NOTE]  
>  Não é possível migrar anúncios para pacotes virtuais. Esta é uma exceção à migração de anúncios.  

### <a name="applications"></a>Aplicações  
 Você pode migrar aplicativos de uma hierarquia de origem com suporte do System Center 2012 Configuration Manager ou System Center Configuration Manager para uma hierarquia de destino. Se reatribuir um cliente da hierarquia de origem para a hierarquia de destino, o cliente manterá o histórico das aplicações anteriormente instaladas, para impedir que o cliente volte a executar as aplicações migradas.  

##  <a name="BKMK_MigrateCollections"></a>Planejar a migração de coleções  
 Você pode migrar os critérios para coleções de uma hierarquia de origem com suporte do System Center 2012 Configuration Manager ou System Center Configuration Manager. Para isso, use um trabalho de migração baseada em objeto. Ao migrar uma coleção migrará as respetivas regras, e não as informações sobre os membros da coleção nem as informações ou objetos relacionados com os membros da coleção.  

 Não há suporte para migração do objeto da coleção quando você migra de uma hierarquia de origem do Configuration Manager 2007.  

##  <a name="Plan_migrate_OSD"></a>Planejar a migração de implantações de sistema operacional  
É possível migrar os seguintes objetos de implementação de sistemas operativos a partir de uma hierarquia de origem suportada:  

-   Imagens e pacotes de sistemas operativos. O caminho de origem das imagens de inicialização é atualizado para o local da imagem padrão para o Kit de instalação (Windows AIK) no site de destino. Eis os requisitos e limitações da migração de imagens e pacotes de sistemas operativos:  

    -   Para migrar os arquivos de imagem com êxito, a conta de computador do servidor de provedor de SMS para o site de nível superior da hierarquia de destino deve ter **leitura** e **gravar** permissão para os arquivos de origem da imagem do local do Windows AIK do local de origem.  

    -   Quando você migra um pacote de instalação do sistema operacional, certifique-se de que a configuração do pacote nos pontos do site de origem para a pasta que contém o arquivo WIM e não o próprio arquivo WIM. Se o pacote de instalação apontar para o ficheiro WIM, a migração do pacote de instalação falhará.  

    -   Quando você migra um pacote de imagem de inicialização de um site de origem do Configuration Manager 2007, a ID do pacote do pacote não é mantida no site de destino. O resultado é que os clientes da hierarquia de destino não poderão utilizar pacotes de imagens de arranque que estejam disponíveis em pontos de distribuição partilhados.  

-   Sequências de tarefas. Quando você migra uma sequência de tarefas que tem uma referência a um pacote de instalação do cliente, essa referência é substituída por uma referência ao pacote de instalação de cliente da hierarquia de destino.  

    > [!NOTE]  
    >  Quando você migra uma sequência de tarefas, o Configuration Manager pode migrar objetos que não são necessários na hierarquia de destino. Esses objetos incluem imagens de inicialização e pacotes de instalação de cliente do Configuration Manager 2007.  

-   Controladores e pacotes de controladores. Quando você migra pacotes de driver, a conta de computador do provedor de SMS na hierarquia de destino deve ter controle total para a origem do pacote.

##  <a name="Plan_Migrate_Compliance_settings"></a>Planejar a migração de gerenciamento da configuração desejada  
É possível migrar itens de configuração e linhas de base de configuração.  

> [!NOTE]  
>  Não há suporte para itens de configuração não interpretados das hierarquias de origem do Configuration Manager 2007 para a migração. Não é possível migrar nem importar estes itens de configuração para a hierarquia de destino. Para obter mais informações sobre itens de configuração não interpretados, consulte itens de configuração não interpretada a [sobre itens de configuração no gerenciamento de configurações desejadas](http://go.microsoft.com/fwlink/?LinkId=103846) tópico na biblioteca de documentação do Configuration Manager 2007.  

Você pode importar pacotes de configuração do Configuration Manager 2007. O processo de importação converte automaticamente os pacotes de configuração para ser compatível com o System Center Configuration Manager.  

##  <a name="Plan_migrate_Boundaries"></a>Planejar a migração de limites  
 É possível migrar limites entre hierarquias. Quando você migra limites do Configuration Manager 2007, cada limite do site de origem migra ao mesmo tempo e é adicionado ao novo grupo de limites que é criado na hierarquia de destino. Quando você migra limites de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager, cada limite selecionado é adicionado ao novo grupo de limites na hierarquia de destino.  

 Cada grupo de limites criado automaticamente está ativado para localização de conteúdo, mas não para atribuição de site. Deste modo, é evitada a sobreposição de limites para atribuição de sites entre as hierarquias de origem e de destino. Quando você migra de um site de origem do Configuration Manager 2007, isso ajuda a impedir que novos clientes do Configuration Manager 2007 instalados sejam incorretamente atribuídos à hierarquia de destino. Por padrão, os clientes do System Center Configuration Manager não são atribuídos automaticamente aos sites do Configuration Manager 2007.  

 Durante a migração, se partilhar um ponto de distribuição com a hierarquia de destino, todos os limites associados a essa distribuição migram automaticamente para a hierarquia de destino. Na hierarquia de destino, a migração cria um novo grupo de limites somente leitura para cada ponto de distribuição compartilhado. Se alterar os limites do ponto de distribuição da hierarquia de destino, o grupo de limites da hierarquia de destino será atualizado com estas alterações durante o próximo ciclo de recolha de dados.  

##  <a name="Plan_Migrate_reports"></a>Planejar a migração de relatórios  
Gerenciador de configuração não dá suporte à migração de relatórios. Em alternativa, utilize o SQL Server Reporting Services Report Builder para exportar relatórios da hierarquia de origem e, em seguida, importá-los para a hierarquia de destino.  

> [!NOTE]  
>  Porque há alterações de esquema para relatórios entre o Configuration Manager 2007 e System Center Configuration Manager, teste cada relatório que você importa de uma hierarquia do Configuration Manager 2007 para garantir que ele funcione conforme o esperado.  

Para obter mais informações sobre relatórios, consulte [Reporting no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="Plan_Migrate_Org_Folders"></a>Planejar a migração organizacionais e de pastas de pesquisa  
 É possível migrar pastas organizacionais e pastas de procura de uma hierarquia de origem suportada para uma hierarquia de destino. Além disso, de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, você pode migrar os critérios para uma pesquisa salva para uma hierarquia de destino.  

 Por predefinição, o processo de migração mantém as estruturas de pastas de procura e de pastas administrativas de objetos e coleções. No entanto, no assistente criar trabalho de migração, sobre o **configurações** página, você pode configurar um trabalho de migração para não migre a estrutura organizacional de objetos ao desmarcar a caixa para essa opção. As estruturas organizacionais das coleções são sempre mantidas.  

 Uma exceção a esta regra é uma pasta de procura com aplicações virtuais. Quando um pacote do App-V é migrado, o pacote do App-V é transformado em um aplicativo no System Center Configuration Manager. Após a migração da pasta de pesquisa, apenas os pacotes restantes são encontrados, e a pasta de pesquisa não é possível localizar um pacote do App-V por causa dessa conversão para um aplicativo quando migra o pacote do App-V.  

 Quando você migra uma pesquisa salva de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, você migra os critérios da pesquisa, e não as informações sobre os resultados da pesquisa. Migração de uma pesquisa salva não é aplicável por meio de um site de origem do Configuration Manager 2007.  

##  <a name="Plan_Migrate_AI"></a>Planejar a migração de personalizações do Asset Intelligence  
 É possível migrar personalizações do Asset Intelligence de uma hierarquia de origem suportada para uma hierarquia de destino. Não há nenhuma alteração significativa na estrutura das personalizações do Asset Intelligence entre o Configuration Manager 2007 e System Center Configuration Manager.  

> [!NOTE]  
>  System Center Configuration Manager não dá suporte à migração de objetos de inteligência de ativos de um site do Configuration Manager 2007 que está usando o Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="Plan_Migrate_SWM_Rules"></a>Planejar a migração de personalizações das regras de medição de software  
 Não há nenhum alterações significativas na medição de software entre o Configuration Manager 2007 e System Center Configuration Manager. É possível migrar as regras de medição de software de uma hierarquia de origem suportada para uma hierarquia de destino.  

 Por predefinição, as regras de medição de software que migra para uma hierarquia de destino não estão associadas a um site específico da hierarquia de destino e, em vez disso, aplicam-se a todos os clientes da hierarquia. Para aplicar uma regra de medição de software a clientes de um site específico, tem de editar a regra de medição após a respetiva migração.  

