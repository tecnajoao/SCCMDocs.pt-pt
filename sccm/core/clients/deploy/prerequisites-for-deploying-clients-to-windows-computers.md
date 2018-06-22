---
title: Pré-requisitos de implementação do cliente Windows
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para implementar o cliente do Configuration Manager em computadores Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf929e605a7d44ac2f29226177d3ab962eb8fba0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336855"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Pré-requisitos para implementar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementar clientes do Configuration Manager no seu ambiente tem as seguintes dependências externas e dependências de produto. Além disso, cada método de implementação de clientes tem as suas próprias dependências, que deverão ser satisfeitas para que as instalações de clientes tenham êxito.  

  Certifique-se que reveja também [configurações suportadas](../../../core/plan-design/configs/supported-configurations.md) para confirmar que os dispositivos satisfazem os requisitos de SO de cliente do Configuration Manager e mínimos de hardware.  

 Para obter informações sobre os pré-requisitos do cliente do Configuration Manager para Linux e UNIX, consulte [planear a implementação do cliente para computadores Linux e UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  Os números de versão do software apresentados neste artigo listam apenas os números de versão mínima necessários.  



##  <a name="BKMK_prereqs_computers"></a> Pré-requisitos para clientes de computador  
 Utilize as seguintes informações para determinar os pré-requisitos de instalação nos computadores cliente do Configuration Manager.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|||  
|-|-|  
|Windows Installer versão 3.1.4000.2435|Necessário para suportar a utilização de ficheiros de atualização do Windows Installer (.msp) para pacotes e atualizações de software.|  
|[KB2552033](https://go.microsoft.com/fwlink/p/?LinkId=240048)|Instale esta correção nos servidores do site com o Windows Server 2008 R2 quando a instalação push do cliente estiver ativada.|  
|Serviço de Transferência Inteligente em Segundo Plano Microsoft (BITS) versão 2.5|Necessário para permitir transferências de dados otimizadas entre o computador cliente e os sistemas de sites do Configuration Manager. O BITS não é transferido automaticamente durante a instalação do cliente. Quando o BITS é instalado, normalmente é necessário reiniciar o computador para concluir a instalação.<br /><br /> A maioria dos sistemas operativos incluem o BITS caso contrário (por exemplo, Windows Server 2003 R2 SP2), deve instalar o BITS antes de instalar o cliente do Configuration Manager.|  
|Programador de Tarefas Microsoft|Ative este serviço no cliente para a instalação de cliente que pretende concluir.|  

### <a name="bkmk_ExternalDependencies"></a> Dependências externas ao Configuration Manager e transferidas automaticamente durante a instalação  
 O cliente do Configuration Manager tem algumas dependências externas potenciais. Estas dependências dependem do sistema operativo e do software instalado no computador cliente.  

 Se estas dependências forem necessárias para concluir a instalação do cliente, serão automaticamente instaladas com o software de cliente.  

|||  
|-|-|  
|Windows Update Agent versão 7.0.6000.363|Necessário para o Windows suportar a deteção e implementação de atualizações.|  
|Microsoft Core XML Services (MSXML) versão 6.20.5002 ou posterior|Necessário para suportar o processamento de documentos XML no Windows.|  
|Compressão de Diferencial Remota da Microsoft (RDC)|Necessário para otimizar a transmissão de dados através da rede.|  
|Microsoft Visual C++ 2013 Redistributable versão 12.0.21005.1|Necessário para suportar operações de cliente. Quando esta atualização é instalada em computadores cliente, poderá ser necessário reiniciar o computador para concluir a instalação.|  
|Microsoft Visual C++ 2005 Redistributable versão 8.0.50727.42|Para a versão 1606 e anterior, necessária para suportar operações do Microsoft SQL Server Compact.|  
|APIs Windows Imaging 6.0.6001.18000|Necessário para permitir que o Configuration Manager para gerir ficheiros de imagem (. wim) do Windows.|  
|Microsoft Policy Platform 1.2.3514.0|Necessário para permitir aos clientes avaliar as definições de compatibilidade.|  
|Microsoft Silverlight 5.1.41212.0|Necessário para suportar a experiência de utilizador do Web site do Catálogo de Aplicações. A partir do Configuration Manager 1802, Silverlight está já não é instalado automaticamente. A funcionalidade principal do catálogo de aplicações está agora incluída no Centro de Software. Suporte para as extremidades de web site do catálogo de aplicações com a primeira atualização lançada após 1 de Junho de 2018.<!--1356195-->|  
|Microsoft .NET Framework versão 4.5.2|Necessário para suportar operações de cliente. Instalado automaticamente no computador cliente se não tiver o Microsoft .NET Framework versão 4.5 ou posterior instalado. Para obter mais informações, veja [Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2](#dotNet).|  
|Componentes do Microsoft SQL Server Compact 3.5 SP2|Necessários para armazenar informações relacionadas com operações de cliente.|  
|Componentes do Microsoft Windows Imaging|Requeridos pelo Microsoft .NET Framework 4.0 para Windows Server 2003 ou Windows XP SP2 para computadores de 64 bits.|
|Cliente de software de PC do Microsoft Intune|Não é possível executar o cliente de software de PC do Intune e o cliente do Configuration Manager no mesmo computador. Certifique-se de que o cliente do Intune é removido antes de instalar o cliente do Configuration Manager.|

####  <a name="dotNet"></a> Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2  

> [!NOTE]  
>  Em 12 de Janeiro de 2016, suporte para o .NET 4.0, 4.5 e 4.5.1 expiraram. Para obter mais informações, consulte [FAQ de política do ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  

 Pode ser necessário um reinício para concluir a instalação do Microsoft .NET Framework versão 4.5.2. O utilizador verá uma **reinício necessário** notificação no tabuleiro do sistema. Cenários comuns que necessitam que os computadores cliente sejam reiniciados:  

-   Serviços ou aplicações .NET estão em execução no computador.  

-   Uma ou mais atualizações de software necessárias para a instalação do .NET estão em falta.  

-   Um reinício do computador está pendente desde a instalação anterior de atualizações do software .NET Framework.  

 Após a instalação do .NET Framework 4.5.2, poderão ser instaladas posteriormente atualizações adicionais ao mesmo, que podem necessitar de reinícios adicionais do computador.  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 Para obter mais informações, consulte [determinar as funções de sistema de sites para clientes](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|Ponto de gestão|Embora um ponto de gestão não é necessário para implementar o cliente do Configuration Manager, tem de ter um ponto de gestão para transferir informações entre computadores cliente e servidores do Configuration Manager. Sem um ponto de gestão, não é possível gerir computadores cliente.|  
|Ponto de distribuição|O ponto de distribuição é uma função do sistema de sites opcional mas recomendada para implementação de cliente. Todos os pontos de distribuição alojam os ficheiros de origem do cliente, que permitem aos computadores localizar o ponto de distribuição mais próximo a partir das quais transferir os ficheiros de origem do cliente durante a implementação do cliente. Se o site não possuir um ponto de distribuição, os computadores transferirão os ficheiros de origem do cliente a partir do respetivo ponto de gestão.|  
|Ponto de estado de contingência|O ponto de estado de contingência é uma função do sistema de sites opcional mas recomendada para implementação de cliente. O ponto de estado de contingência controla a implementação de cliente, permitindo aos computadores do site do Configuration Manager para enviar mensagens de estado quando não conseguirem comunicar com um ponto de gestão.|  
|Ponto do Reporting Services|O ponto do Reporting Services é uma função do sistema de sites opcional mas recomendada, que permite apresentar relatórios relacionados com a implementação e gestão de clientes. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Dependências do método de instalação  
 Os pré-requisitos seguintes são específicos para os vários métodos de instalação de cliente.  

#### <a name="client-push-installation"></a>Instalação push do cliente  

   -   As contas de instalação push do cliente servem para ligar a computadores para instalação do cliente, sendo especificadas no separador **Contas** da caixa de diálogo **Propriedades da Instalação Push do Cliente**. A conta tem de ser membro do grupo de administradores local no computador de destino.  

         Se não especificar uma conta de instalação de push de cliente, é utilizada a conta de computador do servidor do site.  

   -   Computador no qual está a instalar o cliente terá ter sido detetado pelo menos um método de deteção do Configuration Manager.  

   -   O computador tem uma partilha ADMIN$.  

   -   **Ativar a instalação de push de cliente para os recursos atribuídos** tem de ser selecionada no **propriedades de instalação Push do cliente** caixa de diálogo, se pretender emitir automaticamente o cliente do Configuration Manager detetados recursos.  

   -   O computador cliente terá de conseguir contactar um ponto de distribuição ou um ponto de gestão para transferir os ficheiros de suporte.  


Tem de ter as permissões de segurança seguintes para instalar o cliente do Configuration Manager utilizando push de cliente:  

   -   Para configurar a conta de instalação Push do cliente: **Modificar** e permissão de leitura para o **Site** objeto.  

   -   Para utilizar o push de cliente para instalar o cliente em coleções, dispositivos e consultas: **Modificar recurso** e **leitura** permissão para o objeto coleção.  


A função de segurança **Administrador de Infraestrutura** inclui as permissões necessárias para gerir a instalação push do cliente.  


#### <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

   -   Se ainda não foi expandido o esquema do Active Directory ou se estiver a instalar os clientes de outra floresta, as propriedades de instalação para CCMSetup.exe têm de ser aprovisionadas no registo do computador utilizando a política de grupo. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   O cliente do Configuration Manager tem de ser publicado para o ponto de atualização de software.  

   -   O computador cliente terá de conseguir contactar um ponto de distribuição ou um ponto de gestão para poder transferir os ficheiros de suporte.  


Para as permissões de segurança necessárias para gerir atualizações de software do Configuration Manager, consulte [pré-requisitos para atualizações de software](../../../sum/plan-design/prerequisites-for-software-updates.md).  


#### <a name="group-policy-based-installation"></a>Instalação baseada em política de grupo  

   -   Se ainda não foi expandido o esquema do Active Directory ou se estiver a instalar os clientes de outra floresta, as propriedades de instalação para CCMSetup.exe têm de ser aprovisionadas no registo do computador utilizando a política de grupo. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   O computador cliente terá de conseguir contactar um ponto de gestão para transferir os ficheiros de suporte.  


#### <a name="logon-script-based-installation"></a>Instalação baseada no script de início de sessão  

O computador cliente terá de conseguir contactar um ponto de distribuição ou um ponto de gestão para poder transferir os ficheiros de suporte. A menos que tenha especificado CCMSetup.exe com a propriedade da linha de comandos **ccmsetup /source**.  


#### <a name="manual-installation"></a>Instalação manual  

O computador cliente terá de conseguir contactar um ponto de distribuição ou um ponto de gestão para poder transferir os ficheiros de suporte. A menos que tenha especificado CCMSetup.exe com a propriedade da linha de comandos **ccmsetup /source**.  


#### <a name="microsoft-intune-mdm-installation"></a>Instalação de MDM do Microsoft Intune

 - Requer uma subscrição do Microsoft Intune e as licenças adequadas.  

 - Requer o dispositivo tem acesso à internet, mesmo que não está baseada na internet.  

 - Consoante o caso de utilização, também pode exigir uma ou ambas as seguintes tecnologias de:  

     - Azure Active Directory  

     - Gateway de gestão de nuvem  


#### <a name="workgroup-computer-installation"></a>Instalação do computador do grupo de trabalho  

Para poder aceder aos recursos no domínio do servidor de site do Configuration Manager, a conta de acesso de rede tem de ser configurada para o site.  

Para obter mais informações sobre como configurar a conta de acesso de rede, consulte o [conceitos fundamentais da gestão de conteúdos](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalação baseada em distribuição de software (apenas para atualizações)  

   -   Se ainda não foi expandido o esquema do Active Directory ou se estiver a instalar os clientes de outra floresta, as propriedades de instalação para CCMSetup.exe têm de ser aprovisionadas no registo do computador utilizando a política de grupo. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   O computador cliente terá de conseguir contactar um ponto de distribuição ou um ponto de gestão para transferir os ficheiros de suporte.  


Para as permissões de segurança necessárias para atualizar o cliente do Configuration Manager utilizando a gestão de aplicações, consulte [segurança e privacidade para gestão de aplicações](../../../apps/plan-design/security-and-privacy-for-application-management.md).  


#### <a name="automatic-client-upgrades"></a>Atualizações automáticas de clientes  

Terá de ser membro da função de segurança **Administrador Total** para configurar atualizações automáticas de clientes.  


### <a name="firewall-requirements"></a>Requisitos da firewall  

Se existir uma firewall entre os servidores de sistema de sites e os computadores em que pretende instalar o cliente do Configuration Manager, consulte [Firewall do Windows e definições de porta para clientes](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Pré-requisitos para clientes de dispositivos móveis  

Quando instalar o cliente do Configuration Manager em dispositivos móveis e inscrevê-los, utilize estas informações para determinar os pré-requisitos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

-   Uma autoridade de certificação (AC) empresarial da Microsoft com modelos de certificado para implementar e gerir os certificados necessários para dispositivos móveis.  

     A AC emissora terá de aprovar automaticamente os pedidos de certificados dos utilizadores de dispositivos móveis durante o processo de inscrição.  

     Para obter mais informações sobre os requisitos de certificado, consulte [segurança e privacidade para perfis de certificado](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   Um grupo de segurança que contenha os utilizadores que podem inscrever os respetivos dispositivos móveis.  

     Este grupo de segurança é utilizado para configurar o modelo de certificado que é utilizado durante a inscrição de dispositivos móveis.  

-   Opcional mas recomendado: um alias DNS (registo CNAME) com o nome **ConfigMgrEnroll**. Configure este alias para o nome do servidor de proxy do ponto de inscrição.  

     Este DNS alias é necessário para suportar a deteção automática para o serviço de inscrição. Se não configurar este registo DNS, os utilizadores terão de especificar manualmente o nome do ponto de proxy de registo como parte do processo de inscrição.  

-   Funções do sistema de sites do ponto de dependências de função do sistema de sites para os computadores que executam o ponto de registo e o proxy de inscrição.  

     Veja [Sistemas operativos suportados para servidores do sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 Para obter mais informações, consulte [determinar as funções de sistema de sites para clientes](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Ponto de gestão que é configurado para ligações de cliente HTTPS e ativado para dispositivos móveis  

     Um ponto de gestão é sempre necessário para instalar o cliente do Configuration Manager em dispositivos móveis. Para além dos requisitos de configuração de HTTPS e ativado para dispositivos móveis, o ponto de gestão tem de ser configurado com um FQDN de internet e aceitar ligações de cliente a partir da internet.  

-   Ponto de registo e ponto proxy de registo  

     Um ponto proxy de registo gere os pedidos de inscrição de dispositivos móveis e o ponto de registo conclui o processo de inscrição. O ponto de registo terá de estar na mesma floresta do Active Directory que o servidor de site, mas o ponto proxy de registo poderá estar noutra floresta.  

-   Definições de cliente para a inscrição de dispositivos móveis  

     Configure as definições de cliente para permitir que os utilizadores inscrevam dispositivos móveis e configurem pelo menos um perfil de inscrição.  

-   Ponto do Reporting Services  

     O ponto do Reporting Services é uma função do sistema de sites opcional mas recomendada, que permite apresentar relatórios relacionados com a inscrição de dispositivos móveis e a gestão de clientes.  

     Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Para configurar a inscrição de dispositivos móveis, terá de possuir as seguintes permissões de segurança:  

    -   Para adicionar, modificar e eliminar as funções de sistema de sites de inscrição: **Modificar** permissão para o **Site** objeto.  

    -   Para configurar as definições de cliente para inscrição: Predefinições de cliente necessitam **modificar** permissão para o **Site** objetos e definições personalizadas de cliente requerem **agente do cliente** permissões.  

     A função de segurança **Administrador Total** inclui as permissões necessárias para configurar as funções do sistema de sites de inscrição.  

     Para gerir os dispositivos móveis inscritos, terá de possuir as seguintes permissões de segurança:  

    -   Para apagar ou extinguir um dispositivo móvel: **Eliminar recurso** para o **coleção** objeto.  

    -   Para cancelar a eliminação ou extinção de comando: **Eliminar recurso** para o **coleção** objeto.  

    -   Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o **coleção** objeto.  

    -   Bloqueio a remoto ou reposição do código de acesso num dispositivo móvel: **Modificar** recurso para o **coleção** objeto.  

     A função de segurança **Administrador de Operações** inclui as permissões necessárias para gerir dispositivos móveis.  

     Para obter mais informações sobre como configurar permissões de segurança, consulte [Noções básicas da administração baseada em funções](../../../core/understand/fundamentals-of-role-based-administration.md) e [configurar a administração baseada em funções](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Requisitos da firewall  
Os dispositivos de rede intervenientes, tais como routers e firewalls, e a Firewall do Windows, se for caso disso, têm de permitir o tráfego associado ao registo do dispositivo móvel:  

-   Entre os dispositivos móveis e o ponto de proxy de inscrição: HTTPS (por predefinição, TCP 443)  

-   Entre o ponto de proxy de inscrição e o ponto de inscrição: HTTPS (por predefinição, TCP 443)  


Se utilizar um servidor Web proxy, este tem de ser configurado para túnel SSL; o protocolo de bridge SSL não é suportado para dispositivos móveis.  
