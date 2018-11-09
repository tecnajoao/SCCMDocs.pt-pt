---
title: Cogestão para os dispositivos com Windows 10
titleSuffix: Configuration Manager
description: Saiba como ao mesmo tempo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 1791217e22e2bcc6d5fd2603abee3aaced816afe
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223743"
---
# <a name="co-management-for-windows-10-devices"></a>Cogestão para os dispositivos com Windows 10    

Com as atualizações anteriores do Windows 10, já pode participar num dispositivo Windows 10 para o local do Active Directory (AD) e com base na cloud do Azure AD ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, usufrui cogestão essa melhoria. Permite-lhe gerir em simultâneo dispositivos do Windows 10 versão 1709 através do Configuration Manager e o Intune. <!-- 1350871 -->


## <a name="why-co-management"></a>Por que motivo cogestão?

Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que eles gerenciam dispositivos móveis com um custo mais baixo e simplificado, a solução baseada na cloud. No entanto, a efetuar a transição da gestão tradicional para a gestão moderna pode ser um desafio.  


## <a name="what-is-co-management"></a>O que é a cogestão?

A cogestão permite-lhe ao mesmo tempo gerir dispositivos Windows 10 através do Configuration Manager e o Intune. É uma solução que fornece uma ponte entre o tradicional para a gestão moderna e dá-lhe um caminho para fazer a transição de forma faseada.


## <a name="benefits"></a>Benefícios 

Uso de imediato as seguintes funcionalidades do Intune:  
 
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

 Existem dois caminhos principais para entrar em contacto cogestão:  

   - O Configuration Manager Aprovisiona cogestão: Inscrever os dispositivos do Azure Windows 10 associados a um AD que já são clientes do Configuration Manager no Intune.  

   - Intune aprovisionado: Para dispositivos que já estão inscritos no Intune, instalar o cliente do Configuration Manager para atingir um Estado de cogestão. 


### <a name="configuration-manager"></a>Configuration Manager

 -  Atualize para o Configuration Manager versão 1710 ou posterior.


### <a name="azure-active-directory"></a>O Azure Active Directory

 - Dispositivos Windows 10 têm de ser associados ao Azure AD. Eles podem ser qualquer um dos seguintes tipos:  

     - [Azure híbrido associado ao AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup), em que o dispositivo é associado ao Active Directory no local e registado com o Azure Active Directory.

     - Azure AD associado apenas. (Este tipo é por vezes referido como "cloud associados a um domínio")<!--SCCMDocs issue 605-->

 - [Ativar a inscrição automática do Windows 10](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="intune"></a>Intune

 - [Como configurar a subscrição do Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [configurar o Intune](/intune/setup-steps)  

 - [Iniciar a migração do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a cogestão. No entanto, pode começar a migrar utilizadores para o Intune autónomo e, em seguida, ativar os dispositivos Windows 10 associados para a cogestão. Para obter mais informações sobre a migração para o Intune autónomo, consulte [iniciar a migração da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Ativar a cogestão 

 > [!Important]  
 > A partir da versão 1802, para ativar a cogestão, sua conta de utilizador administrativo no Configuration Manager tem de ser um **administrador total** com **todos os** âmbitos de segurança. Para obter mais informações, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó. Clique em **configurar cogestão** na faixa de opções para abrir o **Assistente de ativação da cogestão**. 
   
1. Sobre o **subscrição** página, clique em **sessão**. Inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.  

    > [!Tip]   
    > Certifique-se de que a conta utilizada para iniciar sessão no seu inquilino tem uma licença do Intune atribuída, caso contrário, ele falhará com a mensagem de erro "O utilizador não reconhecido".  

2. Sobre o **ativação** página, selecione seu **a inscrição automática no Intune** definição. Copie a linha de comandos para dispositivos já inscritos no Intune, se necessário.  

    > [!Note]  
    > A partir da versão 1806, a inscrição automática não é imediata para todos os clientes. Este comportamento ajuda a escala de inscrição melhor para ambientes de grandes dimensões. O Configuration Manager a aleatorização de inscrição com base no número de clientes. Por exemplo, se o ambiente tiver 100.000 clientes, quando habilitar essa configuração, inscrição ocorre ao longo de vários dias.<!--1358003-->  

3. Sobre o **cargas de trabalho** página, para cada carga de trabalho, escolher o grupo de dispositivos para mover-se através de gestão com o Intune.  

4. Sobre o **teste** , selecione uma coleção de dispositivos para ser o **coleção de projetos-piloto**. Verifique se o **resumo** e conclua o assistente.  


### <a name="upgrade-windows-10-client"></a>Atualizar o cliente do Windows 10

- Atualizar para o [Windows 10, versão 1709 (também conhecido como o Fall Creators Update) e posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)


### <a name="configure-workloads-to-switch-to-intune"></a>Configurar cargas de trabalho para mudar para o Intune 

O [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) artigo mostra-lhe como mudar cargas de trabalho específicas do Configuration Manager para o Intune. O artigo tem também instruções sobre como alterar os grupos de dispositivos para os quais as cargas de trabalho são transferidas.

#### <a name="compliance-policies"></a>Políticas de conformidade 
Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para ser considerado conforme pelas políticas de acesso condicional. Também utilize políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter detalhes, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### <a name="windows-update-policies"></a>Políticas de atualização do Windows
Atualização do Windows para políticas de empresas permitem-lhe configurar políticas de diferimento de atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update para empresas. Para obter detalhes, consulte [configurar o Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### <a name="resource-access-policies"></a>Políticas de acesso de recursos
Políticas de acesso de recurso configurar VPN, Wi-Fi, e-mail e as definições do certificado em dispositivos. Para obter detalhes, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

#### <a name="endpoint-protection"></a>Endpoint Protection
A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection pode ser transitada para Intune. Para obter mais informações, consulte [Endpoint Protection do Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10) <!-- 1357365 --> e [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### <a name="device-configuration"></a>Configuração do dispositivo
A partir do Configuration Manager 1806, a carga de trabalho de configuração do dispositivo pode ser transferida para Intune. Para obter mais informações, consulte [criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) e [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Aplicações de clique-e-Use do Office
A partir do Configuration Manager 1806, a carga de trabalho do Office 365 pode ser transferida para o Intune. Para obter mais informações, consulte [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### <a name="mobile-apps"></a>Aplicações móveis
A partir do Configuration Manager versão 1806, a carga de trabalho de aplicações móveis pode ser transferida para o Intune. Esta funcionalidade é uma funcionalidade de pré-lançamento. Para ativá-la, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software.<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalar o cliente do Configuration Manager para os dispositivos inscritos no Intune

Quando os dispositivos Windows 10 inscritos no Intune, instalar o cliente de Configuration Manager em dispositivos [usando um específico da linha de comandos](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) para preparar os clientes para a cogestão. Em seguida, ativar a cogestão da consola do Configuration Manager para mover as cargas de trabalho específicas para o Intune para dispositivos específicos do Windows 10.
Para dispositivos Windows 10 que ainda não estejam inscritos no Intune, utilize a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, utilize [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar o fora da caixa de experiência de configuração inicial (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.

Ao utilizar o Intune para instalar o cliente do Configuration Manager, ativar uma [gateway de gestão da nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager.



## <a name="monitor-co-management"></a>Monitor de cogestão

[O dashboard de cogestão](/sccm/core/clients/manage/co-management-dashboard) ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.



## <a name="next-steps"></a>Passos seguintes

[Preparar os dispositivos com Windows 10 para a cogestão](co-management-prepare.md)
