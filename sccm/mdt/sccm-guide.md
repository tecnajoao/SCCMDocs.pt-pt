---
title: "Início rápido - System Center 2012 R2 Configuration Manager"
titleSuffix: Microsoft Deployment Toolkit
description: "Um guia de início rápido de mensagens em fila para o Microsoft Deployment Toolkit com o System Center 2012 R2 Configuration Manager. "
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: b12de852-a799-4c16-b51c-cc3abbd3ca3a
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 8f768ec6eef945163667b346118d2d65dcb2e3c6
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
---
# <a name="quick-start-guide-for-microsoft-system-center-2012-r2-configuration-manager"></a>Guia de introdução do Microsoft System Center 2012 R2 Configuration Manager  
 Microsoft Deployment Toolkit (MDT) 2013 fornece tecnologias para implementar sistemas operativos Windows e Microsoft Office. Este guia de introdução ajuda-o a avaliar rapidamente o MDT 2013, fornecendo instruções passo a passo condensed para utilizá-la para instalar o sistema operativo do Windows 8.1 com o Microsoft System Center 2012 R2 Configuration Manager. Este guia de introdução demonstra como efetuar o cenário de implementação do novo computador, que abrange a implementação do Windows 8.1 para um novo computador. Este cenário pressupõe que não há nenhum perfil para preservar ou dados de utilizador.  

> [!NOTE]     
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

 Depois de utilizar este guia para avaliar o MDT, reveja o resto da documentação de orientação do MDT para saber mais sobre as funcionalidades avançadas da tecnologia.  

## <a name="prerequisites"></a>Pré-requisitos  
 Instalações zero Touch instalação através do Configuration Manager tem os seguintes pré-requisitos.  

### <a name="required-software"></a>Software necessário  
 Para concluir este guia, é necessário o seguinte software:  

-   Windows Server 2008 R2  

-   Microsoft SQL Server 2008 R2  

-   SQL Server 2008 R2 Service Pack 1 (SP1)  

-   SQL Server 2008 R2 SP1 a atualização cumulativa 6 (CU6)  

-   Windows 8,1  

-   System Center 2012 R2 Configuration Manager  

-   Microsoft .NET Framework versão 3.5 com SP1  

-   Windows PowerShell versão 2.0  

-   Ambiente de pré-instalação do Windows (Windows PE), que está incluído no Configuration Manager  

-   Serviços de rede, incluindo o sistema de nomes de domínio (DNS) e protocolo de configuração dinâmica de anfitrião (DHCP)  

-   Serviços de domínio do Active Directory (AD DS)  

 Consulte o [configurações suportadas para o Configuration Manager](http://technet.microsoft.com/library/gg682077.aspx) para combinações de software adicionais que podem ser utilizadas para instalar o Configuration Manager.  

> [!NOTE]   
>  O sequenciador de tarefas utilizados em implementações de MDT requer que criar Global à direita possível atribuir o objeto para as credenciais utilizadas para aceder e executar o Deployment Workbench e o processo de implementação. Este direito está normalmente disponível para contas com permissões ao nível do administrador (a menos que removeu explicitamente). Além disso, a segurança especializada – perfil de segurança da funcionalidade limitada (SSLF) remove o direito de criar a objetos globais e não deve ser aplicada a computadores implementados com o MDT.  

### <a name="computer-configuration"></a>Configuração do computador  
 Para concluir este guia, configure os computadores listados na seguinte tabela. Estes computadores podem ser computadores físicos ou máquinas virtuais (VMs) com os recursos de sistema designados.  


|**Computador**|**A descrição e o sistema de recursos**|  
|-|-|  
|WDG-MDT-01|Este computador é executada a infraestrutura do MDT e o Configuration Manager. O computador executar o Windows Server 2008 R2 com os seguintes serviços de rede instalados:<br /><br /> -AD DS<br />-Servidor DNS<br />-DHCP Server<br />-Serviços de implementação<br /><br /> Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador quad-core em execução em 2,66 gigahertz (GHz) ou mais rápida<br />-igual ou superior de memória física 4 gigabytes (GB)<br />-A partição de disco que tem 40 GB ou mais de espaço em disco disponível; ele irá tornar-se a partição da unidade C<br />-Um CD-ROM ou DVD-ROM unidade que será atribuída a letra de unidade D<br />-A partição de disco que tem 40 GB ou mais de espaço em disco disponível; irá tornar-se a partição E.|  
|WDG-REF-01|Este é o computador de referência, que é executada sem sistema operativo atual. Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador que executa a 1,4 GHz ou mais rápida<br />-1 GB ou mais memória física<br />-16 GB ou mais de espaço em disco disponível|  
|WDG-CLI-01|Este é o computador de destino, que é executada sem sistema operativo atual. Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador que executa a 1,4 GHz ou mais rápida<br />-1 GB ou mais memória física<br />-16 GB ou mais de espaço em disco disponível|  

 Os recursos listados na tabela anterior refletem os recursos de sistema recomendados para executar os passos neste guia. Para informações sobre os requisitos de recursos de sistema mínimos para:  

-   Windows Server 2008 R2, consulte [instalar o Windows Server 2008 R2](http://technet.microsoft.com/library/dd379511.aspx)  

-   SQL Server 2008 R2, consulte [Hardware e requisitos de Software para instalar o SQL Server 2008 R2](http://technet.microsoft.com/library/ms143506.aspx)  

> [!NOTE]   
>  Este guia pressupõe que o MDT está a ser avaliado nos computadores físicos ou virtuais de 64 bits (x64). Se a avaliar o MDT nas plataformas de 32 bits (x86), transferência e instalação x86 edições do MDT e os componentes que este guia descreve.  

## <a name="step-1-prepare-the-prerequisite-infrastructure"></a>Passo 1: Preparar a infraestrutura de pré-requisito  
 Para efeitos deste guia, todos os serviços de infraestrutura de pré-requisito executado no computador com o nome *WDG-MDT-01*. Instale funções de servidor, serviços e software de pré-requisito neste computador antes de instalar o MDT.  

> [!NOTE]   
>  Esta secção assume que está a criar uma nova infraestrutura do Configuration Manager para o MDT. Se estiver a utilizar uma infraestrutura existente do Configuration Manager, reveja os passos nesta secção e substitua os nomes de recursos existente para os recursos criados nesta secção (por exemplo, o nome do computador e as pastas partilhadas na rede). Depois de rever nesta secção, avance para [passo 2: Preparar o ambiente do MDT](#PrepareMDTEnvironment).  

 Prepare a infraestrutura de pré-requisito antes de instalar o MDT por:  

-   Instalar o Windows Server 2008 R2, tal como descrito no [passo 1-1: Instale o Windows Server 2008 R2](#InstallWindowsServer)  

-   Criar as pastas necessárias e a rede partilhas conforme descrito em [passo 1-2: Criar as pastas necessárias e partilhas de rede](#CreateRequiredFolders)  

-   Obter o software necessário para executar os passos neste guia, conforme descrito em [passo 1-3: Obter o Software necessário](#ObtainRequiredSoftware)  

-   Instalar a função de servidor do AD DS, conforme descrito em [passo 1-4: Instalar a função de servidor DS AD](#InstallADDSRole)  

-   Instalar a função de servidor do servidor DHCP, conforme descrito em [passo 1-5: Instalar a função de servidor do servidor DHCP](#InstallDHCPServerRole)  

-   Instalar a função de servidor serviços Web (IIS), conforme descrito em [passo 1-6: Instalar a função de servidor do Web Services (IIS)](#InstallIISRole)  

-   Adicionar as funcionalidades do Windows Server 2008 R2 necessárias, conforme descrito em [passo 1-7: Adicionar as funcionalidades do necessários do Windows Server 2008 R2](#AddRequiredServerFeatures)  

-   Criar as contas de utilizador e o serviço necessário para executar os passos neste guia, conforme descrito em [passo 1-8: Criar o utilizador necessário e contas de serviço](#CreateRequiredUserAccounts)  

-   Instalar o SQL Server 2008 R2 para o Configuration Manager para utilizar conforme descrito em [passo 1 e 9: Instale o SQL Server 2008 R2](#InstallSQLServer)  

-   Adicionar o servidor do site para o grupo de segurança de administradores, conforme descrito em [passo 1 a 10: Adicione o servidor de Site para o grupo de segurança de administradores](#AddSiteSecuritytoAdminGroup)  

-   Instalar o Configuration Manager conforme descrito em [passo 1-11: Instalar o Configuration Manager](#InstallConfigManager)  

-   Configurar a conta de acesso de rede que utilizam a clientes do Configuration Manager para aceder a distribuição do Configuration Manager pontos conforme descrito em [passo 1-12: Configurar a conta de acesso de rede](#ConfigureNetworkAccessAccount)  

-   Configurar os limites de site do Configuration Manager e os grupos de limites, conforme descrito em [passo 1-13: Configurar os limites de Site do Configuration Manager e os grupos de limites](#ConfigurationManagerSiteBoundaries)  

-   Configurar a publicação de informações do site no AD DS e DNS, conforme descrito em [passo 1-14: Configurar a publicação de informações do Site no AD DS e DNS](#ConfigurePublishingSiteInfo)  

###  <a name="InstallWindowsServer"></a>Passo 1-1: Instale o Windows Server 2008 R2  
  Informações para instalar o Windows Server 2008 R2.  Aceite os valores predefinidos exceto indicação em contrário.  

|Quando lhe for pedido para| Forneça estes valores|   
|-|-|  
|**Onde pretende instalar o Windows?**|**Disco 0 espaço não alocado**|  
|**Palavra-passe**|Qualquer palavra-passe segura|  
|**Nome do computador**|**WDG-MDT-01**|  
|**Formato para os volumes C e i**|**NTFS**|  
|**Configuração de TCP/IP**|Configurar com uma configuração de endereço IP estático, com as outras opções de configuração de TCP/IP conforme apropriado para o ambiente|  

###  <a name="CreateRequiredFolders"></a>Passo 1-2: Criar as pastas necessárias e partilhas de rede  
 O processo de implementação do MDT requer pastas adicionais que são utilizadas como origem para ficheiros ou para armazenar ficheiros criados durante o processo de implementação do MDT. Alguns destas pastas tem de ser partilhado para que possa ser acedidos a partir de outros computadores.  

#### <a name="to-create-the-required-folders-and-share"></a>Para criar as pastas necessárias e partilhar  
1. O processo de implementação do MDT requer várias pastas. Crie as seguintes pastas e partilhas com as permissões especificadas para cada partilha.    

  |Criar esta pasta  |Com este nome de partilha  |Com estas permissões de partilha.  |  
  |----|----|----|  
  |E:\Source$|$ De origem|**Administradores:** Coproprietário<br /><br /> **Todos os utilizadores:** Leitura|  
  |E:\Images$|$ De imagens|**Administradores:** Coproprietário<br /><br /> **Todos os utilizadores:** Leitura|  
  |E:\Capture$|Capturar$|**Administradores:** Coproprietário<br /><br /> **Todos os utilizadores:** Leitura|  
  |E:\Packages$|$ De pacotes|**Administradores:** Coproprietário<br /><br /> **Todos os utilizadores:** Leitura|  

2. Crie as seguintes pastas:  

    -   E:\CMDownloads  

    -   E:\Source$\CustomSettings  

    -   E:\Source$\Drivers  

    -   E:\Source$\Windows_8-1  

    -   E:Source$ MDT_2013  

    -   E:Source$ SQL2008R2  

    -   E:Source$ SQL2008R2SP1  

    -   E:Source$ SQL2008R2CU6  

    -   E:Source$ ConfigMgr  

    -   E:Packages$ controladores  

3. Copie os controladores de dispositivo para o computador de referência (WDG-REF-01) e o computador de destino (WDG-CLI-01) para E:\Source$\Drivers.  

> [!NOTE]   
>  Os processos neste guia partem do princípio de que o computador de referência e o computador de destino têm os mesmos dispositivos e não necessitam de controladores de dispositivos diferentes.  

###  <a name="ObtainRequiredSoftware"></a>Passo 1-3: Obter o Software necessário  
 Para além do Windows Server 2008 R2, Windows 8.1 e do Configuration Manager, determinado software é necessário para avaliar o MDT com base nos processos neste guia.  A tabela seguinte lista o software necessário para efetuar implementações com o MDT, onde obter o software e onde pretende colocar o software em WDG-MDT-01.  

 |**Obter este software**|**Coloque nesta pasta**|  
 |-|-|  
 |MDT 2013|E:\Source$\MDT_2013|  
 |Ficheiros de distribuição do Windows 8.1 do suporte de dados do produto|E:\Source$\Windows_8-1|  
 |Controladores de dispositivo necessários para os computadores de referência e de destino (WDG-REF-01 e WDG-CLI-01)|E:\Source$\Drivers|  
 |SQL Server 2008 R2 a partir do suporte do produto|E:\Source$\SQL2008R2|  
 |SQL Server 2008 R2 SP1, disponíveis em [http://www.microsoft.com/download/details.aspx?id=26727](http://www.microsoft.com/download/details.aspx?id=26727)|E:\Source$\SQL2008R2SP1|  
 |SQL Server 2008 R2 SP1 CU6, disponíveis em [http://support.microsoft.com/kb/2679367](http://support.microsoft.com/kb/2679367)|E:\Source$\SQL2008R2SP1CU6|  
 |Gestor de configuração a partir do suporte do produto|E:\Source$\ConfigMgr|  

###  <a name="InstallADDSRole"></a>Passo 1-4: Instalar a função de servidor DS AD  
 AD DS é necessário para fornecer autenticação e a atuar como um repositório para valores de configuração para os produtos da Microsoft e tecnologias que utiliza o MDT, tais como o SQL Server 2008 R2 e o Configuration Manager.  

 Para instalar o AD DS, execute o Assistente de DCPROMO para configurar o computador como um controlador de domínio. Instale o AD DS com as seguintes informações aceitar as predefinições, a menos que especificado em contrário.  

|**Quando lhe for pedido**|**Fazê-lo**|
|-|-|   
|Para o tipo de domínio|Crie um novo domínio numa floresta nova.|  
|O nome de domínio completamente qualificado|Tipo **mdt2013.corp.woodgrovebank.com**.|  
|Para o nível funcional de floresta|Selecione **Windows Server 2008 R2**.|  
|Para instalar o serviço servidor DNS como parte do processo de instalação do controlador de domínio|Clique em **Sim**.|  

###  <a name="InstallDHCPServerRole"></a>Passo 1-5: Instalar a função de servidor do servidor DHCP  
 A função de servidor do servidor DHCP é necessário para fornecer a configuração automática de IP para os computadores de destino. Instale o servidor DHCP, utilizando as seguintes informações aceitar as predefinições, a menos que especificado em contrário.  

> [!NOTE]   
>  Se estiver a utilizar um ambiente virtualizado, desative qualquer configuração de DHCP que fornece o software de Virtualização do computador. Certifique-se de que o serviço de servidor DHCP está em execução WDG-MDT-01 é o único fornecedor de configuração de IP utilizando o DHCP.  

|**Na página do Assistente**|**Fazê-lo**|  
|-|-|  
|**Autorizar o servidor DHCP no Active Directory**|Autorize WDG-MDT-01 para fornecer configuração de IP de cliente.|  
|**Âmbitos de DHCP**|Crie um âmbito adequado que pode ser utilizado para configurar automaticamente o TCP/IP para WDG-REF-01 e WDG-CLI-01.|  
|**Configuração de modo sem monitorização de estado de DHCPv6**|Desative o modo sem monitorização de estado de DHCPv6 para este servidor.|  

###  <a name="InstallIISRole"></a>Passo 1-6: Instalar a função de servidor do Web Services (IIS)  
 Instale a função de servidor serviços Web (IIS) com os serviços de função listados na seguinte tabela.  Estes serviços de função são necessários para o SQL Server 2008 R2 e o Configuration Manager. Salvo especificação em contrário, utilize os valores predefinidos.  

|Serviço de função|Estado|  
|-|-|  
|Servidor Web|instalado|  
|Funcionalidades HTTP Comuns|instalado|  
|Conteúdo Estático|instalado|  
|Documento Predefinido|instalado|  
|Navegação nos Diretórios|instalado|  
|Erros de HTTP|instalado|  
|Redirecionamento HTTP|instalado|  
|Publicação WebDAV|instalado|  
|Programação de Aplicações|instalado|  
|ASP.NET|instalado|  
|Extensibilidade .NET|instalado|  
|ASP|Não instalado|  
|CGI|Não instalado|  
|Extensões ISAPI|instalado|  
|Filtros ISAPI|instalado|  
|Lado do servidor inclui|Não instalado|  
|Estado de funcionamento e diagnósticos|instalado|  
|Registo HTTP|instalado|  
|Ferramentas de registo|instalado|  
|Monitor de Pedidos|instalado|  
|rastreio|instalado|  
|Registo personalizado|Não instalado|  
|Registo de ODBC|Não instalado|  
|Segurança|instalado|  
|Autenticação Básica|Não instalado|  
|Autenticação do Windows|instalado|  
|Autenticação resumida|Não instalado|  
|Autenticação de mapeamento de certificados de cliente|Não instalado|  
|Autenticação de mapeamento de certificados de cliente do IIS|Não instalado|  
|Autorização de URL|Não instalado|  
|Filtragem de Pedidos|instalado|  
|Restrições de domínio e de IP|Não instalado|  
|Desempenho|instalado|  
|Compressão de Conteúdo Estático|instalado|  
|Compressão de conteúdo dinâmico|Não instalado|  
|Ferramentas de Gestão|instalado|  
|Consola de gestão do IIS|instalado|  
|Ferramentas e Scripts de gestão do IIS|Não instalado|  
|Serviço de gestão|Não instalado|  
|Compatibilidade de Gestão do IIS 6|instalado|  
|Compatibilidade com Metabase do IIS 6|instalado|  
|Compatibilidade com WMI do IIS 6|instalado|  
|Ferramentas de 6 Scripting do IIS|Não instalado|  
|Consola de gestão 6 do IIS|Não instalado|  
|Serviço de publicação de FTP|Não instalado|  
|Servidor de FTP|Não instalado|  
|Consola de gestão de FTP|Não instalado|  
|Núcleo da Web Alojável do IIS|Não instalado|  

###  <a name="AddRequiredServerFeatures"></a>Passo 1-7: Adicionar as funcionalidades do necessários do Windows Server 2008 R2  
 Para além de instalar as funções de servidor necessárias do Windows Server 2008 R2, adicione as seguintes funcionalidades necessárias no Gestor de servidor no **funcionalidades resumo** secção:  

-   Serviço de transferência inteligente em segundo plano  

-   Compressão de diferencial remota  

###  <a name="CreateRequiredUserAccounts"></a>Passo 1-8: Criar o utilizador necessário e contas de serviço  
 Configuration Manager e o SQL Server 2008 R2 necessitam de contas de utilizador durante o processo de instalação.  Utilize as seguintes informações para criar estas contas.  


|**Criar esta conta**|**Com estas definições**|  
|-|-|  
|Conta de serviço do SQL Server Agent|1.  No **nome próprio**, tipo **SQL Agent**.<br />2.  No **Apelido**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLAgent**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o serviço do agente do SQL Server 2008 R2**.|  
|Conta de serviço do motor de base de dados do SQL Server|1.  No **nome próprio**, tipo **motor de base de dados do SQL Server**.<br />2.  No **Apelido**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLDBEngine**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o motor de base de dados do SQL Server 2008 R2**.|  
|Conta de serviço do SQL Server Reporting Services|1.  No **nome próprio**, tipo **SQL Reporting**.<br />2.  No **Apelido**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLReport**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o SQL Server 2008 R2 reporting services**.|  
|Conta de acesso de rede do cliente do System Center Configuration Manager do sistema|1.  No **nome próprio**, tipo **CM 2012**.<br />2.  No **Apelido**, tipo **acesso de rede do cliente**.<br />3.  No **nome de início de sessão do utilizador**, tipo **CMNetAccess**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  No **Descrição**, tipo **utilizada como a conta de acesso de rede para o cliente do Configuration Manager de conta de serviço**.|  

###  <a name="InstallSQLServer"></a>Passo 1 e 9: Instale o SQL Server 2008 R2  
 Antes de instalar o Configuration Manager, instale o SQL Server 2008 R2 com SP1 e CU6 para SP1.  

> [!NOTE]   
>  Para ativar todas as funcionalidades do SQL Server 2008 R2, instale a função de servidor serviços Web (IIS) antes de instalar o SQL Server 2008 R2.  

#### <a name="to-install-sql-server-2008-r2"></a>Para instalar o SQL Server 2008 R2
1.  Inicie o Centro de instalação do SQL Server.  

2.  No Centro de instalação do servidor de SQL Server, no painel de navegação, clique em **instalação**.  

3.  No painel de detalhes, clique em **nova instalação ou adicionar funcionalidades a uma instalação existente**.  

     Inicia o Assistente de configuração do SQL Server 2008 R2.  

4.  Instale o SQL Server 2008 R2 com as seguintes informações aceitar as predefinições, a menos que especificado em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Regras de suporte de configuração**|Clique em **OK**.|  
  |**Chave de produto**|Clique em **Seguinte**.|  
  |**Termos de licenciamento**|Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
  |**Ficheiros de suporte de configuração**|Clique em **Instalar**.|  
  |**Regras de suporte de configuração**|Certifique-se de que não existem resultados críticos existem para as regras e, em seguida, clique em **seguinte**.|  
  |**Função de configuração**|Clique em **instalação de funcionalidades do SQL Server**e clique em **seguinte**.|  
  |**Seleção de funcionalidades**|1.  Selecione **serviços de motor de base de dados** caixa de verificação.<br />2.  Selecione **Reporting Services** caixa de verificação.<br />3.  Selecione **pesquisa em texto completo** caixa de verificação.<br />4.  Selecione **ferramentas de gestão - concluir** caixa de verificação.<br />5.  Clique em **Seguinte**.|  
  |**Regras de instalação**|Clique em **Seguinte**.|  
  |**Configuração de instância**|Clique em **Seguinte**.|  
  |**Requisitos de espaço em disco**|Clique em **Seguinte**.|  
  |**Configuração do servidor**|1.  Para **do SQL Server Agent**, na **nome da conta**, tipo **MDT2013\SQLAgent**e, em **palavra-passe**, tipo  **P@ssw0rd**.<br />2.  Para **motor de base de dados do SQL Server**, na **nome da conta**, tipo **MDT2013\SQLDBEngine**, na **palavra-passe**, tipo  **P@ssw0rd** .<br />3.  Para **SQL Server Reporting Services**, na **nome da conta**, tipo **MDT2013\SQLReport**, na **palavra-passe**, tipo  **P@ssw0rd** .<br />4.  Clique em **Seguinte**.|  
  |**Configuração do motor de base de dados**|Clique em **adicionar utilizador atual**e clique em **seguinte**.|  
  |**Configuração do Reporting Services**|Clique em **Seguinte**.|  
  |**Relatório de erros**|Clique em **Seguinte**.|  
  |**Regras de configuração de instalação**|Clique em **Seguinte**.|  
  |**Pronto para instalar**|Clique em **Instalar**.|  
  |**Concluir**|Clique em **Fechar**.|  

5.  Feche o Centro de instalação do SQL Server.  

#### <a name="to-install-sql-server-2008-r2-sp1"></a>Para instalar o SQL Server 2008 R2 SP1
1.  No Explorador do Windows, aceda a E:\Source$\SQL2008R2SP1 e faça duplo clique **SQLServer2008R2SP1-KB2528583 x64 ENU.exe**.  

     O **extrair ficheiros** caixa de diálogo mostra o processo de extração de ficheiros. Quando o processo estiver concluído, o SQL Server 2008 R2 Service Pack 1 atualização Assistente de configuração é iniciado.  

2.  Instale o SQL Server 2008 R2 SP1 com as seguintes informações aceitar as predefinições, a menos que especificado em contrário.        

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Atualização do SQL Server 2008 R2**|Clique em **Seguinte**.|  
  |**Termos de licenciamento**|Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
  |**Selecionar funcionalidades**|Clique em **Seguinte**.|  
  |**Verifique os ficheiros em utilização**|Clique em **Seguinte**.|  
  |**Pronto para atualizar**|Clique em **atualização**.|  
  |**Progresso da atualização**|O progresso é apresentado na página do assistente, como a atualização é executada e concluído.|  
  |**Concluir**|Clique em **Fechar**.|  

#### <a name="to-install-sql-server-2008-r2-sp1-cu6"></a>Para instalar o SQL Server 2008 R2 SP1 CU6
1.  No Explorador do Windows, aceda a E:\Source$\SQL2008R2SP1CU6 e faça duplo clique **446622_intl_x64_zip.exe**.  

     O **Microsoft Self-Extractor** é apresentada a caixa de diálogo.  

2.  No **Microsoft Self-Extractor** caixa de diálogo, clique em **continuar**.  

3.  No **Microsoft Self-Extractor** caixa de diálogo **selecione a pasta onde pretende descomprimir os ficheiros para**, tipo **E:\Source$\SQL2008R2SP1CU6**e, em seguida, clique em  **OK**.  

    > [!NOTE]   
    >  Pode clicar em reticências (…), procure a pasta de E:\Source$\SQL2008R2SP1CU6.  

     O processo de extração é apresentado. Quando o processo estiver concluído, é apresentado o estado de conclusão.  

4.  No **Microsoft Self-Extractor** caixa de diálogo, clique em **OK**.  

5.  No Explorador do Windows, aceda a E:\Source$\SQL2008R2SP1CU6 e faça duplo clique **SQLServer2008R2-KB2679367-x64.exe**.  

     O **extrair ficheiros** caixa de diálogo mostra o processo de extração de ficheiros. Quando o processo estiver concluído, o SQL Server 2008 R2 Service Pack 1 CU6 atualização Assistente de configuração é iniciado.  

6.  Instale o SQL Server 2008 R2 SP1 CU6 com as seguintes informações aceitar as predefinições, a menos que especificado em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Atualização do SQL Server 2008 R2**|Clique em **Seguinte**.|  
  |**Termos de licenciamento**|Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
  |**Selecionar funcionalidades**|Clique em **Seguinte**.|  
  |**Verifique os ficheiros em utilização**|Clique em **Seguinte**.|  
  |**Pronto para atualizar**|Clique em **atualização**.|  
  |**Progresso da atualização**|O progresso é apresentado na página do assistente, como a atualização é executada.|  
  |**Concluir**|Clique em **Fechar**.|  

  O **instalar uma atualização do SQL Server 2008 R2** é apresentada a caixa de diálogo que lhe pede para reiniciar o computador para concluir a configuração.  

7.  No **instalar uma atualização do SQL Server 2008 R2** caixa de diálogo, clique em **OK**.  

8.  Reinicie o computador.  

9. Depois de instalar o SQL Server 2008 R2 SP1 CU6, o número de compilação do SQL Server deve ser 10.51.2811.0.  

    > [!TIP]    
    >  Pode verificar o número de compilação do SQL Server visualizando as atualizações do SQL Server aplicadas em programas e funcionalidades do painel de controlo item ao clicar em **ver atualizações instaladas**.  

###  <a name="AddSiteSecuritytoAdminGroup"></a>Passo 1-10: Adicione o servidor de Site para o grupo de segurança de administradores  
 Quando todos os computadores estão na mesma floresta, adicione manualmente a conta de computador do servidor de site para o grupo de administradores locais em cada computador. Conclua este passo antes de configurar o computador como um sistema de sites.  

 **Para adicionar o servidor de site para o grupo de segurança de administradores**  

1.  Clique em **iniciar**, aponte para **ferramentas administrativas**e, em seguida, clique em **computadores e utilizadores do Active Directory**.  

2.  Na árvore da consola computadores e utilizadores do Active Directory, aceda a mdt2013.corp.woodgrovebank.com/Builtin.  

3.  No painel de pré-visualização, faça duplo clique **administradores**e, em seguida, clique em **propriedades**.  

4.  No **administradores propriedades** caixa de diálogo, clique em de **membros** separador e, em seguida, clique em **adicionar**.  

5.  No **selecionar utilizadores, contactos, computadores ou grupos** caixa de diálogo, clique em **tipos de objeto**.  

6.  No **tipos de objeto** caixa de diálogo **tipos de objeto**, selecione **computadores**e, em seguida, clique em **OK**.  

7.  No **selecionar utilizadores, contactos, computadores ou grupos** caixa de diálogo **introduzir os nomes de objeto a selecionar**, tipo **WDG-MDT-01**. Clique em **verificar nomes**e, em seguida, clique em **OK**.  

8.  Feche as janelas abertas.  

###  <a name="InstallConfigManager"></a>Passo 1-11: Instalar o Configuration Manager  
 Quando os produtos e tecnologias tem sido instaladas, instale o Configuration Manager. Antes disso, no entanto, expanda o esquema do Active Directory para que computadores possam localizar os pontos de distribuição, pontos de localizador de serviço e outras funções de servidor. Além disso, pode expandir o esquema após a instalação do Configuration Manager. Para obter mais informações sobre como expandir o esquema do Active Directory para o Configuration Manager, consulte a secção "Expandir o esquema do Active Directory," na biblioteca de documentação do Configuration Manager, que é instalada com o Configuration Manager.  

 Após expandir o esquema do Active Directory, instale o Configuration Manager. A configuração do MDT-WDG-01 suporta do Configuration Manager para este exemplo. A configuração de computadores na rede de produção pode variar. Para obter mais informações sobre os pré-requisitos para instalar o Configuration Manager, consulte o artigo [configurações suportadas para o Configuration Manager](http://technet.microsoft.com/library/gg682077.aspx).  

#### <a name="to-install-configuration-manager"></a>Para instalar o Configuration Manager
1.  Inicie o ecrã inicial de configuração do System Center 2012 R2 Configuration Manager.  

2.  No ecrã inicial configuração do System Center 2012 R2 Configuration Manager, clique o **instalar** ligação.  

     A Microsoft assistente System Center 2012 R2 Configuration Manager a configuração é iniciado.  

3.  Conclua a Microsoft assistente System Center 2012 R2 Configuration Manager configuração com as seguintes informações aceitar as predefinições, a menos que especificado em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Antes de começar**|Clique em **Seguinte**.|  
  |**Introdução**|Clique em **Seguinte**.|  
  |**Chave de produto**|No **introduzir a chave de produto de 25 carateres**, tipo ***product_key*** (onde *product_key* é a chave de produto para o Configuration Manager).|  
  |**Termos de licenciamento de Software da Microsoft**|Selecione o **aceito estes termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
  |**Licenças de pré-requisitos**|1.  No **Microsoft SQL Server 2008 R2 Express** secção, selecione o **aceito estes termos de licenciamento** caixa de verificação.<br />2.  No **Microsoft SQL Server 2008 Native Client** secção, selecione o **aceito estes termos de licenciamento** caixa de verificação.<br />3.  No **Microsoft Silverlight 4** secção, selecione o **aceito estes termos de licenciamento e as atualizações automáticas do Silverlight** caixa de verificação.<br />4.  Clique em **Seguinte**.|  
  |**Atualizar os componentes de pré-requisito**|No **transferir e utilizar as atualizações mais recentes. As atualizações serão guardadas na seguinte localização**, tipo **E:\CMDownloads**e, em seguida, clique em **seguinte**.|  
  |**Seleção de idioma do servidor**|Clique em **Seguinte**.|  
  |**Seleção de idioma do cliente**|Clique em **Seguinte**.|  
  |**Definições de instalação e site**|1.  No **código do Site**, tipo **NYC**.<br />2.  No **nome do Site**, tipo **Nova Iorque cidade Site**.<br />3.  Clique em **Seguinte**.|  
  |**Instalação de Site principal**|1.  Clique em **instalar o site primário como um site autónomo**.<br />2.  Clique em **Seguinte**.<br />     O **do Configuration Manager** aparece a caixa de diálogo, confirmar que pretende que a instalação deste site como um site autónomo.<br />3.  No **do Configuration Manager** caixa de diálogo, clique em **Sim**.|  
  |**Informações de base de dados**|Clique em **Seguinte**.|  
  |**Definições do fornecedor SMS**|Clique em **Seguinte**.|  
  |**Definições de comunicação do computador cliente**|Clique em **configurar o método de comunicação em cada função do sistema de sites**e, em seguida, clique em **seguinte**.|  
  |**Funções do sistema de sites**|Clique em **Seguinte**.|  
  |**Configuração do programa de melhoramento de experiência de cliente**|1.  Selecione a participação no programa de melhoramento da experiência do cliente para a sua organização adequada.<br />2.  Clique em **Seguinte**.|  
  |**Resumo de definições**|Clique em **Seguinte**.|  
  |**Verificação de pré-requisitos**|Clique em **Iniciar instalação**.|  
  |**Instalar**|1.  Monitorize o processo de instalação até que esteja concluída.<br />2.  Clique em **Fechar**.|  

4.  Feche todas as janelas abertas e caixas de diálogo.  

 Quando o assistente estiver concluído, o Configuration Manager está instalado.  

###  <a name="ConfigureNetworkAccessAccount"></a>Passo 1-12: Configurar a conta de acesso de rede  
 O cliente do Configuration Manager necessita de uma conta para fornecer credenciais quando aceder a pontos de distribuição do Configuration Manager, partilhas de implementação do MDT e pastas partilhadas. Esta conta é denominada o *conta de acesso à rede*. A conta de CMNetAccess foi criada anteriormente no processo para utilizar como a conta de acesso à rede.  

#### <a name="to-configure-the-network-access-account"></a>Para configurar a conta de acesso à rede  
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, vá para o Site/descrição geral da configuração/Sites.  

4.  No painel de pré-visualização, clique em **NYC - Nova Iorque cidade Site**.  

5.  No Friso, clique em **definições**, clique em **configurar componentes do Site**e, em seguida, clique em **distribuição de Software**.  

6.  No **propriedades do componente de distribuição de Software** caixa de diálogo, clique em de **conta de acesso à rede** separador.  

7.  No **conta de acesso à rede**, clique em **especifique a conta que aceder a localizações de rede**, clique em **definir**e, em seguida, clique em **nova conta**.  

     O **conta de utilizador do Windows** é apresentada a caixa de diálogo.  

8.  Concluir o **conta de utilizador do Windows** caixa de diálogo com as seguintes informações e, em seguida, clique em **OK**.    

 |**Para este**|**Fazê-lo**|  
 |-|-|  
 |**Nome de utilizador**|Tipo **MDT2013\CMNetAccess**.|  
 |**Palavra-passe**|Tipo  **P@ssw0rd** .|  
 |**Confirmar palavra-passe**|Tipo  **P@ssw0rd** .|  

9. No **propriedades do componente de distribuição de Software** caixa de diálogo, clique em **OK**.  

10. Feche as janelas abertas.  

###  <a name="ConfigurationManagerSiteBoundaries"></a>Passo 1-13: Configurar os limites de Site do Configuration Manager e os grupos de limites  
 O cliente do Configuration Manager tem de conhecer os limites para o site. A menos que sejam especificados limites do site, o cliente assume que o computador com o Configuration Manager num site remoto. Adicione que um limite de site com base na sub-rede IP que WDG-MDT-01, WDG-REF-01 e utilize WDG-CLI-01. Em seguida, adicione o limite de site para um grupo de limites de site.  

#### <a name="to-create-a-configuration-manager-site-boundary"></a>Para criar um limite de site do Configuration Manager
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, aceda a hierarquia de descrição geral/configuração/limites.  

4.  No Friso, clique em **criar limites**.  

     O **criar limites** é aberta a caixa de diálogo.  

5.  Concluir o **criar limites** caixa de diálogo com as seguintes informações e, em seguida, clique em **OK**.  

    > [!NOTE]   
    >  Para este exemplo, o limite de site é especificado por endereço de rede. No entanto, também pode especificar limites de site utilizando do AD DS sites nome ou um intervalo de endereços IP.  

   |**Para este**|**Fazê-lo**|  
   |-|-|  
   |**Descrição**|Tipo **limite de sub-rede IP**.|  
   |**Tipo**|Selecione **sub-rede IP**.|  
   |**Rede**|Tipo ***network_address*** (onde *network_address* é o endereço de rede da sub-rede de onde os computadores estão instalados).|  
   |**Máscara de sub-rede**|Tipo ***subnet_mask*** (onde *subnet_mask* é a máscara de sub-rede da sub-rede de onde os computadores estão instalados).|  

#### <a name="to-add-the-configuration-manager-site-boundary-to-a-site-boundary-group"></a>Para adicionar o limite de site do Configuration Manager a um grupo de limites de site  
1.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

2.  Na área de trabalho administração, aceda a grupos de configuração/limites de descrição geral/hierarquia.  

3.  No Friso, clique em **criar grupo de limites**.  

     O **criar grupo de limites** é aberta a caixa de diálogo.  

4.  Concluir o **geral** separador do **criar grupo de limites** caixa de diálogo com as informações seguintes.

  |**Para este**|**Fazê-lo**|  
  |-|-|  
  |**Nome**|Tipo **grupo de limites de Nova Iorque Cidade**.|  
  |**Descrição**|Tipo **este é o grupo de limites para os limites de site no site de Nova Iorque Cidade**.|  
  |Limites|1.  Clique em **Adicionar**.<br />     O **adicionar limites** é apresentada a caixa de diálogo.<br />2.  No **adicionar limites** caixa de diálogo, selecione ***site_boundary*** (onde *site_boundary* é o limite de site que criou anteriormente no processo) e, em seguida, clique em **OK**.<br />     O limite de site é apresentado na lista de limites.|  

5.  Concluir o **referências** separador do **criar grupo de limites** caixa de diálogo com as seguintes informações e, em seguida, clique em **OK**.  

  |**Para este**|**Fazê-lo**|  
  |-|-|  
  |**Atribuição de site**|Selecione o **utilizar este grupo de limites para atribuição de site** caixa de verificação.|  
  |**Localização de conteúdo**|1.  Clique em **Adicionar**.<br />     O **adicionar sistemas de sites** é apresentada a caixa de diálogo.<br />2.  No **adicionar sistemas de sites** caixa de diálogo, selecione  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     O servidor de sistema de sites é apresentado na lista de servidores do sistema de sites.|  

6.  Feche as janelas abertas.  

###  <a name="ConfigurePublishingSiteInfo"></a>Passo 1-14: Configurar a publicação de informações do Site no AD DS e DNS  
 O cliente do Configuration Manager tem de localizar as várias funções de servidor do Configuration Manager. Modificar as propriedades do site para publicar as informações do site no AD DS e no DNS.  

 **Para configurar a publicação de informações do site no AD DS e no DNS**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, vá para o Site/descrição geral da configuração/Sites.  

4.  No painel de pré-visualização, clique em **NYC - Nova Iorque cidade Site**.  

5.  No Friso, clique em **propriedades**.  

6.  No **propriedades do Site de Nova Iorque Cidade** caixa de diálogo a **publicação** separador, certifique-se de que o **mdt2013.corp.woodgrovebank.com** floresta do Active Directory estiver listada, e em seguida, clique em **Cancelar**.  

7.  Feche as janelas abertas.  

##  <a name="PrepareMDTEnvironment"></a>Passo 2: Preparar o ambiente do MDT  
 É o primeiro passo no processo de implementação para preparar o ambiente do MDT. Quando estiver concluído este passo, pode criar o computador de referência e implementar uma imagem capturada do mesmo no computador de destino (WDG-CLI-01) através da integração do Configuration Manager com o MDT.  

 Prepare o ambiente do MDT por:  

-   Instalar o MDT conforme descrito em [passo 1 de 2: Instale o MDT](#InstallMDT)  

-   Ativar a integração da consola do Configuration Manager ao executar o script de configurar a integração do ConfigMgr, conforme descrito em [passo 2 de 2: Ativar a integração da consola do Configuration Manager](#EnableConfigManagerConsole)  

###  <a name="InstallMDT"></a>Passo 1 de 2: Instale o MDT  
 Para instalar o MDT, conclua os seguintes passos:  

1.  No Explorador do Windows, aceda a E:\Source$\MDT_2013.  

2.  Faça duplo clique em **MicrosoftDeploymentToolkit2013_x64.msi** (para sistemas operativos de 64 bits) ou **MicrosoftDeploymentToolkit2013_x86.msi** (para sistemas de operativos de 32 bits) e, em seguida, clique em **Instalar**.  

     Inicia o Assistente de configuração do Microsoft implementação Toolkit 2013.  

3.  Conclua a implementação Toolkit 2013 Assistente de configuração Microsoft utilizando as informações na tabela seguinte.  Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Bem-vindo ao Microsoft Deployment Toolkit Assistente de configuração de 2013**|Clique em **Seguinte**.|  
  |**Contrato de licença de utilizador final**|Clique em **aceito os termos no contrato de licença**e, em seguida, clique em **seguinte**.|  
  |**Configuração personalizada**|Clique em **Seguinte**.|  
  |**Pronto para instalar o Microsoft implementação Toolkit de 2013**|Clique em **Instalar**.|  
  |**Instalar o Microsoft Deployment Toolkit 2013**|É apresentado o progresso da instalação do MDT.|  
  |**A concluir o Assistente de configuração do Microsoft Deployment Toolkit 2013**|Clique em **Concluir**.|  

 Concluído o Assistente de configuração do Microsoft implementação Toolkit 2013 e instalação do MDT no WDG-MDT-01.  

###  <a name="EnableConfigManagerConsole"></a>Passo 2 de 2: Ativar a integração da consola do Configuration Manager  
 Antes de poder utilizar as funcionalidades de integração do Gestor de configuração do MDT, execute o script de configurar a integração do ConfigMgr. Este script copia os ficheiros de integração adequado para a pasta na qual o Configuration Manager está instalado. O script também adiciona classes Windows Management Instrumentation (WMI) para as novas ações personalizadas do MDT. As classes são adicionadas ao compilar um novo ficheiro de formato de objeto gerido (. mof), que contém as novas definições de classe.  

 **Para ativar a integração da consola do Configuration Manager**  

> [!NOTE]   
>  Certifique-se de que a consola do Configuration Manager está fechada ao efetuar estes passos.  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **configurar a integração do ConfigMgr**.  

     Inicia o Assistente para configurar a integração do ConfigMgr.  

2.  Conclua o Assistente de integração de ConfigMgr configurar utilizando as informações na tabela seguinte. Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Opções**|1.  Certifique-se de que o **instalar as extensões de consola do MDT para o System Center 2012 R2 Configuration Manager** caixa de verificação está selecionada.<br />2.  Certifique-se de que o **adicionar as ações de sequência de tarefas do MDT a um servidor do System Center 2012 R2 Configuration Manager** caixa de verificação está selecionada.<br />3.  No **nome do servidor de Site**, certifique-se de que o valor é **WDG-MDT-01.mdt2013.corp.woodgrovebank.com**.<br />4.  No **código do Site**, certifique-se de que o valor é **NYC**.<br />5.  Clique em **Seguinte**.|  
  |**Confirmação**|Clique em **Concluir**.|  

 Concluído o Assistente para configurar a integração do ConfigMgr e o MDT é integrado com o Configuration Manager.  

## <a name="step-3-create-and-configure-a-task-sequence-to-create-a-reference-computer"></a>Passo 3: Criar e configurar uma sequência de tarefas para criar um computador de referência  
 Quando preparar o ambiente do MDT, crie o computador de referência. O computador de referência é o modelo para implementar novas imagens em computadores de destino. Configure este computador (WDG-REF-01) exatamente como irá configurar os computadores de destino. Em seguida, irá capturar uma imagem do computador de referência e implementar a imagem nos computadores de destino.  

 Criar o computador de referência, WDG-REF-01, por:  

-   Criar uma sequência de tarefas para implementar o Windows 8.1 para o computador de referência, tal como descrito no MDT [passo 1 de 3: Criar uma sequência de tarefas do MDT para implementar o computador de referência](#CreateMDTTaskSequence)  

-   Selecionar os pontos de distribuição para os novos pacotes e imagens que o assistente criar MDT tarefas sequência cria conforme descrito em [passo 2 de 3: Selecione os pontos de distribuição para os novos pacotes e a imagens](#SelectDistroPoints)  

-   Adicionar os controladores de dispositivo necessários para um novo pacote de unidade e para as imagens de arranque apropriado, conforme descrito em [passo 3 de 3: Adicionar os controladores de dispositivo necessários](#AddDeviceDrivers)  

-   Ativar a monitorização do processo de implementação MDT, conforme descrito em [passo 3-4: Ativar a implementação do MDT monitorização de processos](#EnableMDTDeployProcess)  

-   Configurar os ficheiros de configuração do MDT para o computador de referência — especificamente, o ficheiro CustomSettings.ini, conforme descrito em [passo 3-5: Personalizar os ficheiros de configuração do MDT para o computador de referência](#CustomizeMDTConfigFiles)  

-   Atualizar os pontos de distribuição do Configuration Manager para o pacote de ficheiros de definições personalizadas, conforme descrito em [passo 3 a 6: Atualizar os pontos de distribuição para o pacote de ficheiros de definições personalizadas](#UpdateDistroPoint)  

-   Personalizar a sequência de tarefas para o computador de referência, conforme descrito em [passo 3-7: Personalizar a sequência de tarefas para o computador de referência](#CustomizeTaskSequence)  

###  <a name="CreateMDTTaskSequence"></a>Passo 1 de 3: Criar uma sequência de tarefas do MDT para implementar o computador de referência  
 Utilize o Assistente de criação MDT tarefas sequência na consola do Configuration Manager para criar sequências de tarefas no Configuration Manager que estão integradas com o MDT. MDT inclui o modelo de sequência de tarefas de cliente padrão, que pode utilizar para implementar o computador de referência.  

 Assistente de criação MDT tarefas sequência substitui os pacotes e imagens selecionadas para os marcadores de posição nos modelos de sequência de tarefas. Depois de concluir o assistente, a nova sequência de tarefas referencia o pacotes adequados e imagens.  

> [!NOTE]   
>  Utilize sempre o Assistente de criação MDT tarefas sequência para criar sequências de tarefas com base nos modelos de sequência de tarefas de MDT. Embora pode importar manualmente os modelos de sequência de tarefas, a Microsoft não recomenda este processo.  

#### <a name="to-create-a-task-sequence-for-deploying-the-reference-computer"></a>Para criar uma sequência de tarefas para implementar o computador de referência  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **sequências de tarefas** , clique em **criar sequência de tarefas do MDT**.  

     Inicia o Assistente de criação MDT tarefas sequência.  

5.  Conclua o Assistente de criação MDT tarefas sequência utilizando as informações na tabela seguinte. Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Escolha o modelo**|Selecione **sequência de tarefas de cliente**e, em seguida, clique em **seguinte**.|  
  |**Escolha o modelo: Geral**|1.  No **nome da sequência de tarefas**, tipo **implementação de referência do Windows 8.1**.<br />2.  No **comentários de sequência de tarefas**, tipo **sequência para implementar o Windows 8.1 para o computador de referência (WDG-REF-01) de tarefas**e, em seguida, clique em **seguinte**.|  
  |**Escolha o modelo: Detalhes**|1.  Clique em **aderir a um grupo de trabalho**.<br />2.  No **Workgroup**, tipo **WORKGROUP**.<br />3.  No **nome de utilizador**, tipo **Woodgrove Bank empregado**.<br />4.  No **nome da organização**, tipo **Banco Woodgrove**.<br />5.  No **chave de produto**, tipo ***product_key*** (onde *product_key* é a chave de produto para Windows 8.1).<br />6.  Clique em **Seguinte**.|  
  |**Escolha o modelo: Capturar definições**|<ol><li>Clique em **esta sequência de tarefas pode ser utilizada para capturar e imagem**.</li><li>No **captura destino**, tipo  **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**.</li><li>No **conta para captura**, clique em **definir**.</li><li>Concluir o **conta de utilizador do Windows** caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome de utilizador**, tipo **MDT2013\Administrator**.</li><li>No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .</li></ol></li><li>Clique em **OK**.</li><li>Clique em **Seguinte**.</li></ol>|  
  |**Imagem de arranque**|1.  Clique em **criar um novo pacote de imagem de arranque**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\WINPE_Custom**e, em seguida, clique em **seguinte**.|  
  |**Imagem de arranque: Definições gerais**|1.  No **nome**, tipo **personalizada do Windows PE**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **personalizado versão do Windows PE para serem utilizados na implementação de computadores de referência e de destino**e, em seguida, clique em **seguinte**.|  
  |**Imagem de arranque: Opções**|Em **plataforma**, clique em **x64**e, em seguida, clique em **seguinte**.|  
  |**Imagem de arranque: Componentes**|Clique em **Seguinte**.|  
  |**Imagem de arranque: Personalização**|Clique em **Seguinte**.|  
  |**Pacote de MDT**|1.  Clique em **criar um novo pacote de ficheiros de Toolkit do Microsoft implementação**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\MDT_Files**e, em seguida, clique em **seguinte**.|  
  |**MDT pacote: Detalhes do MDT**|1.  No **nome**, tipo **ficheiros MDT**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **fornece acesso aos ficheiros do MDT durante o processo de implementação do Configuration Manager**e, em seguida, clique em **seguinte**.|  
  |**Imagem do SO**|1.  Clique em **pacote de instalação de criar um novo SO**.<br />2.  No **localização de pasta de instalação do SO**, tipo  **\\\WDG-MDT-01\Source$\Windows_7**.<br />3.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\Windows_7**e, em seguida, clique em **seguinte**.|  
  |**Imagem do SO: Detalhes da imagem**|1.  No **nome**, tipo **Windows 8.1**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **utilizada para implementar em computadores de referência de pacote de Windows 8.1**e, em seguida, clique em **seguinte**.|  
  |**Método de implementação**|Clique em **Seguinte**.|  
  |**Pacote de cliente**|Clique em **criar um novo pacote de cliente do ConfigMgr**e, em seguida, clique em **seguinte**.|  
  |**Pacote USMT**|1.  Clique em **criar um novo pacote USMT**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\USMT**e, em seguida, clique em **seguinte**.|  
  |**Pacote do USMT: Detalhes do USMT**|1.  No **nome**, tipo **USMT**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **ficheiros da USMT utilizados para capturar e restaurar informações de migração de estado de utilizador**e, em seguida, clique em **seguinte**.|  
  |**Pacote de definições**|1.  Clique em **criar um novo pacote de definições**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\CustomSettings_Reference**e, em seguida, clique em **seguinte**.|  
  |**Pacote de definições: Detalhes de definições**|1.  No **nome**, tipo **definições personalizadas do MDT referência computador**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **definições de configuração para o processo de implementação do MDT (por exemplo, CustomSettings.ini) para o computador de referência**e, em seguida, clique em **seguinte**.|  
  |**Pacote Sysprep**|Clique em **Seguinte**.|  
  |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
  |**Progresso**|É apresentado o progresso da criação de sequência de tarefas.|  
  |**Confirmação**|Clique em **Concluir**.|  

   A nova sequência de tarefas é apresentado no painel de pré-visualização.  

###  <a name="SelectDistroPoints"></a>Passo 3-2: Selecione os pontos de distribuição para os novos pacotes e a imagens  
 Assistente de criação MDT tarefas sequência cria um número de pacotes e imagens. Depois destes pacotes e imagens são criadas, selecione os pontos de distribuição a partir da qual as imagens e o pacote será copiado e disponíveis para computadores de destino.  

> [!NOTE]   
>  Neste exemplo, não há apenas um ponto de distribuição (WDG-MDT-01). No entanto, a maioria das redes de produção tem vários pontos de distribuição. Quando executar este passo num ambiente de produção, selecione os pontos de distribuição apropriados para a rede.  

#### <a name="to-select-the-distribution-points-for-software-distribution-packages"></a>Para selecionar os pontos de distribuição para pacotes de distribuição de software  
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de visualização, selecione **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo utilizando as informações na tabela seguinte. Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Geral**|Clique em **Seguinte**.|  
  |**Gerais: Conteúdo**|Clique em **Seguinte**.|  
  |**Gerais: Destino do conteúdo**|1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione **WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     WDG-MDT-01.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
  |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
  |**Progresso**|O progresso da distribuição de software é apresentado.|  
  |**Conclusão**|Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="AddDeviceDrivers"></a>Passo 3 de 3: Adicionar os controladores de dispositivo necessários  
 Quando tiver sido criada a sequência de tarefas do MDT, adicione os controladores de dispositivo necessários para o computador de referência (WDG-REF-01) para a imagem de arranque do Windows PE e a imagem do Windows 8.1. Adicione os controladores de dispositivo no nó de controladores na consola do Configuration Manager. Criar um pacote que contém os controladores de dispositivo e inserir os controladores numa imagem do Windows PE personalizada criada anteriormente no processo.  

 Depois de criar o pacote que contém os controladores de dispositivo, selecione a distribuição de ponto no qual o pacote será implementado.  

#### <a name="to-add-the-necessary-device-drivers"></a>Para adicionar os controladores de dispositivo necessários
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda à descrição geral/operativo sistemas/controladores.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar controlador**.  

     O novo Assistente para importar controlador é iniciado.  

5.  Conclua o novo Assistente para importar controlador utilizando as informações na tabela seguinte.  Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Localizar controlador**|No **pasta de origem**, tipo  **\\\WDG-MDT-01\Source$\Drivers**e, em seguida, clique em **seguinte**.|  
  |**Localize os controladores: Detalhes do controlador**|Clique em **Seguinte**.|  
  |**Localize os controladores: Adicionar controladores ao pacote**|<ol><li>Clique em **novo pacote**.</li><li>Concluir o **novo pacote de controladores** caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome**, tipo ***device_driver_name*** pacote (onde *device_driver_name* é um nome descritivo para os controladores de dispositivo).</li><li>No **comentário**, tipo **controladores de dispositivo que são necessários para os computadores de referência e de destino**.</li></ol></li><li>No **origem do pacote de controlador**, tipo  **\\\WDG-MDT-01\Packages$\Drivers**e, em seguida, clique em **OK**.</li><li>Clique em **Seguinte**.</li></ol>|  
  |**Localize os controladores: Adicionar controlador a imagens de arranque**|1.  Na lista de imagens, selecione o **personalizada do Windows PE** caixa de verificação.<br />2.  Selecione o **atualizar pontos de distribuição após concluir** caixa de verificação e, em seguida, clique em **seguinte**.|  
  |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
  |**Progresso**|O progresso para importar os controladores de dispositivo é apresentado.|  
  |**Confirmação**|Clique em **Fechar**.|  

#### <a name="to-select-the-distribution-points-for-the-driver-package"></a>Para selecionar os pontos de distribuição para o pacote de controladores
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda a descrição geral/operativo sistemas/a pacotes de controladores.  

4.  No painel de pré-visualização, clique em ***device_driver_name*** **pacote** (onde *device_driver_name* é um nome descritivo para os controladores de dispositivo).  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Geral**|Clique em **Seguinte**.|  
  |**Gerais: Conteúdo**|Clique em **Seguinte**.|  
  |**Gerais: Destino do conteúdo**|1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
  |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
  |**Progresso**|O progresso da distribuição de software é apresentado.|  
  |**Conclusão**|Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="EnableMDTDeployProcess"></a>Passo 3-4: Ativar a implementação do MDT monitorização de processos  
 Antes de implementar o computador de referência (WDG-REF-01) com os dados de arranque de sequências de tarefas, ative a monitorização de MDT do processo de implementação de ZTI. Ativar a monitorização de **monitorização** separador na partilha de implementação **propriedades** caixa de diálogo. Posteriormente no processo, irá monitorizar o processo de implementação de ZTI utilizando Deployment Workbench ou **Get-MDTMonitorData** cmdlet.  

 **Para ativar a monitorização do processo de implementação de ZTI do MDT**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação de Workbench/implementação.  

3.  No painel ações, clique em **novas partilhas de implementação**.  

     Inicia o Assistente de nova partilha de implementação.  

4.  Conclua o Assistente de partilha de implementação novo com as seguintes informações

   |**Na página do Assistente**|**Fazê-lo**|  
   |-|-|  
   |**Na página do Assistente**|**Fazê-lo**|  
   |**Caminho**|No **caminho de partilha de implementação**, tipo **C:\DeploymentShare$**e, em seguida, clique em **seguinte**.|  
   |**Partilha**|Clique em **Seguinte**.|  
   |**Nome descritivo**|Clique em **Seguinte**.|  
   |**Opções**|Clique em **Seguinte**.|  
   |**Resumo**|Clique em **Seguinte**.|  
   |**Progresso**|O progresso para criar a partilha de implementação é apresentado.|  
   |**Confirmação**|Clique em **Concluir**.|  

  Depois de concluída as implementação Assistente de nova partilha e a nova partilha de implementação — partilha de implementação MDT (C:\DeploymentShare$)—appears no painel de detalhes.  


5.  No painel de detalhes, clique em **partilha de implementação do MDT (C:\DeploymentShare$)**.  

6.  No painel ações, clique em **propriedades**.  

     O **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** é aberta a caixa de diálogo.  

7.  No **propriedades de partilha de implementação MDT (C:\DeploymentShare$)** caixa de diálogo a **monitorização** separador, selecione o **ativar a monitorização para esta partilha de implementação** caixa de verificação e, em seguida, clique em **aplicar**.  

8.  No **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** caixa de diálogo a **regras** separador, tenha em atenção que o **EventService** propriedade foi adicionada para o Ficheiro CustomSettings.ini e, em seguida, clique em **OK**.  

  O **EventService** propriedade é o seguinte:  

    ```  
    EventService=http://WDG-MDT-01:9800  
    ```  

9. Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizeMDTConfigFiles"></a>Passo 3-5: Personalizar os ficheiros de configuração do MDT para o computador de referência  
 Quando tiver sido criada a sequência de tarefas do MDT, personalize os ficheiros de configuração do MDT que fornecem as definições de configuração para a implementação do Windows 8.1 para o computador de destino. Especificamente, personalize o ficheiro CustomSettings.ini.  

 Quando a personalização do ficheiro CustomSettings.ini estiver concluída, guarde ficheiros atualizados para a pasta de origem para o pacote de definições personalizadas do MDT referência computador criado anteriormente no processo (E:\Packages$\CustomSettings_Reference). Em seguida, adicione o **DoCapture** e **EventService** propriedades e valores correspondentes para o CustomSettings.ini do ficheiro para que o processo de implementação do MDT captura uma imagem das (do computador de referência WDG-REF-01) após a implementação do Windows 8.1.  

#### <a name="to-customize-the-mdt-configuration-files-for-the-reference-computer"></a>Para personalizar os ficheiros de configuração do MDT para o computador de referência

1.  No Explorador do Windows, aceda ao E:\Packages$\CustomSettings_Reference e, em seguida, faça duplo clique em **CustomSettings.ini**.  

2.  Abra o Microsoft Notepad e, em seguida, adicione as seguintes linhas ao fim do ficheiro CustomSettings.ini:

    ```  
    DoCapture=YES  
    EventService=http://WDG-MDT-01:9800  
    ```  

    Exemplo do ficheiro CustomSettings.ini depois de adicionar a propriedade DoCapture:

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  
    SkipCapture=YES  
    SkipAdminPassword=NO  
    SkipProductKey=YES  
    DoCapture=YES  
    EventService=http://WDG-MDT-01:9800  
    ```  

3.  No bloco de notas, guarde o ficheiro e, em seguida, saia bloco de notas.  

###  <a name="UpdateDistroPoint"></a>Passo 3 a 6: Atualizar os pontos de distribuição para o pacote de ficheiros de definições personalizadas  
 Quando a pasta de origem tiver sido atualizada para o pacote de definições de personalizado do computador de referência do MDT no Configuration Manager, atualize os pontos de distribuição para o pacote de ficheiros de definições de personalizada de computador de referência de MDT. Atualizar os pontos de distribuição copia a versão atualizada do ficheiro CustomSettings.ini para as partilhas de implementação especificadas no pacote.  

 **Para atualizar a distribuição aponta para o pacote de definições personalizadas**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para gestão/pacotes de aplicações/descrição geral.  

4.  No painel de pré-visualização, clique em **definições personalizadas do MDT referência computador**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **atualizar pontos de distribuição**.  

     O **do Configuration Manager** abre a caixa de diálogo, notificam que pretender atualizar o pacote em todos os pontos de distribuição.  

6.  No **do Configuration Manager** caixa de diálogo, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

 O Configuration Manager começa a atualizar os pontos de distribuição com as versões mais recentes do ficheiro CustomSettings.ini. Este processo pode demorar vários minutos. Verificar o estado do pacote, até que o **última atualização** valor do Estado de pacote foi atualizado para uma recente data e hora.  

###  <a name="CustomizeTaskSequence"></a>Passo 3-7: Personalizar a sequência de tarefas para o computador de referência  
 Para a maioria das implementações, o **implementação de referência do Windows 8.1** criada anteriormente no processo de sequência de tarefas executa todos os passos necessários sem modificação. Neste exemplo, modificar a sequência de tarefas para definir a palavra-passe para a conta de administrador local para um valor conhecido. Por predefinição, a sequência de tarefas define a palavra-passe para a conta de administrador local para um valor aleatório. Personalização adicional da sequência de tarefas poderá ser necessária dependendo do ambiente.  

 **Para personalizar a sequência de tarefas de implementação de referência do Windows 8.1**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **sequência de tarefas** , clique em **editar**.  

     O **Editor de sequência de tarefas de implementação do Windows 8.1 referência** é aberta a caixa de diálogo.  

6.  No **Editor de sequência de tarefas de implementação do Windows 8.1 referência** caixa de diálogo, aceda a PostInstall/aplicar as definições do Windows.  

7.  No **propriedades** separador, clique em **ativar a conta e especificar a palavra-passe de administrador local**.  

8.  No **propriedades** separador **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** e, em seguida, clique em **aplicar** .  

9. Efetue quaisquer modificações adicionais para a sequência de tarefas que requer que o ambiente e, em seguida, clique em **OK**.  

10. Feche todas as janelas abertas e caixas de diálogo.  

## <a name="step-4-deploy-windows-81-and-capture-an-image-of-the-reference-computer"></a>Passo 4: Implementar o Windows 8.1 e capturar uma imagem do computador de referência  
 Quando tiver criado a sequência de tarefas para implementar o Windows 8.1 para o computador de referência e capturar uma imagem do computador de referência, inicie a sequência de tarefas. Crie a captura de sistema operativo utilizando o Assistente de suporte de dados de sequência de tarefas na consola do Configuration Manager.  

 Implementar o Windows 8.1 e capturar uma imagem do computador de referência por:  

-   Adicionar o computador de referência para a base de dados do site do Configuration Manager, conforme descrito em [passo 4-1: Adicionar o computador de referência para a base de dados do Site do Configuration Manager](#AddRefComptoConfigDB)  

-   Criar uma coleção que contenha o computador de referência que acabou de adicionar conforme descrito em [passo 4-2: Criar uma coleção que contenha o computador de referência](#CreateCollectionContainRefComp)  

-   Implemente a sequência de tarefas do computador de referência, conforme descrito em [passo 4-3: Implementar a sequência de tarefas do computador de referência](#DeployRefCompTaskSeq)  

-   Utilizar o Assistente de suporte de dados de sequência de tarefas para criar uma sequência de tarefas com suportes de dados em disco conforme descrito em [passo 4-4: Criar tarefas sequência suportes de dados](#CreateTaskSeqBootMedia)  

-   A iniciar o computador de referência com a sequência de tarefas com suportes de dados em disco conforme descrito em [passo 4-5: Iniciar o computador de referência com o suporte de suportes de sequência de tarefas](#StartRefCompwithTaskSeqBootMedia)  

###  <a name="AddRefComptoConfigDB"></a>Passo 4-1: Adicionar o computador de referência para a base de dados do Site do Configuration Manager  
 Para implementar um sistema operativo sem suporte de dados autónomo para um novo computador que o Configuration Manager não gerir atualmente, adicione o novo computador para a base de dados do site do Configuration Manager antes de iniciar o processo de implementação do sistema operativo. O Configuration Manager pode detetar automaticamente computadores na rede que tenha um sistema de operativo de Windows instalado. No entanto, se o computador não tiver nenhum sistema operativo instalado, utilize o Assistente para importar informações de computador para importar as informações do computador novo.  

#### <a name="to-add-the-reference-computer-to-the-configuration-manager-site-database"></a>Para adicionar o computador de referência para a base de dados do site do Configuration Manager  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda à descrição geral/dispositivos.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar informações sobre o computador**.  

     O Assistente Importar informações o computador é iniciado.  

5.  Conclua o Assistente de importação de informações de computador, utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

  |**Na página do Assistente**|**Fazê-lo**|  
  |-|-|  
  |**Selecione a origem**|Clique em **importar computador individual**e, em seguida, clique em **seguinte**.|  
  |**Selecione a origem: Único computador**|1.  No **nome do computador**, tipo **WDG-REF-01**.<br />2.  No **endereço MAC**, tipo ***mac_address*** (onde *mac_address* é o controlo [MAC] endereço do adaptador de rede principal para o computador de referência, o media access WDG-REF-01).<br />3.  Clique em **Seguinte**.|  
  |**Selecione a origem: Pré-visualização de dados**|Clique em **Seguinte**.|  
  |**Selecione a origem: Escolher coleção de destino**|Clique em **Seguinte**.|  
  |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
  |**Progresso**|O progresso para importar o computador é apresentado.|  
  |**Confirmação**|Clique em **Fechar**.|  

 Para obter mais informações sobre como adicionar um novo computador para a base de dados do site do Configuration Manager, consulte a secção "para importar informações sobre o computador para um único computador," na secção "Como para implementar sistemas operativos no Configuration Manager," na configuração Biblioteca de documentação Manager, que é instalado com o Configuration Manager.  

###  <a name="CreateCollectionContainRefComp"></a>Passo 4-2: Criar uma coleção que contenha o computador de referência  
 Na consola do Configuration Manager, crie uma coleção que inclua o computador de referência (WDG-REF-01). Esta coleção de computadores é utilizada mais tarde, quando a sequência de tarefas de publicidade criado anteriormente no processo.  

 **Para criar uma coleção que inclui o computador de referência**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda a coleções de dispositivos/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar**e, em seguida, clique em criar dispositivo **coleção**.  

     Inicia o Assistente para criar coleção de dispositivos.  

5.  Conclua o Assistente de coleção de dispositivos criar com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Geral**|<ol><li>No **nome**, tipo **Microsoft Deployment – o computador de referência**.</li><li>No **comentário**, tipo **computador que está a ser o computador de referência para os computadores de destino a ser implementado**.</li><li>No **coleção limitado**, clique em **procurar**.<br /><br />     O **selecionar coleção** é apresentada a caixa de diálogo. Conclua a caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome**, clique em **todos os sistemas**.</li><li>Clique em **OK**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Regras de Associação**|<ol><li>Clique em **Adicionar regra**e, em seguida, clique em **regra direta**.<br /><br />     O direto associação Assistente para criar regra é iniciado.</li><li>Conclua o direta associação Assistente para criar regra, efetuando os seguintes passos:<br /><br /> <ol><li>Na página de **Boas-vindas**, clique em **Seguinte**.</li><li>No **procurar recursos** na página **classe de recursos**, selecione **recurso do sistema**; na **nome de atributo**, selecione  **Nome**; na **valor**, tipo **WDG-REF-01**; e, em seguida, clique em **seguinte**.</li><li>No **selecionar recursos** página, selecione **WDG-REF-01**e, em seguida, clique em **seguinte**.</li><li>No **resumo** página, clique em **seguinte**.</li><li>No **progresso** página, ver o progresso para criar a nova regra de associação.</li><li>No **conclusão** página, clique em **fechar**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para criar a coleção de dispositivos é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para criar coleções no Configuration Manager," no Gestor de configuração biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="DeployRefCompTaskSeq"></a>Passo 4-3: Implementar a sequência de tarefas do computador de referência  
 Na consola do Configuration Manager, implemente a sequência de tarefas que criou anteriormente no processo para a coleção de dispositivos que inclui o computador de referência criado anteriormente no processo.  

#### <a name="to-deploy-the-task-sequence"></a>Para implementar a sequência de tarefas
1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **implementar**.  

     Inicia o Assistente de implementação de Software.  

6.  Conclua o Assistente para implementar Software com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Geral**|1.  No **coleção**, clique em **procurar**.<br />2.  No **procurar coleção** caixa de diálogo, clique em **Microsoft Deployment – o computador de referência**e, em seguida, clique em **OK**.<br />3.  No **comentário**, tipo **implementar o Windows 8.1 para o computador de referência e, em seguida, captura uma imagem do computador de referência**.<br />4.  Clique em **Seguinte**.|  
    |**Definições de implementação**|1.  No **objetivo**, selecione **disponível**.<br />2.  Selecione o **tornar disponível para efetuar o arranque de suportes de dados e PXE** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Definições de implementação: Agenda**|Clique em **Seguinte**.|  
    |**Definições de implementação: Experiência de utilizador**|Clique em **Seguinte**.|  
    |**Definições de implementação: Alertas**|Clique em **Seguinte**.|  
    |**Definições de implementação: Pontos de distribuição**|Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para implementar a sequência de tarefas é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para implementar uma sequência de tarefas," no Gestor de configuração biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="CreateTaskSeqBootMedia"></a>Passo 4-4: Criar tarefas sequência suportes de dados  
 Para iniciar o processo do MDT, fornecem um método para iniciar o computador com o Windows PE e o software necessário ao criar o disco de suportes de dados de sequência de tarefas. Utilize o Assistente de suporte de dados de sequência de tarefas na consola do Configuration Manager para criar suportes de dados para armazenamento de uma unidade flash USB, CD ou DVD.  

#### <a name="to-create-a-task-sequence-bootable-media-disk"></a>Para criar um disco de suportes de dados de sequência de tarefas  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para Microsoft System Center 2012. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar suporte de sequência de tarefas**.  

     Inicia o assistente suporte de dados de criação de sequência de tarefas.  

5.  Conclua o Assistente de criação tarefas sequência de suportes de dados com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Selecione o tipo de suporte de dados**|1.  Clique em **suportes de dados**.<br />2.  Limpar o **permitir a implementação do sistema operativo autónoma** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Selecione o tipo de suporte: Gestão de suporte de dados**|Clique em **suporte de dados baseado no Site**e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Tipo de suporte de dados**|No **ficheiro de multimédia**, tipo  **\\\WDG-MDT-01\Capture$\CM2012_TS_Boot_Media.iso**e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Segurança**|No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Imagem de arranque**|1.  No **imagem de arranque**, clique em **procurar**.<br />2.  No **selecionar uma imagem de arranque** caixa de diálogo, clique em **personalizada do Windows PE**e, em seguida, clique em **OK**.<br />3.  No **ponto de distribuição**, clique em  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />4.  No **ponto de gestão**, clique em  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />5.  Clique em **Seguinte**.|  
    |**Selecione o tipo de suporte: Personalização**|Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para criar o suporte de dados de sequência de tarefas é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

    O assistente cria o ficheiro CM2012_TS_Boot_Media.iso na pasta partilhada WDG-MDT-01Capture$.  

6.  Se WDG-REF-01 um computador físico, crie um CD ou DVD da organização internacionais para ficheiro uniformização (ISO). Se WDG-REF-01 uma VM, inicie a VM diretamente a partir do ficheiro ISO.  

 Para obter mais informações sobre como criar o disco de suportes de dados de sequência de tarefas, consulte a secção "Como para criar suportes de dados" no Gestor de configuração biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="StartRefCompwithTaskSeqBootMedia"></a>Passo 4-5: Iniciar o computador de referência com o suporte de suportes de sequência de tarefas  
 Inicie o computador de referência (WDG-REF-01) com o disco de suportes de dados de sequência de tarefas criado anteriormente no processo. Esta média inicia o Windows PE no computador de referência e inicia o processo de MDT. No final do processo do MDT, Windows 8.1 está implementado no computador de referência e \WDG-MDT-01\Capture$\WDG-REF-01.wim é guardada uma imagem do computador de referência.  

> [!NOTE]   
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows.  

#### <a name="to-start-the-reference-computer-with-the-task-sequence-bootable-media"></a>Para iniciar o computador de referência com as tarefas sequência suportes de dados

1.  Inicie WDG-REF-01 com a tarefa sequência suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de sequência de tarefas.  

2.  Conclua o Assistente de sequência de tarefas com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Bem-vindo ao Assistente de sequência de tarefas**|No **palavra-passe**, tipo  **P@ssw0rd** e, em seguida, clique em **seguinte**.|  
    |**Selecione uma sequência de tarefas**|Na caixa de lista, selecione **implementação de referência do Windows 8.1**e, em seguida, clique em **seguinte**.|  

#### <a name="to-monitor-the-reference-computer-deployment-process-using-the-deployment-workbench-complete-the-following-steps-on-wdg-mdt-01"></a>Para monitorizar o processo de implementação de computador de referência utilizando o Deployment Workbench, conclua os seguintes passos no WDG-MDT-01

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring.  

3.  No painel de detalhes, veja o processo de implementação para **WDG-REF-01**.  

4.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes. Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

5.  No painel de detalhes, clique em **WDG-REF-01**.  

6.  No painel ações, clique em **propriedades**.  

     O **WDG-REF-01 propriedades** é apresentada a caixa de diálogo.  

7.  No **WDG-REF-01 propriedades** caixa de diálogo a **identidade** separador, ver as informações de monitorização fornecidas sobre o processo de implementação da seguinte forma:

    |**Informações**|**Descrição**|  
    |-|-|  
    |**ID**|Identificador exclusivo para o computador que está a ser implementado.|  
    |**Nome do computador**|O nome do computador que está a ser implementado.|  
    |**Estado de implementação**|O estado atual do computador que está a ser implementado; o estado pode ser um dos seguintes:<br /><br /> -   **Executar**. A sequência de tarefas é bom estado de funcionamento e em execução.<br />-   **Não foi possível**. A sequência de tarefas falha e o processo de implementação foi bem-sucedido.<br />-   **Concluir**. A sequência de tarefas foi concluída.<br />-   **Responder**. A sequência de tarefas não tiver atualizado o seu estado nas últimas quatro horas e é prestada, tentados.|  
    |**Passo**|O passo de sequência tarefas atual a ser executado.|  
    |**Progresso**|O progresso global da sequência de tarefas. A barra de progresso indica quantos passos de sequência de tarefas terem sido executados fora do número total de passos de sequência de tarefas.|  
    |**Iniciar**|A hora de início do processo de implementação.|  
    |**Fim**|A hora em que terminou o processo de implementação.|  
    |**Decorrido**|O período de tempo, o processo de implementação tem estado em execução ou demorou a execução se foi concluído o processo de implementação.|  
    |**Erros**|O número de erros encontrados durante o processo de implementação.|  
    |**Avisos**|O número de avisos durante o processo de implementação.|  
    |**Ambiente de trabalho remoto**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota com o computador que está a ser implementado através da funcionalidade de ambiente de trabalho remoto do Windows. Este método parte do princípio de que:<br /><br /> -O sistema operativo de destino está em execução e tiver ativada de suporte de ambiente de trabalho remoto<br />-   **mstsc.exe** está no caminho do **Nota:**  Este botão é sempre visível, mas pode não ser capaz de estabelecer uma sessão de ambiente de trabalho remoto, se o computador monitorizado está a executar o Windows PE, não foi concluída a instalação do sistema operativo de destino ou não tem ativada a funcionalidade de ambiente de trabalho remoto.|  
    |**Ligação de VM**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota para uma VM em execução no HyperV®. Este método parte do princípio de que:<br /><br /> -A implementação está a ser efetuada a uma VM em execução no Hyper-V<br />-   **vmconnect.exe** está localizado na pasta %ProgramFiles%\Hyper-V **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que os componentes de integração do Hyper-V estão em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Controlo remoto de daRT**|Este botão permite-lhe estabelecer uma sessão de controlo remoto utilizando a funcionalidade Visualizador remoto na Diagnostics e Recovery Toolkit (DaRT).<br /><br /> Este método parte do princípio de que:<br /><br /> -DaRT ter sido implementado no computador de destino e estiver em execução<br />-   **DartRemoteViewer.exe** está localizado na pasta %ProgramFiles%\Microsoft DaRT 7\v7 **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que DaRT está em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Atualizar automaticamente estas informações a cada 10 segundos**|Caixa de verificação que controla se as informações na caixa de diálogo é automaticamente atualizadas. Se a caixa de verificação:<br /><br /> -Selecionado, as informações são atualizadas cada 10 segundos<br />-Limpo, as informações não são automaticamente atualizadas e têm de ser manualmente atualizadas utilizando o **atualizar agora** botão|  
    |**Atualizar neste momento**|Este botão imediatamente atualiza as informações apresentadas na caixa de diálogo.|  

8.  No **WDG-REF-01 propriedades** caixa de diálogo, clique em **OK**.  

9. Feche o Deployment Workbench.  

#### <a name="to-monitor-the-reference-computer-deployment-process-using-the-get-mdtmonitordata-cmdlet-complete-the-following-steps-on-wdg-mdt-01"></a>Para monitorizar o processo de implementação de computador de referência utilizando o cmdlet Get-MDTMonitorData, conclua os seguintes passos no WDG-MDT-01

1.  No WDG-MDT-01, clique em **iniciar**, clique em **ferramentas administrativas**e, em seguida, clique em **módulos do Windows PowerShell**.  

     Abre a linha de comandos de módulos do Windows PowerShell.  

2.  Criar uma unidade do PowerShell que utiliza o fornecedor do PowerShell do MDT, executando o [New-PSDrive](http://technet.microsoft.com/library/hh849829.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    New-PSDrive -Name DS001 -PSProvider mdtprovider -Root d:\DeploymentShare$  
    ```  

3.  Ver o MDT monitorização processo executando o **Get-MDTMonitorData** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-MDTMonitorData -Path DS001:  
    ```  

     Este comando devolve os dados de monitorização recolhidos pelo MDT monitorização do serviço está em execução no mesmo computador que aloja a partilha de implementação, conforme mostrado no seguinte exemplo de saída:  

    ```  
    Name               : WDG-REF-01  
    PercentComplete    : 96  
    Settings           :  
    Warnings           : 0  
    Errors             : 0  
    DeploymentStatus   : 1  
    StartTime          : 6/7/2012 6:45:39 PM  
    EndTime            :   
    ID                 : 1  
    UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1  
    CurrentStep        : 130  
    TotalSteps         : 134  
    StepName           : Gather  
    LastTime           : 6/7/2012 8:46:32 PM  
    DartIP             :  
    DartPort           :  
    DartTicket         :  
    VMHost             : XYL-DC-02  
    VMName             : WDG-REF-01  
    ComputerIdentities : {}  
    ```  

4.  Feche a consola do Windows PowerShell.  

 Se ocorrerem problemas durante a implementação, consulte o documento de MDT *referência de resolução de problemas*. Quando tiver terminado, uma imagem capturada do computador de referência deve existir no \\\WDG-MDT-01\Capture$\WDG-REF-01.wim.  

## <a name="step-5-create-and-configure-a-task-sequence-to-deploy-the-target-computer"></a>Passo 5: Criar e configurar uma sequência de tarefas para implementar o computador de destino  
 Após a conclusão da sequência de tarefas para implementar o computador de referência (WDG-REF-01), uma imagem capturada do computador de referência é armazenada no \\\WDG-MDT-01\Capture$\WDG-REF-01.wim. Agora, crie uma sequência de tarefas que irá implementar a imagem capturada do computador de referência para o computador de destino (WDG-CLI-01). Quando este passo é concluído, pode implementar a imagem capturada do computador de referência para o computador de destino.  

 Criar e configurar uma sequência de tarefas para implementar o computador de destino:  

-   Importar o ficheiro. wim capturado no passo anterior para o Configuration Manager utilizando o Assistente para adicionar imagem de sistema operativo, conforme descrito em [passo 5-1: Importar o ficheiro. wim capturado para o Configuration Manager](#ImportCapturedwimFile)  

-   Utilizando o Assistente de criação MDT tarefas sequência para criar um modelo de sequência de tarefas do MDT para implementar a imagem capturada do computador de referência para o computador de destino, conforme descrito em [passo 5-2: Criar uma sequência de tarefas do MDT para implementar a imagem capturada](#CreateMDTTaskSeqDeployCapturedImage)  

-   Selecionar os pontos de distribuição para os novos pacotes e imagens que o assistente criar MDT tarefas sequência cria conforme descrito em [passo 5-3: Selecione os pontos de distribuição para os novos pacotes e a imagens](#SelectDistroPointsNewPackagesImages)  

-   Personalizar os ficheiros de configuração do MDT para o computador de destino — especificamente, o ficheiro CustomSettings.ini, conforme descrito em [passo 5-4: Personalizar os ficheiros de configuração do MDT](#CustomizetheMDTConfigFiles)  

-   Atualizar os pontos de distribuição do Configuration Manager para o pacote de definições personalizadas, conforme descrito em [passo 5-5: Atualizar os pontos de distribuição para o pacote de definições personalizadas](#UpdateDistroPointsforCustomSettings)  

-   Personalizar a sequência de tarefas para o computador de destino, conforme descrito em [passo 5-6: Personalizar a sequência de tarefas para o computador de destino](#CustomizeTaskSequenceTargetComputer)  

###  <a name="ImportCapturedwimFile"></a>Passo 5-1: Importar o ficheiro. wim capturado para o Configuration Manager  
 Depois da imagem do computador de referência (WDG-REF-01) é capturada no ficheiro. wim, importe o ficheiro. wim capturado para o Configuration Manager. Importe o ficheiro. wim capturado para o nó de imagens do sistema operativo utilizando o Assistente para adicionar imagem de sistema operativo.  

 O wim capturado contém duas imagens, um para cada partição no computador de referência. Identificar quais das imagens tem a Windows 8.1 capturada do sistema operativo ao verificar a descrição da imagem que contém *Windows 8.1*. Irá utilizar o índice de imagem quando criar a sequência de tarefas para implementar a imagem capturada ao computador de destino.  

 **Para importar o ficheiro. wim capturado para o Configuration Manager**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para imagens de sistema de operativo/sistemas operativos/descrição geral.  

4.  No Friso, no **criar** , clique em **adicionar imagem de sistema operativo**.  

     Inicia o Assistente para adicionar imagem de sistema operativo.  

5.  Conclua o Assistente de imagem de sistema operativo adicionar utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Na página do Assistente**|**Fazê-lo**|  
    |**Origem de dados**|No **caminho**, tipo  **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**e, em seguida, clique em **seguinte**.|  
    |**Geral**|1.  No **nome**, tipo **imagem de referência do Windows 8.1**.<br /><br /> 1.  No **versão**, tipo **1.00**.<br /><br /> 1.  No **comentários**, tipo **Windows 8.1 Capturar imagem do computador de referência (WDG-REF-01) utilizado para implementar em computadores de destino**e, em seguida, clique em **seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para importar a imagem do sistema operativo é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

6.  No painel de pré-visualização, clique em **imagem de referência do Windows 8.1**.  

7.  No painel de pré-visualização, clique o **detalhes** separador.  

     É apresentada a lista de partições de sistema operativo capturada. o wim. O índice de imagem contém Windows 8.1 é o índice de imagem que irá especificar mais tarde durante o Assistente de criação MDT tarefas sequência.  

8.  Registe o índice de imagem contém Windows 8.1.  

    > [!TIP]    
    >  Para efeitos deste exemplo, o índice de imagens 2 deve ter o sistema operativo do Windows 8.1.  

###  <a name="CreateMDTTaskSeqDeployCapturedImage"></a>Passo 5-2: Criar uma sequência de tarefas do MDT para implementar a imagem capturada  
 Depois da imagem ser capturada, crie uma sequência de tarefas para implementar a imagem capturada do computador de referência (WDG-REF-01) para o computador de destino (WDG-CLI-01). A maioria dos pacotes necessários para esta sequência de tarefas foram criada anteriormente no processo. No entanto, tem de criar um novo pacote de definições do MDT personalizadas que tenha as definições de configuração correto para o computador de destino e cria uma imagem do sistema operativo da imagem capturada do computador de referência.  

#### <a name="to-create-a-task-sequence-template-to-deploy-the-captured-image-to-the-target-computer"></a>Para criar um modelo de sequência de tarefas para implementar a imagem capturada ao computador de destino  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **sequências de tarefas** , clique em **criar sequência de tarefas do MDT**.  

     Inicia o Assistente de criação MDT tarefas sequência.  

5.  Conclua a criar MDT assistente sequência de tarefas com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Escolha o modelo**|Selecione **sequência de tarefas de cliente**e, em seguida, clique em **seguinte**.|  
    |**Escolha o modelo: Geral**|1.  No **nome da sequência de tarefas**, tipo **implementação de destino do Windows 8.1**.<br />2.  No **comentários de sequência de tarefas**, tipo **sequência para implementar a imagem do computador de referência capturada ao computador de destino (WDG-CLI-01) de tarefas**e, em seguida, clique em **seguinte**.|  
    |**Escolha o modelo: Detalhes**|<ol><li>Clique em **aderir a um domínio**.</li><li>No **domínio**, tipo **mdt2013.corp.woodgrovebank.com**.</li><li>No **conta**, clique em **definir**e, em seguida, conclua o **conta de utilizador do Windows** caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome de utilizador**, tipo **MDT2013\Administrator**.</li><li>No **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** .</li><li>Clique em **OK**.</li></ol></li><li>No **nome de utilizador**, tipo **Woodgrove Bank empregado**.</li><li>No **nome da organização**, tipo **Banco Woodgrove**.</li><li>No **chave de produto**, tipo ***product_key*** (onde *product_key* é a chave de produto para Windows 8.1).</li><li>Clique em **Seguinte**.</li></ol>|  
    |**Escolha o modelo: Capturar definições**|Clique em **Seguinte**.|  
    |**Imagem de arranque**|1.  No **especificar um pacote de imagem de arranque existentes**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **personalizada do Windows PE**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Pacote de MDT**|1.  No **especificar um pacote de ficheiros de Toolkit do Microsoft implementação existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **ficheiros MDT**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Imagem do SO**|1.  Clique em **imagem de especificar um SO existente**.<br />2.  No **imagem de especificar um SO existente**, clique em **procurar**.<br />3.  No **selecionar um pacote** caixa de diálogo, clique em **imagem de referência do Windows 8.1**e, em seguida, clique em **OK**.<br />4.  Clique em **Seguinte**.|  
    |**Imagem do SO: Índice de imagem do SO**|1.  No **o ficheiro de imagem (WIM) do sistema operativo selecionado contiver várias imagens**. **Especifique a imagem que pretende implementar**, selecione ***image_index*** (onde *image_index* é o índice de imagem da imagem que contém o Windows 8.1, que foi identificado na secção [Passo 5-1: Importar o wim de Captured ficheiro para o Configuration Manager](#ImportCapturedwimFile); para efeitos deste guia, selecione **2**).<br />2.  Clique em **Seguinte**.|  
    |**Método de implementação**|Clique em **Seguinte**.|  
    |**Pacote de cliente**|1.  No **especificar um pacote de cliente do ConfigMgr existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **a atualização de cliente do Microsoft Configuration Manager**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Pacote USMT**|1.  No **especificar um pacote USMT existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **USMT**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Pacote de definições**|1.  Clique em **criar um novo pacote de definições**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\CustomSettings_Target**e, em seguida, clique em **seguinte**.|  
    |**Pacote de definições: Detalhes de definições**|1.  No **nome**, tipo **definições personalizadas do MDT destino computador**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **definições de configuração para o processo de implementação do MDT (por exemplo, CustomSettings.ini) para o computador de destino**e, em seguida, clique em **seguinte**.|  
    |**Pacote Sysprep**|Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|É apresentado o progresso da criação de sequência de tarefas.|  
    |**Confirmação**|Clique em **Concluir**.|  

 É apresentada a lista de sequências de tarefas. A sequência de tarefas que acabou de criar (implementação de destino do Windows 8.1) está listada na lista de sequências de tarefas.  

###  <a name="SelectDistroPointsNewPackagesImages"></a>Passo 5-3: Selecione os pontos de distribuição para os novos pacotes e a imagens  
 Assistente de criação MDT tarefas sequência cria um número de pacotes e imagens. Depois destes pacotes e imagens são criadas, selecione os pontos de distribuição a partir da qual as imagens e o pacote será copiado e disponíveis para computadores de destino.  

> [!NOTE]
>  Neste exemplo, não há apenas um ponto de distribuição (WDG-MDT-01). No entanto, a maioria das redes de produção tem vários pontos de distribuição. Quando executar este passo num ambiente de produção, selecione os pontos de distribuição apropriados para a rede.  

#### <a name="to-select-the-distribution-points-for-software-distribution-packages"></a>Para selecionar os pontos de distribuição para pacotes de distribuição de software  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de visualização, selecione **implementação de destino do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Geral**|Clique em **Seguinte**.|  
    |**Conteúdo**|Clique em **Seguinte**.|  
    |**Gerais: Conteúdo**|Clique em **Seguinte**.|  
    |**Gerais: Destino do conteúdo**|1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDGMDT01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso da distribuição de software é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizetheMDTConfigFiles"></a>Passo 5-4: Personalizar os ficheiros de configuração do MDT  
 Quando a sequência de tarefas para o computador de destino tiver sido criado, personalizar os ficheiros de configuração do MDT que fornecem as definições de configuração para a implementação do Windows 8.1 para o computador de destino — especificamente, CustomSettings.ini.  

 Quando tiver sido personalizado ficheiro CustomSettings.ini, guarde ficheiros atualizados para a pasta de origem para o pacote de definições personalizadas de MDT criado anteriormente no processo (E:\Packages$\CustomSettings_Target).  

#### <a name="to-customize-the-mdt-configuration-files-for-the-target-computer"></a>Para personalizar os ficheiros de configuração do MDT para o computador de destino  

1.  No Explorador do Windows, aceda à pasta E:\Packages$\CustomSettings_Target e, em seguida, faça duplo clique em **CustomSettings.ini**.  

2.  Abra o bloco de notas e, em seguida, adicione as seguintes linhas ao ficheiro CustomSettings.ini:  

    ```  
    EventService=http://WDG-MDT-01:9800  
    ```  

     Esta definição irá configurar a monitorização da implementação de computador de destino.  

    > [!NOTE]
    >  Efetue as alterações que são necessários pelo seu ambiente.  

     **Exemplo do ficheiro CustomSettings.ini editado:**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  
    SkipCapture=YES  
    SkipAdminPassword=NO  
    SkipProductKey=YES  
    EventService=http://WDG-MDT-01:9800  

    ```  

3.  Guarde o ficheiro e, em seguida, feche o bloco de notas.  

###  <a name="UpdateDistroPointsforCustomSettings"></a>Passo 5-5: Atualizar os pontos de distribuição para o pacote de definições personalizadas  
 Quando a pasta de origem tiver sido atualizada para o pacote de definições de personalizado do computador de destino do MDT no Configuration Manager, atualize os pontos de distribuição para o pacote de definições de personalizado do computador de destino do MDT. Atualizar os pontos de distribuição copia a versão atualizada do ficheiro CustomSettings.ini para as partilhas de implementação especificadas no pacote.  

#### <a name="to-update-the-distribution-points-for-the-custom-settings-package"></a>Para atualizar a distribuição aponta para o pacote de definições personalizadas  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para gestão/pacotes de aplicações/descrição geral.  

4.  No painel de pré-visualização, clique em **definições personalizadas do MDT destino computador**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **atualizar pontos de distribuição**.  

     O **do Configuration Manager** abre a caixa de diálogo, notificam que pretender atualizar o pacote em todos os pontos de distribuição.  

6.  No **do Configuration Manager** caixa de diálogo, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizeTaskSequenceTargetComputer"></a>Passo 5-6: Personalizar a sequência de tarefas para o computador de destino  
 Para a maioria das implementações, a sequência de tarefas de implementação de destino do Windows 8.1 criada anteriormente no processo efetua os passos necessários sem modificação. Neste exemplo, modifique o modelo de sequência de tarefas para definir a palavra-passe para a conta de administrador local para um valor conhecido. (Por predefinição, a sequência de tarefas define a palavra-passe para a conta de administrador local para um valor aleatório.) A sequência de tarefas pode exigir mais personalização, dependendo do ambiente.  

#### <a name="to-customize-the-windows-81-target-deployment-task-sequence"></a>Para personalizar a sequência de tarefas de implementação de destino do Windows 8.1

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **sequência de tarefas** , clique em **editar**.  

     O **Editor de sequência de tarefas de implementação do Windows 8.1 referência** é aberta a caixa de diálogo.  

6.  No **Editor de sequência de tarefas de implementação do Windows 8.1 referência** caixa de diálogo, aceda a PostInstall/aplicar as definições do Windows.  

7.  No **propriedades** separador, clique em **ativar a conta e especificar a palavra-passe de administrador local**.  

8.  No **propriedades** separador **palavra-passe** e **Confirmar palavra-passe**, tipo  **P@ssw0rd** e, em seguida, clique em **aplicar** .  

9. Efetue quaisquer modificações adicionais para a sequência de tarefas que requer que o ambiente e, em seguida, clique em **OK**.  

10. Feche todas as janelas abertas e caixas de diálogo.  



## <a name="step-6-deploy-the-captured-image-of-the-reference-computer-to-the-target-computer"></a>Passo 6: Implementar a imagem capturada do computador de referência para o computador de destino  
 Quando capturar a imagem do computador de referência e criado e configurado a sequência de tarefas, implemente a imagem capturada. Configure o MDT para fornecer todas as definições de configuração necessárias para implementar o computador de destino. Depois de iniciar o processo de implementação, a imagem do computador de referência com o Windows 8.1 é implementada no computador de destino e automaticamente configurada com as definições especificadas.  

 Implemente a imagem capturada por:  

-   Adicionar o computador de destino para a base de dados do site do Configuration Manager, conforme descrito em [passo 6-1: Adicionar o computador de destino para a base de dados do Site do Configuration Manager](#AddTargetComptoConfigManager)  

-   Criar uma coleção de computadores que inclui o computador de destino, conforme descrito em [passo 6-2: Criar uma coleção de computadores que inclui o computador de destino](#CreateComputerCollectionIncludesTarget)  

-   Implementar a sequência de tarefas criada anteriormente no processo, como descrito no [passo 6-3: Implementar a sequência de tarefas do computador de destino](#DeployTargetComputerTaskSequence)  

-   Iniciar o computador de destino com os dados de arranque de sequências de tarefas, tal como descrito no [passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas](#StartTargetComputerTaskSequenceMedia)  

###  <a name="AddTargetComptoConfigManager"></a>Passo 6-1: Adicionar o computador de destino para a base de dados do Site do Configuration Manager  
 Para implementar um sistema operativo sem suporte de dados autónomo para um novo computador que o Configuration Manager não gerir atualmente, adicione o novo computador para a base de dados do site do Configuration Manager antes de iniciar o processo de implementação do sistema operativo. O Configuration Manager pode detetar automaticamente computadores na rede que tenha um sistema de operativo de Windows instalado. No entanto, se o computador não tiver nenhum sistema operativo instalado, utilize o Assistente para importar informações de computador para importar as informações do computador novo.  

#### <a name="to-add-the-target-computer-to-the-configuration-manager-site-database"></a>Para adicionar o computador de destino para a base de dados do site do Configuration Manager  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda à descrição geral/dispositivos.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar informações sobre o computador**.  

     O Assistente Importar informações o computador é iniciado.  

5.  Conclua o Assistente de importação de informações de computador, utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Selecione a origem**|Clique em **importar computador individual**e, em seguida, clique em **seguinte**.|  
    |**Selecione a origem: Único computador**|1.  No **nome do computador**, tipo **WDG-CLI-01**.<br />2.  No **endereço MAC**, tipo ***mac_address*** (onde *mac_address* é o endereço MAC do adaptador de rede principal para o computador de destino, WDG-CLI-01).<br />3.  Clique em **Seguinte**.|  
    |**Selecione a origem: Pré-visualização de dados**|Clique em **Seguinte**.|  
    |**Selecione a origem: Escolher coleção de destino**|Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para importar o computador é apresentado.|  
    |**Confirmação**|Clique em **Fechar**.|  

 Para obter mais informações sobre como adicionar um novo computador para a base de dados do site do Configuration Manager, consulte a secção "para importar informações sobre o computador para um único computador," na secção, "Como para implementar sistemas operativos no Configuration Manager," na configuração Gestor de biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="CreateComputerCollectionIncludesTarget"></a>Passo 6-2: Criar uma coleção de computadores que inclui o computador de destino  
 Na consola do Configuration Manager, crie uma coleção que inclua o computador de destino (WDG-CLI-01). Utilize esta coleção de computador mais tarde quando a sequência de tarefas que criou anteriormente no processo de publicidade.  

#### <a name="to-create-a-computer-collection-that-includes-the-target-computer"></a>Para criar uma coleção de computadores que inclui o computador de destino

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda a coleções de dispositivos/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar coleção de dispositivos**.  

     Inicia o Assistente para criar coleção de dispositivos.  

5.  Conclua o Assistente de coleção de dispositivos criar com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Na página do Assistente**|**Fazê-lo**|  
    |**Geral**|<ol><li>No **nome**, tipo **Microsoft Deployment – Batch 01**.</li><li>No **comentário**, tipo **computadores que estão a ser incluído no lote de computadores implementados primeiro**.</li><li>No **coleção limitado**, clique em **procurar**.<br /><br />     O **selecionar coleção** é apresentada a caixa de diálogo. Conclua a caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **selecionar coleção** caixa de diálogo **nome**, clique em **todos os sistemas**.</li><li>Clique em **OK**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Regras de Associação**|<ol><li>Clique em **Adicionar regra**e, em seguida, clique em **regra direta**.<br /><br />     O direto associação Assistente para criar regra é iniciado.</li><li>Conclua o direta associação Assistente para criar regra, efetuando os seguintes passos:<br /><br /> <ol><li>Na página de **Boas-vindas**, clique em **Seguinte**.</li><li>No **procurar recursos** na página **classe de recursos**, selecione **recurso do sistema**; na **nome de atributo**, selecione  **Nome**; na **valor**, tipo **WDG-CLI-01**; e, em seguida, clique em **seguinte**.</li><li>No **selecionar recursos** página, selecione **WDG-CLI-01**e, em seguida, clique em **seguinte**. **Nota:**          O processo para adicionar o computador de destino (WDG-CLI-01) para todos os sistemas pode demorar alguns minutos a concluir. Se WDG-CLI-01 não aparecer na lista, repita os passos b e c até WDGCLI01 aparece.</li><li>No **resumo** página, clique em **seguinte**.</li><li>No **conclusão** página, clique em **fechar**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para criar a coleção de dispositivos é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para criar coleções no Configuration Manager," no Gestor de configuração biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="DeployTargetComputerTaskSequence"></a>Passo 6-3: Implementar a sequência de tarefas do computador de destino  
 Na consola do Configuration Manager, implemente a sequência de tarefas que criou anteriormente no processo para os computadores de destino. Implemente a sequência de tarefas na coleção de computadores de destino criado anteriormente no processo.  

#### <a name="to-deploy-the-task-sequence"></a>Para implementar a sequência de tarefas  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **implementação de destino do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **implementar**.  

     Inicia o Assistente de implementação de Software.  

6.  Conclua o Assistente para implementar Software com as informações seguintes.  Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Geral**|1.  No **coleção**, clique em **procurar**.<br />2.  No **procurar coleção** caixa de diálogo, clique em **Microsoft Deployment – Batch 01**e, em seguida, clique em **OK**.<br />3.  No **comentário**, tipo **implementar o Windows 8.1 para o lote de computadores de destino primeiro**.<br />4.  Clique em **Seguinte**.|  
    |**Definições de implementação**|1.  No **objetivo**, selecione **disponível**.<br />2.  Selecione o **tornar disponível para efetuar o arranque de suportes de dados e PXE** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Definições de implementação: Agenda**|Clique em **Seguinte**.|  
    |**Definições de implementação: Experiência de utilizador**|Clique em **Seguinte**.|  
    |**Definições de implementação: Alertas**|Clique em **Seguinte**.|  
    |**Definições de implementação: Pontos de distribuição**|Clique em **Seguinte**.|  
    |**Resumo**|1.  Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior.<br />2.  Clique em **Seguinte**.|  
    |**Progresso**|O progresso para implementar a sequência de tarefas é apresentado.|  
    |**Conclusão**|Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para implementar uma sequência de tarefas," no Gestor de configuração biblioteca de documentação que é instalado com o Configuration Manager.  

###  <a name="StartTargetComputerTaskSequenceMedia"></a>Passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas  
 Inicie o computador de destino (WDG-CLI-01) com a tarefa sequência suportes de dados criado anteriormente no processo. Esta média inicia o Windows PE no computador de referência e inicia o processo de MDT. No final do processo do MDT, Windows 8.1 é implementado no computador de destino.  

> [!NOTE]
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows.  

#### <a name="to-start-the-target-computer-with-the-task-sequence-bootable-media"></a>Para iniciar o computador de destino com o suporte de suportes de sequência de tarefas

1.  Inicie WDG-CLI-01 com a tarefa sequência suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de sequência de tarefas.  

2.  Conclua o Assistente de sequência de tarefas com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|      
    |**Bem-vindo ao Assistente de sequência de tarefas**|No **palavra-passe**, tipo  **P@ssw0rd** e, em seguida, clique em **seguinte**.|  
    |**Selecione uma sequência de tarefas**|Na caixa de lista, selecione **implementação de destino do Windows 8.1**e, em seguida, clique em **seguinte**.|  

#### <a name="to-monitor-the-reference-computer-deployment-process-using-the-deployment-workbench"></a>Para monitorizar o processo de implementação de computador de referência utilizando o Deployment Workbench

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring.  

3.  No painel de detalhes, veja o processo de implementação para **WDG-CLI-01**.  

4.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes. Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

5.  No painel de detalhes, clique em **WDG-CLI-01**.  

6.  No painel ações, clique em **propriedades**.  

     O **WDG-CLI-01 propriedades** é apresentada a caixa de diálogo.  

7.  No **WDG-CLI-01 propriedades** caixa de diálogo a **identidade** separador, ver as informações de monitorização fornecidas sobre o processo de implementação, conforme descrito na seguinte tabela:

    |**Informações**|**Descrição**|  
    |-|-|  
    |**ID**|Identificador exclusivo para o computador que está a ser implementado.|  
    |**Nome do computador**|O nome do computador que está a ser implementado.|  
    |**Estado de implementação**|O estado atual do computador que está a ser implementado; o estado pode ser um dos seguintes:<br /><br /> -   **Executar**. A sequência de tarefas é bom estado de funcionamento e em execução.<br />-   **Não foi possível**. A sequência de tarefas falha e o processo de implementação foi bem-sucedido.<br />-   **Concluir**. A sequência de tarefas foi concluída.<br />-   **Responder**. A sequência de tarefas não tiver atualizado o seu estado nas últimas quatro horas e é prestada, tentados.|  
    |**Passo**|O passo de sequência tarefas atual a ser executado.|  
    |**Progresso**|O progresso global da sequência de tarefas. A barra de progresso indica quantos passos de sequência de tarefas terem sido executados fora do número total de passos de sequência de tarefas.|  
    |**Iniciar**|A hora de início do processo de implementação.|  
    |**Fim**|A hora em que terminou o processo de implementação.|  
    |**Decorrido**|O período de tempo, o processo de implementação tem estado em execução ou demorou a execução se foi concluído o processo de implementação.|  
    |**Erros**|O número de erros encontrados durante o processo de implementação.|  
    |**Avisos**|O número de avisos durante o processo de implementação.|  
    |**Ambiente de trabalho remoto**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota com o computador que está a ser implementado através da funcionalidade de ambiente de trabalho remoto do Windows. Este método parte do princípio de que:<br /><br /> -O sistema operativo de destino está em execução e tiver ativada de suporte de ambiente de trabalho remoto<br />-   **mstsc.exe** está no caminho do **Nota:**  Este botão é sempre visível, mas pode não ser capaz de estabelecer uma sessão de ambiente de trabalho remoto, se o computador monitorizado está a executar o Windows PE, não foi concluída a instalação do sistema operativo de destino ou não tem ativada a funcionalidade de ambiente de trabalho remoto.|  
    |**Ligação de VM**|Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota para uma VM em execução no Hyper-V. Este método parte do princípio de que:<br /><br /> -A implementação está a ser efetuada a uma VM em execução no Hyper-V<br />-   **vmconnect.exe** está localizado na pasta %ProgramFiles%\Hyper-V **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que os componentes de integração do Hyper-V estão em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Controlo remoto de daRT**|Este botão permite-lhe estabelecer uma sessão de controlo remoto utilizando a funcionalidade Visualizador remoto na Diagnostics e Recovery Toolkit (DaRT).<br /><br /> Este método parte do princípio de que:<br /><br /> -DaRT ter sido implementado no computador de destino e estiver em execução<br />-   **DartRemoteViewer.exe** está localizado na pasta %ProgramFiles%\Microsoft DaRT 7\v7 **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que DaRT está em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Atualizar automaticamente estas informações a cada 10 segundos**|Caixa de verificação que controla se as informações na caixa de diálogo é automaticamente atualizadas. Se a caixa de verificação:<br /><br /> -Selecionado, as informações são atualizadas cada 10 segundos<br />-Limpo, as informações não são automaticamente atualizadas e têm de ser manualmente atualizadas utilizando o **atualizar agora** botão|  
    |**Atualizar neste momento**|Este botão imediatamente atualiza as informações apresentadas na caixa de diálogo.|  

8.  No **WDG-REF-01 propriedades** caixa de diálogo, clique em **OK**.  

9. Feche o Deployment Workbench.  

#### <a name="to-monitor-the-reference-computer-deployment-process-using-the-get-mdtmonitordata-cmdlet"></a>Para monitorizar o processo de implementação de computador de referência utilizando o cmdlet Get-MDTMonitorData

1.  No WDG-MDT-01, clique em **iniciar**, aponte para **ferramentas administrativas**e, em seguida, clique em **módulos do Windows PowerShell**. Abre a linha de comandos de módulos do Windows PowerShell.  

2.  Criar uma unidade do PowerShell que utiliza o fornecedor do PowerShell do MDT, executando o [New-PSDrive](http://technet.microsoft.com/library/hh849829.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    New-PSDrive -Name DS001 -PSProvider mdtprovider -Root d:\DeploymentShare$  
    ```  

3.  Ver o MDT monitorização processo executando o **Get-MDTMonitorData** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-MDTMonitorData -Path DS001:  
    ```  

     Este comando devolve os dados de monitorização recolhidos pelo MDT monitorização do serviço está em execução no mesmo computador que aloja a partilha de implementação conforme mostrado no seguinte exemplo de saída:  

    ```  
    Name               : WDG-REF-01  
    PercentComplete    : 96  
    Settings           :  
    Warnings           : 0  
    Errors             : 0  
    DeploymentStatus   : 1  
    StartTime          : 6/7/2012 6:45:39 PM  
    EndTime            :   
    ID                 : 1  
    UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1  
    CurrentStep        : 130  
    TotalSteps         : 134  
    StepName           : Gather  
    LastTime           : 6/7/2012 8:46:32 PM  
    DartIP             :  
    DartPort           :  
    DartTicket         :  
    VMHost             : XYL-DC-02  
    VMName             : WDG-REF-01  
    ComputerIdentities : {}  

    Name               : WDG-CLI-01  
    PercentComplete    : 26  
    Settings           :  
    Warnings           : 0  
    Errors             : 0  
    DeploymentStatus   : 1  
    StartTime          : 6/7/2012 3:07:13 AM  
    EndTime            :   
    ID                 : 2  
    UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1  
    CurrentStep        : 49  
    TotalSteps         : 134  
    StepName           : Capture Network Settings using MDT  
    LastTime           : 6/7/2012 3:08:32 AM  
    DartIP             :  
    DartPort           :  
    DartTicket         :  
    VMHost             :   
    VMName             :   
    ComputerIdentities : {}  
    ```  

4.  Feche a consola do Windows PowerShell.  

 Se ocorrerem problemas durante a implementação, consulte o documento de MDT *referência de resolução de problemas*. Quando concluída com êxito, o computador de destino com um sistema de operativo Windows 8.1 configurado como o computador de referência.
