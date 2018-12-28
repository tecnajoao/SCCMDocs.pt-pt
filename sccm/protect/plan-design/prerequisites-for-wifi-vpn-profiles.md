---
title: Pré-requisitos para perfis Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre as permissões de segurança necessárias para gerir perfis de certificado, perfis de Wi-Fi e perfis VPN no System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9cf922f99ade06459a785e54775a9aedfd8e7a23
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414553"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Pré-requisitos para Wi-Fi e perfis VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Wi-Fi e perfis VPN no System Center Configuration Manager têm dependências apenas dentro do produto.  

 É necessário possuir as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de certificado, perfis Wi-Fi e perfis VPN:  

- Para ver e gerir alertas e relatórios para perfis Wi-Fi e: **Crie**, **eliminar**, **modificar**, **modificar relatório**, **leitura**, e **executar relatório** para o **alertas** objeto.  

- Para criar e gerir perfis de certificado: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil de certificado** objeto.  

- Para gerir implementações de perfis de Wi-Fi, certificado e VPN: **Implementar políticas de configuração**, **Modificar alerta de estado do cliente**, **leitura**, e **ler recurso** para o **coleção**objeto.  

- Para gerir todas as políticas de configuração: **Crie**, **eliminar**, **modificar**, **leitura**, e **definir âmbito de segurança** para o **política de configuração**  objeto.  

- Para executar consultas relacionadas com perfis de Wi-Fi e VPN: **Leia** permissão para o **consulta** objeto.  

- Para ver informações sobre perfis de Wi-Fi e VPN na consola do System Center Configuration Manager: **Leia** permissão para o **Site** objeto.  

- Para ver mensagens de estado para perfis Wi-Fi e VPN: **Leia** permissão para o **mensagens de estado** objeto.  

- Para criar e modificar o perfil de certificado de AC fidedigna: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil de certificado de AC fidedigna** objeto.  

- Para criar e gerir perfis VPN: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil da VPN** objeto.  

- Para criar e gerir perfis Wi-Fi: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** para o **perfil Wi-Fi** objeto.  

  O **Gestor de acesso de recursos da empresa** função de segurança inclui as permissões que são necessárias para gerir perfis de Wi-Fi no System Center Configuration Manager. Para mais informações, consulte [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md).
