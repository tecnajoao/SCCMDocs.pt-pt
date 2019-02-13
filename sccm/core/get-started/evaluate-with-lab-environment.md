---
title: Avaliar num ambiente de laboratório
titleSuffix: Configuration Manager
description: Crie um ambiente de laboratório para avaliar o System Center Configuration Manager para utilização na sua organização.
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e9f851f6dcd21de261729215bad196233610272
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127682"
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o System Center Configuration Manager ao criar o seu ambiente de laboratório

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Saiba como criar um ambiente de laboratório para avaliar o System Center Configuration Manager para utilização na sua organização.  

 System Center Configuration Manager é uma ferramenta complexa e poderosa para gerir os seus utilizadores, dispositivos e software. É uma boa idéia de avaliar minuciosamente o System Center Configuration Manager antes da implantação completa, para que possa aliar uma compreensão conceptual a exercícios práticos.  

 Este guia destina-se principalmente a administradores que estão a avaliar a utilização do Configuration Manager em ambientes corporativos:  

-   Administradores que pretendem uma solução para gerir totalmente PCs, servidores e dispositivos móveis  

-   Administradores em indústrias de alta segurança que necessitam da segurança da gestão de dispositivos no local com a flexibilidade da gestão de dispositivos baseado na nuvem  

-   Os administradores que pretendem gerir a dimensionamento de segurança da sua arquitetura de servidor no local  

## <a name="what-this-lab-does"></a>O que faz este laboratório  
 O principal objetivo da criação deste ambiente de laboratório é para lhe fornecer os conhecimentos gerais para começar a trabalhar com o Configuration Manager e para melhorar a compreensão do Configuration Manager. Verá como uma assemblagem expedita da versão atual do Configuration Manager, ao utilizar dois servidores:  

-   Um que aloja o Active Directory, o controlador de domínio e o servidor DNS  

-   Associados a um que aloja o Configuration Manager e todos os componentes do SQL Server  

As máquinas cliente estão instaladas no Hyper-V. O próprio laboratório também pode ser executado como um sistema totalmente virtualizado num único servidor.  

## <a name="what-this-lab-does-not-do"></a>O que não faz este laboratório  
 Este laboratório não o orienta através de todos os cenários do Configuration Manager. Não foi concebido para ser migrado imediatamente para um ambiente ativo.  

 Quando criar este laboratório, terá um ambiente funcional para utilizar. Mas este ambiente não estará otimizado para fatores como o desempenho do sistema, gestão de espaço de disco rígido e armazenamento do SQL Server.  

##  <a name="BKMK_EvalRec"></a> Leitura recomendada antes de criar o laboratório  
 Há vários conteúdos disponíveis na [documentação para o System Center Configuration Manager](http://docs.microsoft.com/sccm/). Recomendamos que leia os tópicos seguintes desta biblioteca antes de começar a criar o laboratório:  

-   Aprenda os principais conceitos sobre a consola do Configuration Manager, portais do utilizador final e cenários de exemplo [introdução ao System Center Configuration Manager](../../core/understand/introduction.md).  

-   Saiba mais sobre as capacidades de gestão principal do Configuration Manager numa [funcionalidades e capacidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Aumente o seu conhecimento com [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Conheça a importância das funções de segurança nas [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Saiba mais sobre a gestão de conteúdos no [conceitos de gerenciamento de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Saiba como suportar com êxito as tarefas diárias em toda a implementação num [compreender como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  
