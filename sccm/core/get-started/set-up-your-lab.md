---
title: "Configurar o seu laboratório System Center Configuration Manager | Microsoft Docs"
description: "Configure um laboratório para avaliar o Configuration Manager com atividades de reais simuladas."
ms.custom: na
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
caps.latest.revision: "11"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a8bacdbde00973cfd45963b355c8f810ab06a83d
ms.sourcegitcommit: 4c3906cf9614420cb8527da9e48978eb0b8f0e7a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/22/2017
---
# <a name="set-up-your-system-center-configuration-manager-lab"></a>Configurar o seu laboratório System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguir as orientações neste tópico irá permitem-lhe configurar um laboratório para avaliar o Configuration Manager com atividades de reais simuladas.  

##  <a name="BKMK_LabCore"></a> Componentes principais  
 Como configurar o ambiente para o System Center Configuration Manager requer alguns componentes principais para suportar a instalação do Configuration Manager.    

-   **O ambiente de laboratório utiliza o Windows Server 2012 R2**, na qual iremos irá instalar o System Center Configuration Manager.  

     Pode transferir uma versão de avaliação do Windows Server 2012 R2 a partir de [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Considere modificar ou desativar a configuração de segurança avançada do Internet Explorer para aceder mais facilmente a algumas das transferências referidas durante estes exercícios. Reveja [Internet Explorer: Configuração de segurança avançada](https://technet.microsoft.com/en-us/library/dd883248\(v=ws.10\).aspx) para obter informações adicionais.  

-   **O ambiente de laboratório utiliza o SQL Server 2012 SP2** para a base de dados do site.  

     Pode transferir uma versão de avaliação do SQL Server 2012 a partir de [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=29066).  

     O SQL Server tem [versões do SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) que devem ser cumpridos para utilização com o System Center Configuration Manager.  

    -   O Configuration Manager requer uma versão de 64 bits do SQL Server para alojar a base de dados do site.  

    -   **SQL_Latin1_General_CP1_CI_AS** como classe do **Agrupamento SQL** . A  

    -   **Autenticação do Windows**, [em vez da autenticação SQL](https://technet.microsoft.com/en-us/library/ms144284.aspx), é necessária.  

    -   Um dedicado **instância do SQL Server** é necessária.  

    -   Não limitar o **memória do sistema endereçável** para o SQL Server.  

    -   Configurar o **conta de serviço do SQL Server** a serem executados utilizando um pouco de direitos de conta de utilizador de domínio.  

    -   Tem de instalar **do SQL Server reporting services**.  

    -   **Comunicações entre locais** utiliza o SQL Server Service Broker na porta predefinida TCP 4022. As  

    -   **Comunicações intra-site** entre o motor de base de dados do SQL Server e o sistema de sites do Configuration Manager Selecione funções de utilizam a porta TCP 1433 predefinida.  

-   **O controlador de domínio utiliza o Windows Server 2008 R2** com serviços de domínio do Active Directory instalado. O controlador de domínio também funciona como o anfitrião para o DHCP e os servidores DNS para utilizam com um nome de domínio completamente qualificado.  

     Para obter mais informações, consulte este [descrição geral dos serviços de domínio do Active Directory](https://technet.microsoft.com/en-us/library/hh831484).  

-   **Hyper-V é utilizado com alguns máquinas de virtuais** para verificar se os passos de gestão executados estes exercícios estão a funcionar conforme esperado. É recomendado um mínimo de três máquinas virtuais, com o Windows 7 (ou posterior) instalado.  

     Para obter mais informações, consulte este [descrição geral do Hyper-V](https://technet.microsoft.com/en-us/library/hh831531.aspx).  

-   **permissões de administrador** são necessárias para todos estes componentes. O  

    -   O Configuration Manager requer um administrador com permissões de segurança no ambiente do Windows Server  

    -   do Active Directory requer um administrador com permissões para modificar o esquema  

    -   Máquinas virtuais requerem permissões locais nas próprias máquinas  

Apesar de não é necessária para este laboratório, pode rever [configurações suportadas para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para obter informações adicionais sobre os requisitos para implementar o System Center Configuration Manager. Consulte a documentação sobre versões de software que não se encontram referenciado aqui.  

Depois de instalar todos estes componentes, existem passos adicionais que deve efetuar para configurar o ambiente do Windows para o Configuration Manager:  

##  <a name="BKMK_LabADPrep"></a> Preparar o conteúdo do Active Directory para o laboratório  
 Para este laboratório, irá criar um grupo de segurança, em seguida, adicionar um utilizador de domínio ao mesmo.  

-   Grupo de segurança: **Avaliação**  

    -   Âmbito do grupo: **Universal**  

    -   Tipo de grupo: **Segurança**  

-   Utilizador de domínio: **ConfigUser**  

     Em circunstâncias normais, não concederia acesso universal a todos os utilizadores no seu ambiente. Está a fazê-lo com este utilizador para simplificar a colocação do seu laboratório online.  

Os passos necessários para permitir que os clientes do Configuration Manager consulta Active Directory Domain Services para localizar recursos de site estão listados por cima dos próximos procedimentos.  

##  <a name="BKMK_CreateSysMgmtLab"></a> Criar o contentor de Gestão do Sistema.  
 O Configuration Manager não criará automaticamente o contentor de gestão do sistema necessário nos serviços de domínio do Active Directory quando o esquema é expandido. Por conseguinte, irá criar este para o laboratório. Este passo irá solicitar-lhe que [instale o Editor de ADSI.](https://technet.microsoft.com/en-us/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)  

 Certifique-se de que iniciou sessão com uma conta que tenha a permissão **Criar Todos os Objetos Subordinados** no recipiente **Sistema** nos Serviços de Domínio do Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Para criar o contentor de Gestão do Sistema:  

1.  Execute o **Editor de ADSI**e estabeleça ligação ao domínio em que reside o servidor de site.  

2.  Expanda **domínio&lt;nome de domínio completamente qualificado\>**, expanda **< nome único\>**, faça duplo clique **CN = System**, clique em **novo**e, em seguida, clique em **objeto**.  

3.  Na caixa de diálogo **Criar Objeto** , selecione **Contentor**e clique em **Seguinte**.  

4.  Na caixa **Valor** , escreva **System Management**e, em seguida, clique em **Seguinte**.  

5.  Clique em **Concluir** para concluir o procedimento.  

##  <a name="BKMK_SetSecPermLab"></a> Definir permissões de segurança no contentor de Gestão do Sistema  
 Conceda à conta do computador do servidor de site as permissões necessárias para publicar informações do site no contentor. Irá utilizar também o Editor de ADSI para esta tarefa.  

> [!IMPORTANT]  
>  Certifique-se de que está ligado ao domínio do servidor de site antes de iniciar o procedimento seguinte.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Para definir permissões de segurança no contentor de Gestão do Sistema:  

1.  No painel de consola, expanda o **o domínio do servidor do site**, expanda **DC =&lt;nome único do servidor\>**e, em seguida, expanda **CN = System**. Clique com o botão direito do rato em **CN=System Management**e clique em **Propriedades**.  

2.  Na caixa de diálogo **CN=Propriedades de gestão do sistema** , clique no separador **Segurança** e, em seguida, clique em **Adicionar** para adicionar a conta de computador do servidor de site. Conceda permissões de **Controlo Total** à conta.  

3.  Clique em **avançadas**, selecione a conta de computador do servidor do site e, em seguida, clique em **editar**.  

4.  Na lista **Aplicar em** , selecione **Este objeto e os objetos subordinados**.  

5.  Clique em **OK** para fechar a consola **Editor de ADSI** e conclua o procedimento.  

     Para obter informações adicionais sobre este procedimento, reveja [expandir o esquema do Active Directory para o System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="BKMK_ExtADSchLab"></a> Expandir o esquema do Active Directory utilizando ExtADSch.exe  
 Irá expandir o esquema do Active Directory para este laboratório, porque isto permite-lhe utilizar todas as funcionalidades do Configuration Manager e funcionalidades com o mínimo de sobrecarga administrativa. A extensão do esquema do Active Directory é uma configuração de toda a floresta e só pode ser efetuada uma vez por floresta. Expandir o esquema permanentemente modifica o conjunto de classes e atributos na configuração base do Active Directory. Esta ação é irreversível. Expandir o esquema permite ao Configuration Manager para aceder a componentes que irão permitir que esta função de forma mais eficaz no seu ambiente de laboratório.  

> [!IMPORTANT]  
>  Certifique-se de que iniciou sessão no controlador de domínio principal do esquema com uma conta que seja membro do grupo de segurança **Admins de esquemas** . Qualquer tentativa de utilizar credenciais alternativas irá falhar.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Para expandir o esquema do Active Directory utilizando ExtADSch.exe:  

1.  Crie uma cópia de segurança do Estado do sistema do controlador de domínio de mestre de esquema. Para obter mais informações sobre como fazer uma cópia de segurança do controlador de domínio principal, consulte [Cópia de Segurança do Windows Server](https://technet.microsoft.com/en-us/library/cc770757.aspx)  

2.  Navegue para **\SMSSETUP\BIN\X64** no suporte de dados de instalação.  

3.  Execute o **extadsch.exe**.  

4.  Certifique-se de que a extensão do esquema foi bem sucedida, revendo o **extadsch.log** localizado na pasta de raiz da unidade do sistema.  

     Para obter informações adicionais sobre este procedimento, reveja [expandir o esquema do Active Directory para o System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="BKMK_OtherTasksLab"></a> Outras tarefas necessárias  
 Também terá de realizar as seguintes tarefas antes da instalação.  

 **Criar uma pasta para armazenar todas as transferências**  

 Durante este exercício, é provável que sejam necessárias várias transferências para os componentes do suporte de instalação. Antes de iniciar os procedimentos de instalação, determine uma localização que não requeira a transferência destes ficheiros até que decida desativar o laboratório. É recomendável utilizar uma única pasta com subpastas separadas para armazenar estas transferências.  

 **Instale o .NET e ative a Windows Communication Foundation**  

 Tem de instalar duas .NET Frameworks: primeiro, a .NET 3.5.1 e depois a .NET 4.5.2+. Terá também de ativar a WCF (Windows Communication Foundation). A WCF foi concebida para oferecer uma abordagem para cálculo distribuído, interoperabilidade abrangente e suporte direto para orientação do serviço e simplifica a programação de aplicações ligadas através de um modelo de programação orientado para o serviço. Reveja [O que é a Windows Communication Foundation?](https://technet.microsoft.com/en-us/subscriptions/ms731082\(v=vs.90\).aspx) para informações adicionais sobre a WCF.  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Para instalar o .NET e ativar a Windows Communication Foundation:  

1.  Abra o **Server Manager**e depois navegue para **Gerir**. Clique em **Adicionar Funções e Funcionalidades** para abrir o **Assistente para Adicionar Funções e Funcionalidades.**  

2.  Reveja as informações fornecidas no painel **Antes de Começar** e, em seguida, clique em **Seguinte**.  

3.  Selecione **Instalação baseada em funções ou funcionalidades**e, em seguida, clique em **Seguinte**.  

4.  Selecione o servidor em **Agrupamento de Servidores**e, em seguida, clique em **Seguinte**.  

5.  Reveja o painel **Funções de Servidor** e, em seguida, clique em **Seguinte**.  

6.  Adicione as seguintes **Funcionalidades** selecionando-as na lista:  

    -   **Funcionalidades do .NET Framework 3.5**  

        -   **.NET Framework 3.5 (inclui .NET 2.0 e 3.0)**  

    -   **Funcionalidades do .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **Serviços WCF**  

            -   **Ativação HTTP**  

            -   **Partilha de portas TCP**  

7.  Reveja **Função de Servidor Web (IIS)** e o ecrã **Serviços de Função** e, em seguida, clique em **Seguinte**.  

8.  Reveja o ecrã **Confirmação** e, em seguida, clique em **Seguinte**.  

9. Clique em **Instalar** e certifique-se de que a instalação foi concluída corretamente no painel **Notificações** do **Gestor de Servidores**.  

10. Depois de concluída a instalação base do .NET, navegue para o [Centro de Transferências da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=42643) para obter o instalador da Web para o .NET Framework 4.5.2. Clique no botão **Transferir** e, em seguida, em **Executar** para iniciar o instalador. O instalador irá detetar e instalar automaticamente os componentes necessários no idioma selecionado.  

Para obter mais informações, consulte os seguintes artigos para saber porque motivo estes .NET Frameworks são necessários:  

-   [Versões e dependências do .NET Framework](https://technet.microsoft.com/en-us/library/bb822049.aspx)  

-   [Instruções de Compatibilidade de Aplicações do .NET Framework 4 RTM](https://technet.microsoft.com/en-us/library/dd889541.aspx)  

-   [Como: Atualizar uma aplicação ASP.NET Web para ASP.NET 4](https://technet.microsoft.com/en-us/library/dd483478\(VS.100\).aspx)  

-   [Perguntas Frequentes sobre a Política de Ciclo de Vida do Microsoft .NET Framework](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR avesso - no processo lado a lado](https://msdn.microsoft.com/en-us/magazine/ee819091.aspx)  

**Ativar BITS, IIS e RDC**  

O [Serviço de Transferência Inteligente em Segundo Plano (BITS)](https://technet.microsoft.com/en-us/library/dn282296.aspx) é utilizado para aplicações que têm de transferir ficheiros assíncronos entre um cliente e um servidor. Ao medir o fluxo de transferências em primeiro e segundo plano, o BITS mantém a capacidade de resposta de outras aplicações de rede. Retoma também automaticamente as transferências de ficheiros se uma sessão de transferência for interrompida.  

O utilizador deve instalar o BITS para este laboratório, porque este servidor de site será também utilizado como ponto de gestão.  

Serviços de Informação Internet (IIS) é um servidor Web flexível e escalável que pode ser utilizado para alojar tudo na Web. É utilizado pelo Configuration Manager para um número de funções de sistema de sites. Para obter informações adicionais sobre o IIS, consulte [sites para servidores de sistema de sites no System Center Configuration Manager](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Compressão de Diferencial Remota (RDC)](https://technet.microsoft.com/en-us/library/cc754372.aspx) é um conjunto de API que as aplicações podem utilizar para determinar se foram efetuadas quaisquer alterações a um conjunto de ficheiros. A RDC permite que a aplicação replique apenas as partes alteradas de um ficheiro, mantendo o tráfego de rede para um mínimo.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Para ativar as funções de servidor de site BITS, IIS e RDC:  

1.  No servidor de site, abra **Server Manager**. Navegue para **Gerir**. Clique em **Adicionar Funções e Funcionalidades** para abrir o **Assistente para Adicionar Funções e Funcionalidades**.  

2.  Reveja as informações fornecidas no painel **Antes de Começar** e, em seguida, clique em **Seguinte**.  

3.  Selecione **Instalação baseada em funções ou funcionalidades**e, em seguida, clique em **Seguinte**.  

4.  Selecione o servidor em **Agrupamento de Servidores**e, em seguida, clique em **Seguinte**.  

5.  Adicione as seguintes **Funções de Servidor** selecionando-as na lista:  

    -   **Servidor Web (IIS)**  

        -   **Funcionalidades HTTP Comuns**  

            -   **Documento Predefinido**  

            -   **Navegação nos Diretórios**  

            -   **Erros de HTTP**  

            -   **Conteúdo Estático**  

            -   **Redirecionamento HTTP**  

        -   **Estado de Funcionamento e de Diagnóstico**  

            -   **Registo HTTP**  

            -   **Ferramentas de Registo**  

            -   **Monitor de Pedidos**  

            -   **Rastreio**  

    -   **Desempenho**  

        -   **Compressão de Conteúdo Estático**  

        -   **Compressão de Conteúdo Dinâmico**  

    -   **Security**  

        -   **Filtragem de Pedidos**  

        -   **Autenticação Básica**  

        -   **Autenticação por Mapeamento de Certificados de Clientes**  

        -   **Restrições de Domínio e de IP**  

        -   **Autorização de URL**  

        -   **Autorização do Windows**  

    -   **Programação de Aplicações**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **Extensões ISAPI**  

        -   **Filtros ISAPI**  

        -   **O Lado do Servidor Inclui**  

    -   **Servidor FTP**  

        -   **Serviço FTP**  

    -   **Ferramentas de Gestão**  

        -   **Consola de Gestão do IIS**  

        -   **Compatibilidade de Gestão do IIS 6**  

            -   **Compatibilidade com Metabase do IIS 6**  

            -   **Consola de Gestão do IIS 6**  

            -   **Ferramentas de Scripts do IIS 6**  

            -   **Compatibilidade com WMI do IIS 6**  

        -   **Scripts e Ferramentas de Gestão do IIS 6**  

        -   **Serviço de Gestão**  

6.  Adicione as seguintes **Funcionalidades** selecionando-as na lista:  

    -   **Serviço de Transferência Inteligente em Segundo Plano (BITS)**  

          -   **Extensão de Servidor IIS**  

    -   **Ferramentas de Administração Remota do Servidor**  

          -   **Ferramentas de Administração de Funcionalidades**  

          -   **Ferramentas de Extensões de Servidor BITS**  

7.  Clique em **Instalar** e certifique-se de que a instalação foi concluída corretamente no painel **Notificações** do **Gestor de Servidores**.  

Por predefinição, o IIS bloqueia vários tipos de extensões de ficheiro e localizações de pastas contra o acesso através de comunicação HTTP ou HTTPS. Para permitir que estes ficheiros sejam distribuídos a sistemas cliente, terá de configurar a filtragem de pedidos do IIS no ponto de distribuição. Para obter mais informações, consulte [IIS filtragem de pedidos para pontos de distribuição](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Para configurar a filtragem de IIS nos pontos de distribuição:  

1.  Abra **IIS Manager** e selecione o nome do seu servidor na barra lateral. Esta ação permite-lhe aceder ao ecrã **Início** .  

2.  Certifique-se de que **Vista de Funcionalidades** está selecionada na parte inferior do ecrã **Início** . Navegue para **IIS** e abra **Filtragem de Pedidos**.  

3.  No painel **Ações** , clique em **Permitir Extensão de Nome de Ficheiro…**  

4.  Introduza **.msi** na caixa de diálogo e clique em **OK**.  

##  <a name="BKMK_InstallCMLab"></a> Instalar o Gestor de Configuração  
Irá criar um [determinar quando deve utilizar um site primário](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) para gerir clientes diretamente. Isto permitirá que o seu ambiente de laboratório suportar a gestão para [escala do sistema de sites](/sccm/core/plan-design/configs/size-and-scale-numbers) de potenciais dispositivos.  
Durante este processo, irá também instalar a consola do Configuration Manager, que será utilizada para gerir os dispositivos de avaliação passa.  

Antes de iniciar a instalação, inicie o [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) no servidor utilizando o Windows Server 2012 para confirmar que todas as definições foram ativadas corretamente.  

#### <a name="to-download-and-install-configuration-manager"></a>Para transferir e instalar o Gestor de Configuração:  

1.  Navegue para o [avaliações do System Center](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) página para transferir a versão de avaliação mais recente do System Center Configuration Manager.  

2.  Descomprima o suporte de dados de transferência para a localização predefinida.  

3.  Siga o procedimento de instalação listado em [instalar um site utilizando o Assistente de configuração do System Center Configuration Manager](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites). De acordo com esse procedimento, deve introduzir o seguinte:  

    |Passo no procedimento de instalação do site|Seleção|  
    |-----------------------------------------|---------------|  
    |Passo 4: a página **Chave de produto**|Selecione **Avaliação**.|  
    |Passo 7:  **Transferências de pré-requisitos**|Selecione **Transferir ficheiros necessários** e especifique a localização predefinida.|  
    |Passo 10: **Definições de instalação e site**|-   **Código do site:LAB**<br />-   **Nome do site:Evaluation**<br />-   **Pasta de instalação:** especifique a localização predefinida.|  
    |Passo 11: **Instalação de Site principal**|Selecione **Instalar o site principal como um site autónomo**, em seguida, clique em **Seguinte**.|  
    |Passo 12: **Instalação da base de dados**|-   **Nome de SQL Server (FQDN):** aqui o FQDN.<br />-   **Nome da instância:** deixe em branco, porque irá utilizar a instância predefinida do SQL que instalou anteriormente.<br />-   **Porta do Service Broker:** deixe como a porta predefinida de 4022.|  
    |Passo 13: **Instalação da base de dados**|Deixe estas definições como a predefinição.|  
    |Passo 14: **Fornecedor de SMS**|Deixe estas definições como a predefinição.|  
    |Passo 15: **Definições de comunicação de cliente**|Confirme se **Todas as funções do sistema de site aceitam apenas comunicação HTTPS dos clientes** não estiver selecionada|  
    |Passo 16: **Funções do sistema de sites**|Introduza o FQDN e confirme que a seleção de **Todas as funções do sistema de site aceitam apenas comunicação HTTPS dos clientes** ainda está desmarcada.|  

##  <a name="BKMK_EnablePubLab"></a>Ativar a publicação para o site do Configuration Manager  
Cada site do Configuration Manager publica as suas próprias informações específicas de site no contentor de gestão do sistema na sua partição de domínio no esquema do Active Directory. Os canais Bidirecionais de comunicação entre o Active Directory e do Configuration Manager devem ser abertos para processar este tráfego. Irá também ativar a Deteção de Florestas para determinar certos componentes do seu Active Directory e da infraestrutura de rede.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação:  

1.  No canto inferior esquerdo da consola do Configuration Manager, clique em **administração**.  

2.  Na área de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Métodos de Deteção**.  

3.  Selecione **Deteção de Florestas do Active Directory** e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , selecione **Ativar Deteção de Floresta do Active Directory**. Quando esta opção estiver ativa, selecione **Criar limites de site do Active Directory automaticamente quando os mesmos forem detetados**. É apresentada uma caixa de diálogo que indica **Quer executar a deteção completa assim que possível?** Clique em **Sim**.  

5.  No grupo **Método de Deteção** na parte superior do ecrã, clique em **Executar Agora a Deteção de Florestas**e, em seguida, navegue para **Florestas do Active Directory** na barra lateral. A floresta do Active Directory deve ser mostrada na lista de florestas detetadas.  

6.  Navegue para a parte superior do ecrã, para o separador **Geral** .  

7.  Na área de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Florestas do Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Para ativar um site do Configuration Manager publicar informações do site para a floresta do Active Directory:  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Irá configurar uma nova floresta que ainda não tenha sido detetada.  

3.  Na área de trabalho **Administração** , clique em **Florestas do Active Directory**.  

4.  No separador **Publicação** das propriedades do site, selecione a floresta ligada e, em seguida, clique em **Ok** para guardar a configuração.
