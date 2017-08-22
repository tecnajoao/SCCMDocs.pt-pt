---
title: "Gerir a largura de banda de rede para o conteúdo | Microsoft Docs"
description: "Configure o agendamento, limitação e conteúdo pré-configurado para o System Center Configuration Manager."
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d9dff97126c34a726677de60dd7647370c553b6e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-network-bandwidth-for-content"></a>Gerir a largura de banda de rede para o conteúdo
Para ajudar a gerir a largura de banda de rede que é utilizada para o processo de gestão de conteúdos do System Center Configuration Manager, pode utilizar os controlos incorporados para agendamento e limitação. Também pode utilizar conteúdo pré-configurado. As secções seguintes descrevem estas opções em mais detalhe.

##  <a name="BKMK_PlanningForThrottling"></a>Agendamento e limitação  

 Quando criar um pacote, altere o caminho de origem para o conteúdo ou atualizar o conteúdo no ponto de distribuição, os ficheiros são copiados do caminho de origem para a biblioteca de conteúdos no servidor do site. Em seguida, o conteúdo é copiado da biblioteca de conteúdos no servidor do site para a biblioteca de conteúdos nos pontos de distribuição. Quando são atualizados ficheiros de origem de conteúdo e os ficheiros de origem que já tenham sido distribuídos, o Configuration Manager obtém apenas os ficheiros novos ou atualizados e, em seguida, envia-os para o ponto de distribuição.

 Pode utilizar os controlos de agendamento e limitação para comunicação site a site e para a comunicação entre o servidor do site e um ponto de distribuição remoto. Se a largura de banda de rede é limitada, mesmo depois de configurar os controlos de agendamento e limitação, talvez deva considerar pré-configurar o conteúdo no ponto de distribuição.  

 No Configuration Manager, pode configurar uma agenda e especificar definições de limitação nos pontos de distribuição remotos que determinam quando e como é efetuada a distribuição de conteúdo. Cada ponto de distribuição remoto pode ter diferentes configurações que ajudam a limitações de largura de banda de rede do endereço do servidor do site para ponto de distribuição remoto. Os controlos de agendamento e limitação para o ponto de distribuição remoto são semelhantes às definições para um endereço de remetente padrão. Neste caso, as definições são utilizadas por um novo componente designado Gestor de transferência do pacote.

 Gestor de transferência de pacotes distribui os conteúdos de um servidor de site, como um site primário ou site secundário, a um ponto de distribuição que está instalado num sistema de sites. As definições de limitação são especificadas no **limites de velocidade** são especificados no separador e as definições de agendamento de **agenda** separador, para um ponto de distribuição que não é um servidor de site. As definições de hora baseiam-se no fuso horário do site de envio, não o ponto de distribuição.  

> [!IMPORTANT]  
>  O **limites de velocidade** e **agenda** separadores são apresentados apenas nas propriedades dos pontos de distribuição que não estejam instalados num servidor do site.  

Para obter mais informações, consulte [instalar e configurar pontos de distribuição para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="BKMK_PrestagingContent"></a>Conteúdo pré-configurado  
 Pode pré-configurar conteúdo para adicionar os ficheiros de conteúdo à biblioteca de conteúdos no ponto de servidor ou a distribuição de um site, antes de distribuir o conteúdo. Porque os ficheiros de conteúdo já estão na biblioteca de conteúdos, não são transferidos através da rede quando distribuir o conteúdo. Pode pré-configurar ficheiros de conteúdo para aplicações e pacotes.  

Na consola do Configuration Manager, selecione o conteúdo que pretende pré-configurar e, em seguida, utilize o **criar Assistente de ficheiro de conteúdo pré-configurado**. Esta ação cria um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros e metadados associados para o conteúdo. Em seguida, pode importar manualmente o conteúdo num ponto de servidor ou a distribuição do site. Tenha em atenção os seguintes pontos:  

-   Quando importar o ficheiro de conteúdo pré-configurado num servidor do site, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no servidor do site e, em seguida, registados na base de dados do servidor do site.  

-   Quando importar o ficheiro de conteúdo pré-configurado num ponto de distribuição, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no ponto de distribuição. É enviada uma mensagem de estado para o servidor de site que informa o site que o conteúdo está disponível no ponto de distribuição.  

Opcionalmente, pode configurar o ponto de distribuição como **pré-configurado** para ajudar a gerir a distribuição de conteúdo. Em seguida, quando distribui conteúdo, pode escolher se pretende:  

-   Pré-configurar sempre o conteúdo no ponto de distribuição.  

-   Pré-configurar o conteúdo inicial para o pacote e, em seguida, utilize o processo de distribuição de conteúdo padrão quando existem atualizações ao conteúdo.  

-   Utilize sempre o processo de distribuição de conteúdo padrão para o conteúdo do pacote.  

###  <a name="BKMK_DetermineToPrestageContent"></a>Determinar se deve pré-configurar conteúdo  
 Pondere a pré-configuração conteúdo para aplicações e pacotes nos seguintes cenários:  

-   **Para resolver o problema de largura de banda de rede limitada do servidor do site para um ponto de distribuição.** Se o agendamento e limitação não são suficientes para satisfazer as suas preocupações em largura de banda, pondere a pré-configuração de conteúdo no ponto de distribuição. Cada ponto de distribuição tem a **ativar conteúdo pré-configurado para este ponto de distribuição** definição que pode escolher nas propriedades do ponto de distribuição. Quando ativa esta opção, o ponto de distribuição é identificado como um ponto de distribuição pré-configurado e pode escolher como gerir o conteúdo numa base por pacote.  

    As seguintes definições estão disponíveis nas propriedades de uma aplicação, pacote, pacote de controladores, imagem de arranque, instalador do sistema operativo e imagens. Estas definições permitem-lhe escolher como conteúdo de distribuição é gerida nos pontos de distribuição remotos que estão identificados como pré-configurados:  

    -   **Transferir o conteúdo automaticamente quando os pacotes são atribuídos aos pontos de distribuição**: Utilize esta opção se tiver pacotes mais pequenos, e as definições de agendamento e limitação controlo suficiente para distribuição de conteúdo.  

    -   **Transferir apenas alterações de conteúdo para o ponto de distribuição**: Utilize esta opção se prevê que as futuras atualizações dos conteúdos do pacote sejam geralmente pequenas que o pacote inicial. Por exemplo, poderá pré-configurar uma aplicação como o Microsoft Office, porque o tamanho do pacote inicial é superior a 700 MB e é demasiado grande para ser enviado através da rede. No entanto, as atualizações de conteúdo para este pacote podem ser inferior a 10 MB e são aceitáveis para distribuir através da rede. Noutro exemplo, poderá ser pacotes de controladores, onde o tamanho inicial do pacote é grande, mas adições incrementais de controladores ao pacote sejam pequenas.  

    -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: Utilize esta opção se tiver pacotes volumosos conteúdos como um sistema operativo, e nunca pretende utilizar a rede para distribuir o conteúdo ao ponto de distribuição. Quando seleciona esta opção, terá de pré-configurar o conteúdo no ponto de distribuição.  

    > [!IMPORTANT]  
    >  As opções anteriores são aplicáveis numa base por pacote e só são utilizadas quando um ponto de distribuição é identificado como pré-configurado. Pontos de distribuição que não tenham sido identificados como pré-configurados ignoram estas definições. Neste caso, conteúdo serão sempre distribuído através da rede do servidor do site para os pontos de distribuição.  

-   **Para restaurar a biblioteca de conteúdos num servidor do site.** Quando um servidor de site falha, informações sobre pacotes e aplicações que estão contidas na biblioteca de conteúdos são restauradas para a base de dados do site como parte do processo de restauro, mas os ficheiros de biblioteca de conteúdos não são restaurados como parte do processo. Se não tiver uma cópia de segurança do sistema de ficheiros para restaurar a biblioteca de conteúdos, pode criar um ficheiro de conteúdo pré-configurado a partir de outro site que contém os pacotes e aplicações que tem de ter. Pode, em seguida, extraia o ficheiro de conteúdo pré-configurado num servidor do site recuperado. Para obter mais informações sobre a recuperação e cópia de segurança de servidor de site, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  
