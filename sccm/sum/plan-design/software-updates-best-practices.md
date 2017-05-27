---

title: "Melhores práticas para atualizações de software | Documentos do Microsoft"
description: "Utilize estas melhores práticas para atualizações de software no System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.translationtype: Machine Translation
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017



---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Procedimentos recomendados para atualizações de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém melhores práticas para atualizações de software no System Center Configuration Manager. As informações estão ordenadas em melhores práticas para a instalação inicial e melhores práticas para operações em curso.  

## <a name="installation-best-practices"></a>Melhores práticas de instalação  
 Utilize as seguintes melhores práticas quando instalar atualizações de software no Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Utilize uma Base de Dados WSUS Partilhada para Pontos de Atualização de Software  
 Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. Ao partilhar a mesma base de dados, pode reduzir significativamente o impacto que pode ocorrer no desempenho do cliente e da rede quando os clientes mudam para um novo ponto de atualização de software. Ainda ocorre uma verificação de diferenças quando um cliente muda para um novo ponto de atualização de software que partilha uma base de dados com o antigo ponto de atualização de software, mas esta verificação é muito menor do que seria se o servidor WSUS tivesse a sua própria base de dados.  

> [!IMPORTANT]  
>  Também tem de partilhar as pastas de conteúdo do WSUS quando utiliza uma base de dados partilhada do WSUS para os pontos de atualização de software.  

 Para obter mais informações sobre a mudança de ponto de atualização de software, consulte o [mudança de ponto de atualização de Software](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) secção a [planear atualizações de software no System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md) tópico.  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Quando o Configuration Manager e o WSUS utilizam o mesmo SQL Server, configure um deles para utilizar uma instância nomeada e a outra para utilizar a instância predefinida do SQL Server  
 Quando as bases de dados do Configuration Manager e do WSUS utilizam o mesmo SQL Server e partilham a mesma instância do SQL Server, não consegue determinar facilmente a utilização de recursos entre as duas aplicações. Quando utiliza uma instância diferente do SQL Server do Configuration Manager e do WSUS, é mais fácil diagnosticar e resolver problemas de utilização de recursos que possam ocorrer para cada aplicação.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Especifique a definição "Armazenar atualizações localmente" para a instalação do WSUS  
 Quando instala o WSUS, selecione o **armazenar atualizações localmente** definição. Quando esta definição está selecionada, os termos de licenciamento que estão associados às atualizações de software são transferidos durante o processo de sincronização e armazenados no disco rígido local do servidor WSUS. Quando esta definição não estiver selecionada, os computadores cliente poderão falhar a verificação da existência de conformidade de atualizações de software para atualizações de software com termos de licenciamento. Quando instala o ponto de atualização de software, o Gestor de Sincronização do WSUS verifica se esta definição está ativada a cada 60 minutos, por predefinição.  

## <a name="operational-best-practices"></a>Melhores Práticas Operacionais  
 Utilize as seguintes melhores práticas quando utilizar atualizações de software:  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Limite as atualizações de software a 1000 numa única implementação de atualização de software  
 Tem de limitar o número de atualizações de software a 1000 para cada implementação de atualização de software. Quando criar uma regra de implementação automática, certifique-se de que os critérios que especifica não resultam em mais de 1000 atualizações de software. Ao implementar manualmente atualizações de software, não selecione mais de 1000 atualizações para implementar.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Crie um novo grupo de atualização de software sempre que for executada uma regra de implementação automática para "Patch Terça" e para implementação em geral  
 Existe um limite de 1000 atualizações de software para uma implementação de atualização de software. Quando criar uma regra de implementação automática, especifique se pretende utilizar um grupo de atualização existente ou criar um novo grupo de atualização sempre que a regra for executada. Quando especificar critérios numa regra de implementação automática que resulte em várias atualizações de software e a regra for executada periodicamente, especifique criar um novo grupo de atualização de software sempre que a regra for executada. Isto irá impedir que a implementação exceda o limite de 1000 atualizações de software por implementação.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Utilize um grupo de atualização de software existente para regras de implementação automática de atualizações de definições do Endpoint Protection  
 Utilize sempre um grupo de atualização de software existente quando utilizar uma regra de implementação automática para implementar atualizações de definições do Endpoint Protection com frequência. Caso contrário, poderão ser criados centenas de grupos de atualização de software ao longo do tempo. Normalmente, os editores de atualizações de definição configuram as atualizações de definição para expirarem quando são substituídas por quatro atualizações mais recentes. Por conseguinte, o grupo de atualizações de software que é criado pela regra de implementação automática nunca irá conter mais de quatro atualizações de definições para o editor: uma ativa e três substituídas.  

## <a name="see-also"></a>Consulte Também  
 [Planear atualizações de software no System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md)

