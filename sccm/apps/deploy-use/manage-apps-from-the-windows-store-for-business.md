---
title: Gerir aplicações da loja Microsoft para empresas
titleSuffix: Configuration Manager
description: Gerir e implementar aplicações da Microsoft Store para empresas com o System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336124"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Gerir aplicações da loja Microsoft para empresas com o System Center Configuration Manager
O [Microsoft Store para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações do Windows para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode sincronizar a lista de aplicações que comprou com o Configuration Manager. Em seguida, pode ver estas aplicações na consola do Configuration Manager e implementá-las como poderia implementar qualquer outra aplicação.


## <a name="online-and-offline-apps"></a>Aplicações online e offline

A Microsoft Store para empresas suportam dois tipos de aplicação:

- **Online** -requer que este tipo de licença aos utilizadores e dispositivos para ligar ao arquivo de obter uma aplicação e a sua licença. Dispositivos Windows 10 tem de ser do Azure Active Directory associados a um domínio.
- **Offline** -permite-lhe cache aplicações e de licenças para implementar diretamente dentro da sua rede no local. Dispositivos não precisa de ligar à loja ou tenham uma ligação à Internet.

[Leia mais](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre o Microsoft Store para empresas.

O Configuration Manager suporta a gestão Microsoft Store para aplicações empresariais em dispositivos Windows 10 com o cliente do Configuration Manager tanto também dispositivos Windows 10 inscritos com o Microsoft Intune. O Configuration Manager oferece as seguintes capacidades para aplicações online e offline.

> [!IMPORTANT]
> Para utilizar o Microsoft Store para empresas, dispositivos Windows 10 tem de executar a versão de Novembro de 2015 (versão 1511) ou posterior.


|Funcionalidade|Aplicações offline|Aplicações online|
|------------|------------|------------|
|Sincronizar os dados da aplicação para o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicações do Configuration Manager a partir de aplicações da loja|Sim|Sim|
|Suporta gratuitamente aplicações da loja|Sim|Sim|
|Suporte para pagas aplicações da loja|Não|Sim<sup>1</sup>|
|Suporta as implementações necessárias para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suporta as implementações disponíveis para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suportar aplicações de linha de negócio da loja|Sim|Sim|

<sup>1</sup>para implementar as aplicações licenciadas online para Windows 10 PCs com o cliente do Configuration Manager, tem de executar o Windows 10 criadores Update, ou posterior.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implementação de aplicações online utilizando o Microsoft Store para empresas com computadores que executem o cliente do Configuration Manager
Antes de implementar o Microsoft Store para aplicações empresariais para os computadores que executam o cliente do Configuration Manager completa, considere os seguintes pontos:

- Para uma funcionalidade completa, PCs tem de executar o Windows 10 criadores Update, ou posterior.
- Os PCs têm de ser associados ao Azure Active Directory no mesmo inquilino onde registada da Microsoft Store para empresas como uma ferramenta de gestão.
- Quando PCs tem sessão iniciados com a conta de administrador incorporada, não vão conseguir aceder Microsoft Store para aplicações empresariais.
- PCs tem de ter uma ligação de internet em direto para o Microsoft Store para empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas para os computadores com versões anteriores do Windows 10
Em computadores que executam uma versão anterior do que a atualização criadores (com o cliente do Configuration Manager) do Windows 10, aplica-se a seguinte funcionalidade:


- Quando a imposição de instalação pelo utilizador que instalar a aplicação, a aplicação atingir o prazo de instalação, ou por pós-instalação a reavaliação das implementações necessárias:
    - A aplicação é "imposta", iniciando a Store Microsoft para a aplicação de negócio. 
    - O utilizador final tem de concluir, em seguida, a instalação a partir da loja, antes da aplicação está instalada
    - No Gestor de configuração da consola falha de relatórios de estado da aplicação com o seguinte erro: "A aplicação Microsoft Store foi aberta no cliente do PC e está à espera que o utilizador concluir a instalação."
- No próximo ciclo de avaliação do aplicação:
    - Se a aplicação foi instalada pelo utilizador final da loja, a aplicação comunica o estado **êxito**. 
    - Se o utilizador final não tentou instalar a aplicação da loja:
        - Necessário implementações tentar iniciar o arquivo e impor novamente a instalação da aplicação.
        - As implementações disponíveis não são impostas novamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas adicionais para computadores com versões anteriores do Windows 10:

- Não é possível implementar aplicações de linha de negócio da Microsoft Store para empresas
- Quando implementa pagas aplicações da loja, os utilizadores finais tem início de sessão para o arquivo de compra e a aplicação próprios.
- Se implementar uma política de grupo para desativar o acesso para a versão de consumidor do Microsoft Store, implementações da Microsoft Store para empresas não funcionam, mesmo que a Microsoft Store para empresas está ativada.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurar o Microsoft Store para a sincronização de negócio
Sincronizar a lista de aplicações adquirido pela sua organização permite-lhe ver estas aplicações na consola do Configuration Manager.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Para versões do Configuration Manager antes de 1706

**No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web". Esta ação dá-lhe um ID de cliente que precisar mais tarde.**
1. No nó do Active Directory da [ https://manage.windowsazure.com ](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.
2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.
3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique o **seguinte** seta.
4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir *https://yourdomain/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registado**
1.  Realce a aplicação que criou e clique em **configurar**.
2.  Em **chaves**, selecione uma duração da lista e, em seguida, clique em **guardar**. Esta ação cria uma nova chave de cliente. Não saia desta página até ter com êxito integrado Store da Microsoft para empresas para o Configuration Manager.

**Na Microsoft Store para empresas, configurar o Configuration Manager como a ferramenta de gestão de arquivo**
1.  Abra [ https://businessstore.microsoft.com/managementtools ](https://businessstore.microsoft.com/managementtools) e início de sessão se lhe for pedido.
2.  Se o pedido de aceitar os termos de utilização.
3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.
4.  No **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.
5.  Clique em **ativar** junto da aplicação que importou.
6.  No **gerir > informações de conta** página, selecione **aplicações licenciadas offline** se pretender permitir que as aplicações licenciadas offline sejam compradas.

**Adicione a conta de arquivo para o Configuration Manager**

1. Certifique-se de que adquiriu, pelo menos, uma aplicação do Microsoft Store para empresas. No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **Microsoft Store para empresas**.
2.  No **home page** separador o **Microsoft Store para empresas** , clique em **adicionar Microsoft conta da loja para empresas**. 
3.  Adicione o ID do inquilino, o ID de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.
4. Quando tiver terminado, pode ver a conta sob **Microsoft Store para empresas** na consola do Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Para o Configuration Manager versão 1706 e posterior
<!-- ...remove above after 1802 -->

1. Na consola, aceda a **administração** > **serviços em nuvem** > **serviços do Azure**e, em seguida, escolha **configurar o Azure Serviços** para iniciar o **Assistente de serviços do Azure**.
2. No **serviços do Azure** página, selecione o serviço que pretende configurar e, em seguida, clique em **seguinte**.
3. No **geral** página, forneça um nome amigável para o nome do serviço do Azure e uma descrição opcional e, em seguida, clique em **seguinte**.
4. No **aplicação** página, especifique o seu ambiente do Azure e, em seguida, clique em **procurar** para abrir o **aplicação Server** janela.
5. No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**. Aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponível, utilize uma das seguintes ações:
    - **Crie:** Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e de inquilino. Em seguida, depois de iniciar sessão no Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes valores do portal do Azure.
    - **Importar:** Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino. Em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de **verifique** informações, clique em **OK** para continuar. 
6. Reveja o **informações** página e conclua quaisquer passos adicionais e configurações, conforme indicado. Estas configurações são necessárias para utilizar o serviço com o Configuration Manager. Por exemplo, para configurar o Microsoft Store para empresas:
    - No Azure, tem de registar o Configuration Manager como uma aplicação web ou a Web API e registar o ID de cliente. Também especificar uma chave de cliente para utilização pela ferramenta de gestão (que é o Configuration Manager).
    - Na Microsoft Store para o portal da empresa tem de configurar o Configuration Manager como a ferramenta de gestão de arquivo, ativar o suporte para aplicações licenciadas offline e, em seguida, comprar, pelo menos, uma aplicação. 
7. Clique em **seguinte** quando estiver pronto para continuar.
8. No **configurações aplicação** página, conclua as configurações de idioma e o catálogo de aplicações para este serviço e, em seguida, clique em **seguinte**.
9. Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **Microsoft Store para empresas** como um **o tipo de serviço de nuvem**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Criar e implementar uma aplicação do Configuration Manager a partir de um Store Microsoft para a aplicação de negócio
Após a sincronização, criar e implementar as aplicações da loja, tal como faria com qualquer outra aplicação.

1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.
2.  Escolha a aplicação que pretende implementar, em seguida, no **home page** separador o **criar** , clique em **Criar aplicação**.
Uma aplicação do Configuration Manager é criada que contém o Store Microsoft para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.

> [!IMPORTANT]
> Para dispositivos inscritos com o Microsoft Intune, as aplicações implementadas só estão disponíveis ao utilizador que inscreveu originalmente o dispositivo. Não existem outros utilizadores podem aceder à aplicação.

## <a name="next-steps"></a>Passos seguintes

No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.

Para cada aplicação da loja que gere, pode ver informações sobre a aplicação. Estas informações incluem o nome da aplicação, plataforma, o número de licenças para a aplicação que é proprietário e o número de licenças que tem disponíveis.

Depois de implementar as aplicações online, as atualizações para essa aplicação ficará diretamente a partir da Microsoft Store. Além disso, Configuration Manager não verifica a compatibilidade da versão de aplicações online, apenas que o Windows apresenta a aplicação como instalado.  

Ao implementar aplicações offline para dispositivos Windows 10 com o cliente do Configuration Manager, não permitir que os utilizadores atualizar aplicações externas para implementações do Configuration Manager. É especialmente importante em ambientes de vários utilizadores como classrooms controlo das atualizações às aplicações offline. É uma opção para desativar o Microsoft Store utilizando [política de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Depois da Microsoft Store para o administrador da empresa adquire uma aplicação offline, não publique a aplicação aos utilizadores através da loja. Esta configuração assegura que os utilizadores não conseguem instalar nem atualizar online. Os utilizadores só irão receber as atualizações de aplicações offline através do Gestor de configuração. 
