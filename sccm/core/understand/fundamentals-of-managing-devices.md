---
title: Noções básicas de gestão de dispositivos
titleSuffix: Configuration Manager
description: Saiba como utilizar o System Center Configuration Manager para gerir dispositivos.
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d5fe709f403676c36d77e23e3ebe40a66101a44
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Noções básicas sobre gestão de dispositivos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager pode gerir duas categorias amplas de dispositivos:

-   *Os clientes* são dispositivos como estações de trabalho, computadores portáteis, servidores e dispositivos móveis em que instalar o software de cliente do Configuration Manager. Algumas funções de gestão, como o inventário de hardware, requerem este software de cliente.  

-   *Dispositivos geridos* podem incluir *clientes*, mas normalmente é um dispositivo móvel em que o software de cliente do Configuration Manager não está instalado. Neste tipo de dispositivo, gerir utilizando o Intune ou a gestão de dispositivos móveis incorporada no local no Configuration Manager.

Também pode agrupar e identificar os dispositivos com base no utilizador, não apenas o tipo de cliente.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager

Existem duas formas de utilizar o software de cliente do Configuration Manager para gerir um dispositivo. É a primeira forma para detetar o dispositivo na sua rede e, em seguida, implementar o software de cliente nesse dispositivo. A outra forma consiste em instalar manualmente o software de cliente num novo computador e, em seguida, ter nesse computador associe ao seu site quando é associado a sua rede. Para detetar dispositivos em que o software de cliente não está instalado, execute um ou mais dos métodos de deteção incorporados. Depois de um dispositivo for detetado, utilize um dos vários métodos para instalar o software de cliente. Para informações sobre como utilizar a deteção, veja [Executar a deteção para o System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Depois de descobrir os dispositivos que são suportados para executar o software de cliente do Configuration Manager, pode utilizar um dos vários métodos para instalar o software. Depois de o software ser instalado e o cliente atribuído a um site primário, pode começar a gerir o dispositivo.  Métodos de instalação comuns incluem:

 - Instalação de push de cliente.

 - Instalação baseada em atualização de software.

 - Política de grupo.

 - Instalação manual num computador.
 - Incluindo o cliente como parte de uma imagem do sistema operativo que implementar.  


 Depois de o cliente ser instalado, é possível simplificar as tarefas de gestão de dispositivos através da utilização de coleções. As coleções são grupos de dispositivos ou utilizadores que criar para que possa geri-los como um grupo. Por exemplo, pode querer instalar uma aplicação de dispositivo móvel em todos os dispositivos móveis que inscreve do Configuration Manager. Se for este o caso, pode utilizar a coleção de todos os dispositivos móveis.  

 Para obter mais informações, consulte estes tópicos:  

-   [Escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Métodos de instalação de cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introdução às coleções no System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Definições do cliente  
 Quando instalar o Configuration Manager pela primeira vez, todos os clientes na hierarquia são configurados através da utilização de predefinições de cliente que podem ser alteradas. As definições de cliente incluem estas opções de configuração:

 -  Frequência com os dispositivos comunicam com o site.

 -  Indica se o cliente está definido para atualizações de software e outras operações de gestão.

 -  Se os utilizadores podem inscrever os respetivos dispositivos móveis, por isso, se estiver a geridos pelo Configuration Manager.  

Pode criar definições personalizadas de cliente e, em seguida, atribuí-las a coleções.  Membros da coleção estão configurados para terem as definições personalizadas e vários personalizadas de cliente pode criar as definições que são aplicadas pela ordem que especificar (por ordem numérica).  Se houver conflitos, a definição que tiver o menor número de ordem substitui as outras definições.  

O diagrama seguinte mostra um exemplo de como criar e aplicar definições de cliente personalizadas.  

 ![Definições do cliente](media/ClientSettings.gif)  

 Para obter mais informações sobre definições de cliente, consulte  
                [Como configurar definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) e [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager  
 O Configuration Manager suporta a gestão de alguns dispositivos que não instalou o software de cliente e não são geridos pelo Intune. Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) e [gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestão baseada no utilizador  
 O Configuration Manager suporta coleções de utilizadores do Active Directory Domain Services. Quando utiliza uma coleção de utilizadores, pode instalar software em todos os computadores que os membros a utilização de coleção. Para se certificar de que só instala o software que implementar nos dispositivos que são especificados como dispositivo primário do utilizador, configure a afinidade dispositivo / utilizador. Um utilizador pode ter um ou mais dispositivos primários.  

 Uma das formas em que os utilizadores podem controlar a sua experiência de implementação de software consiste em utilizar o **Centro de Software** interface do cliente. O **Centro de Software** é instalado automaticamente nos computadores cliente e é executada a partir de **iniciar** menu. O **Centro de Software** permite aos utilizadores gerir o seu próprio software e efetuar as seguintes tarefas:  

-   Instale software.  

-   Agendar software para instalar automaticamente fora das horas de trabalho.  

-   Configure quando o Configuration Manager pode instalar software num dispositivo.  

-   Configure as definições de acesso para controlo remoto, se o controlo remoto está configurado no Configuration Manager.  

-   Configure opções para gestão de energia, se um administrador configura esta opção.  


 Uma ligação no **Centro de Software** permite aos utilizadores ligar para o **catálogo de aplicações**, onde podem procurar, instalar e solicitar software. O **catálogo de aplicações** também é utilizado para configurar as definições de preferência, apagar dispositivos móveis e, quando for definida, especifique um dispositivo primário para a afinidade dispositivo / utilizador.   

 Os utilizadores também podem aceder a **catálogo de aplicações** através de uma intranet de browser ou a sessão de Internet.  
