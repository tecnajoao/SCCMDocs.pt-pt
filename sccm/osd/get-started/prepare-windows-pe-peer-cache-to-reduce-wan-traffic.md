---
title: Preparar a cache ponto a ponto do Windows PE para reduzir o tráfego WAN
titleSuffix: Configuration Manager
description: A Cache de ponto a ponto do Windows PE funciona em do PE do Windows para obter o conteúdo de um elemento de rede local e minimizar o tráfego WAN quando não existe nenhum ponto de distribuição local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 804b21733422bd654764f2199fe33d184d54cce4
ms.sourcegitcommit: d021f82e4bc35a8e9b5d291bf779ce52b4f47eb8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656480"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>Preparar a cache ponto a ponto do Windows PE para reduzir o tráfego WAN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando implementa um novo sistema operativo no System Center Configuration Manager, os computadores que executam a sequência de tarefas podem utilizar a Cache ponto a ponto do Windows PE para obter conteúdo de um elemento de rede local (uma origem de cache ponto a ponto) em vez de transferirem conteúdo de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local.  

 A Cache ponto a ponto do Windows PE é semelhante à [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache), mas funciona no ambiente de pré-instalação do Windows (Windows PE). Os termos seguintes são utilizados para descrever os clientes que utilizam a Cache Ponto a Ponto do Windows PE:  

-   Um **cliente de cache ponto a ponto** é um computador que está configurado para utilizar a Cache Ponto a Ponto do Windows PE.  

-   Uma **origem de cache ponto a ponto** é um cliente que está configurado para a cache ponto a ponto e que fornece conteúdo a outros clientes de cache ponto a ponto que pedem esse conteúdo.  

Utilize as secções seguintes para gerir a Cache ponto a ponto.

##  <a name="BKMK_PeerCacheObjects"></a> Objetos armazenados numa origem de Cache Ponto a Ponto  
 Uma sequência de tarefas configurada para utilizar a Cache Ponto a Ponto do Windows PE pode obter os seguintes objetos de conteúdos durante a execução no Windows PE:  

- Imagem do sistema operativo  

- Pacote de controladores  

- Pacotes e programas (quando o cliente continua a executar a sequência de tarefas no sistema operativo completo, o cliente obtém este conteúdo de uma origem de cache ponto a ponto se a sequência de tarefas foi configurada originalmente para a cache ponto a ponto ao executar o Windows PE.)  

- Imagens de arranque adicionais  

  Os objetos de conteúdos seguintes nunca são transferidos com a cache ponto a ponto. Em vez disso, são transferidos de um ponto de distribuição ou pelo Windows BranchCache se tiver configurado o Windows BranchCache no seu ambiente:  

- Aplicações  

- Atualizações de software  

##  <a name="BKMK_PeerCacheWork"></a> Como funciona a Cache Ponto a Ponto do Windows PE?  
 Considere um cenário onde uma sucursal não tem um ponto de distribuição mas tem vários clientes ativados para utilizar a Cache Ponto a Ponto do Windows PE. Implementa a sequência de tarefas configurada para utilizar a cache ponto a ponto em vários clientes que estão configurados para fazer parte da origem da cache ponto a ponto. O primeiro cliente a executar a sequência de tarefas difunde um pedido para um elemento com o conteúdo. Se não encontrar nenhum elemento, obtém o conteúdo a partir de um ponto de distribuição na WAN. O cliente instala a nova imagem e, em seguida, armazena o conteúdo em seu cache de cliente do Configuration Manager para que possa funcionar como uma origem de cache ponto a ponto para outros clientes. Quando o cliente seguinte executar a sequência de tarefas, difunde um pedido na sub-rede para uma origem de cache ponto a ponto e o primeiro cliente responde e torna o seu conteúdo na cache disponível.  

##  <a name="BKMK_PeerCacheDetermine"></a> Determinar os clientes que vão fazer parte da origem da Cache Ponto a Ponto do Windows PE  
 Para ajudar a determinar quais os computadores a selecionar como origem da Cache Ponto a Ponto do Windows PE, deve considerar vários aspetos:  

-   A origem da Cache Ponto a Ponto do Windows PE deve ser um computador de secretária sempre ligado e disponível para os clientes da cache ponto a ponto.  

-   A Cache Ponto a Ponto do Windows PE tem um tamanho de cache de cliente suficiente para armazenar as imagens.  

##  <a name="BKMK_PeerCacheRequirements"></a> Requisitos para um cliente utilizar uma origem de Cache Ponto a Ponto do Windows PE  
 Para os clientes utilizarem uma origem de Cache Ponto a Ponto do Windows PE, têm de cumprir os seguintes requisitos:  

-   O cliente do Configuration Manager tem de ser capaz de comunicar através das seguintes portas na sua rede:  

    -   Porta para a difusão de rede inicial, para encontrar uma origem de cache ponto a ponto. Por predefinição, a porta é 8004.  

    -   Porta para transferência de conteúdos de uma origem de cache ponto a ponto (HTTP e HTTPS). Por predefinição, esta porta é 8003.  

        > [!TIP]  
        >  Os clientes utilizarão HTTPS para transferir conteúdos, quando estiverem disponíveis. No entanto, é utilizado o mesmo número de porta para HTTP ou HTTPS.  

-   [Configure a Cache de Cliente dos Clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache) nos clientes para se certificar de que os mesmos têm espaço suficiente para manter e armazenar as imagens que implementa. A Cache Ponto a Ponto do Windows PE não afeta a configuração ou nem comportamento da cache do cliente.  

-   As opções de implementação para a implementação da sequência de tarefas têm de estar configuradas como Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução.  

##  <a name="BKMK_PeerCacheConfigure"></a> Configurar a Cache Ponto a Ponto do Windows PE  
 Pode utilizar os métodos seguintes para aprovisionar um cliente com conteúdo de cache ponto a ponto, para que possa servir como uma origem de cache ponto a ponto:  

- Um cliente de cache ponto a ponto que não consegue encontrar uma origem de cache ponto a ponto com o conteúdo irá transferir o mesmo de um ponto de distribuição.  Se o cliente recebe as definições de cliente que permitem uma cache ponto a ponto e a sequência de tarefas estiver configurada para preservar o conteúdo da cache, o cliente torna-se numa origem de cache ponto a ponto.  

- Um cliente de cache ponto a ponto pode obter o conteúdo de outro cliente de cache ponto a ponto (uma origem de cache ponto a ponto).  Como o cliente está configurado como uma cache ponto a ponto, quando executa uma sequência de tarefas que está configurada para preservar os conteúdos em cache, o cliente torna-se numa origem de cache ponto a ponto.  

- Um cliente executa uma sequência de tarefas que inclui o passo opcional [Transferir Conteúdo do Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent), que é utilizado para pré-configurar o conteúdo relevante que está incluído na sequência de tarefas da Cache Ponto a Ponto do Windows PE. Quando utiliza este método:  

  -   O cliente não necessita de instalar a imagem que está a ser implementada.  

  -   Além da opção **Transferir Conteúdo do Pacote** , a sequência de tarefas tem também de utilizar a opção **Cache do cliente do Configuration Manager** . O utilizador utiliza esta opção para armazenar conteúdo na cache do cliente para que o cliente possa funcionar como uma origem de cache ponto a ponto para outros clientes de cache ponto a ponto.  

  Os seguintes procedimentos ajudá-lo-ão a configurar a Cache Ponto a Ponto do Windows PE em clientes e a configurar as sequências de tarefas que suporta a cache ponto a ponto.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Para configurar os computadores de origem da Cache Ponto a Ponto do Windows PE  

1. Na consola do Configuration Manager, navegue até **Administration** > **definições de cliente**e, em seguida, crie um novo **definições personalizadas do dispositivo cliente** ou editar um objeto de definições existente. Também pode configurar estas opções para o objeto **Predefinições de Cliente** .  

   > [!TIP]  
   >  Utilize um objeto de definições personalizado para gerir que clientes recebem esta configuração. Por exemplo, é aconselhável evitar esta configuração nos portáteis dos utilizadores que frequentemente trabalham em viagem. Um sistema com elevada mobilidade pode ser uma origem fraca para fornecer conteúdo a outros clientes de cache ponto a ponto.  
   >   
   >  Lembre-se também de que quando configura esta definição como parte das **Predefinições de Cliente**, a configuração aplica-se a todos os clientes do seu ambiente.  

2. Sob **definições de Cache do cliente**, defina **cliente de ativar o Configuration Manager em OS completo partilhem conteúdo** para **Sim**.  

   -   Por predefinição, apenas está ativado HTTP. Se quer permitir que clientes transfiram conteúdo através de HTTPS, defina **Permitir HTTPS para comunicação entre elementos de rede do cliente** como **Sim**.  

   -   Por predefinição, a porta que difunde está definida como a porta 8004 e a porta para transferência de conteúdo está definida como a porta 8003. Pode alterar ambas.  

3. Guarde e implemente as Definições de Cliente nos clientes que selecionou como origem de cache ponto a ponto.  

   Depois de um dispositivo estar configurado com este objeto de definições, o mesmo está configurado para agir como uma origem de cache ponto a ponto. Estas definições devem ser implementadas em potenciais clientes de cache ponto a ponto para configurar as portas e protocolos necessários.  

###  <a name="BKMK_PeerCacheConfigureTS"></a> Configurar uma sequência de tarefas para a Cache Ponto a Ponto do Windows PE  
 Quando configurar uma sequência de tarefas, utilize as seguintes variáveis de sequência de tarefas como Variáveis da Coleção na coleção onde pretende que seja implementada a sequência de tarefas:  

- **SMSTSPeerDownload**  

   Value:  VERDADEIRO  

   Isto permite ao cliente utilizar a Cache Ponto a Ponto do Windows PE.  

- **SMSTSPeerRequestPort**  

   Valor: < número da porta\>  

   Quando não utiliza a porta predefinida configurada nas definições do cliente (8004), tem de configurar esta variável com um valor personalizado da porta de rede a utilizar para a difusão inicial.  

- **SMSTSPreserveContent**  

   Value: VERDADEIRO  

   Este processo sinaliza o conteúdo na sequência de tarefas a ser mantido na cache do cliente do Configuration Manager após a implementação. Isto é diferente de utilizar o smstspersiscontent, que apenas preserva o conteúdo durante a duração da sequência de tarefas e utiliza a cache da sequência de tarefas, não a cache do cliente do Configuration Manager.  

  Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).  

###  <a name="BKMK_PeerCacheValidate"></a> Validar o êxito de utilizar a cache ponto a ponto do Windows PE  
 Depois de utilizar a cache ponto a ponto do Windows PE para implementar e instalar uma sequência de tarefas, pode confirmar que a cache ponto a ponto foi utilizada no processo visualizando o **smsts.log** no cliente que executou a sequência de tarefas.  

 No registo, localize uma entrada semelhante à seguinte em que <*Nomedoservidordeorigem*> identifica o computador do qual o cliente obteve o conteúdo. Este computador deve ser uma origem de cache ponto a ponto e não um servidor de ponto de distribuição. Outros detalhes irão variar com base no seu ambiente e configurações locais.  

-   *<! [LOG [ficheiro transferido de http:// < Nomedoservidordeorigem\>: 8003/SCCM_BranchCache$/SS10000C/SCCM?/Install.wim para c:\\_SMSTaskSequence\Packages\SS10000C\install.wim] LOG]! >< tempo = "14:24:33.329 + 420" data = " 26 de 06-2015 "componente ="ApplyOperatingSystem"context =" "tipo ="1"thread = file="downloadcontent.cpp:1626 "1256" ">*  
