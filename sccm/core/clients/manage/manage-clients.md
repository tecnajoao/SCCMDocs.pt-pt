---
title: Gerir clientes | Documentos do Microsoft
description: Saiba como gerir clientes no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 3a86924b2e5db3ac16eeda78b95ae6747ffd656f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Como gerir clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando um cliente do System Center Configuration Manager está instalado e atribuído com êxito a um site do Configuration Manager, irá ver o dispositivo no **ativos e compatibilidade** área de trabalho a **dispositivos** nó e numa ou mais coleções no **coleções de dispositivos** nó. Quando selecionar o dispositivo ou uma coleção, é possível efetuar operações de gestão. No entanto, existem outras formas de gerir o cliente, que poderão envolver outras áreas de trabalho na consola ou tarefas que não utilizem a consola do Configuration Manager.  

> [!NOTE]  
>  Um cliente do Configuration Manager poderá estar instalado mas não é apresentada na consola do Configuration Manager. Isto pode acontecer se o cliente ainda não tiver sido atribuído com êxito a um site, ou a consola tem de ser atualizada ou uma associação de coleção.  
>   
>  Além disso, um dispositivo também pode ver na consola quando o cliente do Configuration Manager não está instalado. Isto pode acontecer se o dispositivo for detetado mas o cliente do Configuration Manager não está instalado e atribuído. Dispositivos móveis que são geridos utilizando o conector do Exchange Server e os dispositivos que são inscritos pelo Microsoft Intune, não instale o cliente do Configuration Manager.  
>   
>  Utilize o **cliente** coluna na consola do Configuration Manager para determinar se o cliente do Configuration Manager está instalado para que possa geri-lo a partir da consola do Configuration Manager.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Gerir Clientes a partir do Nó Dispositivos  

Tenha em atenção que, consoante o tipo de dispositivo, algumas destas opções poderão não estar disponíveis.  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** >  **dispositivos**.  

3.  Selecione um ou mais dispositivos e, em seguida, selecione uma das seguintes tarefas de gestão de cliente a partir do Friso, ou clicando com o dispositivo:  

    -   **Gerir as informações de afinidade dispositivo/utilizador**  

         Configure as associações entre utilizadores e dispositivos, para que a forma eficiente, pode implementar software para utilizadores.  

         Veja [Associar utilizadores e dispositivos à afinidade de dispositivo do utilizador no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Adicionar o dispositivo a uma coleção nova ou existente**  

         Adicione o dispositivo a uma coleção com uma regra direta.  
         
    -   **Instalar e reinstalar o cliente utilizando o assistente Push do Cliente**  

         Instalar e reinstalar o cliente do Configuration Manager para o reparar ou reconfigurar em computadores que executam o Windows. Inclui as opções de configuração do site e as propriedades de Client. msi que definiu para a instalação de push de cliente.  

        > [!TIP]  
        >  Existem muitas formas diferentes de instalar (e reinstalar) o cliente do Configuration Manager. Embora o assistente Push do cliente constitua um conveniente método de instalação de cliente porque pode executá-lo a partir da consola, este método tem muitas dependências e não é adequado para todos os ambientes. Para obter mais informações sobre as dependências, veja [Pré-requisitos para implementar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Para obter mais informações sobre os outros métodos de instalação do cliente, veja [Métodos de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Veja [Como Instalar Clientes do Configuration Manager Utilizando Push de Cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reatribuir o Site**  

         Reatribui um ou mais clientes, incluindo dispositivos móveis geridos, a outro site primário da hierarquia. Os clientes podem ser reatribuídos individualmente ou podem ser selecionados várias vezes e reatribuídos em massa a um novo site.  

    -   **Administrar o cliente remotamente**  

         Pode executar o Explorador de Recursos para consultar informações sobre o inventário de hardware e software a partir de um cliente Windows e para o administrar remotamente utilizando o Controlo Remoto, Assistência Remota ou Ambiente de Trabalho Remoto.  

         Veja [Como utilizar o Explorador de Recursos para ver o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [Como utilizar o Explorador de Recursos para ver o inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Veja [Como administrar remotamente um computador cliente Windows utilizando o System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Aprovar um cliente**  

         Quando o cliente comunica com os sistemas de sites utilizando HTTP e um certificado autoassinado, tem de aprovar esses clientes para os identificar como computadores fidedignos. Por predefinição, a configuração do site aprova automaticamente os clientes da mesma floresta do Active Directory e de florestas fidedignas, pelo que não terá de aprovar manualmente cada cliente. No entanto, terá de aprovar manualmente os computadores do grupo de trabalho que considere fidedignos e quaisquer outros computadores fidedignos mas que não se encontrem aprovados.  

        > [!WARNING]  
        >  Apesar de algumas funções de gestão poderem funcionar para clientes não aprovados, este é um cenário não suportado para o Configuration Manager.  

         Não é necessário aprovar os clientes que comuniquem sempre com os sistemas de sites utilizando HTTPS, nem os clientes que utilizam um certificado PKI quando comunicam com sistemas de sites utilizando HTTP. Estes clientes estabelecem fidedignidade utilizando os certificados PKI.  

    -   **Bloquear ou desbloquear um cliente**  

         Bloqueie os clientes deixe de considerar fidedignos para os impedir de receber a política de cliente e para impedir que os sistemas de sites do Configuration Manager comuniquem com ele.  

        > [!WARNING]  
        >  Bloquear um cliente apenas impede a comunicação entre o cliente para sistemas de sites do Configuration Manager e não impedindo a comunicação com outros dispositivos. Além disso, quando o cliente comunica com os sistemas de site utilizando HTTP em vez de HTTPS, existem algumas limitações de segurança.  

         Pode desbloquear um cliente que foi bloqueado. No entanto, se desbloquear um computador baseado em Intel AMT que tenha sido aprovisionado para AMT quando foi bloqueado, terá de efetuar passos adicionais para poder gerir novamente esse computador fora de banda.  

         Veja [Determinar se deve bloquear clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Limpar uma implementação de PXE necessária**  

         Voltar a implementar as implementações de PXE necessárias para o computador.  

         Veja [Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gerir as propriedades do cliente**  

         Ver os dados de deteção e as implementações direcionadas para o cliente. Também pode configurar as variáveis utilizadas pelas sequências de tarefas para implementar um sistema operativo no dispositivo.  

    -   **Eliminar o cliente**  

        > [!WARNING]  
        >  Não elimine um cliente se pretender desinstalar o cliente do Configuration Manager ou removê-lo a partir de uma coleção.  

         O **eliminar** ação elimina manualmente o registo do cliente da base de dados do Configuration Manager e normalmente, não deve utilizar esta ação, exceto em cenários de resolução de problemas. Se eliminar o registo do cliente e o cliente estiver ainda instalado e ao comunicar com o Configuration Manager, a deteção de Heartbeat recriará o registo do cliente e este voltará na consola do Configuration Manager, embora o histórico do cliente e eventuais associações anteriores sejam perdidas.  

        > [!NOTE]  
        >  Quando elimina um cliente de dispositivo móvel que tenha sido inscrito pelo Configuration Manager, esta ação revogará também o certificado PKI emitido para o dispositivo móvel e este certificado será então rejeitado pelo ponto de gestão, mesmo que o IIS não verifique o CRL. Os certificados em clientes legados de dispositivos móveis não são revogados quando elimina esses clientes.  

         Para desinstalar o cliente, veja [Desinstalar o Cliente do Configuration Manager](#BKMK_UninstalClient).  

         Para atribuir o cliente a um novo site primário, veja [Como atribuir clientes a um site no Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Para remover o cliente de uma coleção, reconfigure as propriedades da coleção. Veja [Como gerir coleções no System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Eliminar os dados de um dispositivo móvel**  

         É possível eliminar os dados de dispositivos móveis que suportem o comando de eliminação de dados.  

         Esta ação remove de forma permanente todos os dados no dispositivo móvel, incluindo definições pessoais e dados pessoais. Normalmente, esta ação repõe as predefinições de fábrica do dispositivo móvel. Apagar um dispositivo móvel quando o dispositivo móvel já não é considerado fidedigno, exemplo, se tiver sido perdido ou roubado.  

        > [!TIP]  
        >  Consulte a documentação do fabricante para obter mais informações sobre como o dispositivo móvel processa um comando de eliminação remota.  

         Há frequentemente um atraso até que o dispositivo móvel receba o comando de eliminação de dados:  

        -   Se o dispositivo móvel tiver sido inscrito pelo Configuration Manager ou do Microsoft Intune, o cliente receberá o comando quando transfere a política de cliente.  

        -   Se o dispositivo móvel for gerido pelo conector do Exchange Server, receberá o comando quando a sincronizar com o Exchange.  

         Pode utilizar o **apagar estado** coluna para monitorizar quando o dispositivo recebe o comando de eliminação de dados. Até que o dispositivo envie uma confirmação da eliminação para o Configuration Manager pode cancelar o comando de eliminação de dados.  

    -   **Extinguir um dispositivo móvel**  

         O **extinguir** opção só é suportada por dispositivos móveis que são inscritos pelo Intune ou no\-local gestão de dispositivos móveis.  

         Para obter mais informações, veja [Ajudar a proteger os seus dados através de eliminação remota de dados, bloqueio remoto ou reposição do código de acesso com o System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Alterar a propriedade de um dispositivo**  

         Pode alterar a propriedade dos dispositivos para **empresa** ou **pessoal** se um dispositivo não estiver associado a um domínio e não tem o cliente do Configuration Manager instalado.  

         Pode utilizar este valor nos requisitos de aplicações para controlar as implementações e para controlar a quantidade de inventário recolhido dos dispositivos dos utilizadores.  

        Poderá ter de adicionar o **proprietário do dispositivo** coluna para a vista ao clicar com qualquer cabeçalho de coluna e escolhê-la.

         Para obter mais informações, veja [Gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gerir Clientes a partir do Nó Coleções de Dispositivos  
  Muitas das tarefas que pode executar num único dispositivo ou em vários dispositivos no **dispositivos** nó pode ser efetuado em coleções. Isto aplica automaticamente a operação a todos os dispositivos elegíveis da coleção. Tenha em atenção que isto gera um muitos pacotes de rede e aumenta a utilização da CPU no servidor do site.  

  Antes de executar tarefas de gestão de clientes ao nível da coleção, considere o número de dispositivos da coleção, se se encontram ligados por ligações de rede com baixa largura de banda e quanto tempo demorará a tarefa a ser concluída em todos os dispositivos. Assim que tiver sido iniciado, não é possível parar a tarefa a partir da consola.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para gerir os clientes a partir do nó Coleções de Dispositivos  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de dispositivos**.  

3.  Selecione uma coleção e, em seguida, selecione uma das seguintes tarefas de gestão de cliente a partir do Friso, ou clicando na coleção. Estas tarefas de gestão do cliente podem *apenas* ser executadas ao nível da coleção.  

    -   **Analisar os computadores quanto a software maligno e transferir os ficheiros de definições antimalware.**  

         Consulte o artigo [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Implementar software, linhas de base de configuração e sequências de tarefas.**  

         Consulte o artigo:  

        -   [Implementar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planear e configurar as definições de compatibilidade no System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configurar as definições de gestão de energia.**  

         Veja [Como criar e aplicar esquemas de energia no System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Os esquemas de energia só podem ser utilizados em computadores com o Windows.  

    -   **Notificar os computadores para que transfiram a política o mais brevemente possível.**  

         Utilize a notificação do cliente para notificar os clientes Windows selecionados para transferirem a política de computador com a brevidade possível, fora do intervalo de consulta da política de cliente.  

         As tarefas de notificação do cliente são apresentadas no nó **Operações do Cliente** , na área de trabalho **Monitorização** .  

##  <a name="BKMK_ClientCache"></a> Configurar a Cache do Cliente para Clientes do Configuration Manager  
A cache do cliente armazena ficheiros temporários para quando os clientes instalam as aplicações e programas. As atualizações de software também utilizam a cache do cliente, mas não estão restringidas pelo tamanho da cache configurado e tentarão sempre transferir para a cache. Pode configurar as definições da cache do cliente, tais como o tamanho e localização, quando a instalação de cliente do Configuration Manager manualmente, se utilizar a instalação de push de cliente ou após a instalação do cliente.

A partir do Configuration Manager versão 1606, pode especificar o tamanho da pasta cache utilizando as definições de cliente na consola do Configuration Manager.   

 A localização predefinida para a cache do cliente do Configuration Manager é de %*windir*%\ccmcache e o espaço de disco predefinido é 5120 MB.  

> [!IMPORTANT]  
>  Não encripte a pasta utilizada para a cache do cliente. O Configuration Manager não consegue transferir conteúdo para uma pasta encriptada.  

### <a name="about-client-cache"></a>Sobre a cache do cliente  

O cliente do Configuration Manager transfere o conteúdo do software necessário logo que recebe a implementação, mas aguarda executá-la a implementação da hora agendada. Na hora agendada, verifica se o conteúdo está disponível na cache do cliente do Configuration Manager. Se o conteúdo estiver na cache e for a versão correta, o cliente utiliza o conteúdo em cache. Se a versão necessária do conteúdo tiver sido alterada ou se o conteúdo tiver sido eliminado para criar espaço para outro pacote, o conteúdo é transferido novamente para a cache.  

Se o cliente tenta transferir conteúdo de um programa ou aplicação que é maior do que o tamanho da cache, a implementação falha devido ao tamanho insuficiente da cache e o Configuration Manager gera o ID de mensagem de estado 10050. Se o tamanho da cache for aumentado posteriormente, o resultado é:  

-   Para um programa necessário: O cliente não tenta automaticamente Repetir para transferir o conteúdo. É necessário voltar a implementar o pacote e o programa no cliente.  
-   Para uma aplicação necessária: O cliente tenta automaticamente repete a transferência do conteúdo transfere a política de cliente.  

Se o cliente tenta transferir um pacote que é menor do que o tamanho da cache e a cache estiver completo, todas as implementações necessárias continuará a tentar até que o espaço da cache esteja disponível, até que a transferência exceda o tempo limite ou até que seja atingido o limite de repetição para a falha de espaço da cache. Se o tamanho da cache for aumentado posteriormente, o cliente do Configuration Manager tenta transferir o pacote novamente durante o próximo intervalo de repetição. O cliente tenta transferir o conteúdo de quatro em quatro horas até atingir 18 tentativas.  

O conteúdo em cache não é eliminado automaticamente. Permanece na cache durante, pelo menos, um dia após o cliente ter utilizado esse conteúdo. Se configurar as propriedades do pacote com a opção para manter conteúdo na cache do cliente, este não elimina automaticamente o conteúdo do pacote na cache. Se o espaço da cache do cliente estiver utilizado por pacotes que foram transferidos nas últimas 24 horas e o cliente tiver de transferir novos pacotes, é possível aumentar o tamanho da cache do cliente ou escolher a opção de eliminação para eliminar o conteúdo mantido na cache.  

 Utilize os procedimentos seguintes para configurar a cache do cliente durante a instalação manual do cliente ou após a instalação do cliente.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar a cache do cliente quando os clientes são instalados através da instalação manual  

Execute o comando CCMSetup.exe a partir da localização de origem da instalação e, entre as seguintes propriedades, especifique as que forem necessárias, separadas por espaços:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para obter versão 1606, utilize as definições de tamanho da cache disponíveis no **definições de cliente** na consola do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, veja [Definições da Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Para obter mais informações sobre como utilizar estas propriedades de linha de comandos para CCMSetup.exe, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar a pasta da cache do cliente quando os clientes são instalados através da instalação push de cliente  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site adequado e, no **base** no separador de **definições** grupo, selecione **definições de instalação de cliente** > **separador Propriedades de instalação**.  

5.  Especifique as seguintes propriedades, separadas por espaços:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para obter versão 1606, utilize as definições de tamanho da cache disponíveis no **definições de cliente** na consola do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, veja [Definições da Cache do Cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       Para obter mais informações sobre como utilizar estas propriedades de linha de comandos para CCMSetup.exe, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar a pasta da cache do cliente no computador cliente  

1.  No computador cliente, navegue até à **do Configuration Manager** no painel de controlo e faça duplo clique para abrir as propriedades.  

2.  No **Cache** separador definir as propriedades de espaço e a localização. A localização predefinida é *%windir%*\ccmcache.  

5.  Para eliminar os ficheiros na pasta de cache, escolha **eliminar ficheiros**.  

    > [!NOTE]
    > 
    > A pasta da cache é uma pasta do Windows normal, pelo que pode automatizar a eliminação do conteúdo da pasta a utilizar um script, um utilitário ou com o cmdlet do PowerShell `Remove-Item`. 


### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar o tamanho da cache do cliente nas Definições do Cliente

A partir na versão 1606, pode ajustar o tamanho da pasta de cache do cliente sem ter de reinstalar o cliente. Para tal, configure o tamanho da cache do cliente na consola do Configuration Manager com as Definições do Cliente.  

1. Na consola do Configuration Manager, aceda a **Administração** > **Definições do Cliente**.

2. Faça duplo clique em **Predefinições de Cliente**.
  Também pode criar definições personalizadas de cliente para aplicar o tamanho da cache mais seletivamente. Para obter mais informações sobre predefinições e definições de cliente personalizadas, veja [Como configurar as definições do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Escolher **definições de Cache do cliente** e escolha **Sim** para **configurar tamanho da cache do cliente**, em seguida, utilize um a **MB** ou **percentagem das definições de disco**. A cache é ajustada para o tamanho que for menor.

     O cliente do Configuration Manager irá configurar o tamanho da cache com estas definições, quando a política de cliente seguinte é transferida.

##  <a name="BKMK_UninstalClient"></a> Desinstalar o Cliente do Configuration Manager  
 Pode desinstalar o software de cliente do Gestor de configuração do Windows a partir de um computador utilizando **CCMSetup.exe** com o **/desinstalação** propriedade. Execute o ficheiro CCMSetup.exe num computador individual a partir da linha de comandos ou implemente um pacote e um programa para desinstalar o cliente para uma coleção de computadores.  

> [!WARNING]  
>  Não é possível desinstalar o cliente do Configuration Manager a partir de um dispositivo móvel. Se for necessário remover o cliente do Configuration Manager a partir de um dispositivo móvel, terá que apagar o dispositivo, o que elimina todos os dados no dispositivo móvel.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar o cliente do Configuration Manager a partir da linha de comandos  

1.  Abra uma linha de comandos do Windows e altere a pasta para a localização em que se encontra o ficheiro CCMSetup.exe.  

2.  Escreva **Ccmsetup.exe /uninstall**e prima **Enter.**  

> [!NOTE]  
>  O processo de desinstalação não apresenta qualquer resultado no ecrã. Para verificar se a desinstalação do cliente foi bem sucedida, examine o ficheiro de registo **Ccmsetup** na pasta *%windir%\ ccmsetup* no computador cliente.  

##  <a name="BKMK_ConflictingRecords"></a> Gerir Registos em Conflito para Clientes do Configuration Manager  
 Configuration Manager utiliza o ID de hardware para tentar identificar clientes que possam ser duplicados e alertá-lo para os registos em conflito. Por exemplo, se reinstalar um computador, o ID de hardware será o mesmo, mas o GUID utilizado pelo Configuration Manager pode ser alterado.  

 Quando Configuration Manager pode resolver um conflito através da autenticação do Windows da conta de computador ou um certificado PKI de uma origem fidedigna, o conflito é resolvido automaticamente. No entanto, quando o Configuration Manager não consegue resolver o conflito, utiliza uma definição que ou intercala automaticamente os registos quando Deteta IDs de hardware duplicados (a predefinição) ou lhe permite decidir quando intercalar, bloquear ou criar novo cliente registos da hierarquia. Se optar por gerir manualmente os registos duplicados, tem de resolver manualmente registos em conflito na consola do Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para alterar a definição da hierarquia para gerir registos em conflito  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites** > **definições de hierarquia**
2.  No **aprovação do cliente e registos em conflito** separador, selecione a **resolver automaticamente registos em conflito**, ou **resolver manualmente registos em conflito**.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente registos em conflito  

1.  Na consola do Configuration Manager, escolha **monitorização** > **estado do sistema** > **registos em conflito**.  

3.  Selecione um ou mais registos em conflito e, em seguida, escolha **registo em conflito**.  

4.  Selecione um dos seguintes procedimentos:  

    -   **Intercalar** para combinar o registo detetado recentemente com o registo de cliente existente.  

    -   **Novo** para criar um novo registo para o registo do cliente em conflito.  

    -   **Bloquear** para criar um novo registo para o registo do cliente em conflito, mas marcá-lo como bloqueado.  

## <a name="manage-duplicate-hardware-identifiers"></a>Gerir identificadores de hardware duplicados
A partir do Configuration Manager versão 1610, pode fornecer uma lista de IDs do Configuration Manager irá ignorar para efeitos de registo de arranque e de cliente PXE de hardware. Existem dois problemas comuns que isto ajuda a endereço.

1. Vários dispositivos novos, como as 3 Surface Pro, não incluem uma porta Ethernet carregar. Um adaptador USB para Ethernet é geralmente utilizado para estabelecer uma ligação com fios para fins de implementação do sistema operativo. No entanto, estas, muitas vezes, são partilhados adaptadores devido um custo e facilidade de utilização geral. Como o endereço MAC deste adaptador é utilizado para identificar o dispositivo, reutilizar o adaptador fica problemáticas sem ações adicionais administrador entre cada implementação. A partir da versão 1610, pode excluir o endereço MAC deste adaptador para que possa ser reutilizado neste cenário.
2. Enquanto o ID de SMBIOS deveria para ser um identificador exclusivo de hardware, alguns dispositivos de hardware specialty são criados com IDs duplicados. Enquanto não tão comuns como o cenário de adaptador USB para Ethernet acima, a lista de IDs de hardware pode ser utilizada para resolver este problema também.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Para adicionar os identificadores de hardware para o Configuration Manager para ignorar  
1. Na consola do Configuration Manager, aceda a **administração** > **descrição geral** > **configuração do Site** > **Sites**.
2. No **base** separador o **Sites** grupo, selecione **definições de hierarquia**.
3. No **aprovação do cliente e registos em conflito** separador, escolha **adicionar** no **duplicar identificadores de hardware** secção para adicionar os identificadores de hardware novo.

##  <a name="BKMK_PolicyRetrieval"></a> Iniciar a Obtenção de Política para um Cliente do Configuration Manager  
 Um cliente Windows Configuration Manager transfere a política de cliente com base numa agenda configurada como uma definição de cliente. No entanto, poderá haver ocasiões em que pretenderá iniciar a obtenção de política ad-hoc do cliente, por exemplo, para resolução de problemas ou testar.  

Pode iniciar a utilização de obtenção de política:


- [Notificação do cliente](#initiate-client-policy-retrieval-using-client-notification) 
- [O **ações** separador no cliente](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Um script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Para obter informações sobre a obtenção de políticas para clientes com Linux e UNIX, veja [Política de computador para servidores Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>Iniciar a obtenção da política de cliente utilizando a notificação do cliente  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de dispositivos**.  

3.  Selecione a coleção de dispositivos que contém os computadores que pretende transferir a política. No **base** separador o **coleções** grupo, selecione **notificação do cliente** > **transferir política do computador**.  

    > [!NOTE]  
    >  Também pode utilizar a notificação do cliente para iniciar a obtenção da política para um ou mais dispositivos selecionados apresentados num nó de coleção temporário do nó **Dispositivos** .  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Iniciar manualmente a obtenção de política de cliente no separador ações do cliente do Configuration Manager  

1.  Selecione **Configuration Manager** no Painel de Controlo do computador.  

2.  No **ações** separador escolher **ciclo de avaliação de obtenção de política de máquina e** para iniciar a política do computador e, em seguida, escolha **executar agora**.  

4.  Escolher **OK** para confirmar a linha de comandos.  

5.  Repita os passos 3 e 4 para outras ações que sejam necessárias, tais como **Ciclo de Obtenção e Avaliação da Política de Utilizador** para definições de cliente do utilizador.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>Iniciar manualmente a obtenção da política de cliente por script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte no ficheiro:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Guarde o ficheiro com uma extensão .vbs.  

4.  No computador cliente, execute o ficheiro utilizando um dos seguintes métodos:  

    -   Navegue para o ficheiro através do Explorador do Windows e faça duplo clique no ficheiro de script.  

    -   Abra uma linha de comandos e escreva: **cscript &lt;path\filename.vbs >**.  

5.  Escolher **OK** no **Windows Script Host** caixa de diálogo.  

