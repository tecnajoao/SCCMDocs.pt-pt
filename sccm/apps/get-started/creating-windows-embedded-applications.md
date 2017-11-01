---
title: "Criar aplicações Windows Embedded"
titleSuffix: Configuration Manager
description: "Consulte as considerações deve ter em conta quando criar e implementar aplicações para dispositivos Windows Embedded."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: "7"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: e37dabb84cc6d56d9f08b2c0ee07115dd4bcb4fd
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>Criar aplicações Windows Embedded com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de outros requisitos do System Center Configuration Manager e procedimentos para criar uma aplicação, terá também de ter em conta as seguintes considerações ao criar e implementar aplicações para dispositivos Windows Embedded.  

## <a name="general-considerations"></a>Considerações gerais  

-   Ao implementar aplicações em dispositivos Windows Embedded que estão ativados para filtragem de escrita, pode especificar se pretende desativar o filtro de escrita no dispositivo durante a implementação da aplicação. Em seguida, pode optar por reiniciar o filtro de escrita após a implementação de aplicação. Se o filtro de escrita não estiver desativado, o software é implementado numa sobreposição temporária. Isto significa que, a menos que outra implementação Force a manter as alterações, o software será já não é instalado quando o dispositivo for reiniciado.  

-   Ao implementar uma aplicação num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Desta forma, poderá gerir a desativação e a ativação do filtro de escrita, bem como o reinício do dispositivo.  

-   A definição que controla o comportamento do filtro de escrita consiste numa caixa de verificação designada **Confirmar alterações dentro do prazo ou durante uma janela de manutenção (requer reinicialização)**.  

## <a name="tips-for-deploying-applications"></a>Sugestões para implementar aplicações  

**Utilize aplicações necessárias em vez de aplicações disponíveis para dispositivos Windows Embedded que tenham filtros de escrita ativados.** Como os utilizadores não podem instalar aplicações do Centro de Software num dispositivo Windows Embedded com filtros de escrita ativados, implemente sempre as aplicações com um objetivo de implementação **necessário** vez **disponíveis** nestes dispositivos. Normalmente, este não é um problema porque os computadores que executam um sistema operativo Windows Embedded, muitas vezes, executar uma única aplicação que deve ser executada da mesma forma para vários utilizadores. Por este motivo, estes dispositivos são altamente geridos e bloqueados pelo departamento de TI. As aplicações necessárias são ideais para este cenário.

 No entanto, se os utilizadores executarem mais de uma aplicação em dispositivos incorporados quando os filtros de escrita estiverem ativados, informe estes utilizadores sobre as seguintes limitações:  

-   Os utilizadores não podem instalar o software necessário a partir do Centro de Software.  

-   Os utilizadores não podem alterar o seu horário comercial no separador Opções do Centro de Software.  

-   Os utilizadores não podem adiar a instalação de uma aplicação necessária.  

Além disso, os utilizadores direitos limitados não podem iniciar sessão durante um período de manutenção se o Configuration Manager está a consolidar as alterações para instalações de software e atualizações. Durante este período, os utilizadores veem uma mensagem a informá-los de que o dispositivo não está disponível porque está em manutenção.  

**Não implemente aplicações para Windows Embedded dispositivos que tenham filtros de escrita ativados se as aplicações exigirem que o utilizador aceite os termos de licenciamento.** Quando os dispositivos embedded escrita filtros estão desativados para que o Configuration Manager pode instalar software, utilizadores com direitos limitados não podem iniciar sessão no dispositivo. Se a instalação exigir que o utilizador aceite os termos de licenciamento, isto não será possível e a instalação falhará. Certifique-se de que não implementa software em dispositivos Windows Embedded se a instalação exigir a interação do utilizador. Pode utilizar a lista Plataformas Aplicáveis para filtrar estes sistemas operativos.  
