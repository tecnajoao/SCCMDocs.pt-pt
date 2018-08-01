---
title: Elevada disponibilidade
titleSuffix: Configuration Manager
description: Saiba como implementar o Configuration Manager, utilizando as opções que mantêm um elevado nível de serviço disponíveis.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18435bd43ed74daee646096d1e8d8b6ed7b7bc27
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39387103"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opções de elevada disponibilidade para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve como implementar o Configuration Manager utilizando as opções que mantém um elevado nível de serviço disponíveis.   

As seguintes opções do Configuration Manager suportam elevada disponibilidade:   

- A partir da versão 1806, configure o site de administração central e cada site primário com um servidor de sites adicionais em modo passivo.  
 
- Configure um grupo de disponibilidade Always On do SQL Server para a base de dados do site em sites primários e o site de administração central.

- Os sites suportam várias instâncias de funções de sistema de sites que fornecem serviços importantes aos clientes. Por exemplo, pontos de gestão e pontos de distribuição.  

- Sites de administração central e sites primários suportam a cópia de segurança da base de dados do site. A base de dados armazena todas as configurações dos sites e clientes. Os sites numa hierarquia compartilham esses dados de configuração.  

- Opções de recuperação de site interno podem reduzir o tempo de inatividade. Estas opções avançadas simplificam a recuperação quando tiver uma hierarquia com um site de administração central.  

- Os clientes podem remediar automaticamente problemas típicos sem intervenção administrativa.  

- Os sites geram alertas sobre os clientes que não submetam dados recentes, que alerta os administradores para potenciais problemas.  

- O Configuration Manager fornece diversos relatórios incorporados e dashboards. Utilizá-las para identificar problemas e tendências antes que comprometam operações de servidor ou cliente.  


O Configuration Manager inclui vários recursos que fornecem quase em tempo real serviço. Se estas funcionalidades são fundamentais para cumprir os requisitos comerciais, planear e configurar os sites e hierarquias para elevada disponibilidade. Por exemplo:  

- [Ações de notificação de cliente](/sccm/core/clients/manage/manage-clients), tal como o reinício, iniciar verificações do Windows Defender ou o ambiente de trabalho remoto.  

- Mensagens com base no estado das funcionalidades, tais como atualizações de software e proteção de ponto final de monitorização. 

- [Scripts](/sccm/apps/deploy-use/create-deploy-scripts), começando na versão 1706  

- [CMPivot](/sccm/core/servers/manage/cmpivot), começando na versão 1806  


Outros recursos do Configuration Manager não fornecem o serviço em tempo real. Estas funcionalidades incluem, mas não estão limitadas a, as definições de cliente, hardware e inventário de software, implementações de software e as definições de compatibilidade. Esperar que eles operem com alguma latência de dados. É invulgar para a maioria dos cenários que envolvam uma interrupção temporária do serviço para se tornar um problema crítico. Para minimizar o tempo de inatividade e manter a autonomia das operações para fornecer um alto nível de serviço, configure os sites e hierarquias com elevada disponibilidade em mente.  

Por exemplo, clientes do Configuration Manager normalmente funcionam de forma autónoma, utilizando agendas e configurações para as operações e agendas conhecidas para enviar dados para o site para processamento.  

- Quando os clientes não consegue contactar o site, colocam os dados sejam submetidos até que eles podem contactar o site.  

- Os clientes que não é possível contactar o site continuam a funcionar. Eles usam as últimas agendas conhecidas e as informações em cache, até conseguirem contactar o site e receber novas políticas. Por exemplo, um cliente pode manter aplicações anteriormente transferidas que devam executar ou instalar.   

- O site monitoriza os seus sistemas de sites e clientes para atualizações periódicas de estado. Pode gerar alertas quando esses componentes conseguem registar.  

- Relatórios incorporados fornecem informações aprofundadas sobre as operações em curso, histórico de operações e as tendências atuais. O Configuration Manager também suporta mensagens baseadas no Estado que fornecem quase informações em tempo real para operações em curso.  



##  <a name="bkmk_snh"></a> Elevada disponibilidade para sites e hierarquias  

#### <a name="use-a-site-server-in-passive-mode"></a>Utilizar um servidor de site em modo passivo
A partir da versão 1806, instalar um servidor de sites adicionais na *passivo* modo. O servidor de site em modo passivo está além do seu servidor de sites existente no *Active Directory* modo. Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Para obter mais informações, consulte [elevada disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

#### <a name="use-a-remote-content-library"></a>Utilizar uma biblioteca de conteúdos remota
A partir da versão 1806, mova a biblioteca de conteúdos do site para uma localização remota, que fornece armazenamento de elevada disponibilidade. Esta funcionalidade é um requisito para disponibilidade elevada do servidor de site. Para obter mais informações, consulte [a biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library#bkmk_remote).

#### <a name="centralize-content-sources"></a>Centralizar a fontes de conteúdo
Todos os conteúdos de software no Configuration Manager requer uma localização de origem do pacote na rede. Utilize o armazenamento centralizado e elevada disponibilidade para alojar uma localização de origem do pacote comum para todos os conteúdos. 

#### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Utilizar um grupo de disponibilidade Always On do SQL Server para alojar a base de dados do site  
Aloje a base de dados do site em sites primários e o site de administração central em grupos de disponibilidade Always On do SQL Server. Para obter mais informações, consulte [SQL Server Always On para uma base de dados do site de elevada disponibilidade](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

#### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Utilizar um cluster do SQL Server para alojar a base de dados do site  
Quando utilizar um cluster do SQL Server para a base de dados num site de administração central ou site primário, utilize o suporte de ativação pós-falha incorporado no SQL Server.  

Os sites secundários não é possível utilizar um cluster do SQL Server e não suportam a cópia de segurança ou restauro da respetiva base de dados do site. Recupere um site secundário reinstalando o site secundário do respetivo site primário principal.  

#### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Implementar uma hierarquia de sites com um site de administração central e um ou mais sites primários subordinados  
Esta configuração fornece tolerância a falhas quando os sites gerem segmentos sobrepostos da sua rede. Ele também oferece uma opção de recuperação adicionais para utilizar as informações da base de dados partilhada disponível noutro site, para reconstruir a base de dados do site recuperado. Utilize esta opção para substituir uma cópia de segurança falhada ou indisponível da base de dados do site com falha.  

#### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Criar cópias de segurança regulares em sites de administração central e sites primários  
Quando cria e testar uma cópia de segurança regular do site, isto torna-se de que os dados necessários para recuperar um site. Também pratica a recuperar um site no menor período de tempo.  

#### <a name="install-multiple-instances-of-site-system-roles"></a>Instalar várias instâncias de funções de sistema de sites  
Ao instalar várias instâncias de funções do sistema de site essencial, fornecer pontos de contacto redundantes para os clientes. Por exemplo, vários pontos de gestão e pontos de distribuição forneçam serviço redundante, no caso de um servidor específico está offline.  

#### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Instalar várias instâncias do fornecedor de SMS num site  
O fornecedor de SMS fornece o ponto de contacto administrativo para uma ou mais consolas do Configuration Manager. Para fornecer redundância de pontos de contacto para administrar o site e a hierarquia, instale vários fornecedores de SMS.  



##  <a name="bkmk_ssr"></a> Elevada disponibilidade para funções de sistema de sites  
Em cada site, implemente as funções de sistema de sites para fornecer os serviços que pretende que os clientes utilizem nesse site. A base de dados do site contém as informações de configuração para o site e para todos os clientes. Utilize um ou mais das opções disponíveis para fornecer elevada disponibilidade da base de dados do site e a recuperação do site e da base de dados do site se for necessário.  

#### <a name="redundancy-for-important-site-system-roles"></a>Redundância para funções de sistema de sites importantes  
-   Ponto de serviço da web de catálogo de aplicações  

-   Ponto de Web site do catálogo de aplicações  

-   Ponto de distribuição  

-   Ponto de gestão  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado  

Para fornecer redundância de relatórios em sites e clientes, de instalar várias instâncias do ponto do reporting services.

Para obter suporte de ativação pós-falha com o software de ponto de atualização, utilize o Windows PowerShell para instalar esta função numa carga de rede do Windows (NLB) cluster de balanceamento.  

#### <a name="built-in-site-backup"></a>Cópia de segurança incorporada do site  
O Configuration Manager inclui uma tarefa de cópia de segurança incorporada para o ajudar a cópia de segurança do site e das informações críticas com base numa agenda regular. Além disso, o Assistente de configuração do Configuration Manager suporta ações de restauro de site para o ajudar a restaurar o funcionamento de um site.  

#### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publicação de serviços de domínio do Active Directory e DNS  
Configure cada site para publicar dados sobre o site de serviços de domínio do Active Directory e DNS. Esta publicação permite que os clientes identificar o servidor mais acessível na rede. Os clientes também utilizam-lo para identificar quando novos servidores do sistema de sites estão disponíveis para fornecer serviços importantes, como pontos de gestão.  

#### <a name="sms-provider-and-configuration-manager-console"></a>Consola de fornecedor de SMS e o Configuration Manager  
O Configuration Manager suporta a instalação de vários fornecedores de SMS em servidores separados como vários pontos de acesso para a consola. Se um servidor do fornecedor de SMS estiver offline, pode ainda ver e gerir sites e clientes.  

Quando uma consola do Configuration Manager se liga a um site, liga-se para uma instância do fornecedor de SMS nesse site. A instância do fornecedor de SMS é selecionada aleatoriamente. Se o fornecedor de SMS selecionado não estiver disponível, tem as seguintes opções:  

-   Voltar a ligar a consola ao site. Cada novo pedido de ligação é atribuído aleatoriamente uma instância do fornecedor de SMS. É possível que é atribuída uma instância disponível à nova ligação.  

-   Ligue a consola a outro site do Configuration Manager e gerir a configuração a partir dessa ligação. Esta opção apresenta um ligeiro atraso nas alterações de configuração de não mais do que alguns minutos. Depois do fornecedor de SMS para o site estiver online, voltar a ligar a consola do Configuration Manager diretamente para o site que pretende gerir.  

Instale a consola do Configuration Manager em vários computadores para utilização pelos administradores. Cada fornecedor de SMS suporta ligações a partir de mais do que uma consola.  

#### <a name="management-point"></a>Ponto de gestão  
Instalar vários pontos de gestão em cada site primário e permita que os sites publicar dados do site para a sua infraestrutura de Active Directory e DNS.  

Vários pontos de gestão ajudam a balancear a carga a utilização de qualquer ponto de gestão único por vários clientes. Considere também a instalação de uma ou mais réplicas de base de dados para pontos de gestão. Esta configuração reduz as operações de uso intenso do processador do ponto de gestão. Ele também aumenta a disponibilidade desta função de sistema críticos do site.  

Os sites secundários suportam apenas a instalação de um ponto de gestão, que tem de estar localizado no servidor do site secundário. Pontos de gestão em sites secundários não são considerados ter uma configuração de elevada disponibilidade.  

> [!NOTE]  
>  Ligarem dispositivos geridos por gestão de dispositivos móveis no local para apenas um ponto de gestão num site primário. O ponto de gestão é atribuído pelo Configuration Manager para o dispositivo móvel durante a inscrição e, em seguida, não é alterado. Quando instalar vários pontos de gestão e ativar mais do que um para dispositivos móveis, o ponto de gestão que é atribuído a um cliente de dispositivo móvel é determinística.  
>   
>  Se o ponto de gestão que utiliza o cliente do dispositivo móvel ficar indisponível, deve resolver o problema com esse ponto de gestão ou apagar o dispositivo móvel e voltar a inscrever o dispositivo móvel, de modo a que podem ser atribuído a um ponto de gestão operacional que está ativado para dispositivos móveis.  

#### <a name="distribution-point"></a>Ponto de distribuição  
Instalar vários pontos de distribuição e implementar conteúdo em vários pontos de distribuição. Adicione mais do que um ponto de distribuição por grupo de limites para se certificar de que os clientes obtêm várias opções em que o pedido de conteúdo. Configure as relações de grupo de limites para que eles têm um comportamento de contingência previsíveis para outro grupo de limites ou ponto de distribuição de nuvem. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

#### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Ponto de serviço da web de catálogo de aplicações e ponto de Web site do catálogo de aplicações  
Instale mais do que uma instância de cada função de sistema de sites. Para obter melhor desempenho, implemente um de cada no mesmo servidor de sistema do site.  

Cada função de sistema de sites de catálogo de aplicações fornece as mesmas informações que outras instâncias de função, independentemente da sua localização na hierarquia. Quando um cliente faz um pedido para o catálogo de aplicações, e tiver configurado o ponto de clientes para detetar automaticamente o site predefinido do catálogo de aplicações, o cliente é direcionado para uma instância disponível. Os clientes preferem a instâncias de catálogo de aplicações locais, com base na localização de rede atual do cliente.  

Para obter mais informações sobre este cliente definição e automática como funciona a deteção, consulte a [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) secção a [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings) artigo.  



##  <a name="bkmk_client"></a> Elevada disponibilidade para clientes  

#### <a name="client-operations-are-autonomous"></a>As operações de cliente são autónomas  
Autonomia de cliente do Configuration Manager inclui os comportamentos seguintes:  

-   Os clientes não requerem contacto contínuo com quaisquer servidores de sistema de site específico. Utilizam configurações conhecidas para executarem ações pré-configuradas com base numa agenda.  

-   Os clientes podem utilizar qualquer instância disponível de uma função de sistema de sites que forneça serviços aos clientes. Eles tentam contactar servidores conhecidos até eles localizar um servidor disponível.  

-   Os clientes podem executar o inventário, implementações de software e ações agendadas semelhantes independentemente do contacto direto com servidores de sistema de sites.  

-   Os clientes que estão configurados para utilizar um ponto de estado de contingência poderão submeter detalhes para o ponto de estado de contingência quando não conseguirem comunicar com um ponto de gestão.  

#### <a name="clients-can-repair-themselves"></a>Os clientes conseguem reparar-se  
Os clientes remedeiam automaticamente a maioria dos problemas comuns sem intervenção administrativa direta.  

-   Periodicamente, os clientes autoavaliam o respetivo estado. Eles tomar medidas para remediar problemas típicos, utilizando uma cache local dos passos de remediação e arquivos para reparações de origem.  

-   Quando um cliente consegue submeter informações de estado para o respetivo site, o site poderá gerar um alerta. Os utilizadores administrativos que recebam estes alertas poderão tomar imediatamente medidas para restaurar o funcionamento normal do cliente.  

#### <a name="clients-cache-information-to-use-in-the-future"></a>Os clientes colocam informações para utilização futura cache  
Quando um cliente comunica com um ponto de gestão, o cliente pode obter e armazenar em cache as seguintes informações:  

-   Definições do cliente  

-   Agendas do cliente  

-   Informações sobre implementações de software e de um download do software cliente estão agendadas para instalar, quando a instalação estiver configurada para esta ação.  

Quando um cliente não consegue contactar um ponto de gestão, os clientes localmente em cache as informações de estado, o estado e o cliente que reportam ao site. O cliente transfere esses dados depois de estabelecer contato com um ponto de gestão.  

#### <a name="client-can-submit-status-to-a-fallback-status-point"></a>O cliente pode submeter o estado a um ponto de estado de contingência  
Ao configurar um cliente para utilizar um ponto de estado de contingência, está a fornecer um ponto adicional de contacto para o cliente submeter detalhes importantes sobre o respetivo funcionamento. Os clientes que estão configurados para utilizar um ponto de estado de contingência continuam a enviar de estado sobre suas operações para essa função de sistema de sites, mesmo quando o cliente não consegue comunicar com um ponto de gestão.  

#### <a name="central-management-of-client-data-and-client-identity"></a>Gerenciamento central de dados de cliente e a identidade do cliente  
A base de dados do site, em vez do cliente de individual, contém informações importantes sobre a identidade de cada cliente e associando esses dados para um computador específico, ou o utilizador.  

-   Os ficheiros de origem do cliente num computador podem ser desinstalados e reinstalados sem afetar o histórico dos registos para o computador onde está instalado o cliente.  

-   Falha de um computador cliente não afeta a integridade das informações que são armazenadas na base de dados. Estas informações permanecem disponíveis para relatórios.  



##  <a name="bkmk_nonHAoptions"></a> Opções para sites e funções de sistema de sites que não estão altamente disponíveis  
Diversos sistemas de sites não suportam várias instâncias num site ou na hierarquia. Estas informações podem ajudar a preparar para estes sistemas de sites ficar offline.  

#### <a name="site-server-site"></a>Servidor do site (site)  

> [!Note]  
> Esta secção aplica-se apenas às versões do Configuration Manager 1802 e versões anteriores. A partir da versão 1806, o Configuration Manager fornece uma opção de elevada disponibilidade para o servidor do site. Para obter mais informações, consulte [elevada disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

O Configuration Manager não suporta a instalação do servidor do site para cada site num cluster do Windows Server ou cluster NLB.  

As seguintes informações podem ajudar a preparar quando um servidor de sites falha ou não está operacional:  

-   Utilize a tarefa de cópia de segurança incorporada para criar regularmente uma cópia de segurança do site. Num ambiente de teste, regularmente os sites restaurar a partir de uma cópia de segurança.  

-   Implemente vários sites do Configuration Manager primário numa hierarquia com um site de administração central para criar redundância. Se ocorrer uma falha de site, considere utilizar scripts de política ou de início de sessão de grupo do Windows para reatribuir clientes a um site funcional.  

-   Se tiver uma hierarquia com um site de administração central, pode recuperar o site de administração central ou um site primário subordinado utilizando a opção para recuperar uma base de dados do site a partir de outro site na sua hierarquia.  

-   Os sites secundários não não possível restaurar e tem de ser reinstalados.  

#### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Ponto de sincronização do Asset intelligence (hierarquia)  
Esta função de sistema de sites não é considerada missão crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor.  

#### <a name="endpoint-protection-point-hierarchy"></a>Ponto de Endpoint protection (hierarquia)  
Esta função de sistema de sites não é considerada missão crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor.  

#### <a name="enrollment-point-site"></a>Ponto de registo (site)  
Esta função de sistema de sites não é considerada missão crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor.  

#### <a name="enrollment-proxy-point-site"></a>Ponto de proxy de registo (site)  
Esta função de sistema de sites não é considerada missão crítica e fornece uma funcionalidade opcional no Configuration Manager. No entanto, pode instalar várias instâncias desta função de sistema de sites num site e em vários sites na hierarquia. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor.  

Quando tiver mais do que um servidor de proxy de registo num site, utilize um alias de DNS para o nome do servidor. Quando utiliza esta configuração, o DNS round robin fornece alguma tolerância a falhas e balanceamento de carga quando os utilizadores inscrevem os respetivos dispositivos móveis.  

#### <a name="fallback-status-point-site-or-hierarchy"></a>Ponto de estado de contingência (site ou hierarquia)  
Esta função de sistema de sites não é considerada missão crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor. Uma vez que os clientes são atribuídos o ponto de estado de contingência durante a instalação de cliente, terá de modificar os clientes existentes para utilizar o novo servidor de sistema de sites.  


#### <a name="service-connection-point-hierarchy"></a>Ponto de ligação de serviço (hierarquia)
Embora esta função de sistema de sites é essencial para manter o ramo atual do Configuration Manager atualizado, geralmente não é utilizada com frequência. Se este sistema fica offline, utilize uma das seguintes opções:

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstalar a função do servidor atual e instalar a função num novo servidor.  



## <a name="see-also"></a>Consulte também  
- [Configurações suportadas](/sccm/core/plan-design/configs/supported-configurations)  

- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)  

- [Sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)   

- [Pré-requisitos do site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)  

- [Impactos de falha do site](/sccm/core/servers/manage/site-failure-impacts)  

