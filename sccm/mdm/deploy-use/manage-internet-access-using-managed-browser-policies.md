---
title: "Gerir o acesso à Internet através de políticas de browser gerido | Documentos do Microsoft"
description: "Implemente o Browser gerido do Intune para gerir e restringir o acesso à Internet."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: 6
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: d2dd2c25a2714851ba1e71414cabcef38d3ce014
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gerir o acesso à Internet através de políticas de browser gerido com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, pode implementar o Browser gerido do Intune (uma aplicação de navegação na web) e associar a aplicação uma política de browser gerido. A política de browser gerido configura uma lista de permissões ou uma lista de bloqueios que restringe os sites que os utilizadores do browser gerido podem ir para.  

 Como esta aplicação é uma aplicação gerida, também pode aplicar políticas de gestão de aplicações móveis, como controlar a utilização de cortar, copiar e colar. Isto impede capturas de ecrã e também garante que as ligações para conteúdo abrem apenas noutras aplicações geridas. Para obter mais detalhes, consulte o artigo [proteger aplicações ao utilizar políticas de gestão de aplicações móveis](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Se os utilizadores instalarem sozinhos o browser gerido, este não será gerido pelas políticas que especificou. Para garantir que o browser é gerido pelo Configuration Manager, os utilizadores tem desinstalar a aplicação antes de poder implementar-para-los como uma aplicação gerida.  

 Pode criar políticas de browser gerido para os seguintes tipos de dispositivos:  

-   Dispositivos a executar o Android 4 e posterior  

-   Dispositivos que executem iOS 7 e versões posteriores  

> [!NOTE]  
>  Para obter mais informações e para transferir a aplicação de Browser gerido do Intune, consulte o artigo [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) para iOS e [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) para Android.  

## <a name="create-a-managed-browser-policy"></a>Criar uma política de browser gerido  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de gestão de aplicações**.  

3.  No **base** separador o **criar** grupo, selecione **criar política de gestão de aplicações**.  

4.  No **geral** página, introduza o nome e descrição para a política e, em seguida, selecione **seguinte**.  

5.  No **tipo de política** página, selecione a plataforma, selecione **Browser gerido** para a política de escrever e, em seguida, escolha **seguinte**.  

     Na página **Browser Gerido**, selecione uma das seguintes opções:  

    -   **Permitir que o browser gerido abra apenas os URLs listados abaixo**-especificar uma lista dos URLs que o browser gerido pode abrir.  

    -   **Bloquear o browser gerido abra os URLs listados abaixo**-especificar uma lista dos URLs que o browser gerido será impedido de abertura.  

    > [!NOTE]  
    >  Não pode incluir URLs permitidos e bloqueados na mesma política de browser gerido.  

     Para mais informações sobre os formatos de URL pode especificar, consulte o artigo formato do URL para URLs permitidos e bloqueados neste artigo.  

    > [!NOTE]  
    >  O tipo de política gerais permite-lhe alterar a funcionalidade das aplicações que implementa para ajudar a torná-las com as políticas de segurança e a conformidade da empresa. Por exemplo, pode restringir as operações de corte, cópia e colagem numa aplicação restrita. Para mais informações sobre o tipo de política gerais, consulte o artigo [proteger aplicações ao utilizar políticas de gestão de aplicações móveis](protect-apps-using-mam-policies.md).  

6.  Conclua o assistente.  

A nova política é apresentada no nó **Políticas de Gestão de Aplicações** da área de trabalho **Biblioteca de Software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Criar uma implementação de software para a aplicação de browser gerido  
 Após criar a política de browser gerido, pode criar um tipo de implementação de software para a aplicação de browser gerido. Tem de associar ambos os uma política de browser gerido e geral para a aplicação de browser gerido.  

 Para obter mais informações, consulte o artigo [criar aplicações](create-applications.md).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Segurança e privacidade do browser gerido  

-   Em dispositivos iOS, não não possível abrir os Web sites que expirou ou não fidedignos certificados.  

-   As definições que os utilizadores criam para o browser incorporado nos seus dispositivos não são utilizadas pelo browser gerido. O browser gerido não tem acesso a estas definições.  

-   Se configurar as opções **exigir simple PIN para acesso** ou **exigir credenciais da empresa para obter acesso** na política de gestão de aplicações móveis associada com o browser gerido, um utilizador pode clicar em Ajuda na página de autenticação e, em seguida, aceda a qualquer site - mesmo um adicionados a uma lista de bloqueios na política de browser gerido.  

-   O browser gerido só pode bloquear o acesso a sites quando estes são acedidos diretamente. Não pode bloquear o acesso quando são utilizados serviços intermédios (como um serviço de tradução) para aceder ao site.  

## <a name="reference-information"></a>Informações de referência  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato do URL para URLs permitidos e bloqueados  

Utilize as informações seguinte para saber mais sobre os formatos permitidos e os carateres universais que pode utilizar ao especificar os URLs na lista de permissões e bloqueios.  

-   Pode utilizar o símbolo de caráter universal ‘**\***’ de acordo com as regras na lista de padrões permitidos abaixo.  

-   Certifique-se de que adiciona o prefixo **http** ou **https** a todos os URLs quando os introduzir na lista.  

-   Pode especificar os números da porta no endereço. Se não especificar um número da porta, os valores serão:  

    -   Porta 80 para http  

    -   Porta 443 para https  

     A utilização de carateres universais para o número da porta não é suportada, por exemplo, **http://www.contoso.com:\*** e **http://www.contoso.com: /\***  

-   Utilize a tabela seguinte para saber mais sobre os padrões permitidos que pode utilizar ao especificar URLs:  

    |URL|Correspondências|Não corresponde|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Corresponde a uma única página|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Corresponde a uma única página|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Corresponde a todos os URLs a começar com www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Corresponde a todos os subdomínios em contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Corresponde a uma única pasta|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Corresponde a uma única página, ao utilizar um número de porta|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Corresponde a uma única página segura|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Corresponde a uma única pasta e a todas as subpastas|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Seguem-se exemplos de algumas entradas que não pode especificar:  

    -   *.com  

    -   *.contoso /\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   Endereços IP  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: /*  

> [!NOTE]  
>  *. microsoft.com é sempre permitido.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Como são resolvidos os conflitos entre a lista de permissões e de bloqueios  
 Se forem implementadas várias políticas de browser gerido num dispositivo e as definições entrarem em conflito, o modo (permitido ou bloqueado) e as listas de URLs são avaliados em relação a conflitos. No caso de existir um conflito, aplica-se o seguinte comportamento:  

-   Se os modos em cada política forem os mesmos mas as listas de URLs forem diferentes, os URLs não serão impostos no dispositivo.  

-   Se os modos em cada política forem diferentes mas as listas de URLs forem as mesmas, os URLs não serão impostos no dispositivo.  

-   Se um dispositivo estiver a receber políticas de browser gerido pela primeira vez e duas políticas entrarem em conflito, os URLs não serão impostos no dispositivo. Utilize o nó **Conflitos de Política** da área de trabalho **Política** para ver os conflitos.  

-   Se um dispositivo já tiver recebido uma política de browser gerido e for implementada uma segunda política com definições em conflito, as definições originais permanecem no dispositivo. Utilize o nó **Conflitos de Política** da área de trabalho **Política** para ver os conflitos.  
