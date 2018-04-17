---
title: Funcionalidades no Technical Preview 1609
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1609.
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
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: 4beca8479e5adbfa24b597769b792fd91bed9a2c
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1609 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*



Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1609. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    

**Problemas conhecidos neste Technical Preview:**  
*  Quando atualizar para a pré-visualização técnica do Configuration Manager 1609, serão eliminadas quaisquer políticas de atualização de edição que implementou. Para continuar a utilizar estas políticas, tem de recriar e implementá-las.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improvements-to-endpoint-protection"></a>Melhoramentos ao Endpoint Protection
Melhoramento às definições de política de antimalware do Endpoint Protection - pode agora especificar o nível no qual o serviço de proteção de nuvem do Endpoint Protection irá impedir que ficheiros suspeitos. Uma nova definição permite aos administradores especificar "duvidosos" computadores com base nas quantidades elevadas de software maligno que se deparam.

## <a name="increased-number-of-enrolled-devices"></a>Aumento do número de dispositivos inscritos
Os administradores podem agora ativar aos utilizadores a inscrição até 15 dispositivos em gestão de dispositivos móveis híbrida com o Intune. O limite era anteriormente 5 dispositivos por utilizador.

## <a name="additional-apple-dep-settings"></a>Definições adicionais do DEP da Apple

Os administradores podem configurar agora as seguintes definições do programa de inscrição de dispositivos da Apple (DEP) no perfil do DEP para dispositivos iOS e Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Se estiver ativada, Assistente da Apple de configuração solicita este serviço durante a ativação do dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integração com a análise de atualização

Análise de atualização permite-lhe avaliar e analisar a preparação do dispositivo e a compatibilidade com o Windows 10, para permitir atualizações smoother e mais fácil. Com a integração de análise de atualização com o Configuration Manager, pode aceder aos dados de compatibilidade da atualização na consola de administração do Configuration Manager e, em seguida, na lista de dispositivos de destino dispositivos para atualização ou correção.

Pode ler mais sobre a análise de atualização no [introdução à análise de atualização](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Perfis de VPN híbrida de tipos de ligação de nativo para Windows 10

Quando utilizar o Configuration Manager com o Intune, agora, pode criar perfis de VPN do Windows 10 com o Microsoft Automatic, IKEv2, PPTP e L2TP tipos de ligação na consola do Configuration Manager sem utilizar definições OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhoramentos à loja Windows para integração de negócios com o Configuration Manager

Nesta versão, atualizámos [da loja Windows para integração de negócios](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) com estas novas funcionalidades:

**Atualização:** A versão de pré-visualização técnica atual, a funcionalidade de sincronização imediata não está funcional.

- Anteriormente, só foi possível implementar aplicações gratuitas da loja Windows para empresas. Gestor de configuração agora adicionalmente suporta a implementação de paga online licenciado aplicações (apenas para dispositivos inscritos no Intune).
- Agora, pode iniciar uma sincronização imediata entre a loja Windows para empresas e o Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Active Directory

### <a name="try-it-out"></a>Experimente!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Comprar e sincronizar uma aplicações licenciadas online paga

1. Compre uma aplicações licenciadas online paga da loja Windows para empresas.
2. No **administração** área de trabalho da consola do Configuration Manager, clique em **serviços em nuvem** > **atualizações e manutenção** > **loja Windows para empresas**.
3. No **home page** separador o **sincronização** , clique em **sincronizar agora**.
4. Em breve, em seguida, a aplicação que comprou será apresentado o **informações de licença para aplicações da loja** o nó do **gestão de aplicações** área de trabalho.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Criar e implementar uma aplicação do Configuration Manager de dados da aplicação sincronizados

O procedimento para criar e implementar uma aplicação do Configuration Manager de uma aplicação da loja paga é igual para criar uma aplicação a partir de uma aplicação gratuita. Consulte a secção **criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação de negócio** no [gerir aplicações da loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificar a chave secreta do cliente do Azure Active Directory

1. No **administração** área de trabalho da consola do Configuration Manager, clique em **serviços em nuvem** > **atualizações e manutenção** > **loja Windows para empresas**.
2. Selecione a loja Windows para a conta de empresa e, em seguida, clique em **propriedades**.
3. No **da loja Windows para empresas propriedades da conta** caixa de diálogo, introduza uma nova chave no **chave secreta do cliente** campo e, em seguida, clique em **verifique**. Depois de verificar, clique em **aplicar**, em seguida, feche a caixa de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração

Adicionámos muitas novas definições, que pode utilizar os itens de configuração para várias plataformas de dispositivos.
Estas são as definições que existiam no Microsoft Intune numa configuração autónoma e anteriormente estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Se precisar de ajuda com qualquer uma destas definições, abra [gerir definições e funcionalidades nos seus dispositivos com políticas do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies) e, em seguida, selecione o subtopic definições para a plataforma que pretende.


### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android

#### <a name="password-settings"></a>Definições de palavra-passe

- **Memorizar histórico de palavra-passe**
- **Permitir impressões digitais desbloquear**

#### <a name="security-settings"></a>Definições de segurança

- **Exigir encriptação em cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de janelas de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições de aplicação

- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir armazenamento amovível**
- **Permitir tethering Wi-Fi**
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

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**
- **Minutos de inatividade antes da proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos Windows 10 Desktop e Mobile

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavra-passe**
- **Exigir uma palavra-passe quando o dispositivo regressa de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória no dispositivo móvel**
- **Permitir anular inscrições**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir VPN sobre redes móveis**
- **Permitir roaming do VPN sobre redes móveis**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações de centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team

#### <a name="device-settings"></a>Definições do dispositivo

- **Ativar a informações operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolha as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL de imagem de fundo do ecrã de bloqueio**


### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Tipo de palavra-passe obrigatório**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão repetidas permitidas antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração da palavra-passe (dias)**
- **Memorizar histórico de palavra-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir deteção automática de rede intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo

- **Permitir ligação automática a hotspots Wi-Fi**


## <a name="improvements-for-boundary-groups"></a>Melhoramentos para os grupos de limites
Esta pré-visualização introduz alterações importantes para os grupos de limites e como funcionam com pontos de distribuição. Estas alterações ajudará a simplificar a estrutura da sua infraestrutura de conteúdo ao dando-lhe mais controlo sobre como e quando os pontos de contingência de clientes para procurar distribuição adicionais como localizações de origem de conteúdo. Isto inclui pontos de distribuição baseado na nuvem e no local.

Estas melhorias substituir conceitos e comportamentos poderá estar familiarizado com hoje em dia (como configurar pontos de distribuição para ser rápida ou lenta) e substitui-os com um novo modelo que deve ser mais fácil de configurar e manter. Estas alterações também são base para as alterações futuras que irá melhorar outras funções de sistema de sites, que associar a grupos de limites.  

Durante a atualização 1609, a atualização converte das configurações de grupo de limites atuais para ajustar o novo modelo de modo a que estas alterações não disturb as configurações de distribuição de conteúdo (consulte [atualizar os grupos de limites existentes para o novo modelo](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)).

As secções seguintes pormenorizadamente as alterações introduzidas com esta pré-visualização, como funciona o novo modelo e o que pode esperar quando atualizar um site que já tenha configurados os grupos de limites.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Alterações na IU e o comportamento para grupos de limites e localizações de conteúdo
Seguem-se chave alterações aos grupos de limites e a forma como os clientes localizam os conteúdos. Muitas destas alterações e conceitos funcionam em conjunto.
-   **Configurações para rápida ou lenta são removidas:** Já não está a configurar pontos de distribuição individuais para serem rápida ou lenta.  Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Devido a esta alteração, o **referências** separador das propriedades do grupo de limites já não suporta a configuração rápida ou lenta.
-   **Novo grupo de limites de predefinição em cada site:**  Cada site primário tem um novo grupo de limites de predefinição com o nome ***predefinição-Site-limite-grupo\<sitecode >***.  Quando um cliente não está numa localização de rede que está atribuída a um grupo de limites, esse cliente utilizará os sistemas de sites associados ao grupo predefinido do seu site atribuído. Planear a utilização deste grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.    
 -  **'Permitir que as localizações de origem de contingência para conteúdo'** for removido: Já não está explicitamente a configurar um ponto de distribuição para ser utilizado para contingência e as opções para configurar esta são removidas da IU.

    Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação tipo para aplicações foi alterada. Esta definição num tipo de implementação agora permite que um cliente para utilizar o grupo de limites de site predefinido como uma localização de origem de conteúdo.

 -  **Relações de grupos de limites:** Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que estão configuradas no novo limite grupo separador de propriedades com o nome **relações**:
    -   Cada grupo de limites que um cliente é diretamente associado é chamado um **atual** grupo de limites.  
    -   Nenhum grupo de limites pode utilizar um cliente devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo é chamado um **vizinho** grupo de limites.
    -  É o **relações** separador adicionar grupos de limites que podem ser utilizados como um *vizinho* grupo de limites. Também pode configurar um período de tempo em minutos que determina quando um cliente que não consegue localizar o conteúdo a partir de um ponto de distribuição no *atual* grupo irá começar a procurar nas localizações de conteúdo das *vizinho* grupos de limites.

        Quando adicionar ou alterar uma configuração do grupo de limites, terá a opção para o bloco de contingência para esse grupo de limites específico do grupo atual que estiver a configurar.

    Para utilizar a nova configuração, pode define associações explícitas (ligações) a partir de um grupo de limites para outro e configura todos os pontos de distribuição nesse grupo associados com o mesmo tempo em minutos. O tempo que configura determina quando um cliente que não consegue encontrar uma origem de conteúdo do respetivo *atual* grupo de limites pode começar a pesquisar origens de conteúdo desse grupo de limites de vizinho.

    Além dos grupos de limites que configurar explicitamente, cada grupo de limites tem uma ligação implícita para o grupo de limites de site predefinido. Esta ligação fica ativa depois de 120 minutos em que momento o grupo de limites de site predefinido torna-se um grupo de limites de vizinho que permite que os clientes utilizar os pontos de distribuição associados esse grupo de limites como localizações de origem de conteúdo.

    Este comportamento substitui que anteriormente foi referido como contingência para conteúdo.  Pode substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo e definir uma hora específica em minutos ou bloquear contingência inteiramente para impedir a sua utilização.


-   **Os clientes tentam obter conteúdos de cada ponto de distribuição para 2 minutos:** Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição para 2 minutos antes de, em seguida, tentar outro ponto de distribuição. Esta é uma alteração de versões anteriores onde os clientes tentaram ligar a um ponto de distribuição de até 2 horas.

    - O primeiro ponto de distribuição que um cliente tenta utilizar aleatoriamente está selecionado do agrupamento de pontos de distribuição disponíveis do cliente *atual* grupo de limites (ou grupos).

    - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. Este processo repete-se a cada dois minutos até que o cliente localiza o conteúdo ou atinge o último servidor no seu conjunto.

    - Se um cliente não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* agrupamento antes do período de contingência para um *vizinho* for atingido o grupo de limites, o cliente, em seguida, adiciona os pontos de distribuição do *vizinho* até ao fim da respetiva lista atual de grupo e, em seguida, irá procurar o grupo expandido das localizações de origem que inclua os pontos de distribuição a partir de ambos os grupos de limites.

        > [!TIP]  
        > Quando criar uma ligação explícita do grupo de limites atuais para o grupo de limites de site predefinido e definir uma hora de contingência que é inferior à hora de contingência para uma ligação a um grupo de limites de vizinho, os clientes começam a pesquisar localizações de origem do grupo de limites de site predefinido antes, incluindo o grupo de vizinho.

    - Quando o cliente não consegue obter conteúdos do último servidor no agrupamento, começar o processo de novo.


### <a name="how-the-new-model-works"></a>Como funciona o novo modelo
Quando configura grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como pontos de distribuição, para o grupo de limites. Isto ajuda os clientes de ligação a servidores do sistema de sites como perto de pontos de distribuição que estão localizados os clientes na rede.   
-   É possível atribuir o mesmo limite a vários grupos de limites
-   Servidores do sistema de sites, como pontos de distribuição, podem ser associados a vários grupos de limites, disponibilizando-as para uma vasta gama de localizações de rede
-   Se um ponto de distribuição não estiver associado a um grupo de limites, os clientes não poderão utilizar esse ponto de distribuição como localização de origem de conteúdo.

A partir desta pré-visualização técnica, é possível definir relações de grupo de limites para configurar o comportamento de contingência para localizações de origem de conteúdo. Este novo comportamento está configurado no novo **relações** separador de propriedades do grupo de limites e substitui a configuração de sistemas de sites para ser rápida ou lenta e configurar um grupo de limites para permitir a localização de origem de contingência para conteúdo.

No separador relações adicionar outros grupos de limites para configurar uma relação a esses grupos. Cada relação é uma hiperligação unidirecional do **atual** grupo de limites para o grupo de limites que adiciona, que é chamado um **vizinho**. Para cada ligação de que criar, pode configurar pontos de distribuição com um tempo de contingência em minutos. Este tempo é utilizado para determinar após clientes quanto a *atual* grupo de limites pode começar a utilizar pontos de distribuição a *vizinho* grupo de limites que se encontrem não é possível encontrar uma localização de origem de conteúdo válida do respetivo grupo de limites atual.

Quando um cliente não é possível localizar o conteúdo e começa a procurar nas localizações dos grupos de limites de vizinho, aumenta o conjunto de pontos de distribuição disponíveis para que o cliente de forma controlada.  

-   Um grupo de limites pode ter mais de uma relação. Isto permite-lhe configurar contingência aos diferentes vizinhos para ocorrer após os períodos de tempo diferentes.
-   Os clientes irão contingência apenas a um grupo de limites que é um vizinho direto do respetivo grupo de limites atuais.
-   Quando um cliente é um membro de vários grupos de limites, o grupo de limites atual está definido como uma União de tudo o que os grupos de limites do cliente.  Que o cliente pode, em seguida, contingência para um vizinho de qualquer um desses grupos de limites original.

Para além das ligações que define, há uma ligação implícita que é criada automaticamente entre os grupos de limites que cria e o grupo de limites predefinido que é criado automaticamente para cada site. Esta ligação automática:
-   É utilizado por clientes que são não num limite associado a nenhum grupo de limites na hierarquia automaticamente utilizar o grupo de limites predefinidos do respetivo site atribuído para identificar as localizações de origem de conteúdo válida.   
-   É uma opção de contingência de predefinição do grupo de limites atuais ao grupo de limites de sites predefinido que é utilizado depois de 120 minutos.

**Exemplo de como utilizar o novo modelo:**     
Crie três grupos de limites que não partilham limites ou servidores de sistema de sites:
-   Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-   Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-   Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associados ao grupo

A adicionar as localizações de rede dos clientes como limites para apenas o grupo de limites BG_A e, em seguida, configurar relações desse grupo de limites para os outros dois grupos de limites:
-   Configurar pontos de distribuição para o primeiro *vizinho* grupo (BG_B) a ser utilizada após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são boas ligações para as localizações de limites de grupos primeiro.
-   Configurar a segunda *vizinho* grupo (BG_C) a ser utilizada após 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são através de uma WAN dos outros grupos de limites de dois.
-   Pode também adiciona um ponto de distribuição adicionais que está localizado no servidor do site ao grupo de limites de site de sites predefinido. Esta é a localização de origem de conteúdo menos preferencial, mas está centralmente localizado para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
-   O cliente começa a procurar conteúdo dos pontos de distribuição no respetivo *atual* pesquisar a distribuição de cada grupo de limites (BG_A), para que aponte do dois minutos antes de mudar para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-   Se o cliente não conseguir localizar o conteúdo do respetivo *atual* grupo de limites depois de procurar durante 10 minutos, em seguida, adiciona os pontos de distribuição do grupo de limites BG_B para a sua pesquisa. Em seguida, continua a pesquisar conteúdo a partir de um ponto de distribuição no respetivo conjunto combinado de pontos de distribuição que inclui os grupos de limites BG_A tanto BG_B agora. O cliente continua a contactar cada ponto de distribuição de dois minutos antes de mudar para o próximo ponto de distribuição do seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-   Após um adicionais de 10 minutos (totais de 20 minutos) se o cliente ainda não encontrou um ponto de distribuição com conteúdo, que expande o conjunto de pontos de distribuição disponíveis para incluir as da segunda *vizinho* grupo, o grupo de limites BG_C. O cliente agora tem 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a alteração cada dois minutos até ser encontrado conteúdo para um novo ponto de distribuição.
-   Se o cliente não foi encontrado conteúdo depois de um total de 120 minutos, fica novamente para incluir o *grupo de limites de site predefinido* como parte da sua pesquisa contínua. O conjunto de pontos de distribuição inclui agora todos os pontos de distribuição dos três grupos de limites configurado e o ponto de distribuição final localizado no computador do servidor do site.  O cliente, em seguida, continua a pesquisa de conteúdo, alterar a cada dois minutos até ser encontrado conteúdo de pontos de distribuição.

Ao configurar os grupos de vizinho diferentes para estar disponível em alturas diferentes, pode controlar quando são adicionados como uma localização de origem de conteúdo, pontos de distribuição específico e quando, ou se, o cliente utiliza a contingência para o grupo de limites de site predefinido como uma rede de segurança para o conteúdo que não está disponível a partir de qualquer outra localização.


### <a name="bkmk_update"></a>Atualizar os grupos de limites existentes para o novo modelo
Quando instalar a versão 1609 e atualizar o site, as seguintes configurações são efetuadas automaticamente. Estes são concebidas para Certifique-se de que o comportamento de contingência atual permanece disponível, até configurar novos grupos de limites e relações.  
-   Pontos de distribuição não protegido num site são adicionados para o *predefinição-Site-limite-grupo\<sitecode >* grupo de limites desse site.
-   É efetuada uma cópia de cada grupo de limites existentes, que inclui um servidor de site configurado com uma ligação lenta. O nome do novo grupo é  ***\<nome original do grupo de limites > Tmp - lenta -***:  
    -   Sistemas de sites que tenham uma ligação rápida são mantidos no grupo de limites original.
    -   Uma cópia dos sistemas de sites que tenham uma ligação lenta são adicionadas para a cópia do grupo de limites. Os sistemas de site original configurados como lenta permanecem no grupo de limites original para compatibilidade com versões anteriores, mas não são utilizados desse grupo de limites.
    -   Esta cópia do grupo de limites não tem limites associados à mesma. No entanto, é criada uma ligação de contingência entre o grupo original e a nova cópia do grupo de limites com o tempo de contingência definido como zero.

 A tabela seguinte identifica o novo comportamento contingência pode esperar da combinação de definições de implementação original e a distribuição de configurações de pontos:

Configuração de implementação original "não executaram" na rede lenta  |Configuração para "Permitir ao utilizar uma localização de origem de contingência para conteúdo de cliente" do ponto de distribuição original  |Novo comportamento de contingência  
---------|---------|---------
Selecionado     |  Selecionado    |  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Selecionado     |  Não selecionada|  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Não selecionada |  Não selecionada|  **Contingência para vizinho** - utilizar os pontos de distribuição no grupo de limites atual e, em seguida, adicione os pontos de distribuição do grupo de limites de vizinho. A menos que uma ligação explícita para o grupo de limites de site predefinido está configurada, os clientes irão não contingência a esse grupo.    
Não selecionada | Selecionado     |   **Contingência normal** -utilizar pontos de distribuição no grupo de limites atual, em seguida, os do site e vizinho predefinido de grupos de limites

 Todas as outras configurações de implementação resultam em **contingência Normal**.  



## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
O Configuration Manager 1609 Technical Preview introduz um novo dashboard. Para ver o dashboard, na consola do Configuration Manager vá para **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
>[!NOTE]
>No **Novidades** área de trabalho na consola do Configuration Manager, o novo dashboard incorretamente denominado **dashboard de manutenção do Office 365**.

O dashboard apresenta gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
Para obter mais informações, consulte [canais de consumo de descrição geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Regras de implementação automática que tenham o cliente do Office 365 selecionadas no conjunto de produtos disponíveis.

Pode efetuar as seguintes ações no dashboard:
- Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros da coleção específica.
- No lado superior direito do dashboard, clique em **instalador do Office 365** para iniciar o Assistente de instalação de cliente do Office 365 para implementar aplicações do Office 365 nos clientes. Para obter mais informações, consulte [aplicações de implementar o Office 365 para clientes](#deploy-office-365-apps-to-clients).
- No lado direito de meio do dashboard, clique em **criar uma ADR** para abrir o Assistente de regra de implementação automática para criar uma nova regra de implementação automática (ADR). Para criar uma ADR para aplicações do Office 365, selecione **cliente do Office 365** quando escolhe o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- No lado direito de inferior do dashboard, clique em **criar definições de agente de cliente** para abrir as definições do agente de cliente. Para obter mais informações, consulte [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings).



Para obter mais informações sobre as atualizações do Office 365 ProPlus, consulte [gerir o Office 365 ProPlus atualizações com o Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 nos clientes
Nesta versão, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador de 365 do Office que lhe permite configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitações da implementação do Office 365
- Poderá ter problemas ao tentar importar as definições de cliente existente (XML) no Assistente de instalação de aplicações do Office 365. Pode configurar manualmente as definições de cliente sem um problema.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implementar aplicações do Office 365 nos clientes
1. Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **instalador do Office 365** no painel superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. No **definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **seguinte**. Tenha em atenção que a localização tem de ser especificada no formato &#92; &#92; *servidor*&#92;*partilhar*.
4. No **importar as definições de cliente** página, escolha se importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente ou especifique manualmente as definições e, em seguida, clique em **seguinte**.
Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e avance para o passo 7. Tenha em atenção que a localização tem de ser especificada no formato &#92; &#92; *servidor*&#92;*partilhar*&#92;*filename*. XML.

    > [!IMPORTANT]
    >Poderá ter problemas ao tentar importar as definições de cliente existente (XML) nesta pré-visualização técnica.

5. No **cliente produtos** página, selecione o Office 365 suite que utilizar, selecione as aplicações que pretende incluir, selecione os produtos de Office adicionais que devem ser incluídos e, em seguida, clique em **seguinte**.
6. No **as definições de cliente** página, escolha as definições para incluir e, em seguida, clique em **seguinte**.
7. No **implementação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **seguinte**.
Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure as restantes páginas do assistente, tal como faria para uma implementação de aplicação típica. Para obter mais informações, consulte [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação, tal como faria com qualquer outra aplicação no Configuration Manager de **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**.

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar uma ADR para aplicações do Office 365, clique em **criar uma ADR**e selecione **cliente do Office 365** quando escolhe o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="BKMK_UEFIConversion"></a>Melhoramentos para BIOS para conversão de UEFI
Agora, pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o passo de reiniciar o computador irá preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar os passos de sequência de tarefas para preparar a unidade de disco rígido para o BIOS para conversão de UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Uma sequência de tarefas existente para instalar um sistema operativo, irá adicionar um novo grupo com os passos para fazer o BIOS para conversão de UEFI.

1. Crie um novo grupo de sequência de tarefas depois dos passos para capturar ficheiros e definições e antes dos passos para instalar o sistema operativo. Por exemplo, crie um grupo depois do **capturar ficheiros e definições** com o nome de grupo **BIOS para UEFI**.
2. No **opções** separador do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **smstsbootuefi sempre** é **não igual a** para **verdadeiro**. Isto impede que os passos no grupo de executar quando um computador já está no modo UEFI.
![BIOS para o grupo de UEFI](media/BIOS-to-UEFI-group.png)
3. No novo grupo, adicione o **reiniciar o computador** passo de sequência de tarefas. No **especificam o que executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  
4. No **opções** separador, adicione uma variável de sequência de tarefas como uma condição em que **smstsinwinpe é igual a FALSO**. Isto impede que este passo em execução se o computador já está no Windows PE.

    ![Reinicie o passo de computador](media/Restart-in-Windows-PE.png)
5. Adicione um passo para iniciar a ferramenta de OEM converterá o firmware da BIOS em UEFI. Normalmente, este será um **executar linha de comandos** passo de sequência de tarefas com uma linha de comandos para iniciar a ferramenta OEM.
5.  Adicione o passo de sequência de tarefas formatar e particionar disco que será particionar e formatar o disco rígido. No passo, efetue o seguinte:
    1.  Crie a partição de FAT32 será convertida em UEFI antes do sistema operativo está instalado. Escolha **GPT** para **tipo de disco**.
    ![Formatar e particionar passo de disco](media/Format-and-partition-disk.png)
    2.  Vá para as propriedades para a partição FAT32. Introduza **TSUEFIDrive** no **variável** campo. Quando a sequência de tarefas Deteta esta variável, irá preparar para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](media/Partition-properties.png)
    3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para guardar o estado e armazenar ficheiros de registo.
6.  Adicionar o **reiniciar o computador** passo de sequência de tarefas. No **especificam o que executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de conformidade do Intune
Nesta versão, pode obter uma vista rápida do gerais de conformidade para dispositivos e principais razões para inconformidade utilizando o novo gráficos em **área de trabalho de monitorização** na consola do Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Para ver os gráficos de conformidade do Intune
1. Na consola do Configuration Manager, vá para **monitorização** > **descrição geral** > **as definições de compatibilidade**.
2. O **gerais de conformidade de dispositivo** gráfico é apresentado.
3. Clique em de **políticas de conformidade** nó para ver o **gerais de conformidade de dispositivo** e **por motivos de não conformidade superior** gráficos.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitações de gráficos de conformidade do Intune no TP 1609
- Desagregar para o **gerais de conformidade de dispositivo** gráfico atualmente produz um erro.
- O **principais razões de não conformidade** gráfico apresenta o nome da política e não as razões de não conformidade individuais. Pode clicar a política para desagregar e ver os dispositivos que são incompatíveis para essa política.

### <a name="try-it-out"></a>Experimente
Conclua as seguintes secções por ordem:

#### <a name="check-overall-compliance-chart"></a>Gráfico da conformidade global de verificação
1. Adicione no duas iOS políticas de conformidade no Configuration Manager. Uma política deve ter um conjunto de definições para dispositivos (por exemplo, conjunto de comprimento do PIN 6). A outra política deve ter outro conjunto de definições (por exemplo, a complexidade PIN). As definições de política não devem sobrepor-se ou em conflito.
2. Implemente as duas políticas para um conjunto de utilizadores.
3. Inscrever-se dois dispositivos iOS no Intune com a mesma conta de utilizador e uma conta que receberam as políticas no passo anterior. Os dispositivos devem não cumpre os critérios da política de conformidade.
4. No Configuration Manager, verifique o **gerais de conformidade de dispositivo** gráfico. Ambos os dispositivos devem reportar como não conforme.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Verifique o gráfico de principais razões de não conformidade
5. Verifique o **principais razões de não conformidade** gráfico. Este gráfico apresenta uma lista de 5 principais razões para não conformidade, mas quando apenas duas definições de conformidade foram definidas através de políticas apenas parte superior 2 inconformidade motivos são apresentados.
6. Clique das secções no gráfico. Ambos os dispositivos devem aparecer na vista filtrada em **ativos e compatibilidade** > **descrição geral** > **dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Tornar os dispositivos em conformidade e consulte os gráficos
7. -Um dos dispositivos compatíveis com uma das políticas. Verifique o **gerais de conformidade de dispositivo** gráfico novamente. O gráfico deve apresentar um dispositivo compatível e dispositivos não conformes.
8. -O outros dispositivos compatíveis com a mesma política. Isto faz com que um dispositivo compatível com as políticas e de um dispositivo compatível com apenas uma das políticas.
9. Verifique o **principais razões de não conformidade** gráfico. Só deve ser um motivo de não conformidade listado.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
