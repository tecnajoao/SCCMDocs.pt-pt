---
title: "Definições do cliente"
titleSuffix: Configuration Manager
description: "Escolha as definições de cliente utilizando a consola de administrador no System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: fe6b3508b7d54dca1d80818c159cfd4b723f7986
ms.sourcegitcommit: f1535281b2c3fecff773b722c3f7590bf6ba10a0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/03/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as definições de cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Gerir todas as definições de cliente na consola do Configuration Manager do **as definições de cliente** no nó de **administração** área de trabalho. O Configuration Manager inclui um conjunto de predefinições. Quando alterar as predefinições de cliente, estas definições são aplicadas a todos os clientes na hierarquia. Também pode configurar as definições de cliente personalizadas, que substituem as predefinições de cliente quando atribua estas definições a coleções. Para obter mais informações, consulte [como configurar as definições de cliente](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Serviço de transferência inteligente em segundo plano  

-   **Limitar a largura de banda de rede máxima para transferências BITS em segundo plano**   </br>
   Quando esta opção é **Sim**, os clientes utilizam a limitação de largura de banda do BITS. Para configurar outras definições, este grupo, tem de ativar esta definição. 

-   **Hora de início da janela de limitação**   </br>
   Especifique a hora de início local para a janela de limitação do BITS.  

-   **Hora de fim da janela de limitação**   </br>
   Especifique a hora de fim local para a janela de limitação do BITS. Se igual a **hora de início da janela de limitação**, limitação do BITS é sempre ativado.  

-   **Velocidade máxima de transferência durante a janela de limitação (Kbps)** </br>
    Especifica a velocidade máxima de transferência que os clientes podem utilizar durante a janela.  

-   **Permitir transferências BITS fora da janela de limitação**   </br>
   Permitir aos clientes utilizar definições de BITS separadas fora da janela especificada.  

-   **Velocidade máxima de transferência fora da janela de limitação (Kbps)**   </br>
   Especifique a velocidade máxima de transferência que os clientes utilizam fora do janela de limitação do BITS.  



## <a name="client-cache-settings"></a>Definições de cache do cliente

- **Configurar o BranchCache** </br>
  Utilize esta definição para configurar o computador cliente para [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir a colocação em cache de BranchCache no cliente, defina **ativar BranchCache** para **Sim**.

    - **Ativar o BranchCache** </br>
    Permite que o BranchCache nos computadores cliente.

    - **Tamanho máximo da cache do BranchCache (percentagem do disco)** </br>
    A percentagem do disco que permitem o BranchCache utilizar. 

- **Configurar o tamanho da cache do cliente** </br>
  A cache do cliente do Configuration Manager em computadores Windows armazena ficheiros temporários utilizados para instalar aplicações e programas. Se esta opção é **não**, o tamanho predefinido é 5,120 MB.</br>
    Escolha **Sim**, em seguida, especifique:
    - **Tamanho máximo da cache (MB)**
    - **Tamanho máximo da cache (percentagem do disco)** </br>
    Expande o tamanho da cache do cliente para o tamanho máximo em megabytes (MB) ou a percentagem do disco, *que for menor*. 

- **Ativar cliente do Configuration Manager no SO completo para partilhar conteúdo** </br>
    Permite [elemento cache](/sccm/core/plan-design/hierarchy/client-peer-cache) para clientes do Configuration Manager. Escolha **Sim**, em seguida, especifique as informações de porta que o cliente comunica com o computador de ponto a ponto. 
    - **Porta para difusão de rede inicial** (predefinida 8004)
    - **Porta para transferência do conteúdo de elemento de rede** (8003 predefinida) </br>
    O Configuration Manager configura automaticamente regras de Firewall do Windows para permitir que este tráfego. Se utilizar uma firewall diferente, tem de configurar manualmente as regras para permitir que este tráfego.




## <a name="client-policy"></a>Política do cliente  

-   **Intervalo de consulta da política de cliente (minutos)**  </br>
     Especifica a frequência os seguintes clientes do Configuration Manager transferirem a política de cliente:  
      -   Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  
      -   Dispositivos móveis que inscreve do Configuration Manager  
      -   Computadores Mac  
      -   Computadores com o Linux ou UNIX  

-   **Ativar política de utilizador nos clientes**   </br>
   Quando definir esta opção **Sim**e utilizar [deteção de utilizadores](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), em seguida, os clientes recebem aplicações e programas direcionadas para o utilizador com sessão iniciada.  

    O catálogo de aplicações recebe a lista do software disponível para utilizadores do servidor do site. Deste modo, esta definição não tem de ser **Sim** para os utilizadores possam visualizar e pedir aplicações a partir do catálogo de aplicações. Se esta definição é **não**, seguintes comportamentos não funcionam quando os utilizadores utilizam o catálogo de aplicações:  

      -   Os utilizadores não podem instalar as aplicações que veem no Catálogo de Aplicações.  

      -   Os utilizadores veem notificações sobre os seus pedidos de aprovação de aplicações. Em vez disso, devem atualizar o Catálogo de Aplicações e verificar o estado de aprovação.  

      -   Os utilizadores não recebem revisões nem atualizações para as aplicações que são publicadas no catálogo de aplicações. Os utilizadores veem alterações às informações da aplicação no catálogo de aplicações.  

      -   Se remover uma implementação de aplicação depois do cliente instala a aplicação no catálogo de aplicações, os clientes continuam a verificar que a aplicação está instalada até dois dias.  

    Além disso, quando esta definição for **não**, os utilizadores não recebem as aplicações necessárias que implementar nos utilizadores. Os utilizadores também não receber quaisquer outras tarefas de gestão em políticas de utilizador.  

    Esta definição aplica-se aos utilizadores cujos computadores estão na intranet e Internet. Tem de ser **Sim** se também pretender ativar políticas de utilizador na Internet.  

-   **Ativar pedidos da política do utilizador dos clientes Internet**   </br>
   Configure esta definição para **Sim** para os utilizadores receberem a política de utilizador em computadores baseados na Internet. Também tem de aplicar os seguintes requisitos:  

      -   O cliente e o site estão configurados para gestão de clientes baseados na Internet

      -   O **ativar política de utilizador nos clientes** definição é **Sim**  

      -   O ponto de gestão baseado na Internet autentica com êxito o utilizador ao utilizar a autenticação do Windows (Kerberos ou NTLM)  

       Se definir esta opção como **não**, ou qualquer um dos requisitos anteriores não são cumpridos, em seguida, um computador com a Internet apenas recebe políticas de computador. Neste cenário, os utilizadores ainda podem ver, pedir e instalar aplicações a partir de um Catálogo de Aplicações baseado na Internet. Se esta definição é **não**, mas **ativar política de utilizador nos clientes** é **Sim**, os utilizadores não recebem políticas de utilizador, até que o computador está ligado à intranet.  

       Para obter mais informações sobre a gestão de clientes na Internet, consulte [considerações sobre comunicações do cliente da Internet ou numa floresta não fidedigna](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Os pedidos de aprovação de aplicações dos utilizadores não necessitam de políticas de utilizador ou de autenticação de utilizador.  


## <a name="cloud-services"></a>Serviços cloud

-   **Permitir o acesso ao ponto de distribuição de nuvem** </br>
    Configure esta definição para **Sim** para os clientes obter conteúdo de um ponto de distribuição na nuvem. Esta definição não requer que o dispositivo ser baseados na Internet.

-    **Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory** </br> Quando configurar o Azure Active Directory para suportar a associação de híbrida, em seguida, Configuration Manager configura os dispositivos Windows 10 para esta funcionalidade. Para obter mais informações, consulte [como para configurar híbrida do Azure Active Directory dispositivos associados a um](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Permitir que os clientes utilizar um gateway de gestão de nuvem** </br>
    Por predefinição, todos os clientes de roaming de Internet utilizam disponível qualquer [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Um exemplo de quando configurar esta definição para **não** é a utilização do âmbito do serviço, tal como durante um projeto piloto ou para reduzir os custos.



##  <a name="compliance-settings"></a>Definições de compatibilidade  

-   **Ativar a avaliação de compatibilidade nos clientes** </br>
    Configure esta definição para **Sim** para configurar outras definições deste grupo.
 
-   **Agendar avaliação de compatibilidade**   </br>
     Clique em **agenda** para criar a agenda predefinida para a configuração de implementações de linha de base. Este valor é configurável para cada linha de base a **implementar linhas de base de configuração** caixa de diálogo.  

-   **Ativar Dados e Perfis de Utilizador**   </br>
     Escolha **Sim** se pretender implementar [perfis e dados de utilizador](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) itens de configuração.



## <a name="computer-agent"></a>Agente do computador  
-   Notificações de utilizador para as implementações necessárias </br>
    Para mais informações sobre as seguintes três definições, consulte [notificações de utilizador para as implementações necessárias](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -   **Prazo de implementação superior a 24 horas, lembrar o utilizador a cada (horas)**
    -   **Implementação prazo inferior a 24 horas, lembrar o utilizador a cada (horas)**  </br>
    -   **Implementação prazo inferior a 1 hora, lembrar o utilizador a cada (minutos)**  </br>

-   **Ponto de Web sites Predefinido do Catálogo de Aplicações**   </br>
     O Configuration Manager utiliza esta definição para ligar utilizadores ao catálogo de aplicações a partir do Centro de Software. Clique em **conjunto site** para especificar um servidor que aloja o ponto de Web site do catálogo de aplicações. Introduza o nome NetBIOS ou FQDN, especificar deteção automática ou especificar um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor opção uma vez que oferece as seguintes vantagens:  

    -   Se o site tiver um ponto de Web site do catálogo de aplicações, em seguida, os clientes recebem automaticamente um ponto de Web site do catálogo de aplicações do respetivo site.  

    -   O cliente prefers pontos de Web site do catálogo de aplicações ativadas por HTTPS da intranet através de servidores apenas de HTTP. Esta capacidade ajuda a proteger contra um servidor não autorizado.

    -   O ponto de gestão proporciona um ponto de Web site do catálogo de aplicações baseado na Internet de clientes baseados na Internet. O ponto de gestão proporciona um ponto de Web site do catálogo de aplicações baseado na intranet de clientes baseados na intranet.  

     A deteção automática não garante que os clientes recebem o ponto de Web site do catálogo de aplicações mais próximo. Pode decidir não utilizar **Detetar automaticamente** pelos seguintes motivos:  

     -   Pretende configurar manualmente o servidor mais próximo dos clientes ou certificar-se de que não ligam a um servidor através de uma ligação de rede lenta.  

     -   Pretende controlar que clientes ligam ao servidor. Esta configuração pode ser para fins de teste, desempenho ou por razões empresariais.  

     -   Não pretende esperar até 25 horas ou para uma alteração de rede para os clientes utilizar um site do catálogo de aplicações diferentes ponto.  

     Se, especifique o ponto de Web site do catálogo de aplicações em vez de utiliza a deteção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Esta configuração reduz a probabilidade de que o browser pede-lhe que os utilizadores de credenciais quando acedem a um catálogo de aplicações baseado na intranet. Para utilizar o nome NetBIOS, tem de aplicar as seguintes condições:  

     -   O nome NetBIOS é especificado nas propriedades do ponto de Web sites do Catálogo de Aplicações.  

     -   Utilizar o WINS ou todos os clientes estão no mesmo domínio que o ponto de Web site do catálogo de aplicações.  

     -   Configurar o ponto de Web site do catálogo de aplicações para ligações de cliente HTTP ou configurar o servidor para HTTPS e o certificado de servidor web com o nome de NetBIOS.  

     Normalmente, os utilizadores recebem um pedido de credenciais quando o URL tem um FQDN mas não quando o URL é um nome NetBIOS. É expectável que os utilizadores recebam sempre esse pedido quando ligam a partir da Internet, uma vez que esta ligação tem de utilizar o FQDN da Internet. Quando utilizar um cliente baseado na Internet e o browser solicita aos utilizadores credenciais, certifique-se de que o ponto de Web site do catálogo de aplicações pode ligar a um controlador de domínio para a conta de utilizador. Esta configuração permite ao utilizador autenticar através de Kerberos.  

    > [!NOTE]  
    >  Como funciona a deteção automática:  
    >   
    >  O cliente faz um pedido de localização de serviço para um ponto de gestão. Se houver um ponto de Web sites do Catálogo de Aplicações no mesmo site que o cliente, este servidor é atribuído ao cliente como o servidor do Catálogo de Aplicações a utilizar. Quando estiver disponível mais do que um ponto de Web site do catálogo de aplicações no site, um servidor ativado para HTTPS tem precedência sobre um servidor que não está ativado para HTTPS. Após esta filtragem, todos os clientes recebem um dos servidores a utilizar como catálogo de aplicações; O Configuration Manager não não-balanceamento de carga entre múltiplos servidores. Quando o site do cliente não tem um ponto de Web site do catálogo de aplicações, o ponto de gestão devolve não deterministicamente um ponto de Web site do catálogo de aplicações da hierarquia.  
    >   
    >  Os clientes baseados na intranet, se configurar o ponto de Web site do catálogo de aplicações com um nome de NetBIOS para o URL do catálogo de aplicações, o ponto de gestão fornece clientes este nome de NetBIOS em vez do FQDN da intranet. Para clientes baseados na Internet, o ponto de gestão fornece apenas o FQDN de Internet ao cliente.  
    >   
    >  O cliente efetua este pedido de localização de serviço em 25 horas ou sempre que detetar uma alteração de rede. Por exemplo, se o cliente passa da intranet à Internet e o cliente localiza um ponto de gestão baseado na Internet, o ponto de gestão baseado na Internet dá-servidores de ponto de Web site do catálogo de aplicações baseado na Internet para clientes.  

-   **Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer**   </br>
     Se esta opção é **Sim**, o cliente adiciona automaticamente o atual URL de Web site do catálogo de aplicações predefinido a zona de sites fidedignos do Internet Explorer.  

     Esta definição garante que a definição do Internet Explorer para o Modo Protegido não está ativada. Se o modo protegido estiver ativado, o cliente do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. Por predefinição, a zona de sites fidedignos também suporta o início de sessão de utilizador para o Catálogo de Aplicações, que requer autenticação do Windows.  

     Se deixar esta opção como **não**, clientes do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. É um método alternativo configurar estas definições do Internet Explorer noutra zona para o URL do catálogo de aplicações que os clientes utilizam.  

    > [!NOTE]  
    >  Sempre que o Configuration Manager adiciona um catálogo de aplicações predefinido para a zona sites fidedignos, o Configuration Manager remove quaisquer anteriormente adicionados URL do catálogo de aplicações.  
    >   
    >  Se o URL já estiver especificado das zonas de segurança, o Configuration Manager não é possível adicionar o URL. Neste cenário, tem de remover o URL da outra zona ou configurar manualmente as definições do Internet Explorer necessárias.  

-   **Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada**   </br>
     Esta definição tem de ser **Sim** os utilizadores utilizarem o catálogo de aplicações.  

     Se alterar esta definição, ela tem efeito assim que os utilizadores carregarem o respetivo browser ou atualizarem a respetiva janela do browser atualmente aberta.  

     Para obter mais informações sobre esta definição, consulte [certificados do Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Nome da organização apresentada no Centro de Software**   </br>
     Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna.  

-   **Utilizar o novo Centro de Software**   </br>
     Se configurar esta definição de cliente para **Sim**, em seguida, todos os computadores cliente utilizam o novo Centro de Software. Centro de software mostra as aplicações disponíveis ao utilizador que foram anteriormente acessíveis apenas no catálogo de aplicações. O catálogo de aplicações requer o Silverlight, que não é um pré-requisito para o novo Centro de Software.   

     O ponto de Web site do catálogo de aplicações e serviço web do catálogo de aplicações do ponto de sistema de sites funções ainda são necessárias para aplicações disponíveis ao utilizador a aparecer no Centro de Software.  

     Para obter mais informações, consulte [planear e configurar a gestão de aplicações](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Ativar comunicação com o serviço de atestado de estado de funcionamento**  </br>
    Configure esta definição para **Sim** para dispositivos Windows 10 utilizar [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation). Quando ativa esta definição, a seguinte definição também está disponível para a configuração.

    -   **Utilizar o serviço de atestado de estado de funcionamento no local** </br>
        Configure esta definição para **Sim** nos dispositivos utilizar um serviço no local. Configure esta definição para **não** nos dispositivos utilizar o serviço de baseado na nuvem da Microsoft.  

-   **Permissões de Instalação**   </br>
    > [!WARNING]  
    >  Esta definição aplica-se ao Catálogo de Aplicações e ao Centro de Software. Esta definição não tem efeito quando os utilizadores utilizam o Portal da empresa.  

     Configure a forma como os utilizadores podem iniciar a instalação de software, atualizações de software e sequências de tarefa:  

    -   **Todos os utilizadores**: Utilizadores com qualquer permissão, exceto convidado  

    -   **Apenas os administradores**: Os utilizadores têm de ser um membro do grupo Administradores local  

    -   **Apenas administradores e utilizadores primários**: Os utilizadores têm de ser um membro do grupo local de administradores ou utilizadores primários do computador  

    -   **Não existem utilizadores**: Nenhum utilizador com sessão iniciada num computador cliente poderá iniciar a instalação de software, atualizações de software e sequências de tarefas. As implementações necessárias para o computador instalar sempre na data limite. Os utilizadores não é possível iniciar a instalação de software a partir do catálogo de aplicações ou centro de Software.  

-   **Suspender a introdução do PIN do BitLocker após reiniciar**  </br>
     Se a computadores exigirem a introdução do PIN do BitLocker, esta opção ignora o requisito de introduzir um PIN quando o computador for reiniciado após uma instalação de software.  

    -   **Sempre**: O Configuration Manager suspende temporariamente o BitLocker após a instalação de software que requeira um reinício, iniciou um reinício do computador. Esta definição só se aplica a um reinício do computador iniciado pelo Configuration Manager. Esta definição não suspende o requisito de introduzir o PIN do BitLocker quando o utilizador reinicia o computador. O requisito de introdução do PIN do BitLocker retoma após o arranque do Windows.

    -   **Nunca**: O Configuration Manager não suspende o BitLocker no próximo arranque do computador após a instalação de software que requeira um reinício. Neste cenário, a instalação de software não ficará concluída enquanto o utilizador não introduzir o PIN para concluir o processo de arranque padrão e carregar o Windows.

-   **O software adicional gere a implementação de aplicações e atualizações de software**  </br>
     Apenas deverá ativar esta opção nas seguintes condições:  

    -   Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

    -   Utilizar o Configuration Manager software development kit (SDK) para gerir as notificações de agente do cliente e a instalação de aplicações e atualizações de software.  

    > [!WARNING]  
    >  Se escolher esta opção quando nenhuma destas condições aplicam-se, o cliente não instala atualizações de software e as aplicações necessárias. Esta definição não impede que os utilizadores instalar aplicações a partir do catálogo de aplicações ou a instalação de sequências de tarefas, pacotes e programas.  

-   **Política de execução do PowerShell**  </br>
     Configure a forma como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Estes scripts são frequentemente utilizados para deteção de itens de configuração para definições de compatibilidade. Também podem ser enviados numa implementação como um script padrão.  

    -   **Ignorar**: O cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que possam ser executados scripts não assinados.  

    -   **Restrito**: O cliente do Configuration Manager utiliza a configuração atual do Windows PowerShell no computador cliente. Esta configuração determina se podem executar scripts não assinados.  

    -   **Todas assinadas**: O cliente do Configuration Manager apenas executa scripts um fabricante fidedigno assinou-los. Esta restrição aplica-se de forma independente a partir da configuração atual do Windows PowerShell no computador cliente.  

     Esta opção necessita, pelo menos, o Windows PowerShell versão 2.0. A predefinição é **todas assinadas**.  

    > [!TIP]  
    >  Se os scripts não assinados falham para executar devido a esta definição de cliente, o Configuration Manager apresenta este erro das seguintes formas:  
    >   
    > -   O **monitorização** área de trabalho na consola apresenta o ID de erro de estado de implementação **0x87D00327** e uma descrição **Script não está assinado**  
    > -   Os relatórios apresentam o tipo de erro **erro de deteção**e, em seguida, o código de erro **0x87D00327** e uma descrição **Script não está assinado**, ou um código de erro  **0x87D00320** e uma descrição **o anfitrião do script ainda não foi instalado**. Um relatório de exemplo é **detalhes de erros de itens de configuração numa linha de base de configuração para um recurso**.  
    > -   O **DcmWmiProvider.log** ficheiro apresenta a mensagem **Script não está assinado (erro: 87D 00327; Origem: CCM)**.  

-   **Mostrar notificações para novas implementações**  </br>
     Escolha **Sim** para apresentar uma notificação para as implementações disponíveis a menos que uma semana.  Esta mensagem apresenta sempre que o agente do cliente é iniciado.

-   **Desativar a aleatoriedade de prazos**  </br>
     Após o prazo de implementação, esta definição determina se o cliente utiliza um atraso de ativação de até duas horas para instalar atualizações de software necessárias. Por predefinição, o atraso de ativação está desativado.  

     Para cenários com infraestrutura de ambiente de trabalho virtual (VDI), este atraso ajuda a distribuir o processamento de CPU e a transferência de dados para uma máquina anfitriã com várias máquinas virtuais. Mesmo que não utilize VDI, muitos clientes a instalar as mesmas atualizações em simultâneo negativamente podem aumentar a utilização da CPU no servidor do site. Este comportamento pode também mais lentos pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

     Se os clientes tem de instalar atualizações de software necessárias no prazo de implementação sem atrasos, em seguida, configure esta definição para **Sim**. 

-   **Período de tolerância para aplicação após o prazo de implementação (horas)** </br>
     Se quiser conceder aos utilizadores mais tempo a instalar a aplicação necessária ou implementações de atualização de software para além do prazo, em seguida, configure esta definição para **Sim**. Este período de tolerância é de um computador desativado para um período de tempo alargado e o utilizador tem de instalar várias aplicações ou implementações de atualizações. Por exemplo, se um utilizador devolvido a partir das férias e, tem de aguardar durante muito tempo ao cliente instala as implementações de aplicações em atraso. 

     Defina um período de tolerância de 1 a 120 horas. Utilize esta definição juntamente com a propriedade de implementação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador**. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).



##  <a name="computer-restart"></a>Reinício do computador  
 As seguintes definições tem de ser mais curtas duração a janela de manutenção mais curta aplicada ao computador.  

 Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Apresentar uma notificação temporária ao utilizador que indica o intervalo antes do utilizador sessão é terminada ou do computador reinicia (minutos)**
-   **Apresentar uma caixa de diálogo que o utilizador não é possível fechar, que apresenta o intervalo em contagem decrescente antes do utilizador sessão é terminada ou o computador reinicia (minutos)**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Além das informações seguintes, pode encontrar detalhes adicionais sobre como utilizar as definições de cliente do Endpoint Protection no [cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Gerir o cliente do Endpoint Protection nos computadores cliente**  </br>
     Escolha **Sim** se pretender gerir os clientes existentes do Endpoint Protection e o Windows Defender em computadores na sua hierarquia.  

     Escolha esta opção se já tiver instalado o cliente do Endpoint Protection e pretender geri-lo com o Configuration Manager.  Esta instalação separada inclui um processo com script utilizando uma aplicação do Configuration Manager ou o pacote e programa.

-   **Instalar o cliente do Endpoint Protection nos computadores cliente**   </br>
     Escolha **Sim** para instalar e ativar o cliente do Endpoint Protection nos computadores cliente ainda não estiver a executar o cliente.  

    > [!NOTE]  
    >  Se o cliente do Endpoint Protection já estiver instalado, escolher **não** não desinstala o cliente do Endpoint Protection. Para desinstalar o cliente do Endpoint Protection, configure o **cliente gerir o Endpoint Protection nos computadores cliente** definição de cliente para **não**. Em seguida, implemente um pacote e programa para desinstalar o cliente do Endpoint Protection.  

-   **Remover automaticamente software antimalware anteriormente instalado antes da instalação do Endpoint Protection** </br>
    Configure esta definição para **Sim** para o cliente do Endpoint Protection tentar desinstalar outras aplicações de antimalware. Vários clientes antimalware no mesmo dispositivo podem entrar em conflito e afetar o desempenho do sistema.

-   **Permite ao cliente do Endpoint Protection para instalação e reinicia fora das janelas de manutenção. Janelas de manutenção tem de ser, pelo menos, 30 minutos longa para a instalação do cliente** </br>
    Configure esta definição para **Sim** para substituir os comportamentos de instalação típicas com janelas de manutenção. Esta definição cumpre os requisitos de negócio para a prioridade de manutenção do sistema para fins de segurança. 

-   **Para dispositivos Windows Embedded com filtros de escrita, consolide a instalação de cliente do Endpoint Protection (requer reinicialização)**  </br>
     Escolha **Sim** para desativar o filtro de escrita no dispositivo Windows Embedded e reiniciar o dispositivo. Esta ação consolida a instalação no dispositivo.  

     Se configurar esta definição para **não**, em seguida, o cliente será instalado numa sobreposição temporária que limpa quando o dispositivo for reiniciado. Neste cenário, o cliente do Endpoint Protection não ficar totalmente instalados enquanto outra instalação consolida as alterações no dispositivo. Esta configuração é a predefinição.  

-   **Suprimir quaisquer reinícios necessários após o cliente do Endpoint Protection está instalado**  </br>
     Escolha **Sim** para suprimir um reinício do computador se for necessário, após a instalação de cliente do Endpoint Protection.  

    > [!IMPORTANT]  
    >  Se o cliente do Endpoint Protection requer um reinício do computador e esta definição **não**, em seguida, o computador seja reiniciado independentemente de quaisquer janelas de manutenção configuradas.  

-   **Permitido período de tempo que os utilizadores pode adiar um reinício necessário para concluir a instalação do Endpoint Protection (horas)**  </br>
     Se for necessário um reinício após a instalação de cliente do Endpoint Protection, esta definição especifica o número de horas que os utilizadores podem adiar o reinício necessário. Esta definição requer que o **suprimir reinícios de qualquer computador necessários após a instalação do cliente do Endpoint Protection** definição é **não**.  

-   **Desativar origens alternativas (tais como Microsoft Windows Update, Microsoft Windows Server Update Services ou partilhas UNC) para a atualização inicial da definição nos computadores cliente**  </br>
     Escolha **Sim** se pretender que o Configuration Manager para instalar apenas a atualização inicial da definição nos computadores cliente. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda de rede durante a instalação inicial da atualização das definições.  



##  <a name="enrollment"></a>Inscrição

-   **Intervalo de consulta para clientes legados de dispositivos móveis** </br>
    Clique em **intervalo definido** para especificar o período de tempo, em minutos ou horas, o que dispositivos móveis legados consultam de política. Estes dispositivos incluem plataformas, tais como o Windows CE, Mac OS X e Unix ou Linux.

-   **Intervalo de consulta para dispositivos modernos (minutos)** </br>
    Introduza o número de minutos que consultam dispositivos modernos para a política. Esta definição destina-se a dispositivos Windows 10 geridos através da gestão de dispositivos móveis no local.

-   **Permitir que os utilizadores a inscrição de dispositivos móveis e computadores Mac** </br>
    Para ativar a inscrição de utilizador com base dos dispositivos legados, configure esta definição para **Sim**e, em seguida, configure a definição seguinte:

    -   **Perfil de inscrição** </br>
        Clique em **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [configurar as definições de cliente para inscrição](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Permitir que os utilizadores inscreverem dispositivos modernos** </br>
    Para ativar a inscrição de utilizador com base dos dispositivos modernos, configure esta definição para **Sim**e, em seguida, configure a definição seguinte:

    -   **Perfil de inscrição de dispositivos modernos** </br>
        Clique em **definir perfil** criar ou selecionar um perfil de inscrição. Para obter mais informações, consulte [criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventário de Hardware  

-   **Ativar inventário de hardware nos clientes** </br>
    Esta definição está definida como **Sim** por predefinição. Para obter mais informações, consulte [introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Agenda de inventário de hardware** </br>
    Clique em **agenda** para ajustar a frequência com que os clientes a executar o inventário de hardware ciclo. Por predefinição, este ciclo ocorre a cada sete dias.

-   **Máximo de atraso aleatório (minutos)** </br>
    Especifique o número máximo de minutos para que o cliente do Configuration Manager Utilize uma ordem aleatória do inventário de hardware ciclo da agenda definida. Este prazos em todos os clientes ajuda-o processamento de inventário de balanceamento de carga no servidor do site. Pode especificar um valor de 0 a 480 minutos. Por predefinição, este valor é definido como 240 minutos (quatro horas).

-   **Tamanho máximo do ficheiro MIF personalizado (KB)**  </br>
     Especifica o tamanho máximo, em quilobytes (KB) permitido para cada ficheiro de formato MIF (Management Information Format) personalizado que o cliente recolhe durante um ciclo de inventário de hardware. O agente de inventário de hardware do Configuration Manager não processa ficheiros MIF personalizados que excedem este tamanho. Pode especificar um tamanho de 1 KB 5,120 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro de dados de inventário de hardware normal.  

    > [!NOTE]  
    >  Esta definição está disponível apenas nas predefinições do cliente.  

-   **Classes de inventário de hardware**  </br>
     Clique em **definir Classes** para expandir as informações de hardware recolhidas dos clientes sem necessitar de editar manualmente o ficheiro sms_def.mof. Para obter mais informações, consulte [como configurar inventário de hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Recolher ficheiros MIF**  </br>
     Utilize esta definição para especificar se pretende recolher ficheiros MIF de clientes do Configuration Manager durante o inventário de hardware.  

     Para um ficheiro MIF possa ser recolhido pelo inventário de hardware, tem de ser no local correto no computador cliente. Por predefinição, os ficheiros estão localizados nos seguintes caminhos:  

    -   **Ficheiros IDMIF** deve estar na pasta windows\system32\ccm\inventory\idmif. 

    -   **Os ficheiros NOIDMIF** deve estar na pasta windows\system32\ccm\inventory\noidmif.

    > [!NOTE]  
    >  Esta definição está disponível apenas nas predefinições do cliente.

   

##  <a name="metered-internet-connections"></a>Ligações de Internet com tráfego limitado  
 Gerir como Windows 8 e posteriores computadores utilizam ligações à Internet com tráfego limitado para comunicar com o Configuration Manager. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

> [!NOTE]  
>  A definição de cliente configurado não é aplicado nos seguintes cenários:  
>   
> -   O computador estiver numa ligação de dados de roaming: O cliente do Configuration Manager não efetua as tarefas que exigem a dados a serem transferidos para sites do Configuration Manager.  
> -   As propriedades de ligação de rede do Windows estão configuradas como não limitadas: O cliente do Configuration Manager comporta-se como se a ligação se tratasse e, por isso, transfere dados para o site.  

-   **Comunicação com clientes em ligações à Internet com tráfego limitado**  </br>
     Escolha uma das seguintes opções para esta definição:  

    -   **Permitir**: Todas as comunicações de cliente são permitidas através da ligação de Internet limitada, a menos que o dispositivo cliente está a utilizar uma ligação de dados de roaming.  

    -   **Limite**: Apenas as seguintes comunicações de cliente serão permitidas através da ligação à Internet com tráfego limitado:  

        -   Obtenção de políticas de cliente  

        -   Mensagens de estado de cliente a enviar para o site  

        -   Pedidos de instalação de software utilizando o Catálogo de Aplicações  

        -   Implementações necessárias (quando for atingido o prazo de instalação)  

        > [!IMPORTANT]  
        >  O cliente permite sempre instalações de software a partir do Centro de Software ou o catálogo de aplicações, independentemente das definições de ligação à Internet com tráfego limitado.  

         Se for atingido o limite de transferência de dados para a ligação à Internet com tráfego limitado, o cliente tenta já não está a comunicar com sites do Configuration Manager.  

    -   **Bloco**: O cliente do Configuration Manager não tenta comunicar com sites do Configuration Manager quando estiver a utilizar uma ligação à Internet com tráfego limitado. Esta é a opção predefinida.  



##  <a name="power-management"></a>Gestão de energia  

-   **Permitir a gestão de energia dos dispositivos** </br>
    Configure esta definição para **Sim** para ativar a gestão de energia nos clientes. Para obter mais informações, consulte [introdução à gestão de energia](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia**  </br>
     Escolha **Sim** para permitir que os utilizadores do Centro de Software excluam os respetivos computadores a partir de qualquer definições de gestão de energia configuradas.  

-   **Ativar reativação proxy** </br> 
     Especifique **Sim** para completar a definição de reativação por LAN do site quando estiver configurado para pacotes unicast.  

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
         O cliente do Configuration Manager configura automaticamente o número de porta de proxy de reativação nos dispositivos que executam a Firewall do Windows Defender. Clique em **configurar** para especificar os perfis de firewall pretendido.

        Se os clientes executarem uma firewall diferente, tem de configurar manualmente para permitir a **número de porta de proxy de reativação (UDP)**.  
        
    -   **Prefixos IPv6 se necessários para DirectAccess ou outros dispositivos de rede intervenientes. Utilize uma vírgula para separar várias entradas** </br>
        Introduza os prefixos IPv6 necessários para um proxy de reativação a funcionar na sua rede.



##  <a name="remote-tools"></a>Ferramentas remotas  

-   **Ativar Controlo Remoto nos clientes** e **Perfis de exceção de firewall**  </br>
     Clique em **configurar** para ativar a funcionalidade de controlo remoto do Configuration Manager. Opcionalmente, configure as definições da firewall para permitir o controlo remoto funcione nos computadores cliente.  

     Por predefinição, o controlo remoto encontra-se desativado.  

    > [!IMPORTANT]  
    >  Se as definições da firewall não estiverem configuradas, o controlo remoto poderá não funcionar corretamente.  

-   **Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software**  </br>
     Escolha se os utilizadores podem alterar as opções de controlo remoto no Centro de Software.  

-   **Permitir o Controlo Remoto de um computador autónomo**  </br>
     Escolha se um administrador pode utilizar o controlo remoto para aceder a um computador cliente que está a sessão terminada ou bloqueado. Apenas um computador com sessão iniciada e desbloqueado pode ser controlado remotamente quando esta definição estiver desativada.  

-   **Solicitar ao utilizador permissão do Controlo Remoto**  </br>
     Escolha se o computador cliente mostra uma mensagem solicitando a permissão de utilizador antes de permitir que uma sessão de controlo remoto.  

-   **Pedir ao utilizador permissão transferir o conteúdo da área de transferência partilhada** </br>
    Permitir que os utilizadores a oportunidade de aceitar ou recusar as transferências de ficheiros antes de transferir o conteúdo da área de transferência partilhada numa sessão de controlo remoto. Os utilizadores só têm de conceder permissão, uma vez por sessão e o Visualizador não tem a capacidade de conceder si próprios permissão para continuar com a transferência de ficheiros.

-   **Conceder permissão de Controlo Remoto ao grupo de Administradores local**  </br>
     Escolha se a administradores locais no servidor que inicia a ligação de controlo remoto podem estabelecer sessões de controlo remoto nos computadores cliente.  

-   **Nível de acesso permitido**  </br>
     Especifique o nível de acesso de controlo remoto para permitir. Escolha entre as seguintes definições:  
    - **Sem acesso**
    - **Ver apenas**
    - **Controlo total**  

-   **Visualizadores de controlo remoto e assistência remota**  </br>
     Clique em **definir visualizadores** para especificar os nomes dos utilizadores Windows que poderão estabelecer sessões de controlo remoto para computadores cliente.  

-   **Mostrar ícone de notificação de sessão na barra de tarefas**  </br>
     Configure esta definição para **Sim** para mostrar um ícone na barra de tarefas para indicar uma sessão ativa de controlo remoto do cliente Windows.  

-   **Mostrar barra de ligação da sessão**  </br>
     Configure esta definição para **Sim** para mostrar uma barra de ligação de sessão de alta visibilidade nos clientes para indicar uma sessão ativa de controlo remoto.  

-   **Reproduzir um som no cliente**  </br>
     Configure esta definição para utilizar som para indicar quando uma sessão de controlo remoto está ativa num computador cliente. Selecione uma das seguintes opções:
    - **Sem som**
    - **Início e o envio de sessão** (predefinição)
    - **Repetidamente durante a sessão**  

-   **Gerir definições da Assistência Remota não solicitada**  </br>
     Configure esta definição para **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota não solicitadas.  

     Numa sessão de assistência remota não solicitada, o utilizador do computador cliente não pediu a assistência para iniciar a sessão.  

-   **Gerir definições da Assistência Remota solicitada**  </br>
     Configure esta definição para **Sim** para permitir que o Configuration Manager gerir sessões de assistência remota solicitadas.  

     Numa sessão de assistência remota solicitada, o utilizador do computador cliente enviou um pedido para o administrador para a assistência remota.  

-   **Nível de acesso para a Assistência Remota**  </br>
     Escolha o nível de acesso a atribuir às sessões de assistência remota que sejam iniciadas na consola do Configuration Manager.  Selecione uma das seguintes opções:
    - **Nenhum** (predefinição)
    - **Visualização remota**
    - **Controlo total**

    > [!NOTE]  
    >  O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

-   **Gerir definições de Ambiente de Trabalho Remoto**  </br>
     Configure esta definição para **Sim** para permitir que o Configuration Manager gerir sessões de ambiente de trabalho remoto para computadores.  

-   **Permitir que os visualizadores autorizados estabeleçam ligação utilizando a ligação ao Ambiente de Trabalho Remoto**  </br>
     Configure esta definição para **Sim** para adicionar os utilizadores especificados na lista de visualizadores autorizados para o grupo de utilizadores local do ambiente de trabalho remoto nos clientes.  

-   **Exigir autenticação de nível de rede nos computadores com o sistema operativo Windows Vista e versões posteriores**  </br>
     Configure esta definição para **Sim** para utilizar a autenticação de nível de rede (NLA) para estabelecer ligações de ambiente de trabalho remoto para os computadores cliente. NLA inicialmente requer menos recursos do computador remoto porque concluído a autenticação de utilizador antes de estabelecer uma ligação de ambiente de trabalho remoto. Utilizar NLA é uma configuração mais segura. NLA ajuda a proteger o computador contra utilizadores mal intencionados ou software e reduz o risco de ataques denial-of-service.  



## <a name="software-center"></a>Centro de software

-   **Selecione estas novas definições para especificar as informações da empresa** </br>
    Configure esta definição para **Sim**e, em seguida, especifique as seguintes definições para marca Centro de Software para a sua organização:

    - **Nome da empresa** </br>
        Introduza o nome da organização que os utilizadores visualizam no Centro de Software.
    - **Esquema de cores para o Centro de Software** </br>
        Clique em **selecione cor** para definir a cor primária utilizado pelo centro de Software.
    - **Selecionar um logótipo no Centro de Software** </br>
        Clique em **procurar** para selecionar uma imagem a apresentar no Centro de Software. O logótipo tem de ser um JPEG ou PNG de 400 x 100 pixéis com um tamanho máximo de 750 KB.

-   Visibilidade de separador de centro de software </br>
    Configurar as definições adicionais neste grupo para **Sim** para fazer com que os seguintes separadores visível no Centro de Software:
    - **Aplicações**
    - **Atualizações**
    - **Sistemas operativos**
    - **Estado da instalação**
    - **Conformidade do dispositivo**
    - **Opções**

    Por exemplo, se a sua organização utilizar políticas de conformidade e pretender ocultar o separador de conformidade do dispositivo no Centro de Software, configure o **separador de ativar a conformidade do dispositivo** definição **não**.



## <a name="software-deployment"></a>Implementação de software  

-   **Agendar reavaliação das implementações**  </br>
     Configure uma agenda para quando o Configuration Manager deverá reavaliar as regras de requisitos para todas as implementações. O valor predefinido é de sete em sete dias.  

    > [!IMPORTANT]  
    >  Recomendamos que altere este valor para um valor inferior à predefinição de. Uma agenda de reavaliação mais agressiva afeta negativamente o desempenho da sua rede e os computadores cliente.  

     Iniciar esta ação de um cliente escolhendo o **ciclo de avaliação de implementação de aplicação** do **ações** separador do **do Configuration Manager** painel de controlo.  



##  <a name="software-inventory"></a>Inventário de software  

-   **Ativar inventário de software nos clientes** </br>
    Esta definição está definida como **Sim** por predefinição. Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Agendar a recolha de ficheiros e de inventário de software** </br>
    Clique em **agenda** para ajustar a frequência de que os clientes executam ciclos de recolha de ficheiros e inventário de software. Por predefinição, este ciclo ocorre a cada sete dias.

-   **Inventariar detalhe de relatórios**  </br>
     Especifique um dos seguintes níveis de informações de ficheiro ao inventário:
    - **Apenas ficheiro**
    - **Apenas o produto**
    - **Total detalhes** (predefinição)

-   **Inventariar estes tipos de ficheiro**  </br>
     Se pretender especificar os tipos de ficheiro a inventariar, clique em **definir tipos**e, em seguida, configure as seguintes opções:  

    > [!NOTE]  
    >  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que cada definição devolve intercalado.  

    -   Clique em de **novo** ícone para adicionar um novo tipo de ficheiro ao inventário. Em seguida, especifique as seguintes informações no **propriedades do ficheiro inventariado** caixa de diálogo:  

        -   **Nome**: Forneça um nome para o ficheiro que pretende inventariar. Utilize um asterisco (**&#42;**) universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter. Por exemplo, se pretender inventariar todos os ficheiros com a extensão. doc, especifique o nome de ficheiro  **\*. doc**.  

        -   **Localização**: Clique em **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro especificado, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

        -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, todos os ficheiros comprimidos ou encriptados não são inventariados.  

        -   **Excluir ficheiros da pasta Windows**: Quando seleciona esta opção, os ficheiros na pasta Windows e respetivas subpastas não são inventariados.  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades do Ficheiro Inventariado** .  

    -   Adicionar todos os ficheiros que pretende inventariar e, em seguida, clique em **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

-   **Recolher ficheiros**  </br>
     Se pretender recolher ficheiros de computadores cliente, clique em **definir ficheiros** e, em seguida, configure as seguintes definições:  

    > [!NOTE]  
    >  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que cada definição devolve intercalado.  

    -   No **configurar definições do cliente** caixa de diálogo, clique em de **novo** ícone para adicionar um ficheiro a serem recolhidos.  

    -   Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

        -   **Nome**: Forneça um nome para o ficheiro que pretende recolher. Utilize um asterisco (**&#42;**) universal para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar um único caráter.  

        -   **Localização**: Clique em **definir** para abrir o **propriedades do caminho** caixa de diálogo. Configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro que pretende recolher, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

        -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, todos os ficheiros comprimidos ou encriptados não são recolhidos.  

        -   **Parar a recolha de ficheiros quando o tamanho total dos ficheiros excede (KB)**: Especifique o tamanho do ficheiro, em quilobytes (KB) após o qual o cliente deixa de recolher os ficheiros especificados.  

          > [!NOTE]  
          >  O servidor do site recolhe as cinco versões mais recentes dos ficheiros recolhidos e armazena-os no  *&lt;diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol diretório. Se um ficheiro não foi alterada desde o último ciclo de inventário de software, o ficheiro não é recolhido novamente.  
          >   
          >  Inventário de software não recolher ficheiros com mais de 20 MB.  
          >   
          >  O valor **tamanho máximo para todos ficheiros recolhidos (KB)** no **configurar definições do cliente** caixa de diálogo mostra o tamanho máximo para todos ficheiros recolhidos. Quando este tamanho for atingido, interrompe a recolha de ficheiros. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

          > [!IMPORTANT]
          >  Se configurar o inventário de software para recolher muitos ficheiros grandes, esta configuração poderá afetar negativamente o desempenho do seu servidor de site e de rede.  

        Para obter informações sobre como visualizar ficheiros recolhidos, consulte [como utilizar o Explorador de recursos para ver o inventário de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Clique em **OK** para fechar a caixa de diálogo **Propriedades do Ficheiro Recolhido** .  

    -   Adicionar todos os ficheiros que pretende recolher e, em seguida, clique em **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

-   **Definir Nomes**  </br>
     O agente de inventário de software obtém nomes de produto e fabricante de informações de cabeçalho de ficheiro. Estes nomes não são normalizados sempre as informações de cabeçalho de ficheiro. Quando visualiza o inventário de software no Explorador de recursos, podem aparecer versões diferentes do mesmo fabricante ou o nome de produto. Padronizar estes nomes a apresentar, clique em **definir nomes** e, em seguida, configure as seguintes definições:  

    -   **Nome do tipo**: Inventário de software recolhe informações sobre produtos e fabricantes. Escolha se pretende configurar os nomes a apresentar para um **fabricante** ou um **produto**.  

    -   **Nome a apresentar**: Especifique o nome a apresentar que pretende utilizar em vez dos nomes de **nomes inventariados** lista. Clique em de **novo** ícone para especificar um novo nome a apresentar.  

    -   **Nomes inventariados**: Clique em de **novo** ícone para adicionar um nome inventariado. Este nome é substituído no inventário de software pelo nome selecionado no **nome a apresentar** lista. Pode adicionar vários nomes a substituir.  



##  <a name="software-metering"></a>Medição de Software

-   **Ativar medição de software nos clientes** </br>
    Esta definição está definida como **Sim** por predefinição. Para obter mais informações, consulte [medição de Software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Recolha de dados de agenda** </br>
    Clique em **agenda** para ajustar a frequência de que os clientes executam o ciclo de medição de software. Por predefinição, este ciclo ocorre a cada sete dias.



##  <a name="software-updates"></a>Atualizações de software  

-   **Ativar atualizações de software nos clientes**  </br>
     Utilize esta definição para ativar atualizações de software nos clientes do Configuration Manager. Quando desativar esta definição, o Configuration Manager removerá as políticas de implementação existentes do cliente. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

    > [!IMPORTANT]  
    >  Ao desativar esta definição, as políticas de conformidade que dependem de atualizações de software deixarão de funcionar.  

-   **Agendamento da análise de atualização de software**  </br>
     Clique em **agenda** para especificar a frequência que o cliente inicia uma análise da avaliação de compatibilidade. Esta análise determina o estado das atualizações de software no cliente (por exemplo, é necessário ou instalado). Para obter mais informações sobre a avaliação de compatibilidade, consulte [avaliação de compatibilidade de atualizações de Software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Por predefinição, esta análise utiliza uma agenda simples para iniciar a cada sete dias. Pode criar uma agenda personalizada para especificar um dia de início exatas e a hora, utilizar tempo Universal Coordenado (UTC) ou na hora local e configurar o intervalo periódico para um dia da semana específico.  

    > [!NOTE]  
    >  Se especificar um intervalo de menos de um dia, o Configuration Manager assume-se automaticamente como um dia.  

    > [!WARNING]  
    >  A hora de início real em computadores cliente é a hora de início mais um período de tempo aleatório de cópia de segurança duas horas. Este prazos impede que os computadores cliente de iniciar a análise e em simultâneo a ligar ao ponto de atualização de software ativo.  

-   **Agendar a reavaliação de implementação**  </br>
     Clique em **agenda** para configurar a frequência a atualizações de software cliente agente deverá reavaliar as atualizações de software para o estado de instalação nos computadores de cliente do Configuration Manager. Quando as atualizações de software instaladas anteriormente já não se encontram nos clientes, mas são ainda necessárias, o cliente Reinstala as atualizações de software.

     Ajuste esta agenda com base na política da empresa para compatibilidade de atualização de software e indica se os utilizadores podem desinstalarem atualizações de software. Cada ciclo de reavaliação da implementação resulta na atividade de processador de computador cliente e rede. Por predefinição, esta definição utiliza uma agenda simples para iniciar a análise de reavaliação de implementação a cada sete dias.  

    > [!NOTE]  
    >  Se especificar um intervalo de menos de um dia, o Configuration Manager assume-se automaticamente como um dia.  

-   **Quando qualquer prazo de implementação de atualização de software é alcançado, instale todas as outras implementações de atualização de software com prazo a terminar no período de tempo especificado**  </br>
     Configure esta definição para **Sim** instalar todas as atualizações de software a partir de implementações necessárias com prazos ocorrer dentro de um período de tempo especificado. Quando uma implementação de atualização de software necessárias atinge um prazo, o cliente inicia a instalação para as atualizações de software na implementação. Esta definição determina se deve instalar as atualizações de software a partir de outras implementações necessárias com um prazo no período de tempo especificado.  

     Utilize esta definição para agilizar a instalação de atualizações de software necessárias. Esta definição também potencialmente aumenta a segurança do cliente, potencialmente diminui notificações do utilizador final e diminui potencialmente os reinícios do cliente. Por predefinição, esta definição está definida como **não** , por conseguinte, não ativada.  

-   **Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas**  </br>
     Utilize esta definição para especificar o período de tempo da definição anterior. Pode introduzir um valor de 1 a 23 horas e de 1 a 365 dias. Por predefinição, esta definição é configurada durante sete dias.  

-   **Ativar a instalação dos ficheiros de instalação rápida nos clientes** </br>
    Configure esta definição para **Sim** para permitir aos clientes utilizar ficheiros de instalação rápida. Para obter mais informações, consulte [ficheiros de instalação gerir Express para Windows 10 das atualizações](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Porta utilizada para transferir conteúdo para os ficheiros de instalação rápida** </br>
        Esta definição configura a porta local para o serviço de escuta HTTP transferir conteúdo rápido. Está definido para 8005 por predefinição. Não é necessário abrir esta porta na firewall do cliente.

-   **Ativar a gestão do agente de cliente do Office 365** </br>
    Utilize esta definição para ativar a gestão do agente de cliente do Office 365. Quando definir o valor **Sim**, permite que a configuração do Office 365 definições de instalação, transferir os ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager. Para obter mais informações, consulte [gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Mensagens de estado

-   **Mensagem de estado (minutos) de ciclo de comunicação**  </br>
     Especifica com que frequência os clientes reportam mensagens de estado. Esta definição é de 15 minutos por predefinição.



##  <a name="user-and-device-affinity"></a>Afinidade dispositivo / utilizador  

-   **Limiar de utilização de afinidade de dispositivo e utilizador (minutos)**  </br>
     Especifique o número de minutos antes do Configuration Manager cria um mapeamento de afinidade de dispositivo do utilizador.  Por predefinição, este valor é 2880 minutos (dois dias).

-   **Limiar de utilização de afinidade de dispositivo e utilizador (dias)**  </br>
     Especifique o número de dias durante o qual o cliente mede o limiar de afinidade de dispositivo baseada na utilização.  Por predefinição, este valor é 30 dias.

    > [!NOTE]  
    >  Por exemplo, pode especificar **limiar de utilização de afinidade de dispositivo de utilizador (minutos)** como **60** minutos e **limiar de utilização de afinidade de dispositivo do utilizador (dias)** como **5**  dias. Em seguida, o utilizador tem de utilizar o dispositivo durante 60 minutos num período de cinco dias para criar uma afinidade automática com o dispositivo.  

-   **Configurar automaticamente a afinidade de dispositivo e utilizador a partir dos dados de utilização**  </br>
     Escolha **Sim** criar automática afinidade dispositivo / utilizador com base nas informações de utilização que recolhe do Configuration Manager.  

-   **Permitir ao utilizador a definição dos seus dispositivos primários** </br>
    Quando esta definição for **Sim** , em seguida, os utilizadores podem identificar os seus dispositivos primários no Centro de Software.



## <a name="windows-analytics"></a>Análise do Windows

Para obter mais informações sobre estas definições, consulte [configurar clientes para dados de relatório para o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    