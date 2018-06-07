---
title: Alterar a autoridade de MDM ao Intune
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para o Intune autónomo.
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: b295dad503b801ff9d04767f75c1688107016d0b
ms.sourcegitcommit: 493cc42f05b9388ef872e466e5a75d569642b9fc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/01/2018
ms.locfileid: "34569685"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM ao Intune autónomo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Pode alterar um inquilino do Microsoft Intune existente configurado na consola do Configuration Manager (MDM híbrido) para o Intune autónomo. Alterar a autoridade de MDM de inquilinos para o Intune é a fase final no processo de para [migrar utilizadores MDM híbrida e dispositivos ao Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na nuvem.    

> [!Important]    
> Para alterar a autoridade de MDM sem primeiro utilizadores MDM híbrida migrar para o Intune, consulte [alterar a autoridade de MDM](change-mdm-authority.md).

Este artigo fornece informações sobre como alterar um inquilino do Microsoft Intune existente configurado na consola do Configuration Manager (híbrido) para o Intune autónomo e pressupõe que já tenha concluído os passos seguintes:
- Utilizar o [ferramenta de importação de dados do Intune](migrate-import-data.md) para importar objetos do Configuration Manager para o Intune. 
- [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) para garantir que os utilizadores e os respetivos dispositivos continuam a ser geridos depois de serem migrados.
- [Alterar a autoridade de MDM para utilizadores específicos (misturadas autoridade de MDM)](migrate-mixed-authority.md) para começar a gerir dispositivos de utilizador do portal do Azure.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Utilizadores e dispositivos que não foram migrados
Tiver já migrado muitos utilizadores e testar a funcionalidade do Intune para se certificar de que coisas estão a funcionar conforme esperado. Por conseguinte, as políticas, perfis, aplicações, etc. foram configuradas no Intune e tiver testado exaustivamente os objetos sobre os dispositivos. Não deverá haver nenhum as novas configurações necessárias para as políticas ao nível do inquilino após a alteração na autoridade de MDM. No entanto, para os utilizadores e dispositivos que não foram migrados anteriormente, reveja as seguintes informações sobre o que esperar após a alteração na autoridade de MDM:    
- É provável que uma transição tempo (até oito horas) antes do dispositivo ser registado e sincroniza com o serviço.
- Os seus dispositivos tem de ligar com o serviço após a alteração, para que as definições da autoridade de MDM novo (Intune autónomo) substituem as definições existentes no dispositivo.
- Algumas das definições básicas (por exemplo, perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias. 
- Dispositivos que não tem utilizadores associados (normalmente, quando tiver iOS Device Enrollment Program ou efetuar a cenários de inscrição em massa) não são migrados para a autoridade de MDM de novo. Para os dispositivos, tem de chamar o suporte para obter ajuda para movê-los para a autoridade de MDM de novo.

## <a name="prerequisites"></a>Pré-requisitos
Reveja as informações seguintes para se preparar para a alteração à autoridade de MDM:
- Tem de ter o Configuration Manager versão 1610 ou superior para a opção para alterar a autoridade de MDM para estar disponível.
- Certifique-se de que todos os utilizadores que sejam atualmente geridos pelo híbrida MDM tem uma licença do Intune/EMS atribuída antes da alteração na autoridade de MDM. Ter a licença assegura que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração na autoridade de MDM. Para obter mais informações, consulte [licenças do Intune atribuir às suas contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída.

## <a name="change-the-mdm-authority-to-intune"></a>Alterar a autoridade de MDM ao Intune
Utilize o procedimento seguinte para alterar a autoridade de MDM de inquilinos para o Intune.

1.  Na consola do Configuration Manager, vá para **administração** &gt; **descrição geral** &gt; **serviços em nuvem** &gt; **subscrição do Microsoft Intune**e eliminar a sua subscrição do Intune existente.
2.  Selecione **autoridade de MDM de alteração para o Microsoft Intune**e, em seguida, clique em **seguinte**.

    ![Remova o diálogo de subscrição do Microsoft Intune](media/mdm-change-delete-subscription.png)
3.  Iniciar sessão para o inquilino do Intune que utilizou originalmente quando definir a autoridade de MDM no Configuration Manager.
4.  Clique em **Seguinte** e conclua o assistente.
5.  A autoridade de MDM é reposta. A subscrição do Intune já não é apresentada no nó de subscrições do Microsoft Intune da consola do Configuration Manager.
6.  Inicie sessão no [Intune portal](https://aka.ms/IntunePortal).
7.  No painel do Microsoft Intune, clique em **inscrição de dispositivos**.
8.  No painel de descrição geral de inscrição do dispositivo, consulte o **autoridade de MDM** propriedade.

  > [!Important]    
  > Não utilize a consola do Intune clássica. Tem de iniciar sessão Intune no portal do Azure.
7.  Confirme que a autoridade de MDM foi alterada para **Microsoft Intune**. 

## <a name="next-steps"></a>Passos seguintes
Depois de concluída a alteração na autoridade de MDM, reveja as seguintes informações:
- Não deverá haver nenhum impacto considerável aos utilizadores finais durante a alteração na autoridade de MDM. 
- Não é necessário reconfigurar políticas ao nível do inquilino. 
- Pode editar as políticas ao nível do inquilino do Intune no portal do Azure após a alteração na autoridade de MDM.
-  Depois de alterar a autoridade de MDM, execute os seguintes passos para validar que a novos dispositivos são inscritos com êxito para a autoridade de novo:   
    - Inscrever um dispositivo novo
    - Certifique-se de que os dispositivos inscritos recentemente aparecem no Intune.
    - Efetue uma ação, tal como o bloqueio remoto, na consola de administração do dispositivo. Se for bem sucedida, o dispositivo está a ser gerido pela autoridade MDM de novo.
- Se tiver problemas com dispositivos específicos, pode anular a inscrição e inscrever-se novamente os dispositivos para obtê-los à autoridade de novo e geridas como rapidamente quanto possível.
- Para utilizadores e dispositivos que não foram migrados anteriormente:
    - Certifique-se de que os dispositivos são agora apresentados no **dispositivos** painel como os dispositivos geridos. Estes dispositivos têm de verificação e sincronizar com o serviço após a alteração na autoridade de MDM antes de são apresentadas. 
    - Quando o serviço Intune Deteta que a autoridade de MDM de um inquilino foi alterado, que envia uma mensagem de notificação para todos os dispositivos inscritos para registar e sincronizar com o serviço (fora da agendadas regularmente dar entrada no). Por conseguinte, depois da autoridade de MDM para o inquilino foi alterada híbrida ao Intune autónomo, todos os dispositivos que estão ligados à corrente no e online estabelecer ligação com o serviço, recebem a nova autoridade de MDM e de ser geridos pelo Intune autónomo de agora no. Não há sem interrupções da gestão e a proteção destes dispositivos.
    - Dispositivos que estão ligados desativado ou offline durante a (ou pouco depois) a alteração na autoridade de MDM ligar e sincronizar com o serviço sob a autoridade de MDM novo quando estão ligados à corrente no e online.  
    - Os utilizadores podem alterar rapidamente para a autoridade de MDM novo iniciando manualmente um verificação-in do dispositivo para o serviço. Os utilizadores podem facilmente Verifique utilizando a aplicação Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
    - Não há um período provisória quando um dispositivo estiver offline durante a alteração na autoridade de MDM e quando verifica a que o dispositivo para o serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcionais durante este período intermédio, os seguintes perfis permanecem no dispositivo até sete dias (ou até que o dispositivo estabelece ligação com a autoridade de MDM novo e recebe novas definições de substituir a existente aqueles):
        - Perfil de e-mail
        - Perfil da VPN
        - Perfil de certificado
        - Perfil Wi-Fi
        - Perfis de configuração
    - Contacte o suporte para o ajudar a alterar a autoridade de MDM para dispositivos que não estão associados um utilizador. 
