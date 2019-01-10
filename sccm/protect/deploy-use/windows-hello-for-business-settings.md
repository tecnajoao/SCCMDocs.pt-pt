---
title: Definições do Windows Hello para Empresas
titleSuffix: Configuration Manager
description: Saiba como integrar o Windows Hello para empresas com o Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81086b01cef3d60af6e0c93d25b2ad937252d4ba
ms.sourcegitcommit: 94bf7d5b5beb9628cc1fdfe75451d33b5de26f8a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152405"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Windows Hello para empresas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1245704--> O Configuration Manager permite integrar com o Windows Hello para empresas (anteriormente chamado Microsoft Passport para Windows), que é um método de-de início de sessão alternativo para dispositivos Windows 10. O Hello para Empresas utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual. O Hello para empresas permite-lhe utilizar um **gesto de utilizador** para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.


> [!Important]  
> A partir de Dezembro de 2017, Windows Hello para empresas no Configuration Manager é uma [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Implantação do Windows Server 2016 Active Directory Federation serviços autoridade de registo (RA-ADFS) é mais simples, fornece uma melhor experiência de utilizador e tem uma experiência de inscrição de certificados mais determinística.  


Para obter mais informações, consulte [Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).


> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


O Configuration Manager integra-se com o Windows Hello para empresas de duas formas:  

- Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem em não podem utilizar para iniciar sessão.  

- Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Windows Hello para Empresas. Para obter mais informações, consulte [perfis de certificado](introduction-to-certificate-profiles.md).  

- Pode implantar Windows Hello para políticas de negócio para dispositivos Windows 10 associados a um domínio, que executam o cliente do Configuration Manager. Esta configuração está descrita na [configurar o Windows Hello para empresas em dispositivos do Windows 10 associados a um domínio](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) secção. Quando utiliza o Configuration Manager com o Microsoft Intune (híbrido), pode configurar estas definições em dispositivos Windows 10 Mobile e Windows 10. Para obter mais informações, consulte [configurar o Windows Hello para empresas (híbrido) de definições](/sccm/mdm/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para empresas em dispositivos do Windows 10 associados a um domínio

Pode controlar o Windows Hello para empresas em dispositivos do Windows 10 associados a um domínio, criando e implantando um Windows Hello para empresas de perfil. Essa abordagem é recomendada.


Se estiver a utilizar autenticação baseada em certificado, tem também de implementar um perfil de certificado, conforme descrito em [configurar um perfil de certificado](#configure-a-certificate-profile). Se estiver a utilizar autenticação baseada em chave, não é necessário implementar um perfil de certificado.



## <a name="configure-a-windows-hello-for-business-profile"></a>Configurar um Windows perfil Hello para empresas  

Na consola do Configuration Manager, sob **acesso a recursos da empresa**, clique com botão direito **Windows Hello para empresas perfis** e escolha **New** para iniciar o Assistente de perfil. Forneça as definições do pedido pelo assistente, reveja e confirme as definições na última página e clique em **fechar**. Eis um exemplo de definições do possam aparência:  

![Windows Hello para o Assistente de política de negócio, que mostra a lista de definições disponíveis](../media/Hello-for-Business-settings.png)



## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurar um perfil de certificado para inscrever o certificado de inscrição do Windows Hello para Empresas no Configuration Manager  

Se pretender utilizar o Windows Hello para início de sessão baseada em certificados de empresa, configure os seguintes componentes:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que utilize a EKU de início de sessão do Smart Card.  

-   Se pretende armazenar os perfis de certificado do Windows Hello para o contentor de chaves de negócios e o perfil de certificado utiliza a **início de sessão de Smart Card** EKU, tem de configurar as seguintes permissões para o registo de chave garantir que o certificado é validado corretamente.
Primeiro tem de criar o **os administradores de chave** agrupar e adicionados a toda a gestão do Configuration Manager computadores do ponto como membros a este grupo.

Algumas configurações poderão não ser necessário configurar permissões ou podem requerer ainda mais configurações. Consulte a tabela seguinte para obter mais ajuda:

|Versão de cliente do Windows|Configuration Manager versão 1602 ou 1606|Configuration Manager versão 1610|Gestor de configuração 1702 ou posterior|
|-|-|-|-|
|Windows 10 Anniversary Update|Sem correções necessárias<br><br>Não existem permissões necessárias<br><br>Nenhuma atualização de esquema do Windows necessária|Sem correções necessárias (consulte **aviso**)<br><br>Não existem permissões necessárias<br><br>Nenhuma atualização de esquema do Windows necessária|Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 para o Active Directory|
|Atualização para criativos do Windows 10 ou posterior|Não suportado|Instalar [Esta correção](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 para o Active Directory|Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 para o Active Directory|

> [!WARNING]
> Embora [a correção](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) não é necessário para a versão 1610 do Configuration Manager e de atualização de aniversário do Windows 10, ele pode ser instalado.  Se a correção está instalada, terá de configurar permissões e aplicar o esquema do Windows Server 2016 para o Active Directory.

## <a name="to-configure-permissions"></a>Para configurar as permissões

1.  Inicie sessão no controlador de domínio ou estações de trabalho de gestão com o administrador de domínio ou as credenciais equivalentes.
2.  Open **utilizadores e computadores do Active Directory**.
3.  No painel de navegação, seu nome de domínio com o botão direito e, em seguida, clique em **propriedades**.
4.  Sobre o **segurança** separador da *<domain name>* **propriedades** caixa de diálogo, clique em **avançadas**. Se o **segurança** separador não for apresentado, ative **funcionalidades avançadas** do **vista** menu de **Active Directory Users and Computers**.
5.  Clique em **Adicionar**.
6.  Na **entrada de permissão para** *<domain name>* caixa de diálogo, clique em **selecionar um principal**.
7.  Na **selecionar utilizador, computador, conta de serviço ou grupo** caixa de diálogo, escreva **Admins de chave** no **introduza o nome de objeto a selecionar** caixa de texto. Clique em **OK**.
8.  Do **aplica-se ao** lista, selecione **objetos de utilizador de descendente**.
9.  Desloque-se para a parte inferior da página e clique em **Limpar tudo**.
10. Na **propriedades** secção, selecione **ler msDS-KeyCredentialLink**.
11. Clique em **OK** três vezes para concluir a tarefa.


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações, consulte [perfis de certificado](introduction-to-certificate-profiles.md).  




