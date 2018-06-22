---
title: Gerir clientes
titleSuffix: Configuration Manager
description: Saiba como gerir clientes no System Center Configuration Manager.
ms.date: 12/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623d7b6a048b7728e40adb3655dc1017408fb1d7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342227"
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Como gerir clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando o cliente do Configuration Manager instala num dispositivo e atribui com êxito a um site, consulte o dispositivo no **ativos e compatibilidade** área de trabalho a **dispositivos** nó e em uma ou mais as coleções no **coleções de dispositivos** nós. Quando seleciona uma coleção ou do dispositivo, pode efetuar operações de gestão. No entanto, existem outras formas de gerir o cliente, que poderão envolver outras áreas de trabalho na consola ou tarefas fora da consola.  

> [!NOTE]  
>  Se o cliente do Configuration Manager está instalado, mas ainda não atribuído com êxito a um site, pode não apresentar na consola do. Depois do cliente atribui a um site, atualizar associação da coleção e atualize a vista da consola.  
>   
>  Além disso, um dispositivo também pode apresentar na consola quando o cliente do Configuration Manager não está instalado. Este comportamento ocorre se o dispositivo for detetado mas o cliente não está instalado e atribuído. 
>
> Dispositivos móveis geridos utilizando o conector do Exchange Server e os dispositivos inscritos no Microsoft Intune não instalam o cliente do Configuration Manager.  
>   
>  Utilize o **cliente** coluna na consola do Configuration Manager para determinar se o cliente está instalado para que a geri-lo a partir da consola.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Gerir Clientes a partir do Nó Dispositivos  

Dependendo do tipo de dispositivo, algumas destas opções poderão não estar disponíveis.  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** >  **dispositivos**.  

3.  Selecione um ou mais dispositivos e, em seguida, selecione uma destas tarefas de gestão de cliente a partir do Friso, ou clicando com o dispositivo:  

    -   **Gerir as informações de afinidade dispositivo/utilizador**  

         Configure as associações entre utilizadores e dispositivos, de modo a forma eficiente poderá implementar software nos utilizadores.  

         Veja [Associar utilizadores e dispositivos à afinidade de dispositivo do utilizador no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Adicionar o dispositivo a uma coleção nova ou existente**  

         Adicione o dispositivo a uma coleção com uma regra direta.  

    -   **Instalar e reinstalar o cliente utilizando o assistente Push do Cliente**  

         Instalar e reinstalar o cliente do Configuration Manager para reparar ou reconfigurá-lo. Esta opção inclui definições de configuração do site e as propriedades de client.msi que definiu para a instalação push do cliente.  

        > [!TIP]  
        >  Existem muitas formas diferentes de instalar (e reinstalar) o cliente do Configuration Manager. Embora o assistente Push do cliente oferece uma conveniente método de instalação do cliente porque pode executá-lo a partir da consola, este método tem muitas dependências e não é adequado para todos os ambientes. Para obter mais informações sobre as dependências, veja [Pré-requisitos para implementar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Para obter mais informações sobre os outros métodos de instalação do cliente, veja [Métodos de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Veja [Como Instalar Clientes do Configuration Manager Utilizando Push de Cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reatribuir o Site**  

         Reatribui um ou mais clientes, incluindo dispositivos móveis geridos, a outro site primário da hierarquia. Os clientes podem ser reatribuídos individualmente ou podem ser selecionados várias vezes e reatribuídos em massa a um novo site.  

    -   **Administrar o cliente remotamente**  

         Execute o Explorador de recursos para ver as informações de inventário de hardware e software de um cliente Windows. Administrar remotamente o dispositivo utilizando o controlo remoto, assistência remota ou ambiente de trabalho remoto.  

         Consulte [como utilizar o Explorador de recursos para ver o inventário de hardware](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [como utilizar o Explorador de recursos para ver o inventário de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Consulte [como administrar remotamente um computador cliente Windows](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Aprovar um cliente**  

         Quando o cliente comunica com os sistemas de site utilizando HTTP e um certificado autoassinado, tem de aprovar esses clientes para os identificar como computadores fidedignos. Por predefinição, a configuração do site aprova automaticamente os clientes da mesma floresta do Active Directory e de florestas fidedignas, pelo que não terá de aprovar manualmente cada cliente. No entanto, terá de aprovar manualmente computadores de grupo de trabalho que considere de confiança e quaisquer outros computadores não aprovados que considera fidedignos.  

        > [!WARNING]  
        >  Apesar de algumas funções de gestão poderem funcionar para clientes não aprovados, este é um cenário não suportado para o Configuration Manager.  

         Terá de aprovar os clientes que comuniquem sempre com através de HTTPS de sistemas de sites ou clientes que utilizam um certificado PKI quando comunicam com sistemas de site utilizando HTTP. Estes clientes estabelecem fidedignidade utilizando os certificados PKI.  

    -   **Bloquear ou desbloquear um cliente**  

         Bloquear um cliente que já não confia. Bloquear impede que o cliente receber a política e impede que os sistemas de sites ao comunicar com o cliente.  

        > [!WARNING]  
        >  Bloquear um cliente apenas impede a comunicação entre o cliente para sistemas de sites do Configuration Manager e não impedindo a comunicação com outros dispositivos. Além disso, quando o cliente comunica com os sistemas de site utilizando HTTP em vez de HTTPS, existem algumas limitações de segurança.  

         Também pode desbloquear um cliente que está bloqueado. 

         Veja [Determinar se deve bloquear clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Limpar uma implementação de PXE necessária**  

         Volte a implementar as implementações de PXE necessárias para o computador.  

         Veja [Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gerir as propriedades do cliente**  

         Ver os dados de deteção e as implementações direcionadas para o cliente. Também pode configurar variáveis que utilizam sequências de tarefas para implementar um sistema operativo no dispositivo.  

    -   **Eliminar o cliente**  

        > [!WARNING]  
        >  Não elimine um cliente se pretender desinstalar o cliente do Configuration Manager ou removê-lo a partir de uma coleção.  

         O **eliminar** ação elimina manualmente o registo de cliente da base de dados do Configuration Manager e, normalmente, não deve utilizar esta ação, exceto em cenários de resolução de problemas. Se eliminar o registo do cliente, mas o cliente ainda está instalado e a comunicar com o site, a deteção de Heartbeat recria o registo do cliente. O registo do cliente reappears na consola do Configuration Manager, embora o histórico do cliente e eventuais associações anteriores sejam perdidas.  

        > [!NOTE]  
        >  Quando eliminar um cliente de dispositivo móvel que tenha sido inscrito pelo Configuration Manager, esta ação revogará também o certificado PKI emitido para o dispositivo móvel e este certificado será então rejeitado pelo ponto de gestão, mesmo que o IIS não verifique o CRL. Os certificados em clientes legados de dispositivos móveis não são revogados quando elimina esses clientes.  

         Para desinstalar o cliente, veja [Desinstalar o Cliente do Configuration Manager](#BKMK_UninstalClient).  

         Para atribuir o cliente a um novo site primário, veja [Como atribuir clientes a um site no Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Para remover o cliente de uma coleção, reconfigure as propriedades da coleção. Veja [Como gerir coleções no System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Eliminar os dados de um dispositivo móvel**  

         É possível eliminar os dados de dispositivos móveis que suportem o comando de eliminação de dados.  

         Esta ação remove de forma permanente todos os dados no dispositivo móvel, incluindo definições pessoais e dados pessoais. Normalmente, esta ação repõe as predefinições de fábrica do dispositivo móvel. Apaga um dispositivo móvel quando o dispositivo móvel já não é fidedigno. Por exemplo, se o dispositivo é perdido ou roubado.  

        > [!TIP]  
        >  Consulte a documentação do fabricante para obter mais informações sobre como o dispositivo móvel processa um comando de eliminação remota de dados.  

         Não há frequentemente um atraso até que o dispositivo móvel recebe o comando de eliminação de dados:  

        -   Se o dispositivo móvel estiver inscrito pelo Configuration Manager ou pelo Microsoft Intune, o cliente receberá o comando quando transfere a política de cliente.  

        -   Se o dispositivo móvel for gerido pelo conector do Exchange Server, receberá o comando de sincronizar com o Exchange.  

         Pode utilizar o **apagar estado** coluna para monitorizar quando o dispositivo recebe o comando de eliminação de dados. Até que o dispositivo envie uma confirmação da eliminação para o Configuration Manager, pode cancelar o comando de eliminação de dados.  

    -   **Extinguir um dispositivo móvel**  

         O **extinguir** opção só é suportada por dispositivos móveis inscritos pelo Microsoft Intune ou no\-no local a gestão de dispositivos móveis.  

         Para obter mais informações, veja [Ajudar a proteger os seus dados através de eliminação remota de dados, bloqueio remoto ou reposição do código de acesso com o System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Alterar a propriedade de um dispositivo**  

         Se um dispositivo não estiver associado ao domínio e não tenham o cliente de Configuration Manager instalado, utilize esta opção para alterar a propriedade para **empresa** ou **pessoais**.  

         Pode utilizar este valor nos requisitos de aplicações para controlar as implementações e para controlar a quantidade inventário é recolhido dos dispositivos dos utilizadores.  

        Poderá ter de adicionar o **proprietário do dispositivo** coluna para a vista, clique em qualquer cabeçalho de coluna e escolhê-lo.

         Para obter mais informações, veja [Gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gerir clientes a partir do nó coleções de dispositivos  
  Muitas das tarefas que estão disponíveis para dispositivos no **dispositivos** nós também estão disponíveis em coleções. A consola automaticamente aplica-se a operação para todos os dispositivos elegíveis da coleção. Esta ação de um conjunto completo gera os pacotes de rede adicionais e aumenta a utilização da CPU no servidor do site.  

  Considere o seguinte para efetuar tarefas ao nível da coleção. Depois de iniciado, não é possível parar a tarefa a partir da consola. 
 - Quantos dispositivos estão na coleção?
 - Os dispositivos ligados por ligações de rede de largura de banda baixa?
 - Quanto tempo esta tarefa necessários para todos os dispositivos?

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Para gerir os clientes a partir do nó Coleções de Dispositivos  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de dispositivos**.  

3.  Selecione uma coleção e, em seguida, selecione uma das seguintes tarefas de gestão de cliente a partir do Friso, ou clicando na coleção. Estas tarefas de gestão do cliente podem *apenas* ser executadas ao nível da coleção.  

    -   **Analisar os computadores quanto a software maligno e transferir os ficheiros de definições antimalware.**  

         Consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Implementar software, linhas de base de configuração e sequências de tarefas.**  

         Consulte:  

        -   [Implementar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planear e configurar as definições de compatibilidade no System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configurar as definições de gestão de energia.**  

         Veja [Como criar e aplicar esquemas de energia no System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Os esquemas de energia só podem ser utilizados em computadores com o Windows.  

    -   **Notificar os computadores para que transfiram a política o mais brevemente possível.**  

         Utilize a notificação de cliente para notificar os clientes Windows selecionados para transferirem a política de computador logo que possível, fora do intervalo de consulta da política de cliente.  

         As tarefas de notificação do cliente são apresentadas no nó **Operações do Cliente** , na área de trabalho **Monitorização** .  


## <a name="restart-clients"></a>Reinicie os clientes
A partir da versão 1710, pode utilizar a consola do Configuration Manager para identificar os clientes que necessitam de um reinício. Em seguida, utilize uma ação de notificação de cliente reiniciá-las.

> [!Tip]
> Também tem de atualizar os clientes para a versão 1710 para esta capacidade para a função. Recomendamos que ative a atualização automática de cliente a manter os seus clientes atualizados com minimizando a sobrecarga administrativa. Para obter mais informações, consulte [utiliza a atualização automática do cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).

Para identificar dispositivos que tenham um reinício pendente, vá para o **ativos e compatibilidade** área de trabalho na consola do Configuration Manager e selecione o **dispositivos** nós. Em seguida, ver o estado de cada dispositivo no painel de detalhes de uma nova coluna com o nome **reinício pendente**. Cada dispositivo tem um ou mais dos seguintes valores: 
 - **Não**: não há nenhum reinício pendente
 - **O Configuration Manager**: este valor provém de componente de coordenador de reiniciar o computador cliente (RebootCoordinator.log)
 - **Mudar o nome de ficheiro**: este valor provém de uma operação de mudança de nome de ficheiro pendentes (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations) de relatórios do Windows
 - **Windows Update**: este valor provém do Windows Update Agent Reporting Services um reinício pendente não é necessário para uma ou mais atualizações (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
 - **Adicionar ou remover a funcionalidade**: este valor provém do Windows componente Manutenção baseada em relatórios a adição ou remoção de uma funcionalidade do Windows requer um reinício (HKLM\Software\Microsoft\Windows\CurrentVersion\Component com base Servicing\Reboot Pendente)

**Para criar a notificação de cliente para reiniciar um dispositivo:**
1.  Localize o dispositivo que pretende reiniciar dentro de uma coleção no **coleções de dispositivos** nós da consola.
2.  Faça duplo clique no dispositivo, selecione **notificação do cliente**e, em seguida, selecione **reiniciar**. É aberta uma janela de informações sobre o reinício. Clique em **OK** para confirmar o pedido de reinício.

Quando a notificação é recebida por um cliente, um **Centro de Software** é aberta a janela de notificação a informar o utilizador sobre o reinício. Por predefinição, o reinício ocorre após 90 minutos. Pode modificar a hora de reinício configurando [as definições de cliente](/sccm/core/clients/deploy/configure-client-settings). Definições para o comportamento de reinício se encontram no [reinício do computador](/sccm/core/clients/deploy/about-client-settings#computer-restart) separador das definições predefinidas.


##  <a name="BKMK_ClientCache"></a> Configurar a Cache do Cliente para Clientes do Configuration Manager  
A cache do cliente armazena ficheiros temporários para quando os clientes instalam as aplicações e programas. As atualizações de software também utilizam a cache do cliente, mas sempre tentarem transferir para a cache, independentemente da definição de tamanho. Configure as definições de cache, tais como o tamanho e localização, quando instalar manualmente o cliente, quando utilizar a instalação de push de cliente ou após a instalação.

A partir do Configuration Manager versão 1606, pode especificar o tamanho da pasta cache utilizando as definições de cliente da consola do Configuration Manager.   

 A localização predefinida para a cache do cliente do Configuration Manager é de %*windir*%\ccmcache e o espaço de disco predefinido é 5120 MB.  

> [!IMPORTANT]  
>  Não encripte a pasta utilizada para a cache do cliente. O Configuration Manager não consegue transferir conteúdo para uma pasta encriptada.  

### <a name="about-client-cache"></a>Sobre a cache do cliente  

O cliente do Configuration Manager transfere o conteúdo do software necessário logo que recebe a implementação, mas aguarda para executá-lo a implementação da hora agendada. Na hora agendada, o cliente do Configuration Manager verifica se o conteúdo está disponível na cache. Se o conteúdo está na cache e é a versão correta, o cliente utiliza os conteúdos em cache. Quando altera a versão necessária do conteúdo, ou se o cliente elimina o conteúdo para disponibilizar espaço para outro pacote, o cliente transfere o conteúdo para a cache novamente.  

Se o cliente tenta transferir conteúdo para um programa ou aplicação que é superior ao tamanho da cache, a implementação falha devido ao tamanho insuficiente da cache. O cliente gera a mensagem de estado 10050 para tamanho insuficiente da cache. Se, posteriormente, aumentar o tamanho da cache, o resultado é:  

-   Para um programa necessário: O cliente não tenta automaticamente repetir a transferência do conteúdo. Volte a implementar o pacote e programa para o cliente.  
-   Para uma aplicação necessária: O cliente tenta automaticamente repetir a transferência do conteúdo quando transfere a política de cliente.  

Se o cliente tenta transferir um pacote que é inferior ao tamanho da cache, mas a cache está cheia, todas as implementações necessárias continuará a tentar até o espaço da cache disponível, a transferência exceder o tempo limite ou a contagem de repetições atinge o limite. Se o tamanho da cache for aumentado posteriormente, o cliente do Configuration Manager tenta transferir o pacote novamente durante o próximo intervalo entre tentativas. O cliente tenta transferir o conteúdo de quatro em quatro horas até atingir 18 tentativas.  

O conteúdo em cache não é eliminado automaticamente. Permanece na cache durante, pelo menos, um dia após o cliente ter utilizado esse conteúdo. Se configurar as propriedades do pacote com a opção para manter conteúdo na cache do cliente, este não elimina automaticamente o conteúdo do pacote na cache. Se o espaço da cache é utilizado por pacotes transferidos nas últimas 24 horas e o cliente tem de transferir novos pacotes, pode aumentar o tamanho da cache ou escolha a opção para eliminar conteúdo persistente na cache.  

 Utilize os procedimentos seguintes para configurar a cache do cliente durante a instalação manual do cliente ou após a instalação do cliente.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Para configurar a cache do cliente quando os clientes são instalados através da instalação manual  

Execute o comando CCMSetup.exe a partir da localização de origem da instalação e, entre as seguintes propriedades, especifique as que forem necessárias, separadas por espaços:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, utilize as definições de tamanho da cache disponíveis no **as definições de cliente** na consola do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [as definições de cache do cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Para obter mais informações sobre como utilizar estas propriedades da linha de comandos para CCMSetup.exe, consulte [acerca das propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Para configurar a pasta da cache do cliente quando os clientes são instalados através da instalação push de cliente  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site apropriado e no **home page** separador o **definições** grupo, escolha **definições de instalação de cliente** > **separador de propriedades de instalação**.  

5.  Especifique as seguintes propriedades, separadas por espaços:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Para a versão 1606, utilize as definições de tamanho da cache disponíveis no **as definições de cliente** na consola do Configuration Manager em vez de SMSCACHESIZE. Para obter mais informações, consulte [as definições de cache do cliente](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       Para obter mais informações sobre como utilizar estas propriedades da linha de comandos para CCMSetup.exe, consulte [acerca das propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Para configurar a pasta da cache do cliente no computador cliente  

1.  No computador cliente, navegue para **do Configuration Manager** no painel de controlo e faça duplo clique para abrir as propriedades.  

2.  No **Cache** separador definir as propriedades de espaço e a localização. A localização predefinida é *%windir%* \ccmcache.  

3.  Para eliminar os ficheiros na pasta de cache, escolha **eliminar ficheiros**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Para configurar o tamanho da cache do cliente nas Definições do Cliente

Ajuste o tamanho da cache do cliente sem ter de reinstalar o cliente configurando o tamanho da cache na consola do Configuration Manager com as definições de cliente.  

1. Na consola do Configuration Manager, aceda a **Administração** > **Definições do Cliente**.

2. Faça duplo clique em **Predefinições de Cliente**.
  Também pode criar definições personalizadas de cliente para aplicar o tamanho da cache mais seletivamente. Para obter mais informações sobre predefinições e definições de cliente personalizadas, veja [Como configurar as definições do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Escolha **as definições de Cache do cliente** e escolha **Sim** para **configurar o tamanho da cache do cliente**, em seguida, utilizar um o **MB** ou **percentagem das definições de disco**. A cache é ajustada para o tamanho que for menor.

     O cliente do Configuration Manager irá configurar o tamanho da cache com estas definições, quando a política de cliente seguinte é transferida.



##  <a name="BKMK_UninstalClient"></a> Desinstalar o Cliente do Configuration Manager  
 Pode desinstalar o software de cliente do Gestor de configuração do Windows a partir de um computador utilizando **CCMSetup.exe** com o **/desinstalar** propriedade. Execute o ficheiro CCMSetup.exe num computador individual a partir da linha de comandos ou implemente um pacote e um programa para desinstalar o cliente para uma coleção de computadores.  

> [!WARNING]  
>  Não é possível desinstalar o cliente do Configuration Manager a partir de um dispositivo móvel. Se for necessário remover o cliente do Configuration Manager a partir de um dispositivo móvel, tem de apagar o dispositivo, o que elimina todos os dados no dispositivo móvel.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Para desinstalar o cliente do Configuration Manager a partir da linha de comandos  

1.  Abra uma linha de comandos do Windows e altere a pasta para a localização em que se encontra o ficheiro CCMSetup.exe.  

2.  Escreva **Ccmsetup.exe /uninstall**e prima **Enter.**  

> [!NOTE]  
>  O processo de desinstalação não apresenta qualquer resultado no ecrã. Para verificar se a desinstalação do cliente foi bem sucedida, examine o ficheiro de registo **CCMSetup.log** na pasta *%windir%\ ccmsetup* no computador cliente.  

##  <a name="BKMK_ConflictingRecords"></a> Gerir Registos em Conflito para Clientes do Configuration Manager  
 O Configuration Manager utiliza o identificador de hardware para tentar identificar clientes que possam ser duplicados e alertá-lo para os registos em conflito. Por exemplo, se reinstalar um computador, o identificador de hardware será o mesmo, mas o GUID utilizado pelo Configuration Manager poderá ter sido alterado.  

 O Configuration Manager automaticamente resolve conflitos, utilizando a autenticação do Windows da conta de computador ou um certificado PKI de uma origem fidedigna. No entanto, quando o Configuration Manager não é possível resolver o conflito de identificadores de hardware duplicados, uma definição da hierarquia determina se deve intercalar automaticamente os registos ou permite-lhe determinar o comportamento. Se optar por gerir manualmente os registos duplicados, tem de resolver manualmente os registos em conflito na consola do Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Para alterar a definição da hierarquia para gerir registos em conflito  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**  >  **Definições de hierarquia**
2.  No **aprovação do cliente e registos em conflito** separador, escolha o **resolver automaticamente registos em conflito**, ou **resolver manualmente registos em conflito**.  

#### <a name="to-manually-resolve-conflicting-records"></a>Para resolver manualmente registos em conflito  

1.  Na consola do Configuration Manager, escolha **monitorização** > **estado do sistema** > **registos em conflito**.  

3.  Selecione um ou mais registos em conflito e, em seguida, escolha **registo em conflito**.  

4.  Selecione uma das seguintes opções:  

    -   **Intercalar** combinar o registo detetado recentemente com o registo de cliente existente.  

    -   **Novo** para criar um novo registo para o registo do cliente em conflito.  

    -   **Bloquear** para criar um novo registo para o registo do cliente em conflito, mas marcá-lo como bloqueado.  

## <a name="manage-duplicate-hardware-identifiers"></a>Gerir os identificadores de hardware duplicados
Fornecer uma lista do hardware efetuar o arranque de identificadores que ignora do Configuration Manager para fins de PXE e registo de cliente, ajuda a resolver problemas comuns de dois.

1. Muitos dispositivos novos, como o 3 Surface Pro, não incluam uma porta Ethernet carregar. Técnicos utilizam um adaptador USB em Ethernet para estabelecer uma ligação com fios para fins de implementação do sistema operativo. No entanto, estes adaptadores são, muitas vezes, partilhados devido ao custo e a facilidade de utilização geral. Como o endereço MAC deste adaptador é utilizado para identificar o dispositivo, a reutilizar o adaptador torna-se problemático sem ações adicionais administrador entre cada implementação. Reutilizar o adaptador neste cenário, exclua o seu endereço MAC.
2. Enquanto o atributo SMBIOS deve ser exclusivo, alguns dispositivos de hardware specialty tem identificadores duplicados. Exclua este identificador duplicado e dependem do endereço MAC exclusivo de cada dispositivo.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Para adicionar os identificadores de hardware para o Configuration Manager para ignorar  
1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **configuração do Site** > **Sites**.
2. No **home page** separador o **Sites** grupo, escolha **definições de hierarquia**.
3. No **aprovação do cliente e registos em conflito** separador, escolha **adicionar** no **duplicado identificadores de hardware** secção para adicionar os identificadores de hardware novo.

##  <a name="BKMK_PolicyRetrieval"></a> Iniciar a Obtenção de Política para um Cliente do Configuration Manager  
 Um cliente Windows Configuration Manager transfere a política de cliente com base numa agenda configurada como uma definição de cliente. No entanto, poderá haver ocasiões em que pretende para iniciar a obtenção de política a pedido do cliente, por exemplo, para resolução de problemas ou testes.  

Pode iniciar a obtenção de política utilizar:


- [Notificação do cliente](#initiate-client-policy-retrieval-using-client-notification)
- [O **ações** separador no cliente](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Um script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Para obter informações sobre a obtenção de políticas para clientes com Linux e UNIX, veja [Política de computador para servidores Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>Iniciar a obtenção de política de cliente utilizando a notificação do cliente  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **coleções de dispositivos**.  

3.  Selecione a coleção de dispositivos que contém os computadores que pretende transferir a política. No **home page** separador o **coleções** grupo, escolha **notificação do cliente** > **transferir política do computador**.  

    > [!NOTE]  
    >  Também pode utilizar a notificação do cliente para iniciar a obtenção da política para um ou mais dispositivos selecionados apresentados num nó de coleção temporário do nó **Dispositivos** .  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Iniciar manualmente a obtenção de política de cliente no separador ações do cliente do Configuration Manager  

1.  Selecione **Configuration Manager** no Painel de Controlo do computador.  

2.  No **ações** separador, escolha **ciclo de avaliação de obtenção de política de máquina e** para iniciar a política de computador e, em seguida, escolha **executar agora**.  

4.  Escolha **OK** para confirmar a linha de comandos.  

5.  Repita os passos 3 e 4 para outras ações que sejam necessárias, tais como **Ciclo de Obtenção e Avaliação da Política de Utilizador** para definições de cliente do utilizador.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>Iniciar manualmente a obtenção de política de cliente por script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte código do Visual Basic Scripting Edition de exemplo para o ficheiro:  

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

5.  Escolha **OK** no **Windows Script Host** caixa de diálogo.  
