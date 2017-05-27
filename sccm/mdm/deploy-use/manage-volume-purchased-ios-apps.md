---
title: "Gerir as aplicações iOS adquiridos volume | Documentos do Microsoft"
description: "Implementar, gerir e controlar licenças para aplicações que adquiriu através da loja de aplicações iOS."
ms.custom: na
ms.date: 05/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4cb711f369698fe8e045f8c83dd96ec6fb29d70
ms.openlocfilehash: ce706e938f558406044f7890c80bb7156c3b262b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gerir aplicações iOS adquiridas em volume com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



 Loja de aplicações iOS permite-lhe comprar várias licenças para uma aplicação que pretende executar na sua empresa. Isto ajuda a reduzir a sobrecarga administrativa de rastrear várias cópias das aplicações que comprou.  

 System Center Configuration Manager ajuda-o a implementar e gerir as aplicações iOS que comprou através do programa ao importar as informações da licença da loja de aplicações e controlar o número de licenças que estão a ser utilizados.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Comprar várias licenças para aplicações iOS através do programa de compra do Apple Volume (VPP). Isto envolve a configurar uma conta Apple VPP a partir do web site da Apple e carregar o token de Apple VPP do Configuration Manager, que fornece as seguintes capacidades:  

-   Sincronize as suas informações de compra do volume com o Configuration Manager. 
 
- Aplicações de sincronização a partir do programa de compra da Apple Volume para empresas e o programa de compra de Volume Apple para educação.

- Associe várias tokens de programa de compra de volume Apple com o Configuration Manager.

-   As aplicações que comprou são apresentadas na consola do Configuration Manager.  

-   Pode implementar aplicações, estas aplicações de monitorização e controlar o número de licenças para cada aplicação que foi utilizado.  

-   Gestor de configuração podem ajudar a recuperar licenças quando exigido pela desinstalar aplicações adquirido o volume que tenha implementado.  

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar, terá de obter um VPP token da Apple e carregar este para o Configuration Manager.  

-   Se tiver utilizado anteriormente um token VPP com um produto MDM diferentes na sua conta Apple VPP existente, tem de gerar um novo para utilizar com o Configuration Manager.  
-   Cada token é válido durante um ano.  
-   Por predefinição, o Configuration Manager sincroniza com o serviço Apple VPP duas vezes por dia para se certificar de que as licenças são sincronizadas com o Configuration Manager.  
      Apenas as alterações para as licenças são sincronizadas. No entanto, uma vez a cada sete dias, irá ser efetuada uma sincronização completa.  
      Quando escolher **sincronização** para efetuar uma sincronização manual, este irá fazer sempre uma sincronização completa.  
-   Se precisar de recuperar nem de restaurar a base de dados do Configuration Manager, recomendamos que efetue uma sincronização manual posteriormente para garantir que os dados de licença sincronizada são atualizados.  
-   Além disso, deve importar um certificado de serviço (APNs) válido do Apple Push Notification da Apple e permite-lhe gerir dispositivos iOS, incluindo a implementação de aplicação. Para obter mais informações, consulte o artigo [configurar a gestão de dispositivos iOS híbrida](enroll-hybrid-ios-mac.md).  
-   O Configuration Manager suporta a adição de até 3000 tokens VPP.

A partir do System Center Configuration Manager 1702, pode agora implementar aplicações licenciadas dispositivos, bem como os utilizadores. Dependendo da capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando implementá-la, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|A aplicação suporta licenciamento do dispositivo?|Tipo de coleção de implementação|Licença alegada|
|Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Passo 1 - obter e carregar um token VPP da Apple  

1.  Na consola do Configuration Manager, escolha **administração** > **serviços em nuvem** > **Apple Volume compra programa Tokens**.   

3.  No **base** separador o **Apple Volume compra programa Tokens** grupo, selecione **adicionar Apple Volume compra programa Token**.  

4.  No **geral** página do **adicionar Apple Volume compra programa Token** assistente, configure as seguintes opções:   

    -   **Nome** -introduza um nome para este token, tal como será apresentado na consola do Configuration Manager.  

    -   **Token** -escolher **procurar**e, em seguida, escolha o token VPP transferido do web site da Apple.  

         Escolha o **conta Consulte VPP Apple** associar e, se ainda não o fez, inscreva-se o programa de compra de volume de empresas ou para educação. Depois de se é inscreveu, transfira o token de Apple VPP da sua conta.  

    -   **Descrição** - opcionalmente, introduza uma descrição que irão ajudar a identificar este token VPP na consola do Configuration Manager.  

    -   **Categorias para melhorar a procura e filtragem atribuídas** - opcionalmente, pode atribuir categorias para o token VPP para facilitar a procura na consola do Configuration Manager.  
    -   **Apple ID** -introduza o ID de correio eletrónico apple associado a VPP Token.
    -   **Tipo de token** -selecione o tipo de token VPP que pretende utilizar. Pode escolher **empresas** e **Enterprise** token tipos.

5.  Escolher **seguinte**e, em seguida, conclua o assistente.  

A partir de **Apple Volume compra programa Tokens** nó, agora pode ver informações sobre o Apple VPP token incluindo quando-foi atualizado pela última, quando a mesma irá expirar e quando que foi sincronizado pela última.

Totalmente pode sincronizar os dados a ser retidos pela Apple com o Configuration Manager em qualquer altura ao escolher **sincronização** no **base** separador o **sincronização** grupo.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Passo 2 - implementar uma aplicação adquirida em grandes volumes  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **informações de licença de aplicações da loja**.  

3.  Escolha a aplicação que pretende implementar, e, em seguida, no **base** separador o **criar** grupo, selecione **Criar aplicação**.
A aplicação do Configuration Manager que é criada tem empresas aplicação na loja Windows. Pode, em seguida, implementar e monitorizar esta aplicação, tal como faria com qualquer outra aplicação do Configuration Manager.

    > [!IMPORTANT]  
    > Tem de escolher um objetivo de implementação **necessário**. Instalações disponíveis não são atualmente suportadas.

 Quando implementar a aplicação, uma licença é utilizada por cada utilizador ou para instalações do dispositivo, cada dispositivo que instala a aplicação.  Se destinar uma coleção de dispositivos com uma aplicação que suporta o licenciamento do dispositivo, uma licença do dispositivo foi reclamada.  Se destinar uma coleção de dispositivos com uma aplicação que não suporta o licenciamento do dispositivo, uma licença de utilizador foi reclamada. 

 Quando cria uma aplicação a partir de **informações de licença de aplicações da loja** nó, a aplicação está associada a licenças de token para a aplicação selecionada.  Por exemplo, poderá ver duas versões da aplicação no nó do mesma. Isto acontece porque cada versão da aplicação está associada a um token de Apple VPP diferentes.  Em seguida, poderia criar aplicações a partir de cada token e implementá-las em separado.

 Para recuperar uma licença, terá de criar uma nova implementação da aplicação com uma ação de implementação **desinstalar**. Não é possível alterar a ação de implementação da implementação original. A licença será reclamada depois de desinstala a aplicação.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Passo 3 - monitorizar aplicações VPP do iOS  
 O **informações de licença de aplicações da loja** nó do **biblioteca de Software** área de trabalho apresenta informações sobre as suas aplicações iOS adquiridos de volume. As informações incluem o número total de licenças que possui para cada aplicação e o número que foram implementadas. Além disso, a vista mostra o token VPP se encontra associada a aplicação e o tipo de token

 Também é possível monitorizar a utilização de licenças de todas as aplicações VPP que comprou, utilizando o **aplicações para iOS com contagens de licença o programa de compra da Apple Volume** relatório.  

 Este relatório mostra o nome de cada aplicação juntamente com o número total de licenças que comprou, o número de licenças disponíveis e muito mais.  

 Para obter ajuda com a execução de relatórios do Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

