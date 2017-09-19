---
title: "Windows Hello para definições da empresa | Microsoft Docs"
description: Saiba como integrar o Windows Hello para empresas com o System Center Configuration Manager.
ms.custom: na
ms.date: 08/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 1985428df0f82ef2e0a92fdec86189d5ffa03aee
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Definições do Windows Hello para Empresas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager permite-lhe integrar com o Windows Hello para empresas (anteriormente o Microsoft Passport for Windows), que é um método de início de sessão alternativo para dispositivos Windows 10. O Hello para Empresas utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual.  

Com o Hello para Empresas, pode utilizar um **gesto de utilizador** para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.

[Saber mais sobre o Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 O Configuration Manager integra-se com o Windows Hello para empresas de duas formas:  

-   Pode utilizar o Configuration Manager para controlar que utilizadores gestos podem e não podem utilizar para iniciar sessão.  

-   Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Windows Hello para Empresas. Para obter mais informações, consulte [perfis de certificado](introduction-to-certificate-profiles.md).  

- Pode implementar o Windows Hello para empresas as políticas para dispositivos Windows 10 associados a um domínio, que executam o cliente do Configuration Manager. Esta configuração está descrita na [configurar o Windows Hello para empresas nos dispositivos Windows 10 associados a domínios](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), abaixo. Quando utilizar o Configuration Manager com o Microsoft Intune (híbrido), pode configurar estas definições em dispositivos Windows 10 Mobile e Windows 10. Consulte [configurar o Windows Hello para empresas definições (híbrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md) para obter mais informações.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para empresas nos dispositivos Windows 10 associados a domínios
Pode controlar o Windows Hello para definições de negócio em dispositivos Windows 10 associados a domínios através da criação e implementação de um Windows Hello para empresas perfil. Esta é a abordagem recomendada.


Se estiver a utilizar autenticação baseada em certificado, terá também de implementar um perfil de certificado, conforme descrito em [configurar um perfil de certificado](#configure-a-certificate-profile). Se estiver a utilizar autenticação baseada em chave, não é necessário implementar um perfil de certificado.

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurar um Windows perfil Hello para empresas  

Na consola do Configuration Manager, em **acesso a recursos da empresa**, faça duplo clique **Windows Hello para empresas perfis** e escolha **novo** para iniciar o Assistente de perfil. Forneça as definições do pedido pelo assistente, reveja e confirme as definições na última página e clique em **fechar**. Eis um exemplo de que as suas definições poderão ter o seguinte aspeto:  

![Definições do Windows Hello para Empresas](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurar um perfil de certificado para inscrever o certificado de inscrição do Windows Hello para Empresas no Configuration Manager  
 Se pretender utilizar o Windows Hello para início de sessão do negócio baseada em certificados, configure o seguinte:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que utilize a EKU de início de sessão do Smart Card.  

-   Se pretende armazenar os perfis de certificado no Windows Hello para o contentor de chaves de negócio e o perfil de certificado utiliza o **início de sessão de Smart Card** EKU, tem de configurar as seguintes permissões para o registo de chave garantir que o certificado é validado corretamente.
Primeiro tem de criar o **chave Admins** grupo e adicionar toda a gestão do Configuration Manager os computadores do ponto como membros a este grupo.

Algumas configurações poderão não ser necessário configurar permissões, ou que possam necessitar de mais configurações. A tabela seguinte para obter mais ajuda, consulte:

|||||
|-|-|-|-|
|Versão de cliente do Windows|Configuration Manager 1602 1606|1610 o Configuration Manager|Gestor de configuração 1702 ou posterior|
|Atualização do Windows 10 Anniversary|Não existem correção necessária<br><br>Não existem permissões necessárias<br><br>Não existe nenhuma atualização de esquema do Windows necessária|Não existem correção necessária<br><br>Não existem permissões necessárias<br><br>Não existe nenhuma atualização de esquema do Windows necessária|Não é necessária nenhuma ação|
|Atualização do Windows 10 criadores ou posterior|Não suportado|Instalar [Esta correção](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 ao Active Directory|Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 ao Active Directory|

## <a name="to-configure-permissions"></a>Configurar as permissões

1.  Início de sessão para um domínio controlador ou a gestão de estações de trabalho com o administrador de domínio, ou equivalentes credenciais.
2.  Abra **utilizadores e computadores do Active Directory**.
3.  No painel de navegação, clique no seu nome de domínio e, em seguida, clique em **propriedades**.
4.  No **segurança** separador do * <domain name> * **propriedades** caixa de diálogo, clique em **avançadas**. Se o **segurança** separador não for apresentado, ative **funcionalidades avançadas** do **vista** menu de **computadores e utilizadores do Active Directory**.
5.  Clique em **Adicionar**.
6.  No **entrada de permissão para** * <domain name> * caixa de diálogo, clique em **selecionar um principal**.
7.  No **selecionar utilizador, computador, conta de serviço ou grupo** caixa de diálogo, escreva **chave Admins** no **introduza o nome de objeto a selecionar** caixa de texto.  Clique em **OK**.
8.  Do **aplica-se a** lista, selecione **objetos de utilizador descendente**.
9.  Desloque-se na parte inferior da página e clique em **Desmarcar tudo**.
10. No **propriedades** secção, selecione **ler msDS-KeyCredentialLink**.
11. Clique em **OK** três vezes para concluir a tarefa.


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações, consulte [perfis de certificado](introduction-to-certificate-profiles.md).  




