---
title: "Gestão conjunta para dispositivos Windows 10"
description: "Saiba como em simultâneo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 4b582d5fbd9e2e916c439b149e117f1a65da98bf
ms.sourcegitcommit: 5f4a584d4a833b0cc22bd8c47da7dd55aced97fa
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/05/2017
---
# <a name="co-management-for-windows-10-devices"></a>Gestão conjunta para dispositivos Windows 10    
<!-- 1350871 -->
Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que o se gerem dispositivos móveis utilizando um custo simplificado, inferior, uma solução baseada na nuvem. No entanto, efetuar a transição do gestão tradicional para gestão moderna pode ser um desafio. Nas atualizações anteriores do Windows 10, já pode associar um dispositivo Windows 10 no local do Active Directory (AD) e baseado na nuvem do Azure AD em simultâneo (híbrido do Azure AD). A partir do Configuration Manager versão 1710, gestão conjunta tira partido deste melhoramento e permite-lhe gerir em simultâneo Windows 10, dispositivos de 1709 (também conhecido como a atualização de criadores de reversão) versão através do Configuration Manager e o Intune. É uma solução que fornece uma ponte de tradicional para gestão moderna e dá-lhe um caminho para fazer a transição utilizando uma abordagem faseada. 

Existem dois caminhos principais para aceder à gestão conjunta.  É um Gestor de configuração de gestão conjunta aprovisionada em dispositivos Windows 10 geridos pelo Configuration Manager e o Azure AD híbrido associados ser inscrito no Intune. O outro está Intune aprovisionado para dispositivos que estão inscritos no Intune e, em seguida, instalado com o alcance de cliente do Configuration Manager num Estado de gestão conjunta.  

## <a name="prerequisites"></a>Pré-requisitos
Tem de ter os seguintes pré-requisitos no local antes de poder ativar gestão conjunta. Existem pré-requisitos gerais e pré-requisitos diferentes para dispositivos com o cliente do Configuration Manager e dispositivos que não tenham o cliente instalado.

### <a name="general-prerequisites"></a>Pré-requisitos gerais
Seguem-se pré-requisitos gerais para a ativar a gestão conjunta:  

- Configuration Manager versão 1710 ou posterior
- Azure AD
- Licença do Intune ou do EMS para todos os utilizadores
- [Inscrição automática de AD do Azure](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) ativada
- Subscrição do Intune &#40; Definido como a autoridade MDM no Intune **Intune**&#41;


   > [!Note]  
   > Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a gestão de conjunta. Se estiver interessado em migrar para o Intune autónomo, consulte o artigo [começar a migrar do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos com o cliente do Configuration Manager
- Windows 10, versão 1709 (também conhecido como a atualização de criadores de reversão) e posterior
- [Azure AD híbrido associado](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (associado a um AD e AD do Azure)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos sem o cliente do Configuration Manager
- Windows 10, versão 1709 (também conhecido como a atualização de criadores de reversão) e posterior
- [Gateway de gestão de nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (ao utilizar o Intune para instalar o cliente do Configuration Manager)

## <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho que pode mudar para o Intune
Depois de ativar a gestão conjunta, o Configuration Manager continua a gerir todas as cargas de trabalho. Quando decidir o que está pronto, pode fazer com que o Intune começar a gerir as cargas de trabalho disponíveis. Pode fazer com o Intune gerir as seguintes cargas de trabalho.   

### <a name="compliance-policies"></a>Políticas de conformidade
Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para serem considerados conformes pelo acesso condicional políticas. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter mais informações, consulte [políticas de conformidade do dispositivo](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Windows Update para as políticas de negócio
Windows Update para políticas de empresas permitem-lhe configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou atualizações de qualidade de dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Para obter mais informações, consulte [configurar o Windows Update para políticas de diferimento por empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Políticas de acesso a recursos
Políticas de acesso a recursos configurar definições de certificado, e-mail, Wi-Fi e VPN em dispositivos. Para obter mais informações, consulte [implementar perfis de acesso a recursos](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

## <a name="architectural-overview-for-co-management"></a>Descrição geral da arquitetura de gestão conjunta
O diagrama seguinte fornece uma descrição geral da arquitetura de gestão conjunta e como se enquadra no existentes infraestruturas de configuração e o Intune.

![Diagrama da arquitetura de gestão conjunta](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Cenários para ativar a gestão conjunta  
Pode ativar a gestão conjunta para ambos os dispositivos Windows 10 inscritos no Microsoft Intune e os clientes existentes do Gestor de configuração do Windows 10. Ambos os cenários resultam em dispositivos Windows 10 em simultâneo geridos pelo Configuration Manager e o Intune, bem como associado ao AD e o Azure AD.  

### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos no Intune  
Quando os dispositivos Windows 10 inscritos no Intune, pode instalar o cliente do Configuration Manager nos dispositivos (utilizando um argumento da linha de comandos específico) para preparar os clientes para gestão conjunta. Em seguida, ativar a gestão conjunta da consola do Configuration Manager para iniciar a mover as cargas de trabalho específicas para o Intune para dispositivos Windows 10 específicos.  

Para dispositivos Windows 10 que ainda não estão inscritos no Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, pode utilizar [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar o fora de caixa de experiência de primeira execução (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.  

### <a name="configuration-manager-clients"></a>Clientes do Configuration Manager
Quando tiver dispositivos Windows 10 que sejam clientes do Configuration Manager, pode inscrever estes dispositivos e ativar a gestão conjunta da consola do Configuration Manager. Informações de inquilino de acionadores de Gestor de configuração automática inscrição no Intune com base no Azure AD.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remoto disponíveis no Intune no Azure para dispositivos geridos conjuntamente
Quando um dispositivo Windows 10 está ativado para a gestão conjunta, tem as seguintes ações remotas disponíveis para o utilizador do Intune no Azure:  
- [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Eliminação seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar o dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Início de raiz](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Passos seguintes
[Preparar os dispositivos com Windows 10 para a cogestão](co-management-prepare.md)