---
title: "Configurar a gestão de dispositivos Android híbrida com o System Center Configuration Manager e o Microsoft Intune | Documentos do Microsoft"
description: "Prepare para gerir dispositivos móveis Android com o Configuration Manager e do Intune."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 27a92dc1c3710ff55f0b145386319dda371533d9
ms.openlocfilehash: 0e93cd55ce49afb6395dcbe758c933bf509dd367
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbrida do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico ajuda o ativar a inscrição de híbrido do Android e Android para dispositivos de trabalho do administrador de TI. O administrador de TI pode então utilizar o System Center Configuration Manager para gerir os dispositivos através de uma subscrição do Microsoft Intune configurado. A partir do Google Play, os utilizadores podem transferir a aplicação do portal da empresa Android que permite inscrever Android (incluindo Samsung KNOX Standard) e o Android, para dispositivos de trabalho. 

Como administrador do Configuration Manager, pode gerir as definições de compatibilidade, apagar ou extinguir dispositivos Android, implementar aplicações e recolher inventário de hardware e software. Se a aplicação do portal da empresa para Android não está instalada em dispositivos Android, em seguida, não terá todas as funcionalidades de gestão (como definições de inventário e de conformidade), mas ainda pode implementar aplicações em dispositivos Android.  

## <a name="enable-android-enrollment"></a>Ativar a inscrição do Android  
Os seguintes passos permitem gerir dispositivos Android sem um perfil de trabalho (ou seja, a inscrição de "Android clássico") do Configuration Manager.

1. Antes de poder configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [híbrida configuração MDM](setup-hybrid-mdm.md).  
2. Na consola do Configuration Manager no **administração** área de trabalho, selecione **descrição geral** > **serviços em nuvem** > **subscrição do Windows Intune** e escolha a sua subscrição do Intune.  
3. No **base** separador o **subscrição** grupo, selecione **configurar platformas** > **Android**.  
4. No **as propriedades de subscrição do Microsoft Intune** diálogo caixa, selecione o **Android** separador e verifique o **inscrição do Android ativar** caixa.  

 Depois da configurar, tem de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Ativar Android para a inscrição de trabalho
Os seguintes passos permitem gerir dispositivos Android sem um perfil de trabalho (ou seja, a inscrição de "Android clássico") do Configuration Manager.

1. Crie uma conta do Google https://accounts.google.com/SignUp a utilizar como seu Android para a conta de administrador de trabalho. Em alternativa, inicie sessão com a conta que será associada a todos os Android trabalho em tarefas de gestão para este inquilino do Intune. Isto pode ser uma conta do Google que é partilhada entre os administradores a gerir dispositivos Android. Esta é a conta do Google que a organização utiliza para gerir e publicar aplicações no Play para a consola de trabalho. Irá utilizar esta conta para aprovar aplicações na Play para o arquivo de trabalho, por isso, manter um registo de nome de conta e palavra-passe.
2. Ative a inscrição do Android por enlace a conta do Google para o inquilino do Intune, que é gerido no Configuration Manager:
   1. Na consola do Configuration Manager no **administração** área de trabalho, selecione **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune** e escolha a sua subscrição do Intune.
   2. No **base** separador o **subscrição** grupo, selecione **configurar platformas** > **Android para trabalhar**.
   3. Na caixa de diálogo, selecione **configurar Android para trabalhar na consola do Intune**. Abre a consola do Intune no seu browser.
   4. Utilize as credenciais de administrador do Intune para iniciar sessão no portal do Intune.
   5. Escolher **configurar** para abrir o Google Play Android para o Web site de trabalho.
   6. No página de sessão da Google, introduza as credenciais da conta Google do passo 1 e, em seguida, forneça as informações da empresa.
3. Quando regressar ao portal do Intune, Android para o trabalho está ativado e tem três opções de inscrição para Android para dispositivos de trabalho:
   - **Gerir todos os dispositivos como Android** (desativado). Todos os dispositivos Android, incluindo dispositivos que suportem Android para trabalhar, estão inscritos como dispositivos Android convencionais.
   - **Gerir os dispositivos suportados como Android para trabalhar** (ativado). Todos os dispositivos que suportem Android para trabalhar são inscritos como Android, para dispositivos de trabalho. Todos os dispositivos Android que não suporta Android para o trabalho está inscrito como um dispositivo Android convencional.
   - **Gerir os dispositivos suportados para os utilizadores apenas destes grupos como Android para trabalhar** (ativado para apenas alguns grupos). Esta definição permite aos destino Android para gestão de trabalho para um conjunto limitado de utilizadores. Os dispositivos que suportem Android para trabalhar são inscritos como Android para dispositivos de trabalho apenas quando os membros de grupos selecionados inscrevam-los. Todos os outros dispositivos são inscritos como dispositivos Android.

> [!NOTE]
> Um problema conhecido impede o **gerir dispositivos suportados para os utilizadores apenas destes grupos como Android para trabalhar** opção trabalhem conforme esperado. Os dispositivos dos utilizadores no Azure AD especificado grupos irão inscrever como Android, em vez de Android para trabalhar. Para ativar Android para trabalhar, tem de utilizar o **gerir todos os dispositivos suportados como Android para trabalhar** opção.


Depois da configurar, tem de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

Verá o nome de conta e o nome da organização no portal do Intune quando o enlace estiver concluído. Nesse momento, pode fechar ambos os browsers.

### <a name="enroll-an-android-for-work-device"></a>Inscrever Android para o dispositivo de trabalho
Como os utilizadores inscrevem Android para dispositivos de trabalho é semelhante a inscrição para Android. Os utilizadores podem transferir e instalar a aplicação de Portal da empresa para Android nos respetivos dispositivos móveis. O app solicita-lhe-los para criar um perfil de trabalho como parte do processo de inscrição. Depois de criar o perfil de trabalho, os utilizadores tem de mudar para a versão do Portal da empresa gerida. O Portal da empresa gerido está etiquetado com um briefcase laranja pequena no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Gerir Android para dispositivos de trabalho
Depois de ativar Android para a inscrição de trabalho, pode efetuar as seguintes tarefas de gestão para Android para dispositivos de trabalho:
- [Aprovar aplicações](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir definições de compatibilidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir perfis de e-mail](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Eliminação seletiva o perfil de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Passo anterior](create-service-connection-point.md)[junto passo >  ](set-up-additional-management.md)

