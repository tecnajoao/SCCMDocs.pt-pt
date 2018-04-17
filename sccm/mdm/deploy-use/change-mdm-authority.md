---
title: Alterar a autoridade de MDM
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para o Intune autónomo
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/11/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 88380c0db38b1226734d9e60266beb9c702e5a1c
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="change-your-mdm-authority"></a>Alterar a autoridade de MDM
Pode alterar a autoridade de MDM, sem ter de contactar o Support da Microsoft e sem ter de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Este artigo fornece os passos para alterar um inquilino do Microsoft Intune existente configurado na consola do Configuration Manager (híbrido) para o Intune autónomo. Quando concluir os passos neste artigo, os dispositivos são geridos pelo Microsoft Intune a [portal do Azure](https://portal.azure.com). 

> [!Note]    
> Se pretender alterar um inquilino do Microsoft Intune existente, com o conjunto de autoridade MDM ao Intune, para o Configuration Manager (híbrido), consulte o artigo [alterar a autoridade de MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Este artigo é para alterar a sua autoridade MDM não tenha sido anteriormente migrados os utilizadores. Para alterar a autoridade de MDM, depois de ter [migrado um subconjunto de utilizadores](migrate-hybridmdm-to-intunesa.md), consulte [alterar a autoridade de MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Considerações-chave
Depois de alterar a autoridade de MDM, espere uma hora de transição de até oito horas. Pode demorar muito neste antes do dispositivo ser registado e sincroniza com o serviço. Para garantir que os dispositivos inscritos continuam a ser geridos e protegido após a alteração, configure definições diretamente no Intune. Tenha em atenção as seguintes considerações:
- Dispositivos tem de ligar com o serviço após a alteração, para que as definições da autoridade de MDM novo (Intune autónomo) substituem as definições existentes no dispositivo.
- Depois de alterar a autoridade de MDM, algumas das definições básicas (por exemplo, perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias. Recomenda-se que configura as aplicações e definições (políticas, perfis, aplicações, etc.) na autoridade MDM novo logo que possível. Além disso, implemente as definições para os grupos de utilizadores que contêm os utilizadores que possuem dispositivos já inscritos. Quando um dispositivo se liga ao serviço após a alteração na autoridade de MDM, este recebe novas definições da autoridade MDM de novo. Quaisquer políticas recentemente visadas substituem as políticas existentes no dispositivo.
- Depois de alterar para a nova autoridade de MDM, os dados de conformidade no [portal do Azure](https://portal.azure.com) pode demorar até uma semana para reportar com precisão. No entanto, os Estados de compatibilidade no Azure Active Directory e no dispositivo estão corretos. O dispositivo ainda está a ser protegido.
- Dispositivos que não tem utilizadores associados não são migrados para a autoridade de MDM de novo. Este comportamento é, normalmente, quando tiver iOS Device Enrollment Program ou em massa cenários de inscrição. Para os dispositivos, contacte o suporte para obter ajuda para movê-los para a autoridade de MDM de novo.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM ao Intune autónomo
Reveja as informações seguintes para se preparar para a alteração à autoridade de MDM:
- Pode demorar até oito horas para um dispositivo para ligar ao serviço depois de alterar para a autoridade de MDM de novo.
- Certifique-se de que todos os utilizadores que sejam atualmente geridos pelo híbrida ter uma licença do Intune/EMS atribuída antes da alteração na autoridade de MDM. Esta licença assegura que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração na autoridade de MDM. Para obter mais informações, consulte [licenças do Intune atribuir às suas contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída. Certifique-se de que a conta de utilizador administrador pode iniciar sessão no Intune antes da alteração para a autoridade de MDM. A autoridade de MDM deve apresentar **definida para o Configuration Manager** (inquilino híbrida) no Intune no [portal do Azure](https://portal.azure.com) antes da alteração na autoridade de MDM.
- Não deverá haver nenhum impacto considerável aos utilizadores finais durante a alteração na autoridade de MDM. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM ao Intune autónomo
O processo para alterar a autoridade de MDM ao Intune autónomo inclui os seguintes passos de alto nível:  
- Na consola do Configuration Manager, utilize o **autoridade de MDM de alteração para o Microsoft Intune** opção para remover a subscrição existente do Microsoft Intune.
- No Intune no [portal do Azure](https://portal.azure.com), configurar e implementar as novas definições e aplicações a partir da autoridade de MDM novo (Intune).
- Os dispositivos de hora seguintes ligam ao serviço, irá sincronizar e receber as novas definições da autoridade MDM de novo.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM ao Intune autónomo
1. Na consola do Configuration Manager, vá para **administração** &gt; **descrição geral** &gt; **serviços em nuvem** &gt; **subscrição do Microsoft Intune**e eliminar a sua subscrição do Intune existente.
2. Selecione **autoridade de MDM de alteração para o Microsoft Intune**e, em seguida, clique em **seguinte**.
   ![Remover Assistente de subscrição do Microsoft Intune, a página de introdução](./media/mdm-change-delete-subscription.png)
3. Iniciar sessão para o inquilino do Intune que utilizou originalmente quando definir a autoridade de MDM no Configuration Manager.
4. Clique em **Seguinte** e conclua o assistente.
5. A autoridade de MDM está agora definida como **Microsoft Intune**. A subscrição do Intune não apresentar no nó de subscrições do Microsoft Intune da consola do Configuration Manager. 
6. Para verificar se a autoridade MDM é definida, siga os passos seguintes: uma. Iniciar sessão para o [portal do Azure](https://portal.azure.com) utilizar o mesmo inquilino do Intune que utilizou anteriormente. 
    b. Escolha **mais serviços** > **monitorização + gestão** > **Intune** > **deinscriçãodedispositivos**. A autoridade de MDM é apresentada na secção superior direito a **descrição geral** painel. 

## <a name="next-steps"></a>Passos seguintes
Depois de concluída a alteração na autoridade de MDM, reveja os seguintes passos:
- Quando o serviço Intune Deteta que a autoridade de MDM de um inquilino foi alterado, que envia uma mensagem de notificação para todos os dispositivos inscritos para registar e sincronizar com o serviço. Este comportamento está fora da agendadas regularmente dar entrada no. Por conseguinte, depois de alterar a autoridade de MDM para o inquilino do híbrida ao Intune autónomo, todos os dispositivos que estão ligados à corrente no e online estabelecer ligação com o serviço, recebem a autoridade de MDM novo e são geridos pelo Intune autónomo. Não há sem interrupções da gestão e a proteção destes dispositivos.
- Dispositivos que estão ligados desativado ou offline durante a (ou pouco depois) a alteração na autoridade de MDM ligar e sincronizar com o serviço sob a autoridade de MDM novo quando estão ligados à corrente no e online.  
- Os utilizadores podem alterar rapidamente para a autoridade de MDM novo iniciando manualmente um verificação-in do dispositivo para o serviço. Os utilizadores podem facilmente efetuar esta ação através da aplicação Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
- Para validar que coisas estão a funcionar corretamente depois de dispositivos têm deu entrada em e sincronizados com o serviço após a alteração na autoridade de MDM, procure os dispositivos com o [portal do Azure](https://portal.azure.com). Os dispositivos que foram anteriormente geridos pelo Configuration Manager (híbrido) apresentação de agora como dispositivos geridos no Intune.    
- Não há um período provisória quando um dispositivo estiver offline durante a alteração na autoridade de MDM e quando verifica a que o dispositivo para o serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcionais durante este período intermédio, os seguintes perfis permanecem no dispositivo até sete dias (ou até que o dispositivo estabelece ligação com a autoridade de MDM novo e recebe novas definições de substituir a existente aqueles):
    - Perfil de e-mail
    - Perfil da VPN
    - Perfil de certificado
    - Perfil Wi-Fi
    - Perfis de configuração
- Para substituir as definições antigas, certifique-se de que as novas definições que foram concebidas para substituir as definições existentes têm o mesmo nome que as anteriores. Caso contrário, os dispositivos poderão acaba por ficar com as políticas e perfis redundantes.    

  > [!TIP]   
  > Como melhor prática, deve criar todas as definições de gestão e configurações, bem como implementações, imediatamente após a alteração à autoridade de MDM foi concluída. Isto ajuda a garantir que os dispositivos estão protegidos e geridos ativamente durante o período de intermédio.   
-  Depois de alterar a autoridade de MDM, execute os seguintes passos para validar que a novos dispositivos são inscritos com êxito para a autoridade de novo:   
    - Inscrever um dispositivo novo
    - Certifique-se os dispositivos inscritos recentemente aparecem no [portal do Azure](https://portal.azure.com).
    - Efetuar uma ação, tal como o bloqueio remoto desde o [portal do Azure](https://portal.azure.com) no dispositivo. Se for bem sucedida, o dispositivo está a ser gerido pela autoridade MDM de novo.
- Se tiver problemas com dispositivos específicos, anular a inscrição e inscrever-se novamente os dispositivos. Esta ação liga à autoridade de novo e geridas como rapidamente quanto possível.
- Se ativou [Android para trabalho](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) como uma versão híbrida de inquilino e, em seguida, migrar o seu inquilino ao Intune autónomo, o Android para a definição de trabalho em restrições de inscrição pode mostrar como bloqueadas em vez de permitir. Defina manualmente **permitir** para reativar o Android para a inscrição de trabalho.<!--512117-->