---
title: Transições de Estados de validação de exemplo para o Asset Intelligence
titleSuffix: Configuration Manager
description: Veja exemplos de transições de estado de validação do Asset Intelligence no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd4d2075e7980361d341a6ed71ff151ada997060
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>Transições de Estados de validação de exemplo para o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Estados de validação do Asset Intelligence no System Center Configuration Manager não são estáticos e podem ser alterado de ações administrativas para afetar os dados que são armazenados no catálogo do Asset Intelligence. Este tópico fornece exemplos de validação possíveis transições de estado.

##  <a name="BKMK_UncategorizedIsCategorized"></a> O item de catálogo não categorizado foi categorizado pelo utilizador administrativo  

|**Transição de estado**|**Descrição da transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado que não foi categorizado anteriormente pelo System Center Online ou que o utilizador administrativo introduziu no catálogo do Asset Intelligence.|  
|**Não Categorizado** para **Definido peloUtilizador**|O item não categorizado foi categorizado pelo utilizador administrativo.|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> O item de catálogo categorizado foi novamente categorizado pelo utilizador administrativo  

|**Transição de estado**|**Descrição da transição de estado**|  
|--------------------------|--------------------------------------|  
|**Validado**|O item de catálogo foi definido pelos investigadores do System Center Online e está presente no catálogo do Asset Intelligence.|  
|**Validado** para **Definido pelo Utilizador**|O item de catálogo validado foi novamente categorizado pelo utilizador administrativo.|  

> [!NOTE]  
>  Uma vez que as informações de categorização obtidas a partir do System Center Online estão armazenadas na base de dados e não podem ser eliminadas, o utilizador administrativo pode reverter mais tarde para a categorização do System Center Online.  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> O item de catálogo definido pelo utilizador foi novamente categorizado pelo System Center Online  

|**Transição de estado**|**Descrição da transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado introduzido no catálogo do Asset Intelligence que não foi categorizado anteriormente pelo System Center Online ou pelo utilizador administrativo.|  
|**Definido pelo Utilizador**|O item não categorizado foi categorizado pelo utilizador administrativo.|  
|**Definido pelo Utilizador** para **Atualizável**|Um item de catálogo definido pelo utilizador foi categorizado de forma diferente pelo System Center Online durante atualizações em massa manuais do catálogo do Asset Intelligence.<br /><br /> O utilizador administrativo pode utilizar a caixa de diálogo **Resolução de Conflitos de Detalhes de Software** para decidir se deve utilizar as novas informações de categorização ou o valor definido pelo utilizador anterior.|  
|**Atualizável** para **Validado**|O utilizador administrativo utiliza a caixa de diálogo **Resolução de Conflitos de Detalhes de Software** para utilizar as novas informações de categorização recebidas a partir do System Center Online durante a atualização do catálogo anterior.|  
|ou||  
|**Atualizável** para **Definido pelo Utilizador**|O utilizador administrativo utiliza a caixa de diálogo **Resolução de Conflitos de Detalhes de Software** para utilizar o valor definido pelo utilizador anterior.|  

> [!NOTE]  
>  Uma vez que as informações de categorização obtidas a partir do System Center Online estão armazenadas na base de dados e não podem ser eliminadas, o utilizador administrativo pode reverter mais tarde para a categorização do System Center Online.  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> O item de catálogo não categorizado foi submetido para o System Center Online para categorização  

|**Transição de estado**|**Descrição da transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado introduzido na base de dados do Asset Intelligence que não foi categorizado anteriormente pelo System Center Online ou pelo utilizador administrativo.|  
|**Não Categorizado** para **Pendente**|O item não categorizado foi submetido para o System Center Online para categorização pelo utilizador administrativo.|  
|**Pendente** para **Validado**|O item é categorizado pelo System Center Online. O utilizador administrativo importa o item para o catálogo do Asset Intelligence através de uma atualização de catálogo em massa ou da sincronização do catálogo do Asset Intelligence. Ambos estão disponíveis utilizando uma função de sistema de sites do ponto de sincronização do Asset Intelligence.|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> O item de catálogo definido pelo utilizador foi submetido para o System Center Online para categorização  

|**Transição de estado**|**Descrição da transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado introduzido na base de dados do Asset Intelligence que não foi categorizado por um utilizador administrativo ou pelo System Center Online.|  
|**Definido pelo Utilizador**|Categorizou o item não categorizado.|  
|**Definido pelo Utilizador** para **Pendente**|Submete o item definido pelo utilizador para o System Center Online para categorização.|  
|**Pendente** para **Atualizável**|Um item de catálogo definido pelo utilizador foi categorizado de forma diferente pelo System Center Online durante a sincronização do catálogo subsequente. Pode utilizar a ação **Resolver Conflito** para decidir se deve utilizar as novas informações de categorização ou o valor definido pelo utilizador anterior. Para obter mais informações sobre como resolver conflitos, consulte [resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Atualizável** para **Validado**|Utilize a ação **Resolver Conflito** e selecione as novas informações de categorização recebidas a partir do System Center Online durante a atualização do catálogo anterior. Para obter mais informações sobre como resolver conflitos, consulte [resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|ou||  
|**Atualizável** para **Definido pelo Utilizador**|Utilize a ação **Resolver Conflito** e selecione para utilizar o valor definido pelo utilizador anterior. Para obter mais informações sobre como resolver conflitos, consulte [resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Uma vez que as informações de categorização obtidas a partir do System Center Online estão armazenadas na base de dados e não podem ser eliminadas, pode reverter mais tarde para a categorização do System Center Online.  
