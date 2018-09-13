---
title: Ativar as atualizações de terceiros
titleSuffix: Configuration Manager
description: Ativar as atualizações de terceiros no Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbcf7a7d76146cc11dd4bb57b86fe4752c694e02
ms.sourcegitcommit: 1e782268d6c0211bd854b5860de72cfd6c6985c6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/12/2018
ms.locfileid: "44697043"
---
# <a name="enable-third-party-updates"></a>Ativar as atualizações de terceiros 

*Aplica-se a: Versão 1806 do System Center Configuration Manager*

Versão 1806, a partir da **catálogos de atualização de Software de terceiros** nó na consola do Configuration Manager permite-lhe subscrever catálogos de terceiros, publicar suas atualizações para o seu ponto de atualização de software (SUP) e, em seguida, implementá-las para os clientes.  <!--1357605, 1352101, 1358714-->



## <a name="prerequisites"></a>Pré-requisitos 
- Espaço em disco suficiente sobre o software de nível superior atualizar pasta WSUSContent de um ponto para armazenar o conteúdo do binário de origem para atualizações de software de terceiros.
    - A quantidade de armazenamento necessário varia consoante o fornecedor, os tipos de atualizações e atualizações específicas que publicar para a implementação.
    - Se precisar de mover a pasta WSUSContent para outra unidade com mais espaço livre, consulte a [como alterar a localização onde o WSUS armazena as atualizações localmente](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) postagem de blog.
- O serviço de sincronização de atualização de software de terceiros requer acesso à internet.
    - Para obter a lista de catálogos de parceiros, é necessário download.microsoft.com através da porta HTTPS 443. 
    -  Acesso à Internet para todos os catálogos de terceiros e os ficheiros de conteúdo de atualização. Talvez seja necessário portas adicionais sem ser a 443.
    - Atualizações de terceiros utilizam as mesmas definições de proxy como o SUP.

## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Requisitos adicionais quando o SUP é remoto do servidor do site de nível superior 

1. SSL tem de estar ativado no SUP quando for remoto. Isto requer um certificado de autenticação de servidor gerado a partir de uma autoridade de certififcate interno ou através de um fornecedor público.
    - [Configurar o SSL no WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
        - Quando configurar o SSL no WSUS, tenha em atenção a alguns dos serviços web e os diretórios virtuais são sempre HTTP e HTTPS não. 
        - O Configuration Manager transfere o conteúdo de terceiros para pacotes de atualização de software do seu diretório de conteúdo do WSUS através de HTTP.   
    - [Configurar SSL no SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Quando a definição de terceiros atualizações WSUS para configuração do certificado de assinatura **Gestor de configuração gere as atualizações** nas propriedades componente de ponto de atualização de Software, as seguintes configurações são necessárias para permitir que o criação do certificado de assinatura autoassinado do WSUS: 
   - Registo remoto deve estar ativado no servidor do SUP.
   -  O **conta de ligação do servidor WSUS** deve ter permissões de registo remoto no servidor SUP/WSUS. 


3. Crie a seguinte chave de registo no servidor do site do Configuration Manager: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, criar uma nova DWORD denominada **EnableSelfSignedCertificates** com um valor de `1`. 

4. Para ativar a instalar o certificado de assinatura autoassinado do WSUS para os editores confiáveis e de raiz fidedigna armazena no servidor SUP remoto:
   - O **conta de ligação do servidor WSUS** deve possuir permissões de administração remota do servidor SUP.

    Se este item não for possível, exporte o certificado do arquivo WSUS no computador local para os arquivos de fabricante fidedigno e de raiz fidedigna. 

> [!NOTE] 
>O **conta de ligação do servidor WSUS** podem ser identificados, visualizando o **definições de conta de Proxy e** separador nas propriedades da função de sistema de sites do SUP. Se não for especificada uma conta, é utilizada a conta de computador do servidor do site.

## <a name="enable-third-party-updates-on-the-sup"></a>Ativar atualizações de terceiros no SUP
Se ativar esta opção, pode subscrever catálogos de atualizações de terceiros na consola do Configuration Manager. Em seguida, pode publicar as atualizações no WSUS e implementá-las para os clientes. Os seguintes passos devem ser executados uma vez por hierarquia para ativar e configurar a funcionalidade para utilização. Os passos poderão ter de ser novamente executada se alguma vez de substituir o servidor WSUS o SUP de nível superior. 

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nó.
2. Selecione o site de nível superior na hierarquia. No Friso, clique em **configurar componentes do Site**e selecione **ponto de atualização de Software**.
3. Mude para o **atualizações de terceiros** separador. Selecione a opção **ativar atualizações de software de terceiros**.

    ![Captura de ecrã de propriedades SUP de atualizações de terceiros](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configurar o certificado de assinatura de WSUS
Precisará decidir se pretende que o Configuration Manager para gerir automaticamente o certificado de terceiros de assinatura WSUS a utilizar um certificado autoassinado ou se precisar de configurar manualmente o certificado. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Gerir automaticamente o certificado de assinatura de WSUS
Se não tiver um requisito para utilizar certificados PKI, pode optar por gerir automaticamente os certificados de assinatura para atualizações de terceiros. A gestão de certificados do WSUS é feito como parte do ciclo de sincronização e obtém conectado a `wsyncmgr.log`. 

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nó.
2. Selecione o site de nível superior na hierarquia. No Friso, clique em **configurar componentes do Site**e selecione **ponto de atualização de Software**.
3. Mude para o **atualizações de terceiros** separador. Selecione a opção **Configuration Manager gerencia o certificado**. 
4. Um novo certificado do tipo **de terceiros de assinatura de WSUS** é criado na **certificados** no nó **segurança** no **administração**área de trabalho.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Gerir manualmente o certificado de assinatura de WSUS
Se precisar de configurar manualmente o certificado, como a necessidade de utilizar um certificado PKI, terá de utilizar um [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) ou outra ferramenta para fazer isso.  

1. Configurar o certificado com assinatura [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nó.
3. Selecione o site de nível superior na hierarquia. No Friso, clique em **configurar componentes do Site**e selecione **ponto de atualização de Software**.
4. Mude para o **atualizações de terceiros** separador. Selecione a opção para **gerir manualmente o certificado**.


## <a name="enable-third-party-updates-on-the-clients"></a>Ativar as atualizações de terceiros nos clientes
Ative atualizações de terceiros nos clientes nas definições do cliente. A definição define a política de agente de atualização do Windows para [permitir assinado atualizações para uma localização do serviço do Microsoft update de intranet](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#BKMK_comp3). Esta definição também de cliente instala a assinatura de certificado para o arquivo do Editor confiável no cliente do WSUS. O registo de gestão de certificados é visto em `updatesdeployment.log` nos clientes.  Execute estes passos para cada definição de cliente personalizado que pretende utilizar para atualizações de terceiros. Para obter mais informações, consulte a [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates) artigo.

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **definições de cliente** nó.
2. Selecione um existente definição de cliente personalizada ou crie um novo. 
3. Selecione o **atualizações de Software** separador no lado esquerdo. Se não tiver este separador, certifique-se de que o **atualizações de Software** caixa está ativada.
4. Definir **ativar atualizações de software de terceiros** ao **Sim**. 


## <a name="add-a-custom-catalog"></a>Adicionar um catálogo personalizado
*Catálogos de parceiros* são catálogos de fornecedor de software que têm as suas informações já está registadas com a Microsoft. Com catálogos de parceiros, pode subscrevê-los sem ter de especificar quaisquer informações adicionais. São chamados de catálogos de que adiciona *catálogos personalizados*. Pode adicionar um catálogo personalizado de um fornecedor de atualização de terceiros para o Configuration Manager. Catálogos personalizados têm de utilizar https e as atualizações devem ser assinadas digitalmente. 

1. Vá para o **biblioteca de atualizações de Software** área de trabalho, expanda **atualizações de Software**e selecione o **catálogos de atualizações de Software de terceiros** nó. 
   
     ![Captura de ecrã de nó de atualizações de terceiros](media/third-party-updates-node.PNG)
2. Clique em **catálogo de personalizado adicionar** na faixa de opções. 

     ![Atualizações de terceiros Adicionar catálogo personalizado](media/third-party-updates-custom-catalog.png)
1. Sobre o **gerais** , especifique os seguintes itens: 
    - **URL de transferência**: Um endereço HTTPS válido do catálogo personalizado.
    - **Publicador**: O nome da organização que publica o catálogo. 
    - **Nome**: O nome do catálogo, para apresentar na consola do Configuration Manager. 
    - **Descrição**: Uma descrição do catálogo. 
    - **URL de suporte** (opcional): Um endereço HTTPS válido de um Web site para obter ajuda com o catálogo. 
    - **Contacto de suporte** (opcional): Informações de contacto para obter ajuda com o catálogo. 
2. Clique em **próxima** para rever o catálogo de resumo e para continuar com a conclusão da **Assistente de catálogo de personalizada de atualizações de Software de terceiros**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Subscrever um catálogo de terceiros e sincronização de atualizações
Ao subscrever um catálogo de terceiros na consola do Configuration Manager, os metadados para todas as atualizações no catálogo são sincronizados para os servidores WSUS para sua SUPs. A sincronização dos metadados permite que os clientes determinar se alguma das atualizações são aplicáveis. Execute os seguintes passos para cada catálogo de terceiros para que quisesse se inscrever:  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **catálogos de atualizações de Software de terceiros** nó.  
2. Selecione o catálogo para subscrever e clique em **subscrever catálogo** na faixa de opções. 
    ![Atualizações de terceiros Adicionar catálogo personalizado](media/third-party-updates-subscribe.png)
1. Rever e aprovar o certificado de catálogo.  
    >[!NOTE]
    
    > Ao subscrever um catálogo de atualização de software de terceiros, o certificado que rever e aprovar no assistente é adicionado ao site. Este certificado é do tipo **catálogo de atualizações de Software de terceiros**. Pode gerenciá-lo a partir do **certificados** no nó **segurança** no **administração** área de trabalho.  
2. Conclua o assistente. Depois da subscrição inicial, o catálogo deve começar a transferir dentro de alguns minutos. 
    - O catálogo sincroniza automaticamente a cada 7 dias.
    - Clique em **sincronizar agora** na faixa de opções para forçar a sincronização.
3. Depois do catálogo é transferido, os metadados do produto tem de ser sincronizados a partir da base de dados do WSUS no banco de dados do Configuration Manager. [Iniciar manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar as informações do produto.
4. Assim que as informações do produto estão sincronizadas, [configurar o SUP para sincronizar o produto desejado](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) para o Configuration Manager.  
5. [Iniciar manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar atualizações do produto novo para o Configuration Manager.  
6. Quando a sincronização estiver concluída, pode ver as atualizações de terceiros a **todas as atualizações** nó. Estas atualizações são publicadas como **apenas de metadados** atualiza até optar por publicá-los. 
     - O ícone com a seta azul representa uma atualização de software apenas de metadados. ![Ícone de atualização de software apenas de metadados](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publicar e implementar atualizações de software de terceiros 
Assim que as atualizações de terceiros estão no **todas as atualizações** nó, pode escolher quais atualizações devem ser publicadas para a implementação. Quando publica uma atualização, os ficheiros binários são transferidos do fornecedor e colocados no diretório de WSUSContent no SUP de nível superior. 

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione o **todas as atualizações de Software** nó.
2. Clique em **adicionar critérios** para filtrar a lista de atualizações. Por exemplo, adicione **fornecedor** para **HP**. Para ver todas as atualizações da HP.  
3. Selecione as atualizações que são necessários para sua organização. Clique em **publicar conteúdo de atualização de Software de terceiros**.
    - Esta ação transfere os binários de atualização do fornecedor, em seguida, armazena-os na pasta WSUSContent no ponto de atualização de software de nível superior. 
4. [Iniciar manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para alterar o estado das atualizações publicadas de apenas de metadados para atualizações implementáveis com conteúdo. 
    >[!NOTE]
    >Quando publica conteúdos de atualização de software de terceiros, são adicionados todos os certificados utilizados para assinar o conteúdo para o site. Estes certificados são do tipo **atualizações de Software de terceiros conteúdo**. Pode geri-los a partir do **certificados** no nó **segurança** no **administração** área de trabalho.  

5. Reveja o progresso no SMS_ISVUPDATES_SYNCAGENT.log. O registo está localizado no ponto de atualização de software de nível superior na pasta de Logs do sistema de site.
6. Implementar as atualizações com o [implementar atualizações de software](../deploy-use/deploy-software-updates.md) processo. 
7. Na **transferir localizações** página do **implementar Assistente de atualização de Software**, selecione a opção padrão para **transferir atualizações de software a partir da internet**. Neste cenário, o conteúdo já está publicado para o ponto de atualização de software, o que é utilizado para transferir o conteúdo para o pacote de implementação.
8. Os clientes terão executar uma análise e avaliar as atualizações para visualizar os resultados de compatibilidade.  Já pode acionar manualmente este ciclo do painel de controlo do Configuration Manager num cliente ao executar o **atualizações de Software de análise ciclo** ação.


## <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorizar o progresso das atualizações de software de terceiros 

Sincronização de atualizações de software de terceiros é processada pelo componente SMS_ISVUPDATES_SYNCAGENT no ponto de atualização de software padrão de nível superior. Pode ver mensagens de estado este componente, ou ver mais detalhadas de estado no SMS_ISVUPDATES_SYNCAGENT.log. Este registo é no ponto de atualização de software de nível superior na pasta de Logs do sistema de site. Por predefinição este caminho é C:\Program Files\Microsoft Configuration Manager\Logs. Para obter mais informações sobre como monitorizar o processo de gestão de atualizações de software geral, consulte [monitorizar atualizações de software](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Problemas conhecidos

- A máquina em que está a executar a consola é utilizada para transferir as atualizações do WSUS e adicioná-lo para o pacote de atualizações. O certificado de assinatura do WSUS tem de ser fidedigno na máquina de consola. Caso contrário, poderá ver problemas com a verificação de assinatura durante a transferência de atualizações de terceiros. 
- O serviço de sincronização de atualização de software de terceiros não é possível publicar conteúdo para atualizações apenas de metadados que foram adicionadas ao WSUS por outro aplicativo, ferramenta ou script, como SCUP. O **publicar conteúdo de atualização de software de terceiros** ação falhar nestas atualizações. Se precisar de implementar as atualizações de terceiros que ainda não suporta esta funcionalidade, utilize o seu processo existente na totalidade para implementar essas atualizações.  
-  O Configuration Manager possui uma nova versão para o formato de ficheiro cab do catálogo. A nova versão inclui os certificados para os ficheiros binários do fornecedor. Estes certificados são adicionados para o **certificados** no nó **segurança** no **administração** área de trabalho depois de aprovar e o catálogo de confiança.  
     - Ainda pode usar a versão mais antiga do ficheiro de cab do catálogo, desde que o URL de transferência é https e as atualizações são assinadas. O conteúdo não conseguirá publicar porque os certificados para os binários não estão no ficheiro cab e já aprovado. Pode contornar este problema ao detetar o certificado no **certificados** nó, desbloquear, em seguida, publicá-la novamente. Se está publicando várias atualizações assinadas com certificados diferentes, terá de desbloquear cada certificado que é utilizado.
     - Para obter mais informações, consulte as mensagens de estado 11523 e 11524 na abaixo da tabela de mensagens de estado.
-  Quando o serviço de sincronização de atualização de software de terceiros sobre a atualização de software de nível superior ponto requer um servidor proxy para acesso à internet, verificações de assinatura digital podem falhar. Para atenuar este problema, configure as definições de proxy do WinHTTP no sistema de sites. Para obter mais informações, consulte [comandos Netsh para WinHTTP](https://go.microsoft.com/fwlink/p/?linkid=199086).

## <a name="status-messages"></a>Mensagens de estado

| MessageID       | Gravidade           | Descrição | Causa possível| Solução possível
| ------------- |-------------| -----|----|----|
| 11516     | Erro |Falha ao publicar o conteúdo da atualização "Atualizar o ID" de uma vez que o conteúdo não está assinado.  Pode ser publicado apenas o conteúdo com assinaturas válidos.  |O Configuration Manager não permite atualizações não assinadas sejam publicados.| Publicar a atualização de uma forma alternativa. </br></br>Ver se uma atualização assinada está disponível a partir do fornecedor.|
| 11523  | Aviso |  O catálogo "X" não inclui os certificados de assinatura de conteúdo, tentativas para publicar conteúdo de atualização para as atualizações a partir desse catálogo podem ser concluída com êxito até que o conteúdo de certificados de assinatura são adicionados e aprovados. | Esta mensagem pode ocorrer quando importa um catálogo que está a utilizar uma versão mais antiga do formato de arquivo cab.|Contacte o fornecedor de catálogo para obter um catálogo de atualização que inclui o conteúdo de certificados de assinatura. </br> </br> Os certificados para os binários não estão incluídos no ficheiro cab para que o conteúdo não conseguirá publicar. Pode contornar este problema ao detetar o certificado no **certificados** nó, desbloquear, em seguida, publicá-la novamente. Se está publicando várias atualizações assinadas com certificados diferentes, terá de desbloquear cada certificado que é utilizado.|
| 11524| Erro  | Falha ao publicar atualização "ID" devido à falta de atualizar os metadados. | A atualização poderá foram sincronizada com o WSUS fora do Configuration Manager.| Sincronize a atualização com o Configuration Manager antes de tentar publicá-lo é conteúdo.  </br> </br>Se uma ferramenta externa foi utilizada para publicar a atualização como **apenas os metadados de**, em seguida, utilize a mesma ferramenta para publicar o conteúdo da atualização.|



## <a name="working-with-third-party-updates-video"></a>Trabalhar com o vídeo de atualizações de terceiros
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Implementar atualizações de software](./deploy-software-updates.md)
