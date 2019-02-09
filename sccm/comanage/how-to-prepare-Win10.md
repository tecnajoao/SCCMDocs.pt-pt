---
title: Gerenciar dispositivos baseados na internet em conjunto
titleSuffix: Configuration Manager
description: Saiba como preparar os dispositivos baseados na internet do Windows 10 para a cogestão.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: fcb34d46cdbe197021d2dea752f77ce3bb42af5d
ms.sourcegitcommit: 38f56f1d5803370f4262931c2dc4a532bfcf0594
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/08/2019
ms.locfileid: "55905604"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Como preparar os dispositivos baseados na internet para a cogestão

Este artigo se concentra no segundo caminho para a cogestão para novos dispositivos baseados na internet. Este cenário é quando tem novos dispositivos Windows 10 associados ao Azure AD e inscreverem-se automaticamente para o Intune. Instalar o cliente do Configuration Manager para atingir um Estado de cogestão.  



## <a name="windows-autopilot"></a>Windows Autopilot

Para novos dispositivos Windows 10, pode utilizar o serviço de Autopilot para configurar o fora de experiência inicial (OOBE). Este processo inclui a associar o dispositivo para o Azure AD e a inscrição do dispositivo no Intune.  

Para obter mais informações, consulte [descrição geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Para configurar seus dispositivos para ser automaticamente inscrever no Intune quando eles associados ao Azure AD, consulte [dispositivos do Windows de inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Recolher informações do Configuration Manager

A partir da versão 1802, utilize o Configuration Manager para recolher e comunicar as informações do dispositivo necessárias para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, o identificador do produto Windows e um identificador de hardware. É utilizado para registar o dispositivo na Microsoft Store para suportar o Windows Autopilot. 

1. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho, expanda o **Reporting** nó, expanda **relatórios**e selecione o **Hardware - Geral** nó.  

2. Execute o relatório **informações de dispositivo do Windows Autopilot**e veja os resultados.  

3. No Visualizador de relatórios, selecione o **exportar** ícone e escolha o **CSV (delimitado por vírgulas)** opção.  

4. Depois de guardar o ficheiro, carregue os dados para a Microsoft Store para empresas e Education.  

Para obter mais informações, consulte [adicionar dispositivos no Microsoft Store para empresas e educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>Autopilot para dispositivos existentes
<!--1358333-->

[Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível com o Windows 10, versão 1809 ou posterior. Esta funcionalidade permite-lhe criar uma nova imagem e aprovisionar um dispositivo Windows 7 para [modo de controlada pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma sequência de tarefas do Configuration Manager única e nativo. 



## <a name="install-the-configuration-manager-client"></a>Instalar o cliente do Configuration Manager

Para dispositivos baseados na internet no segundo caminho, terá de criar uma aplicação no Intune. Implemente esta aplicação para dispositivos Windows 10 que ainda não clientes do Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obter a linha de comandos do Configuration Manager

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó.  

2. Selecione o objeto de cogestão e, em seguida, escolha **propriedades** na faixa de opções.  

3. Sobre o **ativação** separador, copie a linha de comandos. Cole-o no bloco de notas para guardar para o processo seguinte.  

A seguinte linha de comando é um exemplo: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> A partir da versão 1806, menos propriedades da linha de comandos são agora necessária.  

- As seguintes propriedades de linha de comandos são necessários em todos os cenários:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- As seguintes propriedades são necessárias quando utilizar o Azure AD para autenticação de cliente em vez de certificados de autenticação de clientes baseada na PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Se o cliente fizer roaming para a intranet, a propriedade seguinte é necessária:  
    - SMSMP  

- Se utilizar o seu próprio certificado SSL de PKI e a CRL não é publicado na internet, o seguinte parâmetro é necessário:  
    - /noCRLCheck  
    
     Para obter mais informações, consulte [planejamento de CRL](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

O exemplo seguinte inclui todas as propriedades:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obter mais informações, consulte [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Criar a aplicação no Intune

1. Vá para o [portal do Azure](https://portal.azure.com)e, em seguida, abra a página do Intune.  

2. Selecione **aplicações de cliente** > **aplicações** > **adicionar**.  

3. Sob **outras**, selecione **aplicação de linha de negócio**.  

4. Carregar o **ccmsetup** ficheiro de pacote de aplicação. Encontrar este ficheiro na seguinte pasta no Configuration Manager do servidor do site: `<ConfigMgr installation directory>\bin\i386`.  

5. Depois da aplicação é atualizada, configure as informações da aplicação com a linha de comandos que copiou do Configuration Manager.  

> [!IMPORTANT]    
> Se personalizar esta linha de comandos, certificar-se de que não é mais de 1024 carateres de comprimento. Quando o comprimento de linha de comandos é superior a 1024 carateres, a instalação de cliente falhar.


