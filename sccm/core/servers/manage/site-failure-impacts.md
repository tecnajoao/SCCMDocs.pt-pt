---
title: Impactos de falha do site
titleSuffix: Configuration Manager
description: Compreenda os efeitos de várias falhas num site do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132021"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impactos de falha do site no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O servidor do site e em qualquer um dos outros sistemas de sites pode falhar e causar uma perda dos serviços que fornecem regularmente. Se instalar vários sistemas de sites no mesmo computador, e esse computador falhar, todos os serviços regularmente fornecidos por esses sistemas de sites já não estão disponíveis.

Parte do seu processo de planeamento deve incluir a compreender o impacto sobre o serviço que forneça a sua organização. Como cada sistema de sites no site oferece funcionalidades diferentes, o impacto de uma falha no site é diferente, consoante a função do sistema de site que falhou. 

Uso [opções de elevada disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options) para ajudar a atenuar a falha de qualquer sistema único. Também planear e ponha em prática uma [cópia de segurança e recuperação](/sccm/core/servers/manage/backup-and-recovery) estratégia para reduzir a quantidade de tempo que o serviço está indisponível.

As secções seguintes descrevem o impacto quando o sistema de site especificado não está operacional:


### <a name="site-server"></a>Servidor do site

- Administração de sites não é possível. Não é possível ligar a consola ao site.  

- O ponto de gestão recolhe informações de cliente e armazena em cache até que o servidor do site esteja novamente online.  

- Os utilizadores podem executar as implementações existentes e os clientes podem transferir conteúdo de pontos de distribuição.  


### <a name="site-database"></a>Base de dados do site

- Administração de sites não é possível.  

- Se o cliente de Configuration Manager já tiver uma atribuição de política com as novas políticas, e se o ponto de gestão tiver em cache o corpo de política, o cliente pode tornar um corpo de política de pedido e receber a resposta de corpo de política. No entanto, o site não pode processar quaisquer novos pedidos de atribuição de política.  

- Os clientes podem executar implementações, apenas se eles já recebeu a política e os ficheiros de origem associada são já armazenados em cache localmente no cliente.  


### <a name="management-point"></a>Ponto de gestão

- Embora seja possível criar novas implementações, os clientes não recebem-las até que um ponto de gestão está online.  

- Ainda assim os clientes recolhem o inventário, a medição de software e as informações de estado. Estes dados armazenados localmente até que o ponto de gestão está disponível.  

- Os clientes podem executar implementações, apenas se eles já recebeu a política e os ficheiros de origem associada são já armazenados em cache localmente no cliente.  


### <a name="distribution-point"></a>Ponto de distribuição

- Clientes do Configuration Manager podem executar as implementações, apenas se os ficheiros de origem associado que já tenham sido transferidos localmente ou estão disponíveis numa origem ponto a ponto.

