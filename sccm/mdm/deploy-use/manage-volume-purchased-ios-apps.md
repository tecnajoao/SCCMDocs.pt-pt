---
title: Gerir aplicações iOS adquiridas em volume
titleSuffix: Configuration Manager
description: Implementar, gerir e controlar licenças de aplicações que comprou na loja de aplicações iOS da Apple.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21d8666f6c05b540891037cc1917b755ed22fdcc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129397"
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gerir aplicações iOS adquiridas em volume com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



 Apple iOS app store permite-lhe comprar várias licenças para uma aplicação que pretende executar na sua empresa. Esta capacidade ajuda a reduzir a sobrecarga administrativa de controlar múltiplas cópias das aplicações que comprou.  

 O Configuration Manager ajuda-o a implementar e gerir aplicações iOS adquiridos através do programa. Pode importar as informações da licença a partir da app store e controlar o número de licenças que está a utilizar.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerir aplicações compradas em grandes volumes para dispositivos iOS  
 Compra várias licenças para aplicações iOS através do Apple Volume Purchase Program (VPP). Este processo envolve, primeiro, como configurar uma conta Apple VPP no site da Apple. Em seguida, carregue o token VPP da Apple para o Configuration Manager, que fornece as seguintes capacidades:  

-   Sincronizar as informações de compra de volume com o Configuration Manager  
 
- Aplicações de sincronização do Apple Volume Purchase Program for Business, tanto o Apple Volume Purchase Program for Education  

- Associar vários tokens do programa de compra em volume da Apple com o Configuration Manager  

-   Aplicações que comprou são apresentadas na consola do Configuration Manager  

-   Implementar e monitorizar estas aplicações  

-   Controlar o número de licenças utilizadas para cada aplicação   

-   O Configuration Manager pode ajudá-lo a recuperar licenças quando exigido pela desinstalar aplicações compradas em volume que tenha implementado  



## <a name="before-you-start"></a>Antes de começar  
 Antes de começar, terá de obter um token VPP da Apple e carregá-lo para o Configuration Manager.  

-   Se tiver utilizado anteriormente um token VPP com outro produto MDM na sua conta VPP da Apple, tem de gerar um novo para utilizar com o Configuration Manager.  
-   Cada token é válido durante um ano.  
-   Por predefinição, o Configuration Manager sincroniza com o serviço Apple VPP duas vezes por dia para garantir que as licenças são sincronizadas com o Configuration Manager. Apenas as alterações para as suas licenças são sincronizadas. Uma sincronização completa é realizada uma vez a cada sete dias. Quando escolhe **sincronização** para fazer uma sincronização manual, sempre esta ação faz uma sincronização completa.  
-   Se precisar de recuperar ou restaurar a base de dados do Configuration Manager, recomendamos que efetue uma sincronização manual, posteriormente. Este processo garante que os dados de licença sincronizadas estão atualizados.  
-   Além disso, terá de ter importado um certificado de serviço (APNs) válido do Apple Push Notification da Apple. Este certificado permite-lhe gerir dispositivos iOS, incluindo a implementação de aplicação. Para obter mais informações, consulte [configurar a gestão de dispositivos iOS híbrida](enroll-hybrid-ios-mac.md).  
-   O Configuration Manager suporta a adição de até 3 000 tokens VPP.

Pode implementar aplicações licenciadas para dispositivos e utilizadores. Consoante a capacidade de aplicações para suportar de licenciamento de dispositivos, uma licença adequada seja solicitada quando implantá-lo, da seguinte forma:

|Aplicação suporta o licenciamento de dispositivos?|Tipo de coleção de implementação|Licença solicitada|
|---|---|---|
|Sim|Utilizador|Licença de utilizador|
|Não|Utilizador|Licença de utilizador|
|Sim|Dispositivo|Licença de dispositivo|
|Não|Dispositivo|Licença de utilizador|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Passo 1 - obter e carregar um token VPP da Apple  

1.  Na consola do Configuration Manager, escolha **Administration** > **serviços Cloud** > **Tokens do programa Apple Volume Purchase**.   

3.  Sobre o **home page** separador a **Tokens do programa Apple Volume Purchase** de grupo, escolha **adicionar Token da Apple Volume Purchase Program**.  

4.  Na **gerais** página do **adicionar Token da Apple Volume Purchase Program** assistente, configure as seguintes definições:   

    -   **Nome** -introduza um nome para este token apresentar na consola do Configuration Manager.  

    -   **Token** -escolha **procurar**e, em seguida, selecione o token VPP que transferiu do site da Apple.  

         Clique nas **conta Apple VPP consulte** ligação. Se ainda não o fez, inscreva-se para o programa de compra de volume de empresas ou estabelecimentos de ensino. Depois de se estiver inscrito, transfira o token de VPP da Apple para a sua conta.  

    -   **Descrição** - como opção, introduza uma descrição para ajudar a identificar este token na consola do Configuration Manager.  

    -   **Atribuir categorias para melhorar a procura e na filtragem** - como opção, pode atribuir categorias para o token VPP para facilitar a procurar na consola do Configuration Manager.  
    -   **Apple ID** -introduza o ID de e-mail de apple associado com o Token de VPP.
    -   **Tipo de token** -selecione o tipo de token VPP que pretende utilizar. Pode escolher **Business** e **EDU** tipos de token.

5.  Escolher **seguinte**e, em seguida, conclua o assistente.  

Partir do **Tokens do programa Apple Volume Purchase** nó, pode agora ver informações sobre o token de Apple VPP. Esta vista inclui a última atualização, quando este expirar e quando ele foi a última sincronização.

Pode sincronizar completamente os dados retidos pela Apple com o Configuration Manager em qualquer altura, ao escolher **sincronização** na faixa de opções.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Passo 2 - implementar uma aplicação adquirida em grandes volumes  

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **informações de licença para aplicações de Store**.  

2. Escolha a aplicação que pretende implementar, e, em seguida, no **home page** separador a **Create** de grupo, escolha **Criar aplicação**.
   A aplicação do Configuration Manager que é criada tem o Microsoft Store para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

   > [!IMPORTANT]  
   > Tem de escolher um objetivo de implementação **necessário**. As instalações disponíveis não são atualmente suportadas.

   Ao implementar a aplicação, é utilizada uma licença por cada utilizador, ou para instalações de dispositivo, cada dispositivo que instala a aplicação. Se destinar uma coleção de dispositivos com uma aplicação que suporta o licenciamento do dispositivo, seja solicitada uma licença de dispositivo. Se destinar uma coleção de dispositivos com uma aplicação que não suporta o licenciamento de dispositivos, uma licença de usuário é solicitada. 

   Quando cria uma aplicação a partir da **informações de licença para aplicações de Store** nó, a aplicação está associada com licenças do token da aplicação que selecionou. Por exemplo, poderá ver duas versões da mesma aplicação no nó. Este comportamento acontece porque cada versão da aplicação está associada um token de Apple VPP diferente. Em seguida, pode criar aplicações a partir de cada token e implementá-las separadamente.

   Para recuperar uma licença, tem de criar uma nova implementação da aplicação com uma ação de implementação **desinstalação**. Não é possível alterar a ação de implementação no âmbito da implementação original. A licença é recuperada quando desinstalar a aplicação.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Passo 3 - monitorizar aplicações VPP do iOS  
 O **informações de licença para aplicações de Store** nó da **biblioteca de Software** área de trabalho apresenta informações sobre as suas aplicações iOS compradas em volume. As informações incluem o número total de licenças que é proprietário para cada aplicação e o número que foram implementadas. Além disso, a exibição mostra qual token VPP a aplicação está associada e o tipo de token

 Também pode monitorizar a utilização de licenças de todas as aplicações VPP que comprou utilizando o **aplicações do Apple Volume Purchase Program para iOS com contagens de licença** relatório.  

 Este relatório mostra o nome de cada aplicação juntamente com o número total de licenças que comprou, o número de licenças disponíveis e muito mais.  

 Para obter ajuda com a execução de relatórios do Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



## <a name="delete-an-apple-vpp-token"></a>Eliminar um token de Apple VPP  
<!--505268-->

Utilize o seguinte processo para eliminar um token do Configuration Manager:  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud** e selecione **Tokens do programa Apple Volume Purchase**.  

2. Selecione o token que pretende eliminar.  

3. Clique nas **eliminar** opção na faixa de opções.  

