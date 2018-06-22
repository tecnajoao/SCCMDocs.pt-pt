---
title: Gerir aplicações iOS adquiridas em volume
titleSuffix: Configuration Manager
description: Implementar, gerir e controlar licenças para aplicações compradas através de Apple iOS app store.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f94cc80d41eb346cb1d4c2fc314d310005c7b5f2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350192"
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gerir aplicações iOS adquiridas em volume com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



 Apple iOS app store permite-lhe comprar várias licenças para uma aplicação que pretende executar na empresa. Esta capacidade ajuda a reduzir a sobrecarga administrativa de controlar várias cópias das aplicações que comprou.  

 Configuration Manager o ajuda a implementar e gerir aplicações iOS que comprou a através do programa. Pode importar as informações da licença da loja de aplicações e controlar o número de licenças que estiver a utilizar.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Comprar várias licenças para aplicações iOS através do Apple Volume Purchase Program (VPP). Este processo primeiro envolve configurar uma conta Apple VPP da Apple no site. Em seguida, carregue o token VPP da Apple para o Configuration Manager, que fornece as seguintes capacidades:  

-   Sincronizar as informações de compra em volume com o Configuration Manager  
 
- Aplicações de sincronização do Apple Volume Purchase Program para empresas tanto no Apple Volume Purchase Program para as educação  

- Associar vários tokens de programa de compra da Apple com o Configuration Manager  

-   As aplicações que comprou são apresentadas na consola do Configuration Manager  

-   Implementar e monitorizar estas aplicações  

-   Controlar o número de licenças utilizadas para cada aplicação   

-   Configuration Manager pode ajudar a recuperá licenças quando exigido pela desinstalar aplicações compradas em volume que tenha implementado  



## <a name="before-you-start"></a>Antes de começar  
 Antes de começar, terá de obter um token VPP da Apple e carregá-la para o Configuration Manager.  

-   Se tiver utilizado anteriormente um token VPP com outro produto MDM na sua conta VPP da Apple, tem de gerar um novo para utilizar com o Configuration Manager.  
-   Cada token é válido durante um ano.  
-   Por predefinição, o Configuration Manager sincroniza-se com o serviço Apple VPP duas vezes por dia para garantir que as suas licenças são sincronizadas com o Configuration Manager. Apenas as alterações para as suas licenças são sincronizadas. Uma sincronização completa é executada uma vez a cada sete dias. Quando escolhe **sincronização** para fazer uma sincronização manual, esta ação sempre faz uma sincronização completa.  
-   Se precisar de recuperar ou restaurar a base de dados do Configuration Manager, recomendamos que efetue uma sincronização manual posteriormente. Este processo garante que os dados de licença sincronizadas estão atualizados.  
-   Além disso, tem importou um certificado válido de serviço (APNs) Apple Push Notification da Apple. Este certificado permite-lhe gerir dispositivos iOS, incluindo a implementação de aplicação. Para obter mais informações, consulte [configurar a gestão de dispositivos iOS híbrida](enroll-hybrid-ios-mac.md).  
-   O Configuration Manager suporta a adição de até 3.000 tokens VPP.

Pode implementar aplicações licenciadas em dispositivos e utilizadores. Consoante a capacidade de aplicações suporta o licenciamento do dispositivo, uma licença adequada foi reclamada quando a implementá-la, da seguinte forma:

|Aplicação suporta o licenciamento do dispositivo?|Tipo de coleção de implementação|Licença pedida|
|---|---|---|
|Sim|Utilizador|Licença de utilizador|
|Não|Utilizador|Licença de utilizador|
|Sim|Dispositivo|Licença de dispositivo|
|Não|Dispositivo|Licença de utilizador|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Passo 1 - obter e carregar um token VPP da Apple  

1.  Na consola do Configuration Manager, escolha **administração** > **serviços em nuvem** > **Tokens do Apple Volume Purchase Program**.   

3.  No **home page** separador o **Tokens do Apple Volume Purchase Program** grupo, escolha **adicionar Apple Volume Purchase programa Token**.  

4.  No **geral** página do **adicionar Apple Volume Purchase programa Token** assistente, configure as seguintes definições:   

    -   **Nome** -introduza um nome para este token apresentar na consola do Configuration Manager.  

    -   **Token** -escolha **procurar**e, em seguida, escolha o token VPP que transferiu a partir do web site da Apple.  

         Clique em de **conta VPP da Apple consulte** ligação. Se ainda não o fez, inscreva-se no empresas ou estabelecimentos de ensino volume purchase program. Depois de se inscreveu, transfira o token de VPP da Apple para a sua conta.  

    -   **Descrição** - como opção, introduza uma descrição para o ajudar a identificar este token na consola do Configuration Manager.  

    -   **Atribuir categorias para melhorar a procura e filtragem** - opcionalmente, pode atribuir categorias para o token VPP para facilitar a procurar na consola do Configuration Manager.  
    -   **Apple ID** -introduza o ID de correio eletrónico de apple associado o Token de VPP.
    -   **Tipo de token** -selecione o tipo de token VPP que pretende utilizar. Pode escolher **negócio** e **EDU** tipos de token.

5.  Escolha **seguinte**e, em seguida, conclua o assistente.  

Do **Tokens do Apple Volume Purchase Program** nós, pode agora ver informações sobre o token VPP da Apple. Esta vista inclui quando a última atualização, quando este expirar, e quando este foi a última sincronização.

Totalmente pode sincronizar os dados retidos pela Apple com o Configuration Manager em qualquer altura, selecionando **sincronização** no Friso.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Passo 2 - implementar uma aplicação adquirida em grandes volumes  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **informações de licença para aplicações da loja**.  

3.  Escolha a aplicação que pretende implementar, e, em seguida, no **home page** separador o **criar** grupo, escolha **Criar aplicação**.
A aplicação do Configuration Manager que é criada tem o Microsoft Store para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

    > [!IMPORTANT]  
    > Tem de escolher um objetivo de implementação **necessário**. As instalações disponíveis não são atualmente suportadas.

 Quando implementar a aplicação, é utilizada uma licença por cada utilizador, ou para instalações de dispositivo, cada dispositivo que instala a aplicação. Se visar uma coleção de dispositivos com uma aplicação que suporta o licenciamento do dispositivo, uma licença do dispositivo foi reclamada. Se visar uma coleção de dispositivos com uma aplicação que não suporta o licenciamento do dispositivo, uma licença de utilizador foi reclamada. 

 Quando criar uma aplicação a partir de **informações de licença para aplicações da loja** nó, a aplicação está associada com licenças do token da aplicação selecionada. Por exemplo, poderá ver duas versões da mesma aplicação no nó. Este comportamento é porque cada versão da aplicação está associada um token de Apple VPP diferente. Em seguida, pode criar aplicações de cada token e implementá-las separadamente.

 Para recuperar uma licença, tem de criar uma nova implementação da aplicação com uma ação de implementação **desinstalação**. Não é possível alterar a ação de implementação da implementação original. A licença é recuperada quando desinstalar a aplicação.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Passo 3 - monitorizar aplicações VPP do iOS  
 O **informações de licença para aplicações da loja** o nó do **biblioteca de Software** área de trabalho apresenta informações sobre as suas aplicações iOS compradas em volume. As informações incluem o número total de licenças que possui para cada aplicação e o número que foram implementadas. Além disso, a vista de mostra que a aplicação é associada o token VPP e o tipo do token

 Também pode monitorizar a utilização de licenças de todas as aplicações VPP que comprou a utilizando o **aplicações do Apple Volume Purchase Program para iOS com contagens de licença** relatório.  

 Este relatório mostra o nome de cada aplicação juntamente com o número total de licenças que comprou, o número de licenças disponíveis e muito mais.  

 Para obter ajuda com a execução de relatórios do Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



## <a name="delete-an-apple-vpp-token"></a>Eliminar um token de Apple VPP  
<!--505268-->

Utilize o seguinte processo para eliminar um token do Configuration Manager:  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços em nuvem** e selecione **Tokens do Apple Volume Purchase Program**.  

2. Selecione o token de que pretende eliminar.  

3. Clique em de **eliminar** opção no Friso.  

