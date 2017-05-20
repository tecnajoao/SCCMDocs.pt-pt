---
title: "Como gerir a proteção de dispositivo do Windows | Documentos do Microsoft"
description: "Saiba como utilizar o System Center Configuration Manager para gerir a proteção de dispositivo do Windows."
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Gestão de proteção de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="introduction"></a>Introdução
Proteção de dispositivo do Windows é um grupo de funcionalidades do Windows 10 que foram concebidos para proteger computadores contra software maligno e outro software não fidedigno. -Impede o código malicioso em execução, garantindo que apenas aprovado código, o que já conhece, pode ser executado.

Abrange a proteção de dispositivo hardware e software com base funcionalidade de segurança. Integridade do código configuráveis é uma camada de segurança baseada em software que impõe uma lista de software que está autorizado a executar num PC explícita. Na sua própria, código configurável integridade não tem os pré-requisitos de hardware ou firmware. Políticas de proteção de dispositivo implementadas com o Configuration Manager ativar uma política de integridade do código configuráveis em PCs no coleções de destino que cumprem os requisitos de SKU descritos abaixo e a versão mínima do Windows. Opcionalmente, hipervisor com base em proteção de políticas implementadas através do Configuration Manager podem ser ativadas através da política de grupo em hardware compatível com a integridade do código.

Para saber mais sobre proteção de dispositivo, consulte o artigo [guia de implementação da proteção de dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

Pode utilizar o Configuration Manager para implementar uma política de proteção de dispositivo que permite-lhe configurar o modo em que a proteção de dispositivo serão executados em PCs numa coleção. 

Pode configurar um dos seguintes modos:

1.    **Imposição ativada** - só executáveis são permitidas a execução de confiança.
2.    **Auditoria apenas** - permitir todos os executáveis ser executada, mas registo não fidedigno executáveis que são executados no registo de eventos de cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, a proteção de dispositivo é uma funcionalidade de versão de pré-lançamento. Para ativá-lo, consulte o artigo [pré-lançamento funcionalidades no System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>O que pode executar quando implementa uma política de proteção do dispositivo?

Proteção de dispositivo do Windows permite-lhe controlar vivamente que podem ser executados em PCs que gere. Isto pode ser particularmente útil para PCs de departamentos de alta segurança, onde ficará vitais se software indesejável não é permitida a ser executada.

Ao implementar uma política, normalmente, as seguintes executáveis serão permissão para ser executada:

- Componentes do sistema operativo Windows
- Controladores de hardware Dev Center (que têm assinaturas laboratórios de qualidade de Hardware do Windows)
- Aplicações da loja Windows
- O cliente do Configuration Manager 
- Todo o software implementado através do Configuration Manager que instalar PCs depois da política de proteção de dispositivo é processada. 
- Atualizações de componentes do windows a partir de:
    - Windows Update
    - Windows Update para empresas
    - Windows Server Update Services
    - Gestor de configuração

>[!IMPORTANT]
>Estes não incluir qualquer software que é **não** incorporado no Windows que atualiza automaticamente a partir do software internet ou de terceiros atualizará se estiverem instalados através de qualquer um dos mecanismos de atualização mencionados acima, ou a partir da internet. Apenas alterações de software que estão implementadas através de cliente do Configuration Manager irá permissão para ser executada.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implementar políticas de proteção de dispositivo, leia as seguintes informações:

- A gestão de dispositivos a proteção é uma funcionalidade de versão de pré-lançamento para o Configuration Manager e está sujeito a alterações.
- Para utilizar a proteção de dispositivo, PCs gere tem de executar o Windows 10 Enterprise com a atualização criadores, ou posterior.
- Assim que uma política é processada com êxito num cliente PC, o Configuration Manager está configurado como um instalador geridos no que o cliente e software implementada através de SCCM após a política de processamento é automaticamente fidedigno. Software instalado pela configuração geridos antes da política de proteção de dispositivo é processada não é fidedigno automaticamente.
- Nesta versão de pré-lançamento, assim que um cliente PC recebe uma implementação de uma política de proteção de dispositivo, este será utilize uma ordem aleatória o tempo de processamento da presente política durante um período de duas horas. 
- PCs de cliente tem de ter conectividade ao seu controlador de domínio para uma política de proteção de dispositivo a ser processado com êxito.
- A agenda de avaliação de compatibilidade predefinida para políticas de proteção de dispositivo, configuráveis durante a implementação, é a cada 1 dia. Se a problemas de processamento da política básicos observados, pode ser vantajoso configurar a agenda de avaliação de compatibilidade para ser mais curtos, por exemplo 1 a cada hora. Esta agenda dita com que frequência os clientes irão voltar a tentar processar uma política de proteção de dispositivo em caso de uma falha.
- Independentemente do modo de imposição que selecionar, ao implementar uma política de proteção de dispositivo, o cliente PCs não será possível executar aplicações de HTML com a extensão HTA.

## <a name="how-to-create-a-device-guard-policy"></a>Como criar uma política de proteção de dispositivo
1.    Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.    No **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de proteção de dispositivos**.
3.    No **base** separador o **criar** grupo, clique em **criar política de proteção de dispositivo**.
4.    No **geral** página do **criar Assistente de política de proteção de dispositivo**, especifique o seguinte:
    - **Nome** -introduza um nome exclusivo para esta política de proteção do dispositivo. 
    - **Descrição** - opcionalmente, introduza uma descrição para a política que irão ajudar a identificá-la na consola do Configuration Manager.
    - **Modo de imposição** -escolher um dos seguintes métodos de imposição para proteção de dispositivo no cliente PC.
        - **Imposição ativado** - apenas permitir executáveis fidedignas são permitidas a execução.
        - **Auditoria apenas** - permitir todos os executáveis ser executada, mas registo não fidedigno executáveis que são executados no registo de eventos de cliente local.
5.    Clique em **seguinte**, em seguida, conclua o assistente.

## <a name="how-to-deploy-a-device-guard-policy"></a>Como implementar uma política de proteção de dispositivo
1.    Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.    No **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de proteção de dispositivos**.
3.    A partir da lista de políticas, selecione aquela que pretende implementar, e, em seguida, no **base** separador o **implementação** grupo, clique em **implementar**.
4.    No **implementar política de proteção de dispositivo** caixa de diálogo, selecione a coleção à qual pretende implementar a política, configure uma agenda para quando os clientes irão avaliar a política e, finalmente, selecione se o cliente pode avaliar a política de fora de quaisquer janelas de manutenção configurada.
5.    Quando tiver terminado, clique em **OK** implementar a política. 

Assim que a política é processada num cliente PC, irá ser agendado um reinício para esse cliente de acordo com a **definições de cliente** para **reiniciar o computador**.
**Até que reinicie o computador cliente, a política não irão surtir efeito.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Como monitorizar uma política de proteção de dispositivo

Utilize as informações de [monitorizar as definições de compatibilidade](/sccm/compliance/deploy-use/monitor-compliance-settings) tópico para o ajudar a monitorizar a política implementada para se certificar de que tenha sido aplicado a todos os PCs corretamente.

Utilize o seguinte ficheiro de registo no cliente PCs para monitorizar o processamento de uma política de proteção do dispositivo:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico que está a ser bloqueados ou quando auditada, consulte os seguintes registos de eventos de cliente local. No Visualizador de eventos, os registos relevantes são as seguintes:

1.    Para bloquear e auditoria dos ficheiros executáveis, utilize **registos de serviços e aplicações** > **Microsoft** > **Windows** > **integridade do código** > **operacional**.
2.    Para bloquear e auditoria do Windows Installer e os ficheiros de script, utilize **registos de serviços e aplicações** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para proteção de dispositivo

- Nesta versão de pré-lançamento não implementa políticas de proteção de dispositivo com o modo de imposição **auditorias apenas** num ambiente de produção. Este modo destina-se para o ajudar a testar a capacidade de um laboratório de definição apenas.
- Dispositivos que tenham uma política implementada nos mesmos em **auditorias apenas** modo ou dispositivos que tenham uma política implementada nos mesmos em **imposição ativada** modo, que ainda não foram reiniciados para impor a política são vulneráveis a software não fidedigno que está a ser instalado.
Nesta situação, o software poderá continuar a permissão para ser executada mesmo que o dispositivo for reiniciado, ou recebe uma política no **imposição ativada** modo.
- Para garantir que a política de proteção de dispositivo está efetiva, prepare o dispositivo num ambiente de laboratório, implementar o **imposição ativada** política, em seguida, reiniciar o dispositivo antes de fazer o dispositivo a um utilizador final.
- Não implemente uma política com **imposição ativada**e, em seguida, mais tarde, implemente uma política com **auditorias apenas** no mesmo dispositivo. Isto pode resultar não fidedigno pelo software de serem autorizados a executar.
- Quando utilizar o Configuration Manager para ativar a integridade do código configurável no cliente PCs com as políticas de proteção de dispositivo, tenha em atenção de que a política **não** impedir que os utilizadores com direitos de administrador local a partir de circumventing a política de proteção de dispositivo ou caso contrário, executar software não fidedigno. 
- É a única forma de evitar que os utilizadores com direitos de administrador local a partir da desativação de integridade do código configurável implementar uma política de binária com a sessão iniciada, que é possível através da política de grupo, mas não suportada atualmente no Configuration Manager.
- Definir o Gestor de configuração como um instalador geridos em PCs de cliente utiliza a política de AppLocker. AppLocker só é utilizado para identificar instaladores geridos e imposição de todos os acontece com integridade do código configurável. 





