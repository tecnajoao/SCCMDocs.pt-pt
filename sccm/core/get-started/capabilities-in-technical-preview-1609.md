---
title: Funcionalidades no Technical Preview versão 1609
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31c25622a42586c044e2b9f515f5e89f9e82ba00
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133753"
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1609 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1609. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    

**Problemas conhecidos neste Technical Preview:**  
*  Quando atualizar para a versão 1609 do Configuration Manager Technical Preview, as políticas de atualização de edição que implementou serão eliminadas. Para continuar a utilizar estas políticas, tem de recriar e implementá-las.


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="improvements-to-endpoint-protection"></a>Melhoramentos à proteção de ponto final
Melhoria para definições de política de antimalware do Endpoint Protection - agora pode especificar o nível em que a proteção de ponto final de Cloud Protection Service irá bloquear ficheiros suspeitos. Uma nova definição permite aos administradores especificar "arriscados" computadores com base nas quantidades elevadas de malware que se deparam.

## <a name="increased-number-of-enrolled-devices"></a>Aumento do número de dispositivos inscritos
Os administradores agora podem permitir aos utilizadores inscrever até 15 dispositivos na gestão de dispositivos móveis híbrida com o Intune. O limite era anteriormente 5 dispositivos por utilizador.

## <a name="additional-apple-dep-settings"></a>Definições adicionais do DEP da Apple

Os administradores agora podem configurar as seguintes definições do programa de inscrição de dispositivos da Apple (DEP) no perfil de DEP para dispositivos iOS e Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Se estiver ativada, o Assistente de configuração da Apple solicita este serviço durante a ativação do dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integração com o Upgrade Analytics

Atualização analytics permite-lhe avaliar e analisar a prontidão do dispositivo e a compatibilidade com Windows 10, para permitir que as atualizações mais fácil e mais suaves. Com a integração do Upgrade Analytics com o Configuration Manager, pode acessar os dados de compatibilidade da atualização na consola de administração do Configuration Manager e, em seguida, na lista de dispositivos de destino dispositivos para a atualização ou correção.

Pode ler mais sobre o Upgrade Analytics na [começar com o Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Tipos de ligação nativos para perfis de híbrida VPN do Windows 10

Quando utilizar o Configuration Manager com o Intune, agora pode criar perfis de VPN do Windows 10 com tipos de ligação Microsoft Automatic, IKEv2, PPTP e L2TP na consola do Configuration Manager sem utilizar OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Aprimoramentos na Windows Store para integração de negócios com o Configuration Manager

Nesta versão, atualizamos [Store do Windows para integração de negócios](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) com estas novas funcionalidades:

**Update:** A versão de pré-visualização técnica atual, a funcionalidade de sincronização imediata não está funcional.

- Anteriormente, só pode implementar aplicações gratuitas da Windows Store para empresas. Gestor de configuração agora adicionalmente suporta a implementação de online pago licenciado aplicações (para dispositivos inscritos no Intune).
- Agora pode iniciar uma sincronização imediata entre o Windows Store para empresas e o Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Active Directory

### <a name="try-it-out"></a>Experimente!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Comprar e sincronizar uma aplicação com licença online paga

1. Compre um aplicativo licenciado online pago da Windows Store para empresas.
2. Na **Administration** área de trabalho da consola do Configuration Manager, clique em **serviços Cloud** > **atualizações e manutenção**  >   **Windows Store para empresas**.
3. Sobre o **home page** separador a **sincronização** , clique em **sincronizar agora**.
4. Em breve, em seguida, a aplicação compradas será apresentado o **informações de licença para aplicações de Store** nó do **gestão de aplicações** área de trabalho.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Criar e implementar uma aplicação do Configuration Manager dos dados da aplicação sincronizados

O procedimento para criar e implementar uma aplicação do Configuration Manager a partir de uma aplicação da loja pago é igual de criar uma aplicação a partir de uma aplicação gratuita. Consulte a secção **criar e implementar uma aplicação do Configuration Manager a partir de um Store do Windows para a aplicação de negócio** na [gerir aplicações a partir da Windows Store para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) .


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificar a chave secreta do cliente do Azure Active Directory

1. Na **Administration** área de trabalho da consola do Configuration Manager, clique em **serviços Cloud** > **atualizações e manutenção**  >   **Windows Store para empresas**.
2. Selecione seu Store do Windows para a conta de empresa e, em seguida, clique em **propriedades**.
3. Na **Windows Store para empresas propriedades da conta** caixa de diálogo, introduza uma chave de novo no **chave secreta do cliente** campo e, em seguida, clique em **verificar**. Depois de verificar, clique em **aplicar**, em seguida, feche a caixa de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração

Adicionámos muitas definições novas, que pode usar nos seus itens de configuração para várias plataformas de dispositivos.
Estas são as definições que já existiam no Microsoft Intune numa configuração autónoma e estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Se precisar de ajuda com qualquer uma destas definições, abra [gerir definições e funcionalidades nos seus dispositivos com políticas do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies) e, em seguida, selecione o subtopic de definições para a plataforma que quiser.


### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android

#### <a name="password-settings"></a>Definições de palavra-passe

- **Memorizar histórico de palavras-passe**
- **Permitir impressões digitais desbloquear**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação

- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir armazenamento amovível**
- **Permitir tethering Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir roaming de voz**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir Assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**


### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe é necessária**
- **Memorizar histórico de palavras-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**
- **Minutos de inatividade antes da proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos Windows 10 Desktop e Mobile

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavras-passe**
- **Exigir uma palavra-passe quando o dispositivo regressa de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança

- **Exigir encriptação no dispositivo móvel**
- **Permitir anular inscrições manualmente**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir VPN pela rede móvel**
- **Permitir roaming de VPN por rede móvel**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações do Centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team

#### <a name="device-settings"></a>Definições do dispositivo

- **Ativar as informações operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolher as informações de reunião apresentadas no ecrã de boas-vindos**
- **URL de imagem de fundo do ecrã de bloqueio**


### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Tipo de palavra-passe necessária**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração de palavra-passe (dias)**
- **Memorizar histórico de palavras-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir deteção automática de rede intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir ligação automática a hotspots Wi-Fi**


## <a name="improvements-for-boundary-groups"></a>Melhorias de grupos de limites
Esta pré-visualização introduz alterações importantes para grupos de limites e como eles funcionam com pontos de distribuição. Estas alterações ajudará a simplificar o design da sua infraestrutura de conteúdo, dando-lhe mais controlo sobre como e quando os pontos de contingência de clientes para distribuição adicionais de pesquisa como localizações de origem de conteúdo. Isto inclui pontos de distribuição baseado na nuvem e no local.

Esses aprimoramentos substituir os conceitos e comportamentos, poderá estar familiarizado hoje (como configurar pontos de distribuição para ser rápido ou lento) e os substitui por um novo modelo que deve ser mais fácil de configurar e manter. Essas alterações também são a base para futuras alterações que irão melhorar a outras funções de sistema de sites, associar a grupos de limites.  

Durante a atualização para a versão 1609, a atualização converte as configurações de grupo de limite atual de acordo com o novo modelo para que estas alterações não incomodar suas configurações de distribuição de conteúdo (consulte [atualizar grupos de limites existentes para o novo modelo](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)).

As secções seguintes detalham as alterações introduzidas com esta pré-visualização, como funciona o novo modelo e o que pode esperar quando atualizar um site que já tenha configurados de grupos de limites.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Alterações na interface do Usuário e o comportamento para grupos de limites e localizações de conteúdo
Seguem-se as principais alterações de grupos de limites e como os clientes localizam os conteúdos. Muitas destas alterações e conceitos funcionam em conjunto.
- **Configurações para rápida ou lenta são removidas:** Já não está a configurar pontos de distribuição individuais para ser rápido ou lento.  Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Por causa dessa alteração, o **referências** separador de propriedades do grupo de limites já não suporta a configuração de rápida ou lenta.
- **Novo grupo de limite predefinido em cada site:**  Cada site primário tem um novo grupo de limites de padrão com o nome ***predefinição---grupo de limite Site\<sitecode >***.  Quando um cliente não está numa localização de rede que é atribuída a um grupo de limites, o que o cliente utilizará os sistemas de sites associados ao grupo predefinido do seu site atribuído. Recomendamos que utilize este grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.    
  -  **"Permitir localizações de origem de contingência de conteúdo"** é removido: Configurar um ponto de distribuição para ser utilizado para contingência já não é explicitamente, e as opções para definir esta opção são removidas da interface do Usuário.

  Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação foi alterado o tipo para aplicações. Esta definição num tipo de implementação agora permite que um cliente utilizar o grupo de limites de site padrão como uma localização de origem de conteúdo.

  -  **Relações de grupos de limites:** Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que estão configuradas no novo separador de propriedades de grupo limites com o nome **relações**:
  -   Cada grupo de limites que um cliente é diretamente associado é chamado um **atual** grupo de limites.  
  -   Nenhum grupo de limites um cliente pode utilizar devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo é chamado um **vizinho** grupo de limites.
  -  É no **relações** separador que adicionar grupos de limites que podem ser utilizados como um *vizinho* grupo de limites. Também pode configurar um período de tempo em minutos que determina quando um cliente que não consegue encontrar o conteúdo de um ponto de distribuição no *atual* grupo irá começar a pesquisar localizações de conteúdo das *vizinho* grupos de limites.

      Quando adicionar ou alterar a configuração de um grupo de limites, terá a opção para o bloco de contingência para esse grupo de limites específicos do grupo atual que está a configurar.

  Para utilizar a nova configuração, define associações explícitas (links) de um grupo de limites para outro e configura todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. O tempo que configurar determina quando um cliente que não consegue encontrar uma origem de conteúdo do respetivo *atual* grupo de limites pode começar a procurar a fontes de conteúdo desse grupo de limite vizinho.

  Além dos grupos de limites que configure explicitamente, cada grupo de limites tem uma ligação implícita para o grupo de limites de site padrão. Esta ligação é ativada após 120 minutos em que altura do grupo de limites de site predefinido torna-se um grupo de limite vizinho que permite que os clientes utilizar os pontos de distribuição associados esse grupo de limites como localizações de origem de conteúdo.

  Este comportamento substitui o que era anteriormente chamado de contingência para conteúdo.  Pode substituir esse comportamento padrão de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo e definir uma hora específica em minutos ou bloqueio contingência inteiramente para evitar seu uso.


- **Os clientes tentam obter o conteúdo de cada ponto de distribuição para até 2 minutos:** Quando um cliente procura de uma localização de origem de conteúdo, ele tenta aceder a cada ponto de distribuição para 2 minutos antes de, em seguida, tentar outro ponto de distribuição. Esta é uma alteração de versões anteriores em que os clientes tentaram ligar a um ponto de distribuição para até 2 horas.

  - O primeiro ponto de distribuição que um cliente tenta utilizar é selecionado aleatoriamente entre o conjunto de pontos de distribuição disponíveis do cliente *atual* grupo de limites (ou grupos).

  - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, ele muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. O processo se repete a cada dois minutos até que o cliente encontra o conteúdo ou alcança o último servidor no seu conjunto.

  - Se um cliente não conseguir encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* conjunto antes do período de contingência para um *vizinho* grupo de limites for atingido, o cliente, em seguida, adiciona os pontos de distribuição de que *vizinho* ao final da lista atual de grupo e, em seguida, irá procurar o grupo expandida das localizações de origem, que inclui os pontos de distribuição a partir de ambos os grupos de limites.

      > [!TIP]  
      > Quando cria uma ligação explícita do grupo de limites atual para o grupo de limites de site padrão e definir um tempo de contingência que é menor que o tempo de contingência para um link para um grupo de limite vizinho, os clientes começará a pesquisar localizações de origem a partir do site predefinido grupo de limites antes de incluir o grupo de vizinho.

  - Quando o cliente não consegue obter o conteúdo do último servidor no agrupamento, ele começa novamente o processo.


### <a name="how-the-new-model-works"></a>Como funciona o novo modelo
Ao configurar grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como pontos de distribuição, ao grupo de limites. Ajuda os clientes de ligação a servidores do sistema de sites como perto de pontos de distribuição que estão localizados os clientes na rede.   
-   Pode atribuir o mesmo limite a vários grupos de limites
-   Servidores do sistema de sites, como pontos de distribuição, podem ser associados a vários grupos de limites, disponibilizando-as a um maior número de localizações de rede
-   Se um ponto de distribuição não estiver associado a um grupo de limites, os clientes não será capazes de usar esse ponto de distribuição como localização de origem de conteúdo.

A partir desta pré-visualização técnica, é possível definir relações de grupo de limites para configurar o comportamento de contingência para localizações de origem de conteúdo. Esse novo comportamento está configurado no novo **relações** separador de propriedades do grupo de limites e substitui a configuração de sistemas de sites para ser lento ou rápido e configurar um grupo de limites para permitir a localização de origem de contingência para conteúdo.

Na guia relações adicionar outros grupos de limites para configurar uma relação a esses grupos. Cada relação é uma ligação unidirecional a partir do **atual** grupo de limites para o grupo de limites adicionar, que é chamado de um **vizinho**. Para cada ligação que criou, pode configurar pontos de distribuição com um tempo de contingência em minutos. Desta vez, é utilizada para determinar após clientes quanto a *atual* grupo de limites pode começar a utilizar pontos de distribuição a *vizinho* grupo de limites, se forem não é possível encontrar uma origem de conteúdo válida localização do respetivo grupo de limites atual.

Quando um cliente não é possível localizar o conteúdo e começa a pesquisar localizações de grupos de limite vizinho, aumenta o conjunto de pontos de distribuição disponíveis para esse cliente de forma controlada.  

-   Um grupo de limites pode ter mais de uma relação. Isto permite-lhe configurar a contingência para diferentes vizinhos de ocorrer após diferentes períodos de tempo.
-   Os clientes serão fallback única para um grupo de limites que é um vizinho direto do respetivo grupo de limites atual.
-   Quando um cliente for membro de vários grupos de limites, o grupo de limites atual é definido como uma União de todos os grupos de limites do cliente.  Esse cliente pode, em seguida, reversão para uma aproximação de qualquer um desses grupos de limite original.

Além das ligações que definir, há um link de implícito que é criado automaticamente entre os grupos de limites que crie e o grupo de limite predefinido que é criado automaticamente para cada site. Esta ligação automática:
-   É utilizado pelos clientes que são não num limite associado a nenhum grupo de limites na sua hierarquia automaticamente utilizar o grupo de limite predefinido através do respetivo site atribuído para identificar as localizações de origem de conteúdo válida.   
-   É uma opção de contingência de predefinição do grupo de limites atual para o grupo de limite predefinido de sites que é utilizada depois de 120 minutos.

**Exemplo de como utilizar o novo modelo:**     
Crie três grupos de limites que não partilham limites ou servidores de sistema de sites:
-   Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associado ao grupo de
-   Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associado ao grupo de
-   Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associado ao grupo de

Adicione as localizações de rede dos seus clientes como limites para apenas o grupo de limites BG_A e depois de configurar relações a partir desse grupo de limites para os outros dois grupos de limites:
-   Configurar pontos de distribuição para os primeiros *vizinho* grupo (BG_B) a ser usado após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são boas para as localizações de limite de grupos primeiro.
-   Configurar a segunda *vizinho* grupo (BG_C) a ser utilizado depois de 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são numa WAN de outros grupos de limites de dois.
-   Também adicionar um ponto de distribuição adicionais que está localizado no servidor do site para o grupo de limites de site de padrão de sites. Esta é a localização de origem de conteúdo menos preferencial, mas é localizado centralmente a todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
-   O cliente começa a procurar o conteúdo a partir de pontos de distribuição no respetivo *atual* grupo de limites (BG_A), pesquisa cada distribuição ponto durante dois minutos antes de mudar para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-   Se o cliente não conseguir localizar o conteúdo a partir de seus *atual* grupo de limites depois de procurar por 10 minutos, em seguida, adiciona os pontos de distribuição do grupo de limites de BG_B à sua pesquisa. Em seguida, continua a pesquisar conteúdo de um ponto de distribuição no respetivo conjunto combinado de pontos de distribuição que inclui agora os do BG_A tanto BG_B grupos de limites. O cliente continua a contactar cada ponto de distribuição durante dois minutos antes de mudar para o próximo ponto de distribuição do seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-   Após um adicional de 10 minutos (total de 20 minutos) se o cliente ainda não encontrou um ponto de distribuição com conteúdo, ele se expande seu pool de pontos de distribuição disponíveis para incluir os da segunda *vizinho* grupo, o limite grupo BG_C. Agora, o cliente tem 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua mudando para um novo ponto de distribuição a cada dois minutos até que o conteúdo é encontrado.
-   Se o cliente não foi encontrado conteúdo depois de um total de 120 minutos, retrocede para incluir o *grupo de limite de site predefinido* como parte da sua pesquisa contínua. Agora, o conjunto de pontos de distribuição inclui todos os pontos de distribuição de três grupos de limites configurados e o ponto de distribuição final localizado no computador do servidor do site.  O cliente, em seguida, continua a pesquisa de conteúdo, a alteração de pontos de distribuição a cada dois minutos até que o conteúdo é encontrado.

Ao configurar os grupos de vizinho diferentes para estar disponível em momentos diferentes controlar quando os pontos de distribuição específicos são adicionados como uma localização de origem de conteúdo e quando, ou se, o cliente utiliza a contingência para o grupo de limites de site padrão como uma rede de segurança para conteúdo que não está disponível a partir de qualquer outra localização.


### <a name="bkmk_update"></a>Atualizar os grupos de limites existentes para o novo modelo
Quando instala a versão versão 1609 e atualizar o site, as seguintes configurações são efetuadas automaticamente. Estes destinam-se para garantir que seu comportamento de contingência atual permanece disponível, até que configure novos grupos de limites e relações.  
- Pontos de distribuição não protegida num site são adicionados para o *predefinição---grupo de limite Site\<sitecode >* grupo de limites desse site.
- É feita uma cópia de cada grupo de limites existentes, que inclui um servidor de site configurado com uma conexão lenta. O nome do novo grupo é  ***\<nome do grupo de limite original > Tmp - lenta -***:  
  -   Sistemas de sites que tenham uma conexão rápida são deixados no grupo de limite original.
  -   Uma cópia dos sistemas de sites que tenham uma conexão lenta são adicionados para a cópia do grupo de limites. Os sistemas de sites original configurados como lenta permanecem no grupo de limite original para compatibilidade com versões anteriores, mas não são utilizados desse grupo de limites.
  -   Esta cópia do grupo de limites não tem limites associados a ele. No entanto, é criada uma ligação de contingência entre o grupo original e a nova cópia do grupo de limites que tem o tempo de contingência definido como zero.

  A tabela seguinte identifica o novo comportamento de fallback pode esperar da combinação de definições de implementação original e a distribuição de configurações de pontos:

Configuração de implementação original para "Não executar o programa" na rede lenta  |Configuração para "Permitir ao cliente utilizar uma localização de origem de contingência para conteúdo" de ponto de distribuição original  |Novo comportamento de contingência  
---------|---------|---------
Selecionado     |  Selecionado    |  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Selecionado     |  Não selecionado|  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Não selecionado |  Não selecionado|  **Contingência para vizinho** – utilizar os pontos de distribuição no grupo de limites atual e, em seguida, adicione os pontos de distribuição do grupo de limite vizinho. A menos que uma ligação explícita para o grupo de limites de site predefinido é configurada, os clientes não irão contingência a esse grupo.    
Não selecionado | Selecionado     |   **Contingência normal** -utilizar pontos de distribuição no grupo de limite atual, em seguida, os do vizinho e o site predefinido de grupos de limites

 Todas as outras configurações de implementação resultam numa **contingência Normal**.  



## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
A versão 1609 do Configuration Manager Technical Preview introduz um novo dashboard. Para ver o dashboard, na consola do Configuration Manager aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
>[!NOTE]
>Na **o que há de novo** área de trabalho na consola do Configuration Manager, o novo dashboard incorretamente é denominado **dashboard de manutenção do Office 365**.

O dashboard apresenta gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
Para obter mais informações, consulte [canais de descrição geral da atualização do Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Regras de implementação automática que tenham o cliente do Office 365 selecionadas no conjunto de produtos disponíveis.

Pode efetuar as seguintes ações no dashboard:
- Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros de uma coleção específica.
- No lado do canto superior direito do dashboard, clique em **Office 365 instalador** para iniciar o Assistente de instalação de cliente do Office 365 para implementar aplicações do Office 365 em clientes. Para obter detalhes, consulte [aplicações de implementar o Office 365 em clientes](#deploy-office-365-apps-to-clients).
- No lado direito do dashboard, clique em **criar uma ADR** para abrir o Assistente de regra de implementação automática para criar uma nova regra de implementação automática (ADR). Para criar uma ADR para aplicações do Office 365, selecione **cliente do Office 365** ao escolher o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- No lado inferior direito do dashboard, clique em **criar definições de agente de cliente** para abrir as definições de agente do cliente. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings).



Para obter mais informações sobre atualizações do Office 365 ProPlus, consulte [com o Gestor de configuração de atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 em clientes
Nesta versão, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador do Office 365 que lhe permite configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdos (CDNs) do Office e implantar os arquivos como uma aplicação no Gestor de configuração.

### <a name="limitations-of-office-365-deployment"></a>Limitações da implementação do Office 365
- Poderá ter problemas ao tentar importar definições de cliente existente (XML) no Assistente de instalação de aplicação do Office 365. Pode configurar manualmente as definições de cliente sem problemas.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implementar aplicações do Office 365 em clientes
1. Na consola do Configuration Manager, navegue até **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **Office 365 instalador** no painel de canto superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. Sobre o **as definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **próxima**. Tenha em atenção que a localização tem de ser especificada no formulário &#92; &#92; *server*&#92;*partilhar*.
4. Sobre o **importar definições de cliente** página, selecione se pretende importar as definições de cliente do Office 365 a partir de um arquivo de configuração XML existente ou especifique manualmente as definições e, em seguida, clique em **próxima**.
Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e avance para o passo 7. Tenha em atenção que a localização tem de ser especificada no formulário &#92; &#92; *server*&#92;*partilhar*&#92;*filename*. XML.

    > [!IMPORTANT]
    >Poderá ter problemas ao tentar importar definições de cliente existente (XML) neste technical Preview.

5. Sobre o **produtos de cliente** página, selecione o Office 365 suite que utilizar, selecione as aplicações que pretende incluir, selecione quaisquer outros produtos do Office que devem ser incluídos e, em seguida, clique em **próxima**.
6. Sobre o **definições de cliente** página, selecione as definições para incluir e, em seguida, clique em **próxima**.
7. Sobre o **implantação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **próxima**.
Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure o restante das páginas do assistente, tal como faria para uma implantação de aplicativos típico. Para obter mais informações, consulte [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação, tal como faria com qualquer outra aplicação no Configuration Manager da **biblioteca de Software** > **descrição geral**  >   **Gestão de aplicações** > **aplicativos**.

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar uma ADR para aplicações do Office 365, clique em **criar uma ADR**e selecione **cliente do Office 365** ao escolher o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="BKMK_UEFIConversion"></a>Melhorias de BIOS para conversão de UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o passo de reiniciar o computador irá preparar uma partição FAT32 na unidade de disco rígida para a transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para o BIOS para conversão de UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Uma sequência de tarefas existente para instalar um sistema operativo, vai adicionar um novo grupo com os passos para fazer o BIOS para conversão de UEFI.

1. Crie um novo grupo de sequência de tarefas após os passos para capturar definições e ficheiros e antes dos passos para instalar o sistema operativo. Por exemplo, criar um grupo depois do **capturar arquivos e configurações** com o nome de grupo **BIOS para UEFI**.
2. Na **opções** separador do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **smstsbootuefi sempre** é **não igual** para **verdadeiro**. Isto impede que os passos no grupo de em execução quando um computador já está no modo UEFI.
![BIOS para o grupo UEFI](media/BIOS-to-UEFI-group.png)
3. Em novo grupo, adicione a **reiniciar o computador** passo de sequência de tarefas. Na **especificam as ações a executar após o reinício**, selecione **está selecionada a imagem de arranque atribuída a esta sequência de tarefas** para iniciar o computador no Windows PE.  
4. Sobre o **opções** separador, adicione uma variável de sequência de tarefas como uma condição em que **smstsinwinpe é igual a false**. Isto impede que este passo em execução se o computador já está no Windows PE.

    ![Reinicie o passo de computador](media/Restart-in-Windows-PE.png)
5. Adicione um passo para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Normalmente, será uma **executar linha de comandos** passo de sequência de tarefas com uma linha de comando para iniciar a ferramenta de OEM.
5.  Adicione o passo de sequência de tarefas formatar e particionar disco que será particionar e formatar o disco rígido. No passo, efetue o seguinte:
    1.  Crie a partição FAT32 que será convertida para UEFI antes do sistema operativo é instalado. Escolher **GPT** para **tipo de disco**.
    ![Formatar e particionar passo de disco](media/Format-and-partition-disk.png)
    2.  Vá para as propriedades para a partição FAT32. Introduza **TSUEFIDrive** no **variável** campo. Quando a sequência de tarefas Deteta esta variável, irá preparar para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades de partição](media/Partition-properties.png)
    3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para salvar seu estado e para armazenar ficheiros de registo.
6.  Adicionar a **reiniciar o computador** passo de sequência de tarefas. Na **especificam as ações a executar após o reinício**, selecione **está selecionada a imagem de arranque atribuída a esta sequência de tarefas** para iniciar o computador no Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de conformidade do Intune
Nesta versão, pode obter uma vista rápida da conformidade geral para dispositivos e os principais motivos de não conformidade com novos gráficos em **área de trabalho de monitorização** na consola do Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Para ver os gráficos de conformidade do Intune
1. Na consola do Configuration Manager, aceda a **monitorização** > **descrição geral** > **as definições de compatibilidade**.
2. O **conformidade do dispositivo global** gráfico é exibido.
3. Clique nas **políticas de conformidade** nó para ver a **conformidade do dispositivo global** e **principais motivos de não conformidade** gráficos.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitações de gráficos de conformidade do Intune na versão 1609 de TP
- A desagregação para o **conformidade do dispositivo global** gráfico atualmente produz um erro.
- O **principais motivos de não conformidade** gráfico lista o nome da política e não os motivos de não conformidade individuais. Pode clicar a política para desagregar e ver os dispositivos que são incompatíveis para essa política.

### <a name="try-it-out"></a>Experimentar
Conclua as seguintes secções por ordem:

#### <a name="check-overall-compliance-chart"></a>Verifique o gráfico de conformidade geral
1. Adicione em duas iOS políticas de conformidade no Configuration Manager. Uma política, deve ter um conjunto de definições para dispositivos (por exemplo, conjunto de comprimento do PIN para 6). A outra diretiva deve ter outro conjunto de definições (por exemplo, a complexidade PIN). As definições de política não devem se sobrepõem ou não está em conflito.
2. Implemente as duas políticas para um conjunto de utilizadores.
3. Inscreva dois dispositivos iOS no Intune com a mesma conta de utilizador e uma conta que receberam as políticas no passo anterior. Os dispositivos devem cumpre os critérios da política de conformidade.
4. No Configuration Manager, consulte a **conformidade do dispositivo global** gráfico. Ambos os dispositivos devem comunicar como não conforme.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Verifique o gráfico de principais motivos de não conformidade
5. Verifique os **principais motivos de não conformidade** gráfico. Este gráfico apresenta uma lista os principais 5 motivos de não conformidade, mas quando apenas duas definições de conformidade foram definidas nas políticas apenas a parte superior 2 não conformidade motivos pelos quais são apresentados.
6. Clique das secções no gráfico. Ambos os dispositivos devem aparecer na exibição filtrada sob **ativos e compatibilidade** > **descrição geral** > **dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Tornar os dispositivos em conformidade e verifique os gráficos
7. Faça um dos dispositivos em conformidade com uma das políticas. Verifique os **conformidade do dispositivo global** novamente do gráfico. O gráfico deverá apresentar um dispositivo em conformidade e um dispositivo não conforme.
8. Que o outro dispositivo fique em conformidade com a mesma política. Isso fará um dispositivo em conformidade com as políticas e um dispositivo em conformidade com apenas uma das políticas.
9. Verifique os **principais motivos de não conformidade** gráfico. Deve haver um motivo de não conformidade listado.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
