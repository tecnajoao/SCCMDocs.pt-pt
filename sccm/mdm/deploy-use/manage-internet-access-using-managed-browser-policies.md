---
title: Gerir o acesso à Internet através de políticas de browser gerido
titleSuffix: Configuration Manager
description: Implemente o Intune Managed Browser para gerir e restringir o acesso à Internet.
ms.date: 07/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ede2563adbd517dbcda0a408fa5b9b166e8e3c12
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129362"
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gerir o acesso à Internet através de políticas de browser gerido com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, pode implementar o Intune Managed Browser (uma aplicação web) e associar a aplicação uma política de browser gerido. Política de browser gerido configura uma lista de permissões ou uma lista de bloqueios que restringe os sites que os utilizadores do browser gerido podem aceder.  

 Uma vez que esta aplicação é uma aplicação gerida, também pode aplicar políticas de gestão de aplicações móveis, como controlar a utilização de cortar, copiar e colar. Isso impede as capturas de ecrã e também garante que apenas abrir ligações para conteúdo em outras aplicações geridas. Para obter detalhes, consulte [proteger aplicações através de políticas de gestão de aplicações móveis](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Se os utilizadores instalarem sozinhos o browser gerido, este não será gerido pelas políticas que especificou. Para garantir que o browser é gerido pelo Configuration Manager, é necessário desinstalar a aplicação antes de poder implementar a eles como uma aplicação gerida.  

 Pode criar políticas de browser gerido para os seguintes tipos de dispositivos:  

-   Dispositivos a executar o Android 4 e posterior  

-   Dispositivos que executem iOS 7 e versões posteriores  

> [!NOTE]  
>  Para obter mais informações e para transferir a aplicação de Browser gerido do Intune, veja [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) para iOS e [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) para Android.  

## <a name="create-a-managed-browser-policy"></a>Criar uma política de browser gerido  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de gestão de aplicações** .  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar política de gestão de aplicações**.  

4.  Sobre o **gerais** página, introduza o nome e descrição para a política e, em seguida, escolha **próxima**.  

5.  Sobre o **tipo de política** página, selecione a plataforma, selecione **Managed Browser** para a política escreva e, em seguida, escolha **seguinte**.  

     Na página **Browser Gerido**, selecione uma das seguintes opções:  

    -   **Permitir que o browser gerido abra apenas os URLs listados abaixo**– especificar uma lista de URLs que o browser gerido pode abrir.  

    -   **Bloquear o browser gerido de abrir os URLs listados abaixo**– especificar uma lista de URLs que o browser gerido não poderá abrir.  

    > [!NOTE]  
    >  Não pode incluir URLs permitidos e bloqueados na mesma política de browser gerido.  

     Para obter mais informações sobre os formatos de URL que pode especificar, consulte o formato de URL para URLs permitidos e bloqueados neste artigo.  

    > [!NOTE]  
    >  O tipo de política geral permite que altere a funcionalidade das aplicações que implementa para ajudar a torná-los com a conformidade da empresa e as políticas de segurança. Por exemplo, pode restringir as operações de corte, cópia e colagem numa aplicação restrita. Para obter mais informações sobre o tipo de política geral, consulte [proteger aplicações através de políticas de gestão de aplicações móveis](protect-apps-using-mam-policies.md).  

6.  Conclua o assistente.  

A nova política é apresentada no nó **Políticas de Gestão de Aplicações** da área de trabalho **Biblioteca de Software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Criar uma implementação de software para a aplicação de browser gerido  
 Após criar a política de browser gerido, pode criar um tipo de implementação de software para a aplicação de browser gerido. Tem de associar ambos os uma política de browser gerido e geral para a aplicação de browser gerido.  

 Para obter mais informações, consulte [criem aplicativos](create-applications.md).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Segurança e privacidade do browser gerido  

-   Em dispositivos iOS, não não possível abrir os Web sites que tenham expirado ou não considerada como fidedigna certificados.  

-   As definições que os utilizadores criam para o browser incorporado nos seus dispositivos não são utilizadas pelo browser gerido. O browser gerido não tem acesso a estas definições.  

-   Se configurar as opções **exigir PIN simples para acesso** ou **exigir credenciais da empresa para obter acesso** na política de gestão de aplicações móveis associada ao browser gerido, um utilizador pode clicar em Ajuda na página de autenticação e, em seguida, passa a qualquer site – até mesmo um adicionado a uma lista de bloqueios na política de browser gerido.  

-   O browser gerido só pode bloquear o acesso a sites quando estes são acedidos diretamente. Não pode bloquear o acesso quando são utilizados serviços intermédios (como um serviço de tradução) para aceder ao site.  

## <a name="reference-information"></a>Informações de referência  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato do URL para URLs permitidos e bloqueados  

Utilize as informações seguinte para saber mais sobre os formatos permitidos e os carateres universais que pode utilizar ao especificar os URLs na lista de permissões e bloqueios.  

- Utilizar o símbolo de caráter universal `*` (asterisco), de acordo com as regras na lista de padrões permitidos abaixo.  

- Todas as URLs com o prefixo **http** ou **https** quando os introduzir na lista.  

- Especifica os números de porta no endereço. Se não especificar um número de porta, são utilizados os seguintes valores:  

  - Porta 80 para http  

  - Porta 443 para https  

    Não utilize carateres universais para o número de porta, o que não é suportado. Por exemplo, `http://www.contoso.com:*`   

- Utilize a tabela seguinte para saber mais sobre os padrões permitidos que pode utilizar ao especificar URLs:  


  |                                           URL                                            |                                                    Correspondências                                                    |                                    Não corresponde                                     |
  |------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
  |                `http://www.contoso.com`<br /><br /> Corresponde a uma única página                |                                               `www.contoso.com`                                               |  `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `contoso.com/`   |
  |                  `http://contoso.com`<br /><br /> Corresponde a uma única página                  |                                                 `contoso.com`                                                 | `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com` |
  | `http://www.contoso.com/*`<br /><br /> Corresponde a todos os URLs a partir do `www.contoso.com` |      `www.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com/videos/tvshows`      |               `host.contoso.com`<br /><br /> `host.contoso.com/images`                |
  |      `http://*.contoso.com/*`<br /><br /> Corresponde a todos os subdomínios em contoso.com      | `developer.contoso.com/resources`<br /><br /> `news.contoso.com/images`<br /><br /> `news.contoso.com/videos` |                                  `contoso.host.com`                                   |
  |           `http://www.contoso.com/images`<br /><br /> Corresponde a uma única pasta            |                                           `www.contoso.com/images`                                            |                             `www.contoso.com/images/dogs`                             |
  |    `http://www.contoso.com:80`<br /><br /> Corresponde a uma única página, ao utilizar um número de porta    |                                          `http://www.contoso.com:80`                                          |                                                                                       |
  |           `https://www.contoso.com`<br /><br /> Corresponde a uma única página segura            |                                           `https://www.contoso.com`                                           |                               `http://www.contoso.com`                                |
  | `http://www.contoso.com/images/*`<br /><br /> Corresponde a uma única pasta e a todas as subpastas |                    `www.contoso.com/images/dogs`<br /><br /> `www.contoso.com/images/cats`                    |                               `www.contoso.com/videos`                                |


- Seguem-se exemplos de algumas entradas que não pode especificar:  

  -   `*.com`  

  -   `*.contoso/*`  

  -   `www.contoso.com/*images`  

  -   `www.contoso.com/*images*pigs`  

  -   `www.contoso.com/page*`  

  -   Endereços IP  

  -   `https://*`  

  -   `http://*`  

  -   `http://www.contoso.com:*`  

  -   `http://www.contoso.com: /*`  

> [!NOTE]  
>  `*.microsoft.com` é sempre permitido.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Como são resolvidos os conflitos entre a lista de permissões e de bloqueios  
 Se forem implementadas várias políticas de browser gerido num dispositivo e as definições entrarem em conflito, o modo (permitido ou bloqueado) e as listas de URLs são avaliados em relação a conflitos. No caso de existir um conflito, aplica-se o seguinte comportamento:  

-   Se os modos em cada política forem os mesmos, mas as listas de URLs forem diferentes, os URLs não serão impostos no dispositivo.  

-   Se os modos em cada política forem diferentes, mas as listas de URLs são os mesmos, os URLs não serão impostos no dispositivo.  

-   Se um dispositivo estiver a receber políticas de browser gerido pela primeira vez e duas políticas entrarem em conflito, os URLs não serão impostos no dispositivo. Utilize o nó **Conflitos de Política** da área de trabalho **Política** para ver os conflitos.  

-   Se um dispositivo já tiver recebido uma política de browser gerido e for implementada uma segunda política com definições em conflito, as definições originais permanecem no dispositivo. Utilize o nó **Conflitos de Política** da área de trabalho **Política** para ver os conflitos.  
