---
title: Estruturar uma hierarquia do site
titleSuffix: Configuration Manager
description: Compreenda as topologias disponíveis e as opções de gestão do Configuration Manager para planear a hierarquia do site.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eb7e4a6645514cedee382932adff76da14d0ba16
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385529"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Estruturar uma hierarquia de sites do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de instalar o primeiro site numa nova hierarquia do Configuration Manager, é uma boa ideia compreender:  

- As topologias disponíveis para o Configuration Manager  

- Os tipos de sites disponíveis e seus relacionamentos entre si  

- O escopo de gerenciamento que fornece de cada tipo de site  

- As opções de gestão de conteúdos que podem reduzir o número de sites que tem de instalar  

Em seguida, planeie uma topologia que atende suas necessidades de negócios atuais e pode expandir posteriormente para gerir o crescimento futuro com eficiência.  

Ao planejar, mantenha-se nas limitações de mente para adicionar sites adicionais para uma hierarquia ou um site autónomo:  

- Instalar um novo site primário abaixo de um site de administração central, até a [suportado o número de sites primários](/sccm/core/plan-design/configs/size-and-scale-numbers) para a hierarquia.  

- [Expandir um site primário de autónomo para instalar um novo site de administração central](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), em seguida, instalar sites primários adicionais.  

- Instalar novos sites secundários abaixo de um site primário, até a [limite suportado para o site primário](/sccm/core/plan-design/configs/size-and-scale-numbers) e toda a hierarquia.  

- Não é possível adicionar num site instalado anteriormente a uma hierarquia existente para intercalar dois sites autónomo. O Configuration Manager só suporta a instalação de novos sites para uma hierarquia existente de sites.  


> [!NOTE]  
> Quando planear uma nova instalação do Configuration Manager, tenha em consideração a [notas de versão](/sccm/core/servers/deploy/install/release-notes), que detalham atuais problemas nas versões do Active Directory. As notas de versão aplicam-se para todos os ramos do Configuration Manager. Quando utiliza a [pré-visualização técnica](/sccm/core/get-started/technical-preview), encontre problemas específicos para essa ramificação da documentação para cada versão do technical preview.  



##  <a name="bkmk_topology"></a> Topologia de hierarquia  

Topologias de hierarquia variam de:  

- Mais simples: Um site primário autónomo único  

- A maioria dos complexos: Um grupo de sites primários e secundários ligados com um site de administração central no site de nível superior da hierarquia  

A principal orientação do tipo e contagem de sites que utiliza numa hierarquia são, normalmente, o número e tipo de dispositivos, que tem de suportar.   

### <a name="standalone-primary-site"></a>Site primário autónomo

Utilize um site primário autónomo quando ele pode suportar a gestão de todos os dispositivos e utilizadores. Para obter mais informações, consulte [dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers). Esta topologia também tem êxito quando localizações geográficas da sua empresa podem ser atendidas por um único site primário. Para ajudar a gerir o tráfego de rede, utilize vários pontos de gestão em grupos de limites e uma infraestrutura de conteúdo cuidadosamente planeada. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

Essa topologia fornece as seguintes vantagens:  

- Overhead administrativo simplificado  

- Atribuição de site de cliente e deteção de recursos e serviços disponíveis simplificadas  

- Eliminação de atrasos possíveis introduzido pela replicação de base de dados entre sites  

- Opção para expandir um site primário autónomo para uma hierarquia maior com um site de administração central. Esta opção permite-lhe, em seguida, instalar novos sites primários para expandir a escala da sua implementação.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Site de administração central com um ou mais sites primários subordinados 

Utilize esta topologia quando precisar de mais de um site primário para suportar a gestão de todos os seus dispositivos e utilizadores. É obrigatório quando precisar de mais do que um único site primário a utilizar. 

Essa topologia fornece as seguintes vantagens:  

- Suporta até 25 sites primários que permitem-lhe expandir a escala da sua hierarquia.    

- Sempre usar o site de administração central, a menos que reinstale os sites. Esta opção é permanente. Não é possível desanexar o site primário subordinado para torná-lo um site primário autónomo.  



##  <a name="BKMK_ChooseCAS"></a> Determinar quando deve utilizar um site de administração central  

Utilize um site de administração central para configurar definições de toda a hierarquia e para monitorizar todos os sites e objetos da hierarquia. Este tipo de site não gere diretamente os clientes. Ele coordena a replicação de dados de site a site, que inclui a configuração de sites e clientes em toda a hierarquia.  

As informações seguintes podem ajudar a decidir quando instalar um site de administração central:  

- O site de administração central é o site de nível superior numa hierarquia.  

- Quando configura uma hierarquia que tenha mais do que um site primário, instale um site de administração central.  

     - Se precisar de duas ou mais sites primários imediatamente, instale primeiro o site de administração central.  

     - Quando já tiver um site primário e deve, em seguida, instalar um site de administração central [expandir o site primário autónomo](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para instalar o site de administração central.  

- O site de administração central suporta apenas sites primários como sites subordinados.  

- O site de administração central não pode ter clientes atribuídos ao mesmo.  

- O site de administração central não suporta funções de sistema de sites que suportem diretamente clientes, tais como pontos de gestão e pontos de distribuição.  

- Gerir todos os clientes na hierarquia e executar todas as tarefas de gestão do site a partir da consola do Configuration Manager que está ligada ao site de administração central. Essas tarefas incluem a instalação de pontos de gestão ou de outras funções de sistema de sites em sites primários ou secundários subordinados.  

- Quando utiliza um site de administração central, é o único local onde ver os dados de todos os sites na sua hierarquia. Estes dados incluem informações como mensagens de estado e dados de inventário.  

- Configure operações de Deteção em toda a hierarquia do site de administração central. Do site de administração central, atribua os métodos de deteção a executar em sites primários individuais.  

- Gerir a segurança em toda a hierarquia atribuindo diferentes funções de segurança, âmbitos de segurança e coleções a diferentes utilizadores administrativos. Estas configurações aplicam-se em cada site na hierarquia.  

- Configure a replicação para controlar a comunicação entre sites na hierarquia. Agende a replicação de base de dados para dados do site e gerir a largura de banda para a transferência de dados baseados em ficheiros entre sites.  



##  <a name="BKMK_ChoosePriimary"></a> Determinar quando deve utilizar um site primário  

Utilize sites primários para gerir clientes. Instale um site primário como site subordinado abaixo de um site de administração central ou como o primeiro site numa nova hierarquia. Um site primário que é o primeiro site de uma hierarquia cria um site primário autónomo. Os sites primários subordinados e os sites primários autónomos suportam sites secundários.  

Considere adicionar sites primários adicionais pelos seguintes motivos:  

- Para aumentar o número de dispositivos, gerir com uma única hierarquia.  

- Para satisfazer requisitos de gestão organizacional. Por exemplo, poderá instalar um site primário numa localização remota para gerir a transferência de conteúdo de implementação numa rede de baixa largura de banda.  

     - Considere em vez disso, usando as opções para limitar a largura de banda de rede ao transferir dados para um ponto de distribuição. Essa capacidade de gestão de conteúdos pode substituir a necessidade de instalar sites adicionais.  


As seguintes informações podem ajudar a decidir quando instalar um site primário:  

- Um site primário pode ser um site primário autónomo ou um site primário do subordinado na hierarquia de maiores dimensões. Quando um site primário é um membro de uma hierarquia com um site de administração central, os sites utilizam a replicação de base de dados para replicar dados entre os sites. A menos que precisa para suportar mais clientes e dispositivos do que um único site primário suporta, considere a instalação de um site primário autónomo. Depois de instalar um site primário autónomo, expandi-lo se for necessário no futuro para reportar a um novo site de administração central para aumentar verticalmente a sua implementação.  

- Um site primário suporta apenas um site de administração central como site principal.  

- Um site primário suporta apenas sites secundários como sites subordinados e oferece suporte a vários sites secundários.  

- Sites primários são responsáveis por processar todos os dados de cliente dos respetivos clientes atribuídos.  

- Sites primários utilizam a replicação de base de dados para comunicar diretamente com o respetivo site de administração central. Este comportamento é configurado automaticamente quando instala um novo site.  



##  <a name="BKMK_ChooseSecondary"></a> Determinar quando deve utilizar um site secundário  

Utilize sites secundários para gerir a transferência de dados de cliente e de conteúdo de implementação através de redes de largura de banda baixa.  

Gerir um site secundário a partir de um site de administração central ou site primário do principal do site secundário. Os sites secundários são associados a um site primário. Não é possível movê-los para outro site principal sem os desinstalar e, em seguida, reinstalá-los como um site subordinado abaixo do novo site primário.

No entanto, pode encaminhar o conteúdo entre dois sites secundários membros para ajudar a gerir a replicação baseada em ficheiros de conteúdo de implementação. Para transferir dados de cliente a um site primário, o site secundário utiliza a replicação de ficheiros. Um site secundário também utiliza a replicação de base de dados para comunicar com o respetivo site primário principal.  

Considere a instalação de um site secundário se qualquer uma das seguintes condições se aplicar:  

- Não necessita de um ponto local de conectividade para um utilizador administrativo.  

- Tem de gerir a transferência de conteúdo de implementação para sites num nível inferior na hierarquia.  

- Tem de gerir informações de cliente que são enviadas para sites num nível superior da hierarquia.  

Se não pretender instalar um site secundário e tiver clientes em localizações remotas, considere as seguintes opções:  

- Utilizar tecnologias de ponto-a-ponto, como o Windows BranchCache  

- Ative pontos de distribuição para controlo de largura de banda e agendamento   

Utilize estas opções de gerenciamento de conteúdo com ou sem sites secundários. Eles ajudam a reduzir o tamanho da sua infraestrutura do Configuration Manager. Para obter mais informações sobre as opções de gestão de conteúdos no Configuration Manager, consulte [determinar quando deve utilizar as opções de gestão de conteúdos](#BKMK_ChooseSecondaryorDP).  


As informações seguintes podem ajudar a decidir quando instalar um site secundário:  

- Se uma instância local do SQL Server não estiver disponível, servidores de sites secundários instalam automaticamente o SQL Server Express durante a instalação do site.  

- Instalação de site secundário é iniciada a partir da consola do Configuration Manager, em vez de executar o programa de configuração diretamente num computador.  

- Sites secundários utilizam um subconjunto das informações da base de dados do site. Este comportamento reduz a quantidade de dados SQL replicados entre o site primário principal e o site secundário.  

- Os sites secundários suportam o encaminhamento de conteúdo baseados em ficheiros para outros sites secundários que tenham um site primário do elemento principal comum.  

- Instalações de site secundário instalar automaticamente as gestão e distribuição de ponto de ponto de site funções do sistema no servidor do site secundário.  



##  <a name="BKMK_ChooseSecondaryorDP"></a> Determinar quando deve utilizar as opções de gestão de conteúdos  

Se tiver clientes em localizações de rede remotas, considere utilizar uma ou mais opções de gestão de conteúdo em vez de um site primário ou secundário. As seguintes opções, muitas vezes, remover a necessidade de instalar um site:  

- Otimização de entrega para o Windows 10  

- Cache de elemento de rede do Configuration Manager  

- BranchCache do Windows  

- Configurar pontos de distribuição para controlo de largura de banda  

- Copia manualmente conteúdo para pontos de distribuição (conteúdo pré-configurado)  


Se qualquer uma das seguintes condições se aplicarem, considere implementar um ponto de distribuição em vez de instalar outro site:  

- A largura de banda de rede é suficiente para computadores cliente na localização remota comuniquem com um ponto de gestão no site primário. Os clientes comunicam com um ponto de gestão para a política de cliente de download, inventário de envio, envio comunicar o estado e informações de deteção de envio.  

- Serviço de transferência inteligente em segundo plano (BITS) não fornece controlo de largura de banda suficiente para os seus requisitos de rede.  

Para obter mais informações sobre as opções de gestão de conteúdos no Configuration Manager, consulte [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  



##  <a name="bkmk_beyond"></a> Além da topologia de hierarquia  

Juntamente com a topologia de hierarquia inicial, considere também as seguintes perguntas:  

- As funções de sistema de sites fornecem serviços ou as funcionalidades de diferentes sites da hierarquia?  

- Como são gerenciando configurações de toda a hierarquia e capacidades em sua infra-estrutura?  


As seguintes considerações comuns são abordadas em artigos separados. Esta informação é importante para influenciar ou ser influenciadas pela estrutura da hierarquia:  

- Quando estiver a planear [gerir computadores e dispositivos](/sccm/core/clients/manage/manage-clients), considere se os dispositivos estão no local, na cloud, ou incluir os dispositivos pertencentes ao utilizador (BYOD). Além disso, considere como vai gerir dispositivos que suportam várias opções de gestão. Por exemplo, a gerir dispositivos Windows 10 com o Configuration Manager ou que a integração com o Microsoft Intune. Para obter mais informações, consulte [escolher uma solução de gestão de dispositivos](/sccm/core/plan-design/choose-a-device-management-solution).  

- Compreenda como a sua infraestrutura de rede disponível pode afetar o fluxo de dados entre localizações remotas. Para obter mais informações, consulte [preparar o ambiente de rede](/sccm/core/plan-design/network/configure-firewalls-ports-domains). Considere também a localização geográfica dos seus utilizadores e dispositivos, e eles aceder à sua infraestrutura através de sua rede no local ou na internet.  

- Planear uma infraestrutura de conteúdo distribuir de forma eficiente o conteúdo que implementar em dispositivos que gere. Este conteúdo pode ser aplicações, atualizações de software ou sistemas operativos. Para obter mais informações, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

- Determinar qual [funcionalidades e capacidades do Configuration Manager](/sccm/core/plan-design/changes/features-and-capabilities) que pretende utilizar. Diferentes funcionalidades necessitam de funções de sistema de site diferente ou de infraestrutura do Windows. Na hierarquia de vários sites, decida onde implementá-las para o uso mais eficiente dos seus recursos de rede e servidor.  

- Considere a segurança dos dados e dispositivos, incluindo a utilização de uma infraestrutura de chaves públicas (PKI). Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


Reveja os seguintes artigos para configurações especificas de sites:  

- [Planear o Fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)  

- [Planear a base de dados do site](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- [Planear servidores de sistema de sites e funções de sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)  

- [Plano de segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Gerir a largura de banda da rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) ao implementar conteúdos num site  


Considere as configurações que abrangem sites e hierarquias  

- [Opções de elevada disponibilidade](/sccm/protect/understand/high-availability-options) para sites e hierarquias

- [Expandir o esquema do Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema) e configurar sites para [publicar dados do site](/sccm/core/servers/deploy/configure/publish-site-data)  

- [Transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites)  

- [Noções básicas sobre a administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)  

- [Gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet)  

