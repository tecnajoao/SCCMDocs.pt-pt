---
title: "As configurações do cliente | Microsoft Docs"
description: "Escolha as configurações do cliente usando o console de administração no System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c8717925dba42451b1e241a7c2f59e43896d7d99
ms.openlocfilehash: 4a169098f30e4a9d708e41ee25c6a400d5ff0e85
ms.contentlocale: pt-pt
ms.lasthandoff: 06/19/2017

---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Todas as configurações de cliente no System Center Configuration Manager são gerenciadas no console do Configuration Manager do **configurações do cliente** nó o **administração** espaço de trabalho. Configuration Manager vem com um conjunto de configurações padrão. Quando você altera as configurações do cliente padrão, essas configurações são aplicadas a todos os clientes na hierarquia. Também pode configurar definições de cliente personalizadas, que substituem as predefinições do cliente, ao atribuí-las a coleções. Para obter mais informações sobre como configurar definições do cliente, veja [Como configurar definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

Muitas das definições de cliente são facilmente compreensíveis. Outras pessoas são descritas aqui.  

## <a name="background-intelligent-transfer-service"></a>Serviço de transferência inteligente em segundo plano  

-   **Limitar a largura de banda de rede máxima para transferências BITS em segundo plano**  

   Quando essa opção é **True** ou **Sim**, os clientes usarão a limitação de largura de banda do BITS.  

-   **Hora de início da janela de limitação**  

   Especifique a hora de início local para o período de limitação do BITS.  

-   **Hora de fim da janela de limitação**  

   Especifique a hora de término de local para o período de limitação do BITS. Se for igual a **hora de início do período de limitação**, limitação do BITS sempre estará habilitada.  

-   **Velocidade máxima de transferência durante a janela de limitação (Kbps)**  

   Especifique a taxa de transferência máxima que os clientes podem usar durante a janela.  

-   **Permitir transferências BITS fora da janela de limitação**  

   Escolha esta opção para permitir que os clientes do Configuration Manager usar configurações de BITS separadas fora do período especificado.  

-   **Velocidade máxima de transferência fora da janela de limitação (Kbps)**  

   Especifique a taxa de transferência máxima que os clientes usarão fora os BITS de limitação de janela, quando você optou por permitir fora da janela de limitação do BITS.  

## <a name="client-cache-settings"></a>Configurações de cache do cliente

- **Configurar o BranchCache**

  Começando na versão 1606, use essa configuração para configurar o computador cliente para [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir que o BranchCache em cache no cliente, defina **habilitar BranchCache** para **Sim**.

- **Configurar o tamanho de cache do cliente**

  O cache do cliente em computadores Windows armazena arquivos temporários usados para instalar aplicativos e programas. Escolha **Sim** para especificar **tamanho máximo do cache** (megabytes ou percentual do disco). O tamanho do cache do cliente pode expandir o tamanho máximo em MB ou a porcentagem de disco, **o que for menor**. Se essa opção for **não**, o tamanho padrão é 5.120 MB.

## <a name="client-policy"></a>Política do cliente  

-   **Intervalo de consulta da política de cliente (minutos)**  

   Especifique a frequência com a qual os seguintes clientes do Configuration Manager baixam política de cliente:  

  -   Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  

  -   Dispositivos móveis que registra do Configuration Manager  

  -   Computadores Mac  

  -   Computadores com o Linux ou UNIX  

-   **Ativar consulta de política de utilizador nos clientes**  

   Quando você define esta opção **True** ou **Sim**, e o Configuration Manager tem [descoberto o usuário](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), os clientes em computadores receberão aplicativos e programas destinados ao usuário conectado.  

   Como o catálogo de aplicativos recebe a lista de softwares disponíveis para usuários do servidor do site, essa configuração não precisa ser **True** ou **Sim** para que os usuários vejam e solicitem aplicativos do catálogo de aplicativos. Porém, se essa configuração é **False** ou **não**, o seguinte não funcionará quando os usuários utilizarem o catálogo de aplicativos:  

  -   Os utilizadores não podem instalar as aplicações que veem no Catálogo de Aplicações.  

  -   Os utilizadores não verão notificações sobre os pedidos de aprovação de aplicação. Em vez disso, devem atualizar o Catálogo de Aplicações e verificar o estado de aprovação.  

  -   Os utilizadores não receberão revisões nem atualizações para as aplicações que são publicadas no catálogo de Catálogo de Aplicações. Mas, eles verão as alterações nas informações do aplicativo no catálogo de aplicativos.  

  -   Se remover a implementação de uma aplicação depois de o cliente ter instalado a aplicação a partir do Catálogo de Aplicações, os clientes continuam a verificar se a aplicação está instalada até um máximo de 2 dias.  

   Além disso, quando essa configuração for **False** ou **não**, os usuários não receberão os aplicativos necessários que você implanta em usuários ou quaisquer outras tarefas de gerenciamento de políticas de usuário.  

   Essa configuração aplica-se aos usuários quando o computador está na intranet e Internet. Ele deve ser **True** ou **Sim** se deseja habilitar políticas do usuário na Internet.  

-   **Ativar pedidos da política do utilizador dos clientes Internet**  

   Quando o cliente e o site são configurados para gerenciamento de clientes baseados na Internet e você definir essa opção como **True** ou **Sim** e ambas das seguintes condições se aplicarem, os usuários recebem a política de usuário quando o computador está na Internet:  

  -   O **habilitar sondagem de política de usuário nos clientes** configuração do cliente é **True**, ou **habilitar política de usuário em clientes** é **Sim**.  

  -   O ponto de gestão baseado na Internet autentica com êxito o utilizador através da autenticação do Windows (Kerberos ou NTLM).  

   Se deixar esta opção como **Falso** ou **Não**, ou se a condição falhar, um computador com a Internet receberá apenas políticas de computador. Neste cenário, os utilizadores ainda podem ver, pedir e instalar aplicações a partir de um Catálogo de Aplicações baseado na Internet. Se essa configuração for **False** ou **não** mas **habilitar sondagem de política de usuário nos clientes** é **True** ou **habilitar política de usuário em clientes** é **Sim**, os usuários não receberão as políticas de usuário até que o computador está conectado à intranet.  

   Para obter mais informações sobre como gerenciar clientes na Internet, consulte [considerações para comunicações de cliente da Internet ou de uma floresta não confiável](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) na [as comunicações entre os pontos de extremidade no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Os pedidos de aprovação de aplicações dos utilizadores não necessitam de políticas de utilizador ou de autenticação de utilizador.  

##  <a name="compliance-settings"></a>Definições de compatibilidade  

-   **Agendar avaliação de compatibilidade**  

     Escolha **agenda** para criar o agendamento padrão que será mostrado aos usuários quando eles implantam uma linha de base de configuração. Este valor pode ser configurado para cada linha de base na caixa de diálogo **Implementar Linhas de Base de Configuração** .  

-   **Ativar Dados e Perfis de Utilizador**  

     Escolha **Sim** se você deseja implantar [perfis e dados de usuário](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) itens de configuração para computadores com Windows 8 em sua hierarquia.  

## <a name="computer-agent"></a>Agente de computador  

-   **Ponto de Web sites Predefinido do Catálogo de Aplicações**  

     Configuration Manager usa essa configuração para conectar usuários ao catálogo de aplicativos do Centro de Software. Pode especificar um servidor que aloja o ponto de Web sites do Catálogo de Aplicações através do nome NetBIOS ou FQDN, especificar deteção automática ou especificar um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor opção uma vez que oferece as seguintes vantagens:  

    -   Os clientes recebem automaticamente um ponto de site do catálogo de aplicativos do seu site, se o site tiver um ponto de site do catálogo de aplicativos.  

    -   Aplicativo catálogo pontos de site da intranet configurados para HTTPS terá preferência sobre os que não estão configurados para HTTPS. Isso ajuda a proteger contra um servidor não autorizado.

    -   Quando os clientes são configurados para gerenciamento de clientes baseados na Internet e intranet, eles recebem um ponto de site do catálogo de aplicativos baseados na Internet quando estão na Internet e um ponto de site do catálogo de aplicativos baseado na intranet quando estão na intranet.  

     A deteção automática não garante que os clientes receberão um ponto de Web sites do Catálogo de Aplicações que esteja mais próximo deles. Pode decidir não utilizar **Detetar automaticamente** pelos seguintes motivos:  

     -   Pretende configurar manualmente o servidor mais próximo dos clientes ou certificar-se de que não ligam a um servidor através de uma ligação de rede lenta.  

     -   Pretende controlar que clientes ligam ao servidor. Isto pode ser para fins de teste, desempenho ou por razões empresariais.  

     -   Não vai querer esperar 25 horas ou esperar por uma alteração de rede para que os clientes sejam configurados com um ponto de Web sites do Catálogo de Aplicações.  

     Se você especifica o ponto de site do catálogo de aplicativos em vez de usa a detecção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Isso ajuda a reduzir a probabilidade de que os usuários serão solicitados credenciais quando eles se conectam ao catálogo de aplicativos na intranet. Para utilizar o nome NetBIOS, tem de aplicar as seguintes condições:  

     -   O nome NetBIOS é especificado nas propriedades do ponto de Web sites do Catálogo de Aplicações.  

     -   Usar o WINS ou todos os clientes estão no mesmo domínio que o ponto de site do catálogo de aplicativos.  

     -   O ponto de site do catálogo de aplicativos está configurado para conexões de cliente HTTP, ou ele está configurado para conexões de cliente HTTPS e o certificado do servidor web tem o nome NetBIOS.  

     Normalmente, os usuários apresentam credenciais quando a URL tem um FQDN, mas não quando a URL é um nome NetBIOS. É expectável que os utilizadores recebam sempre esse pedido quando ligam a partir da Internet, uma vez que esta ligação tem de utilizar o FQDN da Internet. Quando os utilizadores recebem o pedido de credenciais quando estão na Internet, assegure-se de que o servidor que executa o ponto de Web sites do Catálogo de Aplicações pode ligar a um controlador de domínio para a conta de utilizador, de forma que o utilizador possa ser autenticado através de Kerberos.  

    > [!NOTE]  
    >  Como funciona a deteção automática:  
    >   
    >  O cliente faz um pedido de localização de serviço para um ponto de gestão. Se houver um ponto de Web sites do Catálogo de Aplicações no mesmo site que o cliente, este servidor é atribuído ao cliente como o servidor do Catálogo de Aplicações a utilizar. Quando mais de um ponto de sites do catálogo de aplicativos está disponível no site, um servidor habilitado para HTTPS tem precedência sobre um servidor que não está habilitado para HTTPS. Depois dessa filtragem, todos os clientes recebem um dos servidores para usar como o catálogo de aplicativos; Gerenciador de configuração não não balanceamento de carga entre vários servidores. Quando o site do cliente não tem um ponto de site do catálogo de aplicativos, o ponto de gerenciamento retorna forma não determinística um ponto de sites da hierarquia.  
    >   
    >  Quando o cliente está na intranet, se o ponto de site do catálogo de aplicativos escolhido é configurado com um nome NetBIOS para a URL do catálogo de aplicativos, os clientes receberão esse nome NetBIOS em vez do FQDN de intranet. Quando o cliente é detetado na Internet, apenas o FQDN da Internet é atribuído ao cliente.  
    >   
    >  O cliente efetua este pedido de localização de serviço em 25 horas ou sempre que detetar uma alteração de rede. Por exemplo, se o cliente passar da intranet para a Internet, e conseguir localizar um ponto de gestão baseado na Internet, o ponto de gestão baseado na Internet atribui os servidores do ponto de Web sites do Catálogo de Aplicações baseado na Internet aos clientes.  

-   **Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer**  

     Se essa opção for **True** ou **Sim**, o site de catálogo de aplicativos padrão atual URL é automaticamente adicionado à zona de sites confiáveis no Internet Explorer em clientes.  

     Esta definição garante que a definição do Internet Explorer para o Modo Protegido não está ativada. Se o modo protegido estiver habilitado, o cliente do Configuration Manager não poderá instalar aplicativos do catálogo de aplicativos. Por predefinição, a zona de sites fidedignos também suporta o início de sessão de utilizador para o Catálogo de Aplicações, que requer autenticação do Windows.  

     Se você deixar essa opção como **False**, clientes do Configuration Manager podem não conseguir instalar aplicativos do catálogo de aplicativos, a menos que essas configurações do Internet Explorer estejam definidas em outra zona para a URL do catálogo de aplicativos que os clientes usam.  

    > [!NOTE]  
    >  Sempre que o Configuration Manager adiciona um catálogo de aplicativos padrão à zona sites confiáveis, o Configuration Manager remove uma URL do catálogo de aplicativo padrão anterior que o Configuration Manager adicionou antes de adicionar uma nova entrada.  
    >   
    >  Gerenciador de configuração não é possível adicionar a URL se ela já é especificada em uma das zonas de segurança. Nesse cenário, você deve remover a URL da outra zona ou definir manualmente as configurações necessárias do Internet Explorer.  

-   **Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada**  

     Essa configuração deve ser **Sim** se os usuários executam o cliente do Configuration Manager e usar o catálogo de aplicativos.  

     Se alterar esta definição, ela tem efeito assim que os utilizadores carregarem o respetivo browser ou atualizarem a respetiva janela do browser atualmente aberta.  

     Para obter mais informações sobre essa configuração, consulte [certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicativos](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) na [segurança e privacidade para gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nome da organização apresentada no Centro de Software**  

     Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna.  

-   **Utilizar o novo Centro de Software**  

     Se habilitada, todos os computadores cliente afetados por essas configurações de cliente usará o novo centro de Software. Centro de software mostra os aplicativos disponíveis para o usuário que foram anteriormente acessíveis apenas no catálogo de aplicativos dependente do Silverlight.  

     Funções ainda são necessárias para os aplicativos disponíveis para o usuário sejam exibidos no Centro de Software de sistema de site do ponto a ponto de sites do catálogo de aplicativos e serviços web do catálogo de aplicativos.  

     Para obter mais informações, veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Permissões de Instalação**  

    > [!WARNING]  
    >  Esta definição aplica-se ao Catálogo de Aplicações e ao Centro de Software. Esta definição não produz efeitos quando os utilizadores usam o portal da empresa.  

     Configure a forma como os utilizadores podem iniciar a instalação de software, atualizações de software e sequências de tarefa:  

    -   **Todos os usuários**: Usuários conectados a um computador cliente com qualquer autorização, exceto convidado, podem iniciar a instalação de software, atualizações de software e as sequências de tarefas.  

    -   **Somente os administradores**: Os usuários conectados a um computador cliente devem ser um membro do grupo Administradores local para iniciar a instalação de software, atualizações de software e as sequências de tarefas.  

    -   **Somente administradores e usuários primários**: Os usuários conectados a um computador cliente devem ser um membro do grupo Administradores local ou um usuário primário do computador para iniciar a instalação de software, atualizações de software e as sequências de tarefas.  

    -   **Nenhum usuário**: Não há usuários conectados a um computador cliente podem iniciar a instalação de software, atualizações de software e as sequências de tarefas. Implantações necessárias para o computador são sempre instaladas no prazo. Os usuários não é possível iniciar a instalação do software do catálogo de aplicativos ou do Centro de Software.  

-   **Suspender a introdução do PIN do BitLocker após reiniciar**  

     Se a introdução do PIN do BitLocker estiver configurada nos computadores, esta opção permite contornar o requisito de introdução de um PIN quando o computador é reiniciado após uma instalação de software.  

    -   **Sempre**: Configuration Manager suspende temporariamente o BitLocker após ter instalado o software que requer uma reinicialização e iniciou uma reinicialização do computador. Essa configuração se aplica somente a uma reinicialização do computador que é iniciada pelo Configuration Manager e não suspende a necessidade de inserir o PIN do BitLocker quando o usuário reinicia o computador. O requisito de introdução do PIN do BitLocker é retomado após o arranque do Windows.

    -   **Nunca**: Gerenciador de configuração não suspenda o BitLocker na próxima inicialização do computador após a instalação do software que requer uma reinicialização. Neste cenário, a instalação de software não ficará concluída enquanto o utilizador não introduzir o PIN para concluir o processo de arranque padrão e carregar o Windows.

-   **O software adicional gere a implementação de aplicações e atualizações de software**  

     Apenas deverá ativar esta opção nas seguintes condições:  

    -   Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

    -   Use o Configuration Manager software development kit (SDK) para gerenciar notificações do agente cliente e a instalação de aplicativos e atualizações de software.  

    > [!WARNING]  
    >  Se você escolher essa opção quando nenhuma dessas condições se aplicar, atualizações de software e aplicativos necessários não serão instalados em clientes. Essa configuração não evita que usuários instalem aplicativos do catálogo de aplicativos, ou impedir que os pacotes, programas e sequências de tarefas sejam instalados em computadores cliente.  

-   **Política de execução do PowerShell**  

     Configure como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Esses scripts geralmente são usados para detecção de itens de configuração para as configurações de conformidade. Eles também podem ser enviados em uma implantação como um script padrão.  

    -   **Ignorar**: O cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que podem executar scripts não assinados.  

    -   **Restrito**: O cliente do Configuration Manager usa a configuração atual do Windows PowerShell no computador cliente. Essa configuração determina se os scripts não assinados podem ser executados.  

    -   **Tudo assinado**: O cliente do Configuration Manager só executa scripts se um fornecedor confiável entrou-los. Esta restrição aplica-se de forma independente a partir da configuração atual do Windows PowerShell no computador cliente.  

     Essa opção requer pelo menos o Windows PowerShell versão 2.0. O padrão é **tudo assinado**.  

    > [!TIP]  
    >  Se os scripts não assinados não funcionarem devido a essa configuração do cliente, o Configuration Manager relata esse erro das seguintes maneiras:  
    >   
    > -   ID do erro **0X87D00327** e a descrição do **Script não está assinado** como um erro de status de implantação no **monitoramento** espaço de trabalho do console do Configuration Manager.  
    > -   Códigos de erro e descrições de **0X87D00327** e **Script não está assinado** ou **0X87D00320** e **o host de script ainda não foi instalado** com o tipo de erro **erro de descoberta** em relatórios. Um exemplo é **detalhes de erros de itens de configuração em uma linha de base de configuração para um ativo**.  
    > -   A mensagem **Script não está assinado (erro: 87D00327; Origem: CCM)** no **DcmWmiProvider.log** arquivo.  

-   **Mostrar notificações para novas implementações**  

     Escolha **Sim** se você deseja exibir uma notificação para implantações que foram disponível menos de uma semana.  Essa mensagem será exibida sempre que o agente cliente inicia.

-   **Desativar a aleatoriedade de prazos**  

     Essa configuração determina se o cliente usa um atraso de ativação de até 2 horas para instalar atualizações de software necessárias quando o prazo é alcançado. Por predefinição, o atraso de ativação está desativado.  

     Para cenários de virtual desktop infrastructure (VDI), esse atraso pode ajudar a distribuir o processamento da CPU e de transferência de dados para um computador que tenha várias máquinas virtuais que executam o cliente do Configuration Manager. Mesmo que você não use VDI, se muitos clientes instalarem as mesmas atualizações ao mesmo tempo, isso pode aumentar negativamente o uso da CPU no servidor do site. Ele pode também diminuir os pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

     Se as atualizações de software devem ser instaladas sem demora quando o prazo configurado for alcançado, escolha **Sim** para essa configuração.  

-   **Período de cortesia para imposição após o prazo de implantação (horas)**

     Em alguns casos, você talvez queira conceder aos usuários mais tempo para implantações de aplicativo de instalação necessários ou atualizações de software, além de qualquer prazos que você configurou. Isso geralmente pode ser necessário quando um computador desativado por um longo período de tempo e precisa instalar um grande número de implantações de aplicativo ou atualização. Por exemplo, se um usuário tiver retornado apenas de férias, eles talvez precise aguardar um longo enquanto como aplicativo vencido implantações são instaladas. Para ajudar a resolver esse problema, você pode definir um período de cortesia de imposição, implantar as configurações de cliente do Configuration Manager em uma coleção.

     Você pode definir um período de cortesia de 1 a 120 horas. Essa configuração é usada em conjunto com a propriedade de implantação **atrase a imposição dessa implantação de acordo com as preferências do usuário**. Para obter mais detalhes, consulte [implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).

##  <a name="computer-restart"></a>Reinicialização do computador  
 Quando especificar estas definições de reinício do computador, certifique-se de que o valor do intervalo de notificação temporária de reinício e de que o valor do intervalo final de contagem regressiva têm uma duração inferior à da janela de manutenção mais curta que estiver aplicada ao computador.  

 Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **Gerenciar o cliente do Endpoint Protection em computadores cliente**  

     Escolha **True** ou **Sim** se você quiser gerenciar clientes existentes do Endpoint Protection em computadores na sua hierarquia.  

     Escolha esta opção se você já tiver instalado o cliente Endpoint Protection e deseja gerenciá-lo com o Configuration Manager.  

     Além disso, escolha esta opção se você quiser criar um script para desinstalar uma solução antimalware existente, instalar o cliente do Endpoint Protection e implantar este script usando um aplicativo do Configuration Manager ou o pacote e programa.  

-   **Instalar o cliente do Endpoint Protection nos computadores cliente**  

     Escolha **True** ou **Sim** para instalar e habilitar o cliente Endpoint Protection em computadores cliente onde ele não ainda estiver instalado.  

    > [!NOTE]  
    >  Se o cliente Endpoint Protection já estiver instalado, escolhendo **False** ou **não** não desinstalará o cliente Endpoint Protection. Para desinstalar o cliente Endpoint Protection, defina o **cliente de gerenciar o Endpoint Protection em computadores cliente** configuração do cliente para **False** ou **não**. Em seguida, implante um pacote e programa para desinstalar o cliente do Endpoint Protection.  

-   **Para dispositivos Windows Embedded com filtros de escrita, consolidar a instalação de cliente do Endpoint Protection (necessita de reinicialização)**  

     Escolha **Sim** para desabilitar o filtro de gravação no dispositivo Windows Embedded e reiniciar o dispositivo. Esta opção consolida a instalação no dispositivo.  

     Se for especificado **Não** , o cliente será instalado numa sobreposição temporária que será eliminada quando o dispositivo for reiniciado. Neste cenário, o cliente do Endpoint Protection não será consolidado enquanto outra instalação não consolidar as alterações no dispositivo. Esta é a predefinição.  

-   **Suprimir qualquer reinicialização necessária do computador depois que o cliente Endpoint Protection está instalado**  

     Escolha **True** ou **Sim** para suprimir a reinicialização do computador, se for necessário depois que o cliente do Endpoint Protection é instalado.  

    > [!IMPORTANT]  
    >  Se o cliente do Endpoint Protection exigir uma reinicialização do computador e essa configuração é **False**, a reinicialização ocorrerá independentemente das janelas de manutenção que foram configuradas.  

-   **Permitido período de tempo que os usuários pode adiar o reinício necessário para concluir a instalação do Endpoint Protection (horas)**  

     Especifique o número de horas que os usuários podem adiar a reinicialização do computador se isso for necessário depois que o cliente do Endpoint Protection é instalado. Essa opção pode ser configurada somente se o **suprimir qualquer necessária do computador é reiniciado após o cliente Endpoint Protection é instalado** opção é **False**.  

-   **Desabilitar origens alternativas (como o Windows Update, Microsoft Windows Server Update Services ou compartilhamentos UNC) para a atualização de definição inicial em computadores cliente**  

     Escolha **True** ou **Sim** se você quiser que o Configuration Manager para instalar somente a atualização de definição inicial em computadores cliente. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda de rede durante a instalação inicial da atualização das definições.  

##  <a name="hardware-inventory"></a>Inventário de Hardware  

-   **Tamanho máximo do ficheiro MIF personalizado (KB)**  

     Especifique o tamanho máximo, em quilobytes, permitidos para cada arquivo de formato MIF (Management Information) personalizado que será coletado de um cliente durante um ciclo de inventário de hardware. Se algum arquivo MIF exceder este tamanho, o inventário de hardware do Configuration Manager não processará-los. Você pode especificar um tamanho de 1 e 5.000 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro de dados de inventário de hardware normal.  

    > [!NOTE]  
    >  Essa configuração está disponível apenas nas configurações do cliente padrão.  

-   **Classes de inventário de hardware**  

     No Configuration Manager, você pode estender as informações de hardware que coleta dos clientes sem editar manualmente o arquivo SMS_def MOF. Escolha **definir Classes** se você quiser estender o inventário de hardware do Configuration Manager. Para obter mais informações, consulte [como configurar o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Recolher ficheiros MIF**  

     Use essa configuração para especificar se deseja coletar arquivos MIF de clientes do Configuration Manager durante o inventário de hardware.  

     Para um arquivo MIF seja coletado pelo inventário de hardware, ele deverá no local correto no computador cliente. Por padrão, os arquivos estão localizados da seguinte maneira:  

    -   Arquivos IDMIF devem estar na pasta Windows\System32\CCM\Inventory\Idmif.  

    -   Arquivos NOIDMIF devem estar na pasta Windows\System32\CCM\Inventory\Noidmif.  

    > [!NOTE]  
    >  Essa configuração está disponível apenas nas configurações do cliente padrão.

-   **Máximo de atraso aleatório**

    A coleção de informações de hardware é aleatória em até quatro horas para que a operação não ocorrer simultaneamente em todos os clientes. Você pode definir o atraso máximo para restringir o tempo durante o qual a operação ocorre.      

##  <a name="metered-internet-connections"></a>Conexões de Internet limitadas  
 Você pode gerenciar como computadores cliente Windows 8 se comunicam com sites do Configuration Manager quando eles usam conexões de Internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

> [!NOTE]  
>  Nos seguintes cenários, a definição do cliente configurado não é aplicada a computadores cliente com Windows 8:  
>   
> -   O computador estiver em uma conexão de dados móveis: O cliente do Configuration Manager não executa as tarefas que exigem que os dados devem ser transferidos para sites do Configuration Manager.  
> -   As propriedades de conexão de rede do Windows são configuradas como ilimitadas: O cliente do Configuration Manager se comporta como se esta é uma conexão de Internet ilimitada e por isso transfere os dados para os sites do Configuration Manager.  

-   **Comunicação com clientes em ligações à Internet com tráfego limitado**  

     A partir da lista pendente, escolha uma das seguintes opções para computadores cliente com Windows 8:  

    -   **Permitir**: Todas as comunicações de cliente são permitidas pela conexão de Internet limitado, a menos que o dispositivo do cliente está usando uma conexão de dados móvel.  

    -   **Limite de**: Somente as comunicações do cliente seguintes são permitidas pela conexão de Internet limitada:  

        -   Obtenção de políticas de cliente  

        -   Mensagens de estado de cliente a enviar para o site  

        -   Pedidos de instalação de software utilizando o Catálogo de Aplicações  

        -   Implementações necessárias (quando for atingido o prazo de instalação)  

        > [!IMPORTANT]  
        >  Se um utilizador iniciar a instalação de software a partir do Centro de Software ou do Catálogo de Aplicações, estas operações serão sempre permitidas, independentemente das definições de ligação de Internet limitada.  

         Se o limite de transferência de dados for alcançado para a conexão de Internet limitado, o cliente não tenta se comunicar com sites do Configuration Manager.  

    -   **Bloco**: O cliente do Configuration Manager não tentará se comunicar com sites do Configuration Manager quando ele está em uma conexão de Internet limitado. Este é o valor predefinido.  

##  <a name="power-management"></a>Gestão de energia  

-   **Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia**  

     Na lista suspensa, escolha **True** ou **Sim** permitir que os usuários do Centro de Software excluam o computador de qualquer configurado as configurações de gerenciamento de energia.  

-   **Ativar reativação proxy**  

     Especifique **Sim** para completar a definição de reativação por LAN do site quando estiver configurado para pacotes unicast.  

     Para obter mais informações sobre o proxy de ativação, consulte [planejar como ativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Não ative a reativação proxy numa rede de produção sem compreender primeiro como funciona e avaliá-la num ambiente de teste.  

-   **Reativar o número da porta proxy (UDP)**  

     Mantenha o valor padrão para o número da porta que os computadores usam para enviar pacotes de ativação para computadores em suspensão de gerenciados. Ou então, altere o número para um valor de sua escolha.  

     O número de porta especificado aqui é configurado automaticamente para clientes que executam o Firewall do Windows quando você usar o **exceção do Firewall do Windows para o proxy de ativação** opção. Se os clientes tiverem outra firewall em execução, terá de a configurar manualmente para permitir o número da porta UDP especificado para esta definição.  

-   **Reativar por LAN o número da porta (UDP)**  

     Mantenha o valor padrão 9, a menos que você tiver alterado o número de porta Wake On LAN (UDP) no **portas** guia do site **propriedades**.  

    > [!IMPORTANT]  
    >  Este número tem de corresponder ao número nas **Propriedades**do site. Se você alterar esse número em um só lugar, ele não será atualizado automaticamente em outro lugar.  

##  <a name="remote-tools"></a>Ferramentas remotas  

-   **Ativar Controlo Remoto nos clientes** e **Perfis de exceção de firewall**  

     Escolha se o controle remoto do Configuration Manager está habilitado para todos os computadores cliente que recebem essas configurações de cliente. Escolha **configurar** para habilitar o controle remoto. Opcionalmente, defina configurações de firewall para permitir o controle remoto funcione em computadores cliente.  

     Por predefinição, o controlo remoto encontra-se desativado.  

    > [!IMPORTANT]  
    >  Se as definições da firewall não estiverem configuradas, o controlo remoto poderá não funcionar corretamente.  

-   **Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software**  

     Escolha se os usuários podem alterar as opções de controle remoto do Centro de Software.  

-   **Permitir o Controlo Remoto de um computador autónomo**  

     Escolha se um administrador pode usar o controle remoto para acessar um computador cliente que está desconectado ou bloqueado. Apenas um computador conectado e desbloqueado pode ser controlado remotamente quando essa configuração é desabilitada.  

-   **Solicitar ao utilizador permissão do Controlo Remoto**  

     Escolha se o computador cliente mostrará uma mensagem que pede a permissão do usuário antes de permitir uma sessão de controle remoto.  

-   **Conceder permissão de Controlo Remoto ao grupo de Administradores local**  

     Escolha se os administradores locais no servidor que inicia a conexão de controle remoto podem estabelecer sessões de controle remoto em computadores cliente.  

-   **Nível de acesso permitido**  

     Especifica o nível de acesso de controlo remoto que será permitido. Pode escolher entre:  

    -   Controlo total  

    -   Visualizar apenas  

    -   Nenhum  

-   **Visualizadores permitidos**  

     Escolha **definir visualizadores** para abrir o **definir a configuração do cliente** caixa de diálogo caixa e especifique os nomes de usuários do Windows que podem estabelecer sessões de controle remoto em computadores cliente.  

-   **Mostrar ícone de notificação de sessão na barra de tarefas**  

     Escolha esta opção para mostrar um ícone na barra de tarefas do cliente de computadores para indicar que uma sessão de controle remoto está ativa.  

-   **Mostrar barra de ligação da sessão**  

     Escolha esta opção para mostrar a barra de conexão de sessão de alta visibilidade no cliente computadores para indicar que uma sessão de controle remoto está ativa.  

-   **Reproduzir um som no cliente**  

     Escolha esta opção para usar som para indicar quando uma sessão de controle remoto está ativa em um computador cliente. Poderá ser reproduzido um som quando a sessão for ligada ou desligada, ou ser reproduzido um som repetidamente durante a sessão.  

-   **Gerir definições da Assistência Remota não solicitada**  

     Escolha esta opção para permitir que o Configuration Manager gerenciar sessões de assistência remota não solicitada.  

     Em uma sessão de assistência remota não solicitada, o usuário no computador cliente não solicitou a assistência para iniciar a sessão.  

-   **Gerir definições da Assistência Remota solicitada**  

     Escolha esta opção para permitir que o Configuration Manager gerenciar sessões de assistência remota solicitada.  

     Em uma sessão de assistência remota solicitada, o usuário no computador cliente enviou uma solicitação para o administrador de assistência remota.  

-   **Nível de acesso para a Assistência Remota**  

     Escolha o nível de acesso para atribuir a sessões de assistência remota iniciadas no console do Configuration Manager.  

    > [!NOTE]  
    >  O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

-   **Gerir definições de Ambiente de Trabalho Remoto**  

     Escolha esta opção para permitir que o Configuration Manager gerencie sessões da área de trabalho remota para computadores.  

-   **Permitir que os visualizadores autorizados estabeleçam ligação utilizando a ligação ao Ambiente de Trabalho Remoto**  

     Escolha esta opção para permitir que os usuários especificados na lista de visualizadores autorizados a serem adicionados ao grupo de usuário local de área de trabalho remota em computadores cliente.  

-   **Exigir autenticação de nível de rede nos computadores com o sistema operativo Windows Vista e versões posteriores**  

     Escolha esta opção mais segura, se você quiser usar a autenticação de nível de rede para estabelecer conexões de área de trabalho remota para computadores cliente que executam o Windows Vista ou posterior. Autenticação de rede requer menos recursos do computador remoto inicialmente porque termina de autenticação do usuário antes de estabelecer uma conexão de área de trabalho remota. Este método é mais seguro porque pode ajudar a proteger o computador contra utilizadores mal intencionados ou software malicioso, reduzindo o risco de ataques denial-of-service.  

## <a name="software-deployment"></a>Implementação de software  

-   **Agendar reavaliação das implementações**  

     Configure um agendamento para quando o Configuration Manager reavalia as regras de requisito para todas as implantações. O valor predefinido é a cada 7 dias.  

    > [!IMPORTANT]  
    >  É recomendável que você não altere esse valor para um valor menor do que o padrão. Isso pode afetar negativamente o desempenho de sua rede e dos computadores cliente.  

     Você também pode iniciar essa ação em um computador de cliente do Configuration Manager escolhendo a ação **ciclo de avaliação de implantação do aplicativo** do **ações** guia de **do Configuration Manager** no painel de controle.  

##  <a name="software-inventory"></a>Inventário de software  

-   **Inventariar detalhe de relatórios**  

     Especifica o nível de informações dos ficheiros a inventariar. Você pode inventariar detalhes sobre o arquivo, os detalhes sobre o produto associado com o arquivo, ou todas as informações sobre o arquivo.  

-   **Inventariar estes tipos de ficheiro**  

     Se você quiser especificar os tipos de arquivo para inventariar, escolha **definir tipos** e, em seguida, configure o seguinte no **definir a configuração do cliente** caixa de diálogo:  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente são aplicadas a um computador, o inventário que retorna cada configuração será mesclado.  

    -   Escolha o **novo** ícone para adicionar um novo tipo de arquivo para o inventário. Em seguida, especifique as seguintes informações no **propriedades de arquivo inventariado** caixa de diálogo:  

        -   **Nome**: Forneça um nome para o arquivo que você deseja inventariar. Você pode usar o * *\**  caractere para representar qualquer cadeia de caracteres de texto e o **?** para representar um único caráter. Por exemplo, se você deseja inventariar todos os arquivos com a extensão. doc, especifique o nome do arquivo  **\*. doc**.  

        -   **Local**: Escolha **definir** para abrir o **propriedades de caminho** caixa de diálogo. Você pode configurar o inventário de software para pesquisar todos os discos rígidos do cliente para o arquivo especificado, pesquisar um caminho especificado (por exemplo, **C:\Folder**), ou procurar uma variável especificada (por exemplo, *% windir %*). Você também pode pesquisar todas as subpastas no caminho especificado.  

        -   **Excluir arquivos criptografados e compactados**: Quando você escolhe essa opção, todos os arquivos que foram compactados ou criptografados não serão inventariados.  

        -   **Excluir arquivos na pasta Windows**: Quando você escolhe essa opção, todos os arquivos na pasta do Windows e suas subpastas não serão inventariados.  

    -   Escolha **Okey** para fechar o **propriedades de arquivo inventariado** caixa de diálogo.  

    -   Adicionar todos os arquivos que você deseja inventariar e, em seguida, escolha **Okey** para fechar o **definir a configuração do cliente** caixa de diálogo.  

-   **Recolher ficheiros**  

     Se você quiser coletar arquivos de computadores cliente, escolha **definir arquivos** e, em seguida, configure o seguinte:  

    > [!NOTE]  
    >  Se várias configurações personalizadas do cliente são aplicadas a um computador, o inventário que retorna cada configuração será mesclado.  

    -   No **definir a configuração do cliente** caixa de diálogo caixa, escolha o **novo** ícone para adicionar um arquivo a ser coletado.  

    -   Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

        -   **Nome**: Forneça um nome para o arquivo que você deseja coletar. Você pode usar o * *\**  caractere para representar qualquer cadeia de caracteres de texto e o **?** para representar um único caráter.  

        -   **Local**: Escolha **definir** para abrir o **propriedades de caminho** caixa de diálogo. Você pode configurar o inventário de software para pesquisar todos os discos rígidos do cliente para o arquivo que você deseja coletar, pesquisar um caminho especificado (por exemplo, **C:\Folder**), ou procurar uma variável especificada (por exemplo, *% windir %*). Você também pode pesquisar todas as subpastas no caminho especificado.  

        -   **Excluir arquivos criptografados e compactados**: Quando você escolhe essa opção, todos os arquivos que foram compactados ou criptografados não serão coletados.  

        -   **Pare a coleta de arquivo quando o tamanho total dos arquivos excede (KB)**: Especifique o tamanho do arquivo (em quilobytes) depois do qual nenhum dos arquivos especificados em **nome** serão coletados.  

          > [!NOTE]  
          >  O servidor do site coleta as cinco versões alteradas mais recentemente de arquivos coletados e as armazena no  *&lt;diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol directory. Se um ficheiro não tiver sido alterado desde a recolha do último inventário de software, o ficheiro não será novamente recolhido.  
          >   
          >  Inventário de software não coletar arquivos maiores que 20 MB.  
          >   
          >  O valor **tamanho máximo para todos os arquivos coletados (KB)** no **definir a configuração do cliente** caixa de diálogo mostra o tamanho máximo de todos os arquivos coletados. Quando este tamanho for atingido, a recolha de ficheiros será interrompida. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

          > [!IMPORTANT]
          >  Se configurar o inventário de software para recolher muitos ficheiros de grandes dimensões, poderá afetar negativamente o desempenho da rede e do servidor de site.  

        Para obter informações sobre como exibir arquivos coletados, consulte [como usar o Gerenciador de recursos para exibir o inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Escolha **Okey** para fechar o **propriedades do arquivo coletado** caixa de diálogo.  

    -   Adicionar todos os arquivos que você deseja coletar e, em seguida, escolha **Okey** para fechar o **definir a configuração do cliente** caixa de diálogo.  

-   **Definir Nomes**  

     Durante o inventário de software, são obtidos nomes de fabricantes e de produtos a partir das informações de cabeçalho dos ficheiros instalados nos clientes do site. Como nem sempre esses nomes se encontram padronizados nas informações de cabeçalho dos ficheiros, ao visualizar as informações do inventário de software no Explorador de Recursos ou ao executar consultas poderão, por vezes, ser apresentadas diversas versões do mesmo nome de fabricante ou produto. Se você deseja padronizar esses nomes para exibição, escolha **definir nomes** e, em seguida, configure o seguinte no **definir a configuração do cliente** caixa de diálogo:  

    -   **Tipo de nome**: Inventário de software coleta informações sobre produtos e fabricantes. Na lista suspensa, escolha se deseja configurar nomes de exibição para um **fabricante** ou um **produto**.  

    -   **Nome de exibição**: Especifique o nome de exibição que você deseja usar no lugar dos nomes na **nomes inventariados** lista. Você pode escolher o **novo** ícone para especificar um novo nome para exibição.  

    -   **Nomes inventariados**: Escolha o **novo** ícone para adicionar um novo nome inventariado que será substituído no inventário de software, o nome escolhido no **nome de exibição** lista. Poderá adicionar vários nomes a substituir.  

##  <a name="software-updates"></a>Atualizações de software  

-   **Ativar atualizações de software nos clientes**  

     Use essa configuração para habilitar as atualizações de software em clientes do Configuration Manager. Quando você desabilitar essa configuração, o Configuration Manager removerá as políticas de implantação existente do cliente. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

    > [!IMPORTANT]  
    >  Quando você desabilitar essa configuração, as políticas de NAP e conformidade que se baseiam na configuração de dispositivo para as atualizações de software não funcionarão mais.  

-   **Agendamento da análise de atualização de software**  

     Utilize esta definição para especificar a frequência com que o cliente inicia uma análise de avaliação da compatibilidade das atualizações de software. A análise de avaliação da compatibilidade determina o estado das atualizações de software no cliente (por exemplo, necessária ou instalada). Para obter mais informações sobre avaliação de conformidade, consulte [avaliação de conformidade das atualizações de Software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Por padrão, um agendamento simples é usado e a verificação de conformidade é iniciada a cada 7 dias. Poderá optar por criar um agendamento personalizado para especificar uma data e hora de início exatas, optar pela utilização da hora local ou UTC e configurar o intervalo periódico para um dia da semana específico.  

    > [!NOTE]  
    >  Se você especificar um intervalo de menos de 1 dia, Configuration Manager automaticamente padrão será 1 dia.  

    > [!WARNING]  
    >  A hora de início real em computadores cliente é a hora de início mais um período de tempo aleatório de até 2 horas. Isto evita que os computadores cliente iniciem a análise e estabeleçam ligação ao Windows Server Update Services (WSUS) no servidor ativo de ponto de atualização de software ao mesmo tempo.  

-   **Agendar a reavaliação de implementação**  

     Use essa configuração para configurar a frequência na qual o agente de cliente de atualizações de Software reavalia as atualizações de software para status de instalação em computadores cliente do Configuration Manager. Quando atualizações de software que foram instaladas anteriormente não são encontradas em computadores cliente e ainda são necessárias, elas são reinstaladas.

     O agendamento de reavaliação de implantação deve ser ajustado com base na política da empresa para conformidade de atualização de software, se os usuários têm a capacidade de desinstalar as atualizações de software e assim por diante. Lembre-se de que cada ciclo de reavaliação de implantação resulte em alguma atividade da CPU do computador cliente e de rede. Por padrão, um agendamento simples é usado e a verificação de reavaliação de implantação é iniciada a cada 7 dias.  

    > [!NOTE]  
    >  Se você especificar um intervalo de menos de 1 dia, Configuration Manager automaticamente padrão será 1 dia.  

-   **Quando qualquer prazo de implementação da atualização de software é alcançado, instale todas as outras implementações de atualização de software com prazo a terminar no período de tempo especificado**  

     Utilize esta definição para instalar todas as atualizações de software em implementações necessárias com prazos incluídos num determinado período de tempo. Quando um prazo é alcançado para um software necessário atualizar a implantação, a instalação é iniciada em clientes das atualizações de software na implantação. Esta definição determina se deve ser iniciada também a instalação das atualizações de software definidas noutras implementações necessárias com um prazo configurado no período de tempo especificado.  

     Utilize esta configuração para agilizar a instalação da atualização de software para atualizações de software necessárias, aumentar potencialmente a segurança, reduzir potencialmente a apresentação de notificações e reduzir potencialmente os reinícios do sistema em computadores cliente. Por predefinição, esta definição não está ativada.  

-   **Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas**  

     Utilize esta definição para especificar o intervalo de tempo da definição anterior. Pode introduzir um valor de 1 a 23 horas e de 1 a 365 dias. Por predefinição, esta definição está configurada para 7 dias.  

-   **Habilitar a instalação dos arquivos de instalação expressa em clientes**

-   **Porta usada para baixar o conteúdo de arquivos de instalação do Express**

-   **Habilitar o gerenciamento do Office 365 cliente novamente** Use essa configuração para habilitar o gerenciamento do agente de cliente do Office 365. Quando você define o valor como **Sim**, ele permite que você definir as configurações de instalação do Office 365, baixar arquivos do Office conteúdo entrega CDNs (redes) e implantar os arquivos como um aplicativo no Configuration Manager.

##  <a name="user-and-device-affinity"></a>Afinidade de dispositivo e de usuário  

-   **Limiar de utilização de afinidade de dispositivo e utilizador (minutos)**  

     Especifique o número de minutos antes do Configuration Manager cria um mapeamento de afinidade de dispositivo de usuário.  

-   **Limiar de utilização de afinidade de dispositivo e utilizador (dias)**  

     Especifique o número de dias nos quais o limite de afinidade com base em uso é medido.  

    > [!NOTE]  
    >  Por exemplo, se **limite de uso de afinidade de dispositivo de usuário (minutos)** é especificado como **60** minutos e **limite de uso de afinidade de dispositivo de usuário (dias)** é especificado como **5** dias, o usuário deve usar o dispositivo por 60 minutos em um período de 5 dias para criar automaticamente uma afinidade de dispositivo de usuário.  

-   **Configurar automaticamente a afinidade de dispositivo e utilizador a partir dos dados de utilização**  

     Escolha **True** ou **Sim** para permitir que o Configuration Manager criar automaticamente afinidades de dispositivo com base nas informações de uso são coletadas de usuário.  

##  <a name="mobile-devices"></a>Dispositivos móveis  

-   **Perfis de inscrição de dispositivos móveis**  

     Para poder configurar esta definição, deve primeiro configurar como **Verdadeiro** a definição de utilizador de dispositivo móvel **Permitir aos utilizadores a inscrição de dispositivos móveis**. Em seguida, você pode escolher **definir perfil** para especificar um perfil de registro que contém informações sobre o modelo de certificado a ser usado durante o processo de registro, o site que tem um ponto de registro e ponto proxy do registro e o site que irá gerenciar o dispositivo após o registro.  

    > [!IMPORTANT]  
    >  Certifique-se de que configurou um modelo de certificado para utilizar na inscrição do dispositivo móvel antes de configurar esta opção.  

##  <a name="enrollment"></a>Inscrição  

-   **Perfis de inscrição de dispositivos móveis**  

     Para poder configurar esta definição, deve primeiro configurar como **Sim** a definição de utilizador de inscrição **Permitir aos utilizadores a inscrição de dispositivos móveis e computadores Mac**. Em seguida, você pode escolher **definir perfil** para especificar um perfil de registro que contém informações sobre o modelo de certificado a ser usado durante o processo de registro, o site que tem um ponto de registro e ponto proxy do registro e o site que irá gerenciar o dispositivo após o registro.  

    > [!IMPORTANT]  
    >  Certifique-se de que configurou um modelo de certificado para utilizar na inscrição do dispositivo móvel ou na inscrição do certificado do cliente Mac antes de configurar esta opção.  

## <a name="user-and-device-affinity"></a>Afinidade de dispositivo e de usuário  

-   **Permitir ao utilizador a definição dos seus dispositivos primários**  

     Especifique se os usuários têm permissão para identificar seus próprios dispositivos primários no **meus dispositivos** guia do catálogo de aplicativos.  

