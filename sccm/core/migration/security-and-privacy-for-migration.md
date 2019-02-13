---
title: Migração de segurança e privacidade
titleSuffix: Configuration Manager
description: Obtenha melhores práticas de segurança e informações de privacidade para a migração para o seu ambiente do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 277ed98ee4c77acda809affcdc61c56f0eb4c636
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126033"
---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Segurança e privacidade da migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém melhores práticas de segurança e informações de privacidade para a migração para o seu ambiente do System Center Configuration Manager.  

## <a name="security-best-practices-for-migration"></a>Melhores práticas de segurança para a migração  
 Utilize a seguinte prática recomendada de segurança para a migração.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Utilize a conta de computador para a conta de fornecedor de SMS de Site de origem e a conta de servidor de SQL de Site de origem, em vez de uma conta de utilizador.|Se tiver de utilizar uma conta de utilizador para a migração, remova os detalhes da conta quando a migração estar concluída.|  
|Utilize o IPsec quando migrar o conteúdo a partir de um ponto de distribuição num site de origem para um ponto de distribuição no seu site de destino.|Embora o conteúdo migrado é protegido por hash para detetar a adulteração, se os dados são modificados durante a transferência, a migração falhará.|  
|Restrinja e monitorize os utilizadores administrativos que podem criar tarefas de migração.|A integridade da base de dados da hierarquia de destino depende da integridade dos dados que o utilizador administrativo escolhe para importar a partir da hierarquia de origem. Além disso, este utilizador administrativo pode ler todos os dados da hierarquia de origem.|  

### <a name="security-issues-for-migration"></a>Problemas de segurança para a migração  
Migração tem os seguintes problemas de segurança:  

-   Clientes que estão impedidos de um site de origem com êxito podem ser atribuídos à hierarquia de destino antes do respetivo registo de cliente é migrado.  

     Embora o Configuration Manager mantém o estado bloqueado dos clientes migrados, o cliente pode atribuir com êxito para a hierarquia de destino se a atribuição ocorrer antes de concluída a migração do registo de cliente.  

-   As mensagens de auditoria não são migradas.  

Quando migrar os dados a partir de um site de origem para um site de destino, perderá todas as informações de auditorias da hierarquia de origem.  

## <a name="privacy-information-for-migration"></a>Informações de privacidade para a migração  
 A migração Deteta informações das bases de dados do site identificadas numa infraestrutura de origem e armazena esses dados para a base de dados na hierarquia de destino. As informações que o System Center Configuration Manager pode detetar a partir de um site de origem ou uma hierarquia dependem das funcionalidades que foram ativadas no ambiente de origem, bem como as operações de gestão que foram efetuadas nesse ambiente de origem.  

 Para obter mais informações sobre a segurança e informações de privacidade, consulte um dos seguintes tópicos:  

-   Para obter mais informações sobre as informações de privacidade do Configuration Manager 2007, consulte [segurança e privacidade para o Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) na biblioteca de documentação do Configuration Manager 2007.  

-   Para obter mais informações sobre as informações de privacidade do System Center 2012 Configuration Manager, consulte [segurança e privacidade do System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) no System Center 2012 Configuration Manager biblioteca de documentação.  

-   Para obter mais informações sobre as informações de privacidade do System Center Configuration Manager, consulte [segurança e privacidade para o System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Pode migrar alguns ou todos os dados suportados de um site de origem para uma hierarquia de destino.  

A migração não está ativada por predefinição e requer vários passos de configuração. Informações de migração não são enviadas à Microsoft.  

Antes de migrar dados de uma hierarquia de origem, considere os requisitos de privacidade.  
