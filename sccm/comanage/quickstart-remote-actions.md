---
title: Ações remotas com cogestão
titleSuffix: Configuration Manager
description: Executar ações remotas do Intune para dispositivos cogeridos
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81ea4687c0d05e81f493aeab389cb0175f20144f
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073006"
---
# <a name="remote-actions-with-co-management"></a>Ações remotas com cogestão

Tem de certificar-se de que todos os dispositivos que gere está acessível, não importa de onde se encontra, sempre que se liga. Terá também de fornecer tudo o que precisam para se manterem produtivos, ao proteger as aplicações e dados de cada usuário. Com as ações de dispositivos suportadas pelo Intune, pode resolver remotamente essas funções críticas.

No vídeo seguinte, gerente de programa principal Heidi Cheng e gerente de programas sênior Danny Guillory discutem e demonstrar ações remotas com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Benefícios

Ações remotas de dispositivos dão-lhe os controlos de gestão no dispositivo sem interferir com os dados pessoais. Estas ações remotas de dispositivos permitem-lhe: 
- Eliminar dados da empresa em dispositivos perdidos ou roubados  
- Mudar o nome de um dispositivo  
- Reiniciar um dispositivo  
- Inventário de dispositivos de revisão  
- Controlar remotamente um dispositivo  
- Apagar aplicações pré-instaladas do OEM com um reinício de começar do zero  
- Efetue uma reposição de fábrica em todos os dispositivos Windows 10  

Estas funções são uma forma simples e importante para proteger dados empresariais armazenados nestes dispositivos, no email ou o OneDrive.

Para obter mais informações sobre estas ações, consulte [disponíveis ações remotas](#available-remote-actions). 



## <a name="case-studies"></a>Estudos de caso

A firma de consultoria global Avanade utiliza regularmente ações remotas para gerir os dispositivos utilizados pelos seus 30 000 funcionários. Num [mensagem de blogue recentes](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), CIO da Avanade indicado:

> *Nosso win imediata de ter a funcionalidade do Intune foi a capacidade de repor remotamente o Windows numa máquina. Isso é importante para nós para máquinas perdidas ou roubadas, que são mais comuns em nossa força de trabalho altamente móvel. * 
>  *Essa é uma funcionalidade que caso contrário, teríamos que para criar e manter um pacote personalizado do ConfigMgr.*

Para obter mais informações sobre como utilizar estas ações remotas, consulte [ações do dispositivo disponíveis](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposta de valor

Quando um dispositivo do Configuration Manager está cogerido, ele adiciona imediatamente essas funções que o Configuration Manager não tem nativamente. Agora, pode agora fazer qualquer ação remota, que é suportada pelo Intune. 

Com a cogestão, os dispositivos do Configuration Manager estão agora assim como qualquer outro dispositivo gerido pelo Intune. Por exemplo, eles têm uma presença completa na cloud, e pode contatá-las, desde que eles têm acesso à internet. Pode fazer todas essas ações sem realizar quaisquer passos adicionais para além de ativar a cogestão.

Uma vez que o processo de inscrição automática é transparente ao usuário, não há nenhum impacto sobre a sua produtividade. O usuário não precisa de fazer nada.


### <a name="available-remote-actions"></a>Ações remotas disponíveis

Utilize estas ações remotas do Intune uma vez que [ativar a cogestão](/sccm/comanage/how-to-enable) no Configuration Manager.

#### <a name="remove-devices"></a>Remover dispositivos
- **Extinguir**: Esta ação remove dados e aplicações geridas (quando aplicável), definições e email perfis atribuídos a esse dispositivo. O dispositivo, em seguida, é removido da gestão do Intune. Este processo ocorre a próxima ação de extinção do tempo o dispositivo for registado e recebe a ligação remota. A função de extinção mantém os dados pessoais do utilizador no dispositivo.  

- **Apagar**: Esta ação restaura as predefinições de fábrica do dispositivo. Se escolher a opção para **manter a conta de utilizador e estado de inscrição**, em seguida, os dados de utilizador são mantidos. Caso contrário, a unidade é apagada em segurança.  

- **Delete**: Se quiser remover dispositivos do Intune no portal do Azure, eliminá-los a partir do painel de dispositivo específico. Da próxima vez que o dispositivo verifica, ele remove quaisquer dados organizacionais armazenados nele.  

Para obter mais informações, consulte [remover dispositivos através de eliminação de dados, extinguir ou anular a inscrição do dispositivo manualmente](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Eliminação seletiva
<!--SCCMDocs issue 973--> Ao escolher uma **eliminação seletiva de aplicações**, ele remove dados da aplicação da empresa sem remover dados pessoais. Utilize esta ação quando um dispositivo é considerado como perdido ou roubado. 

Para obter mais informações, consulte [como eliminar apenas dados empresariais de aplicações geridas pelo Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>Sincronização
O **sincronização** ação de dispositivo força o dispositivo selecionado a dar entrada imediatamente no Intune. Quando um dispositivo dá entrada, recebe imediatamente todas as ações ou políticas pendentes que atribuiu a ele.

Esta funcionalidade pode ajudá-lo a validar e resolver problemas de políticas que atribuiu, sem aguardar o próximo check-in agendado imediatamente.

Para obter mais informações, consulte [sincronizar dispositivos para obter as mais recentes políticas e ações com o Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Reiniciar
O **reiniciar** ação de dispositivo faz com que o dispositivo optar por reiniciar. Esta ação é útil quando existe um reinício pendente, mas o utilizador não está disponível para fazê-lo.

Para obter mais informações, consulte [reiniciar remotamente dispositivos com o Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Começar do zero
O **começar do zero** ação de dispositivo remove todas as aplicações instaladas num dispositivo com o Windows 10, versão 1703 ou posterior. Começar do zero ajuda a remover aplicações pré-instaladas (OEM) que normalmente são instaladas com um novo dispositivo.

Se optar por não manter os dados de utilizador, o dispositivo restaura o estado de out-of-box. Ele anular a inscrição no Azure AD e do MDM.

Se o ter predeterminados padrões relacionados à qual as aplicações devem ser no dispositivo, em seguida, esta ação elimina os que não satisfazem os critérios.

Para obter mais informações, consulte [utilização começar do zero para repor dispositivos Windows 10 com o Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Controlo remoto
Dispositivos geridos pelo Intune podem ser administrados remotamente usando [TeamViewer](https://www.teamviewer.com/). O TeamViewer é um programa de terceiros que adquira separadamente.

Para obter mais informações, consulte [utilização TeamViewer para administrar remotamente dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurar

Além do controlo remoto através do TeamViewer, para começar a utilizar estas ações remotas de dispositivos no Intune, nenhuma configuração adicional é necessária após [ativar a cogestão](/sccm/comanage/how-to-enable).

Para obter mais informações sobre como utilizar o TeamViewer para o controlo remoto, consulte [utilização TeamViewer para administrar remotamente dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

