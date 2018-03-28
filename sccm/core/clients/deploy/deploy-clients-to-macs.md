---
title: Implementar os clientes Mac
titleSuffix: Configuration Manager
description: Saiba como implementar clientes em computadores Mac no System Center Configuration Manager.
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: ''
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 1b7f20a48e0e7219d933c367fb9f0315fc287dfd
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2018
---
# <a name="how-to-deploy-clients-to-macs"></a>Como implementar clientes em Mac

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico descreve como implementar e manter o cliente do Configuration Manager em computadores Mac. Para saber mais sobre o que tem de configurar antes de implementar clientes em computadores Mac, consulte [preparar para implementar o software de cliente para Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quando instala um novo cliente para computadores Mac, poderá ter também instala atualizações do Configuration Manager para refletir as novas informações de cliente na consola do Configuration Manager.

Estes procedimentos, tem duas opções para instalar os certificados de cliente. Saiba mais sobre certificados de cliente para Macs no [preparar para implementar o software de cliente para Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Utilize o Gestor de configuração de inscrição utilizando o [ferramenta CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de inscrição não suporta a renovação automática de certificados, pelo que terá de reinscrever os computadores Mac antes que o certificado instalado expire.    

-   [Utilize um método de pedido e instalação de certificado que seja independente do Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  Para implementar o cliente para dispositivos que executem macOS Sierra, o nome do requerente do certificado de ponto de gestão tem de ser configurado corretamente, por exemplo, utilizando o FQDN do servidor de ponto de gestão.


## <a name="configure-client-settings-for-enrollment"></a>Configurar as definições de cliente para inscrição  
 Tem de utilizar o [predefinições de cliente](../../../core/clients/deploy/about-client-settings.md) para configurar a inscrição para computadores Mac; não é possível utilizar definições de cliente personalizadas.  

 Isto é necessário para o Configuration Manager para pedir e instalar o certificado no Mac.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Para configurar as predefinições de cliente do Configuration Manager para inscrever certificados para Macs  

1.  Na consola do Configuration Manager, escolha **administração** >  **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  Selecione o **inscrição** secção e, em seguida, configure estas definições:  

    1.  **Permitir que os utilizadores a inscrição de dispositivos móveis e computadores de Mac: Sim**  

    2.  **Perfil de inscrição:** Escolha **definir perfil**.  

6.  No **perfil de inscrição de dispositivo móvel** diálogo caixa, escolha **criar**.  

7.  Na caixa de diálogo **Criar Perfil de Inscrição** , introduza um nome para este perfil de inscrição e, em seguida, configure o **Código do site de gestão**. Selecione o site primário do Configuration Manager que contém os pontos de gestão que irão gerir estes computadores Mac.  

    > [!NOTE]  
    >  Se não conseguir selecionar o site, certifique-se de que pelo menos um ponto de gestão do site está configurado para suportar dispositivos móveis.  

8.  Escolha **adicionar**.  

9. No **adicionar autoridade de certificação para dispositivos móveis** diálogo caixa, selecione o servidor de autoridade (AC) de certificação que irão emitir certificados para computadores Mac.  

10. No **criar perfil de inscrição** caixa de diálogo, selecione o modelo que criou no passo 3 de certificados do computador Mac.  

11. Clique em **OK** para fechar o **perfil de inscrição** caixa de diálogo e, em seguida, o **predefinições de cliente** caixa de diálogo.  

    > [!TIP]  
    >  Se pretender alterar o intervalo de política de cliente, utilize **intervalo de consulta da política de cliente** no **política de cliente** grupo de definições de cliente.  

 Todos os utilizadores serão configurados com estas definições da próxima vez que transferiram a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção da política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Além das definições de cliente de inscrição, certifique-se de que configurou as seguintes definições do dispositivo cliente:  

-   **Inventário de hardware**: Ativar e configurar esta opção se pretender recolher o inventário de hardware de computadores cliente Mac e Windows. Para obter mais informações, consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **As definições de compatibilidade**: Ativar e configurar esta opção se pretender avaliar e remediar definições em computadores cliente Mac e Windows. Para obter mais informações, consulte [planear e configurar as definições de compatibilidade](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Para obter mais informações sobre definições de cliente do Configuration Manager, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

## <a name="download-the-client-source-files-for-macs"></a>Transfira os ficheiros de origem do cliente para Macs  

1.  Transfira o pacote de ficheiros de cliente do Mac OS X, **ConfigmgrMacClient.msi**, e guarde-o num computador com o Windows.  

     Este ficheiro não é fornecido no suporte de instalação do Configuration Manager. Pode transferir este ficheiro a partir do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  No computador Windows, execute **ConfigmgrMacClient.msi** para extrair o pacote de cliente Mac, Macclient.dmg para uma pasta no disco local (por predefinição **C:\Program Files (x86) \Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copie o ficheiro Macclient.dmg para uma pasta no computador Mac.  

4.  No computador Mac, execute o ficheiro de Macclient.dmg para extrair os ficheiros para uma pasta no disco local.  

5.  Na pasta, certifique-se de que os ficheiros Ccmsetup e CMClient.pkg foram extraídos e de que foi criada uma pasta Ferramentas que contém as ferramentas CMDiagnostics, CMUninstall, CMAppUtil e CMEnroll.

    -  **Ccmsetup**: Instala o cliente do Configuration Manager nos seus computadores Mac.  

    -   **CMDiagnostics**: Recolhe informações de diagnóstico relacionadas com o cliente do Configuration Manager nos seus computadores Mac.  

    -   **CMUninstall**: Desinstalar o cliente de computadores Mac.  

    -   **CMAppUtil**: Converte pacotes da aplicações Apple num formato que pode ser implementado como uma aplicação do Configuration Manager.  

    -   **CMEnroll**: Pede e instala o certificado de cliente para um computador Mac, para que, em seguida, pode instalar o cliente de Configuration Manager.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Instalar o cliente e, em seguida, inscrever o certificado de cliente no Mac  

Pode inscrever clientes individuais com o [Assistente de inscrição de computador Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para automatização que ativa o registo de muitos clientes, utilize o [ferramenta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscrever o cliente com o Assistente de inscrição de computador Mac  

1.  Depois de concluída a instalação do cliente, é aberto o Assistente de inscrição de computador. Se o assistente não for aberto, ou se fechar inadvertidamente, clique em **inscrever** do **do Configuration Manager** página de preferências para abri-lo.  

2.  Na segunda página do assistente, fornece:  

    -   **Nome de utilizador** - O nome de utilizador pode ser especificado nos seguintes formatos:  

        -   'domínio \ nome'. Por exemplo: 'contoso\mnorth'  

        -   'user@domain'.   Por exemplo: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Quando utilizar um endereço de correio eletrónico para preencher o **nome de utilizador** campo, o Configuration Manager utiliza automaticamente o nome de domínio do endereço de correio eletrónico e o nome predefinido do servidor de ponto de proxy de inscrição para preencher o **nome do servidor** campo. Se este nome de domínio e o nome do servidor não corresponder ao nome do servidor de ponto de proxy de inscrição, dizer aos utilizadores o nome correto a utilizar quando inscrever os respetivos computadores Mac.  

         O nome de utilizador e a palavra-passe correspondente têm de corresponder a uma conta de utilizador do Active Directory que disponha de permissões de Leitura e Inscrição no modelo de certificado do cliente Mac.  

    -   **Palavra-passe** -introduza uma palavra-passe correspondente ao nome de utilizador especificado.  

    -   **Nome do servidor** -introduza o nome do servidor de ponto de proxy de inscrição.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Cliente e o certificado de automatização com CMEnroll  

Utilize este procedimento para inscrição de certificados de cliente com a ferramenta CMEnroll e automatização de instalação do cliente e a pedir. Para executar a ferramenta tem de ter uma conta de utilizador do Active Directory.

1.  No computador Mac, navegue para a pasta onde extraiu o conteúdo do ficheiro Macclient.dmg.  

2.  Introduza a seguinte linha de comandos: **sudo ./ccmsetup**  

3.  Aguarde até ver a mensagem **Instalação concluída** . Embora o instalador apresenta uma mensagem que tem de reiniciar agora, não reiniciar e continuar para o passo seguinte.  

4.  A partir da pasta Ferramentas no computador Mac, escreva o seguinte: **sudo. / CMEnroll -s &lt;nome_servidor_proxy_inscrição > - ignorecertchainvalidation -u &lt;nome de utilizador ' >**  

    Após a instalação do cliente, o Assistente para Inscrever um Computador Mac abre para ajudá-lo a inscrever o computador Mac. Para inscrever o cliente através deste método, consulte [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) neste tópico.  

5. Escreva a palavra-passe da conta de utilizador do Active Directory.  Ao introduzir este comando, são-lhe pedidas duas palavras-passe: O primeiro pedido é para a conta de utilizador super executar o comando. O segundo pedido refere-se à conta de utilizador do Active Directory. Os pedidos parecem idênticos, por isso certifique-se de que os especifica pela sequência correta.  

    O nome de utilizador pode ser especificado nos seguintes formatos:  

    -   'domínio \ nome'. Por exemplo: 'contoso\mnorth'  

    -   'user@domain'.   Por exemplo: 'mnorth@contoso.com'  

     O nome de utilizador e a palavra-passe correspondente têm de corresponder a uma conta de utilizador do Active Directory que disponha de permissões de Leitura e Inscrição no modelo de certificado do cliente Mac.  

     Exemplo: Se o servidor de ponto de proxy de inscrição é denominado **server02.contoso.com**e um nome de utilizador **contoso\mnorth** ter sido concedidas permissões para o modelo de certificado de cliente Mac, escreva o seguinte:  **sudo. / /cmenroll -s server02.contoso.com - ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Se o nome de utilizador contiver qualquer um dos carateres  **&lt;> "+ =,** inscrição irá falhar. Obtenha um certificado de fora de banda com um nome de utilizador que não contenha estes carateres.  
    >  
    >  Para assegurar uma experiência de utilizador mais estável, pode criar scripts dos passos e comandos de instalação para que os utilizadores apenas precisem de indicar o respetivo nome de utilizador e palavra-passe.  

5.  Aguarde até ver a mensagem **Inscrito com êxito** .  

6.  Para limitar o certificado inscrito para o Configuration Manager, no computador Mac, abra uma janela de terminal e efetue as seguintes alterações:  

    a.  Introduza o comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  No **acesso Keychain** caixa de diálogo a **Keychains** secção, escolha **sistema**e, em seguida, no **categoria** secção, escolha **chaves**.  

    c.  Expanda as chaves para ver os certificados do cliente. Depois de identificar o certificado com uma chave privada acabada de instalar, faça duplo clique na chave.  

    d.  No **controlo de acesso** separador, escolha **confirmar antes de permitir o acesso**.  

    e.  Navegue até à **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient**e, em seguida, escolha **adicionar**.  

    f.  Escolha **guardar alterações** e feche o **acesso Keychain** caixa de diálogo.  

7.  Reinicie o computador Mac.  

 Verifique se a instalação do cliente foi bem-sucedida abrindo o item **Configuration Manager** nas **Preferências do Sistema** do computador Mac. Pode também atualizar e ver a coleção **Todos os Sistemas** para confirmar se o computador Mac aparece nesta coleção como um cliente gerido.  

> [!TIP]  
>  Para ajudar a resolver problemas do cliente Mac, pode utilizar o programa CMDiagnostics incluído com o pacote de cliente de Mac OS X para recolher as informações de diagnóstico seguintes:  
>   
>  -   Uma lista dos processos em execução  
> -   A versão do sistema operativo Mac OS X  
> -   Falhas do Mac OS X relatórios relacionados com o cliente do Configuration Manager, incluindo **CCM\*.crash** e **System preference**.  
> -   O ficheiro de materiais (LM) e a propriedade lista (. plist) criados pela instalação de cliente do Configuration Manager.  
> -   O conteúdo da pasta /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  As informações recolhidas pelo CmDiagnostics são adicionadas a um ficheiro zip que é guardado no ambiente de trabalho do computador com o nome*< hostname\>***-***&gt;data e hora\>* . zip.* * *


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Utilize um método de pedido e instalação de certificado que seja independente do Configuration Manager  

Em primeiro lugar, efetuar estas tarefas específicas de [preparar para implementar o software de cliente para Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients):

1. [Implementar um certificado de servidor web nos servidores de sistema de sites](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Implementar um certificado de autenticação de cliente nos servidores de sistema de sites](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configurar o ponto de gestão e o ponto de distribuição](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Opcional: Instalar o ponto do reporting services](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Em seguida, efetue estas tarefas:

5. [Transfira os ficheiros de origem do cliente para Macs](#download-the-client-source-files-for-macs) .  
6. Utilize as instruções que acompanham o método de implementação do certificado escolhido para solicitar e instalar o certificado de cliente no computador Mac.  
7.  Navegue para a pasta onde extraiu o conteúdo do ficheiro macclient.dmg transferido do Centro de Transferências da Microsoft.  

3.  Introduza a seguinte linha de comandos: **sudo. / ccmsetup -MP < FQDN de Internet do ponto de gestão\> - SubjectName < valor do requerente do certificado\>**.  O valor do requerente do certificado é sensível às maiúsculas e minúsculas, devendo pois escrevê-lo tal como é apresentado nos detalhes do certificado.  

     Exemplo: Se o FQDN de Internet nas propriedades do sistema de sites for **server03.contoso.com** e o certificado de cliente Mac tiver o FQDN **mac12.contoso.com** como nome comum no requerente do certificado, escreva:  **sudo. / ccmsetup -MP server03.contoso.com - SubjectName mac12.contoso.com**  

4.  Aguarde até ver a mensagem **Instalação concluída** e reinicie o computador Mac.  

5.  Para se certificar de que este certificado é acessível ao Gestor de configuração, no computador Mac, abra uma janela de terminal e efetue estas alterações:  

    a.  Introduza o comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  No **acesso Keychain** caixa de diálogo a **Keychains** secção, escolha **sistema**e, em seguida, no **categoria** secção, escolha **chaves**.  

    c.  Expanda as chaves para ver os certificados do cliente. Depois de identificar o certificado com uma chave privada acabada de instalar, faça duplo clique na chave.  

    d.  No **controlo de acesso** separador, escolha **confirmar antes de permitir o acesso**.  

    e.  Navegue até à **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient**e, em seguida, escolha **adicionar**.  

    f.  Escolha **guardar alterações** e feche o **acesso Keychain** caixa de diálogo.  

6.  Se tiver mais de um certificado que contém o mesmo valor do requerente, tem de especificar o número de série do certificado para identificar o certificado que pretende utilizar para o cliente do Configuration Manager. Para tal, utilize o seguinte comando: **sudo defaults write com.microsoft.ccmclient SerialNumber-data "< número de série\>"**.  

     Por exemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Certifique-se de que a instalação de cliente foi bem-sucedida abrindo o **do Configuration Manager** item em **preferências do sistema** no Mac. Pode também atualizar e ver o **todos os sistemas** coleção para confirmar que o Mac aparece nesta coleção como um cliente gerido.  

## <a name="renewing-the-mac-client-certificate"></a>Renovar o certificado do cliente Mac  
 Utilize o procedimento seguinte antes de renovar o certificado de computador nos computadores Mac.  

 Este procedimento remove o SMSID, que é necessário para que o cliente possa utilizar um certificado novo ou renovado no computador Mac.  

> [!IMPORTANT]  
>  Quando remove e substitui o SMSID do cliente, o histórico armazenado do cliente, tais como o inventário é eliminado após a eliminação do cliente a partir da consola do Configuration Manager.  

### <a name="to-renew-the-mac-client-certificate"></a>Para renovar o certificado do cliente Mac  

1.  Criar e preencher uma coleção de dispositivos para os computadores Mac que têm de renovar os certificados de computador.  

2.  Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** do assistente, especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo:Mac OS X**  

4.  Na página **Plataformas Suportadas** do assistente, certifique-se de que estão selecionadas todas as versões do Mac OS X.  

5.  Na página **Definições** do assistente, clique em **Novo** e, na caixa de diálogo **Criar Definição** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo de definição:Script**  

    -   **Tipo de dados:Cadeia**  

6.  Na caixa de diálogo **Criar Definição** , em **Script de deteção**, clique em **Adicionar script** para especificar um script que deteta os computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Deteção** , introduza o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolha **OK** para fechar o **Editar Script de deteção** caixa de diálogo.  

9. No **Criar definição** caixa de diálogo, para **script de remediação (opcional)**, escolha **adicionar script** para especificar um script que remove o SMSID quando localizado nos computadores Mac.  

10. Na caixa de diálogo **Criar Script de Remediação** , introduza o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar o **criar Script de remediação** caixa de diálogo.  

12. No **regras de compatibilidade** página do assistente, selecione **novo**e, em seguida, no **criar regra** diálogo caixa, especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Definição selecionada:** Escolha **procurar** e, em seguida, selecione o script de deteção especificado anteriormente.  

    -   No campo **os seguintes valores** , introduza **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Ative a opção **Executar o script de remediação especificado quando esta definição é incompatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Crie uma linha de base de configuração que contenha o item de configuração criado recentemente e implemente-a na coleção de dispositivos criada no passo 1.  

     Para obter mais informações sobre como criar e implementar linhas de base de configuração, consulte [como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Após ter instalado um novo certificado nos computadores Mac cujo SMSID foi removido, execute o seguinte comando para configurar o cliente para utilizar o novo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Se tiver mais de um certificado que contém o mesmo valor do requerente, em seguida, tem de especificar o número de série do certificado para identificar o certificado que pretende utilizar para o cliente do Configuration Manager. Para tal, utilize o seguinte comando: **sudo defaults write com.microsoft.ccmclient SerialNumber-data "< número de série\>"**.  

     Por exemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Reinicie.  


## <a name="see-also"></a>Consulte também

[Manutenção de clientes de Mac](/sccm/core/clients/manage/maintain-mac-clients)
