---
title: Resolver problemas de integração de Lookout
titleSuffix: Configuration Manager
description: Este tópico descreve problemas de resolução de problemas que ocorrem frequentemente com Lookout integração.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ee978543248e70182e12a3d6234cfd12be80dc98
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Resolver problemas Lookout integração com o Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="troubleshoot-login-errors"></a>Resolver erros de início de sessão
### <a name="403-errors"></a>403 erros
Poderá ver um erro 403 quando iniciar sessão para o [consola Lookout MTP](https://aad.lookout.com): **não está autorizado a aceder ao serviço** Isto pode acontecer se o nome de utilizador especificado não é um membro do grupo do Azure Active Directory (Azure AD) que está configurado para aceder à Lookout MTP.

Lookout MTP está configurado para permitir que apenas utilizadores de um configurado do Azure AD de grupo para ter acesso. Se não souber qual o grupo está configurado com acesso ao Lookout MTP, contacte o suporte de Lookout.

Pode contactar o suporte de Lookout através nos seguintes métodos:

* E-mail: enterprisesupport@lookout.com
* Início de sessão para o [MTP consola](http://aad.lookout.com)e navegue para o **suporte** módulo.
* Aceda a: https://enterprise.support.lookout.com/hc/requests e efetuar um pedido de suporte.

### <a name="unable-to-sign-in"></a>Não é possível iniciar sessão
Poderá ver o seguinte erro quando o utilizador de administrador global do Azure AD não aceitou o programa de configuração inicial do Lookout.

![captura de ecrã do ecrã de início de sessão Lookout que mostra o início de sessão no registo de erros](media/lookout-consent-not-accepted-error.png)

Para resolver este problema, tem do utilizador de administrador global no início de sessão https://aad.lookout.com/les?action=consent e aceitar o pedido para iniciar o programa de configuração. Pode encontrar informações mais detalhadas no [configurar a sua subscrição com o Lookout MTP](set-up-your-subscription-with-lookout.md) tópico

## <a name="troubleshoot-device-status-issues"></a>Resolver problemas de estado do dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Dispositivo não ser apresentado na lista de dispositivos de consola Lookout MTP

Isto pode acontecer dos seguintes cenários:
* Quando o utilizador proprietário este dispositivo não está no **inscrição grupo** especificado no **Lookout MTP consola**.  Do **sistema** módulo, acedo ao **conector do Intune** separador e observe o **inscrição gestão** definições.  Deverá ver uma ou mais grupos do Azure AD configurados para a inscrição.  Certifique-se de que o utilizador proprietário do dispositivo em falta faz parte de um especificado dos grupos do Azure AD.  Assim que um novo utilizador é adicionado ao grupo de inscrição irá demorar para o intervalo de consulta configurado (a predefinição é 5 minutos) para ver o dispositivo apresentada no **dispositivos** módulo da consola de MTP Lookout.

* Se o dispositivo não é suportado por Lookout MTP.  Os dispositivos são não suportado serão apresentados no **dispositivos geridos pelo** secção das definições na consola de MTP Lookout conector.

### <a name="device-continues-to-be-reported-as-pending"></a>Dispositivo continua a ser reportados como **pendente**

Um dispositivo que está a ser mostrada **pendente** significa que o utilizador final não abriu o Lookout para a aplicação de trabalho e tapped o **ativar** botão. Para obter mais detalhes sobre a ativação de dispositivos com o Lookout para a aplicação de trabalho, leia o tópico seguinte:

[É-lhe pedido que instale o Lookout for Work no seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Na consola do Lookout MTP, um dispositivo que mostra como Active Directory, mas não tem um ID de dispositivo.
Isto significa que o utilizador proprietário este dispositivo não está no grupo de inscrição, especificado na consola de MTP Lookout.   Um dispositivo pode entrar neste estado é se o utilizador proprietário do dispositivo foi removido do grupo de inscrição ou o grupo de inscrição que o utilizador pertence a tem foi removido.

Do **sistema** módulo na consola do Lookout MTP, vá para o **conector do Intune** separador e rever o **inscrição** definições.  Deverá ver uma ou mais grupos do Azure AD configurados para a inscrição.  Certifique-se de que o utilizador proprietário do dispositivo faz parte de um dos grupos do Azure AD especificados.

Enquanto um dispositivo está neste estado, o Lookout irá continuar a notificar o utilizador de qualquer ameaças detetadas, mas não irá enviar quaisquer informações de ameaças para o Intune.

### <a name="device-shows-disconnected-state"></a>Dispositivo mostra o estado desligado

Desligado significa que não tem ouvidos Lookout MTP do dispositivo para através de um intervalo de tempo pré-configurada (a predefinição é 30 dias com um mínimo de 7 dias). Isto significa que a aplicação Portal da empresa ou o Lookout para a aplicação de trabalho não está instalado no dispositivo ou tiver sido desinstalado. Reinstalar as aplicações deve resolver este problema. Quando o utilizador abre o Lookout for Work e ativa a aplicação, os resyncs de dispositivo com o Lookout MTP e o Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forçar uma ressincronização no dispositivo
Do **dispositivos** módulo da consola Lookout MTP, o administrador pode selecionar o dispositivo e escolher eliminá-la.   Da próxima vez que o proprietário do dispositivo abre o Lookout para aplicação de trabalho e taps **ativar**, o estado do dispositivo executará uma ressincronização completa.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>O proprietário do dispositivo já não está a utilizar este dispositivo
Tem de apagar o dispositivo e pedir ao utilizador para inscrever, tal como descrito no novo [neste tópico](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


Também pode ir para o **dispositivos** módulo da consola de MTP Lookout e escolha **eliminar**.

O novo utilizador está a ser um dos grupos de inscrição especificados na consola do Lookout MTP, desde que o dispositivo será apresentada uma vez do Azure AD associa o dispositivo para o novo utilizador.

## <a name="compliance-remediation-workflows"></a>Fluxos de trabalho de remediação de conformidade
[É-lhe pedido que instale o Lookout for Work no seu dispositivo Android]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[É necessário resolver uma ameaça que Lookout for Work, foi encontrado no seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
