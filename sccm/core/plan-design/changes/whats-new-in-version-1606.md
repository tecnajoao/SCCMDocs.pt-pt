---
title: Novidades na versão 1606
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1606 do System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0d45586267e06185752f597549f798be19d4d47b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897054"
---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para o System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511 ou 1602 a atualização 1606. A versão 1511 é a versão de linha de base inicial que utilizar para instalar novos sites do Configuration Manager.
> [!TIP]  
>  Saiba mais sobre:  
>   
>  -   [Instalar novos sites](/sccm/core/servers/deploy/install) (usando uma versão de linha de base como a versão 1511)  
>  -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602 ou 1606)  

 As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1606 do Configuration Manager.  



## <a name="updatesandservicing"></a>As atualizações e manutenção

### <a name="changes-for-the-updates-and-servicing-node"></a>Alterações para atualizações e manutenção de nó
Seguem-se as alterações para atualizações e manutenção do nó na consola do Configuration Manager:
> [!NOTE]
> Estas alterações não estão disponíveis até depois de instalar a versão 1606.

- **Alteração de nome de nó:**

    Na **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi alterado para **atualizações e estado de manutenção**.
- **Obter mais detalhes de estado de instalação:**

    Ao visualizar o estado de instalação de atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (Isto aplica-se apenas para o site de nível superior onde a função de sistema de sites de ponto de ligação de serviço está instalada.)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, existe agora informações mais detalhadas para cada passo, incluindo o ficheiro de registo pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **administração** e **monitorização** áreas de trabalho, o **atualizações e manutenção** nó inclui um novo botão da faixa de opções chamada **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar avisos de pré-requisitos (de dentro do Assistente de atualização) e essa instalação de atualização pára devido a um aviso, em seguida, pode selecionar **ignorar avisos de pré-requisitos** do faixa de opções. Isto aciona uma continuação automática a instalação da atualização.  



- **Exibição mais clara de atualizações:**

    Na **atualizações e manutenção** nó, agora, ver apenas a atualização instalada mais recentemente e quaisquer novas atualizações que estão disponíveis para instalação. Para ver atualizações instaladas anteriormente, clique no novo **histórico** botão é exibido na faixa de opções.  

-   **Opção de nome mudada para pré-produção:**

    Na **atualizações e manutenção** nó, o **opções de clientes** botão agora é chamado **promover cliente de pré-produção**.


###  <a name="pre-release-features"></a>Funcionalidades de pré-lançamento
A partir da versão 1606, tem de dar consentimento para utilizar as funcionalidades de pré-lançamento no System Center Configuration Manager antes de poder selecionar e ativar a respetiva utilização. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Novo comportamento de atualização de ponto de distribuição
Atualização 1606 introduz alterações que melhoram a disponibilidade dos pontos de distribuição quando instalar atualizações futuras.

Após a atualização 1606 estiver instalado, quando em seguida, instalar uma atualização nesse site que exige a reinstalação automática do standard e distribuição de extração funções de sistema de sites do ponto, todos os pontos de distribuição já não ficam offline para atualizar, ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização para um subconjunto dos pontos de distribuição num determinado momento. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Isso permite que os pontos de distribuição que não tenham começado a atualizar ou que concluiu a atualização, para permanecer online e capaz de fornecer conteúdo aos clientes.



## <a name="accessibility"></a> Acessibilidade
Para navegar entre os nós de diferentes de uma área de trabalho, agora pode inserir a primeira letra do nome de um nó. Cada pressionamento de tecla move o cursor para o próximo nó que começa com essa letra. Para utilizadores que têm um leitor de tela, o leitor lê o nome de um nó. Para obter mais informações sobre as opções de acessibilidade, consulte [funcionalidades de acessibilidade no System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="administration"></a>Administração
Seguem-se as alterações à administração na consola do Configuration Manager:
### <a name="oms-connector"></a>Conector do OMS

Pode agora ligar o Configuration Manager como coleções do System Center Configuration Manager, para o [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/). Isso torna visível no OMS dados, como coleções da sua implementação do Configuration Manager. Encontrar mais informações, consulte [a sincronizar dados do Configuration Manager para o Microsoft Operations Management Suite aqui](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

O conector do OMS é uma funcionalidade de pré-lançamento. Para ativá-la, consulte [utilizar as funcionalidades de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Suporte para o tamanho da cache nas definições do cliente

Agora pode configurar o tamanho da pasta cache em computadores cliente com **definições de cliente** na consola do Configuration Manager. Anteriormente, apenas pode definir o tamanho da cache do cliente ao instalar ou reinstalar o software de cliente. Agora, pode especificar o tamanho da cache como uma definição de cliente (padrão ou personalizado) e, em seguida, tem de reinstalar essas definições aplicadas com a próxima atualização de política do cliente, sem a necessidade de um cliente. Para obter mais informações, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local

### <a name="support-for-multiple-device-management-points"></a>Suporte para vários pontos de gestão de dispositivos

No local a gestão de dispositivos móveis (MDM) suporta agora uma nova capacidade na atualização de aniversário do Windows 10 que configura automaticamente um dispositivo inscrito para ter mais do que um ponto de gestão de dispositivos disponível para utilização. Esta capacidade permite ao dispositivo reverter para outro ponto de gestão de dispositivos, quando um normalmente utiliza não está disponível. Esta funcionalidade só funciona para PCs e dispositivos com a atualização de aniversário do Windows 10 instalada.


## <a name="application-management"></a>Gestão de aplicações

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gerir aplicações a partir da Loja Windows para Empresas

O [Windows Store para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e comprar aplicações Windows para a sua organização, individualmente ou em volume. Ao ligar a loja para o Configuration Manager, pode sincronizar a lista de aplicações que comprou com o Configuration Manager, visualizá-las na consola do Configuration Manager e implementá-las como faria com qualquer outra aplicação.

Para obter detalhes, consulte [gerir aplicações a partir da Windows Store para empresas com o System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gerir aplicações iOS compradas em volume

O fluxo de trabalho para gerir aplicações iOS compradas em volume e implementar com o Configuration Manager, foi melhorado.

Para obter detalhes, consulte [gerir aplicações de iOS compradas em volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interface de utilizador do Centro de software

A interface de utilizador do Centro de Software foi otimizada para a deteção mais fácil.
*  O **estado de instalação** e **Software instalado** separadores foram combinados num único **estado da instalação** separador.
*  **As atualizações**, **sistemas operativos**, e **aplicativos** foram separados em três guias separados.
* Agora podem ser selecionadas várias atualizações para instalação de uma só vez ou todas as atualizações podem ser instaladas ao mesmo tempo, ao clicar em **instalar todos os**.

### <a name="content-status-links"></a>Ligações de estado do conteúdo
Nas propriedades de uma aplicação ou pacote, agora há um link que leva-o para o estado para esse objeto.

## <a name="software-updates"></a>Atualizações de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Definição de cliente para gerir o agente de cliente do Office 365
Agora, pode utilizar uma definição para gerir o agente do cliente do Office 365 de cliente do Configuration Manager. Depois de configurar estas definições e implementar atualizações do Office 365, o agente do cliente do Configuration Manager funciona com o agente do cliente do Office 365 para transferir e instalar atualizações do Office 365 a partir de um ponto de distribuição.

Para obter detalhes, consulte [com o Gestor de configuração de atualizações de gerir o Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Mudar manualmente clientes para um novo ponto de atualização de software
Agora pode ativar uma opção que permite que o comutador de clientes do Configuration Manager para um novo software de ponto de atualização quando existirem problemas com o ponto de atualização de software ativo. Depois de ativada, os clientes irão procurar outro ponto de atualização de software na análise seguinte.

Para obter detalhes, consulte [planear atualizações de software no Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software
Quando uma atualização de software que requeira um reinício é implementada utilizando o Configuration Manager e está instalada num computador, é agendado um reinício pendente. Também é apresentada uma caixa de diálogo de reinício. A partir do Configuration Manager versão 1606, as opções **atualizar e reiniciar** e **atualizar e encerrar** estão disponíveis sempre que existe um reinício pendente para uma atualização de software do Configuration Manager . Estas estão disponíveis as opções de energia do Windows de computadores Windows 10. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não serão apresentadas quando o computador for reiniciado.

Para obter detalhes, consulte [planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Executar análise de conformidade de atualizações de software imediatamente após um cliente de atualizações de software de instalações e reinícios do
Agora, pode executar uma análise de compatibilidade imediatamente após um cliente instala as atualizações de software e reinicializações. Para definir esta opção no tendo em vista uma implementação, o **experiência de utilizador** página do Assistente de implementação Software atualizações, selecione **se alguma atualização nesta implementação exigir um reinício do sistema, execute o ciclo de avaliação de implementação após atualizações reiniciar**. Isto permite ao cliente verificar a existência de atualizações de software adicionais que se tornam aplicáveis após o cliente é reiniciado e, em seguida, instalá-las (e ficam em conformidade) durante a mesma janela de manutenção. Para obter detalhes, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates) ou [implementar manualmente atualizações de software](/sccm/sum/deploy-use/manually-deploy-software-updates).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Melhorias para o passo de sequência de tarefas: Instalar Atualizações de Software
Uma nova definição **avaliar atualizações de software nos resultados da análise em cache**, lhe dá a opção para fazer uma análise completa de atualizações de software, em vez de usar os resultados da análise em cache. Para obter detalhes, consulte [passos de sequência de tarefas no System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Além disso, uma nova variável sequência de tarefas, **SMSTSSoftwareUpdateScanTimeout**, está disponível. Esta variável permite-lhe controlar o tempo limite para a análise de atualizações de software durante o passo de sequência de tarefas instalar atualizações de Software. O valor predefinido é 30 minutos. Para obter detalhes, consulte [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida. A partir do Configuration Manager versão 1606, o programa de configuração do Windows determina a melhor letra de unidade a utilizar (normalmente c) durante a implementação do sistema operativo, por predefinição.

Para obter detalhes, consulte [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizar o tamanho da janela de TFTP de Ramdisk baseada em pontos de distribuição com PXE ativado
Agora pode personalizar o tamanho da janela de Ramdisk baseada em pontos de distribuição com PXE ativado. Se tiver personalizado a rede, pode causar falha com um erro de tempo limite, a transferência da imagem de arranque, porque o tamanho da janela é demasiado grande. A personalização de tamanho de janela de Ramdisk baseada em ficheiro protocolo TFTP (Trivial Transfer) permite-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os seus requisitos de rede específicas.

Para obter detalhes, consulte [preparar funções do sistema de sites para implementações do sistema operativo com o System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="smart-lock-setting-for-android-devices"></a>Definição de bloqueio inteligente para dispositivos Android
Uma nova definição **permitir Smart Lock e outros agentes de confiança**, foi adicionada para o item de configuração do Android e Samsung KNOX Standard.

Esta definição permite-lhe controlar a funcionalidade Smart Lock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como "agentes de fidedignidade," permite-lhe desativar ou ignorar a palavra-passe de ecrã do bloqueio de dispositivo se o dispositivo estiver numa localização fidedigna. Por exemplo, um local confiável pode ser quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores configurem o Smart Lock.

Para obter detalhes, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerido sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Configuração do dispositivo e a proteção

### <a name="product-name-changes"></a>Alterações de nome de produto

* Microsoft Passport for Work é agora conhecido como **Windows Hello para empresas**.
* Proteção de dados empresariais é agora conhecida como **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementação do Windows Hello para empresas (Passport for Work)

Pode agora implementar Windows Hello para políticas de negócio para dispositivos Windows 10 associados a domínios geridos pelo cliente do Configuration Manager.

Consola do Configuration Manager foi atualizada para refletir estas alterações.

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS
O Configuration Manager pode ajudar a gerir o bloqueio de ativação, uma funcionalidade do veja iOS a minha aplicação do iPhone para iOS 7.1 e dispositivos posteriores. Quando o Bloqueio de Ativação está ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:
* Desative encontrar o meu iPhone.
* Apagar o dispositivo.
* Reative o dispositivo.

O Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação de duas formas:

- Ative o Bloqueio de Ativação em dispositivos supervisionados.
- Ignore o Bloqueio de Ativação em dispositivos supervisionados.

Para obter detalhes, consulte [gerir o bloqueio de ativação com o System Center Configuration Manager iOS](../../../mdm/deploy-use/manage-ios-activation-lock.md).


### <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Windows Defender

Proteção de ponto de extremidade pode ajudar a gerir e monitorizar a proteção de ameaças avançada do Windows Defender (ATP). Windows Defender ATP é um serviço novo que irá ajudar as empresas a detetar, investigar e responder a ataques avançados em suas redes. As políticas do Configuration Manager podem ajudá-lo a integrar e monitorizar os computadores geridos com o Windows 10, versão 1607 (build 14328) ou posterior.

Para obter detalhes, consulte [a proteção de ameaças avançada do Windows Defender](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorias de dispositivos
Pode criar categorias de dispositivos, que podem ser utilizadas para colocar dispositivos em coleções de dispositivos automaticamente quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Em seguida, os utilizadores têm de escolher uma categoria de dispositivo quando estes inscrevem um dispositivo no Intune. Além disso, pode alterar a categoria de um dispositivo a partir da consola do Configuration Manager.

Para obter detalhes, consulte [como automaticamente categorizar dispositivos em coleções com o System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série IMEI ou iOS

É possível identificar os dispositivos pertencentes ao importar os números do internacional do equipamento móvel (IMEI) de identidade ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI de dispositivos ou pode introduzir manualmente as informações do dispositivo. Informação importada define a propriedade dos dispositivos que são inscritos como "Corporate" nas listas de dispositivos. Uma licença do Intune ainda é necessária para cada utilizador que acede ao serviço.

Para obter mais detalhes, consulte [pré-declarar dispositivos com números de série IMEI ou iOS](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Comunicação do serviço de atestado de estado de funcionamento no local

Agora pode ativar a monitorização para Windows 10 PCs ao utilizar apenas a infraestrutura no local de serviços de atestado de estado de funcionamento, para que computadores sem Internet acessam pode relatório de atestado de estado de funcionamento do dispositivo (DHA).

Para obter detalhes, consulte [atestado de estado de funcionamento do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Controlo Remoto
Permitir que os utilizadores a oportunidade de aceitar ou recusar as transferências de ficheiros antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto. Os utilizadores apenas têm de conceder permissão, uma vez por sessão, e o Visualizador não tem a capacidade para atribuir permissão para prosseguir com a transferência de ficheiros. Pode encontrar esta nova definição no **administração** área de trabalho. Aceda a **definições de cliente**e, em seguida, no **predefinições**, abra a **ferramentas remotas** painel.
