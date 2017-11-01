---
title: "Preparar funções do sistema de sites para implementações de sistemas operativos"
titleSuffix: Configuration Manager
description: "Configure as funções do sistema de site antes de implementar sistemas operativos no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c07172bec1032b021c2d7b7ccaabe33c96b930d2
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Preparar funções do sistema de sites para implementações de sistemas operativos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para implementar sistemas operativos no System Center Configuration Manager, primeiro tem de preparar o seguinte site as funções do sistema que necessitam de considerações e configurações específicas.

##  <a name="BKMK_DistributionPoints"></a> Pontos de distribuição  
 A função do sistema de sites do ponto de distribuição contém ficheiros de origem para os clientes transferirem, como, por exemplo, o conteúdo da aplicação, atualizações de software, imagens do sistema operativo e imagens de arranque. É possível controlar a distribuição de conteúdo utilizando opções de largura de banda, de limitação e de agendamento.  

 É importante que tenha pontos de distribuição suficientes para suportar a implementação de sistemas operativos nos computadores. Também é importante que planeie a disposição destes pontos de distribuição na sua hierarquia. Encontrará maioria destas informações de planeamento em [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). No entanto, existem algumas considerações adicionais de planeamento para pontos de distribuição específicos da implementação do sistema operativo.  

###  <a name="BKMK_AdditionalPlanning"></a> Considerações adicionais de planeamento para pontos de distribuição  
 Seguem-se alguns aspetos de planeamento adicionais a ter em consideração para os pontos de distribuição:  

-   **Como posso impedir a implementações de sistemas operativos indesejados?**  

     Do Configuration Manager não distingue os servidores de site de outros computadores de destino numa coleção. Se implementar uma sequência de tarefas necessária numa coleção que contenha um servidor do site, este último executa a sequência de tarefas da mesma forma que qualquer outro computador da coleção. Certifique-se de que a implementação do sistema operativo utiliza uma coleção que contenha os clientes que pretende que executem a implementação.  

     Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é automaticamente instalada num cliente e tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas com um objetivo Necessário que implemente um sistema operativo. Para reduzir o risco de uma implementação de alto risco indesejada, pode configurar definições de verificação de implementação. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Quantos computadores podem receber uma imagem do sistema operativo em simultâneo a partir de um único ponto de distribuição?**  

     Para calcular o número de pontos de distribuição necessários, tenha em consideração a velocidade de processamento e a E/S de disco do ponto de distribuição, a largura de banda disponível na rede e o efeito que o tamanho do pacote de imagens tem nestes recursos. Por exemplo, numa rede Ethernet de 100 megabytes (MB), o número máximo de computadores para processar um pacote de imagens de 4 gigabytes (GB) numa hora é de 11 computadores, se não forem tidos em consideração outros fatores de recursos do servidor.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Se tiver de implementar um sistema operativo num número específico de computadores num determinado período de tempo, distribua a imagem por um número apropriado de pontos de distribuição.  

-   **Posso implementar um sistema operativo num ponto de distribuição?**  

     Pode implementar um sistema operativo num ponto de distribuição, mas a imagem do sistema operativo tem de ser recebida a partir de um ponto de distribuição diferente.  

###  <a name="BKMK_PXEDistributionPoint"></a> Configurar pontos de distribuição para aceitar pedidos PXE  
 Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, tem de configurar um ou mais pontos de distribuição para aceitar pedidos PXE. Assim que configurar o ponto de distribuição, este irá responder ao pedido de arranque PXE e determinar a ação de implementação adequada a executar.

> [!IMPORTANT]  
>  Os [Serviços de Implementação do Windows](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) têm de ser instalados em todos os pontos de distribuição preparados para PXE.  

 Utilize o procedimento seguinte para modificar um ponto de distribuição existente para que possa aceitar pedidos PXE. Para obter informações sobre como instalar um novo ponto de distribuição, veja [Instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>Para modificar um ponto de distribuição existente para aceitar pedidos PXE  

1.  Na consola do Configuration Manager, clique em **administração**, expanda **descrição geral** e clique em **pontos de distribuição**.  

2.  Selecione o ponto de distribuição que pretende configurar e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

3.  Na página de propriedades do ponto de distribuição, clique em de **PXE** separador e selecione **ativar suporte PXE para clientes** para ativar o PXE deste ponto de distribuição.  

4.  Clique em **Sim** na caixa de diálogo **Analisar as Portas Necessárias para PXE** para confirmar que pretende ativar o PXE. O Configuration Manager configura automaticamente as portas predefinidas uma firewall do Windows. Tem de configurar manualmente as portas se utilizar uma firewall diferente.  

    > [!NOTE]  
    >  Se o WDS e o DHCP estiverem instalados no mesmo servidor, tem de configurar o WDS para escutar numa porta diferente (uma vez que o DHCP escuta na mesma porta). Para obter mais informações, veja [Considerações sobre quando tiver o WDS e DHCP no mesmo servidor](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Selecione **Permitir que este ponto de distribuição responda a pedidos PXE recebidos** para ativar o WDS de modo a que responda a pedidos de serviço PXE recebidos. Pode utilizar esta definição para ativar e desativar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

6.  Selecione **ativar suporte para computadores desconhecidos** para implementar sistemas operativos em computadores que não são geridos pelo Configuration Manager.  

7.  Selecione **Exigir uma palavra-passe quando os computadores utilizam PXE**e, em seguida, especifique uma palavra-passe segura para fornecer segurança adicional à sua implementação PXE.  

8.  Na lista **Afinidade Dispositivo/Utilizador** , escolha como quer que o ponto de distribuição associe os utilizadores ao computador de destino para implementações PXE.  

    -   Selecione **Não utilizar afinidade dispositivo/utilizador** para não associar utilizadores ao computador de destino.  

    -   Selecione **Permitir afinidade dispositivo/utilizador com aprovação manual** para aguardar a aprovação de um utilizador administrativo antes de associar os utilizadores ao computador de destino.  

    -   Selecione **Permitir afinidade dispositivo/utilizador com aprovação automática** para associar automaticamente os utilizadores ao computador de destino sem aguardar aprovação.  

     Para obter mais informações, consulte [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

9. Especifique que o ponto de distribuição responde a pedidos PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se optar por que o ponto de distribuição responda às interfaces de uma rede específica, forneça o endereço MAC para cada interface de rede.  

10. Especifique em segundos o tempo de atraso do ponto de distribuição antes de responder a pedidos do computador quando são utilizados vários pontos de distribuição preparados para PXE.  

11. Clique em **OK** para atualizar as propriedades do ponto de distribuição.  

###  <a name="BKMK_RamDiskTFTP"></a> Personalizar o tamanho do bloco TFTP do disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado  
Pode personalizar o tamanho do bloco TFTP do disco de RAM e a partir do Configuration Manager versão 1606, o tamanho da janela de pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos.   
Terá de testar as definições personalizadas no seu ambiente para determinar o que é mais eficiente.  

-   **Tamanho do bloco TFTP**: O tamanho do bloco é o tamanho dos pacotes de dados que são enviados pelo servidor para o cliente que está a transferir o ficheiro (conforme referido em RFC 2347). Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, tamanhos de bloco maiores resultam em pacotes fragmentados, não suportados pela maioria das implementações de cliente PXE.  

-   **Tamanho da janela de TFTP**: TFTP necessita de um pacote de confirmação (ACK) para cada bloco de dados que são enviados. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. O sistema baseado em janelas do TFTP é uma funcionalidade dos Serviços de Implementação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. O aumento do tamanho desta janela reduz o número de atrasos no percurso de ida e volta entre o cliente e o servidor, e diminui o tempo global que é necessário para transferir uma imagem de arranque.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela de TFTP do disco de RAM  

-   Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

     **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPWindowSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de janela personalizado >  

 O valor predefinido é 1 (1 bloco de dados preenche a janela)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco de TFTP do disco de RAM  

-   Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

     **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPBlockSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de bloco personalizado >  

 O valor predefinido é 4096 (4k).  


###  <a name="BKMK_DPMulticast"></a> Configurar pontos de distribuição para suportarem multicast  
 Multicast é um método de otimização da rede que pode ser utilizado em pontos de distribuição quando se prevê a transferência da mesma imagem do sistema operativo por vários clientes em simultâneo. Quando é utilizado o multicast, a imagem do sistema operativo pode ser transferida em simultâneo por vários computadores à medida que é multidifundida pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente através de uma ligação separada. Para suportar multicast, tem de configurar, pelo menos, um ponto de distribuição. Para obter mais informações, consulte [utilizar multicast para implementar o Windows através da rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Antes de implementar o sistema operativo, tem de configurar um ponto de distribuição para suportar multicast. Utilize o procedimento seguinte para modificar um ponto de distribuição existente para suportar multicast. Para obter informações sobre como instalar um novo ponto de distribuição, consulte [instalar e configurar pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>Para ativar o multicast num ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Descrição geral**e selecione o nó **Pontos de Distribuição** .  

3.  Selecione o ponto de distribuição que pretende utilizar para multidifundir a imagem do sistema operativo.  

4.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Selecione o separador **Multicast** e configure as seguintes opções:  

    -   **Ativar o Multicast**: Tem de selecionar esta opção para o ponto de distribuição suportar multicast.  

    -   **Conta de ligação de multicast**: Especifique uma conta para ligar à base de dados do site.  

    -   **Definições de endereço multicast**: Especifique os endereços IP para enviar dados para os computadores de destino. Por predefinição, o endereço IP é obtido a partir de um servidor DHCP que se encontra ativado para distribuir endereços multicast. Dependendo do ambiente de rede, poderá especificar um intervalo de endereços IP entre 239.0.0.0 e 239.255.255.255.  

        > [!IMPORTANT]  
        >  Estes endereços IP devem ser acessíveis aos computadores de destino que pedem a imagem do sistema operativo. Isto significa que os routers e as firewalls entre o computador de destino e o servidor do site têm de ser configurados para permitir tráfego multicast.  

    -   **Intervalo de portas UDP**: Especifique o intervalo de portas UDP para enviar dados para os computadores de destino.  

        > [!IMPORTANT]  
        >  Estas portas devem ser acessíveis aos computadores de destino que pedem a imagem do sistema operativo. Isto significa que os routers e as firewalls entre o computador de destino e o servidor do site têm de ser configurados para permitir tráfego multicast.  

    -   **Ativar multicast agendado**: Especifique como o Configuration Manager controla quando iniciar a implementação de sistemas operativos em computadores de destino. Clique em **Ativar multicast agendado**e selecione as opções seguintes.  

         No **atraso de início de sessão** caixa, especifique o número de minutos que o Configuration Manager aguarda antes de respondes ao primeiro pedido de implementação.  

         No **tamanho mínimo de sessão** caixa, especifique o número de pedidos deve ser recebido antes de começar a Configuration Manager implementar o sistema operativo.  

    -   **Velocidade de transferência**: Selecione a velocidade de transferência para transferir dados para os computadores de destino.  

    -   **Máximo de clientes**: Especifique o número máximo de computadores de destino que pode transferir o sistema operativo a partir deste ponto de distribuição.  

6.  Clique em **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> Ponto de migração de estado  
 O ponto de migração de estado armazena os dados de estado do utilizador que são capturados num computador e, em seguida, restaurados noutro. No entanto, quando captura definições de utilizador para a implementação de um sistema operativo no mesmo computador, como, por exemplo, uma implementação em que atualiza o sistema operativo no computador de destino, pode escolher se pretende armazenar os dados no mesmo computador através de ligações fixas ou utilizar um ponto de migração de estado. Algumas implementações de computadores, quando cria o armazenamento de Estados, o Configuration Manager cria automaticamente uma associação entre o armazenamento de Estados e o computador de destino. Quando planear o ponto de migração de estado, considere os seguintes fatores.  

### <a name="user-state-size"></a>Tamanho do estado do utilizador  
 O tamanho do estado do utilizador afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do utilizador e o número de computadores a migrar. Considere também as definições a serem migradas do computador. Por exemplo, se já existir uma cópia de segurança da pasta **Os Meus Documentos** num servidor, então é possível que não tenha de a migrar como parte da implementação da imagem. Evite as migrações desnecessárias para reduzir o tamanho geral do estado do utilizador e diminuir o efeito que teria no desempenho da rede e no armazenamento em disco no ponto de migração de estado.  

### <a name="user-state-migration-tool"></a>Ferramenta de migração de estado do utilizador  
 Para capturar e restaurar o estado do utilizador durante a implementação dos sistemas operativos, tem de utilizar o pacote da Ferramenta de Migração de Estado do Utilizador (USMT) que aponta para os ficheiros de origem da USMT. O Configuration Manager cria automaticamente este pacote na consola do Configuration Manager na **biblioteca de Software** > **gestão de aplicações** > **pacotes**. O Configuration Manager utiliza a USMT 10.0, que é distribuído no Windows Assessment and Deployment Kit (Windows ADK) para capturar o estado do utilizador de um sistema operativo e restaurá-lo noutro sistema operativo.  

 Para obter uma descrição dos diferentes cenários de migração com a USMT 10.0, veja [Cenários Comuns de Migração](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Política de retenção  
 Quando configura o ponto de migração de estado, pode especificar o período de tempo para manter os dados de estado do utilizador que estão armazenados no mesmo. O período de tempo para manter os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm no armazenamento em disco.  

-   A potencial necessidade de manter os dados durante algum tempo para o caso de ser necessária uma nova migração dos dados.  

 Migração de estado ocorre em duas fases: Os dados de captura e restauro dos dados. Quando captura dados, os dados de estado do utilizador são recolhidos e guardados no ponto de migração de estado. Quando restaurar os dados, os dados de estado do utilizador são recuperados a partir do ponto de migração de estado, escritos no computador de destino e, em seguida, o passo da sequência de tarefas **Disponibilizar Armazenamento de Estados** disponibiliza os dados armazenados. Quando os dados são disponibilizados, o temporizador de retenção é iniciado. Se selecionar a opção de eliminar imediatamente os dados migrados, os dados de estado do utilizador são eliminados logo que são disponibilizados. Se selecionar a opção de manter os dados por um determinado período tempo, os dados são eliminados quando decorrer esse período de tempo, após a disponibilização dos dados de estado. Quanto mais longo for período de retenção definido, mais espaço em disco poderá ser necessário.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar dados de migração de estado do utilizador  
 Ao configurar o ponto de migração de estado, tem de especificar a unidade do servidor para armazenar os dados de migração de estado do utilizador. Selecione uma unidade numa lista fixa de unidades. No entanto, algumas destas unidades podem não ser graváveis, como a unidade de CD ou uma unidade de partilha exterior à rede. Além disso, algumas letras de unidade podem não estar mapeadas para as unidades do computador. Tem de especificar uma unidade gravável e partilhada quando configurar o ponto de migração de estado.  

### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  
 Poderá utilizar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do utilizador:  

-   Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

-   Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

 Ao utilizar estes assistentes, será solicitado que forneça as seguintes informações sobre o ponto de migração de estado:  

-   As pastas em que os dados de estado do utilizador serão armazenados.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

-   A política de eliminação da função. Poderá especificar que os dados de estado do utilizador sejam eliminados imediatamente ou um número de dias especificado após serem restaurados num computador.  

-   Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Se ativar esta opção, não será possível utilizar o ponto de migração de estado para armazenar os dados de estado do utilizador.  

 Para obter os passos instalar uma função de sistema de sites, consulte [adicionar funções do sistema de sites](../../core/servers/deploy/configure/add-site-system-roles.md).  
