---
title: Notificação de cliente
titleSuffix: Configuration Manager
description: Gerir clientes ao tomar medidas imediatas partir da consola central do Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a643924cbaef928f9db4011f634ae96171ab7914
ms.sourcegitcommit: 544f335cfd1bfd0a1d4973439780e9f5e9ee8bed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562096"
---
# <a name="client-notification-in-configuration-manager"></a>Notificação do cliente no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Tomar medidas imediatas nos clientes remotos, enviar um cliente de ação de notificação a partir da consola do Configuration Manager. Inicie estas ações num dispositivo individual ou numa coleção de dispositivos. 



## <a name="actions"></a>Ações

As ações seguintes estão na faixa de opções no grupo de dispositivo ou a coleção do separador base. 


### <a name="install-client"></a>Instalar cliente

Abre o **instalar o cliente assistente**. Este assistente utiliza a instalação de push de cliente para instalar um cliente do Configuration Manager. Para obter mais informações, consulte [instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### <a name="permissions"></a>Permissões
Esta ação requer o **modificar recurso** e **leitura** permissões sobre o **coleção** objeto. 

Por predefinição, as seguintes funções incorporadas tem estas permissões:
- Administrador da aplicação  
- Administrador total  
- Administrador de infraestrutura  
- Administrador de operações  
- Gestor de implementação do SO  

Adicione estas permissões para quaisquer funções personalizadas que precisam enviar por push do cliente.


### <a name="run-script"></a>Executar script

Abre o **executar Script** Assistente para executar um script do PowerShell em todos os clientes na coleção. Para obter mais informações, consulte [criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

#### <a name="permissions"></a>Permissões
Esta ação requer o **executar Script** permissão sobre a **coleção** objeto. 

As seguintes funções incorporadas têm esta permissão, por predefinição:
- Administrador total  
- Administrador de infraestrutura  
- Administrador de operações  

Adicione esta permissão para quaisquer funções personalizadas que precisam para executar scripts.


### <a name="start-cmpivot"></a>Iniciar CMPivot

Inicia **CMPivot**, que executada consultas em tempo real contra os dispositivos visados. Para obter mais informações, consulte [CMPivot](/sccm/core/servers/manage/cmpivot).

#### <a name="permissions"></a>Permissões
Esta ação requer as mesmas permissões que o [executar script](#run-script) ação. 



## <a name="client-notification"></a>Notificação de cliente

Essas ações estão sob o **notificação do cliente** menu, no Friso do grupo de dispositivo ou a coleção do separador base.

Na versão 1806 ou anterior, o **notificação do cliente** opção só está disponível a partir do nó de coleção de dispositivos ou quando visualizado a associação de uma coleção de dispositivos. A partir da versão 1810, pode iniciar uma **notificação do cliente** diretamente a partir do **dispositivos** nó. Já não é um requisito para estar dentro de uma vista de associação de coleção. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions"></a>Permissões
<!--SCCMDocs-pr issue #2972--> A partir da versão 1810, ações de notificação do cliente agora exigem que o **notificar recursos** permissão no objeto de coleção. Esta permissão aplica-se a todas as ações sob a **notificação do cliente** menu. 

As seguintes funções incorporadas têm esta permissão, por predefinição:
- Administrador total  
- Administrador de infraestrutura  

Adicione esta permissão para quaisquer funções personalizadas que tem de utilizar as ações de notificação do cliente.


### <a name="download-computer-policy"></a>Transferir política do computador

Atualize a política de dispositivo. Para obter mais informações, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  


### <a name="download-user-policy"></a>Transferir política do utilizador

Atualize a política de utilizador.  


### <a name="collect-discovery-data"></a>Recolher dados de deteção

Clientes de Acionador para enviar um registo de dados de deteção (DDR). Para obter mais informações, consulte [deteção de Heartbeat](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  


### <a name="collect-software-inventory"></a>Recolher inventário de software

Ciclo de clientes de Acionador a executar um inventário de software. Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  


### <a name="collect-hardware-inventory"></a>Recolher inventário de hardware

Ciclo de clientes de Acionador a executar um inventário de hardware. Para obter mais informações, consulte [introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  


### <a name="evaluate-application-deployments"></a>Avaliar implementações de aplicações

Ciclo de clientes de Acionador a executar uma edição de avaliação de implementação de aplicação. Para obter mais informações, consulte [agendar reavaliação para implementações](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  


### <a name="evaluate-software-update-deployments"></a>Avaliar implementações de atualizações de software

Ciclo de clientes de Acionador a executar uma avaliação de implementação de atualizações de software. Para obter mais informações, consulte [introdução às atualizações de software](/sccm/sum/understand/software-updates-introduction).  


### <a name="switch-to-the-next-software-update-point"></a>Mude para o próximo ponto de atualização de software

Ponto de atualização de clientes de Acionador para mudar para o seguinte software disponível. Para obter mais informações, consulte [mudança de ponto de atualização de Software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  


### <a name="evaluate-device-health-attestation"></a>Avaliar atestado de estado de funcionamento do dispositivo

Acione os clientes do Windows 10 para verificar e enviar o respetivo estado de funcionamento do dispositivo mais recente. Para obter mais informações, consulte [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation).  


### <a name="check-conditional-access-compliance"></a>Verificação de conformidade de acesso condicional

Clientes de Acionador para verificar a compatibilidade com o acesso condicional. Para obter mais informações, consulte [gerir o acesso aos serviços do O365 para PCs](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


### <a name="wake-up"></a>Reativar

A partir da versão 1810, acionador em suspensão dispositivos para retornar ao estado de energia total.


### <a name="restart"></a>Reiniciar

Acione os dispositivos selecionados para reiniciar. 



## <a name="endpoint-protection"></a>Endpoint Protection

As seguintes ações estão sob o **Endpoint Protection** menu. Esse menu é da faixa de opções no grupo de recolha do separador base. Quando seleciona um ou mais dispositivos, estas ações são sobre o **objeto selecionado** separador do Friso.

Para obter mais informações, consulte [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

#### <a name="permissions"></a>Permissões
Esta ação requer o **impor segurança** permissão sobre a **coleção** objeto. 

As seguintes funções incorporadas têm esta permissão, por predefinição:
- Administrador total  
- Gestor do Endpoint Protection  
- Administrador de operações  

Adicione esta permissão para quaisquer funções personalizadas que precisam para acionar ações do Endpoint Protection.


### <a name="full-scan"></a>Análise completa

Acionar o Endpoint Protection ou o Windows Defender para executar uma *completo* análise de antimalware.  


### <a name="quick-scan"></a>Análise rápida

Acionar o Endpoint Protection ou o Windows Defender para executar uma *Rápido* análise de antimalware.  


### <a name="download-definition"></a>Definição da transferência

Acione o Windows Defender ou Endpoint Protection para transferir as definições de antimalware mais recentes.  



## <a name="see-also"></a>Consulte também

- [Como gerir clientes](/sccm/core/clients/manage/manage-clients)
- [Como gerir coleções](/sccm/core/clients/manage/collections/manage-collections)
