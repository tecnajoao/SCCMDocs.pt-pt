---
title: Desinstalar os sites | Documentos do Microsoft
description: "Utilize estas informações como guia para desinstalar um site do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: b4c4fc305adbb4acd5bb4941b856a6a4aa648d0f
ms.openlocfilehash: 6ad06753dc0e1d0958f7131afbf3ecb75eecb2e3
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Desinstalar sites e hierarquias no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes informações como guia se precisar de desinstalar um site do System Center Configuration Manager.  

Para encerrar uma hierarquia com vários sites, é importante a sequência de remoção. Comece por desinstalar os sites na parte inferior da hierarquia e, em seguida, mover para cima:  

1.  Remova sites secundários ligados a sites primários.  
2.  Remova sites primários.
3.  Depois de todos os sites primários serem removidos, pode desinstalar o site de administrações centrais.  


##  <a name="BKMK_RemoveSecondarysite"></a> Remover um site secundário de uma hierarquia  
Não é possível mover um site secundário ou reatribuir um site secundário para um novo site primário principal. Para ser removido de uma hierarquia, um site secundário tem de ser eliminado do respetivo site principal direto. Utilize o assistente eliminar de Site a secundário a partir da consola do Configuration Manager para remover um site secundário. Quando remover um site secundário, tem de escolher se pretende eliminá-la ou desinstalá-lo:  

-   **Desinstalar o site secundário**. Utilize esta opção para remover um site secundário funcional acessível a partir da rede. Esta opção desinstala o Configuration Manager a partir do servidor do site secundário e, em seguida, elimina todas as informações sobre o site e os respetivos recursos da hierarquia de sites do Configuration Manager. Se o Configuration Manager instalado o SQL Server Express como parte da instalação do site secundário, do Configuration Manager desinstalará o SQL Server Express quando desinstalar o site secundário. Se o SQL Server Express tiver sido instalado antes de instalar o site secundário, o Configuration Manager não desinstalará o SQL Server Express.  

-   **Eliminar o site secundário**. Utilize esta opção se uma das seguintes opções for verdadeira:  

    -   Não foi possível instalar um site secundário  
    -   O site secundário continua a ser apresentada na consola do Configuration Manager após a desinstalação

    Esta opção elimina todas as informações sobre o site e os respetivos recursos da hierarquia do Configuration Manager, mas deixa o Configuration Manager instalado no servidor do site secundário.  

    > [!NOTE]  
    >  Também pode utilizar a ferramenta manutenção da hierarquia e a **/DELSITE** opção para eliminar um site secundário. Para obter mais informações, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Para desinstalar ou eliminar um site secundário  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos administrativos no computador do site secundário  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site primário, se for remoto  
    -   Função de segurança de administrador de infraestrutura ou de administrador global no site primário principal  
    -   Direitos sysadmin na base de dados do site secundário  

2.  Na consola do Configuration Manager, selecione **administração**.  
3.  No **administração** área de trabalho, expanda **configuração do Site**e, em seguida, selecione **Sites**.  
4.  Selecione o servidor de site secundário que pretende remover.  
5.  No **base** separador o **Site** grupo, selecione **eliminar**.  
6.  Na página **Geral** , selecione se pretende desinstalar ou eliminar o site secundário e clique em **Seguinte**.  
7.  No **resumo** página, verifique as definições e, em seguida, selecione **seguinte**.  
8.  No **conclusão** página, selecione **fechar** para sair do assistente.  

##  <a name="BKMK_UninstallPrimary"></a> Desinstalar um site primário  
Pode executar a configuração do Configuration Manager para desinstalar um site primário que não tenha um site secundário associado. Antes de desinstalar um site primário, considere o seguinte:  

-   Quando os clientes do Configuration Manager estão dentro dos limites configurados no site e o site primário é parte de uma hierarquia do Configuration Manager, considere adicionar os limites a outro site primário da hierarquia antes de desinstalar o site primário.  
-   Quando o servidor do site primário deixa de estar disponível, tem de utilizar a Ferramenta de Manutenção da Hierarquia no site de administração central para eliminar o site primário da base de dados do site. Para obter mais informações, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Utilize o procedimento seguinte para desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site"></a>Para desinstalar um site primário  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos de administrador local no servidor do site de administração central  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site de administração central, se for remoto
    -   Direitos sysadmin na base de dados do site de administração central  
    -   Direitos de administrador local no computador do site primário  
    -   Direitos de administrador local no servidor de base de dados do site remoto para o site primário, se for remoto  
    -   Um nome de utilizador associado com a função de segurança de administrador de infraestrutura ou de administrador global no site de administração central  

2.  Inicie a configuração do Configuration Manager no servidor do site primário utilizando um dos seguintes métodos:  

    -   No **iniciar**, selecione **configuração do Configuration Manager**.  
    -   Abrir Setup.exe de &lt; *ConfigMgrInstallationMedia*> \smssetup\bin\x64.  
    -   Abrir Setup.exe de &lt; *ConfigMgrInstallationPath*> \bin\x64.  

3.  No **antes de começar** página, selecione **seguinte**.  
4.  No **introdução** página, selecione **desinstalar um site do Configuration Manager**e, em seguida, selecione **seguinte**.  
5.  No **desinstalar o Site do Configuration Manager**, especifique se pretende remover a base de dados do site a partir do servidor do site primário e se pretende remover a consola do Configuration Manager. Por predefinição, a Configuração remove ambos os itens.  

    > [!IMPORTANT]  
    >  Quando um site secundário está associado ao site primário, tem de remover o site secundário antes de poder desinstalar o site primário.  

6.  Selecione **Sim** para confirmar a desinstalação do site primário do Configuration Manager.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Desinstalar um site primário configurado com vistas distribuídas  
 Antes de desinstalar um site primário subordinado que tenha sido distribuído vistas ativadas para a respetiva ligação de replicação para o site de administração central, tem de desativar as vistas distribuídas na sua hierarquia. Utilize as seguintes informações para desativar as vistas distribuídas antes de desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Para desinstalar um site primário configurado com vistas distribuídas  

1.  Antes de desinstalar qualquer site primário, tem de desativar as vistas distribuídas de cada ligação da hierarquia entre o site de administração central e um site primário.  
2.  Depois de desativar as vistas distribuídas de cada ligação, confirme que os dados do site primário é concluída reinicialização no site de administração central. Para monitorizar a inicialização dos dados, na consola do Configuration Manager, no **monitorização** área de trabalho, ver a ligação no **replicação de base de dados** nó.  
3.  Após a reinicialização bem-sucedida dos dados com o site de administração central, pode desinstalar o site primário. Para desinstalar um site primário, consulte o artigo [desinstalar um site primário](#BKMK_UninstallPrimary).  
4.  Quando o site primário está completamente desinstalado, pode reconfigurar as vistas distribuídas em ligações aos sites primários.  

    > [!IMPORTANT]  
    >  Se desinstalar o site primário antes de desativar as vistas distribuídas em cada site ou antes dos dados do site primário reinicializa com êxito no site de administração central, a replicação dos dados entre sites primários e o site de administração central pode falhar. Neste cenário, tem de desativar as vistas distribuídas de cada ligação na sua hierarquia do site e, em seguida, após os reinicialização bem-sucedida dos dados com o site de administração central, pode reconfigurar as vistas distribuídas.  

##  <a name="BKMK_UninstallCAS"></a> Desinstalar o site de administração central  
 Pode executar a configuração do Configuration Manager para desinstalar um site de administração central que não tenha sites primários subordinados. Utilize o procedimento seguinte para desinstalar o site de administração central.  

#### <a name="to-uninstall-a-central-administration-site"></a>Para desinstalar um site de administração central  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração detém os seguintes direitos de segurança:  

    -   Direitos de administrador local no servidor do site de administração central  
    -   Direitos de administrador local no servidor de base de dados do site para o site de administração central, se o servidor de base de dados do site não estiver instalado no servidor do site 

2.  Inicie a configuração do Configuration Manager no servidor do site de administração central, utilizando um dos seguintes métodos:  

    -   Em **Iniciar**, clique em **Configuração do Configuration Manager**.  
    -   Abrir Setup.exe de &lt; *ConfigMgrInstallationMedia*> \smssetup\bin\x64.  
    -   Abrir Setup.exe de &lt; *ConfigMgrInstallationPath*> \bin\x64.  

3.  No **antes de começar** página, selecione **seguinte**.  
4.  No **introdução** página, selecione **desinstalar um site do Configuration Manager**e, em seguida, selecione **seguinte**.  
5.  No **desinstalar o Site do Configuration Manager**, especifique se pretende remover a base de dados do site do servidor do site de administração central e se pretende remover a consola do Configuration Manager. Por predefinição, a Configuração remove ambos os itens.  

    > [!IMPORTANT]  
    >  Quando existe um site primário associado ao site de administração central, tem de desinstalar o site primário antes de poder desinstalar o site de administração central.  

6.  Selecione **Sim** para confirmar a desinstalação do site de administração central do Configuration Manager.  

