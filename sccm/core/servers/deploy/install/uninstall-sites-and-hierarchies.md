---
title: Desinstalar sites
titleSuffix: Configuration Manager
description: Utilize estes detalhes como guia para desinstalar um site do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50543fdd042eb0285c070d8714cb98eec9a7629f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129073"
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Desinstalar sites e hierarquias no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize os seguintes detalhes como guia se precisar de desinstalar um site do System Center Configuration Manager.  

Para desativar uma hierarquia com múltiplos sites, a sequência de remoção é importante. Comece por desinstalar os sites na parte inferior da hierarquia e, em seguida, mover para cima:  

1.  Remova sites secundários ligados a sites primários.  
2.  Remova os sites primários.
3.  Depois de todos os sites primários serem removidos, pode desinstalar o site de administrações centrais.  


##  <a name="BKMK_RemoveSecondarysite"></a> Remover um site secundário de uma hierarquia  
Não é possível mover um site secundário ou reatribuir um site secundário para um novo site primário principal. Para ser removido de uma hierarquia, um site secundário deve ser excluído do respetivo site principal direto. Utilize a eliminar o Assistente para Site secundário da consola do Configuration Manager para remover um site secundário. Quando remove um site secundário, tem de escolher se pretende eliminá-lo ou desinstale-a:  

-   **Desinstalar o site secundário**. Utilize esta opção para remover um site secundário funcional acessível a partir da rede. Esta opção desinstala o Configuration Manager do servidor do site secundário e, em seguida, elimina todas as informações sobre o site e os respetivos recursos da hierarquia do site do Configuration Manager. Se o Configuration Manager instalado o SQL Server Express como parte da instalação do site secundário, Configuration Manager irá desinstalar o SQL Express quando desinstalar o site secundário. Se o SQL Server Express tiver sido instalado antes de instalar o site secundário, o Configuration Manager será desinstalado não SQL Server Express.  

-   **Eliminar o site secundário**. Utilize esta opção se uma das seguintes opções for verdadeira:  

    -   Não foi possível instalar um site secundário  
    -   O site secundário continua a ser apresentada na consola do Configuration Manager após a desinstalação

    Esta opção elimina todas as informações sobre o site e os respetivos recursos da hierarquia do Configuration Manager, mas deixa o Configuration Manager instalado no servidor do site secundário.  

    > [!NOTE]  
    >  Também pode utilizar a ferramenta manutenção da hierarquia e o **/DELSITE** opção para eliminar um site secundário. Para obter mais informações, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Para desinstalar ou eliminar um site secundário  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos administrativos no computador do site secundário  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site primário, se for remoto  
    -   Função de segurança de administrador de infraestrutura ou de administrador global no site primário principal  
    -   Direitos sysadmin na base de dados do site secundário  

2.  Na consola do Configuration Manager, selecione **administração**.  
3.  Na **Administration** área de trabalho, expanda **configuração do Site**e, em seguida, selecione **Sites**.  
4.  Selecione o servidor de site secundário que pretende remover.  
5.  Sobre o **home page** separador a **Site** grupo, selecione **eliminar**.  
6.  Na página **Geral** , selecione se pretende desinstalar ou eliminar o site secundário e clique em **Seguinte**.  
7.  Sobre o **resumo** página, verifique as definições e, em seguida, selecione **próxima**.  
8.  Sobre o **conclusão** página, selecione **fechar** para sair do assistente.  

##  <a name="BKMK_UninstallPrimary"></a> Desinstalar um site primário  
Pode executar a configuração do Configuration Manager para desinstalar um site primário que não tenha um site secundário associado. Antes de desinstalar um site primário, considere o seguinte:  

-   Quando os clientes do Configuration Manager estão dentro dos limites configurados no site e o site primário é parte de uma hierarquia do Configuration Manager, considere adicionar os limites a outro site primário na hierarquia antes de desinstalar o site primário .  
-   Quando o servidor do site primário deixa de estar disponível, tem de utilizar a Ferramenta de Manutenção da Hierarquia no site de administração central para eliminar o site primário da base de dados do site. Para obter mais informações, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Utilize o procedimento seguinte para desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site"></a>Para desinstalar um site primário  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos de administrador local no servidor do site de administração central  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site de administração central, se for remoto
    -   Direitos sysadmin na base de dados do site de administração central  
    -   Direitos de administrador local no computador do site primário  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site primário, se for remoto  
    -   Um nome de utilizador associado à função de segurança administrador de infraestrutura ou de administrador global no site de administração central  

2.  Inicie configuração do Configuration Manager no servidor do site primário utilizando um dos seguintes métodos:  

    -   No **começar**, selecione **configuração do Configuration Manager**.  
    -   Abrir Setup.exe partir &lt; *Suportededadosdeinstalaçãodoconfigmgr*> \SMSSETUP\BIN\X64.  
    -   Abrir Setup.exe partir &lt; *Caminhodeinstalaçãodoconfigmgr*> \BIN\X64.  

3.  Sobre o **antes de começar** página, selecione **próxima**.  
4.  Sobre o **introdução** página, selecione **desinstalar um site do Configuration Manager**e, em seguida, selecione **seguinte**.  
5.  Sobre o **desinstalar o Site do Configuration Manager**, especifique se pretende remover a base de dados do site do servidor do site primário e se pretende remover a consola do Configuration Manager. Por predefinição, a Configuração remove ambos os itens.  

    > [!IMPORTANT]  
    >  Quando um site secundário está associado ao site primário, tem de remover o site secundário antes de poder desinstalar o site primário.  

6.  Selecione **Sim** para confirmar a desinstalação do site primário do Configuration Manager.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Desinstalar um site primário configurado com vistas distribuídas  
 Antes de desinstalar um site primário subordinado que possui vistas ativadas para a respetiva ligação de replicação para o site de administração central distribuídas, tem de desativar as vistas distribuídas na sua hierarquia. Utilize as seguintes informações para desativar as vistas distribuídas antes de desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Para desinstalar um site primário configurado com vistas distribuídas  

1.  Antes de desinstalar qualquer site primário, tem de desativar as vistas distribuídas de cada ligação na hierarquia entre o site de administração central e um site primário.  
2.  Depois de desativar as vistas distribuídas de cada ligação, certifique-se que os dados do site primário é concluída a reinicializar no site de administração central. Para monitorizar a inicialização dos dados, na consola do Configuration Manager, no **monitorização** área de trabalho, ver a ligação no **replicação de base de dados** nó.  
3.  Após a reinicialização bem-sucedida dos dados com o site de administração central, pode desinstalar o site primário. Para desinstalar um site primário, consulte [desinstalar um site primário](#BKMK_UninstallPrimary).  
4.  Quando o site primário está completamente desinstalado, pode reconfigurar as vistas distribuídas em ligações aos sites primários.  

    > [!IMPORTANT]  
    >  Se desinstalar o site primário antes de desativar as vistas distribuídas em cada site ou antes dos dados do site primário reinicializa com êxito no site de administração central, replicação de dados entre sites primários e a administração central site poderá falhar. Neste cenário, tem de desativar as vistas distribuídas de cada ligação na sua hierarquia do site e, em seguida, após os reinicialização bem-sucedida dos dados com o site de administração central, pode reconfigurar as vistas distribuídas.  

##  <a name="BKMK_UninstallCAS"></a> Desinstalar o site de administração central  
 Pode executar a configuração do Configuration Manager para desinstalar um site de administração central que não tenha sites primários subordinados. Utilize o procedimento seguinte para desinstalar o site de administração central.  

#### <a name="to-uninstall-a-central-administration-site"></a>Para desinstalar um site de administração central  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração detém os seguintes direitos de segurança:  

    -   Direitos de administrador local no servidor do site de administração central  
    -   Direitos de administrador local no servidor de base de dados do site para o site de administração central, se o servidor de base de dados do site não estiver instalado no servidor do site 

2.  Inicie a configuração do Configuration Manager no servidor do site de administração central utilizando um dos seguintes métodos:  

    -   Em **Iniciar**, clique em **Configuração do Configuration Manager**.  
    -   Abrir Setup.exe partir &lt; *Suportededadosdeinstalaçãodoconfigmgr*> \SMSSETUP\BIN\X64.  
    -   Abrir Setup.exe partir &lt; *Caminhodeinstalaçãodoconfigmgr*> \BIN\X64.  

3.  Sobre o **antes de começar** página, selecione **próxima**.  
4.  Sobre o **introdução** página, selecione **desinstalar um site do Configuration Manager**e, em seguida, selecione **seguinte**.  
5.  Sobre o **desinstalar o Site do Configuration Manager**, especifique se pretende remover a base de dados do site do servidor do site de administração central e se pretende remover a consola do Configuration Manager. Por predefinição, a Configuração remove ambos os itens.  

    > [!IMPORTANT]  
    >  Quando existe um site primário associado ao site de administração central, tem de desinstalar o site primário antes de poder desinstalar o site de administração central.  

6.  Selecione **Sim** para confirmar a desinstalação do site de administração central do Configuration Manager.  
