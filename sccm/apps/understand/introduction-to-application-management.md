---
title: Introdução à gestão de aplicações
titleSuffix: Configuration Manager
description: Descubra as informações básicas, que terá de gerir e implementar aplicações do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70ab4136f39b4bf559c3d460ca1528bb4de0f6e1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384295"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introdução à gestão de aplicações no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Neste artigo, irá aprender as noções básicas antes de começar a trabalhar com aplicações do Configuration Manager.  

> [!TIP]  
>  Se já estiver familiarizado com a gestão de aplicações no Configuration Manager, ignore este artigo. Avançar para a criação de um aplicativo de exemplo: [Criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).  



## <a name="what-is-an-application"></a>O que é uma aplicação?  

Embora *aplicativo* é um termo utilizado em informática, no Gestor de configuração, significa algo específico. Pense numa aplicação como uma caixa. Esta caixa contém um ou mais conjuntos de ficheiros de instalação de um pacote de software (conhecido como um *tipo de implementação*), juntamente com instruções sobre como implementar o software.  

Ao implementar a aplicação em dispositivos, **requisitos** decidir que tipo de implementação do Configuration Manager instala no dispositivo.  

Pode fazer muitas coisas mais com um aplicativo. Irá aprender sobre essas coisas enquanto lê este guia. As secções seguintes apresentam alguns conceitos que tem de saber antes de começar a se aprofundar mais:  

#### <a name="deployment-type"></a>Tipo de implementação
Se o *aplicativo* é a caixa, o *tipo de implementação* é o conjunto de conteúdo na caixa. Um aplicativo precisa, pelo menos, um tipo de implementação, como ele determina como instalar a aplicação. Utilize mais do que um tipo de implementação para configurar o conteúdo diferente e o programa de instalação para a mesma aplicação. 

Por exemplo, a sua empresa tem um aplicativo de linha de negócio chamado Astoria. Os desenvolvedores de aplicativos fornecem das seguintes formas de instalar a aplicação:
- Pacote de instalador do Windows para todas as funcionalidades em dispositivos Windows 10
- Um pacote de App-V para utilização no farm de servidores de terminal
- Um pacote de aplicações Android para usuários móveis  

Criar um único aplicativo para Astoria no Configuration Manager. O aplicativo define os metadados de alto nível sobre a aplicação que é comum em todos os métodos de instalação e plataformas. Em seguida, crie três tipos de implementação para os métodos de instalação disponíveis e implementar a aplicação em todos os utilizadores. Com base nos requisitos da e outras configurações nos tipos de implementação, o Configuration Manager determina o método correto em cada caso de utilização. 

Para obter mais informações, consulte [criar tipos de implementação para a aplicação](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).

#### <a name="requirements"></a>Requisitos
Nas versões anteriores do Configuration Manager, deverá criar uma coleção de dispositivos para implementar uma aplicação. Embora ainda seja possível criar uma coleção, utilize *requisitos* para especificar mais critérios para uma implementação de aplicações.

Por exemplo, especifica que uma aplicação só pode ser instalada nos dispositivos que executam o Windows 10. Ao implementar a aplicação para todos os seus dispositivos, ele instala apenas nos dispositivos que executam o Windows 10.

O Configuration Manager avalia os requisitos para determinar se instala uma aplicação e algum dos respetivos tipos de implementação. Em seguida, determina o tipo de implementação correto para a instalação da aplicação. A cada sete dias, por predefinição, o cliente do Configuration Manager revê as regras de requisitos para determinar a conformidade, de acordo com a definição de cliente **agendar reavaliação para implementações**.

Para obter mais informações, consulte [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application) e [tipo de implementação requisitos](/sccm/apps/deploy-use/create-applications#bkmk_dt-require).

#### <a name="global-conditions"></a>Condições globais
Apesar de utilizar requisitos com um tipo de implementação específico numa única aplicação, também pode criar *condições globais*. Estas condições são uma biblioteca de requisitos predefinidos que pode utilizar com qualquer aplicação e o tipo de implementação. O Configuration Manager inclui um conjunto de condições globais incorporadas ou, pode criar o seu próprio. 

Para obter mais informações, consulte [criar condições globais](/sccm/apps/deploy-use/create-global-conditions).

#### <a name="simulated-deployment"></a>Implementação simulada
R *simulated implementação* avalia os requisitos, o método de deteção e dependências para uma aplicação. Um cliente reporta os resultados sem realmente instalar a aplicação. 

Para obter mais informações, consulte [simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).  

#### <a name="deployment-action"></a>Ação de implementação
R *ação de implementação* Especifica se pretende instalar ou desinstalar a aplicação estiver a implementar. Nem todos os tipos de implementação suportam a ação de desinstalação. 

Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  

#### <a name="deployment-purpose"></a>Objetivo da implementação
O *objetivo da implementação* Especifica se a aplicação de implementação é **necessário** ou **disponível**:  

- O cliente instala automaticamente um *necessário* implementação de acordo com a agenda que definir. Se o aplicativo não estiver oculto, um utilizador pode controlar o respetivo estado de implementação. Eles também podem utilizar o Centro de Software para instalar a aplicação antes do prazo.  

- Se implementar a aplicação a um utilizador como *disponível*, vê-lo no Centro de Software e poderá solicitá-la a pedido.  

Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  

#### <a name="revisions"></a>Revisões
Quando são efetuadas *revisões* para uma aplicação ou um tipo de implementação, o Configuration Manager cria uma nova versão da aplicação. Efetue as seguintes ações na consola do Configuration Manager: 
- Visualizar o histórico de cada revisão da aplicação
- Ver as respetivas propriedades
- Restaurar uma versão anterior de uma aplicação
- Eliminar uma versão antiga

Para obter mais informações, consulte [atualizar e extinguir aplicações](/sccm/apps/deploy-use/update-and-retire-applications).  

#### <a name="detection-method"></a>Método de deteção
Uso *métodos de deteção* para detetar se um dispositivo já tiver instalado uma aplicação. Se o método de deteção indicar que a aplicação está instalada, o Configuration Manager não tenta instalá-la novamente.

Para obter mais informações, consulte [opções de método de deteção de tipo de implementação](/sccm/apps/deploy-use/create-applications##bkmk_dt-detect).

#### <a name="dependencies"></a>Dependências
*Dependências* definem um ou mais tipos de implementação de outra aplicação que o cliente tem de instalar antes que ele instala este tipo de implementação. 

Para obter mais informações, consulte [dependências de tipo de implementação](/sccm/apps/deploy-use/create-applications#bkmk_dt-depend).  

#### <a name="supersedence"></a>Substituição
O Configuration Manager permite atualizar ou substituir as aplicações existentes utilizando uma *substituição* relação. Ao substituir uma aplicação, especifique um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída. Também pode decidir se atualizar ou desinstalar a aplicação substituída antes do cliente instala a aplicação substituta.

Para obter mais informações, consulte [substituição de aplicações](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

#### <a name="user-centric-management"></a>Gestão centrada no utilizador
Suportam de aplicações do Configuration Manager *gestão centrada no utilizador*, que permite associar utilizadores específicos a dispositivos específicos. Em vez de ter de memorizar o nome de dispositivo de um utilizador, implemente aplicações para o usuário e para o dispositivo. Esta funcionalidade ajuda-o a certificar-se de que as aplicações mais importantes estão sempre disponíveis em cada um dos dispositivos do utilizador. Se um utilizador adquirir um novo computador, o Configuration Manager instala automaticamente as aplicações no dispositivo antes de iniciar sessão. 

Para obter mais informações, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="what-application-types-can-you-deploy"></a>Que tipos de aplicação pode implementar?  

O Configuration Manager permite-lhe implementar os seguintes tipos de aplicação:  

- Windows Installer (msi)  

- Pacote de aplicação do Windows (appx ou. appxbundle)  

    > [!Note]  
    > A partir da versão 1806, este tipo inclui o novo pacote de aplicação do Windows 10 (msix) e o pacote de aplicação (msixbundle) formatos.<!--1357427-->  

- Pacote de aplicação do Windows na Microsoft Store  

- Microsoft App-V v4 e v5  

- macOS  


Além disso, quando gerir dispositivos através do Microsoft Intune ou Configuration Manager no local-gestão de dispositivos, gerir estes tipos de aplicação adicionais:  

- Pacote de aplicação do Windows Phone (xap)  

- Pacote de aplicação do Windows Phone na Microsoft Store  

- Pacote de aplicação para iOS (. ipa)  

- Pacote de aplicação para iOS a partir da App Store  

- Pacote de aplicação para Android (ficheiro. apk)  

- Pacote de aplicação para Android no Google Play  

- Windows Installer através de MDM (msi)  

- Aplicação Web



## <a name="state-based-applications"></a>Aplicações baseadas no estado  

Aplicações do Configuration Manager utilizam monitorização baseada no estado. Pode controlar o último Estado de implementação de aplicação para utilizadores e dispositivos. As mensagens de estado apresentam informações sobre os dispositivos individuais. Por exemplo, se implementar uma aplicação numa coleção de utilizadores, pode ver o estado de conformidade da implantação e o objetivo da implementação na consola do Configuration Manager. Monitorizar a implementação de software a partir da **monitorização** área de trabalho na consola do Configuration Manager. Para obter mais informações, consulte [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

O cliente do Configuration Manager regularmente revê as implementações de aplicações. Por exemplo:  

- Um utilizador desinstalar uma aplicação implementada. No próximo ciclo de avaliação, o Configuration Manager detetar que a aplicação não estiver presente. Em seguida, o cliente reinstala automaticamente a aplicação.  

- O Configuration Manager não tiver instalado uma aplicação num dispositivo porque não conseguiu cumprir os requisitos. Posteriormente, é efetuada uma alteração ao dispositivo, que passa a satisfazer os requisitos. O Configuration Manager Deteta essa alteração, e o cliente instala a aplicação.  

Pode definir o intervalo de reavaliação para implementações de aplicações. Utilize o **agendar reavaliação para implementações** definição cliente do **implementação de Software** grupo. Para obter mais informações, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#software-deployment).  



## <a name="get-started-creating-an-application"></a>Introdução à criação de uma aplicação  

Se pretender avançar diretamente e criar uma aplicação, irá encontrar instruções na [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application) artigo.  

Se estiver familiarizado com as noções básicas e estiver à procura de para obter mais informações de referência sobre todas as opções disponíveis, comece a [criem aplicativos](/sccm/apps/deploy-use/create-applications).  



## <a name="software-center"></a>Centro de software  

Centro de software é um aplicativo de Windows instalado com o cliente do Configuration Manager. Utilizá-lo para as seguintes ações:  
- Procurar e pedir aplicações implementadas para o dispositivo ou utilizador
- Instalar e agendar instalações de software
- Ver o estado de instalação para aplicações, atualizações de software e sistemas operativos
- Configurar definições de controlo remoto
- Configurar a gestão de energia

Para obter mais informações, consulte os artigos seguintes:  
- [Planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Manual do utilizador do Software Center](/sccm/core/understand/software-center)

> [!Note]  
> A função de ponto de serviço do catálogo de aplicações web já não é necessária 1806, mas ainda é uma função suportada. 
> 
> A função de Web site do catálogo de aplicações não é suportada na versão 1806. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="packages-and-programs"></a>Pacotes e programas  

O Configuration Manager continua a suportar pacotes e programas que eram utilizados nas versões anteriores do produto. 

Para obter mais informações, consulte [pacotes e programas](/sccm/apps/deploy-use/packages-and-programs).  



## <a name="next-steps"></a>Passos seguintes

Agora que compreende os conceitos básicos do gerenciamento de aplicativos no Configuration Manager, avance para os artigos seguintes:
- [Criar e implementar uma aplicação de exemplo](/sccm/apps/get-started/create-and-deploy-an-application)
- [Planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Criar aplicações](/sccm/apps/deploy-use/create-applications)
