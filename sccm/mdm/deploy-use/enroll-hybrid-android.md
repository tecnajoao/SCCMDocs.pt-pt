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
ms.openlocfilehash: fb488ccfc186fcc56ea91c30b6c0319aead5208e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416984"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbrida do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo ajuda-o a ativar a inscrição de híbrida do Android e dispositivos Android for Work. Em seguida, pode utilizar o Configuration Manager para gerir os dispositivos através de uma subscrição do Microsoft Intune configurado. No Google Play, os utilizadores podem transferir a aplicação do portal da empresa para Android que permite inscrever Android (incluindo Samsung KNOX Standard) e Android para dispositivos de trabalho.

Com o Configuration Manager podem gerir as definições de compatibilidade, apagar ou extinguir dispositivos Android, implementar aplicações e recolher o inventário de software e hardware. Sem a aplicação Portal da empresa Android instalada no dispositivo, não tem as funcionalidades de gestão, como definições de inventário e de compatibilidade, mas pode continuar a implementar aplicações em dispositivos Android.  



## <a name="enable-android-enrollment"></a>Ativar a inscrição de Android  
Os passos seguintes permitem gerir dispositivos Android sem um perfil de trabalho (ou seja, a inscrição de "Android clássico") do Configuration Manager.

1. Antes de poder configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).  
2. Na consola do Configuration Manager nos **administração** área de trabalho, escolha **descrição geral** > **serviços Cloud**  >  **Subscrição do Microsoft Intune** e escolha a sua subscrição do Intune.  
3. Sobre o **home page** separador a **subscrição** de grupo, selecione **configurar plataformas** > **Android**.  
4. Na **propriedades de subscrição do Microsoft Intune** caixa de diálogo caixa, escolha a **Android** separador e verificar o **ativar inscrição Android** caixa. Pode optar por **bloquear dispositivos pessoais** para a inscrição de limite [pré-declarados pretencentes dispositivos](predeclare-devices-with-hardware-id.md).

   Depois de configurá-lo, terá de informar os utilizadores como devem inscrever os dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.



## <a name="enable-android-for-work-enrollment"></a>Ativar o Android para a inscrição de trabalho
Os passos seguintes permitem gerir dispositivos Android com um perfil de trabalho do Configuration Manager.

1. [Criar uma conta do Google](https://accounts.google.com/SignUp) para utilizar como do Android para a conta de administrador de trabalho. Em alternativa, inicie sessão com a conta associada a todos os Android para tarefas de gestão de trabalho para este inquilino do Intune. Esta conta pode ser uma conta do Google que é partilhada entre os administradores que gerir dispositivos Android. Esta conta é a conta Google que sua organização utiliza para gerir e publicar aplicações na consola Play for Work. Utilize esta conta para aprovar as aplicações na Play Store de trabalho, portanto, mantenha um registo de nome da conta e palavra-passe.
2. Ative a inscrição de dispositivos Android ao vincular a conta Google para o inquilino do Intune que é gerido no Configuration Manager:
   1. Na consola do Configuration Manager nos **administração** área de trabalho, escolha **descrição geral** > **serviços Cloud**  >  **Subscrições do Microsoft Intune** e escolha a sua subscrição do Intune.
   2. Sobre o **home page** separador o **subscrição** de grupo, selecione **configurar plataformas** > **Android for Work**.
   3. Na caixa de diálogo, escolha **configurar o Android for Work na consola do Intune**. Abre a consola do Intune no seu browser.
   4. Utilize as credenciais de administrador do Intune para iniciar sessão no Intune no portal do Azure.
   5. Clique em **Managed Google Play**. 
       1. Selecione **concordo** para conceder permissão à Microsoft para [enviar informações de utilizador e dispositivo para a Google](/intune/data-intune-sends-to-google).
       2. Selecione **inicie o Google para ligar agora** para abrir o Google Play site Android for Work. O site abre num novo separador no browser.
       3. No início de sessão página do Google, introduza a conta Google do passo 1.
       4. Forneça o nome da sua empresa **nome da organização**. Para **fornecedor de gestão (EMM) do Enterprise mobility**, "Microsoft Intune" deverá ser apresentado. 
       5. Aceitar o contrato Android for Work e, em seguida, escolha **confirmar**. O pedido será processado.

   6. Da Google início de sessão na página, introduza as credenciais da conta Google a partir do passo 1 e, em seguida, forneça as informações da sua empresa.
3. Ao retornar para o Intune no portal do Azure, vá para o **Android for Work** painel de inscrição e clique em **perfis de trabalho**. O Android for Work está agora ativado. Tem duas opções de inscrição do Android para dispositivos de trabalho:
   - **Gerir todos os dispositivos como Android** (desativado). Todos os dispositivos Android, incluindo os dispositivos que suportam o Android for Work, que são inscritos como dispositivos Android convencionais.
   - **Gerir dispositivos suportados como Android for Work** (ativado). Todos os dispositivos que suportam o Android for Work são inscritos como Android para dispositivos de trabalho. Todos os dispositivos Android que não suportam o Android for Work é inscrito como um dispositivo Android convencional.

> [!NOTE]
> Um problema conhecido impede que o **gerir dispositivos suportados para utilizadores apenas nestes grupos como Android for Work** opção de funcionar conforme esperado. Os dispositivos dos utilizadores especificado em grupos do Azure AD a inscrever como Android, em vez do Android for Work. Para ativar o Android for Work, tem de utilizar o **gerir dispositivos suportados como Android for Work** opção.


Depois de configurá-lo, indique aos utilizadores como devem inscrever os dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

Quando a ligação estiver concluída, verá o nome da conta e o nome de organização no Intune no portal do Azure. Nessa altura, pode fechar ambos os navegadores.

### <a name="enroll-an-android-for-work-device"></a>Inscrever um dispositivo Android for Work
Como os utilizadores inscrevem Android para dispositivos de trabalho é semelhante a inscrição para Android. Os utilizadores podem transferir e instalar a aplicação Portal da empresa para Android nos respetivos dispositivos móveis. A aplicação lhe pede para criar um perfil de trabalho como parte do processo de inscrição. Depois do perfil de trabalho é criado, os utilizadores tem de mudar para a versão gerida do Portal da empresa. O Portal da empresa gerido é identificado com uma pequeno mala laranja no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Faça a gestão de Android para dispositivos de trabalho
Depois de ativar o Android para inscrição de trabalho, pode efetuar as seguintes tarefas de gestão para Android para dispositivos de trabalho:
- [Aprovar aplicações](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir as definições de conformidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir perfis de e-mail](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Eliminação seletiva de perfil de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
> [< Anterior passo](create-service-connection-point.md)[passo seguinte >  ](set-up-additional-management.md)
