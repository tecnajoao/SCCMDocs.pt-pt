---
title: "Reativação de clientes | Microsoft Docs"
description: Planeie como pretende reativar os clientes no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 20f595a5b0634a627dff9ba6feeb848754615f2c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planeie como pretende reativar os clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Suporte do Configuration Manager dois reativação tecnologias de rede de área local (LAN) para reativar os computadores no modo de suspensão quando pretende instalar o software necessário, tal como aplicações e atualizações de software: pacotes de reativação tradicionais e comandos de ativação AMT.  

Poderá complementar o método de pacote de reativação tradicional utilizando as definições de cliente de proxy de reativação. Proxy de reativação utiliza um protocolo ponto a ponto e computadores selecionados para verificar se outros computadores na sub-rede estão ativos e ativa-os se necessário. Quando o site está configurado para Wake On LAN e os clientes são configurados para proxy de reativação, o processo funciona da seguinte forma:  

1.  Computadores com o cliente do Configuration Manager instalado e que não estejam em modo de suspensão na verificação de sub-rede se outros computadores na sub-rede estão ativos. Tal, enviam entre si um comando ping de TCP/IP a cada cinco segundos.  

2.  Se não houver nenhuma resposta de outros computadores, os mesmos serão considerados em modo de suspensão. Os computadores que estiverem ativos tornam-se *computador gestor* para a sub-rede.  

     Porque é possível que um computador pode não responder por um motivo que está em modo de suspensão (por exemplo, se estiver desligado, removido da rede, ou a definição de cliente do reativação proxy já não é aplicado), será enviado aos computadores um pacote de reativação todos os dias às 13h00 e 14h00 hora local. Os computadores que não responderem já não irão ser considerados como estando em modo de suspensão e não serão reativados por proxy de reativação.  

     Para suportar o proxy de reativação, pelo menos três computadores têm de estar ativo para cada sub-rede. Para atingir esse objetivo, três computadores não determinística são escolhidos ser *computadores responsáveis* para a sub-rede. Isto significa que, ficam ativos, independentemente de qualquer política de energia configurados no modo de suspensão ou hibernação após um período de inatividade. Computadores responsáveis honrar encerrar ou reiniciar os comandos, por exemplo, como resultado de tarefas de manutenção. Se isto acontecer, os restantes computadores responsáveis ativarão reativação de outro computador na sub-rede para que a sub-rede continue a ter três computadores responsáveis.  

3.  Computadores gestores solicitam ao comutador de rede para redirecionar o tráfego de rede para os computadores em modo de suspensão para si próprios.  

     O redirecionamento é assegurado pelo computador gestor difundir uma moldura de Ethernet que utiliza o endereço MAC do computador em modo de suspensão como endereço de origem. Isto torna o comutador de rede se comporte como se o computador em modo de suspensão foi movido para a mesma porta que o computador gestor está ligado. O computador gestor também envia pacotes ARP para os computadores em modo de suspensão manter a entrada da cache ARP ATUALIZADA. O computador gestor também responderá aos pedidos ARP destinados o computador em modo de suspensão e a resposta com o endereço MAC do computador em modo de suspensão.  

    > [!WARNING]  
    >  Durante este processo, o mapeamento de IP para MAC para o computador em modo de suspensão não foi alterada. Funciona do proxy de reativação informa o comutador de rede que outro adaptador de rede está a utilizar a porta que se encontrava registada por outra placa de rede. No entanto, este comportamento é conhecido como uma deflexão de MAC e invulgar para a operação de rede padrão. Algumas ferramentas de monitorização de rede procuram este comportamento para e podem assumir que algo está errado. Por conseguinte, estas ferramentas de monitorização podem gerar alertas ou encerrar portas quando utilizar o proxy de reativação.  
    >   
    >  Não utilize um proxy de reativação se a monitorização ferramentas e serviços de rede não permitirem deflexões de MAC.  

4.  Quando o computador gestor Deteta um novo pedido de ligação de TCP para um computador em modo de suspensão e o pedido é para uma porta que o computador em modo de suspensão estava a escutar no entrou em suspensão, o computador gestor envia um pacote de reativação para o computador em modo de suspensão e, em seguida, interrompe a redirecionar o tráfego para este computador.  

5.  O computador em modo de suspensão recebe o pacote de reativação e é reativado. O computador tenta automaticamente repete a ligação e desta vez, o computador é reativado e pode responder.  

 Proxy de reativação tem os seguintes pré-requisitos e limitações:  

> [!IMPORTANT]  
>  Se tiver uma equipa separada responsável pela infraestrutura de rede e os serviços de rede, notifique e inclua esta equipa durante a avaliação e período de teste. Por exemplo, numa rede que utiliza o controlo de acesso de rede 802.1 X, proxy de reativação não funcionará e poderá interromper o serviço de rede. Além disso, o proxy de reativação pode fazer com que algumas ferramentas gerem alertas ao detetarem o tráfego para reativar outros computadores da monitorização de rede.  

-   Os clientes suportados são o Windows 7, Windows 8, Windows Server 2008 R2, Windows Server 2012.  

-   Sistemas operativos convidados que são executados numa máquina virtual não são suportados.  

-   Os clientes tem de estar ativados para proxy de reativação, utilizando as definições de cliente. Embora o funcionamento do proxy de reativação não depender de inventário de hardware, os clientes não comunicarão a instalação do serviço proxy de reativação, a menos que estejam ativados para o inventário de hardware e submetido pelo menos um inventário de hardware.  

-   Rede adaptadores (e possivelmente o BIOS) tem de ser ativado e configurado para pacotes de reativação. Se o adaptador de rede não estiver configurado para pacotes de reativação ou se esta definição estiver desativada, o Configuration Manager irá configurar automaticamente e ativá-la para um computador quando receber a definição para ativar o proxy de reativação do cliente.  

-   Se um computador tiver mais do que um adaptador de rede, não é possível configurar qual a placa a utilizar para um proxy de reativação; a escolha é não determinística. No entanto, a placa selecionada é registada no SleepAgent_ < domínio\> @SYSTEM_0.log ficheiro.  

-   A rede tem de permitir pedidos de eco ICMP (pelo menos dentro da sub-rede). Não é possível configurar os intervalo que é utilizado para enviar o ICMP comandos ping de 5 segundos.  

-   Comunicação é não encriptada, não autenticada e IPsec não é suportado.  

-   Não são suportadas as seguintes configurações de rede:  

    -   802.1 X com autenticação de porta  

    -   Redes sem fios  

    -   Comutadores de rede que vinculam endereços MAC a portas específicas  

    -   Redes apenas IPv6  

    -   Durações de concessão DHCP inferiores a 24 horas  

Se pretender reativar computadores para instalação de software agendadas, tem de configurar cada site primário a utilização de pacotes de reativação.  

 Para utilizar o proxy de reativação, tem de implementar definições de cliente de proxy de reativação de gestão de energia para além de configurar o site primário.  

Também tem de decidir se deve utilizar pacotes de difusão direcionadas para a sub-rede ou pacotes unicast e o número da porta UDP para utilizar. Por predefinição, os pacotes de reativação tradicionais são transmitidos através da porta UDP 9, mas para ajudar a aumentar a segurança, pode selecionar uma porta alternativa para o site se esta porta alternativa é suportada pelo routers e firewalls intervenientes.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Escolher entre Unicast e difusão direcionada para sub-rede para reativação por LAN  
 Se optar por reativar os computadores enviando pacotes de reativação tradicionais, terá de decidir se pretende transmitir pacotes unicast ou pacotes de difusão direcionados de sub-rede. Se utilizar um proxy de reativação, tem de utilizar pacotes unicast. Caso contrário, utilize a tabela seguinte para o ajudar a determinar o método de transmissão a escolha.  

|Método de transmissão|Partido|Desvantagens|  
|-------------------------|---------------|------------------|  
|Unicast|Uma solução mais segura que difusões direcionadas por sub-rede porque o pacote é enviado diretamente para um computador em vez de todos os computadores de uma sub-rede.<br /><br /> Não poderá necessitar da reconfiguração dos routers (poderá ter de configurar a cache ARP).<br /><br /> Consome menos largura de banda de rede que as transmissões de difusão direcionadas para a sub-rede.<br /><br /> Suportado com IPv4 e IPv6.|Pacotes de reativação não localizar computadores de destino que alteraram os seus endereços de sub-rede após o último inventário de hardware agendado.<br /><br /> Os comutadores poderão ter de ser configurada para reencaminhar os pacotes UDP.<br /><br /> Algumas placas de rede não podem responder a reativação pacotes no modo de suspensão todos os Estados se utilizarem unicast como método de transmissão.|  
|Difusão direcionada para sub-rede|Taxa de êxito superior do unicast se tiver computadores que mudam frequentemente de endereço IP na mesma sub-rede.<br /><br /> É necessária a reconfiguração do comutador.<br /><br /> Elevada taxa de compatibilidade com placas de computador para todos os Estados de suspensão, porque difusões direcionadas por sub-rede eram o método de transmissão original para o envio de pacotes de reativação.|Solução menos segura do que utilizar unicast porque um intruso poderia enviar sequências contínuas de pedidos de eco ICMP a partir de um endereço de origem falsificado para o endereço de difusão. Isto faz com que todos os anfitriões respondam a esse endereço de origem. Se os routers estiverem configurados para permitir difusões direcionadas por sub-rede, a configuração adicional é recomendada por razões de segurança:<br /><br /> -Configure os routers para permitirem difusões apenas direcionadas para o IP do Gestor de configuração do servidor do site, utilizando um número de porta UDP especificado.<br />-Configure o Configuration Manager para utilizar o número da porta não predefinido especificado.<br /><br /> Poderá necessitar da reconfiguração de todos os routers intervenientes para permitir difusões direcionadas por sub-rede.<br /><br /> Consome mais largura de banda de rede que as transmissões unicast.<br /><br /> Suportado com IPv4 apenas; IPv6 não é suportado.|  

> [!WARNING]  
>  Existem riscos de segurança associados a difusões direcionadas para: Um intruso poderia enviar sequências contínuas de pedidos de eco Internet Control Message Protocol (ICMP) de um endereço de origem falsificado para o endereço de difusão, com que todos os anfitriões respondam a esse endereço de origem. Este tipo de serviço de ataque de recusa de geralmente é designada por um ataque "smurf" e é normalmente limitado por não permitir difusões direcionadas por sub-rede.
