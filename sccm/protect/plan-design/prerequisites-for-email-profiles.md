---
title: Pré-requisitos para perfis de e-mail
titleSuffix: Configuration Manager
description: Saiba mais sobre perfis de e-mail no System Center Configuration Manager e suas dependências externamente e dentro do produto.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1bb46973334dcec74715dd6123d71ddc4c0331b6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142345"
---
# <a name="email-profile-prerequisites"></a>Pré-requisitos para perfis de e-mail

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis de e-mail no System Center Configuration Manager têm dependências externas e dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Têm de ser concedidas permissões de segurança específicas para gerir perfis de e-mail|Tem de ter as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de e-mail:<br /><br /> -Para ver e gerir alertas e relatórios para perfis de e-mail: **Crie**, **eliminar**, **modificar**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **alertas** objeto.<br /><br /> -Para criar e gerir perfis de certificado: **Política de autor**, **modificar relatório**, **leitura** e **executar relatório** permissões para o **perfil de certificado** objeto.<br /><br /> -Para gerir implementações de perfis de e-mail: **Implementar políticas de configuração**, **modificar cliente alerta de estado**, **leitura**, e **ler recurso** permissões para o **coleção** objeto.<br /><br /> -Para gerir todas as políticas de configuração: **Crie**, **eliminar**, **modificar**, **leitura** e **definir âmbito de segurança** permissões para o  **Política de configuração** objeto.<br /><br /> -Para executar consultas relacionadas com perfis de e-mail: **Leia** permissão para o **consulta** objeto.<br /><br /> -Para ver informações sobre perfis de e-mail na consola do System Center Configuration Manager: **Leia** permissão para o **Site** objeto.<br /><br /> -Para ver mensagens de estado para perfis de e-mail: **Leia** permissão para o **mensagens de estado** objeto.<br /><br /> -Para criar e gerir perfis de e-mail: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **perfil de aprovisionamento de comunicações**objeto.<br /><br /> O **Gestor de acesso de recursos da empresa** função de segurança inclui as permissões que são necessárias para gerir perfis de e-mail no System Center Configuration Manager. Para mais informações, consulte [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail com o endereço SMTP principal do utilizador, deteção de utilizadores do System Center Configuration Manager tem de ser configurada para detetar os **correio** atributo no Active Directory ( Este é configurado por predefinição).|  

## <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail com o endereço SMTP principal do utilizador, este endereço tem de existir a **correio** atributo no Active Directory.<br /><br /> Para mais informações, consulte a documentação do Windows Server.|
