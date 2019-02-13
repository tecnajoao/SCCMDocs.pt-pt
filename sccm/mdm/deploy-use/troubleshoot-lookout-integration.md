---
title: Resolução de problemas de integração do Lookout
titleSuffix: Configuration Manager
description: Este tópico descreve resoluções de problemas que ocorrem frequentemente com integração do Lookout.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6055efad94952a7dcd7714cdfb5730289d8dafc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136148"
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Resolver problemas de integração do Lookout com o Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="troubleshoot-login-errors"></a>Resolver erros de início de sessão
### <a name="403-errors"></a>403 erros
Poderá ver um erro 403 quando iniciar sessão para o [consola do Lookout MTP](https://aad.lookout.com): **não está autorizado a aceder ao serviço** Isto pode acontecer quando o nome de utilizador especificado não é um membro do (Azure Active Directory Grupo do Azure AD) que está configurado para aceder ao Lookout MTP.

O lookout MTP está configurado para permitir que apenas utilizadores do Azure AD configurado tenham acesso de grupo. Se tiver certeza que grupo está configurado com acesso ao Lookout MTP, contacte o suporte do Lookout.

Pode contactar o suporte do Lookout através dos seguintes métodos:

* E-mail: enterprisesupport@lookout.com
* Início de sessão para o [consola MTP](http://aad.lookout.com)e navegue para o **suporte** módulo.
* Aceda a: https://enterprise.support.lookout.com/hc/requests e fazer um pedido de suporte.

### <a name="unable-to-sign-in"></a>Não é possível iniciar sessão
Poderá ver o seguinte erro se o utilizador de administrador global do Azure AD não aceitar a configuração inicial do Lookout.

![captura de ecrã do ecrã de início de sessão Lookout a mostrar o início de sessão no erro](media/lookout-consent-not-accepted-error.png)

Para resolver este problema, o utilizador de administrador global tem início de sessão para https://aad.lookout.com/les?action=consent e aceitar o pedido para iniciar a configuração. Pode encontrar informações mais detalhadas na [configurar a sua subscrição com o Lookout MTP](set-up-your-subscription-with-lookout.md) tópico

## <a name="troubleshoot-device-status-issues"></a>Resolver problemas de estado do dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Dispositivo não aparecer na lista de dispositivos de consola do Lookout MTP

Isto pode ocorrer em qualquer um dos seguintes cenários:
* Quando o utilizador que é proprietário deste dispositivo não está no **grupo de inscrição** especificado na **consola do Lookout MTP**.  Do **System** módulo, vá para o **conector do Intune** separador e examinar o **gestão de inscrições** definições.  Deverá ver um ou mais grupos do Azure AD configurados para inscrição.  Certifique-se de que o utilizador proprietário do dispositivo em falta faz parte de um especificado dos grupos do Azure AD.  Quando é adicionado um novo utilizador ao grupo de inscrição, irá demorar até ao intervalo de consulta configurado (a predefinição de é de 5 minutos) para ver o dispositivo aparecer na **dispositivos** módulo na consola do Lookout MTP.

* Se o dispositivo não é suportado pelo Lookout MTP.  Os dispositivos que não são suportados irão aparecer na **dispositivos geridos pelo** secção de definições do conector na consola do Lookout MTP.

### <a name="device-continues-to-be-reported-as-pending"></a>Dispositivo continua a ser comunicado como **pendente**

Um dispositivo que está a mostrar **pendente** significa que o utilizador final não abriu a aplicação Lookout for work e não tocou a **ativar** botão. Para obter mais detalhes sobre a ativação de dispositivos com o Lookout for Work a aplicação, leia o tópico seguinte:

[Lhe for pedido para instalar o Lookout for Work no seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Na consola do Lookout MTP, um dispositivo está a aparecer como ativo, mas não tem um ID de dispositivo.
Isso significa que o utilizador que é proprietário deste dispositivo não está no grupo de inscrição, especificado na consola do Lookout MTP.   Um dispositivo pode ficar neste estado se o utilizador que é proprietário do dispositivo foi removido do grupo de inscrição ou o grupo de inscrição que o utilizador pertence tiver sido removido.

Do **sistema** módulo na consola do Lookout MTP, aceda ao **conector do Intune** separador e reveja o **inscrição** definições.  Deverá ver um ou mais grupos do Azure AD configurados para inscrição.  Certifique-se de que o utilizador que é proprietário do dispositivo faz parte de um dos grupos do Azure AD especificados.

Enquanto um dispositivo está neste estado, o Lookout irá continuar a notificar o utilizador de quaisquer ameaças detetadas, mas não envia informações de ameaças para o Intune.

### <a name="device-shows-disconnected-state"></a>Dispositivo mostra um estado desligado

Desligado significa que o Lookout MTP não teve notícias do dispositivo ao longo de um intervalo de tempo pré-configurado (a predefinição é 30 dias com um mínimo de 7 dias). Isso significa que a aplicação Portal da empresa ou o Lookout for Work a aplicação não está instalado no dispositivo ou foi desinstalada. Reinstalar as aplicações deve resolver este problema. Quando o usuário abre o Lookout for Work e ativa o aplicativo, o dispositivo sincroniza novamente com o Lookout MTP e o Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forçar a ressincronização no dispositivo
Partir do **dispositivos** módulo da consola do Lookout MTP, o administrador pode selecionar o dispositivo e optar por eliminá-lo.   Da próxima vez que o proprietário do dispositivo abre o Lookout for Work a aplicação e toques **Activate**, o estado do dispositivo fará uma ressincronização completa.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>O proprietário do dispositivo já não está a utilizar este dispositivo
Tem de apagar o dispositivo e pedir ao novo utilizador para inscrever, conforme descrito em [neste tópico](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


Também pode ir para o **dispositivos** módulo na consola do Lookout MTP e escolha **eliminar**.

Desde que o utilizador novo esteja dos grupos de inscrição especificados na consola do Lookout MTP, o dispositivo irá aparecer assim que o Azure AD associar o dispositivo para o novo utilizador.

## <a name="compliance-remediation-workflows"></a>Fluxos de trabalho de remediação de conformidade
[Lhe for pedido para instalar o Lookout for Work no seu dispositivo Android]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Tem de resolver uma ameaça que o Lookout for Work encontrou no seu dispositivo Android ](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
