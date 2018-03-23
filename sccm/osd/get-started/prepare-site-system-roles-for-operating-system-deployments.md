---
title: Preparar funções do sistema de sites para OSD
titleSuffix: Configuration Manager
description: Configurar as funções de sistema de sites antes de implementar sistemas operativos
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: ''
caps.handback.revision: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1675f6ed3070972354ea4a14a65339c299ee01f
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Preparar funções do sistema de sites para implementações de sistemas operativos com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para implementar sistemas operativos no Configuration Manager, primeiro tem de preparar o seguinte site as funções do sistema que necessitam de considerações e configurações específicas.



##  <a name="BKMK_DistributionPoints"></a> Pontos de distribuição  
 A função de sistema de sites de ponto de distribuição aloja os ficheiros de origem para os clientes transfiram. Este conteúdo é para aplicações, atualizações de software, imagens SO, imagens de arranque e pacotes de controladores. É possível controlar a distribuição de conteúdo utilizando opções de largura de banda, de limitação e de agendamento.  

 É importante que tenha pontos de distribuição suficientes para suportar a implementação de sistemas operativos nos computadores. Também é importante que planeie para o posicionamento dos seguintes pontos de distribuição na hierarquia. Para obter mais informações, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Este artigo inclui algumas considerações adicionais de planeamento para pontos de distribuição específicos para a implementação do SO.  


###  <a name="BKMK_AdditionalPlanning"></a> Considerações adicionais de planeamento para pontos de distribuição  
 Os seguintes itens são aspetos a considerar para pontos de distribuição de planeamento adicionais:  

-   **Como impedir a implementações de SO indesejadas?**  

     O Configuration Manager não distinguir servidores do site de outros computadores de destino numa coleção. Se implementar uma sequência de tarefas necessária numa coleção que inclui um servidor de site, é executada a sequência de tarefas da mesma forma como qualquer outro computador na coleção. Certifique-se de que a sua implementação do sistema operativo utiliza uma coleção que inclua os clientes que se destinam.  

     Gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é automaticamente instalada num cliente e tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas com um objetivo de obrigatório que implementa o sistema operativo. Para reduzir o risco de uma implementação de alto risco indesejada, configure definições de verificação de implementação. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Quantos computadores podem receber uma imagem do SO em simultâneo de um único ponto de distribuição?**  

     Estimar quantos pontos de distribuição necessários, considere as seguintes variáveis:  
       - A velocidade de processamento do ponto de distribuição
       - A velocidade do disco do ponto de distribuição
       - A largura de banda disponível na rede
       - O tamanho do pacote de imagem   
  
    Por exemplo, se não considerar qualquer outro servidor fatores de recursos, o número máximo de computadores que pode processar um pacote de imagem de quatro gigabyte (GB) numa hora numa rede de Ethernet de 100-megabit por segundo é de 11 computadores.  

    `100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

    Se tiver de implementar o sistema operativo num número específico de computadores num determinado tempo, distribua a imagem por um número apropriado de pontos de distribuição.  

-   **Pode implementar um sistema para um ponto de distribuição?**  

     Pode implementar o sistema operativo para um ponto de distribuição, mas a imagem do SO deve ser recebida a partir de um ponto de distribuição diferente.  


###  <a name="BKMK_PXEDistributionPoint"></a> Configurar pontos de distribuição para aceitar pedidos PXE  
 Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, tem de configurar um ou mais pontos de distribuição para aceitar pedidos PXE. Depois de configurar o ponto de distribuição, responde a pedidos de arranque PXE e determina a ação de implementação adequada a tomar. Para obter mais informações, consulte [instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe).  


###  <a name="BKMK_RamDiskTFTP"></a> Personalizar os tamanhos de bloco e a janela de TFTP do disco de RAM em pontos de distribuição com PXE ativado  
Pode personalizar os tamanhos de bloco e a janela de TFTP do disco de RAM para pontos de distribuição com PXE ativado. Se tiver personalizado a rede, um tamanho de bloco ou da janela grande causam a transferência da imagem de arranque falhe, com um erro de tempo limite. As personalizações de tamanho de bloco e a janela de TFTP do disco de RAM permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os requisitos de rede específicos. Para determinar que configuração é mais eficiente, teste as definições personalizadas no seu ambiente.  

-   **Tamanho do bloco TFTP**: O tamanho do bloco é o tamanho dos pacotes de dados que o servidor envia ao cliente que está a transferir o ficheiro. Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, um tamanho de bloco maiores oportunidades potenciais pacotes fragmentados, que não suportam a maioria das implementações de cliente PXE.  

-   **Tamanho da janela de TFTP**: TFTP necessita de um pacote de confirmação (ACK) para cada bloco de dados que são enviados. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. Modos de janela TFTP permite-lhe definir quantos blocos de dados demora para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. Se aumentar o tamanho desta janela, reduz o número de atrasos reportadas round-trip entre o cliente e o servidor e -diminui o tempo geral necessário para transferir uma imagem de arranque.  
  


#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificar o tamanho da janela de TFTP do disco de RAM  
Para personalizar o tamanho da janela de TFTP do disco de RAM, adicione a seguinte chave de registo em pontos de distribuição com PXE ativado:  

  - **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  - **Nome**: RamDiskTFTPWindowSize  
  - **Tipo**: REG_DWORD  
  - **Valor**: &lt;tamanho de janela personalizado >  </br>
     O valor predefinido é **1** (um bloco de dados preenche a janela)  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificar o tamanho do bloco TFTP do disco de RAM  
Para personalizar o tamanho da janela de TFTP do disco de RAM, adicione a seguinte chave de registo em pontos de distribuição com PXE ativado:  

  - **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  - **Nome**: RamDiskTFTPBlockSize  
  - **Tipo**: REG_DWORD  
  - **Valor**: &lt;tamanho de bloco personalizado >  </br>
     O valor predefinido é **4096**.  


###  <a name="BKMK_DPMulticast"></a> Configurar pontos de distribuição para suportarem multicast  
 Multicast é um método de otimização de rede. Pode utilizá-lo em pontos de distribuição quando se prevê a transferência da mesma imagem do SO em simultâneo por vários clientes. Quando utilizar o multicast, vários computadores em simultâneo podem transferir a imagem do SO, que é multidifundida pelo ponto de distribuição. Sem multicast, o ponto de distribuição envia uma cópia dos dados para cada cliente através de uma ligação separada. Para obter mais informações, consulte [utilizar multicast para implementar o Windows através da rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Antes de implementar o sistema operativo, configure um ponto de distribuição para suportar multicast. Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).


##  <a name="BKMK_StateMigrationPoints"></a> Ponto de migração de estado  
 O ponto de migração de estado armazena dados de estado de utilizador que USMT captura num computador e, em seguida, restaura noutro computador. No entanto, quando captura definições de utilizador para uma implementação do SO no mesmo computador, como uma implementação em que atualiza o Windows no computador de destino, pode escolher se pretende armazenar os dados no mesmo computador, utilizando ligações fixas ou utilizar um ponto de migração de estado . Algumas implementações de computadores, quando cria o armazenamento de Estados, o Configuration Manager cria automaticamente uma associação entre o armazenamento de Estados e o computador de destino. Quando planear para o ponto de migração de estado, considere os seguintes fatores:    

### <a name="user-state-size"></a>Tamanho do estado do utilizador  
 O tamanho do estado do utilizador afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do utilizador e o número de computadores a migrar. Considere também as definições a serem migradas do computador. Por exemplo, se o **os meus documentos** pasta já cópias de segurança para um servidor, em seguida, talvez não tiver a migrar como parte da implementação da imagem. Evite as migrações desnecessárias mantém o tamanho geral do Estado de utilizador mais pequenos e diminui o efeito que teria no armazenamento de disco e de desempenho de rede no ponto de migração de estado.  

### <a name="user-state-migration-tool"></a>Ferramenta de migração de estado do utilizador  
 Para capturar e restaurar o estado do utilizador durante a implementação dos sistemas operativos, tem de utilizar o pacote da Ferramenta de Migração de Estado do Utilizador (USMT) que aponta para os ficheiros de origem da USMT. O Configuration Manager cria automaticamente este pacote na consola do Configuration Manager na **biblioteca de Software** > **gestão de aplicações** > **pacotes**. O Configuration Manager utiliza o USMT 10 capturar o estado de utilizador de um SO e, em seguida, restaurá-lo para outro. O Windows Assessment and Deployment Kit (Windows ADK) para Windows 10 inclui o USMT 10.

 Para obter uma descrição dos diferentes cenários migração para o USMT 10, consulte [cenários comuns de migração](/windows/deployment/usmt/usmt-common-migration-scenarios) na documentação do Windows.  

### <a name="retention-policy"></a>Política de retenção  
 Quando configura o ponto de migração de estado, especifique o período de tempo para manter os dados de estado de utilizador que armazena. O período de tempo para manter os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm no armazenamento em disco.  

-   A potencial necessidade de manter os dados durante algum tempo para o caso de ser necessária uma nova migração dos dados.
  
  
Migração de estado ocorre em duas fases: captura e restauro dos dados. Quando captura dados, os dados de estado do utilizador são recolhidos e guardados no ponto de migração de estado. Quando restaurar os dados, os dados de estado do utilizador são recuperados a partir do ponto de migração de estado, escritos no computador de destino e, em seguida, o passo da sequência de tarefas **Disponibilizar Armazenamento de Estados** disponibiliza os dados armazenados. Quando os dados são disponibilizados, o temporizador de retenção é iniciado. Se selecionar a opção para eliminar imediatamente os dados migrados, os dados de estado do utilizador são eliminados assim que for lançada. Se selecionar a opção de manter os dados por um determinado período tempo, os dados são eliminados quando decorrer esse período de tempo, após a disponibilização dos dados de estado. Mais tempo, definir a retenção período, o espaço em disco adicional está necessária.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar dados de migração de estado do utilizador  
 Ao configurar o ponto de migração de estado, tem de especificar a unidade do servidor para armazenar os dados de migração de estado do utilizador. Selecione uma unidade numa lista fixa de unidades. No entanto, algumas destas unidades podem não ser graváveis, como a unidade de CD ou uma unidade de partilha exterior à rede. Algumas letras de unidade podem não estar mapeadas para as unidades do computador. Especifique uma unidade gravável e partilhada quando configurar o ponto de migração de estado.  

### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  
 Poderá utilizar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do utilizador:  

-   Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

-   Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

 Quando utiliza estes assistentes, é-lhe pedido que forneça as seguintes informações para o ponto de migração de estado:  

-   As pastas em que os dados de estado do utilizador serão armazenados.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

-   A política de eliminação da função. Especificar que os dados de estado do utilizador sejam eliminados imediatamente é restaurada num computador, ou após um número de dias após o restauro de dados do utilizador num computador específico.  

-   Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Se ativar esta opção, não será possível utilizar o ponto de migração de estado para armazenar os dados de estado do utilizador.  

 Para obter os passos instalar uma função de sistema de sites, consulte [adicionar funções do sistema de sites](../../core/servers/deploy/configure/add-site-system-roles.md).  
