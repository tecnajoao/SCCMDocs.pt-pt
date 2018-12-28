---
title: Implementar clientes de Mac
titleSuffix: Configuration Manager
description: Saiba como implementar clientes em computadores Mac no Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba8182795759a29b4a5c8e4dfaa73f7c764dd7ff
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424889"
---
# <a name="how-to-deploy-clients-to-macs"></a>Como implementar clientes em Macs

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve como implementar e manter o cliente do Configuration Manager em computadores Mac. Para saber mais sobre o que tem de configurar antes de implementar clientes em computadores Mac, consulte [preparar a implementação de software de cliente para os Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quando instala um novo cliente para computadores Mac, terá de instalar também a atualizações do Configuration Manager para refletir as novas informações de cliente na consola do Configuration Manager.

Nestes procedimentos, tem duas opções para a instalação de certificados de cliente. Saiba mais sobre certificados de cliente para os Macs na [preparar a implementação de software de cliente para os Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

- Utilize o Gestor de configuração a inscrição através do [ferramenta CMEnroll](#bkmk_enroll). O processo de inscrição não suporta a renovação automática. Voltar a inscrever o computador Mac antes do certificado instalado expire.    

- [Utilizar um método de pedido e instalação de certificado independente do Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Para implementar o cliente em dispositivos com macOS Sierra, configurar corretamente o **nome do requerente** do certificado de ponto de gestão. Por exemplo, utilize o FQDN do servidor de ponto de gestão.



## <a name="configure-client-settings"></a>Configurar definições de cliente  

Utilize o [predefinições de cliente](/sccm/core/clients/deploy/about-client-settings) para configurar a inscrição para computadores Mac. Não é possível utilizar definições personalizadas de cliente. Para pedir e instalar o certificado, o cliente do Configuration Manager para Mac requer as predefinições de cliente.  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Selecione o **definições de cliente** nó e, em seguida, selecione **predefinições de cliente**.  

2. Na **home page** separador do Friso, no **propriedades** de grupo, escolha **propriedades**.  

3. Selecione o **inscrição** secção e, em seguida, configure as seguintes definições:  

    1. **Permitir que os utilizadores a inscrição de dispositivos móveis e computadores Mac**: **Sim**  

    2. **Perfil de inscrição:** Escolher **definir perfil**.  

4. Na **perfil de inscrição de dispositivo móvel** caixa de diálogo caixa, escolha **criar**.  

5. Na **criar perfil de inscrição** caixa de diálogo, introduza um nome para este perfil de inscrição. Em seguida, configure as **código do site de gestão**. Selecione o site primário do Configuration Manager que contém os pontos de gestão para estes computadores Mac.  

    > [!NOTE]  
    >  Se não é possível selecionar o site, certifique-se de que configurar, pelo menos, um ponto de gestão no site para suportar dispositivos móveis.  

6. Escolher **adicionar**.  

7. Na **adicionar autoridade de certificação para dispositivos móveis** janela, selecione o servidor de autoridade de certificação que emite certificados para computadores Mac.  

8. Na **criar perfil de inscrição** caixa de diálogo, selecione o modelo que criou anteriormente de certificados do computador Mac.  

9. Selecione **OK** para fechar a **perfil de inscrição** caixa de diálogo e, em seguida, o **predefinições de cliente** caixa de diálogo.  

    > [!TIP]  
    > Se quiser alterar o intervalo de política de cliente, utilize **intervalo de consulta da política de cliente** no **política de cliente** grupo de definições de cliente.  

Da próxima vez que os dispositivos transferem políticas de cliente, o Gestor de configuração aplica-se estas definições para todos os utilizadores. Para iniciar a obtenção da política para um único cliente, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

Além das definições de cliente de inscrição, certifique-se de que configurou as seguintes definições de dispositivo do cliente:  

- **Inventário de hardware**: Ativar e configurar esse recurso se pretender recolher o inventário de hardware de computadores cliente Mac e Windows. Para obter mais informações, consulte [como expandir o inventário de hardware](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

- **Definições de compatibilidade**: Ativar e configurar esse recurso se pretender avaliar e remediar definições em computadores cliente Mac e Windows. Para obter mais informações, consulte [planear e configurar as definições de compatibilidade](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

Para obter mais informações, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).  



## <a name="bkmk_download"></a> Transferir o cliente de Mac  

1. Transferir o pacote de ficheiros de cliente de Mac OS X do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Guarde **configmgrmacclient. msi** para um computador que executa o Windows. Este ficheiro não está no suporte de instalação do Configuration Manager.  

2. Execute o instalador no computador Windows. Extrair o pacote de cliente de Mac **macclient**, para uma pasta no disco local. O caminho predefinido é `C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client`.  

3. Copiar o **macclient** ficheiro para uma pasta no computador Mac.  

4. No computador Mac, execute **macclient** para extrair os ficheiros para uma pasta no disco local.  

5. Na pasta, certifique-se de que ele contém os seguintes ficheiros: 

    - **Ccmsetup**: Instala o cliente de Configuration Manager nos seus computadores de Mac utilizando **Cmclient**  

    - **CMDiagnostics**: Recolhe informações de diagnóstico relacionadas com o cliente do Configuration Manager nos computadores Mac  

    - **CMUninstall**: Desinstalar o cliente de seus computadores Mac  

    - **CMAppUtil**: Converte pacotes de aplicações Apple num formato que pode implementar como uma aplicação do Configuration Manager  

    - **CMEnroll**: Pede e instala o certificado de cliente para um computador Mac, para que, em seguida, pode instalar o cliente do Configuration Manager  



## <a name="bkmk_enroll"></a> Inscrever o cliente de Mac  

Inscrição de clientes individuais com o [Assistente de inscrição de computador Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para automatizar a inscrição para o número de clientes, utilize o [ferramenta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscrever o cliente com o Assistente de inscrição de computador Mac  

1. Depois de instalar o cliente, é aberto o Assistente de inscrição de computador. Para iniciar manualmente o assistente, selecione **inscrever** partir do **Configuration Manager** página de preferências.  

2. Na segunda página do assistente, forneça as seguintes informações:  

   - **Nome de utilizador**: O nome de utilizador pode ser especificado nos seguintes formatos:  

     - `domain\name`. Por exemplo: `contoso\mnorth`  

     - `user@domain`. Por exemplo: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Quando utiliza um endereço de correio eletrónico para preencher os **nome de utilizador** campo, o Configuration Manager povoa automaticamente a **nome do servidor** campo. Utiliza o nome predefinido do servidor de ponto de proxy de inscrição e o nome de domínio do endereço de e-mail. Se esses nomes não corresponder ao nome do servidor de ponto de proxy de inscrição, corrigir os **nome do servidor** durante a inscrição.  

       O nome de utilizador e palavra-passe correspondente tem de corresponder a uma conta de utilizador do Active Directory que tenha **leitura** e **inscrever** permissões no modelo de certificado de cliente Mac.  

   - **Nome do servidor**: O nome do servidor de ponto de proxy de registo.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Cliente e o certificado de automatização com CMEnroll  

Utilize este procedimento para automação de instalação do cliente e a pedir e inscrição de certificados de cliente com a ferramenta CMEnroll. Para executar a ferramenta, tem de ter uma conta de utilizador do Active Directory.

1. No computador Mac, navegue para a pasta onde extraiu o conteúdo do **macclient** ficheiro.  

2. Introduza o seguinte comando: `sudo ./ccmsetup`  

3. Aguarde até ver a mensagem **Instalação concluída** . Embora o instalador exiba uma mensagem a indicar que tem de reiniciar agora, não reinicie e continuar para o passo seguinte.  

4. Partir do **ferramentas** pasta no computador Mac, escreva o seguinte comando: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Após a instalação do cliente, o Assistente para Inscrever um Computador Mac abre para ajudá-lo a inscrever o computador Mac. Para obter mais informações, consulte [inscrever o cliente utilizando o Assistente de inscrição de computador Mac](#bkmk_enroll).  

     Exemplo: Se o servidor de ponto de proxy de registo com o nome **server02.contoso.com**, e concede **contoso\mnorth** permissões para o modelo de certificado de cliente Mac, escreva o seguinte comando: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Se o nome de utilizador inclui qualquer um dos seguintes carateres, a inscrição falha: `<>"+=,`. Utilize um certificado de fora de banda com um nome de utilizador que não inclua estes carateres.  
    >  
    > Para uma experiência de utilizador mais estável, o script os passos de instalação. Em seguida, os utilizadores só têm de fornecer o nome de utilizador e palavra-passe.  

5. Escreva a palavra-passe da conta de utilizador do Active Directory. Ao introduzir este comando, pede-lhe duas palavras-passe. É a primeira palavra-passe para a conta de utilizador super executar o comando. O segundo pedido refere-se à conta de utilizador do Active Directory. Os pedidos parecem idênticos, por isso certifique-se de que os especifica pela sequência correta.  

6. Aguarde até ver a mensagem **Inscrito com êxito** .  

7. Para limitar o certificado inscrito para o Configuration Manager, no computador Mac, abra uma janela de terminal e efetue as seguintes alterações:  

    1. Introduza o comando `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Na **acesso Keychain** janela, na **Keychains** secção, escolha **sistema**. Em seguida, no **categoria** secção, escolha **chaves**.  

    3. Expanda as chaves para ver os certificados do cliente. Localizar o certificado com uma chave privada que instalar e abrir a chave.  

    4. Sobre o **controlo de acesso** separador, escolha **confirmar antes de permitir o acesso**.  

    5. Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient**e, em seguida, escolha **Add**.  

    6. Escolher **guardar alterações** e feche o **acesso Keychain** caixa de diálogo.  

8. Reinicie o computador Mac.  

Para verificar que a instalação do cliente é efetuada com êxito, abra a **Configuration Manager** item no **preferências do sistema** no computador Mac. Também atualizar e ver os **todos os sistemas** coleção na consola do Configuration Manager. Confirme que o computador Mac aparece nesta coleção como um cliente gerenciado.  

> [!TIP]  
> Para ajudar a resolver problemas relacionados com o cliente Mac, utilize o **CMDiagnostics** ferramenta incluída com o pacote de cliente Mac. Utilize-o para recolher as informações de diagnóstico seguintes:  
>   
> - Uma lista dos processos em execução  
> - A versão do sistema operativo Mac OS X  
> - Relatórios relacionados ao cliente do Configuration Manager, incluindo de falhas do Mac OS X **CCM\*.crash** e **System preference**.  
> - O ficheiro de fatura de materiais (LM) e a propriedade listam o ficheiro (. plist) criado pela instalação de cliente do Configuration Manager.  
> - O conteúdo da pasta **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> As informações recolhidas pelo CmDiagnostics são adicionadas a um ficheiro zip que é guardado na área de trabalho do computador e o nome `cmdiag-<hostname>-<datetime>.zip`



## <a name="bkmk_external"></a> Gerir certificados externos ao Configuration Manager

Pode usar um pedido e instalação do método de certificado independente do Configuration Manager. Utilizar o mesmo processo geral, mas incluem os seguintes passos adicionais: 

- Quando instala o cliente do Configuration Manager, utilize o **MP** e **SubjectName** opções da linha de comandos. Introduza o seguinte comando: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. O nome de requerente do certificado diferencia maiúsculas de minúsculas, devendo pois escrevê-lo tal como é apresentado nos detalhes do certificado.  

     Exemplo: FQDN de internet do ponto de gestão for **server03.contoso.com**. O certificado de cliente Mac tiver o FQDN **mac12.contoso.com** como nome comum no requerente do certificado. Utilize o seguinte comando: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Se tiver mais de um certificado que contém o mesmo valor do requerente, especifique o número de série do certificado a utilizar para o cliente do Configuration Manager. Utilize o seguinte comando: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Por exemplo: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Renovar o certificado de cliente de Mac  

Este procedimento remove o SMSID. O cliente do Configuration Manager para Mac requer um ID novo utilizar um certificado novo ou renovado.  

> [!IMPORTANT]  
> Depois de substituir o SMSID, do cliente ao eliminar o recurso antigo na consola do Configuration Manager, também eliminar histórico armazenado do cliente. Por exemplo, hardware histórico de inventário para esse cliente.  


1. Criar e preencher uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de computador.  

2. Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3. Na página **Geral** do assistente, especifique as seguintes informações:  

    - **Nome**: **Remova o SMSID para Mac**  

    - **Tipo de**: **Mac OS X**  

4. Sobre o **plataformas suportadas** , selecione todas as versões de Mac OS X.  

5. Sobre o **configurações** página, selecione **New**. Na **Criar definição** janela, especifique as seguintes informações:  

    - **Nome**: **Remova o SMSID para Mac**  

    - **Tipo de definição**: **Script**  

    - **Tipo de dados**: **Cadeia de caracteres**  

6. Na **Criar definição** janela, para **script de deteção**, selecione **adicionar script**. Esta ação Especifica um script para detetar computadores de Mac configurados com um SMSID.  

7. Na **Editar Script de deteção** janela, introduza o seguinte script de shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Escolher **OK** para fechar a **Editar Script de deteção** janela.  

9. Na **Criar definição** janela, para **script de remediação (opcional)**, escolha **adicionar script**. Esta ação Especifica um script para remover o SMSID quando localizado nos computadores Mac.  

10. Na **criar Script de remediação** janela, introduza o seguinte script de shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolher **OK** para fechar a **criar Script de remediação** janela.  

12. Sobre o **regras de conformidade** página, selecione **New**. Em seguida, no **criar regra** janela, especifique as seguintes informações:  

    - **Nome**: **Remova o SMSID para Mac**  

    - **Definição selecionada**: Escolher **procurar** e, em seguida, selecione o script de deteção especificado anteriormente.  

    - Na **os seguintes valores** campo: **O par domínio/predefinido de (com.microsoft.ccmclient, SMSID) não existe**.  

    - Ativar a opção para **executar o script de remediação especificado quando esta definição é incompatível**.  

13. Conclua o assistente.  

14. Crie uma linha de base de configuração que contém este item de configuração. Implemente a linha de base para a coleção de destino.  

     Para obter mais informações, consulte [como criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).  

15. Depois de instalar um novo certificado em computadores Mac cujo smsid foi removido, execute o seguinte comando para configurar o cliente para utilizar o novo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Consulte também

[Preparar a implementação de clientes em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)

[Manutenção de clientes de Mac](/sccm/core/clients/manage/maintain-mac-clients)
