---
title: Atestado de estado de funcionamento
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de atestado de estado de funcionamento do dispositivo podem ser visualizada na consola do Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 116c12d86c097222844e76dde877b674ca7498b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127121"
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Atestado de estado de funcionamento do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores podem ver o estado do [Atestado de Estado de Funcionamento do Dispositivo Windows 10](https://technet.microsoft.com/library/mt592023.aspx) na consola do Configuration Manager.  O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado - O antimalware de início antecipado (ELAM) protege o computador durante o arranque e antes da inicialização de controladores de terceiros. [Como ativar ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - A Encriptação de Unidade BitLocker do Windows é um software que encripta todos os dados armazenados no volume do sistema operativo do Windows.  [Como ativar o BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Arranque seguro - O arranque seguro é uma norma de segurança desenvolvida por membros do setor de PC para o ajudar a certificar-se de que o computador arranca utilizando apenas o software que seja considerada fidedigno pelo fabricante do PC. [Saiba mais sobre o Arranque Seguro](https://technet.microsoft.com/library/hh824987.aspx)  
-   Integridade do código - A integridade do código é uma funcionalidade que melhora a segurança do sistema operativo ao validar a integridade de um controlador ou ficheiro de sistema sempre que é carregado na memória. [Saiba mais sobre Integridade do Código](https://technet.microsoft.com/library/dd348642.aspx)  

Esta funcionalidade está disponível para PCs e recursos no local geridos pelo Configuration Manager e para dispositivos móveis geridos com o Microsoft Intune. Os administradores podem especificar se a comunicação é efetuada através da nuvem ou de infraestruturas no local. Atestado de estado de funcionamento do dispositivo de locais monitorização administrador ativa para monitorar PCs cliente sem acesso à internet.

## <a name="enable-health-attestation"></a>Ativar o atestado de estado de funcionamento

 **Requisitos:**  

-   Dispositivos de cliente com o Windows 10 versão 1607 ou versão 1607 do Windows Server 2016 com [atestado de estado de funcionamento do dispositivo ativada](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation).
-   TPM 1.2 ou TPM 2 ativado para dispositivos.
-   Ao utilizar a gestão na cloud, de pontos de comunicação entre o agente do cliente do Configuration Manager e o gerenciamento com *has.spserv.microsoft.com* serviço de atestado de estado de funcionamento (porta 443) (gestão na cloud). Quando no local, o cliente tem de ser capaz de comunicar com o ponto de gestão atestado de estado de funcionamento do dispositivo.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento em computadores cliente do Configuration Manager

Utilize este procedimento para ativar a monitorização de atestado de estado de funcionamento do dispositivo para dispositivos que ligam à internet.

1.  Na consola do Configuration Manager, escolha **Administração** > **Descrição geral** > **Definições de Cliente**.  Selecione o separador das definições **Agente do Computador** .  
2.  Na caixa de diálogo **Predefinições** , selecione **Agente do Computador** e, em seguida, desloque para baixo para **Ativar comunicação com o Health Attestation Service**  
3.  Defina **Ativar comunicação com o Serviço de Atestado de Estado de Funcionamento** para **Sim**e, em seguida, clique em **OK**.  
4. As coleções de dispositivos devem comunicar o estado de funcionamento do dispositivo de destino.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento no local em computadores cliente do Configuration Manager
Utilize este procedimento para ativar a monitorização de atestado de estado de funcionamento do dispositivo para dispositivos no local que não ligam à internet.

A partir do Configuration Manager 1702, o URL de serviço do atestado de estado de funcionamento do dispositivo no local pode ser configurado no ponto de gestão para suportar dispositivos de cliente sem acesso à internet.

1. Na consola do Configuration Manager, navegue até **Administration** > **descrição geral** > **configuração do Site**  >   **Sites**.
2. Com o botão direito do site primário ou secundário com o ponto de gestão que suportam clientes de atestado de estado de funcionamento de dispositivos no local e selecione **configurar componentes do site** > **ponto de gestão**. O **propriedades do componente de ponto de gestão** é aberta a página.
3. Sobre o **opções avançadas** separador, selecione **Add** e especifique um URL de serviço do atestado de estado de funcionamento do dispositivo no local válido. Pode adicionar várias URLs. Se forem especificadas várias URLs no local, os clientes recebem o conjunto completo e aleatoriamente escolher quais pode ser utilizado.
4.  Na consola do Configuration Manager, escolha **Administração** > **Descrição geral** > **Definições de Cliente**.  Selecione o separador das definições **Agente do Computador** .  
5.  Desloque para baixo até **ativar comunicação com o serviço de atestado de estado de funcionamento**e definido como **Sim**.
7.  Clique nas **utilização no local serviço de integridade de Attestaion** opção e definido como **Sim**.
8. As coleções de dispositivos devem comunicar o estado de funcionamento do dispositivo com as definições de agente de cliente para permitir relatórios de atestado de estado de funcionamento do dispositivo de destino.

Também pode **edite** ou **remover** URLs do serviço de atestado de estado de funcionamento de dispositivo.

> [!NOTE]
> Se tiver utilizado o atestado de estado de funcionamento do dispositivo antes de atualizar para o Configuration Manager 1702, os URLs no local especificado nas definições de agente do cliente é preencher previamente nas propriedades do ponto de gestão durante a atualização. Clientes no local irão continuar a utilizar o URL especificado nas definições do agente de cliente até que sejam atualizados. Eles, em seguida, muda para um dos URLs especificados no ponto de gestão.

## <a name="monitor-device-health-attestation"></a>Monitorizar o atestado de estado de funcionamento do dispositivo

1.  Para visualizar a vista do atestado de estado de funcionamento, na consola do Configuration Manager, vá para a área de trabalho de **Monitorização** , clique no nó **Segurança** e, em seguida, clique em **Atestado de Estado de Funcionamento**.  
2.  O Atestado de Estado de Funcionamento é apresentado.  

O Atestado de Estado de Funcionamento do Dispositivo apresenta o seguinte:  

-   **Atestado do Estado de Funcionamento** - Mostra a partilha de dispositivos com os estados de conformidade, não conformidade, erro e desconhecidos  
-   **Atestado de Estado de Funcionamento de Relatórios de Dispositivos** - Mostra a percentagem de dispositivos que comunicam o estado de Atestado de Estado de Funcionamento  
-   **Dispositivos Não Conformes por Tipo de Cliente** - Mostra a partilha de dispositivos móveis e computadores não compatíveis  
-   **Definições Principais do Atestado de Estado de Funcionamento em Falta** - Mostra o número de dispositivos em falta na definição de atestado de estado de funcionamento, listados por definição

Estado de atestado de estado de funcionamento do dispositivo do cliente pode ser utilizado para definir regras de acesso condicional nas políticas de conformidade para dispositivos geridos pelo Configuration Manager com o Microsoft Intune. Para mais detalhes, veja [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
