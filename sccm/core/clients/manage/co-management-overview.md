---
title: Cogestão para dispositivos Windows 10
titleSuffix: Configuration Manager
description: Saiba como ao mesmo tempo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 3f29d2bb2fa1660b127be38f1e40396878aa29b1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383587"
---
# <a name="co-management-for-windows-10-devices"></a>Cogestão para dispositivos Windows 10    
 Com as atualizações anteriores do Windows 10, já pode participar num dispositivo Windows 10 para o local do Active Directory (AD) e com base na cloud do Azure AD ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, cogestão tira partido deste melhoramento e permite-lhe gerir em simultâneo os dispositivos do Windows 10 versão 1709 através do Configuration Manager e o Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>Por que motivo cogestão?
Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que eles gerenciam dispositivos móveis com um custo mais baixo e simplificado, a solução baseada na cloud. No entanto, a efetuar a transição da gestão tradicional para a gestão moderna pode ser um desafio.  
## <a name="what-is-co-management"></a>O que é a cogestão?
A cogestão permite-lhe ao mesmo tempo gerir dispositivos Windows 10 através do Configuration Manager e o Intune. É uma solução que fornece uma ponte entre o tradicional para a gestão moderna e dá-lhe um caminho para fazer a transição de forma faseada.

## <a name="benefits"></a>Benefícios 
- Uso imediato de funcionalidades do Intune 
    - Ações remotas
        - [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Eliminação seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
        - [Começar do zero](https://docs.microsoft.com/intune/device-fresh-start)
    - Orquestração com o Intune para as cargas de trabalho seguintes:
        - [Políticas de conformidade](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Políticas de acesso de recursos](https://docs.microsoft.com/intune/device-profiles)
        - [Políticas de atualização do Windows](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Proteção de ponto final](https://docs.microsoft.com/intune/endpoint-protection-windows-10), começando na versão 1802 do Gestor de configuração. <!-- 1357365 -->
        - [Configuração do dispositivo](https://docs.microsoft.com/intune/device-profile-create), começando no Configuration Manager 1806. <!-- 1357903 -->
        - [Aplicações do Office Clique-e-use](https://docs.microsoft.com/intune/apps-add-office365), começando no Configuration Manager 1806 <!--1357841-->
        - [Aplicações móveis](https://docs.microsoft.com/intune/app-management), começando no Configuration Manager 1806 como uma funcionalidade de pré-lançamento. <!--1357892-->

## <a name="how-to-configure-co-management"></a>Como configurar cogestão
Existem dois caminhos principais para entrar em contacto cogestão. Um caminho é aprovisionado cogestão, onde os dispositivos Windows 10 geridos pelo Configuration Manager e o Azure AD híbrido associado ao se inscrever no Intune do Configuration Manager. O outro caminho é de dispositivos do Intune aprovisionado que estão inscritos no Intune e, em seguida, instalados com o cliente do Configuration Manager atingir um Estado de cogestão.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Atualize para o Configuration Manager versão 1710 ou posterior.


### <a name="azure-active-directory"></a>**O Azure Active Directory**
  - [Azure AD híbrido associou](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (associados ao AD e o Azure AD).
  - [Ative a inscrição automática do Windows 10.](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Como configurar a subscrição do Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [configurar o Intune](/intune/setup-steps)  
 - [Iniciar a migração do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

> [!Note]  
> Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a cogestão. No entanto, pode começar a migrar utilizadores para o Intune autónomo e, em seguida, ativar os dispositivos Windows 10 associados para a cogestão. Para obter mais informações sobre a migração para o Intune autónomo, consulte [iniciar a migração da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Ativar a cogestão 
 Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**. Escolher **configurar cogestão** a partir do friso para abrir o **Assistente de ativação de cogestão** 
   
1. Sobre o **subscrição** página, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**. Certifique-se de que a conta utilizada para iniciar sessão no seu inquilino tem uma licença do Intune atribuída, caso contrário, ele falhará com a mensagem de erro "O utilizador não reconhecido".   
2. Na **ativação** página, selecione seu **a inscrição automática no Intune** definição. Copie a linha de comandos para dispositivos já inscritos no Intune, se necessário. 
3. Sobre o **cargas de trabalho** página, para cada carga de trabalho, escolher o grupo de dispositivos para mover-se através de gestão com o Intune.
4. Na **transição** , selecione uma coleção de dispositivos para ser o **coleção de projetos-piloto**. Verifique se o **resumo** e conclua o assistente. 

### <a name="upgrade-windows-10-client"></a>Atualizar o cliente do Windows 10
- Atualizar para o [Windows 10, versão 1709 (também conhecido como o Fall Creators Update) e posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Configurar cargas de trabalho para mudar para o Intune 
O [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) artigo mostra-lhe como mudar cargas de trabalho específicas do Configuration Manager para o Intune. O artigo tem também instruções sobre como alterar os grupos de dispositivos para os quais as cargas de trabalho são transferidas.

- **Políticas de conformidade:** Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para ser considerado conforme pelas políticas de acesso condicional. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter detalhes, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Políticas de atualização do Windows:** Atualização do Windows para políticas de empresas permitem-lhe configurar políticas de diferimento de atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update para empresas. Para obter detalhes, consulte [configurar o Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Políticas de acesso de recursos:** Políticas de acesso de recurso configurar VPN, Wi-Fi, e-mail e as definições do certificado em dispositivos. Para obter detalhes, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection pode ser transitada para Intune. Para obter mais informações, consulte [Endpoint Protection do Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10) <!-- 1357365 --> e [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)

- **Configuração do dispositivo** a partir do Configuration Manager 1806, a carga de trabalho de configuração do dispositivo pode ser transitada para o Intune. Para obter mais informações, consulte [criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) e [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

- **Aplicações de clique-e-Use do Office:** A partir do Configuration Manager 1806, a carga de trabalho do Office 365 pode ser transferida para o Intune. Para obter mais informações, consulte [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

- **Aplicações móveis:** A partir do Configuration Manager versão 1806, a carga de trabalho de aplicações móveis pode ser transferida para o Intune. Esta é a funcionalidade de pré-lançamento. Para ativá-la, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software.<!--1357892-->

### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalar o cliente do Configuration Manager para os dispositivos inscritos no Intune
Quando os dispositivos Windows 10 inscritos no Intune, pode instalar o cliente do Configuration Manager nos dispositivos ([usando um argumento da linha de comandos específico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) para preparar os clientes para a cogestão. Em seguida, ativar a cogestão da consola do Configuration Manager para mover as cargas de trabalho específicas para o Intune para dispositivos específicos do Windows 10.
Para dispositivos Windows 10 que ainda não estejam inscritos no Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, pode utilizar [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar o fora da caixa de experiência de configuração inicial (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.
 - Ativar [Gateway de gestão da nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (apenas ao utilizar o Intune para instalar o cliente do Configuration Manager).

## <a name="monitor-co-management"></a>Monitor de cogestão
[O dashboard de cogestão](/sccm/core/clients/manage/co-management-dashboard) ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.


## <a name="next-steps"></a>Passos seguintes
[Preparar os dispositivos com Windows 10 para a cogestão](co-management-prepare.md)
