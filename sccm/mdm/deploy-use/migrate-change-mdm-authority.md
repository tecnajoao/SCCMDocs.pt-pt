---
title: Alterar a sua autoridade MDM ao Intune
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM no Configuration Manager (híbrido) para o Intune autónomo.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: d5efcb78ad5e732691cc2f214f81db0b357e0e19
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111115"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Alterar a sua autoridade MDM para o Intune autónomo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Pode alterar um inquilino existente do Microsoft Intune configurado na consola do Configuration Manager (MDM híbrida) para o Intune autónomo. Alterar a autoridade de MDM de nível de inquilino para o Intune é a fase final do processo para [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na cloud.    

> [!Important]    
> Para alterar a autoridade MDM sem primeiro migrar usuários MDM híbrida para o Intune, consulte [alterar a sua autoridade MDM](change-mdm-authority.md).

Este artigo fornece informações sobre como alterar um inquilino existente do Microsoft Intune configurado na consola do Configuration Manager (híbrido) para o Intune autónomo e pressupõe que já tenha concluído os passos seguintes:
- Utilizar o [ferramenta de importação de dados do Intune](migrate-import-data.md) para importar objetos do Configuration Manager para o Intune. 
- [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) para garantir que os utilizadores e os respetivos dispositivos continuam a ser geridos depois de serem migrados.
- [Alterar a autoridade de MDM para utilizadores específicos (autoridade MDM misturadas)](migrate-mixed-authority.md) para começar a gerir dispositivos de utilizador do portal do Azure.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Utilizadores e dispositivos que não foram migrados
Já tiver migrado muitos usuários e testada de funcionalidades do Intune para se certificar de que as coisas estão funcionando como esperado. Por conseguinte, as políticas, perfis, aplicações, etc. foram configuradas no Intune e se tiver testado exaustivamente os objetos nos dispositivos. Não deve haver nenhum novas configurações necessárias para as suas políticas ao nível do inquilino após a alteração da autoridade de MDM. No entanto, para utilizadores e dispositivos que não foram migrados anteriormente, reveja as seguintes informações sobre o que esperar após a alteração da autoridade de MDM:    
- É provável que uma transição de tempo (até oito horas) antes do dispositivo for registado e sincroniza com o serviço.
- Os dispositivos têm de se ligar o serviço após a alteração para que as definições da nova autoridade de MDM (Intune autónomo) substituam as definições existentes no dispositivo.
- Algumas das definições básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias. 
- Dispositivos que não têm utilizadores associados (normalmente, quando tiver iOS do programa de inscrição de dispositivos ou em massa de cenários de inscrição) não são migrados para a nova autoridade MDM. Para esses dispositivos, terá de contactar o suporte para assistência para movê-los para a nova autoridade MDM.

## <a name="prerequisites"></a>Pré-requisitos
Reveja as informações seguintes para preparar a alteração para a autoridade de MDM:
- Tem de ter o Configuration Manager versão 1610 ou superior para a opção para alterar a autoridade de MDM para estar disponível.
- Certifique-se de que todos os utilizadores atualmente geridos de forma híbrida MDM ter uma licença do Intune/EMS atribuída antes da alteração da autoridade de MDM. Ter a licença garante que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração da autoridade de MDM. Para obter mais informações, consulte [atribuir licenças do Intune às contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída.

## <a name="change-the-mdm-authority-to-intune"></a>Alterar a autoridade MDM para Intune
Utilize o procedimento seguinte para alterar a autoridade de MDM de nível de inquilino para o Intune.

1.  Na consola do Configuration Manager, aceda a **Administration** &gt; **descrição geral** &gt; **serviços Cloud** &gt; **Subscrição do Microsoft Intune**e eliminar a sua subscrição do Intune existente.
2.  Selecione **alterar a autoridade de MDM para o Microsoft Intune**e, em seguida, clique em **próxima**.

    ![Remover o diálogo de subscrição do Microsoft Intune](media/mdm-change-delete-subscription.png)
3.  Inicie sessão no inquilino do Intune que utilizou originalmente quando definiu a autoridade de MDM no Configuration Manager.
4.  Clique em **Seguinte** e conclua o assistente.
5.  Agora é reposta a autoridade de MDM. A subscrição do Intune já não é apresentada no nó de subscrições do Microsoft Intune da consola do Configuration Manager.
6.  Inicie sessão para o [portal do Intune](https://aka.ms/IntunePortal).
7.  No painel do Microsoft Intune, clique em **inscrição de dispositivos**.
8.  No painel de descrição geral de inscrição do dispositivo, consulte a **autoridade de MDM** propriedade.

  > [!Important]    
  > Não utilize a consola clássica do Intune. Tem de iniciar sessão Intune no portal do Azure.
7.  Confirme que a autoridade de MDM foi alterada para **Microsoft Intune**. 

## <a name="next-steps"></a>Passos seguintes
Após concluir a alteração na autoridade de MDM, reveja as seguintes informações:
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração da autoridade de MDM. 
- Não tem de reconfigurar as políticas ao nível do inquilino. 
- Pode editar as políticas ao nível do inquilino do Intune no portal do Azure após a alteração da autoridade de MDM.
-  Depois de alterar a autoridade de MDM, execute os seguintes passos para validar que os dispositivos foram inscritos com êxito para a nova autoridade:   
    - Inscrever um novo dispositivo
    - Certifique-se de que os dispositivos inscritos recentemente aparecem no Intune.
    - Execute uma ação, como o bloqueio remoto, a partir da consola de administração para o dispositivo. Se tiver êxito, o dispositivo está a ser gerido pela nova autoridade de MDM.
- Se tiver problemas com dispositivos específicos, pode anular a inscrição e reinscrever os dispositivos para ligá-los ligado para a nova autoridade e gerenciados mais rapidamente possível.
- Para utilizadores e dispositivos que não foram migrados anteriormente:
    - Certifique-se de que os dispositivos são agora apresentados na **dispositivos** painel como dispositivos geridos. Estes dispositivos têm registarem e sincronizarem com o serviço após a alteração da autoridade de MDM, antes de elas são exibidas. 
    - Quando o serviço do Intune Deteta que a autoridade MDM de um inquilino foi alterado, envia uma mensagem de notificação para todos os dispositivos inscritos se registarem e sincronizarem com o serviço (fora agendado regularmente check-in). Portanto, depois da autoridade de MDM para o inquilino ser alterada da híbrida para o Intune autónomo, todos os dispositivos que estão ligados e online se ligar ao serviço, receberão a nova autoridade MDM e geridos pelo Intune autónomo daqui em diante. Não há nenhuma interrupção para o gerenciamento e proteção destes dispositivos.
    - Dispositivos que estão ligados desativado ou offline durante (ou pouco depois) a alteração da autoridade MDM de ligar e sincronizar com o serviço sob a nova autoridade MDM quando eles estão ligados e online.  
    - Os utilizadores podem mudar rapidamente para a nova autoridade MDM ao iniciar manualmente um check-in do dispositivo para o serviço. Os utilizadores podem facilmente check-in ao utilizar a aplicação Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
    - Há um período provisório em que um dispositivo está offline durante a alteração da autoridade de MDM e do que o dispositivo é registado no serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcional durante este período provisório, os seguintes perfis permanecem no dispositivo até sete dias (ou até que o dispositivo estabelece ligação com a nova autoridade MDM e receba as novas definições que substituir o existente aqueles):
        - Perfil de e-mail
        - Perfil da VPN
        - Perfil de certificado
        - Perfil de Wi-Fi
        - Perfis de configuração
    - Contacte o suporte para o ajudar a alterar a autoridade MDM para dispositivos que não estão associados um utilizador. 
