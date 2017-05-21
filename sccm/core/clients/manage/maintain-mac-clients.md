---
title: Manter os clientes Mac | Documentos do Microsoft
description: "Tarefas de manutenção para os clientes do Configuration Manager Mac."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
caps.latest.revision: 12
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 3bf6651f58dc0c2aa4773f77115c3fbcd4a33221
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="maintain-mac-clients"></a>Manter os clientes Mac
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguem-se os procedimentos para desinstalar os clientes Mac e para renovar os respetivos certificados.

##  <a name="uninstalling-the-mac-client"></a>A desinstalar o cliente de Mac  

1.  Num computador Mac, abra uma janela de terminal e navegue para a pasta que contém **macclient**.  

2.  Navegue para a pasta Ferramentas e introduza a seguinte linha de comandos:  

     **. / CMUninstall - c**  

    > [!NOTE]  
    >  O **- c** propriedade indica ao cliente de desinstalar para remover os registos de falhas do cliente também e ficheiros de registo. Fazemos esta para evitar confusões caso reinstale o cliente mais tarde.  

3.  Se necessário, manualmente remover o certificado de autenticação de cliente do Configuration Manager estava a utilizar, ou revogue-o. CMUnistall não remove nem revoga este certificado.  

##  <a name="renewing-the-mac-client-certificate"></a>Renovar o certificado do cliente Mac  
 Utilize um dos seguintes métodos para renovar o certificado do cliente Mac:  

-   [Renovar o Assistente de certificado](#renew-certificate-wizard)  

-   [Renovar o certificado manualmente](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Renovar o Assistente de certificado  

1.  Configure os seguintes valores como *cadeias* no ficheiro ccmclient plist que controla quando abre o Assistente para renovar o certificado:  

 -   **RenewalPeriod1** – Especifica, em segundos, o primeiro período de renovação em que os utilizadores podem renovar o certificado. O valor predefinido é de 3 888 000 segundos (45 dias). Não configure um valor inferior a 300, o período de irá reverter para a predefinição. 

 -   **RenewalPeriod2** – Especifica, em segundos, o segundo período de renovação em que os utilizadores podem renovar o certificado. O valor predefinido é de 259.200 segundos (3 dias). Se este valor está configurado e for maior que ou igual a 300 segundos e é menor ou igual a **RenewalPeriod1**, será utilizado o valor. Se o **RenewalPeriod1** for superior a 3 dias, será utilizado um valor de 3 dias para o **RenewalPeriod2**.  Se o **RenewalPeriod1** for inferior a 3 dias, o **RenewalPeriod2** é definido para o mesmo valor que o **RenewalPeriod1**.  

 -   **RenewalReminderInterval1** – Especifica, em segundos, a frequência com que o Assistente para renovar o certificado será apresentado aos utilizadores durante o primeiro período de renovação. O valor predefinido é de 86.400 segundos (1 dia). Se **RenewalReminderInterval1** for superior a 300 segundos e inferior ao valor configurado em **RenewalPeriod1**, será utilizado o valor configurado. Caso contrário, será utilizado o valor predefinido de 1 dia.  

 -   **RenewalReminderInterval2** – Especifica, em segundos da frequência com que o Assistente para renovar o certificado será apresentado aos utilizadores durante o segundo período de renovação. O valor predefinido é de 28.800 segundos (8 horas). Se o **RenewalReminderInterval2** for superior a 300 segundos, inferior ou igual ao **RenewalReminderInterval1** e inferior ou igual ao **RenewalPeriod2**, será utilizado o valor configurado. Caso contrário, será utilizado um valor de 8 horas.  

     **Exemplo:** Se os valores forem mantidos nas predefinições, 45 dias antes do certificado expirar, o assistente será aberto a cada 24 horas.  3 dias antes de o certificado expirar o assistente será aberto a cada 8 horas.  

     **Exemplo:** Utilize a seguinte linha de comandos, ou um script, para definir o primeiro período de renovação para 20 dias.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Quando abre o Assistente para renovar o certificado, o **nome de utilizador** e **nome do servidor** campos estarão normalmente pré-preenchidos e o utilizador apenas pode introduzir uma palavra-passe para renovar o certificado.  

    > [!NOTE]  
    >  Se o assistente não for aberto, ou se fechar inadvertidamente o assistente, clique em **Renovar** , na página de preferências do **Configuration Manager** para abrir o assistente.  

###  <a name="renew-certificate-manually"></a>Renovar o certificado manualmente  
 Um período de validade comum para um certificado de cliente Mac é de 1 ano. O Configuration Manager não renova automaticamente o certificado de utilizador que solicita durante a inscrição, pelo que deverá utilizar o seguinte procedimento para renovar o certificado manualmente.  

> [!IMPORTANT]  
>  Se o certificado expirar, terá de desinstalar, reinstalar e voltar a inscrever o cliente Mac.  

 Este procedimento remove o SMSID, necessário para pedir um novo certificado para o mesmo computador Mac. Quando remove e substitui o SMSID do cliente, o histórico armazenado do cliente, tais como o inventário é eliminado após a eliminação do cliente a partir da consola do Configuration Manager.  

1.  Crie e preencha uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de utilizador.  

    > [!WARNING]  
    >  O Configuration Manager monitoriza o período de validade do certificado que inscreve para computadores Mac. Deverá monitorizar esta forma independente do Configuration Manager para identificar os computadores Mac a adicionar a esta coleção.  

2.  Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo:Mac OS X**  

4.  No **plataformas suportadas** página, certifique-se de que todas as versões de Mac OS X estão selecionadas.  

5.  No **definições** página, selecione **novo** e, em seguida, no **Criar definição** diálogo caixa, especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo de definição:Script**  

    -   **Tipo de dados:Cadeia**  

6.  No **Criar definição** caixa de diálogo, para **script de deteção**, escolha **adicionar script** para especificar um script que Deteta os computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Deteção** , introduza o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolher **OK** para fechar o **Editar Script de deteção** caixa de diálogo.  

9. No **Criar definição** caixa de diálogo, para **script de remediação (opcional)**, escolha **adicionar script** para especificar um script que remove o SMSID quando localizado nos computadores Mac.  

10. Na caixa de diálogo **Criar Script de Remediação** , introduza o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolher **OK** para fechar o **criar Script de remediação** caixa de diálogo.  

12. Na página **Regras de Compatibilidade** do assistente, clique em **Novo**e, na caixa de diálogo **Criar Regra** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Definição selecionada:** Escolher **procurar** e, em seguida, selecione o script de deteção especificado anteriormente.  

    -   No campo **os seguintes valores** , introduza **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Ative a opção **Executar o script de remediação especificado quando esta definição é incompatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Criar uma linha de base de configuração que contém o item de configuração criado recentemente e implemente-a na coleção de dispositivos que criou no passo 1.  

     Para mais informações sobre como criar e implementar linhas de base de configuração, consulte o artigo [como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) e [como implementar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Em computadores Mac cujo SMSID tenha sido removido, execute o seguinte comando para instalar um novo certificado:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Quando solicitado, forneça a palavra-passe da conta de utilizador super para executar o comando e, em seguida, a palavra-passe da conta de utilizador do Active Directory.  

16. Para limitar o certificado inscrito ao Configuration Manager, no computador Mac, abra uma janela de terminal e efetue as seguintes alterações:  

    a.  Introduza o comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  No **acesso Keychain** caixa de diálogo, no **Keychains** secção, escolha **sistema**e, em seguida, no **categoria** secção, escolha **chaves**.  

    c.  Expanda as chaves para ver os certificados do cliente. Depois de identificar o certificado com uma chave privada acabada de instalar, faça duplo clique na chave.  

    d.  No **controlo de acesso** separador, escolha **confirmar antes de permitir acesso**.  

    e.  Navegue até à **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient**e, em seguida, escolha **adicionar**.  

    f.  Escolher **guardar alterações** e feche o **acesso Keychain** caixa de diálogo.  

17. Reinicie o computador Mac.  


