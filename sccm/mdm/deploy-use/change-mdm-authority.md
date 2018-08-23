---
title: Alterar a autoridade MDM
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM no Configuration Manager (híbrido) para o Intune autónomo
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 692ffb04546da4f65b2198e582999582c996fdb2
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42586351"
---
# <a name="change-your-mdm-authority"></a>Alterar a autoridade MDM

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode alterar a autoridade MDM sem ter de contactar Support da Microsoft e sem ter de anular a inscrição e inscrever novamente os seus dispositivos geridos existentes. Este artigo fornece os passos para alterar um inquilino existente do Microsoft Intune configurado na consola do Configuration Manager (híbrido) para o Intune autónomo. Quando concluir os passos neste artigo, os dispositivos são geridos pelo Microsoft Intune no [portal do Azure](https://portal.azure.com). 

Este artigo é alterar a sua autoridade MDM quando os utilizadores ainda não tiver migrado. Para alterar a sua autoridade MDM depois [migrados um subconjunto de utilizadores](migrate-hybridmdm-to-intunesa.md), consulte [alterar a sua autoridade MDM](migrate-change-mdm-authority.md).

> [!Important]  
> A partir de 13 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="key-considerations"></a>Considerações principais

Depois de alterar a autoridade de MDM, esperar que um tempo de transição de até oito horas. Pode demorar esse tempo antes do dispositivo for registado e sincroniza com o serviço. Para garantir que os dispositivos inscritos continuam a ser geridos e protegidos depois da alteração, configure as definições diretamente no Intune. Tenha em atenção as seguintes considerações:

- Dispositivos tem de ligar com o serviço após a alteração para que as definições da nova autoridade de MDM (Intune autónomo) substituam as definições existentes no dispositivo.  

- Depois de alterar a autoridade de MDM, algumas das definições básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias. Recomenda-se que configure aplicações e definições (políticas, perfis, aplicações, etc.) na nova autoridade de MDM logo que possível. Além disso, implemente as definições para os grupos de utilizadores que contêm utilizadores com dispositivos inscritos existentes. Quando um dispositivo se liga ao serviço após a alteração da autoridade de MDM, receba as novas definições da nova autoridade de MDM. Todas as políticas recentemente visadas substituem as políticas existentes no dispositivo.  

- Depois de mudar para a nova autoridade MDM, os dados de conformidade no [portal do Azure](https://portal.azure.com) pode demorar até uma semana para o relatório com precisão. No entanto, os Estados de conformidade no Azure Active Directory e no dispositivo estão corretas. O dispositivo ainda está protegido.  

- Dispositivos que não têm utilizadores associados não são migrados para a nova autoridade MDM. Este comportamento é, normalmente, quando tiver o programa de inscrição do dispositivo iOS ou em massa de cenários de inscrição. Para esses dispositivos, contacte o suporte para obter ajuda para movê-los para a nova autoridade MDM.  



## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM para o Intune autónomo

Reveja as informações seguintes para preparar a alteração para a autoridade de MDM:

- Pode demorar até oito horas para um dispositivo para ligar ao serviço depois de mudar para a nova autoridade MDM.  

- Certifique-se de que todos os utilizadores atualmente geridos de forma híbrida têm uma licença do Intune/EMS atribuída antes da alteração da autoridade de MDM. Esta licença garante que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração da autoridade de MDM. Para obter mais informações, consulte [atribuir licenças do Intune às contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).  

- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída. Confirme que a conta de utilizador administrador pode iniciar sessão no Intune antes da alteração para a autoridade de MDM. A autoridade de MDM deverá apresentar **definida para o Configuration Manager** (inquilino híbrido) no Intune no [portal do Azure](https://portal.azure.com) antes da alteração da autoridade de MDM.  

- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração da autoridade de MDM. 



## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade MDM para o Intune autónomo

O processo para alterar a autoridade de MDM para o Intune autónomo inclui os seguintes passos de alto nível:  

- Na consola do Configuration Manager, utilize o **alterar a autoridade de MDM para o Microsoft Intune** opção para remover a subscrição existente do Microsoft Intune.  

- No Intune no [portal do Azure](https://portal.azure.com), configurar e implementar novas definições e aplicações a partir da nova autoridade de MDM (Intune).  

- Os próxima vez que os dispositivos se ligar ao serviço, irá sincronizar e receber as novas definições da nova autoridade de MDM.  

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM para o Intune autónomo
1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud**e selecione o **subscrição do Microsoft Intune** nó. Elimine a sua subscrição do Intune existente.  

2. Selecione **alterar a autoridade de MDM para o Microsoft Intune**e, em seguida, clique em **próxima**.  

   ![Remover Assistente de subscrição do Microsoft Intune, a página de introdução](./media/mdm-change-delete-subscription.png)

3. Inicie sessão no inquilino do Intune que utilizou originalmente quando definiu a autoridade de MDM no Configuration Manager.  

4. Clique em **Seguinte** e conclua o assistente.  

5. A autoridade de MDM está agora definida como **Microsoft Intune**. A subscrição do Intune não apresenta no nó de subscrições do Microsoft Intune da consola do Configuration Manager.  

6. Para verificar que a autoridade de MDM é definida, siga os passos seguintes:  

    1. Inicie sessão para o [portal do Azure](https://portal.azure.com) utilizar o mesmo inquilino do Intune que utilizou anteriormente.  

    2. Escolher **todos os serviços** > **Intune** > **inscrição de dispositivos**. A autoridade de MDM é apresentada na seção superior direito **descrição geral**.  



## <a name="next-steps"></a>Passos seguintes

Após concluir a alteração na autoridade de MDM, reveja os seguintes passos:  

- Quando o serviço do Intune Deteta que a autoridade MDM de um inquilino foi alterado, envia uma mensagem de notificação para todos os dispositivos inscritos se registarem e sincronizarem com o serviço. Este comportamento é fora o check-in agendado regularmente. Portanto, depois de alterar a autoridade de MDM para o inquilino da híbrida para o Intune autónomo, todos os dispositivos que estão ligados e online se ligar ao serviço, receberão a nova autoridade MDM e são geridos pelo Intune autónomo. Não há nenhuma interrupção para o gerenciamento e proteção destes dispositivos.  

- Dispositivos que estão ligados desativado ou offline durante (ou pouco depois) a alteração da autoridade MDM de ligar e sincronizar com o serviço sob a nova autoridade MDM quando eles estão ligados e online.   

- Os utilizadores podem mudar rapidamente para a nova autoridade MDM ao iniciar manualmente um check-in do dispositivo para o serviço. Os utilizadores podem facilmente fazer esta ação ao utilizar a aplicação Portal da empresa e iniciar uma verificação de conformidade do dispositivo.  

- Para validar que as coisas estão funcionando corretamente após os dispositivos têm check-in e sincronizados com o serviço após a alteração da autoridade de MDM, procure os dispositivos com o [portal do Azure](https://portal.azure.com). Os dispositivos geridos anteriormente pelo exibição do Configuration Manager (híbrido) agora como dispositivos geridos no Intune.    

- Há um período provisório em que um dispositivo está offline durante a alteração da autoridade de MDM e do que o dispositivo é registado no serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcional durante este período provisório, os seguintes perfis permanecem no dispositivo até sete dias (ou até que o dispositivo estabelece ligação com a nova autoridade MDM e receba as novas definições que substituir o existente aqueles):  
    - Perfil de e-mail
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração  

- Para substituir as definições de antigas, certifique-se de que as novas definições que se destinam-se para substituir definições existentes têm o mesmo nome que as. Caso contrário, os dispositivos poderão ficar com políticas e perfis redundantes.    

  > [!TIP]   
  > Crie todas as definições de gestão e configurações, bem como implementações, logo após a conclusão da alteração para a autoridade de MDM. Esta ação ajuda a proteger e gerir os dispositivos ativamente durante o período provisório.   

-  Depois de alterar a autoridade de MDM, execute os seguintes passos para validar que os dispositivos foram inscritos com êxito para a nova autoridade:   

    - Inscrever um novo dispositivo  

    - Certifique-se de que os dispositivos inscritos recentemente aparecem na [portal do Azure](https://portal.azure.com).  

    - Executar uma ação, como o bloqueio remoto, a partir da [portal do Azure](https://portal.azure.com) no dispositivo. Se tiver êxito, o dispositivo está a ser gerido pela nova autoridade de MDM.  
    
- Se tiver problemas com dispositivos específicos, anular a inscrição e inscrever novamente os dispositivos. Esta ação liga-se para a nova autoridade e gerenciados mais rapidamente possível.  

- Se tiver habilitado [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) como uma mistura de inquilino e, em seguida, migrar o seu inquilino para o Intune autónomo, o Android para a definição de trabalho em restrições de inscrição pode mostrar como bloqueado, em vez de permitir. Defini-lo manualmente **permitir** para voltar a activar Android para a inscrição de trabalho.<!--512117-->  

- Depois de alterar a autoridade de MDM, o Apple VPP token e associados [aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) não são automaticamente removidos. Para limpar estas informações, siga os passos em [eliminar um token de Apple VPP](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token). Depois de concluída a operação, o site remove o token. Ele também remove do nó da aplicação de Store licenciado quaisquer metadados de aplicação para esse token.<!--SCCMDocs issue 579-->  

    Em raras ocorrências, poderá ver um erro que o site não foi possível eliminar o objeto de gestão.  

    - Se o token não estiver visível, ignore o erro  

    - Se o token ainda estiver listado, repita para eliminá-lo  

