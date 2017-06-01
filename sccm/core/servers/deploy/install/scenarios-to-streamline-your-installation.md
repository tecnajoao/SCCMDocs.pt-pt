---
title: "Cenários de instalação | Documentos do Microsoft"
description: "Saiba mais técnicas para instalar uma nova hierarquia do Configuration Manager quando estiver a atualizar ou atualizar um site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9dac6b3fa92c193e3c1a75dd804e0b72fb5394b9
ms.openlocfilehash: dbc303ea9df5a429cb2ef8bd89f372639a4ae2b2
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Cenários para simplificar a instalação do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o lançamento de versões de atualização para System Center Configuration Manager atual ramificação, existem novos cenários para simplificar a instalação de uma nova hierarquia para uma versão de atualização (como atualizar 1610) e para atualizar a partir do Microsoft System Center 2012 Configuration Manager.

Os cenários suportados incluem:  

**Instalar uma hierarquia novo para o System Center Configuration Manager atual ramo** que executa uma versão de atualização.  

-   Instalar apenas no site de nível superior e, em seguida, instalar imediatamente uma atualização para trazer esse site atual com a versão de atualização que irá utilizar. Em seguida, pode instalar sites adicionais diretamente para essa versão de atualização.  
-   Neste cenário, ignorar o processo de instalação de sites adicionais a um nível de linha de base e, em seguida, atualizando-as para a versão de atualização que pretende utilizar.  
-   Neste cenário, ignorar o processo de instalação de clientes para uma versão de linha de base e voltar a instalá-los quando atualizar para uma versão posterior.  

**Atualizar um Microsoft System Center 2012 Configuration Manager** infraestrutura para uma versão de atualização do System Center Configuration Manager.  

-   Atualizar manualmente o site de administração central e cada site primário para uma versão do plano base (como versão 1606) antes de instalar uma versão de atualização (como versão 1610).  
-   Não atualize os sites secundários a partir do Microsoft System Center 2012 Configuration Manager até que os sites primários de executam a versão de atualização que irá utilizar.  
-   Não atualize os clientes a partir do Microsoft System Center 2012 Configuration Manager até que os sites primários de executam a versão de atualização que irá utilizar.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Cenário: Instalar uma nova hierarquia para uma versão de atualização  
Neste cenário de exemplo, instale o primeiro site de uma hierarquia utilizando a versão de linha de base do System Center Configuration Manager, como versão 1610. Em seguida, instale a atualização de 1610 antes de implementar sites adicionais ou clientes.  

-   Uma vez que pretender utilizar uma versão de atualização (como versão 1610) e não permaneça na versão plano base (como versão 1606), precisa de instalar sites adicionais e, em seguida, atualizá-los. Isto aplica-se também aos clientes.  
-   Não instale sites secundários com a versão 1606 e, em seguida, atualizá-los para a versão 1610. Instale sites secundários em vez disso, após a execução de sites primários de versão 1610.  

Siga esta sequência:  

1.  **Instalar um site de nível superior para a nova hierarquia** utilizando o suporte de dados de linha de base.  

    -   Pode utilizar suportes de dados de linha de base apenas para instalar o primeiro site numa nova hierarquia.  
    -   Por exemplo, instale um site de nível superior utilizando a versão de linha de base do 1606. Para obter mais informações, consulte o artigo [utilizar o Assistente de configuração para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Após este passo, o seu site de nível superior é executado versão 1606.  

2.  **Utilize as atualizações na consola para atualizar o seu site de nível superior para uma versão posterior.**  

    -   Antes de instalar quaisquer sites subordinados ou clientes, atualize o seu site de nível superior para a versão de atualização que pretende utilizar.  
    -   Por exemplo, pode atualizar o site de nível superior que executa versão 1606 para versão 1610. Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Após este passo, o seu site de nível superior é executado versão 1610.  

3.  **Instale os novos sites primários subordinados abaixo de um site de administração central.**  

    -   Utilize o suporte de dados de instalação a partir da pasta CD.Latest no servidor do site de administração central para instalar sites primários subordinados. Para obter mais informações, veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest do System Center Configuration Manager)](../../../../core/servers/manage/the-cd.latest-folder.md).  

      Este suporte de dados de origem é necessário para assegurar que os novos sites primários subordinados correspondem à versão do site de administração central.  

    Após este passo, os novos sites primários subordinados executem versão 1610.  

4.  **Em cada site primário, utilize a opção na consola para instalar novos sites secundários.**  

    -   Porque não foi possível instalar sites secundários enquanto os sites primários foram na versão 1606, não é necessário atualizar sites secundários.  
    -   Em vez disso, instale novos sites secundários que executam versão 1610. Para obter mais informações, veja [Instalar um site secundário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) no tópico [Utilizar o Assistente de Configuração para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Após este passo, os novos sites secundários são instalados e execute versão 1610.  

5.  **Instale novos clientes no site primário.**  

    -   Porque não foi possível instalar os clientes enquanto os sites primários foram na versão 1606, não é necessário atualizar os clientes a partir da versão 1606 para versão 1610.  
    -   Em vez disso, instale novos clientes que executam versão 1610. Para obter mais informações, consulte o artigo [implementar clientes no System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Após este passo, os novos clientes são instalados com a versão 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Cenário: Atualização do System Center 2012 Configuration Manager para uma versão de atualização do System Center Configuration Manager, ramo atual  
Neste cenário de exemplo, atualize a infraestrutura do Microsoft System Center 2012 Configuration Manager para uma versão de atualização do System Center Configuration Manager, como versão 1610.  

-   O site de administração central e cada site primário tem de atualizar para a versão de linha de base 1606 antes de instalar a atualização para a versão 1610.  
-   Os sites secundários e os clientes não atualizar ou instalar a versão 1606. Em vez disso, mudam diretamente a partir do Microsoft System Center 2012 Configuration Manager para System Center Configuration Manager versão 1610.  

Siga esta sequência:  

1.  **Atualizar o seu site do Microsoft System Center 2012 Configuration Manager de nível superior** para uma versão de linha de base do mesmo atual utilizando suportes de dados de origem para o System Center Configuration Manager (como versão 1606). Para obter mais informações, consulte o artigo [atualizar para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Como cenários de atualização tradicionais, pode sempre atualizar primeiro o site de nível superior de uma hierarquia e, em seguida, atualizar os sites subordinados.  

    Após este passo, o seu site de nível superior é executado versão 1606.  

2.  **Atualize cada site primário subordinado na hierarquia** para essa mesma versão de linha de base.  

    -   Ao atualizar a partir do Microsoft System Center 2012 Configuration Manager, tem de atualizar manualmente cada site primário para uma versão de linha de base do mesmo atual.  
    -   Neste momento, não irá atualizar sites secundários.  

    Após este passo, cada site primário executa versão 1606.  

3.  **Definir janelas de manutenção em sites primário subordinado.** Após atualizar todos os sites primários para a versão do plano base, planeie a configurar janelas de manutenção para controlar quando desses sites que instalarem atualizações de infraestrutura. Para obter mais informações, consulte o artigo [como utilizar as janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Janelas de manutenção são denominadas *service windows* na versão 1606.)  

    -   Um site primário subordinado instala automaticamente as mesmas atualizações que o utilizador instala num site de administração central.  
    -   Sties secundários não instalam automaticamente novas versões. Deve atualizá-los manualmente a partir de dentro da consola.  

  Após este passo, quando instalar atualizações no site de administração central, os sites primários subordinados irão instalar apenas essa atualização quando for permitido pela respetiva janela de manutenção.  

4.  **Instale a versão de atualização no seu site de nível superior.** Este procedimento atualiza o site de nível superior. Depois de um site de administração central instala a versão de atualização, cada site primário subordinado instala automaticamente a atualização, a menos que a instalação está bloqueada por uma janela de manutenção.  

    -   Por exemplo, pode atualizar o site de nível de versão 1606 versão 1610. Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Após este passo, o seu site de administração central e cada site primário executa versão 1610.  

5.  **Atualize os sites secundários.** Depois de um site primário, instala a atualização e executa versão 1610, utilize a opção na consola para atualizar sites secundários.  

    -   Isto atualiza os sites secundários diretamente a partir do Microsoft System Center 2012 Configuration Manager para a versão de atualização que tenha instalado no site primário.  
    -   Para informações sobre como atualizar um site secundário, consulte o artigo [atualizar sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) no [atualizar para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) tópico.  

6.  **Atualizar clientes.** Para atualizar os clientes, utilize as informações no [como atualizar clientes para computadores com Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Isto atualiza os clientes diretamente a partir do Microsoft System Center 2012 Configuration Manager para a versão de atualização que tenha instalado no site primário.  

    Após este passo, os clientes são atualizados para a versão 1610 sem primeiro atualizar para versão 1606.

