---
title: Microsoft Store para empresas
titleSuffix: Configuration Manager
description: Gerir e implementar aplicações a partir da Microsoft Store para empresas com o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae137cae29d49413ca11668ff0cc744168e91e21
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383682"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-configuration-manager"></a>Gerir aplicações a partir da Microsoft Store para empresas com o Configuration Manager

O [Microsoft Store para empresas](https://www.microsoft.com/business-store) é onde encontrar e adquirir aplicações do Windows para a sua organização. Quando se liga a loja para o Configuration Manager, em seguida, sincronizar a lista de aplicações que comprou. Veja estas aplicações na consola do Configuration Manager e implementá-las como implementa qualquer outra aplicação.


## <a name="bkmk_apps"></a> Aplicações online e offline

A Microsoft Store para empresas suportam dois tipos de aplicação:

- **Online**: Este tipo de licença requer utilizadores e dispositivos para ligar à loja para obter uma aplicação e a sua licença. Dispositivos Windows 10 tem de ser do Azure Active Directory (Azure AD) associados a um domínio.  

- **Offline**: Este tipo permite-lhe aplicações de cache e licenças para implementar diretamente dentro da sua rede no local. Dispositivos não precisam de ligar para o arquivo ou ter uma ligação à internet.

[Leia mais](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre o Microsoft Store para empresas.

O Configuration Manager suporta a gestão Microsoft Store para as aplicações de negócio em dispositivos Windows 10 com o cliente do Configuration Manager tanto também dispositivos Windows 10 inscritos com o Microsoft Intune. O Configuration Manager oferece as seguintes funcionalidades para aplicações online e offline:


|Funcionalidade|Aplicações offline|Aplicações online|
|------------|------------|------------|
|Sincronizar dados de aplicação para o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicações do Configuration Manager a partir de aplicações da loja|Sim|Sim|
|Suportar gratuitamente as aplicações da loja|Sim|Sim|
|Suporte para aplicações pagas na loja|Não|Sim<sup>1</sup>|
|Suportar as implementações necessárias para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suportar as implementações disponíveis para coleções de utilizadores ou dispositivos|Sim|Sim|
|Suportar aplicações de linha de negócio da loja|Sim|Sim|
|Aprovisionar uma aplicação da loja para todos os utilizadores num dispositivo<sup>2</sup><!--1358310-->|Sim|Sim|

- <sup>1</sup> para implementar aplicações licenciadas online em dispositivos Windows 10 com o cliente do Configuration Manager, devem executar o Windows 10, versão 1703 ou posterior.  

- <sup>2</sup> a partir da versão 1806. Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  


### <a name="deploying-online-apps-using-the-microsoft-store-for-business-to-devices-that-run-the-configuration-manager-client"></a>Implementação de aplicações online usando o Microsoft Store para empresas para dispositivos que executam o cliente do Configuration Manager

Antes de implantar o Microsoft Store para aplicações de negócio em dispositivos que executam o cliente do Configuration Manager completo, considere os seguintes pontos:

- Para todas as funcionalidades, dispositivos têm de ser o Windows 10, versão 1703 ou posterior.  

- Dispositivos tem de estar associados ao Azure AD no mesmo inquilino em que registrou a Microsoft Store para empresas como uma ferramenta de gerenciamento.  

- Quando a conta de administrador local inicia sessão no dispositivo, não pode aceder a Microsoft Store para aplicações de negócio.  

- Dispositivos têm de ter uma ligação em direto da internet para a Microsoft Store para empresas. Para obter mais informações, incluindo a configuração de proxy, consulte [pré-requisitos](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  


### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Notas para os dispositivos com versões anteriores do Windows 10

Em dispositivos com o cliente do Configuration Manager e em execução com o Windows 10 versão 1607 ou anterior, aplica-se a seguinte funcionalidade:  

Quando impõe a instalação da aplicação no dispositivo por um dos seguintes métodos:  

- O utilizador instala a aplicação  

- A implementação de atinge o prazo de instalação   

- Após a instalação reavaliação para implementações necessárias  

Em seguida, os comportamentos seguintes ocorrem:  

- O cliente do Configuration Manager "impõe" a aplicação ao iniciar o Microsoft Store para a aplicação de negócio  

- O utilizador tem de concluir a instalação a partir da loja  

- Na consola do Configuration Manager, o estado de implementação de aplicação reportará falha com o seguinte erro: "A aplicação da Microsoft Store foi aberta no PC cliente e está à espera que o utilizador concluir a instalação."  

No próximo ciclo de avaliação do aplicativo:  

- Se o utilizador instalou a aplicação da loja, a aplicação comunica o estado **sucesso**  

- Se o utilizador não tente instalar a aplicação da loja:  

    - Para as implementações necessárias, o cliente do Configuration Manager tenta volte a iniciar a aplicação da loja  

    - As implementações disponíveis não são impostas novamente


#### <a name="further-notes-for-devices-running-earlier-versions-of-windows-10"></a>Notas adicionais para dispositivos com versões anteriores do Windows 10:

- Não é possível implementar aplicações de linha de negócio a partir da Microsoft Store para empresas  

- Quando implementa aplicações pagas na loja, os utilizadores tem de iniciar sessão na loja e adquirir a aplicação próprios  

- Se implementar uma política de grupo para desativar o acesso para a versão de consumidor da Microsoft Store, implementações a partir da Microsoft Store para empresas não funcionam. Este comportamento ocorre mesmo que a Microsoft Store para empresas está ativada.  



## <a name="bkmk_setup"></a> Configurar o Microsoft Store para a sincronização de negócios

Sincronizar a lista de aplicações adquirido pela sua organização permite-lhe ver estas aplicações na consola do Configuration Manager.

Ligar o seu site do Configuration Manager para o Azure AD e a Microsoft Store para empresas. Para obter mais informações e detalhes desse processo, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard). Criar uma ligação para o **Microsoft Store para empresas** serviço.


### <a name="bkmk_config"></a> Informações complementares e configuração 

Sobre o **aplicação** página do Assistente de serviços do Azure, primeiro configure a **ambiente do Azure** e **aplicação Web**. Em seguida, leia os **mais informações** seção na parte inferior da página. Estas informações incluem as seguintes ações adicionais em que a Microsoft Store para o portal da empresa:  

- Configure o Configuration Manager como a ferramenta de gestão de armazenamento. Para obter mais informações, consulte [fornecedor de gestão de configurar](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Ative o suporte para aplicações licenciadas offline. Para obter mais informações, consulte [distribuir as aplicações offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Adquira pelo menos uma aplicação. Para obter mais informações, consulte [encontrar e adquirir aplicações](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Sobre o **configurações** página do Assistente de serviços do Azure, especifique as seguintes informações:  

- **Caminho para a Microsoft Store para armazenamento de conteúdos de aplicações de negócio**: Especifique um caminho de rede partilhada, incluindo uma pasta. Por exemplo, `\\server\share\folder`. Quando o servidor do site sincroniza com o arquivo, ele coloca em cache o conteúdo nesta localização. Quando cria uma aplicação no Configuration Manager, o servidor de site copia o conteúdo da aplicação desse cache local para a biblioteca de conteúdos do site.  

- **Selecionar idiomas**: Selecione os idiomas para sincronizar a partir da loja e apresentar aos utilizadores no Centro de Software. Por exemplo, se o usuário configura o Windows para o alemão, em seguida, o Centro de Software mostra alemães cadeias de caracteres para a aplicação da loja. Esse comportamento requer esse idioma a ser sincronizados e existir para o aplicativo específico.    

- **Idioma predefinido**: Se o idioma do utilizador não estiver disponível, selecione um idioma predefinido a utilizar.  



## <a name="bkmk_deploy"></a> Criar e implementar uma aplicação do Configuration Manager a partir de um Microsoft Store para a aplicação de negócio

Após a sincronização, criar e implementar as aplicações de loja semelhantes a qualquer outra aplicação.

1.  Na **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações de Store**.  

2.  Escolha a aplicação que pretende implementar, em seguida, clique em **Criar aplicação** na faixa de opções.  

O site cria uma aplicação do Configuration Manager que contém o Microsoft Store para a aplicação de negócio. 

Em seguida, implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager. Para obter mais informações, consulte os artigos seguintes:  
- [Implementar aplicações](/sccm/apps/deploy-use/deploy-applications)
- [Monitorizar aplicações a partir da consola](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> Para dispositivos inscritos com o Microsoft Intune, as aplicações implementadas só estão disponíveis para o utilizador que inscreveu originalmente o dispositivo. Não existem outros utilizadores podem aceder à aplicação.



## <a name="next-steps"></a>Passos seguintes

Na **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações de Store**.

Para cada aplicação de loja que gere, ver as seguintes informações sobre a aplicação:
- Nome da aplicação
- Plataforma de aplicações
- O número de licenças para a aplicação que é proprietário
- O número de licenças disponíveis

Depois de implementar aplicações online, todas as atualizações para essa aplicação vêm diretamente a partir da Microsoft Store. Além disso, o Configuration Manager não verificar conformidade de versão de aplicações online, apenas que o Windows reporta a aplicação como instalado.  

Ao implementar as aplicações offline para dispositivos Windows 10 com o cliente do Configuration Manager, não permitem aos utilizadores Atualizar aplicativos externos para implementações do Configuration Manager. Controle de atualizações para as aplicações offline é especialmente importante em ambientes de vários utilizadores como salas de aulas. Uma opção para desativar o Microsoft Store é através de [política de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Depois da Microsoft Store para empresas administrador adquire uma aplicação offline, não o publicar a aplicação aos utilizadores através da loja. Esta configuração garante que os utilizadores não conseguem instalar nem atualizar online. Os utilizadores só recebem atualizações de aplicações offline através do Gestor de configuração. 
