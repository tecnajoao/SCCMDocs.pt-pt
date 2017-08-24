---
title: "Definições de cliente | Microsoft Docs"
description: "Escolha as definições de cliente utilizando a consola de administrador no System Center Configuration Manager."
ms.custom: na
ms.date: 08/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a8233c361e1a78b14a02f328da445814624e38d8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as definições de cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Todas as definições de cliente no System Center Configuration Manager são geridas na consola do Configuration Manager do **as definições de cliente** no nó de **administração** área de trabalho. O Configuration Manager inclui um conjunto de predefinições. Quando alterar as predefinições de cliente, estas definições são aplicadas a todos os clientes na hierarquia. Também pode configurar definições de cliente personalizadas, que substituem as predefinições do cliente, ao atribuí-las a coleções. Para obter mais informações sobre como configurar definições do cliente, veja [Como configurar definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

Muitas das definições de cliente são facilmente compreensíveis. Outras pessoas são descritas aqui.  

## <a name="background-intelligent-transfer-service"></a>Serviço de transferência inteligente em segundo plano  

-   **Limitar a largura de banda de rede máxima para transferências BITS em segundo plano**  

   Quando esta opção é **verdadeiro** ou **Sim**, os clientes irão utilizar a limitação de largura de banda do BITS.  

-   **Hora de início da janela de limitação**  

   Especifique a hora de início local para a janela de limitação do BITS.  

-   **Hora de fim da janela de limitação**  

   Especifique a hora de fim local para a janela de limitação do BITS. Se igual a **hora de início da janela de limitação**, limitação do BITS é sempre ativado.  

-   **Velocidade máxima de transferência durante a janela de limitação (Kbps)**  

   Especifique a velocidade máxima de transferência que os clientes podem utilizar durante a janela.  

-   **Permitir transferências BITS fora da janela de limitação**  

   Escolha esta opção para permitir que os clientes do Configuration Manager utilizar as definições de BITS separadas fora da janela especificada.  

-   **Velocidade máxima de transferência fora da janela de limitação (Kbps)**  

   Especifique a velocidade máxima de transferência que os clientes utilizam fora os BITS da janela de limitação, quando tiver optado por permitir fora da janela de limitação do BITS.  

## <a name="client-cache-settings"></a>Definições de cache do cliente

- **Configurar o BranchCache**

  A partir da versão 1606, utilize esta definição para configurar o computador cliente para [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir a colocação em cache de BranchCache no cliente, defina **ativar BranchCache** para **Sim**.

- **Ativar o BranchCache**

Permite que o BranchCache nos computadores cliente.

- **Tamanho máximo da cache do BranchCache (percentagem do disco)**.

- **Configurar o tamanho da cache do cliente**

  A cache do cliente em computadores Windows armazena ficheiros temporários utilizados para instalar aplicações e programas. Escolha **Sim** , em seguida, especifique:
    - **Tamanho máximo da cache** (em megabytes). 
    - **Tamanho máximo da cache** (percentagem do disco).
Pode expandir o tamanho da cache do cliente para o tamanho máximo em MB ou percentagem do disco, **que for menor**. Se esta opção é **não**, o tamanho predefinido é 5,120 MB.

- **Ativar cliente do Configuration Manager no SO completo para partilhar conteúdo**

Permite o elemento de cache para clientes do Configuration Manager. Em seguida, especifique as informações de porta que o cliente comunica com o computador de ponto a ponto. O Configuration Manager irá configurar automaticamente regras de Firewall do Windows para permitir que este tráfego. Se utilizar uma firewall diferente, tem de configurar manualmente as regras para permitir que este tráfego.




## <a name="client-policy"></a>Política do cliente  

-   **Intervalo de consulta da política de cliente (minutos)**  

   Especifique a frequência os seguintes clientes do Configuration Manager transferirem a política de cliente:  

  -   Computadores Windows (por exemplo, ambientes de trabalho, servidores, computadores portáteis)  

  -   Dispositivos móveis que inscreve do Configuration Manager  

  -   Computadores Mac  

  -   Computadores com o Linux ou UNIX  

-   **Ativar consulta de política de utilizador nos clientes**  

   Quando definir esta opção **verdadeiro** ou **Sim**, e o Configuration Manager possui [detetado o utilizador](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), os clientes em computadores recebem aplicações e programas destinados ao utilizador com sessão iniciada.  

   Uma vez que o catálogo de aplicações recebe a lista de software disponível para utilizadores do servidor do site, esta definição não tem de ser **verdadeiro** ou **Sim** para os utilizadores possam visualizar e pedir aplicações a partir do catálogo de aplicações. Porém, se esta definição é **falso** ou **não**, o seguinte elemento não funcionará quando os utilizadores utilizam o catálogo de aplicações:  

  -   Os utilizadores não podem instalar as aplicações que veem no Catálogo de Aplicações.  

  -   Os utilizadores não verão notificações sobre os pedidos de aprovação de aplicação. Em vez disso, devem atualizar o Catálogo de Aplicações e verificar o estado de aprovação.  

  -   Os utilizadores não receberão revisões nem atualizações para as aplicações que são publicadas no catálogo de Catálogo de Aplicações. Mas, verão as alterações às informações de aplicação no catálogo de aplicações.  

  -   Se remover a implementação de uma aplicação depois de o cliente ter instalado a aplicação a partir do Catálogo de Aplicações, os clientes continuam a verificar se a aplicação está instalada até um máximo de 2 dias.  

   Além disso, quando esta definição for **falso** ou **não**, os utilizadores não irão receber as aplicações necessárias implementadas para utilizadores ou quaisquer outras tarefas de gestão em políticas de utilizador.  

   Esta definição aplica-se aos utilizadores cujos computadores estão na intranet e Internet. Tem de ser **verdadeiro** ou **Sim** se também pretender ativar políticas de utilizador na Internet.  

-   **Ativar pedidos da política do utilizador dos clientes Internet**  

   Quando o cliente e o site estão configurados para gestão de clientes baseados na Internet e configurar esta opção como **verdadeiro** ou **Sim** e ambos os procedimentos seguintes aplicam-se condições, os utilizadores recebem a política de utilizador quando os respetivos computadores estão na Internet:  

  -   O **ativar consulta de política de utilizador nos clientes** definição de cliente é **verdadeiro**, ou **ativar política de utilizador nos clientes** é **Sim**.  

  -   O ponto de gestão baseado na Internet autentica com êxito o utilizador através da autenticação do Windows (Kerberos ou NTLM).  

   Se deixar esta opção como **falso** ou **não**, ou qualquer uma da falha de condições, um computador com o será Internet receber apenas políticas de computador. Neste cenário, os utilizadores ainda podem ver, pedir e instalar aplicações a partir de um Catálogo de Aplicações baseado na Internet. Se esta definição é **falso** ou **não** mas **ativar consulta de política de utilizador nos clientes** é **verdadeiro** ou **ativar política de utilizador nos clientes** é **Sim**, os utilizadores não irão receber políticas de utilizador, até que o computador está ligado à intranet.  

   Para obter mais informações sobre a gestão de clientes na Internet, consulte [considerações sobre comunicações do cliente da Internet ou numa floresta não fidedigna](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) no [comunicações entre pontos finais no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Os pedidos de aprovação de aplicações dos utilizadores não necessitam de políticas de utilizador ou de autenticação de utilizador.  

##  <a name="compliance-settings"></a>Definições de compatibilidade  

-   **Agendar avaliação de compatibilidade**  

     Escolha **agenda** para criar a agenda predefinida que é apresentada aos utilizadores quando implementam uma linha de base de configuração. Este valor pode ser configurado para cada linha de base na caixa de diálogo **Implementar Linhas de Base de Configuração** .  

-   **Ativar Dados e Perfis de Utilizador**  

     Escolha **Sim** se pretender implementar [perfis e dados de utilizador](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) itens de configuração para computadores com Windows 8 na sua hierarquia.  

## <a name="computer-agent"></a>Agente do computador  

-   **Ponto de Web sites Predefinido do Catálogo de Aplicações**  

     O Configuration Manager utiliza esta definição para ligar utilizadores ao catálogo de aplicações a partir do Centro de Software. Pode especificar um servidor que aloja o ponto de Web sites do Catálogo de Aplicações através do nome NetBIOS ou FQDN, especificar deteção automática ou especificar um URL para implementações personalizadas. Na maioria dos casos, a deteção automática é a melhor opção uma vez que oferece as seguintes vantagens:  

    -   Os clientes recebem automaticamente um ponto de Web site do catálogo de aplicações do respetivo site, se o site tiver um ponto de Web site do catálogo de aplicações.  

    -   Aplicação catálogo pontos do Web site da intranet que estão configurados para HTTPS são dada preferência por aqueles que não estão configurados para HTTPS. Isto ajuda a proteger contra um servidor não autorizado.

    -   Quando os clientes são configurados para gestão de clientes baseados na intranet e baseado na Internet, recebem um ponto de Web site do catálogo de aplicações baseado na Internet quando estão na Internet e um ponto de Web site do catálogo de aplicações baseado na intranet quando estão na intranet.  

     A deteção automática não garante que os clientes receberão um ponto de Web sites do Catálogo de Aplicações que esteja mais próximo deles. Pode decidir não utilizar **Detetar automaticamente** pelos seguintes motivos:  

     -   Pretende configurar manualmente o servidor mais próximo dos clientes ou certificar-se de que não ligam a um servidor através de uma ligação de rede lenta.  

     -   Pretende controlar que clientes ligam ao servidor. Esta configuração pode ser para fins de teste, desempenho ou por razões empresariais.  

     -   Não vai querer esperar 25 horas ou esperar por uma alteração de rede para que os clientes sejam configurados com um ponto de Web sites do Catálogo de Aplicações.  

     Se, especifique o ponto de Web site do catálogo de aplicações em vez de utiliza a deteção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Isto ajuda a reduzir a probabilidade de que os utilizadores serão solicitado que as credenciais quando se ligam ao catálogo de aplicações na intranet. Para utilizar o nome NetBIOS, tem de aplicar as seguintes condições:  

     -   O nome NetBIOS é especificado nas propriedades do ponto de Web sites do Catálogo de Aplicações.  

     -   Utilizar o WINS ou todos os clientes estão no mesmo domínio que o ponto de Web site do catálogo de aplicações.  

     -   O ponto de Web site do catálogo de aplicações está configurado para ligações de cliente HTTP, ou está configurado para ligações de cliente HTTPS e o certificado de servidor web com o nome de NetBIOS.  

     Normalmente, os utilizadores recebem um pedido de credenciais quando o URL tem um FQDN mas não quando o URL é um nome NetBIOS. É expectável que os utilizadores recebam sempre esse pedido quando ligam a partir da Internet, uma vez que esta ligação tem de utilizar o FQDN da Internet. Quando os utilizadores recebem o pedido de credenciais quando estão na Internet, assegure-se de que o servidor que executa o ponto de Web sites do Catálogo de Aplicações pode ligar a um controlador de domínio para a conta de utilizador, de forma que o utilizador possa ser autenticado através de Kerberos.  

    > [!NOTE]  
    >  Como funciona a deteção automática:  
    >   
    >  O cliente faz um pedido de localização de serviço para um ponto de gestão. Se houver um ponto de Web sites do Catálogo de Aplicações no mesmo site que o cliente, este servidor é atribuído ao cliente como o servidor do Catálogo de Aplicações a utilizar. Quando estiver disponível mais do que um ponto de Web site do catálogo de aplicações no site, um servidor ativado para HTTPS tem precedência sobre um servidor que não está ativado para HTTPS. Após esta filtragem, todos os clientes recebem um dos servidores a utilizar como catálogo de aplicações; O Configuration Manager não não-balanceamento de carga entre múltiplos servidores. Quando o site do cliente não tem um ponto de Web site do catálogo de aplicações, o ponto de gestão devolve não deterministicamente um ponto de Web site do catálogo de aplicações da hierarquia.  
    >   
    >  Quando o cliente está na intranet, se o ponto de Web site do catálogo de aplicações que escolheu é configurado com um nome de NetBIOS para o URL do catálogo de aplicações, os clientes recebem este nome de NetBIOS em vez do FQDN da intranet. Quando o cliente é detetado na Internet, apenas o FQDN da Internet é atribuído ao cliente.  
    >   
    >  O cliente efetua este pedido de localização de serviço em 25 horas ou sempre que detetar uma alteração de rede. Por exemplo, se o cliente passar da intranet para a Internet, e conseguir localizar um ponto de gestão baseado na Internet, o ponto de gestão baseado na Internet atribui os servidores do ponto de Web sites do Catálogo de Aplicações baseado na Internet aos clientes.  

-   **Adicionar Web site predefinido do Catálogo de Aplicações à zona de sites fidedignos do Internet Explorer**  

     Se esta opção é **verdadeiro** ou **Sim**, o atual predefinição catálogo de aplicações Web site URL é adicionado automaticamente à zona sites fidedignos no Internet Explorer dos clientes.  

     Esta definição garante que a definição do Internet Explorer para o Modo Protegido não está ativada. Se o modo protegido estiver ativado, o cliente do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações. Por predefinição, a zona de sites fidedignos também suporta o início de sessão de utilizador para o Catálogo de Aplicações, que requer autenticação do Windows.  

     Se deixar esta opção como **falso**, clientes do Configuration Manager poderão não conseguir instalar aplicações a partir do catálogo de aplicações, a menos que estas definições do Internet Explorer estão configuradas noutra zona para o URL do catálogo de aplicações que os clientes utilizam.  

    > [!NOTE]  
    >  Sempre que o Configuration Manager adiciona um catálogo de aplicações predefinido para a zona sites fidedignos, o Gestor de configuração remove um URL de catálogo de aplicações predefinido anterior que o Configuration Manager adicionou, antes de adicionar uma nova entrada.  
    >   
    >  O Configuration Manager não é possível adicionar o URL, se já estiver especificado das zonas de segurança. Neste cenário, tem de remover o URL da outra zona ou configurar manualmente as definições do Internet Explorer necessárias.  

-   **Permitir que as aplicações Silverlight sejam executadas em modo de confiança elevada**  

     Esta definição tem de ser **Sim** se os utilizadores executem o cliente do Configuration Manager e utilizar o catálogo de aplicações.  

     Se alterar esta definição, ela tem efeito assim que os utilizadores carregarem o respetivo browser ou atualizarem a respetiva janela do browser atualmente aberta.  

     Para obter mais informações sobre esta definição, consulte [certificados do Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) no [segurança e privacidade para gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nome da organização apresentada no Centro de Software**  

     Escreva o nome que os utilizadores visualizam no Centro de Software. Estas informações de imagem corporativa ajudam os utilizadores a identificar esta aplicação como uma origem fidedigna.  

-   **Utilizar o novo Centro de Software**  

     Se estiver ativada, todos os computadores cliente visados por estas definições de cliente irão utilizar o novo Centro de Software. Centro de software mostra as aplicações disponíveis ao utilizador que foram anteriormente acessíveis apenas o catálogo de aplicações dependente do Silverlight.  

     O ponto de Web site do catálogo de aplicações e serviço web do catálogo de aplicações do ponto de sistema de sites funções ainda são necessárias para aplicações disponíveis ao utilizador a aparecer no Centro de Software.  

     Para obter mais informações, veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Permissões de Instalação**  

    > [!WARNING]  
    >  Esta definição aplica-se ao Catálogo de Aplicações e ao Centro de Software. Esta definição não produz efeitos quando os utilizadores usam o portal da empresa.  

     Configure a forma como os utilizadores podem iniciar a instalação de software, atualizações de software e sequências de tarefa:  

    -   **Todos os utilizadores**: Os utilizadores com sessão iniciados num computador cliente com qualquer permissão, exceto convidado, podem iniciar a instalação de software, atualizações de software e sequências de tarefas.  

    -   **Apenas os administradores**: Os utilizadores com sessão iniciados num computador cliente tem de ser membro do grupo Administradores local para iniciar a instalação de software, atualizações de software e sequências de tarefas.  

    -   **Apenas administradores e utilizadores primários**: Os utilizadores com sessão iniciados num computador cliente tem de ser um membro do grupo local de administradores ou utilizadores primários do computador para iniciar a instalação de software, atualizações de software e sequências de tarefas.  

    -   **Não existem utilizadores**: Nenhum utilizador com sessão iniciada num computador cliente poderá iniciar a instalação de software, atualizações de software e sequências de tarefas. As implementações necessárias para o computador são sempre instaladas na data limite. Os utilizadores não é possível iniciar a instalação de software a partir do catálogo de aplicações ou centro de Software.  

-   **Suspender a introdução do PIN do BitLocker após reiniciar**  

     Se a introdução do PIN do BitLocker estiver configurada nos computadores, esta opção permite contornar o requisito de introdução de um PIN quando o computador é reiniciado após uma instalação de software.  

    -   **Sempre**: O Configuration Manager suspende temporariamente o BitLocker após a instalação de software que requeira um reinício, iniciou um reinício do computador. Esta definição só se aplica a um reinício do computador que é iniciado pelo Configuration Manager e não suspende o requisito de introduzir o PIN do BitLocker quando o utilizador reinicia o computador. O requisito de introdução do PIN do BitLocker é retomado após o arranque do Windows.

    -   **Nunca**: O Configuration Manager não suspende o BitLocker no próximo arranque do computador após a instalação de software que requeira um reinício. Neste cenário, a instalação de software não ficará concluída enquanto o utilizador não introduzir o PIN para concluir o processo de arranque padrão e carregar o Windows.

-   **O software adicional gere a implementação de aplicações e atualizações de software**  

     Apenas deverá ativar esta opção nas seguintes condições:  

    -   Está a utilizar uma solução de fornecedor que necessita que esta definição seja ativada.  

    -   Utilizar o Configuration Manager software development kit (SDK) para gerir as notificações de agente do cliente e a instalação de aplicações e atualizações de software.  

    > [!WARNING]  
    >  Se escolher esta opção quando nenhuma destas condições aplicam-se, atualizações de software e as aplicações necessárias não são instaladas nos clientes. Esta definição não impede que os utilizadores instalar aplicações a partir do catálogo de aplicações ou impedir que os pacotes, programas e sequências de tarefas que está a ser instalado em computadores cliente.  

-   **Política de execução do PowerShell**  

     Configure a forma como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Estes scripts são frequentemente utilizados para deteção de itens de configuração para definições de compatibilidade. Também podem ser enviados numa implementação como um script padrão.  

    -   **Ignorar**: O cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que possam ser executados scripts não assinados.  

    -   **Restrito**: O cliente do Configuration Manager utiliza a configuração atual do Windows PowerShell no computador cliente. Esta configuração determina se podem executar scripts não assinados.  

    -   **Todas assinadas**: O cliente do Configuration Manager apenas executa scripts um fabricante fidedigno assinou-los. Esta restrição aplica-se de forma independente a partir da configuração atual do Windows PowerShell no computador cliente.  

     Esta opção necessita, pelo menos, o Windows PowerShell versão 2.0. A predefinição é **todas assinadas**.  

    > [!TIP]  
    >  Se os scripts não assinados falham para executar devido a esta definição de cliente, o Configuration Manager apresenta este erro das seguintes formas:  
    >   
    > -   ID de erro **0X87D00327** e a descrição **Script não está assinado** como um erro de estado de implementação no **monitorização** área de trabalho da consola do Configuration Manager.  
    > -   Códigos de erro e descrições dos **0X87D00327** e **Script não está assinado** ou **0X87D00320** e **o anfitrião do script ainda não foi instalado** com o tipo de erro de **erro de deteção** nos relatórios. Um exemplo é **detalhes de erros de itens de configuração numa linha de base de configuração para um recurso**.  
    > -   A mensagem **Script não está assinado (erro: 87D 00327; Origem: CCM)** no **DcmWmiProvider.log** ficheiro.  

-   **Mostrar notificações para novas implementações**  

     Escolha **Sim** se pretende apresentar uma notificação para implementações que tenham sido disponíveis a menos que uma semana.  Esta mensagem será apresentado sempre que o agente do cliente é iniciado.

-   **Desativar a aleatoriedade de prazos**  

     Esta definição determina se o cliente utiliza um atraso de ativação de até 2 horas para instalar atualizações de software necessárias quando o prazo for atingido. Por predefinição, o atraso de ativação está desativado.  

     Para cenários com infraestrutura de ambiente de trabalho virtual (VDI), este atraso pode ajudar a distribuir o processamento de CPU e a transferência de dados para um computador que disponha de várias máquinas virtuais que executam o cliente do Configuration Manager. Mesmo que não utilize VDI, se vários clientes instalarem as mesmas atualizações ao mesmo tempo, esta pode negativamente aumentar a utilização da CPU no servidor do site. Pode também mais lentos pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

     Se as atualizações de software necessárias tem de estar instaladas sem atrasos quando o prazo configurado for atingido, selecione **Sim** para esta definição.  

-   **Período de tolerância para aplicação após o prazo de implementação (horas)**

     Em alguns casos, pode querer dar aos utilizadores mais tempo para as implementações de aplicações de instalação necessária ou atualizações de software para além de qualquer prazos que configurou. Pode normalmente ser necessária quando um computador foi desativado por um longo período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização. Por exemplo, se um utilizador apenas tiver devolvido de férias, poderá ter de aguardar algum enquanto como uma aplicação em atraso implementações estão instaladas. Para ajudar a resolver este problema, pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

     Pode definir um período de tolerância de 1 a 120 horas. Esta definição é utilizada em conjunto com a propriedade de implementação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador**. Para obter mais detalhes, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).

##  <a name="computer-restart"></a>Reinício do computador  
 Quando especificar estas definições de reinício do computador, certifique-se de que o valor do intervalo de notificação temporária de reinício e de que o valor do intervalo final de contagem regressiva têm uma duração inferior à da janela de manutenção mais curta que estiver aplicada ao computador.  

 Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **Gerir o cliente do Endpoint Protection nos computadores cliente**  

     Escolha **verdadeiro** ou **Sim** se pretender gerir os clientes existentes do Endpoint Protection nos computadores na sua hierarquia.  

     Escolha esta opção se já tiver instalado o cliente do Endpoint Protection e pretender geri-lo com o Configuration Manager.  

     Além disso, escolha esta opção se pretender criar um script de desinstalação de uma solução antimalware, instalar o cliente do Endpoint Protection e implementar este script utilizando uma aplicação do Configuration Manager ou pacote e programa.  

-   **Instalar o cliente do Endpoint Protection nos computadores cliente**  

     Escolha **verdadeiro** ou **Sim** para instalar e ativar o cliente do Endpoint Protection nos computadores cliente onde ainda não estiver instalada.  

    > [!NOTE]  
    >  Se o cliente do Endpoint Protection já estiver instalado, escolher **falso** ou **não** não conseguir desinstalar o cliente do Endpoint Protection. Para desinstalar o cliente do Endpoint Protection, configure o **cliente gerir o Endpoint Protection nos computadores cliente** definição de cliente para **falso** ou **não**. Em seguida, implemente um pacote e programa para desinstalar o cliente do Endpoint Protection.  

-   **Para dispositivos Windows Embedded com filtros de escrita, consolidar a instalação de cliente do Endpoint Protection (necessita de reinicialização)**  

     Escolha **Sim** para desativar o filtro de escrita no dispositivo Windows Embedded e reiniciar o dispositivo. Esta opção consolida a instalação no dispositivo.  

     Se for especificado **Não** , o cliente será instalado numa sobreposição temporária que será eliminada quando o dispositivo for reiniciado. Neste cenário, o cliente do Endpoint Protection não será consolidado enquanto outra instalação não consolidar as alterações no dispositivo. Esta é a predefinição.  

-   **Suprimir quaisquer reinícios necessários após o cliente do Endpoint Protection está instalado**  

     Escolha **verdadeiro** ou **Sim** para suprimir um reinício do computador se for necessário depois do cliente do Endpoint Protection está instalado.  

    > [!IMPORTANT]  
    >  Se o cliente do Endpoint Protection requer um reinício do computador e esta definição **falso**, o computador será reiniciado independentemente das janelas de manutenção que tenham sido configuradas.  

-   **Permitido período de tempo que os utilizadores pode adiar um reinício necessário para concluir a instalação do Endpoint Protection (horas)**  

     Especifique o número de horas que os utilizadores podem adiar um reinício do computador, se necessário, depois do cliente do Endpoint Protection está instalado. Esta opção pode ser configurada apenas se o **suprimir reinícios de qualquer computador necessários após a instalação do cliente do Endpoint Protection** opção é **falso**.  

-   **Desativar origens alternativas (por exemplo, o Windows Update, Microsoft Windows Server Update Services ou partilhas UNC) para a atualização inicial da definição nos computadores cliente**  

     Escolha **verdadeiro** ou **Sim** se pretender que o Configuration Manager para instalar apenas a atualização inicial da definição nos computadores cliente. Esta definição pode ser útil para evitar ligações de rede desnecessárias e reduzir a largura de banda de rede durante a instalação inicial da atualização das definições.  

##  <a name="hardware-inventory"></a>Inventário de Hardware  

-   **Tamanho máximo do ficheiro MIF personalizado (KB)**  

     Especifica o tamanho máximo, em kilobytes, permitidos para cada ficheiro de formato MIF (Management Information Format) personalizado que irá ser recolhido a partir de um cliente durante um ciclo de inventário de hardware. Se os ficheiros MIF excederem este tamanho, o inventário de hardware do Configuration Manager não irá processá-los. Pode especificar um tamanho de 1 a 5.000 KB. Por predefinição, este valor é definido para 250 KB. Esta definição não afeta o tamanho do ficheiro de dados de inventário de hardware normal.  

    > [!NOTE]  
    >  Esta definição está disponível apenas nas predefinições do cliente.  

-   **Classes de inventário de hardware**  

     No Configuration Manager, pode expandir as informações de hardware recolhidas dos clientes sem necessitar de editar manualmente o ficheiro sms_def.mof. Escolha **definir Classes** se pretender expandir o inventário de hardware do Configuration Manager. Para obter mais informações, consulte [como configurar inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Recolher ficheiros MIF**  

     Utilize esta definição para especificar se pretende recolher ficheiros MIF de clientes do Configuration Manager durante o inventário de hardware.  

     Para um ficheiro MIF possa ser recolhido pelo inventário de hardware, é necessário no local correto no computador cliente. Por predefinição, os ficheiros estão localizados da seguinte forma:  

    -   Ficheiros IDMIF devem estar na pasta windows\system32\ccm\inventory\idmif.  

    -   Os ficheiros NOIDMIF devem estar na pasta windows\system32\ccm\inventory\noidmif.  

    > [!NOTE]  
    >  Esta definição está disponível apenas nas predefinições do cliente.

-   **Máximo de atraso aleatório**

    A recolha de informações de hardware é aleatória por até quatro horas para que a operação não ter ocorrido em simultâneo em todos os clientes. Pode definir o atraso máximo para restringir o tempo durante os quais ocorre a operação.      

##  <a name="metered-internet-connections"></a>Ligações de Internet com tráfego limitado  
 Pode gerir a forma como os computadores cliente Windows 8 comunicam com sites do Configuration Manager quando utilizam ligações de Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

> [!NOTE]  
>  Nos seguintes cenários, a definição do cliente configurado não é aplicada a computadores cliente com Windows 8:  
>   
> -   O computador estiver numa ligação de dados de roaming: O cliente do Configuration Manager não efetua as tarefas que exigem a dados a serem transferidos para sites do Configuration Manager.  
> -   As propriedades de ligação de rede do Windows estão configuradas como não limitadas: O cliente do Configuration Manager comporta-se como se esta é uma ligação de Internet não limitada e, por isso, transfere dados para os sites do Configuration Manager.  

-   **Comunicação com clientes em ligações à Internet com tráfego limitado**  

     A partir da lista pendente, escolha uma das seguintes opções para computadores cliente com Windows 8:  

    -   **Permitir**: Todas as comunicações de cliente são permitidas através da ligação de Internet limitada, a menos que o dispositivo cliente está a utilizar uma ligação de dados de roaming.  

    -   **Limite**: Apenas as seguintes comunicações de cliente serão permitidas através da ligação à Internet com tráfego limitado:  

        -   Obtenção de políticas de cliente  

        -   Mensagens de estado de cliente a enviar para o site  

        -   Pedidos de instalação de software utilizando o Catálogo de Aplicações  

        -   Implementações necessárias (quando for atingido o prazo de instalação)  

        > [!IMPORTANT]  
        >  Se um utilizador iniciar a instalação de software a partir do Centro de Software ou do Catálogo de Aplicações, estas operações serão sempre permitidas, independentemente das definições de ligação de Internet limitada.  

         Se for atingido o limite de transferência de dados para a ligação à Internet com tráfego limitado, o cliente tenta já não está a comunicar com sites do Configuration Manager.  

    -   **Bloco**: O cliente do Configuration Manager não tenta comunicar com sites do Configuration Manager quando estiver a utilizar uma ligação à Internet com tráfego limitado. Este é o valor predefinido.  

##  <a name="power-management"></a>Gestão de energia  

-   **Permitir aos utilizadores excluir o respetivo dispositivo da gestão de energia**  

     Na lista pendente, escolha **verdadeiro** ou **Sim** para permitir que os utilizadores do Centro de Software excluam os respetivos computadores a partir de qualquer definições de gestão de energia configuradas.  

-   **Ativar reativação proxy**  

     Especifique **Sim** para completar a definição de reativação por LAN do site quando estiver configurado para pacotes unicast.  

     Para obter mais informações sobre o proxy de reativação, consulte [planear como reativar os clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Não ative a reativação proxy numa rede de produção sem compreender primeiro como funciona e avaliá-la num ambiente de teste.  

-   **Reativar o número da porta proxy (UDP)**  

     Mantenha o valor predefinido para o número de porta que geridos computadores utilize para enviar pacotes de reativação para computadores em modo de suspensão. Em alternativa, alterar o número para um valor à sua escolha.  

     O número de porta que especificar aqui é automaticamente configurado para clientes que executam a Firewall do Windows quando utiliza o **exceção de Firewall do Windows para proxy de reativação** opção. Se os clientes tiverem outra firewall em execução, terá de a configurar manualmente para permitir o número da porta UDP especificado para esta definição.  

-   **Reativar por LAN o número da porta (UDP)**  

     Mantenha o valor predefinido 9, exceto se tiver alterado o número de porta de reativação por LAN (UDP) no **portas** separador do site **propriedades**.  

    > [!IMPORTANT]  
    >  Este número tem de corresponder ao número nas **Propriedades**do site. Se alterar este número num único local, não é automaticamente atualizado no outro.  

##  <a name="remote-tools"></a>Ferramentas remotas  

-   **Ativar Controlo Remoto nos clientes** e **Perfis de exceção de firewall**  

     Escolha se o controlo remoto do Configuration Manager está ativado para todos os computadores cliente que recebem estas definições de cliente. Escolha **configurar** para ativar o controlo remoto. Opcionalmente, configure as definições da firewall para permitir o controlo remoto funcione nos computadores cliente.  

     Por predefinição, o controlo remoto encontra-se desativado.  

    > [!IMPORTANT]  
    >  Se as definições da firewall não estiverem configuradas, o controlo remoto poderá não funcionar corretamente.  

-   **Os utilizadores podem alterar as definições de política ou de notificação no Centro de Software**  

     Escolha se os utilizadores podem alterar as opções de controlo remoto no Centro de Software.  

-   **Permitir o Controlo Remoto de um computador autónomo**  

     Escolha se um administrador pode utilizar o controlo remoto para aceder a um computador cliente que está a sessão terminada ou bloqueado. Apenas um computador com sessão iniciada e desbloqueado pode ser controlado remotamente quando esta definição estiver desativada.  

-   **Solicitar ao utilizador permissão do Controlo Remoto**  

     Escolha se o computador cliente apresentará uma mensagem que lhe pede permissão do utilizador antes de permitir que uma sessão de controlo remoto.  

-   **Conceder permissão de Controlo Remoto ao grupo de Administradores local**  

     Escolha se a administradores locais no servidor que inicia a ligação de controlo remoto podem estabelecer sessões de controlo remoto nos computadores cliente.  

-   **Nível de acesso permitido**  

     Especifica o nível de acesso de controlo remoto que será permitido. Pode escolher entre:  

    -   Controlo total  

    -   Visualizar apenas  

    -   Nenhum  

-   **Visualizadores permitidos**  

     Escolha **definir visualizadores** para abrir o **configurar definições do cliente** diálogo caixa e especificar os nomes dos utilizadores Windows que poderão estabelecer sessões de controlo remoto para computadores cliente.  

-   **Mostrar ícone de notificação de sessão na barra de tarefas**  

     Escolha esta opção para apresentar um ícone na barra de tarefas do cliente de computadores para indicar que se encontra ativa uma sessão de controlo remoto.  

-   **Mostrar barra de ligação da sessão**  

     Escolha esta opção para apresentar uma barra de ligação de sessão de alta visibilidade no cliente computadores para indicar que se encontra ativa uma sessão de controlo remoto.  

-   **Reproduzir um som no cliente**  

     Escolha esta opção para utilizar som para indicar quando uma sessão de controlo remoto está ativa num computador cliente. Poderá ser reproduzido um som quando a sessão for ligada ou desligada, ou ser reproduzido um som repetidamente durante a sessão.  

-   **Gerir definições da Assistência Remota não solicitada**  

     Escolha esta opção para permitir que o Configuration Manager gerir sessões de assistência remota não solicitada.  

     Uma sessão de assistência remota não solicitada, o utilizador do computador cliente não pediu a assistência para iniciar a sessão.  

-   **Gerir definições da Assistência Remota solicitada**  

     Escolha esta opção para permitir que o Configuration Manager gerir sessões de assistência remota solicitada.  

     Numa sessão de assistência remota solicitada, o utilizador do computador cliente enviou um pedido para o administrador para a assistência remota.  

-   **Nível de acesso para a Assistência Remota**  

     Escolha o nível de acesso a atribuir às sessões de assistência remota que sejam iniciadas na consola do Configuration Manager.  

    > [!NOTE]  
    >  O utilizador do computador cliente tem sempre de conceder permissão para que ocorra uma sessão de Assistência Remota.  

-   **Gerir definições de Ambiente de Trabalho Remoto**  

     Escolha esta opção para permitir que o Configuration Manager gerir sessões de ambiente de trabalho remoto para computadores.  

-   **Permitir que os visualizadores autorizados estabeleçam ligação utilizando a ligação ao Ambiente de Trabalho Remoto**  

     Escolha esta opção para permitir que os utilizadores especificados na lista de visualizadores autorizados a ser adicionado ao grupo de utilizadores local do ambiente de trabalho remoto em computadores cliente.  

-   **Exigir autenticação de nível de rede nos computadores com o sistema operativo Windows Vista e versões posteriores**  

     Escolha esta opção mais segura se pretender utilizar a autenticação de nível de rede para estabelecer ligações de ambiente de trabalho remoto a computadores cliente que executam o Windows Vista ou posterior. Autenticação de nível de rede requer menos recursos do computador remoto inicialmente porque concluído a autenticação de utilizador antes de estabelecer uma ligação de ambiente de trabalho remoto. Este método é mais seguro porque pode ajudar a proteger o computador contra utilizadores mal intencionados ou software malicioso, reduzindo o risco de ataques denial-of-service.  

## <a name="software-deployment"></a>Implementação de software  

-   **Agendar reavaliação das implementações**  

     Configure uma agenda para quando o Configuration Manager deverá reavaliar as regras de requisitos para todas as implementações. O valor predefinido é a cada 7 dias.  

    > [!IMPORTANT]  
    >  Recomendamos que altere este valor para um valor inferior à predefinição de. Fazer com que poderá afetar negativamente o desempenho da sua rede e os computadores cliente.  

     Também poderá iniciar esta ação de um computador de cliente do Configuration Manager, selecionando a ação **ciclo de avaliação de implementação de aplicação** do **ações** separador de **do Configuration Manager** no painel de controlo.  

##  <a name="software-inventory"></a>Inventário de software  

-   **Inventariar detalhe de relatórios**  

     Especifica o nível de informações dos ficheiros a inventariar. Pode Inventariar os detalhes sobre o ficheiro, os detalhes sobre o produto associado o ficheiro ou todas as informações sobre o ficheiro.  

-   **Inventariar estes tipos de ficheiro**  

     Se pretender especificar os tipos de ficheiro a inventariar, escolha **definir tipos** e, em seguida, configure o seguinte no **configurar definições do cliente** caixa de diálogo:  

    > [!NOTE]  
    >  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que devolve a cada definição será intercalado.  

    -   Escolha o **novo** ícone para adicionar um novo tipo de ficheiro ao inventário. Em seguida, especifique as seguintes informações no **propriedades do ficheiro inventariado** caixa de diálogo:  

        -   **Nome**: Forneça um nome para o ficheiro que pretende inventariar. Pode utilizar o * *\**  para representar qualquer cadeia de texto e o **?** para representar um único caráter. Por exemplo, se pretender inventariar todos os ficheiros com a extensão. doc, especifique o nome de ficheiro  **\*. doc**.  

        -   **Localização**: Escolha **definir** para abrir o **propriedades do caminho** caixa de diálogo. Pode configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro especificado, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

        -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, os ficheiros comprimidos ou encriptados não serão inventariados.  

        -   **Excluir ficheiros da pasta Windows**: Quando seleciona esta opção, todos os ficheiros na pasta Windows e respetivas subpastas não serão inventariados.  

    -   Escolha **OK** para fechar o **propriedades do ficheiro inventariado** caixa de diálogo.  

    -   Adicionar todos os ficheiros que pretende inventariar e, em seguida, escolha **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

-   **Recolher ficheiros**  

     Se pretender recolher ficheiros de computadores cliente, escolha **definir ficheiros** e, em seguida, configure o seguinte:  

    > [!NOTE]  
    >  Se forem aplicadas várias definições personalizadas de cliente para um computador, o inventário que devolve a cada definição será intercalado.  

    -   No **configurar definições do cliente** diálogo caixa, escolha o **novo** ícone para adicionar um ficheiro a serem recolhidos.  

    -   Na caixa de diálogo **Propriedades do Ficheiro Recolhido** , forneça as seguintes informações:  

        -   **Nome**: Forneça um nome para o ficheiro que pretende recolher. Pode utilizar o * *\**  para representar qualquer cadeia de texto e o **?** para representar um único caráter.  

        -   **Localização**: Escolha **definir** para abrir o **propriedades do caminho** caixa de diálogo. Poderá configurar o inventário de software para procurar todos os discos de rígido do cliente para o ficheiro que pretende recolher, procurar num caminho especificado (por exemplo, **C:\Folder**), ou procure numa variável especificada (por exemplo, *% windir %*). Também poderá procurar em todas as subpastas do caminho especificado.  

        -   **Excluir ficheiros comprimidos e encriptados**: Quando seleciona esta opção, os ficheiros comprimidos ou encriptados não serão recolhidos.  

        -   **Parar a recolha de ficheiros quando o tamanho total dos ficheiros excede (KB)**: Especifica o tamanho do ficheiro (em quilobytes) após o qual dos ficheiros especificados em **nome** serão recolhidos.  

          > [!NOTE]  
          >  O servidor do site recolhe as cinco versões mais recentes dos ficheiros recolhidos e armazena-os no  *&lt;diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol diretório. Se um ficheiro não tiver sido alterado desde a recolha do último inventário de software, o ficheiro não será novamente recolhido.  
          >   
          >  Inventário de software não recolher ficheiros com mais de 20 MB.  
          >   
          >  O valor **tamanho máximo para todos ficheiros recolhidos (KB)** no **configurar definições do cliente** caixa de diálogo mostra o tamanho máximo para todos ficheiros recolhidos. Quando este tamanho for atingido, a recolha de ficheiros será interrompida. Todos os ficheiros já recolhidos serão mantidos e enviados para o servidor do site.  

          > [!IMPORTANT]
          >  Se configurar o inventário de software para recolher muitos ficheiros de grandes dimensões, poderá afetar negativamente o desempenho da rede e do servidor de site.  

        Para obter informações sobre como visualizar ficheiros recolhidos, consulte [como utilizar o Explorador de recursos para ver o inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Escolha **OK** para fechar o **propriedades do ficheiro recolhido** caixa de diálogo.  

    -   Adicionar todos os ficheiros que pretende recolher e, em seguida, escolha **OK** para fechar o **configurar definições do cliente** caixa de diálogo.  

-   **Definir Nomes**  

     Durante o inventário de software, são obtidos nomes de fabricantes e de produtos a partir das informações de cabeçalho dos ficheiros instalados nos clientes do site. Como nem sempre esses nomes se encontram padronizados nas informações de cabeçalho dos ficheiros, ao visualizar as informações do inventário de software no Explorador de Recursos ou ao executar consultas poderão, por vezes, ser apresentadas diversas versões do mesmo nome de fabricante ou produto. Se pretender padronizar estes nomes a apresentar, escolha **definir nomes** e, em seguida, configure o seguinte no **configurar definições do cliente** caixa de diálogo:  

    -   **Nome do tipo**: Inventário de software recolhe informações sobre produtos e fabricantes. Na lista pendente, escolha se pretende configurar os nomes a apresentar para um **fabricante** ou um **produto**.  

    -   **Nome a apresentar**: Especifique o nome a apresentar que pretende utilizar em vez dos nomes de **nomes inventariados** lista. Pode escolher o **novo** ícone para especificar um novo nome a apresentar.  

    -   **Nomes inventariados**: Escolha o **novo** ícone para adicionar um novo nome inventariado, que será substituído no inventário de software pelo nome selecionado no **nome a apresentar** lista. Poderá adicionar vários nomes a substituir.  

##  <a name="software-updates"></a>Atualizações de software  

-   **Ativar atualizações de software nos clientes**  

     Utilize esta definição para ativar atualizações de software nos clientes do Configuration Manager. Quando desativar esta definição, o Configuration Manager removerá as políticas de implementação existentes do cliente. Quando voltar a ativar esta definição, o cliente transferirá a política de implementação atual.  

    > [!IMPORTANT]  
    >  Ao desativar esta definição, NAP políticas e conformidade de definições que se baseiam na definição de dispositivo para atualizações de software deixarão de funcionar.  

-   **Agendamento da análise de atualização de software**  

     Utilize esta definição para especificar a frequência com que o cliente inicia uma análise de avaliação da compatibilidade das atualizações de software. A análise de avaliação da compatibilidade determina o estado das atualizações de software no cliente (por exemplo, necessária ou instalada). Para obter mais informações sobre a avaliação de compatibilidade, consulte [avaliação de compatibilidade de atualizações de Software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Por predefinição, é utilizada uma agenda simples e a análise de compatibilidade é iniciada a cada 7 dias. Poderá optar por criar um agendamento personalizado para especificar uma data e hora de início exatas, optar pela utilização da hora local ou UTC e configurar o intervalo periódico para um dia da semana específico.  

    > [!NOTE]  
    >  Se especificar um intervalo de menos de 1 dia, o Configuration Manager será automaticamente predefinido para 1 dia.  

    > [!WARNING]  
    >  A hora de início real em computadores cliente é a hora de início mais um período de tempo aleatório de até 2 horas. Isto evita que os computadores cliente iniciem a análise e estabeleçam ligação ao Windows Server Update Services (WSUS) no servidor ativo de ponto de atualização de software ao mesmo tempo.  

-   **Agendar a reavaliação de implementação**  

     Utilize esta definição para configurar a frequência o agente de cliente de atualizações de Software reavalia atualizações de software para o estado de instalação nos computadores de cliente do Configuration Manager. Quando as atualizações de software que tenham sido anteriormente instaladas já não se encontram em computadores cliente e ainda são necessárias, são reinstaladas.

     A agenda de reavaliação de implementação deve ser ajustada com base na política da empresa relativamente a compatibilidade de atualização de software, se os utilizadores têm a capacidade de desinstalar as atualizações de software e assim sucessivamente. Lembre-se de que cada ciclo de reavaliação da implementação resulta em alguma atividade da CPU do computador cliente e rede. Por predefinição, é utilizada uma agenda simples e a análise da reavaliação de implementação é iniciada a cada 7 dias.  

    > [!NOTE]  
    >  Se especificar um intervalo de menos de 1 dia, o Configuration Manager será automaticamente predefinido para 1 dia.  

-   **Quando qualquer prazo de implementação da atualização de software é alcançado, instale todas as outras implementações de atualização de software com prazo a terminar no período de tempo especificado**  

     Utilize esta definição para instalar todas as atualizações de software em implementações necessárias com prazos incluídos num determinado período de tempo. Quando é atingido um prazo para um software necessário atualizar a implementação, é iniciada a instalação em clientes para as atualizações de software na implementação. Esta definição determina se deve ser iniciada também a instalação das atualizações de software definidas noutras implementações necessárias com um prazo configurado no período de tempo especificado.  

     Utilize esta configuração para agilizar a instalação da atualização de software para atualizações de software necessárias, aumentar potencialmente a segurança, reduzir potencialmente a apresentação de notificações e reduzir potencialmente os reinícios do sistema em computadores cliente. Por predefinição, esta definição não está ativada.  

-   **Período de tempo para o qual todas as implementações pendentes com prazo nesta hora também serão instaladas**  

     Utilize esta definição para especificar o intervalo de tempo da definição anterior. Pode introduzir um valor de 1 a 23 horas e de 1 a 365 dias. Por predefinição, esta definição está configurada para 7 dias.  

-   **Ativar a instalação dos ficheiros de instalação rápida nos clientes**

-   **Porta utilizada para transferir conteúdo para os ficheiros de instalação rápida**

-   **Ativar a gestão de cliente de 365 do Office novamente** Utilize esta definição para ativar a gestão do agente de cliente do Office 365. Quando definir o valor **Sim**, permite-lhe configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager.

##  <a name="user-and-device-affinity"></a>Afinidade dispositivo / utilizador  

-   **Limiar de utilização de afinidade de dispositivo e utilizador (minutos)**  

     Especifique o número de minutos antes do Configuration Manager cria um mapeamento de afinidade de dispositivo do utilizador.  

-   **Limiar de utilização de afinidade de dispositivo e utilizador (dias)**  

     Especifique o número de dias durante o qual será medido o limiar de afinidade baseada na utilização.  

    > [!NOTE]  
    >  Por exemplo, se **limiar de utilização de afinidade de dispositivo de utilizador (minutos)** está especificado como **60** minutos e **limiar de utilização de afinidade de dispositivo do utilizador (dias)** está especificado como **5** dias, o utilizador tem de utilizar o dispositivo durante 60 minutos num período de 5 dias para criar automaticamente uma afinidade de dispositivo do utilizador.  

-   **Configurar automaticamente a afinidade de dispositivo e utilizador a partir dos dados de utilização**  

     Escolha **verdadeiro** ou **Sim** para permitir que o Configuration Manager criar automaticamente afinidades de dispositivo com base nas informações de utilização recolhidas utilizador.  

##  <a name="mobile-devices"></a>Dispositivos móveis  

-   **Perfis de inscrição de dispositivos móveis**  

     Para poder configurar esta definição, deve primeiro configurar como **Verdadeiro** a definição de utilizador de dispositivo móvel **Permitir aos utilizadores a inscrição de dispositivos móveis**. Em seguida, pode escolher **definir perfil** para especificar um perfil de inscrição com informações sobre o modelo de certificado a utilizar durante o processo de inscrição, o site que tem um ponto de registo e ponto proxy de registo e o site que irá gerir o dispositivo após a inscrição.  

    > [!IMPORTANT]  
    >  Certifique-se de que configurou um modelo de certificado para utilizar na inscrição do dispositivo móvel antes de configurar esta opção.  

##  <a name="enrollment"></a>Inscrição  

-   **Perfis de inscrição de dispositivos móveis**  

     Para poder configurar esta definição, deve primeiro configurar como **Sim** a definição de utilizador de inscrição **Permitir aos utilizadores a inscrição de dispositivos móveis e computadores Mac**. Em seguida, pode escolher **definir perfil** para especificar um perfil de inscrição com informações sobre o modelo de certificado a utilizar durante o processo de inscrição, o site que tem um ponto de registo e ponto proxy de registo e o site que irá gerir o dispositivo após a inscrição.  

    > [!IMPORTANT]  
    >  Certifique-se de que configurou um modelo de certificado para utilizar na inscrição do dispositivo móvel ou na inscrição do certificado do cliente Mac antes de configurar esta opção.  

## <a name="user-and-device-affinity"></a>Afinidade dispositivo / utilizador  

-   **Permitir ao utilizador a definição dos seus dispositivos primários**  

     Especifique se os utilizadores estão autorizados a identificar os seus próprios dispositivos primários no **os meus dispositivos** separador do catálogo de aplicações.  
