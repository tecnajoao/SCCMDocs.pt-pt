---
title: Como utilizar o Explorador de recursos
titleSuffix: Configuration Manager
description: Utilize o Explorador de recursos para ver o inventário de hardware no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f39d06072222c14627481f21139f06ee6656c4
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384992"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Como utilizar o Explorador de recursos para ver o inventário de hardware no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Explorador de recursos no Configuration Manager para ver informações sobre o inventário de hardware. O site recolhe informações de clientes na sua hierarquia.  

> [!Tip]  
>  Explorador de recursos não apresenta todos os dados até que um ciclo de inventário de hardware é executado no cliente para o qual está se conectando.  



## <a name="overview"></a>Descrição Geral

Explorador de recursos tem as seguintes secções relacionadas com o inventário de hardware:  

- **Hardware**: Mostra o inventário de hardware mais recente recolhido do dispositivo cliente especificado.  

    - O **estado de estação de trabalho** nó mostra a hora e data do último inventário de hardware do dispositivo.  

- **Histórico de hardware**: Um histórico dos itens inventariados que foram alterados desde o último ciclo de inventário de hardware.  

    - Expanda um item para ver uma **atual** nó e um ou mais nós com a data de histórica. Compare as informações do nó atual para um de nós do histórico para ver os itens que foram alterados.  

> [!NOTE]  
> Por predefinição, o Configuration Manager elimina dados de inventário de hardware que tenham estado Inativos durante 90 dias. Ajustar este número de dias no **eliminar histórico de inventário desatualizado** tarefa de manutenção do site. Para obter mais informações, consulte [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks).  



## <a name="bkmk_open"></a> Como abrir o Explorador de recursos   

1.  Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione o **dispositivos** nó. Também pode selecionar qualquer coleção na **coleções de dispositivos** nó.  

2.  Selecione um dispositivo. No Friso, sobre o **home page** separador e **dispositivos** , clique em **iniciar**e, em seguida, selecione **Explorador de recursos**.   

> [!Tip]  
> No Explorador de recursos, clique com botão direito num item no painel de resultados de certas para ações adicionais. Clique em **propriedades** para ver esse item num formato diferente.  



## <a name="bkmk_bigint"></a> Utilização de valores de número inteiro grande
<!--1357880--> Em versões do Configuration Manager 1802 e anterior, o inventário de hardware tem um limite de números inteiros maiores do que 4,294,967,296 (2 ^ 32). Este limite pode ser contatado para atributos, como tamanhos de disco rígido em bytes. O ponto de gestão não processa os valores de número inteiro acima desse limite, para que nenhum valor é armazenado na base de dados. 

A partir da versão 1806, o limite foi aumentado para 18,446,744,073,709,551,616 (2 ^ 64). 

Para uma propriedade com um valor que não é alterado, como o tamanho total do disco, poderá não ver de imediato o valor depois de atualizar o site. A maioria dos inventário de hardware é um relatório de delta. O cliente envia apenas valores que alterarem. Para contornar este comportamento, adicione outra propriedade para a mesma classe. Esta ação faz com que o cliente atualizar todas as propriedades na classe que foi alterado. 



## <a name="see-also"></a>Consulte também

Para obter informações sobre como ver o inventário de hardware de clientes que executam o Linux e UNIX, consulte [como monitorizar clientes para servidores Linux e UNIX](/sccm/core/clients/manage/monitor-clients-for-linux-and-unix-servers).  

Explorador de recursos também mostra o inventário de Software. Para obter mais informações, consulte [como utilizar o Explorador de recursos para ver o inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).
