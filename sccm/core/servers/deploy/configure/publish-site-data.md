---
title: Publicar dados do site
titleSuffix: Configuration Manager
description: "Saiba como publicar sites do Configuration Manager para serviços de domínio do Active Directory."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: "8"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 70f3d0d048d1a80e9f11cc111166dd3ade0325f5
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publicar dados do site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de expandir o esquema do Active Directory para o System Center Configuration Manager, pode publicar sites do Configuration Manager para serviços de domínio do Active Directory (AD DS). Isto permite aos computadores do Active Directory obterem de forma segura informações do site de uma origem fidedigna. Embora a publicação de informações de site para o AD DS não são necessárias para funcionalidades básicas do Configuration Manager, pode reduzir a sobrecarga administrativa para fazê-lo.  

-   **Quando um site estiver configurado para publicar no AD DS**, clientes do Configuration Manager poderão procurar automaticamente pontos de gestão através da publicação no Active Directory. Se utilizarem uma consulta LDAP para um servidor de catálogo global.  

-   **Quando um site não publica no AD DS**, os clientes precisarão de um mecanismo alternativo para localizar o respetivo ponto de gestão predefinido.  

Para obter informações sobre como os clientes localizam um ponto de gestão, consulte [compreender a forma como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sites para publicar no AD DS  
 Seguem-se os passos de nível superior:  

-   Tem [expandir o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) em cada floresta onde pretenda publicar dados do site. Certifique-se também a **System Management** contentor está presente.  

-   Tem de conceder a conta de computador de cada site primário que irá publicar dados **controlo total** para o **System Management** contentor e todos os seus objetos subordinados.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para permitir que um site do Configuration Manager publicar informações do site na floresta do Active Directory

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**e clique em **Sites**. Selecione o site que pretende ter publicar os respetivos dados de site. Em seguida, no **home page** separador o **propriedades** , clique em **propriedades**.  

3.  No **publicação** separador de propriedades do site, selecione as florestas nas quais este site irá publicar dados do site.  

4.  Clique em **OK** para guardar a configuração.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , clique em **Florestas do Active Directory**. Se a Deteção de Florestas do Active Directory tiver sido executada anteriormente, as florestas detetadas serão apresentadas no painel de resultados. A floresta local e quaisquer florestas fidedignas são detetadas quando a Deteção de Florestas do Active Directory é executada. Apenas é necessário adicionar manualmente as florestas não fidedignas.  

    -   Para configurar uma floresta detetada anteriormente, selecione uma floresta no painel de resultados. Em seguida, no **home page** separador o **propriedades** , clique em **propriedades** para abrir as propriedades da floresta. Continue com o passo 3.  

    -   Para configurar uma nova floresta que não está listada, no **home page** separador o **criar** , clique em **adicionar floresta** para abrir o **adicionar florestas** caixa de diálogo. Continue com o passo 3.  

3.  No **geral** separador, conclua as configurações da floresta que pretende detetar e especifique o **conta de floresta do Active Directory**.  

    > [!NOTE]  
    >  A Deteção de Florestas do Active Directory requer uma conta global para detetar e publicar em florestas não fidedignas. Se não utilizar a conta de computador do servidor do site, só pode selecionar uma conta global.  

4.  Se pretende permitir que os sites publiquem dados do site nesta floresta, conclua as configurações para publicação nesta floresta no separador **Publicação** .  

    > [!NOTE]  
    >  Se permitir os sites publiquem numa floresta, tem de expandir o esquema do Active Directory dessa floresta para o Configuration Manager. A conta de floresta do Active Directory tem de ter permissões de controlo total ao contentor do sistema dessa floresta.  

5.  Quando concluir a configuração desta floresta para ser utilizada com a Deteção de Florestas do Active Directory, clique em **OK** para guardar a configuração.  
