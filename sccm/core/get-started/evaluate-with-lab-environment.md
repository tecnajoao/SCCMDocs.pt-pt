---
title: Avaliar do Configuration Manager | Documentos do Microsoft
description: "Crie um ambiente de laboratório para avaliar o System Center Configuration Manager para utilização na sua organização."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0ea90d3f3bef80b8acf9018a1338ae05fc948af4
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o System Center Configuration Manager ao criar o seu ambiente de laboratório

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Saiba como criar um ambiente de laboratório para avaliar o System Center Configuration Manager para utilização na sua organização.  

 System Center Configuration Manager é uma ferramenta complexa e poderosa para gerir os seus utilizadores, dispositivos e software. É uma boa ideia cuidadosamente avaliar o System Center Configuration Manager antes da implementação completa, para que pode marry Noções básicas sobre conceptual com experimenta interativa.  

 Este guia se destinar principalmente para administradores que estiver a avaliar a utilização do Configuration Manager em ambientes empresariais:  

-   Os administradores que pretendem completamente uma solução para gerir PCs, servidores e dispositivos móveis  

-   Administradores de alta segurança industries que necessitam da segurança da gestão de dispositivos no local com a flexibilidade da gestão de dispositivos baseada na nuvem  

-   Administradores que pretendem gerir a cópia de dimensionamento da respetiva arquitetura de servidor no local  

## <a name="what-this-lab-does"></a>O que faz este laboratório  
 É o principal objetivo da criação deste ambiente de laboratório para lhe dar o conhecimento geral para começar a trabalhar com o Configuration Manager e para melhorar a compreensão do Configuration Manager. Irá guiá-lo através de uma assemblagem desaprovisionamento da versão atual do Configuration Manager, utilizando os dois servidores:  

-   Uma que aloja o Active Directory, o controlador de domínio e o servidor DNS  

-   Um que aloja o Configuration Manager e todos os componentes de SQL Server de associados  

As máquinas cliente estão instaladas no Hyper-V. O próprio laboratório também pode ser executado como um sistema totalmente virtualizado num único servidor.  

## <a name="what-this-lab-does-not-do"></a>O que não faz este laboratório  
 Este laboratório não leva-o através de todos os cenários de Configuration Manager. Não foi concebido para ser imediatamente migrado para um ambiente de Active Directory.  

 Quando criar este laboratório, terá um ambiente funcional para utilizar. Mas este ambiente não será otimizado para fatores, como o desempenho do sistema, gestão de espaço em disco e armazenamento do SQL Server.  

##  <a name="BKMK_EvalRec"></a>Recomendado antes de criar o laboratório de leitura  
 Existe uma variedade de conteúdo no [documentação para System Center Configuration Manager](http://docs.microsoft.com/sccm/). Recomendamos que leia os tópicos seguintes desta biblioteca antes de iniciar a criação de laboratório:  

-   Saiba conceitos principais sobre a consola do Configuration Manager, portais pelo utilizador final e cenários de exemplo [introdução ao System Center Configuration Manager](../../core/understand/introduction.md).  

-   Saiba mais sobre as capacidades de gestão principal do Configuration Manager no [funcionalidades e capacidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Bolster seus conhecimentos com [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Saiba a importância das funções de segurança no [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Saiba mais sobre gestão de conteúdo no [conceitos de gestão de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Saiba como suportar com sucesso as tarefas diárias em toda a sua implementação no [compreender como os clientes localizam os recursos do site e os serviços do System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

