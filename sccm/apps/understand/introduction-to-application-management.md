---
title: "Introdução ao gerenciamento de aplicativos | Microsoft Docs"
description: "Descubra as informações básicas, que você precisará gerenciar e implantar aplicativos do System Center Configuration Manager."
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: 18
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 959a36413d06bb225f260bd44c1d3d59efd44e69
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Introdução ao gerenciamento de aplicativos no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Neste tópico, você aprenderá os conceitos básicos que você precisa saber antes de começar a trabalhar com aplicativos do System Center Configuration Manager.  

> [!TIP]  
>  Se você já estiver familiarizado com a forma de gerenciar aplicativos no Configuration Manager, você pode ignorar este tópico e passar para a criação de um aplicativo de exemplo. Consulte [Criar e implementar uma aplicação com o System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>O que é uma aplicação?  
 Embora *aplicativo* é um termo amplamente usado em computação, no Configuration Manager, isso significa algo diferente. Pense numa aplicação como uma caixa. Essa caixa contém um ou mais conjuntos de arquivos de instalação de um pacote de software (conhecido como um **tipo de implantação**), além de instruções sobre como implantar o software.  

 Quando a aplicação é implementada em dispositivos, os **requisitos** determinam o tipo de implementação que está instalado no dispositivo.  

 Você pode fazer muitas coisas mais com um aplicativo. Você saberá mais sobre essas coisas como ler este guia. A tabela a seguir apresenta alguns conceitos que você precisará saber antes de começar a se aprofundar:  

|Conceito|Descrição|    
|-|-|  
|**Requirements**|Nas versões anteriores do Configuration Manager, geralmente você deve criar uma coleção que contém os dispositivos que você desejava implantar um aplicativo. Embora você ainda pode criar uma coleção, com os requisitos, você pode especificar critérios mais detalhados para uma implantação de aplicativo.<br /><br /> Por exemplo, pode especificar que uma aplicação só pode ser instalada em dispositivos com o Windows 10. Em seguida, você pode implantar o aplicativo em seus dispositivos, mas ele será instalado somente em dispositivos que executam o Windows 10.<br /><br /> Configuration Manager avalia os requisitos para determinar se um aplicativo e qualquer de seus tipos de implantação será instalado. Em seguida, determina o tipo de implementação correto para a instalação da aplicação. Por predefinição, a cada sete dias as regras de requisitos são reavaliadas para garantir a compatibilidade, de acordo com a definição de cliente **Agendar a reavaliação das implementações**.<br /><br /> Para obter detalhes, consulte [criar e implantar um aplicativo](../../apps/get-started/create-and-deploy-an-application.md).|  
|**Condições globais**|Embora os requisitos são usados com um tipo de implantação específico em um único aplicativo, você também pode criar condições globais. Esses são uma biblioteca de requisitos predefinidos que você pode usar com qualquer aplicativo e o tipo de implantação.<br /><br /> Gerenciador de configuração contém um conjunto de condições globais internas e você também pode criar seus próprios.<br /><br /> Para obter detalhes, consulte [criar condições globais](../../apps/deploy-use/create-global-conditions.md).|  
|**Implementação simulada**|Avalia os requisitos, método de detecção e dependências de um aplicativo. Ele relata os resultados sem realmente instalar o aplicativo.<br /><br /> Para obter detalhes, consulte [simular implantações de aplicativos](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Ação de implementação**|Especifica se você deseja instalar ou desinstalar (quando houver suporte), o aplicativo que você está implantando.<br /><br /> Para obter detalhes, consulte [implantar aplicativos](../../apps/deploy-use/deploy-applications.md).|  
|**Objetivo da implementação**|Especifica se a aplicação de implementação será **Necessária**, ou **Disponível**.<br /><br /> **Necessário** significa que o aplicativo é implantado automaticamente de acordo com o agendamento que foi configurado. No entanto, o utilizador pode controlar o estado de implementação da aplicação caso este não se encontre oculto, podendo instalar a aplicação antes do fim do prazo utilizando o Centro de Software.<br /><br /> **Disponível** significa que, se a aplicação for implementada para um utilizador, este verá a aplicação publicada no Centro de Software e pode solicitá-la a pedido.<br /><br /> Para obter detalhes, consulte [implantar aplicativos](../../apps/deploy-use/deploy-applications.md).|  
|**Revisões**|Quando você faz revisões em um aplicativo ou a um tipo de implantação é contido em um aplicativo, o Configuration Manager cria uma nova versão do aplicativo. Você pode exibir o histórico de revisão de cada aplicativo, exibir suas propriedades, restaurar uma versão anterior de um aplicativo ou excluir uma versão antiga.<br /><br /> Para obter detalhes, consulte [atualizar e desativar aplicativos](../../apps/deploy-use/update-and-retire-applications.md).|  
|**Método de deteção**|Os métodos de deteção são utilizados para detetar se uma aplicação implementada já está instalada. Se o método de detecção indica que o aplicativo é instalado, o Configuration Manager não tenta instalá-lo novamente.<br /><br /> Para obter detalhes, consulte [criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|**Dependências**|As dependências definem um ou mais tipos de implementação a partir de outra aplicação que tem de ser instalada antes de um tipo de implementação ser instalado. Você pode configurar os tipos de implantação dependentes para instalar automaticamente antes que um tipo de implantação está instalado.<br /><br /> Para obter detalhes, consulte [criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|**Substituição**|Configuration Manager permite que você atualize ou substitua os aplicativos existentes usando uma relação de substituição. Quando você substitui um aplicativo, você pode especificar um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído. Você também pode decidir se para atualizar ou desinstalar o aplicativo substituído antes do aplicativo substituto é instalado.<br /><br /> Para obter detalhes, consulte [criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|**Gestão centrada no utilizador**|Suportam a aplicativos do Configuration Manager gerenciamento centrado no usuário, permitindo que você associar usuários específicos a dispositivos específicos. Em vez de ter de memorizar o nome do dispositivo de um utilizador, pode agora implementar aplicações para o utilizador e para o dispositivo. Esta funcionalidade ajuda-o a garantir que as aplicações mais importantes se encontram sempre disponíveis em cada dispositivo a que um utilizador específico acede. Se um usuário adquire um novo computador, você pode instalar automaticamente os aplicativos do usuário no dispositivo antes que ele entrar.<br /><br /> Para obter detalhes, consulte [vincular usuários e dispositivos com afinidade de dispositivo de usuário](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).|  

## <a name="what-application-types-can-you-deploy"></a>Que tipos de aplicação pode implementar?  
 Gerenciador de configuração permite que você implante os seguintes tipos de aplicativo:  

- Windows Installer (ficheiro *.msi)
- Pacote de aplicativo do Windows (*. AppX, *. appxbundle)
- Pacote de aplicações do Windows (na Loja Windows)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Ficheiro CAB do Windows Mobile
- macOS  


Além disso, quando você gerenciar dispositivos por meio do Microsoft Intune ou Configuration Manager gerenciamento de dispositivo local, você pode gerenciar esses tipos de aplicativo adicionais:

- Pacote de aplicação do Windows Phone (ficheiro *.xap)
- Pacote de Aplicações para iOS (ficheiro *.ipa)
- Pacote de Aplicações para Android (ficheiro *.apk)
- Pacote de aplicação para Android no Google Play
- Pacote de aplicação do Windows Phone (na Loja Windows Phone)
- Windows Installer através de MDM
- Aplicação Web



## <a name="state-based-applications"></a>Aplicações baseadas no estado  
 Aplicativos do Configuration Manager usam o com base no estado de monitoramento, pelo qual você pode controlar o último estado de implantação de aplicativo para usuários e dispositivos. As mensagens de estado apresentam informações sobre os dispositivos individuais. Por exemplo, se um aplicativo é implantado em uma coleção de usuários, você pode exibir o estado de conformidade da implantação e a finalidade da implantação no console do Configuration Manager. Você pode monitorar a implantação de todo o software usando o **monitoramento** espaço de trabalho no console do Configuration Manager. As implementações de software incluem atualizações de software, definições de compatibilidade, aplicações, sequências de tarefas e pacotes e programas. Para obter mais informações, consulte [monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Implantações de aplicativo são regularmente reavaliadas pelo Configuration Manager. Por exemplo:  

-   Uma aplicação implementada é desinstalada pelo utilizador final. No próximo ciclo de avaliação, o Configuration Manager detecta que o aplicativo não está presente e reinstalá-lo.  

-   Uma aplicação não foi instalada num dispositivo por não satisfazer os requisitos. Posteriormente, é efetuada uma alteração ao dispositivo, que passa a satisfazer os requisitos. Configuration Manager detecta essa alteração e o aplicativo está instalado.  


 Você pode definir o intervalo de reavaliação de implantações de aplicativo usando o **agendar a reavaliação de implantações** configuração do cliente. Para obter mais informações, consulte [sobre configurações do cliente](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Introdução à criação de uma aplicação  
 Se você quiser começar imediatamente e iniciar a criação de um aplicativo, você encontrará um passo a passo para criar um aplicativo simples no [criar e implantar um aplicativo](../../apps/get-started/create-and-deploy-an-application.md) tópico.  

 Se você estiver familiarizado com os conceitos básicos e deseja obter mais informações de referência sobre todas as opções disponíveis, comece por [criar aplicativos](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Centro de Software e o Catálogo de Aplicações  
 Nas versões anteriores do Configuration Manager, o Centro de Software foi usado para instalar e agendar instalações de software, definir configurações de controle remoto e configurar o gerenciamento de energia. Os usuários podem se conectar ao catálogo de aplicativos para procurar e solicitar software, definir algumas preferências e apagar remotamente seus dispositivos móveis.  

 Embora essas configurações ainda estejam disponíveis no System Center Configuration Manager, uma nova versão do Centro de Software está agora disponível que permite procurar aplicativos. Você não precisa usar o catálogo de aplicativos, o que requer um navegador da web habilitado para Silverlight. No entanto, as funções de sistema de sites de ponto de sites do Catálogo de Aplicações e de ponto de serviço Web do Catálogo de Aplicações ainda são necessárias para que as aplicações disponíveis ao utilizador sejam apresentadas no Centro de Software.  

 Para obter mais informações, consulte [planejar e configurar o gerenciamento de aplicativo](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="configuration-manager-packages-and-programs"></a>Gerenciador de configuração de pacotes e programas  
 Configuration Manager continua a suportar pacotes e programas que foram usados nas versões anteriores do produto. Uma implementação que utiliza pacotes e programas pode ser mais adequada do que uma implementação que utiliza uma aplicação quando implementa qualquer um dos seguintes procedimentos:  

-   Scripts que não instalam uma aplicação num computador, tal como um script para desfragmentar a unidade de disco do computador.  

-   Os scripts "pontuais" não têm de ser monitorizados continuamente.  

-   Os scripts que são executados num agendamento periódico e não podem utilizar a avaliação global.

 Para obter mais informações, consulte [pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  

