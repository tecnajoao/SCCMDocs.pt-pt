---
title: Criar aplicações Windows Embedded
titleSuffix: Configuration Manager
description: Veja as considerações que deve levar em conta quando criar e implementar aplicações para dispositivos Windows Embedded.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a76ce199b84db200ed023d610f40dbf6f9f989c2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120870"
---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>Criar aplicações Windows Embedded com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de outros requisitos do System Center Configuration Manager e procedimentos para criar uma aplicação, terá também de ter em conta as seguintes considerações ao criar e implementar aplicações para dispositivos Windows Embedded.  

## <a name="general-considerations"></a>Considerações gerais  

-   Quando implementa aplicações em dispositivos Windows Embedded que estão ativados para filtragem de escrita, pode especificar se pretende desativar o filtro de escrita no dispositivo durante a implementação de aplicação. Em seguida, pode optar por reiniciar o filtro de escrita após a implementação de aplicação. Se o filtro de escrita não estiver desativado, o software é implementado numa sobreposição temporária. Isso significa que, a menos que outra implementação Force a alterações para persistir, o software será já não é instalado quando o dispositivo for reiniciado.  

-   Ao implementar uma aplicação num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Desta forma, poderá gerir a desativação e a ativação do filtro de escrita, bem como o reinício do dispositivo.  

-   A definição que controla o comportamento do filtro de escrita consiste numa caixa de verificação designada **Confirmar alterações dentro do prazo ou durante uma janela de manutenção (requer reinicialização)**.  

## <a name="tips-for-deploying-applications"></a>Sugestões para implementar aplicações  

**Utilize as aplicações necessárias em vez de aplicações disponíveis para dispositivos Windows Embedded que tenham filtros de escrita ativados.** Uma vez que os utilizadores não podem instalar aplicações do Centro de Software num dispositivo Windows Embedded com filtros de escrita ativados, implemente sempre as aplicações com um objetivo de implementação **necessária** vez **disponíveis**nestes dispositivos. Normalmente, isso não é um problema porque os computadores que executam um sistema operativo Windows Embedded utilizam frequentemente um único aplicativo que deve ser executada da mesma forma para vários utilizadores. Por este motivo, estes dispositivos são altamente geridos e bloqueados pelo departamento de TI. As aplicações necessárias são ideais para este cenário.

 No entanto, se os utilizadores executarem mais de uma aplicação em dispositivos incorporados quando os filtros de escrita estiverem ativados, informe estes utilizadores sobre as seguintes limitações:  

-   Os utilizadores não podem instalar o software necessário a partir do Centro de Software.  

-   Os utilizadores não podem alterar o seu horário comercial no separador Opções do Centro de Software.  

-   Os utilizadores não podem adiar a instalação de uma aplicação necessária.  

Além disso, os usuários de direitos limitados não podem iniciar sessão durante um período de manutenção se o Configuration Manager está a efetuar alterações nas instalações e atualizações de software. Durante este período, os utilizadores veem uma mensagem a informá-los de que o dispositivo não está disponível porque está em manutenção.  

**Não implemente aplicações para o Windows Embedded dispositivos que tenham filtros de escrita ativados se as aplicações exigirem que o utilizador aceitar os termos de licença.** Quando escrita filtros estão desativados, para que o Configuration Manager pode instalar software em dispositivos embedded, os utilizadores com direitos restritos não podem iniciar sessão no dispositivo. Se a instalação exigir que o utilizador aceite os termos de licenciamento, isto não será possível e a instalação falhará. Certifique-se de que não implementa software em dispositivos Windows Embedded se a instalação exigir a interação do utilizador. Pode utilizar a lista Plataformas Aplicáveis para filtrar estes sistemas operativos.  
