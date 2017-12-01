---
title: "Interoperabilidade entre versões"
titleSuffix: Configuration Manager
description: "Saiba como evitar conflitos entre várias hierarquias do System Center Configuration Manager na mesma rede."
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: "8"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 5b7b4c938ae057e7bcb7f281ddb266ade0cdafb4
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre diferentes versões do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar e operar, várias hierarquias independentes do System Center Configuration Manager, na mesma rede. No entanto, porque hierarquias diferentes do Configuration Manager não interagir fora do processo de migração, cada hierarquia necessita de configurações para impedir conflitos entre as mesmas. Além disso, pode criar determinadas configurações para ajudar a recursos que gere interagem com os sistemas de sites da hierarquia correta.  

 As secções seguintes fornecem informações sobre a utilização de diferentes versões do Configuration Manager na mesma rede:  

-   [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

-   [Interoperabilidade para a Consola do Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitações do Configuration Manager numa hierarquia com várias versões](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  
 Sites de diferentes versões não podem coexistir na mesma hierarquia, exceto durante o processo de atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager ou a partir de uma versão do System Center Configuration Manager para uma versão mais recente (utilizando as atualizações na consola).   

 Uma vez que pode implementar um site do System Center Configuration Manager e a hierarquia do lado do lado a lado com um site existente do System Center 2012 Configuration Manager ou a hierarquia, recomendamos que planeie impedir que os clientes de uma das versões tentem aderir um site a partir de outra versão.

Por exemplo, se duas ou mais hierarquias do Configuration Manager tiverem sobreposição de limites (consulte [sobreposição de limites](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)) que incluam as mesmas localizações de rede, é uma melhor prática para atribuir cada novo cliente a um site específico em vez de utilizar a atribuição automática de site. Para obter informações sobre a atribuição automática de site no System Center 2012 Configuration Manager, consulte [como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Além disso, não é possível instalar um cliente do System Center 2012 Configuration Manager num computador que aloje uma função de sistema de sites do System Center Configuration Manager, nem pode instalar um cliente do System Center Configuration Manager num computador que aloje uma função de sistema de site do System Center 2012 Configuration Manager.  

 Da mesma forma, os seguintes clientes e a seguinte ligação de rede privada Virtual (VPN) não são suportadas:  

-   Qualquer System Center 2012 Configuration Manager ou a versão anterior do cliente de computador  

-   Qualquer System Center 2012 Configuration Manager ou o cliente de gestão de dispositivos anterior  

-   Cliente de gestão de dispositivos para Windows CE Platform Builder (qualquer versão)  

-   Ligação VPN do System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre a atribuição de sites a clientes  
 Os clientes do System Center Configuration Manager podem ser atribuídos a um único site primário. Quando a atribuição automática de sites é utilizada para atribuir clientes a um site durante a instalação do cliente e mais do que um grupo de limites incluir o mesmo limite, tendo os grupos de limites diferentes sites atribuídos, não é possível prever a verdadeira atribuição de site de um cliente.  

 Se existir sobreposição de limites em vários sites do Configuration Manager e hierarquias, os clientes poderão não ser atribuídos ao site esperado ou poderão não ser atribuídos a um site de todo.  

 Os clientes do System Center Configuration Manager verificar a versão do site do Configuration Manager antes de concluir a atribuição de site e não pode ser atribuídos a uma versão anterior, quando e se existir sobreposição de limites de site. No entanto, as clientes do System Center 2012 Configuration Manager podem ser atribuídos incorretamente a um site do System Center Configuration Manager.  

 Para impedir que os clientes atribuição não intencional para o site incorreto quando duas hierarquias tiverem sobreposição de limites, recomendamos que configure parâmetros de instalação de cliente do Configuration Manager para atribuir clientes a um site específico.  

##  <a name="bkmk_mixed"></a>Limitações do Configuration Manager numa hierarquia com várias versões  
 Quando estiver no processo de atualização de um site do System Center Configuration Manager, existem vezes quando diversos sites serão têm versões diferentes. Por exemplo, poderá atualizar um site de administração central para uma nova versão mas, devido a janelas de manutenção do site, um ou mais sites primários podem não atualizar até uma hora e data posterior.  

 Quando diversos sites de uma única hierarquia executam versões diferentes, algumas funcionalidades não se encontram disponíveis. Isto pode afetar o modo como gere objetos do Configuration Manager na consola do Configuration Manager e que funcionalidades estão disponíveis para os clientes. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não está acessível em sites ou para clientes que executam uma versão inferior do service pack.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Limitações ao atualizar o Configuration Manager  

|Objeto|Detalhes|  
|------------|-------------|  
|Conta de acesso à rede|**Quando efetuar a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager:** Ao visualizar os detalhes de conta de acesso à rede de uma consola do Configuration Manager que está ligada a um site de administração central que foi atualizado para o System Center Configuration Manager, a consola não apresenta detalhes de contas configuradas num site primário que executa o System Center 2012 Configuration Manager. Depois de atualizar o site primário para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Ao visualizar os detalhes de conta de acesso à rede de uma consola do Configuration Manager que está ligada a um site de administração central que foi atualizado para uma nova versão do System Center Configuration Manager, a consola não apresenta detalhes de contas configuradas num site primário que executa uma versão anterior. Depois de atualizar o site primário para a mesma versão que o site de administração central, os detalhes da conta são visíveis na consola.|  
|Imagens de arranque para implementação de sistemas operativos|**Quando efetuar a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager:**  Quando o site de nível superior de uma hierarquia atualiza para o System Center Configuration Manager, as imagens de arranque predefinidas são automaticamente atualizadas para imagens com base no Windows Assessment and Deployment Kit 10 (Windows ADK) de arranque. Utilize estas imagens de arranque apenas para implementações em clientes localizados em sites do System Center Configuration Manager. Para obter mais informações, veja [Planear a interoperabilidade da implementação do sistema operativo no System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Desde que novas versões do cm6long não atualizem a versão do Windows ADK, que está a ser utilizado, há sem qualquer efeito nas imagens de arranque.|  
|Novos passos de sequência de tarefas|Quando cria uma sequência de tarefas com um passo introduzido numa versão do Configuration Manager que não está disponível numa versão anterior, podem ocorrer os seguintes problemas:<br /><br /> Ocorre um erro quando tenta editar a sequência de tarefas a partir de um site que está a executar uma versão anterior do Configuration Manager.<br /><br /> A sequência de tarefas não é executado num computador que executa uma versão anterior do cliente do Configuration Manager.|  
|Cliente para comunicações de ponto de gestão de nível inferior|Um cliente de Configuration Manager que comunica com um ponto de gestão a partir de um site que executa uma versão inferior do cliente só pode utilizar a funcionalidade que suporta a versão de nível inferior do Configuration Manager. Por exemplo, se implementar conteúdo de um site do System Center Configuration Manager que foi atualizado recentemente para um cliente que comunica com um ponto de gestão que ainda não atualizado para essa versão, esse cliente não é possível utilizar novas funcionalidades da versão mais recente.|  

##  <a name="BKMK_ConsoleInterop"></a>Interoperabilidade para a consola do Configuration Manager  
 A tabela seguinte contém informações sobre a utilização da consola do Configuration Manager num ambiente com várias versões do Configuration Manager.  

|Ambiente de interoperabilidade|Mais informações|  
|----------------------------------|----------------------|  
|Um ambiente com o System Center 2012 Configuration Manager e o System Center Configuration Manager|Para gerir um site do Configuration Manager, a consola e o site, que a consola liga tem de executar a mesma versão do Configuration Manager. Por exemplo, não é possível utilizar uma consola do System Center 2012 Configuration Manager para gerir um site do System Center Configuration Manager, ou vice versa.<br /><br /> Não é suportada para instalar a consola do System Center 2012 Configuration Manager e a consola do System Center Configuration Manager no mesmo computador.|  
|Um ambiente com múltiplas versões do System Center Configuration Manager|System Center Configuration Manager não suporta a instalação de mais do que uma única consola do Configuration Manager num computador. Para utilizar várias consolas específicas de versões diferentes do System Center Configuration Manager, tem de instalar as consolas diferentes em computadores separados.<br /><br /> Durante o processo de atualização de sites numa hierarquia para uma nova versão, pode ligar uma consola a um site que executa uma versão mais recente e visualizar informações sobre outros sites dessa hierarquia. No entanto, esta configuração não é recomendada, pois é possível que as diferenças entre a versão da consola e versão do site do Configuration Manager podem originar problemas de dados de e algumas funcionalidades que estão disponíveis na versão mais recente do produto não estarão disponíveis na consola do. <br /></br / > não é suportada para gerir um site quando utiliza uma consola com uma versão que não corresponde à versão do site. Se o fizer, poderá causar perda de dados e pode colocar o seu site em risco. Por exemplo, não é suportado para utilizar uma consola de versão 1610 para gerir um site que executa a versão 1606. |
