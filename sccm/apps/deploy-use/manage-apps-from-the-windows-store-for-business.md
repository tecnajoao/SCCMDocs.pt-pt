---
title: "Gerir aplicações da loja Windows para empresas | Microsoft Docs"
description: "Gerir e implementar aplicações da loja Windows para empresas com o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 369b6a82a20a90ca534f9484c0be71096dd35a30
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gerir aplicações da Loja Windows para Empresas com o System Center Configuration Manager
O [loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações do Windows para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode sincronizar a lista de aplicações que comprou com o Configuration Manager. Em seguida, pode ver estas aplicações na consola do Configuration Manager e implementá-las como poderia implementar qualquer outra aplicação.


## <a name="online-and-offline-apps"></a>Aplicações online e offline

Na loja Windows para empresas suportam dois tipos de aplicação:

- **Online** -requer que este tipo de licença aos utilizadores e dispositivos para ligar ao arquivo de obter uma aplicação e a sua licença. Dispositivos Windows 10 tem de ser do Azure Active Directory associados a um domínio.
- **Offline** -permite-lhe cache aplicações e de licenças para implementar diretamente na sua rede no local, sem ligar ao arquivo de ou ter uma ligação à Internet.

[Leia mais](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) sobre a loja Windows para empresas.

O Configuration Manager suporta a gerir a loja Windows para aplicações empresariais em dispositivos Windows 10 com o cliente do Configuration Manager tanto também os dispositivos Windows 10 inscritos com o Microsoft Intune (conhecido como configuração híbrida). O Configuration Manager oferece as seguintes capacidades para aplicações online e offline.

> [!IMPORTANT]
> Para utilizar esta capacidade, dispositivos Windows 10 tem de executar a versão de Novembro de 2015 (versão 1511) ou posterior.


|Funcionalidade|Aplicações offline|Aplicações online|
|------------|------------|------------|
|Sincronizar os dados da aplicação para o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicações do Configuration Manager a partir de aplicações da loja|Sim|Sim|
|Suporta gratuitamente aplicações da loja|Sim|Sim|
|Suporte para pagas aplicações da loja|Não|Sim|
|Suporta as implementações necessárias para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suporta as implementações disponíveis para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suportar aplicações de linha de negócio da loja|Sim|Sim|

Para implementar as aplicações licenciadas online para Windows 10 PCs com o cliente do Configuration Manager, tem de executar o Windows 10 criadores Update, ou posterior.

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implementação de aplicações online utilizando a loja Windows para empresas com computadores que executem o cliente do Configuration Manager
Antes de implementar a loja Windows para empresas aplicações para computadores que executem o cliente do Configuration Manager completa, considere os seguintes pontos:

- Para uma funcionalidade completa, PCs tem de executar o Windows 10 criadores Update, ou posterior.
- PCs têm de estar associados a um Azure Active Directory à área de trabalho e de estar no mesmo inquilino do AAD onde registada na loja Windows para empresas como uma ferramenta de gestão.
- Quando PCs tem sessão iniciados com a conta de administrador incorporada, não vão conseguir aceder loja Windows para as aplicações da empresa.
- PCs tem de ter uma ligação de internet em direto para a loja Windows para empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas para os computadores com versões anteriores do Windows 10
Em computadores que executam uma versão anterior do que a atualização criadores (com o cliente do Configuration Manager) do Windows 10, aplica-se a seguinte funcionalidade:


- Quando instalação é imposta ao utilizador instalar a aplicação, seja pela aplicação atingir o prazo de instalação ou por post instalação reavaliação para implementações necessárias:
    - A aplicação é "imposta", iniciando a loja Windows para a aplicação de negócio. 
    - O utilizador final tem de concluir, em seguida, a instalação a partir da loja, antes da aplicação está instalada
    - O estado da aplicação nos relatórios de consola do Configuration Manager falhou com o erro "aplicação loja Windows foi aberta no cliente do PC e está à espera que o utilizador concluir a instalação."
- No próximo ciclo de avaliação do aplicação:
    - Se a aplicação foi instalada pelo utilizador final da loja, a aplicação comunica o estado **êxito**. 
    - Se o utilizador final não tentou instalar a aplicação da loja:
        - Necessário implementações tentar iniciar o arquivo e impor novamente a instalação da aplicação.
        - As implementações disponíveis não são impostas novamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas adicionais para computadores com versões anteriores do Windows 10:

- Não é possível implementar aplicações de linha de negócio da loja Windows para empresas
- Quando implementa pagas aplicações da loja, os utilizadores finais tem início de sessão para o arquivo de compra e a aplicação próprios.
- Se tiver implementado um acesso de desativação de política de grupo para a versão de consumidor da loja Windows, as implementações da loja Windows para empresas não funcionam, mesmo que a loja Windows para empresas está ativada.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a loja Windows para a sincronização de negócio

### <a name="for-configuration-manager-versions-prior-to-1706"></a>Para versões do Configuration Manager antes de 1706

**No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web". Esta ação dá-lhe um ID de cliente que precisar mais tarde.**
1. No nó do Active Directory da [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.
2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.
3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique o **seguinte** seta.
4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir *https://yourdomain/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registado**
1.  Realce a aplicação que criou e clique em **configurar**.
2.  Em **chaves**, selecione uma duração da lista e, em seguida, clique em **guardar**. Esta ação cria uma nova chave de cliente. Não saia desta página até ter com êxito integrado na loja do Windows para empresas para o Configuration Manager.

**Na loja Windows para empresas, configurar o Configuration Manager como a ferramenta de gestão de arquivo**
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e início de sessão se lhe for pedido.
2.  Se o pedido de aceitar os termos de utilização.
3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.
4.  No **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.
5.  Clique em **ativar** junto da aplicação que importou.
6.  No **gerir > informações de conta** página, selecione **aplicações licenciadas offline** se pretender permitir que as aplicações licenciadas offline sejam compradas.

**Adicione a conta de arquivo para o Configuration Manager**

1. Certifique-se de que adquiriu, pelo menos, uma aplicação da loja Windows para empresas. No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **loja Windows para empresas**.
2.  No **home page** separador o **loja Windows para empresas** , clique em **adicionar da loja Windows para empresas conta**. 
3.  Adicione o ID do inquilino, o id de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.
4. Quando tiver terminado, pode ver a conta configurada no **loja Windows para empresas** lista na consola do Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Para o Configuration Manager versão 1706 e posterior

1. Na consola, aceda a **administração** > **descrição geral** > **gestão de serviços em nuvem** > **Azure** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** para iniciar o **Assistente de serviços do Azure**.
2. No **serviços do Azure** página, selecione o serviço que pretende configurar e, em seguida, clique em **seguinte**.
3. No **geral** página, forneça um nome amigável para o nome do serviço do Azure e uma descrição opcional e, em seguida, clique em **seguinte**.
4. No **aplicação** página, especifique o seu ambiente do Azure e, em seguida, clique em **procurar** para abrir o **aplicação Server** janela.
5. No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**. Aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponível, utilize um dos seguintes:
    - **Crie:** Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e de inquilino. Em seguida, depois, inicie sessão no Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.
    - **Importar:** Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de **verifique** informações, clique em **OK** para continuar. 
6. Reveja o **informações** página e conclua quaisquer passos adicionais e configurações, conforme indicado. Estas configurações são necessárias para utilizar o serviço com o Configuration Manager. Por exemplo, para configurar a loja Windows para empresas:
    - No Azure tem de registar o Configuration Manager como uma aplicação web ou a Web API e registar o ID de cliente. Também especificar uma chave de cliente para utilização pela ferramenta de gestão (que é o Configuration Manager).
    - Na loja Windows para a consola de negócio tem de configurar o Configuration Manager como a ferramenta de gestão de armazenamento, ativar o suporte para aplicações licenciadas offline e, em seguida, comprar, pelo menos, uma aplicação. 
7. Clique em **seguinte** quando estiver pronto para continuar.
8. No **configurações aplicação** página, conclua as configurações de idioma e o catálogo de aplicações para este serviço e, em seguida, clique em **seguinte**.
9. Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **loja Windows para empresas** como um **o tipo de serviço de nuvem**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação de negócio.
1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.
2.  Escolha a aplicação que pretende implementar, em seguida, no **home page** separador o **criar** , clique em **Criar aplicação**.
Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.

> [!IMPORTANT]
> Para dispositivos inscritos no Intune, as aplicações implementadas só estão disponíveis ao utilizador que inscreveu originalmente o dispositivo. Não existem outros utilizadores podem aceder à aplicação.

## <a name="next-steps"></a>Passos seguintes

No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.

Para cada aplicação da loja que gere, pode ver informações sobre a aplicação, incluindo o respetivo nome, plataforma e número de licenças para a aplicação que lhe pertence e o número de licenças que tem disponíveis.
