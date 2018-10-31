---
title: Preparar o Windows 10 para a cogestão
titleSuffix: Configuration Manager
description: Saiba como preparar os dispositivos Windows 10 para a cogestão.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 9aab4273129e6a3032d7e85d2545e6abc5b616c4
ms.sourcegitcommit: 8dd9199bfe8e27f62e9df307f1c6ac58a3b81717
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/30/2018
ms.locfileid: "50237161"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar os dispositivos com Windows 10 para a cogestão
Pode ativar a cogestão em dispositivos Windows 10 que estão associados ao AD e o Azure AD e inscritos no Microsoft Intune e um cliente no Configuration Manager. Para novos dispositivos Windows 10 e para dispositivos já inscritos no Intune, instale o cliente de Configuration Manager antes de poderem ser cogeridos. Para dispositivos Windows 10 que já são clientes do Configuration Manager, pode inscrever os dispositivos com o Intune e ativar a cogestão na consola do Configuration Manager.

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não suportam a cogestão.



## <a name="prerequisites"></a>Pré-requisitos

Tem de ter os seguintes pré-requisitos em vigor antes de poder ativar a cogestão. Existem pré-requisitos gerais e pré-requisitos diferentes para dispositivos com o cliente do Configuration Manager e dispositivos que não têm o cliente instalado.


### <a name="general-prerequisites"></a>Pré-requisitos gerais

Seguem-se pré-requisitos gerais para a ativar a cogestão:  

- Configuration Manager versão 1710 ou posterior  

    - A partir do Configuration Manager versão 1806, pode ligar várias instâncias do Configuration Manager para um único inquilino do Intune. <!--1357944-->  

- [Site integrado com o Azure AD para gestão na cloud](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- Licença do Intune ou do EMS para todos os utilizadores  

- [Inscrição automática do Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) ativada  

- Subscrição do Intune e a autoridade de MDM no Intune definido como **Intune**.  

    - Se estiver a utilizar [misto autoridade](/sccm/mdm/deploy-use/migrate-mixed-authority), primeiro concluir a migração para o Intune autónomo. Em seguida, defina a autoridade de MDM ao Intune antes de configurar cogestão.<!--SCCMDocs issue #797-->


> [!Note]  
> Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a cogestão. No entanto, pode começar a migrar utilizadores para o Intune autónomo e, em seguida, ativar os dispositivos Windows 10 associados para a cogestão. Para obter mais informações sobre a migração para o Intune autónomo, consulte [iniciar a migração da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### <a name="prerequisite-azure-resource-manager-roles"></a>Funções de pré-requisitos do Azure Resource Manager
<!--SCCMDocs issue #667--> Para obter mais informações sobre as funções do Azure, consulte [compreender as diferentes funções](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).
|Action|Função necessária|
|----|----|
|Configurar um gateway de gestão da cloud|Gestor de subscrições do Azure|
|Configurar um ponto de distribuição de nuvem|Gestor de subscrições do Azure|
|Criar aplicações do Azure Active Directory a partir da consola do Configuration Manager|Administrador Global do Azure Active Directory|
|Importar aplicações de cliente e servidor do Azure na consola do Configuration Manager| Administrador do Configuration Manager, não existem funções do Azure adicionais necessárias.|
|Configurar cogestão através do Assistente de cogestão| Direitos de utilizador de Active Directory do Azure, juntamente com a ser um administrador do Configuration Manager com todos os direitos de âmbito. 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos com o cliente do Configuration Manager

- Windows 10, versão 1709 ou posterior  

- [Azure híbrido associado ao AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (associados ao AD e o Azure AD) ou do Azure AD associado a um só (este tipo é por vezes referido como "cloud associados a um domínio").


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos sem o cliente do Configuration Manager

- Windows 10, versão 1709 ou posterior  

- [Gateway de gestão da nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (ao utilizar o Intune para instalar o cliente do Configuration Manager)  


> [!IMPORTANT]
> Dispositivos móveis Windows 10 não suportam a cogestão.



## <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager

Crie uma aplicação no Intune para dispositivos Windows 10 que ainda não clientes do Configuration Manager. Ao criar a aplicação nas próximas seções, utilize a seguinte linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line"></a>Linha de comandos de exemplo
Se o ter os seguintes valores:

- **URL de ponto final a autenticação mútua de gateway de gestão de cloud**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!Note]    
   >Utilize o **MutualAuthPath** valor no **vProxy_Roles** vista SQL para o **URL de ponto final a autenticação mútua de gateway de gestão de cloud** valor.  

- **FQDN do ponto de gestão (MP)**: `mp1.contoso.com`    
- **Sitecode**: `PS1`    
- **ID de inquilino do Azure AD**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **ID de aplicação de cliente do Azure AD**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **URI de ID de recurso do AAD**: `ConfigMgrServer`    

  > [!Note]    
  > Utilize o **IdentifierUri** valor encontrado no **vSMS_AAD_Application_Ex** vista SQL para o **URI de ID de recurso do AAD** valor.  

Em seguida, utilize a seguinte linha de comando:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> A partir da versão 1806, menos propriedades da linha de comandos são agora necessária.  

- As seguintes propriedades de linha de comandos são necessários em todos os cenários:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- As seguintes propriedades são necessárias quando utilizar o Azure AD para autenticação de cliente em vez de certificados de autenticação de clientes baseada na PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- A propriedade seguinte é necessária se o cliente forem se mover para a intranet:  
    - SMSMP  

O exemplo seguinte inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).


> [!Tip]
> Encontre os parâmetros da linha de comandos para o seu site com os seguintes passos:     
> 
> 1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó.  
> 
> 2. No Friso, selecione **configurar cogestão** para abrir o Assistente de ativação da cogestão. (Se já tiver configurado a cogestão, selecione **propriedades**. Em seguida, avance para o passo 4.)    
> 
> 3. Na página de subscrição, selecione **sessão**. Inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.    
> 
> 4. Na página de ativação, selecione **cópia** para copiar a linha de comandos para a área de transferência. Em seguida, guarde a linha de comandos para utilizar o procedimento para criar a aplicação.  
> 
> 5. Clique em **Cancelar** para sair do assistente.  

> [!Important]    
> Se personalizar a linha de comandos para instalar o cliente do Configuration Manager, certifique-se de que a linha de comandos não exceder os 1024 carateres. Quando a linha de comandos é superior a 1024 carateres, a instalação de cliente falhar.



## <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10

Para novos dispositivos Windows 10, pode utilizar o serviço de Autopilot para configurar o fora de experiência, que inclui a associar o dispositivo ao AD e o Azure AD, bem como a inscrição do dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.  

1. Ative o AutoPilot para novos dispositivos Windows 10. Para obter detalhes, consulte [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > A partir da versão 1802, utilize o Configuration Manager para recolher e comunicar as informações do dispositivo necessárias para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, o identificador do produto Windows e um identificador de hardware. Na consola do Configuration Manager, **monitorização** área de trabalho, expanda o **Reporting** nó, expanda **relatórios**e selecione o **Hardware - geral**  nó. Executar o novo relatório **informações de dispositivo do Windows AutoPilot** e ver os resultados. No Visualizador de relatórios clique a **exportar** ícone e selecione o **CSV (delimitado por vírgulas)** opção. Depois de guardar o ficheiro, carregue os dados para a Microsoft Store para empresas e Education. Para obter mais informações, consulte [adicionar dispositivos no Microsoft Store para empresas e educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter detalhes, consulte [dispositivos do Windows de inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

3. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que deseja gerenciar em conjunto. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   



## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não inscritos no Intune ou um cliente do Configuration Manager

Para dispositivos Windows 10 que não estão inscritos no Intune ou que têm o cliente do Configuration Manager, pode utilizar a inscrição automática para inscrever o dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.

1. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter detalhes, consulte [dispositivos do Windows de inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

2. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que deseja gerenciar em conjunto. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).



## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 inscritos no Intune

Para dispositivos Windows 10 que já tenham sido inscritos no Intune, crie uma aplicação no Intune para implementar o cliente do Configuration Manager. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  



## <a name="next-steps"></a>Passos seguintes

[Mudar as cargas de trabalho do Configuration Manager para o Intune](co-management-switch-workloads.md)
