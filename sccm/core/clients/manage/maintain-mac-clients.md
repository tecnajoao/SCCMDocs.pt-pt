---
title: Manutenção de clientes de Mac
titleSuffix: Configuration Manager
description: Tarefas de manutenção para os clientes do Configuration Manager Mac.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 337df4d64b6edda589344b52a100e5a90381676c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421200"
---
# <a name="maintain-mac-clients"></a>Manutenção de clientes de Mac
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguem-se procedimentos para desinstalar os clientes Mac e de renovação de seus certificados.

##  <a name="uninstalling-the-mac-client"></a>Desinstalar o cliente de Mac  

1.  Num computador Mac, abra uma janela de terminal e navegue para a pasta que contém **macclient**.  

2.  Navegue para a pasta Ferramentas e introduza a seguinte linha de comandos:  

     **. / CMUninstall - c**  

    > [!NOTE]  
    >  O **- c** propriedade indica ao cliente desinstalar também remover registos de falha do cliente e ficheiros de registo. Recomendamos esta opção para evitar confusão, se reinstalar o cliente mais tarde.  

3.  Se for necessário, manualmente remover o certificado de autenticação de cliente que estava a utilizar o Configuration Manager, ou revogue. CMUnistall não remove nem revoga este certificado.  

##  <a name="renewing-the-mac-client-certificate"></a>Renovar o certificado do cliente Mac  
 Utilize um dos seguintes métodos para renovar o certificado do cliente Mac:  

-   [Assistente de certificado de renovação](#renew-certificate-wizard)  

-   [Renovar manualmente o certificado](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Assistente de certificado de renovação  

1. Configure os seguintes valores como *cadeias de caracteres* no ficheiro ccmclient que controla quando é aberto o Assistente para renovar o certificado:  

   - **RenewalPeriod1** -Especifica, em segundos, o primeiro período de renovação na qual os utilizadores podem renovar o certificado. O valor predefinido é de 3 888 000 segundos (45 dias). Não configure um valor inferior a 300, como o período de irá reverter para a predefinição. 

   - **RenewalPeriod2** -Especifica, em segundos, o segundo período de renovação na qual os utilizadores podem renovar o certificado. O valor predefinido é de 259.200 segundos (3 dias). Se este valor estiver configurado e for igual ou superior a 300 segundos e inferior ou igual a **RenewalPeriod1**, será utilizado o valor. Se o **RenewalPeriod1** for superior a 3 dias, será utilizado um valor de 3 dias para o **RenewalPeriod2**.  Se o **RenewalPeriod1** for inferior a 3 dias, o **RenewalPeriod2** é definido para o mesmo valor que o **RenewalPeriod1**.  

   - **RenewalReminderInterval1** -Especifica, em segundos, a frequência com que o Assistente para renovar o certificado será apresentado aos utilizadores durante o primeiro período de renovação. O valor predefinido é de 86.400 segundos (1 dia). Se **RenewalReminderInterval1** for superior a 300 segundos e inferior ao valor configurado em **RenewalPeriod1**, será utilizado o valor configurado. Caso contrário, será utilizado o valor predefinido de 1 dia.  

   - **RenewalReminderInterval2** -Especifica, em segundos a frequência com que o Assistente para renovar o certificado será apresentado aos utilizadores durante o segundo período de renovação. O valor predefinido é de 28.800 segundos (8 horas). Se o **RenewalReminderInterval2** for superior a 300 segundos, inferior ou igual ao **RenewalReminderInterval1** e inferior ou igual ao **RenewalPeriod2**, será utilizado o valor configurado. Caso contrário, será utilizado um valor de 8 horas.  

     **Example:** Se os valores forem deixados com as predefinições, 45 dias antes do certificado expirar, o assistente será aberto a cada 24 horas.  3 dias antes de o certificado expirar o assistente será aberto a cada 8 horas.  

     **Example:** Utilize a seguinte linha de comando ou um script, para definir o primeiro período de renovação como 20 dias.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Quando abre o Assistente para renovar o certificado, o **nome de utilizador** e **nome do servidor** campos estarão normalmente pré-preenchidos e o utilizador pode introduzir uma palavra-passe para renovar o certificado.  

   > [!NOTE]  
   >  Se o assistente não for aberto, ou se fechar inadvertidamente o assistente, clique em **Renovar** , na página de preferências do **Configuration Manager** para abrir o assistente.  

###  <a name="renew-certificate-manually"></a>Renovar manualmente o certificado  
 Um período de validade comum para um certificado de cliente Mac é de 1 ano. O Configuration Manager não renova automaticamente o certificado de utilizador que pede durante a inscrição, pelo que deverá utilizar o procedimento seguinte para renovar o certificado manualmente.  

> [!IMPORTANT]  
>  Se o certificado expirar, terá de desinstalar, reinstalar e voltar a inscrever o cliente Mac.  

 Este procedimento remove o SMSID, necessário para pedir um novo certificado para o mesmo computador Mac. Quando remove e substitui o SMSID do cliente, o histórico armazenado do cliente, como o inventário é eliminado depois de eliminar o cliente da consola do Configuration Manager.  

1.  Criar e preencher uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de utilizador.  

    > [!WARNING]  
    >  O Configuration Manager não monitorizar o período de validade do certificado que inscreve para computadores Mac. Deverá monitorizar esta forma independente do Configuration Manager para identificar os computadores Mac a adicionar a esta coleção.  

2.  Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo:Mac OS X**  

4.  Sobre o **plataformas suportadas** página, certifique-se de que estão selecionadas todas as versões de Mac OS X.  

5.  Na **definições** página, selecione **New** e, em seguida, no **Criar definição** diálogo caixa, especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo de definição:Script**  

    -   **Tipo de dados:Cadeia**  

6.  Na **Criar definição** caixa de diálogo, para **script de deteção**, escolha **adicionar script** para especificar um script que Deteta os computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Deteção** , introduza o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolher **OK** para fechar a **Editar Script de deteção** caixa de diálogo.  

9. Na **Criar definição** caixa de diálogo, para **script de remediação (opcional)**, escolha **adicionar script** para especificar um script que remove o SMSID quando localizado nos computadores Mac.  

10. Na caixa de diálogo **Criar Script de Remediação** , introduza o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolher **OK** para fechar a **criar Script de remediação** caixa de diálogo.  

12. Na página **Regras de Compatibilidade** do assistente, clique em **Novo**e, na caixa de diálogo **Criar Regra** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Definição selecionada:** Escolher **procurar** e, em seguida, selecione o script de deteção especificado anteriormente.  

    -   No campo **os seguintes valores** , introduza **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Ative a opção **Executar o script de remediação especificado quando esta definição é incompatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Criar uma linha de base de configuração que contém o item de configuração que acabou de criar e implementá-la para a coleção de dispositivos que criou no passo 1.  

     Para obter mais informações sobre como criar e implementar linhas de base de configuração, consulte [como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) e [como implementar linhas de base de configuração no sistema Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Em computadores Mac cujo SMSID tenha sido removido, execute o seguinte comando para instalar um novo certificado:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Quando solicitado, forneça a palavra-passe da conta de utilizador super para executar o comando e, em seguida, a palavra-passe da conta de utilizador do Active Directory.  

16. Para limitar o certificado inscrito para o Configuration Manager, no computador Mac, abra uma janela de terminal e efetue as seguintes alterações:  

    a.  Introduza o comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Na **acesso Keychain** caixa de diálogo, na **Keychains** secção, escolha **sistema**e, em seguida, no **categoria** secção, escolha  **Chaves**.  

    c.  Expanda as chaves para ver os certificados do cliente. Depois de identificar o certificado com uma chave privada acabada de instalar, faça duplo clique na chave.  

    d.  Sobre o **controlo de acesso** separador, escolha **confirmar antes de permitir o acesso**.  

    e.  Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient**e, em seguida, escolha **Add**.  

    f.  Escolher **guardar alterações** e feche o **acesso Keychain** caixa de diálogo.  

17. Reinicie o computador Mac.  

