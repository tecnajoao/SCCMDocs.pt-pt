---
title: "Resolver problemas relacionados com a integração de atento | O System Center Configuration Manager"
description: "Este tópico descreve problemas de resolução de problemas que ocorrem frequentemente com atento integração."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4fd2d3b8aae6a2f42e7c6a87723d16368be30984
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Resolver problemas relacionados com atento a integração com o Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="troubleshoot-login-errors"></a>Resolver problemas de erros de início de sessão
### <a name="403-errors"></a>403 erros
Poderá ver um erro de 403 quando iniciar sessão a [consola atento MTP](https://aad.lookout.com): **não está autorizado a aceder ao serviço** Isto pode acontecer quando o nome de utilizador especificado não é um membro do grupo do Azure Active Directory (Azure AD) que está configurado para aceder à atento MTP.

Atento MTP está configurado para permitir que o grupo de apenas os utilizadores a partir de um Azure AD configurado para ter acesso. Se não souber o grupo está configurado com acesso ao atento MTP, contacte o suporte de atento.

Pode contactar o suporte de atento através de sobre os métodos seguintes:

* E-mail:enterprisesupport@lookout.com
* Início de sessão para o [MTP consola](http://aad.lookout.com)e navegue para o **suporte** módulo.
* Aceda a: https://enterprise.support.lookout.com/hc/en-us/requests e efetuar um pedido de suporte.

### <a name="unable-to-sign-in"></a>Não é possível iniciar sessão
Poderá ver o seguinte erro quando o utilizador de administrador global do Azure AD não aceitou a configuração de atento inicial.

![captura de ecrã do ecrã de início de sessão atento que mostra início de sessão no registo de erros](media/lookout-consent-not-accepted-error.png)

Para resolver este problema, o utilizador de administrador global tem início de sessão para https://aad.lookout.com/les?action=consent e aceitar o pedido para iniciar o programa de configuração. Podem encontrar informações mais detalhadas na [configurar a sua subscrição com atento MTP](set-up-your-subscription-with-lookout.md) tópico

## <a name="troubleshoot-device-status-issues"></a>Resolver problemas de estado do dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Dispositivo que não aparecem na lista de dispositivos de consola atento MTP

Isto pode ocorrer em qualquer um dos seguintes cenários:
* Quando o utilizador que detém este dispositivo não se encontre no **inscrição grupo** especificado no **atento MTP consola**.  A partir do **sistema** módulo, acedo ao **conector do Intune** separador e observe o **inscrição gestão** definições.  Deverá ver um ou mais grupos do Azure AD configurados para a inscrição.  Certifique-se de que o utilizador proprietário do dispositivo em falta faz parte de um dos especificado grupos do Azure AD.  Depois de um novo utilizador é adicionado ao grupo de inscrição demorará para o intervalo de consulta configurado (5 minutos é a predefinição) para ver o dispositivo aparecem no **dispositivos** módulo da atento MTP consola.

* Se o dispositivo não é suportado por atento MTP.  Os dispositivos que estão não suportado irão aparecer no **dispositivos geridos pelo** secção das definições na consola de MTP atento conector.

### <a name="device-continues-to-be-reported-as-pending"></a>Dispositivo continua a ser reportados como **pendente**

Um dispositivo que está a mostrar **pendente** significa que o utilizador final não abriu o atento para a aplicação de trabalho e tocou o **ativar** botão. Para obter mais detalhes sobre a ativação de dispositivo com atento para a aplicação de trabalho, leia o tópico seguinte:

[Lhe for pedido para instalar atento para trabalhar no seu dispositivo Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Na consola do atento MTP, um dispositivo que mostra como ativo, mas não tem um ID de dispositivo.
Isto significa que o utilizador que detém este dispositivo não está no grupo de inscrição, especificado na consola de MTP atento.   Um dispositivo pode obter este estado é se o utilizador proprietário do dispositivo foi removido do grupo de inscrição ou o grupo de inscrição que pertence o utilizador tem foi removido.

A partir do **sistema** módulo na consola do atento MTP, aceda ao **conector Intune** separador e rever o **inscrição** definições.  Deverá ver um ou mais grupos do Azure AD configurados para a inscrição.  Certifique-se de que o utilizador proprietário do dispositivo faz parte de um dos grupos do Azure AD especificados.

Enquanto um dispositivo está neste estado, atento irá continuar a notificar o utilizador de qualquer ameaças detetado, mas não irá enviar quaisquer informações de ameaças ao Intune.

### <a name="device-shows-disconnected-state"></a>Dispositivo mostra o estado desligado

Desligado significa que não tem ouvido MTP atento a partir do dispositivo para através de um intervalo de tempo pré-configuradas (a predefinição é 30 dias, com um mínimo de 7 dias). Isto significa que a aplicação de Portal da empresa ou atento para a aplicação de trabalho não está instalado no dispositivo ou foi desinstalado. Reinstalar as aplicações, deve resolver este problema. Quando o utilizador abre-se atento trabalho e ativa a aplicação, os resyncs de dispositivo com atento MTP e o Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forçar uma ressincronização no dispositivo
A partir de **dispositivos** módulo da consola atento MTP, o administrador pode selecionar o dispositivo e opte por eliminá-lo.   Da próxima vez que o proprietário do dispositivo abre-se atento a aplicação de trabalho e toca **ativar**, o estado do dispositivo fará uma ressincronização completa.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>O proprietário do dispositivo já não está a utilizar neste dispositivo
Tem de apagar o dispositivo e solicite ao utilizador novo a inscrever conforme descrito em [neste tópico](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


Também pode ir para o **dispositivos** módulo da consola MTP atento e escolha **eliminar**.

Desde que o novo utilizador estiver em nenhum dos grupos de inscrição especificados na consola do atento MTP, o dispositivo serão apresentados assim que o dispositivo para o novo utilizador associe o Azure AD.

## <a name="compliance-remediation-workflows"></a>Fluxos de trabalho de remediação de conformidade
[Lhe for pedido para instalar atento para trabalhar no seu dispositivo Android]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Para resolver uma ameaça que atento trabalho encontrado no seu dispositivo Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

