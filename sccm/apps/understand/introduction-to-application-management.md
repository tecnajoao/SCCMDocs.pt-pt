---
title: Introdução à gestão de aplicações
titleSuffix: Configuration Manager
description: Detete as informações básicas, que terá de gerir e implementar aplicações do System Center Configuration Manager.
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bcdc5800a1c280c99289528c40e0efee8acf5ad5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336175"
---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Introdução à gestão de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Neste tópico, irá aprender as noções básicas que precisa de saber antes de começar a trabalhar com aplicações do System Center Configuration Manager.  

> [!TIP]  
>  Se já estiver familiarizado com a gestão de aplicações no Configuration Manager, pode ignorar este tópico e avançar para a criação de uma aplicação de exemplo. Consulte [Criar e implementar uma aplicação com o System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>O que é uma aplicação?  
 Embora *aplicação* é um termo bastante utilizado em informática, no Gestor de configuração, significa algo diferente. Pense numa aplicação como uma caixa. Esta caixa contém um ou mais conjuntos de ficheiros de instalação de um pacote de software (conhecido como um **tipo de implementação**), juntamente com instruções sobre como implementar o software.  

 Quando a aplicação é implementada em dispositivos, os **requisitos** determinam o tipo de implementação que está instalado no dispositivo.  

 Pode fazê-lo inúmeros aspetos mais com uma aplicação. Irá aprender sobre estes coisas como ler este guia. A tabela seguinte apresenta alguns conceitos que terá de saber antes de começar a investigar mais:  

|Conceito|Descrição|    
|-|-|  
|**Requirements**|Em versões anteriores do Configuration Manager, normalmente criaria uma coleção que contém os dispositivos que quer implementar uma aplicação. Embora ainda possa criar uma coleção com os requisitos, que pode especificar critérios mais detalhados para uma implementação de aplicação.<br /><br /> Por exemplo, pode especificar que uma aplicação só pode ser instalada em dispositivos com o Windows 10. Em seguida, pode implementar a aplicação nos seus dispositivos, mas só será instalada nos dispositivos que executam o Windows 10.<br /><br /> O Configuration Manager avalia os requisitos para determinar se uma aplicação e algum dos respetivos tipos de implementação será instalado. Em seguida, determina o tipo de implementação correto para a instalação da aplicação. Por predefinição, a cada sete dias as regras de requisitos são reavaliadas para garantir a compatibilidade, de acordo com a definição de cliente **Agendar a reavaliação das implementações**.<br /><br /> Para obter mais informações, consulte [criar e implementar uma aplicação](../../apps/get-started/create-and-deploy-an-application.md).|  
|**Condições globais**|Apesar dos requisitos são utilizados com um tipo de implementação específico numa única aplicação, também pode criar condições globais. Estes são uma biblioteca de requisitos predefinidos que pode utilizar com qualquer aplicação e o tipo de implementação.<br /><br /> Gestor de configuração contém um conjunto de condições globais incorporadas e também pode criar os seus próprios.<br /><br /> Para obter mais informações, consulte [criar condições globais](../../apps/deploy-use/create-global-conditions.md).|  
|**Implementação simulada**|Avalia os requisitos, o método de deteção e dependências para uma aplicação. -Reporta os resultados sem instalar efetivamente a aplicação.<br /><br /> Para obter mais informações, consulte [simular implementações de aplicações](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Ação de implementação**|Especifica se pretende instalar ou desinstalar (quando suportadas), a aplicação estiver a implementar.<br /><br /> Para obter mais informações, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).|  
|**Objetivo da implementação**|Especifica se a aplicação de implementação será **Necessária**, ou **Disponível**.<br /><br /> **Necessário** significa que a aplicação é implementada automaticamente, de acordo com a agenda que tenha sido configurada. No entanto, o utilizador pode controlar o estado de implementação da aplicação caso este não se encontre oculto, podendo instalar a aplicação antes do fim do prazo utilizando o Centro de Software.<br /><br /> **Disponível** significa que, se a aplicação for implementada para um utilizador, este verá a aplicação publicada no Centro de Software e pode solicitá-la a pedido.<br /><br /> Para obter mais informações, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).|  
|**Revisões**|Quando são efetuadas revisões de uma aplicação ou um tipo de implementação que está contido numa aplicação, o Configuration Manager cria uma nova versão da aplicação. Pode visualizar o histórico de cada revisão da aplicação, ver as respetivas propriedades, restaurar uma versão anterior de uma aplicação ou eliminar uma versão antiga.<br /><br /> Para obter mais informações, consulte [atualizar e extinguir aplicações](../../apps/deploy-use/update-and-retire-applications.md).|  
|**Método de deteção**|Os métodos de deteção são utilizados para detetar se uma aplicação implementada já está instalada. Se o método de deteção indicar que a aplicação está instalada, o Configuration Manager não tenta instalá-la novamente.<br /><br /> Para obter mais informações, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).|  
|**Dependências**|As dependências definem um ou mais tipos de implementação a partir de outra aplicação que tem de ser instalada antes de um tipo de implementação ser instalado. Pode configurar os tipos de implementação dependentes para serem automaticamente instalados antes de um tipo de implementação está instalado.<br /><br /> Para obter mais informações, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).|  
|**Substituição**|O Configuration Manager permite-lhe atualizar ou substituir as aplicações existentes utilizando uma relação de substituição. Se substituir uma aplicação, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída. Também pode decidir se atualizar ou desinstalar a aplicação substituída antes da aplicação substituta está instalado.<br /><br /> Para obter mais informações, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).|  
|**Gestão centrada no utilizador**|Aplicações do Configuration Manager suportam gestão centrada no utilizador, permitindo-lhe associar utilizadores específicos a dispositivos específicos. Em vez de ter de memorizar o nome do dispositivo de um utilizador, pode agora implementar aplicações para o utilizador e para o dispositivo. Esta funcionalidade ajuda-o a garantir que as aplicações mais importantes se encontram sempre disponíveis em cada dispositivo a que um utilizador específico acede. Se um utilizador adquirir um novo computador, poderá instalar automaticamente as aplicações do utilizador no dispositivo antes de iniciar sessão.<br /><br /> Para obter mais informações, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).|  

## <a name="what-application-types-can-you-deploy"></a>Que tipos de aplicação pode implementar?  
 O Configuration Manager permite-lhe implementar os seguintes tipos de aplicação:  

- Windows Installer (ficheiro *.msi)
- Pacote de aplicações do Windows (\*. AppX, \*. appxbundle)
- Pacote de aplicações do Windows (na Loja Windows)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Ficheiro CAB do Windows Mobile
- macOS  


Além disso, quando gerir dispositivos através do Microsoft Intune do Configuration Manager local ou na gestão de dispositivos, pode gerir estes tipos de aplicação adicionais:

- Pacote de aplicação do Windows Phone (ficheiro *.xap)
- Pacote de Aplicações para iOS (ficheiro *.ipa)
- Pacote de Aplicações para Android (ficheiro *.apk)
- Pacote de aplicação para Android no Google Play
- Pacote de aplicação do Windows Phone (na Loja Windows Phone)
- Windows Installer através de MDM
- Aplicação Web



## <a name="state-based-applications"></a>Aplicações baseadas no estado  
 Aplicações do Configuration Manager utilizam monitorização baseada no Estado, que pode controlar o último Estado de implementação de aplicação para utilizadores e dispositivos. As mensagens de estado apresentam informações sobre os dispositivos individuais. Por exemplo, se uma aplicação for implementada para uma coleção de utilizadores, pode ver o estado de compatibilidade da implementação e o objetivo da implementação na consola do Configuration Manager. Pode monitorizar a implementação de todo o software utilizando o **monitorização** área de trabalho na consola do Configuration Manager. As implementações de software incluem atualizações de software, definições de compatibilidade, aplicações, sequências de tarefas e pacotes e programas. Para obter mais informações, consulte [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 As implementações de aplicações são regularmente reavaliadas pelo Configuration Manager. Por exemplo:  

-   Uma aplicação implementada é desinstalada pelo utilizador final. No próximo ciclo de avaliação, o Configuration Manager detetar que a aplicação não está presente e reinstalará.  

-   Uma aplicação não foi instalada num dispositivo por não satisfazer os requisitos. Posteriormente, é efetuada uma alteração ao dispositivo, que passa a satisfazer os requisitos. O Configuration Manager Deteta essa alteração e a aplicação está instalada.  


 Pode definir o intervalo de reavaliação para implementações de aplicações utilizando o **agendar reavaliação para implementações** definição de cliente. Para obter mais informações, consulte [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Introdução à criação de uma aplicação  
 Se pretender avançar diretamente e começar a criar uma aplicação, encontrará uma explicação passo a passo para criar uma aplicação simples no [criar e implementar uma aplicação](../../apps/get-started/create-and-deploy-an-application.md) tópico.  

 Se estiver familiarizado com as noções básicas e estiver à procura de informações mais detalhadas referência sobre todas as opções disponíveis, inicie a partir da [criar aplicações](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Centro de Software e o Catálogo de Aplicações  
 Em versões anteriores do Configuration Manager, o Centro de Software foi utilizado para instalar e agendar instalações de software, configurar definições de controlo remoto e configurar a gestão de energia. Os utilizadores foi possível ligar ao catálogo de aplicações para procurar e solicitar software, definir algumas preferências e apagar remotamente os seus dispositivos móveis.  

 Enquanto estas definições ainda estão disponíveis no System Center Configuration Manager, agora está disponível uma versão nova do Centro de Software que lhe permite procurar aplicações. Não tem de utilizar o catálogo de aplicações, que requer um browser com capacidade para Silverlight web. No entanto, as funções de sistema de sites de ponto de sites do Catálogo de Aplicações e de ponto de serviço Web do Catálogo de Aplicações ainda são necessárias para que as aplicações disponíveis ao utilizador sejam apresentadas no Centro de Software.  

 Para obter mais informações, consulte [planear e configurar a gestão de aplicações](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="configuration-manager-packages-and-programs"></a>O Configuration Manager pacotes e programas  
 O Configuration Manager continua a suportar pacotes e programas que foram utilizados em versões anteriores do produto. Uma implementação que utiliza pacotes e programas pode ser mais adequada do que uma implementação que utiliza uma aplicação quando implementa qualquer um dos seguintes procedimentos:  

-   Scripts que não instalam uma aplicação num computador, tal como um script para desfragmentar a unidade de disco do computador.  

-   Os scripts "pontuais" não têm de ser monitorizados continuamente.  

-   Os scripts que são executados num agendamento periódico e não podem utilizar a avaliação global.

 Para obter mais informações, consulte [pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  
