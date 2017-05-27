---
title: "Pré-requisitos para perfis de e-mail | Documentos do Microsoft"
description: "Saiba mais sobre perfis de e-mail no System Center Configuration Manager e as respetivas dependências externamente e dentro do produto."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: 451317db1d7aab888c03d1a099b9ce25311e06d0
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="email-profile-prerequisites"></a>Pré-requisitos de perfil de e-mail

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis de e-mail no System Center Configuration Manager têm dependências externas e dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Têm de ser concedidas permissões de segurança específicas para gerir perfis de e-mail|Tem de ter as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de e-mail:<br /><br /> -Para ver e gerir alertas e relatórios para perfis de e-mail: **Criar**, **eliminar**, **modificar**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **alertas** objeto.<br /><br /> -Para criar e gerir perfis de certificado: **Política de autor**, **modificar relatório**, **leitura** e **executar relatório** permissões para o **perfil de certificado** objeto.<br /><br /> -Para gerir implementações de perfis de e-mail: **Implementar políticas de configuração**, **modificar cliente alerta de estado**, **leitura**, e **ler recurso** permissões para o **coleção** objeto.<br /><br /> -Para gerir todas as políticas de configuração: **Criar**, **eliminar**, **modificar**, **leitura** e **definir âmbito de segurança** permissões para o **política de configuração** objeto.<br /><br /> -Para executar consultas relacionadas com perfis de e-mail: **Leitura** permissão para o **consulta** objeto.<br /><br /> -Para ver informações de perfis de e-mail na consola do System Center Configuration Manager: **Leitura** permissão para o **Site** objeto.<br /><br /> -Para ver mensagens de estado para perfis de e-mail: **Leitura** permissão para o **mensagens de estado** objeto.<br /><br /> -Para criar e gerir perfis de e-mail: **Política de autor**, **modificar relatório**, **leitura**, e **executar relatório** permissões para o **perfil de aprovisionamento de comunicações** objeto.<br /><br /> O **Gestor de acesso a recursos da empresa** função de segurança inclui as permissões que são necessárias para gerir perfis de e-mail no System Center Configuration Manager. Para obter mais informações, veja [Configurar a segurança no System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail utilizando o endereço SMTP principal do utilizador, deteção de utilizadores do System Center Configuration Manager deve ser configurada para detetar a **correio** atributo do Active Directory (configurado por predefinição).|  

## <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Atributo de correio no active directory|Se pretender gerar o e-mail dos utilizadores endereço num perfil de e-mail utilizando o endereço SMTP principal do utilizador, este endereço tem de existir o **correio** atributo no Active Directory.<br /><br /> Para mais informações, consulte a documentação do Windows Server.|

