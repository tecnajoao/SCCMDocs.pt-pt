---
title: Como gerir o Windows Device Guard
titleSuffix: Configuration Manager
description: Saiba como utilizar o System Center Configuration Manager para gerir o Windows Device Guard.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb36d753c3ae05e1e38849709b417ac709281203
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127920"
---
# <a name="device-guard-management-with-configuration-manager"></a>Gestão de proteção de dispositivos com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="introduction"></a>Introdução
O Device Guard é um grupo de recursos do Windows 10 que foram concebidos para proteger os PCs contra software maligno e outro software não fidedigno. Evita que código mal-intencionado em execução, garantindo que apenas aprovado código, o que sabe, pode ser executado.

O Device Guard abrange tanto a software, como a funcionalidade de segurança baseada em hardware. Controlo de aplicações do Windows Defender é uma camada de segurança baseada em software que impõe uma lista explícita de software que pode ser executada num PC. Sozinho, o controlo de aplicações não tem os pré-requisitos de hardware ou de firmware. Políticas de controlo de aplicações implementadas com o Configuration Manager ativar uma política em PCs em coleções de destinadas que cumprem os requisitos de SKU descritos neste artigo e de versão mínima do Windows. Opcionalmente, a proteção baseada em hipervisor de políticas de controlo de aplicações implementadas através do Configuration Manager pode ser ativada por meio da diretiva de grupo em hardware compatível com.

Para saber mais sobre o Device Guard, veja a [guia de implementação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

   > [!NOTE]
   > Políticas de integridade de código configuráveis a partir do Windows 10, versão 1709, são conhecidas como controlo de aplicações do Windows Defender.

## <a name="using-device-guard-with-configuration-manager"></a>Usando o Device Guard com o Configuration Manager

Pode utilizar o Configuration Manager para implementar uma política de controlo de aplicações do Windows Defender. Esta política permite-lhe configurar o modo no qual Device Guard é executado em computadores numa coleção. 

Pode configurar um dos seguintes modos:

1.  **Imposição ativada** – só fidedigno executáveis podem ser executados.
2.  **Apenas auditoria** - permitir a execução de todos os executáveis, mas o registo não confiável executáveis que são executados no registo de eventos de cliente local.

>[!TIP]
>Nesta versão do Configuration Manager, o Device Guard é uma funcionalidade de pré-lançamento. Para ativá-la, consulte [no System Center Configuration Manager de funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>O que pode executar quando implementa uma política de controlo de aplicações do Windows Defender?

Windows Device Guard permite-lhe vivamente controlar o que pode ser executada em PCs que gere. Esta funcionalidade pode ser útil para PCs nos departamentos de alta segurança, onde é vital que não é possível executar o software indesejável.

Ao implementar uma política, normalmente, podem executar os executáveis seguintes:

- Componentes do sistema operativo Windows
- Controladores de centro de desenvolvimento de hardware (que têm assinaturas de Windows Hardware Quality Labs)
- Aplicações da Windows Store
- O cliente do Configuration Manager 
- Todo o software implementado através do Configuration Manager que PCs instalar depois da política de controlo de aplicações do Windows Defender é processada. 
- Atualizações de componentes do windows de:
    - Windows Update
    - Windows Update para empresas
    - Windows Server Update Services
    - Configuration Manager
    - Opcionalmente, software com uma boa reputação, conforme determinado pelo gráfico de segurança inteligente Microsoft (ISG). O ISG inclui o Windows Defender SmartScreen e outros serviços Microsoft. O dispositivo tem de executar Windows Defender SmartScreen e Windows 10 versão 1709 ou posterior para este software para ser confiável.

>[!IMPORTANT]
>Esses itens não inclua qualquer software que seja *não* incorporado no Windows que atualiza automaticamente o software da internet ou de terceiros da atualiza se eles são instalados por meio de qualquer um dos mecanismos de atualização mencionados anteriormente, ou a partir da internet. Apenas alterações de software que são implementadas no entanto pode executar o cliente do Configuration Manager.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implementar políticas de controlo de aplicações do Windows Defender, leia as seguintes informações:

- Gestão de proteção de dispositivos é uma funcionalidade de pré-lançamento para o Configuration Manager e está sujeitas a alterações.
- Para utilizar com o Configuration Manager de Device Guard, PCs que gere tem de executar o Windows 10 Enterprise versão 1703 ou posterior.
- Assim que uma política é processada com êxito num cliente de PC, o Configuration Manager está configurado como um instalador gerido no cliente. Software implementado através do mesmo, depois dos processos de política, é automaticamente fidedigno. Software instalado pelo Configuration Manager antes dos processos de política de controlo de aplicações do Windows Defender não é fidedigno automaticamente.
- PCs cliente tem de ter conectividade ao seu controlador de domínio para que uma política de controlo de aplicações do Windows Defender para ser processado com êxito.
- O agendamento de avaliação de compatibilidade predefinido para políticas de controlo de aplicações, configuráveis durante a implementação, é um dia. Se foram observados problemas no processamento da política, poderá ser vantajoso configurar a agenda de avaliação de conformidade para ser mais curto, por exemplo, a cada hora. Esta agenda dita a frequência com que os clientes repita a tentativa processar uma política de controlo de aplicações do Windows Defender se ocorrer uma falha.
- Independentemente do modo de imposição que selecionar, ao implementar uma política de controlo de aplicações do Windows Defender, o cliente de PCs não é possível executar aplicativos HTML com o HTA de extensão.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Como criar uma política de controlo de aplicações do Windows Defender
1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.  Na **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **controlo de aplicações do Windows Defender**.
3.  Sobre o **home page** separador a **criar** , clique em **política de controlo de aplicação criar**.
4.  Na **gerais** página do **Assistente de política de controlo de aplicações criar**, especifique as seguintes definições:
    - **Nome** -introduza um nome exclusivo para esta política de controlo de aplicações do Windows Defender. 
    - **Descrição** - como opção, introduza uma descrição para a política que o ajuda a identificá-la na consola do Configuration Manager.
    - **Impor um reinício de dispositivos, para que esta política pode ser imposta para todos os processos** -depois da política é processada num cliente de PC, um reinício está agendado no cliente, de acordo com o **definições de cliente** para  **Reinício do computador**.
        - Dispositivos com Windows 10 versão 1703 ou anterior sempre serão reiniciados automaticamente.
        - A partir do Windows 10 versão 1709, aplicativos em execução no dispositivo não terão a nova política de controlo de aplicações aplicada às mesmas até após um reinício. No entanto, os aplicativos iniciados após a política se aplica respeitará a nova política de controlo de aplicações. 
    - **Modo de imposição** -escolha um dos seguintes métodos de imposição para o Device Guard no PC cliente.
        - **Imposição ativada** – apenas permitir a execução são permitidos de executáveis fidedignos.
        - **Apenas auditoria** - permitir a execução de todos os executáveis, mas o registo não confiável executáveis que são executados no registo de eventos de cliente local.
5.  Na **as inclusões** separador da **política de controlo de aplicações criar assistente**, escolher se pretende **autorizar o software que é considerado fidedigno pelo gráfico de segurança inteligente**.
6. Clique em **adicionar** se pretender adicionar confiança para ficheiros ou pastas específicos em PCs. Na **adicione o ficheiro fidedigno ou pasta** caixa de diálogo, pode especificar um ficheiro local ou um caminho de pasta para confiar. Também pode especificar um caminho de pasta ou ficheiro num dispositivo remoto no qual tem permissão para ligar. Ao adicionar confiança para ficheiros ou pastas específicos de uma política de controlo de aplicações do Windows Defender, pode:
    - Resolver problemas com os comportamentos de instalador gerido
    - Confiar em aplicações de linha de negócio que não não possível implementar com o Configuration Manager
    - Confie em aplicações que estão incluídas numa imagem de implantação do sistema operativo. 
8.  Clique em **seguinte**, para concluir o assistente.

>[!IMPORTANT]
>A inclusão de ficheiros ou pastas fidedignas só é suportada em PCs de cliente com a versão 1706 ou posterior do cliente do Configuration Manager. Se quaisquer regras de inclusão estão incluídas numa política de controlo de aplicações do Windows Defender e a política, em seguida, é implementada para um PC com uma versão anterior do cliente do Configuration Manager de cliente, a política irá falhar a ser aplicado. Atualizar destes clientes mais antigos irá resolver este problema. Políticas que não incluem quaisquer regras de inclusão ainda podem ser aplicadas em versões anteriores do cliente do Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Como implementar uma política de controlo de aplicações do Windows Defender
1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2.  Na **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **controlo de aplicações do Windows Defender**.
3.  Na lista de políticas, selecione aquela que pretende implementar, e, em seguida, no **home page** separador a **implantação** , clique em **implementar política de controlo de aplicação**.
4.  Na **política de controlo de aplicações implementar** diálogo caixa, selecione a coleção à qual pretende implementar a política. Em seguida, configure uma agenda para quando os clientes avaliar a política. Por fim, selecione se o cliente pode avaliar a política de fora de quaisquer janelas de manutenção configurada.
5.  Quando tiver terminado, clique em **OK** para implementar a política. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Como monitorizar uma política de controlo de aplicações do Windows Defender

Utilize as informações no [monitorizar as definições de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings) artigo para ajudar a monitorizar o que a política implementada foi aplicada a todos os PCs corretamente.

Para monitorizar o processamento de uma política de controlo de aplicações do Windows Defender, utilize o ficheiro de registo seguinte nos PCs cliente:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar o software específico que está a ser bloqueado ou auditada, consulte os seguintes registos de eventos do cliente local:

1.  Para bloquear e auditoria de ficheiros executáveis, utilize **Applications and Services Logs** > **Microsoft** > **Windows**  >  **Integridade de código** > **operacional**.
2.  Para bloquear e auditoria do Windows Installer e arquivos de script, utilize **Applications and Services Logs** > **Microsoft** > **Windows**  >  **AppLocker** > **MSI e Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-device-guard"></a>Informações de segurança e privacidade para o Device Guard

- Nesta versão de pré-lançamento, não implementa políticas de controlo de aplicações do Windows Defender com o modo de imposição **auditoria apenas** num ambiente de produção. Este modo destina-se que o ajudarão a capacidade de teste num laboratório de configuração apenas.
- Dispositivos que têm uma política implementada na **apenas auditoria** ou **imposição ativada** modo que não ter sido reiniciada para impor a política, são vulneráveis a instalação de software não fidedigno.
Nesta situação, o software poderá continuar a ter permissão para ser executado mesmo se o dispositivo for reiniciado, ou recebe uma política no **imposição ativada** modo.
- Para garantir que a política de controlo de aplicações do Windows Defender está em vigor, prepare o dispositivo num ambiente de laboratório. Em seguida, implemente o **imposição ativada** política e por fim, reiniciar o dispositivo antes de o atribuir o dispositivo a um utilizador final.
- Não implemente uma política com **imposição ativada**e, em seguida, posteriormente, implementar uma política com **auditoria apenas** ao mesmo dispositivo. Esta configuração pode resultar em que está a ser permitida a execução de software não fidedigno.
- Quando utilizar o Configuration Manager para ativar o controlo de aplicações do Windows Defender em PCs cliente, a diretiva não impede que os utilizadores com direitos de administrador local de contornar as políticas de controlo de aplicações ou caso contrário, executar software não fidedigno. 
- É a única forma de impedir que os utilizadores com direitos de administrador local, desde desativar o controlo de aplicações implementar uma política de binária assinada. Esta implementação é possível por meio da diretiva de grupo mas não suportado atualmente no Configuration Manager.
- Configuração do Configuration Manager como um instalador gerido nos PCs cliente utiliza a política de AppLocker. O AppLocker só é utilizado para identificar geridos instaladores e imposição de todos os acontece com controlo de aplicações do Windows Defender. 




