---
title: Cliente de interoperabilidade expandida
titleSuffix: Configuration Manager
description: Saiba como utilizar o cliente de interoperabilidade expandido para o suporte de longa duração de um cliente do Configuration Manager estático com um site de sucursal atual.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f46fdb622a55c7281de89c84d5e66e54ab149548
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339541"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utilize o software de cliente do Configuration Manager para interoperabilidade expandida com versões futuras de um site do ramo atual

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  

Requisitos de negócio não podem permitir-lhe atualizar regularmente o cliente de Configuration Manager em alguns dispositivos. Por exemplo, poderá ser necessário está em conformidade com políticas de gestão de alterações ou o dispositivo poderá ser fundamentais. Acomodar estas necessidades ao instalar um novo cliente para utilização de longa duração, denominado o cliente de interoperabilidade expandida (EIC). Utilize o EIC apenas para dispositivos específicos que não podem ser atualizados frequentemente, como dispositivos de ponto de venda ou de local público. Continuar a utilizar [atualização automática de cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) para a maior parte dos clientes. 

## <a name="how-this-scenario-works"></a>Como funciona este cenário

Normalmente, quando instala um novo [atualização na consola](/sccm/core/servers/manage/install-in-console-updates) no Configuration Manager, os clientes atualizar automaticamente os respetivos software de cliente para que possam utilizar as novas funcionalidades. Com este cenário, é ainda atualizar para o ramo atual receber as novas funcionalidades e atualizações. A maioria dos dispositivos atualizar o software de cliente do Configuration Manager com cada atualização de versão a que instalar. No entanto, num subconjunto de sistemas críticos que não pretende receber atualizações de software de cliente, instala o cliente de interoperabilidade expandida. Estes clientes não instalam o novo software de cliente até explicitamente implementar uma nova versão do software de cliente aos mesmos.



## <a name="supported-versions"></a>Versões suportadas
A tabela seguinte lista as versões do cliente do Configuration Manager que são suportadas para este cenário:

| Versão  | Data de disponibilidade  | Data de fim de suporte  |
|---------|---------|---------|
|1802<br/>5.00.8634     | 1 de Maio de 2018        | Não anterior ao 1 de Maio de 2020        |
|1606<br/>5.00.8412     | 18 de Novembro de 2016        | 1 de Maio de 2019        |

> [!TIP]  
> O EIC é suportada para, pelo menos, dois anos a partir da data da versão. Para obter mais informações sobre datas de versão, consulte [suporte para versões do System Center Configuration Manager current branch](/sccm/core/servers/manage/current-branch-versions-supported)).  

Planear atualizar o cliente de interoperabilidade expandidas em dispositivos que gere com o ramo atual antes do suporte para o cliente expira. Para tal, transfira uma nova versão do cliente da Microsoft e, em seguida, implementar esse software de cliente atualizado nos seus dispositivos que utilizam o cliente de interoperabilidade expandida atual.



## <a name="how-to-use-the-eic"></a>Como utilizar o EIC

1. Obter uma versão suportada do EIC do `\SMSSETUP\Client` na pasta do suporte de instalação de atualização do Configuration Manager. Certifique-se de que copie todo o conteúdo da pasta.  

2. Instale manualmente o EIC nesses dispositivos. Para obter mais informações, consulte [instalar manualmente o cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).  

    > [!Important]  
    > Ao atualizar os clientes de versão 1606 para versão 1802, utilize a opção CCMSETUP **/AlwaysExcludeUpgrade:True**. Caso contrário, o cliente poderá receber a política do ponto de gestão para atualizar automaticamente antes da política de exclusão.

3. Adicionar estes dispositivos a uma coleção e excluir esse coleção de atualizações automáticas de cliente. Para obter mais informações, consulte [utiliza a atualização automática do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

> [!TIP]  
> Para localizar o suporte de dados do Configuration Manager no [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), aceda ao **transfere e chaves** separador, procure `System Center Config`e, em seguida, selecione **System Center Config Mgr (ramo atual)**.



## <a name="limitations-of-the-extended-interoperability-client"></a>Limitações do cliente interoperabilidade expandida

- Atualizações para o software de cliente de interoperabilidade expandida não estão disponíveis através da utilização de atualizações na consola. Para obter mais informações sobre como atualizar clientes EIC, consulte [como utilizar o EIC](#how-to-use-the-eic).  

- O EIC só suporta as seguintes funcionalidades:  

   - Atualizações de software  
   - Inventário de hardware e software
   - Pacotes e programas



## <a name="next-steps"></a>Passos seguintes

Para garantir que os clientes estão corretamente instalados nos dispositivos que pretende, consulte [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients).
