---
title: "Configurar a gestão de dispositivos Android híbrida com o Microsoft Intune"
titleSuffix: Configuration Manager
description: "Prepare para gerir dispositivos móveis Android com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: "9"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 4b638b0325aa5f75d60a008ea60531a818ec76c2
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/01/2017
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbrida do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico ajuda-o ao administrador ativar a inscrição híbrida do Android e Android para dispositivos de trabalho. O administrador de TI, em seguida, pode utilizar o System Center Configuration Manager para gerir os dispositivos através de uma subscrição do Microsoft Intune configurado. A partir do Google Play, os utilizadores podem transferir a aplicação do portal da empresa para Android que permite inscrever Android (incluindo Samsung KNOX Standard) e Android, para dispositivos de trabalho.

Como administrador do Configuration Manager, pode gerir as definições de compatibilidade, apagar ou eliminar os dispositivos Android, implementar aplicações e recolher inventário de hardware e software. Sem a aplicação Portal da empresa Android instalada no dispositivo, não tem capacidades de gestão, como definições de inventário e compatibilidade, mas ainda pode implementar aplicações em dispositivos Android.  

## <a name="enable-android-enrollment"></a>Ativar a inscrição de dispositivos Android  
Os passos seguintes permitem gerir dispositivos Android sem um perfil de trabalho (ou seja, inscrição "Android clássico") do Configuration Manager.

1. Antes de poder configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).  
2. Na consola do Configuration Manager no **administração** área de trabalho, escolha **descrição geral** > **serviços em nuvem** > **subscrição do Microsoft Intune** e escolha a sua subscrição do Intune.  
3. No **home page** separador o **subscrição** grupo, escolha **configurar plataformas** > **Android**.  
4. No **propriedades de subscrição do Microsoft Intune** diálogo caixa, escolha o **Android** separador e verifique o **ativar inscrição Android** caixa. Pode optar por **bloco pessoal dispositivos pertencentes à empresa** para limitar a inscrição para [predeclared dispositivos](predeclare-devices-with-hardware-id.md).

 Depois da configurar, terá de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Ativar Android para a inscrição de trabalho
Os passos seguintes permitem gerir dispositivos Android com um perfil de trabalho do Configuration Manager.

1. Crie uma conta do Google https://accounts.google.com/SignUp para utilizar como Android para a conta de administrador de trabalho. Em alternativa, inicie sessão com a conta associada Android todas as tarefas de gestão de trabalho para este inquilino Intune. Esta conta pode ser uma conta do Google que é partilhada entre os administradores que gerem os dispositivos Android. Esta é a conta do Google pela sua organização para gerir e publicar aplicações na Play para a consola de trabalho. Pode utilizar esta conta para aprovar aplicações na Play para o arquivo de trabalho, por isso, manter controlar do nome da conta e palavra-passe.
2. Ative a inscrição de dispositivos Android através do enlace a conta do Google para o inquilino do Intune que é gerido no Configuration Manager:
   1. Na consola do Configuration Manager no **administração** área de trabalho, escolha **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune** e escolha a sua subscrição do Intune.
   2. No **home page** separador o **subscrição** grupo, escolha **configurar plataformas** > **Android para trabalho**.
   3. Na caixa de diálogo, escolha **configurar Android para o trabalho na consola do Intune**. Abre a consola do Intune no seu browser.
   4. Utilize as credenciais de administrador do Intune para iniciar sessão portal do Intune.
   5. Escolha **configurar** para abrir o Android da Google Play para o Web site de trabalho.
   6. Na sessão do Google na página, introduza as credenciais da conta Google do passo 1 e, em seguida, forneça as informações da sua empresa.
3. Quando regressar ao portal do Intune, o Android para o trabalho está ativado e tem três opções de inscrição para Android para dispositivos de trabalho:
   - **Gerir todos os dispositivos como Android** (desativada). Todos os dispositivos Android, incluindo dispositivos que suportam o Android for Work, que são inscritos como dispositivos Android convencionais.
   - **Gerir os dispositivos suportados como Android para trabalho** (ativado). Todos os dispositivos que suportam o Android de trabalho são inscritos como Android, para dispositivos de trabalho. Todos os dispositivos Android que não suporta Android para o trabalho está inscrito como um dispositivo Android convencional.
   - **Gerir os dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** (ativado para apenas alguns grupos). Permite destino Android para gestão de trabalho para um conjunto limitado de utilizadores. Os dispositivos que suportam o Android de trabalho são inscritos como Android para dispositivos de trabalho apenas quando os membros de grupos selecionados inscrevê-los. Todos os outros dispositivos inscritos como dispositivos Android.

> [!NOTE]
> Um problema conhecido impede o **gerir dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** opção de funcionar conforme esperado. Os dispositivos dos utilizadores no especificado inscrever de grupos do Azure AD como Android, em vez de Android para o trabalho. Para ativar o Android de trabalho, tem de utilizar o **gerir todos os dispositivos suportados como Android para trabalho** opção.


Depois da configurar, terá de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

Quando o enlace é concluída, pode ver o nome de conta e o nome da organização no portal do Intune. Nessa altura, pode fechar ambos os browsers.

### <a name="enroll-an-android-for-work-device"></a>Inscrever um Android para dispositivos de trabalho
Como inscrever os seus utilizadores Android para dispositivos de trabalho é semelhante a inscrição para Android. Os utilizadores podem transferir e instalar a aplicação Portal da empresa para Android nos respetivos dispositivos móveis. A aplicação irá solicitar-lhes criar um perfil de trabalho como parte do processo de inscrição. Depois de criar o perfil de trabalho, os utilizadores devem mudar para a versão gerida do Portal da empresa. O Portal da empresa geridos é marcado com um pequeno briefcase laranja no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Gerir Android para dispositivos de trabalho
Depois de ativar Android para a inscrição de trabalho, pode realizar as seguintes tarefas de gestão para Android para dispositivos de trabalho:
- [Aprovar aplicações](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir as definições de conformidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir perfis de e-mail](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Eliminar o perfil de trabalho de forma seletiva](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Anterior passo](create-service-connection-point.md)[passo seguinte >  ](set-up-additional-management.md)
