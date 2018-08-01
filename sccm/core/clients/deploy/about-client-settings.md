---
title: Definições do cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre o padrão e definições personalizadas para controlar os comportamentos de cliente
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38306efc9fbd7b38a5c5f0dad57fbd1a1b2c0557
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385410"
---
# <a name="about-client-settings-in-configuration-manager"></a>Acerca das definições de cliente no Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Gerir todas as definições de cliente na consola do Configuration Manager do **definições de cliente** nó a **administração** área de trabalho. O Configuration Manager é fornecido com um conjunto de configurações padrão. Quando alterar as predefinições de cliente, estas definições são aplicadas a todos os clientes na hierarquia. Também pode configurar definições de cliente personalizadas, que substituem as predefinições de cliente, quando atribui às coleções. Para obter mais informações, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).

As secções seguintes descrevem as definições e as opções mais detalhadamente.  
 

## <a name="background-intelligent-transfer-service-bits"></a>Serviço de transferência inteligente em segundo plano (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitar a largura de banda de rede máxima para transferências de plano de fundo de BITS
Quando esta opção está **Sim**, os clientes utilizam a limitação de largura de banda do BITS. Para configurar outras definições neste grupo, tem de ativar esta definição. 

### <a name="throttling-window-start-time"></a>Hora de início da janela de limitação
Especifique a hora de início local para a janela de limitação do BITS.  

### <a name="throttling-window-end-time"></a>Hora de fim da janela de limitação
Especifique a hora de fim de local para a janela de limitação do BITS. Se a hora de fim é igual para o **hora de início da janela de limitação**, limitação do BITS é sempre ativado.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Velocidade máxima de transferência durante a janela de limitação (Kbps)
Especifique a velocidade de transferência máxima que os clientes podem utilizar durante a janela.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Permitir transferências BITS fora da janela de limitação
Permitir que os clientes utilizar as definições de BITS separadas fora da janela especificada.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Velocidade máxima de transferência fora da janela de limitação (Kbps)
Especifique a velocidade de transferência máxima que os clientes podem utilizar fora do janela de limitação do BITS.  



## <a name="client-cache-settings"></a>Definições de cache do cliente

### <a name="configure-branchcache"></a>Configurar BranchCache
Configurar o computador cliente para [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir a colocação em cache de BranchCache no cliente, defina **ativar o BranchCache** ao **Sim**.

- **Ativar BranchCache** </br>
    Permite que o BranchCache nos computadores cliente.

- **Tamanho máximo da cache do BranchCache (percentagem do disco)** </br>
    A percentagem do disco que lhe permite BranchCache utilizar. 

### <a name="configure-client-cache-size"></a>Configurar o tamanho da cache do cliente
A cache do cliente do Configuration Manager em computadores Windows armazena ficheiros temporários, utilizados para instalar aplicações e programas. Se esta opção estiver definida como **não**, o tamanho predefinido é 5,120 MB.

Se escolher **Sim**, em seguida, especifique:
- **Tamanho máximo da cache (MB)**
- **Tamanho máximo da cache (percentagem do disco)** </br>
O tamanho da cache do cliente se expande para o tamanho máximo em megabytes (MB) ou a percentagem do disco, o que for menor. 

### <a name="enable-configuration-manager-client-in-full-os-to-share-content"></a>Ativar cliente do Configuration Manager em OS completo partilhem conteúdo
Permite [configurar o peering em cache](/sccm/core/plan-design/hierarchy/client-peer-cache) para clientes do Configuration Manager. Escolher **Sim**e, em seguida, especifique a porta através do qual o cliente comunica com o computador de ponto a ponto. 
- **Porta para difusão de rede inicial** (predefinida 8004)
- **Porta para transferência de conteúdo de elemento de rede** (8003 predefinida) </br>
O Configuration Manager configura automaticamente regras de Firewall do Windows para permitir que este tráfego. Se utilizar uma firewall diferente, tem de configurar manualmente as regras para permitir que este tráfego.




## <a name="client-policy"></a>Política de cliente  

### <a name="client-policy-polling-interval-minutes"></a>Intervalo de consulta da política de cliente (minutos)

Especifica a frequência com que os seguintes clientes do Configuration Manager transferirem a política de cliente:
-   Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  
-   Dispositivos móveis que inscreve do Configuration Manager  
-   Computadores Mac  
-   Computadores com o Linux ou UNIX  

### <a name="enable-user-policy-on-clients"></a>Ativar política de utilizador nos clientes

Quando define esta opção como **Sim**e utilize [deteção de utilizadores](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser), em seguida, os clientes recebem aplicações e programas direcionadas para o utilizador com sessão iniciada.  

O catálogo de aplicações recebe a lista do software disponível para utilizadores do servidor do site. Portanto, esta definição não tem de ser **Sim** para os utilizadores vejam e pedir aplicações a partir do catálogo de aplicações. Se esta definição estiver **não**, os seguintes comportamentos não funcionam quando os utilizadores utilizarem o catálogo de aplicações:  

-   Os utilizadores não é possível instalar as aplicações que visualizam no catálogo de aplicações.  

-   Os utilizadores não veem notificações sobre os pedidos de aprovação de aplicação. Em vez disso, devem atualizar o Catálogo de Aplicações e verificar o estado de aprovação.  

-   Os utilizadores não recebem revisões nem atualizações para as aplicações que são publicadas no catálogo de aplicações. Os utilizadores veem as alterações às informações de aplicação no catálogo de aplicações.  

-   Se remover uma implementação de aplicação depois do cliente instala a aplicação no catálogo de aplicações, os clientes continuam a verificar que a aplicação é instalada durante dois dias.  

Além disso, se esta definição é **não**, os utilizadores não recebem as aplicações necessárias implementadas para utilizadores. Os utilizadores também não receber quaisquer outras tarefas de gestão em políticas de utilizador.  

Esta definição aplica-se aos utilizadores cujos computadores estão na intranet ou na internet. Tem de ser **Sim** se também pretender ativar políticas de utilizador na internet.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Ativar pedidos da política de utilizador dos clientes internet

Defina esta opção como **Sim** para os utilizadores receberem a política de utilizador em computadores baseados na internet. Também se aplicam os seguintes requisitos:  

-   O cliente e o site estão configurados para [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management) ou uma [gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

-   O **ativar política de utilizador nos clientes** definição é **Sim**.  

-   O ponto de gestão baseado na internet autentica com êxito o utilizador ao utilizar a autenticação do Windows (Kerberos ou NTLM). Para obter mais informações, consulte [considerações sobre comunicações do cliente a partir da internet](/sccm/core/plan-design/hierarchy/communications-between-endpoints#BKMK_clientspan).  

-   A partir da versão 1710, o gateway de gestão na cloud com êxito autentica o utilizador com o Azure Active Directory. Para obter mais informações, consulte [implementar aplicações disponíveis para o utilizador em dispositivos associados ao AD Azure](\sccm\apps\deploy-use\deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

Se definir esta opção como **não**, ou qualquer um dos requisitos anteriores não forem cumpridas, em seguida, um computador com a internet apenas recebe políticas de computador. Neste cenário, os utilizadores ainda podem ver, pedir e instalar aplicações a partir de um catálogo de aplicações baseado na internet. Se esta definição estiver **não**, mas **ativar política de utilizador nos clientes** é **Sim**, os utilizadores não recebem políticas de utilizador, até que o computador estiver ligado à intranet.  

> [!NOTE]  
>  Para a gestão de clientes baseada na internet, pedidos de aprovação de aplicações dos utilizadores não precisam de políticas de utilizador ou a autenticação de utilizador. O gateway de gestão da nuvem não suporta pedidos de aprovação de aplicações.   



## <a name="cloud-services"></a>Serviços cloud

### <a name="allow-access-to-cloud-distribution-point"></a>Permitir o acesso ao ponto de distribuição da nuvem
Defina esta opção como **Sim** para os clientes obtenham conteúdo de um ponto de distribuição de nuvem. Esta definição não exige o dispositivo esteja baseado na internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registar automaticamente novos dispositivos associados a um domínio do Windows 10 com o Azure Active Directory 
Quando configurar o Azure Active Directory para suportar a associação ao híbrido, o Configuration Manager configura dispositivos do Windows 10 para essa funcionalidade. Para obter mais informações, consulte [como configurar híbrida do Azure Active Directory dispositivos associados ao](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Permitir que os clientes utilizar um gateway de gestão da cloud
Por predefinição, todos os clientes de roaming de internet utilizam qualquer disponíveis [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Um exemplo de quando configurar esta definição para **não** é para utilização do âmbito do serviço, tal como durante um projeto piloto ou para reduzir os custos.



##  <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="enable-compliance-evaluation-on-clients"></a>Ativar avaliação de compatibilidade nos clientes
Defina esta opção como **Sim** para configurar outras definições neste grupo.
 
### <a name="schedule-compliance-evaluation"></a>Agendar avaliação de compatibilidade
Selecione **agenda** para criar a agenda predefinida para a configuração de implementações de linha de base. Este valor pode ser configurado para cada linha de base a **implementar Baseline da configuração** caixa de diálogo.  

### <a name="enable-user-data-and-profiles"></a>Ativar perfis e dados de utilizador
Escolher **Sim** se pretender implementar [perfis e dados de utilizador](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items) itens de configuração.



## <a name="computer-agent"></a>Agente do computador  

### <a name="user-notifications-for-required-deployments"></a>Notificações do utilizador para as implementações necessárias

Para obter mais informações sobre as seguintes três definições, consulte [notificações do utilizador para as implementações necessárias](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):

-   **Prazo de implementação superior a 24 horas, lembrar o utilizador a cada (horas)**
-   **Menos de 24 horas de prazo de implementação, lembrar o utilizador a cada (horas)** 
-   **Menos de 1 hora de prazo de implementação, lembrar o utilizador a cada (minutos)** 

### <a name="default-application-catalog-website-point"></a>Ponto de Web sites Predefinido do Catálogo de Aplicações

O Configuration Manager utiliza esta definição para ligar utilizadores ao catálogo de aplicações do Centro de Software. Selecione **Web site do conjunto** para especificar um servidor que aloja o ponto de Web site do catálogo de aplicações. Introduza o nome NetBIOS ou FQDN, especificar deteção automática ou especificar um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor opção, porque oferece as seguintes vantagens:  

-   Se o site tiver um ponto de Web site do catálogo de aplicações, em seguida, os clientes recebem automaticamente um ponto de Web site do catálogo de aplicações do respetivo site.  

-   O cliente prefere pontos de Web sites do catálogo de aplicações ativadas por HTTPS na intranet aos servidores apenas de HTTP. Esta capacidade ajuda a proteger contra um servidor não autorizado.

-   O ponto de gestão fornece um ponto de Web sites do catálogo de aplicações baseado na internet de clientes baseados na internet. O ponto de gestão fornece um ponto de Web sites do catálogo de aplicações baseado na intranet de clientes baseados na intranet.  

A deteção automática não garante que os clientes recebem o mais próximo ponto de sites do catálogo de aplicações. Pode decidir não usar a opção para **detetar automaticamente** pelos seguintes motivos:  

-   Pretende configurar o servidor mais próximo para clientes manualmente ou certifique-se de que eles não ligam a um servidor através de uma ligação de rede lenta.  

-   Pretende controlar que clientes ligam ao servidor. Esta configuração pode ser para fins de teste, desempenho ou por razões empresariais.  

-   Não quiser esperar 25 horas ou para uma alteração de rede utilizar um site do catálogo de aplicações diferente, os clientes de ponto.  

Se Especifica o ponto de sites do catálogo de aplicações em vez de utiliza a deteção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Esta configuração reduz a probabilidade de que o browser solicita aos usuários as credenciais quando acede a um catálogo de aplicativos baseados na intranet. Para utilizar o nome NetBIOS, tem de aplicar as seguintes condições:  

-   O nome NetBIOS é especificado nas propriedades do ponto de Web sites do Catálogo de Aplicações.  

-   Utilizar o WINS ou todos os clientes estão no mesmo domínio que o ponto de sites do catálogo de aplicações.  

-   Configurar o ponto de Web site do catálogo de aplicações para ligações de cliente HTTP, ou configurar o servidor para HTTPS e o certificado de servidor web tem o nome de NetBIOS.  

Normalmente, aos utilizadores que introduzam credenciais quando o URL tem um FQDN, mas não quando o URL é um nome NetBIOS. Esperar que os usuários sempre ser pedido quando ligam a partir da internet, uma vez que esta ligação tem de utilizar o FQDN de internet. Para um cliente baseado na internet, quando o navegador da web solicita aos usuários as credenciais, certifique-se de que o ponto de sites do catálogo de aplicações pode ligar a um controlador de domínio para a conta de utilizador. Esta configuração permite ao utilizador autenticar através de Kerberos.  

> [!NOTE]  
>  Segue-se a deteção automática de como funciona:  
>   
>  O cliente faz um pedido de localização de serviço para um ponto de gestão. Se houver um ponto de Web sites do Catálogo de Aplicações no mesmo site que o cliente, este servidor é atribuído ao cliente como o servidor do Catálogo de Aplicações a utilizar. Quando mais do que um ponto de Web sites do catálogo de aplicações está disponível no site, um servidor ativado para HTTPS tem precedência sobre um servidor que não está ativado para HTTPS. Após esta filtragem, todos os clientes recebem um dos servidores para utilizar como o catálogo de aplicações. O Configuration Manager não balanceamento de carga entre vários servidores. Quando o site do cliente não tem um ponto de Web site do catálogo de aplicações, o ponto de gestão devolve não deterministicamente um ponto de Web site do catálogo de aplicações a partir da hierarquia.  
>   
>  Para clientes baseados na intranet, se configurar o ponto de sites do catálogo de aplicações com um nome de NetBIOS para o URL do catálogo de aplicações, o ponto de gestão utiliza-o. Ele não usa o FQDN da intranet. Para clientes baseados na internet, o ponto de gestão fornece apenas o FQDN de internet para o cliente.  
>   
>  O cliente efetua este pedido de localização de serviço a cada 25 horas ou sempre que detetar uma alteração de rede. Por exemplo, se o cliente passar da intranet à internet, que é uma alteração de rede. Se o cliente, em seguida, localiza um ponto de gestão baseado na internet, o ponto de gestão baseado na internet fornece servidores de ponto do Web site de catálogo de aplicações baseado na internet para clientes.  

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer

Se esta opção estiver **Sim**, o cliente adiciona automaticamente o atual URL de Web site do catálogo de aplicações predefinido para a zona de sites fidedignos do Internet Explorer.  

Esta definição garante que a definição do Internet Explorer para o modo protegido não está ativada. Se o modo protegido estiver ativado, o cliente do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. Por predefinição, a zona de sites fidedignos também suporta a sessão do utilizador para o catálogo de aplicações, que requer autenticação do Windows.  

Se deixar esta opção como **não**, clientes do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. É um método alternativo configurar estas definições do Internet Explorer noutra zona para o URL do catálogo de aplicações que os clientes utilizam.  

> [!NOTE]  
>  Sempre que o Configuration Manager adiciona um padrão de URL do catálogo de aplicações à zona de sites fidedignos, o Configuration Manager remove qualquer URL do catálogo de aplicações adicionado anteriormente.  
>   
>  Se o URL já foi especificado das zonas de segurança, o Configuration Manager não é possível adicionar o URL. Neste cenário, tem de remover o URL da outra zona ou configurar manualmente as definições do Internet Explorer necessárias.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada

Esta definição tem de ser **Sim** para os utilizadores utilizarem o catálogo de aplicações.  

Se alterar esta definição, entra em vigor quando os utilizadores em seguida respetivo browser ou Atualize sua janela do browser atualmente aberta.  

Para obter mais informações sobre esta definição, consulte [certificados do Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações](/sccm/apps/plan-design/security-and-privacy-for-application-management#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nome da organização apresentada no Centro de Software

Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna.  

### <a name="use-new-software-center"></a>Utilizar o novo Centro de Software

Se definir esta opção como **Sim**, em seguida, todos os computadores cliente utilizam o Centro de Software. Centro de software mostra aplicações disponíveis ao utilizador que anteriormente, eram acessíveis apenas no catálogo de aplicações. O catálogo de aplicações requer o Silverlight, que não é um pré-requisito para o Centro de Software. A partir do Configuration Manager 1802, a predefinição é **Sim**.  

Funções ainda são necessárias para as aplicações disponíveis ao utilizador sejam apresentadas no Centro de Software de sistema de sites do ponto do ponto de Web sites do catálogo de aplicações e o serviço web do catálogo de aplicações.  

Para obter mais informações, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

### <a name="enable-communication-with-health-attestation-service"></a>Ativar comunicação com o serviço de atestado de estado de funcionamento

Defina esta opção como **Sim** para dispositivos Windows 10 utilizar [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation). Quando ativa esta definição, a definição seguinte também está disponível para a configuração.

### <a name="use-on-premises-health-attestation-service"></a>Utilizar o serviço de atestado de estado de funcionamento no local

Defina esta opção como **Sim** para dispositivos utilizar um serviço no local. Defina como **não** para dispositivos a utilizar o serviço Microsoft baseado na nuvem.  

### <a name="install-permissions"></a>Permissões de instalação

> [!IMPORTANT]  
>  Esta definição aplica-se ao Catálogo de Aplicações e ao Centro de Software. Esta definição não tem efeito quando os utilizadores utilizarem o Portal da empresa.  

Configure a forma como os utilizadores podem iniciar a instalação de software, atualizações de software e sequências de tarefa:  

-   **Todos os utilizadores**: Utilizadores com qualquer permissão, exceto convidado.  

-   **Apenas os administradores**: Os utilizadores tem de ser membro do grupo Administradores local.  

-   **Apenas os administradores e utilizadores primários**: Os utilizadores tem de ser um membro do grupo local de administradores ou utilizadores primários do computador.  

-   **Não existem utilizadores**: Nenhum utilizador tiver sessão iniciada no computador cliente pode iniciar a instalação de software, atualizações de software e sequências de tarefas. As implementações necessárias para o computador instalar sempre na data limite. Os utilizadores não é possível iniciar a instalação de software a partir do catálogo de aplicações ou o Centro de Software.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Suspender a introdução do PIN do BitLocker no reinício

Se os computadores necessitam de introdução do PIN do BitLocker, em seguida, esta opção ignora o requisito de introduzir um PIN quando o computador é reiniciado após uma instalação de software.  

-   **Sempre**: O Configuration Manager suspende temporariamente o BitLocker após a instalação de software que requeira um reinício, iniciou um reinício do computador. Esta definição aplica-se apenas a um reinício do computador iniciado pelo Configuration Manager. Esta definição não suspende o requisito de introduzir o PIN do BitLocker quando o utilizador reinicia o computador. Retoma o requisito de introdução do PIN do BitLocker após o arranque do Windows.

-   **Nunca**: O Configuration Manager não suspender o BitLocker após a instalação de software que requeira um reinício. Neste cenário, a instalação de software não é possível concluir até que o utilizador não introduzir o PIN para concluir o processo de inicialização padrão e carregar o Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>O software adicional gere a implementação de aplicações e atualizações de software

Ative esta opção apenas se uma das seguintes condições se aplicar:  

-   Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

-   Utilize o Configuration Manager software development kit (SDK) para gerir as notificações de agente de cliente e a instalação de aplicações e atualizações de software.  

> [!WARNING]  
>  Se escolher esta opção quando nenhuma dessas condições aplicam-se, o cliente não instala atualizações de software e as aplicações necessárias. Esta definição não impede que os utilizadores de instalar aplicações a partir do catálogo de aplicações ou a instalação de pacotes, programas e sequências de tarefas.  

### <a name="powershell-execution-policy"></a>Política de execução do PowerShell

Configure como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Pode utilizar estes scripts para a deteção de itens de configuração para definições de compatibilidade. Também pode enviar os scripts numa implantação como um script padrão.  

-   **Ignorar**: O cliente do Configuration Manager ignora a configuração de Windows PowerShell no computador cliente, para que possam ser executados scripts não assinados.  

-   **Restrito**: O cliente do Configuration Manager utiliza a configuração atual do PowerShell no computador cliente. Esta configuração determina se possam ser executados scripts não assinados.  

-   **Todas assinadas**: O cliente do Configuration Manager apenas executa scripts que um fabricante fidedigno assinou-los. Esta restrição aplica-se independentemente da configuração atual do PowerShell no computador cliente.  

Esta opção necessita, pelo menos, Windows PowerShell versão 2.0. A predefinição é **todas assinadas**.  

> [!TIP]  
>  Se os scripts não assinados não conseguem ser executados devido a esta definição de cliente, o Configuration Manager comunicará este erro das seguintes formas:  
>   
> -   O **monitorização** área de trabalho na consola apresenta o ID de erro de estado de implementação **0x87D00327**. Ele também apresenta a descrição **Script não está assinado**.  
> -   Os relatórios apresentam o tipo de erro **erro de deteção**. Em seguida, os relatórios apresentam o código de erro **0x87D00327** e a descrição **Script não está assinado**, ou código de erro **0x87D00320** e a descrição **o anfitrião do script ainda não foi instalado**. Um relatório de exemplo é: **Detalhes de erros de itens de configuração numa linha de base de configuração para um recurso**.  
> -   O **Dcmwmiprovider** ficheiro apresenta a mensagem **Script não está assinado (erro: 87D00327; Origem: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Mostrar notificações para novas implementações

Escolher **Sim** para apresentar uma notificação para implementações disponíveis para menos de uma semana. Esta mensagem é exibida sempre que o agente do cliente for iniciado.

### <a name="disable-deadline-randomization"></a>Desativar a aleatoriedade de prazos

Após o prazo de implementação, esta definição determina se o cliente utiliza um atraso de ativação de até duas horas para instalar atualizações de software necessárias. Por predefinição, o atraso de ativação está desativado.  

Para cenários de infraestrutura de ambiente de trabalho virtual (VDI), este atraso ajuda a distribuir o processamento de CPU e transferência de dados para uma máquina de anfitrião com várias máquinas virtuais. Mesmo que não utilize VDI, muitos clientes, as mesmas atualizações ao mesmo tempo a instalar negativamente podem aumentar a utilização da CPU no servidor do site. Esse comportamento pode também reduzir a pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

Se os clientes tem de instalar atualizações de software necessárias no prazo de implementação sem demora, em seguida, configure esta definição para **Sim**. 

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Período de tolerância para aplicação após o prazo de implementação (horas)

Se pretender dar aos utilizadores mais tempo para instalar a aplicação necessária ou implementações de atualização de software para além do prazo, defina esta opção como **Sim**. Este período de tolerância é de um computador desativado para um período de tempo alargado e o utilizador tem de instalar várias aplicações ou implementações de atualizações. Por exemplo, esta definição é útil se um usuário devolve de férias e tem de esperar por um longo tempo, enquanto o cliente instala as implementações de aplicações em atraso. 

Defina um período de tolerância de 1 a 120 horas. Utilize esta definição juntamente com a propriedade de implementação **Trasar imposição para esta implementação, de acordo com as preferências do usuário**. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).


##  <a name="computer-restart"></a>Reinício do computador  
As seguintes definições tem de ser mais curtas duração que a janela de manutenção mais curta, aplicada ao computador.  

-   **Apresentar uma notificação temporária ao utilizador que indica o intervalo antes do utilizador é terminada ou o computador reinicia (minutos)**
-   **Exibir uma caixa de diálogo que o utilizador não é possível fechar, que apresenta o intervalo de contagem regressiva antes do utilizador é terminado ou o computador reinicia (minutos)**

Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](/sccm/core/clients/manage/collections/use-maintenance-windows).



## <a name="delivery-optimization"></a>Otimização da entrega

<!-- 1324696 --> Utilizar grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede empresarial e em escritórios remotos. [Otimização da entrega do Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é uma tecnologia baseada na cloud, o ponto-a-ponto para partilhar conteúdo entre os dispositivos Windows 10. A partir da versão 1802, configure a otimização de entrega a utilizar os grupos de limites, quando partilha de conteúdo entre elementos de rede.

 > [!Note]
 > Otimização da entrega só está disponível em clientes Windows 10

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Grupos de limites de utilize o Gestor de configuração para o ID do grupo de otimização de entrega
 Escolher **Sim** para aplicar o identificador de grupo de limites como o identificador de grupo de Otimização da entrega no cliente. Quando o cliente comunica com o serviço de cloud de otimização de entrega, ele usa esse identificador para localizar os colegas com os conteúdos pretendidos. 



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Além das informações seguintes, pode encontrar detalhes sobre como utilizar as definições de cliente do Endpoint Protection no [cenário de exemplo: Utilizar o Endpoint Protection para proteger os computadores contra software maligno](/sccm/protect/deploy-use/scenarios-endpoint-protection).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gerir o cliente do Endpoint Protection nos computadores cliente

Escolher **Sim** se pretender gerir clientes existentes do Endpoint Protection e o Windows Defender em computadores na sua hierarquia.  

Escolha esta opção se já tiver instalado o cliente do Endpoint Protection e geri-lo com o Configuration Manager. Esta instalação separada inclui um processo com script que utiliza uma aplicação do Configuration Manager ou o pacote e programa. Dispositivos Windows 10 a partir do Configuration Manager 1802, não precisam de ter instalado o agente de proteção de ponto final. No entanto, esses dispositivos ainda precisará **cliente gerir o Endpoint Protection nos computadores cliente** ativada. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalar o cliente do Endpoint Protection nos computadores cliente

Escolher **Sim** para instalar e ativar o cliente do Endpoint Protection nos computadores cliente que já não está a executar o cliente. Os clientes do Windows 10 a partir do Configuration Manager 1802, não precisam de ter instalado o agente de proteção de ponto final.  

> [!NOTE]  
>  Se o cliente do Endpoint Protection já estiver instalado, a escolha **não** não desinstalar o cliente do Endpoint Protection. Para desinstalar o cliente do Endpoint Protection, configure as **cliente gerir o Endpoint Protection nos computadores cliente** definição de cliente **não**. Em seguida, implemente um pacote e programa para desinstalar o cliente do Endpoint Protection.  

<!-- removed in 1806, SMS 511544
### Automatically remove previously installed antimalware software before Endpoint Protection is installed

Set this option to **Yes** for the Endpoint Protection client to attempt to uninstall other antimalware applications. Multiple antimalware clients on the same device can conflict, and impact system performance.
-->

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Permitir cliente do Endpoint Protection para instalação e reinicia fora das janelas de manutenção. Janelas de manutenção tem de ser, pelo menos, 30 minutos tempo para que a instalação do cliente

Defina esta opção como **Sim** para substituir os comportamentos de instalação típico com janelas de manutenção. Esta definição atende aos requisitos de negócios para a prioridade de manutenção do sistema por motivos de segurança. 

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Para dispositivos Windows Embedded com filtros de escrita, consolidar a instalação de cliente do Endpoint Protection (requer reinicialização)

Escolher **Sim** para desativar o filtro de escrita no dispositivo Windows Embedded e reiniciar o dispositivo. Esta ação compromete-se a instalação do dispositivo.  

Se escolher **não**, o cliente será instalado numa sobreposição temporária que limpe quando o dispositivo for reiniciado. Neste cenário, o cliente do Endpoint Protection totalmente não instala, enquanto as alterações outra instalação para o dispositivo. Esta configuração é a predefinição.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Suprimir os reinícios de computador necessários após a instalação do cliente do Endpoint Protection

Escolher **Sim** para suprimir um reinício do computador após a instalação de cliente do Endpoint Protection.  

> [!IMPORTANT]  
>  Se o cliente do Endpoint Protection requer um reinício do computador e esta definição é **não**, em seguida, o computador seja reiniciado independentemente de quaisquer janelas de manutenção configuradas.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Permitido no período de quando os utilizadores pode adiar um reinício necessário para concluir a instalação do Endpoint Protection (horas)

Se for necessário um reinício após a instalação de cliente do Endpoint Protection, esta definição especifica o número de horas que os utilizadores podem adiar o reinício necessário. Esta definição necessita que a definição para **suprimir reinícios de qualquer computador necessários após a instalação do cliente do Endpoint Protection** é **não**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Desativar origens alternativas (tais como o Microsoft Windows Update, Microsoft Windows Server Update Services ou partilhas UNC) para a atualização inicial das definições nos computadores cliente

Escolher **Sim** se pretender que o Configuration Manager para instalar apenas a atualização inicial das definições nos computadores cliente. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda de rede, durante a instalação inicial da atualização da definição.  



##  <a name="enrollment"></a>Inscrição

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalo de consulta para clientes legados de dispositivos móveis
Selecione **Definir intervalo** para especificar o período de tempo, em minutos ou horas, o que os dispositivos móveis legados consultar de política. Estes dispositivos incluem plataformas, como o Windows CE, Mac OS X e Unix ou Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervalo de consulta para dispositivos modernos (minutos)
Introduza o número de minutos que façam consultas de dispositivos modernos para a política. Esta definição destina-se a dispositivos Windows 10 que são geridos através da gestão de dispositivos móveis no local.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Permitir que os utilizadores a inscrição de dispositivos móveis e computadores Mac
Para ativar a inscrição de utilizador com base dos dispositivos legados, defina esta opção como **Sim**e, em seguida, configure a definição seguinte:

-   **Perfil de inscrição** </br>
Selecione **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [configurar as definições de cliente para inscrição](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

### <a name="allow-users-to-enroll-modern-devices"></a>Permitir aos utilizadores inscreverem dispositivos modernos
Para ativar baseada no utilizador a inscrição de dispositivos modernos, defina esta opção como **Sim**e, em seguida, configure a definição seguinte:

-   **Perfil de inscrição de dispositivos modernos** </br>
Selecione **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventário de Hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Ativar inventário de hardware nos clientes

Por predefinição, esta definição é **Sim**. Para obter mais informações, consulte [introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

### <a name="hardware-inventory-schedule"></a>Agenda de inventário de hardware

Selecione **agenda** para ajustar a frequência com que os clientes executem o inventário de hardware de ciclo. Por predefinição, este ciclo ocorre a cada sete dias.

### <a name="maximum-random-delay-minutes"></a>Atraso aleatório máximo (minutos)

Especifique o número máximo de minutos para que o cliente do Configuration Manager tornar o inventário de hardware ciclo a partir da agenda definida. Esta escolha aleatória entre todos os clientes ajuda o processamento de inventário de balanceamento de carga no servidor do site. Pode especificar qualquer valor entre 0 e 480 minutos. Por predefinição, este valor é definido como 240 minutos (4 horas).

### <a name="maximum-custom-mif-file-size-kb"></a>Máximo personalizado tamanho de ficheiro MIF (KB)

Especifique o tamanho máximo, em quilobytes (KB), permitido para cada ficheiro de formato MIF (Management Information Format) personalizado que o cliente recolhe durante um ciclo de inventário de hardware. O agente de inventário de hardware do Configuration Manager não processa ficheiros MIF personalizados que excederem este tamanho. Pode especificar um tamanho de 1 KB a 5,120 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro de dados de inventário de hardware normal.  

> [!NOTE]  
>  Esta definição está disponível apenas nas predefinições do cliente.  

### <a name="hardware-inventory-classes"></a>Classes de inventário de hardware

Selecione **definir Classes** para expandir as informações de hardware recolhidas dos clientes sem editar manualmente o ficheiro sms_def MOF. Para obter mais informações, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).  

### <a name="collect-mif-files"></a>Recolher ficheiros MIF

Utilize esta definição para especificar se pretende recolher ficheiros MIF de clientes do Configuration Manager durante o inventário de hardware.  

Para um ficheiro MIF possa ser recolhido pelo inventário de hardware, tem de ser no local correto no computador cliente. Por predefinição, os ficheiros estão localizados nos seguintes caminhos:  

-   **Ficheiros IDMIF** deve estar na pasta Windows\System32\CCM\Inventory\Idmif. 

-   **Ficheiros NOIDMIF** deve estar na pasta Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
>  Esta definição está disponível apenas nas predefinições do cliente.

   

##  <a name="metered-internet-connections"></a>Ligações de internet com tráfego limitado  
 Gerir como Windows 8 e posteriores computadores utilizam ligações à internet limitadas para se comunicar com o Configuration Manager. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa conexão de internet com tráfego limitado.  

> [!NOTE]  
>  A definição de cliente configurado não é aplicado nos seguintes cenários:  
>   
> -   Se o computador encontra-se com uma ligação de dados de roaming, o cliente do Configuration Manager não executa quaisquer tarefas que exigem dados a serem transferidos para sites do Configuration Manager.  
> -   Se as propriedades de ligação de rede do Windows estão configuradas como tráfego ilimitado, o cliente do Configuration Manager se comporta como se a ligação é não limitada e, então, transfere dados para o site.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicação com clientes em ligações de internet com tráfego limitado

Escolha uma das seguintes opções para esta definição:  

-   **Permitir**: Todas as comunicações de cliente são permitidas através da ligação de internet limitada, a menos que o dispositivo cliente está a utilizar uma ligação de dados de roaming.  

-   **Limite**: Apenas as seguintes comunicações de cliente serão permitidas através da ligação à internet com tráfego limitado:  

    -   Obtenção de políticas de cliente  

    -   Mensagens de estado de cliente a enviar para o site  

    -   Pedidos de instalação de software utilizando o Catálogo de Aplicações  

    -   Implementações necessárias (quando for atingido o prazo de instalação)  

    > [!IMPORTANT]  
    >  O cliente permite sempre instalações de software a partir do Centro de Software ou o catálogo de aplicações, independentemente da internet com tráfego limitado, as definições de ligação.  

    Se o cliente atinge o limite de transferência de dados para a ligação à internet com tráfego limitado, o cliente é já não tenta comunicar com sites do Configuration Manager.  

-   **Bloco**: O cliente do Configuration Manager não tenta comunicar com sites do Configuration Manager, quando se encontra com uma ligação à internet com tráfego limitado. Esta opção é a predefinição.  



##  <a name="power-management"></a>Gestão de energia  

### <a name="allow-power-management-of-devices"></a>Permitir gestão de energia de dispositivos

Defina esta opção como **Sim** para ativar a gestão de energia nos clientes. Para obter mais informações, consulte [introdução à gestão de energia](/sccm/core/clients/manage/power/introduction-to-power-management).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia

Escolher **Sim** para permitir que os utilizadores do Centro de Software excluam os respetivos computadores de quaisquer definições de gestão de energia configuradas.  

### <a name="enable-wake-up-proxy"></a>Ativar reativação proxy

Especifique **Sim** para completar a definição de reativação por LAN do site, quando é configurado para pacotes unicast.  

Para obter mais informações sobre o proxy de reativação, consulte [planear como reativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

> [!WARNING]  
>  Não ative o proxy de reativação numa rede de produção sem compreender primeiro como funciona e avaliá-lo num ambiente de teste.  

Em seguida, configure as seguintes definições adicionais conforme necessário:

-   **O número de porta de proxy de reativação (UDP)**: O número de porta que os clientes utilizam para enviar pacotes de reativação para computadores de suspensão. Mantenha a porta predefinida 25536 ou alterar o número para um valor à sua escolha.  

-   **O número de porta de reativação por LAN (UDP)**: Mantenha o valor predefinido 9, a menos que tenha alterado o número de porta de reativação por LAN (UDP) no **portas** separador do site **propriedades**.  

    > [!IMPORTANT]  
    >  Este número tem de corresponder ao número nas **Propriedades**do site. Se alterar este número desses lugares, não é automaticamente atualizado no outro.  

-   **Exceção de Firewall do Windows Defender para reativação proxy**: O cliente do Configuration Manager configura automaticamente o número de porta de proxy de reativação nos dispositivos que executam a Firewall do Windows Defender. Selecione **configurar** para especificar os perfis de firewall pretendido.

    Se os clientes executarem uma firewall diferente, configurá-lo manualmente para permitir que o **número de porta de proxy de reativação (UDP)**.  
        
-   **Prefixos do IPv6 se for necessário para o DirectAccess ou outros dispositivos de rede intervenientes. Utilize uma vírgula para especificar múltiplas entradas**: Introduza os prefixos IPv6 necessários para o proxy de reativação a funcionar na sua rede.



##  <a name="remote-tools"></a>Ferramentas remotas  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Ativar controlo remoto nos clientes e os perfis de exceção de Firewall

Selecione **configurar** para ativar a funcionalidade de controlo remoto do Configuration Manager. Opcionalmente, configure as definições da firewall para permitir o controlo remoto funcione nos computadores cliente.  

Por predefinição, o controlo remoto encontra-se desativado.  

> [!IMPORTANT]  
>  Se não configurar as definições da firewall, o controlo remoto poderá não funcionar corretamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software

Escolha se os utilizadores podem alterar as opções de controlo remoto no Centro de Software.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Permitir o controlo remoto de um computador autónomo

Escolha se um administrador pode utilizar o controlo remoto para aceder a um computador cliente que é terminado ou de bloqueado. Apenas um computador com sessão iniciada e desbloqueado pode ser controlado remotamente quando esta definição estiver desativada.  

### <a name="prompt-user-for-remote-control-permission"></a>Pedir ao utilizador permissão do controlo remoto

Escolha se o computador cliente mostra uma mensagem solicitando a permissão do usuário antes de permitir que uma sessão de controlo remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Pedir ao utilizador permissão de transferência de conteúdo da área de transferência partilhada

Antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto, permitir que os utilizadores a oportunidade de aceitar ou recusar as transferências de ficheiros. Os utilizadores apenas têm de conceder permissão, uma vez por sessão. O Visualizador não é possível atribuir a permissão para transferir o ficheiro.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Conceder permissão de controlo remoto ao grupo de administradores local

Escolha se a administradores locais no servidor que inicia a ligação de controlo remoto podem estabelecer sessões de controlo remoto a computadores cliente.  

### <a name="access-level-allowed"></a>Nível de acesso permitido

Especifique o nível de acesso de controlo remoto para permitir. Escolha entre as seguintes definições:  
- **Sem acesso**
- **Visualizar apenas**
- **Controlo total**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Visualizadores autorizados do controlo remoto e assistência remota

Selecione **definir visualizadores** para especificar os nomes dos utilizadores do Windows que poderão estabelecer sessões de controlo remoto para computadores cliente.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostrar ícone de notificação de sessão na barra de tarefas

Configure esta definição para **Sim** para mostrar um ícone na barra de tarefas do Windows do cliente para indicar uma sessão de controlo remoto ativa.  

### <a name="show-session-connection-bar"></a>Mostrar barra de ligação de sessão

Defina esta opção como **Sim** para mostrar uma barra de ligação de sessão de alta visibilidade nos clientes, para indicar uma sessão de controlo remoto ativa.  

### <a name="play-a-sound-on-client"></a>Reproduzir um som no cliente

Defina esta opção para utilizar som para indicar quando a sessão de controlo remoto está ativa num computador cliente. Selecione uma das seguintes opções:
- **Sem som**
- **Início e no envio da sessão** (predefinição)
- **Repetidamente durante a sessão**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gerir definições de assistência remota não solicitada

Configure esta definição para **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota não solicitadas.  

Numa sessão de assistência remota não solicitada, o utilizador do computador cliente não pedir assistência para iniciar a sessão.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gerir definições da assistência remota solicitada

Defina esta opção como **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota solicitadas.  

Numa sessão de assistência remota solicitada, o utilizador do computador cliente enviou um pedido para o administrador de assistência remota.  

### <a name="level-of-access-for-remote-assistance"></a>Nível de acesso para a assistência remota

Escolha o nível de acesso para atribuir a sessões de assistência remota que sejam iniciadas na consola do Configuration Manager. Selecione uma das seguintes opções:
- **Nenhum** (predefinição)
- **Visualização remota**
- **Controlo total**

> [!NOTE]  
>  O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

### <a name="manage-remote-desktop-settings"></a>Gerir definições de ambiente de trabalho remoto

Defina esta opção como **Sim** para permitir que o Configuration Manager gerir sessões de ambiente de trabalho remoto para computadores.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Permitir que os visualizadores ligar utilizando a ligação de ambiente de trabalho remoto

Defina esta opção como **Sim** para adicionar os utilizadores especificados na lista de visualizadores autorizados para o grupo de usuários local do ambiente de trabalho remoto nos clientes.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Exigir autenticação de nível de rede nos computadores que executam o sistema operacional Windows Vista e versões posteriores

Defina esta opção como **Sim** para utilizar a autenticação de nível de rede (NLA) para estabelecer ligações de ambiente de trabalho remoto para computadores cliente. NLA inicialmente requer menos recursos do computador remoto, uma vez que terminar a autenticação de utilizador antes de estabelecer uma ligação de ambiente de trabalho remoto. Usar o NLA é uma configuração mais segura. NLA ajuda a proteger o computador contra utilizadores mal intencionados ou software e reduz o risco de ataques denial-of-service.  



## <a name="software-center"></a>Centro de software

### <a name="select-these-new-settings-to-specify-company-information"></a>Selecione estas definições para especificar as informações da empresa
Defina esta opção como **Sim**e, em seguida, especifique as seguintes definições para a marca Centro de Software para a sua organização:

- **Nome da empresa**: Introduza o nome da organização que os utilizadores veem no Centro de Software.  

- **Esquema de cores para o Centro de Software**: Clique em **selecionar cor** para definir a cor primária utilizada pelo centro de Software.  

- **Selecionar um logótipo para o Centro de Software**: Clique em **procurar** para selecionar uma imagem a aparecer no Centro de Software. O logótipo tem de ser um JPEG, PNG ou BMP de 400 x 100 pixéis, com um tamanho máximo de 750 KB. O nome de ficheiro do logótipo não deve conter espaços.  
         
### <a name="bkmk_HideUnapproved"></a> Ocultar aplicações não aprovadas no Centro de Software
A partir do Configuration Manager versão 1802, quando ativa esta opção, as aplicações disponíveis ao utilizador que exigem a aprovação estão ocultos no Centro de Software.   <!--1355146-->

### <a name="bkmk_HideInstalled"></a> Ocultar aplicações instaladas no Centro de Software
A partir do Configuration Manager versão 1802, quando ativa esta opção, os aplicativos que já estejam instalados já não mostram no separador aplicações. Esta opção estiver definida como predefinição ao instalar ou atualizar para o Configuration Manager 1802. Aplicações instaladas ainda estão disponíveis para revisão no separador de estado de instalação. <!--1357592-->   
 
### <a name="bkmk_HideAppCat"></a> Ocultar a hiperligação de catálogo de aplicações no Centro de Software
A partir do Configuration Manager versão 1806, pode especificar a visibilidade da ligação de site da web do catálogo de aplicações no Centro de Software. Quando esta opção estiver definida, os utilizadores não verão a ligação de site da web do catálogo de aplicações no nó de estado de instalação do Centro de Software. <!--1358214-->


### <a name="software-center-tab-visibility"></a>Visibilidade de separador do Centro de software
Configurar as definições adicionais neste grupo para **Sim** para fazer com que os seguintes separadores visível no Centro de Software:
- **Aplicações**
- **Atualizações**
- **Sistemas operativos**
- **Estado da instalação**
- **Conformidade do dispositivo**
- **Opções**
- **Especifique um separador personalizado para o Centro de Software** (a partir da versão 1806) <!--1358132-->
    - **Nome do separador**
    - **URL de conteúdo**

>[!NOTE]
> Algumas funcionalidades do Web site poderão não funcionar quando utilizá-lo como uma guia personalizada no Centro de Software. Lembre-se de que os resultados de teste antes de implementar isso para os clientes. <!--519659-->

Por exemplo, se sua organização não utiliza políticas de conformidade e de que pretende ocultar o separador de conformidade do dispositivo no Centro de Software, defina **separador de ativar a conformidade do dispositivo** ao **não**.



## <a name="software-deployment"></a>Implementação de software  

### <a name="schedule-re-evaluation-for-deployments"></a>Agendar reavaliação para implementações
Configure um agendamento para quando o Configuration Manager revê as regras de requisitos para todas as implementações. O valor predefinido é a cada sete dias.  

> [!IMPORTANT]  
>  Não altere este valor para um valor inferior a predefinição. Um agendamento de reavaliação da mais agressivo pode afetar negativamente o desempenho da sua rede e dos computadores cliente.  

Iniciar esta ação de um cliente da seguinte forma: no **do Configuration Manager** controlar o painel, a partir do **ações** separador, selecione **ciclo de avaliação de implementação de aplicação**.  



##  <a name="software-inventory"></a>Inventário de software  

### <a name="enable-software-inventory-on-clients"></a>Ativar inventário de software nos clientes

Esta opção estiver definida como **Sim** por predefinição. Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

### <a name="schedule-software-inventory-and-file-collection"></a>Agendar a recolha de ficheiros e inventário de software

Selecione **agenda** para ajustar a frequência que os clientes executam ciclos de coleção de ficheiros e inventário de software. Por predefinição, este ciclo ocorre a cada sete dias.

### <a name="inventory-reporting-detail"></a>Inventariar detalhe de relatórios

Especifique um dos seguintes níveis de informações de ficheiro ao inventário:
- **Apenas ficheiro**
- **Apenas produto**
- **Ver os detalhes completos** (predefinição)

### <a name="inventory-these-file-types"></a>Inventariar estes tipos de ficheiro

Se pretender especificar os tipos de ficheiro a inventariar, selecione **definir tipos**e, em seguida, configure as seguintes opções:  

> [!NOTE]  
>  Se várias definições personalizadas de cliente são aplicadas a um computador, o inventário que retorna cada definição é mesclado.  

-   Selecione **New** para adicionar um novo tipo de ficheiro ao inventário. Em seguida, especifique as seguintes informações na **propriedades do ficheiro inventariado** caixa de diálogo:  

    -   **Nome**: Forneça um nome para o ficheiro que pretende inventariar. Utilizar um asterisco (**&#42;**) caráter universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter. Por exemplo, se pretender inventariar todos os ficheiros com a extensão. doc, especifique o nome de ficheiro  **\*. doc**.  

    -   **Localização**: Selecione **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para todos os discos rígidos de cliente para o ficheiro especificado de pesquisa, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

    -   **Excluir ficheiros comprimidos e encriptados**: Ao escolher esta opção, os ficheiros comprimidos ou encriptados não são inventariados.  

    -   **Excluir ficheiros na pasta Windows**: Ao escolher esta opção, os ficheiros na pasta Windows e respetivas subpastas não são inventariados.  

    Selecione **OK** para fechar a **propriedades do ficheiro inventariado** caixa de diálogo. Adicionar todos os ficheiros que pretende inventariar e, em seguida, selecione **OK** para fechar a **configurar definições do cliente** caixa de diálogo.  

### <a name="collect-files"></a>Recolher ficheiros

Se pretender recolher ficheiros de computadores cliente, selecione **definir ficheiros**e, em seguida, configure as seguintes definições:  

> [!NOTE]  
>  Se várias definições personalizadas de cliente são aplicadas a um computador, o inventário que retorna cada definição é mesclado.  

-   Na **configurar definições do cliente** caixa de diálogo, selecione **New** para adicionar um ficheiro a recolher.  

-   Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

    -   **Nome**: Forneça um nome para o ficheiro que pretende recolher. Utilizar um asterisco (**&#42;**) caráter universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter.  

    -   **Localização**: Selecione **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para procurar todos os discos rígidos de cliente para o ficheiro que pretende recolher, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

    -   **Excluir ficheiros comprimidos e encriptados**: Ao escolher esta opção, todos os ficheiros comprimidos ou encriptados não são recolhidos.  

    -   **Parar a recolha de ficheiros quando o tamanho total dos ficheiros exceder (KB)**: Especifique o tamanho do ficheiro, em quilobytes (KB), após o qual o cliente deixa de recolher os ficheiros especificados.  

    > [!NOTE]  
    >  O servidor do site recolhe as cinco versões mais recentes dos ficheiros recolhidos e armazena-os no `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` diretório. Se um ficheiro não mudou desde o último ciclo de inventário de software, o ficheiro não é recolhido novamente.  
    >   
    >  Inventário de software não recolhe ficheiros maiores do que 20 MB.  
    >   
    >  O valor **tamanho máximo para todos ficheiros recolhidos (KB)** no **configurar definições do cliente** caixa de diálogo mostra o tamanho máximo para todos ficheiros recolhidos. Quando este tamanho for atingido, deixa de recolha de ficheiros. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

    > [!IMPORTANT]
    >  Se configurar o inventário de software para recolher muitos ficheiros grandes, esta configuração poderá afetar negativamente o desempenho do seu servidor de rede e o site.  

    Para obter informações sobre como ver ficheiros recolhidos, consulte [como utilizar o Explorador de recursos para ver o inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

    Selecione **OK** para fechar a **propriedades do ficheiro recolhido** caixa de diálogo. Adicionar todos os ficheiros que pretende recolher e, em seguida, selecione **OK** para fechar a **configurar definições do cliente** caixa de diálogo.  

### <a name="set-names"></a>Definir nomes

O agente de inventário de software obtém o fabricante e nomes de produtos de informações de cabeçalho do ficheiro. Esses nomes sempre não são padronizados nas informações de cabeçalho de ficheiro. Ao visualizar o inventário de software no Explorador de recursos, podem aparecer diferentes versões do mesmo fabricante ou o nome do produto. Para padronizar estes nomes a apresentar, selecione **definir nomes**e, em seguida, configure as seguintes definições:  

-   **Tipo de nome**: Inventário de software recolhe informações sobre produtos e fabricantes. Escolha se pretende configurar nomes a apresentar para um **fabricante** ou uma **produto**.  

-   **Nome a apresentar**: Especifique o nome a apresentar que pretende utilizar em vez dos nomes na **nomes inventariados** lista. Para especificar um novo nome a apresentar, selecione **New**.  

-   **Nomes inventariados**: Para adicionar um nome inventariado, selecione **New**. Este nome é substituído no inventário de software pelo nome selecionado na **nome a apresentar** lista. Pode adicionar vários nomes a substituir.  



##  <a name="software-metering"></a>Medição de Software

### <a name="enable-software-metering-on-clients"></a>Ativar a medição de software nos clientes
Esta definição está definida como **Sim** por predefinição. Para obter mais informações, consulte [medição de Software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

### <a name="schedule-data-collection"></a>Agendar recolha de dados
Selecione **agenda** para ajustar a frequência que os clientes executam o ciclo de medição de software. Por predefinição, este ciclo ocorre a cada sete dias.



##  <a name="software-updates"></a>Atualizações de software  

### <a name="enable-software-updates-on-clients"></a>Ativar atualizações de software nos clientes

Utilize esta definição para ativar atualizações de software nos clientes do Configuration Manager. Quando desativar esta definição, o Configuration Manager remove as políticas de implementação existentes dos clientes. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

> [!IMPORTANT]  
>  Quando desativar esta definição, as políticas de conformidade que dependem de atualizações de software deixarão de funcionar.  

### <a name="software-update-scan-schedule"></a>Agendamento de análise de atualização de software

Selecione **agenda** para especificar a frequência com que o cliente inicia uma análise de avaliação de compatibilidade. Esta análise determina o estado das atualizações de software no cliente (por exemplo, necessário ou instalado). Para obter mais informações sobre a avaliação de conformidade, consulte [avaliação de compatibilidade de atualizações de Software](/sccm/sum/understand/software-updates-introduction#BKMK_SUMCompliance).  

Por predefinição, esta análise utiliza uma agenda simples para iniciar a cada sete dias. Pode criar uma agenda personalizada. Pode especificar um dia de início exatas e a hora, utilizar tempo Universal Coordenado (UTC) ou a hora local e configurar o intervalo periódico para um dia determinado da semana.  

> [!NOTE]  
>  Se especificar um intervalo de menos de um dia, o Configuration Manager automaticamente por predefinição, um dia.  

> [!WARNING]  
>  A hora de início real em computadores cliente é a hora de início mais um período de tempo, aleatório de até duas horas. Este aleatoriedade impede que computadores cliente iniciem a análise e em simultâneo a ligar ao ponto de atualização de software ativo.  

### <a name="schedule-deployment-re-evaluation"></a>Agendar reavaliação de implementação

Selecione **agenda** para configurar a frequência com que o agente de cliente de atualizações de software revê as atualizações de software para obter o estado de instalação nos computadores de cliente do Configuration Manager. Quando as atualizações de software instaladas anteriormente já não são encontradas nos clientes, mas são ainda necessárias, o cliente Reinstala as atualizações de software.

Ajustar esta agenda com base na política da empresa de conformidade de atualização de software, e se os utilizadores podem desinstalar as atualizações de software. Cada ciclo de reavaliação de implementação resulta numa atividade de processador de computador do cliente e de rede. Por predefinição, esta definição utiliza uma agenda simples para iniciar a verificação de reavaliação de implementação a cada sete dias.  

> [!NOTE]  
>  Se especificar um intervalo de menos de um dia, o Configuration Manager automaticamente por predefinição, um dia.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Quando qualquer prazo de implementação de atualização de software é alcançado, instale todas as outras implementações de atualização de software com prazo a terminar no período de tempo especificado

Defina esta opção como **Sim** para instalar todas as atualizações de software a partir de implementações necessárias com prazos ocorra de acordo com um período de tempo especificado. Quando uma implementação de atualização de software necessárias atinge um prazo, o cliente inicia a instalação das atualizações de software na implementação. Esta definição determina se deve instalar as atualizações de software a partir de outras implementações necessárias com um prazo dentro do tempo especificado.  

Utilize esta definição para acelerar a instalação de atualizações de software necessárias. Esta definição também tem o potencial de aumentar a segurança de cliente, diminuir notificações para o usuário e reduzir os reinícios de cliente. Por predefinição, esta definição encontra-se definida como **Não**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas

Utilize esta definição para especificar o período de tempo para a configuração anterior. Pode introduzir um valor de 1 a 23 horas e de 1 a 365 dias. Por predefinição, esta definição é configurada durante sete dias.  

### <a name="enable-installation-of-express-installation-files-on-clients"></a>Ativar a instalação de ficheiros de instalação rápida nos clientes

Defina esta opção como **Sim** para permitir aos clientes utilizar ficheiros de instalação rápida. Para obter mais informações, consulte [ficheiros de instalação de gerir Express para Windows 10 das atualizações](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates). 


### <a name="port-used-to-download-content-for-express-installation-files"></a>Porta utilizada para transferir conteúdo para ficheiros de instalação rápida

Esta definição configura a porta local para o serviço de escuta HTTP baixar conteúdo express. Ele é definido como 8005 por predefinição. Não precisa de abrir essa porta no firewall do cliente.

### <a name="enable-management-of-the-office-365-client-agent"></a>Ativar a gestão do agente de cliente do Office 365

Quando define esta opção como **Sim**, permite que a configuração das definições de instalação do Office 365. Ele também permite a transferir ficheiros a partir de redes de entrega de conteúdos (CDNs) do Office e implantar os arquivos como uma aplicação no Configuration Manager. Para obter mais informações, consulte [gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

### <a name="enable-third-party-software-updates"></a>Ativar as atualizações de software de terceiros 

Quando define esta opção como **Sim**, ele define a política para "Permitir com sessão iniciada atualizações para uma localização do serviço do Microsoft update de intranet" e instala o certificado de assinatura para o arquivo do Editor confiável no cliente. Esta definição de cliente foi adicionado no Configuration Manager versão 1802.



## <a name="state-messaging"></a>Mensagens de estado

### <a name="state-message-reporting-cycle-minutes"></a>Mensagem de estado (minutos) do ciclo de comunicação
Especifica a frequência com que os clientes reportam mensagens de estado. Esta definição é de 15 minutos por predefinição.



##  <a name="user-and-device-affinity"></a>Afinidade dispositivo / utilizador  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Limiar de utilização de afinidade de dispositivo de utilizador (minutos)
Especifique o número de minutos antes do Configuration Manager cria um mapeamento de afinidade de dispositivo do utilizador. Por predefinição, este valor é 2880 minutos (dois dias).

### <a name="user-device-affinity-usage-threshold-days"></a>Limiar de utilização de afinidade de dispositivo do utilizador (dias)
Especifique o número de dias durante o qual o cliente mede o limiar de afinidade de dispositivo com base na utilização. Por predefinição, este valor é de 30 dias.

> [!NOTE]  
>  Por exemplo, especificar **limiar de utilização de afinidade de dispositivo de utilizador (minutos)** como **60** minutos, e **limiar de utilização de afinidade de dispositivo do utilizador (dias)** como **5**  dias. Em seguida, o utilizador tem de utilizar o dispositivo durante 60 minutos num período de 5 dias para criar uma afinidade automática com o dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurar automaticamente a afinidade de dispositivo do utilizador a partir de dados de utilização
Escolher **Sim** criar automática afinidade dispositivo / utilizador com base nas informações de utilização que recolhe do Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Permitir ao utilizador a definição dos seus dispositivos primários
Quando esta definição for **Sim**, os usuários podem identificar os seus dispositivos primários no Centro de Software.



## <a name="windows-analytics"></a>Análise do Windows

Para obter mais informações sobre estas definições, consulte [configurar clientes para dados de relatório para o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
