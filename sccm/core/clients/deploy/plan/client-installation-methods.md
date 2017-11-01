---
title: "Métodos de instalação de cliente"
titleSuffix: Configuration Manager
description: "Saiba mais métodos de instalação de cliente para o System Center Configuration Manager."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 4c600212c817e8b490e93938387b18c65baee042
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalação de cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar diferentes métodos para instalar o software de cliente do Configuration Manager. Pode utilizar um método ou uma combinação de métodos. Este tópico pode ler sobre cada método, para saber que funcionará melhor na sua organização.  

## <a name="client-push-installation"></a>Instalação push do cliente  

 **Plataforma de cliente suportada:** Windows  

 **Vantagens**  

-   Pode ser utilizado para instalar o cliente num único computador, numa coleção de computadores ou para os resultados de uma consulta.  

-   Pode ser utilizado para instalar automaticamente o cliente em todos os computadores detetados.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas no separador **Cliente** na caixa de diálogo **Propriedades da Instalação Push do Cliente**.  

 **Desvantagens**  

-   Pode causar tráfego de rede elevado quando efetuar instalações push em coleções de grandes dimensões.  

-   Só pode ser utilizado em computadores que tenham sido detetados pelo Configuration Manager.  

-   Não pode ser utilizado para instalar clientes num grupo de trabalho.  

-   Deve ser especificada uma conta de instalação push de cliente com direitos administrativos no computador cliente pretendido.  

-   A Firewall do Windows tem de ser configurada com exceções nos computadores cliente para que a instalação push do cliente seja concluída.  

-   Não é possível cancelar a instalação push do cliente. Quando utiliza este método de instalação de cliente para um site, o Configuration Manager tenta instalar o cliente em todos os recursos detetados e repete as tentativas de eventuais falhas durante 7 dias.  

 Para obter mais informações sobre este método de instalação, veja [How to deploy clients to Windows computers in System Center Configuration Manager (Como implementar clientes em computadores Windows no System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens:**  

-   Pode utilizar a infraestrutura de atualizações de software existente para gerir o software de cliente.  

-   Pode instalar automaticamente o software de cliente em novos computadores se as definições do Windows Server Update Services (WSUS) e da Política de Grupo estiverem instaladas corretamente nos Serviços de Domínio do Active Directory.  

-   Não necessita que os computadores sejam detetados antes de instalar o cliente.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Irá reinstalar o software de cliente, se este for removido.  

-   Não necessita que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

 **Desvantagens:**  

-   Como pré-requisito, requer uma infraestrutura de atualizações de software a funcionar.  

-   Tem de utilizar o mesmo servidor para a instalação do cliente e para as atualizações de software e este servidor tem de residir num site primário.  

-   Para instalar novos clientes, é necessário configurar um Objeto de Política de Grupo (GPO) nos Serviços de Domínio do Active Directory com a porta e o ponto de atualização de software ativos do cliente.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para aprovisionar computadores com propriedades de instalação de cliente.  

 Para obter mais informações sobre este método de instalação, veja [How to deploy clients to Windows computers in System Center Configuration Manager (Como implementar clientes em computadores Windows no System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens:**  

-   Não necessita que os computadores sejam detetados antes de instalar o cliente.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Não necessita que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

 **Desvantagens:**  

-   Pode causar tráfego de rede elevado se estiver a ser instalado um elevado número de clientes.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar as definições de política de grupo para adicionar propriedades de instalação de cliente aos computadores no seu site.  

 Para obter mais informações sobre este método de instalação, veja [How to deploy clients to Windows computers in System Center Configuration Manager (Como implementar clientes em computadores Windows no System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens:**  

-   Não necessita que os computadores sejam detetados antes de instalar o cliente.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

 **Desvantagens:**  

-   Pode causar tráfego de rede elevado se estiver a ser instalado um elevado número de clientes durante um período de tempo curto.  

-   Pode demorar muito tempo a instalar em todos os computadores cliente se os utilizadores não iniciarem sessão na rede com frequência.  

 Para obter mais informações sobre este método de instalação, veja [How to deploy clients to Windows computers in System Center Configuration Manager (Como implementar clientes em computadores Windows no System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Instalação manual  
 **Plataforma de cliente suportada:** Windows, UNIX/Linux, Mac OS X  

 **Vantagens:**  

-   Não necessita que os computadores sejam detetados antes de instalar o cliente.  

-   Pode ser útil para fins de teste.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

 **Desvantagens:**  

-   Sem automatização, portanto demorada.  

 Para mais informações sobre como instalar manualmente o cliente em cada plataforma, consulte o seguinte:  

-   [Como implementar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [Como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [Como implementar clientes em Mac no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  
