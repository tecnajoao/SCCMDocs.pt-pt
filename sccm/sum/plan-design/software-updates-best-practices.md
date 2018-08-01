---
title: Melhores práticas para atualizações de software
titleSuffix: Configuration Manager
description: Utilize estas melhores práticas para atualizações de software no Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: fd16b33b885786d7a613096456774fc05d70f8a4
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383121"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Melhores práticas para atualizações de software no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo inclui procedimentos recomendados para atualizações de software no Configuration Manager. As informações estão ordenadas em melhores práticas para a instalação inicial e para operações em curso.  



## <a name="bkmk_install"></a> Melhores práticas de instalação  

Utilize as seguintes melhores práticas quando instalar atualizações de software no Configuration Manager.  


### <a name="bkmk_shared-susdb"></a> Utilizar uma base de dados WSUS partilhada para pontos de atualização de software  

Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. Se partilhar a mesma base de dados, ele reduzirá significativamente, embora não elimine completamente, o cliente e o impacto de desempenho de rede que podem ocorrer quando os clientes mudarem para um novo ponto de atualização de software. Uma análise de delta ainda ocorre quando um cliente muda para um ponto de atualização de software novo que partilhas de ponto de uma base de dados com a atualização de software antigo, mas a verificação é muito menor do que seria se o servidor WSUS tem sua própria base de dados. Para obter mais informações sobre a mudança de ponto de atualização de software, consulte [mudança de ponto de atualização de Software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Também partilhe as pastas de conteúdo do WSUS locais quando utiliza uma base de dados WSUS partilhada para pontos de atualização de software.  

Para obter mais informações sobre o compartilhamento da base de dados do WSUS, consulte as seguintes mensagens de blogue:  

- [Como implementar um SUSDB partilhada para pontos de atualização de software do Configuration Manager](https://blogs.technet.microsoft.com/configurationmgr/2016/10/12/how-to-implement-a-shared-susdb-for-configuration-manager-software-update-points/)  

- [Considerações para várias instâncias WSUS partilha uma base de dados de conteúdo ao utilizar o System Center Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="bkmk_sql-instance"></a> Quando o Configuration Manager e o WSUS utilizam o mesmo SQL Server, configure uma para utilizar uma instância nomeada e outra para utilizar a instância predefinida  

Quando as bases de dados do Configuration Manager e o WSUS partilham a mesma instância do SQL Server, não é possível determinar facilmente a utilização de recursos entre as duas aplicações. Utilize várias instâncias de SQL Server do Configuration Manager e o WSUS. Esta configuração torna mais fácil de solucionar problemas e diagnosticar problemas de utilização de recursos que possam ocorrer para cada aplicativo.  


### <a name="bkmk_store-local"></a> Especifique a definição "Store atualizações localmente"  

Quando instala o WSUS, selecione a definição para **Store atualizações localmente**. Esta definição faz com que o WSUS transferir os termos de licenciamento que estão associados a atualizações de software. Ele transfere os termos durante o processo de sincronização e armazena-os no disco rígido local para o servidor WSUS. Se não selecionar esta definição, os computadores cliente poderão falhar verificações de conformidade para atualizações de software com termos de licenciamento. O **Gestor de sincronização WSUS** componente do ponto de atualização de software verifica se esta definição é ativada a cada 60 minutos, por predefinição.  



## <a name="bkmk_operation"></a> Melhores práticas operacionais  

Utilize as seguintes melhores práticas quando utilizar atualizações de software:  


### <a name="bkmk_object-limit"></a> Limitar as atualizações de software a 1000 numa implementação de atualização de software  

Limite o número de atualizações de software a 1000 em cada implementação de atualização de software. Quando cria uma regra de implementação automática, certifique-se de que os critérios especificados não resulta em mais de 1000 atualizações de software. Se implementar manualmente atualizações de software, não selecione mais de 1000 atualizações.  


### <a name="bkmk_new-group"></a> Criar um novo grupo de atualização de software sempre que uma ADR é executada para "Patch Terça" e para as implementações gerais  

Existe um limite de 1000 atualizações de software numa implementação. Quando cria uma regra de implementação automática (ADR), especifique se pretende utilizar um grupo de atualização existente ou criar um novo grupo de atualização sempre que a regra for executada. Se especificar critérios em regras de implementação automática que resulte em várias atualizações de software e a regra é executada numa agenda periódica, crie um novo grupo de atualização de software sempre que a regra for executada. Este comportamento impede que a implementação exceda o limite de 1000 atualizações de software por implementação.  


### <a name="bkmk_same-group"></a> Utilizar um grupo de atualização de software existente para ADRs para atualizações de definições do Endpoint Protection  

Quando utiliza uma ADR para implementar atualizações de definições do Endpoint Protection com frequência, utilize sempre um grupo de atualização de software existente. Caso contrário, a ADR cria potencialmente centenas de grupos de atualização de software ao longo do tempo. Os editores de atualizações, normalmente, defina as atualizações de definição para expirarem quando eles são substituídos por quatro atualizações mais recentes. Por conseguinte, o grupo de atualizações de software criado para a ADR contém nunca mais de quatro atualizações de definições para o Editor: uma ativa e três substituídas.  



## <a name="see-also"></a>Consulte Também  
 [Planear as atualizações de software](/sccm/sum/plan-design/plan-for-software-updates)
