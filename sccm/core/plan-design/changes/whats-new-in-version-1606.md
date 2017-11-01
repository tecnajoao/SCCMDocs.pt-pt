---
title: "Nova versão 1606"
titleSuffix: Configuraton Manager
description: "Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1606 do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: "40"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 346a1c7199a2d9dbb2cb174502adbb8d03a39f86
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>O que &#39; s novidade na versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1606 para o System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511 ou 1602. A versão 1511 é a versão de linha de base inicial que utilizar para instalar novos sites do Configuration Manager.
> [!TIP]  
>  Saiba mais sobre:  
>   
>  -   [Instalar novos sites](/sccm/core/servers/deploy/install) (utilizando uma versão de linha de base como a versão 1511)  
>  -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602 ou 1606)  

 As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1606 do Configuration Manager.  



## <a name="updatesandservicing"></a>Atualizações e manutenção

### <a name="changes-for-the-updates-and-servicing-node"></a>Alterações para as atualizações e manutenção de nó
Seguem-se as alterações para as atualizações e manutenção nó na consola do Configuration Manager:
> [!NOTE]
> Estas alterações não estão disponíveis até depois de instalar a versão 1606.

- **Alteração do nome de nó:**

    No **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi mudado para **atualizações e manutenção estado**.
- **Obter mais detalhes de estado da instalação:**

    Ao visualizar o estado de instalação de atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (aplica-se apenas para o site de nível superior em que a função de sistema de sites de ponto de ligação de serviço está instalada.)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, não há agora informações mais detalhadas de cada passo, incluindo o ficheiro de registo pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **administração** e **monitorização** áreas de trabalho, o **atualizações e manutenção** nó inclui um novo botão no Friso chamado **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar os avisos de pré-requisitos (de dentro do Assistente de atualização) e essa instalação de atualização forem devido a um aviso, em seguida, pode selecionar **ignorar os avisos de pré-requisitos** a partir do Friso. Isto aciona uma continuação da instalação da atualização automática.  



- **Vista de limpeza de atualizações:**

    No **atualizações e manutenção** nós, agora ver apenas a atualização instalada mais recentemente e novas atualizações que estão disponíveis para a instalação. Para ver atualizações instaladas anteriormente, clique no novo **histórico** botão que aparece no Friso.  

-   **Opção cujo nome foi alterada para pré-produção:**

    No **atualizações e manutenção** nó, o **opções de clientes** botão chama-se agora **promover o cliente de pré-produção**.


###  <a name="pre-release-features"></a>Funcionalidades de pré-lançamento
A partir do 1606, tem de dar consentimento para utilizar as funcionalidades de pré-lançamento no System Center Configuration Manager para poder selecionar e ativar a sua utilização. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Novo comportamento de atualização do ponto de distribuição
Atualização 1606 introduz alterações melhorar a disponibilidade dos pontos de distribuição quando instalar atualizações futuras.

Após a atualização 1606 está instalado, quando instala uma atualização nesse site que requer a reinstalação automática do seguinte funções do sistema de sites de ponto de standard e distribuição de solicitação, todos os pontos de distribuição já não fique offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização para um subconjunto dos pontos de distribuição em qualquer momento. O resultado é que alguns pontos de distribuição fique offline para instalar a atualização. Isto permite que os pontos de distribuição que ainda não ter iniciada atualizar ou que concluiu a atualização, permanecer online e é capaz de fornecer conteúdo aos clientes.



## <a name="accessibility"></a>Acessibilidade
Para navegar entre os nós de uma área de trabalho diferentes, agora pode introduzir a primeira letra do nome de um nó. Cada chave prima move o cursor para o próximo nó que comece com essa letra. Para utilizadores que tenham um leitor de ecrã, o leitor lê terminar o nome do nó. Para mais informações sobre as opções de acessibilidade, consulte [funcionalidades de acessibilidade no System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="administration"></a>Administração
Seguem-se as alterações à administração na consola do Configuration Manager:
### <a name="oms-connector"></a>Conector do OMS

Agora pode ligar o Configuration Manager como coleções do System Center Configuration Manager, para o [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/). Isto torna visíveis na OMS dados, tais como coleções da implementação do Configuration Manager. Encontrar mais informações, consulte [a sincronizar dados do Configuration Manager para o Microsoft Operations Management Suite aqui](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

O conector do OMS é uma funcionalidade de pré-lançamento. Para ativá-la, consulte o artigo [utilizar as funcionalidades de pré-lançamento das atualizações da](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Suporte para o tamanho da cache nas definições do cliente

Agora, pode configurar o tamanho da pasta cache nos computadores cliente com **as definições de cliente** na consola do Configuration Manager. Anteriormente, só foi possível definir o tamanho da cache do cliente ao instalar ou reinstalar o software de cliente. Agora pode especificar o tamanho da cache como uma definição de cliente (predefinido ou personalizado) e, em seguida, reinstalar essas definições aplicadas com a seguinte atualização de política do cliente, sem necessidade de um cliente. Para obter mais informações, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local

### <a name="support-for-multiple-device-management-points"></a>Suporte para vários pontos de gestão de dispositivos

No local a gestão de dispositivos móveis (MDM) suporta agora uma nova capacidade no Windows 10 aniversário da atualização que configura automaticamente um dispositivo inscrito tem mais do que um ponto de gestão de dispositivos disponível para utilização. Esta capacidade permite ao dispositivo reverter para outro ponto de gestão de dispositivos, quando um normalmente utiliza não está disponível. Esta capacidade funciona apenas para PCs e dispositivos com a atualização de aniversário do Windows 10 instalada.


## <a name="application-management"></a>Gestão de aplicações

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gerir aplicações a partir da Loja Windows para Empresas

O [loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações do Windows para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode sincronizar a lista de aplicações que comprou com o Configuration Manager, ver estes na consola do Configuration Manager e implementá-las, tal como faria com qualquer outra aplicação.

Para obter mais informações, consulte [gerir aplicações da loja Windows para empresas com o System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gerir aplicações compradas em volume do iOS

O fluxo de trabalho para aplicações iOS compradas em volume a gerir e implementar com o Configuration Manager, foi melhorado.

Para obter mais informações, consulte [gerir aplicações iOS compradas em volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interface de utilizador do Centro de software

A interface de utilizador do Centro de Software foi está mais simples para deteção mais fácil.
*  O **estado da instalação** e **instalado Software** separadores tem sido combinados numa única **estado da instalação** separador.
*  **Atualizações**, **sistemas operativos**, e **aplicações** foram separadas em três separadores separados.
* Agora é possível selecionar várias atualizações para a instalação de uma só vez, ou todas as atualizações podem ser instaladas em simultâneo, clicando em **instalar todas as**.

### <a name="content-status-links"></a>Ligações de estado do conteúdo
Nas propriedades de uma aplicação ou pacote, agora há uma ligação que leva-o para o estado para esse objeto.

## <a name="software-updates"></a>Atualizações de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Definição de cliente para gerir o agente do cliente do Office 365
Agora, pode utilizar uma definição para gerir o agente do cliente do Office 365 de cliente do Configuration Manager. Depois de configurar esta opção e implementar atualizações do Office 365, o agente do cliente do Configuration Manager funciona com o agente do cliente do Office 365 para transferir e instalar atualizações do Office 365 a partir de um ponto de distribuição.

Para obter mais informações, consulte [gerir o Office 365 ProPlus atualizações com o Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Mudar manualmente os clientes para um novo ponto de atualização de software
Agora, pode ativar uma opção que permite que o comutador de clientes do Configuration Manager para um novo software de um ponto de atualização quando existem problemas com o ponto de atualização de software ativo. Depois de ativada, os clientes irão procurar outro ponto de atualização de software na análise seguinte.

Para obter mais informações, consulte [planear atualizações de software no Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software
Quando uma atualização de software que requeira um reinício é implementada através do Configuration Manager e está instalada num computador, foi agendado um reinício pendente. Também é apresentada uma caixa de diálogo de reinício. A partir do Configuration Manager versão 1606, as opções **atualizar e reinicie** e **Update e no encerramento** estão disponíveis sempre que há um reinício pendente para uma atualização de software do Configuration Manager. Estes estão disponíveis nas opções de energia do Windows de computadores Windows 10. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não apresentará depois de reiniciar o computador.

Para obter mais informações, consulte [planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Executar a análise de compatibilidade de atualizações de software imediatamente após um cliente instala as atualizações de software e o reinício
Pode agora executar uma análise de compatibilidade imediatamente após um cliente, instala as atualizações de software e o reinício. Para definir esta opção para uma implementação, o **experiência de utilizador** página do Assistente de implementação Software atualizações, selecione **se alguma atualização nesta implementação exigir um reinício do sistema, execute o ciclo de avaliação da implementação após o reinício atualizações**. Isto permite que o cliente Verifique para atualizações de software adicionais que se tornam aplicáveis após o cliente é reiniciado e, em seguida, instalá-las (e se tornam compatíveis) durante a mesma janela de manutenção. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates) ou [implementar manualmente atualizações de software](/sccm/sum/deploy-use/manually-deploy-software-updates).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Melhoramentos para o passo de sequência de tarefas: Instalar Atualizações de Software
Uma nova definição, **avaliar atualizações de software a partir dos resultados de análise em cache**, dá-lhe a opção de efetuar uma análise completa para atualizações de software, em vez de utilizar os resultados da análise em cache. Para obter mais informações, consulte [passos de sequência de tarefas no System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Além disso, uma nova variável sequência de tarefas, **SMSTSSoftwareUpdateScanTimeout**, está disponível. Esta variável permite-lhe controlar o tempo limite para a análise de atualizações de software durante o passo de sequência de tarefas instalar atualizações de Software. O valor predefinido é 30 minutos. Para obter mais informações, consulte [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter foi preterido. A partir do Configuration Manager versão 1606, a configuração do Windows determina a letra de unidade melhor a utilizar (normalmente c) durante a implementação do sistema operativo, por predefinição.

Para obter mais informações, consulte [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizar o tamanho da janela de TFTP do disco de RAM para pontos de distribuição com PXE ativado
Agora, pode personalizar o tamanho da janela de disco de RAM para pontos de distribuição com PXE ativado. Se tiver personalizado a rede, causam a falhar com um erro de tempo limite, a transferência da imagem de arranque porque o tamanho da janela é demasiado grande. A personalização de tamanho de janela de disco de RAM ficheiro transferência protocolo Trivial (TFTP) permite-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os requisitos de rede específicos.

Para obter mais informações, consulte [preparar funções do sistema de sites para implementações do sistema operativo com o System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="smart-lock-setting-for-android-devices"></a>Definição de bloqueio inteligente para dispositivos Android
Uma nova definição, **permitir Smart Lock e outros agentes de confiança**, foi adicionada para o item de configuração do Android e Samsung KNOX Standard.

Esta definição permite-lhe controlar a funcionalidade de bloqueio do smart card em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como "agentes de confiança", permite desativar ou ignorar a palavra-passe da ecrã de bloqueio do dispositivo se o dispositivo estiver numa localização fidedigna. Por exemplo, numa localização fidedigna pode ser quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores configurem o bloqueio do smart card.

Para obter mais informações, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Proteção e de configuração do dispositivo

### <a name="product-name-changes"></a>Alterações de nome de produto

* Microsoft Passport for Work é agora conhecido como **Windows Hello para empresas**.
* Proteção de dados empresariais é agora conhecida como **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementação do Windows Hello para empresas (o Passport for Work)

Pode agora implementar Windows Hello para as políticas de negócio para dispositivos Windows 10 associados a domínios geridos pelo cliente de Configuration Manager.

Consola do Configuration Manager foi atualizada para refletir estas alterações.

### <a name="ios-activation-lock"></a>Bloqueio de ativação de iOS
O Configuration Manager pode ajudar a gerir o bloqueio de ativação, uma funcionalidade de encontrar iOS a minha aplicação iPhone para iOS 7.1 ou dispositivos posteriores. Quando o Bloqueio de Ativação está ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:
* Desative encontrar o meu iPhone.
* Apagar o dispositivo.
* Reative o dispositivo.

O Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação de duas formas:

- Ative o Bloqueio de Ativação em dispositivos supervisionados.
- Ignore o Bloqueio de Ativação em dispositivos supervisionados.

Para obter mais informações, consulte [gerir o bloqueio de ativação com o System Center Configuration Manager iOS](../../../mdm/deploy-use/manage-ios-activation-lock.md).


### <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

Proteção de ponto final pode ajudar a gerir e monitorizar o Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP é um novo serviço que o irão ajudar as empresas para detetar, analisar e responder a ataques avançados nas respetivas redes. Políticas do Gestor de configuração podem ajudá-lo com a sua integração e monitorizar os computadores geridos com o Windows 10, versão 1607 (criar 14328) ou posterior.

Para obter mais informações, consulte [Windows Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorias de dispositivos
Pode criar categorias de dispositivo, que podem ser utilizadas para colocar dispositivos em coleções de dispositivos automaticamente quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando inscreverem um dispositivo no Intune. Além disso, pode alterar a categoria de um dispositivo a partir da consola do Configuration Manager.

Para obter mais informações, consulte [como categorizar automaticamente os dispositivos em coleções com o System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série iOS ou IMEI

Pode identificar dispositivos pertencentes ao importar os números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) contendo os números IMEI de dispositivo ou pode introduzir manualmente as informações do dispositivo. Informação importada define a propriedade dos dispositivos inscritos como "Empresa" nas listas de dispositivos. Uma licença do Intune é ainda necessária para cada utilizador que acede ao serviço.

Para obter mais detalhes, consulte [pré-declarar dispositivos com números de série iOS ou IMEI](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Comunicação do serviço de atestado de estado de funcionamento no local

Agora, pode ativar os serviços de atestado de estado de funcionamento para Windows 10 PCs a monitorização utilizando apenas a infraestrutura no local, para que computadores sem Internet aceder pode relatório de atestado de estado de funcionamento do dispositivo (DHA).

Para obter mais informações, consulte [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Controlo Remoto
Permitir que os utilizadores a oportunidade de aceitar ou recusar as transferências de ficheiros antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto. Os utilizadores só têm de conceder permissão, uma vez por sessão e o Visualizador não tem a capacidade de conceder si próprios permissão para continuar com a transferência de ficheiros. Pode encontrar esta nova definição no **administração** área de trabalho. Aceda a **as definições de cliente**e, em seguida, no **predefinições**, abra o **ferramentas remotas** painel.
