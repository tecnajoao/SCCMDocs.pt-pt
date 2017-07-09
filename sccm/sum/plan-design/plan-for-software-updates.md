---

title: "Planejar atualizações de software | Microsoft Docs"
description: "Um plano para a infraestrutura de ponto de atualização de software é essencial antes de usar as atualizações de software em um ambiente de produção do System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: b5a2fd9f15992c9e5ef8aede64af5446b6852b1a
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---

# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Planear atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Antes de usar as atualizações de software em um ambiente de produção do System Center Configuration Manager, é importante que você percorra o processo de planejamento. Ter um bom plano para a infraestrutura de ponto de atualização de software é a chave para uma implementação de atualizações de software com êxito.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendações de planeamento da capacidade para atualizações de software  
 Pode utilizar as seguintes recomendações como uma linha base que pode ajudá-lo a determinar as informações para o planeamento da capacidade de atualizações de software que é adequado para a sua organização. Os requisitos de capacidade em si podem variar das recomendações que estão listadas neste tópico, consoante os seguintes critérios: o seu ambiente de rede específico, o hardware que utiliza para alojar o sistema de sites do ponto de atualização de software, o número de clientes que estão instalados e as funções do sistema de sites que estão instaladas no servidor.  

###  <a name="BKMK_SUMCapacity"></a> Planeamento da capacidade para o ponto de atualização de software  
 O número de clientes suportados depende da versão do Windows Server Update Services (WSUS) que é executada no ponto de atualização de software, além de depender também da possibilidade de o sistema de sites do ponto de atualização de software coexistir com uma outra função do sistema de sites.  

-   O ponto de atualização de software consegue suportar até 25.000 clientes quando o WSUS é executado no computador do ponto de atualização de software e o ponto de atualização de software coexiste com uma outra função do sistema de sites.  

-   O ponto de atualização de software pode dar suporte a até 150.000 clientes quando o computador remoto atende aos requisitos do WSUS, o WSUS é usado com o Configuration Manager e você configurar o seguinte:

    Pools de aplicativos do IIS:
    - Aumentar o comprimento da fila de WsusPool para 2000
    - Aumentar o limite de memória particular de WsusPool x4 horas ou definido como 0 (ilimitado)      

    Para obter detalhes sobre os requisitos de hardware para o ponto de atualização de software, consulte [recomendados de hardware para sistemas de site](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).

-   Por padrão, o Configuration Manager não oferece suporte Configurando pontos de atualização de software como clusters NLB. Antes de 1702 de versão do Configuration Manager, você pode usar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software em um cluster NLB. No entanto, a partir do Configuration Manager versão 1702, não há suporte para pontos de atualização de software como clusters NLB e atualizações para o Configuration Manager versão 1702 serão bloqueadas se essa configuração for detectada.

### <a name="capacity-planning-for-software-updates-objects"></a>Planeamento da capacidade para objetos de atualizações de software  
 Utilize as seguintes informações de capacidade para planear os objetos de atualizações de software.  

-   **Limite de 1000 atualizações de software numa implementação**  

     Tem de limitar o número de atualizações de software a 1000 para cada implementação de atualização de software. Quando cria uma regra de implementação automática, especifique um critério que limita o número de atualizações de software que são devolvidas. A regra de implementação automática falha quando os critérios que especificar devolverem mais de 1000 atualizações de software. Você pode verificar o status da regra de implantação automática no **regras de implantação automática** nó no console do Configuration Manager. Ao implementar manualmente atualizações de software, não selecione mais de 1000 atualizações para implementar.  

     Você também deve limitar o número de atualizações de software a 1.000 em uma linha de base de configuração. Para obter mais informações, consulte [criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="BKMK_SUPInfrastructure"></a> Determinar a infraestrutura do ponto de atualização de software  
 O site de administração central e todos os sites subordinados principais têm de ter um ponto de atualização de software onde irá implementar atualizações de software. Ao planejar para a infraestrutura de ponto de atualização de software, você precisa determinar as seguintes dependências:
 - onde instalar o ponto de atualização de software para o site
 - quais sites exigem um ponto de atualização de software que aceita comunicação de clientes baseados na Internet
 - Se você precisa de um software de ponto de atualização em um site secundário.

Utilize as secções seguintes para determinar a infraestrutura do ponto de atualização de software.  

> [!IMPORTANT]  
>  Para obter informações sobre as dependências internas e externas que são necessários para atualizações de software, consulte [pré-requisitos para atualizações de software](prerequisites-for-software-updates.md).  

 Você pode adicionar vários pontos de atualização de software em um site primário do Configuration Manager. A capacidade para ter vários pontos de atualização de software num site fornece tolerância a falhas, sem requerer a complexidade do NLB. No entanto, a ativação pós-falha que recebe com vários pontos de atualização de software não é tão sólida quanto o NLB para o balanceamento de carga puro sendo, ao invés disso, concebida para a tolerância a falhas. Além disso, a conceção de ativação pós-falha do ponto de atualização de software é diferente do modelo de aleatoriedade puro que é utilizado na conceção para pontos de gestão. Ao contrário do que sucede na conceção de pontos de gestão, nos pontos de atualização de software existem custos de desempenho para o cliente e para a rede que estão associados a uma mudança para um novo ponto de atualização de software. Quando o cliente muda para um novo servidor WSUS para analisar a existência de atualizações de software, o resultado é um aumento do tamanho do catálogo e exigências associadas do lado do cliente e a nível do desempenho da rede. Por conseguinte, o cliente preserva a afinidade com o último ponto de atualização de software para o qual foi analisado com êxito.  

 O primeiro ponto de atualização de software que instalar num site principal é a origem de sincronização para todos os pontos de atualização de software adicionais que adicionar no site primário. Depois de adicionar os seus pontos de atualização de software e iniciar a sincronização das atualizações de software, pode ver o estado dos pontos de atualização de software e da origem de sincronização no nó **Estado de Sincronização do Ponto de Atualização de Software** da área de trabalho **Monitorização** .  

 Quando um ponto de atualização de software falha e esse ponto de atualização de software está configurado como a origem de sincronização para os outros pontos de atualização de software no site, terá de remover manualmente o ponto de atualização de software em falha e selecionar um novo ponto de atualização de software para utilizar como a origem de sincronização. Para obter mais informações sobre como remover uma atualização de software do ponto, consulte [remover a função do sistema de site do ponto de atualização de software](../get-started/remove-a-software-update-point.md).  

###  <a name="BKMK_SUPList"></a> Lista de pontos de atualização de software  
 O Configuration Manager fornece ao cliente uma lista de pontos de atualização de software nos seguintes cenários: quando um novo cliente recebe a política para habilitar atualizações de software, ou quando um cliente não pode entrar em contato com seu ponto de atualização de software e precisa mudar para outro ponto de atualização de software. O cliente seleciona aleatoriamente um ponto de atualização de software na lista e dá prioridade aos pontos de atualização de software situados na mesma floresta. Configuration Manager fornece aos clientes uma lista diferente dependendo do tipo de cliente.  

-   **Clientes baseados em intranet**: Recebe uma lista de pontos de atualização de software que você pode configurar para permitir conexões somente da intranet ou uma lista de pontos de atualização de software que permitem conexões do cliente da Internet e intranet.  

-   **Clientes baseados na Internet**: Recebe uma lista de pontos de atualização de software que você configurar para permitir conexões somente da Internet ou uma lista de pontos de atualização de software que permitem conexões do cliente da Internet e intranet.  

###  <a name="BKMK_SUPSwitching"></a> Mudança do ponto de atualização de software  
> [!NOTE]
> A partir da versão 1702, os clientes usam grupos de limites para localizar um novo ponto de atualização de software e para localizar e fallback uma nova atualização de software ponto se o ano atual não estiver mais acessível. Você pode adicionar pontos de atualização de software individual para grupos de limites diferentes para controlar quais servidores em que um cliente possa encontrar. Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no [Configurando grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) tópico.

Caso tenha vários pontos de atualização de software num site e um deles falhar ou ficar indisponível, os clientes ligar-se-ão a um ponto de atualização de software diferente e continuarão a analisar a presença das mais recentes atualizações de software. Quando um cliente for atribuído pela primeira vez a um ponto de atualização de software, o mesmo manter-se-á atribuído a esse ponto de atualização de software, exceto se não conseguir analisar a presença de atualizações de software nesse ponto de atualização de software.  

A análise da existência de atualizações de software pode falhar com uma série de diferentes códigos de erro de repetições e não repetições. Quando a análise falha com um código de erro de repetição, o cliente inicia um processo de repetição para procurar as atualizações de software no ponto de atualização de software. As condições de alto nível que resultam num código de erro de repetição são normalmente causadas porque o servidor WSUS está indisponível ou porque está temporariamente sobrecarregado. O cliente utiliza o seguinte processo quando falha na análise de atualizações de software:  

1.  O cliente analisa a existência de atualizações de software à hora agendada ou quando é iniciado através do painel de controlo no cliente, ou utilizando o SDK. Se a análise falhar, o cliente aguarda 30 minutos para repetir a análise e utiliza o mesmo ponto de atualização de software.  

2.  O cliente tenta novamente um mínimo de quatro vezes em intervalos de 30 minutos. Após a quarta falha, e depois de aguardar dois minutos adicionais, o cliente desloca-se para o ponto de atualização de software seguinte na lista de pontos de atualização de software.  

3.  O cliente vai pelo mesmo processo no novo ponto de atualização de software. Após uma verificação bem-sucedida, o cliente continuará a se conectar ao novo ponto de atualização de software.

 A lista seguinte fornece informações adicionais que pode considerar para os cenários de repetição e mudança do ponto de atualização de software:  

-   Se um cliente está desligado da intranet da empresa e não consegue analisar a presença de atualizações de software, esse cliente não muda para outro ponto de atualização de software. Esta é uma falha esperada, porque o cliente não consegue aceder à rede da empresa ou ao ponto de atualização de software que permite a ligação da intranet. O cliente do Configuration Manager determina a disponibilidade do ponto de atualização de software da intranet.  

-   Se a gestão de clientes baseada na Internet estiver ativada e existirem vários pontos de atualização de software que estão configurados para aceitarem comunicação de clientes na Internet, o processo de mudança seguirá o processo de repetição padrão que é descrito no cenário anterior.  

-   Se o processo de análise tiver sido iniciado mas o cliente for desligado da corrente antes de a análise estar concluída, tal não é considerada uma falha da análise e não conta como uma das quatro tentativas de repetição.  

Quando o Configuration Manager recebe qualquer um dos seguintes códigos de erro do Windows Update Agent, ele terá a repetição de conexão do cliente:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Para pesquisar o significado de um código de erro, você deve converter o código de erro decimal para hexadecimal e procure o valor hexadecimal em um site, como o [Windows Update Agent - Wiki de códigos de erro](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx).


###  <a name="BKMK_ManuallySwitchSUPs"></a>Mudar manualmente clientes para um novo ponto de atualização de software
A partir do Configuration Manager versão 1606, pode ativar a opção para clientes do Configuration Manager mudarem para um novo ponto de atualização de software quando existirem problemas com o ponto de atualização de software ativo. Esta opção só resulta em alterações quando um cliente recebe vários pontos de atualização de software a partir de um ponto de gestão.  

Ative esta opção numa coleção de dispositivos ou num conjunto de dispositivos selecionados. Depois de ativada, os clientes irão procurar outro ponto de atualização de software na análise seguinte. Dependendo das suas definições de configuração do WSUS (classificações de atualizações, produtos, se os pontos de atualização de software partilham uma base de dados WSUS, etc.), a transição para um novo ponto de atualização de software irá gerar tráfego de rede adicional. Por conseguinte, só deve utilizar esta opção quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para ativar a opção para mudar pontos de atualização de software  

1.  Na consola do Configuration Manager, aceda a **Ativos e Compatibilidade > Descrição geral > Coleções de dispositivos**.  

2.  No separador **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e, em seguida, clique em **Mudar para o Ponto de Atualização de Software seguinte**.  


###  <a name="BKMK_SUP_CrossForest"></a> Pontos de atualização de software numa floresta não fidedigna  
 Pode criar um ou mais pontos de atualização de software num site para suportar clientes numa floresta que não considera fidedigna. Para adicionar um ponto de atualização de software noutra floresta, tem primeiro de instalar e configurar um servidor WSUS na floresta. Em seguida, inicie o Assistente para adicionar um servidor de site do Configuration Manager com a função do sistema de site do ponto de atualização de software. No assistente, configure as seguintes definições para ligar com êxito ao WSUS na floresta não fidedigna:  

-   Especifique uma conta de Instalação do Sistema de Sites que pode aceder ao servidor WSUS na floresta.  

-   Especifique a conta de Ligação ao Servidor WSUS para utilizar para ligar ao servidor WSUS.  

 Por exemplo, dispõe de um site principal na floresta A com pontos de atualização de software (SUP01 e SUP02). Do mesmo modo, para o mesmo site principal, dispõe de dois pontos de atualização de software (SUP03 e SUP04) na floresta B. Quando a mudança ocorre neste exemplo, é atribuída prioridade aos pontos de atualização de software da mesma floresta que o cliente.  

###  <a name="BKMK_WSUSSyncSource"></a> Utilizar um servidor WSUS existente como origem de sincronização no site de nível superior  
 Normalmente, o site de nível superior na sua hierarquia está configurado para sincronizar metadados de atualizações de software com o Microsoft Update. Quando sua política de segurança corporativa não permite acesso à Internet do site de nível superior, você pode configurar a origem da sincronização para o site de nível superior para usar um servidor WSUS existente que não esteja na hierarquia do Configuration Manager. Por exemplo, pode ter um servidor WSUS instalado no seu DMZ com acesso à Internet, mas o site de nível superior não. Pode configurar o servidor WSUS no DMZ como origem de sincronização para os metadados de atualizações de software. Certifique-se de que o servidor do WSUS no rede de Perímetro sincroniza atualizações de software que atendem aos critérios necessários na hierarquia do Configuration Manager. Caso contrário, o site de nível superior poderá não sincronizar as atualizações de software que espera. Ao instalar o ponto de atualização de software, configure uma conta de ligação ao WSUS com acesso ao servidor WSUS no DMZ e confirme se a firewall permite tráfego para as portas adequadas. Para obter mais informações, examine o [portas usadas pelo ponto de atualização de software para a origem da sincronização](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="BKMK_NLBSUPSP1"></a> Ponto de atualização de software configurado para utilizar um NLB  
 A mudança de ponto de atualização de software resolverá provavelmente as necessidades dos utilizadores em matéria de tolerância de falhas. Por padrão, o Configuration Manager não oferece suporte Configurando pontos de atualização de software como clusters NLB. Antes de 1702 de versão do Configuration Manager, você pode usar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software em um cluster NLB. No entanto, a partir do Configuration Manager versão 1702, não há suporte para pontos de atualização de software como clusters NLB e atualizações para o Configuration Manager versão 1702 serão bloqueadas se essa configuração for detectada. Para obter mais informações sobre o cmdlet Set-CMSoftwareUpdatePoint do PowerShell, consulte o [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="BKMK_SUPSecSite"></a> Ponto de atualização de software num site secundário  
 O ponto de atualização de software é opcional num site secundário. Quando instala um ponto de atualização de software num site secundário, a base de dados de WSUS é configurada como uma réplica do ponto de atualização de software predefinido no site primário principal. Apenas pode instalar um ponto de atualização de software num site secundário. Os dispositivos atribuídos a um site secundário são configurados para utilizar um ponto de atualização de software no site principal quando não existe um ponto de atualização de software instalado no site secundário. Normalmente, deverá instalar um ponto de atualização de software num site secundário nos casos em que existam limitações de largura de banda de rede entre os dispositivos que estão atribuídos ao site secundário e os pontos de atualização de software do site primário principal, bem como quando o ponto de atualização de software está prestes a atingir o limite de capacidade. Após a instalação e configuração de um ponto de atualização de software com êxito no site secundário, é atualizada para todo o site uma política para os computadores cliente que estejam atribuídos ao site, passando estes a utilizar o novo ponto de atualização de software.  

##  <a name="BKMK_SUPInstallation"></a>Planejar a instalação do ponto de atualização de Software  
 Antes de criar uma função de sistema de site do ponto de atualização de software no Configuration Manager, há vários requisitos que devem ser consideradas dependendo de sua infraestrutura do Configuration Manager. Se configurar o ponto de atualização de software para comunicar utilizando SSL, é particularmente importante que leia esta secção devido aos passos adicionais que têm de ser tomados para que os pontos de atualização de software da hierarquia funcionem corretamente. Esta secção contém informações sobre os passos que deverá executar para planear e preparar a instalação de um ponto de atualização de software com êxito.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requisitos do ponto de atualização de software  
 A função do sistema de site do ponto de atualização de software deve ser instalada em um sistema de site que atenda aos requisitos mínimos do WSUS e as configurações com suporte para sistemas de site do Configuration Manager.  

-   Para obter mais informações sobre os requisitos mínimos para a função de servidor do WSUS no Windows Server 2012, consulte [examinar as considerações e requisitos de sistema](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) na biblioteca de documentação do Windows Server 2012.  

-   Para obter mais informações sobre as configurações com suporte para sistemas de site do Configuration Manager, consulte [Site e pré-requisitos de sistema de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="BKMK_PlanningForWSUS"></a> Planear a instalação do WSUS  

As atualizações de software necessitam que esteja instalada uma versão suportada do WSUS em todos os servidores de sistemas de sites que estejam configurados para a função de sistema de sites de ponto de atualização de software. Além disso, se não instalar o ponto de atualização de software no servidor do site, necessitará de instalar a Consola de Administração do WSUS no computador do servidor do site, caso ainda não esteja instalada. Tal permitirá ao servidor do site comunicar com o WSUS que está a ser executado no ponto de atualização de software.  

 Ao usar o WSUS no Windows Server 2012, você deve configurar permissões adicionais para permitir **o WSUS Configuration Manager** verifica no Configuration Manager se conecte ao WSUS para realizar a integridade periódicas. Escolha uma das seguintes opções para configurar as permissões:  

-   Adicionar a conta **SYSTEM** ao grupo **Administradores WSUS**  

-   Adicionar a conta **NT AUTHORITY\SYSTEM** como utilizador da base de dados WSUS (SUSDB) e configurar uma associação mínima à função de base de dados webService  

 Para obter mais informações sobre como instalar o WSUS no Windows Server 2012, veja [Instalar a Função de Servidor WSUS](http://go.microsoft.com/fwlink/p/?LinkId=272355) na biblioteca de documentação do Windows Server 2012.  

 Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. A partilha da mesma base de dados reduzirá significativamente, embora não elimine completamente o impacto ao nível do cliente e do desempenho de rede que poderá ocorrer quando os clientes mudarem para um novo ponto de atualização de software. A análise de diferenças continuará a ser executada quando um cliente mudar para um novo ponto de atualização de software que partilhe uma base de dados com o ponto de atualização de software antigo, embora a análise seja muito mais rápida do que seria se o WSUS tivesse uma base de dados própria.  

####  <a name="BKMK_CustomWebSite"></a> Configurar o WSUS para utilizar um Web site personalizado  
 Quando instala o WSUS, pode optar por utilizar o Web site predefinido existente do IIS ou criar um Web site personalizado do WSUS. Crie um site personalizado para o WSUS para que o IIS hospede serviços do WSUS em um site virtual dedicado, em vez de compartilhar o mesmo site que é usado por outros aplicativos ou os outros sistemas de site do Configuration Manager. Este aspeto será particularmente válido caso instale a função de sistema de sites de ponto de atualização de software no servidor do site. Quando você executa o WSUS no Windows Server 2012 ou Windows Server 2016, o WSUS é configurado por padrão para usar a porta 8530 para HTTP e a porta 8531 para HTTPS. Necessitará de especificar estas definições de porta quando criar o ponto de atualização de software num site.  

####  <a name="BKMK_WSUSInfrastructure"></a> Utilizar uma infraestrutura do WSUS existente  
 Você pode selecionar um servidor WSUS que estava ativo no seu ambiente antes da instalação do Configuration Manager como um ponto de atualização de software. Quando o ponto de atualização de software estiver configurado, necessitará de especificar as definições de sincronização. Configuration Manager se conecta ao servidor do WSUS que é executado no servidor de ponto de atualização de software e configura o WSUS com as mesmas configurações. Se você sincronizou WSUS antes que ele foi configurado como um ponto de atualização de software com produtos ou classificações que você não configurou como parte das configurações de sincronização de ponto de atualização de software, o software atualiza os metadados para os produtos e as classificações são sincronizados para todos os metadados de atualizações de software no banco de dados do WSUS independentemente das configurações de sincronização que você configurou para o ponto de atualização de software. Por conseguinte, poderão surgir metadados de atualizações de software inesperados na base de dados do site. Você experimentará o mesmo comportamento ao adicionar produtos ou classificações diretamente no console de administração do WSUS e logo em seguida iniciar a sincronização. Cada hora, por padrão, o Configuration Manager se conecta ao WSUS no ponto de atualização de software e redefine as configurações modificadas fora do Configuration Manager. As atualizações de software que não correspondam aos produtos e classificações especificados nas definições de sincronização serão definidas como expiradas e posteriormente removidas da base de dados do site.

 Quando um servidor do WSUS é configurado como um ponto de atualização de software, não é possível usá-lo como um servidor autônomo do WSUS. Se você precisar de um servidor WSUS autônomo separado que não é gerenciado pelo Configuration Manager, você deve configurá-lo em um servidor diferente.

####  <a name="BKMK_WSUSAsReplica"></a> Configurar o WSUS como servidor de réplica  
 Quando cria uma função de sistema de sites de ponto de atualização de software num servidor de sites primário, não poderá utilizar um servidor WSUS que esteja configurado como uma réplica. Quando o servidor do WSUS é configurado como uma réplica, o Configuration Manager Falha ao configurar o servidor WSUS e a sincronização do WSUS falha também. Quando um ponto de atualização de software é criado em um site secundário, Configuration Manager configura o WSUS para ser um servidor de réplica do WSUS que é executado no ponto de atualização de software no site primário pai. O primeiro ponto de atualização de software que instalar num site primário será o ponto de atualização de software predefinido. Os pontos de atualização de software adicionais no site serão configurados como réplicas do ponto de atualização de software predefinido.  

####  <a name="BKMK_WSUSandSSL"></a> Decidir se pretende configurar o WSUS para utilizar SSL  
 Pode utilizar o protocolo SSL para ajudar a proteger o WSUS que é executado no ponto de atualização de software. O WSUS utiliza SSL para autenticar computadores cliente e servidores WSUS a jusante para o servidor WSUS. O WSUS também utiliza SSL para encriptar os metadados de atualização de software. Quando escolhe proteger o WSUS com SSL, tem de preparar o servidor WSUS antes de instalar o ponto de atualização de software.  

 Quando instalar e configurar o ponto de atualização de software, terá de selecionar a definição **Ativar as comunicações SSL para o Servidor WSU** . Caso contrário, o Configuration Manager configura o WSUS para não usar SSL. Quando ativar SSL para o WSUS que é executado num ponto de atualização de software, o WSUS que é executado no ponto de atualização de software em quaisquer sites subordinados têm também de ser configurados para a utilização de SSL.  

###  <a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  
 Atualizações de software em um site de administração central do Configuration Manager se comunicar com o WSUS que é executado no ponto de atualização de software, que por sua vez, se comunica com a origem da sincronização sincronizar o software atualiza os metadados. Os pontos de atualização de software num site subordinado comunicam com o ponto de atualização de software no site principal. Quando existe mais do que um ponto de atualização de software num site primário, os pontos adicionais de atualização de software têm de comunicar com o primeiro ponto de atualização de software que está instalado no site, que é o ponto de atualização de software predefinido.  

 O firewall pode precisar ser configurado para aceitar as portas HTTP ou HTTPS usadas pelo WSUS nos seguintes cenários: quando você tiver um firewall corporativo entre o ponto de atualização de software do Configuration Manager e a Internet; Quando você tiver um ponto de atualização de software e sua origem de sincronização upstream; ou, quando você tem os pontos de atualização de software adicional. A ligação ao Microsoft Update é sempre configurada para utilizar a porta 80 para HTTP e a porta 443 para HTTPS. Pode utilizar uma porta personalizada para a ligação do WSUS que é executado no ponto de atualização de software num site subordinado ao WSUS que é executado no ponto de atualização de software no site principal. Quando a política de segurança não permite a ligação, terá de utilizar o método de sincronização de exportação e importação. Para obter mais informações, veja a secção [Origem de sincronização](#BKMK_SyncSource) deste tópico. Para obter mais informações sobre as portas utilizadas pelo WSUS, veja [Como determinar as definições de porta utilizadas pelo WSUS no System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Restringir o Acesso a Domínios Específicos  
 Se a sua organização não permitir que as portas e os protocolos estejam abertos a todos os endereços na firewall entre o ponto de atualização de software e a Internet, poderá restringir o acesso aos seguintes domínios, de modo a que o WSUS e as Atualizações Automáticas possam comunicar com o Microsoft Update:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Poderá ter de adicionar os seguintes endereços à firewall que está localizada entre os dois sistemas de sites nos seguintes casos: se os sites subordinados têm um ponto de atualização de software ou se existe um ponto de atualização de software remoto ativo baseado na Internet num site:  

 **Ponto de atualização de software no site subordinado**  

-   http://&lt*FQDN para o software de ponto de atualização no site filho*>  

-   https://&lt*FQDN para o software de ponto de atualização no site filho*>  

-   http://&lt*FQDN para o software de ponto de atualização no site pai*>  

-   https://&lt*FQDN para o software de ponto de atualização no site pai*>  

##  <a name="BKMK_SyncSettings"></a> Planear as definições de sincronização  
 Sincronização de atualizações de software no Configuration Manager é o processo de recuperar metadados de atualizações de software com base em critérios que você definir. O site de nível superior na sua hierarquia, o site de administração central ou o site primário autónomo sincroniza atualizações de software do Microsoft Update. Você tem a opção de configurar o ponto de atualização de software no site de nível superior para sincronizar com um servidor WSUS existente, não na hierarquia do Configuration Manager. Os sites subordinados principais sincronizam os metadados de atualizações de software a partir do ponto de atualização de software no site de administração central. Antes de instalar e configurar um ponto de atualização de software, utilize esta secção para planear as definições de sincronização.  

###  <a name="BKMK_SyncSource"></a> Origem de sincronização  
 As definições da origem de sincronização para o ponto de atualização de software especificam a localização sobre onde o ponto de atualização de software obtém metadados de atualizações de software e se os eventos de relatório WSUS são criados durante o processo de sincronização.  

-   **Origem da sincronização:** O ponto de atualização de software no site de nível superior configura a origem da sincronização para o Microsoft Update por padrão. Tem a opção de sincronizar o site de nível superior com um servidor WSUS existente. O ponto de atualização de software num site subordinado principal configura a origem de sincronização bem como o ponto de atualização de software no site de administração central por predefinição.  

    > [!NOTE]  
    >  O primeiro ponto de atualização de software que instalar num site primário, que é o ponto de atualização de software predefinido, sincroniza com o site de administração central. Os pontos de atualização de software adicionais no site primário sincronizam-se com o ponto de atualização de software predefinido no site primário.  

     Quando um ponto de atualização de software é desligado do Microsoft Update ou do servidor de atualização a montante, pode configurar a origem de sincronização para não se sincronizar com uma origem de sincronização configurada mas, ao invés, utilizar a função de exportação e importação da ferramenta WSUSUtil para sincronizar as atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventos de relatórios do WSUS:** O Windows Update Agent em computadores cliente pode criar mensagens de eventos que são usadas para relatórios do WSUS. Esses eventos não são usados pela atualização de software no Configuration Manager e, portanto, o **não criar eventos de relatório do WSUS** opção é selecionada por padrão. Quando estes eventos não são criados, o único momento em que o computador cliente se deve ligar ao servidor WSUS é durante a avaliação de atualização de software e análises de compatibilidade. Se esses eventos forem necessários para relatórios fora das atualizações de software no Configuration Manager, você precisará modificar essa configuração para criar eventos de relatórios do WSUS.  

###  <a name="BKMK_SyncSchedule"></a> Agenda de sincronização  
 Você pode configurar o agendamento de sincronização apenas no ponto de atualização de software no site de nível superior na hierarquia do Configuration Manager. Quando configura a agenda de sincronização, o ponto de atualização de software sincroniza-se com a origem de sincronização à data e à hora que especificar. A agenda personalizada permite-lhe sincronizar atualizações de software a uma data e hora em que os pedidos do servidor WSUS, servidor de sites e rede são baixos, como às 2:00 da manhã uma vez por semana. Como alternativa, você pode iniciar a sincronização no site de nível superior usando a **atualizações de Software de sincronização** ação o **todas as atualizações de Software** ou **grupos de atualização de Software** nó no console do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executada num período de tempo que seja adequado ao seu ambiente. Um cenário típico é a definição da agenda de sincronização de atualizações de software para iniciar a execução poucos instantes após a edição de atualização de segurança regular da Microsoft, na segunda terça-feira de cada mês, vulgarmente designada Patch de Terça-feira. Outro cenário típico possível consiste em definir a agenda de sincronização de atualizações de software para ser executada diariamente, caso sejam utilizadas atualizações de software para a entrega de atualizações de definições e de motor do Endpoint Protection.  

 Depois de o ponto de atualização de software concluir a sincronização com êxito, é enviado um pedido de sincronização aos sites subordinados. Se tiver pontos de atualização de software adicionais num site primário, é enviado um pedido de sincronização a cada ponto de atualização de software. O processo é repetido em todos os sites na hierarquia.  

###  <a name="BKMK_UpdateClassifications"></a> Classificações de atualizações  
 Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, serão sincronizados os metadados de atualizações de software para as classificações especificadas. Configuration Manager permite que você sincronize as atualizações de software com as seguintes classificações de atualização:  

-   **Atualizações críticas:** Especifica uma atualização lançada em larga escala para um problema específico que aborda um bug crítico não relacionado à segurança.  

-   **Atualizações de definições:** Especifica uma atualização para vírus ou outros arquivos de definição.  

-   **Pacotes de recursos:** Especifica novos recursos de produtos que são distribuídos fora de uma versão de produto e recursos que normalmente são incluídos na próxima versão completa do produto.  

-   **Atualizações de segurança:** Especifica uma atualização lançada em larga escala para um problema específico do produto relacionadas à segurança.  

-   **Pacotes de serviço:** Especifica um conjunto cumulativo de hotfixes que são aplicados a um aplicativo. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.  

-   **Ferramentas:** Especifica um utilitário ou recurso que ajuda a concluir uma ou mais tarefas.  

-   **Pacotes cumulativos de atualização:** Especifica um conjunto cumulativo de hotfixes que são reunidos para facilitar a implantação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  

-   **Atualizações:** Especifica uma atualização para um aplicativo ou arquivo que está atualmente instalado.  

 As definições de classificação de atualização são configuradas apenas no site de nível superior. As definições de classificação de atualização não são configuradas no ponto de atualização de software em sites subordinados porque os metadados de atualizações de software são replicados desde o site de nível superior até sites subordinados principais. Quando selecionar as classificações de atualização, tenha em atenção que quanto mais classificações selecionar, mais tempo demorará para sincronizar os metadados de atualizações de software.  

> [!WARNING]  
>  Como procedimento recomendado, desmarque todas as classificações antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione as classificações nas propriedades do Componente de Ponto de Atualização de Software e, em seguida, reinicie o processo de sincronização.  

###  <a name="BKMK_UpdateProducts"></a> Produtos  
 Os metadados para cada atualização de software definem um ou mais produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um sistema operativo ou aplicação. Um exemplo de um produto é o Microsoft Windows Server 2008. Uma família de produtos é o sistema operativo base ou a aplicação a partir da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Microsoft Windows, do qual o Microsoft Windows Server 2008 é membro. Pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos.  

 Quando as atualizações de software são aplicáveis a vários produtos, e pelo menos um dos produtos é selecionado para sincronização, todos os produtos aparecerão no console do Configuration Manager mesmo se alguns produtos não foram selecionados. Por exemplo, se o Windows Server 2012 for o único sistema operativo que subscreveu, e se uma atualização de software se aplicar ao Windows Server 2012 e ao Windows Server 2012 Datacenter Edition, ambos os produtos estarão na base de dados do site.  

 As definições do produto são configuradas apenas no site de nível superior. As definições do produto não são configuradas no ponto de atualização de software para sites subordinados porque os metadados de atualizações de software são replicados desde o site de nível superior até sites subordinados principais. Quando selecionar produtos, tenha em atenção que quantos mais produtos selecionar, mais tempo demorará a sincronizar os metadados de atualizações de software.  

> [!IMPORTANT]  
>  O Configuration Manager armazena uma lista de produtos e famílias de produtos que você pode escolher ao instalar primeiro o ponto de atualização de software. Produtos e famílias de produtos que são lançadas após o lançamento do Configuration Manager podem não estar disponíveis para selecionar até que você conclua a sincronização de atualizações de software, que atualiza a lista de produtos disponíveis e as famílias de produtos que você pode escolher. Como procedimento recomendado, desmarque todos os produtos antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione os produtos nas propriedades do Componente de Ponto de Atualização de Software e, em seguida, reinicie o processo de sincronização.  

###  <a name="BKMK_SupersedenceRules"></a>Regras de substituição  
 Normalmente, uma atualização de software que substitui outra atualização de software executa uma ou mais das seguintes ações:  

-   Melhora ou atualiza a correção que foi fornecida por uma ou mais atualizações publicadas anteriormente.  

-   Melhora a eficiência do pacote de ficheiros de atualização substituído, que é instalado em computadores cliente se a atualização for aprovada para instalação. Por exemplo, a atualização substituída poderá conter ficheiros que já não sejam relevantes para a correção ou para os sistemas operativos que são suportados pela nova atualização, por isso esses ficheiros não estão incluídos no pacote de ficheiros de atualização de substituição.  

-   Atualiza as versões mais recentes de um produto. Por outras palavras, atualiza versões que já não são aplicáveis a versões ou configurações antigas de um produto. As atualizações também podem substituir outras atualizações se tiverem sido efetuadas modificações para expandir o suporte de idiomas. Por exemplo, uma versão mais recente de uma atualização de produto do Microsoft Office poderá remover o suporte de um sistema operativo antigo, mas poderá acrescentar suporte adicional para novos idiomas na versão de atualização inicial.  

 Nas propriedades do ponto de atualização de software, é possível especificar que as atualizações de software substituídas expiram de imediato, o que evita que sejam incluídas nas novas implementações e sinaliza as implementações existentes para indicar que contêm uma ou mais atualizações de software expiradas. Em alternativa, pode especificar um prazo para que as atualizações de software substituídas expirem, permitindo-lhe continuar a implementá-las. Considere os seguintes cenários em que poderá ser necessário implementar uma atualização de software substituída:  

-   Se a atualização de software de substituição suportar apenas as versões mais recentes de um sistema operativo e alguns dos computadores cliente tiverem versões anteriores do sistema operativo.  

-   Se uma atualização de software de substituição tiver uma aplicabilidade mais restrita do que a atualização de software que substitui. Esta condição torná-la-ia inadequada para alguns computadores cliente.  

-   Se não tiver sido aprovada uma atualização de software de substituição para implementação no ambiente de produção.  

    > [!NOTE]  
    >  Quando o Configuration Manager define uma atualização de software substituídas **expirado**, ele não define a atualização **expirado** no WSUS. No entanto, quando a tarefa de limpeza do WSUS é executado, as atualizações definido como **expirado** no Configuration Manager são definidas com o status de **recusadas** no WSUS server e o Windows Update Agent em computadores não verificará mais essas atualizações. Isso significa que os clientes continuarão verificar se há uma atualização expirada até que a tarefa de limpeza é executado. Para obter informações sobre a tarefa de limpeza do WSUS, consulte [manutenção de atualizações de Software](/sccm/sum/deploy-use/software-updates-maintenance).
    
###  <a name="BKMK_UpdateLanguages"></a> Idiomas  
 As definições de idioma do ponto de atualização de software permitem configurar os idiomas para os quais os detalhes de resumo (metadados de atualizações de software) estão sincronizados para atualizações de software, e os ficheiros de idioma de atualização de software que serão transferidos para as atualizações de software.  

#### <a name="software-update-file"></a>Ficheiro de atualização de software  
 Os idiomas configurados na definição **Ficheiro de atualização de software** nas propriedades do ponto de atualização de software fornecem o conjunto de idiomas predefinidos que estão disponíveis quando são transferidas atualizações num site. É possível modificar os idiomas que são selecionados por predefinição sempre que as atualizações de software são transferidas ou implementadas. Durante o processo de transferência, os ficheiros de atualização de software dos idiomas configurados são transferidos para a localização da origem do pacote de implementação se os ficheiros de atualização de software estiverem disponíveis no idioma selecionado. Depois, são copiados para a biblioteca de conteúdos no servidor do site e, em seguida, para os pontos de distribuição que estão configurados para o pacote.  

 As definições de idioma do ficheiro de atualização de software devem ser configuradas com os idiomas que são mais utilizados no seu ambiente. Por exemplo, se os computadores cliente que estão atribuídos ao site utilizarem maioritariamente os idiomas inglês e japonês para o sistema operativo ou para as aplicações e raramente forem utilizados outros idiomas no site, selecione Inglês e Japonês na coluna **Ficheiro de Atualização de Software** quando transferir ou implementar a atualização de software e desmarque os outros idiomas. Este procedimento permite utilizar as predefinições da página **Seleção de Idioma** da implementação e transferir assistentes. Também evita que sejam transferidos ficheiros de atualização desnecessários. Essa configuração é definida em cada ponto de atualização de software na hierarquia do Configuration Manager.  

#### <a name="summary-details"></a>Detalhes de resumo  
 Durante o processo de sincronização, as informações dos detalhes de resumo (metadados de atualizações de software) são atualizadas para as atualizações de software nos idiomas especificados. Os metadados fornecem as informações sobre a atualização de software, tais como o nome, a descrição, os produtos suportados pela atualização, a classificação da atualização, o ID do artigo, o URL de transferência, as regras de aplicabilidade, etc.  

 As definições de detalhes de resumo são configuradas apenas no site de nível superior. Os detalhes de resumo não são configurados no ponto de atualização de software dos sites subordinados porque os dados de atualizações de software são replicados do site de administração central para esses sites através de replicação baseada em ficheiros. Ao selecionar os idiomas de detalhes de resumo, selecione apenas os idiomas de que necessita no seu ambiente. Quanto mais idiomas forem selecionados, mais tempo demorará a sincronização dos metadados de atualizações de software. Configuration Manager exibe os metadados de atualizações de software na localidade do sistema operacional no qual o console do Configuration Manager é executado. Se as propriedades localizadas das atualizações de software não estiverem disponíveis no idioma do sistema operativo, as informações das atualizações de software são apresentadas em inglês.  

> [!IMPORTANT]  
>  É importante que você selecione todos os idiomas de detalhes do resumo necessários na hierarquia do Configuration Manager. Quando o ponto de atualização de software no site de nível superior é sincronizado com a origem de sincronização, os idiomas de detalhes de resumo selecionados determinam os metadados de atualizações de software que são obtidos. Se modificar os idiomas de detalhes de resumo depois de a sincronização ter sido executada pelo menos uma vez, os metadados de atualizações de software para os idiomas de detalhes de resumo modificados são obtidos apenas para atualizações de software novas ou atualizadas. As atualizações de software que já foram sincronizadas não são atualizadas com novos metadados para os idiomas modificados, a menos que exista uma alteração da atualização de software na origem de sincronização.  

##  <a name="BKMK_MaintenanceWindow"></a> Planear uma Janela de Manutenção de Atualizações de Software  
 Pode adicionar uma janela de manutenção dedicada para a instalação de atualizações de software. Isto permite-lhe configurar uma janela de manutenção geral e uma janela de manutenção diferente para atualizações de software. Quando uma janela de manutenção geral e a janela de manutenção de atualizações de software estão ambas configuradas, os clientes instalam atualizações de software apenas durante a janela de manutenção de atualizações de software. Para obter mais informações sobre janelas de manutenção, consulte [como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="BKMK_RestartOptions"></a> Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software
Quando uma atualização de software que requer uma reinicialização é implantada usando o Configuration Manager e instalado em um computador, uma reinicialização pendente é agendada e é exibida uma caixa de diálogo de reinicialização.

A partir do Configuration Manager versão 1606, a opção para **Atualizar e Reiniciar**e para **Atualizar e Encerrar** está disponível em computadores Windows 10 nas opções de energia do Windows, sempre que existe um reinício pendente para uma atualização de software do Configuration Manager. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não será apresentada depois do reinício do computador.

Em versões anteriores do Configuration Manager, quando uma reinicialização está pendente para Windows 8 e posteriores computadores, e quando você desligar ou reinicia o computador usando as opções de energia do Windows (em vez de na caixa de diálogo de reinicialização), o permanece de caixa de diálogo de reinicialização depois da reinicialização do computador e o computador ainda será necessário reiniciar o prazo configurado.

## <a name="next-steps"></a>Passos seguintes
Quando você planejar atualizações de software, consulte [gerenciamento de atualizações de preparação para o software](../get-started/prepare-for-software-updates-management.md).

