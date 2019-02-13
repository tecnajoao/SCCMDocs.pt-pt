---
title: Métodos de instalação de cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre os métodos de instalação do cliente do Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c206a8045429551f361f640febbcda4a39ef9698
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139947"
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalação de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar diferentes métodos para instalar o software de cliente do Configuration Manager. Utilize um método ou uma combinação dos métodos. Este artigo descreve cada método, para que possa saber qual funciona melhor para sua organização.  

## <a name="client-push-installation"></a>Instalação push do cliente  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode ser utilizado para instalar o cliente num único computador, numa coleção de computadores ou para os resultados de uma consulta.  

-   Pode ser utilizado para instalar automaticamente o cliente em todos os computadores detetados.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas no separador **Cliente** na caixa de diálogo **Propriedades da Instalação Push do Cliente**.  

#### <a name="disadvantages"></a>Desvantagens  

-   Pode causar tráfego de rede elevado quando efetuar instalações push em coleções de grandes dimensões.  

-   Só pode ser utilizada em computadores que tenham sido detetados pelo Configuration Manager.  

-   Não pode ser utilizado para instalar clientes num grupo de trabalho.  

-   Deve ser especificada uma conta de instalação push de cliente com direitos administrativos no computador cliente pretendido.  

-   Firewall do Windows tem de ser configurado com exceções nos computadores cliente.   

-   Não é possível cancelar a instalação push do cliente. Configuration Manager tenta instalar o cliente em todos os recursos detetados. Ele repete as tentativas falhadas durante sete dias.  

Para obter mais informações, consulte [como instalar clientes com a instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode utilizar a infraestrutura de atualizações de software existente para gerir o software de cliente.  

-   Se o Windows Server Update Services (WSUS) e configurações de diretiva de grupo no Active Directory Domain Services estão configuradas corretamente, ele poderá instalar automaticamente o software de cliente em novos computadores.  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Se o cliente for removido, este método irá reinstalá-lo.  

-   Não precisa de configurar e manter uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Como pré-requisito, requer uma infraestrutura de atualizações de software a funcionar.  

-   Tem de utilizar o mesmo servidor para a instalação de cliente e atualizações de software. Este servidor tem de residir num site primário.  

-   Para instalar novos clientes, tem de configurar um objeto de política de grupo nos serviços de domínio do Active Directory com o ponto de atualização de software ativo e a porta do cliente.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para aprovisionar computadores com propriedades de instalação do cliente.  

Para obter mais informações, consulte [como instalar clientes com a instalação baseada em atualização de software](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Instalação da política de grupo  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Não precisa de configurar e manter uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se um grande número de clientes está a ser instalado, ele pode causar tráfego de rede elevado.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para adicionar as propriedades de instalação de cliente para computadores no seu site.  

Para obter mais informações, consulte [como instalar clientes com diretiva de grupo](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Instalação do script de início de sessão  

**Plataforma de cliente suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se um grande número de clientes está a ser instalado durante um período curto período de tempo, ele pode causar tráfego de rede elevado.  

-   Se os utilizadores não iniciarem sessão na rede, pode demorar muito tempo a instalar em todos os computadores cliente.  

Para obter mais informações, consulte [como instalar clientes com scripts de logon](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript).  



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



## <a name="microsoft-intune-mdm-installation"></a>Instalação do Microsoft Intune MDM

**Plataformas de cliente suportadas**: Windows 10

#### <a name="advantages"></a>Vantagens  

-   Não necessita que os computadores sejam detetados antes do cliente pode ser instalado.  

-   Não precisa de configurar e manter uma conta de instalação para o computador cliente pretendido.  

-   Pode utilizar a autenticação moderna com o Azure Active Directory.  

-   Pode instalar e atribuir a computadores na internet.  

-   Pode automatizar com o Windows AutoPilot e o Microsoft Intune para a cogestão.  

#### <a name="disadvantages"></a>Desvantagens  

-   Requer tecnologias adicionais fora do Configuration Manager.  

-   Requer o dispositivo tem acesso à internet, mesmo que não é baseado na internet.  

Para obter mais informações, veja os artigos seguintes:  

-   [Como instalar clientes em dispositivos Windows geridos por MDM do Intune](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

