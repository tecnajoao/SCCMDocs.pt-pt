---
title: "Configurar definições de cliente | Documentos do Microsoft"
description: "Selecione as definições de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 478d562bfb7fdb3921a4278741ff096e81e6092a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Como configurar as definições de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode gerir todas as definições do cliente no System Center Configuration Manager, a partir de **administração** > **definições de cliente**. Modifique as predefinições quando pretender configurar definições para todos os utilizadores e dispositivos da hierarquia que não têm definições personalizadas aplicadas. Se pretender aplicar definições diferentes apenas nalguns utilizadores ou dispositivos, crie definições personalizadas e implemente-as nas coleções.  

Para obter informações sobre cada definição do cliente, consulte o artigo [sobre definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Também pode utilizar itens de configuração a fim de gerir os clientes para avaliar, controlar e retificar a compatibilidade de configuração dos dispositivos. Para obter mais informações, consulte o artigo [garantir a conformidade de dispositivos com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configurar as predefinições de cliente    

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

3.  No **base** separador, escolha **propriedades**.  

4.  Veja e configure as definições do cliente de cada grupo de definições do painel de navegação.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção de política para um único cliente, consulte o artigo [iniciar a obtenção de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) no [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Criar e implementar definições personalizadas de cliente  
Quando implementar estas definições personalizadas, elas substituirão as predefinições do cliente. Antes de iniciar este procedimento, certifique-se de que tem uma coleção com os utilizadores ou dispositivos que necessitam destas definições personalizadas de cliente.  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente**.  

3.  No **base** separador o **criar** grupo, selecione **criar definições personalizadas do cliente**e, em seguida, selecione:  

    -   **Criar Definições Personalizadas do Dispositivo Cliente**  

    -   **Criar Definições Personalizadas do Utilizador Cliente**  

4.  Especifique uma descrição exclusiva de nome e a opção.  

5.  Selecione uma ou mais das caixas de verificação que apresentem um grupo de definições.  

6.  Selecione cada grupo de definições a partir do painel de navegação e configurar as definições disponíveis, em seguida, clique em **OK**.   

8.  Selecione a definição que criou de cliente personalizado. No **base** separador o **definições de cliente** grupo, selecione **implementar**.  

9. No **selecionar coleção** caixa de diálogo, seleccione a colecção apropriada e, em seguida, selecione **OK**. Pode verificar a coleção selecionada clicando no separador **Implementações** do painel de detalhes.  

10. Veja a ordem da definição personalizada do cliente que acabou de criar. Quando tem várias definições personalizadas de cliente, estas são aplicadas de acordo com o seu número de ordem. Se existirem conflitos, a definição que tiver o menor número de ordem substitui as outras definições. Para alterar o número de ordem, no **base** separador o **definições de cliente** grupo, selecione **Mover Item para cima** ou **Mover Item para baixo**.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção de política para um único cliente, consulte o artigo [iniciar a obtenção de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) no [como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="view-client-settings"></a>Ver definições de cliente  
 Quando tiverem sido implementadas várias definições do cliente no mesmo dispositivo, utilizador ou grupo de utilizadores, a atribuição de prioridades e a combinação de definições podem ser complexas. Para ver as definições de cliente:  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos** > **utilizadores** ou **coleções de utilizadores**.  

3.  Selecione um dispositivo, um utilizador ou um grupo de utilizadores e, no grupo **Definições do Cliente** , selecione **Definições de Cliente Resultantes**.  

4.  Selecione uma definição no painel da esquerda do cliente e as definições são apresentadas. Nesta vista, as definições são só de leitura. 

    > [!NOTE]  
    >  Para ver as definições de cliente, tem de ter acesso de leitura às definições do cliente.  

    
