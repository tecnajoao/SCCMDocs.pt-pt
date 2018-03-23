---
title: Métodos de instalação de cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre os métodos de instalação do cliente do Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: ''
caps.handback.revision: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38f7d428149f4a4ac2b0bcb604031eca60a0fae5
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalação de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar diferentes métodos para instalar o software de cliente do Configuration Manager. Utilize um método ou uma combinação de métodos. Este artigo descreve cada método de, pelo que pode saber o que funciona melhor para a sua organização.  

## <a name="client-push-installation"></a>Instalação push do cliente  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode ser utilizado para instalar o cliente num único computador, numa coleção de computadores ou para os resultados de uma consulta.  

-   Pode ser utilizado para instalar automaticamente o cliente em todos os computadores detetados.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas no separador **Cliente** na caixa de diálogo **Propriedades da Instalação Push do Cliente**.  

#### <a name="disadvantages"></a>Desvantagens  

-   Pode causar tráfego de rede elevado quando efetuar instalações push em coleções de grandes dimensões.  

-   Só pode ser utilizado em computadores que tenham sido detetados pelo Configuration Manager.  

-   Não pode ser utilizado para instalar clientes num grupo de trabalho.  

-   Deve ser especificada uma conta de instalação push de cliente com direitos administrativos no computador cliente pretendido.  

-   Firewall do Windows tem de ser configurada com exceções nos computadores cliente.   

-   Não é possível cancelar a instalação push do cliente. Configuration Manager tenta instalar o cliente em todos os recursos detetados. Repetir eventuais falhas de sete dias.  

Para obter mais informações, consulte [como instalar clientes com a instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode utilizar a infraestrutura de atualizações de software existente para gerir o software de cliente.  

-   Se o Windows Server Update Services (WSUS) e definições de política de grupo no Active Directory Domain Services estão configuradas corretamente, este poderá instalar automaticamente o software de cliente em novos computadores.  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Se o cliente for removido, este método reinstala-o.  

-   Não requer que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Como pré-requisito, requer uma infraestrutura de atualizações de software a funcionar.  

-   Tem de utilizar o mesmo servidor para a instalação de cliente e atualizações de software. Este servidor tem de residir num site primário.  

-   Para instalar novos clientes, tem de configurar um objeto de política de grupo nos serviços de domínio do Active Directory com o ponto de atualização de software ativo e a porta do cliente.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para aprovisionar computadores com propriedades de instalação de cliente.  

Para obter mais informações, consulte [como instalar clientes com a instalação baseada em atualização de software](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Instalação da política de grupo  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Não requer que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se estiver a ser instalado um elevado número de clientes, pode causar tráfego de rede elevado.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para adicionar propriedades de instalação de cliente aos computadores no seu site.  

Para obter mais informações, consulte [como instalar clientes com a política de grupo](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Instalação do script de início de sessão  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se um grande número de clientes está a ser instalado durante um curto período de tempo, pode causar tráfego de rede elevado.  

-   Se os utilizadores não iniciarem sessão na rede, pode demorar muito tempo a instalar em todos os computadores cliente.  

Para obter mais informações, consulte [como instalar clientes com scripts de início de sessão](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Instalação manual  

**Plataforma de cliente suportada**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Pode ser útil para fins de teste.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Sem automatização, portanto demorada.  

Para obter mais informações sobre como instalar manualmente o cliente em cada plataforma, consulte os artigos seguintes:  

-   [Como implementar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)  

-   [Como implementar clientes em servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)  

-   [Como implementar clientes em Macs](/sccm/core/clients/deploy/deploy-clients-to-macs)  



## <a name="microsoft-intune-mdm-installation"></a>Instalação de MDM do Microsoft Intune

**Plataformas de cliente suportadas**: Windows 10

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Não requer que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

-   Pode utilizar a autenticação moderna no Azure Active Directory.  

-   Pode, instale e atribua os computadores na internet.  

-   Pode automatizar com AutoPilot do Windows e o Microsoft Intune para gestão conjunta.  

#### <a name="disadvantages"></a>Desvantagens  

-   Necessita de tecnologias adicionais fora do Configuration Manager.  

-   Requer o dispositivo tem acesso à internet, mesmo se não for baseado na internet.  

Para obter mais informações, consulte os artigos seguintes:  

-   [Como instalar clientes em dispositivos Windows geridos por MDM do Intune](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

