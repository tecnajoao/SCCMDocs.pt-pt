---
title: Atualização dos clientes
titleSuffix: Configuration Manager
description: Obtenha informações sobre como atualizar clientes no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0531c50792b6617eeb5e294bfad3626a0089c1f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131494"
---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Atualização dos clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar diferentes métodos para atualizar o software de cliente do System Center Configuration Manager em computadores Windows, servidores UNIX e Linux e computadores Mac. Aqui estão as vantagens e desvantagens de cada método.  

> [!TIP]  
>  Se estiver a atualizar a infraestrutura do servidor a partir de uma versão anterior do \(como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager\), recomendamos que conclua a atualização do servidor incluindo a instalação de todas as atualizações do current branch, antes de atualizar os clientes do Configuration Manager. Dessa forma, também terá a versão mais recente do software de cliente.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

- Pode ser utilizada para novas instalações de cliente ou para atualizações.  

- Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

- Não necessita que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se estiver a atualizar muitos dos clientes.  

- Se o esquema do Active Directory não estiver expandido para o Configuration Manager, tem de utilizar [definições de política de grupo](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) para adicionar as propriedades de instalação de cliente para computadores no seu site.  


## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de instalar o cliente.  

- Pode ser utilizada para novas instalações de cliente ou para atualizações.  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se estiver a atualizar muitos clientes num curto período de tempo.  

- Pode demorar muito tempo para atualizar todos os computadores cliente se os utilizadores não iniciarem sessão na rede.  

  Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando Scripts de Início de Sessão](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Instalação manual  
 **Plataforma de cliente suportada:** Windows, UNIX/Linux e Mac OS X  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

- Pode ser útil para fins de teste.  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Sem automatização, portanto demorada.  

  Para obter mais informações, consulte os tópicos seguintes:  

- [Como Instalar Manualmente Clientes do Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Como atualizar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Como atualizar clientes em computadores Mac no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Instalação de atualização (gestão de aplicações)  
 **Plataforma de cliente suportada:** Windows  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 com este método. Neste cenário, pode implantar o cliente do Configuration Manager como um pacote a partir do site do Configuration Manager 2007 ou pode utilizar a atualização automática do cliente que cria e implementa automaticamente um pacote que contém a versão mais recente do cliente.  

#### <a name="advantages"></a>Vantagens  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se distribuir o cliente para coleções grandes.  

- Só pode ser utilizado para atualizar o software de cliente em computadores que tenham sido detetados e atribuídos ao site.  

  Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando um Pacote e Programa](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Atualização automática de cliente  

> [!NOTE]  
>  Pode ser utilizado para atualizar clientes do Configuration Manager 2007 para clientes do System Center Configuration Manager. Um cliente do Configuration Manager 2007 pode atribuir a um site do Configuration Manager, mas não é possível efetuar nenhuma ação além da atualização automática de cliente.  

 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Devido à escolha aleatória ao longo do período especificado, a atualização automática só é adequada para as atualizações de cliente em grande escala. Outros métodos são demasiado lento em grande escala, ou não tem escolha aleatória. 

    > [!Note]
    > Criar um piloto de cliente não é bom para grande escala como ele não tornar aleatórios em todos os.  
- Pode ser utilizado para manter automaticamente os clientes no site na versão mais recente.  

- Requer uma administração mínima.  

#### <a name="disadvantages"></a>Desvantagens  

- Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

- Aplica-se a todos os clientes na hierarquia que estão atribuídos a um site. Não pode ser limitado por coleção.  

- Opções de agendamento limitadas.  

  Para mais informações, veja [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Teste de clientes  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Pode ser utilizado para testar novas versões de cliente numa coleção de pré-produção mais pequena.  

- Quando o teste estiver concluído, os clientes em pré-produção são promovidos para produção e atualizados automaticamente em todo o site do Configuration Manager.  

#### <a name="disadvantages"></a>Desvantagens  

- Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

  [Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
