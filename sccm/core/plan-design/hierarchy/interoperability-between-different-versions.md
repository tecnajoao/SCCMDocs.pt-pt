---
title: "Interoperabilidade entre versões do Configuration Manager | Documentos do Microsoft"
description: "Saiba como evitar conflitos entre várias hierarquias do System Center Configuration Manager na mesma rede."
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 28593d271603ff9775425327996d844d7ed358cd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre diferentes versões do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar e operar, várias hierarquias independentes do System Center Configuration Manager, na mesma rede. No entanto, uma vez que hierarquias diferentes do Configuration Manager não interagem fora do processo de migração, cada hierarquia necessita de configurações para impedir conflitos entre as mesmas. Além disso, pode criar determinadas configurações para ajudar os recursos que gere interagem com os sistemas de sites da hierarquia correta.  

 As secções seguintes fornecem informações sobre a utilização de diferentes versões do Configuration Manager na mesma rede:  

-   [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

-   [Interoperabilidade para a Consola do Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitações do Configuration Manager numa hierarquia com várias versões](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  
 Sites de diferentes versões não podem coexistir na mesma hierarquia, exceto durante o processo de atualização do System Center 2012 Configuration Manager para System Center Configuration Manager ou a partir de uma versão do System Center Configuration Manager para uma versão mais recente (utilizando as atualizações na consola).   

 Uma vez que pode implementar um site do System Center Configuration Manager e da hierarquia lado-a-lado com um site existente do System Center 2012 Configuration Manager ou uma hierarquia, recomendamos que planeie impedir que os clientes a partir de qualquer uma das versões tentem aderir um site a partir de outra versão.

Por exemplo, se duas ou mais hierarquias do Configuration Manager tiverem sobreposição de limites (consulte [sobreposição de limites](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)) que incluam as mesmas localizações de rede, é recomendado atribuir cada novo cliente a um site específico em vez de utilizar a atribuição automática de site. Para obter informações sobre a atribuição automática de sites no System Center 2012 Configuration Manager, consulte o artigo [como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Além disso, não é possível instalar um cliente a partir do System Center 2012 Configuration Manager num computador que aloje uma função de sistema de sites a partir do System Center Configuration Manager, nem pode instalar um cliente do System Center Configuration Manager num computador que aloje uma função de sistema de sites a partir do System Center 2012 Configuration Manager.  

 Da mesma forma, os seguintes clientes e a seguinte ligação de rede privada Virtual (VPN) não são suportadas:  

-   Qualquer System Center 2012 Configuration Manager ou a versão de cliente do computador anterior  

-   Qualquer System Center 2012 Configuration Manager ou o cliente de gestão de dispositivos anterior  

-   Cliente de gestão de dispositivos para Windows CE Platform Builder (qualquer versão)  

-   Ligação VPN do System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre a atribuição de sites a clientes  
 Os clientes do System Center Configuration Manager podem ser atribuídos a apenas um único site primário. Quando a atribuição automática de sites é utilizada para atribuir clientes a um site durante a instalação do cliente e mais do que um grupo de limites incluir o mesmo limite, tendo os grupos de limites diferentes sites atribuídos, não é possível prever a verdadeira atribuição de site de um cliente.  

 Se existir sobreposição de limites em vários sites do Configuration Manager e hierarquias, os clientes poderão não ser atribuídos ao site esperado ou poderão não ser atribuídos a um site em qualquer altura.  

 Os clientes do Configuration Manager do System Center verificam a versão do site do Configuration Manager antes de concluírem a atribuição de site e não podem ser atribuídos a uma versão anterior quando e se existir sobreposição de limites de site. No entanto, os clientes do System Center 2012 Configuration Manager incorretamente podem ser atribuídos a um site do System Center Configuration Manager.  

 Para impedir que os clientes intencional ao site errado quando duas hierarquias tiverem sobreposição de limites, recomendamos que configure parâmetros de instalação de cliente do Configuration Manager para atribuir clientes a um site específico.  

##  <a name="bkmk_mixed"></a>Limitações do Configuration Manager numa hierarquia com várias versões  
 Quando estiver a atualizar um site do System Center Configuration Manager, há horas quando diversos sites irão ter versões diferentes. Por exemplo, poderá atualizar um site de administração central para uma nova versão mas, devido a janelas de manutenção do site, um ou mais sites primários podem não atualizar até uma hora e data posterior.  

 Quando diversos sites de uma única hierarquia executam versões diferentes, algumas funcionalidades não se encontram disponíveis. Isto pode afetar o modo como gere objetos do Configuration Manager na consola do Configuration Manager e a funcionalidade está disponível para clientes. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não está acessível nos sites ou para os clientes que executem uma versão de service pack inferior.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Limitações ao atualizar o Configuration Manager  

|Objeto|Detalhes|  
|------------|-------------|  
|Conta de acesso à rede|**Ao atualizar a partir do System Center 2012 Configuration Manager para System Center Configuration Manager:** Quando visualiza detalhes de conta de acesso à rede a partir de uma consola do Configuration Manager que está ligado a um site de administração central que atualizou para o System Center Configuration Manager, a consola não apresenta detalhes para contas que estão configuradas num site primário que executa o System Center 2012 Configuration Manager. Depois do site primário é atualizado para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Quando visualiza detalhes de conta de acesso à rede a partir de uma consola do Configuration Manager que está ligado a um site de administração central que tenha atualizado para uma nova versão do System Center Configuration Manager, a consola não apresenta detalhes para contas que estão configuradas num site primário que executa uma versão anterior. Depois do site primário é atualizado para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.|  
|Imagens de arranque para implementação de sistemas operativos|**Ao atualizar a partir do System Center 2012 Configuration Manager para System Center Configuration Manager:**  Quando o site de nível superior de uma hierarquia de atualização para o System Center Configuration Manager, as imagens de arranque predefinidas são automaticamente atualizadas para imagens com base no Windows Assessment and 10 de Kit de implementação (Windows ADK) de arranque. Utilize estas imagens de arranque apenas para implementações em clientes localizados em sites do Configuration Manager do System Center. Para obter mais informações, veja [Planear a interoperabilidade da implementação do sistema operativo no System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Desde que as novas versões de cm6long não atualizar a versão do Windows ADK, que está a ser utilizado, não existe não terá qualquer efeito nas imagens de arranque.|  
|Novos passos de sequência de tarefas|Quando criar uma sequência de tarefas com um passo introduzido na versão do Configuration Manager que não está disponível numa versão anterior, pode deparar-os seguintes problemas:<br /><br /> -Um erro ocorre quando tenta editar a sequência de tarefas a partir de um site que está a executar uma versão anterior do Configuration Manager.<br /><br /> -A sequência de tarefas não é executado num computador que executa uma versão anterior do cliente do Configuration Manager.|  
|Comunicações de ponto de gestão de nível de cliente para|Um cliente do Configuration Manager que comunica com um ponto de gestão a partir de um site que executa uma versão inferior do cliente só pode utilizar a funcionalidade que suporta a versão anterior do Configuration Manager. Por exemplo, se implementar conteúdo de um site do System Center Configuration Manager que foi atualizado recentemente a um cliente que comunica com um ponto de gestão que não tenha sido atualizado para essa versão, esse cliente não é possível utilizar novas funcionalidades da versão mais recente.|  

##  <a name="BKMK_ConsoleInterop"></a>Interoperabilidade para a consola do Configuration Manager  
 A tabela seguinte contém informações sobre a utilização da consola do Configuration Manager num ambiente que tem uma mistura de versões do Configuration Manager.  

|Ambiente de interoperabilidade|Mais informações|  
|----------------------------------|----------------------|  
|Um ambiente com o System Center 2012 Configuration Manager e System Center Configuration Manager|Para gerir um site do Configuration Manager, a consola e o site que a consola liga tem de executar a mesma versão do Configuration Manager. Por exemplo, não é possível utilizar uma consola do System Center 2012 Configuration Manager para gerir um site do System Center Configuration Manager, ou vice versa.<br /><br /> Não é suportada para instalar a consola do System Center 2012 Configuration Manager e a consola do System Center Configuration Manager no mesmo computador.|  
|Um ambiente com múltiplas versões do System Center Configuration Manager|System Center Configuration Manager não suporta a instalação de mais do que uma única consola do Configuration Manager num computador. Para utilizar várias consolas específicas de versões diferentes do System Center Configuration Manager, tem de instalar as consolas diferentes em computadores separados.<br /><br /> Durante o processo de atualização de sites numa hierarquia para uma nova versão, pode ligar uma consola a um site que executa uma versão mais recente e ver informações sobre outros sites dessa hierarquia. No entanto, esta configuração não é recomendada, é possível que as diferenças entre a versão da consola e versão do site do Configuration Manager podem resultar em problemas de dados, e algumas funcionalidades que estão disponíveis na versão mais recente do produto não estarão disponíveis na consola. <br /></br / > não é suportada para gerir um site ao utilizar uma consola com uma versão que não corresponde a versão do site. Se o fizer, poderá provocar perda de dados e pode colocar o seu site em risco. Por exemplo, não é suportada para utilizar uma consola a partir da versão 1610 para gerir um site que executa versão 1606. |

