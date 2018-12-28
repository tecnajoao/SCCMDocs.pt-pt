---
title: Configurar definições de cliente
titleSuffix: Configuration Manager
description: Selecione as definições de cliente no System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03485b4be2295676d125f3f3e28d2cd7d62728d3
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420061"
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Como configurar as definições de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gere todas as definições de cliente no System Center Configuration Manager, do **Administration** > **definições de cliente**. Modifique as predefinições quando pretender configurar definições para todos os utilizadores e dispositivos da hierarquia que não têm definições personalizadas aplicadas. Se pretender aplicar definições diferentes apenas nalguns utilizadores ou dispositivos, crie definições personalizadas e implementar em coleções.  

Para obter informações sobre cada definição de cliente, consulte [sobre as definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Também pode utilizar itens de configuração a fim de gerir os clientes para avaliar, controlar e retificar a compatibilidade de configuração dos dispositivos. Para obter mais informações, consulte [garantir a conformidade de dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configurar as predefinições de cliente    

1. Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

2. Sobre o **home page** separador, escolha **propriedades**.  

3. Veja e configure as definições do cliente de cada grupo de definições do painel de navegação.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) na [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Criar e implementar definições personalizadas de cliente  
Quando implementar estas definições personalizadas, elas substituirão as predefinições do cliente. Antes de iniciar este procedimento, certifique-se de que tem uma coleção com os utilizadores ou dispositivos que necessitam destas definições personalizadas de cliente.  

1. Na consola do Configuration Manager, escolha **Administration** > **definições de cliente**.  

2. Sobre o **home page** separador a **criar** de grupo, escolha **criar definições personalizadas do cliente**e, em seguida, escolha o:  

   -   **Criar Definições Personalizadas do Dispositivo Cliente**  

   -   **Criar Definições Personalizadas do Utilizador Cliente**  

3. Especifique uma descrição de nome e a opção exclusiva.  

4. Selecione uma ou mais das caixas de verificação que apresentam um grupo de definições.  

5. Selecione cada grupo de definições no painel de navegação e configurar as definições disponíveis, em seguida, clique em **OK**.   

6. Selecione a definição que criou de cliente personalizado. Sobre o **home page** separador o **as definições de cliente** de grupo, selecione **implementar**.  

7. Na **selecionar coleção** caixa de diálogo, selecione a coleção apropriada e, em seguida, escolha **OK**. Pode verificar a coleção selecionada clicando no separador **Implementações** do painel de detalhes.  

8. Ver a ordem do cliente personalizado que criou a definição. Quando tem várias definições personalizadas de cliente, estas são aplicadas de acordo com o seu número de ordem. Se existirem conflitos, a definição que tiver o menor número de ordem substitui as outras definições. Para alterar o número de ordem, no **home page** separador a **definições de cliente** de grupo, escolha **Mover Item para cima** ou **Mover Item para baixo**.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) na [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  



##  <a name="view-client-settings"></a>Ver definições de cliente  
 Ao implementar várias definições de cliente para o mesmo dispositivo, utilizador ou grupo de utilizadores, a combinação de definições e priorização é complexo. Para ver as definições de cliente:  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos** > **utilizadores** ou **coleções de utilizadores** .  

3.  Selecione um dispositivo, um utilizador ou um grupo de utilizadores e, no grupo **Definições do Cliente** , selecione **Definições de Cliente Resultantes**.  

4.  Selecione uma definição no painel à esquerda do cliente e as definições são apresentadas. Nesta vista, as definições são só de leitura. 

    > [!NOTE]  
    >  Para ver as definições de cliente, tem de ter acesso de leitura às definições de cliente.  

    