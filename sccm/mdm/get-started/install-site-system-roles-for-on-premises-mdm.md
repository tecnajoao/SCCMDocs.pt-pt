---
title: "Instalar funções de MDM no local - Configuration Manager | Documentos do Microsoft"
description: "Instale funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
caps.latest.revision: 9
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4913606e2f8a36e0004f711b24ecd836d0485124
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Instalar funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-local gestão de dispositivos móveis requer as seguintes funções de sistema de sites na sua infraestrutura de sites do Configuration Manager:  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de distribuição  

-   Ponto de gestão de dispositivos  

-   Ponto de ligação de serviço  

 Se estiver a adicionar na\-local gestão de dispositivos móveis para a sua organização que tem a maioria dos PCs e dispositivos geridos utilizando o software de cliente do Configuration Manager, poderá ter da maioria das funções de sistema de sites já instaladas como parte da sua infraestrutura existente. Se não estiver, consulte o artigo [adicionar funções do sistema de sites para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) para obter informações completas sobre como adicioná-los ao seu site.  

> [!NOTE]  
>  Se utilizar réplicas de base de dados com a função de sistema de sites do ponto de gestão do dispositivo, os dispositivos inscritos recentemente inicialmente conseguirão ligar ao ponto de gestão de dispositivo até que a réplica de base de dados sincroniza com o mesmo. Esta falha de ligação ocorre porque a réplica de base de dados não tem as informações sobre os dispositivos inscritos recentemente necessárias para uma ligação com êxito. Réplicas sincronizam a cada 5 minutos, para que os dispositivos irão falhar ligar para os primeiro 5 minutos depois da inscrição (2, normalmente, as tentativas de ligação), após o qual o dispositivo irá ligar-se com êxito.  

 Se estiver a utilizar funções de sistema de sites existente ou adicionar novas, deve configurá-los para ser utilizado para gerir dispositivos modernos. Siga os passos abaixo para configurar o ponto de distribuição e o ponto de gestão de dispositivos para funcionar corretamente para\-local gestão de dispositivos móveis:  

> [!NOTE]  
>  O ramo atual do Configuration Manager só suporta ligações de intranet a partir de dispositivos para os pontos de distribuição e pontos de gestão de dispositivos para\-local gestão de dispositivos móveis. No entanto, se também estiver a gerir computadores Mac OS X, esses clientes necessitam de ligações de internet a essas funções de sistema de sites. Nesse caso, quando configura as propriedades do ponto de distribuição e o ponto de gestão de dispositivos, deve utilizar o **permitir ligações a intranet e internet** em vez disso, a definição.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Para configurar funções de sistema de sites para gerir dispositivos modernos:  

1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**.  

2.  Servidor de sistema de sites selecione com o ponto de distribuição ou ponto de gestão de dispositivos que pretende configurar, abra as propriedades de **sistema de sites** e certifique-se de que tem um FQDN especificado. Clique em **OK**.  

3.  Abrir propriedades para a distribuição do ponto de função do sistema de sites. No separador Geral, certifique-se **HTTPS** está selecionado e selecione **permitir ligações apenas de intranet**.  

     Se também separadamente que está a gerir computadores Mac com o cliente do Configuration Manager, utilize **permitir ligações a intranet e internet** em vez disso.  

    > [!NOTE]  
    >  Pontos de distribuição configurados para ligações de intranet requerem limites do site seja configurado para os mesmos. O ramo atual do Configuration Manager só suporta limites de intervalo IPv4 para\-local gestão de dispositivos móveis. Para obter mais informações sobre como configurar limites de sites, consulte o artigo [definir limites de site e os grupos de limites para o System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4.  Clique na caixa de verificação junto a **permitir que os dispositivos móveis ligar a este ponto de distribuição**e, em seguida, clique em **OK**.  

5.  Abrir propriedades para a gestão do ponto de função do sistema de sites. No separador Geral, certifique-se **HTTPS** está selecionado e selecione **permitir ligações apenas de intranet**.  

     Se também separadamente que está a gerir computadores Mac com o cliente do Configuration Manager, utilize **permitir ligações a intranet e internet** em vez disso.  

6.  Clique na caixa de verificação junto a **permitir dispositivos móveis e computadores Mac utilizem este ponto de gestão**. Clique em **OK**.  

     Esta opção eficazmente o ponto de gestão para um ponto de gestão de dispositivos.  

 Depois das funções de sistema de sites tenham sido adicionadas e configuradas para gerir dispositivos modernos, em seguida, terá de configurar os servidores que alojam as funções como pontos finais fidedignos para inscrição e comunicar com os dispositivos geridos. Consulte o artigo [configurar certificados para comunicações de fidedignas para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) para obter mais informações.  

