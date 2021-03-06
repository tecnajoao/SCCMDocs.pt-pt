---
title: Confirmar os requisitos de nomes de domínio
titleSuffix: Configuration Manager
description: Certifique-se os requisitos de nome de domínio com o System Center Configuration Manager.
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e80a001153012763f56686df66ab7c6fcbf9b88
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127393"
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confirmar os requisitos de nome de domínio com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se necessário, siga os passos seguintes para satisfazer as dependências externas ao Configuration Manager:

1. Cada utilizador tem de ter uma licença do Intune atribuída a inscrição de dispositivos. Para associar as licenças do Intune aos utilizadores, cada utilizador tem de ter um nome de principal de utilizador (UPN) que pode ser resolvido publicamente (por exemplo, johndoe@contoso.com) ou um ID de início de sessão alternativo configurado no Azure Active Directory. Configurar um ID de início de sessão alternativo permite aos utilizadores iniciar sessão com um endereço de e-mail, por exemplo, mesmo que o respetivo UPN está num formato NetBIOS (por exemplo, contoso\diogoandrade).

   - Se a sua empresa utiliza UPNs resolvíveis publicamente (ou seja, johndoe@contoso.com), é necessária nenhuma configuração adicional.
   - Se a sua empresa utiliza um UPN não puder ser resolvido (ou seja, contoso\diogoandrade), deve [configurar um ID alternativo no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2. Implementar e configurar serviços de Federação do Active Directory (AD FS). (Opcional)

    Quando configurar o início de sessão único, os utilizadores podem iniciar sessão com as credenciais da empresa para acessar os serviços no Intune.

    Para obter mais informações, consulte os tópicos seguintes:
   -   [Preparar para início de sessão único](http://go.microsoft.com/fwlink/?LinkID=271124)
   -   [Planear e implementar o AD FS 2.0 para utilização com o início de sessão único](http://go.microsoft.com/fwlink/?LinkID=271125)

3. Implemente e configure a sincronização de diretórios.

    Sincronização de diretórios permite-lhe preencher o Intune com contas de utilizador sincronizado. As contas de utilizador sincronizadas e os grupos de segurança são adicionados ao Intune. A incapacidade de ativar a sincronização do Directory é uma das causas comuns pelos quais os dispositivos não conseguem inscrever-se durante a configuração do MDM do Configuration Manager com o Microsoft Intune.

    Para obter mais informações, veja [Integração de diretórios](http://go.microsoft.com/fwlink/?LinkID=271120) na biblioteca de documentação do Active Directory.

4. Opcional, mas não recomendado: Se não estiver a utilizar serviços de Federação do Active Directory, repor palavras-passe de Microsoft Online dos utilizadores.

    Se não estiver a utilizar o AD FS, tem de definir uma palavra-passe do Microsoft Online para cada utilizador.

> [!div class="button"]
> [< Anterior passo](create-mdm-collection.md)[passo seguinte >](configure-intune-subscription.md)
