---
title: "Noções básicas de segurança | Documentos do Microsoft"
description: "Saiba mais sobre as camadas de segurança para o System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d56c8a76e4770336d4a2ab519e776e48fec8ebcd
ms.openlocfilehash: df3198885259b1db4a1aadee0db6512a1a2d4911
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Noções básicas de segurança do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Segurança para o System Center Configuration Manager é constituído por várias camadas. A primeira camada é fornecida por funcionalidades de segurança do Windows para o sistema operativo e da rede e inclui:  

-   Partilha de ficheiros para transferir ficheiros entre componentes do Configuration Manager.  

-   Controlo de listas de acesso (ACL) para ajudar a proteger ficheiros e chaves de registo.  

-   Segurança do protocolo Internet (IPsec) para ajudar a proteger as comunicações.  

-   Política de grupo para configurar a política de segurança.  

-   Permissões de modelo de objeto do componente (DCOM) distribuída para aplicações distribuídas, como a consola do Configuration Manager.  

-   Os serviços de domínio do Active para armazenar as entidades de segurança.  

-   Segurança, incluindo alguns grupos que são criados durante a configuração do Configuration Manager da conta do Windows.  

Em seguida, os componentes de segurança adicionais, tal como firewalls e deteção de intrusões, ajudam a fornecer defesa da todo o ambiente. Os certificados emitidos pelas infraestrutura de chaves públicas (PKI) padrão da indústria fornecem autenticação, assinatura e encriptação.  

Para além da segurança fornecida pela infraestrutura de servidor e de rede do Windows, do Configuration Manager controla o acesso à consola do Configuration Manager e os respetivos recursos de várias formas. Por predefinição, apenas os administradores locais possuem direitos sobre os ficheiros e chaves de registo que são necessárias para executar a consola do Configuration Manager nos computadores onde está instalado.  

A próxima camada de segurança baseia-se no acesso através do WMI (Windows Management Instrumentation), nomeadamente o Fornecedor de SMS. O fornecedor de SMS é um componente do Configuration Manager que concede um utilizador acesso à consulta a base de dados do site para obter informações. Por predefinição, o acesso ao fornecedor de é restrito a membros do grupo Admins de SMS local. Este grupo no primeiro contém apenas o utilizador que instalou o Configuration Manager. Para conceder permissão a outras contas no repositório CIM (Common Information Model) e no fornecedor de SMS, adicione-as ao grupo de Administradores de SMS.  

A camada final de segurança baseia-se nas permissões para objetos da base de dados do site. Por predefinição, a conta de sistema Local e a conta de utilizador que utilizou para instalar o Configuration Manager podem administrar todos os objetos na base de dados do site. Pode conceder e restringir as permissões a utilizadores administrativos adicionais na consola do Configuration Manager utilizando a administração baseada em funções.  



## <a name="role-based-administration"></a>Administração baseada em funções  
 O Configuration Manager utiliza a administração baseada em funções para ajudar a proteger objetos, como coleções, implementações e sites. Este modelo de administração define e gere de forma centralizada as definições de acesso de segurança de toda a hierarquia para todos os sites e definições do site. Funções de segurança são atribuídas a utilizadores administrativos e permissões de grupo. As permissões estão ligadas a diferentes tipos de objeto do Configuration Manager, como as permissões que são utilizados para criar ou alterar as definições de cliente. Os âmbitos de segurança de instâncias específicas de objetos que um utilizador administrativo é responsável para gerir, como uma aplicação que instala o Microsoft Office. A combinação de funções de segurança, âmbitos de segurança e coleções define os objetos que um utilizador administrativo pode ver e gerir. O Configuration Manager instala algumas funções de segurança predefinidas para tarefas de gestão típicas. No entanto, pode criar suas próprias funções de segurança para satisfazer as suas necessidades comerciais específicas.  

 Para obter mais informações, consulte o artigo [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Proteger pontos finais de cliente  
 Comunicação do cliente com funções do sistema de sites é protegida com certificados autoassinados, ou ao utilizar certificados PKI. Terá de utilizar um certificado PKI para clientes de computador que o Configuration Manager Deteta na Internet e para clientes de dispositivos móveis. O certificado PKI utiliza HTTPS para proteger pontos finais de cliente. As funções do sistema de sites a que os clientes se ligam podem ser configuradas para comunicação HTTPS ou HTTP com o cliente. Computadores cliente comunicam sempre utilizando o método mais seguro disponível. Computadores cliente só voltam a utilizar o método de comunicação de HTTP menos seguro na intranet se possuir funções de sistema de sites que permitem comunicação HTTP.  

 Para obter mais informações, consulte o artigo [Cryptographic controla referência técnica para o System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Contas e grupos do Configuration Manager  
 O Configuration Manager utiliza a conta de sistema Local na maioria das operações do site. Algumas tarefas de gestão podem exigir a criação e manutenção de contas adicionais. São criadas vários grupos predefinidos e funções do SQL Server durante a configuração. Poderá ter de adicionar manualmente as contas de utilizadores ou computadores a grupos predefinidos e funções do SQL Server.  

 Para obter mais informações, veja [Contas utilizadas no System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Privacidade  
 Embora os produtos de gestão empresarial ofereçam muitas vantagens por permitirem gerir muitos clientes de forma eficaz, também tem de estar ciente de como este software pode afetar a privacidade dos utilizadores na sua organização. System Center Configuration Manager inclui diversas ferramentas para recolher dados e monitorizar dispositivos. Algumas ferramentas poderão emitir motivos de privacidade.  

 Por exemplo, quando instala o cliente do Configuration Manager, muitas definições de gestão são ativadas por predefinição. Isto faz com que o software de cliente enviar informações para o site do Configuration Manager. Informações de cliente são armazenadas na base de dados do Configuration Manager e as informações não são enviadas à Microsoft. Antes de implementar o System Center Configuration Manager, considere os requisitos de privacidade.  

