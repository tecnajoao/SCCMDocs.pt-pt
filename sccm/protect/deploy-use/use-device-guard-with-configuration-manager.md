---
title: Como gerir o Windows Device Guard | Microsoft Docs
description: "Saiba como utilizar o System Center Configuration Manager para gerir a proteção de dispositivos do Windows."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 4555f7a9a6b5efd0fa01e9a101ea16bae7685117
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Gestão de proteção de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="introduction"></a>Introdução
A proteção de dispositivos é um grupo de funcionalidades do Windows 10 que foram concebidas para proteger os PCs contra malware e outro software não fidedigno. Impede que código malicioso em execução, garantindo que apenas aprovado código, o que souber, pode ser executado.

Device Guard abrange o software e a funcionalidade de segurança baseada em hardware. Integridade do código configurável é uma camada de segurança baseada em software, que impõe uma lista explícita de software que pode ser executada em PCs. No seu próprio, código configurável integridade não tem quaisquer pré-requisitos de hardware e firmware. As políticas de proteção de dispositivos implementadas com o Configuration Manager permitem uma política de integridade de código configuráveis em PCs em coleções de destino que cumprem os requisitos de SKU descritos neste tópico e a versão mínima do Windows. Opcionalmente, proteção baseada em hipervisor das políticas de integridade de código implementado através do Configuration Manager pode ser ativada através da política de grupo com capacidade de hardware.

Para saber mais sobre Device Guard, leia o [guia de implementação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Utilizar a proteção de dispositivos com o Configuration Manager

Pode utilizar o Configuration Manager para implementar uma política de proteção de dispositivos que lhe permite configurar o modo no qual Device Guard é executada em computadores numa coleção. 

Pode configurar um dos seguintes modos de:

1.  **Imposição ativada** - só permitidos a execução de executáveis de confiança.
2.  **Só de auditoria** - permitir a execução de todos os executáveis, mas não considerada como fidedigna registo executáveis que são executados no registo de eventos de cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, Device Guard é uma funcionalidade de pré-lançamento. Para ativá-la, consulte o artigo [no System Center Configuration Manager de funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>O que pode ser executado quando implementar uma política de proteção de dispositivos?

Windows Device Guard permite-lhe controlar vivamente que pode ser executada em PCs que gere. Esta funcionalidade pode ser útil para PCs departamentos de alta segurança, onde é vital que não é possível executar o software indesejável.

Ao implementar uma política, normalmente, podem executar o executáveis seguintes:

- Componentes do sistema operativo Windows
- Controladores de hardware Dev Center (que têm as assinaturas de Windows Hardware Quality Labs)
- Aplicações da loja Windows
- O cliente do Configuration Manager 
- Todo o software implementado através do Configuration Manager que instalar PCs depois da política de proteção de dispositivos está a ser processada. 
- Atualizações de componentes do windows de:
    - Atualização do Windows
    - Atualização do Windows para empresas
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Estes itens não incluam qualquer software que é *não* incorporado no Windows que atualiza automaticamente o software da internet ou por terceiros atualizações se estiverem instalados através de qualquer um dos mecanismos de atualização mencionados anteriormente, ou a partir da internet. Apenas as alterações ao software que são implementadas através do cliente do Configuration Manager pode ser executado.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implementar políticas de Device Guard, leia as seguintes informações:

- Gestão de proteção de dispositivos é uma funcionalidade de pré-lançamento para o Configuration Manager e está sujeita a alterações.
- Para utilizar a proteção de dispositivos com o Configuration Manager, os PCs que gere tem de executar a versão do Windows 10 Enterprise 1703 ou posterior.
- Assim que uma política é processada com êxito num cliente PC, Configuration Manager é configurado como um instalador geridos em que o cliente e software implementado através do SCCM depois dos processos de política é automaticamente fidedigno. Software instalado pela configuração geridos antes dos processos de política do Device Guard não é fidedigno automaticamente.
- Os computadores cliente têm de ter conectividade ao respetivo controlador de domínio para uma política de proteção de dispositivo a ser processado com êxito.
- O agendamento de avaliação de compatibilidade predefinido para políticas Device Guard, configuráveis durante a implementação, é de 1 dia. Se os problemas no processamento da política são observados, pode ser vantajoso configurar a agenda de avaliação de compatibilidade para ser mais curto, por exemplo, cada hora. Esta agenda dita com que frequência os clientes questão processar uma política de Device Guard quando uma falha.
- Independentemente do modo de imposição que selecionar, ao implementar uma política de Device Guard, PCs não é possível executar aplicações de HTML com a extensão .hta de cliente.

## <a name="how-to-create-a-device-guard-policy"></a>Como criar uma política de proteção de dispositivos
1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.  No **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de proteção de dispositivos**.
3.  No **home page** separador o **criar** , clique em **criar política de proteção de dispositivos**.
4.  No **geral** página do **dispositivo Guard Assistente para criar política**, especifique as seguintes definições:
    - **Nome** -introduza um nome exclusivo para esta política Device Guard. 
    - **Descrição** - como opção, introduza uma descrição para a política que o ajuda a identificá-la na consola do Configuration Manager.
    - **Modo de imposição** -escolher um dos seguintes métodos de imposição para Device Guard no PC cliente.
        - **Imposição ativado** - apenas permitir permitidas a execução de executáveis fidedignas.
        - **Só de auditoria** - permitir a execução de todos os executáveis, mas não considerada como fidedigna registo executáveis que são executados no registo de eventos de cliente local.
5.  No **as inclusões** separador do **dispositivo Guard Assistente para criar política**, clique em **adicionar** se pretender opcionalmente adicionar confiança para ficheiros ou pastas específicos nos PCs. 
6.  No **adicionar confiança de ficheiro ou pasta** diálogo caixa, especifique informações sobre o ficheiro ou pasta que pretende confiança. Pode especificar um caminho de ficheiro ou pasta local ou ligar a um dispositivo remoto para o qual tem permissão para ligar e especifique um caminho de ficheiro ou pasta em que o dispositivo.
Ao adicionar confiança para ficheiros específicos para pastas numa política Device Guard, pode:
    - Ultrapassar problemas com os comportamentos de instalador gerido
    - Aplicações de linha de negócio de confiança que não não possível implementar com o Configuration Manager
    - As aplicações que estão incluídas numa imagem de implementação do sistema operativo de confiança. 
7.  Clique em **seguinte**, em seguida, conclua o assistente.

>[!IMPORTANT]
>A inclusão de pastas ou ficheiros fidedignos só é suportada em computadores cliente com a versão 1706 ou posterior do cliente do Configuration Manager. Se quaisquer regras de inclusão estão incluídas na política de proteção de dispositivos e a política, em seguida, for implementada para um PC com uma versão anterior no cliente do Configuration Manager de cliente, a política irá falhar sejam aplicadas. Atualizar destes clientes mais antigos serão resolver este problema. Políticas que não incluam quaisquer regras de inclusão ainda podem ser aplicadas em versões anteriores do cliente do Configuration Manager.

## <a name="how-to-deploy-a-device-guard-policy"></a>Como implementar uma política de proteção de dispositivos
1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.  No **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de proteção de dispositivos**.
3.  Na lista de políticas, selecione aquela que pretende implementar, e, em seguida, no **home page** separador o **implementação** , clique em **implementar**.
4.  No **implementar política de proteção de dispositivos** diálogo caixa, selecione a coleção à qual pretende implementar a política. Em seguida, configure uma agenda para quando os clientes avaliar a política. Por fim, selecione se o cliente pode avaliar a política fora de quaisquer janelas de manutenção configurada.
5.  Quando tiver terminado, clique em **OK** para implementar a política. 

Assim que a política é processada num cliente PC, um reinício é agendado em que o cliente em conformidade com a **as definições de cliente** para **reiniciar computador**.
Enquanto não reiniciar o cliente do PC, a política não entram em vigor.

## <a name="how-to-monitor-a-device-guard-policy"></a>Como monitorizar uma política de proteção de dispositivos

Utilize as informações de [monitorizar as definições de compatibilidade](/sccm/compliance/deploy-use/monitor-compliance-settings) tópico para ajudar a monitorizar a que a política implementada foi aplicada a todos os PCs corretamente.

Para monitorizar o processamento de uma política de Device Guard, utilize o seguinte ficheiro de registo no cliente PCs:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico que está a ser bloqueado ou auditada, consulte os seguintes registos de eventos do cliente local:

1.  Para bloquear e auditoria de ficheiros executáveis, utilize **registos de serviços e aplicações** > **Microsoft** > **Windows** > **integridade do código** > **operacional**.
2.  Para bloquear e auditoria do Windows Installer e os ficheiros de script, utilize **registos de serviços e aplicações** > **Microsoft** > **Windows** > **AppLocker** > **MSI e o Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para a proteção de dispositivos

- Nesta versão de pré-lançamento, não implementa políticas de proteção de dispositivos com o modo de imposição **só de auditoria** num ambiente de produção. Este modo destina-se para o ajudar a testar a capacidade de um laboratório apenas a definição.
- Dispositivos que tenham uma política implementada para os mesmos em **só de auditoria** ou **imposição ativada** modo, o que não foram reiniciados para impor a política são vulneráveis ao software não fidedigno que está a ser instalado.
Nesta situação, o software poderá continuar a permissão para ser executada mesmo que o reinício do dispositivo, ou recebe uma política no **imposição ativada** modo.
- Para garantir que a política de Device Guard efetiva, prepare o dispositivo num ambiente de laboratório. Em seguida, implemente o **imposição ativada** política e por fim, reiniciar o dispositivo antes de dar o dispositivo a um utilizador final.
- Não implemente uma política com **imposição ativada**e, em seguida, posteriormente, implementar uma política com **só de auditoria** ao mesmo dispositivo. Esta configuração poderá resultar em software não fidedigno que está a ser permitida a execução.
- Quando utilizar o Configuration Manager para ativar a integridade do código configuráveis no cliente PCs com as políticas de Device Guard, a política não impede que os utilizadores com direitos de administrador local circumventing a política de Device Guard ou caso contrário, executar software não fidedigno. 
- É a única forma de impedir que os utilizadores com direitos de administrador local da desativação de integridade do código configuráveis para implementar uma política de binária assinada. Esta implementação é possível através da política de grupo, mas não suportado atualmente no Configuration Manager.
- A definição de cópia de segurança do Configuration Manager como um instalador geridos em computadores de cliente utiliza a política de AppLocker. AppLocker só é utilizado para identificar os programas de instalação geridos e imposição de todos os acontece com a integridade do código configurável. 




