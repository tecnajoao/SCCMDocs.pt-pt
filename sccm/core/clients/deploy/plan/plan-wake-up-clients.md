---
title: Reativação de clientes
titleSuffix: Configuration Manager
description: Planear como reativar clientes no System Center Configuration Manager com o reativação em LAN (WOL).
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ad20f88d6296a45c97e7c04d94624f9341d369e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125981"
---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planear como reativar clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 O Configuration Manager suporta pacotes de reativação tradicionais para reativar os computadores no modo de suspensão quando pretende instalar o software necessário, tal como aplicações e atualizações de software.  

Pode complementar o método de pacotes de reativação tradicional utilizando as definições de cliente de proxy de reativação. Proxy de reativação utiliza um protocolo ponto-a-ponto e computadores selecionados para verificar se outros computadores na sub-rede estão ativos e ativa-os se necessário. Quando o site está configurado para Wake On LAN e os clientes estão configurados para proxy de reativação, o processo funciona da seguinte forma:  

1. Computadores com o cliente do Configuration Manager instalado e que não estão em modo de suspensão no cheque sub-rede se outros computadores na sub-rede estão ativos. Esta verificação que fazem, enviam entre si um comando de ping de TCP/IP cada cinco segundos.  

2. Se não houver nenhuma resposta de outros computadores, os mesmos serão considerados em modo de suspensão. Os computadores que estiverem ativos tornam-se *computador gestor* para a sub-rede.  

    Como é possível que um computador não responder por um motivo que está em modo de suspensão (por exemplo, está desligado, removido da rede ou a definição de cliente do reativação proxy já não é aplicado), será enviado aos computadores um pacote de reativação todos os dias em p 2. M. hora local. Os computadores que não respondem já não serão assumidos em modo de suspensão e não serão reativados a cópia de segurança por um proxy de reativação.  

    Para suportar o proxy de reativação, pelo menos três computadores têm de estar ativo para cada sub-rede. Para alcançar este requisito, três computadores de forma não determinística são escolhidos para ser *computadores responsáveis* para a sub-rede. Este estado significa que eles permaneçam ativos, não obstante qualquer política de energia configurados para o modo de suspensão ou hibernação após um período de inatividade. Computadores responsáveis honrar encerrar ou reiniciar os comandos, por exemplo, como resultado de tarefas de manutenção. Se esta ação acontece, reativação os restantes computadores responsáveis ativarão outro computador na sub-rede, para que a sub-rede continue a ter três computadores responsáveis.  

3. Os computadores gestores solicitam o comutador de rede para redirecionar o tráfego de rede para os computadores em modo de suspensão para si próprios.  

    O redirecionamento é assegurado pelo computador gestor difundir um pacote Ethernet que utiliza o endereço MAC do computador em modo de suspensão como endereço de origem. Esse comportamento faz com que o comutador de rede se comporte como se o computador em modo de suspensão foi movido para a mesma porta que o computador gestor se encontre. O computador gestor também envia pacotes ARP para os computadores em modo de suspensão manter a entrada da cache ARP ATUALIZADA. O computador gestor também responderá aos pedidos ARP o computador e respostas que ela teve com o endereço MAC do computador em modo de suspensão em modo de suspensão.  

   > [!WARNING]  
   >  Durante este processo, o mapeamento de IP para MAC para o computador em modo de suspensão permanece igual. Proxy de reativação funciona informa o comutador de rede que outro adaptador de rede está a utilizar a porta que foi registrada por outra placa de rede. No entanto, esse comportamento é conhecido como uma deflexão de MAC e é invulgar para a operação de rede padrão. Algumas ferramentas de monitorização de rede procuram este comportamento para e podem assumir que algo está errado. Por conseguinte, estas ferramentas de monitorização podem gerar alertas ou encerrar portas quando utilizar o proxy de reativação.  
   >   
   >  Não utilize um proxy de reativação se sua rede, ferramentas e serviços de monitorização não permitirem deflexões de MAC.  

4. Quando o computador gestor Deteta um novo pedido de ligação de TCP para um computador em modo de suspensão e o pedido é uma porta que o computador em modo de suspensão estava a escutar no antes de entrar em suspensão, o computador gestor envia um pacote de reativação para o computador em modo de suspensão e, em seguida, pára redirecionar o tráfego para este computador.  

5. O computador em modo de suspensão recebe o pacote de reativação e é reativado. O computador remetente repetirá automaticamente a ligação e desta vez, o computador é reativado e pode responder.  

   Proxy de reativação tem os seguintes pré-requisitos e limitações:  

> [!IMPORTANT]  
>  Se tiver uma equipa separada responsável pela infraestrutura de rede e serviços de rede, notifique e inclua esta equipa durante sua avaliação e o período de teste. Por exemplo, numa rede que utiliza o controlo de acesso de rede 802.1x, um proxy de reativação não funcionará e poderá interromper o serviço de rede. Além disso, um proxy de reativação pode fazer com que algumas ferramentas para gerar alertas ao detetarem o tráfego para reativar outros computadores de monitorização de rede.  

-   Todos os sistemas de operativos Windows listados como suportado clientes [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportadas para reativação por LAN.  

-   Sistemas operativos convidados que são executados numa máquina virtual não são suportados.  

-   Os clientes tem de estar ativados para um proxy de reativação, utilizando as definições de cliente. Embora a operação de um proxy de reativação não depende de inventário de hardware, os clientes não reportam a instalação do serviço proxy de reativação a menos que estejam ativados para o inventário de hardware e submetido, pelo menos, um inventário de hardware.  

-   Rede adaptadores (e possivelmente o BIOS) tem de ser ativado e configurado para pacotes de reativação. Se o adaptador de rede não estiver configurado para pacotes de reativação ou se esta definição estiver desativada, o Configuration Manager irá configurar automaticamente e ativá-la para um computador ao receber a definição para ativar o proxy de reativação do cliente.  

-   Se um computador tiver mais de um adaptador de rede, não é possível configurar qual a placa a utilizar para o proxy de reativação; a escolha é não determinística. No entanto, a placa selecionada é registada no ficheiro sleepagent _ < domínio\> @SYSTEM_0.log ficheiro.  

-   A rede tem de permitir pedidos de eco ICMP (pelo menos na sub-rede). Não é possível configurar o intervalo de cinco segundos, que é utilizado para enviar os comandos de ping ICMP.  

-   Comunicação é não encriptada e não autenticada e IPsec não é suportado.  

-   Não são suportadas as seguintes configurações de rede:  

    -   802.1x com autenticação de porta  

    -   Redes sem fio  

    -   Comutadores de rede que vinculam endereços MAC para portas específicas  

    -   Redes apenas IPv6  

    -   Durações de concessão DHCP inferiores a 24 horas  

Se pretender reativar computadores para instalação de software agendadas, tem de configurar cada site primário a utilização de pacotes de reativação.  

 Para utilizar um proxy de reativação, tem de implementar definições de cliente de proxy de reativação de gestão de energia para além de configurar o site primário.  

Decida se deve utilizar pacotes de difusão direcionadas ou pacotes unicast bem como o número da porta UDP para utilizar. Por predefinição, os pacotes de reativação tradicionais são transmitidos através da porta UDP 9, mas para ajudar a aumentar a segurança, pode selecionar uma porta alternativa para o site caso esta seja suportada pelos routers e firewalls intervenientes.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Escolher entre Unicast e difusão direcionada para sub-rede para reativação por LAN  
 Se optar por reativar os computadores enviando pacotes de reativação tradicionais, deve decidir se pretende transmitir pacotes unicast ou pacotes de difusão direcionados de sub-rede. Se utilizar um proxy de reativação, tem de utilizar pacotes unicast. Caso contrário, utilize a tabela seguinte para ajudar a determinar o método de transmissão para escolher.  

|Método de transmissão|Vantagem|Desvantagem|  
|-------------------------|---------------|------------------|  
|Unicast|Uma solução mais segura do que as difusões direcionadas porque o pacote é enviado diretamente para um computador em vez de todos os computadores de uma sub-rede.<br /><br /> Não poderá necessitar da reconfiguração dos routers (poderá ter de configurar a cache ARP).<br /><br /> Consome menos largura de banda de rede que transmissões de difusão direcionadas.<br /><br /> Suportado com IPv4 e IPv6.|Dos pacotes de reativação não localizar os computadores de destino que alteraram o respetivo endereço de sub-rede após o último inventário de hardware agendado.<br /><br /> Comutadores poderão ter de ser configurado para reencaminhar os pacotes UDP.<br /><br /> Algumas placas de rede não podem responder a reativação pacotes no modo de suspensão todos os Estados se utilizarem unicast como método de transmissão.|  
|Difusão direcionada para sub-rede|Taxa de êxito superior do unicast se tiver computadores que alteram frequentemente o respetivo endereço de IP na mesma sub-rede.<br /><br /> É necessária a reconfiguração do comutador.<br /><br /> Elevada taxa de compatibilidade com placas de computador para todos os Estados de suspensão, porque difusões direcionadas eram o método de transmissão original para o envio de pacotes de reativação.|Solução menos segura do que o uso unicast, porque um intruso poderia enviar sequências contínuas de pedidos de eco ICMP a partir de um endereço de origem falsificado para o endereço de difusão. Isso faz com que todos os anfitriões respondam a esse endereço de origem. Se os roteadores estão configurados para permitir difusões direcionadas, a configuração adicional é recomendada por motivos de segurança:<br /><br /> -Configure routers para permitirem apenas IP-difusões direcionadas para sub-redes do Gestor de configuração do servidor do site, utilizando um número de porta UDP especificado.<br />-Configure o Configuration Manager para utilizar o número da porta não predefinido especificado.<br /><br /> Poderá necessitar da reconfiguração de todos os routers intervenientes para permitir difusões direcionadas.<br /><br /> Consome mais largura de banda de rede que as transmissões unicast.<br /><br /> Apenas; suportado com IPv4 IPv6 não é suportado.|  

> [!WARNING]  
>  Existem riscos de segurança associados a difusões direcionadas: Um intruso poderia enviar sequências contínuas de pedidos de eco do controle mensagem ICMP (Internet Protocol) de um endereço de origem falsificado para o endereço de difusão, com que todos os anfitriões respondam a esse endereço de origem. Esse tipo de negação de serviço normalmente é chamado de um ataque "smurf" e é normalmente limitado ao não permitir difusões direcionadas.
