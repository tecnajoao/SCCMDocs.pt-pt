---
title: "Pré-requisitos de perfis de Wi-Fi e VPN"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as permissões de segurança necessárias para gerir perfis de certificado, perfis Wi-Fi e perfis VPN no System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 9f459ad76768443c218bbc86d75b3f5ae34596b3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Pré-requisitos para Wi-Fi e perfis VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Wi-Fi e perfis VPN no System Center Configuration Manager têm dependências apenas dentro do produto.  

 É necessário possuir as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de certificado, perfis Wi-Fi e perfis VPN:  

-   Para ver e gerir alertas e relatórios para perfis Wi-Fi e: **Criar**, **eliminar**, **modificar**, **modificar relatório**, **leitura**, e **executar relatório** para o **alertas** objeto.  

-   Para criar e gerir perfis de certificado: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil de certificado** objeto.  

-   Para gerir implementações de perfis de Wi-Fi, certificado e VPN: **Implementar políticas de configuração**, **modificar cliente alerta de estado**, **leitura**, e **ler recurso** para o **coleção** objeto.  

-   Para gerir todas as políticas de configuração: **Criar**, **eliminar**, **modificar**, **leitura**, e **definir âmbito de segurança** para o **política de configuração** objeto.  

-   Para executar consultas relacionadas com perfis de Wi-Fi e VPN: **Leitura** permissão para o **consulta** objeto.  

-   Para ver informações sobre perfis de Wi-Fi e VPN na consola do System Center Configuration Manager: **Leitura** permissão para o **Site** objeto.  

-   Para ver mensagens de estado para perfis de Wi-Fi e VPN: **Leitura** permissão para o **mensagens de estado** objeto.  

-   Para criar e modificar o perfil de certificado de AC fidedigna: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil de certificado de AC fidedigna** objeto.  

-   Para criar e gerir perfis VPN: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil da VPN** objeto.  

-   Para criar e gerir perfis Wi-Fi: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil Wi-Fi** objeto.  

 O **Gestor de acesso a recursos da empresa** função de segurança inclui estas permissões que são necessárias para gerir perfis de Wi-Fi no System Center Configuration Manager. Para obter mais informações, veja [Configurar a segurança no System Center Configuration Manager](../../core/plan-design/security/configure-security.md).
