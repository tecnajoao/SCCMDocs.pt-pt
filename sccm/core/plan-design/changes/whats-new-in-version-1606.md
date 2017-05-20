---
title: Novo no System Center Configuration Manager atualizar 1606 | Documentos do Microsoft
description: "Obter informações sobre as alterações e novas capacidades introduzidas na versão 1606 do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 34809ddf7819eab5deb3995cd8138c7b38cd2f9a
ms.openlocfilehash: 9fdff6049d6e5cde1032864e5d7aa8df71e53686
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>O que &#39; s Novidades na versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1606 para System Center Configuration Manager está disponível como uma atualização na consola de sites instaladas anteriormente que executam a versão 1511 ou 1602. Versão 1511 é a linha de base inicial que utilizar para instalar novos sites do Configuration Manager.
> [!TIP]  
>  Saiba mais sobre:  
>   
>  -   [Instalar novos sites](/sccm/core/servers/deploy/install) (utilizando uma versão de linha de base como 1511)  
>  -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como atualizar 1602 ou 1606)  

 As secções seguintes fornecem detalhes sobre as alterações e funcionalidades novas, introduzidas na versão 1606 do Configuration Manager.  



## <a name="updatesandservicing"></a>As atualizações e manutenção

### <a name="changes-for-the-updates-and-servicing-node"></a>Alterações para as atualizações e a servir nó
Seguem-se as alterações para as atualizações e a servir nó na consola do Configuration Manager:
> [!NOTE]
> Estas alterações não estão disponíveis até depois de instalar a versão 1606.

- **Alteração do nome de nó:**

    No **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi mudado para **atualizações e o estado de manutenção**.
- **Obter mais detalhes de estado de instalação:**

    Quando visualiza o estado de instalação de atualização de um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (aplica-se apenas para o site de nível superior onde a função de sistema de sites de ponto de ligação de serviço é instalada.)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, agora é informações mais detalhadas sobre cada passo, incluindo o ficheiro de registo pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **administração** e **monitorização** áreas de trabalho, o **atualizações e a manutenção** nó inclui um novo botão no Friso denominado **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar os avisos de pré-requisitos (a partir de dentro do Assistente de atualização) e essa instalação de atualização halts devido a um aviso, em seguida, pode selecionar **ignorar os avisos de pré-requisitos** a partir do Friso. Isto aciona uma continuação da instalação de atualização automática.  



- **Vista de limpeza de atualizações:**

    No **atualizações e a manutenção** nó, agora verá apenas a atualização instalada mais recentemente e quaisquer novas atualizações que estão disponíveis para instalação. Para ver atualizações instaladas anteriormente, clique no novo **histórico** botão que aparece no Friso.  

-   **Opção cujo nome foi mudada de pré-produção:**

    No **atualizações e a manutenção** nó, o **opções de cliente** botão chama-se agora **promover cliente de pré-produção**.


###  <a name="pre-release-features"></a>Funcionalidades de pré-lançamento
A partir do 1606, deve fornecer consentimento para utilizar funcionalidades da versão de pré-lançamento do System Center Configuration Manager antes de poder selecionar e ativar a utilização. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Novo comportamento de atualização de ponto de distribuição
Atualização 1606 introduz alterações que melhoram a disponibilidade dos pontos de distribuição quando a instalação de atualizações futuras.

Após atualização 1606 está instalado, quando instala uma atualização desse site que requer a reinstalação automática do junto padrão e distribuição de solicitação funções de sistema de sites do ponto, todos os pontos de distribuição já não ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização a um subconjunto dos pontos de distribuição num determinado momento. O resultado é que alguns pontos de distribuição ficam offline para instalar a atualização. Isto permite que os pontos de distribuição que ainda não tiver começado atualizar, ou que concluiu a atualização, que deverá permanecer disponível online e poderá fornecer conteúdo aos clientes.



## <a name="accessibility"></a>Acessibilidade
Para navegar entre os nós diferentes de uma área de trabalho, pode agora introduzir a primeira letra do nome de um nó. Cada chave prima move o cursor para o nó seguinte que começa por essa letra. Para utilizadores que têm um leitor de ecrã, o leitor lê saber o nome desse nó. Para mais informações sobre as opções de acessibilidade, consulte o artigo [funcionalidades de acessibilidade no System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="administration"></a>Administração
Seguem-se as alterações à administração na consola do Configuration Manager:
### <a name="oms-connector"></a>Conector OMS

Agora pode ligar o Configuration Manager como coleções a partir do System Center Configuration Manager, para o [conjunto de aplicações de gestão de operações do Microsoft (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/). Isto torna visíveis na OMS dados, tais como coleções a partir de implementação do Configuration Manager. Pode encontrar mais informações, consulte o artigo [sincronizar dados do Configuration Manager para o conjunto de gestão de operações de Microsoft aqui](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

O conector OMS é uma funcionalidade pré-lançamento. Para ativá-lo, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Suporte para o tamanho da cache nas definições de cliente

Agora pode configurar o tamanho da pasta cache em computadores cliente com **definições de cliente** na consola do Configuration Manager. Anteriormente, só é possível definir o tamanho da cache do cliente ao instalar ou reinstalar o software de cliente. Agora pode especificar o tamanho da cache como uma definição de cliente (predefinido ou personalizado) e, em seguida, tem de reinstalar essas definições aplicadas com a seguinte atualização de política do cliente, sem necessidade de um cliente. Para obter mais informações, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local

### <a name="support-for-multiple-device-management-points"></a>Suporte para vários pontos de gestão de dispositivos

No local a gestão de dispositivos móveis (MDM) agora suporta uma nova funcionalidade no Windows 10 aniversário Update que configura automaticamente um dispositivo inscrito para ter mais do que um ponto de gestão de dispositivos disponível para utilização. Esta capacidade permite que o dispositivo reverter para outro ponto de gestão de dispositivos, quando um utiliza normalmente não está disponível. Esta capacidade funciona apenas para PCs e dispositivos com o Windows 10 aniversário Update instalado.


## <a name="application-management"></a>Gestão de aplicações

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gerir aplicações a partir da Loja Windows para Empresas

O [da loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações do Windows para a sua organização, quer seja individualmente ou no volume. Ao ligar-se no arquivo do Configuration Manager, pode sincronizar a lista de aplicações que tenha comprado com o Configuration Manager, ver na consola do Configuration Manager e implementá-las como faria com qualquer outra aplicação.

Para obter mais detalhes, consulte o artigo [gerir aplicações na loja Windows para empresas com o System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gerir as aplicações iOS adquiridos de volume

O fluxo de trabalho para gerir as aplicações iOS adquiridos de volume e implementar estas com o Configuration Manager, foi melhorado.

Para obter mais detalhes, consulte o artigo [gerir as aplicações iOS adquirido o volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interface de utilizador do Centro de software

A interface de utilizador do Centro de Software tem sido otimizada de mover para a deteção mais fácil.
*  O **estado da instalação** e **instalado Software** foram combinados separadores num único **estado da instalação** separador.
*  **Atualizações**, **sistemas operativos**, e **aplicações** foram separadas em três separadores separadas.
* Várias atualizações agora podem ser selecionadas para instalação em simultâneo, ou todas as atualizações podem ser instaladas em simultâneo clicando **instalar todas as**.

### <a name="content-status-links"></a>Ligações de estado do conteúdo
Nas propriedades de uma aplicação ou pacote, existe agora uma ligação que leva-o para o estado para esse objeto.

## <a name="software-updates"></a>Atualizações de software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Definição de cliente para gerir o agente de cliente do Office 365
Agora, pode utilizar uma definição para gerir o agente de cliente do Office 365 do cliente do Configuration Manager. Depois de configurar estas definições e implementar atualizações do Office 365, o agente do cliente do Configuration Manager é funciona com o agente de cliente do Office 365 para transferir e instalar atualizações do Office 365 a partir de um ponto de distribuição.

Para obter mais detalhes, consulte o artigo [gerir Office 365 ProPlus atualizações com o Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Mudar manualmente os clientes para um novo ponto de atualização de software
Atualmente, pode ativar uma opção que permita o comutador de clientes do Configuration Manager para um novo software de ponto de atualização quando existem problemas com o ponto de atualização de software ativo. Depois de ativada, os clientes irão procurar outro ponto de atualização de software na análise seguinte.

Para obter mais detalhes, consulte o artigo [planear atualizações de software no Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software
Quando uma atualização de software que requeira um reinício é implementada através do Configuration Manager e é instalada num computador, está agendado um reinício pendente. Também é apresentada uma caixa de diálogo de reinício. A partir do Configuration Manager versão 1606, as opções **atualização e reinicie** e **atualização e encerramento** estão disponíveis sempre que existe um reinício pendente para uma atualização de software do Configuration Manager. Estas estão disponíveis nas opções de energia do Windows de computadores Windows 10. Depois de utilizar uma das seguintes opções, a caixa de diálogo de reinício não serão apresentados depois de reiniciar o computador.

Para obter mais detalhes, consulte o artigo [planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Execute a análise de conformidade de atualizações de software imediatamente após um cliente instala as atualizações de software e o reinício
Agora pode executar uma análise da compatibilidade imediatamente após um cliente, instala as atualizações de software e o reinício. Definir esta opção para uma implementação, o **experiência de utilizador** página do Assistente de implementação Software atualizações, selecione **se qualquer atualização nesta implementação requer um reinício do sistema, execute as atualizações de ciclo de avaliação da implementação após o reinício**. Isto permite que o cliente para verificar a existência de atualizações de software adicional que se tornam aplicável após o cliente é reiniciado, a e, em seguida, para instalá-las (e se tornam compatíveis) durante a mesma janela de manutenção. Para obter mais detalhes, consulte o artigo [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates) ou [implementar manualmente atualizações de software](/sccm/sum/deploy-use/manually-deploy-software-updates).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Melhoramentos para o passo de sequência de tarefas: Instalar Atualizações de Software
Uma nova definição **avaliar as atualizações de software a partir dos resultados da análise em cache**, dá-lhe a opção de efetuar uma análise completa de atualizações de software, em vez de utilizar os resultados da análise em cache. Para obter mais detalhes, consulte o artigo [passos de sequência de tarefas no System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Além disso, uma nova variável sequência de tarefas, **SMSTSSoftwareUpdateScanTimeout**, está disponível. Esta variável permite-lhe controlar o tempo limite para a análise de atualizações de software durante o passo de sequência de tarefas instalar atualizações de Software. O valor predefinido é 30 minutos. Para obter mais detalhes, consulte o artigo [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida. Configuração do Windows a partir do Configuration Manager versão 1606, determina a letra de unidade melhor a utilizar (normalmente c:) durante a implementação do sistema operativo, por predefinição.

Para obter mais detalhes, consulte o artigo [no System Center Configuration Manager de variáveis incorporadas de sequência de tarefas](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizar o tamanho da janela de TFTP de disco de RAM para pontos de distribuição com PXE ativado
Agora pode personalizar o tamanho da janela de disco de RAM para pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá originar a transferência de imagem de arranque a falhar com um erro de tempo limite, porque o tamanho da janela é demasiado grande. A personalização de tamanho da janela de disco de RAM transferência protocolo TFTP (Trivial File) permite-lhe otimizar o tráfego TFTP quando estiver a utilizar o PXE para satisfazer os requisitos de rede específicas.

Para obter mais detalhes, consulte o artigo [preparar funções do sistema de sites para implementações do sistema operativo com o System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="smart-lock-setting-for-android-devices"></a>Definição de bloqueio de smart card para dispositivos Android
Uma nova definição **permitir o bloqueio de smart card e outros confiar agentes**, foi adicionado ao item de configuração Android e Samsung KNOX Standard.

Esta definição permite-lhe controlar a funcionalidade de bloqueio de smart card em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como "fidedignidade de agentes," permite-lhe desativar ou ignorar a palavra-passe do dispositivo bloqueio ecrã se o dispositivo estiver numa localização fidedigna. Por exemplo, pode ser uma localização fidedigna quando está ligado a um dispositivo Bluetooth específico, ou quando é próximo uma etiqueta de NFC. Pode utilizar esta definição para impedir que os utilizadores a partir da configuração de bloqueio de smart card.

Para obter mais detalhes, consulte o artigo [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Configuração do dispositivo e a proteção

### <a name="product-name-changes"></a>Alterações de nome de produto

* Microsoft Passport para o trabalho é agora conhecida como **Windows Hello para empresas**.
* Proteção de dados da empresa é agora conhecida como **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementação do Windows Hello para empresas (Passport para trabalho)

Pode agora implementar Windows Hello para as políticas de negócio para dispositivos Windows 10 associados a um domínio geridos pelo cliente do Configuration Manager.

Consola do Configuration Manager foi atualizada para refletir essas alterações.

### <a name="ios-activation-lock"></a>iOS bloqueio de ativação
Do Configuration Manager pode ajudar a gerir o iOS bloqueio de ativação, uma funcionalidade do encontrar a minha aplicação iPhone para iOS 7.1 ou posterior. Quando o Bloqueio de Ativação está ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:
* Desative a localizar o meu iPhone.
* Apagar o dispositivo.
* Reativar o dispositivo.

O Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação de duas formas:

- Ative o Bloqueio de Ativação em dispositivos supervisionados.
- Ignore o Bloqueio de Ativação em dispositivos supervisionados.

Para obter mais detalhes, consulte o artigo [gerir o iOS bloqueio de ativação com o System Center Configuration Manager](../../../mdm/deploy-use/manage-ios-activation-lock.md).


### <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender avançadas proteção ameaça

Endpoint Protection pode ajudar a gerir e monitorizar o Windows Defender avançadas ameaça proteção (ATP). Windows Defender ATP é um novo serviço que o irá ajudar empresas para detetar, analisar e responder a ataques avançadas nos redes deles. As políticas do Configuration Manager podem ajudá-lo carregar e monitorizar os computadores geridos a executar o Windows 10, versão 1607 (criar 14328) ou posterior.

Para obter mais detalhes, consulte o artigo [a proteção de ameaça avançada do Windows Defender](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorias de dispositivos
Pode criar categorias de dispositivo, o que podem ser utilizadas para colocar dispositivos coleções de dispositivos automaticamente quando está a utilizar o Configuration Manager com o Microsoft Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando estes inscreverem um dispositivo no Intune. Além disso, pode alterar a categoria de um dispositivo a partir da consola do Configuration Manager.

Para obter mais detalhes, consulte o artigo [como categorizar automaticamente dispositivos para coleções com o System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predeclare dispositivos com números de série IMEI ou iOS

Pode identificar dispositivos pertencentes ao importar os seus números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI do dispositivo, ou pode introduzir manualmente as informações de dispositivo. Informação importada define a propriedade dos dispositivos inscritos como "Empresa", nas listas de dispositivos. Uma licença do Intune é ainda necessária para cada utilizador que acedem ao serviço.

Para obter mais detalhes, consulte o artigo [Predeclare dispositivos com números de série IMEI ou iOS](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Comunicação do serviço de estado de funcionamento atestado no local

Atualmente, pode ativar a monitorização para Windows 10 PCs utilizando apenas a infraestrutura no local de serviços de atestado de estado de funcionamento, para que computadores sem Internet aceder pode relatório atestado de estado de funcionamento do dispositivo (DHA).

Para obter mais detalhes, consulte o artigo [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Controlo Remoto
Permitir que os utilizadores a oportunidade de aceitar ou recusar as transferências de ficheiros antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto. Os utilizadores só precisam conceder permissão uma vez por sessão e o Visualizador não tem a capacidade para conceder permissões para continuar com a transferência de ficheiros a próprios. Pode encontrar esta nova definição no **administração** área de trabalho. Aceda a **definições de cliente**e, em seguida, no **predefinições**, abra o **ferramentas remotas** painel.

