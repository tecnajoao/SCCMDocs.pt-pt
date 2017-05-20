---
title: Atestado de estado de funcionamento | Documentos do Microsoft
description: Saiba mais sobre a funcionalidade de atestado de estado de funcionamento do dispositivo podem ser visualizada na consola do Configuration Manager.
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 23b1d24e908d04b64c3bbfa518793a44e696d468
ms.openlocfilehash: 54b3433a002b8ef29059bab04458138348f95d66
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Atestado de estado de funcionamento do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores podem ver o estado do [Atestado de Estado de Funcionamento do Dispositivo Windows 10](https://technet.microsoft.com/library/mt592023.aspx) na consola do Configuration Manager.  O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado - O antimalware de início antecipado (ELAM) protege o computador durante o arranque e antes da inicialização de controladores de terceiros. [Como ativar ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - A Encriptação de Unidade BitLocker do Windows é um software que encripta todos os dados armazenados no volume do sistema operativo do Windows.  [Como ativar o BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Arranque seguro - O arranque seguro é uma norma de segurança desenvolvida por membros do setor de PC para o ajudar a certificar-se de que o computador arranca utilizando apenas o software que seja considerada fidedigno pelo fabricante do PC. [Saiba mais sobre o Arranque Seguro](https://technet.microsoft.com/library/hh824987.aspx)  
-   Integridade do código - A integridade do código é uma funcionalidade que melhora a segurança do sistema operativo ao validar a integridade de um controlador ou ficheiro de sistema sempre que é carregado na memória. [Saiba mais sobre Integridade do Código](https://technet.microsoft.com/library/dd348642.aspx)  

Esta funcionalidade está disponível para PCs e recursos no local geridos pelo Configuration Manager e para dispositivos móveis geridos com o Microsoft Intune. Os administradores podem especificar se a comunicação é efetuada através da nuvem ou de infraestruturas no local. No local atestado de estado de funcionamento do dispositivo monitorização administrador permite monitorizar cliente PCs sem acesso à internet.

## <a name="enable-health-attestation"></a>Ativar atestado de estado de funcionamento

 **Requisitos:**  

-   Dispositivos de cliente a executar o Windows 10 versão 1607 ou versão do Windows Server 2016 1607 com [atestado de estado de funcionamento do dispositivo ativado](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
-    1.2 do TPM ou dispositivos de 2 de TPM ativado
-   Comunicação entre o agente de cliente do Configuration Manager e has.spserv.microsoft.com (porta 443) serviço de estado de funcionamento atestado (nuvem gestão) ou com o ponto de gestão ativado atestado de estado de funcionamento do dispositivo (no local)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento em computadores cliente do Configuration Manager

Utilize este procedimento para ativar a monitorização de atestado de estado de funcionamento do dispositivo para dispositivos que liga à internet.

1.  Na consola do Configuration Manager, escolha **Administração** > **Descrição geral** > **Definições de Cliente**.  Selecione o separador das definições **Agente do Computador** .  
2.  Na caixa de diálogo **Predefinições** , selecione **Agente do Computador** e, em seguida, desloque para baixo para **Ativar comunicação com o Health Attestation Service**  
3.  Defina **Ativar comunicação com o Serviço de Atestado de Estado de Funcionamento** para **Sim**e, em seguida, clique em **OK**.  
4. As coleções de dispositivos que devem comunicar o estado de funcionamento do dispositivo de destino.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento no local em computadores cliente do Configuration Manager
Utilize este procedimento para ativar a monitorização de atestado de estado de funcionamento do dispositivo para dispositivos no local que não ligam à internet.

Iniciando com o Configuration Manager 1702, o URL de serviço do atestado de estado de funcionamento do dispositivo no local pode ser configurado no ponto de gestão para suportar dispositivos cliente sem acesso à internet.

1. Na consola do Configuration Manager, navegue **administração** > **descrição geral** > **configuração do Site** > **Sites**.
2. Com o botão direito do site primário ou secundário com o ponto de gestão que suporte para clientes de atestado de estado de funcionamento de dispositivos no local e selecione **configurar componentes do site** > **ponto de gestão**. O **propriedades do componente de ponto de gestão** é aberta a página.
3. No **opções avançadas** separador, selecione **adicionar** e especifique um URL de serviço de atestado de estado de funcionamento de dispositivos de válido no local. Pode adicionar vários URLs. Se forem especificados várias URLs no local, os clientes recebem o conjunto completo e escolher qual utilizar aleatoriamente.
4.  Na consola do Configuration Manager, escolha **Administração** > **Descrição geral** > **Definições de Cliente**.  Selecione o separador das definições **Agente do Computador** .  
5.  No **predefinições** caixa de diálogo, selecione **agente do computador** e, em seguida, desloque para baixo para **utilização no local serviço de integridade de Attestaion**e definido para **Sim**.
6. As coleções de dispositivos que devem comunicar o estado de funcionamento do dispositivo com as definições de agente de cliente para ativar a denúncia de atestado de estado de funcionamento do dispositivo de destino.

Pode também **editar** ou **remover** os URLs do serviço de atestado de estado de funcionamento do dispositivo.

> [!NOTE]
> Se utilizou o atestado de estado de funcionamento do dispositivo antes de atualizar para o Configuration Manager 1702, os URLs no local especificado nas definições de agente do cliente é pré-preencher nas propriedades do ponto de gestão durante a atualização. Os clientes no local irão continuar a utilizar o URL especificado nas definições do agente cliente até que sejam atualizados. Em seguida, mudarão para um dos URLs especificados no ponto de gestão.

## <a name="monitor-device-health-attestation"></a>Monitorizar atestado de estado de funcionamento do dispositivo

1.  Para visualizar a vista do atestado de estado de funcionamento, na consola do Configuration Manager, vá para a área de trabalho de **Monitorização** , clique no nó **Segurança** e, em seguida, clique em **Atestado de Estado de Funcionamento**.  
2.  O Atestado de Estado de Funcionamento é apresentado.  

O Atestado de Estado de Funcionamento do Dispositivo apresenta o seguinte:  

-   **Atestado do Estado de Funcionamento** - Mostra a partilha de dispositivos com os estados de conformidade, não conformidade, erro e desconhecidos  
-   **Atestado de Estado de Funcionamento de Relatórios de Dispositivos** - Mostra a percentagem de dispositivos que comunicam o estado de Atestado de Estado de Funcionamento  
-   **Dispositivos Não Conformes por Tipo de Cliente** - Mostra a partilha de dispositivos móveis e computadores não compatíveis  
-   **Definições Principais do Atestado de Estado de Funcionamento em Falta** - Mostra o número de dispositivos em falta na definição de atestado de estado de funcionamento, listados por definição

Estado do cliente atestado de estado de funcionamento do dispositivo pode ser utilizado para definir as regras de acesso condicional nas políticas de conformidade para dispositivos geridos pelo Configuration Manager com o Microsoft Intune. Para mais detalhes, veja [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
