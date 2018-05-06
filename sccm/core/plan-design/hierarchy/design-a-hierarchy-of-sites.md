---
title: 'Estruturar uma hierarquia do site '
titleSuffix: Configuration Manager
description: Compreenda as topologias disponíveis e as opções de gestão do System Center Configuration Manager, pelo que pode planear a hierarquia de sites.
ms.date: 8/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 602d9455dcdd69209ef8ba157916b35db976b89f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Estruturar uma hierarquia de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de instalar o primeiro site numa nova hierarquia do System Center Configuration Manager, é boa ideia compreender as topologias disponíveis para o Configuration Manager, os tipos de sites disponíveis e relações entre si e o âmbito de gestão que cada tipo de site fornece.
Em seguida, após a consideração dos opções de gestão de conteúdo que podem reduzir o número de sites que tem de instalar, que pode planear a topologia de forma eficiente serve as necessidades atuais e pode expandir mais tarde para gerir o crescimento futuro.  

Quando planear, tenha em limitações de atenção para adicionar sites adicionais para uma hierarquia ou site autónomo:
-   Pode instalar um novo site primário abaixo de um site de administração central, até o [suportado número de sites primários](/sccm/core/plan-design/configs/size-and-scale-numbers) para a hierarquia.
-   Pode [expandir um site primário autónomo para instalar um novo site de administração central](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), para que, em seguida, pode instalar sites primários adicionais.
-   Pode instalar novos sites secundários abaixo de um site primário, até [suportado limites para o site primário](/sccm/core/plan-design/configs/size-and-scale-numbers) e hierarquia geral.
-   Não é possível adicionar um site instalado anteriormente a uma hierarquia existente para intercalar os dois sites autónomos. É suportada apenas uma instalação de novos sites para uma hierarquia de sites existente.


> [!NOTE]
> Quando planear uma nova instalação do Configuration Manager, tenha em atenção o [notas de versão]( /sccm/core/servers/deploy/install/release-notes), que detalhe atuais problemas nas versões do Active Directory. As notas de versão aplicam-se a todos os ramos do Configuration Manager.  No entanto, quando utiliza o [ramo de pré-visualização técnica]( /sccm/core/get-started/technical-preview), irá encontrar problemas específicos apenas nessa sucursal na documentação de cada versão do Technical Preview.  

##  <a name="bkmk_topology"></a> Topologia de hierarquia  
 Hierarquia topologias intervalo de um único site primário autónomo a um grupo de sites primários e secundários ligados com um site de administração central no site de nível superior (camada superior) da hierarquia.   O controlador de chave do tipo e contagem de sites que utiliza numa hierarquia é, normalmente, o número e tipo de dispositivos que têm de suportar, da seguinte forma:   

 **Site primário autónomo:** Utilizar um site primário autónomo, quando um único site primário pode suportar a gestão de todos os seus dispositivos e utilizadores (consulte [dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers)). Esta topologia também é efetuada com êxito quando as diferentes localizações geográficas da sua empresa podem ser com êxito efetuadas por um único site primário.  Para ajudar a gerir o tráfego de rede, pode utilizar pontos de gestão preferenciais e uma infraestrutura de conteúdo cuidadosamente planeada (consulte [conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 As vantagens desta topologia incluem:  

-   Overhead administrativo simplificado.  

-   A atribuição de site do cliente simplificada e a deteção de serviços e recursos disponíveis.  

-   Eliminação de possível desfasamento introduzido pela replicação de base de dados entre sites.

-   Opção de expandir uma hierarquia primária autónoma para uma hierarquia maior com um site de administração central. o que lhe permite, depois, instalar novos sites primários para expandir a escala da implementação.  


**Site de administração central com um ou mais sites primários subordinados:** Utilize esta topologia quando precisa de mais do que um site primário para suportar a gestão de todos os seus dispositivos e utilizadores.  Que é necessário quando tiver de utilizar mais do que um único site primário. As vantagens desta topologia incluem:  


-   Suporta até 25 sites primários que permitem-lhe expandir a escala da sua hierarquia.  

-   Utilizará sempre o site de administração central (a menos que reinstale os sites). Esta é uma opção permanente. Não é possível anular a exposição de um site primário subordinado para torná-lo um site primário autónomo.

 As secções seguintes podem ajudá-lo a compreender quando deve utilizar um site específico ou a opção de gestão de conteúdos em vez de um site adicional.  

##  <a name="BKMK_ChooseCAS"></a> Determinar quando deve utilizar um site de administração central  
 Utilize um site de administração central para configurar as definições de toda a hierarquia e para monitorizar todos os sites e objetos na hierarquia. Este tipo de site não gere diretamente os clientes mas coordenar a replicação de dados entre sites, que inclui a configuração de sites e clientes em toda a hierarquia.  

**As seguintes informações podem ajudar a decidir quando instalar um site de administração central:**  

-   O site de administração central é o site de nível superior numa hierarquia.  

-   Quando configura uma hierarquia que tenha mais do que um site primário, tem de instalar um site de administração central. Se precisar de dois ou mais sites primários imediatamente, instale primeiro o site de administração central. Quando já tiver um site primário e para, em seguida, instalar um site de administração central, deve [expandir o site primário autónomo](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para instalar o site de administração central.

-   O site de administração central suporta apenas sites primários como sites subordinados.  

-   O site de administração central não pode ter clientes atribuídos ao mesmo.  

-   O site de administração central não suporta funções de sistema de sites que suportem diretamente clientes, tais como pontos de gestão e pontos de distribuição.  

-   Pode gerir todos os clientes na hierarquia e efetuar tarefas de gestão do site para qualquer site subordinado quando utiliza uma consola do Configuration Manager que está ligada ao site de administração central. Isto pode incluir a instalação de pontos de gestão ou de outras funções de sistema de sites em sites primários ou secundários subordinados.  

-   Quando utiliza um site de administração central, este é o único local onde pode ver os dados de todos os sites na hierarquia. Estes dados incluem informações como o inventário dados e mensagens de estado.  

-   Pode configurar operações de Deteção em toda a hierarquia do site de administração central através da atribuição de métodos de deteção a executar em sites individuais.  

-   Pode gerir a segurança em toda a hierarquia atribuindo diferentes funções de segurança, âmbitos de segurança e coleções a diferentes utilizadores administrativos. Estas configurações aplicam-se em cada site na hierarquia.  

-   Pode configurar a replicação de ficheiros e a replicação de base de dados para controlar a comunicação entre sites na hierarquia. Isto inclui agendar a replicação de base de dados para dados do site e gerir a largura de banda para a transferência de dados baseada em ficheiros entre sites.  

##  <a name="BKMK_ChoosePriimary"></a> Determinar quando deve utilizar um site primário  
 Utilize sites primários para gerir clientes. Pode instalar um site primário como site primário subordinado abaixo de um site de administração central ou como o primeiro site numa nova hierarquia. Um site primário que é instalado como o primeiro site de uma hierarquia cria um site primário autónomo. Os sites primários subordinados e sites primários autónomos suportam sites secundários como sites subordinados do site primário.  

 Considere a utilização de um site primário por qualquer um dos seguintes motivos:  

-   Para gerir dispositivos e utilizadores.  

-   Para aumentar o número de dispositivos que pode gerir com uma única hierarquia.  

-   Para fornecer um ponto adicional de conectividade para administração da implementação.  

-   Para satisfazer requisitos de gestão organizacional. Por exemplo, poderá instalar um site primário numa localização remota para gerir a transferência de conteúdo de implementação numa rede de largura de banda baixa. No entanto, com o System Center Configuration Manager, pode utilizar as opções para limitar a utilização de largura de banda de rede ao transferir dados para um ponto de distribuição. Se a capacidade de gestão de conteúdo pode substituir a necessidade de instalar sites adicionais.  


**As seguintes informações podem ajudar a decidir quando instalar um site primário:**  

-   Um site primário pode ser um site primário autónomo ou um site primário subordinado numa hierarquia maior. Quando um site primário é um membro de uma hierarquia com um site de administração central, os sites utilizam a replicação de base de dados para replicar dados entre os sites. A menos que seja necessário suportar mais clientes e dispositivos que um único site primário pode suportar, considere a instalação de um site primário autónomo.  Depois de um site primário autónomo estiver instalado, pode expandi-lo para comunicar para um novo site de administração central para aumentar verticalmente a sua implementação.  

-   Um site primário suporta apenas um site de administração central como site principal.  

-   Um site primário suporta apenas sites secundários como sites subordinados e também pode suportar vários sites subordinados secundários.  

-   Os sites primários são responsáveis por processar todos os dados de cliente dos respetivos clientes atribuídos.  

-   Sites primários utilizam a replicação de base de dados para comunicar diretamente com o respetivo site de administração central (que é configurado automaticamente quando instala um novo site).  

##  <a name="BKMK_ChooseSecondary"></a> Determinar quando deve utilizar um site secundário  
 Utilize sites secundários para gerir a transferência de dados de cliente e de conteúdo de implementação em redes com pouca largura de banda.  

 Gerir um site secundário a partir de um site de administração central ou site primário do principal do site secundário. Sites secundários têm de estar associados a um site primário e não é possível movê-los para outro site principal sem os desinstalar e reinstalar como site subordinado abaixo do novo site primário.

No entanto, pode encaminhar conteúdos entre dois sites secundários membros para ajudar a gerir a replicação baseada em ficheiros de conteúdo de implementação. Para transferir dados de cliente a um site primário, o site secundário utiliza a replicação baseada em ficheiros. Um site secundário também utiliza a replicação de base de dados para comunicar com o respetivo site primário principal.  

 Considere a instalação de um site secundário se qualquer uma das seguintes condições se aplicar:  

-   Não necessita de um ponto local de conectividade para um utilizador administrativo.  

-   Tem de gerir a transferência de conteúdo de implementação para sites num nível inferior da hierarquia.  

-   Tem de gerir informações de cliente que são enviadas para sites num nível superior da hierarquia.  

 Se não pretender instalar um site secundário e tiver clientes em localizações remotas, considere utilizar o Windows BranchCache ou instalar pontos de distribuição ativados para o controlo da largura de banda e agendamento. Pode utilizar estas opções de gestão de conteúdo com ou sem sites secundários e podem ajudar a reduzir o número de sites e servidores que tem de instalar. Para obter informações sobre as opções de gestão de conteúdos no Configuration Manager, consulte [determinar quando deve utilizar as opções de gestão de conteúdos](#BKMK_ChooseSecondaryorDP).  


**As seguintes informações podem ajudar a decidir quando instalar um site secundário:**  

-   Sites secundários instalam automaticamente do SQL Server Express durante a instalação de site se não estiver disponível uma instância local do SQL Server.  

-   Instalação do site secundário é iniciada a partir da consola do Configuration Manager, em vez de executar o programa de configuração diretamente num computador.  

-   Os sites secundários utilizam um subconjunto das informações na base de dados do site, que reduz a quantidade de dados que replica através da replicação de base de dados entre o site primário principal e o site secundário.  

-   Os sites secundários suportam o encaminhamento de conteúdo baseado em ficheiros para outros sites secundários que tenham um site primário principal comum.  

-   Instalações de site secundário implementam automaticamente um ponto de gestão e um ponto de distribuição que estão localizados no servidor do site secundário.  

##  <a name="BKMK_ChooseSecondaryorDP"></a> Determinar quando deve utilizar as opções de gestão de conteúdo  
 Se tiver clientes em localizações de rede remotas, considere utilizar uma ou mais opções de gestão de conteúdo em vez de um site primário ou secundário. Muitas vezes, pode remover a necessidade de instalar um site quando utiliza o Windows BranchCache, configura pontos de distribuição para controlo de largura de banda ou copia manualmente conteúdo para pontos de distribuição (conteúdo pré-configurado).  


**Considere implementar um ponto de distribuição em vez de instalar outro site, se qualquer uma das seguintes condições se aplicar:**  

-   A largura de banda de rede é suficiente para computadores cliente na localização remota comuniquem com um ponto de gestão para transferir a política de cliente e enviar o inventário, comunicar o estado e as informações de deteção.  

-   Serviço de transferência inteligente em segundo plano (BITS) não fornece controlo de largura de banda suficiente para os seus requisitos de rede.  

 Para obter mais informações sobre as opções de gestão de conteúdos no Configuration Manager, consulte [conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a> Para além da topologia da hierarquia  
 Para além de uma topologia de hierarquia inicial, considere os serviços ou funcionalidades que estarão disponíveis de diferentes sites numa hierarquia (funções do sistema de sites) e os como ao nível da hierarquia de configurações e as funções serão geridas na sua infraestrutura. As seguintes considerações comuns são abordadas em tópicos separados. Estes são importantes porque eles podem influenciar ou ser influenciados pela estrutura da hierarquia:  

-   Quando estiver a preparar para [gerir computadores e dispositivos com o System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), considere se os dispositivos que gere estão no local, na nuvem, ou incluem os dispositivos propriedade do utilizador (BYOD).  Além disso, considere a forma como irá gerir dispositivos que são suportados por várias opções de gestão, tais como computadores Windows 10 que podem ser geridos diretamente pelo Configuration Manager ou apesar de integração com o Microsoft Intune.  

-   Compreender a forma como a infraestrutura de rede disponível pode afetar o fluxo de dados entre localizações remotas (consulte [preparar o ambiente de rede para o System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Considere também onde estão localizados geograficamente os utilizadores e dispositivos que gere e se acedem à sua infraestrutura através do seu domínio empresarial ou da Internet.  

-   Plano para uma infraestrutura de conteúdo para distribuir de forma eficiente as informações que implementa (ficheiros e aplicações) nos dispositivos que gere (consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Determinar qual [funcionalidades e capacidades do System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) que pretende utilizar, a infraestrutura do Windows ou funções de sistema de sites que necessitam e, em que sites numa hierarquia vários sites pode implementá-las para a utilização mais eficaz dos seus recursos de rede e servidor.  

-   Considere a segurança dos dados e dispositivos, incluindo a utilização de um PKI. Consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Reveja os seguintes recursos para configurações especificas de sites:**  

-   [Planear o fornecedor de SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planear a base de dados do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Planear servidores de sistema de sites e funções de sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planear a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Gerir a largura de banda da rede](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) ao implementar conteúdos num site  


**Considere as configurações que abrangem sites e hierarquias:**  

-   [Opções de elevada disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options) para sites e hierarquias

-   [Expandir o esquema do Active Directory para o System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) e configurar sites para [publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)
