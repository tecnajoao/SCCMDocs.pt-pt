---
title: "Reativação de clientes | Documentos do Microsoft"
description: Planear como reativar clientes no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 20f595a5b0634a627dff9ba6feeb848754615f2c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planear como reativar clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 O Configuration Manager suporta duas tecnologias de rede local (LAN) para reativar os computadores em modo de suspensão quando pretende instalar o software necessário, tal como aplicações e atualizações de software de reativação: pacotes de reativação tradicionais e comandos de ativação AMT.  

Poderá complementar o método de pacotes de reativação tradicional utilizando as definições de cliente de proxy de reativação. O proxy de reativação utiliza um protocolo ponto a ponto e computadores selecionados para verificar se outros computadores da sub-rede estão ativos, reativando-os se necessário. Quando o site está configurado para reativação por LAN e os clientes estão configurados para proxy de reativação, o processo funciona do seguinte modo:  

1.  Computadores com o cliente do Configuration Manager instalado e que não estejam em modo de suspensão na sub-rede verificam se outros computadores da sub-rede estão ativos. Para tal, enviam entre si um comando ping de TCP/IP 5 em 5 segundos.  

2.  Se não existir resposta de outros computadores, são considerados em modo de suspensão. Os computadores que estiverem ativos tornam-se *computador gestor* para a sub-rede.  

     Porque é possível que um computador pode não responder por um motivo que está em modo de suspensão (por exemplo, se estiver desligado, removido da rede, ou a definição de cliente do reativação proxy já não é aplicada), será enviado aos computadores um pacote de reativação todos os dias às 14h00 de hora local. Computadores que não responderem deixarão de ser considerados em modo de suspensão e não serão reativados através do proxy de reativação.  

     Para suportar o proxy de reativação, pelo menos três computadores têm de estar ativo em cada sub-rede. Para atingir esse objetivo, três computadores são não determinística optado por ser *computadores responsáveis respeitarão* para a sub-rede. Isto significa que os mesmos permanecerão ativos, apesar de qualquer política de energia configuradas em modo de suspensão ou hibernação após um período de inatividade. Computadores responsáveis respeitarão encerramento ou reinicie comandos, por exemplo, como resultado de tarefas de manutenção. Se isto acontecer, os restantes computadores responsáveis ativarão reativação de outro computador da sub-rede para que a sub-rede continue a dispor de três computadores responsáveis.  

3.  Computadores gestores solicitam ao comutador de rede para redirecionar o tráfego de rede para os computadores em modo de suspensão para si próprios.  

     O redirecionamento é assegurado pelo computador gestor difusão um pacote Ethernet que utiliza o endereço MAC do computador em modo de suspensão como endereço de origem. Isto faz com que o comutador de rede funcionará como se o computador em modo de suspensão tivesse mudado para a mesma porta que o computador gestor se encontre. O computador gestor também envia pacotes ARP para os computadores em modo de suspensão manter a entrada da cache ARP ATUALIZADA. O computador gestor também responderá aos pedidos ARP destinados o computador em modo de suspensão e a responder com o endereço MAC do computador em modo de suspensão.  

    > [!WARNING]  
    >  Durante este processo, o mapeamento de IP para MAC para o computador em modo de suspensão permanecerá igual. O proxy de reativação é funciona informa o comutador de rede que uma placa de rede diferente está a utilizar a porta que se encontrava registada por outra placa de rede. No entanto, este comportamento é conhecido como uma deflexão de MAC e é pouco usual padrão de rede. Algumas ferramentas de monitorização de rede procuram este comportamento para e podem concluir que existe alguma anomalia. Por conseguinte, estas ferramentas de monitorização podem gerar alertas ou encerrar portas quando utilizar o proxy de reativação.  
    >   
    >  Não utilize o proxy de reativação se as suas ferramentas e serviços de monitorização de rede não permitirem deflexões de MAC.  

4.  Quando um computador gestor Deteta um novo pedido de ligação de TCP para um computador em modo de suspensão e o pedido é uma porta que o computador em modo de suspensão estava a escutar no entrou modo de suspensão, o computador gestor envia um pacote de reativação ao computador em modo de suspensão e, em seguida, interrompe o redirecionamento de tráfego para esse computador.  

5.  O computador em modo de suspensão recebe o pacote de reativação e é reativado. O computador repetirá automaticamente a ligação e desta vez, o computador estará ativo e poderá responder.  

 O proxy de reativação tem os seguintes pré-requisitos e limitações:  

> [!IMPORTANT]  
>  Se tiver uma equipa individual que é responsável pela infraestrutura de rede e os serviços de rede, notifique e inclua esta equipa durante a sua avaliação e o período de teste. Por exemplo, numa rede que utiliza o controlo de acesso de rede 802.1 X, o proxy de reativação não funcionará e poderá interromper o serviço de rede. Além disso, o proxy de reativação pode fazer com que algumas ferramentas gerem alertas ao detetarem o tráfego para reativar outros computadores de monitorização de rede.  

-   Os clientes suportados são o Windows 7, Windows 8, Windows Server 2008 R2, Windows Server 2012.  

-   Sistemas operativos convidados que são executados numa máquina virtual não são suportados.  

-   Os clientes tem de estar ativados para o proxy de reativação, utilizando as definições de cliente. Embora o funcionamento do proxy de reativação não depender do inventário de hardware, os clientes não comunicarão a instalação do serviço proxy de reativação a menos que estejam ativados para o inventário de hardware e tenham submetido pelo menos um inventário de hardware.  

-   Rede adaptadores (e possivelmente o BIOS) tem de estar ativadas e configuradas para receberem pacotes de reativação. Se a placa de rede não estiver configurada para pacotes de reativação ou se esta definição estiver desativada, o Configuration Manager irá configurar automaticamente e ativá-lo para um computador quando receber a definição para ativar o proxy de reativação do cliente.  

-   Se um computador tiver mais do que uma placa de rede, não é possível configurar a placa a utilizar para o proxy de reativação; a escolha é não determinística. No entanto, a placa selecionada é registada no ficheiro sleepagent _ < domínio\> @SYSTEM_0.log ficheiro.  

-   A rede tem de permitir pedidos de eco ICMP (pelo menos compreendido pela sub-rede). Não é possível configurar o intervalo que é utilizado para enviar o ICMP, de comandos de ping de 5 segundos.  

-   Comunicações são desencriptadas não autenticadas, e IPsec não é suportado.  

-   As seguintes configurações de rede não são suportadas:  

    -   802.1 X com autenticação de porta  

    -   Redes sem fios  

    -   Comutadores de rede que vinculam endereços MAC a portas específicas  

    -   Redes apenas IPv6  

    -   Durações de concessão DHCP inferiores a 24 horas  

Se pretender reativar computadores para instalações de software agendadas, tem de configurar cada site primário para utilizar pacotes de reativação.  

 Para utilizar o proxy de reativação, tem de implementar definições de cliente de proxy de reativação de gestão de energia para além de configurar o site primário.  

Também tem de decidir se pretende utilizar pacotes de difusão direcionadas para a sub-rede ou pacotes unicast bem como o número de porta UDP pretende utilizar. Por predefinição, os pacotes de reativação tradicionais são transmitidos através da porta UDP 9, mas para ajudar a aumentar a segurança, pode selecionar uma porta alternativa para o site se esta porta alternativa é suportada pelos routers intervenientes e firewalls.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Escolher entre Unicast e difusão direcionada para sub-rede para reativação por LAN  
 Se optar por reativar os computadores enviando pacotes de reativação tradicionais, deverá decidir se pretende transmitir pacotes unicast ou pacotes de difusão direcionados de sub-rede. Se utilizar o proxy de reativação, tem de utilizar pacotes unicast. Caso contrário, utilize a tabela seguinte para ajudar a determinar o método de transmissão adequado.  

|Método de transmissão|Partido|Desvantagens|  
|-------------------------|---------------|------------------|  
|Unicast|Uma solução mais segura que as difusões direcionadas para sub-rede porque o pacote é enviado diretamente para um computador em vez de todos os computadores de uma sub-rede.<br /><br /> Não poderá necessitar da reconfiguração dos routers (poderá ter de configurar a cache ARP).<br /><br /> Consome menos largura de banda de rede que transmissões de difusão direcionadas para sub-redes.<br /><br /> Suportado com IPv4 e IPv6.|Pacotes de reativação não conseguirão localizar os computadores de destino que tenham sido alterados cujo endereço de sub-rede após o último inventário de hardware agendado.<br /><br /> Os comutadores poderão ter de ser configurados para reencaminhar os pacotes UDP.<br /><br /> Algumas placas de rede poderão não responder aos reativação dos Estados de pacotes em todos os modos de suspensão se utilizarem unicast como método de transmissão.|  
|Difusão direcionada para sub-rede|Taxa de êxito superior do unicast se tiver computadores que mudam frequentemente de endereço IP na mesma sub-rede.<br /><br /> Não é necessária nenhuma reconfiguração do comutador.<br /><br /> Elevada taxa de compatibilidade com placas de computador para todos os Estados de suspensão, dado difusões direcionadas para a sub-rede eram o método de transmissão original para o envio dos pacotes de reativação.|Solução menos segura do que utilizar unicast, dado um intruso poderá enviar sequências contínuas de pedidos de eco ICMP a partir de um endereço de origem falsificado para o endereço de difusão. Isto faz com que todos os anfitriões responderão a esse endereço de origem. Se os routers estiverem configurados para permitir difusões direcionadas para a sub-rede, a configuração adicional é recomendada por razões de segurança:<br /><br /> -Configure os routers para permitirem difusões direcionadas apenas IP do Gestor de configuração do servidor do site, através da utilização de um número de porta UDP especificado.<br />-Configure o Configuration Manager para utilizar o número de porta não predefinido especificado.<br /><br /> Poderá necessitar da reconfiguração de todos os routers intervenientes para permitir difusões direcionadas para a sub-rede.<br /><br /> Consome mais largura de banda de rede que as transmissões unicast.<br /><br /> Suportado com IPv4 IPv6 não é suportada.|  

> [!WARNING]  
>  Existem riscos de segurança associados difusões direcionadas para a sub-rede: Um intruso poderá enviar sequências contínuas de pedidos de eco de Internet Control Message Protocol (ICMP) a partir de um endereço de origem falsificado para o endereço de difusão, que fazem com que todos os anfitriões responderão a esse endereço de origem. Este tipo de serviço ataque de recusa de geralmente designado um ataque "smurf" e é normalmente limitado através da não reativação difusões direcionadas para a sub-rede.

