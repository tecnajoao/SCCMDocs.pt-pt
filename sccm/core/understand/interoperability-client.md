---
title: Cliente de interoperabilidade expandido
titleSuffix: Configuration Manager
description: Saiba como utilizar o cliente de interoperabilidade expandido para o suporte a longo prazo de um cliente de Configuration Manager estático com um site do ramo atual.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e339d096b64bb35cd344e601212ae5ec1f5504ec
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119631"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utilizar o software de cliente do Configuration Manager para a interoperabilidade estendida com futuras versões de um site do ramo atual

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  

Requisitos de negócio poderão não permitir atualizar regularmente o cliente do Configuration Manager em alguns dispositivos. Por exemplo, poderá ter de estar em conformidade com políticas de gestão de alteração, ou o dispositivo poderá ser de missão crítica. Acomodar essas necessidades, instalando um novo cliente para utilização a longo prazo, chamado do cliente de interoperabilidade estendida (EIC). Utilize o EIC apenas para dispositivos específicos que não podem ser atualizados com frequência, como o local público ou dispositivos de ponto de venda. Continuar a utilizar [atualização automática de cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) para a maioria dos seus clientes. 

## <a name="how-this-scenario-works"></a>Como funciona este cenário

Normalmente, quando instala um novo [atualização na consola](/sccm/core/servers/manage/install-in-console-updates) no Configuration Manager, os clientes atualizar automaticamente o software de cliente para que eles podem usar esses novos recursos. Com este cenário, ainda a atualização para o current branch receber as novas funcionalidades e atualizações. A maioria dos dispositivos Atualize o software de cliente do Configuration Manager com cada atualização de versão a que instalar. No entanto, num subconjunto dos sistemas críticos que não pretende receber atualizações de software de cliente, instala o cliente de interoperabilidade estendida. Estes clientes não instalam novo software de cliente até que implementa explicitamente uma nova versão do software de cliente aos mesmos.



## <a name="supported-versions"></a>Versões suportadas
A tabela seguinte lista as versões do cliente do Configuration Manager que são suportadas para este cenário:

| Versão  | Data de disponibilidade  | Data de fim do suporte  |
|---------|---------|---------|
|1802<br/>5.00.8634     | 1 de Maio de 2018        | Não anterior a 1 de Maio de 2020        |
|1606<br/>5.00.8412     | 18 de Novembro de 2016        | 1 de Maio de 2019        |

> [!TIP]  
> O EIC é suportada para, pelo menos, dois anos a contar da data de lançamento. Para obter mais informações sobre as datas de lançamento, consulte [suporte para versões de ramo atual do System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)).  

Planear atualizar o cliente de interoperabilidade estendida em dispositivos que gere com o ramo atual antes de suporte para o cliente expira. Para fazer isso, transfira uma nova versão do cliente da Microsoft e, em seguida, implantar esse software de cliente atualizado para os seus dispositivos que utilizam o cliente de interoperabilidade estendida atual.



## <a name="how-to-use-the-eic"></a>Como utilizar o EIC

1. Obter uma versão suportada do EIC do `\SMSSETUP\Client` pasta do suporte de instalação de atualização do Configuration Manager. Certifique-se de que copia todo o conteúdo da pasta.  

2. Instale manualmente o EIC nesses dispositivos. Para obter mais informações, consulte [instalar manualmente o cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).  

    > [!Important]  
    > Ao atualizar os clientes da versão 1606 para versão 1802, utilize a opção de CCMSETUP **/AlwaysExcludeUpgrade:True**. Caso contrário, o cliente pode receber uma política do ponto de gestão para atualizar automaticamente antes da política de exclusão.

3. Adicionar estes dispositivos a uma coleção e excluir essa coleção de atualizações automáticas de clientes. Para obter mais informações, consulte [utiliza a atualização automática do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

> [!TIP]  
> Para localizar o suporte de dados do Configuration Manager na [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), vá para o **Downloads e chaves** separador, procure `System Center Config`e, em seguida, selecione **System Center O Gestor de configuração (ramo atual)**.



## <a name="limitations-of-the-extended-interoperability-client"></a>Limitações do cliente de interoperabilidade expandido

- Atualizações de software de cliente a interoperabilidade estendida não estão disponíveis ao utilizar atualizações na consola. Para obter mais informações sobre como atualizar clientes EIC, consulte [como utilizar o EIC](#how-to-use-the-eic).  

- O EIC só suporta as seguintes funcionalidades:  

   - Atualizações de software  
   - Inventário de hardware e software
   - Pacotes e programas



## <a name="next-steps"></a>Passos seguintes

Para garantir que os clientes estão corretamente instalados nos dispositivos que pretende, veja [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients).
