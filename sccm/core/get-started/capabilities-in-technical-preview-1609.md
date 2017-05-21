---
title: "Capacidades na pré-visualização técnica 1609 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1609."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 89a41c8a3137d0e54011ddf9a1d9b4894ecb7df8
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1609 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1609. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    

**Problemas conhecidos neste pré-visualização técnica:**  
*  Quando atualizar para a pré-visualização técnica do Configuration Manager 1609, serão eliminadas quaisquer políticas de atualização de edição que tiver implementado. Para continuar a utilizar estas políticas, tem de recriar e implementá-las.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improvements-to-endpoint-protection"></a>Melhoramentos no Endpoint Protection
Melhoramento para definições de política de proteção contra software maligno do Endpoint Protection - já pode especificar o nível no qual o serviço de proteção de nuvem do Endpoint Protection irá bloquear ficheiros suspeitos. Uma nova definição permite aos administradores especificar os computadores "arriscados" as quantidades de software maligno que se deparam elevadas.

## <a name="increased-number-of-enrolled-devices"></a>Aumento do número de dispositivos inscritos
Os administradores agora podem permitir que os utilizadores a inscrição de até 15 dispositivos na gestão de dispositivos móveis híbrida com o Intune. O limite anteriormente era de 5 dispositivos por utilizador.

## <a name="additional-apple-dep-settings"></a>Definições adicionais do DEP da Apple

Os administradores agora podem configurar as seguintes definições do programa de inscrição de dispositivos da Apple (DEP) no perfil de DEP para iOS e dispositivos de Mac:
- **ID de toque**
- **Zoom**
- **Siri**

Se estiver ativada, o Assistente de configuração da Apple pede-lhe para este serviço durante a ativação do dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integração com a análise de atualização

Análise de atualização permite-lhe avaliar e analisar a compatibilidade com o Windows 10 e preparação do dispositivo para permitir que as atualizações mais facilmente e mais suaves. Com a integração de análise de atualização com o Configuration Manager, pode aceder aos dados de atualização de compatibilidade na consola de administração do Configuration Manager e, em seguida, na lista de dispositivos de destino dispositivos para a atualização ou a remediação.

Pode ler mais sobre como atualizar o sistema analítico no [introdução ao atualizar Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Perfis de VPN híbrida de tipos de ligação nativo do Windows 10

Ao utilizar o Configuration Manager com o Intune, agora pode criar perfis VPN do Windows 10 com Microsoft Automatic, IKEv2, PPTP e L2TP tipos de ligação na consola do Configuration Manager sem utilizar o OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhoramentos à loja Windows para a integração de negócio com o Configuration Manager

Nesta versão, iremos atualizou [da loja Windows para a integração de empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) com estas novas funcionalidades:

**Atualização:** Na versão de pré-visualização técnica atual, a funcionalidade de sincronização imediata não está funcional.

- Anteriormente, apenas pode implementar aplicações gratuitas da loja Windows para empresas. Gestor de configuração agora adicionalmente suporta implementar pago online licenciado aplicações (para dispositivos do Intune inscritos apenas).
- Agora pode iniciar uma sincronização imediata entre a loja Windows para empresas e do Configuration Manager.
- Agora pode modificar a chave de segredo de cliente obtidas a partir do Azure Active Directory

### <a name="try-it-out"></a>Experimente!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Comprar e sincronizar uma aplicação licenciada online paga

1. Compre uma aplicação licenciada online paga na loja Windows para empresas.
2. No **administração** área de trabalho da consola do Configuration Manager, clique em **serviços em nuvem** > **atualizações e a manutenção** > **da loja Windows para empresas**.
3. No **base** separador o **sincronização** grupo, clique em **sincronizar agora**.
4. Logo que posteriormente, a aplicação que adquiriu aparecerá no **informações de licença de aplicações da loja** nó do **gestão de aplicações** área de trabalho.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Criar e implementar uma aplicação do Configuration Manager a partir de dados da aplicação sincronizados

O procedimento para criar e implementar uma aplicação do Configuration Manager a partir de uma aplicação da loja paga é igual ao criar uma aplicação a partir de uma aplicação gratuita. Consulte a secção **criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação de empresas** no [gerir aplicações na loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modifique a chave de segredo do cliente a partir do Azure Active Directory

1. No **administração** área de trabalho da consola do Configuration Manager, clique em **serviços em nuvem** > **atualizações e a manutenção** > **da loja Windows para empresas**.
2. Selecione a loja Windows para a conta de empresa e, em seguida, clique em **propriedades**.
3. No **loja Windows para propriedades da conta de negócio** diálogo caixa, introduza uma nova chave no **chave de segredo do cliente** de campo e, em seguida, clique em **Verifique se**. Depois de verificar, clique em **aplicar**, em seguida, feche a caixa de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de compatibilidade para itens de configuração

Adicionámos muitas novas definições que pode utilizar nos seus itens de configuração de várias plataformas de dispositivo.
Estas são as definições que anteriormente existiam no Microsoft Intune numa configuração isolada e estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Se precisar de ajuda com qualquer uma destas definições, abra [gerir as definições e funcionalidades nos seus dispositivos com as políticas do Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies) e, em seguida, selecione o subtópico definições para a plataforma que pretende.


### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android

#### <a name="password-settings"></a>Definições de palavra-passe

- **Memorizar histórico de palavra-passe**
- **Permitir desbloqueio desbloquear**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de janelas pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação

- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir armazenamento amovível**
- **Permitir partilha de Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir chamadas em roaming**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir Assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**


### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe é exigida**
- **Memorizar histórico de palavra-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos de Mac OS X

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**
- **Minutos de inatividade antes de screensaver ativa**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos móveis e de ambiente de trabalho do Windows 10

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavra-passe**
- **Exigir uma palavra-passe quando o dispositivo devolve a partir de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória no dispositivo móvel**
- **Permitir manual unenrollment**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir VPN por rede móvel**
- **Permitir roaming de VPN por rede móvel**
- **Permitir a reposição de telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações do Centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team

#### <a name="device-settings"></a>Definições do dispositivo

- **Ativar as informações operacionais do Azure**
- **Ativar Miracast sem fios projeção**
- **Escolha as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL da imagem de fundo Lockscreen**


### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações do Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Tipo de palavra-passe obrigatório**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração de palavra-passe (dias)**
- **Memorizar histórico de palavra-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir deteção automática de rede intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações do Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir ligação automática a hotspots Wi-Fi**


## <a name="improvements-for-boundary-groups"></a>Melhoramentos na cópia de grupos de limites
Esta pré-visualização introduz alterações importantes para os grupos de limites e como funcionam com pontos de distribuição. Estas alterações ajudará a simplificar a estrutura da sua infraestrutura de conteúdo ao dando-lhe mais controlo sobre como e quando pontos como localizações de origem de conteúdo de contingência de clientes para pesquisar distribuição adicionais. Isto inclui no local e os pontos de distribuição baseado na nuvem.

Estes melhoramentos substituir conceitos e comportamentos poderá estar familiarizado com hoje (como configurar pontos de distribuição para ser rápida ou lenta) e substitui-os com um novo modelo que deve ser mais fácil de configurar e manter. Estas alterações também são bases para que as alterações futuras que irão melhorar a outras funções de sistema do site que efetuada a associação a grupos de limites.  

Durante a atualização para 1609, a atualização converte das configurações de grupo de limites atuais para ajustar o novo modelo de modo a que estas alterações não incomodar as configurações de distribuição de conteúdo (consulte [atualizar grupos de limites existentes para o novo modelo](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)).

As secções seguintes descrevem pormenorizadamente as alterações introduzidas com esta pré-visualização, como o novo modelo funciona e que pode esperar quando atualizar um site que já tenha configurados os grupos de limites.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Alterações na IU e o comportamento para grupos de limites e localizações de conteúdo
Seguem-se chave alterações aos grupos de limites e como os clientes localizarem conteúdo. Muitas destas alterações e conceitos trabalhar em conjunto.
-    **Configurações para rápida ou lenta são removidas:** Já não configurar pontos de distribuição individuais para serem rápida ou lenta.  Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Devido a esta alteração, o **referências** separador da folha de propriedades do grupo de limites já não suporta a configuração rápida ou lenta.
-     **Novo grupo de limites predefinidos em cada site:**  Cada site primário tem um novo grupo de limites predefinidos, com o nome ***limites-grupo de predefinido-Site\<sitecode >***.  Quando um cliente não se encontre numa localização de rede que está atribuída a um grupo de limites, esse cliente utilizará os sistemas de sites associados ao grupo predefinido do site atribuído. Planear a utilização deste grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.      
 -    **'Permitir localizações de origem de contingência para conteúdo'** é removido: Configurar um ponto de distribuição para ser utilizado para contingência já não explicitamente, e as opções para configurar estas são removidas da IU.

    Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação tipo para aplicações foi alterado. Esta definição agora num tipo de implementação permite que um cliente para utilizar o grupo de limites de site predefinidos como uma localização de origem de conteúdo.

 -    **Relações de grupos de limites:** Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que são configuradas no separador de propriedades do grupo de limites novo com o nome **relações**:
     -    Cada grupo de limites que está diretamente associado um cliente é designado por um **atual** grupo de limites.  
    -     Nenhum grupo de limites um cliente pode utilizar devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo chama-se um **vizinho** grupo de limites.
    -  É o **relações** separador que adicionar grupos de limites que podem ser utilizados como um *vizinho* grupo de limites. Também pode configurar um período de tempo em minutos que determina quando um cliente que não consegue localizar conteúdo num ponto de distribuição no *atual* grupo irá começar a procurar em localizações de conteúdo às *vizinho* grupos de limites.

        Quando adicionar ou alterar uma configuração do grupo de limites, terá a opção para bloquear contingência a esse grupo de limites específicos do grupo atual que estiver a configurar.

    Para utilizar a nova configuração, define associações explícitas (ligações) a partir de um grupo de limites para outro e configurar todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. Determina o tempo que configura quando um cliente que não consegue localizar uma origem de conteúdo a partir do respetivo *atual* grupo de limites, pode começar a procurar fontes de conteúdo a partir desse grupo de limites de vizinho.

    Para além dos grupos de limites que configurar explicitamente, cada grupo de limites tem uma ligação de implícita para o grupo de limites de site predefinido. Esta ligação fica ativa depois de 120 minutos em que momento o grupo de limites de site predefinidos torna-se um grupo de limites de vizinho que permite que os clientes utilizar os pontos de distribuição associados esse grupo de limites como localizações de origem de conteúdo.

    Este comportamento substitui o que foi anteriormente designado contingência para conteúdo.  Pode substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo e definir uma hora específica em minutos ou bloquear contingência completamente para impedir a sua utilização.


-     **Os clientes tentam obter conteúdo a partir de cada ponto de distribuição para até 2 minutos:** Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição para 2 minutos antes de, em seguida, tentar outro ponto de distribuição. Esta é uma mudança de versões anteriores onde os clientes tentaram ligar a um ponto de distribuição até 2 horas.

    - O primeiro ponto de distribuição que um cliente tenta utilizar aleatoriamente está selecionado o conjunto de pontos de distribuição disponíveis no cliente do *atual* grupo de limites (ou grupos).

    - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, este muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. Este processo repete-se em dois minutos até o cliente localiza o conteúdo ou atinge o último servidor no seu conjunto.

    - Se um cliente não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* conjunto antes que o período de contingência para um *vizinho* grupo de limites for atingido, o cliente, em seguida, adiciona os pontos de distribuição que *vizinho* grupo para o fim da respetiva lista atual e, em seguida, irá pesquisar o grupo expandido das localizações de origem que inclua os pontos de distribuição a partir de ambos os grupos de limites.

        > [!TIP]  
        > Quando criar uma ligação explícita o atual grupo de limites para o grupo de limites de site predefinidos e definir uma hora de contingência que é menor do que o tempo de contingência para uma ligação para um grupo de limites de vizinho, os clientes irão começar a procurar localizações de origem a partir do grupo de limites de site predefinidos antes incluindo o grupo de vizinho.

    - Quando o cliente não consegue obter conteúdo a partir do servidor do último no agrupamento de, inicia o processo novamente.


### <a name="how-the-new-model-works"></a>Como funciona o novo modelo
Quando configura grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como os pontos de distribuição, ao grupo de limites. Isto ajuda a clientes de ligação para servidores do sistema de sites, como pontos de distribuição que estão localizados junto de clientes na rede.   
-    Pode atribuir o mesmo limite a vários grupos de limites
-    Servidores de sistema de sites, como pontos de distribuição, podem ser associados a vários grupos de limites, disponibilizando-as a um leque mais alargado de localizações de rede
-    Se um ponto de distribuição não estiver associado a um grupo de limites, os clientes não será possível utilizar esse ponto de distribuição como localização de origem de conteúdo.

A partir deste pré-visualização técnica, é possível definir relações de grupo de limites para configurar o comportamento de contingência para localizações de origem de conteúdo. Este novo comportamento está configurado no novo **relações** separador das propriedades do grupo de limites e substitui a configuração de sistemas de sites para ser rápida ou lenta e configurar um grupo de limites para permitir a localização de origem de contingência para conteúdo.

No separador relações adicionar outros grupos de limites para configurar uma relação a esses grupos. Cada relação é uma associação unidirecional a partir de **atual** grupo de limites para o grupo de limites que adiciona, que é designado por um **vizinho**. Para cada ligação que cria, pode configurar pontos de distribuição com uma hora de contingência em minutos. Este tempo é utilizado para determinar após clientes quanto a *atual* grupo de limites pode começar a utilizar pontos de distribuição a *vizinho* grupo de limites que se encontrem não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo grupo de limites atual.

Quando um cliente não é possível localizar o conteúdo e começa a procurar nas localizações a partir de grupos de limites de vizinho,-aumenta o conjunto de pontos de distribuição disponíveis para esse cliente de forma controlada.  

-    Um grupo de limites pode ter mais de uma relação. Isto permite-lhe configurar reversão para neighbors diferentes para ocorrer depois diferentes períodos de tempo.
-    Os clientes serão contingência apenas a um grupo de limites que é um vizinho direto do respetivo grupo de limites atual.
-    Quando um cliente for membro de vários grupos de limites, o grupo de limites atual está definido como uma União muito do cliente grupos de limites.  Que o cliente pode em seguida, reversão para um vizinho de qualquer um desses grupos de limites original.

Para além das ligações que define, existe uma ligação implícita que é criada automaticamente entre os grupos de limites que cria e o grupo de limites de predefinido que é automaticamente criado para cada site. Esta ligação automática:
-    É utilizado por clientes que são não num limite associado automaticamente a nenhum grupo de limites na hierarquia utilizam o grupo de limites predefinidos a partir do respetivo site atribuído para identificar localizações de origem de conteúdo válida.   
-     É uma opção de contingência de predefinição do atual grupo de limites para o grupo de limites predefinidos de sites que é utilizado depois de 120 minutos.

**Exemplo de como utilizar o novo modelo:**     
Crie três grupos de limites que não partilham limites ou servidores do sistema de sites:
-    Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associado ao grupo de
-    Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associado ao grupo de
-    Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associado ao grupo de

Pode adiciona as localizações de rede dos clientes como limites ao apenas o grupo de limites BG_A e, em seguida, configurar relações desse grupo de limites para os outros dois grupos de limites:
-    Configurar pontos de distribuição para o primeiro *vizinho* grupo (BG_B) para serem utilizados após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são com boas ligações para as localizações de limite de grupos primeiro.
-    Configurar o segundo *vizinho* grupo (BG_C) para ser utilizado, passados 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são através de uma WAN a partir de outros dois grupos de limites.
-    Pode também adiciona um ponto de distribuição adicionais que esteja localizado no servidor do site ao grupo de limites de site de sites predefinido. Esta é a localização de origem de conteúdo menos preferencial, mas se centralmente encontra todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
-    O cliente começa procurar conteúdo a partir de pontos de distribuição no respetivo *atual* procurar distribuição de cada grupo de limites (BG_A), aponte para dois minutos antes de mudar para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-    Se o cliente não conseguir encontrar o conteúdo a partir do respetivo *atual* grupo de limites após à procura de 10 minutos, em seguida, adiciona os pontos de distribuição a partir do grupo de limites BG_B à sua pesquisa. Em seguida, continua a pesquisar conteúdo num ponto de distribuição no seu conjunto combinado de pontos de distribuição que inclui agora as do BG_A tanto BG_B grupos de limites. O cliente continua a contactar cada ponto de distribuição para dois minutos antes de mudar para o próximo ponto de distribuição a partir do seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-    Após 10 minutos (total de 20 minutos) adicionais se o cliente ainda não encontrou um ponto de distribuição com conteúdo, expande o conjunto de pontos de distribuição disponíveis para incluir os da segunda *vizinho* agrupar, grupo de limites BG_C. Agora, o cliente tem 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a alterar para um novo ponto de distribuição de todos os dois minutos até é encontrado conteúdo.
-    Se o cliente não foi encontrado conteúdo após um total de 120 minutos,-reverterá para incluir o *grupo de limites de site predefinidos* como parte da sua pesquisa contínua. O conjunto de pontos de distribuição inclui agora todos os pontos de distribuição a partir de grupos de limites configurados três e o ponto de distribuição final localizado no computador do servidor do site.  O cliente, em seguida, continua a pesquisa de conteúdo, alterar cada dois minutos até é encontrado conteúdo a pontos de distribuição.

Ao configurar os grupos de vizinho diferentes para estar disponível em alturas diferentes, pode controlar quando são adicionados como uma localização de origem de conteúdo, pontos de distribuição específico e quando, ou se, o cliente utiliza contingência para o grupo de limites de site predefinidos como uma rede de segurança de conteúdo que não está disponível a partir de qualquer outra localização.


### <a name="bkmk_update"></a>Atualizar os grupos de limites existentes para o novo modelo
Quando instala a versão 1609 e atualizar o seu site, as seguintes configurações são efetuadas automaticamente. Estas são direcionadas para assegurar que o comportamento de contingência atual permanece disponível até configurar novos grupos de limites e relações.  
-    Pontos de distribuição não protegidas num site são adicionados ao *limites-grupo de predefinido-Site\<sitecode >* grupo de limites desse site.
-    É efetuada uma cópia de cada grupo de limites existentes que inclua um servidor de sites configurado com uma ligação lenta. O nome do novo grupo é *** \<nome original do grupo de limites > Tmp - lenta -***:  
    -    Sistemas de sites que tenham uma ligação rápida são mantidos no grupo de limites original.
    -    Uma cópia dos sistemas de sites que tenham uma ligação lenta são adicionados à cópia do grupo de limites. Os sistemas de sites original configurados como lenta permanecem no grupo de limites original de compatibilidade com versões anteriores, mas não são utilizados desse grupo de limites.
    -     Esta cópia do grupo de limites não tiverem limites associados à mesma. No entanto, é criada uma ligação de contingência entre o grupo original e a nova cópia do grupo de limites que tenha o tempo de contingência definido como zero.

 A tabela seguinte identifica o novo comportamento de contingência que poderá esperar da combinação de original definições de implementação e pontos de distribuição configurações:

Configuração de implementação original para "Não executar o programa" numa rede lenta  |Configuração para "Permitir a utilizar uma localização de origem de contingência para conteúdo de cliente" do ponto de distribuição original  |Novo comportamento de contingência  
---------|---------|---------
Selecionada     |  Selecionada    |  **Nenhum contingência** -utilize apenas os pontos de distribuição num grupo de limites atual       
Selecionada     |  Não selecionado|  **Nenhum contingência** -utilize apenas os pontos de distribuição num grupo de limites atual       
Não selecionado |  Não selecionado|  **Contingência para vizinho** - utilizar pontos de distribuição num grupo de limites atual e, em seguida, adicione os pontos de distribuição a partir do grupo de limites de vizinho. A menos que é configurada uma ligação de explícita para o grupo de limites de site predefinidos, os clientes não poderá contingência a esse grupo.    
Não selecionado | Selecionada        |   **Contingência normal** -utilizar pontos de distribuição num grupo de limites atual, em seguida, as do vizinho e o site predefinido de grupos de limites

 Todas as outras configurações de implementação resultam em **contingência Normal**.  



## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
A pré-visualização técnica do Configuration Manager 1609 apresenta um novo dashboard. Para ver o dashboard, na consola do Configuration Manager vá para **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
>[!NOTE]
>No **Novidades** área de trabalho na consola do Configuration Manager, o novo dashboard incorretamente chama-se **manutenção do Office 365 dashboard**.

O dashboard apresenta gráficos para os seguintes:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
Para obter mais informações, consulte o artigo [canais de consumo de descrição geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Regras de implementação automática que tenham o cliente do Office 365 selecionado no conjunto de produtos disponíveis.

Pode efetuar as seguintes ações no dashboard:
- Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros de uma coleção específica.
- No lado do dashboard do canto superior direito, clique em **instalador do Office 365** para iniciar o Assistente de instalação de cliente do Office 365 para implementar aplicações do Office 365 em clientes. Para obter mais detalhes, consulte o artigo [aplicações de implementar o Office 365 para clientes](#deploy-office-365-apps-to-clients).
- No lado direito de meio do dashboard, clique em **criar um ADR** para abrir o Assistente de regra de implementação automática para criar uma nova regra de implementação automática (ADR). Para criar um ADR para aplicações do Office 365, selecione **cliente do Office 365** quando escolher o produto. Para obter mais informações, consulte o artigo [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- No lado inferior direito do dashboard, clique em **criar definições de agente de cliente** para abrir as definições do agente de cliente. Para obter mais informações, consulte o artigo [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings).



Para obter mais informações sobre atualizações do Office 365 ProPlus, consulte o artigo [gerir Office 365 ProPlus atualizações com o Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 para clientes
Nesta versão, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador do Office 365 que permite-lhe configurar definições de instalação do Office 365, transferem ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitações da implementação do Office 365
- Poderá ter problemas ao tentar importar as definições de cliente existente (XML) no Assistente de instalação da aplicação do Office 365. Pode configurar manualmente as definições de cliente sem um problema.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implementar aplicações do Office 365 em clientes
1. Na consola do Configuration Manager, navegue para **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **instalador do Office 365** no painel do canto superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. No **definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **seguinte**. Tenha em atenção que a localização tem de ser especificada o formulário &#92; &#92; *server*&#92; *partilhar*.
4. No **importar definições de cliente** página, selecione se pretende importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente ou especifique manualmente as definições e, em seguida, clique em **seguinte**.
Quando tiver um ficheiro de configuração existente, introduza a localização para o ficheiro e avance para o passo 7. Tenha em atenção que a localização tem de ser especificada o formulário &#92; &#92; *server*&#92; *partilhar*&#92;* nome de ficheiro*. XML.

    > [!IMPORTANT]
    >Poderá ter problemas ao tentar importar as definições de cliente existente (XML) neste technical preview.

5. No **cliente produtos** página, selecione o Office 365 conjunto de aplicações que utilizam, selecione as aplicações que pretende incluir, selecione os produtos Office adicionais que devem ser incluídos e, em seguida, clique em **seguinte**.
6. No **definições de cliente** página, selecione as definições para incluir e, em seguida, clique em **seguinte**.
7. No **implementação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **seguinte**.
Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure o resto das páginas do assistente, tal como faria para uma implementação de aplicação normal. Para obter mais informações, consulte o artigo [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação, tal como faria com qualquer outra aplicação no Configuration Manager a partir de **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**.

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar um ADR para aplicações do Office 365, clique em **criar um ADR**e selecione **cliente do Office 365** quando escolher o produto. Para obter mais informações, consulte o artigo [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="BKMK_UEFIConversion"></a>Melhoramentos na cópia de BIOS para conversão de UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o passo de reiniciar o computador irá preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar os passos de sequência de tarefas para preparar o disco rígido para o BIOS para conversão de UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Na sequência de tarefas existente para instalar um sistema operativo, irá adicionar um novo grupo de seguir os passos de BIOS para conversão de UEFI.

1. Crie um novo grupo de sequência de tarefas depois dos passos para capturar ficheiros e definições e antes dos passos para instalar o sistema operativo. Por exemplo, crie um grupo após o **capturar ficheiros e definições** grupo denominado **BIOS para UEFI**.
2. No **opções** separador do novo grupo, adicionar uma nova variável de sequência de tarefas como uma condição onde **smstsbootuefi sempre** é **não igual** para **verdadeiro**. Isto impede que os passos no grupo em execução quando um computador já está no modo UEFI.
![BIOS para o grupo UEFI](media/BIOS-to-UEFI-group.png)
3. No grupo novo, adicionar o **reiniciar o computador** passo de sequência de tarefas. No **especificam as ações a executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  
4. No **opções** separador, adicione uma variável de sequência de tarefas como uma condição onde **_SMSTSInWinPE é igual a FALSO**. Isto impede que este passo se o computador já está no Windows PE a ser executado.

    ![Reinicie o passo de computador](media/Restart-in-Windows-PE.png)
5. Adicione um passo para iniciar a ferramenta do OEM que irá converter o firmware de BIOS para UEFI. Normalmente, será uma **executar linha de comandos** passo de sequência de tarefas com uma linha de comandos para iniciar a ferramenta de OEM.
5.    Adicione o passo de sequência de tarefas formatar e particionar disco que será particionar e formatar o disco rígido. No passo, efetue o seguinte:
    1.    Crie a partição de FAT32 que serão convertidas em UEFI antes do sistema operativo está instalado. Escolher **GPT** para **tipo de disco**.
    ![Formatar e particionar passo de disco](media/Format-and-partition-disk.png)
    2.    Ir para as propriedades para a partição FAT32. Introduza **TSUEFIDrive** no **variável** campo. Quando a sequência de tarefas Deteta esta variável, irá preparar para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](media/Partition-properties.png)
    3. Crie uma partição NTFS que utiliza o motor de sequência de tarefas para guardar o estado e armazenar ficheiros de registo.
6.    Adicionar o **reiniciar o computador** passo de sequência de tarefas. No **especificam as ações a executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de conformidade do Intune
Nesta versão, pode obter uma vista rápida da conformidade global para dispositivos e as razões principais para inconformidade através de gráficos novo em **área de trabalho de monitorização** na consola do Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Para ver os gráficos de conformidade do Intune
1. Na consola do Configuration Manager, aceda a **monitorização** > **descrição geral** > **definições de compatibilidade**.
2. O **geral conformidade do dispositivo** gráfico é apresentado.
3. Clique na **políticas de conformidade** nó para ver o **geral conformidade do dispositivo** e **motivos de conformidade não início** gráficos.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitações de gráficos de conformidade do Intune no TP 1609
- Desagregar para o **geral conformidade do dispositivo** gráfico atualmente produz um erro.
- O **principais razões de não conformidade** gráfico apresenta o nome da política e não as razões individuais de não conformidade. Pode clicar a política de desagregação e ver os dispositivos que estão em conformidade para essa política.

### <a name="try-it-out"></a>Experimente
Conclua as seguintes secções por ordem:

#### <a name="check-overall-compliance-chart"></a>Gráfico de conformidade geral de verificação
1. Adicione no duas iOS políticas de conformidade no Configuration Manager. Uma política deve ter um conjunto de definições para dispositivos (por exemplo, conjunto de comprimento do PIN a 6). A política de outra deve ter outro conjunto de definições (por exemplo, a complexidade PIN). As definições de política não devem sobrepor-se ou estar em conflito.
2. Implemente duas políticas para um conjunto de utilizadores.
3. Inscreva dispositivos iOS dois no Intune utilizando a mesma conta de utilizador e uma conta que recebeu políticas no passo anterior. Os dispositivos não devem cumprir os critérios da política de conformidade.
4. No Configuration Manager, verifique o **geral conformidade do dispositivo** gráfico. Ambos os dispositivos devem reportar como não conformidade.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Verifique o gráfico de razões de não conformidade superior
5. Verifique o **principais razões de não conformidade** gráfico. Este gráfico apresenta uma lista de 5 principais razões para não conformidade, mas quando apenas duas definições de compatibilidade foram definidas através de políticas apenas parte superior 2 inconformidade motivos pelos quais são apresentados.
6. Clique das secções no gráfico. Ambos os dispositivos devem aparecer na vista filtrada em **ativos e compatibilidade** > **descrição geral** > **dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Que dispositivos fique em conformidade e verificar os gráficos
7. Um dos dispositivos que fique em conformidade com uma das políticas. Verifique o **geral conformidade do dispositivo** gráfico novamente. O gráfico deverá apresentar um dispositivo compatível e dos dispositivos não conformes.
8. Que o outro dispositivo fique em conformidade com a mesma política. Isto faz com que um dispositivo compatível com as políticas e dos dispositivos compatíveis com apenas uma das políticas.
9. Verifique o **principais razões de não conformidade** gráfico. Só deve ser uma razão de não conformidade listada.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)

