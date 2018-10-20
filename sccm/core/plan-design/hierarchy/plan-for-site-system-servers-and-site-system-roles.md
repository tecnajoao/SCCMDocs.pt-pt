---
title: Planear funções de sistema de sites
titleSuffix: Configuration Manager"
description: Considere os servidores do sistema de sites e funções de sistema de sites como planear a hierarquia do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f2c3052337b5c985798c15950a541086587176d1
ms.sourcegitcommit: 19fc4f27667d51502fc9d7d02d164f2837d65dae
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461312"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planear servidores de sistema de sites e funções de sistema de sites no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Cada site do Configuration Manager que instalar inclui um servidor de site que um **servidor do sistema de site**. O site também pode incluir servidores do sistema de sites adicionais em computadores que são remotos em relação ao servidor do site. Os servidores do sistema de sites (o servidor do site ou um servidor do sistema de sites remoto) suportam **funções do sistema de sites**.  


##  <a name="bkmk_siteservers"></a> Servidores do sistema de sites  

Quando instala uma função de sistema de sites num computador, esse computador torna-se um servidor de sistema de sites. Em cada site, pode instalar um ou mais servidores de sistema de sites adicionais. Não é preciso instalar servidores de sistema de sites adicionais e pode optar por executar todas as funções de sistema de sites diretamente no computador do servidor de site. Cada servidor de sistema de sites suporta uma ou mais funções de sistema de sites. Servidores adicionais podem ajudar a expandir as capacidades e a capacidade de um site ao partilhar a carga de processamento que funções de sistema de sites colocam num servidor.  

Ao considerar a adição de um servidor de sistema de sites, certifique-se de que o servidor cumpre os pré-requisitos para a utilização pretendida. Também adicioná-lo numa localização de rede com largura de banda suficiente para comunicar com os pontos finais esperados. Estes pontos finais incluem o servidor do site, recursos do domínio, uma localização com base na cloud, os servidores de sistema de sites e clientes.  



##  <a name="bkmk_planroles"></a> Site system roles  

Instale funções do sistema de sites num servidor para fornecer capacidades adicionais para o site. Alguns exemplos:  

-   Pontos de gestão adicionais para que o site consegue suportar mais dispositivos, até a capacidade de suporte do site.  

-   Pontos de distribuição adicionais para expandir a infraestrutura de conteúdo, melhorando o desempenho das distribuições de conteúdo para os dispositivos.  

-   Uma ou mais funções de sistema de sites específicos de funcionalidades. Por exemplo, um ponto de atualização de software permite-lhe gerir atualizações de software para dispositivos geridos. Um ponto do reporting services permite-lhe executar relatórios para monitorizar, compreender e compartilhar informações sobre o seu ambiente.  


Diferentes sites do Configuration Manager podem suportar diferentes conjuntos de funções do sistema de sites. O conjunto de suporte de funções do sistema de sites depende do tipo de site. (Os tipos de sites incluem um site de administração central, sites primários ou sites secundários.) A topologia da hierarquia pode limitar a colocação de algumas funções em determinados tipos de site. Por exemplo, o ponto de ligação de serviço só é suportado no site de nível superior da hierarquia. O site de nível superior poderá ser um site de administração central ou um site primário autónomo. Esta função não é suportada num site primário subordinado ou em sites secundários.  

Após a instalação de um site, pode mover a localização de algumas funções de sistema de sites da localização predefinida no servidor do site para outro servidor. Por exemplo, o ponto de gestão ou a distribuição de ponto de instalação de funções por predefinição num servidor do site primário ou secundário. Também instale instâncias adicionais de algumas funções de sistema de sites para expandir as capacidades do seu site e para cumprir os requisitos comerciais. Algumas funções são necessárias, enquanto outras são opcionais.  

#### <a name="configuration-manager-site-server"></a>Servidor de site do Configuration Manager
Esta função identifica o servidor onde a configuração do Configuration Manager é executada para instalar um site ou o servidor no qual instala um site secundário. Não é possível mover ou até que a desinstalação do site de desinstalar esta função.  

#### <a name="configuration-manager-site-system"></a>Sistema de sites do Configuration Manager
Esta função é atribuída a qualquer computador no qual instala um site ou instalar uma função de sistema de sites. Não é possível mover ou de desinstalar esta função até remover a última função do sistema de sites do computador.  

#### <a name="configuration-manager-component-site-system-role"></a>Função de sistema de sites de componente do Configuration Manager
Esta função identifica um sistema de sites que executa uma instância dos **SMS Executive** serviço. É necessário para suportar outras funções, como pontos de gestão. Não é possível mover ou de desinstalar esta função até remover a última função do sistema de sites aplicáveis do computador.  

#### <a name="configuration-manager-site-database-server"></a>Servidor de base de dados do site do Configuration Manager
O site atribui esta função para servidores de sistema de sites que contenham uma instância da base de dados do site. Só mova esta função para um novo servidor ao executar o programa de configuração para modificar o site para utilizar uma instância diferente do SQL Server para alojar a base de dados do site.  

#### <a name="sms-provider"></a>Fornecedor de SMS
O site atribui esta função para cada computador que aloja uma instância do fornecedor de SMS. O fornecedor é a interface entre uma consola do Configuration Manager e a base de dados do site. Por predefinição, esta função instala automaticamente no servidor do site de um site de administração central e sites primários. Instale instâncias adicionais em cada site para conceder acesso a utilizadores administrativos adicionais ou para redundância.  

Para instalar fornecedores adicionais, executar a configuração do Configuration Manager para [gerir o fornecedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider). Em seguida, instale fornecedores adicionais em computadores adicionais. Instale apenas uma instância do fornecedor de SMS num computador. Esse computador tem de estar no mesmo domínio que o servidor do site.  

#### <a name="application-catalog-web-service-point"></a>Ponto de serviço Web do Catálogo de Aplicações
Uma função de sistema de sites que fornece informações sobre software para o site do catálogo de aplicações a partir da biblioteca de software. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

#### <a name="application-catalog-website-point"></a>Ponto de site do Catálogo de Aplicações
Uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível a partir do Catálogo de Aplicações. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

Quando o catálogo de aplicações suportar computadores cliente na internet, para obter mais segurança, instale o ponto de sites do catálogo de aplicações numa rede de perímetro. Em seguida, instale o ponto de serviço web do catálogo de aplicações na intranet.  

#### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence
Uma função de sistema de sites liga à Microsoft para transferir informações para o catálogo do Asset Intelligence. Esta função também carrega títulos não categorizados, para que a Microsoft pode considerá-las para inclusão futura no catálogo. A hierarquia suporta apenas uma única instância desta função no site de nível superior da sua hierarquia. Se expandir um site primário autónomo para uma hierarquia maior, desinstale esta função do site primário. Em seguida, instale-o no site de administração central. 

Para obter mais informações, consulte [Asset Intelligence no Configuration Manager](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence).  

#### <a name="certificate-registration-point"></a>Ponto de registo de certificados
Uma função de sistema de sites que comunica com um servidor que executa o serviço de inscrição de dispositivos de rede (NDES). Esta função gere pedidos de certificado que utilizam o protocolo de inscrição de certificado (SCEP) simples. Esta função só é suportada em sites primários e no site de administração central.

Embora um ponto de registo de certificados único pode fornecer funcionalidade a uma hierarquia completa, pode querer instalar várias instâncias desta função num site e em vários sites na mesma hierarquia. Este design ajuda com balanceamento de carga. Quando existem várias instâncias numa hierarquia, os clientes são atribuídos aleatoriamente a um dos pontos de registo de certificados.  

Cada ponto de registo de certificados requer acesso a uma instância separada do NDES. Não é possível configurar dois ou mais pontos de registo de certificados para utilizar a mesma instância do NDES. Além disso, não instale o ponto de registo de certificados no mesmo servidor que executa o NDES.  

#### <a name="cloud-management-gateway-connection-point"></a>Ponto de ligação de gateway de gestão na cloud
Uma função de sistema de sites para comunicação com o [gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="data-warehouse-service-point"></a>Ponto de serviço do armazém de dados
Utilize o ponto de serviço do armazém de dados para armazenar e gerar relatórios sobre dados históricos de longo prazo no seu ambiente do Configuration Manager. Para obter mais informações, consulte [armazém de dados](/sccm/core/servers/manage/data-warehouse).  

#### <a name="distribution-point"></a>Ponto de distribuição
Uma função de sistema de sites que contém ficheiros de origem para os clientes transferirem, por exemplo: 
- Conteúdo da aplicação
- Pacotes de software
- Atualizações de software
- Imagens do sistema operacional
- Imagens de arranque  

Por predefinição, esta função é instalada no servidor do site de quando instala um novo site primário ou secundário. Esta função não é suportada num site de administração central. Instale várias instâncias desta função num site suportado e em vários sites na mesma hierarquia. Para obter mais informações, consulte [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management), e [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

#### <a name="endpoint-protection-point"></a>Ponto de Endpoint Protection
Uma função de sistema de sites do Configuration Manager utiliza para aceitar os termos de licenciamento do Endpoint Protection e para configurar a associação predefinida para o serviço de proteção de Cloud. A hierarquia suporta apenas uma única instância desta função e tem de estar no site de nível superior. Se expandir um site primário autónomo para uma hierarquia maior, desinstalar esta função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, consulte [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).  

#### <a name="enrollment-point"></a>Ponto de inscrição
Uma função de sistema de sites que utiliza certificados PKI para o Configuration Manager para registrar computadores móveis, dispositivos e macOS. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

Se um utilizador inscreve dispositivos móveis utilizando o Gestor de configuração e a conta de utilizador do Active Directory estiver numa floresta não considerada como fidedigna pela floresta do servidor de site, instale um ponto de registo na floresta do utilizador. Em seguida, o Configuration Manager pode autenticar o utilizador.  

#### <a name="enrollment-proxy-point"></a>Ponto proxy de registo
Uma função de sistema de sites que gere os pedidos de inscrição do Gestor de configuração de computadores móveis, dispositivos e macOS. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

Se forem suportados dispositivos móveis na internet, instale um ponto de proxy de registo numa rede de perímetro e instalá-lo na intranet.   

#### <a name="exchange-server-connector"></a>Conector do Exchange Server
Para obter informações sobre esta função, veja [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

#### <a name="fallback-status-point"></a>Ponto de estado de contingência
Uma função de sistema de sites que o ajuda a monitorizar a instalação de cliente. Identifica os clientes que não são geridos porque não é possível comunicar com o respetivo ponto de gestão. Embora esta função é suportada apenas em sites primários, pode instalar várias instâncias desta função num site e em vários sites na mesma hierarquia.     

#### <a name="management-point"></a>Ponto de gestão
Uma função de sistema de sites que fornece informações de localização de serviços e políticas a clientes. Ele também recebe dados de configuração de clientes.  

Por predefinição, esta função é instalada no servidor do site de quando instala um novo site primário ou secundário. Os sites primários suportam várias instâncias desta função. Os sites secundários suportam um único ponto de gestão. Também conhecido como um ponto de gestão do proxy, esta função num site secundário fornece um ponto de contacto para os clientes obterem políticas de utilizador e computador local.  

Configure pontos de gestão para suportar HTTP ou HTTPs. Eles também podem suportar dispositivos móveis que gere com a gestão de dispositivos móveis no local do Configuration Manager (MDM). Para ajudar a reduzir a carga de processamento colocada no servidor de base de dados do site por pontos de gestão à medida que atendem pedidos de clientes, utilize [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reporting-services-point"></a>Ponto do Reporting Services
Uma função de sistema de sites que se integra no SQL Server Reporting Services para criar e gerir relatórios do Configuration Manager. Esta função é suportada em sites primários e o site de administração central, e pode instalar várias instâncias desta função num site suportado. Para obter mais informações, consulte [planeamento de relatórios](/sccm/core/servers/manage/planning-for-reporting).  

#### <a name="service-connection-point"></a>Ponto de ligação de serviço
Uma função de sistema de sites que carrega dados de utilização do seu site e é necessária para disponibilizar atualizações para o Configuration Manager na consola do. Esta função também ajuda a gerir dispositivos móveis com o Microsoft Intune e MDM no local A hierarquia suporta apenas uma única instância desta função e tem de estar no site de nível superior da sua hierarquia. Se expandir um site primário autónomo para uma hierarquia maior, desinstalar esta função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, consulte [sobre o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

#### <a name="software-update-point"></a>Ponto de atualização de software
Uma função de sistema de sites que se integra com o Windows Server Update Services (WSUS) para fornecer atualizações de software para clientes do Configuration Manager. Esta função é suportada em todos os sites:  

-   Instale este sistema de sites no site de administração central para sincronizar com o WSUS.  

-   Configure cada instância desta função em sites primários subordinados para sincronizar com o site de administração central.  

-   Quando a transferência de dados em toda a rede estiver lenta, considere a instalação de um ponto de atualização de software em sites secundários.  

Para obter mais informações, consulte [planear atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).  

#### <a name="state-migration-point"></a>Ponto de Migração de Estado
Quando migra um computador para um novo sistema operativo, esta função de sistema de sites armazena dados de estado do utilizador. Esta função é suportada em sites primários e em sites secundários. Instale várias instâncias desta função num site e em vários sites na mesma hierarquia. Para obter mais informações sobre o armazenamento do Estado do utilizador ao implementar um sistema operacional, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  



## <a name="next-steps"></a>Passos seguintes

Algumas funções de sistema de sites do Configuration Manager exigem ligações à internet. Se o seu ambiente requer tráfego de internet para utilizar um servidor proxy, configure estas funções de sistema de sites para usar o proxy. Para obter mais informações, consulte [suporte de servidor de Proxy](/sccm/core/plan-design/network/proxy-server-support).  
