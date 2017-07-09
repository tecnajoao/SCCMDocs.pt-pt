---
title: "Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Prepare para gerenciar dispositivos móveis Android com o Configuration Manager e o Intune."
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
ms.sourcegitcommit: 86620254897aa9a775dc433de7010b5814c1ec3e
ms.openlocfilehash: af6fa2dfae5549e89c46d05d0cef1e24342558f9
ms.contentlocale: pt-pt
ms.lasthandoff: 07/06/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbrida do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Este tópico ajuda o administrador de TI habilitar o registro de híbrido do Android e Android para dispositivos de trabalho. O administrador de TI, em seguida, pode usar o System Center Configuration Manager para gerenciar os dispositivos por meio de uma assinatura Microsoft Intune configurado. No Google Play, os usuários podem baixar o aplicativo do portal da empresa Android que permite que eles registrem Android (incluindo Samsung KNOX Standard) e Android para dispositivos de trabalho.

Como um administrador do Configuration Manager, você pode gerenciar as configurações de conformidade, apagar ou excluir dispositivos Android, implantar aplicativos e coletar inventários de hardware e software. Sem o aplicativo de Portal da empresa Android instalado no dispositivo, você não tem recursos de gerenciamento, como as configurações de inventário e de conformidade, mas você ainda pode implantar aplicativos para dispositivos Android.  

## <a name="enable-android-enrollment"></a>Habilitar o registro do Android  
As etapas a seguir permitem que o Configuration Manager gerenciar dispositivos Android sem um perfil de trabalho (ou seja, o registro de "Android clássico").

1. Antes de configurar o registro para qualquer plataforma, concluir os pré-requisitos e procedimentos em [MDM híbrido do programa de instalação](setup-hybrid-mdm.md).  
2. No console do Configuration Manager no **administração** espaço de trabalho, escolha **visão geral** > **serviços de nuvem** > **assinatura do Microsoft Intune** e escolha sua assinatura do Intune.  
3. No **início** guia o **assinatura** de grupo, escolha **configurar plataformas** > **Android**.  
4. No **propriedades de assinatura do Microsoft Intune** caixa de diálogo caixa, escolha o **Android** guia e verifique o **habilitar registro do Android** caixa.  

 Depois de você configurá-lo, você precisa permitir que os usuários saibam como registrar seus dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Habilitar o Android para o registro de trabalho
As etapas a seguir permitem que o Configuration Manager gerenciar dispositivos Android com um perfil de trabalho.

1. Crie uma conta do Google no https://accounts.google.com/SignUp para usar como o Android para a conta de administrador do trabalho. Ou entre com a conta associada com Android todas as tarefas de gerenciamento de trabalho para este locatário do Intune. Essa conta pode ser uma conta do Google que é compartilhada entre os administradores que gerenciam dispositivos Android. Essa é a conta do Google que sua organização usa para gerenciar e publicar aplicativos no Play para o console do trabalho. Você pode usar essa conta para aprovar aplicativos Play para armazenamento de trabalho, para manter o controle do nome de conta e senha.
2. Habilite registro do Android associando-se a conta do Google para o locatário do Intune gerenciado no Configuration Manager:
   1. No console do Configuration Manager no **administração** espaço de trabalho, escolha **visão geral** > **serviços de nuvem** > **assinaturas do Microsoft Intune** e escolha sua assinatura do Intune.
   2. No **início** guia o **assinatura** de grupo, escolha **configurar plataformas** > **Android para trabalho**.
   3. Na caixa de diálogo, escolha **configurar Android para o trabalho no console do Intune**. O console do Intune será aberto no navegador da web.
   4. Use suas credenciais de administrador do Intune para entrar no portal do Intune.
   5. Escolha **configurar** para abrir o Android da Google Play para o site de trabalho.
   6. Na entrada do Google na página, digite as credenciais de conta do Google da etapa 1 e, em seguida, fornecer informações de sua empresa.
3. Ao retornar ao portal do Intune, Android para o trabalho está habilitado e você tem três opções de registro para o Android para dispositivos de trabalho:
   - **Gerenciar todos os dispositivos, como Android** (desabilitado). Todos os dispositivos Android, incluindo dispositivos que dão suporte ao Android para o trabalho, são registrados como dispositivos Android convencionais.
   - **Gerenciar dispositivos com suporte, como Android para o trabalho** (habilitado). Todos os dispositivos que dão suporte ao Android para o trabalho são registrados, como Android, para dispositivos de trabalho. Qualquer dispositivo Android que não dão suporte ao Android para o trabalho é registrado como um dispositivo Android convencional.
   - **Gerenciar dispositivos com suporte para os usuários somente desses grupos como Android para trabalho** (habilitadas para apenas alguns grupos). Permite que você Android para gerenciamento de trabalho a um conjunto limitado de usuários de destino. Dispositivos que dão suporte ao Android para o trabalho são registrados como Android para dispositivos de trabalho somente quando os membros dos grupos selecionados registrá-los. Todos os outros dispositivos são registrados como dispositivos Android.

> [!NOTE]
> Impede que um problema conhecido do **gerenciar dispositivos com suporte para os usuários somente desses grupos como Android para trabalho** opção funcione conforme o esperado. Os dispositivos dos usuários do registro de grupos do AD do Azure como Android, em vez de Android para o trabalho. Para habilitar o Android para o trabalho, você deve usar o **gerenciar todos os dispositivos com suporte, como Android para o trabalho** opção.


Depois de você configurá-lo, você precisa permitir que os usuários saibam como registrar seus dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

Quando a associação é concluída, você deve ver o nome da conta e o nome de organização no portal do Intune. Nesse momento, você pode fechar ambos os navegadores.

### <a name="enroll-an-android-for-work-device"></a>Registrar um Android para o dispositivo de trabalho
Como os usuários registram Android para dispositivos de trabalho é semelhante ao registro para o Android. Os usuários podem baixar e instalar o aplicativo de Portal da empresa para Android em seus dispositivos móveis. O aplicativo solicita-los para criar um perfil de trabalho como parte do processo de registro. Depois que o perfil de trabalho é criado, os usuários devem alternar para a versão gerenciada do Portal da empresa. O Portal da empresa gerenciados é marcado com uma pequena pasta laranja no canto inferior direito.

### <a name="manage-android-for-work-devices"></a>Gerenciar Android para dispositivos de trabalho
Depois de habilitar o Android para o registro de trabalho, você pode executar as seguintes tarefas de gerenciamento para o Android para dispositivos de trabalho:
- [Aprovar aplicativos](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerir as definições de conformidade](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gerenciar perfis de email](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Apagar seletivamente o perfil de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Anterior etapa](create-service-connection-point.md)[próxima etapa >  ](set-up-additional-management.md)

