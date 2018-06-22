---
title: Pré-requisitos para perfis de e-mail
titleSuffix: Configuration Manager
description: Saiba mais sobre perfis de e-mail no System Center Configuration Manager e as respetivas dependências externamente e dentro do produto.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58e1f4b56c99cf29c112773b2a82c70695e58744
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351399"
---
# <a name="email-profile-prerequisites"></a>Pré-requisitos de perfil de e-mail

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis de e-mail no System Center Configuration Manager tem dependências externas e dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Têm de ser concedidas permissões de segurança específicas para gerir perfis de e-mail|Tem de ter as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de e-mail:<br /><br /> -Para ver e gerir alertas e relatórios para perfis de e-mail: **Criar**, **eliminar**, **modificar**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **alertas** objeto.<br /><br /> -Para criar e gerir perfis de certificado: **Política de autor**, **modificar relatório**, **leitura** e **executar relatório** permissões para o **perfil de certificado** objeto.<br /><br /> -Para gerir implementações de perfis de e-mail: **Implementar políticas de configuração**, **modificar cliente alerta de estado**, **leitura**, e **ler recurso** permissões para o **coleção** objeto.<br /><br /> -Para gerir todas as políticas de configuração: **Criar**, **eliminar**, **modificar**, **leitura** e **definir âmbito de segurança** permissões para o  **Política de configuração** objeto.<br /><br /> -Para executar consultas relacionadas com perfis de e-mail: **Leitura** permissão para o **consulta** objeto.<br /><br /> -Para ver informações sobre perfis de e-mail na consola do System Center Configuration Manager: **Leitura** permissão para o **Site** objeto.<br /><br /> -Para ver mensagens de estado para perfis de e-mail: **Leitura** permissão para o **mensagens de estado** objeto.<br /><br /> -Para criar e gerir perfis de e-mail: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **perfil de aprovisionamento de comunicações**objeto.<br /><br /> O **Gestor de acesso a recursos da empresa** função de segurança inclui estas permissões que são necessárias para gerir perfis de e-mail no System Center Configuration Manager. Para obter mais informações, veja [Configurar a segurança no System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail utilizando o endereço SMTP principal do utilizador, a deteção de utilizadores do System Center Configuration Manager tem de ser configurada para detetar o **correio** atributo do Active Directory (configurado por predefinição).|  

## <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail utilizando o endereço SMTP principal do utilizador, este endereço tem de existir o **correio** atributo no Active Directory.<br /><br /> Para mais informações, consulte a documentação do Windows Server.|
