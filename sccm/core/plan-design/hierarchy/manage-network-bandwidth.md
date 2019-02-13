---
title: Gerir a largura de banda de rede para o conteúdo
titleSuffix: Configuration Manager
description: Configure agendamento, limitação e conteúdo pré-configurado para o System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03d85a55e51125e40e1df766382b0a074d865a51
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141624"
---
# <a name="manage-network-bandwidth-for-content"></a>Gerir a largura de banda de rede para o conteúdo
Para ajudar a gerir a largura de banda de rede que é utilizada para o processo de gerenciamento de conteúdo do System Center Configuration Manager, pode utilizar os controles internos de agendamento e limitação. Também pode utilizar conteúdo pré-configurado. As secções seguintes descrevem estas opções mais detalhadamente.

##  <a name="BKMK_PlanningForThrottling"></a>Agendamento e limitação  

 Quando criar um pacote, altere o caminho de origem para o conteúdo ou atualizar o conteúdo no ponto de distribuição, os ficheiros são copiados do caminho de origem para a biblioteca de conteúdos no servidor do site. Em seguida, o conteúdo é copiado da biblioteca de conteúdos no servidor do site para a biblioteca de conteúdos nos pontos de distribuição. Quando os ficheiros de origem de conteúdo são atualizados e os ficheiros de origem já tenham sido distribuídos, o Configuration Manager obtém apenas os ficheiros novos ou atualizados e, em seguida, envia-os para o ponto de distribuição.

 Pode usar controles de agendamento e limitação para comunicação de site a site e para a comunicação entre um servidor de site e um ponto de distribuição remoto. Se a largura de banda de rede é limitada, até mesmo depois de configurar os controlos de agendamento e limitação, talvez deva considerar pré-configurar o conteúdo no ponto de distribuição.  

 No Configuration Manager, pode configurar uma agenda e especificar definições de limitação em pontos de distribuição remotos que determinam quando e como a distribuição de conteúdo é executada. Cada ponto de distribuição remoto pode ter diferentes configurações que o ajudam a limitações de largura de banda de rede do endereço do servidor do site para o ponto de distribuição remoto. Os controlos de agendamento e limitação para o ponto de distribuição remoto são semelhantes às definições para um endereço de remetente padrão. Neste caso, as definições são utilizadas por um novo componente chamado de Gestor de transferência.

 Gestor de transferência de pacotes distribui os conteúdos de um servidor do site, como um site primário ou site secundário, para um ponto de distribuição que está instalado num sistema de sites. As definições de limitação são especificadas no **limites de velocidade** separador e as definições de agendamento estão especificados no **agenda** guia, para um ponto de distribuição que não é um servidor de site. As definições de hora baseiam-se no fuso horário do site de envio, não é o ponto de distribuição.  

> [!IMPORTANT]  
>  O **limites de velocidade** e **agenda** separadores são apresentados apenas nas propriedades de pontos de distribuição que não estão instalados num servidor do site.  

Para obter mais informações, consulte [instalar e configurar pontos de distribuição para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="BKMK_PrestagingContent"></a>Conteúdo pré-configurado  
 Pode pré-configurar conteúdo para adicionar os ficheiros de conteúdo à biblioteca de conteúdos no ponto de servidor ou a distribuição de um site, antes de distribuir o conteúdo. Uma vez que os ficheiros de conteúdo já estão na biblioteca de conteúdos, não são transferidos através da rede quando distribuir o conteúdo. Pode pré-configurar ficheiros de conteúdo para aplicações e pacotes.  

Na consola do Configuration Manager, selecione o conteúdo que pretende pré-configurar e, em seguida, utilize o **criar Assistente de ficheiro de conteúdo pré-configurado**. Esta ação cria um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros e metadados associados para o conteúdo. Em seguida, pode importar manualmente o conteúdo num ponto de servidor ou a distribuição do site. Tenha em atenção os seguintes pontos:  

-   Quando importar o ficheiro de conteúdo pré-configurado num servidor do site, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no servidor do site e, em seguida, registados na base de dados de servidor do site.  

-   Quando importar o ficheiro de conteúdo pré-configurado num ponto de distribuição, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no ponto de distribuição. É enviada uma mensagem de estado para o servidor do site que informa o site que o conteúdo está disponível no ponto de distribuição.  

Opcionalmente, pode configurar o ponto de distribuição como **pré-configurado** para ajudar a gerir a distribuição de conteúdo. Em seguida, quando distribui conteúdo, pode escolher se pretende:  

-   Pré-configurar sempre o conteúdo no ponto de distribuição.  

-   Pré-configurar o conteúdo inicial para o pacote e, em seguida, utilize o processo de distribuição de conteúdo padrão, caso existam atualizações ao conteúdo.  

-   Utilize sempre o processo de distribuição de conteúdo padrão para o conteúdo do pacote.  

###  <a name="BKMK_DetermineToPrestageContent"></a>Determinar se deve pré-configurar conteúdo  
 Considere a pré-configuração conteúdo para aplicações e pacotes nos seguintes cenários:  

-   **Para resolver o problema de largura de banda de rede limitada do servidor do site para um ponto de distribuição.** Se o agendamento e limitação não são suficientes para satisfazer as suas preocupações em matéria de largura de banda, pondere a pré-configuração de conteúdo no ponto de distribuição. Cada ponto de distribuição tem o **ativar conteúdo pré-configurado para este ponto de distribuição** definição que pode escolher nas propriedades do ponto de distribuição. Quando ativa esta opção, o ponto de distribuição é identificado como um ponto de distribuição pré-configurado e pode escolher como gerir o conteúdo numa base por pacote.  

    As seguintes definições estão disponíveis nas propriedades de uma aplicação, pacote, pacote de controladores, imagem de arranque, instalador do sistema operativo e imagens. Estas definições permitem-lhe escolher como conteúdo de distribuição é gerida nos pontos de distribuição remotos que estão identificados como pré-configurados:  

    -   **Transferir o conteúdo automaticamente quando os pacotes são atribuídos aos pontos de distribuição**: Utilize esta opção quando tiver pacotes mais pequenos e as definições de agendamento e limitação fornecem controlo suficiente para distribuição de conteúdo.  

    -   **Transferir apenas alterações de conteúdo para o ponto de distribuição**: Utilize esta opção quando esperar atualizações futuras para o conteúdo do pacote sejam geralmente pequenas que o pacote inicial. Por exemplo, poderá pré-configurar uma aplicação como o Microsoft Office, porque o tamanho inicial do pacote é 700 MB e é demasiado grande para ser enviado através da rede. No entanto, as atualizações de conteúdo deste pacote podem ser inferior a 10 MB e são aceitáveis para distribuir através da rede. Outro exemplo poderá ser pacotes de controladores, onde o tamanho do pacote inicial elevado, mas adições incrementais de controladores para o pacote podem ser pequeno.  

    -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: Utilize esta opção se tiver pacotes volumosos que incluam conteúdos como um sistema operativo, e nunca deseja utilizar a rede para distribuir o conteúdo ao ponto de distribuição. Quando seleciona esta opção, tem de pré-configurar o conteúdo no ponto de distribuição.  

    > [!IMPORTANT]  
    >  As opções anteriores são aplicáveis numa base por pacote e só são utilizadas quando um ponto de distribuição é identificado como pré-configurado. Pontos de distribuição que não tenham sido identificados como pré-configurados ignoram estas definições. Neste caso, conteúdos serão sempre distribuídos através da rede do servidor do site para os pontos de distribuição.  

-   **Para restaurar a biblioteca de conteúdos num servidor do site.** Quando um servidor de site falha, informações sobre pacotes e aplicações que estão contidas na biblioteca de conteúdos são restauradas para a base de dados do site como parte do processo de restauro, mas os ficheiros de biblioteca de conteúdos não são restaurados como parte do processo. Se não tiver uma cópia de segurança do sistema de ficheiros para restaurar a biblioteca de conteúdos, pode criar um ficheiro de conteúdo pré-configurado a partir de outro site que contém os pacotes e aplicações que tem de ter. Em seguida, é possível extrair o ficheiro de conteúdo pré-configurado num servidor do site recuperado. Para obter mais informações sobre recuperação e cópia de segurança de servidor de site, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  
