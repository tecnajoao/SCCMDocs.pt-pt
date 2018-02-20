---
title: "Definições do cliente"
titleSuffix: Configuration Manager
description: "Escolha as definições de cliente utilizando a consola de administrador no System Center Configuration Manager."
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: dddfde242a67a0b4a9311c0fb6f0b2f0e6742cc2
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/19/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as definições de cliente no System Center Configuration Manager

Aplica-se a: System Center Configuration Manager (ramo atual)*

Gerir todas as definições de cliente na consola do Configuration Manager do **as definições de cliente** no nó de **administração** área de trabalho. O Configuration Manager inclui um conjunto de predefinições. Quando alterar as predefinições de cliente, estas definições são aplicadas a todos os clientes na hierarquia. Também pode configurar as definições de cliente personalizadas, que substituem as predefinições de cliente quando atribuí-las a coleções. Para obter mais informações, consulte [como configurar as definições de cliente](../../../core/clients/deploy/configure-client-settings.md).

As secções seguintes descrevem as definições e as opções mais detalhadamente.  
 

## <a name="background-intelligent-transfer-service-bits"></a>Serviço de transferência inteligente em segundo plano (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitar a largura de banda de rede máxima para transferências de fundo do BITS
Quando esta opção é **Sim**, os clientes utilizam a limitação de largura de banda do BITS. Para configurar outras definições, este grupo, tem de ativar esta definição. 

### <a name="throttling-window-start-time"></a>Hora de início da janela de limitação
Especifique a hora de início local para a janela de limitação do BITS.  

### <a name="throttling-window-end-time"></a>Hora de fim da janela de limitação
Especifique a hora de fim local para a janela de limitação do BITS. Se a hora de fim é igual do **hora de início da janela de limitação**, limitação do BITS é sempre ativado.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Velocidade máxima de transferência durante a janela de limitação (Kbps)
Especifique a velocidade máxima de transferência que os clientes podem utilizar durante a janela.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Permitir transferências BITS fora da janela de limitação
Permitir aos clientes utilizar definições de BITS separadas fora da janela especificada.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Velocidade máxima de transferência fora da janela de limitação (Kbps)
Especifique a velocidade máxima de transferência que os clientes podem utilizar fora do janela de limitação do BITS.  



## <a name="client-cache-settings"></a>Definições de cache do cliente

### <a name="configure-branchcache"></a>Configurar o BranchCache
Configurar o computador cliente para [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir a colocação em cache de BranchCache no cliente, defina **ativar BranchCache** para **Sim**.

- **Ativar o BranchCache** </br>
    Permite que o BranchCache nos computadores cliente.

- **Tamanho máximo da cache do BranchCache (percentagem do disco)** </br>
    A percentagem do disco que permitem o BranchCache utilizar. 

### <a name="configure-client-cache-size"></a>Configurar o tamanho da cache do cliente
A cache do cliente do Configuration Manager em computadores Windows armazena ficheiros temporários utilizados para instalar aplicações e programas. Se esta opção estiver definida como **não**, o tamanho predefinido é 5,120 MB.

Se optar por **Sim**, em seguida, especifique:
- **Tamanho máximo da cache (MB)**
- **Tamanho máximo da cache (percentagem do disco)** </br>
Expande o tamanho da cache do cliente para o tamanho máximo em megabytes (MB) ou a percentagem do disco, o que for menor. 

### <a name="enable-configuration-manager-client-in-full-os-to-share-content"></a>Ativar cliente do Configuration Manager no SO completo para partilhar conteúdo
Permite [elemento cache](/sccm/core/plan-design/hierarchy/client-peer-cache) para clientes do Configuration Manager. Escolha **Sim**e, em seguida, especifique a porta através do qual o cliente comunica com o computador de ponto a ponto. 
- **Porta para difusão de rede inicial** (predefinida 8004)
- **Porta para transferência do conteúdo de elemento de rede** (8003 predefinida) </br>
O Configuration Manager configura automaticamente regras de Firewall do Windows para permitir que este tráfego. Se utilizar uma firewall diferente, tem de configurar manualmente as regras para permitir que este tráfego.




## <a name="client-policy"></a>Política do cliente  

### <a name="client-policy-polling-interval-minutes"></a>Intervalo de consulta da política de cliente (minutos)

Especifica a frequência os seguintes clientes do Configuration Manager transferirem a política de cliente:
-   Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  
-   Dispositivos móveis que inscreve do Configuration Manager  
-   Computadores Mac  
-   Computadores com o Linux ou UNIX  

### <a name="enable-user-policy-on-clients"></a>Ativar política de utilizador nos clientes

Quando definir esta opção **Sim**e utilizar [deteção de utilizadores](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), em seguida, os clientes recebem aplicações e programas direcionadas para o utilizador com sessão iniciada.  

O catálogo de aplicações recebe a lista do software disponível para utilizadores do servidor do site. Assim, esta definição não tem de ser **Sim** para os utilizadores possam visualizar e pedir aplicações a partir do catálogo de aplicações. Se esta definição é **não**, seguintes comportamentos não funcionam quando os utilizadores utilizam o catálogo de aplicações:  

-   Os utilizadores não podem instalar as aplicações que veem no Catálogo de Aplicações.  

-   Os utilizadores veem notificações sobre os seus pedidos de aprovação de aplicações. Em vez disso, devem atualizar o Catálogo de Aplicações e verificar o estado de aprovação.  

-   Os utilizadores não recebem revisões nem atualizações para as aplicações que são publicadas no catálogo de aplicações. Os utilizadores veem alterações às informações da aplicação no catálogo de aplicações.  

-   Se remover uma implementação de aplicação depois do cliente instala a aplicação no catálogo de aplicações, os clientes continuam a verificar que a aplicação está instalada até dois dias.  

Além disso, se esta definição é **não**, os utilizadores não recebem as aplicações necessárias que implementar nos utilizadores. Os utilizadores também não receber quaisquer outras tarefas de gestão em políticas de utilizador.  

Esta definição aplica-se aos utilizadores cujos computadores estão na intranet ou à internet. Tem de ser **Sim** se também pretender ativar políticas de utilizador na internet.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Ativar pedidos da política de utilizador dos clientes internet

Defina esta opção para **Sim** para os utilizadores receberem a política de utilizador em computadores baseados na internet. Também são aplicáveis os seguintes requisitos:  

-   O cliente e o site estão configurados para gestão de clientes baseados na internet.

-   O **ativar política de utilizador nos clientes** definição é **Sim**.  

-   O ponto de gestão baseado na internet autentica com êxito o utilizador ao utilizar a autenticação do Windows (Kerberos ou NTLM).  

Se definir esta opção para **não**, ou qualquer um dos requisitos anteriores não são cumpridos, em seguida, um computador com a internet apenas recebe políticas de computador. Neste cenário, os utilizadores ainda podem ver, pedir e instalar aplicações a partir de um catálogo de aplicações baseado na internet. Se esta definição é **não**, mas **ativar política de utilizador nos clientes** é **Sim**, os utilizadores não recebem políticas de utilizador, até que o computador está ligado à intranet.  

Para obter mais informações sobre a gestão de clientes na internet, consulte [considerações sobre comunicações do cliente da internet ou numa floresta não fidedigna](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

> [!NOTE]  
>  Os pedidos de aprovação de aplicações dos utilizadores não necessitam de políticas de utilizador ou de autenticação de utilizador.  


## <a name="cloud-services"></a>Serviços cloud

### <a name="allow-access-to-cloud-distribution-point"></a>Permitir o acesso ao ponto de distribuição de nuvem
Defina esta opção para **Sim** para os clientes obter conteúdo de um ponto de distribuição na nuvem. Esta definição não requer que o dispositivo ser baseados na internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory 
Quando configurar o Azure Active Directory para suportar a associação de híbrida, o Configuration Manager configura dispositivos Windows 10 para esta funcionalidade. Para obter mais informações, consulte [como para configurar híbrida do Azure Active Directory dispositivos associados a um](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Permitir que os clientes utilizar um gateway de gestão de nuvem
Por predefinição, todos os clientes de roaming de internet utilizam disponível qualquer [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Um exemplo de quando configurar esta definição para **não** é a utilização do âmbito do serviço, tal como durante um projeto piloto ou para reduzir os custos.



##  <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="enable-compliance-evaluation-on-clients"></a>Ativar avaliação de compatibilidade nos clientes
Defina esta opção para **Sim** para configurar outras definições deste grupo.
 
### <a name="schedule-compliance-evaluation"></a>Agendar avaliação de compatibilidade
Selecione **agenda** para criar a agenda predefinida para a configuração de implementações de linha de base. Este valor é configurável para cada linha de base a **implementar linhas de base de configuração** caixa de diálogo.  

### <a name="enable-user-data-and-profiles"></a>Ativar perfis e dados de utilizador
Escolha **Sim** se pretender implementar [perfis e dados de utilizador](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) itens de configuração.



## <a name="computer-agent"></a>Agente do computador  

### <a name="user-notifications-for-required-deployments"></a>Notificações de utilizador para as implementações necessárias

Para mais informações sobre as seguintes três definições, consulte [notificações de utilizador para as implementações necessárias](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):

-   **Prazo de implementação superior a 24 horas, lembrar o utilizador a cada (horas)**
-   **Implementação prazo inferior a 24 horas, lembrar o utilizador a cada (horas)** 
-   **Implementação prazo inferior a 1 hora, lembrar o utilizador a cada (minutos)** 

### <a name="default-application-catalog-website-point"></a>Ponto de Web sites Predefinido do Catálogo de Aplicações

O Configuration Manager utiliza esta definição para ligar utilizadores ao catálogo de aplicações a partir do Centro de Software. Selecione **conjunto site** para especificar um servidor que aloja o ponto de Web site do catálogo de aplicações. Introduza o nome NetBIOS ou FQDN, especificar deteção automática ou especificar um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor opção, porque este oferece as seguintes vantagens:  

-   Se o site tiver um ponto de Web site do catálogo de aplicações, em seguida, os clientes recebem automaticamente um ponto de Web site do catálogo de aplicações do respetivo site.  

-   O cliente prefers pontos de Web site do catálogo de aplicações ativadas por HTTPS da intranet através de servidores apenas de HTTP. Esta capacidade ajuda a proteger contra um servidor não autorizado.

-   O ponto de gestão proporciona um ponto de Web site do catálogo de aplicações baseado na internet de clientes baseados na internet. O ponto de gestão proporciona um ponto de Web site do catálogo de aplicações baseado na intranet de clientes baseados na intranet.  

A deteção automática não garante que os clientes recebem o ponto de Web site do catálogo de aplicações mais próximo. Pode decidir não utilizar **Detetar automaticamente** pelos seguintes motivos:  

-   Pretende configurar o servidor mais próximo para clientes manualmente ou certifique-se de que não ligam a um servidor através de uma ligação de rede lenta.  

-   Pretende controlar que clientes ligam ao servidor. Esta configuração pode ser para fins de teste, desempenho ou por razões empresariais.  

-   Não pretende esperar até 25 horas ou para uma alteração de rede para os clientes utilizar um site do catálogo de aplicações diferentes ponto.  

Se, especifique o ponto de Web site do catálogo de aplicações em vez de utiliza a deteção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Esta configuração reduz a probabilidade de que o browser pede-lhe que os utilizadores de credenciais quando acedem a um catálogo de aplicações baseado na intranet. Para utilizar o nome NetBIOS, tem de aplicar as seguintes condições:  

-   O nome NetBIOS é especificado nas propriedades do ponto de Web sites do Catálogo de Aplicações.  

-   Utilizar o WINS ou todos os clientes estão no mesmo domínio que o ponto de Web site do catálogo de aplicações.  

-   Configurar o ponto de Web site do catálogo de aplicações para ligações de cliente HTTP ou configurar o servidor para HTTPS e o certificado de servidor web com o nome de NetBIOS.  

Normalmente, os utilizadores recebem um pedido de credenciais quando o URL tem um FQDN, mas não quando o URL é um nome NetBIOS. Espere que os utilizadores sempre ser-lhe pedido quando ligam a partir da internet, porque esta ligação tem de utilizar o FQDN de internet. Para um cliente baseado na internet, quando o browser solicita aos utilizadores credenciais, certifique-se de que o ponto de Web site do catálogo de aplicações pode ligar a um controlador de domínio para a conta de utilizador. Esta configuração permite ao utilizador autenticar através de Kerberos.  

> [!NOTE]  
>  Segue-se a deteção automática como funciona:  
>   
>  O cliente faz um pedido de localização de serviço para um ponto de gestão. Se houver um ponto de Web sites do Catálogo de Aplicações no mesmo site que o cliente, este servidor é atribuído ao cliente como o servidor do Catálogo de Aplicações a utilizar. Quando estiver disponível mais do que um ponto de Web site do catálogo de aplicações no site, um servidor ativado para HTTPS tem precedência sobre um servidor que não está ativado para HTTPS. Após esta filtragem, todos os clientes recebem um dos servidores a utilizar como catálogo de aplicações. O Configuration Manager não não-balanceamento de carga entre múltiplos servidores. Quando o site do cliente não tem um ponto de Web site do catálogo de aplicações, o ponto de gestão devolve não deterministicamente um ponto de Web site do catálogo de aplicações da hierarquia.  
>   
>  Os clientes baseados na intranet, se configurar o ponto de Web site do catálogo de aplicações com um nome de NetBIOS para o URL do catálogo de aplicações, o ponto de gestão utiliza-o. Não utilize o FQDN da intranet. Os clientes baseados na internet, o ponto de gestão fornece apenas o FQDN de internet ao cliente.  
>   
>  O cliente efetua este pedido de localização de serviço cada 25 horas ou sempre que Deteta uma alteração de rede. Por exemplo, se o cliente passar da intranet à internet, que é uma alteração de rede. Se o cliente, em seguida, localiza um ponto de gestão baseado na internet, o ponto de gestão baseado na internet atribui baseado na internet servidores de ponto de Web site do catálogo de aplicações aos clientes.  

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer

Se esta opção é **Sim**, o cliente adiciona automaticamente o atual URL de Web site do catálogo de aplicações predefinido a zona de sites fidedignos do Internet Explorer.  

Esta definição garante que a definição do Internet Explorer para o Modo Protegido não está ativada. Se o modo protegido estiver ativado, o cliente do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. Por predefinição, a zona sites fidedignos também suporta a sessão do utilizador para o catálogo de aplicações, que requer autenticação do Windows.  

Se deixar esta opção como **não**, clientes do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. É um método alternativo configurar estas definições do Internet Explorer noutra zona para o URL do catálogo de aplicações que os clientes utilizam.  

> [!NOTE]  
>  Sempre que o Gestor de configuração adiciona um URL do catálogo de aplicações predefinido para a zona sites fidedignos, o Configuration Manager remove quaisquer anteriormente adicionados URL do catálogo de aplicações.  
>   
>  Se o URL já estiver especificado das zonas de segurança, o Configuration Manager não é possível adicionar o URL. Neste cenário, tem de remover o URL da outra zona ou configurar manualmente as definições do Internet Explorer necessárias.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada

Esta definição tem de ser **Sim** os utilizadores utilizarem o catálogo de aplicações.  

Se alterar esta definição, entra em vigor quando os utilizadores em seguida o respetivo browser ou Atualize a respetiva janela do browser atualmente aberta.  

Para obter mais informações sobre esta definição, consulte [certificados do Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nome da organização apresentada no Centro de Software

Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna.  

### <a name="use-new-software-center"></a>Utilizar o novo Centro de Software

Se definir esta opção para **Sim**, em seguida, todos os computadores cliente utilizam o Centro de Software. Centro de software mostra as aplicações disponíveis ao utilizador que foram anteriormente acessíveis apenas no catálogo de aplicações. O catálogo de aplicações requer o Silverlight, que não é um pré-requisito para o Centro de Software.   

O ponto de Web site do catálogo de aplicações e serviço web do catálogo de aplicações do ponto de sistema de sites funções ainda são necessárias para aplicações disponíveis ao utilizador a aparecer no Centro de Software.  

Para obter mais informações, consulte [planear e configurar a gestão de aplicações](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

### <a name="enable-communication-with-health-attestation-service"></a>Ativar comunicação com o serviço de atestado de estado de funcionamento

Defina esta opção para **Sim** para dispositivos Windows 10 utilizar [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation). Quando ativa esta definição, a seguinte definição também está disponível para a configuração.

### <a name="use-on-premises-health-attestation-service"></a>Utilizar o serviço de atestado de estado de funcionamento no local

Defina esta opção para **Sim** nos dispositivos utilizar um serviço no local. Definido como **não** nos dispositivos utilizar o serviço baseado na nuvem da Microsoft.  

### <a name="install-permissions"></a>Permissões de instalação

> [!IMPORTANT]  
>  Esta definição aplica-se ao Catálogo de Aplicações e ao Centro de Software. Esta definição não tem efeito quando os utilizadores utilizam o Portal da empresa.  

Configure a forma como os utilizadores podem iniciar a instalação de software, atualizações de software e sequências de tarefa:  

-   **Todos os utilizadores**: Utilizadores com qualquer permissão, exceto convidado.  

-   **Apenas os administradores**: Os utilizadores tem de ser um membro do grupo de administradores locais.  

-   **Apenas administradores e utilizadores primários**: Os utilizadores tem de ser um membro do grupo local de administradores ou utilizadores primários do computador.  

-   **Não existem utilizadores**: Nenhum utilizador com sessão iniciada num computador cliente poderá iniciar a instalação de software, atualizações de software e sequências de tarefas. As implementações necessárias para o computador instalar sempre na data limite. Os utilizadores não é possível iniciar a instalação de software a partir do catálogo de aplicações ou centro de Software.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Suspender introdução de PIN do BitLocker no reinício

Se a computadores exigirem a introdução do PIN do BitLocker, esta opção ignora o requisito de introduzir um PIN quando o computador for reiniciado após uma instalação de software.  

-   **Sempre**: O Configuration Manager suspende temporariamente o BitLocker após a instalação de software que requeira um reinício, iniciou um reinício do computador. Esta definição só se aplica a um reinício do computador iniciado pelo Configuration Manager. Esta definição não suspende o requisito de introduzir o PIN do BitLocker quando o utilizador reinicia o computador. O requisito de introdução do PIN do BitLocker retoma após o arranque do Windows.

-   **Nunca**: O Configuration Manager não suspende o BitLocker após a instalação de software que requeira um reinício. Neste cenário, a instalação de software não ficará concluída enquanto o utilizador não introduzir o PIN para concluir o processo de arranque padrão e carregar o Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>O software adicional gere a implementação de aplicações e atualizações de software

Ative esta opção apenas se um dos seguintes condições se aplicar:  

-   Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

-   Utilizar o Configuration Manager software development kit (SDK) para gerir as notificações de agente do cliente e a instalação de aplicações e atualizações de software.  

> [!WARNING]  
>  Se escolher esta opção quando nenhuma destas condições aplicam-se, o cliente não instala atualizações de software e as aplicações necessárias. Esta definição não impede que os utilizadores instalar aplicações a partir do catálogo de aplicações ou a instalação de sequências de tarefas, pacotes e programas.  

### <a name="powershell-execution-policy"></a>Política de execução do PowerShell

Configure a forma como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Pode utilizar estes scripts para a deteção de itens de configuração para definições de compatibilidade. Também pode enviar os scripts numa implementação como um script padrão.  

-   **Ignorar**: O cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente, para que possam ser executados scripts não assinados.  

-   **Restrito**: O cliente do Configuration Manager utiliza a configuração atual do PowerShell no computador cliente. Esta configuração determina se podem executar scripts não assinados.  

-   **Todas assinadas**: O cliente do Configuration Manager apenas executa scripts um fabricante fidedigno assinou-los. Esta restrição aplica-se independentemente da configuração atual do PowerShell no computador cliente.  

Esta opção necessita, pelo menos, o Windows PowerShell versão 2.0. A predefinição é **todas assinadas**.  

> [!TIP]  
>  Se os scripts não assinados falham para executar devido a esta definição de cliente, o Configuration Manager apresenta este erro das seguintes formas:  
>   
> -   O **monitorização** área de trabalho na consola apresenta o ID de erro de estado de implementação **0x87D00327**. Também apresenta a descrição **Script não está assinado**.  
> -   Os relatórios apresentam o tipo de erro **erro de deteção**. Em seguida, apresentam o código de erro **0x87D00327** e a descrição **Script não está assinado**, ou um código de erro **0x87D00320** e a descrição **o anfitrião do script ainda não foi instalado**. É um relatório de exemplo: **Detalhes de erros de itens de configuração numa linha de base de configuração para um recurso**.  
> -   O **DcmWmiProvider.log** ficheiro apresenta a mensagem **Script não está assinado (erro: 87D00327; Source: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Mostrar notificações para novas implementações

Escolha **Sim** para apresentar uma notificação para as implementações disponíveis para menos de uma semana. Esta mensagem é apresentada sempre que o agente do cliente é iniciado.

### <a name="disable-deadline-randomization"></a>Desativar a aleatoriedade de prazos

Após o prazo de implementação, esta definição determina se o cliente utiliza um atraso de ativação de até duas horas para instalar atualizações de software necessárias. Por predefinição, o atraso de ativação está desativado.  

Para cenários com infraestrutura de ambiente de trabalho virtual (VDI), este atraso ajuda a distribuir o processamento de CPU e a transferência de dados para uma máquina anfitriã com várias máquinas virtuais. Mesmo que não utilize VDI, muitos clientes a instalar as mesmas atualizações ao mesmo tempo podem negativamente aumentar a utilização da CPU no servidor do site. Este comportamento pode também mais lentos pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

Se os clientes tem de instalar atualizações de software necessárias no prazo de implementação sem atrasos, em seguida, configure esta definição para **Sim**. 

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Período de tolerância para aplicação após o prazo de implementação (horas)

Se quiser conceder aos utilizadores mais tempo a instalar a aplicação necessária ou implementações de atualização de software para além do prazo, defina esta opção para **Sim**. Este período de tolerância é de um computador desativado para um período de tempo alargado e o utilizador tem de instalar várias aplicações ou implementações de atualizações. Por exemplo, esta definição é útil se um utilizador devolvido a partir das férias e, tem de aguardar durante muito tempo, enquanto o cliente instala as implementações de aplicações em atraso. 

Defina um período de tolerância de 1 a 120 horas. Utilize esta definição juntamente com a propriedade de implementação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador**. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).


##  <a name="computer-restart"></a>Reinício do computador  
As seguintes definições tem de ser mais curtas duração a janela de manutenção mais curta aplicada ao computador.  

-   **Apresentar uma notificação temporária ao utilizador que indica o intervalo antes do utilizador sessão é terminada ou do computador reinicia (minutos)**
-   **Apresentar uma caixa de diálogo que o utilizador não é possível fechar, que apresenta o intervalo em contagem decrescente antes do utilizador sessão é terminada ou o computador reinicia (minutos)**

Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).

##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Além das informações seguintes, pode obter detalhes sobre como utilizar as definições de cliente do Endpoint Protection no [cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gerir o cliente do Endpoint Protection nos computadores cliente

Escolha **Sim** se pretender gerir os clientes existentes do Endpoint Protection e o Windows Defender em computadores na sua hierarquia.  

Escolha esta opção se já tiver instalado o cliente do Endpoint Protection e pretender geri-lo com o Configuration Manager. Esta instalação separada inclui um processo com script que utiliza uma aplicação do Configuration Manager ou o pacote e programa.

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalar o cliente do Endpoint Protection nos computadores cliente

Escolha **Sim** para instalar e ativar o cliente do Endpoint Protection nos computadores cliente que não executem o cliente.  

> [!NOTE]  
>  Se o cliente do Endpoint Protection já estiver instalado, escolher **não** não desinstala o cliente do Endpoint Protection. Para desinstalar o cliente do Endpoint Protection, configure o **cliente gerir o Endpoint Protection nos computadores cliente** definição de cliente para **não**. Em seguida, implemente um pacote e programa para desinstalar o cliente do Endpoint Protection.  

### <a name="automatically-remove-previously-installed-antimalware-software-before-endpoint-protection-is-installed"></a>Remover automaticamente software antimalware anteriormente instalado antes da instalação do Endpoint Protection

Defina esta opção para **Sim** para o cliente do Endpoint Protection tentar desinstalar outras aplicações de antimalware. Vários clientes antimalware no mesmo dispositivo podem entrar em conflito e o impacto no desempenho do sistema.

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Permite ao cliente do Endpoint Protection para instalação e reinicia fora das janelas de manutenção. Janelas de manutenção tem de ser, pelo menos, 30 minutos longa para a instalação do cliente

Defina esta opção para **Sim** para substituir os comportamentos de instalação típicas com janelas de manutenção. Esta definição cumpre os requisitos de negócio para a prioridade de manutenção do sistema para fins de segurança. 

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Para dispositivos Windows Embedded com filtros de escrita, consolide a instalação de cliente do Endpoint Protection (requer reinicialização)

Escolha **Sim** para desativar o filtro de escrita no dispositivo Windows Embedded e reiniciar o dispositivo. Esta ação consolida a instalação no dispositivo.  

Se optar por **não**, o cliente será instalado numa sobreposição temporária que limpa quando o dispositivo for reiniciado. Neste cenário, o cliente do Endpoint Protection não ficar totalmente instalados enquanto outra instalação consolida as alterações no dispositivo. Esta configuração é a predefinição.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Suprimir quaisquer reinícios necessários após o cliente do Endpoint Protection está instalado

Escolha **Sim** para suprimir um reinício do computador após a instalação de cliente do Endpoint Protection.  

> [!IMPORTANT]  
>  Se o cliente do Endpoint Protection requer um reinício do computador e esta definição **não**, em seguida, o computador seja reiniciado independentemente de quaisquer janelas de manutenção configuradas.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Permitido período de tempo que os utilizadores pode adiar um reinício necessário para concluir a instalação do Endpoint Protection (horas)

Se for necessário um reinício após a instalação de cliente do Endpoint Protection, esta definição especifica o número de horas que os utilizadores podem adiar o reinício necessário. Esta definição necessita que a definição de **suprimir reinícios de qualquer computador necessários após a instalação do cliente do Endpoint Protection** é **não**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Desativar origens alternativas (tais como Microsoft Windows Update, Microsoft Windows Server Update Services ou partilhas UNC) para a atualização inicial da definição nos computadores cliente

Escolha **Sim** se pretender que o Configuration Manager para instalar apenas a atualização inicial da definição nos computadores cliente. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda de rede, durante a instalação inicial da atualização da definição.  



##  <a name="enrollment"></a>Inscrição

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalo de consulta para clientes legados de dispositivos móveis
Selecione **intervalo definido** para especificar o período de tempo, em minutos ou horas, o que dispositivos móveis legados consultam de política. Estes dispositivos incluem plataformas, tais como o Windows CE, Mac OS X e Unix ou Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervalo de consulta para dispositivos modernos (minutos)
Introduza o número de minutos que consultam dispositivos modernos para a política. Esta definição é para dispositivos Windows 10 que são geridos através da gestão de dispositivos móveis no local.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Permitir que os utilizadores a inscrição de dispositivos móveis e computadores Mac
Para ativar a inscrição de utilizador com base dos dispositivos legados, defina esta opção para **Sim**e, em seguida, configure a definição seguinte:

-   **Perfil de inscrição** </br>
Selecione **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [configurar as definições de cliente para inscrição](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

### <a name="allow-users-to-enroll-modern-devices"></a>Permitir que os utilizadores inscreverem dispositivos modernos
Para ativar a inscrição de utilizador com base dos dispositivos modernos, defina esta opção para **Sim**e, em seguida, configure a definição seguinte:

-   **Perfil de inscrição de dispositivos modernos** </br>
Selecione **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventário de Hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Ativar inventário de hardware nos clientes

Por predefinição, esta definição é **Sim**. Para obter mais informações, consulte [introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

### <a name="hardware-inventory-schedule"></a>Agenda de inventário de hardware

Selecione **agenda** para ajustar a frequência com que os clientes a executar o inventário de hardware ciclo. Por predefinição, este ciclo ocorre a cada sete dias.

### <a name="maximum-random-delay-minutes"></a>Máximo de atraso aleatório (minutos)

Especifique o número máximo de minutos para que o cliente do Configuration Manager Utilize uma ordem aleatória do inventário de hardware ciclo da agenda definida. Este prazos em todos os clientes ajuda-o processamento de inventário de balanceamento de carga no servidor do site. Pode especificar qualquer valor entre 0 e 480 minutos. Por predefinição, este valor é definido como 240 minutos (4 horas).

### <a name="maximum-custom-mif-file-size-kb"></a>Máximo personalizado tamanho de ficheiro MIF (KB)

Especifica o tamanho máximo, em quilobytes (KB) permitido para cada ficheiro de formato MIF (Management Information Format) personalizado que o cliente recolhe durante um ciclo de inventário de hardware. O agente de inventário de hardware do Configuration Manager não processa ficheiros MIF personalizados que excedem este tamanho. Pode especificar um tamanho de 1 KB 5,120 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro de dados de inventário de hardware normal.  

> [!NOTE]  
>  Esta definição está disponível apenas nas predefinições do cliente.  

### <a name="hardware-inventory-classes"></a>Classes de inventário de hardware

Selecione **definir Classes** para expandir as informações de hardware recolhidas dos clientes sem necessitar de editar manualmente o ficheiro sms_def.mof. Para obter mais informações, consulte [como configurar inventário de hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Recolher ficheiros MIF

Utilize esta definição para especificar se pretende recolher ficheiros MIF de clientes do Configuration Manager durante o inventário de hardware.  

Para um ficheiro MIF possa ser recolhido pelo inventário de hardware, tem de ser no local correto no computador cliente. Por predefinição, os ficheiros estão localizados nos seguintes caminhos:  

-   **Ficheiros IDMIF** deve estar na pasta windows\system32\ccm\inventory\idmif. 

-   **Os ficheiros NOIDMIF** deve estar na pasta windows\system32\ccm\inventory\noidmif.

> [!NOTE]  
>  Esta definição está disponível apenas nas predefinições do cliente.

   

##  <a name="metered-internet-connections"></a>Ligações de internet com tráfego limitado  
 Gerir como Windows 8 e posteriores computadores utilizam ligações à internet com tráfego limitado para comunicar com o Configuration Manager. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à internet limitada.  

> [!NOTE]  
>  A definição de cliente configurado não é aplicado nos seguintes cenários:  
>   
> -   Se o computador estiver numa ligação de dados de roaming, o cliente do Configuration Manager efetua as tarefas que exigem a dados a serem transferidos para sites do Configuration Manager.  
> -   Se as propriedades de ligação de rede do Windows estão configuradas como não limitadas, o cliente do Configuration Manager funciona como se a ligação se tratasse e, por isso, transfere dados para o site.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicação com clientes em ligações à internet com tráfego limitado

Escolha uma das seguintes opções para esta definição:  

-   **Permitir**: Todas as comunicações de cliente são permitidas através da ligação de internet limitada, a menos que o dispositivo cliente está a utilizar uma ligação de dados de roaming.  

-   **Limit**: Apenas as seguintes comunicações de cliente serão permitidas através da ligação à internet com tráfego limitado:  

    -   Obtenção de políticas de cliente  

    -   Mensagens de estado de cliente a enviar para o site  

    -   Pedidos de instalação de software utilizando o Catálogo de Aplicações  

    -   Implementações necessárias (quando for atingido o prazo de instalação)  

    > [!IMPORTANT]  
    >  O cliente permite sempre instalações de software a partir do Centro de Software ou o catálogo de aplicações, independentemente da internet com tráfego limitado, as definições de ligação.  

    Se o cliente atingir o limite de transferência de dados para a ligação à internet com tráfego limitado, o cliente tenta já não está a comunicar com sites do Configuration Manager.  

-   **Block**: O cliente do Configuration Manager não tenta comunicar com sites do Configuration Manager quando estiver a utilizar uma ligação à internet com tráfego limitado. Esta é a opção predefinida.  



##  <a name="power-management"></a>Gestão de energia  

### <a name="allow-power-management-of-devices"></a>Permitir a gestão de energia dos dispositivos

Defina esta opção para **Sim** para ativar a gestão de energia nos clientes. Para obter mais informações, consulte [introdução à gestão de energia](/sccm/core/clients/manage/power/introduction-to-power-management).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia

Escolha **Sim** para permitir que os utilizadores do Centro de Software excluam os respetivos computadores a partir de qualquer definições de gestão de energia configuradas.  

### <a name="enable-wake-up-proxy"></a>Ativar o proxy de reativação

Especifique **Sim** para completar a definição de reativação por LAN do site, quando está configurado para pacotes unicast.  

Para obter mais informações sobre o proxy de reativação, consulte [planear como reativar os clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

> [!WARNING]  
>  Não ative a reativação proxy numa rede de produção sem compreender primeiro como funciona e avaliá-la num ambiente de teste.  

Em seguida, configure as seguintes definições adicionais, conforme necessário:

-   **Reativar o número da porta proxy (UDP)**  </br>
         O número de porta que os clientes utilizam para enviar pacotes de reativação para computadores de suspensão. Mantenha a porta predefinida 25536 ou altere o número para um valor à sua escolha.  

-   **Reativar por LAN o número da porta (UDP)** </br> 
         Mantenha o valor predefinido 9, exceto se tiver alterado o número de porta de reativação por LAN (UDP) no **portas** separador do site **propriedades**.  

    > [!IMPORTANT]  
    >  Este número tem de corresponder ao número nas **Propriedades**do site. Se alterar este número num único local, não é automaticamente atualizado no outro.  

-   **Exceção de Firewall do Windows Defender para proxy de reativação** </br>
         O cliente do Configuration Manager configura automaticamente o número de porta de proxy de reativação nos dispositivos que executam a Firewall do Windows Defender. Selecione **configurar** para especificar os perfis de firewall pretendido.

    Se os clientes executarem uma firewall diferente, tem de configurar manualmente para permitir a **número de porta de proxy de reativação (UDP)**.  
        
-   **Prefixos IPv6 se necessários para DirectAccess ou outros dispositivos de rede intervenientes. Utilize uma vírgula para separar várias entradas** </br>
        Introduza os prefixos IPv6 necessários para um proxy de reativação a funcionar na sua rede.



##  <a name="remote-tools"></a>Ferramentas remotas  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Ativar controlo remoto nos clientes e perfis de exceção de Firewall

Selecione **configurar** para ativar a funcionalidade de controlo remoto do Configuration Manager. Opcionalmente, configure as definições da firewall para permitir o controlo remoto funcione nos computadores cliente.  

Por predefinição, o controlo remoto encontra-se desativado.  

> [!IMPORTANT]  
>  Se as definições da firewall não estiverem configuradas, o controlo remoto poderá não funcionar corretamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software

Escolha se os utilizadores podem alterar as opções de controlo remoto no Centro de Software.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Permitir o controlo remoto de um computador autónomo

Escolha se um administrador pode utilizar o controlo remoto para aceder a um computador cliente que está a sessão terminada ou bloqueado. Apenas um computador com sessão iniciada e desbloqueado pode ser controlado remotamente quando esta definição estiver desativada.  

### <a name="prompt-user-for-remote-control-permission"></a>Pedir ao utilizador permissão do controlo remoto

Escolha se o computador cliente mostra uma mensagem solicitando a permissão de utilizador antes de permitir que uma sessão de controlo remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Pedir ao utilizador permissão transferir o conteúdo da área de transferência partilhada

Permitir que os utilizadores a oportunidade de aceitar ou recusar transferências de ficheiros, antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto. Os utilizadores só têm de conceder permissão, uma vez por sessão e o Visualizador não tem a capacidade de conceder si próprios permissão para continuar com a transferência de ficheiros.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Conceder permissão de controlo remoto ao grupo de administradores local

Escolha se a administradores locais no servidor que inicia a ligação de controlo remoto podem estabelecer sessões de controlo remoto nos computadores cliente.  

### <a name="access-level-allowed"></a>Nível de acesso permitido

Especifique o nível de acesso de controlo remoto para permitir. Escolha entre as seguintes definições:  
- **Sem acesso**
- **Ver apenas**
- **Controlo total**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Visualizadores de controlo remoto e assistência remota

Selecione **definir visualizadores** para especificar os nomes dos utilizadores Windows que poderão estabelecer sessões de controlo remoto para computadores cliente.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostrar ícone de notificação de sessão na barra de tarefas

Configure esta definição para **Sim** para mostrar um ícone na barra de tarefas para indicar uma sessão ativa de controlo remoto do cliente Windows.  

### <a name="show-session-connection-bar"></a>Mostrar barra de ligação de sessão

Defina esta opção para **Sim** para mostrar uma barra de ligação de sessão de alta visibilidade nos clientes, para indicar uma sessão ativa de controlo remoto.  

### <a name="play-a-sound-on-client"></a>Reproduzir um som no cliente

Defina esta opção para utilizar som para indicar quando uma sessão de controlo remoto está ativa num computador cliente. Selecione uma das seguintes opções:
- **Sem som**
- **Início e o envio de sessão** (predefinição)
- **Repetidamente durante a sessão**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gerir definições de assistência remota não solicitada

Configure esta definição para **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota não solicitadas.  

Numa sessão de assistência remota não solicitada, o utilizador do computador cliente não pediu a assistência para iniciar a sessão.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gerir definições da assistência remota solicitada

Defina esta opção para **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota solicitadas.  

Numa sessão de assistência remota solicitada, o utilizador do computador cliente enviou um pedido para o administrador para a assistência remota.  

### <a name="level-of-access-for-remote-assistance"></a>Nível de acesso para a assistência remota

Escolha o nível de acesso a atribuir às sessões de assistência remota que sejam iniciadas na consola do Configuration Manager. Selecione uma das seguintes opções:
- **Nenhum** (predefinição)
- **Visualização remota**
- **Controlo total**

> [!NOTE]  
>  O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

### <a name="manage-remote-desktop-settings"></a>Gerir definições de ambiente de trabalho remoto

Defina esta opção para **Sim** para permitir que o Configuration Manager gerir sessões de ambiente de trabalho remoto para computadores.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Permitir que os visualizadores autorizados estabeleçam ligação utilizando a ligação de ambiente de trabalho remoto

Defina esta opção para **Sim** para adicionar os utilizadores especificados na lista de visualizadores autorizados para o grupo de utilizadores local do ambiente de trabalho remoto nos clientes.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Exigir autenticação de nível de rede nos computadores que executam o sistema operativo Windows Vista e versões posteriores

Defina esta opção para **Sim** para utilizar a autenticação de nível de rede (NLA) para estabelecer ligações de ambiente de trabalho remoto para os computadores cliente. NLA requer inicialmente menos recursos do computador remoto, uma vez concluído a autenticação de utilizador antes de estabelecer uma ligação de ambiente de trabalho remoto. Utilizar NLA é uma configuração mais segura. NLA ajuda a proteger o computador contra utilizadores mal intencionados ou software e reduz o risco de ataques denial-of-service.  



## <a name="software-center"></a>Centro de software

### <a name="select-these-new-settings-to-specify-company-information"></a>Selecione estas novas definições para especificar as informações da empresa
Defina esta opção para **Sim**e, em seguida, especifique as seguintes definições para marca Centro de Software para a sua organização:

- **Nome da empresa** </br>
Introduza o nome da organização que os utilizadores visualizam no Centro de Software.
- **Esquema de cores para o Centro de Software** </br>
Selecione **selecione cor** para definir a cor primária utilizada pelo centro de Software.
- **Selecionar um logótipo no Centro de Software** </br>
Selecione **procurar** para selecionar uma imagem a apresentar no Centro de Software. O logótipo tem de ser um JPEG, PNG ou BMP de 400 x 100 pixéis, com um tamanho máximo de 750 KB. O nome de ficheiro de logótipo não deve conter espaços. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

### <a name="software-center-tab-visibility"></a>Visibilidade de separador de centro de software
Configurar as definições adicionais neste grupo para **Sim** para fazer com que os seguintes separadores visível no Centro de Software:
- **Aplicações**
- **Atualizações**
- **Sistemas operativos**
- **Estado da instalação**
- **Conformidade do dispositivo**
- **Opções**

Por exemplo, se a sua organização utilizar políticas de conformidade e, se pretender ocultar o separador de conformidade do dispositivo no Centro de Software, defina **separador de ativar a conformidade do dispositivo** para **não**.



## <a name="software-deployment"></a>Implementação de software  

### <a name="schedule-re-evaluation-for-deployments"></a>Agendar a reavaliação das implementações
Configure uma agenda para quando o Configuration Manager deverá reavaliar as regras de requisitos para todas as implementações. O valor predefinido é de sete em sete dias.  

> [!IMPORTANT]  
>  Recomendamos que altere este valor para um valor inferior à predefinição de. Uma agenda de reavaliação mais agressiva afeta negativamente o desempenho da sua rede e os computadores cliente.  

Iniciar esta ação de um cliente da seguinte forma: no **do Configuration Manager** painel, de controlo do **ações** separador, selecione **ciclo de avaliação de implementação de aplicação**.  



##  <a name="software-inventory"></a>Inventário de software  

### <a name="enable-software-inventory-on-clients"></a>Ativar inventário de software nos clientes

Isto está definido como **Sim** por predefinição. Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

### <a name="schedule-software-inventory-and-file-collection"></a>Agendar a recolha de ficheiros e de inventário de software

Selecione **agenda** para ajustar a frequência de que os clientes executam ciclos de recolha de ficheiros e inventário de software. Por predefinição, este ciclo ocorre a cada sete dias.

### <a name="inventory-reporting-detail"></a>Inventariar detalhe de relatórios

Especifique um dos seguintes níveis de informações de ficheiro ao inventário:
- **Apenas ficheiro**
- **Apenas o produto**
- **Total detalhes** (predefinição)

### <a name="inventory-these-file-types"></a>Inventariar estes tipos de ficheiro

Se pretender especificar os tipos de ficheiro a inventariar, selecione **definir tipos**e, em seguida, configure as seguintes opções:  

> [!NOTE]  
>  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que cada definição devolve intercalado.  

-   Selecione **novo** para adicionar um novo tipo de ficheiro ao inventário. Em seguida, especifique as seguintes informações no **propriedades do ficheiro inventariado** caixa de diálogo:  

    -   **Nome**: Forneça um nome para o ficheiro que pretende inventariar. Utilize um asterisco (**&#42;**) universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter. Por exemplo, se pretender inventariar todos os ficheiros com a extensão. doc, especifique o nome de ficheiro  **\*. doc**.  

    -   **Localização**: Selecione **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro especificado, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

    -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, todos os ficheiros comprimidos ou encriptados não são inventariados.  

    -   **Excluir ficheiros da pasta Windows**: Quando seleciona esta opção, os ficheiros na pasta Windows e respetivas subpastas não são inventariados.  

    Selecione **OK** para fechar o **propriedades do ficheiro inventariado** caixa de diálogo. Adicionar todos os ficheiros que pretende inventariar e, em seguida, selecione **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

### <a name="collect-files"></a>Recolher ficheiros

Se pretender recolher ficheiros de computadores cliente, selecione **definir ficheiros**e, em seguida, configure as seguintes definições:  

> [!NOTE]  
>  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que cada definição devolve intercalado.  

-   No **configurar definições do cliente** caixa de diálogo, selecione **novo** para adicionar um ficheiro a serem recolhidos.  

-   Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

    -   **Nome**: Forneça um nome para o ficheiro que pretende recolher. Utilize um asterisco (**&#42;**) universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter.  

    -   **Localização**: Selecione **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro que pretende recolher, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

    -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, todos os ficheiros comprimidos ou encriptados não são recolhidos.  

    -   **Parar a recolha de ficheiros quando o tamanho total dos ficheiros excede (KB)**: Especifique o tamanho do ficheiro, em quilobytes (KB) após o qual o cliente deixa de recolher os ficheiros especificados.  

    > [!NOTE]  
    >  Servidor do site recolhe as cinco versões mais recentes dos ficheiros recolhidos e armazena-os no  *&lt;diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol diretório. Se um ficheiro não foi alterada desde o último ciclo de inventário de software, o ficheiro não é recolhido novamente.  
    >   
    >  Inventário de software não recolher ficheiros com mais de 20 MB.  
    >   
    >  O valor **tamanho máximo para todos ficheiros recolhidos (KB)** no **configurar definições do cliente** caixa de diálogo mostra o tamanho máximo para todos ficheiros recolhidos. Quando este tamanho for atingido, interrompe a recolha de ficheiros. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

    > [!IMPORTANT]
    >  Se configurar o inventário de software para recolher muitos ficheiros grandes, esta configuração poderá afetar negativamente o desempenho do seu servidor de site e de rede.  

    Para obter informações sobre como visualizar ficheiros recolhidos, consulte [como utilizar o Explorador de recursos para ver o inventário de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Selecione **OK** para fechar o **propriedades do ficheiro recolhido** caixa de diálogo. Adicionar todos os ficheiros que pretende recolher e, em seguida, selecione **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

### <a name="set-names"></a>Definir nomes

O agente de inventário de software obtém nomes de produto e fabricante de informações de cabeçalho de ficheiro. Estes nomes não são normalizados sempre as informações de cabeçalho de ficheiro. Quando visualiza o inventário de software no Explorador de recursos, podem aparecer versões diferentes do mesmo fabricante ou o nome de produto. Padronizar estes nomes a apresentar, selecione **definir nomes**e, em seguida, configure as seguintes definições:  

-   **Nome do tipo**: Inventário de software recolhe informações sobre produtos e fabricantes. Escolha se pretende configurar os nomes a apresentar para um **fabricante** ou um **produto**.  

-   **Nome a apresentar**: Especifique o nome a apresentar que pretende utilizar em vez dos nomes de **nomes inventariados** lista. Para especificar um novo nome de apresentação, selecione **novo**.  

-   **Nomes inventariados**: Para adicionar um nome inventariado, selecione **novo**. Este nome é substituído no inventário de software pelo nome selecionado no **nome a apresentar** lista. Pode adicionar vários nomes a substituir.  



##  <a name="software-metering"></a>Medição de Software

### <a name="enable-software-metering-on-clients"></a>Ativar medição de software nos clientes
Esta definição está definida como **Sim** por predefinição. Para obter mais informações, consulte [medição de Software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

### <a name="schedule-data-collection"></a>Recolha de dados de agenda
Selecione **agenda** para ajustar a frequência de que os clientes executam o ciclo de medição de software. Por predefinição, este ciclo ocorre a cada sete dias.



##  <a name="software-updates"></a>Atualizações de software  

### <a name="enable-software-updates-on-clients"></a>Ativar atualizações de software nos clientes

Utilize esta definição para ativar atualizações de software nos clientes do Configuration Manager. Quando desativar esta definição, o Configuration Manager removerá as políticas de implementação existentes do cliente. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

> [!IMPORTANT]  
>  Ao desativar esta definição, as políticas de conformidade que dependem de atualizações de software deixarão de funcionar.  

### <a name="software-update-scan-schedule"></a>Agendamento da análise de atualização de software

Selecione **agenda** para especificar a frequência que o cliente inicia uma análise da avaliação de compatibilidade. Esta análise determina o estado das atualizações de software no cliente (por exemplo, é necessário ou instalado). Para obter mais informações sobre a avaliação de compatibilidade, consulte [avaliação de compatibilidade de atualizações de Software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Por predefinição, esta análise utiliza uma agenda simples para iniciar a cada sete dias. Pode criar uma agenda personalizada. Pode especificar um dia de início exatas e a hora, utilizar tempo Universal Coordenado (UTC) ou na hora local e configurar o intervalo periódico para um dia da semana específico.  

> [!NOTE]  
>  Se especificar um intervalo de menos de um dia, o Configuration Manager assume-se automaticamente como um dia.  

> [!WARNING]  
>  A hora de início real em computadores cliente é a hora de início mais um período de tempo aleatório, até duas horas. Este prazos impede que os computadores cliente de iniciar a análise e em simultâneo a ligar ao ponto de atualização de software ativo.  

### <a name="schedule-deployment-re-evaluation"></a>Agendar reavaliação de implementação

Selecione **agenda** para configurar a frequência a atualizações de software cliente agente deverá reavaliar as atualizações de software para o estado de instalação nos computadores de cliente do Configuration Manager. Quando as atualizações de software instaladas anteriormente já não se encontram nos clientes, mas são ainda necessárias, o cliente Reinstala as atualizações de software.

Ajustar esta agenda com base na política da empresa relativamente a compatibilidade de atualização de software, e se os utilizadores podem desinstalarem atualizações de software. Cada ciclo de reavaliação da implementação resulta na atividade de processador de computador cliente e rede. Por predefinição, esta definição utiliza uma agenda simples para iniciar a análise de reavaliação de implementação a cada sete dias.  

> [!NOTE]  
>  Se especificar um intervalo de menos de um dia, o Configuration Manager assume-se automaticamente como um dia.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Quando qualquer prazo de implementação de atualização de software é alcançado, instale todas as outras implementações de atualização de software com prazo a terminar no período de tempo especificado

Defina esta opção para **Sim** instalar todas as atualizações de software a partir de implementações necessárias com prazos ocorrer dentro de um período de tempo especificado. Quando uma implementação de atualização de software necessárias atinge um prazo, o cliente inicia a instalação para as atualizações de software na implementação. Esta definição determina se deve instalar as atualizações de software a partir de outras implementações necessárias com um prazo no período de tempo especificado.  

Utilize esta definição para agilizar a instalação de atualizações de software necessárias. Esta definição também tem o potencial de aumentar a segurança de cliente, diminuir notificações para o utilizador e diminuir a reinícios de cliente. Por predefinição, esta definição encontra-se definida como **Não**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas

Utilize esta definição para especificar o período de tempo da definição anterior. Pode introduzir um valor de 1 a 23 horas e, de 1 a 365 dias. Por predefinição, esta definição está configurada para 7 dias.  

### <a name="enable-installation-of-express-installation-files-on-clients"></a>Ativar a instalação dos ficheiros de instalação rápida nos clientes

Defina esta opção para **Sim** para permitir aos clientes utilizar ficheiros de instalação rápida. Para obter mais informações, consulte [ficheiros de instalação gerir Express para Windows 10 das atualizações](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="port-used-to-download-content-for-express-installation-files"></a>Porta utilizada para transferir conteúdo para os ficheiros de instalação rápida

Esta definição configura a porta local para o serviço de escuta HTTP transferir conteúdo rápido. Está definido para 8005 por predefinição. Não é necessário abrir esta porta na firewall do cliente.

### <a name="enable-management-of-the-office-365-client-agent"></a>Ativar a gestão do agente de cliente do Office 365

Quando definir esta opção para **Sim**, permite que a configuração das definições de instalação do Office 365. Também lhe permite transferir os ficheiros de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager. Para obter mais informações, consulte [gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Mensagens de estado

### <a name="state-message-reporting-cycle-minutes"></a>Mensagem de estado (minutos) de ciclo de comunicação
Especifica com que frequência os clientes reportam mensagens de estado. Esta definição é de 15 minutos por predefinição.



##  <a name="user-and-device-affinity"></a>Afinidade dispositivo / utilizador  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Limiar de utilização de afinidade de dispositivo de utilizador (minutos)
Especifique o número de minutos antes do Configuration Manager cria um mapeamento de afinidade de dispositivo do utilizador.  Por predefinição, este valor é 2880 minutos (2 dias).

### <a name="user-device-affinity-usage-threshold-days"></a>Limiar de utilização de afinidade de dispositivo do utilizador (dias)
Especifique o número de dias durante o qual o cliente mede o limiar de afinidade de dispositivo baseada na utilização.  Por predefinição, este valor é 30 dias.

> [!NOTE]  
>  Por exemplo, pode especificar **limiar de utilização de afinidade de dispositivo de utilizador (minutos)** como **60** minutos, e **limiar de utilização de afinidade de dispositivo do utilizador (dias)** como **5**  dias. Em seguida, o utilizador tem de utilizar o dispositivo durante 60 minutos num período de 5 dias para criar uma afinidade automática com o dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurar automaticamente a afinidade de dispositivo do utilizador a partir dos dados de utilização
Escolha **Sim** criar automática afinidade dispositivo / utilizador com base nas informações de utilização que recolhe do Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Permitir que o utilizador definir os seus dispositivos primários
Quando esta definição for **Sim**, os utilizadores podem identificar os seus dispositivos primários no Centro de Software.



## <a name="windows-analytics"></a>Windows Analytics

Para obter mais informações sobre estas definições, consulte [configurar clientes para dados de relatório para o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
