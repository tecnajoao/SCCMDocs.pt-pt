---
title: 'Instalar funções para MDM no local '
titleSuffix: Configuration Manager
description: Instale funções de sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a24edacba97dcce91057e2403585a0843a4b212
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424430"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Instalar funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-locais a gestão de dispositivos móveis requer as seguintes funções de sistema de sites na sua infraestrutura de sites do Configuration Manager:  

- Ponto de inscrição  

- Ponto proxy de registo  

- Ponto de distribuição  

- Ponto de gestão de dispositivos  

- Ponto de ligação de serviço  

  Se estiver a adicionar no\-local gestão de dispositivos móveis à sua organização que tenha a maioria dos PCs e dispositivos geridos com o software de cliente do Configuration Manager, poderá ter a maioria das funções do sistema de sites já instaladas como parte de seu existente infraestrutura. Caso contrário, veja [adicionar funções do sistema de site para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) para obter informações completas sobre como adicioná-los ao seu site.  

> [!NOTE]  
>  Se utilizar réplicas de base de dados com a função de sistema de sites do ponto de gestão do dispositivo, os dispositivos inscritos recentemente inicialmente conseguirão ligar ao ponto de gestão de dispositivos até que a réplica de base de dados sincronize com o mesmo. Esta falha de ligação ocorre porque a réplica de base de dados não tem as informações sobre os dispositivos inscritos recentemente necessárias para uma ligação com êxito. As réplicas sincronizam a cada 5 minutos, para que os dispositivos não conseguirão estabelecer ligação durante os primeiro 5 minutos após a inscrição (normalmente, 2 tentativas de ligação), após o qual o dispositivo será ligado com êxito.  

 Se estiver a utilizar funções de sistema de sites existente ou adicionar novas, deve configurá-las para ser utilizado para gerir dispositivos modernos. Siga os passos abaixo para configurar o ponto de distribuição e ponto de gestão de dispositivos para funcionar corretamente na\-no local a gestão de dispositivos móveis:  

> [!NOTE]  
>  O current branch do Configuration Manager suporta apenas ligações de intranet de dispositivos para os pontos de distribuição e pontos de gestão de dispositivos para em\-no local a gestão de dispositivos móveis. No entanto, se também estiver a gerir computadores Mac OS X, esses clientes precisam de ligações de internet a essas funções de sistema de sites. Nesse caso, quando configurar as propriedades do ponto de distribuição e o ponto de gestão de dispositivos, deve utilizar o **permitir ligações de intranet e internet** em vez disso, a definição.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Para configurar funções de sistema de sites para gerir dispositivos modernos:  

1. Na consola do Configuration Manager, clique em **Administration** > **descrição geral** > **configuração do Site**  >   **Servidores e funções de sistema de sites**.  

2. Servidor de sistema de sites selecione com o ponto de distribuição ou ponto de gestão de dispositivos que pretende configurar, abra as propriedades para **sistema de sites** e certifique-se de que tem um FQDN especificado. Clique em **OK**.  

3. Abra as propriedades para a distribuição ponto de função do sistema de sites. Na guia Geral, certifique-se **HTTPS** está selecionado e selecione **permitir apenas ligações a intranet**.  

    Se estiver a gerir também separadamente computadores Mac com o cliente do Configuration Manager, utilize **permitir ligações de intranet e internet** em vez disso.  

   > [!NOTE]  
   >  Pontos de distribuição configurados para ligações de intranet precisam limites de site para ser configurado para eles. O current branch do Configuration Manager suporta apenas limites de intervalo de IPv4 para em\-no local a gestão de dispositivos móveis. Para obter mais informações sobre como configurar limites de site, consulte [definir limites de site e grupos de limites para o System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Clique na caixa de verificação junto a **permitir que os dispositivos móveis liguem a este ponto de distribuição**e, em seguida, clique em **OK**.  

5. Abra as propriedades para a gestão de função de sistema de sites do ponto. Na guia Geral, certifique-se **HTTPS** está selecionado e selecione **permitir apenas ligações a intranet**.  

    Se estiver a gerir também separadamente computadores Mac com o cliente do Configuration Manager, utilize **permitir ligações de intranet e internet** em vez disso.  

6. Clique na caixa de verificação junto a **permitir que dispositivos móveis e computadores Mac utilizem este ponto de gestão**. Clique em **OK**.  

    Esta opção transforma eficazmente o ponto de gestão para um ponto de gestão de dispositivos.  

   Depois das funções de sistema de sites foram adicionadas e configuradas para gerir dispositivos modernos, em seguida, tem de configurar os servidores que alojam as funções como pontos finais fidedignos para inscrever e comunicar com os dispositivos geridos. Ver [configurar certificados para comunicações fidedignas para a gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) para obter mais informações.  
