---
title: Gestão conjunta para dispositivos Windows 10
titleSuffix: Configuration Manager
description: Saiba como em simultâneo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 3a667ae075ac688d4b49789ed88f858c2ff39397
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="co-management-for-windows-10-devices"></a>Gestão conjunta para dispositivos Windows 10    
 Com atualizações anteriores do Windows 10, já pode associar um dispositivo Windows 10 no local do Active Directory (AD) e baseado na nuvem do Azure AD em simultâneo (híbrido do Azure AD). A partir do Configuration Manager versão 1710, gestão conjunta tira partido deste melhoramento e permite-lhe gerir em simultâneo dispositivos do Windows 10 versão 1709 através do Configuration Manager e o Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>Por que motivo gestão conjunta?
Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que o se gerem dispositivos móveis utilizando um custo simplificado, inferior, uma solução baseada na nuvem. No entanto, efetuar a transição do gestão tradicional para gestão moderna pode ser um desafio.  
## <a name="what-is-co-management"></a>O que é gestão conjunta?
Gestão conjunta permite-lhe gerir em simultâneo dispositivos Windows 10 através do Configuration Manager e o Intune. É uma solução que fornece uma ponte de tradicional para gestão moderna e dá-lhe um caminho para fazer a transição utilizando uma abordagem faseada.

## <a name="benefits"></a>Benefícios 
- Utilização imediata de funcionalidades do Intune 
    - Ações remoto
        - [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Eliminação seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Reiniciar o dispositivo](https://docs.microsoft.com/intune/device-restart)
        - [Início de raiz](https://docs.microsoft.com/intune/device-fresh-start)
    - Orquestração com o Intune para as cargas de trabalho seguintes:
        - [Políticas de conformidade](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
        - [Políticas de Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Proteção de ponto final](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10), começando no Configuration Manager 1802. <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Como configurar a gestão conjunta
Existem dois caminhos principais para aceder à gestão conjunta. É um Gestor de configuração de gestão conjunta aprovisionada em dispositivos Windows 10 geridos pelo Configuration Manager e o Azure AD híbrido associados ser inscrito no Intune. O outro está Intune aprovisionado para dispositivos que estão inscritos no Intune e, em seguida, instalado com o alcance de cliente do Configuration Manager num Estado de gestão conjunta.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Atualize para o Configuration Manager versão 1710 ou posterior.


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [Azure AD híbrido associado](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (associado ao AD e o Azure AD).
  - [Ative a inscrição automática do Windows 10.](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Como configurar a subscrição do Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [configurar o Intune](/intune/setup-steps)  
 - [Iniciar a migração do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

> [!Note]  
> Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a gestão de conjunta. No entanto, pode começar a migrar os utilizadores ao Intune autónomo e, em seguida, ativar os dispositivos Windows 10 associados para gestão conjunta. Para obter mais informações sobre como migrar para o Intune autónomo, consulte [começar a migrar do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Ativar a gestão conjunta 
 Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**. Escolha **configurar a gestão conjunta** a partir do friso para abrir o **Assistente de ativação da gestão conjunta** 
   
1. No **subscrição** página, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.    
2. No **ativação** página, escolha o **inscrição automática no Intune** definição. Copie a linha de comandos para os dispositivos já inscritos no Intune, se necessário. 
3. No **cargas de trabalho** página, para cada carga de trabalho, escolha o grupo de dispositivos para mover para gestão com o Intune.
4. No **transição** página, selecione uma coleção de dispositivos para ser o **piloto coleção**. Certifique-se a **resumo** e conclua o assistente. 

### <a name="upgrade-windows-10-client"></a>Atualizar o cliente Windows 10
- Atualizar para [versão 1709 (também conhecido como a atualização de criadores de reversão) do Windows 10 e posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Configurar as cargas de trabalho para mudar para o Intune 
O [cargas de trabalho podem ser transitado para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) artigo mostra-lhe como mudar de cargas de trabalho específicas do Configuration Manager para o Intune. O artigo tem também instruções sobre como alterar os grupos de dispositivos para os quais as cargas de trabalho são transferidas.

- **Políticas de conformidade:** Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para serem considerados conformes pelo acesso condicional políticas. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter mais informações, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Políticas de Windows Update:** Windows Update para políticas de empresas permitem-lhe configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou atualizações de qualidade de dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Para obter mais informações, consulte [configurar o Windows Update para políticas de diferimento por empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Políticas de acesso de recursos:** Políticas de acesso a recursos configurar definições de certificado, e-mail, Wi-Fi e VPN em dispositivos. Para obter mais informações, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection pode ser transitada para o Intune. Para obter mais informações, consulte [Endpoint Protection do Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10) <!-- 1357365 --> e [cargas de trabalho podem ser transitado para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalar o cliente do Configuration Manager para os dispositivos inscritos no Intune
Quando os dispositivos Windows 10 inscritos no Intune, pode instalar o cliente do Configuration Manager nos dispositivos ([utilizando um argumento da linha de comandos específico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) para preparar os clientes para gestão conjunta. Em seguida, ativar a gestão conjunta da consola do Configuration Manager para iniciar a mover as cargas de trabalho específicas para o Intune para dispositivos Windows 10 específicos.
Para dispositivos Windows 10 que ainda não estão inscritos no Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, pode utilizar [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar o fora de caixa de experiência de primeira execução (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.
 - Ativar [Gateway de gestão de nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (apenas quando utilizar o Intune para instalar o cliente do Configuration Manager).

## <a name="monitor-co-management"></a>Gestão de coadministrador do monitor
[O dashboard de gestão conjunta](/sccm/core/clients/manage/co-management-dashboard) ajuda-o a rever máquinas que estejam conjuntamente geridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que necessitem de atenção.


## <a name="next-steps"></a>Passos seguintes
[Preparar os dispositivos com Windows 10 para a cogestão](co-management-prepare.md)
