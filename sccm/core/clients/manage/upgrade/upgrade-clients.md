---
title: Atualização dos clientes
titleSuffix: Configuration Manager
description: Obter informações sobre como atualizar clientes no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76b6b3e1e3ee8e1cdbfbb61890b5a1f7ac5e853f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Atualização dos clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar diferentes métodos para atualizar o software de cliente do System Center Configuration Manager em computadores Windows, servidores UNIX e Linux e computadores Mac. Seguem-se as vantagens e desvantagens de cada método.  

> [!TIP]  
>  Se estiver a atualizar a infraestrutura do servidor a partir de uma versão anterior do \(como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager\), recomendamos que conclua a atualização do servidor incluindo a instalação de todas as atualizações do current branch, antes de atualizar os clientes do Configuration Manager. Desta forma, também terá da versão mais recente do software de cliente.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens**  

-   Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Não necessita que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

 **Desvantagens**  

-   Pode causar tráfego de rede elevado se estiver a atualizar muitos clientes.  

-   Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar [definições de política de grupo](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) para adicionar propriedades de instalação de cliente aos computadores no seu site.  


## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens**  

-   Não necessita que os computadores sejam detetados antes de instalar o cliente.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

 **Desvantagens**  

-   Pode causar tráfego de rede elevado se estiver a atualizar muitos clientes num curto período de tempo.  

-   Pode demorar muito tempo a atualizar todos os computadores cliente se os utilizadores não iniciarem sessão na rede.  

 Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando Scripts de Início de Sessão](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Instalação manual  
 **Plataforma de cliente suportada:** Windows, UNIX/Linus, Mac OS X  

 **Vantagens**  

-   Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

-   Pode ser útil para fins de teste.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

 **Desvantagens**  

-   Sem automatização, portanto demorada.  

 Para obter mais informações, consulte os tópicos seguintes:  

-   [Como instalar clientes do Configuration Manager manualmente](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Como atualizar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [Como atualizar clientes em computadores Mac no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Instalação de atualização (gestão de aplicações)  
 **Plataforma de cliente suportada:** Windows  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 com este método. Neste cenário, pode implementar o cliente do Configuration Manager como um pacote a partir do site do Configuration Manager 2007 ou pode utilizar a atualização automática de cliente que cria e implementa automaticamente um pacote que contém a versão mais recente do cliente.  

 **Vantagens**  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

 **Desvantagens**  

-   Pode causar tráfego de rede elevado se distribuir o cliente para coleções de grandes dimensões.  

-   Só pode ser utilizado para atualizar o software de cliente em computadores que tenham sido detetados e atribuídos ao site.  

 Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando um Pacote e Programa](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Atualização automática de cliente  

> [!NOTE]  
>  Pode ser utilizado para atualizar clientes do Configuration Manager 2007 para clientes do System Center Configuration Manager. Um cliente do Configuration Manager 2007 pode atribuir a um site do Configuration Manager, mas não é possível efetuar nenhuma ação além da atualização automática de cliente.  

 **Plataforma de cliente suportada:** Windows  

 **Vantagens**  

-   Pode ser utilizado para manter automaticamente os clientes no site na versão mais recente.  

-   Requer uma administração mínima.  

 **Desvantagens**  

-   Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

-   Não é adequado para atualizar vários clientes em simultâneo.  

-   Aplica-se a todos os clientes na hierarquia que estão atribuídos a um site. Não pode ser limitado por coleção.  

-   Opções de agendamento limitadas.  

 Para mais informações, veja [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Teste de clientes  
 **Plataforma de cliente suportada:** Windows  

 **Vantagens**  

-   Pode ser utilizado para testar novas versões de cliente numa coleção de pré-produção mais pequena.  

-   Quando os testes são concluídos, os clientes em pré-produção são promovidos para produção e atualizados automaticamente em todo o site do Configuration Manager.  

 **Desvantagens**  

-   Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

 [Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
