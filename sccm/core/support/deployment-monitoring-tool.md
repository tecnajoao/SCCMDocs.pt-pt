---
title: Ferramenta de Monitorização da Implementação
titleSuffix: Configuration Manager
description: Utilize a ferramenta de monitorização de implementação para resolver problemas de implementações de software num cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2188ce295f999b392166c99133822ad8fc1e441e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125243"
---
# <a name="deployment-monitoring-tool"></a>Ferramenta de Monitorização da Implementação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta de monitorização de implementação é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma interface gráfica do usuário projetada para ajudar na resolução de problemas de aplicativos, da atualização de software e implementações de linha de base de configuração num cliente do Configuration Manager. A ferramenta é só de leitura, pois não altera nenhum Estado no cliente. Pode utilizá-lo com segurança para diagnosticar cenários comuns de implantação.


## <a name="features"></a>Funcionalidades

- Executá-lo como um administrador para resolver implementações num cliente local.  

- Resolver problemas de implementações de um cliente remoto. Inicie a ferramenta e ligar a uma máquina remota como administrador.  

- Exportar para XML, todos os dados recolhidos na ferramenta. Partilhar o ficheiro XML com outras pessoas e utilizá-la como uma plataforma comum para falar sobre resolução de problemas de implementações.  

- Anteriormente, importar dados exportados para um computador diferente e utilizá-lo para executar a ferramenta no modo offline.   


## <a name="usage"></a>Utilização

A ferramenta de monitorização de implantação suporta apenas a interface gráfica do usuário. Para iniciar a ferramenta, execute **DeploymentMonitoringTool.exe** como administrador. Existem três vistas:  

- **Propriedades de cliente**: Uma lista de atributos úteis sobre o dispositivo e o cliente do Configuration Manager. Esta vista é a predefinição.   

- **Implementações**: Ver todas as implementações direcionadas atualmente. Selecione uma implementação no painel de resultados para ver mais informações no painel de detalhes.  

- **Todas as atualizações**: Ver todas as atualizações de software e o respetivo estado.  

Copiar dados em qualquer vista, selecione uma célula e prima **CTRL** + **C**.


### <a name="actions-menu"></a>Menu de ações

As ações seguintes estão disponíveis no **ações** menu:  

- **Ligar à máquina remota**: Selecione um computador para ligar a. Quando não especificar um nome de utilizador e palavra-passe, utiliza as credenciais atuais. Clique em **guardar** para ligar ao computador remoto.  

- **Exportar dados**: Selecione o ficheiro para escrever os dados para e clique em **guardar**. Utilize o ficheiro XML exportado para resolução de problemas remota num computador diferente.  

- **Importar dados**: Selecione um ficheiro a importar para a ferramenta.  

- **Ver registo**: É aberto um ficheiro de registo associado, consoante o modo de exibição:  
    - Propriedades de cliente: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Implementações de: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Todas as atualizações: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Consulte também

- [Implementar aplicações](/sccm/apps/deploy-use/deploy-applications)
- [Implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates)
- [Implementar linhas de base da configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines)
