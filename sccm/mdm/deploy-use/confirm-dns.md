---
title: "Confirmar os requisitos de nome de domínio com o System Center Configuration Manager | Documentos do Microsoft"
description: "Confirme os requisitos de nome de domínio com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: 18
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 35b24294073956a6bdb14cae07705f56d31e00a9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confirmar os requisitos de nome de domínio com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se necessário, execute os seguintes passos para satisfazer as dependências do externas ao Configuration Manager:

1. Cada utilizador tem de ter uma licença do Intune atribuída para inscrever dispositivos. Para associar as licenças do Intune aos utilizadores, cada utilizador tem de ter um nome de principal de utilizador (UPN) que pode ser resolvido publicamente (por exemplo, johndoe@contoso.com) ou um ID de início de sessão alternativo configurado no Azure Active Directory. Configurar um ID de início de sessão alternativo permite que os utilizadores iniciem sessão com um endereço de e-mail, por exemplo, mesmo que o respetivo UPN está num formato NetBIOS (por exemplo, contoso\diogoandrade).

  - Se a sua empresa utiliza UPNs resolvível publicamente (ou seja, johndoe@contoso.com), não é necessária nenhuma configuração adicional.
  - Se a sua empresa utiliza um UPN não resolvível (ou seja, contoso\diogoandrade), tem [configurar um ID alternativo no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Implementar e configurar serviços de Federação do Active Directory (AD FS). (Opcional)

     Quando configurar o início de sessão único, os utilizadores podem iniciar sessão com as respetivas credenciais empresariais para aceder aos serviços do Intune.

     Para obter mais informações, consulte os tópicos seguintes:
    -   [Preparar para o início de sessão único](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planear e implementar o AD FS 2.0 para utilização com o início de sessão único](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Implemente e configure a sincronização de diretórios.

     Sincronização de diretórios permite-lhe preencher o Intune com contas de utilizador sincronizadas. As contas de utilizador sincronizadas e os grupos de segurança são adicionados ao Intune. A incapacidade de ativar a sincronização do Directory é uma das causas comuns pelos quais os dispositivos não conseguem inscrever-se durante a configuração do MDM do Configuration Manager com o Microsoft Intune.

     Para obter mais informações, veja [Integração de diretórios](http://go.microsoft.com/fwlink/?LinkID=271120) na biblioteca de documentação do Active Directory.

4.  Opcional, não recomendado: Se não estiver a utilizar serviços de Federação do Active Directory, repor palavras-passe de Microsoft Online dos utilizadores.

     Se não estiver a utilizar o AD FS, tem de definir uma palavra-passe do Microsoft Online para cada utilizador.

> [!div class="button"]
[< Passo anterior](create-mdm-collection.md)[junto passo >  ](configure-intune-subscription.md)

