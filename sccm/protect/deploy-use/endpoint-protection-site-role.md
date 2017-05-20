---
title: "Criar função de sistema de sites de ponto de Endpoint Protection | Documentos do Microsoft"
description: "Saiba como configurar o Endpoint Protection para gerir a segurança e software maligno em computadores de cliente do Configuration Manager."
defintion: 
definition: 
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: af0aafb4b7209d840676d16723509f399c662aad
ms.openlocfilehash: 6e717bcbe5ef8c3f2efa717d0cebb9e675e7c127
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Criar uma função de sistema de sites de ponto de Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 A função de sistema de sites de ponto do Endpoint Protection tem de ser instalada antes de poder utilizar o Endpoint Protection. Tem de ser instalada apenas num servidor do sistema de sites e tem de ser instalada na parte superior da hierarquia num site de administração central ou num site primário autónomo.

 Utilize um dos seguintes procedimentos consoante pretenda instalar um novo servidor de sistema de sites para o Endpoint Protection ou utilizar um servidor de sistema de sites existente:
 - [Instalar um novo servidor de sistema de sites](#new-site-system-server)
 - [Instalar um servidor de sistema de sites existente](#existing-site-system-server)

> [!IMPORTANT]
>  Quando instala um ponto de Endpoint Protection, um cliente do Endpoint Protection está instalado no servidor que aloja o ponto do Endpoint Protection. Os serviços e análises estão desativados neste cliente para permitir que coexista com qualquer solução antimalware existente que esteja instalada no servidor. Se, posteriormente, ativar este servidor para gestão pelo Endpoint Protection e selecione a opção para remover qualquer solução antimalware de terceiros, o produto de terceiros não será removido. Tem de desinstalar este produto manualmente.

## <a name="new-site-system-server"></a>Novo servidor de sistema de sites

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Servidores e Funções de Sistema de Sites**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**.

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.

5.  Na página **Seleção da Função do Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Seguinte**.

6.  Na página **Endpoint Protection** , selecione a caixa de verificação **Aceito os termos de licenciamento do Endpoint Protection** e clique em **Seguinte**.

    > [!IMPORTANT]
    >  Não é possível utilizar Endpoint Protection no Configuration Manager, a menos que está a aceitar os termos de licenciamento.

7.  No **serviço de proteção de nuvem** página, selecione o nível de informações que pretende enviar à Microsoft para ajudar a desenvolver novas definições e, em seguida, clique em **seguinte**.

    > [!NOTE]
    >  Esta opção configura as definições de serviço de proteção de nuvem (anteriormente conhecido como o serviço de proteção ativa Microsoft ou mapas) que são utilizadas por predefinição. Em seguida, pode configurar definições personalizadas para cada política antimalware que criar. Aderir ao serviço de proteção de nuvem, para ajudar a manter os seus computadores mais segura fornecendo Microsoft com exemplos de software maligno que podem ajudar a Microsoft para manter as definições antimalware mais atualizados. Além disso, quando se junta o serviço de proteção de nuvem, o cliente do Endpoint Protection pode utilizar o serviço de assinatura dinâmico para transferir novas definições antes de serem publicados ao Windows Update. Para obter mais informações, consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Conclua o assistente.


## <a name="existing-site-system-server"></a>Servidor de sistema de sites existente

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  No **administração** área de trabalho, expanda **configuração do Site**, clique em **servidores e funções de sistema de sites**e, em seguida, selecione o servidor que pretende utilizar para o Endpoint Protection.

3.  No separador **Home Page** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Sites**.

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.

5.  Na página **Seleção da Função do Sistema** , selecione **Ponto do Endpoint Protection** na lista de funções disponíveis e clique em **Seguinte**.

6.  Na página **Endpoint Protection** , selecione a caixa de verificação **Aceito os termos de licenciamento do Endpoint Protection** e clique em **Seguinte**.

    > [!IMPORTANT]
    >  Não é possível utilizar Endpoint Protection no Configuration Manager, a menos que está a aceitar os termos de licenciamento.

7.  No **serviço de proteção de nuvem** página, selecione o nível de informações que pretende enviar à Microsoft para ajudar a desenvolver novas definições e, em seguida, clique em **seguinte**.

    > [!NOTE]
    >  Esta opção configura as definições de serviço de proteção de nuvem (anteriormente conhecidas como mapas) que são utilizadas por predefinição. Pode configurar definições personalizadas para cada política antimalware que configurar. Para obter mais informações, consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Conclua o assistente.

