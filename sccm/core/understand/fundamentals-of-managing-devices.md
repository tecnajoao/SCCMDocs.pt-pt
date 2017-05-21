---
title: "Noções básicas de gestão de dispositivos | Documentos do Microsoft"
description: Saiba como utilizar o System Center Configuration Manager para gerir dispositivos.
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 45d84122a86da880268c93ecd994250df6b76c8a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Noções básicas sobre gestão de dispositivos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager pode gerir duas vastas categorias de dispositivos:

-   *Os clientes* são dispositivos como estações de trabalho, computadores portáteis, servidores e dispositivos móveis onde instalar o software de cliente do Configuration Manager. Algumas funções de gestão, como o inventário de hardware, requerem este software de cliente.  

-   *Dispositivos geridos* podem incluir *clientes*, mas normalmente é um dispositivo móvel quando não está instalado o software de cliente do Configuration Manager. Neste tipo de dispositivo, pode gere utilizando o Intune ou gestão de dispositivos móveis incorporada no local no Configuration Manager.

Pode também agrupar e identificar os dispositivos com base no utilizador, não apenas o tipo de cliente.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager

Existem duas formas de utilizar o software de cliente do Configuration Manager para gerir um dispositivo. É a primeira forma detetar o dispositivo na sua rede e, em seguida, implementar o software de cliente nesse dispositivo. A forma como deve instalar manualmente o software de cliente num novo computador e, em seguida, ter nesse computador aderirem ao seu site quando é associado a sua rede. Para detetar dispositivos onde não está instalado o software de cliente, execute um ou mais dos métodos de deteção incorporados. Depois de um dispositivo for detetado, utilize um dos vários métodos para instalar o software de cliente. Para informações sobre como utilizar a deteção, veja [Executar a deteção para o System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Após a detetar os dispositivos que são suportados para executar o software de cliente do Configuration Manager, pode utilizar um dos vários métodos para instalar o software. Depois de o software ser instalado e o cliente atribuído a um site primário, pode começar a gerir o dispositivo.  Métodos de instalação comuns incluem:

 - Instalação de push de cliente.

 - Instalação baseada em atualização de software.

 - Política de grupo.

 - Instalação manual num computador.
 - Incluindo o cliente como parte de uma imagem do sistema operativo que implementar.  


 Depois de o cliente ser instalado, é possível simplificar as tarefas de gestão de dispositivos através da utilização de coleções. As coleções são grupos de dispositivos ou utilizadores que criar para que possa geri-los como um grupo. Por exemplo, poderá querer instalar uma aplicação de dispositivo móvel em todos os dispositivos móveis que inscreve do Configuration Manager. Se for este o caso, pode utilizar a coleção todos os dispositivos móveis.  

 Para mais informações, consulte estes tópicos:  

-   [Escolha uma solução de gestão de dispositivos para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Métodos de instalação de cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introdução às coleções no System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Definições do cliente  
 Quando instalar o Configuration Manager pela primeira vez, todos os clientes na hierarquia são configurados utilizando as predefinições de cliente que podem ser alteradas. As definições de cliente incluem estas opções de configuração:

 -  Frequência os dispositivos comunicam com o site.

 -  Se o cliente está configurado para atualizações de software e outras operações de gestão.

 -  Se os utilizadores podem inscrever os respetivos dispositivos móveis para que estejam geridas pelo Configuration Manager.  

Pode criar definições personalizadas de cliente e, em seguida, atribuí-las a coleções.  Membros da coleção estão configurados para terem as definições personalizadas e pode criar personalizadas de cliente várias definições que são aplicadas pela ordem que especificou (por ordem numérica).  Se houver conflitos, a definição que tiver o menor número de ordem substitui as outras definições.  

O diagrama seguinte mostra um exemplo de como criar e aplicar definições de cliente personalizadas.  

 ![Definições do cliente](media/ClientSettings.gif)  

 Para obter mais informações sobre definições de cliente, consulte  
                [Como configurar definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager  
 O Configuration Manager suporta a gestão de alguns dispositivos que não instalou o software de cliente e não são geridos pelo Intune. Para obter mais informações, consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestão baseada no utilizador  
 O Configuration Manager suporta coleções de utilizadores do Active Directory Domain Services. Quando utiliza uma coleção de utilizadores, pode instalar software em todos os computadores que os membros a utilização de coleção. Certifique-se de que apenas instala o software que implementar nos dispositivos que são especificados como dispositivo primário do utilizador, configure a afinidade dispositivo / utilizador. Um utilizador pode ter um ou mais dispositivos primários.  

 Uma das formas que os utilizadores podem controlar a sua experiência de implementação de software consiste em utilizar o **Centro de Software** interface de cliente. O **Centro de Software** é instalado automaticamente nos computadores cliente e é executada a partir de **iniciar** menu. O **Centro de Software** permite aos utilizadores gerir o seu próprio software e efetuar as seguintes tarefas:  

-   Instale software.  

-   Agendar software para instalar automaticamente fora do horário de trabalho.  

-   Configure quando o Configuration Manager pode instalar software num dispositivo.  

-   Configure as definições de acesso para controlo remoto, se o controlo remoto está configurado no Configuration Manager.  

-   Configure opções de gestão de energia, se um administrador configura esta opção.  


 Uma ligação no **Centro de Software** permite que os utilizadores a estabelecer ligação com o **catálogo de aplicações**, onde podem procurar, instalar e solicitar software. O **catálogo de aplicações** também é utilizado para configurar as definições de preferência, apagar dispositivos móveis e, quando este estiver configurado, especifique um dispositivo primário para a afinidade dispositivo / utilizador.   

 Os utilizadores também podem aceder a **catálogo de aplicações** através de uma intranet do browser ou sessão de Internet.  

