---
title: Configurar a gestão de energia
titleSuffix: Configuration Manager
description: Configure a gestão de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9561528d8f02cf5909c83a88a276e1d263343589
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142243"
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configurar a gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar a gestão de energia no System Center Configuration Manager, tem de efetuar os seguintes passos de configuração.  

## <a name="enable-and-configure-power-management-client-settings"></a>Ativar e configurar as definições de cliente de gestão de energia  
 Este procedimento configura as predefinições de cliente para a gestão de energia e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores que pretende que utilizem gestão de energia. Para obter mais informações sobre como criar definições personalizadas de dispositivos, consulte [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Para ativar a gestão de energia e configurar as definições de cliente  

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração** , clique em **Definições do Cliente**.  

3. Clique em **Predefinições de Cliente**.  

4. No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

5. Na caixa de diálogo **Predefinições de Cliente** , clique em **Gestão de Energia**.  

6. Configure o seguinte valor para as definições de cliente de gestão de energia:  

   -   **Permitir gestão de energia dos dispositivos** – Na lista pendente, selecione **Verdadeiro** para ativar a gestão de energia.  

7. Configure as definições de cliente de que necessita. Para obter uma lista das definições de cliente de gestão de energia que pode configurar, consulte a secção [Power Management](../../../../core/clients/deploy/about-client-settings.md#power-management) no tópico [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) .  

8. Clique em **OK** para fechar a caixa de diálogo **Predefinições de Cliente** .  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Excluir computadores da gestão de energia  
 Pode impedir que as coleções de computadores recebam definições de gestão de energia. Se um computador for membro de qualquer coleção excluída das definições de gestão de energia, esse computador não aplica definições de gestão de energia, mesmo que seja membro de outra coleção que aplique definições de gestão de energia.  

 Pode pretender excluir computadores da gestão de energia por qualquer uma das seguintes razões:  

-   Tem um requisito comercial para os computadores estarem sempre ligados.  

-   Criou uma coleção de controlo dos computadores na qual não pretende aplicar definições de gestão de energia.  

-   Alguns dos computadores não podem aplicar definições de gestão de energia.  

-   Pretende excluir computadores que executem o Windows Server da gestão de energia.  

> [!NOTE]  
>  Se a opção **Permitir que os utilizadores excluam o seu dispositivo da gestão de energia** estiver configurada nas definições de cliente, os utilizadores podem excluir os seus próprios computadores da gestão de energia através do Centro de Software.  

 Para saber quais os computadores que foram excluídos da gestão de energia, execute o relatório **Computadores Excluídos**. Para obter mais informações sobre este relatório, consulte [computadores excluídos](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) na [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  As definições de energia aplicadas a computadores que executam o Windows XP ou o Windows Server 2003 não são revertidas para os valores originais, mesmo que exclua o computador da gestão de energia. Em versões posteriores do Windows, excluir um computador da gestão de energia faz com que todas as definições de energia sejam revertidas para os valores originais. Não é possível reverter as definições de energia individuais para os valores originais.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Para excluir uma coleção de computadores da gestão de energia  

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3. Na lista **Coleções de Dispositivos** , selecione a coleção que pretende excluir da gestão de energia e, no separador **Base** , no grupo **Propriedades** , clique em **Propriedades**.  

4. Na **gestão de energia** separador da <em>< nome da coleção\></em>**propriedades** caixa de diálogo, selecione **nunca aplicar a gestão de energia definições para computadores desta coleção**.  

5. Clique em **OK** para fechar a <em>< nome da coleção\></em>**propriedades** caixa de diálogo e guardar as suas definições.  
