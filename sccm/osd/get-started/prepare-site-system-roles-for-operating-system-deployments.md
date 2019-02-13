---
title: Preparar funções do sistema de sites para OSD
titleSuffix: Configuration Manager
description: Configurar as funções de sistema de sites antes de implementar sistemas operativos no Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c7f54ccda217ebbae543b70aeead37f6c55cf0f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125692"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Preparar funções do sistema de sites para implementações de sistema operacional com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para implementar sistemas operativos no Configuration Manager, primeiro prepare o seguinte site funções do sistema que exigem considerações e configurações específicas.



##  <a name="BKMK_DistributionPoints"></a> Pontos de distribuição  

A função de sistema de sites de ponto de distribuição aloja os ficheiros de origem para os clientes transferirem. Este conteúdo destina-se a aplicações, atualizações de software, imagens SO, imagens de arranque e pacotes de controladores. Controlar a distribuição de conteúdo utilizando opções de limitação e de agendamento, largura de banda.  

É importante que tem pontos de distribuição suficientes para suportar a implementação de sistemas operativos nos computadores. Também é importante que planeie a disposição destes pontos de distribuição na hierarquia. Para obter mais informações, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure). Este artigo inclui algumas considerações adicionais de planeamento para pontos de distribuição específicos para implementação do SO.  


###  <a name="BKMK_AdditionalPlanning"></a> Considerações adicionais de planeamento para pontos de distribuição  

Os seguintes itens são coisas a serem considerados para pontos de distribuição de planeamento adicionais:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Como posso impedir a implementações de sistema operacional indesejadas?  
O Configuration Manager não distingue os servidores de site de outros computadores de destino numa coleção. Se implementar uma sequência de tarefas necessária numa coleção que inclui um servidor de site, ele executa a sequência de tarefas da mesma forma como qualquer outro computador na coleção. Certifique-se de que a implementação do sistema operacional utiliza uma coleção que inclua os clientes pretendidos.  

Gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é automaticamente instalada num cliente e tem o potencial de causar resultados indesejados. Por exemplo, a existência de uma sequência de tarefas com um objetivo de obrigatório que implementa um sistema operacional. Para reduzir o risco de uma implementação de alto risco indesejada, configure definições de verificação de implementação. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Quantos computadores podem receber uma imagem de SO de uma só vez a partir de um ponto de distribuição único?  
Para calcular a quantos pontos de distribuição necessários, considere as seguintes variáveis:  
- A velocidade de processamento do ponto de distribuição
- Velocidade do disco do ponto de distribuição
- A largura de banda disponível na rede
- O tamanho do pacote de imagem   
  
Por exemplo, se não considerar qualquer outro servidor fatores de recursos, o número máximo de computadores para processar um pacote de imagem de 4 GB dentro de uma hora numa rede de Ethernet de 100-megabit/seg é de 11 computadores.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Se tiver de implementar um sistema operacional para um número específico de computadores num determinado período de tempo, distribua a imagem por um número apropriado de pontos de distribuição.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Pode implementar um sistema operacional para um ponto de distribuição?  
Pode implementar um sistema operacional para um ponto de distribuição, mas a imagem do SO têm de ser recebida de um ponto de distribuição diferente.  


###  <a name="BKMK_PXEDistributionPoint"></a> Configurar pontos de distribuição para aceitar pedidos PXE  

Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, configure um ou mais pontos de distribuição para aceitar pedidos PXE. Depois de configurar o ponto de distribuição, ele responde a pedidos de arranque PXE e determina a ação de implementação adequada a tomar. Para mais informações, consulte [Install or modify a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  


###  <a name="BKMK_RamDiskTFTP"></a> Personalizar os tamanhos de bloco e janela de TFTP do disco de RAM em pontos de distribuição com PXE ativado  

Pode personalizar os tamanhos de bloco e a janela de TFTP de Ramdisk baseada em pontos de distribuição com PXE ativado. Se personalizou sua rede, um tamanho de bloco ou da janela grandes pode causar falha com um erro de tempo limite a transferência da imagem de arranque. As personalizações de tamanho de bloco e a janela de TFTP de RamDisk permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os seus requisitos de rede específicas. Para determinar que configuração é mais eficiente, teste as definições personalizadas no seu ambiente.  

-   **Tamanho do bloco TFTP**: O tamanho do bloco é o tamanho dos pacotes de dados que o servidor envia ao cliente que está a transferir o ficheiro. Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, um tamanho de bloco maiores nos leva a pacotes fragmentados, a maioria das implementações de cliente PXE nepodporují.  

-   **Tamanho da janela TFTP**: TFTP necessita de um pacote de confirmação (ACK) para cada bloco de dados que são enviados. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. Janelas do TFTP permite-lhe definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. Se aumentar o tamanho desta janela, reduz o número de atrasos de ida e volta entre o cliente e servidor e ela diminui o tempo geral necessário para transferir uma imagem de arranque.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificar o tamanho da janela de TFTP do disco  
Para personalizar o tamanho da janela de TFTP de RamDisk, adicione a seguinte chave de registo em pontos de distribuição com PXE ativado:  

- **Localização**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPWindowSize  
- **Tipo de**: REG_DWORD  
- **Valor**: (tamanho de janela personalizado)  
    - O valor predefinido é **1** (um bloco de dados preenche a janela).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificar o tamanho do bloco TFTP do disco  
Para personalizar o tamanho da janela de TFTP de RamDisk, adicione a seguinte chave de registo em pontos de distribuição com PXE ativado:  

- **Localização**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPBlockSize  
- **Tipo de**: REG_DWORD  
- **Valor**: (tamanho de bloco personalizado)  
    - O valor predefinido é **4096**.  

> [!Note]  
> Serviços de implantação do Windows e o serviço de resposta de PXE do Configuration Manager suportam essas configurações de TFTP.  


###  <a name="BKMK_DPMulticast"></a> Configurar pontos de distribuição para suportarem multicast  

Multicast é um método de otimização de rede. Utilize-o em pontos de distribuição quando se prevê a transferência da mesma imagem do sistema operacional em simultâneo por vários clientes. Quando for utilizado multicast, vários computadores podem transferir em simultâneo a imagem do SO como multicast de, pelo ponto de distribuição. Sem multicast, o ponto de distribuição envia uma cópia dos dados para cada cliente através de uma ligação separada. Para obter mais informações, consulte [utilizar multicast para implementar o Windows através da rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

Antes de implementar o sistema operacional, configure um ponto de distribuição para suportar multicast. Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast).



##  <a name="BKMK_StateMigrationPoints"></a> Ponto de migração de estado  

O ponto de migração de estado armazena dados de perfil do usuário que a USMT captura num computador e, em seguida, restaura noutro computador. No entanto, quando captura definições de utilizador para uma implementação de sistema operacional no mesmo computador, como uma implementação em que atualiza o Windows no computador de destino, pode escolher se pretende armazenar os dados no mesmo computador, utilizando ligações fixas ou utilizar um ponto de migração de estado . Algumas implementações de computadores, quando cria o arquivo de estado, o Configuration Manager automaticamente cria uma associação entre o armazenamento de Estados e o computador de destino. Quando planear para o ponto de migração de estado, considere os seguintes fatores:    


### <a name="user-state-size"></a>Tamanho do estado do utilizador  

O tamanho do estado do utilizador afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do utilizador e o número de computadores a migrar. Considere também as definições a serem migradas do computador. Por exemplo, se o **meus documentos** pasta já foi efetuada para um servidor, em seguida, talvez não precisa migrar como parte da implementação da imagem. Evite as migrações desnecessárias mantém o tamanho geral do Estado do utilizador menores e reduz o efeito que teria no armazenamento de disco e desempenho de rede no ponto de migração de estado.  


### <a name="user-state-migration-tool"></a>Ferramenta de migração de estado do utilizador  

Para capturar e restaurar o estado do utilizador durante a implantação dos sistemas operativos, utilize um pacote da ferramenta de migração de perfil do usuário (USMT) que aponta para os ficheiros de origem USMT. Gestor de configuração cria automaticamente este pacote na consola do Configuration Manager no **biblioteca de Software** > **gestão de aplicações**  >   **Pacotes**. O Configuration Manager utiliza o USMT 10 para capturar o estado do utilizador de um SO e, em seguida, restaurá-lo para outro. A avaliação do Windows e o Deployment Kit (Windows ADK) para Windows 10 inclui o USMT 10.

Para obter uma descrição dos diferentes cenários migração para o USMT 10, veja [cenários comuns de migração](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) na documentação do Windows.  


### <a name="retention-policy"></a>Política de retenção  

Quando configurar o ponto de migração de estado, especifique o período de tempo para manter os dados de estado de utilizador que armazena. O período de tempo para manter os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm no armazenamento em disco.  

-   A potencial necessidade de manter os dados durante algum tempo para o caso de ser necessária uma nova migração dos dados.  
  
  
Migração de estado ocorre em duas fases: captura de dados e restauro dos dados. Quando captura dados, os dados de estado do utilizador são recolhidos e guardados no ponto de migração de estado. Quando restaurar os dados, os dados de estado do utilizador são recuperados a partir do ponto de migração de estado, escritos no computador de destino e, em seguida, o passo da sequência de tarefas **Disponibilizar Armazenamento de Estados** disponibiliza os dados armazenados. Quando os dados são disponibilizados, o temporizador de retenção é iniciado. Se selecionar a opção de eliminar imediatamente os dados migrados, os dados de estado do utilizador são eliminados quando for lançada. Se selecionar a opção de manter os dados por um determinado período tempo, os dados são eliminados quando decorrer esse período de tempo, após a disponibilização dos dados de estado. Mais tempo definir o período de retenção período, o mais espaço em disco que provavelmente exigir.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar dados de migração de estado do utilizador  

Quando configurar o ponto de migração de estado, especifique a unidade do servidor para armazenar os dados de migração de estado do utilizador. Selecione uma unidade numa lista fixa de unidades. No entanto, algumas destas unidades podem não ser graváveis, como a unidade de CD ou uma unidade de partilha exterior à rede. Algumas letras de unidade podem não estar mapeadas para as unidades do computador. Especifique uma unidade gravável e partilhada quando configurar o ponto de migração de estado.  


### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  

Utilize os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado de utilizador:  

-   Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

-   Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

Quando utilizar estes assistentes, lhe for pedido para fornecer as seguintes informações para o ponto de migração de estado:  

-   As pastas em que os dados de estado do utilizador serão armazenados.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

-   A política de eliminação da função. Especificar que os dados de estado do utilizador são eliminados imediatamente após o restauro, num computador, ou após um número específico de dias após os dados de utilizador são restaurados num computador.  

-   Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Quando ativa esta opção, não é possível utilizar o ponto de migração de estado para armazenar dados de estado do utilizador.  

Para obter os passos instalar uma função de sistema de sites, consulte [adicionar funções do sistema de sites](/sccm/core/servers/deploy/configure/add-site-system-roles).  
