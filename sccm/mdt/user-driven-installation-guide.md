---
title: Início rápido - instalação orientado por utilizador
titleSuffix: Microsoft Deployment Toolkit
description: 'Um guiide de início rápido para utilizar o Microsoft Deployment Toolkit para instalação orientado por utilizador. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: dcddc250-9361-4e69-af45-472da4ef5fd5
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 56d65db90e87e67cb3d0dcdd3224206444d44888
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
ms.locfileid: "27821584"
---
# <a name="quick-start-guide-for-user-driven-installation"></a>Guia de introdução para instalação orientado por utilizador  
 Microsoft Deployment Toolkit (MDT) 2013 fornece tecnologias para implementar sistemas operativos Windows e Microsoft Office. Este guia de introdução ajuda-o a avaliar rapidamente o MDT 2013, fornecendo instruções passo a passo condensed para utilizá-la para instalar o sistema de operativo do Windows 8.1 e o Microsoft Office Professional Plus 2010 com o modo instalação (UDI) e a Microsoft System Center 2012 R2 Configuration Manager. Este guia de introdução demonstra como efetuar o cenário de implementação MDT novo computador, que abrange a implementação do Windows 8.1 para um novo computador. Este cenário pressupõe que não há nenhum perfil para preservar ou dados de utilizador.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

 Depois de utilizar este guia para avaliar o MDT, reveja o resto da documentação de orientação do MDT para saber mais sobre as funcionalidades avançadas da tecnologia.  

> [!NOTE]
>  A configuração de infraestrutura descrita aqui é para fins de avaliação e não se destina a um sistema de produção.  

## <a name="prerequisites"></a>Pré-requisitos  
 As instalações de UDI utilizando o System Center 2012 R2 Configuration Manager tem os seguintes pré-requisitos.  

### <a name="required-software"></a>Software necessário  
 Para concluir este guia, é necessário o seguinte software:  

-   Windows Server 2008 R2  

-   Microsoft SQL Server® 2008 R2  

-   SQL Server 2008 R2 Service Pack 1 (SP1)  

-   SQL Server 2008 R2 SP1 a atualização cumulativa 6 (CU6)  

-   Windows 8,1  

-   System Center 2012 R2 Configuration Manager  

-   Office Professional Plus 2010 licenciamento em volume, versão de 32 bits  

-   Microsoft .NET Framework versão 3.5 com SP1  

-   Windows PowerShell™ versão 2.0  

-   Ambiente de pré-instalação do Windows (Windows PE), que está incluído no Configuration Manager  

-   Serviços de rede, incluindo o sistema de nomes de domínio (DNS) e protocolo de configuração dinâmica de anfitrião (DHCP)  

-   Serviços de domínio do Active Directory Directory® (AD DS)  

> [!NOTE]
>  O sequenciador de tarefas utilizados em implementações de MDT requer que criar Global à direita possível atribuir o objeto para as credenciais utilizadas para aceder e executar o Deployment Workbench e o processo de implementação. Este direito está normalmente disponível para contas com permissões ao nível do administrador (a menos que removeu explicitamente). Além disso, a segurança especializada – perfil de segurança da funcionalidade limitada (SSLF) remove o direito de criar a objetos globais e não deve ser aplicada a computadores implementados com o MDT.  

### <a name="computer-configuration"></a>Configuração do computador  
 Para concluir este guia, configure os computadores listados na tabela 1. Estes computadores podem ser computadores físicos ou máquinas virtuais (VMs) com os recursos de sistema designados.  

### <a name="table-1-computers-used-in-this-guide"></a>Tabela 1. Computadores utilizados neste guia  

|**Computador** |**A descrição e o sistema de recursos** |  
|-|-|  
|WDG-MDT-01|Este computador é executada a infraestrutura do MDT e o Configuration Manager. O computador executar o Windows Server 2008 R2 com os seguintes serviços de rede instalados:<br /><br /> -AD DS<br />-Servidor DNS<br />-DHCP Server<br />-Serviços de implementação<br /><br /> Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador quad-core em execução em 2,66 gigahertz (GHz) ou mais rápida<br />-igual ou superior de memória física 4 gigabytes (GB)<br />-A partição de disco que tem 40 GB ou mais de espaço em disco disponível; ele irá tornar-se a partição da unidade C<br />-Um CD-ROM ou DVD-ROM unidade que será atribuída a letra de unidade D<br />-A partição de disco que tem 40 GB ou mais de espaço em disco disponível; irá tornar-se a partição E.|  
|WDG-REF-01|Este é o computador de referência, que é executada sem sistema operativo atual. Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador que executa a 1,4 GHz ou mais rápida<br />-1 GB ou mais memória física<br />-16 GB ou mais de espaço em disco disponível|  
|WDG-CLI-01|Este é o computador de destino, que é executada sem sistema operativo atual. Os recursos do sistema do computador são os seguintes:<br /><br /> -Processador que executa a 1,4 GHz ou mais rápida<br />-1 GB ou mais memória física<br />-16 GB ou mais de espaço em disco disponível|  

 Os recursos listados na tabela 1 refletem os recursos de sistema recomendados para executar os passos neste guia. Para informações sobre os requisitos de recursos de sistema mínimos para:  

-   Windows Server 2008 R2, consulte [instalar o Windows Server 2008 R2](http://technet.microsoft.com/library/dd379511\(WS.10\).aspx)  

-   SQL Server 2008 R2, consulte [Hardware e requisitos de Software para instalar o SQL Server 2008 R2](http://technet.microsoft.com/library/ms143506.aspx)  

> [!NOTE]
>  Este guia pressupõe que o MDT está a ser avaliado nos computadores físicos ou virtuais de 64 bits (x64). Se a avaliar o MDT nas plataformas de 32 bits (x86), transferência e instalação x86 edições do MDT e os componentes que este guia descreve.  

## <a name="step-1-prepare-the-prerequisite-infrastructure"></a>Passo 1: Preparar a infraestrutura de pré-requisito  
 Para efeitos deste guia, todos os serviços de infraestrutura de pré-requisito executado no computador com o nome *WDG-MDT-01*. Instale funções de servidor, serviços e software de pré-requisito neste computador antes de instalar o MDT.  

> [!NOTE]
>  Esta secção assume que está a criar uma nova infraestrutura do Configuration Manager para o MDT. Se estiver a utilizar uma infraestrutura existente do Configuration Manager, reveja os passos nesta secção e substitua os nomes de recursos existente para os recursos criados nesta secção (por exemplo, o nome do computador e as pastas partilhadas na rede). Depois de rever nesta secção, avance para [passo 2: Preparar o ambiente do MDT](#PreparetheMDTEnvironment)  

 Prepare a infraestrutura de pré-requisito antes de instalar o MDT por:  

-   Instalar o Windows Server 2008 R2, tal como descrito no [passo 1-1: Instale o Windows Server 2008 R2](#InstallWindowsServer2008)  

-   Criar as pastas necessárias e a rede partilhas conforme descrito em [passo 1-2: Criar as pastas necessárias e partilhas de rede](#CreatetheRequiredFoldersandNetworkShares)  

-   Obter o software necessário para executar os passos neste guia, conforme descrito em [passo 1-3: Obter o Software necessário](#ObtaintheRequiredSoftware)  

-   Instalar a função de servidor do AD DS, conforme descrito em [passo 1-4: Instalar a função de servidor DS AD](#InstalltheADDSServerRole)  

-   Instalar a função de servidor do servidor DHCP, conforme descrito em [passo 1-5: Instalar a função de servidor do servidor DHCP](#InstalltheDHCPServerServerRole)  

-   Instalar a função de servidor serviços Web (IIS), conforme descrito em [passo 1-6: Instalar a função de servidor do Web Services (IIS)](#InstalltheWebServicesServerRole)  

-   Adicionar as funcionalidades do Windows Server 2008 R2 necessárias, conforme descrito em [passo 1-7: Adicionar as funcionalidades do necessários do Windows Server 2008 R2](#AddtheRequiredWindowsServer2008Features)  

-   Criar as contas de utilizador e o serviço necessário para executar os passos neste guia, conforme descrito em [passo 1-8: Criar o utilizador necessário e contas de serviço](#CreatetheRequiredUserandServiceAccounts)  

-   Instalar o SQL Server 2008 R2 para o Configuration Manager para utilizar conforme descrito em [passo 1 e 9: Instale o SQL Server 2008 R2](#InstallSQLServer2008)  

-   Adicionar o servidor do site para o grupo de segurança de administradores, conforme descrito em [passo 1 a 10: Adicione o servidor de Site para o grupo de segurança de administradores](#AddtheSiteServertotheAdministratorsSecurityGroup)  

-   Instalar o Configuration Manager conforme descrito em [passo 1-11: Instalar o Configuration Manager](#InstallConfigurationManager)  

-   Configurar a conta de acesso de rede que utilizam a clientes do Configuration Manager para aceder a distribuição do Configuration Manager pontos conforme descrito em [passo 1-12: Configurar a conta de acesso de rede](#ConfiguretheNetworkAccessAccount)  

-   Configurar os limites de site do Configuration Manager e os grupos de limites, conforme descrito em [passo 1-13: Configurar os limites de Site do Configuration Manager e os grupos de limites](#ConfiguretheConfigurationManagerSiteBoundaries)  

-   Configurar a publicação de informações do site no AD DS e DNS, conforme descrito em [passo 1-14: Configurar a publicação de informações do Site no AD DS e DNS](#ConfigurethePublishingofSiteIntofrmation)  

-   Configuração da deteção de utilizadores do AD DS, tal como descrito no [passo 1-15: Configurar a deteção de utilizadores do Active Directory](#ConfigureDiscoveryofActiveDirectoryUsers)  

###  <a name="InstallWindowsServer2008"></a>Passo 1-1: Instale o Windows Server 2008 R2  
 Utilize as informações no 2 para instalar o Windows Server 2008 R2. Aceite os valores predefinidos exceto indicação em contrário.  

### <a name="table-2-information-for-installing-windows-server-2008-r2"></a>Tabela 2. Informações para instalar o Windows Server 2008 R2  

|**Quando lhe for pedido para** |**Forneça estes valores** |  
|-|-|  
|**Onde pretende instalar o Windows?** |**Disco 0 espaço não alocado** |  
|**Palavra-passe** |Qualquer palavra-passe segura|  
|**Nome do computador** |**WDG-MDT-01** |  
|**Formato para os volumes C e i** |**NTFS** |  
|**Configuração de TCP/IP** |Configurar com uma configuração de endereço IP estático, com as outras opções de configuração de TCP/IP conforme apropriado para o ambiente|  

###  <a name="CreatetheRequiredFoldersandNetworkShares"></a>Passo 1-2: Criar as pastas necessárias e partilhas de rede  
 O processo de implementação do MDT requer pastas adicionais que são utilizadas como origem para ficheiros ou para armazenar ficheiros criados durante o processo de implementação do MDT. Alguns destas pastas tem de ser partilhado para que possa ser acedidos a partir de outros computadores.  

 **Para criar as pastas necessárias e partilhas**  

1.  Criar as pastas e partilhas listadas na tabela 3 com as permissões especificadas para cada partilha  

    ### <a name="table-3-folders-that-the-mdt-deployment-process-requires"></a>Tabela 3. Pastas de que necessita do processo de implementação do MDT  

    |**Criar esta pasta** |**Com este nome de partilha** |**Com estas permissões de partilha.** |  
    |-|-|-|  
    |E:\Source$|$ De origem|**Os administradores**: Coproprietário<br /><br /> **Todas as pessoas**: Leitura|  
    |E:\Images$|$ De imagens|**Os administradores**: Coproprietário<br /><br /> **Todas as pessoas**: Leitura|  
    |E:\Capture$|Capturar$|**Os administradores**: Coproprietário<br /><br /> **Todas as pessoas**: Leitura|  
    |E:\Packages$|$ De pacotes|**Os administradores**: Coproprietário<br /><br /> **Todas as pessoas**: Leitura|  

2.  Crie as seguintes pastas:  

    -   E:\CMDownloads  

    -   E:\Source$\CustomSettings  

    -   E:\Source$\Drivers  

    -   E:Source$ Windows_8-1  

    -   E:Source$ MDT_2013  

    -   E:Source$ SQL2008R2  

    -   E:Source$ SQL2008R2SP1  

    -   E:Source$ SQL2008R2CU6  

    -   E:Source$ OfficeProPlus2010  

    -   E:Source$ ConfigMgr  

    -   E:Packages$ controladores  

3.  Copie os controladores de dispositivo para o computador de referência (WDG-REF-01) e o computador de destino (WDG-CLI-01) para E:\Source$\Drivers.  

    > [!NOTE]
    >  Os processos neste guia partem do princípio de que o computador de referência e o computador de destino têm os mesmos dispositivos e não necessitam de controladores de dispositivos diferentes.  

###  <a name="ObtaintheRequiredSoftware"></a>Passo 1-3: Obter o Software necessário  
 Para além do Windows Server 2008 R2, Windows 8.1 e System Center 2012 R2 Configuration Manager, determinado software é necessário para avaliar o MDT com base nos processos neste guia. Tabela 4 lista o software necessário para efetuar implementações com o MDT, onde obter o software e onde pretende colocar o software em WDG-MDT-01.  

### <a name="table-4-additional-software-required-for-deployment-using-mdt"></a>Tabela 4. Software adicional necessário para a implementação com o MDT  

|**Obter este software** |**Coloque nesta pasta** |  
|-|-|  
|MDT 2013|E:\Source$\MDT_2013|  
|Ficheiros de distribuição do Windows 8.1 do suporte de dados do produto|E:\Source$\Windows_8-1|  
|Controladores de dispositivo necessários para os computadores de referência e de destino (WDG-REF-01 e WDG-CLI-01)|E:\Source$\Drivers|  
|SQL Server 2008 R2 a partir do suporte do produto|E:\Source$\SQL2008|  
|SQL Server 2008 R2 SP1, disponíveis em [http://www.microsoft.com/download/en/details.aspx?id=26727](http://www.microsoft.com/download/en/details.aspx?id=26727)|E:\Source$\SQL2008R2SP1|  
|SQL Server 2008 R2 SP1 CU6, disponíveis em [http://support.microsoft.com/kb/2679367](http://support.microsoft.com/kb/2679367)|E:\Source$\SQL2008R2SP1CU6|  
|System Center 2012 R2 Configuration Manager do suporte de dados do produto|E:\Source$\ConfigMgr|  
|Office Professional Plus 2010 32-bit licenciamento em Volume da versão do suporte de dados do produto|E:\<PONTODEMONTAGEM> $\OfficeProPlus2010 de origem|  

###  <a name="InstalltheADDSServerRole"></a>Passo 1-4: Instalar a função de servidor DS AD  
 AD DS é necessário para fornecer autenticação e a atuar como um repositório para valores de configuração para os produtos da Microsoft e tecnologias que utiliza o MDT, tais como o Microsoft SQL Server e o Configuration Manager.  

 Para instalar o AD DS, execute o Assistente de DCPROMO para configurar o computador como um controlador de domínio. Instale o AD DS utilizando as informações na tabela 5, aceitar as predefinições, a menos que especificado em contrário.  

### <a name="table-5-information-for-installing-ad-ds"></a>Tabela 5. Informações para instalar o AD DS  

|**Quando lhe for pedido** |**Fazê-lo** |  
|-|-|  
|Para o tipo de domínio|Crie um novo domínio numa floresta nova.|  
|O nome de domínio completamente qualificado|Tipo **mdt2013.corp.woodgrovebank.com**.|  
|Para o nível funcional de floresta|Selecione **Windows Server 2008 R2.** |  
|Para instalar o serviço servidor DNS como parte do processo de instalação do controlador de domínio|Clique em **Sim**.|  

###  <a name="InstalltheDHCPServerServerRole"></a>Passo 1-5: Instalar a função de servidor do servidor DHCP  
 A função de servidor do servidor DHCP é necessário para fornecer a configuração automática de IP para os computadores de destino. Instale o servidor DHCP, utilizando as informações na tabela 6, aceitar as predefinições, a menos que especificado em contrário.  

> [!NOTE]
>  Se estiver a utilizar um ambiente virtualizado, desative qualquer configuração de DHCP que fornece o software de Virtualização do computador. Certifique-se de que o serviço de servidor DHCP está em execução WDG-MDT-01 é o único fornecedor de configuração de IP utilizando o DHCP.  

### <a name="table-6-information-for-installing-the-dhcp-server-server-role"></a>Tabela 6. Informações para instalar a função de servidor do servidor DHCP  

|**Na página do Assistente** |**Fazê-lo** |  
|-|-|  
|**Autorizar o servidor DHCP no Active Directory** |Autorize WDG-MDT-01 para fornecer configuração de IP de cliente.|  
|**Âmbitos de DHCP** |Crie um âmbito adequado que pode ser utilizado para configurar automaticamente o TCP/IP para WDG-REF-01 e WDG-CLI-01.|  
|**Configuração de modo sem monitorização de estado de DHCPv6** |Desative o modo sem monitorização de estado de DHCPv6 para este servidor.|  

###  <a name="InstalltheWebServicesServerRole"></a>Passo 1-6: Instalar a função de servidor do Web Services (IIS)  
 Instale a função de servidor serviços Web (IIS) com os serviços de função listados na tabela 7, que são necessários para o SQL Server 2008 R2 e o Configuration Manager. Salvo especificação em contrário, utilize os valores predefinidos.  

### <a name="table-7-information-for-installing-the-web-services-iis-server-role"></a>A tabela 7. Informações para instalar a função de servidor do Web Services (IIS)  

|**Serviço de função** |**Estado** |  
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

###  <a name="AddtheRequiredWindowsServer2008Features"></a>Passo 1-7: Adicionar as funcionalidades do necessários do Windows Server 2008 R2  
 Para além de instalar as funções de servidor necessárias do Windows Server 2008 R2, adicione as seguintes funcionalidades necessárias no Gestor de servidor no **funcionalidades resumo** secção:  

-   Serviço de transferência inteligente em segundo plano  

-   Compressão de diferencial remota  

###  <a name="CreatetheRequiredUserandServiceAccounts"></a>Passo 1-8: Criar o utilizador necessário e contas de serviço  
 Configuration Manager e o SQL Server 2008 R2 necessitam de contas de utilizador durante o processo de instalação. Tabela 8 apresenta as informações necessárias para criar estas contas.  

### <a name="table-8-information-for-creating-the-required-accounts"></a>Tabela 8. Informações para criar as contas necessárias  

|**Criar esta conta** |**Com estas definições** |  
|-|-|  
|Conta de serviço do SQL Server Agent|1.  No **nome próprio**, tipo **SQL Agent**.<br />2.  No **Apelido**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLAgent**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o serviço do agente do SQL Server 2008 R2**.|  
|Conta de serviço do motor de base de dados do SQL Server|1.  No **nome próprio**, tipo **motor de base de dados do SQL Server**.<br />2.  No **Apelido**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLDBEngine**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o motor de base de dados do SQL Server 2008 R2**.|  
|Conta de serviço do SQL Server Reporting Services|1.  No **nome próprio**, tipo **SQL Reporting**.<br />2.  **No último nome**, tipo **conta de serviço**.<br />3.  No **nome de início de sessão do utilizador**, tipo **SQLReport**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  Torne a conta de um membro do grupo de segurança Admins do domínio.<br />8.  No **Descrição**, tipo **Service conta utilizada para executar o SQL Server 2008 R2 reporting services**.|  
|Conta de acesso de rede do cliente do System Center Configuration Manager do sistema|1.  No **nome próprio**, tipo **CM 2012**.<br />2.  No **Apelido**, tipo **acesso de rede do cliente**.<br />3.  No **início de sessão do utilizador** nome, escreva **CMNetAccess**.<br />4.  No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />5.  Limpar o **o utilizador deve alterar a palavra-passe no próximo início de sessão** caixa de verificação.<br />6.  Selecione o **palavra-passe nunca expira** caixa de verificação.<br />7.  No **Descrição**, tipo **utilizada como a conta de acesso de rede para o cliente do Configuration Manager de conta de serviço**.|  

###  <a name="InstallSQLServer2008"></a>Passo 1 e 9: Instale o SQL Server 2008 R2  
 Antes de instalar o Configuration Manager, instale o SQL Server 2008 R2 SP1 e CU6.  

> [!NOTE]
>  Para ativar todas as funcionalidades do SQL Server 2008 R2, instale a função de servidor serviços Web (IIS) antes de instalar o SQL Server 2008 R2.  

 **Para instalar o SQL Server 2008 R2**  

1.  Inicie o Centro de instalação do SQL Server.  

2.  No Centro de instalação do servidor de SQL Server, no painel de navegação, clique em **instalação**.  

3.  No painel de pré-visualização, clique em **nova instalação ou adicionar funcionalidades a uma instalação existente**.  

     Inicia o Assistente de configuração do SQL Server 2008 R2.  

4.  Instale o SQL Server 2008 R2 utilizando as informações na tabela 9, aceitar as predefinições, a menos que especificado em contrário.  

    ### <a name="table-9-information-for-installing-sql-server-2008-r2"></a>Tabela 9. Informações para instalar o SQL Server 2008 R2  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Regras de suporte de configuração** |Clique em **OK**.|  
    |**Chave de produto** |Clique em **Seguinte**.|  
    |**Termos de licenciamento** |Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Ficheiros de suporte de configuração** |Clique em **Instalar**.|  
    |**Regras de suporte de configuração** |Certifique-se de que não existem resultados críticos existem para as regras e, em seguida, clique em **seguinte**.|  
    |**Função de configuração** |Clique em **instalação de funcionalidades do SQL Server**e, em seguida, clique em **seguinte**.|  
    |**Seleção de funcionalidades** |1.  Selecione o **serviços de motor de base de dados** caixa de verificação.<br />2.  Selecione o **Reporting Services** caixa de verificação.<br />3.  Selecione o **pesquisa em texto completo** caixa de verificação.<br />4.  Selecione o **ferramentas de gestão - concluir** caixa de verificação.<br />5.  Clique em **Seguinte**.|  
    |**Regras de instalação** |Clique em **Seguinte**.|  
    |**Configuração de instância** |Clique em **Seguinte**.|  
    |**Requisitos de espaço em disco** |Clique em **Seguinte**.|  
    |**Configuração do servidor** |1.  Para **do SQL Server Agent**, na **nome da conta**, tipo **MDT2013\SQLAgent**, na **palavra-passe**, tipo **P@ssw0rd**.<br />2.  Para **motor de base de dados do SQL Server**, na **nome da conta**, tipo **MDT2013\SQLDBEngine**, na **palavra-passe**, tipo **P@ssw0rd**.<br />3.  Para **SQL Server Reporting Services**, na **nome da conta**, tipo **MDT2013\SQLReport**, na **palavra-passe**, tipo **P@ssw0rd**.<br />4.  Clique em **Seguinte**.|  
    |**Configuração do motor de base de dados** |Clique em **adicionar utilizador atual**e, em seguida, clique em **seguinte**.|  
    |**Configuração do Reporting Services** |Clique em **Seguinte**.|  
    |**Relatório de erros** |Clique em **Seguinte**.|  
    |**Regras de configuração de instalação** |Clique em **Seguinte**.|  
    |**Pronto para instalar** |Clique em **Instalar**.|  
    |**Concluir** |Clique em **Fechar**.|  

5.  Feche o Centro de instalação do SQL Server.  

 **Para instalar o SQL Server 2008 R2 SP1**  

1.  No Explorador do Windows, aceda a E:\Source$\SQL2008R2SP1 e faça duplo clique **SQLServer2008R2SP1-KB2528583 x64 ENU.exe**.  

     O **extrair ficheiros** caixa de diálogo mostra o processo de extração de ficheiros. Quando o processo estiver concluído, o SQL Server 2008 R2 Service Pack 1 atualização Assistente de configuração é iniciado.  

2.  Instale o SQL Server 2008 R2 SP1 com as informações na tabela 10, aceitar as predefinições, a menos que especificado em contrário.  

    ### <a name="table-10-information-for-installing-sql-server-2008-r2-sp1"></a>Tabela 10. Informações para instalar o SQL Server 2008 R2 SP1  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Atualização do SQL Server 2008 R2** |Clique em **Seguinte**.|  
    |**Termos de licenciamento** |Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Selecionar funcionalidades** |Clique em **Seguinte**.|  
    |**Verifique os ficheiros em utilização** |Clique em **Seguinte**.|  
    |**Pronto para atualizar** |Clique em **atualização**.|  
    |**Progresso da atualização** |O progresso é apresentado na página do assistente, como a atualização é executada e concluída.|  
    |**Concluir** |Clique em **Fechar**.|  

 **Para instalar o SQL Server 2008 R2 SP1 CU6**  

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

6.  Instale o SQL Server 2008 R2 SP1 CU6 utilizando as informações na tabela 11, aceitar as predefinições, a menos que especificado em contrário.  

    ### <a name="table-11-information-for-installing-sql-server-2008-r2-sp1-cu6"></a>Tabela 11. Informações para instalar o SQL Server 2008 R2 SP1 CU6  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Atualização do SQL Server 2008 R2** |Clique em **Seguinte**.|  
    |**Termos de licenciamento** |Selecione o **aceito os termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Selecionar funcionalidades** |Clique em **Seguinte**.|  
    |**Verifique os ficheiros em utilização** |Clique em **Seguinte**.|  
    |**Pronto para atualizar** |Clique em **atualização**.|  
    |**Progresso da atualização** |O progresso é apresentado na página do assistente, como a atualização é executada e concluída.|  
    |**Concluir** |Clique em **Fechar**.|  

     O **instalar uma atualização do SQL Server 2008 R2** é apresentada a caixa de diálogo que lhe pede para reiniciar o computador para concluir a configuração.  

7.  No **instalar uma atualização do SQL Server 2008 R2** caixa de diálogo, clique em **OK**.  

8.  Reinicie o computador.  

9. Depois de instalar o SQL Server 2008 R2 SP1 CU6, o número de compilação do SQL Server deve ser 10.51.2811.0.  

    > [!TIP]
    >  Pode verificar o número de compilação do SQL Server visualizando as atualizações do SQL Server aplicadas em programas e funcionalidades do painel de controlo item ao clicar em **ver atualizações instaladas**.  

###  <a name="AddtheSiteServertotheAdministratorsSecurityGroup"></a>Passo 1-10: Adicione o servidor de Site para o grupo de segurança de administradores  
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

###  <a name="InstallConfigurationManager"></a>Passo 1-11: Instalar o Configuration Manager  
 Quando os produtos e tecnologias tem sido instaladas, instale o Configuration Manager. Antes disso, no entanto, expanda o esquema do Active Directory para que computadores possam localizar os pontos de distribuição, pontos de localizador de serviço e outras funções de servidor. Além disso, pode expandir o esquema após a instalação do Configuration Manager. Para obter mais informações sobre como expandir o esquema do Active Directory para o Configuration Manager, consulte a secção "Expandir o esquema do Active Directory," na biblioteca de documentação do Configuration Manager, que é instalada com o Configuration Manager.  

 Após expandir o esquema do Active Directory, instale o Configuration Manager. A configuração do MDT-WDG-01 suporta do Configuration Manager para este exemplo. A configuração de computadores na rede de produção pode variar. Para obter mais informações sobre os pré-requisitos para instalar o Configuration Manager, consulte o artigo [configurações suportadas para o Configuration Manager](http://technet.microsoft.com/library/gg682077.aspx).  

 **Para instalar o Configuration Manager**  

1.  Inicie o ecrã inicial de configuração do System Center 2012 R2 Configuration Manager.  

2.  No ecrã inicial configuração do System Center 2012 R2 Configuration Manager, clique o **instalar** ligação.  

     A Microsoft assistente System Center 2012 R2 Configuration Manager a configuração é iniciado.  

3.  Conclua a Microsoft assistente System Center 2012 R2 Configuration Manager configuração utilizar as informações na tabela 12. Aceite as predefinições, a menos que especificado em contrário.  

    ### <a name="table-12-information-for-installing-configuration-manager"></a>A tabela 12. Informações para instalar o Configuration Manager  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Antes de começar** |Clique em **Seguinte**.|  
    |**Introdução** |Clique em **Seguinte**.|  
    |**Chave de produto** |No **introduzir a chave de produto de 25 carateres**, tipo ***product_key*** (onde *product_key* é a chave de produto para o Configuration Manager).|  
    |**Termos de licenciamento de Software da Microsoft** |Selecione o **aceito estes termos de licenciamento** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Atualizar os componentes de pré-requisito** |No **transferir e utilizar as atualizações mais recentes. As atualizações serão guardadas na seguinte localização**, tipo **E:\CMDownloads**e, em seguida, clique em **seguinte**.|  
    |**Seleção de idioma do servidor** |Clique em **Seguinte**.|  
    |**Seleção de idioma do cliente** |Clique em **Seguinte**.|  
    |**Definições de instalação e site** |1.  No **código do Site**, tipo **NYC**.<br />2.  No **nome do Site**, tipo **Nova Iorque cidade Site**.<br />3.  Clique em **Seguinte**.|  
    |**Instalação de Site principal** |1.  Clique em **instalar o site primário como um site autónomo**.<br />2.  Clique em **Seguinte**.<br />     O **do Configuration Manager** aparece a caixa de diálogo, confirmar que pretende que a instalação deste site como um site autónomo.<br />3.  No **do Configuration Manager** caixa de diálogo, clique em **Sim**.|  
    |**Informações de base de dados** |Clique em **Seguinte**.|  
    |**Definições do fornecedor SMS** |Clique em **Seguinte**.|  
    |**Definições de comunicação do computador cliente** |Clique em **configurar o método de comunicação em cada função do sistema de sites**e, em seguida, clique em **seguinte**.|  
    |**Funções do sistema de sites** |Clique em **Seguinte**.|  
    |**Configuração do programa de melhoramento de experiência de cliente** |Selecione a participação no programa de melhoramento da experiência do cliente para a sua organização adequada e, em seguida, clique em **seguinte**.|  
    |**Resumo de definições** |Clique em **Seguinte**.|  
    |**Verificação de pré-requisitos** |Clique em **Iniciar instalação**.|  
    |**Instalar** |Monitorizar o processo de instalação até que esteja concluída e, em seguida, clique em **fechar**.|  

4.  Feche todas as janelas abertas e caixas de diálogo.  

 Quando o assistente estiver concluído, o Configuration Manager está instalado.  

###  <a name="ConfiguretheNetworkAccessAccount"></a>Passo 1-12: Configurar a conta de acesso de rede  
 O cliente do Configuration Manager necessita de uma conta para fornecer credenciais quando aceder a pontos de distribuição do Configuration Manager, partilhas de implementação do MDT e pastas partilhadas. Esta conta é denominada o *conta de acesso à rede*. A conta de CMNetAccess foi criada anteriormente no processo para utilizar como a conta de acesso à rede.  

 **Para configurar a conta de acesso à rede**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, vá para o Site/descrição geral da configuração/Sites.  

4.  No painel de pré-visualização, clique em **NYC - Nova Iorque cidade Site**.  

5.  No Friso, clique em **definições**, clique em **configurar componentes do Site**e, em seguida, clique em **distribuição de Software**.  

6.  No **propriedades distribuição de Software** caixa de diálogo, clique em de **conta de acesso à rede** separador.  

7.  No **conta de acesso à rede**, clique em **especifique a conta que aceder a localizações de rede**, clique em **definir**e, em seguida, clique em **nova conta**.  

     O **conta de utilizador do Windows** é apresentada a caixa de diálogo.  

8.  Concluir o **conta de utilizador do Windows** caixa de diálogo com as informações na tabela 13 e, em seguida, clique em **OK**.  

    ### <a name="table-13-information-required-to-complete-the-windows-user-account-dialog-box"></a>Tabela 13. Informações necessárias para concluir a caixa de diálogo de conta de utilizador do Windows  

    |**Para este** |**Fazê-lo** |  
    |-|-|  
    |**Nome de utilizador** |Tipo **MDT2013\CMNetAccess**.|  
    |**Palavra-passe** |Tipo **P@ssw0rd**.|  
    |**Confirmar palavra-passe** |Tipo **P@ssw0rd**.|  

9. No **propriedades distribuição de Software** caixa de diálogo, clique em **OK**.  

10. Feche as janelas abertas.  

###  <a name="ConfiguretheConfigurationManagerSiteBoundaries"></a>Passo 1-13: Configurar os limites de Site do Configuration Manager e os grupos de limites  
 O cliente do Configuration Manager tem de conhecer os limites para o site. A menos que sejam especificados limites do site, o cliente assume que o computador com o Configuration Manager num site remoto. Adicione que um limite de site com base na sub-rede IP que WDG-MDT-01, WDG-REF-01 e utilize WDG-CLI-01. Em seguida, adicione o limite de site para um grupo de limites de site.  

 **Para criar um limite de site do Configuration Manager**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, aceda a hierarquia de descrição geral/configuração/limites.  

4.  No Friso, clique em **criar limites**.  

     O **criar limites** é aberta a caixa de diálogo.  

5.  Concluir o **criar limites** caixa de diálogo com as informações na tabela 14 e, em seguida, clique em **OK**.  

    > [!NOTE]
    >  Para este exemplo, o limite de site é especificado por endereço de rede. No entanto, também pode especificar limites de site utilizando do AD DS sites nome ou um intervalo de endereços IP.  

    ### <a name="table-14-information-required-to-complete-the-create-boundary-dialog-box"></a>Tabela 14. Informações necessárias para concluir a criar a caixa de diálogo de limites  

    |**Para este** |**Fazê-lo** |  
    |-|-|  
    |**Descrição** |Tipo **limite de sub-rede IP**.|  
    |**Tipo** |Selecione **sub-rede IP**.|  
    |Rede|Tipo ***network_address*** (onde *network_address* é o endereço de rede da sub-rede de onde os computadores estão instalados).|  
    |**Máscara de sub-rede** |Tipo ***subnet_mask*** (onde *subnet_mask* é a máscara de sub-rede da sub-rede de onde os computadores estão instalados).|  

 **Para adicionar o limite de site do Configuration Manager a um grupo de limites de site**  

1.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

2.  Na área de trabalho administração, aceda a grupos de configuração/limites de descrição geral/hierarquia.  

3.  No Friso, clique em **criar grupo de limites**.  

     O **criar grupo de limites** é aberta a caixa de diálogo.  

4.  Concluir o **geral** separador do **criar grupo de limites** caixa de diálogo com as informações na tabela 15.  

    ### <a name="table-arabic-15-information-required-to-complete-the-general-tab-of-the-create-boundary-group-dialog-box"></a>Tabela ARABIC 15. Informações necessárias para concluir o separador Geral da criar a caixa de diálogo de grupo de limites  

    |**Para este** |**Fazê-lo** |  
    |-|-|  
    |**Nome** |Tipo **grupo de limites de Nova Iorque Cidade**.|  
    |Descrição|Tipo **grupo de limites para os limites de site no site de Nova Iorque Cidade**.|  
    |**Limites** |1.  Clique em **Adicionar**.<br />     O **adicionar limites** é apresentada a caixa de diálogo.<br />2.  No **adicionar limites** caixa de diálogo, selecione ***site_boundary*** (onde *site_boundary* é o limite de site que criou anteriormente no processo) e, em seguida, clique em **OK**.<br />     O limite de site é apresentado na lista de limites.|  

5.  Concluir o **referências** separador do **criar grupo de limites** caixa de diálogo com as informações na tabela 16 e, em seguida, clique em **OK**.  

    ### <a name="table-16-information-required-to-complete-the-references-tab-of-the-create-boundary-group-dialog-box"></a>Tabela 16. Informações necessárias para concluir o separador de referências do criar caixa de diálogo de grupo de limites  

    |**Para este** |**Fazê-lo** |  
    |-|-|  
    |**Atribuição de site** |Selecione o **utilizar este grupo de limites para atribuição de site** caixa de verificação.|  
    |**Localização de conteúdo** |1.  Clique em **Adicionar**.<br />     O **adicionar sistemas de sites** é apresentada a caixa de diálogo.<br />2.  No **adicionar sistemas de sites** caixa de diálogo, selecione  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     O servidor de sistema de sites é apresentado na lista de servidores do sistema de sites.|  

6.  Feche as janelas abertas.  

###  <a name="ConfigurethePublishingofSiteIntofrmation"></a>Passo 1-14: Configurar a publicação de informações do Site no AD DS e DNS  
 O cliente do Configuration Manager tem de localizar as várias funções de servidor do Configuration Manager. Modificar as propriedades do site para publicar as informações do site no AD DS e no DNS.  

 **Para configurar a publicação de informações do site no AD DS e no DNS**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, vá para o Site/descrição geral da configuração/Sites.  

4.  No painel de pré-visualização, clique em **NYC - Nova Iorque cidade Site**.  

5.  No Friso, clique em **propriedades**.  

6.  No **propriedades do Site de Nova Iorque Cidade** caixa de diálogo a **publicação** separador, certifique-se de que o **mdt2013.corp.woodgrovebank.com** floresta do Active Directory estiver listada, e em seguida, clique em **Cancelar**.  

7.  Feche as janelas abertas.  

###  <a name="ConfigureDiscoveryofActiveDirectoryUsers"></a>Passo 1-15: Configurar a deteção de utilizadores do Active Directory  
 Em alguns casos, o software será implementado para coleções de utilizadores que o Configuration Manager Deteta. O Configuration Manager pode contas de utilizador de deteção armazenadas no AD DS utilizando o método de deteção de utilizador do Active Directory.  

 **Para configurar a deteção de utilizadores do Active Directory**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **administração**.  

3.  Na área de trabalho administração, aceda à hierarquia/descrição geral/deteção métodos.  

4.  No painel de pré-visualização, clique em **deteção de utilizador do Active Directory**.  

5.  No Friso, no **home page** separador, clique em **propriedades**.  

     O **propriedades de deteção de utilizador do Active Directory** é apresentada a caixa de diálogo.  

6.  No **propriedades de deteção de utilizador do Active Directory** caixa de diálogo a **geral** separador, execute os seguintes passos:  

    1.  Selecione o **ativar a deteção de utilizador do Active Directory** caixa de verificação.  

    2.  No **contentores do Active Directory**, clique em **novo**.  

         O **novo contentor do Active Directory** é apresentada a caixa de diálogo.  

    3.  No **novo contentor do Active Directory** caixa de diálogo **caminho**, clique em **procurar**.  

         O **selecionar novo contentor** é apresentada a caixa de diálogo.  

    4.  No **selecionar novo contentor** caixa de diálogo, clique em **mdt2013**e, em seguida, clique em **OK**.  

         No **novo contentor do Active Directory** caixa de diálogo, o caminho de acesso protocolo LDAP (Lightweight Directory) é apresentado no **caminho** caixa.  

    5.  No **novo contentor do Active Directory** caixa de diálogo, clique em OK.  

     O caminho LDAP, é apresentado no **contentores do Active Directory** caixa de listagem.  

7.  No **propriedades de deteção de utilizador do Active Directory** caixa de diálogo, clique em **OK**.  

     O **do Configuration Manager** caixa de diálogo for apresentada, consulta que pretende executar a deteção logo que possível.  

8.  No **do Configuration Manager** caixa de diálogo, clique em **Sim**.  

9. Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

10. Em recursos e compatibilidade área de trabalho, aceda à descrição geral/utilizadores.  

     A lista de utilizadores detetados no AD DS é apresentada no painel de pré-visualização.  

11. Feche as janelas abertas.  

##  <a name="PreparetheMDTEnvironment"></a>Passo 2: Preparar o ambiente do MDT  
 É o primeiro passo no processo de implementação para preparar o ambiente do MDT. Quando estiver concluído este passo, pode criar o computador de referência e implementar uma imagem capturada do mesmo no computador de destino (WDG-CLI-01) através da integração do Configuration Manager com o MDT.  

 Prepare o ambiente do MDT por:  

-   Instalar o MDT conforme descrito em [passo 1 de 2: Instale o MDT](#InstallMDT)  

-   Ativar a integração da consola do Configuration Manager ao executar o Assistente de configurar a integração do ConfigMgr, conforme descrito em [passo 2 de 2: Ativar a integração da consola do Configuration Manager](#EnableConfigurationManagerConsoleIntegration)  

###  <a name="InstallMDT"></a>Passo 1 de 2: Instale o MDT  
 Para instalar o MDT, conclua os seguintes passos:  

1.  No Explorador do Windows, aceda a E:\Source$\MDT_2013.  

2.  Faça duplo clique em **MicrosoftDeploymentToolkit2013_x64.msi** (para sistemas operativos de 64 bits) ou **MicrosoftDeploymentToolkit2013_x86.msi** (para sistemas de operativos de 32 bits) e, em seguida, clique em **Instalar**.  

     Inicia o Assistente de configuração do Microsoft implementação Toolkit 2013.  

3.  Conclua a implementação Toolkit 2013 Assistente de configuração Microsoft utilizando as informações na tabela 17. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-17-information-for-completing-the-microsoft-deployment-toolkit-2013-setup-wizard"></a>Tabela 17. Informações para concluir o Assistente de configuração do Microsoft Deployment Toolkit 2013  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Bem-vindo ao Microsoft Deployment Toolkit Assistente de configuração de 2013** |Clique em **Seguinte**.|  
    |**Contrato de licença de utilizador final** |Clique em **aceito os termos no contrato de licença**e, em seguida, clique em **seguinte**.|  
    |**Configuração personalizada** |Clique em **Seguinte**.|  
    |**Pronto para instalar o Microsoft implementação Toolkit de 2013** |Clique em **Instalar**.|  
    |**Instalar o Microsoft Deployment Toolkit 2013** |É apresentado o progresso da instalação do MDT.|  
    |**Concluir o Assistente de configuração do Microsoft Deployment Toolkit 2013** |Clique em **Concluir**.|  

 Concluído o Assistente de configuração do Microsoft implementação Toolkit 2013 e instalação do MDT no WDG-MDT-01.  

###  <a name="EnableConfigurationManagerConsoleIntegration"></a>Passo 2 de 2: Ativar a integração da consola do Configuration Manager  
 Antes de poder utilizar as funcionalidades de integração do Gestor de configuração do MDT, execute o Assistente de configurar a integração do ConfigMgr. Este assistente copia os ficheiros de integração adequado para a pasta na qual o Configuration Manager está instalado. O assistente também adiciona classes Windows Management Instrumentation (WMI) para as novas ações personalizadas do MDT. As classes são adicionadas ao compilar um novo ficheiro de formato de objeto gerido (. mof), que contém as novas definições de classe.  

 **Para ativar a integração da consola do Configuration Manager**  

> [!NOTE]
>  Certifique-se de que a consola do Configuration Manager está fechada ao efetuar estes passos.  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **configurar a integração do ConfigMgr**.  

     Inicia o Assistente para configurar a integração do ConfigMgr.  

2.  Conclua o Assistente de integração de ConfigMgr configurar utilizando as informações na tabela 18. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-18-information-for-completing-the-configure-configmgr-integration-wizard"></a>Tabela 18. Informações para concluir a configurar o Assistente de integração do ConfigMgr  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Opções** |1.  Certifique-se de que o **instalar as extensões de consola do MDT para o ConfigMgr 2012** caixa de verificação está selecionada.<br />2.  Certifique-se de que o **adicionar as ações de sequência de tarefas do MDT para um servidor do ConfigMgr** caixa de verificação está selecionada.<br />3.  No **nome do servidor de Site**, certifique-se de que o valor é **WDG-MDT-01.mdt2013.corp.woodgrovebank.com**.<br />4.  No **código do Site**, certifique-se de que o valor é **NYC**.<br />5.  Clique em **Seguinte**.|  
    |**Confirmação** |Clique em **Concluir**.|  

 Concluído o Assistente para configurar a integração do ConfigMgr e o MDT é integrado com o Configuration Manager.  

## <a name="step-3-create-and-configure-a-task-sequence-to-create-a-reference-computer"></a>Passo 3: Criar e configurar uma sequência de tarefas para criar um computador de referência  
 Quando preparar o ambiente do MDT, crie o computador de referência. O computador de referência é o modelo para implementar novas imagens em computadores de destino. Configure este computador (WDG-REF-01) exatamente como irá configurar os computadores de destino. Em seguida, irá capturar uma imagem do computador de referência e implementar a imagem nos computadores de destino.  

 Criar o computador de referência, WDG-REF-01, por:  

-   Criar uma sequência de tarefas para implementar o Windows 8.1 para o computador de referência, tal como descrito no MDT [passo 1 de 3: Criar uma sequência de tarefas do MDT para implementar o computador de referência](#CreateMDTTaskSequenceforDeployingReferenceComputer)  

-   Selecionar os pontos de distribuição para os novos pacotes e imagens que o assistente criar MDT tarefas sequência cria conforme descrito em [passo 2 de 3: Selecione os pontos de distribuição para os novos pacotes e a imagens](#SelectDistributionPointsfortheNewPackages)  

-   Adicionar os controladores de dispositivo necessários para um novo pacote de unidade e para as imagens de arranque apropriado, conforme descrito em [passo 3 de 3: Adicionar os controladores de dispositivo necessários](#AddtheNecessaryDeviceDrivers)  

-   Ativar a monitorização do processo de implementação MDT, conforme descrito em [passo 3-4: Ativar a implementação do MDT monitorização de processos](#EnableMDTDeploymentProcessMonitoring)  

-   Configurar os ficheiros de configuração do MDT para o computador de referência — especificamente, o ficheiro CustomSettings.ini, conforme descrito em [passo 3-5: Personalizar os ficheiros de configuração do MDT para o computador de referência](#CustomizeMDTConfigFilesforReferenceComputer)  

-   Atualizar os pontos de distribuição do Configuration Manager para o pacote de ficheiros de definições personalizadas, conforme descrito em [passo 3 a 6: Atualizar os pontos de distribuição para o pacote de ficheiros de definições personalizadas](#UpdateDistributionPointsforCustomSettings)  

-   Personalizar a sequência de tarefas para o computador de referência, conforme descrito em [passo 3-7: Personalizar a sequência de tarefas para o computador de referência](#CustomizeTaskSequenceforReferenceComputer)  

###  <a name="CreateMDTTaskSequenceforDeployingReferenceComputer"></a>Passo 1 de 3: Criar uma sequência de tarefas do MDT para implementar o computador de referência  
 Utilize o Assistente de criação MDT tarefas sequência na consola do Configuration Manager para criar sequências de tarefas no Configuration Manager que estão integradas com o MDT. MDT inclui o modelo de sequência de tarefas de cliente padrão, que pode utilizar para implementar o computador de referência.  

 Assistente de criação MDT tarefas sequência substitui os pacotes e imagens selecionadas para os marcadores de posição nos modelos de sequência de tarefas. Depois de concluir o assistente, a nova sequência de tarefas referencia o pacotes adequados e imagens.  

> [!NOTE]
>  Utilize sempre o Assistente de criação MDT tarefas sequência para criar sequências de tarefas com base nos modelos de sequência de tarefas de MDT. Embora pode importar manualmente os modelos de sequência de tarefas, a Microsoft não recomenda este processo.  

 **Para criar uma sequência de tarefas para implementar o computador de referência**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **sequências de tarefas** , clique em **criar sequência de tarefas do MDT**.  

     Inicia o Assistente de criação MDT tarefas sequência.  

5.  Conclua o Assistente de criação MDT tarefas sequência utilizando as informações na tabela 19. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-19-information-for-completing-the-create-mdt-task-sequence-wizard"></a>Tabela 19. Informações para concluir o Assistente de criação MDT tarefas sequência  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Escolha o modelo** |Selecione **sequência de tarefas de cliente**e, em seguida, clique em **seguinte**.|  
    |**Escolha o modelo: Geral** |1.  No **nome da sequência de tarefas**, tipo **implementação de referência do Windows 8.1**.<br />2.  No **comentários de sequência de tarefas**, tipo **sequência para implementar o Windows 8.1 para o computador de referência (WDG-REF-01) de tarefas**e, em seguida, clique em **seguinte**.|  
    |**Escolha o modelo: Detalhes** |1.  Clique em **aderir a um grupo de trabalho**.<br />2.  No **Workgroup**, tipo **WORKGROUP**.<br />3.  No **nome de utilizador**, tipo **Woodgrove Bank empregado**.<br />4.  No **nome da organização**, tipo **Banco Woodgrove**.<br />5.  No **chave de produto**, tipo ***product_key*** (onde *product_key* é a chave de produto para Windows 8.1).<br />6.  Clique em **Seguinte**.|  
    |**Escolha o modelo: Capturar definições** |<ol><li>Clique em **esta sequência de tarefas pode ser utilizada para capturar e imagem**.</li><li>No **captura destino**, tipo  **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**.</li><li>No **conta para captura**, clique em **definir**.</li><li>Concluir o **conta de utilizador do Windows** caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome de utilizador**, tipo **MDT2013\Administrator**.</li><li>No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.</li></ol></li><li>Clique em **OK**.</li><li>Clique em **Seguinte**.</li></ol>|  
    |**Imagem de arranque** |1.  Clique em **criar um novo pacote de imagem de arranque**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\WINPE_Custom**e, em seguida, clique em **seguinte**.|  
    |**Imagem de arranque: Definições gerais** |1.  No **nome**, tipo **personalizada do Windows PE**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **personalizado versão do Windows PE para serem utilizados na implementação de computadores de referência e de destino**e, em seguida, clique em **seguinte**.|  
    |**Imagem de arranque: Opções** |Em **plataforma**, clique em **x64**e, em seguida, clique em **seguinte**.|  
    |**Imagem de arranque: Componentes** |Clique em **Seguinte**.|  
    |**Imagem de arranque: Personalização** |Clique em **Seguinte**.|  
    |**Pacote de MDT** |1.  Clique em **criar um novo pacote de ficheiros de Toolkit do Microsoft implementação**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\MDT_Files**e, em seguida, clique em **seguinte**.|  
    |**MDT pacote: Detalhes do MDT** |1.  No **nome**, tipo **ficheiros MDT**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **fornece acesso aos ficheiros do MDT durante o processo de implementação do Configuration Manager**e, em seguida, clique em **seguinte**.|  
    |**Imagem do SO** |1.  Clique em **pacote de instalação de criar um novo SO**.<br />2.  No **localização de pasta de instalação do SO**, tipo  **\\\WDG-MDT-01\Source$\Windows_8-1**.<br />3.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\Windows_8-1**e, em seguida, clique em **seguinte**.|  
    |**Imagem do SO: Detalhes da imagem** |1.  No **nome**, tipo **Windows 8.1**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **utilizada para implementar em computadores de referência de pacote de Windows 8.1**e, em seguida, clique em **seguinte**.|  
    |**Método de implementação** |Clique em **Seguinte**.|  
    |**Pacote de cliente** |Clique em **criar um novo pacote de cliente do ConfigMgr**e, em seguida, clique em **seguinte**.|  
    |**Pacote USMT** |1.  Clique em **criar um novo pacote USMT**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\USMT**e, em seguida, clique em **seguinte**.|  
    |**Pacote do USMT: Detalhes do USMT** |1.  No **nome**, tipo **USMT**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **ficheiros da USMT utilizados para capturar e restaurar informações de migração de estado de utilizador**e, em seguida, clique em **seguinte**.|  
    |**Pacote de definições** |1.  Clique em **criar um novo pacote de definições**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\CustomSettings_Reference**e, em seguida, clique em **seguinte**.|  
    |**Pacote de definições: Detalhes de definições** |1.  No **nome**, tipo **definições personalizadas do MDT referência computador**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **definições de configuração para o processo de implementação do MDT (por exemplo, CustomSettings.ini) para o computador de referência**e, em seguida, clique em **seguinte**.|  
    |**Pacote Sysprep** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |É apresentado o progresso da criação de sequência de tarefas.|  
    |**Confirmação** |Clique em **Concluir**.|  

 A nova sequência de tarefas é apresentado no painel de pré-visualização.  

###  <a name="SelectDistributionPointsfortheNewPackages"></a>Passo 3-2: Selecione os pontos de distribuição para os novos pacotes e a imagens  
 Assistente de criação MDT tarefas sequência cria um número de pacotes e imagens. Depois destes pacotes e imagens são criadas, selecione os pontos de distribuição a partir da qual as imagens e o pacote será copiado e disponíveis para computadores de destino.  

> [!NOTE]
>  Neste exemplo, não há apenas um ponto de distribuição (WDG-MDT-01). No entanto, a maioria das redes de produção tem vários pontos de distribuição. Quando executar este passo num ambiente de produção, selecione os pontos de distribuição apropriados para a rede.  

 **Para selecionar os pontos de distribuição para pacotes de distribuição de software**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de visualização, selecione **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo utilizando as informações no 20. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-20-information-for-completing-the-distribute-content-wizard"></a>A tabela 20. Informações para concluir a distribuir o conteúdo Assistente  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |Clique em **Seguinte**.|  
    |**Gerais: Conteúdo** |Clique em **Seguinte**.|  
    |**Gerais: Destino do conteúdo** |1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDGMDT01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso da distribuição de software é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="AddtheNecessaryDeviceDrivers"></a>Passo 3 de 3: Adicionar os controladores de dispositivo necessários  
 Quando tiver sido criada a sequência de tarefas do MDT, adicione os controladores de dispositivo necessários para o computador de referência (WDG-REF-01) para a imagem de arranque do Windows PE e a imagem do Windows 8.1. Adicione os controladores de dispositivo no nó de controladores na consola do Configuration Manager. Criar um pacote que contém os controladores de dispositivo e inserir os controladores numa imagem do Windows PE personalizada criada anteriormente no processo.  

 Depois de criar o pacote que contém os controladores de dispositivo, selecione a distribuição de ponto no qual o pacote será implementado.  

 **Para adicionar os controladores de dispositivo necessários**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda à descrição geral/operativo sistemas/controladores.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar controlador**.  

     O novo Assistente para importar controlador é iniciado.  

5.  Conclua o novo Assistente para importar controlador utilizando as informações na tabela 21. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-21-information-for-completing-the-import-new-driver-wizard"></a>Tabela 21. Informações para concluir o novo Assistente para importar controlador  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Localizar controlador** |**Na pasta de origem**, tipo  **\\\WDG-MDT-01\Source$\Drivers**e, em seguida, clique em **seguinte**.|  
    |**Localize os controladores: Detalhes do controlador** |Clique em **Seguinte**.|  
    |**Localize os controladores: Adicionar controladores ao pacote** |<ol><li>Clique em **novo pacote**.</li><li>Concluir o **novo pacote de controladores** caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome**, tipo ***device_driver_name*** **pacote** (onde *device_driver_name* é um nome descritivo para os controladores de dispositivo).</li><li>No **comentário**, tipo **controladores de dispositivo que são necessários para os computadores de referência e de destino**.</li></ol></li><li>No **origem do pacote de controlador**, tipo  **\\\WDG-MDT-01\Packages$\Drivers**e, em seguida, clique em **OK**.</li><li>Clique em **Seguinte**.</li></ol>|  
    |**Localize os controladores: Adicionar controlador a imagens de arranque** |1.  Na lista de imagens, selecione o **personalizada do Windows PE** caixa de verificação.<br />2.  Selecione o **atualizar pontos de distribuição após concluir** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para importar os controladores de dispositivo é apresentado.|  
    |**Confirmação** |Clique em **Fechar**.|  

 **Para selecionar os pontos de distribuição para o pacote de controladores**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda a descrição geral/operativo sistemas/a pacotes de controladores.  

4.  No painel de pré-visualização, clique em ***device_driver_name*** **pacote** (onde *device_driver_name* é um nome descritivo para os controladores de dispositivo).  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo utilizando as informações na tabela 22. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-22-information-for-completing-the-distribute-content-wizard"></a>Tabela 22. Informações para concluir a distribuir o conteúdo Assistente  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |Clique em **Seguinte**.|  
    |**Gerais: Conteúdo** |Clique em **Seguinte**.|  
    |**Gerais: Destino do conteúdo** |1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso da distribuição de software é apresentado.|  
    |Conclusão|Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="EnableMDTDeploymentProcessMonitoring"></a>Passo 3-4: Ativar a implementação do MDT monitorização de processos  
 Antes de implementar o computador de referência (WDG-REF-01) com os dados de arranque de sequências de tarefas, ative a monitorização de MDT do processo de implementação de ZTI. Ativar a monitorização de **monitorização** separador na partilha de implementação **propriedades** caixa de diálogo. Posteriormente no processo, irá monitorizar o processo de implementação de ZTI utilizando Deployment Workbench ou **Get-MDTMonitorData** cmdlet.  

 **Para ativar a monitorização do processo de implementação de ZTI do MDT**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação de Workbench/implementação.  

3.  No painel ações, **clique novas partilhas de implementação**.  

     Inicia o Assistente de nova partilha de implementação.  

4.  Conclua o Assistente de partilha de implementação novo utilizando as informações na tabela 23.  

    ### <a name="table-23-information-for-completing-the-new-deployment-share-wizard"></a>Tabela 23. Informações para concluir o Assistente de nova partilha de implementação  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Caminho** |**No caminho de partilha de implementação**, tipo **C:\DeploymentShare$** e, em seguida, clique em **seguinte**.|  
    |**Partilha** |Clique em **Seguinte**.|  
    |**Nome descritivo** |Clique em **Seguinte**.|  
    |**Opções** |Clique em **Seguinte**.|  
    |**Resumo** |Clique em **Seguinte**.|  
    |**Progresso** |O progresso para criar a partilha de implementação é apresentado.|  
    |**Confirmação** |Clique em Concluir.|  

     Depois de concluída as implementação Assistente de nova partilha e a nova partilha de implementação — partilha de implementação MDT (C:\DeploymentShare$)—appears no painel de detalhes.  

5.  No painel de detalhes, clique em **partilha de implementação do MDT (C:\DeploymentShare$)**.  

6.  No painel ações, clique em propriedades.  

     O **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** é aberta a caixa de diálogo.  

7.  No **propriedades de partilha de implementação MDT (C:\DeploymentShare$)** caixa de diálogo a **monitorização** separador, selecione o **ativar a monitorização para esta partilha de implementação** caixa de verificação e, em seguida, clique em **aplicar**.  

8.  No **propriedades de partilha de implementação do MDT (C:\DeploymentShare$)** caixa de diálogo a **regras** separador, tenha em atenção que o **EventService** propriedade foi adicionada para o Ficheiro CustomSettings.ini e, em seguida, clique em **OK**.  

     O **EventService** propriedade é o seguinte:  

    ```  
    EventService=http://WDG-MDT-01:9800  
    ```  

9. Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizeMDTConfigFilesforReferenceComputer"></a>Passo 3-5: Personalizar os ficheiros de configuração do MDT para o computador de referência  
 Quando tiver sido criada a sequência de tarefas do MDT, personalize os ficheiros de configuração do MDT que fornecem as definições de configuração para a implementação do Windows 8.1 para o computador de destino. Especificamente, personalize o ficheiro CustomSettings.ini.  

 Quando a personalização do ficheiro CustomSettings.ini estiver concluída, guarde ficheiros atualizados para a pasta de origem para o pacote de definições personalizadas do MDT referência computador criado anteriormente no processo (E:\Packages$\CustomSettings_Reference). Em seguida, adicione o **DoCapture** e **EventService** propriedades e valores correspondentes para o CustomSettings.ini do ficheiro para que o processo de implementação do MDT captura uma imagem das (do computador de referência WDG-REF-01) após a implementação do Windows 8.1.  

 **Para personalizar os ficheiros de configuração do MDT para o computador de referência**  

1.  No Explorador do Windows, aceda ao E:\Packages$\CustomSettings_Reference e, em seguida, faça duplo clique em **CustomSettings.ini**.  

2.  Abra o Microsoft Notepad e, em seguida, adicione as seguintes linhas ao fim do ficheiro CustomSettings.ini, conforme mostrado na listagem 1:  

    ```  
    DoCapture=YES  
    EventService=http://WDG-MDT-01:9800  
    ```  

    > [!NOTE]
    >  Certifique-se de que remova quaisquer definições adicionais que não são apresentadas na listagem 1.  

     **Listar 1. Ficheiro CustomSettings.ini depois de adicionar a propriedade DoCapture**  

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

3.  Guarde o ficheiro e, em seguida, saia bloco de notas.  

###  <a name="UpdateDistributionPointsforCustomSettings"></a>Passo 3 a 6: Atualizar os pontos de distribuição para o pacote de ficheiros de definições personalizadas  
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

###  <a name="CustomizeTaskSequenceforReferenceComputer"></a>Passo 3-7: Personalizar a sequência de tarefas para o computador de referência  
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

8.  No **propriedades** separador **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**e, em seguida, clique em **aplicar** .  

9. Efetue quaisquer modificações adicionais para a sequência de tarefas que requer que o ambiente e, em seguida, clique em **OK**.  

10. Feche todas as janelas abertas e caixas de diálogo.  

## <a name="step-4-deploy-windows-81-and-capture-an-image-of-the-reference-computer"></a>Passo 4: Implementar o Windows 8.1 e capturar uma imagem do computador de referência  
 Quando tiver criado a sequência de tarefas para implementar o Windows 8.1 para o computador de referência e capturar uma imagem do computador de referência, inicie a sequência de tarefas. Crie a captura de sistema operativo utilizando o Assistente de suporte de dados de sequência de tarefas na consola do Configuration Manager.  

 Implementar o Windows 8.1 e capturar uma imagem do computador de referência por:  

-   Adicionar o computador de referência para a base de dados do site do Configuration Manager, conforme descrito em [passo 4-1: Adicionar o computador de referência para a base de dados do Site do Configuration Manager](#AddReferenceComputertoConfigurationManagerSite)  

-   Criar uma coleção que contenha o computador de referência que acabou de adicionar conforme descrito em [passo 4-2: Criar uma coleção que contenha o computador de referência](#CreateCollectionthatContainsReferenceComputer)  

-   Implemente a sequência de tarefas do computador de referência, conforme descrito em [passo 4-3: Implementar a sequência de tarefas do computador de referência](#DeployReferenceComputerTaskSequence)  

-   Utilizar o Assistente de suporte de dados de sequência de tarefas para criar uma sequência de tarefas com suportes de dados em disco conforme descrito em [passo 4-4: Criar tarefas sequência suportes de dados](#CreateTaskSequenceBootableMedia)  

-   A iniciar o computador de referência com a sequência de tarefas com suportes de dados em disco conforme descrito em [passo 4-5: Iniciar o computador de referência com o suporte de suportes de sequência de tarefas](#StartReferenceComputerwithTaskSequenceBootableMedia)  

###  <a name="AddReferenceComputertoConfigurationManagerSite"></a>Passo 4-1: Adicionar o computador de referência para a base de dados do Site do Configuration Manager  
 Para implementar um sistema operativo sem suporte de dados autónomo para um novo computador que o Configuration Manager não gerir atualmente, adicione o novo computador para a base de dados do site do Configuration Manager antes de iniciar o processo de implementação do sistema operativo. O Configuration Manager pode detetar automaticamente computadores na rede que tenha um sistema de operativo de Windows instalado. No entanto, se o computador não tiver nenhum sistema operativo instalado, utilize o Assistente para importar informações de computador para importar as informações do computador novo.  

 **Para adicionar o computador de referência para a base de dados do site do Configuration Manager**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda à descrição geral/dispositivos.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar informações sobre o computador**.  

     O Assistente Importar informações o computador é iniciado.  

5.  Conclua o Assistente de importação de informações de computador, utilizando as informações nas 24. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-24-information-for-completing-import-computer-information-wizard"></a>Tabela 24. Informações para concluir o Assistente de importação de informações de computador  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Selecione a origem** |Clique em **importar computador individual**e, em seguida, clique em **seguinte**.|  
    |Selecione a origem: Único computador|1.  No **nome do computador**, tipo **WDG-REF-01**.<br />2.  No **endereço MAC**, tipo ***mac_address*** (onde *mac_address* é o controlo [MAC] endereço do adaptador de rede principal para o computador de referência, o media access WDG-REF-01).<br />3.  Clique em **Seguinte**.|  
    |**Selecione a origem: Pré-visualização de dados** |Clique em **Seguinte**.|  
    |**Selecione a origem: Escolher coleção de destino** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para importar o computador é apresentado.|  
    |**Confirmação** |Clique em **Fechar**.|  

 Para obter mais informações sobre como adicionar um novo computador para a base de dados do site do Configuration Manager, consulte a secção "para importar informações sobre o computador para um único computador," na secção, "Como para implementar sistemas operativos no Configuration Manager," na configuração Biblioteca de documentação Manager, que é instalado com o Configuration Manager.  

###  <a name="CreateCollectionthatContainsReferenceComputer"></a>Passo 4-2: Criar uma coleção que contenha o computador de referência  
 Na consola do Configuration Manager, crie uma coleção que inclua o computador de referência (WDG-REF-01). Esta coleção de computadores é utilizada mais tarde, quando a sequência de tarefas de publicidade criado anteriormente no processo.  

 **Para criar uma coleção que inclui o computador de referência**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda a coleções de dispositivos/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar**e, em seguida, clique em **criar coleção de dispositivos**.  

     Inicia o Assistente para criar coleção de dispositivos.  

5.  Conclua o Assistente de coleção de dispositivos criar utilizando as informações na tabela 25. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-25-information-for-completing-the-create-device-collection-wizard"></a>Tabela 25. Informações para concluir o Assistente de coleção de dispositivos de criação  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |<ol><li>No **nome**, tipo **Microsoft Deployment – o computador de referência**.</li><li>No **comentário**, tipo **computador que está a ser o computador de referência para os computadores de destino a ser implementado**.</li><li>No **coleção limitado**, clique em **procurar**.<br /><br />     O **selecionar coleção** é apresentada a caixa de diálogo. Conclua a caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **nome**, clique em **todos os sistemas**.</li><li>Clique em **OK**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Regras de Associação** |<ol><li>Clique em **Adicionar regra**e, em seguida, clique em **regra direta**.<br /><br />     O direto associação Assistente para criar regra é iniciado.</li><li>Conclua o direta associação Assistente para criar regra, efetuando os seguintes passos:<br /><br /> <ol><li>Na página de **Boas-vindas**, clique em **Seguinte**.</li><li>No **procurar recursos** na página **classe de recursos**, selecione **recurso do sistema**; na **nome de atributo**, selecione  **Nome**; na **valor**, tipo **WDG-REF-01**; e, em seguida, clique em **seguinte**.</li><li>No **selecionar recursos** página, selecione **WDG-REF-01**e, em seguida, clique em **seguinte**.</li><li>No **resumo** página, clique em **seguinte**.</li><li>No **progresso** página, ver o progresso para criar a nova regra de associação.</li><li>No **conclusão** página, clique em **fechar**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para criar a coleção de dispositivos é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para criar coleções no Configuration Manager," na biblioteca de documentação do Configuration Manager, que é instalado com o Configuration Manager.  

###  <a name="DeployReferenceComputerTaskSequence"></a>Passo 4-3: Implementar a sequência de tarefas do computador de referência  
 Na consola do Configuration Manager, implemente a sequência de tarefas que criou anteriormente no processo para a coleção de dispositivos que inclui o computador de referência criado anteriormente no processo.  

 **Para implementar a sequência de tarefas**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **implementação de referência do Windows 8.1**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **implementar**.  

     Inicia o Assistente de implementação de Software.  

6.  Conclua o Assistente para implementar Software utilizando as informações na tabela 26. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-arabic-26-information-for-completing-the-deploy-software-wizard"></a>Tabela de ARABIC 26. Informações para concluir o Assistente de implementação Software  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |1.  No **coleção**, clique em **procurar**.<br />2.  No **procurar coleção** caixa de diálogo, clique em **Microsoft Deployment – o computador de referência**e, em seguida, clique em **OK**.<br />3.  No **comentário**, tipo **implementar o Windows 8.1 para o computador de referência e, em seguida, captura uma imagem do computador de referência**.<br />4.  Clique em **Seguinte**.|  
    |**Definições de implementação** |1.  No **objetivo**, selecione **disponível**.<br />2.  Selecione o **tornar disponível para efetuar o arranque de suportes de dados e PXE** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Definições de implementação: Agenda** |Clique em **Seguinte**.|  
    |**Definições de implementação: Experiência de utilizador** |Clique em **Seguinte**.|  
    |**Definições de implementação: Alertas** |Clique em **Seguinte**.|  
    |**Definições de implementação: Pontos de distribuição** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para implementar a sequência de tarefas é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para implementar uma sequência de tarefas," na biblioteca de documentação do Configuration Manager, que é instalado com o Configuration Manager.  

###  <a name="CreateTaskSequenceBootableMedia"></a>Passo 4-4: Criar tarefas sequência suportes de dados  
 Para iniciar o processo do MDT, fornecem um método para iniciar o computador com o Windows PE e o software necessário ao criar o disco de suportes de dados de sequência de tarefas. Utilize o Assistente de suporte de dados de sequência de tarefas na consola do Configuration Manager para criar suportes de dados para armazenamento de uma unidade flash USB, CD ou DVD.  

 **Para criar um disco de suportes de dados de sequência de tarefas**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar suporte de sequência de tarefas**.  

     Inicia o assistente suporte de dados de criação de sequência de tarefas.  

5.  Conclua o Assistente de criação tarefas sequência de suportes de dados utilizando as informações na tabela 27. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-27-information-for-completing-the-create-task-sequence-media-wizard"></a>27 de tabela. Informações para concluir o Assistente de suporte de dados de sequência de tarefas de criação  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Selecione o tipo de suporte de dados** |1.  Clique em **suportes de dados**.<br />2.  Limpar o **permitir a implementação do sistema operativo autónoma** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Selecione o tipo de suporte: Gestão de suporte de dados** |Clique em **suporte de dados baseado no Site**e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Tipo de suporte de dados** |No **ficheiro de multimédia**, tipo  **\\\WDG-MDT-01\Capture$\CM2012_TS_Boot_Media.iso**e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Segurança** |No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**e, em seguida, clique em **seguinte**.|  
    |**Selecione o tipo de suporte: Imagem de arranque** |1.  No **imagem de arranque**, clique em **procurar**.<br />2.  No **selecionar uma imagem de arranque** caixa de diálogo, clique em **personalizada do Windows PE**e, em seguida, clique em **OK**.<br />3.  No **ponto de distribuição**, clique em  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />4.  No **ponto de gestão**, clique em  **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />5.  Clique em **Seguinte**.|  
    |**Selecione o tipo de suporte: Personalização** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para criar o suporte de dados de sequência de tarefas é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

     O assistente cria o ficheiro CM2012_TS_Boot_Media.iso na pasta partilhada WDG-MDT-01Capture$.  

6.  Se WDG-REF-01 um computador físico, crie um CD ou DVD da organização internacionais para ficheiro uniformização (ISO). Se WDG-REF-01 uma VM, inicie a VM diretamente a partir do ficheiro ISO.  

 Para obter mais informações sobre como criar o disco de suportes de dados de sequência de tarefas, consulte a secção "Como para criar suportes de dados" na biblioteca de documentação do Configuration Manager, que é instalado com o Configuration Manager.  

###  <a name="StartReferenceComputerwithTaskSequenceBootableMedia"></a>Passo 4-5: Iniciar o computador de referência com o suporte de suportes de sequência de tarefas  
 Inicie o computador de referência (WDG-REF-01) com o disco de suportes de dados de sequência de tarefas criado anteriormente no processo. Esta média inicia o Windows PE no computador de referência e inicia o processo de MDT. No final do processo do MDT, Windows 8.1 está implementado no computador de referência e \WDG-MDT-01\Capture$\WDG-REF-01.wim é guardada uma imagem do computador de referência.  

> [!NOTE]
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows.  

 **Para iniciar o computador de referência com as tarefas sequência suportes de dados**  

1.  Inicie WDG-REF-01 com a tarefa sequência suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de sequência de tarefas.  

2.  Conclua o Assistente de sequência de tarefas utilizando as informações na tabela 28. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-28-information-for-completing-the-task-sequence-wizard"></a>28 de tabela. Informações para concluir o Assistente de sequência de tarefas  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Bem-vindo ao Assistente de sequência de tarefas** |No **palavra-passe**, tipo **P@ssw0rd**e, em seguida, clique em **seguinte**.|  
    |**Selecione uma sequência de tarefas** |Na caixa de lista, selecione **implementação de referência do Windows 8.1**e, em seguida, clique em **seguinte**.|  

 **Para monitorizar o processo de implementação de computador de referência utilizando o Deployment Workbench**  

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring.  

3.  No painel de detalhes, veja o processo de implementação para WDG-REF-01.  

4.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes. Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

5.  No painel de detalhes, clique em **WDG-REF-01**.  

6.  No painel ações, clique em **propriedades**.  

     O **WDG-REF-01 propriedades** é apresentada a caixa de diálogo.  

7.  No **WDG-REF-01 propriedades** caixa de diálogo a **identidade** separador, ver as informações de monitorização fornecidas sobre o processo de implementação, conforme descrito em 29 de tabela.  

    ### <a name="table-29-monitoring-information-about-the-deployment-process"></a>29 de tabela. Informações sobre o processo de implementação de monitorização  

    |**Informações** |**Descrição** |  
    |-|-|  
    |**ID** |Identificador exclusivo para o computador que está a ser implementado.|  
    |**Nome do computador** |O nome do computador que está a ser implementado.|  
    |Estado de implementação|O estado atual do computador que está a ser implementado; o estado pode ser um dos seguintes:<br /><br /> -   **Executar**. A sequência de tarefas é bom estado de funcionamento e em execução.<br />-   **Não foi possível**. A sequência de tarefas falha e o processo de implementação foi bem-sucedido.<br />-   **Concluir**. A sequência de tarefas foi concluída.<br />-   **Responder**. A sequência de tarefas não tiver atualizado o seu estado nas últimas quatro horas e é prestada, tentados.|  
    |**Passo** |O passo de sequência tarefas atual a ser executado.|  
    |**Progresso** |O progresso global da sequência de tarefas. A barra de progresso indica quantos passos de sequência de tarefas terem sido executados fora do número total de passos de sequência de tarefas.|  
    |**Iniciar** |A hora de início do processo de implementação.|  
    |**Fim** |A hora em que terminou o processo de implementação.|  
    |**Decorrido** |O período de tempo, o processo de implementação tem estado em execução ou demorou a execução se foi concluído o processo de implementação.|  
    |**Erros** |O número de erros encontrados durante o processo de implementação.|  
    |**Avisos** |O número de avisos durante o processo de implementação.|  
    |**Ambiente de trabalho remoto** |Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota com o computador que está a ser implementado através da funcionalidade de ambiente de trabalho remoto do Windows. Este método parte do princípio de que:<br /><br /> -O sistema operativo de destino está em execução e tiver ativada de suporte de ambiente de trabalho remoto<br />-   **mstsc.exe** está no caminho do **Nota:**  Este botão é sempre visível, mas pode não ser capaz de estabelecer uma sessão de ambiente de trabalho remoto, se o computador monitorizado está a executar o Windows PE, não foi concluída a instalação do sistema operativo de destino ou não tem ativada a funcionalidade de ambiente de trabalho remoto.|  
    |**Ligação de VM** |Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota para uma VM em execução no HyperV®. Este método parte do princípio de que:<br /><br /> -A implementação está a ser efetuada a uma VM em execução no Hyper-V<br />-   **vmconnect.exe** está localizado na pasta %ProgramFiles%\Hyper-V **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que os componentes de integração do Hyper-V estão em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Controlo remoto de daRT** |Este botão permite-lhe estabelecer uma sessão de controlo remoto utilizando a funcionalidade Visualizador remoto na Diagnostics e Recovery Toolkit (DaRT).<br /><br /> Este método parte do princípio de que:<br /><br /> -DaRT ter sido implementado no computador de destino e estiver em execução<br />-   **DartRemoteViewer.exe** está localizado na pasta %ProgramFiles%\Microsoft DaRT 7\v7 **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que DaRT está em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Atualizar automaticamente estas informações a cada 10 segundos** |Caixa de verificação que controla se as informações na caixa de diálogo é automaticamente atualizadas. Se a caixa de verificação:<br /><br /> -Selecionado, as informações são atualizadas cada 10 segundos<br />-Limpo, as informações não são automaticamente atualizadas e têm de ser manualmente atualizadas utilizando o **atualizar agora** botão|  
    |**Atualizar neste momento** |Este botão imediatamente atualiza as informações apresentadas na caixa de diálogo.|  

8.  No **WDG-REF-01 propriedades** caixa de diálogo, clique em **OK**.  

9. Feche o Deployment Workbench.  

 **Para monitorizar o processo de implementação de computador de referência utilizando o cmdlet Get-MDTMonitorData**  

1.  No WDG-MDT-01, clique em **iniciar**, aponte para **ferramentas administrativas**e, em seguida, clique em **módulos do Windows PowerShell**.  

     Abre a linha de comandos de módulos do Windows PowerShell.  

2.  Criar uma unidade do Windows PowerShell que utiliza o fornecedor do PowerShell do MDT, executando o [New-PSDrive](http://technet.microsoft.com/library/hh849829.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

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

-   Importar o ficheiro. wim capturado no passo anterior para o Configuration Manager utilizando o Assistente para adicionar imagem de sistema operativo, conforme descrito em [passo 5-1: Importar o ficheiro. wim capturado para o Configuration Manager](#ImportCapturedwimFileintoCOnfigurationManager)  

-   Utilizando o Assistente de criação MDT tarefas sequência para criar um modelo de sequência de tarefas do MDT para implementar a imagem capturada do computador de referência para o computador de destino, conforme descrito em [passo 5-2: Criar uma sequência de tarefas do MDT para implementar a imagem capturada](#CreateMDTTaskSequencetoDeployCapturedImage)  

-   Selecionar os pontos de distribuição para os novos pacotes e imagens que o assistente criar MDT tarefas sequência cria conforme descrito em [passo 5-3: Selecione os pontos de distribuição para os novos pacotes e a imagens](#SelectDistributionPointsforNewPackagesandImages)  

-   Personalizar os ficheiros de configuração do MDT para o computador de destino — especificamente, o ficheiro CustomSettings.ini, conforme descrito em [passo 5-4: Personalizar os ficheiros de configuração do MDT](#CustomizeMDTConfigurationFiles)  

-   Atualizar os pontos de distribuição do Configuration Manager para o pacote de definições personalizadas, conforme descrito em [passo 5-5: Atualizar os pontos de distribuição para o pacote de definições personalizadas](#UpdateDistributionPointsforCustomSettingsPackage)  

-   Personalizar a sequência de tarefas para o computador de destino, conforme descrito em [passo 5-6: Personalizar a sequência de tarefas para o computador de destino](#CustomizeTaskSequenceforTargetComputer)  

-   Configurar uma instalação autónoma do Office Professional Plus 2010, conforme descrito em [passo 5-7: Configurar uma instalação autónoma do Office Professional Plus 2010](#ConfigureUnattendedInstallationofOfficeProPlus)  

-   Criar uma aplicação do Configuration Manager para implementar o Office Professional Plus 2010 conforme descrito em [passo 5-8: Criar um Office Professional Plus 2010 aplicação](#CreateOfficeProPlusApplication)  

-   Distribuir a aplicação do Office Professional Plus 2010 para os pontos de distribuição, conforme descrito em [passo 5-9: Distribuir o Office Professional Plus 2010 aplicação](#DistributeOfficePeoPlusApplication)  

-   Disponibilizar a aplicação do Office Professional Plus 2010 para todos os utilizadores, tal como descrito no [passo 5-10: Tornar o Office Professional Plus 2010 aplicação disponível a todos os utilizadores](#MakeOfficeProPlusApplicationAvailable)  

-   Personalizar o ficheiro de configuração do Assistente de UDI conforme descrito em [passo 5-11: Personalizar o ficheiro de configuração do assistente UDI para o computador de destino](#CustomizeUDIWizardConfigFile)  

-   Criar uma nova página do assistente personalizados para recolher informações de implementação adicional, conforme descrito em [passo 5-13: Criar uma nova página do assistente personalizado](#CreateNewCustomWizardPage)  

-   Adicionar controlos para a página do assistente personalizada novo, conforme descrito em [passo 5-14: Adicionar controlos à nova página do assistente personalizado](#AddControlstoNewcustomWizardPage)  

-   Atualizar o MDT ficheiros de pacote que contém o ficheiro de configuração do Assistente de UDI atualizado conforme descrito em [passo 5-15: Atualizar os pontos de distribuição para o pacote de ficheiros do MDT](#UpdateDistributionPointsforMDTFilesPackage)  

###  <a name="ImportCapturedwimFileintoCOnfigurationManager"></a>Passo 5-1: Importar o ficheiro. wim capturado para o Configuration Manager  
 Depois da imagem do computador de referência (WDG-REF-01) é capturada no ficheiro. wim, importe o ficheiro. wim capturado para o Configuration Manager. Importe o ficheiro. wim capturado para o nó de imagens do sistema operativo utilizando o Assistente para adicionar imagem de sistema operativo.  

 O ficheiro WIM capturado contém duas imagens, um para cada partição no computador de referência. Identifique-se de que as imagens tem o sistema de operativo capturado Windows 8.1 utilizando a descrição da imagem que contém o Windows 8.1. Utilize o índice de imagem quando criar a sequência de tarefas para implementar a imagem capturada ao computador de destino.  

 **Para importar o ficheiro. wim capturado para o Configuration Manager**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para imagens de sistema de operativo/sistemas operativos/descrição geral.  

4.  No Friso, no **criar** , clique em **adicionar imagem de sistema operativo**.  

     Inicia o Assistente para adicionar imagem de sistema operativo.  

5.  Conclua o Assistente de imagem de sistema operativo adicionar utilizando as informações na tabela 30. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-30-information-for-completing-the-add-operating-system-image-wizard"></a>30 de tabela. Informações para concluir o Assistente de imagem do sistema operativo adicionar  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Origem de dados** |No caminho, escreva  **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**e, em seguida, clique em **seguinte**.|  
    |**Geral** |1.  No **nome**, tipo **imagem de referência do Windows 8.1**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **Windows 8.1 Capturar imagem do computador de referência (WDG-REF-01) utilizado para implementar em computadores de destino**e, em seguida, clique em **seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para importar a imagem do sistema operativo é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

6.  No painel de pré-visualização, clique em **imagem de referência do Windows 8.1**.  

7.  No painel de pré-visualização, clique o **detalhes** separador.  

     É apresentada a lista de partições de sistema operativo capturada no ficheiro. wim. O índice de imagem contém Windows 8.1 é o índice de imagem que irá especificar mais tarde durante o Assistente de criação MDT tarefas sequência.  

8.  Registe o índice de imagem contém Windows 8.1.  

    > [!TIP]
    >  Para efeitos deste exemplo, o índice de imagens 2 deve ter o sistema operativo do Windows 8.1.  

###  <a name="CreateMDTTaskSequencetoDeployCapturedImage"></a>Passo 5-2: Criar uma sequência de tarefas do MDT para implementar a imagem capturada  
 Depois da imagem ser capturada, crie uma sequência de tarefas para implementar a imagem capturada do computador de referência (WDG-REF-01) para o computador de destino (WDG-CLI-01). A maioria dos pacotes necessários para esta sequência de tarefas foram criada anteriormente no processo. No entanto, tem de criar um novo pacote de definições do MDT personalizadas que tenha as definições de configuração correto para o computador de destino e cria uma imagem do sistema operativo da imagem capturada do computador de referência.  

 **Para criar um modelo de sequência de tarefas para implementar a imagem capturada ao computador de destino**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No Friso, no **home page** separador o **sequências de tarefas** , clique em **criar sequência de tarefas do MDT**.  

     Inicia o Assistente de criação MDT tarefas sequência.  

5.  Conclua o Assistente de criação MDT tarefas sequência utilizando as informações na tabela 31. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-31-information-for-completing-the-create-mdt-task-sequence-wizard"></a>31 de tabela. Informações para concluir o Assistente de criação MDT tarefas sequência  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Escolha o modelo** |Selecione **sequência de tarefas de cliente**e, em seguida, clique em **seguinte**.|  
    |**Escolha o modelo: Geral** |1.  No **nome da sequência de tarefas**, tipo **UDI - implementação do Windows 8.1 destino**.<br />2.  No **comentários de sequência de tarefas**, tipo **sequência para implementar a imagem do computador de referência capturada ao computador de destino (WDG-CLI-01) de tarefas com o UDI**e, em seguida, clique em **seguinte**.|  
    |Escolha o modelo: Detalhes|1.  No **utilize o nome**, tipo **Woodgrove Bank empregado**.<br />2.  No **nome da organização**, tipo **Banco Woodgrove**.<br />3.  Clique em **Seguinte**.|  
    |**Escolha o modelo: Capturar definições** |Clique em **Seguinte**.|  
    |**Imagem de arranque** |1.  No **especificar um pacote de imagem de arranque existentes**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **personalizada do Windows PE**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Pacote de MDT** |1.  No **especificar um pacote de ficheiros de Toolkit do Microsoft implementação existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **ficheiros MDT**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Imagem do SO** |1.  Clique em **imagem de especificar um SO existente**.<br />2.  No **imagem de especificar um SO existente**, clique em **procurar**.<br />3.  No **selecionar um pacote** caixa de diálogo, clique em **imagem de referência do Windows 8.1**e, em seguida, clique em **OK**.<br />4.  Clique em **Seguinte**.|  
    |**Imagem do SO: Índice de imagem do SO** |1.  No **o ficheiro de imagem (WIM) do sistema operativo selecionado contiver várias imagens. Especifique a imagem que pretende implementar**, selecione ***image_index*** (onde *image_index* é o índice de imagem da imagem que contém o Windows 8.1, que foi identificado no [Passo 5-1: Importar o wim de Captured ficheiro para o Configuration Manager](#ImportCapturedwimFileintoCOnfigurationManager); para efeitos deste guia, selecione de 2).<br />2.  Clique em **Seguinte**.|  
    |**Método de implementação** |Clique em **efetuar uma instalação"modo"** e, em seguida, clique em **seguinte**.|  
    |**Pacote de cliente** |1.  No **especificar um pacote de cliente do ConfigMgr existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **a atualização de cliente do Microsoft Configuration Manager**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |**Pacote USMT** |1.  No **especificar um pacote USMT existente**, clique em **procurar**.<br />2.  No **selecionar um pacote** caixa de diálogo, clique em **USMT**e, em seguida, clique em **OK**.<br />3.  Clique em **Seguinte**.|  
    |Pacote de definições|1.  Clique em **criar um novo pacote de definições**.<br />2.  No **pasta de origem do pacote sejam criados**, tipo  **\\\WDG-MDT-01\Packages$\UDICustomSettings_Target**e, em seguida, clique em **seguinte**.|  
    |**Pacote de definições: Detalhes de definições** |1.  No **nome**, tipo **definições de personalizada de computador de destino de UDI**.<br />2.  No **versão**, tipo **1.00**.<br />3.  No **comentários**, tipo **definições de configuração para o processo de implementação do MDT com o UDI (por exemplo, CustomSettings.ini) para o computador de destino**e, em seguida, clique em **seguinte**.|  
    |**Pacote Sysprep** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |É apresentado o progresso da criação de sequência de tarefas.|  
    |**Confirmação** |Clique em **Concluir**.|  

 É apresentada a lista de sequências de tarefas. A sequência de tarefas que acabou de criar (**UDI – implementação de destino do Windows 8.1**) está listado na lista de sequências de tarefas.  

###  <a name="SelectDistributionPointsforNewPackagesandImages"></a>Passo 5-3: Selecione os pontos de distribuição para os novos pacotes e a imagens  
 Executar a criar MDT assistente sequência de tarefas para criar a sequência de tarefas para o destino gera um novo pacote de distribuição de software e uma nova imagem. Quando o pacote e a imagem são criados, selecione os pontos de distribuição a partir do qual o pacote e a imagem será copiado e disponíveis para computadores de destino.  

> [!NOTE]
>  Neste exemplo, não há apenas um ponto de distribuição (WDG-MDT-01). No entanto, a maioria das redes de produção terão a vários pontos de distribuição. Quando executar este passo num ambiente de produção, selecione os pontos de distribuição apropriados para a rede.  

 Selecione os pontos de distribuição para o pacote de distribuição de software (para o novo pacote de definições personalizadas do computador de destino chamado *definições de personalizado do computador de destino do MDT 2013*) e o pacote de imagem do sistema operativo (para o novo ficheiro. wim capturada do computador de referência chamado *imagem de referência do Windows 8.1*).  

 **Para selecionar os pontos de distribuição para o pacote de distribuição de software**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de visualização, selecione **UDI - implementação do Windows 8.1 destino**.  

     No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

5.  Conclua o Assistente para distribuir conteúdo utilizando as informações na tabela 32. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-32-information-for-completing-the-distribute-content-wizard"></a>Tabela 32. Informações para concluir a distribuir o conteúdo Assistente  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |Clique em **Seguinte**.|  
    |**Conteúdo** |Clique em **Seguinte**.|  
    |**Gerais: Destino do conteúdo** |1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar pontos de distribuição** é apresentada a caixa de diálogo.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDGMDT01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece no **destino do conteúdo** lista.<br />3.  Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso da distribuição de software é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

###  <a name="CustomizeMDTConfigurationFiles"></a>Passo 5-4: Personalizar os ficheiros de configuração do MDT  
 Quando a sequência de tarefas para o computador de destino tiver sido criado, personalizar os ficheiros de configuração do MDT que fornecem as definições de configuração para a implementação do Windows 8.1 para o computador de destino — especificamente, CustomSettings.ini.  

 Quando tiver sido personalizado ficheiro CustomSettings.ini, guarde ficheiros atualizados para a pasta de origem para o pacote de definições personalizadas de MDT criado anteriormente no processo (E:\Packages$\CustomSettings_Target).  

 **Para personalizar os ficheiros de configuração do MDT para o computador de destino**  

1.  No Explorador do Windows, aceda à pasta E:\Packages$\CustomSettings_Target e, em seguida, faça duplo clique em **CustomSettings.ini**.  

2.  Abra o bloco de notas e, em seguida, adicione a seguinte linha ao ficheiro CustomSettings.ini que requer que o ambiente, conforme mostrado na listagem 2:  

     Esta definição configura a monitorização da implementação de computador de destino.  

    > [!NOTE]
    >  Efetue as alterações que necessita do seu ambiente.  

     **Listar 2. Predefinição ficheiro CustomSettings.ini**  

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

###  <a name="UpdateDistributionPointsforCustomSettingsPackage"></a>Passo 5-5: Atualizar os pontos de distribuição para o pacote de definições personalizadas  
 Quando a pasta de origem tiver sido atualizada para o pacote de definições de personalizado do computador de destino do MDT no Configuration Manager, atualize os pontos de distribuição para o pacote de definições de personalizado do computador de destino do MDT. Atualizar os pontos de distribuição copia a versão atualizada do ficheiro CustomSettings.ini para as partilhas de implementação especificadas no pacote.  

 **Para atualizar a distribuição aponta para o pacote de definições personalizadas**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para gestão/pacotes de aplicações/descrição geral.  

4.  No painel de pré-visualização, clique em **definições personalizadas do MDT destino computador**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **atualizar pontos de distribuição**.  

     O **do Configuration Manager** abre a caixa de diálogo, notificam que pretender atualizar o pacote em todos os pontos de distribuição.  

6.  No **do Configuration Manager** caixa de diálogo, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizeTaskSequenceforTargetComputer"></a>Passo 5-6: Personalizar a sequência de tarefas para o computador de destino  
 Para a maioria das implementações, a sequência de tarefas de implementação de destino do Windows 8.1 criada anteriormente no processo efetua os passos necessários sem modificação. Neste exemplo, modifique o modelo de sequência de tarefas para definir a palavra-passe para a conta de administrador local para um valor conhecido. (Por predefinição, a sequência de tarefas define a palavra-passe para a conta de administrador local para um valor aleatório.) A sequência de tarefas pode exigir mais personalização, dependendo do ambiente.  

 **Para personalizar a sequência de tarefas de implementação de destino do Windows 8.1**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **UDI - implementação do Windows 8.1 destino**.  

5.  No Friso, no **home page** separador o **sequência de tarefas** , clique em **editar**.  

     O **Editor de sequência de tarefas de implementação do Windows 8.1 referência** é aberta a caixa de diálogo.  

6.  No **Editor de sequência de tarefas de implementação do Windows 8.1 referência** caixa de diálogo, aceda a PostInstall/aplicar as definições do Windows.  

7.  No **propriedades** separador, clique em **ativar a conta e especificar a palavra-passe de administrador local**.  

8.  No **propriedades** separador **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**e, em seguida, clique em **aplicar** .  

9. Efetue quaisquer modificações adicionais para a sequência de tarefas que requer que o ambiente e, em seguida, clique em **OK**.  

10. Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="ConfigureUnattendedInstallationofOfficeProPlus"></a>Passo 5-7: Configurar uma instalação autónoma do Office Professional Plus 2010  
 O Configuration Manager distribui os ficheiros e pastas utilizadas para implementar o Office Professional Plus 2010, mas não fornece o método para efetuar uma instalação autónoma após a distribuição. Em vez disso, a instalação autónoma tem de ser configurada através de métodos fornecidos no Office Professional Plus 2010. Pode configurar uma instalação autónoma (automática) do Office Professional Plus 2010 utilizando um dos seguintes métodos:  

-   Crie um ficheiro de personalização da configuração da ferramenta de personalização do Office (FPO) (ficheiro. msp).  

-   Modificar o ficheiro Config.xml.  

 Para obter mais informações sobre cada um destes métodos, consulte [personalizar o programa de configuração antes de instalar o Office 2010](http://technet.microsoft.com/library/cc179121.aspx).  

 Para efeitos deste guia, será efetuada a instalação autónoma do Office Professional Plus 2010 através da criação de um ficheiro de personalização da configuração de FPO (ficheiro. msp). Irá guardar a configuração de FPO personalização ficheiro na pasta atualizações, que é analisada automaticamente pelo Assistente de configuração do Office Professional Plus 2010.  

 **Para configurar uma instalação autónoma do Office Professional Plus 2010**  

1.  Numa linha de comandos, escreva o seguinte comando e, em seguida, prima ENTER.  

    ```  
    e:  
    ```  

2.  Numa linha de comandos, escreva o seguinte comando e, em seguida, prima ENTER.  

    ```  
    cd \Source$\OfficeProPlus2010\  
    ```  

3.  Numa linha de comandos, escreva o seguinte comando e, em seguida, prima ENTER.  

    ```  
    setup /admin  
    ```  

     O FPO é iniciado e o **selecione produto** é aberta a caixa de diálogo.  

4.  No FPO, no **selecione produto** caixa de diálogo, clique em **OK**.  

     O FPO carrega as informações adequadas e, em seguida, apresenta as definições que podem ser personalizadas no ficheiro. msp.  

5.  No FPO, no painel de navegação, aceda ao nome do programa de configuração/instalação da localização e a organização.  

6.  No painel de pré-visualização, na **nome da organização**, tipo **Banco Woodgrove**.  

7.  No FPO, no painel de navegação, aceda à interface de utilizador e a configuração/Licensing.  

8.  No painel de visualização, selecione o **aceito os termos no contrato de licença** caixa de verificação.  

9. No painel de pré-visualização, na **apresentar nível**, selecione **nenhum**.  

10. Do **ficheiro** menu, clique em **guardar como**.  

     O **guardar como** é aberta a caixa de diálogo.  

11. No **guardar como** caixa de diálogo, escreva **E:\Source$\OfficeProPlus2010\Updates\OPP2010_Unattend**e, em seguida, clique em **guardar**.  

     O ficheiro OPP2010_Unattend.msp é guardado.  

12. Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CreateOfficeProPlusApplication"></a>Passo 5-8: Criar um Office Professional Plus 2010 aplicação  
 Uma das vantagens para efetuar implementações do MDT com o UDI é a capacidade para o utilizador selecionar as aplicações a instalar no momento da implementação. Pode adicionar qualquer número de aplicações do Configuration Manager e, em seguida, selecione as aplicações quando executar o Assistente de UDI, conforme descrito em [passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas](#StartTargetComputerwithTaskSequenceBootableMedia).  

 Pode configurar as aplicações que são apresentados no Assistente de UDI com o UDI Wizard Designer, conforme descrito em [passo 5-11: Personalizar o ficheiro de configuração do assistente UDI para o computador de destino](#CustomizeUDIWizardConfigFile).  

 **Para criar uma aplicação do Office Professional Plus 2010**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda à descrição geral/aplicação/aplicações de gestão.  

4.  No Friso, no **home page** separador o **criar** , clique em **Criar aplicação**.  

     Inicia o Assistente para criar aplicação.  

5.  Conclua o Assistente para criar aplicação utilizando as informações na tabela 33. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-3-information-for-completing-the-create-application-wizard"></a>Tabela 3. Informações para concluir o Assistente para criar aplicação  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |Clique em **especificar manualmente as informações da aplicação**e, em seguida, clique em **seguinte**.|  
    |**Gerais: Geral** |1.  No **nome**, tipo **Microsoft Office Professional Plus 2010 – x86**.<br />2.  No **comentários do administrador**, tipo **versão de 32 bits do Microsoft Office Professional Plus 2010**.<br />3.  Selecione o **permitem que esta aplicação ser instalado a partir da ação de sequência de tarefas instalar aplicação em vez de implementar a política manualmente** caixa de verificação.<br />4.  Clique em **Seguinte**.|  
    |**Gerais: Catálogo de aplicações** |1.  No **descrição localizada**, tipo **versão de 32 bits do Microsoft Office Professional Plus 2010 para utilização pelos funcionários do Woodgrove Bank**.<br />2.  No **palavras-chave**, **escreva Office Professional Plus 2010**.<br />3.  Clique em **Seguinte**.|  
    |**Gerais: Tipo de implementação s** |<ol><li>Clique em **Adicionar**.<br /><br />     A criar o início da implementação tipo assistente.</li><li>No **implementação Assistente para criar tipo**, no **geral** página, clique em **especificar manualmente as informações de tipo de implementação** e, em seguida, clique em **seguinte**.</li><li>No **gerais: Informações gerais** página, execute os passos seguintes e, em seguida, clique em **seguinte**:<br /><br /> <ol><li>No **nome**, tipo **Microsoft Office Professional Plus 2010 – x32 (Windows Installer)**.</li><li>No **comentários do administrador**, tipo **implementar o Microsoft Office Professional Plus 2010 utilizando nativo do Windows Installer**.</li></ol></li><li>No **gerais: Conteúdo** página, execute os passos seguintes e, em seguida, clique em **seguinte**:<br /><br /> <ol><li>No **localização de conteúdo**, tipo  **\\\WDGMDT01\Source$\OfficeProPlus2010**.</li><li>No **programa de instalação**, tipo **setup.exe**.</li><li>No **programa de desinstalação**, tipo **setup.exe / desinstalar PROPLUS**.</li></ol></li><li>No **gerais: Método de deteção** página, execute os passos seguintes e, em seguida, clique em **seguinte**:<br /><br /> <ol><li>Clique em Adicionar **cláusula**,<br /><br />         O **regra de deteção** é apresentada a caixa de diálogo.</li><li>No **regra de deteção** caixa de diálogo **tipo de definição**, selecione **do Windows Installer**.</li><li>No **código de produto**, clique em **procurar**<br /><br />         O **abra** é apresentada a caixa de diálogo.</li><li>No **caixa de diálogo Abrir** caixa **nome de ficheiro**, tipo  **\\\WDGMDT01\Source$\OfficeProPlus2010\ProPlus.WW\ProPlusWW.msi**e, em seguida, clique em **Abra**.<br /><br />         O código de produto para o Office Professional Plus 2010 aparece no **código de produto** caixa.</li><li>No **regra de deteção** caixa de diálogo, clique em **OK**.</li></ol></li><li>No **gerais: Experiência de utilizador** página, execute os passos seguintes e, em seguida, clique em **seguinte**:<br /><br /> <ol><li>No **comportamento de instalação**, selecione **instalar para o sistema**.</li><li>No **requisito de início de sessão**, selecione **se deve ou não um utilizador iniciado**.</li><li>No **visibilidade do programa de instalação**, selecione **Normal**.</li><li>No **tempo de instalação estimado**, tipo **120**.</li></ol></li><li>No **requisitos** página, clique em **seguinte**.</li><li>No **dependências** página, clique em **seguinte**.</li><li>No **resumo** página, clique em **seguinte**.</li><li>No **conclusão** página, clique em **fechar**.<br /><br />     Inicia o Assistente para criar aplicação.</li><li>Clique em **Seguinte**.</li></ol>|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para criar a aplicação é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

 O Office Professional Plus 2010 – x86 aplicação aparece no painel de pré-visualização.  

###  <a name="DistributeOfficePeoPlusApplication"></a>Passo 5-9: Distribuir o Office Professional Plus 2010 aplicação  
 Depois de criar a aplicação do Office Professional Plus 2010, terá de distribuir a aplicação para os pontos de distribuição. Se o fizer, permite a instalação da aplicação dos pontos de distribuição. Para efeitos deste guia, há apenas um ponto de distribuição (WDG-MDT-01). Nas implementações do Configuration Manager típica, normalmente, existem vários pontos de distribuição.  

 **Para distribuir a aplicação do Office Professional Plus 2010**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda à descrição geral/aplicação/aplicações de gestão.  

4.  No painel de pré-visualização, clique em **Microsoft Office Professional Plus 2012 – x86**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **distribuir conteúdo**.  

     Inicia o Assistente para distribuir conteúdo.  

6.  Conclua o Assistente para distribuir conteúdo utilizando as informações na tabela 34. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-34-information-for-completing-the-distribute-content-wizard"></a>34 de tabela. Informações para concluir a distribuir o conteúdo Assistente  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |Clique em **Seguinte**.|  
    |**Gerais: Conteúdo** |Clique em **Seguinte**.|  
    |**Gerais: Destino do conteúdo** |1.  Clique em **adicionar**e, em seguida, clique em **ponto de distribuição**.<br />     O **adicionar distribuição** é apresentada a caixa de diálogo de pontos.<br />2.  No **adicionar pontos de distribuição** caixa de diálogo, selecione  **\\\WDGMDT01.mdt2013.corp.woodgrovebank.com**e, em seguida, clique em **OK**.<br />     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com aparece na lista de destino do conteúdo.<br />3.  Clique em **Seguinte**.|  
    |Resumo|Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para distribuir a aplicação é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="MakeOfficeProPlusApplicationAvailable"></a>Passo 5-10: Tornar o Office Professional Plus 2010 aplicação disponível a todos os utilizadores  
 Depois de criar a aplicação do Office Professional Plus 2010, terá de distribuir a aplicação para os pontos de distribuição. Se o fizer, permite a instalação da aplicação dos pontos de distribuição. Para efeitos deste guia, há apenas um ponto de distribuição (WDG-MDT-01). Nas implementações do Configuration Manager típica, normalmente, existem vários pontos de distribuição.  

 **Para disponibilizar a aplicação do Office Professional Plus 2010 para todos os utilizadores**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, aceda à descrição geral/aplicação/aplicações de gestão.  

4.  No painel de pré-visualização, clique em **Microsoft Office Professional Plus 2010 – x86**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **implementar**.  

     Inicia o Assistente de implementação de Software.  

6.  Conclua o Assistente para implementar Software utilizando as informações na tabela 35. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-35-information-for-completing-the-deploy-software-wizard"></a>35 de tabela. Informações para concluir o Assistente de implementação Software  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |1.  No **coleção**, clique em **procurar**.<br />     O **selecionar coleção** é apresentada a caixa de diálogo.<br />2.  No **selecionar coleção** caixa de diálogo, clique em **todos os utilizadores**e, em seguida, clique em **OK**.<br />3.  No **comentários**, tipo **tornar Microsoft Office Professional Plus 2010 disponível para implementação em todos os utilizadores**.<br />4.  Clique em **Seguinte**.|  
    |**Conteúdo** |Clique em **Seguinte**.|  
    |**Definições de implementação** |Clique em **Seguinte**.|  
    |**Agendamento** |Clique em **Seguinte**.|  
    |**Alertas** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para implementar a aplicação é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

7.  Feche todas as janelas abertas e caixas de diálogo.  

###  <a name="CustomizeUDIWizardConfigFile"></a>Passo 5-11: Personalizar o ficheiro de configuração do assistente UDI para o computador de destino  
 O modelo de sequência de tarefas de instalação de modo inclui um passo de sequência de tarefas que executa o Assistente de UDI. Quando um passo de sequência de tarefas executa o Assistente de UDI, o passo também faz referência a um ficheiro XML que determina a configuração do Assistente de UDI. O ficheiro de UDIWizard_Config.xml na pasta de Scripts controla o comportamento do Assistente de UDI. Personalize o ficheiro de UDIWizard_Config.xml com o UDI Wizard Designer.  

 O UDI Wizard Designer inclui grupos fase predefinidas para que o Assistente de UDI listados na tabela 36. Pode adicionar ou remover as páginas do assistente que aparecem no Assistente de UDI e a sequência de cada página do Assistente para cada grupo de fase.  

### <a name="table-36-predefined-stage-groups-for-each-supported-mdt-deployment-scenario"></a>Tabela 36. Grupos de fase predefinidas para cada cenário de implementação do MDT suportados  

|**Grupo de fase** |**Descrição** |  
|-|-|  
|**Novo computador** |Utilize este grupo de fase como base para a sua implementação quando uma nova instalação de um sistema operativo Windows for implementada para um novo computador e sem estado de utilizador é migrado.|  
|**Atualizar** |Utilize este grupo de fase como base para a sua implementação quando um computador é atualizado, incluindo computadores que têm de ser recriadas para uniformização de imagem ou para abordar um problema.|  
|**Substituir** |Utilize este grupo de fase como base para a sua implementação quando um computador substitui noutro computador. Os dados de migração de estado de utilizador existente são guardados do computador original. Em seguida, uma nova instalação do Windows é implementada para um novo computador. Por fim, os dados de estado do utilizador são restaurados para o novo computador.|  

 **Para personalizar o ficheiro de configuração do Assistente de UDI para o computador de referência**  

1.  Clique em **iniciar**, aponte para **todos os programas**, aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **UDI Wizard Designer**.  

     Inicia o UDI Wizard Designer.  

2.  No Friso, no **home page** separador o **Menu ficheiro** , clique em **abra**.  

3.  No **abra** caixa de diálogo **nome de ficheiro**, tipo  **\\\WDG-MDT-01\Packages$\MDT_Files\Scripts\UDIWizard_Config.xml**e, em seguida, clique em **Abra**.  

    > [!NOTE]
    >  Esta ação abre a cópia do ficheiro UDIWizard_Config.xml que reside na pasta do pacote do MDT que criou quando executou o Assistente de criação Microsoft implementação tarefas sequência anteriormente no processo.  

4.  Na página biblioteca, clique em **instalar programas**.  

5.  No Friso, no **home page** separador o **editar definições de** , clique em **do Configuration Manager**.  

     O **definições do Site** é apresentada a caixa de diálogo.  

6.  No **caixa de diálogo Definições de Site** , execute os passos seguintes e, em seguida, clique em **OK**:  

    1.  No **nome do servidor de Site**, tipo **WDG-MDT-01**.  

    2.  No **código do Site**, tipo **NYC**.  

    3.  Clique em **validar Site**.  

    4.  No **coleção de aplicações**, tipo **todos os utilizadores**.  

        > [!NOTE]
        >  A coleção do Configuration Manager que escreva aqui tem de corresponder à coleção do Configuration Manager nos quais tiver implementado as suas aplicações. Neste guia, que selecionou a coleção de todos os utilizadores na [passo 5-10: Tornar o Office Professional Plus 2010 aplicação disponível a todos os utilizadores](#MakeOfficeProPlusApplicationAvailable).  

7.  No painel de pré-visualização, no **fluxo** separador, expanda **StageGroup: Novo computador**.  

     A lista de páginas do assistente utilizado o StageGroup: Novo fluxo de computador é apresentado.  

    > [!NOTE]
    >  Tome nota da sequência de páginas do Assistente de StageGroup: Novo fluxo de computador no UDI Wizard Designer. Verá a mesma sequência das páginas do assistente, quando executa o Assistente de UDI no [passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas](#StartTargetComputerwithTaskSequenceBootableMedia).  

8.  Configurar o **StageGroup: Novo computador** fluxo utilizando a informação para cada página listados na tabela 37. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-37-information-for-configuring-udi-wizard-designer-pages"></a>37 de tabela. Informações para configurar páginas de estruturador do assistente UDI  

    |**Página do Assistente** |**Clique no separador de configurar e efetue o seguinte** |  
    |-|-|  
    |**BitLocker** |<ol><li>Em **BitLocker modo**, expanda **BitLocker modo**. No **caixa de verificação do BitLocker**, desmarque a **inicialmente marcar esta caixa de verificação** caixa de verificação.</li><li>Em **BitLocker modo**, clique em **Unlocked** para cada uma das seguintes opções de configuração:<br /><br /> <ul><li>**Caixa de verificação do BitLocker**</li><li>**Botões de opção de modo do BitLocker**</li><li>**Caixa de texto PIN**</li></ul></li></ol><br /> O estado para cada opção de configuração é alterado para **está bloqueado**, que impede os utilizadores destas opções do Assistente de UDI a alteração.|  
    |**Volume** |<ol><li>Em **caixa de combinação de imagem**, expanda **comportamento de combinação de imagem**, em **valores da caixa de combinação imagem**, faça duplo clique **Windows 8.1 RTM (x86)**, e cliczk, em seguida, selecione um **imagem do sistema operativo**.<br /><br />     O **selecionar uma imagem do sistema operativo** é apresentada a caixa de diálogo.</li><li>Concluir o **selecionar uma imagem do sistema operativo** caixa de diálogo, efetuando os seguintes passos e, em seguida, clique em **OK**:<br /><br /> <ol><li>No **selecionar um imagem/instalador do sistema operativo para adicionar**, clique em ***image_index*** (onde *image_index* é o índice de imagem da imagem que contém o Windows 8.1, que era identificado no [passo 5-1: Importar o wim de Captured ficheiro para o Configuration Manager](#ImportCapturedwimFileintoCOnfigurationManager); para efeitos deste guia, selecione **2**).</li><li>No **nome a apresentar**, tipo **imagem de referência do Windows 8.1 – x64**.</li></ol></li><li>Em **caixa de combinação de imagem**, expanda **comportamento de combinação de imagem**; em **valores da caixa de combinação imagem**, faça duplo clique **Windows 8.1 RTM (x86)**, e em seguida, clique em **Remover Item**.<br /><br />     O **eliminar o Item de confirmação** é apresentada a caixa de diálogo.</li><li>No **eliminar o Item de confirmação** caixa de diálogo, clique em **Sim**.</li><li>Em **definições e dados do utilizador**, expanda **comportamento de combinação de dados de utilizador**e, em seguida, selecione o **formato: Limpar todos os dados no volume de destino durante a instalação** caixa de verificação.</li><li>Em **comportamento de combinação de dados de utilizador**, clique em **Unlocked** para cada uma das seguintes opções de configuração:<br /><br /> <ul><li>**Unidade de formato**</li><li>**Diretório do Windows**</li></ul></li></ol><br /> O estado para cada opção de configuração é alterado para **está bloqueado**, que impede os utilizadores destas opções do Assistente de UDI a alteração.|  
    |**Detalhes do novo computador** |1.  Em **detalhes da rede**, expanda **detalhes da rede**; na **botões de opção do grupo de trabalho ou domínio**, clique em **domínio**.<br />2.  Em **botões de opção do grupo de trabalho ou domínio**, clique em **Unlocked**.<br />     O estado muda para **está bloqueado**, que impede os utilizadores de alterar esta opção no Assistente de UDI.<br />3.  Em **detalhes da rede**, expanda **domínios e UOs**e, em seguida, clique em **Adicionar domínio**.<br />     O **criar ou editar as informações do domínio** é apresentada a caixa de diálogo.<br />4.  No **criar ou editar as informações do domínio** caixa de diálogo **nome de domínio** tipo **mdt2013.corp.woodgrovebank.com**.<br />5.  No **criar ou editar as informações do domínio** caixa de diálogo **nome amigável**, tipo **Woodgrove Bank Active Directory Domain**e, em seguida, clique em **OK**.|  
    |**Instalar os programas** |<ol><li>Em **Software e grupos**, faça duplo clique qualquer área em branco e, em seguida, clique em **adicionar grupo de Software**.<br /><br />     O **adicionar/editar um grupo de Software** é apresentada a caixa de diálogo.</li><li>No **adicionar/editar um grupo de Software** caixa de diálogo **nome**, tipo **Woodgrove Bank aplicações**e, em seguida, clique em **OK**.</li><li>Em **Software e grupos**, clique em **Woodgrove Bank aplicações**.</li><li>No Friso, no **home page** separador o **definições gerais de Item de Software** , clique em **adicionar**e, em seguida, clique em **adicionar Software ao grupo**.<br /><br />     Assistente de grupo para adicionar Software é iniciado.</li><li>Conclua o Software de adicionar ao Assistente de grupo, efetuando os seguintes passos:<br /><br /> <ol><li>No **que tipo de item de software que pretende adicionar** página, clique em **pretender adicionar uma aplicação**e, em seguida, clique em **seguinte**.</li><li>No **pesquisa Configuration Manager para o Item de Software para adicionar** na página **nome a apresentar**, tipo **Microsoft Office Professional Plus 2010 – x86**.</li><li>No **pesquisa Configuration Manager para o Item de Software para adicionar** página, clique em **selecione**.<br /><br />         O **procurar aplicações** é apresentada a caixa de diálogo.</li><li>No **procurar aplicações** caixa de diálogo, clique em **pesquisa**, clique em **Microsoft Office Professional Plus 2010 – X86**e, em seguida, clique em **OK** .</li><li>No **Gestor de configuração de pesquisa para o Item de Software para a página do Add**, clique em **concluir**.</li></ol><br />     **Microsoft Office Professional Plus 2010 – x86** aparece por baixo do **Woodgrove Bank aplicações** grupo de software.</li><li>Em **Software e grupos**, clique em **geral Software**.</li><li>No Friso, no **home page** separador o **definições gerais de Item de Software** , clique em **adicionar**e, em seguida, clique em **Remover Item**.<br /><br />     O **eliminar o Item selecionado** é apresentada a caixa de diálogo.</li><li>No **eliminar o Item selecionado** caixa de diálogo, clique em **Sim**.</li><li>Em **Software e grupos**, selecione a caixa de verificação **Woodgrove Bank aplicações**.<br /><br />     O grupo e o Microsoft Office Professional Plus 2010 – x86 estão selecionadas.</li></ol>|  

9. No Friso, no **home page** separador, clique em **guardar**.  

     O **Guardar ficheiro** é apresentada a caixa de diálogo.  

10. No **Guardar ficheiro** caixa de diálogo, clique em **OK**.  

11. Deixe o UDI Wizard Designer aberta para o passo seguinte.  

###  <a name="CreateNewCustomWizardPage"></a>Passo 5-13: Criar uma nova página do assistente personalizado  
 Pode criar páginas de assistente personalizadas que lhe permitem recolher informações de implementação para além das informações recolhidas noutras páginas do Assistente de UDI. Criar páginas de assistente personalizadas com base no **criar sua própria página** tipo de página do assistente. Depois de criar a página do assistente personalizado, pode adicionar controlos e configurar as variáveis de sequência de tarefas controlos definido.  

 Para este guia, o Woodgrove Bank pretende permitir que os utilizadores introduzir o respetivo nome e o departamento de que funcionam. Banco Woodgrove é departmentalized por localização geográfica. Estas informações serão utilizadas para configurar a organização e o nome de utilizador registado no Windows. Neste passo, adicione uma nova página do assistente personalizado para o grupo de fase do novo computador.  

 **Para criar uma nova página do assistente personalizado**  

1.  No Friso, no **home page** separador o **página biblioteca** , clique em **Adicionar página**. O **Adicionar nova página** é apresentada a caixa de diálogo.  

2.  No **Adicionar nova página** caixa de diálogo a **tipo de página** coluna, clique em **criar sua própria página**.  

3.  No **nome a apresentar**, tipo **informações do utilizador**.  

4.  No **nome da página**, tipo **UserInformationPage**e, em seguida, clique em **OK**.  

     O **informações do utilizador** na biblioteca de página é apresentada a página.  

5.  No painel de detalhes, clique o **fluxo** separador.  

6.  No **fluxo** separador, expanda o grupo de fase do novo computador.  

     É apresentada a lista de páginas de assistente, no grupo de fase de novo computador.  

7.  Na biblioteca de página, arraste o **informações do utilizador** página para um ponto de imediatamente antes o **BitLocker** página no grupo de fase de novo computador o **fluxo** separador.  

8.  No Friso, no **home page** separador, clique em **guardar**.  

     O **Guardar ficheiro** é apresentada a caixa de diálogo.  

9. No **Guardar ficheiro** caixa de diálogo, clique em **OK**.  

10. Deixe o UDI Wizard Designer aberta para o passo seguinte.  

###  <a name="AddControlstoNewcustomWizardPage"></a>Passo 5-14: Adicionar controlos à nova página do assistente personalizado  
 Depois da página do assistente personalizada de UDI nova foi adicionada ao grupo de fase de novo computador, os controlos adequados tem de ser adicionado à página do assistente personalizada nova. Os controlos adicionados a página do assistente personalizado da caixa de ferramentas de compilação da página próprio, que é apresentada quando visualiza a página do assistente personalizado no **configurar** separador o UDI Wizard Designer.  

 38 tabela lista os tipos de controlos para a página do assistente personalizadas, que é ilustrado na figura 1.  

### <a name="table-38-types-of-controls-in-the-udi-build-your-own-page-toolbox"></a>Tabela de 38. Tipos de controlos de UDI criar as suas próprias ferramentas da página  

|**Tipo de controlo** |**Descrição** |  
|-|-|  
|**Checkbox** |Este controlo permite-lhe selecionar ou desmarcar uma opção de configuração e funciona como uma caixa de verificação de interface (IU) do utilizador tradicional. Este controlo tem uma etiqueta correspondente que pode utilizar para descrever o objetivo da caixa de verificação. O estado deste controlo é verdadeiro quando a caixa de verificação está selecionada e falso quando a caixa de verificação está desmarcada. O estado da caixa de verificação é armazenado na variável de sequência de tarefas configurada para este controlo. Para obter mais informações sobre este controlo, consulte "Controlo de caixa de verificação" no documento do MDT, *Toolkit referência*.|  
|**Combobox** |Este controlo permite-lhe selecionar um item de uma lista de itens e funciona como uma tradicional IU na lista pendente. Este controlo permite-lhe adicionar ou remover itens da lista e forneça um valor correspondente, que será definido na variável de sequência de tarefas configurada para este controlo. Para obter mais informações sobre este controlo, consulte "Controlo de caixa de combinação" no documento do MDT, *Toolkit referência*.|  
|**Line** |Este controlo permite-lhe adicionar uma linha horizontal dividir uma parte da página do assistente personalizada de outro. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU. Para obter mais informações sobre este controlo, consulte "Controlo de linha" no documento do MDT, *Toolkit referência*.|  
|**Label** |Este controlo permite-lhe adicionar texto descritivo só de leitura para a página do assistente. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU. Para obter mais informações sobre este controlo, consulte "Controlo de etiqueta" no documento do MDT, *Toolkit referência*.|  
|**Radio** |Este controlo permite-lhe selecionar uma opção de configuração de um grupo de dois ou mais opções. Tal como acontece com botões de opção tradicionais, dois ou mais destes controlos podem ser agrupados em conjunto e, em seguida, o utilizador pode selecionar uma das opções no grupo de botões de opção. Um valor exclusivo é atribuído a cada opção. O valor atribuído ao controlo opção selecionada é guardado na variável de sequência de tarefas configurada para este controlo. Para obter mais informações sobre este controlo, consulte "Controlo de botões de opção" no documento do MDT, *Toolkit referência*.|  
|**Bitmap** |Este controlo permite-lhe adicionar um gráfico de mapa de bits (.bmp ficheiro) para a página do assistente personalizado. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU. O caminho para o ficheiro .bmp é relativo à localização do Assistente de UDI (OSDSetupWizard.exe). Para obter mais informações sobre este controlo, consulte "Controlo de mapa de bits" no documento do MDT, *Toolkit referência*.|  
|**Textbox** |Este controlo permite-lhe introduzir o texto na página do assistente personalizado. O texto digitado neste controlo é guardado na variável de sequência de tarefas configurada para este controlo. Para obter mais informações sobre este controlo, consulte "Controlo de caixa de texto" no documento do MDT, *Toolkit referência*.|  

 Pode adicionar qualquer combinação destes controlos para a página do assistente personalizadas com base nas informações que pretende recolher. Além disso, pode utilizar o **Mostrar linhas de grelha** caixa de verificação para mostrar ou ocultar linhas de grelha que podem ser utilizadas para ajudar a conceber visualmente a página do assistente personalizado.  

 Para efeitos deste exemplo, irá criar uma página do assistente personalizado conforme ilustrado na figura 1.  

 ![QuickStartGuideforUDI](media/QuickStartGuideforUDI.jpg "QuickStartGuideforUDI")  
Figura 1. Página do Assistente de personalizada a ser criado  

 **Figura 1. Página do Assistente de personalizada a ser criado**  

 **Para adicionar controlos a página do assistente personalizada novo**  

1.  Na página biblioteca, clique em **informações do utilizador** página.  

2.  No painel de detalhes, clique o **configurar** separador.  

     A caixa de ferramentas de compilação da página própria e a página do assistente vazio são apresentados.  

3.  Na caixa de ferramentas de compilação da página própria, arraste o **etiqueta** controlo para a página do assistente vazio em aproximadamente as coordenadas seguintes:  

    -   *x* = 30  

    -   *y* = 5  

     O controlo de etiqueta é colocado na página do assistente e o nome *label1*.  

4.  Na página do assistente personalizados, clique em **label1** (o controlo de etiqueta adicionado no passo 3).  

     Este controlo age como um cabeçalho de página do assistente personalizado e descreve a finalidade da página.  

5.  Configurar as propriedades de esquema da **label1** no **esquema** separador a utilizar as informações na tabela 39. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-39-label1-layout-properties"></a>39 de tabela. Propriedades de esquema label1  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**Label** |Informações de utilizador e organização|  
    |**X** |30|  
    |**Y** |5|  

6.  Na caixa de ferramentas de compilação da página própria, arraste o **etiqueta** controlo para a página do assistente vazio em aproximadamente as coordenadas seguintes:  

    -   *x* = 60  

    -   *y* = 60  

     O controlo de etiqueta é colocado na página do assistente e o nome *label2*.  

7.  Na página do assistente personalizados, clique em **label2** (o controlo adicionado no passo anterior).  

     Este controlo atua como uma etiqueta para a caixa de texto utilizada para introduzir o nome de utilizador.  

8.  Configurar as propriedades de esquema da **label2** no **esquema** separador a utilizar as informações na tabela 40. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-40-lable2-layout-properties"></a>40 de tabela. Propriedades de esquema lable2  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**Label** |Nome de utilizador|  
    |**X** |60|  
    |**Y** |60|  

9. Na caixa de ferramentas de compilação do próprio página, clique e arraste o **Textbox** controlo para a página do assistente vazio em aproximadamente as coordenadas seguintes:  

    -   *x* = 60  

    -   *y* = 80  

     O **Textbox** controlo é colocado na página do assistente e o nome *text1*.  

10. Na página do assistente personalizados, clique em **text1** (o controlo adicionado no passo anterior).  

     Este controlo está a caixa de texto utilizada para introduzir o nome de utilizador.  

11. Configurar as propriedades de esquema da **text1** no **esquema** separador a utilizar as informações na tabela 41. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-41-text1-layout-properties"></a>Tabela 41. Propriedades de esquema Text1  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**X** |60|  
    |**Y** |80|  
    |**Width** |400|  

12. Configurar as propriedades de definições da **text1** no **definições** separador a utilizar as informações na tabela 42. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-42-text1-settings-properties"></a>42 de tabela. Propriedades de definições de Text1  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**Nome de variável de sequência de tarefas** |**FullName** |  
    |**Nome a apresentar amigável visível na página de resumo** |Nome de utilizador registado|  

13. Na caixa de ferramentas de compilação da página própria, arraste o **etiqueta** controlo para a página do assistente vazio em aproximadamente as coordenadas seguintes:  

    -   *x* = 60  

    -   *y* = 60  

     O **etiqueta** controlo é colocado na página do assistente e o nome *label3*.  

14. Na página do assistente personalizados, clique em **label3** (o controlo adicionado no passo anterior).  

     Este controlo atua como uma etiqueta para a caixa de combinação utilizada para selecionar o nome de departamento para o utilizador ou a organização.  

15. Configurar as propriedades de esquema da **lable3** no **esquema** separador a utilizar as informações na tabela 43. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-43-lable3-layout-properties"></a>43 de tabela. Propriedades de esquema lable3  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**Label** |Nome da organização ou o departamento|  
    |**X** |60|  
    |**Y** |121|  

16. Na caixa de ferramentas de compilação da página própria, arraste o **Combobox** controlo para a página do assistente vazio em aproximadamente as coordenadas seguintes:  

    -   *x* = 60  

    -   *y* = 140  

     O **Combobox** controlo é colocado na página do assistente e o nome *combo1*.  

17. Na página do assistente personalizados, clique em **combo1** (o controlo adicionado no passo anterior).  

     Este controlo está a caixa de combinação utilizada para selecionar o nome da organização.  

18. Configurar as propriedades de esquema da **combo1** no **esquema** separador a utilizar as informações na tabela 44. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-44-combo1-layout-properties"></a>44 de tabela. Propriedades de esquema combo1  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**X** |60|  
    |**Y** |80|  
    |**Width** |400|  

19. Adicionar itens de dados para as propriedades de esquema de **combo1** no **esquema** separador a utilizar as informações na tabela 45. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-45-combo1-data-items"></a>Tabela 45. Itens de dados de combo1  

    |**Value** |**Valor de apresentação** |  
    |-|-|  
    |**Banco Woodgrove – Nova Iorque cidade** |Banco Woodgrove – Nova Iorque cidade|  
    |**Banco Woodgrove – Dallas** |Banco Woodgrove – Dallas|  
    |**Banco Woodgrove – Chicago** |Banco Woodgrove – Chicago|  
    |**Banco Woodgrove – Seattle** |Banco Woodgrove – Seattle|  

20. Configurar as propriedades de definições da **combo1** no **definições** separador a utilizar as informações na tabela 46. Aceite os valores predefinidos, salvo indicação em contrário.  

    ### <a name="table-46-combo1-settings-properties"></a>46 de tabela. Propriedades de definições de combo1  

    |**Propriedade** |**Value** |  
    |-|-|  
    |**Nome de variável de sequência de tarefas** |**OrgName** |  
    |Nome a apresentar amigável visível na página de resumo|Nome da organização registado|  

21. No Friso, no **home page** separador, clique em **guardar**.  

     O **Guardar ficheiro** é apresentada a caixa de diálogo.  

22. No **Guardar ficheiro** caixa de diálogo, clique em **OK**.  

23. Feche o UDI Wizard Designer.  

###  <a name="UpdateDistributionPointsforMDTFilesPackage"></a>Passo 5-15: Atualizar os pontos de distribuição para o pacote de ficheiros do MDT  
 Depois do ficheiro de configuração do Assistente de UDI UDIWizard_Config.xml, foi atualizado para o pacote de ficheiros MDT no Configuration Manager, atualize os pontos de distribuição para o pacote de ficheiros do MDT. Atualizar os pontos de distribuição copia a versão atualizada do ficheiro UDIWizard_Config.xml para as partilhas de implementação especificadas no pacote.  

 **Para atualizar os pontos de distribuição para o pacote de ficheiros de MDT**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para gestão/pacotes de aplicações/descrição geral.  

4.  No painel de pré-visualização, clique em **ficheiros MDT**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **atualizar pontos de distribuição**.  

     O **do Configuration Manager** abre a caixa de diálogo, notificam que pretender atualizar o pacote em todos os pontos de distribuição.  

6.  No **do Configuration Manager** caixa de diálogo, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

 O Configuration Manager começa a atualizar os pontos de distribuição com as versões mais recentes do ficheiro UDIWizard_Config.xml. Este processo pode demorar vários minutos. Verificar o estado do pacote, até que o **última atualização** valor do Estado de pacote foi atualizado para uma recente data e hora.  

## <a name="step-6-deploy-the-captured-image-of-the-reference-computer-to-the-target-computer"></a>Passo 6: Implementar a imagem capturada do computador de referência para o computador de destino  
 Quando capturar a imagem do computador de referência e criado e configurado a sequência de tarefas, implemente a imagem capturada. Configure o MDT para fornecer todas as definições de configuração necessárias para implementar o computador de destino. Depois de iniciar o processo de implementação, a imagem do computador de referência com o Windows 8.1 é implementada no computador de destino e automaticamente configurada com as definições especificadas.  

 Implemente a imagem capturada por:  

-   Adicionar o computador de destino para a base de dados do site do Configuration Manager, conforme descrito em [passo 6-1: Adicionar o computador de destino para a base de dados do Site do Configuration Manager](#AddTargetComputertoConfigureManagerSite)  

-   Criar uma coleção de computadores que inclui o computador de destino, conforme descrito em [passo 6-2: Criar uma coleção de computadores que inclui o computador de destino](#CreateComputerCollectionThatIncludesTargetComputer)  

-   Implementar a sequência de tarefas que criou anteriormente no processo, conforme descrito em [passo 6-3: Implementar a sequência de tarefas do computador de destino](#DeployTargetComputerTaskSequence)  

-   Iniciar o computador de destino com os dados de arranque de sequências de tarefas, tal como descrito no [passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas](#StartTargetComputerwithTaskSequenceBootableMedia)  

###  <a name="AddTargetComputertoConfigureManagerSite"></a>Passo 6-1: Adicionar o computador de destino para a base de dados do Site do Configuration Manager  
 Para implementar um sistema operativo sem suporte de dados autónomo para um novo computador que o Configuration Manager não gerir atualmente, adicione o novo computador para a base de dados do site do Configuration Manager antes de iniciar o processo de implementação do sistema operativo. O Configuration Manager pode detetar automaticamente computadores na rede que tenha um sistema de operativo de Windows instalado. No entanto, se o computador não tiver nenhum sistema operativo instalado, utilize o Assistente para importar informações de computador para importar as informações do computador novo.  

 **Para adicionar o computador de destino para a base de dados do site do Configuration Manager**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda à descrição geral/dispositivos.  

4.  No Friso, no **home page** separador o **criar** , clique em **importar informações sobre o computador**.  

     O Assistente Importar informações o computador é iniciado.  

5.  Conclua o Assistente de importação de informações de computador, utilizando as informações na tabela 47. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-47-information-for-completing-import-computer-information-wizard"></a>47 de tabela. Informações para concluir o Assistente de importação de informações de computador  

    |Na página do Assistente |Faça isto |  
    |-|-|  
    |**Selecione a origem** |Clique em **importar computador individual**e, em seguida, clique em **seguinte**.|  
    |**Selecione a origem: Único computador** |1.  No **nome do computador**, tipo **WDG-CLI-01**.<br />2.  No *endereço MAC*, tipo ***mac_address*** (onde *mac_address* é o endereço MAC do adaptador de rede principal para o computador de destino, WDG-CLI-01).<br />3.  Clique em **Seguinte**.|  
    |**Selecione a origem: Pré-visualização de dados** |Clique em **Seguinte**.|  
    |**Selecione a origem: Escolher coleção de destino** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para importar o computador é apresentado.|  
    |**Confirmação** |Clique em **Fechar**.|  

 Para obter mais informações sobre como adicionar um novo computador para a base de dados do site do Configuration Manager, consulte a secção "para importar informações sobre o computador para um único computador," na secção, "Como para implementar sistemas operativos no Configuration Manager," na configuração Biblioteca de documentação Manager, que é instalado com o Configuration Manager.  

###  <a name="CreateComputerCollectionThatIncludesTargetComputer"></a>Passo 6-2: Criar uma coleção de computadores que inclui o computador de destino  
 Na consola do Configuration Manager, crie uma coleção que inclua o computador de destino (WDG-CLI-01). Utilize esta coleção de computador mais tarde quando a sequência de tarefas que criou anteriormente no processo de publicidade.  

 **Para criar uma coleção de computadores que inclui o computador de destino**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **ativos e compatibilidade**.  

3.  Em recursos e compatibilidade área de trabalho, aceda a coleções de dispositivos/descrição geral.  

4.  No Friso, no **home page** separador o **criar** , clique em **criar coleção de dispositivos**.  

     Inicia o Assistente para criar coleção de dispositivos.  

5.  Conclua o Assistente de coleção de dispositivos criar utilizando as informações na tabela 48. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-48-information-for-completing-the-create-device-collection-wizard"></a>Tabela 48. Informações para concluir o Assistente de coleção de dispositivos de criação  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |<ol><li>No **nome**, tipo **Microsoft Deployment – Batch 01**.</li><li>No **comentário**, tipo **computadores que estão a ser incluído no lote de computadores implementados primeiro**.</li><li>No **coleção limitado**, clique em **procurar**.<br /><br />     O **procurar coleções** é apresentada a caixa de diálogo. Conclua a caixa de diálogo, efetuando os seguintes passos:<br /><br /> <ol><li>No **procurar coleção** caixa de diálogo **nome**, clique em **todos os sistemas**.</li><li>Clique em **OK**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Regras de Associação** |<ol><li>Clique em **Adicionar regra**e, em seguida, clique em **regra direta**.<br /><br />     O direto associação Assistente para criar regra é iniciado.</li><li>Conclua o direta associação Assistente para criar regra, efetuando os seguintes passos:<br /><br /> <ol><li>Na página de **Boas-vindas**, clique em **Seguinte**.</li><li>No **procurar recursos** na página **classe de recursos**, selecione **recurso do sistema**; na **nome de atributo**, selecione  **Nome**; na **valor**, tipo **WDG-CLI-01**; e, em seguida, clique em **seguinte**.</li><li>No **selecionar recursos** página, selecione **WDG-CLI-01**e, em seguida, clique em **seguinte**. **Nota:**          O processo para adicionar o computador de destino (WDG-CLI-01) para todos os sistemas pode demorar alguns minutos a concluir. Se WDG-CLI-01 não aparecer na lista, repita os passos b e c até WDGCLI01 aparece.</li><li>No **resumo** página, clique em **seguinte**.</li><li>No **conclusão** página, clique em **fechar**.</li></ol></li><li>Clique em **Seguinte**.</li></ol>|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para criar a coleção de dispositivos é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para criar coleções no Configuration Manager," na biblioteca de documentação do Configuration Manager, que é instalado com o Configuration Manager.  

###  <a name="DeployTargetComputerTaskSequence"></a>Passo 6-3: Implementar a sequência de tarefas do computador de destino  
 Na consola do Configuration Manager, implemente a sequência de tarefas que criou anteriormente no processo para os computadores de destino. Implemente a sequência de tarefas na coleção de computadores de destino criado anteriormente no processo.  

 **Para implementar a sequência de tarefas**  

1.  Clique em **iniciar**, aponte para **todos os programas**e, em seguida, aponte para **Microsoft System Center 2012**. Aponte para **do Configuration Manager**e, em seguida, clique em **consola do Configuration Manager**.  

2.  Na consola do Configuration Manager, no painel de navegação, clique em **biblioteca de Software**.  

3.  Na área de trabalho biblioteca de Software, vá para sequências de tarefas/sistemas operativo/descrição geral.  

4.  No painel de pré-visualização, clique em **UDI - implementação do Windows 8.1 destino**.  

5.  No Friso, no **home page** separador o **implementação** , clique em **implementar**.  

     Inicia o Assistente de implementação de Software.  

6.  Conclua o Assistente para implementar Software utilizando as informações na tabela 49. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-49-information-for-completing-the-deploy-software-wizard"></a>49 de tabela. Informações para concluir o Assistente de implementação Software  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Geral** |1.  No **coleção**, clique em **procurar**.<br />2.  No **procurar coleção** caixa de diálogo, clique em **Microsoft Deployment – Batch 01**e, em seguida, clique em **OK**.<br />3.  No **comentário**, tipo **implementar o Windows 8.1 para o primeiro lote de computadores de destino com o UDI**.<br />4.  Clique em **Seguinte**.|  
    |**Definições de implementação** |1.  No **objetivo**, selecione **disponível**.<br />2.  Selecione o **tornar disponível para efetuar o arranque de suportes de dados e PXE** caixa de verificação.<br />3.  Clique em **Seguinte**.|  
    |**Definições de implementação: Agenda** |Clique em **Seguinte**.|  
    |**Definições de implementação: Experiência de utilizador** |Clique em **Seguinte**.|  
    |**Definições de implementação: Alertas** |Clique em **Seguinte**.|  
    |**Definições de implementação: Pontos de distribuição** |Clique em **Seguinte**.|  
    |**Resumo** |Reveja as informações de **detalhes** caixa que forneceu ao concluir as páginas do assistente anterior e, em seguida, clique em **seguinte**.|  
    |**Progresso** |O progresso para criar a implementação de sequência de tarefas é apresentado.|  
    |**Conclusão** |Clique em **Fechar**.|  

 Para obter mais informações, consulte a secção "Como para implementar uma sequência de tarefas," na biblioteca de documentação do Configuration Manager, que é instalado com o Configuration Manager.  

###  <a name="StartTargetComputerwithTaskSequenceBootableMedia"></a>Passo 6-4: Iniciar o computador de destino com o suporte de suportes de sequência de tarefas  
 Inicie o computador de destino (WDG-CLI-01) com a tarefa sequência suportes de dados criado anteriormente no processo. Esta média inicia o Windows PE no computador de referência e inicia o processo de MDT. No final do processo do MDT, Windows 8.1 é implementado no computador de destino.  

> [!NOTE]
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows.  

 **Para iniciar o computador de destino com o suporte de suportes de sequência de tarefas**  

1.  Inicie WDG-CLI-01 com a tarefa sequência suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de sequência de tarefas.  

2.  Conclua o Assistente de sequência de tarefas utilizando as informações na tabela 50. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-50-information-for-completing-the-task-sequence-wizard"></a>50 de tabela. Informações para concluir o Assistente de sequência de tarefas  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Bem-vindo ao Assistente de sequência de tarefas** |No **palavra-passe**, tipo **P@ssw0rd**e, em seguida, clique em **seguinte**.|  
    |**Selecione uma sequência de tarefas** |Na caixa de lista, selecione **UDI - implementação do Windows 8.1 destino**e, em seguida, clique em **seguinte**.|  

     No passo de sequência de tarefas apropriada, o Assistente de implementação de UDI é iniciado.  

3.  Conclua o Assistente de implementação de UDI utilizando as informações na tabela 51. Aceite os valores predefinidos exceto indicação em contrário.  

    ### <a name="table-51-information-for-udi-deployment-wizard"></a>51 de tabela. Informações de Assistente de implementação de UDI  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Welcome** |Clique em **Seguinte**.|  
    |**Informações do utilizador** |1.  No **nome de utilizador,** tipo **Woodgrove Bank Chicago empregado**.<br />2.  No **organização ou o nome de departamento**, selecione **Woodgrove Bank – Chicago**.<br />3.  Clique em **Seguinte**.|  
    |**BitLocker** |Clique em **Seguinte**.|  
    |**Volume** |Clique em **Seguinte**.|  
    |**Selecione o destino** |Clique em **Seguinte**.|  
    |**Preparação de implementação** |1.  Reveja as verificações de configuração e certifique-se de que o estado de todas as verificações estão definidos com **êxito**.<br />2.  Clique em *Seguinte*.|  
    |**Detalhes do novo computador** |1.  No **nome do computador**, tipo **WDG-CLI-01**. **Nota:**      Em cenários de computadores desconhecidos, os utilizadores foi possível alterar o nome do computador para o valor adequado.<br />2.  No **nome de utilizador**, tipo **MDT2013\Administrator**.<br />3.  No **palavra-passe** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />4.  Clique em **Seguinte**.|  
    |**Palavra-passe de administrador** |1.  No **palavra-passe de administrador** e **Confirmar palavra-passe**, tipo **P@ssw0rd**.<br />2.  Clique em **Seguinte**.|  
    |**Afinidade dispositivo / utilizador** |Selecione o **utilizador primário do conjunto** caixa de verificação e, em seguida, clique em **seguinte**.|  
    |**Idioma** |Clique em **Seguinte**.|  
    |**Instalar os programas** |Certifique-se de que o **Microsoft Office Professional Plus 2010 – x86** caixa de verificação está selecionada e, em seguida, clique em **seguinte**.|  
    |Resumo|Reveja as informações que forneceu enquanto a concluir as páginas do assistente anterior e, em seguida, clique em **concluir**.|  

 **Para monitorizar o processo de implementação de computador de referência utilizando o Deployment Workbench**  

1.  No WDG-MDT-01, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para a partilha de implementação de partilhas/MDT implementação Workbench/implementação (C:\DeploymentShare$)/Monitoring.  

3.  No painel de detalhes, veja o processo de implementação para WDG-REF-01.  

4.  No painel de ações, clique periodicamente **atualizar**.  

     O estado do processo de implementação é atualizado no painel de detalhes. Continue a monitorizar o processo de implementação até que o processo esteja concluído.  

5.  No painel de detalhes, clique em **WDG-REF-01**.  

6.  No painel ações, clique em **propriedades**.  

     O **WDG-REF-01 propriedades** é apresentada a caixa de diálogo.  

7.  No **WDG-REF-01 propriedades** caixa de diálogo a **identidade** separador, ver as informações de monitorização fornecidas sobre o processo de implementação, conforme descrito na tabela 52.  

    ### <a name="table-52-monitoring-information-about-the-deployment-process"></a>52 de tabela. Informações sobre o processo de implementação de monitorização  

    |**Informações** |**Descrição** |  
    |-|-|  
    |**ID** |Identificador exclusivo para o computador que está a ser implementado.|  
    |**Nome do computador** |O nome do computador que está a ser implementado.|  
    |Estado de implementação|O estado atual do computador que está a ser implementado; o estado pode ser um dos seguintes:<br /><br /> -   **Executar**. A sequência de tarefas é bom estado de funcionamento e em execução.<br />-   **Não foi possível**. A sequência de tarefas falha e o processo de implementação foi bem-sucedido.<br />-   **Concluir**. A sequência de tarefas foi concluída.<br />-   **Responder**. A sequência de tarefas não tiver atualizado o seu estado nas últimas quatro horas e é prestada, tentados.|  
    |**Passo** |O passo de sequência tarefas atual a ser executado.|  
    |**Progresso** |O progresso global da sequência de tarefas. A barra de progresso indica quantos passos de sequência de tarefas terem sido executados fora do número total de passos de sequência de tarefas.|  
    |**Iniciar** |A hora de início do processo de implementação.|  
    |**End** |A hora em que terminou o processo de implementação.|  
    |**Elapsed** |O período de tempo, o processo de implementação tem estado em execução ou demorou a execução se foi concluído o processo de implementação.|  
    |**Erros** |O número de erros encontrados durante o processo de implementação.|  
    |**Avisos** |O número de avisos durante o processo de implementação.|  
    |**Ambiente de trabalho remoto** |Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota com o computador que está a ser implementado através da funcionalidade de ambiente de trabalho remoto do Windows. Este método parte do princípio de que:<br /><br /> -O sistema operativo de destino está em execução e tiver ativada de suporte de ambiente de trabalho remoto<br />-   **mstsc.exe** está no caminho do **Nota:**  Este botão é sempre visível, mas pode não ser capaz de estabelecer uma sessão de ambiente de trabalho remoto, se o computador monitorizado está a executar o Windows PE, não foi concluída a instalação do sistema operativo de destino ou não tem ativada a funcionalidade de ambiente de trabalho remoto.|  
    |**Ligação de VM** |Este botão permite-lhe estabelecer uma ligação de ambiente de trabalho remota para uma VM em execução no hyper-v. Este método parte do princípio de que:<br /><br /> -A implementação está a ser efetuada a uma VM em execução no Hyper-V<br />-   **vmconnect.ex**i está localizado na pasta %ProgramFiles%\Hyper-V **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que os componentes de integração do Hyper-V estão em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Controlo remoto de daRT** |Este botão permite-lhe estabelecer uma sessão de controlo remoto utilizando a funcionalidade Visualizador remoto na DaRT.<br /><br /> Este método parte do princípio de que:<br /><br /> -DaRT ter sido implementado no computador de destino e estiver em execução<br />-   **DartRemoteViewer.exe** está localizado na pasta %ProgramFiles%\Microsoft DaRT 7\v7 **Nota:**  Este botão aparece quando ZTIGather.wsf Deteta que DaRT está em execução no computador monitorizado. Caso contrário, este botão não serão visível.|  
    |**Atualizar automaticamente estas informações a cada 10 segundos** |Caixa de verificação que controla se as informações na caixa de diálogo é automaticamente atualizadas. Se a caixa de verificação:<br /><br /> -Selecionado, as informações são atualizadas cada 10 segundos<br />-Limpo, as informações não são automaticamente atualizadas e têm de ser manualmente atualizadas utilizando o **atualizar** agora no botão|  
    |**Atualizar neste momento** |Este botão imediatamente atualiza as informações apresentadas na caixa de diálogo.|  

8.  No **WDG-REF-01 propriedades** caixa de diálogo, clique em **OK**.  

9. Feche o Deployment Workbench.  

 **Para monitorizar o processo de implementação de computador de referência utilizando o cmdlet Get-MDTMonitorData**  

1.  No WDG-MDT-01, clique em **iniciar**, aponte para **ferramentas administrativas**e, em seguida, clique em **módulos do Windows PowerShell**.  

     Abre a linha de comandos de módulos do Windows PowerShell.  

2.  Criar uma unidade do Windows PowerShell que utiliza o fornecedor do PowerShell do MDT, executando o [New-PSDrive](http://technet.microsoft.com/library/hh849829.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

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

 Após a conclusão do processo de implementação, o Windows 8.1 é iniciado pela primeira vez e o **boas-vindas** separador o **implementação concluída** é apresentada a caixa de diálogo. O **boas-vindas** separador apresenta informações úteis sobre a implementação e fornece informações de contacto no caso de ocorrer problemas com a implementação.  

 Reveja as informações de **resumo de implementação** e **aplicações instaladas** separadores para verificar se o Windows 8.1 e o Office Professional Plus 2010 foram corretamente instalados. Quando tiver terminado de rever estas tabelas, clique em **iniciar Windows** para iniciar sessão do Windows 8.1 pela primeira vez.  

> [!NOTE]
>  Aplicações do Configuration Manager não são apresentadas no **aplicações instaladas** separador. Em vez disso, estes são detetadas quando o utilizador inicia sessão no computador de destino pela primeira vez.
