---
title: Verificações de pré-requisitos
titleSuffix: Configuration Manager
description: Referência dos pré-requisitos específicos verifica a existência de atualizações do Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f17be653d206fd453cdafa4de159804f2fca816
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456690"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista de verificações de pré-requisitos para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre as verificações de pré-requisitos que são executados quando instalar ou atualizar o Configuration Manager. Para obter mais informações, consulte [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker).  



##  <a name="BKMK_Security"></a> Direitos de segurança  


### <a name="security-rights-errors"></a>Direitos de segurança: Erros

#### <a name="administrator-rights-on-central-administration-site"></a>Direitos de administrador no site de administração central 
*Aplica-se a: Site primário*

A conta de utilizador que executa a configuração do Configuration Manager possui **administrador** direitos no servidor do site de administração central.

#### <a name="administrative-rights-on-expand-primary-site"></a>Direitos administrativos no site primário de expansão 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a conta de utilizador que executa a configuração tem **administrador** direitos no servidor do site primário autónomo.

#### <a name="administrative-rights-on-site-system"></a>Direitos administrativos no sistema de sites 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

A conta de utilizador que executa a configuração do Configuration Manager possui **administrador** direitos no servidor do site.

#### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Direitos administrativos do servidor de site de administração central em expandir o site primário 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a conta de computador do servidor do site de administração central tem **administrador** direitos no servidor do site primário autónomo.

#### <a name="connection-to-sql-server-on-central-administration-site"></a>Ligação ao SQL Server no site de administração central 
*Aplica-se a: Site primário*

A conta de utilizador que executa a configuração do Configuration Manager no site primário para adesão a uma hierarquia existente possui a **sysadmin** função na instância do SQL Server para o site de administração central.

#### <a name="site-server-computer-account-administrative-rights"></a>Direitos de conta de computador servidor do site administrativos 
*Aplica-se a: Site primário, o servidor de base de dados do site*

A conta de computador do servidor de site possui **administrador** direitos no ponto de gestão e servidor de SQL.

#### <a name="sql-server-sysadmin-rights"></a>Direitos de administrador do sistema do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

A conta de utilizador que executa a configuração do Configuration Manager tem os **sysadmin** função na instância do SQL Server que selecionou para a instalação de banco de dados do site. Esta verificação também falha quando o programa de configuração não consegue aceder à instância do SQL Server verificar as permissões.

#### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Direitos de administrador do sistema do SQL Server para o site de referência 
*Aplica-se a: Servidor de base de dados do site*

A conta de utilizador que executa a configuração do Configuration Manager tem os **sysadmin** função na instância de função do SQL Server que selecionou como a base de dados do site de referência. SQL Server **sysadmin** são necessárias permissões de função para modificar a base de dados do site.


### <a name="security-rights-warnings"></a>Direitos de segurança: Avisos

#### <a name="site-system-to-sql-server-communication"></a>Sistema de sites para comunicação do SQL Server  
*Aplica-se a: Site secundário, o ponto de gestão*

A conta que configurou para executar o serviço do SQL Server para a instância de base de dados do site tem um nome principal de serviço válido (SPN) nos serviços de domínio do Active Directory. Registe um SPN válido no Active Directory para suportar a autenticação Kerberos.

#### <a name="sql-server-security-mode"></a>Modo de segurança do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

SQL Server está configurado para segurança de autenticação do Windows.



##  <a name="BKMK_Dependencies"></a> Dependências

### <a name="dependencies-errors"></a>Dependências: Erros

#### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapeamentos de migração ativos no site primário de destino 
*Aplica-se a: Site de administração central*

Não existem não existem mapeamentos de migração ativos nos sites primários.

#### <a name="active-replica-mp"></a>MP de réplica ativa 
*Aplica-se a: Site primário*

Existe uma réplica de ponto de gestão do Active Directory.

#### <a name="bits-enabled"></a>BITS ativado 
*Aplica-se a: Ponto de gestão*

Serviço de transferência inteligente em segundo plano (BITS) está instalado no ponto de gestão. Esta verificação pode falhar por um dos seguintes motivos: 
- BITS não está instalado  
- O componente de compatibilidade WMI do IIS 6.0 para o IIS 7.0 não está instalado no servidor ou no anfitrião IIS remoto  
- A configuração não foi possível verificar as definições de IIS remoto. Componentes comuns do IIS não estão instaladas no servidor do site.  

#### <a name="case-insensitive-collation-on-sql-server"></a>Agrupamento de maiúsculas e minúsculas no SQL Server 
*Aplica-se a: Servidor de base de dados do site*

Instalação do SQL Server utiliza um agrupamento de maiúsculas e minúsculas, tal como **SQL_Latin1_General_CP1_CI_AS**.

#### <a name="check-existing-stand-alone-primary-site-for-version-and-site-code"></a>Verificar o site primário autónomo existente para a versão e código do site 
*Aplica-se a: Site de administração central, site primário*

O site primário que pretende expandir é um site primário autónomo. Ele tem a mesma versão do Configuration Manager, mas um código de site diferente do site de administração central para ser instalado.

#### <a name="check-for-incompatible-collection-references"></a>Verificação de referências de coleção incompatíveis 
*Aplica-se a: Site de administração central*

Durante uma atualização, as coleções referenciam apenas outras coleções do mesmo tipo.

#### <a name="client-version-on-management-point-computer"></a>Versão de cliente no computador do ponto de gestão 
*Aplica-se a: Ponto de gestão*

Estiver a instalar o ponto de gestão num servidor que não tem uma versão diferente do cliente do Configuration Manager instalado.

#### <a name="dedicated-sql-server-instance"></a>Instância dedicada do SQL Server 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

Configurou uma instância dedicada do SQL Server para alojar a base de dados do site do Configuration Manager. 

Se a outro site utilizar a instância, tem de selecionar uma instância diferente para o novo site. Também pode desinstalar o outro site ou mover a respetiva base de dados para uma instância diferente do SQL Server.

#### <a name="existing-configuration-manager-server-components-on-server"></a>Componentes de servidor do Configuration Manager existentes no servidor 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

Um servidor do site ou função do sistema de sites já não está instalada no servidor selecionado para instalação do site.

#### <a name="firewall-exception-for-sql-server"></a>Exceção de firewall para SQL Server 
*Aplica-se a: Site de administração central, o site primário, o site secundário, o ponto de gestão*

A Firewall do Windows está desativada ou não existe uma exceção relevante da Firewall do Windows para o SQL Server. 

Permitir Sqlservr.exe ou as portas TCP necessárias para ser acessado remotamente. Por predefinição, o SQL Server escuta na porta TCP 1433 e o SQL Server Service Broker (SSB) utiliza a porta TCP 4022.

#### <a name="iis-service-running"></a>Serviço IIS em execução 
*Aplica-se a: Ponto de gestão, ponto de distribuição*

O IIS é instalado e em execução no servidor para o ponto de gestão ou ponto de distribuição.

#### <a name="match-collation-of-expand-primary-site"></a>Corresponder agrupamento do site primário de expansão 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a base de dados do site para o site primário autónomo tem o mesmo agrupamento que a base de dados do site no site de administração central.

#### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Biblioteca Microsoft diferencial compressão remota (RDC) registrada 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

A biblioteca RDC está registada no servidor do site do Configuration Manager.

#### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

Verifica a versão do Windows Installer. 

Quando esta verificação falha, a configuração não conseguiu verificar a versão ou a versão instalada não satisfaz os requisitos mínimos do Windows Installer 4.5.

#### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versão mínima do .NET Framework para a consola do Configuration Manager 
*Aplica-se a: Consola do Configuration Manager*

Microsoft .NET Framework 4.0 está instalado no computador da consola do Configuration Manager. 

#### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versão mínima do .NET Framework para o servidor de site do Configuration Manager 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

.NET framework 3.5 está instalado ou ativado no servidor de site do Configuration Manager. 

#### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Versão mínima do .NET Framework para instalação de edição do SQL Server Express para o site secundário do Configuration Manager 
*Aplica-se a: Site secundário*

.NET framework 4.0 está instalado ou ativado no servidor de site secundário do Configuration Manager. Esta versão é exigido pelo SQL Server Express.

#### <a name="parent-database-collation"></a>Agrupamento de base de dados principal 
*Aplica-se a: Site primário, o site secundário*

O agrupamento da base de dados do site corresponde ao agrupamento da base de dados do site principal. Todos os sites de uma hierarquia têm de utilizar o mesmo agrupamento de bases de dados.

#### <a name="primary-fqdn"></a>FQDN primário 
*Aplica-se a: Site de administração central, o site primário, o site secundário, o servidor de base de dados do site*

O nome NetBIOS do computador corresponde ao nome do anfitrião local no nome de domínio completamente qualificado (FQDN).

#### <a name="required-sql-server-collation"></a>Agrupamento do SQL Server necessário 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

A instância do SQL Server está configurada para utilizar o **SQL_Latin1_General_CP1_CI_AS** agrupamento. 

Se a base de dados do site do Configuration Manager já está instalada, esta verificação também se aplica à base de dados. Para obter informações sobre como alterar a sua instância do SQL Server e agrupamentos de base de dados, consulte [suporte de unicode e agrupamento do SQL](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support). 

Se estiver a utilizar um sistema operacional chinês e necessite de suporte GB18030, esta verificação não se aplica. Para obter mais informações sobre como ativar o suporte GB18030, consulte [suporte internacional](/sccm/core/plan-design/hierarchy/international-support).

#### <a name="setup-source-folder"></a>Pasta de origem de configuração 
*Aplica-se a: Site secundário*

A conta de computador para o site secundário tem as seguintes permissões para a pasta de origem de configuração e a partilha: 
- **Leitura** permissões do sistema de ficheiros NTFS
- **Leitura** as permissões de partilha 

> [!Note]  
> Se utilizar partilhas administrativas, por exemplo, C$ e D$, a conta de computador do site secundário tem de ser um **administrador** no servidor.  

#### <a name="setup-source-version"></a>Versão da origem de configuração 
*Aplica-se a: Site secundário*

A versão do Configuration Manager na pasta de origem especificado para a instalação de site secundário corresponde à versão do Configuration Manager do site primário.

#### <a name="site-code-in-use"></a>Código do site em utilização 
*Aplica-se a: Site primário* o código do site especificado não está já em utilização na hierarquia do Configuration Manager. Especifique um código de site exclusivo para este site.

#### <a name="sms-provider-in-same-domain-as-site-server"></a>Fornecedor de SMS no mesmo domínio que o servidor do site 
*Aplica-se a: Fornecedor de SMS*

Qualquer instância do fornecedor de SMS está no mesmo domínio que o servidor do site.

#### <a name="sql-server-edition"></a>Edição do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

SQL Server no site não SQL Server Express.

#### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express no site secundário 
*Aplica-se a: Site secundário*

SQL Server Express pode instalar com êxito no servidor do site secundário.

#### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server no servidor do site secundário 
*Aplica-se a: Site secundário*

SQL Server está instalado no servidor do site secundário. Não é possível instalar o SQL Server num sistema de sites remoto de um site secundário.

> [!Warning]  
> Esta verificação aplica-se apenas quando é selecionada a opção de configuração utilizar uma instância existente do SQL Server.  

#### <a name="sql-server-service-running-account"></a>Conta de execução de serviço do SQL Server 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

A conta de início de sessão do serviço do SQL Server não é uma conta de utilizador local ou **serviço LOCAL**. 

Configurar o serviço do SQL Server para utilizar uma conta de domínio válida **serviço de rede**, ou **sistema LOCAL**.

#### <a name="sql-server-tcp-port"></a>Porta de TCP do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

TCP está ativado para a instância do SQL Server e está definido para utilizar uma porta estática.

#### <a name="sql-server-version"></a>Versão do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

Uma versão suportada do SQL Server está instalada no servidor de base de dados do site especificado. 

Para obter mais informações, consulte [suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).

#### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Do ponto de sincronização do Asset Intelligence no site primário expandido 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a função de ponto de sincronização do Asset Intelligence não está instalada no site primário autónomo.

#### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Ponto de Endpoint Protection no site primário expandido 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a função de ponto de Endpoint Protection não está instalada no site primário autónomo.

#### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune Connector no site primário expandido 
*Aplica-se a: Site de administração central*

Quando expande um site primário para uma hierarquia, a função do Microsoft Intune Connector não está instalada no site primário autónomo.

#### <a name="usmt-installed"></a>USMT instalado 
*Aplica-se a: Site de administração central, site primário (apenas autónomo)*

O componente ferramenta de migração de perfil do usuário (USMT) do Windows Assessment and Deployment Kit (ADK) para Windows está instalado.

#### <a name="validate-fqdn-of-sql-server"></a>Validar o FQDN do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

Especificou um FQDN válido para o computador do SQL Server.

#### <a name="verify-central-administration-site-version"></a>Verificar a versão do site de administração central 
*Aplica-se a: Site primário*

O site de administração central tem a mesma versão do Configuration Manager.

#### <a name="windows-deployment-tools-installed"></a>Ferramentas de implementação do Windows instaladas 
*Aplica-se a: Fornecedor de SMS*

O componente de ferramentas de implantação do Windows do Windows ADK está instalado.

#### <a name="windows-failover-cluster"></a>Cluster de Ativação Pós-falha do Windows 
*Aplica-se a: Servidor do site, ponto de gestão, ponto de distribuição*

Servidor com o servidor do site, ponto de gestão ou funções de ponto de distribuição não fazem parte de um Cluster do Windows.

A partir da versão 1810, o processo de configuração do Configuration Manager já não bloqueia a instalação da função de servidor de site num computador com a função do Windows para o Clustering de ativação pós-falha. SQL Always On requer esta função, por isso, anteriormente não foi possível colocar a base de dados no servidor do site. Com esta alteração, pode criar um site de elevada disponibilidade com menos servidores com o SQL Always On e um servidor de site em modo passivo. Para obter mais informações, consulte [opções de elevada disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

#### <a name="windows-pe-installed"></a>PE do Windows instalado 
*Aplica-se a: Fornecedor de SMS*

O componente de ambiente de pré-instalação do Windows (PE) do Windows ADK está instalado.


### <a name="dependencies-warnings"></a>Dependências: Avisos

#### <a name="administrative-rights-on-distribution-point"></a>Direitos administrativos no ponto de distribuição 
*Aplica-se a: Ponto de distribuição*

A conta de utilizador que executa a configuração possui **administrador** direitos no ponto de distribuição.

#### <a name="administrative-rights-on-management-point"></a>Direitos administrativos no ponto de gestão 
*Aplica-se a: Ponto de gestão, ponto de distribuição*

A conta de computador do servidor do site tem **administrador** direitos no ponto de gestão e ponto de distribuição.

#### <a name="administrative-share-site-system"></a>Partilha administrativa (sistema de sites) 
*Aplica-se a: Ponto de gestão*

As partilhas administrativas necessárias estão presentes no computador do sistema de site.

#### <a name="application-compatibility"></a>Compatibilidade de aplicativos 
*Aplica-se a: Site de administração central, site primário*

Aplicações atuais são compatíveis com o esquema de aplicações.

#### <a name="bits-installed"></a>BITS instalado 
*Aplica-se a: Ponto de gestão*

O serviço de transferência inteligente em segundo plano (BITS) está instalado e habilitado no IIS.

#### <a name="configuration-for-sql-server-memory-usage"></a>Configuração para utilização de memória do SQL Server 
*Aplica-se a: Servidor de base de dados do site*

SQL Server está configurado para utilização ilimitada da memória. Configure a memória do SQL Server para ter um limite máximo.

#### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Exceção de firewall para SQL Server (site primário autónomo) 
*Aplica-se a: Site primário (apenas autónomo)*

A Firewall do Windows está desativada ou não existe uma exceção relevante da Firewall do Windows para o SQL Server. 

Permitir Sqlservr.exe ou as portas TCP necessárias para ser acessado remotamente. Por predefinição, o SQL Server escuta na porta TCP 1433 e o Server Service Broker (SSB) utiliza a porta TCP 4022.

#### <a name="firewall-exception-for-sql-server-for-management-point"></a>Exceção de firewall para SQL Server para o ponto de gestão 
*Aplica-se a: Ponto de gestão*

A Firewall do Windows está desativada ou não existe uma exceção relevante da Firewall do Windows para o SQL Server.

#### <a name="iis-https-configuration"></a>Configuração IIS HTTPS 
*Aplica-se a: Ponto de gestão, ponto de distribuição*

Web site do IIS tem enlaces para o protocolo de comunicação HTTPS. 

Ao instalar as funções de sites que necessitam do HTTPS, configure os enlaces de site do IIS no servidor especificado com um certificado de infraestrutura de chaves públicas (PKI) válido.

#### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60) 
*Aplica-se ao site de Administração Central, o site primário, o site secundário, o consola do Configuration Manager, o ponto de gestão, o ponto de distribuição*

Verifica se o MSXML 6.0 ou uma versão posterior está instalada.

#### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 no servidor do site 
*Aplica-se a: Site primário com o conector do Exchange*

Windows PowerShell 2.0 ou uma versão posterior está instalada no servidor do site para o Configuration Manager Exchange Connector. 

#### <a name="remote-connection-to-wmi-on-secondary-site"></a>Ligação remota ao WMI no site secundário 
*Aplica-se a: Site secundário*

A configuração pode estabelecer uma ligação remota ao WMI no servidor do site secundário.

#### <a name="sql-server-process-memory-allocation"></a>Alocação de memória de processo do SQL Server 
*Aplica-se a: Servidor de base de dados do site* 

O SQL Server reserva um mínimo de 8 GB de memória para o site de administração central e site primário e um mínimo de 4 GB de memória para o site secundário.

Para obter mais informações, consulte [como configurar as opções de memória com o SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd).

> [!NOTE]  
> Esta verificação não é aplicável ao SQL Server Express num site secundário. Esta edição é limitada a 1 GB de memória reservada.  

#### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versão de SO do sistema de sites não suportada para atualização 
*Aplica-se a: Site primário, o site secundário*

Funções de sistema de sites além dos pontos de distribuição são instalados em servidores que executam o Windows Server 2012 ou posterior.

Para obter mais informações, consulte [sistemas operativos suportados para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> Esta verificação não é possível resolver o estado das funções de sistema de sites instaladas no Azure ou para o armazenamento na cloud utilizadas pelo Microsoft Intune. Ignore os avisos para estas funções como falsos positivos.

#### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verifique se as permissões do servidor de site para publicar no Active Directory 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

A conta de computador do servidor do site tem **controlo total** permissões para o **System Management** contentor no domínio do Active Directory. 

Para obter mais informações, consulte [preparar o Active Directory para publicação de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> Se verificar manualmente as permissões, pode ignorar este aviso.

#### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v1.1 
*Aplica-se a: Site primário, a consola do Configuration Manager*

O WinRM 1.1 está instalado no servidor do site primário ou o computador da consola do Configuration Manager para executar a consola de gestão fora de banda. 

Para obter mais informações sobre como transferir o WinRM 1.1, consulte [artigo de suporte 936059](https://support.microsoft.com/help/936059).

#### <a name="wsus-on-site-server"></a>WSUS no servidor do site 
*Aplica-se a: Site de administração central, site primário*

Uma versão suportada do Windows Server Update Services (WSUS) está instalada no servidor do site. 

Quando utiliza um ponto de atualização de software num servidor diferente do servidor do site, tem de instalar a consola de administração do WSUS no servidor do site. Para obter mais informações sobre o WSUS, consulte [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).

#### <a name="pending-configuration-item-policy-updates"></a>Atualizações de política de item de configuração pendente 
<!--SCCMDocs-pr issue 2814-->
*Aplica-se a: Site primário*

A partir da versão 1806, se estiver a atualizar da versão 1706 ou posterior, poderá ver este aviso se tiver muitas implementações de aplicações e, pelo menos, um deles requer aprovação. 

Tem duas opções:  

- Ignorar o aviso e continuar com a atualização. Esta ação faz com que mais processamento no servidor do site durante a atualização à medida que processa as políticas. Também poderá ver mais processador carregar no ponto de gestão após a atualização.  

- Rever uma das aplicações que tenha não existem requisitos ou um requisito de sistema operacional específico. Pré-processe alguns da carga no servidor do site naquele momento. Revisão **objreplmgr.log**e, em seguida, monitorizar o processador no ponto de gestão. Depois do processamento estiver concluído, atualize o site. Ainda haverá algum processamento adicional após a atualização, mas menos do que se ignorar o aviso com a primeira opção.  



##  <a name="BKMK_Requirements"></a> Requisitos do sistema  

### <a name="system-requirements-errors"></a>Requisitos de sistema: Erros

#### <a name="server-service-is-running"></a>Serviço de servidor está em execução 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

O serviço de servidor é iniciado e em execução.

#### <a name="domain-membership"></a>Associação ao domínio 
*Aplica-se a: Site de administração central, o site primário, o site secundário, o fornecedor de SMS, o SQL Server*

O computador do Configuration Manager é um membro de um domínio Windows.

#### <a name="free-disk-space-on-site-server"></a>Espaço livre em disco no servidor do site 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

Para instalar o servidor do site, tem de ter, pelo menos, 15 GB de espaço livre em disco. Se instalar o fornecedor de SMS no mesmo servidor, ele precisa de 1 GB de espaço livre adicional.

#### <a name="pending-system-restart"></a>Reinício de sistema pendente 
*Aplica-se a: Site de administração central, site primário, site secundário, consola do Configuration Manager, o fornecedor de SMS, o SQL Server, ponto de gestão, ponto de distribuição*

Antes de executar a configuração, outro programa necessita que o servidor seja reiniciado.

A partir da versão 1810, esta verificação é mais resiliente. Para ver se o computador está num Estado de reinício pendente, ela verifica as localizações de registo seguinte:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="read-only-domain-controller"></a>Controlador de domínio só de leitura 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

Servidores de base de dados do site e servidores de sites secundários não são suportados num controlador de domínio só de leitura (RODC). 

Para obter mais informações, consulte o artigo de Support da Microsoft sobre [problemas ao instalar o SQL Server num controlador de domínio](https://support.microsoft.com/help/2032911).

#### <a name="site-server-fqdn-length"></a>Comprimento do FQDN do servidor do site 
*Aplica-se a: Site de administração central, o site primário, o site secundário*

O comprimento do FQDN do servidor do site.

#### <a name="unsupported-os-for-configuration-manager-console"></a>Sistema operacional sem suporte para a consola do Configuration Manager
*Aplica-se a: Consola do Configuration Manager*

Instale a consola do Configuration Manager em computadores que executem uma versão suportada do SO. 

Para obter mais informações, consulte a [versões de SO suportado para a consola do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

#### <a name="unsupported-os-for-site-server"></a>Sistema operacional sem suporte para o servidor de site 
*Aplica-se a: Site de administração central, o site primário, o site secundário, o consola do Configuration Manager, o ponto de gestão, o ponto de distribuição*

O servidor executa uma versão suportada do SO. 

Para obter mais informações, consulte [servidores do sistema de sites de versões de SO suportado para o Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

#### <a name="verify-database-consistency"></a>Verificar a consistência da base de dados 
*Aplica-se a: Site de administração central, site primário*

Verifica a consistência da base de dados do site no SQL Server.  


### <a name="system-requirements-warnings"></a>Requisitos de sistema: Avisos

#### <a name="active-directory-domain-functional-level"></a>Nível funcional do Active Directory do domínio 
*Aplica-se a: Site de administração central, site primário*

O nível funcional de domínio do Active Directory é um mínimo de Windows Server 2008 R2.

#### <a name="domain-membership"></a>Associação ao domínio 
*Aplica-se a: Ponto de gestão, ponto de distribuição*

O computador do Configuration Manager é um membro de um domínio Windows.

#### <a name="ntfs-drive-on-site-server"></a>Unidade NTFS no servidor do site 
*Aplica-se a: Site primário*

A unidade de disco está formatada com o sistema de ficheiros NTFS. Para melhor segurança, instale os componentes de servidor do site em unidades de disco formatadas com o sistema de ficheiros NTFS.

#### <a name="schema-extensions"></a>Extensões de esquema 
*Aplica-se a: Site de administração central, site primário*

O esquema do Active Directory foi expandido. Se ele tiver expandido, a versão das extensões de esquema que foram utilizados. 

O Configuration Manager não precisa de extensões de esquema do Active Directory para a instalação de servidor do site. A Microsoft recomenda-los para a utilização total de todas as funcionalidades do Configuration Manager. Para obter mais informações sobre as vantagens de expandir o esquema, consulte [preparar o Active Directory para publicação de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).

#### <a name="bkmk_changetracking"></a> Limpeza de controlo de alterações do SQL
*Aplica-se a: Servidor de base de dados do site*

A partir da versão 1810, certifique-se a base de dados do site tem um registo de segurança de dados de controlo de alterações do SQL.<!--SCCMDocs-pr issue 3023-->  

Certifique-se manualmente essa verificação ao executar um procedimento armazenado diagnóstico da base de dados do site. Primeiro, crie uma [ligação de diagnóstico](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) à sua base de dados do site. O método mais simples consiste em utilizar o Editor de consultas do SQL Server Management Studio e ligue-se ao `admin:<instance name>`. 

Numa janela de consulta de ligação de administrador dedicada, execute os seguintes comandos:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Consoante o tamanho da base de dados e o tamanho do registo de segurança, pode executar este procedimento armazenado em alguns minutos ou várias horas. Quando a consulta é concluída, verá duas secções de dados relacionados com o registo de segurança. Primeiro olhar **CT_Days_Old**. Este valor indica a idade (dias) da entrada na tabela syscommittab mais antiga. Deve ser de cinco dias, que é o valor predefinido do Configuration Manager. Não altere este valor predefinido. Às vezes de processamento intensivo de dados ou a replicação, a entrada mais antiga em syscommittab poderia ser mais de cinco dias. Se este valor for superior a sete dias, execute uma limpeza manual de dados de controlo de alterações.  

Para limpar as dados de controlo de alterações, execute o seguinte comando na ligação de administração dedicada: 

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Este comando inicia uma limpeza de syscommittab e todas as tabelas de lado associados. Pode ser executada em vários minutos ou várias horas. Para monitorizar o progresso, consultar o **vlogs da** vista. Para ver o progresso atual, execute a seguinte consulta: 

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

<!-- #### SQL Native Client
<!--SCCMDocs-pr issue 3094->
*Applies to: Central administration site, primary site, secondary site*

A supported version of the SQL Native Client. Starting in version 1810, the minimum version is 11.4.7001.0. 

This SQL Native Client version supports TLS 1.2. For more information, see the following articles:
- [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  
- [How to enable TLS 1.2 for Configuration Manager](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager)  
 -->