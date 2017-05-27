---
title: "Migração de segurança e privacidade | Documentos do Microsoft"
description: "Obter melhores práticas de segurança e informações de privacidade da migração para o seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 8aa6971d75924ab5bcacd70c330913097ecf8717
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Segurança e privacidade da migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém melhores práticas de segurança e informações de privacidade da migração para o seu ambiente do System Center Configuration Manager.  

## <a name="security-best-practices-for-migration"></a>Melhores práticas de segurança para a migração  
 Utilize a seguinte melhor prática de segurança para a migração.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Utilize a conta de computador para a conta de fornecedor de SMS do Site de origem e conta de servidor SQL do Site de origem em vez de uma conta de utilizador.|Se tiver de utilizar uma conta de utilizador para a migração, remova os detalhes da conta depois de concluir a migração.|  
|Utilize o IPsec quando migrar o conteúdo de um ponto de distribuição de um site de origem para um ponto de distribuição no seu site de destino.|Apesar do conteúdo migrado é protegido por hash para detetar a adulteração, se os dados forem modificados durante a transferência, a migração falhará.|  
|Restrinja e monitorize os utilizadores administrativos que podem criar tarefas de migração.|A integridade da base de dados da hierarquia de destino depende da integridade dos dados que o utilizador administrativo escolhe para importar a partir da hierarquia de origem. Além disso, este utilizador administrativo pode ler todos os dados da hierarquia de origem.|  

### <a name="security-issues-for-migration"></a>Problemas de segurança para a migração  
A migração tem os seguintes problemas de segurança:  

-   Os clientes que estão bloqueados num site de origem podem ser atribuído com sucesso à hierarquia de destino antes da migração do respetivo registo de cliente.  

     Apesar do Configuration Manager mantém o estado bloqueado dos clientes migrados, o cliente pode atribuídos com sucesso à hierarquia de destino se a atribuição ocorrer antes de concluída a migração do registo de cliente.  

-   As mensagens de auditoria não são migradas.  

Quando migrar dados a partir de um site de origem para um site de destino, perderá todas as informações de auditoria da hierarquia de origem.  

## <a name="privacy-information-for-migration"></a>Informações de privacidade para a migração  
 A migração Deteta informações a partir de bases de dados do site identificadas numa infraestrutura de origem e armazena estes dados na base de dados da hierarquia de destino. As informações que o System Center Configuration Manager podem detetar a partir de uma hierarquia ou um site de origem dependem das funcionalidades que foram ativadas no ambiente de origem, bem como as operações de gestão que foram efetuadas nesse ambiente de origem.  

 Para obter mais informações sobre a segurança e informações de privacidade, consulte um dos seguintes tópicos:  

-   Para obter mais informações sobre as informações de privacidade para o Configuration Manager 2007, consulte o artigo [segurança e privacidade no Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) na biblioteca de documentação do Configuration Manager 2007.  

-   Para obter mais informações sobre as informações de privacidade do System Center 2012 Configuration Manager, consulte o artigo [segurança e privacidade do System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) na biblioteca de documentação do System Center 2012 Configuration Manager.  

-   Para obter mais informações sobre as informações de privacidade para o System Center Configuration Manager, consulte o artigo [segurança e privacidade para o System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Pode migrar alguns ou todos os dados suportados de um site de origem para uma hierarquia de destino.  

A migração não está ativada por predefinição e requer vários passos de configuração. Informações de migração não são enviadas à Microsoft.  

Antes de migrar dados a partir de uma hierarquia de origem, considere os requisitos de privacidade.  

