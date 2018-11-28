---
title: Noções básicas de segurança
titleSuffix: Configuration Manager
description: Saiba mais sobre as camadas de segurança no Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1a7d8e6fe1824ab2a7fe3cfb6f89965a4b5800c0
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456078"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Noções básicas de segurança para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo resume os seguintes componentes fundamentais de segurança de qualquer ambiente do Configuration Manager:
- [Camadas de segurança](#bkmk_layers)
- [Administração baseada em funções](#bkmk_rba)
- [Proteger pontos finais de cliente](#bkmk_endpoints)
- [Grupos e contas do Configuration Manager](#bkmk_accounts)
- [Privacidade](#bkmk_privacy)

## <a name="bkmk_layers"></a> Camadas de segurança

Segurança para o Configuration Manager é composta pelos seguintes camadas: 
- [Segurança de rede e sistema operacional do Windows](#bkmk_layer-windows)
- [Infraestrutura de rede: firewalls, deteção de intrusões, infraestrutura de chaves públicas (PKI)](#bkmk_layer-network)
- [Controlos de segurança do Configuration Manager](#bkmk_layer-cm)
- [Fornecedor de SMS](#bkmk_layer-provider)
- [Permissões de base de dados do site](#bkmk_layer-db)

#### <a name="bkmk_layer-windows"></a> Segurança de rede e sistema operacional do Windows
A primeira camada é fornecida por recursos de segurança do Windows para o sistema operacional e a rede. Essa camada inclui os seguintes componentes:  

-   Partilha de ficheiros para transferir ficheiros entre componentes do Configuration Manager  

-   Listas de Controlo de Acesso (ACL) para ajudar a proteger ficheiros e chaves de registo  

-   Internet Protocol Security (IPsec) para ajudar a proteger as comunicações  

-   Política de grupo para definir a política de segurança  

-   Permissões de modelo de objeto de componente (DCOM) distribuído para aplicações distribuídas, como a consola do Configuration Manager  

-   os Serviços de Domínio do Active Directory para armazenar as entidades de segurança  

-   Segurança, incluindo alguns grupos que o Configuration Manager cria durante a configuração da conta do Windows  

#### <a name="bkmk_layer-network"></a> Infraestrutura de rede

Componentes de segurança adicionais, como firewalls e deteção de intrusões, ajudar a fornecer defesa para a todo o ambiente. Os certificados emitidos por setor implementações de infraestrutura de chaves públicas (PKI) padrão fornecem autenticação, assinatura e encriptação.  

#### <a name="bkmk_layer-cm"></a> Controlos de segurança do Configuration Manager

Além da segurança fornecida pelo Windows server a infraestrutura de rede, o Configuration Manager controla o acesso ao seu console e os recursos de várias formas. Por predefinição, apenas os administradores locais têm direitos aos ficheiros e chaves do Registro que requer a consola do Configuration Manager em computadores em que instalar.  

#### <a name="bkmk_layer-provider"></a> Fornecedor de SMS

A próxima camada de segurança baseia-se no acesso através do WMI (Windows Management Instrumentation), nomeadamente o Fornecedor de SMS. O fornecedor de SMS é um componente do Configuration Manager que concede um utilizador de acesso para consultar a base de dados do site para obter informações. Por predefinição, o acesso ao fornecedor é restringido aos membros do grupo Admins de SMS local. Este grupo no primeiro contém apenas o utilizador que instalou o Configuration Manager. Para conceder permissão a outras contas no repositório CIM (Common Information Model) e no fornecedor de SMS, adicione-as ao grupo de Administradores de SMS.  

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. <!--1357013-->  

Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="bkmk_layer-db"></a> Permissões de base de dados do site

A camada final de segurança baseia-se nas permissões para objetos da base de dados do site. Por predefinição, a conta Sistema Local e a conta de utilizador que utilizou para instalar o Configuration Manager podem administrar todos os objetos da base de dados do site. Conceder e restringir as permissões a utilizadores administrativos adicionais na consola do Configuration Manager utilizando a administração baseada em funções.  



## <a name="bkmk_rba"></a> Administração baseada em funções  

 O Configuration Manager utiliza a administração baseada em funções para ajudar a proteger objetos, como coleções, implementações e sites. Este modelo de administração define e gere de forma centralizada as definições de acesso de segurança de toda a hierarquia para todos os sites e definições do site. 

 Um administrador atribui *funções de segurança* para os utilizadores administrativos e permissões de grupo. As permissões estão ligadas a diferentes tipos de objeto do Configuration Manager, por exemplo, para criar ou alterar as definições de cliente. 

 *Âmbitos de segurança* agrupam instâncias específicas de objetos que um utilizador administrativo é da responsabilidade de gerir, como uma aplicação que instala o Microsoft Office. 

 A combinação de funções de segurança, âmbitos de segurança e coleções define os objetos que um utilizador administrativo pode ver e gerir. Configuration Manager instala algumas funções de segurança predefinidas para tarefas de gestão comuns. Crie suas próprias funções de segurança para suportar necessidades empresariais específicas.  

 Para obter mais informações, consulte [configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).  



## <a name="bkmk_endpoints"></a> Proteger pontos finais de cliente  

 O Configuration Manager protege a comunicação do cliente para funções de sistema de sites através de um autoassinado ou certificados PKI, ou tokens do Azure Active Directory (Azure AD). Alguns cenários requerem a utilização de certificados PKI. Por exemplo, [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management)e para [clientes de dispositivos móveis](/sccm/mdm/plan-design/plan-on-premises-mdm).  

 Pode configurar as funções do sistema de site ao qual os clientes estabelecem ligação para a comunicação de cliente HTTPS ou HTTP. Computadores cliente comunicam sempre utilizando o método mais seguro disponível. Computadores cliente só voltam a utilizar o método de comunicação menos seguro, se tiver de funções de sistemas de sites que permitem comunicação HTTP.  

 Para obter mais informações, consulte [planear a segurança](/sccm/core/plan-design/security/plan-for-security).



## <a name="bkmk_accounts"></a> Grupos e contas do Configuration Manager  

 Configuration Manager utiliza a conta Sistema Local, na maioria das operações do site. Algumas tarefas de gestão podem implicar a criar e manter contas adicionais. O Configuration Manager cria vários grupos predefinidos e funções do SQL Server durante a configuração. Poderá ter de adicionar manualmente as contas de computador ou utilizador aos grupos padrão e funções do SQL Server.  

 Para obter mais informações, consulte [contas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  



## <a name="bkmk_privacy"></a> Privacidade  

 Antes de implementar do Configuration Manager, considere os requisitos de privacidade. Embora os produtos de gestão empresarial ofereçam muitas vantagens porque eles podem gerir muitos clientes de forma eficaz, este software pode afetar a privacidade dos utilizadores na sua organização. O Configuration Manager inclui diversas ferramentas para recolher dados e monitorizar dispositivos. Algumas ferramentas possam levantar questões de privacidade da sua organização.  

 Por exemplo, quando instalar o cliente do Configuration Manager, permite várias definições de gestão por predefinição. Esta configuração faz com que o software de cliente enviar informações para o site do Configuration Manager. O site armazena informações de cliente da base de dados do site. As informações do cliente não são enviadas diretamente para a Microsoft. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## <a name="see-also"></a>Consulte também

- [Plano de segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)   

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controlos criptográficos](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  
