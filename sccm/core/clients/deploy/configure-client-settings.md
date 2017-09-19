---
title: "Configurar definições de cliente | Microsoft Docs"
description: "Selecione as definições de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: "5"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 0722ecbe96e979966203c2cef9047a3adfdae46e
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Como configurar as definições de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode gerir todas as definições do cliente no System Center Configuration Manager, do **administração** > **as definições de cliente**. Modifique as predefinições quando pretender configurar definições para todos os utilizadores e dispositivos da hierarquia que não têm definições personalizadas aplicadas. Se pretender aplicar definições diferentes apenas nalguns utilizadores ou dispositivos, crie definições personalizadas e implemente-as nas coleções.  

Para obter informações sobre cada definição do cliente, consulte [sobre definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Também pode utilizar itens de configuração a fim de gerir os clientes para avaliar, controlar e retificar a compatibilidade de configuração dos dispositivos. Para obter mais informações, consulte [garantir a compatibilidade do dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configurar as predefinições de cliente    

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

3.  No **home page** separador, escolha **propriedades**.  

4.  Veja e configure as definições do cliente de cada grupo de definições do painel de navegação.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção da política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) no [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Criar e implementar definições personalizadas de cliente  
Quando implementar estas definições personalizadas, elas substituirão as predefinições do cliente. Antes de iniciar este procedimento, certifique-se de que tem uma coleção com os utilizadores ou dispositivos que necessitam destas definições personalizadas de cliente.  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente**.  

3.  No **home page** separador o **criar** grupo, escolha **criar definições personalizadas do cliente**e, em seguida, escolha o:  

    -   **Criar Definições Personalizadas do Dispositivo Cliente**  

    -   **Criar Definições Personalizadas do Utilizador Cliente**  

4.  Especifique uma descrição exclusiva de nome e a opção.  

5.  Selecione um ou mais das caixas de verificação que apresentem um grupo de definições.  

6.  Escolha a cada grupo de definições no painel de navegação e configurar as definições disponíveis, em seguida, clique em **OK**.   

8.  Selecione a definição que criou de cliente personalizado. No **home page** separador o **as definições de cliente** grupo, escolha **implementar**.  

9. No **selecionar coleção** , seleccione a colecção apropriada e, em seguida, escolha **OK**. Pode verificar a coleção selecionada clicando no separador **Implementações** do painel de detalhes.  

10. Veja a ordem da definição personalizada do cliente que acabou de criar. Quando tem várias definições personalizadas de cliente, estas são aplicadas de acordo com o seu número de ordem. Se existirem conflitos, a definição que tiver o menor número de ordem substitui as outras definições. Para alterar o número de ordem, no **home page** separador o **as definições de cliente** grupo, escolha **Mover Item para cima** ou **Mover Item para baixo**.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção da política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) no [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="view-client-settings"></a>Ver definições de cliente  
 Quando tiverem sido implementadas várias definições do cliente no mesmo dispositivo, utilizador ou grupo de utilizadores, a atribuição de prioridades e a combinação de definições podem ser complexas. Para ver as definições de cliente:  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos** > **utilizadores** ou **coleções de utilizadores**.  

3.  Selecione um dispositivo, um utilizador ou um grupo de utilizadores e, no grupo **Definições do Cliente** , selecione **Definições de Cliente Resultantes**.  

4.  Selecione uma definição no painel esquerdo do cliente e as definições são apresentadas. Nesta vista, as definições são só de leitura. 

    > [!NOTE]  
    >  Para ver as definições de cliente, tem de ter acesso de leitura para as definições de cliente.  

    