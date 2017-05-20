---

title: "Instalar e configurar um ponto de atualização de software | Documentos do Microsoft"
description: "Sites primários necessitam de um ponto de atualização de software no site de administração central para avaliação de compatibilidade de atualizações de software e implementar software atualizações de clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.translationtype: Machine Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 1d9911274fd76942131054231cdcc2bcebbd3fcb
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017



---


# <a name="install-and-configure-a-software-update-point"></a>Instalar e configurar um ponto de atualização de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


> [!IMPORTANT]  
>  Antes de instalar a função do sistema de sites do ponto de atualização de software, terá de verificar que o servidor cumpre as dependências necessárias e determina a infraestrutura do ponto de atualização de software no site. Para mais informações sobre como planear atualizações de software e como determinar a sua infraestrutura de ponto de atualização de software, consulte o artigo [planear atualizações de software](../plan-design/plan-for-software-updates.md).  

 O ponto de atualização de software é necessário no site de administração central e nos sites primários para ativar a avaliação de compatibilidade das atualizações de software e para implementar atualizações de software em clientes. O ponto de atualização de software é opcional em site secundários. A função do sistema de sites do ponto de atualização de software tem de ser criada num servidor com o WSUS instalado. O ponto de atualização de software interage com os serviços WSUS para configurar as definições de atualização de software e para solicitar a sincronização de metadados de atualizações de software. Quando tiver uma hierarquia do Configuration Manager, instalar e configurar o ponto de atualização de software no site de administração central em primeiro lugar, em seguida, em sites primários subordinados e, em seguida, opcionalmente, em sites secundários. Quando tiver um site primário autónomo, não um site de administração central, comece por instalar e configurar o ponto de atualização de software no site primário e, depois, como opção, em sites secundários. Algumas definições só estão disponíveis quando configura o ponto de atualização de software num site de nível superior. Existem diferentes opções que tem de considerar dependendo de onde instalou o ponto de atualização de software.  

> [!IMPORTANT]  
>  Pode instalar mais do que um ponto de atualização de software num site. O primeiro ponto de atualização de software que instala é configurado como a origem de sincronização, que sincroniza as atualizações do Microsoft Update ou da origem de sincronização a montante. Os outros pontos de atualização de software no site são configurados como réplicas do primeiro ponto de atualização de software. Por conseguinte, algumas definições não estão disponíveis depois de instalar e configurar o ponto de atualização de software inicial.  

 Pode adicionar a função do sistema de sites do ponto de atualização de software a um servidor de sistema de sites existente ou pode criar uma nova. Na página **Seleção da Função do Sistema** do **Assistente para Criar Servidor do Sistema de Sites** ou do **Assistente para Adicionar Funções ao Sistema de Sites** , consoante opte por adicionar a função do sistema de sites a um servidor de sites novo ou existente, selecione **Ponto de atualização de software**e, em seguida, configure as definições do ponto de atualização de software no assistente. As definições são diferentes consoante a versão do Configuration Manager que utilizar. Para obter mais informações sobre como instalar as funções de sistema de sites, consulte o artigo [instalar funções do sistema de sites](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Utilize as secções seguintes para obter informações sobre as definições do ponto de atualização de software num site.  

## <a name="proxy-server-settings"></a>Definições do servidor proxy  
 Pode configurar as definições do servidor proxy em diferentes páginas do **criar Assistente de servidor de sistema de sites** ou **Adicionar Assistente de funções de sistema de sites** consoante a versão do Configuration Manager que utilizar.  

-   Tem de configurar o servidor proxy e, em seguida, especificar quando utilizar o servidor proxy para atualizações de software. Configure as seguintes definições:  

    -   Configure as definições do servidor proxy na página **Proxy** do assistente ou no separador **Proxy** em Propriedades do sistema de sites. As definições do servidor proxy são específicas do sistema de sites, o que significa que todas as funções do sistema de sites utilizam as definições do servidor proxy que especificou.  

    -   Especifique se utilizar o servidor proxy quando o software do Configuration Manager a sincronizar as atualizações e quando transfere conteúdo utilizando uma regra de implementação automática. Configure as definições do servidor proxy do ponto de atualização de software na página **Definições de Proxy e de Conta** do assistente ou no separador **Definições de Proxy e de Conta** em Propriedades do ponto de atualização de software.  

        > [!NOTE]  
        >  A definição **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática** está disponível, mas não é utilizada para um ponto de atualização de software num site secundário. Apenas o ponto de atualização de software no site de administração central e site primário transfere conteúdo a partir da página do Microsoft Update.  

> [!IMPORTANT]  
>  Por predefinição, a conta **Sistema Local** para o servidor onde foi criada uma regra de implementação automática serve para ligar à Internet e transferir atualizações de software quando são executadas as regras de implementação automática. Quando esta conta não tiver acesso à Internet, as atualizações de software não são transferidas e a entrada seguinte é registada para ruleengine. log: **Falha ao transferir a atualização a partir da internet. Erro = 12007**. Configure as credenciais para ligar ao servidor proxy quando a conta do Sistema Local não tem acesso à Internet.  


## <a name="wsus-settings"></a>Definições de WSUS  
 Tem de configurar definições de WSUS em diferentes páginas do **criar Assistente de servidor de sistema de sites** ou **Adicionar Assistente de funções de sistema de sites** dependendo da versão do Configuration Manager que utiliza em alguns casos, apenas nas propriedades para o software de ponto de atualização, também conhecido como atualizar o ponto de propriedades do componente Software. Utilize as informações nas secções seguintes para configurar as definições de WSUS.  

### <a name="BKMK_wsusport"></a>Definições da porta WSUS  
 Tem de configurar as definições da porta WSUS na página Ponto de Atualização de Software do assistente ou nas propriedades do ponto de atualização de software. Utilize o procedimento seguinte para determinar as definições de porta utilizadas pelo WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Para determinar as definições de porta utilizadas no IIS  

 1.  No servidor WSUS, abra o Gestor de Serviços de Informação Internet (IIS).  

 2.  Expanda **Web Sites**, clique com o botão direito do rato no Web site do servidor WSUS e, em seguida, clique em **Editar Enlaces**. Na caixa de diálogo Enlaces de Site, os valores das portas HTTP e HTTPS são apresentados na coluna **Porta** .


### <a name="configure-ssl-communications-to-wsus"></a>Configurar comunicações SSL para WSUS  
 Pode configurar a comunicação SSL na página **Geral** do assistente ou no separador **Geral** nas propriedades do ponto de atualização de software.  

 Para obter mais informações sobre como utilizar o SSL, veja [Decidir se pretende configurar o WSUS para utilizar SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>Conta de Ligação ao Servidor WSUS  
 Pode configurar uma conta para ser utilizada pelo servidor de sites quando estabelece ligação com o WSUS que é executado no ponto de atualização de software. Quando não configura esta conta, o Configuration Manager utiliza a conta de computador do servidor do site para ligar ao WSUS. Configure a Conta de Ligação ao Servidor WSUS na página **Definições de Proxy e de Conta** do assistente ou no separador **Definições de Proxy e de Conta** em Propriedades do ponto de atualização de software.  Pode configurar a conta em diferentes locais do assistente dependendo da versão do Configuration Manager que utilizar.  

 Para mais informações sobre contas do Configuration Manager, consulte o artigo [contas utilizadas no System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Origem de sincronização  
 Pode configurar a origem de sincronização a montante para a sincronização de atualizações de software na página **Origem de Sincronização** do assistente ou no separador **Definições de Sincronização** das Propriedades do Componente do Ponto de Atualização de Software. As opções de origem de sincronização disponíveis variam consoante o site.  

 Utilize a seguinte tabela para obter as opções disponíveis para configurar o ponto de atualização de software num Web site.  

|Site|Opções de origem de sincronização disponíveis|  
|----------|----------------------------------------------|  
|-   Site de administração central<br />-   Site primário autónomo|-   Sincronizar a partir do site do Microsoft Update<br />-   Sincronizar a partir de uma localização de origem de dados a montante<br />-   Não sincronizar a partir do Microsoft Update nem da origem de dados a montante|  
|-   Pontos de atualização de software adicionais num site<br />-   Site primário subordinado<br />-   Site secundário|-   Sincronizar a partir de uma localização de origem de dados a montante|  

 A seguinte lista contém mais informações sobre cada uma das opções que pode utilizar como origem de sincronização:  

-   **Sincronizar a partir do Microsoft Update**: Utilize esta definição para sincronizar metadados de atualizações de software a partir do Microsoft Update. O site de administração central necessita de ter acesso à Internet, caso contrário a sincronização irá falhar. Esta definição apenas está disponível se configurar o ponto de atualização de software no site de nível superior.  

    > [!NOTE]  
    >  Se existir uma firewall entre o ponto de atualização de software e a Internet, a firewall poderá ter de ser configurada para aceitar as portas HTTP e HTTPS utilizadas pelo Web site do WSUS. Também pode optar por restringir o acesso a domínios limitados na firewall. Para obter mais informações sobre como planear a utilização de uma firewall que suporte atualizações de software, veja [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **Sincronizar a partir de uma localização de origem de dados a montante**: Utilize esta definição para sincronizar metadados de atualizações de software a partir da origem de sincronização a montante. Os sites primários subordinados e sites secundários são automaticamente configurados para utilizar o URL do site principal para esta definição. Pode optar por sincronizar as atualizações de software a partir de um servidor WSUS existente. Especifique um URL, por exemplo https://WSUSServer:8531, em que 8531 corresponde à porta que é utilizada para estabelecer a ligação ao servidor WSUS.  

-   **Não sincronizar a partir do Microsoft Update ou origem de dados a montante**: Utilize esta definição para sincronizar manualmente as atualizações de software quando o ponto de atualização de software no site de nível superior está desligado da Internet. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Se existir uma firewall entre o ponto de atualização de software e a Internet, a firewall poderá ter de ser configurada para aceitar as portas HTTP e HTTPS utilizadas pelo Web site do WSUS. Também pode optar por restringir o acesso a domínios limitados na firewall. Para obter mais informações sobre como planear a utilização de uma firewall que suporte atualizações de software, veja [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Também pode configurar a criação de eventos de relatório do WSUS na página **Origem de Sincronização** do assistente ou no separador **Definições de Sincronização** das Propriedades do Componente do Ponto de Atualização de Software. O Configuration Manager não utiliza estes eventos; Por conseguinte, normalmente deverá selecionar a definição predefinida **não criar eventos de relatório WSUS**.  

## <a name="synchronization-schedule"></a>Agenda de sincronização  
 Configure o agendamento da sincronização na página **Agendamento da Sincronização** do assistente ou nas Propriedades do Componente do Ponto de Atualização de Software. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

 Se ativar a agenda, poderá configurar uma agenda de sincronização periódica simples ou personalizada. Quando configura uma agenda simples, a hora de início baseia-se na hora local do computador que executa a consola do Configuration Manager ao tempo ao criar a agenda. Quando configura a hora de início de uma agenda personalizada, baseia-se a hora local para o computador que executa a consola do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executada num período de tempo que seja adequado ao seu ambiente. Um cenário de típico é a definição da agenda de sincronização de atualizações de software para iniciar a execução poucos instantes após a edição de atualização de segurança regular da Microsoft, na segunda terça-feira de cada mês, vulgarmente designada Patch Terça. Outro cenário típico possível consiste em definir a agenda de sincronização de atualizações de software para ser executada diariamente, caso sejam utilizadas atualizações de software para a entrega de atualizações de definições e de motor do Endpoint Protection.  

> [!NOTE]  
>  Se optar por não ativar a sincronização de atualizações de software com base num agendamento, poderá sincronizar manualmente as atualizações de software a partir do nó **Todas as Atualizações de Software** ou **Grupos de Atualização de Software** na área de trabalho Biblioteca de Software. Para obter mais informações, consulte o artigo [sincronizar atualizações de software](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Regras de substituição  
 Configure as definições de substituição na página **Regras de Substituição** do assistente ou no separador **Regras de Substituição** das Propriedades do Componente do Ponto de Atualização de Software. Apenas pode configurar as regras de substituição no site de nível superior.  

 Esta página permite especificar que as atualizações de software substituídas expiram de imediato, o que evitará que sejam incluídas nas novas implementações e instrui as implementações existentes para informar que as atualizações de software substituídas contêm uma ou mais atualizações de software expiradas. Em alternativa, pode especificar um prazo para que as atualizações de software substituídas expirem, permitindo-lhe continuar a implementá-las. Para obter mais informações, veja [Regras de substituição](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  A página **Regras de Substituição** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

## <a name="classifications"></a>Classificações  
 Configure as definições de classificações na página **Classificações** do assistente ou no separador **Classificações** das Propriedades do Componente do Ponto de Atualização de Software. Para obter mais informações sobre as classificações das atualizações de software, veja [Classificações de atualizações](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  A página **Classificações** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Quando instalar o ponto de atualização de software no site de nível superior pela primeira vez, desmarque todas as classificações de atualizações de software. Após a sincronização inicial de atualizações de software, configure as classificações a partir de uma lista atualizada e, em seguida, reinicie o processo de sincronização. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

## <a name="products"></a>Produtos  
 Configure as definições do produto na página **Produtos** do assistente ou no separador **Produtos** das Propriedades do Componente do Ponto de Atualização de Software.  

> [!NOTE]  
>  A página **Produtos** do assistente apenas estará disponível se configurar o primeiro ponto de atualização de software no site. Esta página não é apresentada quando instala pontos de atualização de software adicionais.  

> [!TIP]  
>  Quando instalar o ponto de atualização de software no site de nível superior pela primeira vez, desmarque todos os produtos. Após a sincronização inicial de atualizações de software, configure os produtos a partir de uma lista atualizada e, em seguida, reinicie a sincronização. Esta definição só é configurada no ponto de atualização de software do site de nível superior.  

## <a name="languages"></a>Idiomas  
 Configure as definições de idioma na página **Idiomas** do assistente ou no separador **Idiomas** das Propriedades do Componente do Ponto de Atualização de Software. Especifique os idiomas e detalhes de resumo que pretende incluir nos ficheiros de sincronização da atualização de software. O **ficheiro de atualização de Software** definição é configurada em cada ponto de atualização de software na hierarquia do Configuration Manager. As definições de **Detalhes do Resumo** apenas são configuradas no ponto de atualização de software de nível superior. Para obter mais informações, veja [Idiomas](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  A página **Idiomas** do assistente apenas estará disponível se instalar o ponto de atualização de software no site de administração central. Pode configurar os idiomas do Ficheiro de Atualização do Software em sites subordinados a partir do separador **Idiomas** das Propriedades do Componente do Ponto de Atualização de Software.  

## <a name="next-steps"></a>Passos seguintes
Instalou o ponto de atualização de software começando no site de superior na sua hierarquia do Configuration Manager. Repita os procedimentos neste tópico para instalar o ponto de atualização de software em sites subordinados.

Depois de ter o software instalados de pontos de atualização, aceda a [sincronizar atualizações de software](synchronize-software-updates.md).

