---
title: Interoperabilidade entre versões
titleSuffix: Configuration Manager
description: Saiba como evitar conflitos entre várias hierarquias do System Center Configuration Manager na mesma rede.
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccb7861b5264d649a8ff4b2340bf34eaaafe7970
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126985"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre diferentes versões do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar e operar várias hierarquias independentes do System Center Configuration Manager, na mesma rede. No entanto, uma vez que hierarquias diferentes do Configuration Manager não interoperam fora do processo de migração, cada hierarquia necessita de configurações para evitar conflitos entre eles. Além disso, pode criar determinadas configurações para ajudar os recursos que gere interagirem com os sistemas de sites da hierarquia correta.  

As secções seguintes fornecem informações sobre a utilização de diferentes versões do Configuration Manager na mesma rede:  

-   [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

-   [Interoperabilidade para a Consola do Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitações do Configuration Manager numa hierarquia com várias versões](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  
Sites de diferentes versões não podem coexistir na mesma hierarquia, exceto durante o processo de atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager ou de uma versão do System Center Configuration Manager para um (versão mais recente através das atualizações na consola).   

Uma vez que pode implementar um site do System Center Configuration Manager e da hierarquia lado a lado com um sistema existente Center 2012 Configuration Manager site ou hierarquia, planeie impedir que os clientes de uma das versões tentem aderir um site a partir de outra versão.

Por exemplo, se tiverem duas ou mais hierarquias do Configuration Manager [sobreposição de limites](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries) que incluam as mesmas localizações de rede, atribuir cada novo cliente a um site específico, em vez de utilizar a atribuição automática de site. Para obter mais informações, consulte [como atribuir clientes a um site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Além disso, não é possível instalar um cliente do System Center 2012 Configuration Manager num computador que aloje uma função de sistema de sites do System Center Configuration Manager, nem pode instalar um cliente do System Center Configuration Manager num computador que aloja um função de sistema de sites do System Center 2012 Configuration Manager.  

Da mesma forma, não são suportadas os seguintes clientes e ligações:  

- Qualquer System Center 2012 Configuration Manager ou a versão de cliente de computador anterior  

- Qualquer System Center 2012 Configuration Manager ou o cliente de gestão de dispositivos anterior  

- Cliente de gestão de dispositivos do Windows CE Platform Builder (qualquer versão)  

- Ligação VPN do System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre a atribuição de sites a clientes  
Clientes do Configuration Manager podem ser atribuídos a um único site primário. Quando a atribuição automática de sites é utilizada para atribuir clientes a um site durante a instalação de cliente e mais de um grupo de limites incluir o mesmo limite e os grupos de limites tem diferentes sites atribuídos, não é possível prever a atribuição de site real de um cliente .  

Se existir sobreposição de limites em vários sites do Configuration Manager e hierarquias, os clientes poderão não ser atribuídos ao site esperado ou poderão não ser atribuídos a um site de todo.  

Os clientes do System Center Configuration Manager verificam a versão do site do Configuration Manager antes de concluírem a atribuição de site e não pode ser atribuídos a uma versão anterior, quando e se existir sobreposição de limites de site. No entanto, os clientes do System Center 2012 Configuration Manager incorretamente podem ser atribuídos a um site do System Center Configuration Manager.  

Para impedir que os clientes de atribuição não intencional para site incorreto quando duas hierarquias tiverem sobreposição de limites, configure parâmetros de instalação de cliente do Configuration Manager para atribuir clientes a um site específico.  

##  <a name="bkmk_mixed"></a> Limitações do Configuration Manager numa hierarquia com várias versões  
Quando estiver no processo de atualização de um site do System Center Configuration Manager, há vezes em diferentes sites serão necessário versões diferentes. Por exemplo, poderá atualizar um site de administração central para uma nova versão mas, devido a janelas de manutenção do site, um ou mais sites primários podem não atualizar até uma hora e data posterior.  

Quando diversos sites de uma única hierarquia executam versões diferentes, algumas funcionalidades não se encontram disponíveis. Isso pode afetar a forma como gere objetos do Configuration Manager na consola do Configuration Manager e que funcionalidade não está disponível para os clientes. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não estão acessível em sites ou para os clientes que executem uma versão inferior do service pack.  

### <a name="limitations-when-upgrading-configuration-manager"></a>Limitações ao atualizar o Configuration Manager  

|Objeto|Detalhes|  
|------------|-------------|  
|Conta de acesso à rede|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:** Ao visualizar os detalhes de conta de acesso à rede de uma consola do Configuration Manager que está ligado a um site de administração central que foi atualizado para o System Center Configuration Manager, a consola não apresenta detalhes de contas que estão configuradas num site primário que executa o System Center 2012 Configuration Manager. Depois do site primário ser atualizado para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Quando exibe os detalhes de conta de acesso à rede de uma consola do Configuration Manager que está ligado a um site de administração central que foi atualizado para uma nova versão do System Center Configuration Manager, a consola não apresenta detalhes de contas que são configuradas num site primário que executa uma versão anterior. Depois do site primário ser atualizado para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.|  
|Imagens de arranque para implementação de SO|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:**  Quando o site de nível superior de uma hierarquia atualiza para o System Center Configuration Manager, as imagens de arranque predefinidas são automaticamente atualizadas para imagens baseadas no Windows Assessment and Deployment Kit 10 (Windows ADK) de arranque. Utilize estas imagens de arranque apenas para implementações em clientes localizados em sites do System Center Configuration Manager. Para obter mais informações, consulte [planear a interoperabilidade de implementação do sistema operacional do](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Desde que novas versões do Configuration Manager não atualizem a versão do Windows ADK, que está a ser utilizado, não há sem qualquer efeito nas imagens de arranque.|  
|Novos passos de sequência de tarefas|Quando cria uma sequência de tarefas com um passo introduzido numa versão do Configuration Manager que não está disponível numa versão anterior, pode encontrar os seguintes problemas:<br /><br /> Ocorre um erro quando tenta editar a sequência de tarefas a partir de um site que está a executar uma versão anterior do Configuration Manager.<br /><br /> A sequência de tarefas não é executado num computador que executa uma versão anterior do cliente do Configuration Manager.|  
|Cliente para a comunicação de ponto de gestão de nível inferior|Um cliente de Configuration Manager que comunique com um ponto de gestão a partir de um site que executa uma versão inferior do cliente só pode utilizar a funcionalidade que suporta a versão de nível inferior do Configuration Manager. Por exemplo, se implementar conteúdo de um site do System Center Configuration Manager que foi atualizado recentemente para um cliente que comunica com um ponto de gestão que ainda não tenha atualizado para essa versão, esse cliente não é possível utilizar novas funcionalidades da versão mais recente versão.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperabilidade para a consola do Configuration Manager  
 A tabela seguinte contém informações sobre a utilização da consola do Configuration Manager num ambiente que tem uma combinação de versões do Configuration Manager.  


| Ambiente de interoperabilidade | Mais informações |
|------------------------------|------------------|
| Um ambiente com o System Center 2012 Configuration Manager e o System Center Configuration Manager | Para gerir um site do Configuration Manager, a consola e o site, que a consola liga ao tem de executar a mesma versão do Configuration Manager. Por exemplo, não é possível utilizar uma consola do System Center 2012 Configuration Manager para gerir um site do System Center Configuration Manager, ou vice versa.<br /><br /> Não é suportada para instalar a consola do System Center 2012 Configuration Manager e a consola do System Center Configuration Manager no mesmo computador.|
| Um ambiente com múltiplas versões do System Center Configuration Manager | System Center Configuration Manager não suporta a instalação de mais do que uma única consola do Configuration Manager num computador. Para utilizar várias consolas específicas diferentes versões do System Center Configuration Manager, instale as consolas diferentes em computadores separados.<br /><br /> Durante o processo de atualização de sites numa hierarquia para uma nova versão, pode ligar uma consola a um site que executa uma versão mais recente e ver informações sobre outros sites dessa hierarquia. No entanto, esta configuração não é recomendada. É possível que as diferenças entre a versão da consola e versão do site do Configuration Manager podem resultar em problemas de dados. Algumas funcionalidades que estão disponíveis na versão mais recente do produto não estarão disponíveis na consola do. <br /><br /> Não é suportada para gerir um site quando utiliza uma consola com uma versão que não corresponde à versão do site. Se o fizer, poderá causar perda de dados e coloca seu site em risco. Por exemplo, não é suportado para utilizar uma consola da versão 1610 para gerir um site que executa a versão 1606. |

