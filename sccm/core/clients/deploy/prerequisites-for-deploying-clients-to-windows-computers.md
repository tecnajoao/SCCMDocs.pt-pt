---
title: Pré-requisitos de implementação do cliente Windows
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para implementar o cliente do Configuration Manager para computadores Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11474f54aaf7a9afe13d411b0dd469abb1eef963
ms.sourcegitcommit: c2c44329f1f9a2e6c14095360b4fc4aafabc27f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51694948"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Pré-requisitos para implementar clientes em computadores Windows no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementar clientes do Configuration Manager no seu ambiente tem as seguintes dependências externas e dependências no produto. Além disso, cada método de implementação de clientes tem as suas próprias dependências, que deverão ser satisfeitas para que as instalações de clientes tenham êxito.  

Para obter mais informações sobre os requisitos de sistema operacional para o cliente do Configuration Manager e mínimos de hardware, consulte [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations).  

> [!NOTE]  
>  Os números de versão do software apresentados neste artigo listam apenas os números de versão mínima necessários.  



##  <a name="BKMK_prereqs_computers"></a> Pré-requisitos para clientes do Windows  

Utilize as seguintes informações para determinar os pré-requisitos de instalação do cliente do Configuration Manager em dispositivos Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Componente|Descrição|  
|---|---|  
|Windows Installer versão 3.1.4000.2435|Necessário para suportar a utilização de ficheiros de atualização do Windows Installer (.msp) para pacotes e atualizações de software.|  
|Serviço de Transferência Inteligente em Segundo Plano Microsoft (BITS) versão 2.5|Necessário para permitir transferências de dados otimizadas entre o computador cliente e sistemas de sites do Configuration Manager. BITS não é transferido automaticamente durante a instalação de cliente. Quando o BITS é instalado em computadores, normalmente requer um reinício para concluir a instalação.<br /><br /> A maioria dos sistemas de operativos incluem o BITS. Caso contrário, instale o BITS antes de instalar o cliente do Configuration Manager.|  
|Programador de Tarefas Microsoft|Ative este serviço no cliente para a instalação de cliente para concluir.|  


### <a name="bkmk_ExternalDependencies"></a> Dependências externas ao Configuration Manager e transferidas automaticamente durante a instalação  

O cliente do Configuration Manager tem dependências externas. Estas dependências dependem da versão do SO e o software instalado no computador cliente.  

Se o cliente requer estas dependências para concluir a instalação, ele automaticamente instala-los.  

|Componente|Descrição|  
|---|---|  
|Windows Update Agent versão 7.0.6000.363|Necessário para o Windows suportar a deteção e implementação de atualizações.|  
|Microsoft Core XML Services (MSXML) versão 6.20.5002 ou posterior|Necessário para suportar o processamento de documentos XML no Windows.|  
|Compressão de Diferencial Remota da Microsoft (RDC)|Necessário para otimizar a transmissão de dados através da rede.|  
|Microsoft Visual C++ 2013 Redistributable versão 12.0.21005.1|Necessário para suportar operações de cliente. Ao instalar esta atualização nos computadores cliente, ele pode exigir um reinício para concluir a instalação.|  
|Microsoft Visual C++ 2005 Redistributable versão 8.0.50727.42|Para a versão 1606 e anterior, necessário para suportar operações do Microsoft SQL Server Compact.|  
|APIs Windows Imaging 6.0.6001.18000|Necessário para permitir que o Configuration Manager para gerir ficheiros de imagem (. wim) do Windows.|  
|Microsoft Policy Platform 1.2.3514.0|Necessário para permitir aos clientes avaliar as definições de compatibilidade.|  
|Microsoft Silverlight 5.1.41212.0|Necessário para suportar a experiência de utilizador do Web site do Catálogo de Aplicações. A partir de 1802 do Gestor de configuração, o cliente não instala automaticamente Silverlight. A funcionalidade primária do catálogo de aplicações agora está incluída no Centro de Software. Suporte para o catálogo de aplicações Web site termina na versão 1806.<!--1356195-->|  
|Microsoft .NET Framework versão 4.5.2|Necessário para suportar operações de cliente. Instalado automaticamente no computador cliente se ele não tem o Microsoft .NET Framework versão 4.5 ou posterior instalado. Para obter mais informações, veja [Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2](#dotNet).|  
|Componentes do Microsoft SQL Server Compact 4.0 SP1|Necessários para armazenar informações relacionadas com operações de cliente.|  


####  <a name="dotNet"></a> Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2  

> [!NOTE]  
>  .NET 4.0, 4.5 e 4.5.1 já não são suportadas. Para obter mais informações, consulte [FAQ de política do ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework versão 4.5.2 pode exigir um reinício para concluir a instalação. O utilizador vê uma **reinício necessário** notificação na Bandeja do sistema. Os seguintes cenários comuns necessitam que os computadores de cliente para reiniciar:  

-   Serviços ou aplicações .NET estão em execução no computador.  

-   Uma ou mais atualizações de software necessárias para a instalação do .NET estão em falta.  

-   Um reinício do computador está pendente desde a instalação anterior de atualizações do software .NET Framework.  


Depois do .NET Framework 4.5.2 é instalado, ele pode exigir atualizações adicionais. Estas atualizações posteriores podem exigir a reinícios de computador adicionais.  


### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

Para obter mais informações, consulte [determinar as funções de sistema de sites para clientes](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

|Componente|Descrição|  
|---|---|  
|Ponto de gestão|Para implementar o cliente do Configuration Manager, não necessita de um ponto de gestão. Os clientes exigem de um ponto de gestão para transferir informações com o site. Sem um ponto de gestão, é possível gerir computadores cliente.|  
|Ponto de distribuição|O ponto de distribuição é uma função de sistema de sites opcional mas recomendado para a gestão e implementação do cliente. Todos os pontos de distribuição alojam os ficheiros de origem do cliente. Os clientes localizam o mais próximo ponto de distribuição a partir das quais transferir os ficheiros de origem durante a implementação de cliente ou atualizar. Se o site não tiver um ponto de distribuição, computadores transferem os ficheiros de origem do cliente a partir do respetivo ponto de gestão.|  
|Ponto de estado de contingência|O ponto de estado de contingência é uma função do sistema de sites opcional mas recomendada para implementação de cliente. O ponto de estado de contingência controla a implementação do cliente e permite aos computadores do site do Configuration Manager para enviar mensagens de estado quando não conseguirem comunicar com um ponto de gestão.|  
|Ponto do Reporting Services|O ponto do reporting services é uma função de sistema de sites opcional mas recomendado. Apresenta relatórios relacionados com a implementação e gestão. Para obter mais informações, consulte [relatórios no Configuration Manager](/sccm/core/servers/manage/reporting).|  


### <a name="installation-method-dependencies"></a>Dependências do método de instalação  

Os pré-requisitos seguintes são específicos para os vários métodos de instalação de cliente.  

#### <a name="client-push-installation"></a>Instalação push do cliente  

   -   O site utiliza contas de instalação push do cliente para ligar a computadores para instalar o cliente. Especificar essas contas no **contas** separador das propriedades de instalação Push do cliente. A conta tem de ser membro do grupo de administradores local no computador de destino.  

         Se não especificar uma conta de instalação push do cliente, o servidor de site utiliza a sua conta de computador.  

   -   O site tem de detetar o computador no qual está a instalar o cliente. É necessário pelo menos um método de deteção do Configuration Manager.  

   -   O computador tem uma partilha ADMIN$.  

   -   Para enviar automaticamente o cliente do Configuration Manager para os recursos detetados, selecione a opção para **ativar instalação push do cliente para os recursos atribuídos** em Propriedades de instalação Push do cliente.  

   -   O computador cliente precisa para comunicar com um ponto de distribuição ou um ponto de gestão para transferir os ficheiros de origem.  

   -   A partir da versão 1806, quando precisar que a autenticação mútua do Kerberos, os clientes devem ser numa floresta do Active Directory fidedigna. Kerberos no Windows depende do Active Directory para autenticação mútua.<!--1358204-->  


Para utilizar o push de cliente, terá das seguintes permissões de segurança:  

   -   Para configurar a conta de instalação push do cliente: **Modificar** e **leitura** permissão para o **Site** objeto.  

   -   Para utilizar o push de cliente para instalar o cliente em coleções, dispositivos e consultas: **Modificar recurso** e **leitura** permissão para o **coleção** objeto.  


O **administrador de infraestrutura** função de segurança predefinida inclui as permissões necessárias para gerenciar as instalações de push de cliente.  


#### <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

   -   Se ainda não tiver expandido o esquema do Active Directory, ou se estiver a instalar os clientes de outra floresta, utilize a política de grupo para os parâmetros de instalação de aprovisionamento para CCMSetup.exe. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Publicar o cliente do Configuration Manager para o ponto de atualização de software.  

   -   Para transferir os ficheiros de origem, o computador cliente tem de comunicar com um ponto de distribuição ou um ponto de gestão.  


Para as permissões de segurança necessárias para gerir atualizações de software do Configuration Manager, consulte [pré-requisitos para atualizações de software](/sccm/sum/plan-design/prerequisites-for-software-updates).  


#### <a name="group-policy-based-installation"></a>Instalação baseada em política de grupo  

   -   Se ainda não tiver expandido o esquema do Active Directory, ou se estiver a instalar os clientes de outra floresta, utilize a política de grupo para os parâmetros de instalação de aprovisionamento para CCMSetup.exe. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Para transferir os ficheiros de origem, o computador cliente tem de comunicar com um ponto de distribuição ou um ponto de gestão.  


#### <a name="logon-script-based-installation"></a>Instalação baseada no script de início de sessão  

Para transferir os ficheiros de origem, o computador cliente tem de comunicar com um ponto de distribuição ou um ponto de gestão. A menos que tenha especificado CCMSetup.exe com o seguinte parâmetro de linha de comandos: `ccmsetup /source`  


#### <a name="manual-installation"></a>Instalação manual  

Para transferir os ficheiros de origem, o computador cliente tem de comunicar com um ponto de distribuição ou um ponto de gestão. A menos que tenha especificado CCMSetup.exe com o seguinte parâmetro de linha de comandos: `ccmsetup /source`  


#### <a name="microsoft-intune-mdm-installation"></a>Instalação do Microsoft Intune MDM

 - Requer uma subscrição do Microsoft Intune e as licenças adequadas.  

 - Requer o dispositivo tem acesso à internet, mesmo que não seja baseado na internet.  

 - Dependendo do caso de utilização, também pode necessitar de uma ou ambas as seguintes tecnologias:  

     - O Azure Active Directory  

     - Gateway de gestão na cloud  


#### <a name="workgroup-computer-installation"></a>Instalação do computador do grupo de trabalho  

Para acessar recursos no domínio do servidor de site do Configuration Manager, configure uma conta de acesso de rede para o site.  

Para obter mais informações sobre como configurar a conta de acesso de rede, consulte a [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalação baseada em distribuição de software (apenas para atualizações)  

   -   Se ainda não tiver expandido o esquema do Active Directory, ou se estiver a instalar os clientes de outra floresta, utilize a política de grupo para os parâmetros de instalação de aprovisionamento para CCMSetup.exe. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).   

   -   Para transferir os ficheiros de origem, o computador cliente tem de comunicar com um ponto de distribuição ou um ponto de gestão.  


Para as permissões de segurança necessárias para atualizar o cliente do Configuration Manager utilizando a gestão de aplicações, consulte [segurança e privacidade para gestão de aplicações](/sccm/apps/plan-design/security-and-privacy-for-application-management).  


#### <a name="automatic-client-upgrades"></a>Atualizações automáticas de clientes  

Terá de ser membro da função de segurança **Administrador Total** para configurar atualizações automáticas de clientes.  


### <a name="firewall-requirements"></a>Requisitos de firewall  

Se existir uma firewall entre os servidores de sistema de sites e os computadores em que pretende instalar o cliente do Configuration Manager, consulte [Firewall do Windows e definições de porta para clientes](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Pré-requisitos para clientes de dispositivos móveis  

Quando instala o cliente do Configuration Manager em dispositivos móveis e inscrevê-los, utilize estas informações para determinar os pré-requisitos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

-   Uma autoridade de certificação (AC) empresarial da Microsoft com modelos de certificado para implementar e gerir os certificados necessários para dispositivos móveis.  

     A AC emissora terá de aprovar automaticamente os pedidos de certificados dos utilizadores de dispositivos móveis durante o processo de inscrição.  

     Para obter mais informações sobre os requisitos de certificado, consulte [segurança e privacidade para perfis de certificado](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles).  

-   Um grupo de segurança que contenha os utilizadores que podem inscrever os respetivos dispositivos móveis.  

     Este grupo de segurança é utilizado para configurar o modelo de certificado que é utilizado durante a inscrição de dispositivos móveis.  

-   Opcional mas recomendado: um alias de DNS (registo CNAME) com o nome **ConfigMgrEnroll**. Configure este alias para o nome do servidor de ponto de proxy de registo.  

     Alias esta DNS é necessário para suportar a deteção automática para o serviço de inscrição. Se não configurar este registo DNS, os utilizadores devem especificar manualmente o nome do ponto de proxy de registo como parte do processo de inscrição.  

-   Funções de sistema de sites do ponto de dependências de função de sistema de sites para os computadores que executam o ponto de registo e o proxy de inscrição.  

     Para obter mais informações, consulte [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  


### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

Para obter mais informações, consulte [determinar as funções de sistema de sites para clientes](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

-   Ponto de gestão que tenha configurado para ligações de cliente HTTPS e ativado para dispositivos móveis  

     Um ponto de gestão é sempre necessário para instalar o cliente de Configuration Manager em dispositivos móveis. Além dos requisitos de configuração de HTTPS e ativado para dispositivos móveis, o ponto de gestão tem de ser configurado com um FQDN de internet e aceitar ligações de cliente a partir da internet.  

-   Ponto de registo e ponto proxy de registo  

     Um ponto proxy de registo gere os pedidos de inscrição de dispositivos móveis e o ponto de registo conclui o processo de inscrição. O ponto de registo terá de estar na mesma floresta do Active Directory que o servidor de site, mas o ponto proxy de registo poderá estar noutra floresta.  

-   Definições de cliente para a inscrição de dispositivos móveis  

     Configure as definições de cliente para permitir que os utilizadores inscrevam dispositivos móveis e configurem pelo menos um perfil de inscrição.  

-   Ponto do Reporting Services  

     O ponto do Reporting Services é uma função do sistema de sites opcional mas recomendada, que permite apresentar relatórios relacionados com a inscrição de dispositivos móveis e a gestão de clientes.  

     Para obter mais informações, consulte [relatórios no Configuration Manager](/sccm/core/servers/manage/reporting).  

-   Para configurar a inscrição de dispositivos móveis, terá de possuir as seguintes permissões de segurança:  

    -   Para adicionar, modificar e eliminar as funções de sistema de sites de inscrição: **Modificar** permissão para o **Site** objeto.  

    -   Para configurar as definições de cliente para inscrição: Predefinições de cliente necessitam **Modify** permissão para o **Site** objeto e as definições personalizadas de cliente necessitam **agente do cliente** permissões.  

     O **administrador total** função de segurança predefinida inclui as permissões necessárias para configurar as funções de sistema de sites de inscrição.  

     Para gerir os dispositivos móveis inscritos, terá de possuir as seguintes permissões de segurança:  

    -   Para apagar ou extinguir um dispositivo móvel: **Eliminar recurso** para o **coleção** objeto.  

    -   Para cancelar uma eliminação ou extinção de comando: **Eliminar recurso** para o **coleção** objeto.  

    -   Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o **coleção** objeto.  

    -   Bloqueio de remoto ou reposição do código de acesso num dispositivo móvel: **Modificar** recurso para o **coleção** objeto.  

     O **administrador de operações** função de segurança predefinida inclui as permissões necessárias para gerir dispositivos móveis.  

     Para obter mais informações sobre como configurar permissões de segurança, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration) e [configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="firewall-requirements"></a>Requisitos de firewall  

Os dispositivos de rede intervenientes, tais como routers e firewalls, e a Firewall do Windows, se for caso disso, têm de permitir o tráfego associado ao registo do dispositivo móvel:  

-   Entre os dispositivos móveis e o ponto de proxy de registo: HTTPS (por predefinição, TCP 443)  

-   Entre o ponto de proxy de registo e o ponto de inscrição: HTTPS (por predefinição, TCP 443)  


Se utilizar um servidor web proxy, tem de estar configurada para o protocolo de túnel SSL. Protocolo de bridge SSL não é suportado para dispositivos móveis.  
