---
title: "Gerir aplicações na loja Windows para empresas | Documentos do Microsoft"
description: "Gerir e implementar aplicações da loja Windows para empresas utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 3/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: f2d9da1c584f78e27e84b7f55e7ffe4dd052a27c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gerir aplicações da Loja Windows para Empresas com o System Center Configuration Manager
O [da loja Windows para empresas](https://www.microsoft.com/business-store) é onde pode encontrar e adquirir aplicações do Windows para a sua organização, individualmente ou em volume. Ao ligar-se no arquivo do Configuration Manager, pode sincronizar a lista de aplicações que tenha comprado com o Configuration Manager, ver na consola do Configuration Manager e implementá-las como faria com qualquer outra aplicação.


## <a name="online-and-offline-apps"></a>Aplicações online e offline

A loja Windows para empresas suporta dois tipos de aplicação:

- **Online** -este tipo de licença requer que os utilizadores e dispositivos para ligar para a loja para obter uma aplicação e a sua licença. Dispositivos Windows 10 tem de ser do Azure Active Directory associados a um domínio.
- **Offline** - organizações podem colocar em cache as aplicações e licenças para implementar diretamente no local de rede, sem ligação para a loja ou está a ter uma ligação à Internet.

[Ler mais](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) sobre a loja Windows para empresas.

O Configuration Manager suporta a gestão da loja Windows para aplicações de negócio no Windows 10 dispositivos a executar o cliente do Configuration Manager e também dispositivos Windows 10 inscritos com o Microsoft Intune (conhecido como uma configuração híbrida). O Configuration Manager oferece as seguintes capacidades para aplicações online e offline.

> [!IMPORTANT]
> Para utilizar esta capacidade, dispositivos Windows 10 tem de executar a versão de Novembro de 2015 (1511) ou posterior.


|Funcionalidade|Aplicações offline|Aplicações online|
|------------|------------|------------|
|Sincronizar os dados da aplicação do Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicações do Configuration Manager a partir de aplicações da loja|Sim|Sim|
|Suporta gratuitamente aplicações da loja|Sim|Sim|
|Suporte para pagas aplicações da loja|Não|Sim|
|Suporta as implementações necessárias para coleções de utilizador ou dispositivo|Sim|Sim|
|Suporta as implementações disponíveis para coleções de utilizador ou dispositivo|Sim|Sim|
|Suporta aplicações de linha de negócio a partir da loja|Sim|Sim|

Para implementar aplicações licenciadas online para Windows 10 PCs com o cliente do Configuration Manager, tem de executar a atualização de criadores do Windows 10, ou posterior.

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>A implementação de aplicações online através da loja Windows para empresas com PCs que executam o cliente do Configuration Manager
Antes da implementação da loja Windows para aplicações de negócio em PCs que executam o cliente do Configuration Manager completa, considere o seguinte:

- Para a funcionalidade completa, PCs têm de executar a atualização de criadores do Windows 10, ou posterior.
- PCs tem de ser do Azure Active Directory à área de trabalho associados e estar no mesmo inquilino AAD onde registou a loja Windows para empresas como uma ferramenta de gestão.
- Quando PCs tem sessão iniciadas com a conta de administrador incorporada, que não é possível aceder à loja Windows para aplicações de negócio.
- PCs tem de ter uma ligação de internet em direto para a loja Windows para empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas para PCs a executar versões anteriores do Windows 10
Em PCs a executar uma versão do Windows 10 mais cedo do que a atualização criadores (com o cliente do Configuration Manager), aplica-se a seguinte funcionalidade:


- Quando a instalação é aplicada quer pelo utilizador a instalar a aplicação ou a aplicação atingir o prazo da instalação ou publique a reavaliação de instalação para as implementações necessárias:
    - A aplicação poderá ser "forçada", iniciando a aplicação de empresa na loja Windows. 
    - O utilizador final tem, em seguida, concluir a instalação da loja antes da instalação, na verdade
    - O estado da aplicação na consola do Configuration Manager irá reportar como falhou com o erro "a aplicação da loja Windows foi aberta no cliente PC e está à espera que o utilizador concluir a instalação."
- No próximo ciclo de avaliação do aplicação:
    - Se a aplicação foi instalada pelo utilizador final a partir da loja, a aplicação irá reportar o estado **êxito**. 
    - Se o utilizador final não a tentar instalar a aplicação da loja:
        - As implementações necessárias irão tentar iniciar o arquivo e impor novamente a instalação da aplicação.
        - As implementações disponíveis não será novamente impostas.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas adicionais para PCs a executar versões anteriores do Windows 10:

- É possível implementar a linha de negócio a partir da loja Windows para empresas
- Quando implementa aplicações pagas da loja, os utilizadores finais serão solicitados para iniciar sessão para o arquivo e compre a aplicação por si próprios.
- Se tiver implementado um acesso de desativação de política de grupo para a versão de consumidor da loja Windows, as implementações da loja Windows para empresas não funcionará, mesmo que a loja Windows para empresas está ativada.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configurar a loja Windows para a sincronização de negócio

**No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Web aplicação and/or Web API". Isto irá dar-lhe um ID de cliente que irá precisar mais tarde.**
1. No nó do Active Directory da [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.
2.  Clique em **adicionar uma aplicação a minha organização está a desenvolver**.
3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique a **seguinte** seta.
4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**. O URL pode ser nada e não precisa de resolver para um endereço real. Por exemplo, pode introduzir *https://yourdomain/sccm*.
5.  Conclua o assistente.

**No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registado**
1.  Realce a aplicação que acabou de criar e clique em **configurar**.
2.  Em **chaves**, selecione uma duração a partir da lista e, em seguida, clique em **guardar**. Esta ação cria uma nova chave de cliente. Não sai desta página até ter com êxito onboarded a loja Windows para empresas para o Configuration Manager.

**Na loja Windows para empresas, configurar o Configuration Manager como a ferramenta de gestão de arquivo**
1.  Abrir [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e início de sessão se lhe for solicitado.
2.  Se solicitado de aceitar os termos de utilização.
3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.
4.  No **pesquisa para a ferramenta de por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.
5.  Clique em **ativar** junto da aplicação que acabou de importar.
6.  No **gerir > informações de conta** página, selecione **Show Offline-Licensed aplicações** se pretender permitir que as aplicações offline licenciado ser comprado.

**Adicione a conta de arquivo para o Configuration Manager**

1. Certifique-se de que adquiriu, pelo menos, uma aplicação da loja Windows para empresas. No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **da loja Windows para empresas**.
2.  No **base** separador o **da loja Windows para empresas** grupo, clique em **para conta de empresas da loja Windows adicionar**. 
3.  Adicionar o ID do inquilino, o id de cliente e a chave de cliente a partir do Azure Active Directory, em seguida, conclua o assistente.
4. Quando tiver terminado, verá a conta configurada no **da loja Windows para empresas** lista na consola do Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação de negócio.
1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença de aplicações da loja**.
2.  Escolha a aplicação que pretende implementar, em seguida, no **base** separador o **criar** grupo, clique em **Criar aplicação**.
Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Pode, em seguida, implementar e monitorizar esta aplicação, tal como faria com qualquer outra aplicação do Configuration Manager.
> [!IMPORTANT]
> Para dispositivos inscritos com o Intune, as aplicações implementadas só estão disponíveis para o utilizador que originalmente inscreveu o dispositivo. Não existem outros utilizadores podem aceder à aplicação.

## <a name="monitor-windows-store-for-business-apps"></a>Monitor da loja Windows para aplicações de negócio

No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, em seguida, clique em **informações de licença de aplicações da loja**.

Para cada aplicação de arquivo de gerir, pode ver informações sobre a aplicação, incluindo o respetivo nome, plataforma, em seguida, número de licenças para a aplicação que é o proprietário e o número de licenças que tem disponível.

