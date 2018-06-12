---
title: Configurar a gestão de dispositivos Android híbrida com o Microsoft Intune
titleSuffix: Configuration Manager
description: Prepare para gerir dispositivos móveis Android com o Configuration Manager e o Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f833a28a22e4b3ffd2c8fc237effec94e26e69e8
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814261"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbrida do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo ajuda-o a ativar a inscrição híbrida do Android e Android para dispositivos de trabalho. Em seguida, pode utilizar a configuração do Configuration Manager para gerir os dispositivos através de uma subscrição do Microsoft Intune configurado. A partir do Google Play, os utilizadores podem transferir a aplicação do portal da empresa para Android que permite inscrever Android (incluindo Samsung KNOX Standard) e Android, para dispositivos de trabalho.

Com o Configuration Manager pode gerir as definições de compatibilidade, eliminar ou eliminar os dispositivos Android, implementar aplicações e recolher inventário de hardware e software. Sem a aplicação Portal da empresa Android instalada no dispositivo, não tem capacidades de gestão, como definições de inventário e compatibilidade, mas ainda pode implementar aplicações em dispositivos Android.  



## <a name="enable-android-enrollment"></a>Ativar a inscrição de dispositivos Android  
Os passos seguintes permitem gerir dispositivos Android sem um perfil de trabalho (ou seja, inscrição "Android clássico") do Configuration Manager.

1. Antes de poder configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).  
2. Na consola do Configuration Manager no **administração** área de trabalho, escolha **descrição geral** > **serviços em nuvem** > **subscrição do Microsoft Intune** e escolha a sua subscrição do Intune.  
3. No **home page** separador o **subscrição** grupo, escolha **configurar plataformas** > **Android**.  
4. No **propriedades de subscrição do Microsoft Intune** diálogo caixa, escolha o **Android** separador e verifique o **ativar inscrição Android** caixa. Pode optar por **bloco pessoal dispositivos pertencentes à empresa** para limitar a inscrição para [predeclared dispositivos](predeclare-devices-with-hardware-id.md).

 Depois da configurar, terá de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.



## <a name="enable-android-for-work-enrollment"></a>Ativar Android para a inscrição de trabalho
Os passos seguintes permitem gerir dispositivos Android com um perfil de trabalho do Configuration Manager.

1. [Criar uma conta do Google](https://accounts.google.com/SignUp) para utilizar como Android para a conta de administrador de trabalho. Em alternativa, inicie sessão com a conta associada Android todas as tarefas de gestão de trabalho para este inquilino Intune. Esta conta pode ser uma conta do Google que é partilhada entre os administradores que gerem os dispositivos Android. Esta conta é a conta do Google pela sua organização para gerir e publicar aplicações na Play para a consola de trabalho. Pode utilizar esta conta para aprovar aplicações na Play para o arquivo de trabalho, por isso, manter controlar do nome da conta e palavra-passe.
2. Ative a inscrição de dispositivos Android através do enlace a conta do Google para o inquilino do Intune que é gerido no Configuration Manager:
   1. Na consola do Configuration Manager no **administração** área de trabalho, escolha **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune** e escolha a sua subscrição do Intune.
   2. No **home page** separador o **subscrição** grupo, escolha **configurar plataformas** > **Android para trabalho**.
   3. Na caixa de diálogo, escolha **configurar Android para o trabalho na consola do Intune**. Abre a consola do Intune no seu browser.
   4. Utilize as credenciais de administrador do Intune para iniciar sessão no Intune no portal do Azure.
   5. Clique em **geridas do Google Play**. 
       1. Selecione **concordo** para conceder a permissão da Microsoft para [enviar informações de utilizador e dispositivo para o Google](/intune/data-intune-sends-to-google).
       2. Selecione **iniciar Google ligar agora** para abrir o Android da Google Play para o Web site de trabalho. O Web site abre num novo separador no seu browser.
       3. Da Google-na página sessão, introduza a conta do Google do passo 1.
       4. Forneça o nome da sua empresa para **nome da organização**. Para **fornecedor de gestão (EMM) do Enterprise mobility**, "Microsoft Intune" deve ser apresentado. 
       5. Concorda com o Android contrato de trabalho e, em seguida, escolha **confirmar**. O pedido será processado.

   6. Da Google-na página sessão, introduza as credenciais da conta Google do passo 1 e, em seguida, forneça as informações da sua empresa.
3. Quando voltar para o Intune no portal do Azure, aceda ao **Android para trabalho** painel de inscrição e clique em **trabalhar perfis**. Android para o trabalho está agora ativada. Tem duas opções de inscrição para Android para dispositivos de trabalho:
   - **Gerir todos os dispositivos como Android** (desativada). Todos os dispositivos Android, incluindo dispositivos que suportam o Android for Work, que são inscritos como dispositivos Android convencionais.
   - **Gerir os dispositivos suportados como Android para trabalho** (ativado). Todos os dispositivos que suportam o Android de trabalho são inscritos como Android, para dispositivos de trabalho. Todos os dispositivos Android que não suportam o Android de trabalho está inscrito como um dispositivo Android convencional.

> [!NOTE]
> Um problema conhecido impede o **gerir dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** opção de funcionar conforme esperado. Os dispositivos dos utilizadores no especificado inscrever de grupos do Azure AD como Android, em vez de Android para o trabalho. Para ativar o Android de trabalho, tem de utilizar o **gerir os dispositivos suportados como Android para trabalho** opção.


Depois da configurar, dizer aos utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

Quando o enlace é concluída, verá o nome de conta e o nome da organização do Intune no portal do Azure. Nessa altura, pode fechar ambos os browsers.

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
[< Anterior passo](create-service-connection-point.md)[passo seguinte >](set-up-additional-management.md)
