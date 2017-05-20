---
title: "Instalar funções do sistema de sites | Documentos do Microsoft"
description: "Assistentes ajudam a adicionar funções do sistema de sites a um servidor de sistema de sites de nova ou existente no site."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 8370e3b102afed518e8154d4944ab420188faccf
ms.openlocfilehash: 76b070f8e203cc0c751f35e5a4b4904504786c04
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Instalar funções do sistema de sites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A consola do System Center Configuration Manager tem duas assistentes que pode utilizar para instalar funções do sistema de sites:  

-   **Adicionar Assistente de funções de sistema de sites**: Utilize este assistente para adicionar funções do sistema de sites a um servidor de sistema de sites existente no site.  

-   **Criar Assistente de servidor do sistema de sites**: Utilize este assistente para especificar um novo servidor como servidor de sistema de sites e, em seguida, instalar uma ou mais funções de sistema de sites no servidor. Este assistente é igual a **Adicionar Assistente de funções de sistema de sites**, exceto que na primeira página, terá de especificar o nome do servidor a utilizar e o site no qual pretende instalá-lo.  

Quando instala uma função de sistema de sites num computador remoto (incluindo uma instância do fornecedor de SMS), a conta de computador do computador remoto é adicionada a um grupo local no servidor do site. Quando o site é instalado num controlador de domínio, o grupo no servidor do site é um grupo de domínio em vez de um grupo local. Neste caso, a função de sistema de site remoto não está operacional até que os reinícios de computador de função de sistema do site ou a permissão Kerberos para a conta do computador remoto é atualizada. Para obter mais informações, veja [Contas utilizadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

Antes de instalar a função de sistema de sites, o Configuration Manager verifica o computador de destino para garantir que cumpre os pré-requisitos para as funções de sistema de sites que selecionou. Compreenda o seguinte sobre a instalação de funções do sistema de sites:  

-   Por predefinição, quando o Configuration Manager instala uma função de sistema de sites, os ficheiros de instalação são instalados na primeira unidade de disco de formatada com NTFS disponível que tenha mais disco espaço. Para impedir que o Configuration Manager instalar em unidades específicas, crie um ficheiro vazio designado **no_sms_on_drive**. Copie-o para a pasta de raiz da unidade antes de instalar o servidor de sistema de sites.  

-   O Configuration Manager utiliza o **conta de instalação do sistema de sites** para instalar funções do sistema de sites. Esta conta é especificada quando executa o assistente aplicável para criar um novo servidor de sistema de sites ou adicionar funções do sistema de sites a um servidor de sistema de sites existente. Por predefinição, esta conta é a conta de sistema local do computador do servidor do site, mas pode especificar uma conta de utilizador de domínio para utilização como conta de instalação do sistema de sites. Para obter mais informações, veja [Contas utilizadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="bkmk_Install"></a>Para instalar funções do sistema de sites num servidor de sistema de sites existente  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda a opção **Configuração do Site**e clique em **Servidores e Funções do Sistema de Sites**. Em seguida, selecione o servidor que pretende utilizar para as novas funções de sistema de sites.  

3.  No separador **Home Page** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Sites**.  

4.  No **geral** página, reveja as definições e, em seguida, clique **seguinte**.  

    > [!TIP]  
    >  Para aceder à função de sistema de sites a partir da Internet, certifique-se de que especificou um nome de domínio completamente qualificado (FQDN) da Internet.  

5.  No **Proxy** página, especifique as definições para um servidor proxy, se as funções de sistema de sites executadas neste servidor de sistema de sites exigirem um servidor proxy para estabelecer ligação a localizações na Internet. Em seguida, clique em **Seguinte**.  

6.  No **seleção da função do sistema** página, selecione as funções de sistema de sites que pretende adicionar e, em seguida, clique em **seguinte**.  

7.  Conclua o assistente.  

> [!TIP]  
>  O cmdlet do Windows PowerShell, New-CMSiteSystemServer efetua a mesma função que este procedimento. Para obter mais informações, consulte o artigo [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) na documentação do System Center 2012 Configuration Manager SP1 referência do Cmdlet.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Para instalar funções do sistema de sites um novo servidor de sistema de sites  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda a opção **Configuração do Site**e clique em **Servidores e Funções do Sistema de Sites**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**.  

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.  

    > [!TIP]  
    >  Para aceder à nova função do sistema de site a partir da Internet, certifique-se de que especifica um FQDN de Internet.  

5.  No **Proxy** página, especifique as definições para um servidor proxy, se as funções de sistema de sites executadas neste servidor de sistema de sites exigirem um servidor proxy para estabelecer ligação a localizações na Internet. Em seguida, clique em **Seguinte**.  

6.  No **seleção da função do sistema** página, selecione as funções de sistema de sites que pretende adicionar e, em seguida, clique em **seguinte**.  

7.  Conclua o assistente.  

> [!TIP]  
>  O cmdlet do Windows PowerShell, New-CMSiteSystemServer efetua a mesma função que este procedimento. Para obter mais informações, consulte o artigo [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) na documentação do System Center 2012 Configuration Manager SP1 referência do Cmdlet.  

