---
title: "Configurar a gestão de energia"
titleSuffix: Configuration Manager
description: "Configure a gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ed6aa0ce35d93837ac133cccedb44dedaa4a9602
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configurar a gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar a gestão de energia no System Center Configuration Manager, tem de efetuar os seguintes passos de configuração.  

## <a name="enable-and-configure-power-management-client-settings"></a>Ativar e configurar as definições de cliente de gestão de energia  
 Este procedimento configura as predefinições de cliente para a gestão de energia e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores que pretende que utilizem gestão de energia. Para obter mais informações sobre como criar definições personalizadas de dispositivos, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Para ativar a gestão de energia e configurar as definições de cliente  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , clique em **Definições do Cliente**.  

3.  Clique em **Predefinições de Cliente**.  

4.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Predefinições de Cliente** , clique em **Gestão de Energia**.  

6.  Configure o seguinte valor para as definições de cliente de gestão de energia:  

    -   **Permitir gestão de energia dos dispositivos** – Na lista pendente, selecione **Verdadeiro** para ativar a gestão de energia.  

7.  Configure as definições de cliente de que necessita. Para obter uma lista de definições de cliente de gestão de energia que pode configurar, consulte o [gestão de energia](../../../../core/clients/deploy/about-client-settings.md#power-management) secção o [sobre definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) tópico.  

8.  Clique em **OK** para fechar a caixa de diálogo **Predefinições de Cliente** .  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Excluir computadores da gestão de energia  
 Pode impedir que as coleções de computadores recebam definições de gestão de energia. Se um computador for membro de qualquer coleção excluída das definições de gestão de energia, esse computador não aplica definições de gestão de energia, mesmo que seja membro de outra coleção que aplique definições de gestão de energia.  

 Pode pretender excluir computadores da gestão de energia por qualquer uma das seguintes razões:  

-   Tem um requisito comercial para os computadores estarem sempre ligados.  

-   Criou uma coleção de controlo dos computadores na qual não pretende aplicar definições de gestão de energia.  

-   Alguns dos computadores não podem aplicar definições de gestão de energia.  

-   Pretende excluir computadores que executem o Windows Server da gestão de energia.  

> [!NOTE]  
>  Se a opção **Permitir que os utilizadores excluam o seu dispositivo da gestão de energia** estiver configurada nas definições de cliente, os utilizadores podem excluir os seus próprios computadores da gestão de energia através do Centro de Software.  

 Para saber quais os computadores que foram excluídos da gestão de energia, execute o relatório **Computadores Excluídos**. Para obter mais informações sobre este relatório consulte [computadores excluídos](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) no [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  As definições de energia aplicadas a computadores que executam o Windows XP ou o Windows Server 2003 não são revertidas para os valores originais, mesmo que exclua o computador da gestão de energia. Em versões posteriores do Windows, excluir um computador da gestão de energia faz com que todas as definições de energia sejam revertidas para os valores originais. Não é possível reverter as definições de energia individuais para os valores originais.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Para excluir uma coleção de computadores da gestão de energia  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , selecione a coleção que pretende excluir da gestão de energia e, no separador **Base** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No **gestão de energia** separador do *< nome da coleção\>***propriedades** caixa de diálogo, selecione **nunca aplicar as definições de gestão de energia aos computadores desta coleção**.  

5.  Clique em **OK** para fechar o *< nome da coleção\>***propriedades** caixa de diálogo e guardar as definições.  
