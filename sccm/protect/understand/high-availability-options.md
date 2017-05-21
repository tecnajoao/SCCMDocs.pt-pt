---
title: Elevada disponibilidade | Documentos do Microsoft
description: "Saiba como implementar o System Center Configuration Manager, utilizando as opções que mantém um elevado nível de serviço disponíveis."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: d3e9afb90cdc85bc7299626b642c52be659e3bdf
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Opções de elevada disponibilidade para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



Pode implementar o System Center Configuration Manager utilizando as opções que mantém um elevado nível de serviço disponíveis.   

Opções que suportem elevada disponibilidade:   

-   Os sites suportam várias instâncias de servidores de sistema de sites que fornecem serviços importantes aos clientes.  

-   Sites de administração central e sites primários suportam cópias de segurança da base de dados do site. A base de dados do site contém todas as configurações dos sites e clientes, sendo partilhada entre os sites numa hierarquia que contêm um site de administração central.  

-   Opções de recuperação de site incorporados podem reduzir o período de indisponibilidade do servidor e incluem opções avançadas que simplificam a recuperação quando tiver uma hierarquia com um site de administração central.  

-   Os clientes podem remediar automaticamente problemas típicos sem intervenção administrativa.  

-   Os sites geram alertas sobre os clientes que não submetam dados recentes, o que alerta os administradores para potenciais problemas.  

-   O Configuration Manager oferece diversos relatórios incorporados que permitem-lhe identificar problemas e tendências antes que comprometam operações de cliente de servidor ou.  

 O Configuration Manager não fornece um serviço em tempo real e de esperar que apresente um funcionamento com alguma latência de dados. Por conseguinte, é pouco usual maior parte dos cenários que envolvam uma interrupção temporária do serviço se tornem num problema crítico. Quando configurou os sites e hierarquias a pensar na elevada disponibilidade, o tempo de inatividade pode ser minimizado, autonomy das operações mantidas, e um elevado nível de serviço fornecido.  

 Por exemplo, os clientes do Configuration Manager normalmente funcionam de forma autónoma, utilizando agendas conhecidas e as configurações de operações e agendando a submissão de dados para o site para processamento.  

-   Quando os clientes não consigam contactar o site, colocam os dados para ser submetidas até que eles possam contactar o site.  

-   Os clientes que não é possível contactar o site continuam a funcionar utilizando as últimas agendas conhecidas e as informações em cache, tais como aplicações anteriormente transferidas que devam executar ou instalar, até conseguirem contactar o site e receber novas políticas.  

-   O site monitoriza os sistemas de sites e clientes, procurando atualizações periódicas de estado e podendo gerar alertas quando as conseguir registar.  

-   Os relatórios incorporados fornecem informações aprofundadas sobre as operações em curso, bem como as tendências e histórico de operações. O Configuration Manager também suporta mensagens baseadas no Estado que fornecem quase em tempo real informações para operações em curso.  

  Utilize as informações neste tópico juntamente com as informações dos seguintes artigos:
-   [Hardware recomendado](../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos suportados para serveres de sistema de sites](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Site e os pré-requisitos de sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a>Elevada disponibilidade para sites e hierarquias  
 **Utilize um cluster do SQL Server para alojar a base de dados do site:**  

 Quando utiliza um cluster do SQL Server para a base de dados num site de administração central ou site primário, é utilizado o suporte de ativação pós-falha incorporado no SQL Server.  

 Os sites secundários não é possível utilizar um cluster do SQL Server e não suportam a cópia de segurança ou restauro da respetiva base de dados do site. Recupere um site secundário reinstalando-o site secundário a partir do respetivo site primário principal.  

 **Utilize um grupo de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site:**  

 A partir da versão 1602, pode utilizar grupos de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site em sites primários e o site de administração central como uma solução de elevada disponibilidade e recuperação de desastres. Para obter mais informações, consulte o artigo [SQL Server AlwaysOn numa base de dados do site elevada para o System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Implemente uma hierarquia de sites com um site de administração central e um ou mais sites primários subordinados:**  

 Esta configuração fornece tolerância a falhas quando os sites gerem segmentos sobrepostos da rede. Além disso, esta configuração oferece uma opção de recuperação adicionais utilizando as informações na base de dados partilhada disponível noutro site, para recriar a base de dados do site recuperado. Pode utilizar esta opção para substituir uma cópia de segurança falhada ou indisponível da base de dados do site em falha.  

 **Crie cópias de segurança regulares em sites de administração central e sites primários:**  

 Quando criar e testar uma cópia de segurança regular do site, pode certificar-se de que tem os dados necessários para recuperar um site bem como da experiência para recuperar um site a quantidade mínima de tempo.  

 **Instale múltiplas instâncias das funções do sistema de sites:**  

 Ao instalar múltiplas instâncias das funções de sistema críticos do site, tais como o ponto de gestão e o ponto de distribuição, está a fornecer pontos de contacto redundantes para os clientes no caso de um servidor do sistema de sites específicas se encontre offline.  

 **Instale múltiplas instâncias do fornecedor de SMS num site:** O fornecedor de SMS fornece o ponto de contacto administrativo para um ou mais consolas do Configuration Manager. Ao instalar múltiplos Fornecedores de SMS, poderá fornecer redundância de pontos de contacto, ao administrar o site e a hierarquia.  

##  <a name="bkmk_ssr"></a>Elevada disponibilidade para funções do sistema de sites  
 Em cada site, implemente as funções de sistema de sites para fornecer os serviços que pretende que os clientes utilizem nesse site. A base de dados do site contém as informações de configuração para o site e para todos os clientes. Utilize um ou mais das opções disponíveis para fornecer elevada disponibilidade da base de dados do site, bem como a recuperação do site e da base de dados do site, se necessário.  

 **Redundância para funções de sistema de sites importantes:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de distribuição  

-   Ponto de gestão  

-   Ponto de atualização de Software  

-   Ponto de migração de estado  

 É possível instalar múltiplas instâncias da função de ponto do Reporting services para fornecer redundância de relatórios em sites e clientes.

 Pode utilizar o PowerShell para instalar a função de sistema de sites de ponto de atualização de Software num cluster de balanceamento de carga de rede ao Windows ' (NLB) para fornecer suporte de ativação pós-falha  


 **Cópia de segurança incorporada do site:**  

 O Configuration Manager inclui uma tarefa de cópia de segurança incorporada para o ajudar a cópia de segurança do site e informações críticas, com base numa agenda regular. Além disso, o Assistente de configuração do Configuration Manager suporta ações de restauro de site para ajudar a restaurar um site de operações.  

 **Publicação de serviços de domínio do Active Directory e no DNS:**  

 Pode configurar cada site para publicar dados sobre servidores de sistema de sites e serviços, serviços de domínio do Active Directory e no DNS. Isto permite que os clientes para identificar o servidor mais acessível na rede e determinem quando se encontram disponíveis novos servidores de sistema de sites que possam fornecer serviços importantes, tais como pontos de gestão.  

 **Consola do fornecedor de SMS e o Configuration Manager:**  

 O Configuration Manager suporta a instalação de vários fornecedores de SMS, cada uma num computador separado, para garantir a vários pontos de acesso para a consola do Configuration Manager. Isto garante que, se um computador com fornecedor de SMS estiver offline, que mantém a capacidade de visualizar e reconfigurar sites do Configuration Manager e os clientes.  

 Quando uma consola do Configuration Manager estabelece ligação a um site, liga-se para uma instância do fornecedor de SMS nesse site. A instância do fornecedor de SMS é selecionada de modo não determinístico. Se o fornecedor de SMS selecionado não estiver disponível, tem as seguintes opções:  

-   Voltar a ligar a consola ao site. Cada novo pedido de ligação é atribuído modo não determinístico uma instância do fornecedor de SMS e é possível que a ligação novo será atribuída uma instância disponível.  

-   Ligue a consola a outro site do Configuration Manager e gerir a configuração a partir dessa ligação. Este procedimento introduz um ligeiro atraso nas alterações de configuração da não mais de alguns minutos. Depois do fornecedor de SMS para o site estiver online, pode voltar a ligar a consola do Configuration Manager diretamente para o site que pretende gerir.  

 Pode instalar a consola do Configuration Manager em vários computadores para utilização por utilizadores administrativos. Cada fornecedor de SMS suporta ligações a partir de várias consolas do Configuration Manager.  

 **Ponto de gestão:**  

 Instale vários pontos de gestão em cada site primário e permita que os sites publiquem dados do site a infraestrutura do Active Directory e no DNS.  

 Vários pontos de gestão ajudam a balancear a carga da utilização de qualquer ponto de gestão individual por vários clientes. Além disso, pode instalar uma ou mais réplicas de base de dados para pontos de gestão reduzam as operações intensivas em CPU do ponto de gestão e aumentem a disponibilidade desta função de sistema críticos do site.  

 Como é possível instalar apenas um ponto de gestão num site secundário, que tem de estar localizado no servidor do site secundário, os pontos de gestão em sites secundários não são considerados como possuindo configurações de elevada disponibilidade.  

> [!NOTE]  
>  Ligam dispositivos geridos por gestão de dispositivos móveis no local a apenas um ponto de gestão num site primário. O ponto de gestão é atribuído pelo Configuration Manager para o dispositivo móvel durante a inscrição e, em seguida, não se altera. Quando instalar vários pontos de gestão e ativar mais do que um deles para dispositivos móveis, o ponto de gestão que está atribuído a um cliente de dispositivo móvel é não determinística.  
>   
>  Se o ponto de gestão que utiliza o cliente de dispositivo móvel ficar indisponível, terá de resolver o problema desse ponto de gestão ou apagar o dispositivo móvel e voltar a inscrever o dispositivo móvel, para que podem ser atribuído a um ponto de gestão operacional que está ativado para dispositivos móveis.  

 **Ponto de distribuição:**  

 Instale vários pontos de distribuição e implemente o conteúdo em vários pontos de distribuição. Pode configurar grupos de limites sobrepostos para localização de conteúdo para assegurar que os clientes em cada sub-rede conseguem aceder uma implementação a partir de dois ou mais pontos de distribuição. Finalmente, considere configurar uma ou mais pontos de distribuição como localizações de contingência para conteúdo.  

 Para obter mais informações sobre localizações de contingência para conteúdo, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Ponto de serviço da web de catálogo de aplicações e ponto de Web site do catálogo de aplicações:**  

 Pode instalar várias instâncias de cada função do sistema de sites e para um melhor desempenho, implementar uma de cada no mesmo computador do sistema de sites.  

 Cada função de sistema de sites do catálogo de aplicações fornece as mesmas informações que outras instâncias dessa função do sistema de sites, independentemente da localização desta função de servidor de sites na hierarquia. Por conseguinte, quando um cliente envia um pedido para o catálogo de aplicações e tiver configurado o cliente de dispositivo do ponto do catálogo de aplicações predefinido Web site automaticamente a definição para detetar, o cliente pode ser direcionado para uma instância disponível. Preferência é atribuída ao servidores locais de sistema do site catálogo de aplicações, com base na localização de rede atual do cliente.  

 Para mais informações sobre este cliente funciona a deteção definição e como automático, consulte o [agente do computador](../../core/clients/deploy/about-client-settings.md#computer-agent) secção a [sobre definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md) tópico.  

##  <a name="bkmk_client"></a>Elevada disponibilidade para clientes  
 **Operações de cliente são autónomas:**  

 Autonomy de cliente do Configuration Manager inclui o seguinte:  

-   Os clientes não requerem contacto contínuo com quaisquer servidores de sistema de sites específicas. Utilizam configurações conhecidas para executarem ações pré-configuradas com base numa agenda.  

-   Os clientes podem utilizar qualquer instância disponível de uma função de sistema de sites que forneça serviços aos clientes e irão tentar contactar servidores conhecidos até ser localizado um servidor disponível.  

-   Os clientes podem executar o inventário, implementações de software e ações agendadas semelhantes, independentemente do contacto direto com servidores de sistema de sites.  

-   Os clientes que estão configurados para utilizar um ponto de estado de contingência poderão submeter detalhes para o ponto de estado de contingência quando não conseguirem comunicar com um ponto de gestão.  

 **Os clientes conseguem reparar-se a si:**  

 Os clientes remedeiam automaticamente problemas mais típicos sem intervenção administrativa direta:  

-   Periodicamente, os clientes autoavaliam o respetivo estado e tomam medidas para remediar problemas típicos, utilizando uma cache local de passos de remediação e ficheiros de origem para reparações.  

-   Quando um cliente não consegue submeter informações de estado para o respetivo site, o site poderá gerar um alerta. Os utilizadores administrativos que recebam estes alertas poderão tomar imediatamente medidas para restaurar o funcionamento normal do cliente.  

 **Os clientes colocam informações para utilização futura em cache:**  

 Quando um cliente comunica com um ponto de gestão, o cliente pode obter e colocar em cache as seguintes informações:  

-   Definições do cliente.  

-   Agendas do cliente.  

-   Informações sobre implementações de software e uma transferência do software de cliente estão agendadas para a instalação, quando a implementação estiver configurada para esta ação.  

 Quando um cliente não consegue contactar um ponto de gestão de clientes localmente colocar em cache as informações de estado, o estado e o cliente que reportam ao site e transfiram esses dados após estabelecerem contacto com um ponto de gestão.  

 **O cliente pode submeter o estado a um ponto de estado de contingência:**  

 Ao configurar um cliente para utilizar um ponto de estado de contingência, está a fornecer um ponto de contacto para o cliente submeter detalhes importantes sobre o respetivo funcionamento adicional. Os clientes que estão configurados para utilizar um ponto de estado de contingência continuarão a enviar estado acerca das suas operações para essa função de sistema de sites, mesmo quando o cliente não consegue comunicar com um ponto de gestão.  

 **Gestão central de dados de cliente e a identidade do cliente:**  

 A base de dados do site, em vez do cliente individual, contém informações importantes sobre a identidade de cada cliente e, associando esses dados para um computador específico ou o utilizador. Isto significa que:  

-   Os ficheiros de origem do cliente num computador podem ser desinstalados e reinstalados sem afetar o histórico dos registos para o computador onde está instalado o cliente.  

-   Falha de um computador cliente não afeta a integridade das informações que são armazenadas na base de dados. Estas informações permanecem disponíveis para relatórios.  

##  <a name="bkmk_nonHAoptions"></a>Opções para sites e funções de sistema de sites que não são de elevada disponibilidade  
 Diversos sistemas de sites não suportam várias instâncias num site ou na hierarquia. Estas informações podem ajudar a preparar para estes sistemas de sites ficar offline.  

 **Servidor do site (site):**  

 O Configuration Manager não suporta a instalação do servidor do site para cada site num cluster do Windows Server ou cluster de NLB.  

 As seguintes informações podem ajudar a preparar quando um servidor de sites falha ou não está operacional:  

-   Utilize a tarefa de cópia de segurança incorporada para criar regularmente uma cópia de segurança do site. Num ambiente de teste, regularmente os sites restauro a partir de uma cópia de segurança.  

-   Implemente vários sites do Configuration Manager primário numa hierarquia com um site de administração central para criar redundância. Se ocorrer uma falha de site, considere utilizar scripts de início de sessão ou de política de grupo do Windows para reatribuir clientes a um site funcional.  

-   Se tiver uma hierarquia com um site de administração central, pode recuperar o site de administração central ou um site primário subordinado utilizando a opção para recuperar uma base de dados do site a partir de outro site na sua hierarquia.  

-   Os sites secundários não podem ser restaurados e tem de ser reinstalados.  

 **Sincronização ponto de Asset Intelligence (hierarquia):**  

 Esta função do sistema de sites não é considerada fundamental para a atividade crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites ficasse offline.  

-   Desinstale a função do servidor atual e instalar a função num novo servidor.  

 **Ponto de Endpoint Protection (hierarquia):**  

 Esta função do sistema de sites não é considerada fundamental para a atividade crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites ficasse offline.  

-   Desinstale a função do servidor atual e instalar a função num novo servidor.  

 **Ponto de registo (site):**  

 Esta função do sistema de sites não é considerada fundamental para a atividade crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites ficasse offline.  

-   Desinstale a função do servidor atual e instalar a função num novo servidor.  

 **Ponto de proxy de registo (site):**  

 Esta função do sistema de sites não é considerada fundamental para a atividade crítica e fornece uma funcionalidade opcional no Configuration Manager. No entanto, pode instalar várias instâncias desta função do sistema de sites num site e, em vários sites na hierarquia. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites ficasse offline.  

-   Desinstale a função do servidor atual e instalar a função num novo servidor.  

 Quando tiver mais do que um servidor de proxy de registo num site, utilize um alias DNS para o nome do servidor. Quando utiliza esta configuração, o DNS round robin assegura alguma tolerância a falhas e balanceamento de carga quando os utilizadores inscrevem os respetivos dispositivos móveis.  

 **Ponto de estado de contingência (site ou hierarquia):**  

 Esta função do sistema de sites não é considerada fundamental para a atividade crítica e fornece uma funcionalidade opcional no Configuration Manager. Se este sistema de sites ficar offline, utilize uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites ficasse offline.  

-   Desinstale a função do servidor atual e instalar a função num novo servidor. Uma vez que o ponto de estado de contingência são atribuídos clientes durante a instalação do cliente, terá de modificar os clientes existentes para utilizarem o novo servidor de sistema de sites.  

### <a name="see-also"></a>Consulte também  
 [Configurações suportadas para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)

