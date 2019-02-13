---
title: Conceitos básicos de administração baseada em funções
titleSuffix: Configuration Manager
description: Utilize a administração baseada em funções para controlar o acesso administrativo ao Configuration Manager e os objetos que gere.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d5da8213f3e0b0f53961b74e11d6f27662ee340
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119998"
---
# <a name="fundamentals-of-role-based-administration-for-system-center-configuration-manager"></a>Noções básicas da administração baseada em funções para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, utilize a administração baseada em função para proteger o acesso necessário para administrar o Configuration Manager. Também protege o acesso aos objetos que gere, como coleções, implementações e sites. Depois de compreender os conceitos apresentados neste tópico, pode [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Centralmente, o modelo de administração baseada em funções define e gere as definições de acesso de segurança ao nível da hierarquia para todos os sites e definições do site utilizando o seguinte:  

- *Funções de segurança* atribuídas a utilizadores administrativos para fornecer a esses utilizadores (ou grupos de utilizadores) permissões para diferentes objetos do Configuration Manager. Por exemplo, a permissão para criar ou alterar as definições de cliente.  

- *Âmbitos de segurança* são utilizados para agrupam instâncias específicas de objetos que um utilizador administrativo é da responsabilidade de gerir, como uma aplicação que instala o Microsoft Office 2010.  

- *Coleções* são utilizados para especificar grupos de recursos de utilizadores e dispositivos que o utilizador administrativo pode gerir.  

  Com a combinação de funções de segurança, âmbitos de segurança e coleções, segregar as atribuições administrativas que satisfazem os requisitos da sua organização. Utilizados em conjunto, elas definem o âmbito administrativo de um usuário, o que é o que esse utilizador pode ver e gerir na sua implementação do Configuration Manager.  

## <a name="benefits-of-role-based-administration"></a>Benefícios da administração baseada em funções  

-   Sites não são utilizados como limites administrativos.  

-   Criar utilizadores administrativos para uma hierarquia e só tem de atribuir-lhes segurança uma vez.  

-   Todas as atribuições de segurança são replicadas e estão disponíveis em toda a hierarquia.  

-   Existem funções de segurança incorporadas, que são utilizadas para atribuir as tarefas administrativas comuns. Crie suas próprias funções de segurança personalizadas para suportar necessidades empresariais específicas.  

-   Os utilizadores administrativos ver apenas os objetos que têm permissões para gerir.  

-   É possível auditar as ações de segurança administrativa.  

Quando estruturar e implementar segurança administrativa para o Configuration Manager, utilize o seguinte para criar uma *âmbito administrativo* para um utilizador administrativo:  

-   [Funções de segurança](#bkmk_Planroles)  

-   [Coleções](#bkmk_planCol)  

-   [Âmbitos de segurança](#bkmk_PlanScope)  


 O âmbito administrativo controla os objetos que um vistas de utilizador administrativo na consola do Configuration Manager e ele controla as permissões que um utilizador tem nesses objetos. As configurações da administração baseada em funções são replicadas para cada site da hierarquia como dados globais e são depois aplicadas a todas as ligações administrativas.  

> [!IMPORTANT]  
>  Os atrasos na replicação entre sites podem impedir que um site receba alterações para a administração baseada em funções. Para obter informações sobre como monitorizar a replicação de base de dados entre sites, consulte a [transferências de dados entre sites no System Center Configuration Manager](../../core/servers/manage/data-transfers-between-sites.md) tópico.  

##  <a name="bkmk_Planroles"></a> Funções de segurança  
 Utilize funções de segurança para conceder permissões de segurança a utilizadores administrativos. As funções de segurança são grupos de permissões de segurança que são atribuídas aos utilizadores administrativos para que estes possam desempenhar as suas tarefas administrativas. Estas permissões de segurança definem as ações administrativas que um utilizador administrativo pode executar e as permissões que são concedidas para tipos de objetos específicos. Como melhor prática de segurança, atribua as funções de segurança que proporcionam menos permissões.  

 O Configuration Manager possui várias funções de segurança incorporadas para suportar agrupamentos comuns de tarefas administrativas e pode criar suas próprias funções de segurança personalizadas para suportar necessidades empresariais específicas. Exemplos das funções de segurança incorporadas:  

-   *Administrador total* concede todas as permissões no Configuration Manager.  

-   *Gestor do Asset Intelligence* concede permissões para gerir o ponto de sincronização do Asset Intelligence, do Asset Intelligence reporting classes, inventário de software, inventário de hardware e regras de medição.  

-   *Gestor de atualizações de software* concede permissões para definir e implementar atualizações de software. Os utilizadores administrativos que estiverem associados esta função podem criar coleções, grupos de atualização de software, implementações e modelos.  

> [!TIP]  
>  Pode ver a lista de funções de segurança incorporadas e funções de segurança personalizadas criadas, incluindo as suas descrições, na consola do Configuration Manager. Para ver as funções, o **administração** área de trabalho, expanda **Security**e, em seguida, selecione **funções de segurança**.  

 Cada função de segurança tem permissões específicas para tipos de objetos diferentes. Por exemplo, o *autor da aplicação* função de segurança tem as seguintes permissões para aplicações: Aprovar, criar, eliminar, modificar, modificar pasta, mover objeto, ler, execute o relatório e definir âmbito de segurança.

 Não é possível alterar as permissões das funções de segurança incorporadas, mas é possível copiar a função, alterá-la e guardar as alterações como uma nova função de segurança personalizada. Também é possível importar funções de segurança exportadas de outra hierarquia, por exemplo, de uma rede de teste. Reveja as funções de segurança e as respetivas permissões para determinar se irá utilizar as funções de segurança incorporadas ou, se tiver de criar as suas próprias funções de segurança personalizada.  

 ### <a name="to-help-you-plan-for-security-roles"></a>Para ajudar a planear funções de segurança  

1.  Identifique as tarefas que os utilizadores administrativos executam no Configuration Manager. Estas tarefas podem estar relacionadas com um ou mais grupos de tarefas de gestão, tais como a implementação de aplicações e pacotes, a implementação de sistemas operativos e definições de compatibilidade, a configuração de sites e da segurança, auditorias, o controlo remoto de computadores e a recolha de dados de inventário.  

2.  Mapeie estas tarefas administrativas para uma ou mais das funções de segurança incorporadas.  

3.  Se alguns dos utilizadores administrativos executam as tarefas de várias funções de segurança, atribua as várias funções de segurança a estes utilizadores administradores em vez de criar uma nova função de segurança que combine todas as tarefas.  

4.  Se as tarefas identificadas não mapearem para as funções de segurança incorporadas, crie e teste novas funções de segurança.  

Para obter informações sobre como criar e configurar funções de segurança para a administração baseada em funções, consulte  [Create custom security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) e [Configure security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) no tópico [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="bkmk_planCol"></a> Coleções  
 As coleções especificam os recursos de utilizador e de computador que um utilizador administrativo pode ver ou gerir. Por exemplo, para poderem implementar aplicações ou efetuar o controlo remoto, os utilizadores administrativos devem ter atribuída uma função de segurança que conceda acesso a uma coleção que contenha esses recursos. É possível selecionar coleções de utilizadores ou dispositivos.  

 Para obter mais informações sobre as coleções, consulte [introdução às coleções no System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md).  

 Antes de configurar a administração baseada em funções, verifique se criou novas coleções por qualquer um dos seguintes motivos:  

-   Organização funcional. Por exemplo, coleções separadas de servidores e de estações de trabalho.  

-   Alinhamento geográfico. Por exemplo, coleções separadas para a América do Norte e para a Europa.  

-   Requisitos de segurança e processos empresariais. Por exemplo, coleções separadas para computadores de produção e de teste.  

-   Alinhamento organizacional. Por exemplo, coleções separadas para cada unidade de negócio.  

Para obter informações sobre como configurar coleções para a administração baseada em funções, consulte  [Configure collections to manage security](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) no tópico [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="bkmk_PlanScope"></a> Âmbitos de segurança  
 Utilize âmbitos de segurança para fornecer aos utilizadores administrativos acesso a objetos com capacidade de segurança. Um âmbito de segurança é um conjunto nomeado de objetos com capacidade de segurança que são atribuídos a utilizadores administrativos como um grupo. Todos os objetos com capacidade de segurança têm de ser atribuídos a um ou mais âmbitos de segurança. O Configuration Manager possui dois âmbitos de segurança incorporados:  

-   O *todos os* âmbito de segurança incorporado concede acesso a todos os âmbitos. Não é possível atribuir objetos a este âmbito de segurança.  

-   O *predefinição* âmbito de segurança incorporado é utilizado para todos os objetos, por predefinição. Ao instalar o Configuration Manager, todos os objetos são atribuídos a este âmbito de segurança.  

Se pretender restringir os objetos que os utilizadores administrativos podem ver e gerir, tem de criar e utilizar os seus próprio âmbitos de segurança personalizados. Os âmbitos de segurança não suportam uma estrutura hierárquica e não podem ser aninhados. Os âmbitos de segurança podem conter um ou mais tipos de objetos, nomeadamente:  

-   Subscrições de alertas  

-   Aplicações  

-   Imagens de arranque  

-   Grupos de limites  

-   Itens de configuração  

-   Definições de cliente personalizadas  

-   Pontos de distribuição e grupos de pontos de distribuição  

-   Pacotes de controladores  

-   Condições globais  

-   Tarefas de migração  

-   Imagens de sistema operativo  

-   Pacotes de instalação de sistema operativo  

-   Pacotes  

-   Consultas  

-   Sites  

-   Regras de medição de software  

-   Grupos de atualizações de software  

-   Pacotes de atualizações de software  

-   Pacotes de sequências de tarefas  

-   Pacotes e itens de definição de dispositivos Windows CE  

Existem também alguns objetos que não podem ser incluídos em âmbitos de segurança porque apenas são protegidos por funções de segurança. Acesso administrativo a esses objetos não pode estar limitado a um subconjunto dos objetos disponíveis. Por exemplo, pode ter um utilizador administrativo que cria grupos de limites que são utilizados para um site específico. Uma vez que o objeto de limite não suporta âmbitos de segurança, não é possível atribuir a este utilizador um âmbito de segurança que forneça acesso apenas aos limites que possam estar associados a esse site. Dado que não é possível associar um objeto de limite a um âmbito de segurança, quando é atribuída a um utilizador uma função de segurança que inclui acesso a objetos de limites, esse utilizador pode aceder a todos os limites na hierarquia.  

Exemplos de objetos que não são limitados por âmbitos de segurança:  

-   Florestas do Active Directory  

-   Utilizadores administrativos  

-   Alertas  

-   Políticas Antimalware  

-   Limites  

-   Associações de computador  

-   Predefinições de cliente  

-   Modelos de implementação  

-   Controladores de dispositivo  

-   Conector do Exchange Server  

-   Mapeamentos site a site de migração  

-   Perfis de inscrição de dispositivos móveis  

-   Funções de segurança  

-   Âmbitos de segurança  

-   Endereços de sites  

-   Funções do sistema de sites  

-   Títulos de software  

-   Atualizações de software  

-   Mensagens de estado  

-   Afinidades de dispositivo do utilizador  

Crie âmbitos de segurança quando tiver de limitar o acesso a instâncias de objetos separadas. Por exemplo:  

-   Tem um grupo de utilizadores administrativos que deve poder ver aplicações de produção e não aplicações de teste. Crie um âmbito de segurança para aplicações de produção e outro para as aplicações de teste.  

-   Utilizadores administrativos diferentes necessitam de acesso diferente a algumas instâncias de um tipo de objeto. Por exemplo, um grupo de utilizadores administrativos necessita de permissão de leitura para grupos de atualização de software específicos e outro grupo de utilizadores administrativos necessita de permissões de modificar e eliminar para outros grupos de atualização de software. Crie âmbitos de segurança diferentes para estes grupos de atualizações de software.  

Para obter informações sobre como configurar âmbitos de segurança para a administração baseada em funções, consulte [Configure security scopes for an object](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) no tópico [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  
