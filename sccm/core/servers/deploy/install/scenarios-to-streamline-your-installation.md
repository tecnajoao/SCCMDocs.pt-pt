---
title: Cenários de instalação
titleSuffix: Configuration Manager
description: Saiba mais técnicas para instalar uma nova hierarquia do Configuration Manager quando estiver a atualizar ou atualizar um site.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77615ab53f715a5d3e5b2e21cda667e6f0a2bc0c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Cenários para simplificar a instalação do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o lançamento de versões de atualização para o ramo atual do System Center Configuration Manager, há novos cenários para simplificar a instalação de uma nova hierarquia para uma versão de atualização (como a atualização 1610) e para atualizar a partir do Microsoft System Center 2012 Configuration Manager.

Os cenários suportados incluem:  

**Instalar uma novo ramo hierarquia System Center Configuration Manager atual** que executa uma versão de atualização.  

-   Instalar apenas o site de nível superior e, em seguida, imediatamente a instalar uma atualização para trazer esse site atual com a versão de atualização que irá utilizar. Em seguida, pode instalar sites adicionais diretamente para essa versão de atualização.  
-   Neste cenário, ignorar o processo de instalação de sites adicionais para um nível de linha de base e, em seguida, atualizando-as para a versão de atualização que pretende utilizar.  
-   Neste cenário, ignorar o processo de instalação de clientes para uma versão de linha de base e voltar a instalá-los quando atualizar para uma versão posterior.  

**Atualizar um Microsoft System Center 2012 Configuration Manager** infraestrutura para uma versão de atualização do System Center Configuration Manager.  

-   Atualizar manualmente o site de administração central e cada site primário para uma versão de linha de base (como a versão 1606) antes de instalar uma versão de atualização (como a versão 1610).  
-   Não atualize os sites secundários do Microsoft System Center 2012 Configuration Manager até que os sites primários executarem a versão de atualização que irá utilizar.  
-   Não atualize os clientes do Microsoft System Center 2012 Configuration Manager até que os sites primários executarem a versão de atualização que irá utilizar.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Cenário: Instalar uma nova hierarquia para uma versão de atualização  
Neste cenário de exemplo, instale o primeiro site de uma hierarquia utilizando uma versão de linha de base do System Center Configuration Manager, como a versão 1610. Em seguida, instale a atualização de 1610 antes de implementar sites ou clientes adicionais.  

-   Dado que pretende utilizar uma versão de atualização (como a versão 1610) e não continuar uma versão de linha de base (como a versão 1606), não precisa de instalar sites adicionais e, em seguida, atualizá-los. Isto também se aplica aos clientes.  
-   Não instale sites secundários com a versão 1606 e, em seguida, atualizá-los para a versão 1610. Em vez disso, instale sites secundários depois dos sites primários executarem a versão 1610.  

Siga esta sequência:  

1.  **Instalar um site de nível superior para a nova hierarquia** utilizando o suporte de dados de linha de base.  

    -   Pode utilizar suportes de dados de linha de base apenas para instalar o primeiro site numa nova hierarquia.  
    -   Por exemplo, instale um site de nível superior utilizando a versão de linha de base do 1606. Para obter mais informações, consulte [utilize o Assistente de configuração para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Após este passo, o site de nível superior executa a versão 1606.  

2.  **Utilize as atualizações na consola para atualizar o site de nível superior para uma versão posterior.**  

    -   Antes de instalar sites subordinados ou clientes, atualize o site de nível superior para a versão de atualização que pretende utilizar.  
    -   Por exemplo, pode atualizar o site de nível superior que executa a versão 1606 para a versão 1610. Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Após este passo, o site de nível superior executa a versão 1610.  

3.  **Instale os novos sites primários subordinados abaixo de um site de administração central.**  

    -   Utilize o suporte de dados de instalação a partir da pasta CD.Latest no servidor do site de administração central para instalar sites primários subordinados. Para obter mais informações, veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest do System Center Configuration Manager)](../../../../core/servers/manage/the-cd.latest-folder.md).  

      Este suporte de dados de origem é necessário para assegurar que os novos sites primários subordinados correspondem à versão do site de administração central.  

    Após este passo, os novos sites primários subordinados executam versão 1610.  

4.  **Em cada site primário, utilize a opção na consola para instalar novos sites secundários.**  

    -   Porque não instalou sites secundários enquanto os sites primários estavam na versão 1606, não terá de atualizar os sites secundários.  
    -   Em vez disso, instale novos sites secundários que executem a versão 1610. Para obter mais informações, veja [Instalar um site secundário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) no tópico [Utilizar o Assistente de Configuração para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Após este passo, novos sites secundários são instalados e executam a versão 1610.  

5.  **Instale novos clientes no site primário.**  

    -   Porque não instalou clientes enquanto os sites primários estavam na versão 1606, não terá de atualizar os clientes da versão 1606 para versão 1610.  
    -   Em vez disso, instale novos clientes que executam a versão 1610. Para obter mais informações, consulte [implementar clientes no System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Após este passo, são instalados novos clientes que executam a versão 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Cenário: Atualização do System Center 2012 Configuration Manager para uma versão de atualização do System Center Configuration Manager, o ramo atual  
Neste cenário de exemplo, atualize a sua infraestrutura do Microsoft System Center 2012 Configuration Manager para uma versão de atualização do System Center Configuration Manager, como a versão 1610.  

-   O site de administração central e cada site primário tem de atualizar para a versão de linha de base 1606 antes de instalar a atualização da versão 1610.  
-   Os sites secundários e os clientes não atualizar ou instalar a versão 1606. Em vez disso, estes passam diretamente do Microsoft System Center 2012 Configuration Manager para System Center Configuration Manager versão 1610.  

Siga esta sequência:  

1.  **Atualizar o site do Microsoft System Center 2012 Configuration Manager de nível superior** para uma versão de linha de base da filial atual utilizando o suporte de dados de origem para o System Center Configuration Manager (como a versão 1606). Para obter mais informações, consulte [atualizar para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Como cenários de atualização tradicionais, atualiza sempre primeiro do site de nível superior de uma hierarquia e, em seguida, atualizar os sites subordinados.  

    Após este passo, o site de nível superior executa a versão 1606.  

2.  **Atualize cada site primário subordinado na hierarquia** para essa mesma versão de linha de base.  

    -   Quando atualizar a partir do Microsoft System Center 2012 Configuration Manager, tem de atualizar manualmente cada site primário para uma versão de linha de base da filial atual.  
    -   Neste momento, não irá atualizar os sites secundários.  

    Após este passo, cada site primário executa a versão 1606.  

3.  **Definir janelas de manutenção em sites primários subordinados.** Depois de atualizar todos os sites primários para a versão de linha de base, planeie configurar janelas de manutenção para controlar quando esses sites instalam atualizações de infraestrutura. Para obter mais informações, consulte [como utilizar janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (As janelas de manutenção são denominadas *serviço windows* versão 1606.)  

    -   Um site primário subordinado instala automaticamente as mesmas atualizações que o utilizador instala num site de administração central.  
    -   Secundários não instalam automaticamente novas versões. Tem de atualizá-los manualmente a partir da consola do.  

  Após este passo, quando instalar atualizações no site de administração central, os sites primários subordinados irão instalar apenas essa atualização quando for permitido pela respetiva janela de manutenção.  

4.  **Instale a versão de atualização no seu site de nível superior.** Isto atualiza o site de nível superior. Depois da versão de atualização é instalado um site de administração central, cada site primário subordinado instala automaticamente a atualização, a menos que a instalação está bloqueada por uma janela de manutenção.  

    -   Por exemplo, pode atualizar o site de nível de versão 1606 de versão 1610. Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Após este passo, o site de administração central e cada site primário executa a versão 1610.  

5.  **Atualize os sites secundários.** Depois de um site primário, instala a atualização e executa a versão 1610, utilize a opção na consola para atualizar sites secundários.  

    -   Este procedimento atualiza os sites secundários diretamente a partir do Microsoft System Center 2012 Configuration Manager para a versão de atualização que instalou no site primário.  
    -   Para informações sobre como atualizar um site secundário, consulte [atualizar sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) no [atualizar para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) tópico.  

6.  **Atualizar clientes.** Para atualizar os clientes, utilize as informações no [como atualizar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Isto atualiza os clientes diretamente a partir do Microsoft System Center 2012 Configuration Manager para a versão de atualização que instalou no site primário.  

    Após este passo, os clientes são atualizados para a versão 1610 sem primeiro atualizar para a versão 1606.
