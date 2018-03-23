---
title: Preparar os dispositivos Windows 10 para gestão conjunta
description: Saiba como preparar os dispositivos Windows 10 para gestão conjunta.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 61aef0351e32ef6cf31911a8dfd27e86de82f38c
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar os dispositivos Windows 10 para gestão conjunta
Pode ativar a gestão conjunta em dispositivos Windows 10 que estejam associados ao AD e o Azure AD e inscritos no Intune e um cliente no Configuration Manager. Para novos dispositivos Windows 10 e para os dispositivos já inscritos no Intune, antes de instalar o cliente do Configuration Manager podem ser conjuntamente geridos. Para dispositivos Windows 10 que já estão a clientes do Configuration Manager, pode inscrever dispositivos com o Intune e ativar a gestão conjunta na consola do Configuration Manager.

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não suportam gestão conjunta.

## <a name="command-line-to-install-configuration-manager-client"></a>Linha de comandos para instalar o cliente do Configuration Manager
Crie uma aplicação nos dispositivos do Intune para Windows 10 que já não são clientes do Configuration Manager. Quando cria a aplicação nas secções seguintes, utilize a seguinte linha de comandos:

ccmsetup.msi CCMSETUPCMD = "/ mp:&#60;*URL de ponto final a autenticação mútua de gateway de gestão de nuvem*&#62;/ CCMHOSTNAME =&#60;*URL de ponto final a autenticação mútua de gateway de gestão de nuvem* &#62;SMSSiteCode =&#60;*Sitecode* &#62; SMSMP = https:&#47;/&#60;*FQDN do MP* &#62; AADTENANTID =&#60;*ID de inquilino do AAD*  &#62; AADTENANTNAME =&#60;*nome do inquilino* &#62; AADCLIENTAPPID =&#60;*AppID do servidor para a integração do AAD* &#62; AADRESOURCEURI = https:&#47;/&#60;*ID de recurso*&#62;"

Por exemplo, se tiver os seguintes valores:

- **URL de ponto final a autenticação mútua de gateway de gestão de nuvem**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilize o **MutualAuthPath** valor o **vProxy_Roles** vista SQL para o **URL de ponto final a autenticação mútua de gateway de gestão de nuvem** valor.

- **FQDN do ponto de gestão (MP)**: sccmmp.corp.contoso.com    
- **Sitecode**: PS1    
- **ID de inquilino do Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome de inquilino do Azure AD**: contoso    
- **ID de aplicação de cliente do Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI de ID de recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Utilize o **IdentifierUri** valor encontrado no **vSMS_AAD_Application_Ex** vista SQL para o **URI de ID de recurso do AAD** valor.

Pretende utilizar a seguinte linha de comandos:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
> Pode encontrar os parâmetros da linha de comandos para o seu site, utilizando os seguintes passos:     
> 1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**.  
> 2. No separador início, no grupo de gerir, escolha **configurar a gestão conjunta** para abrir o Assistente de integração de gestão conjunta.    
> 3. Na página de subscrição, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.    
> 4. Na página de ativação, clique em **cópia** no **dispositivos inscritos no Intune** secção para copiar a linha de comandos para a área de transferência e, em seguida, guarde a linha de comandos para utilizar o procedimento para criar a aplicação.  
> 5. Clique em **Cancelar** para sair do assistente.

> [!Important]    
> Se personalizar a linha de comandos para instalar o cliente do Configuration Manager, certifique-se de que a linha de comandos não pode exceder 1024 carateres. Quando a linha de comandos é superior a 1024 carateres, a instalação de cliente falhar.


## <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para dispositivos Windows 10 novo, pode utilizar o serviço de Autopilot configurar Escalamento de experiência de caixa, que inclui a associar o dispositivo para o AD e o Azure AD, bem como a inscrição do dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.  
1. Ative AutoPilot para novos dispositivos Windows 10. Para obter mais informações, consulte [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > A partir de versão 1802, utilize o Configuration Manager para recolher e comunicar as informações do dispositivo necessárias para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, identificador de produto do Windows e um identificador de hardware. Na consola do Configuration Manager, **monitorização** área de trabalho, expanda o **relatórios** nó, expanda **relatórios**e selecione o **Hardware - geral**  nós. Executar o novo relatório, **informações de dispositivo do Windows AutoPilot** e ver os resultados. No Visualizador de relatórios, clique o **exportar** ícone e selecione o **CSV (delimitado por vírgulas)** opção. Depois de guardar o ficheiro, carrega os dados para a Microsoft Store para empresas e Education. Para obter mais informações, consulte [adicionar dispositivos no Microsoft Store para empresas e as educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter mais informações, consulte [dispositivos Windows inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que pretende gerir conjuntamente. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 que não estão inscritos no Intune ou um cliente do Configuration Manager
Para dispositivos Windows 10 que não estão inscritos no Intune ou que têm o cliente do Configuration Manager, pode utilizar a inscrição automática para inscrever o dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.
1. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter mais informações, consulte [dispositivos Windows inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que pretende gerir conjuntamente. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 inscritos no Intune
Para dispositivos Windows 10 que já estejam inscritos no Intune, crie uma aplicação no Intune para implementar o cliente do Configuration Manager. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## <a name="next-steps"></a>Passos seguintes
[Mudar as cargas de trabalho do Configuration Manager para o Intune](co-management-switch-workloads.md)