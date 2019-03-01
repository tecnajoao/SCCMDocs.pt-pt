---
title: Alterar a sua autoridade MDM ao Intune
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM no Configuration Manager (híbrido) para o Intune autónomo.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 0bf253085adeca0d9ea62d76497eb5ebf5ce89da
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/28/2019
ms.locfileid: "57012433"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Alterar a sua autoridade MDM para o Intune autónomo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Pode alterar um inquilino existente do Microsoft Intune configurado na consola do Configuration Manager (MDM híbrida) para o Intune autónomo. Alterar a autoridade de MDM de nível de inquilino para o Intune é a fase final do processo para [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na cloud.    

> [!Important]    
> Para alterar a autoridade MDM sem primeiro migrar usuários MDM híbrida para o Intune, consulte [alterar a sua autoridade MDM](change-mdm-authority.md).

Este artigo fornece informações sobre como alterar um inquilino existente do Microsoft Intune configurado na consola do Configuration Manager (híbrido) para o Intune autónomo. Parte do princípio de que já concluiu os seguintes passos:
- Utilizar o [ferramenta de importação de dados do Intune](migrate-import-data.md) para importar objetos do Configuration Manager para o Intune. 
- [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) para se certificar de que os utilizadores e os respetivos dispositivos continuam a ser geridos depois de serem migradas.
- [Alterar a autoridade de MDM para utilizadores específicos (autoridade MDM misturadas)](migrate-mixed-authority.md) para começar a gerir dispositivos de utilizador do portal do Azure.


## <a name="users-and-devices-that-havent-been-migrated"></a>Utilizadores e dispositivos que ainda não foram migrados
Já migrados muitos usuários e testada de funcionalidades do Intune para se certificar de que as coisas estão funcionando como esperado. Tiver configurado políticas, perfis e aplicações no Intune e tiver testado exaustivamente os objetos nos dispositivos. Não deve haver nenhum novas configurações necessárias para as suas políticas ao nível do inquilino após a alteração da autoridade de MDM. No entanto, para utilizadores e dispositivos que ainda não migrados anteriormente, reveja as seguintes informações sobre o que esperar após a alteração da autoridade de MDM:    

- É provável que um tempo de transição de até oito horas antes do dispositivo for registado e sincroniza com o serviço.  

- Os dispositivos têm de se ligar o serviço após a alteração para que as definições da nova autoridade de MDM (Intune autónomo) substituam as definições existentes no dispositivo.  

- Algumas das definições básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias.  

- Dispositivos que não têm utilizadores associados não são migrados para a nova autoridade MDM. Estes dispositivos são, normalmente, com cenários para iOS do programa de inscrição ou inscrição em massa. Para mover estes dispositivos para a nova autoridade de MDM, terá de contactar o suporte para obter assistência.



## <a name="prerequisites"></a>Pré-requisitos
Reveja as seguintes informações para preparar a alteração para a autoridade de MDM:
- Tem de ter o Configuration Manager versão 1610 ou superior para ter a opção de alterar a autoridade de MDM.
- Certifique-se de atribuir uma licença do Intune/EMS para todos os utilizadores atualmente geridos de forma híbrida MDM. A licença certifica-se de que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração da autoridade de MDM. Para obter mais informações, veja [Atribuir licenças do Intune às suas contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída.

## <a name="change-the-mdm-authority-to-intune"></a>Alterar a autoridade MDM para Intune
Utilize o procedimento seguinte para alterar a autoridade de MDM de nível de inquilino para o Intune.

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **subscrição do Microsoft Intune** nó. Elimine a sua subscrição do Intune existente.  

2. Selecione **alterar a autoridade de MDM para o Microsoft Intune**e, em seguida, selecione **próxima**.

    ![Remover o diálogo de subscrição do Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Inicie sessão no inquilino do Intune que utilizou originalmente quando definiu a autoridade de MDM no Configuration Manager. Selecione **seguinte** e conclua o assistente.

    Agora é reposta a autoridade de MDM. A subscrição do Intune já não é apresentada no nó de subscrições do Microsoft Intune da consola do Configuration Manager.  

4. Inicie sessão para o [portal do Intune](https://aka.ms/IntunePortal).

5. Selecione **inscrição de dispositivos**.  

6. A inscrição de dispositivos, descrição geral, veja a **autoridade de MDM** propriedade.

   > [!Important]    
   > Não utilize a consola clássica do Intune. Iniciar sessão no Intune no portal do Azure.  

7. Confirme que a autoridade de MDM foi alterada para **Microsoft Intune**. 



## <a name="after-migration"></a>Após a migração

Após concluir a alteração na autoridade de MDM, reveja as seguintes informações:

- Os utilizadores finais não deverão sentir impactos evidentes durante a alteração da autoridade de MDM.  

- Não tem de reconfigurar as políticas ao nível do inquilino.  

- Se precisar de editar políticas ao nível do inquilino, execute esta ação do Intune no portal do Azure.  

- Se tiver problemas com dispositivos específicos, anular a inscrição e inscrever novamente os dispositivos. Esta ação obtém-los ligado para a nova autoridade e gerenciados mais rapidamente possível.


#### <a name="validate-new-device-enrollment"></a>Validar a nova inscrição de dispositivos
Depois de alterar a autoridade de MDM, utilize os seguintes passos para validar que os dispositivos foram inscritos com êxito para a nova autoridade:   
1. Inscrever um novo dispositivo
2. Certifique-se de que os dispositivos inscritos recentemente aparecem no Intune
3. Iniciar uma ação de dispositivo do portal do Intune, tal como [bloqueio remoto](https://docs.microsoft.com/intune/device-remote-lock). Se tiver êxito, o dispositivo com êxito é gerido pela nova autoridade de MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Para os utilizadores e dispositivos que ainda não migrados anteriormente

- Certifique-se de que os dispositivos são agora apresentados na **dispositivos** página como dispositivos geridos. Antes de estes são apresentados, estes dispositivos têm de check-in e sincronizar com o serviço após a alteração da autoridade de MDM. 

- Quando o serviço do Intune Deteta que a autoridade MDM de um inquilino foi alterado, envia uma mensagem de notificação para todos os dispositivos inscritos. Ele instrui os dispositivos se registarem e sincronizarem com o serviço. Esta notificação acontece fora o check-in agendado regularmente. Depois de alterar a autoridade de MDM para o inquilino da híbrida para o Intune autónomo, todos os dispositivos online se ligar ao serviço. Eles receberão a nova autoridade MDM e, em seguida, são geridos pelo Intune autónomo daqui em diante. Não há nenhuma interrupção para o gerenciamento e proteção destes dispositivos.

- Para dispositivos que estejam offline durante ou pouco depois da alteração na autoridade de MDM, eles ligar e sincronizarem com o serviço na nova autoridade de MDM, quando eles estão ligados e online.  

- Pode alterar rapidamente para a nova autoridade MDM ao iniciar manualmente um check-in do dispositivo para o serviço. Utilize a aplicação Portal da empresa para iniciar uma verificação de conformidade do dispositivo.

- Há um período provisório em que um dispositivo está offline durante a alteração da autoridade de MDM e do que o dispositivo é registado no serviço. Certifique-se de que o dispositivo permanece protegido e funcional durante este período provisório, os seguintes perfis permanecem no dispositivo até sete dias. Eles também podem permanecer até que o dispositivo estabelece ligação com a nova autoridade MDM e receba as novas definições que substituirão as existentes:
    - Perfil e-mail
    - Perfil VPN
    - Perfil certificado
    - Perfil Wi-Fi
    - Perfis de configuração

- Para dispositivos que não estão associados a um utilizador, contacte o suporte para o ajudar a alterar a autoridade MDM. 

#### <a name="bkmk-ki-dep"></a> Registos de dispositivos do DEP da Apple
<!--ICM 105091970--> Depois de concluir a migração da MDM híbrida, poderá reparar os dispositivos Apple DEP registos permanecem na consola do Configuration Manager. Depois de alterar a autoridade de MDM ao Intune, não é possível remover estes dispositivos do Configuration Manager. 

Existem duas soluções alternativas:

- Se vir este comportamento antes de alterar a autoridade de MDM, em seguida, elimine os registos DEP no Configuration Manager.  

- Se já tiver migrado e ainda estiver a utilizar o Configuration Manager, utilize o seguinte comando SQL na base de dados do site para remover os registos:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Passos seguintes

Agora que a migração estiver concluída, geri os seus dispositivos móveis com o Intune. Para obter mais informações, consulte [o que há de novo no Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

