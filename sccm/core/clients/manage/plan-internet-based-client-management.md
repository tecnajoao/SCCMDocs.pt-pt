---
title: Gestão de clientes baseada na Internet
titleSuffix: Configuration Manager
description: Crie um plano para gerir clientes baseados na Internet no System Center Configuration Manager.
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f4de7295075de4b5baa5e7ba3fa1a3aea2ec032
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>Planear a gestão de clientes baseados na Internet no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Permite de gestão (algumas vezes referido como IBCM) de clientes baseados na Internet que gere o System Center Configuration Manager quando não estiverem ligados à sua empresa de clientes de rede, mas tem uma ligação padrão à Internet. Este esquema apresenta diversas vantagens, incluindo a redução de custos associada à não execução de redes privadas virtuais (VPNs) e à capacidade de implementar atempadamente as atualizações de software.  

 Devido aos requisitos de segurança superiores associados à gestão de computadores cliente numa rede pública, a gestão de clientes baseada na Internet requer que os clientes e os servidores do sistema de sites a que estes ligam utilizem certificados PKI. Isto permite garantir que as ligações são autenticadas por uma autoridade independente e que os dados de e para estes sistemas de sites são encriptados utilizando Secure Sockets Layer (SSL).  

 Utilize as secções seguintes para o ajudar a planear a gestão de clientes baseada na Internet.  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Funcionalidades que Não São Suportadas na Internet  
 Nem todas as funcionalidades de gestão de clientes são adequadas para a Internet. Por conseguinte, não são suportadas quando os clientes são geridos na Internet. Normalmente, as funcionalidades que não são suportadas para gestão na Internet baseiam-se nos Serviços de Domínio do Active Directory ou não são adequadas para uma rede pública, como é o caso da deteção de rede e da reativação por LAN (WOL).  

 As funcionalidades seguintes não são suportadas quando os clientes são geridos na Internet:  

-   Implementação de cliente através da Internet, como por exemplo push de cliente e implementação de cliente baseada em atualização de software. Em vez disso, utilize a instalação manual de cliente.  

-   Atribuição automática de site.  

-   Reativação por LAN.  

-   Implementação do sistema operativo. No entanto, poderá implementar sequências de tarefas que não implementem um sistema operativo, como por exemplo sequências de tarefas que executem scripts e tarefas de manutenção em clientes.  

-   Controlo remoto.  

-   Implementação de software para utilizadores, a menos que o ponto de gestão baseado na Internet consiga autenticar o utilizador nos Serviços de Domínio do Active Directory utilizando a autenticação do Windows (Kerberos ou NTLM). Tal poderá suceder quando o ponto de gestão baseado na Internet confiar na floresta em que reside a conta do utilizador.  

 Além disso, a gestão de clientes baseada na Internet não suporta roaming. O roaming permite aos clientes localizar sempre os pontos de distribuição mais próximos para transferir conteúdo. Os clientes geridos na Internet comunicam com os sistemas de sites a partir do site atribuído quando tais sistemas são configurados para utilizar um FQDN da Internet, e as funções do sistema de sites permitem ligações de cliente a partir da Internet. Os clientes selecionam de forma não determinística um dos sistemas de sites baseados na Internet, independentemente da largura de banda ou da localização física.  

 Quando tiver um ponto de atualização de software configurado para aceitar ligações a partir da Internet, os clientes baseados na Internet do Configuration Manager que se encontram na Internet efetuam sempre uma análise desse ponto de atualização de software para determinar que atualizações de software são necessárias. No entanto, quando estes clientes se encontram na Internet, começam por tentar transferir as atualizações de software a partir do Microsoft Update, em vez de recorrerem a um ponto de distribuição baseado na Internet. Só em caso de insucesso é que tentarão transferir as atualizações de software necessárias a partir de um ponto de distribuição baseado na Internet. Os clientes que não estão configurados para gestão de clientes baseados na Internet não tentam nunca transferir as atualizações de software do Microsoft Update, utilizando sempre pontos de distribuição do Configuration Manager.  

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>Considerações sobre comunicações do cliente a partir da Internet ou de uma floresta não fidedigna  
 As seguintes funções do sistema de sites instaladas nos sites primários suportam ligações de clientes que se encontram em localizações não fidedignas, como a Internet ou uma floresta não fidedigna (os sites secundários não suportam ligações de clientes de localizações não fidedignas):  

-   Ponto de site do Catálogo de Aplicações  

-   Módulo de Política do Configuration Manager  

-   Ponto de distribuição (os pontos de distribuição baseados na nuvem precisam de HTTPS)  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de software  

 **Acerca dos sistemas de sites com acesso à Internet:**   
Apesar de não é necessário ter uma confiança entre a floresta do cliente e que o servidor de sistema de sites, quando a floresta que contém uma com acesso à sistema de sites de Internet confia na floresta que contém as contas de utilizador, esta configuração suporta políticas baseadas no utilizador para dispositivos na Internet quando ativa a **política de cliente** definição de cliente **ativar pedidos da política de utilizador dos clientes Internet**.  

 Por exemplo, as configurações seguintes ilustram quando a gestão de clientes baseada na Internet suporta políticas de utilizador para dispositivos na Internet:  

-   O ponto de gestão baseado na Internet encontra-se na rede de perímetro em que reside um controlador de domínio para autenticar o utilizador e uma firewall intermediária permite pacotes do Active Directory.  

-   A conta de utilizador encontra-se na Floresta A (a intranet) e o ponto de gestão baseado na Internet encontra-se na Floresta B (a rede de perímetro). A Floresta B confia na Floresta A e uma firewall intermediária permite os pacotes de autenticação.  

-   A conta de utilizador e o ponto de gestão baseado na Internet encontram-se na Floresta A (a intranet). O ponto de gestão é publicado na Internet através de um servidor Web proxy (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, será automaticamente tentada a autenticação NTLM.  

 Como mostra o exemplo anterior, é possível colocar sistemas de sites baseados na Internet na intranet quando estes forem publicados na Internet utilizando um servidor Web proxy, tal como o ISA Server ou o Forefront Threat Management Gateway. Estes sistemas de sites podem ser configurados apenas para ligações de cliente a partir da Internet, ou para ligações de cliente provenientes da Internet e da intranet. Ao utilizar um servidor Web proxy, poderá configurá-lo para bridge de Secure Sockets Layer (SSL) para SSL (mais seguro) ou túnel SSL:  

-   **Protocolo de bridge SSL para SSL:**   
    A configuração recomendada quando utiliza servidores Web proxy para a gestão de clientes baseados na Internet é o protocolo de bridge SSL para SSL, que utiliza a terminação de SSL com a autenticação de SSL. Os computadores cliente têm de ser autenticados utilizando a autenticação de computador e os clientes antigos do dispositivo móvel são autenticados utilizando a autenticação de utilizador. Dispositivos móveis que são inscritos pelo Configuration Manager não suportam o protocolo de bridge SSL.  

     A vantagem da terminação de SSL no servidor Web proxy é que os pacotes da Internet são sujeitos a inspeção antes de serem encaminhados para a rede interna. O servidor Web proxy autentica a ligação do cliente, termina-a e, em seguida, abre uma nova ligação autenticada para os sistemas de sites baseados na Internet. Quando os clientes do Configuration Manager utilizam um servidor web proxy, a identidade do cliente (GUID do cliente) está contida em segurança no payload do pacote para que o ponto de gestão não considere o servidor do web proxy como o cliente. Protocolo de bridge não é suportado no Configuration Manager com HTTP para HTTPS ou de HTTPS para HTTP.  

-   **Protocolo de túnel**:   
    Se o servidor web proxy não suporta os requisitos para o protocolo de bridge SSL ou se quiser configurar o suporte de Internet para dispositivos móveis que são inscritos pelo Configuration Manager, o túnel SSL também é suportado. É uma opção menos segura porque os pacotes SSL da Internet são encaminhados para os sistemas de sites sem a terminação de SSL, não podendo ser, assim, inspecionados quanto a conteúdo malicioso. Quando utiliza o protocolo de túnel SSL, não existem requisitos de certificado para o servidor Web proxy.  

##  <a name="planning-for-internet-based-clients"></a>Planear Clientes Baseados na Internet  
 É necessário decidir se os computadores cliente que são geridos pela Internet são configurados para gestão na intranet e Internet ou para gestão de clientes apenas na Internet. Apenas é possível configurar a opção de gestão de clientes durante a instalação de um computador cliente. Se mudar de ideias mais tarde, tem de reinstalar o cliente.  

> [!NOTE]  
>  Se configurar um ponto de gestão compatível com Internet, os clientes que se liguem ao ponto de gestão serão compatíveis com Internet quando atualizarem a respetiva lista de pontos de gestão disponíveis.  

> [!TIP]  
>  Não é necessário restringir à Internet a configuração de gestão de clientes apenas na Internet e também é possível utilizá-la na intranet.  

 Os clientes que estão configurados para gestão de clientes apenas na Internet comunicam apenas com os sistemas de sites que estão configurados para ligações de cliente da Internet. Esta configuração seria adequada para computadores que sabe que nunca ligam à intranet da empresa, por exemplo, computadores em pontos de venda em localizações remotas. Também pode ser apropriada se pretender restringir a comunicação de cliente HTTPS só (por exemplo, para suportar a firewall e políticas de segurança restringidas) e, quando instalar sistemas de sites baseados na Internet numa rede de perímetro e pretender gerir esses servidores utilizando o cliente do Configuration Manager.  

 Se pretender gerir clientes de grupo de trabalho na Internet, tem de os como apenas Internet.  

> [!NOTE]  
>  Os clientes de dispositivo móvel são configurados automaticamente como apenas Internet quando são configurados para utilizar um ponto de gestão baseado na Internet.  

 Outros computadores cliente podem ser configurados para gestão de clientes na Internet e intranet. Estes podem alternar automaticamente entre a gestão de clientes baseada na Internet e a gestão de clientes na intranet quando detetam uma alteração de rede. Se estes clientes podem localizar e ligar a um ponto de gestão que está configurado para ligações de cliente na intranet, estes clientes são geridos como clientes de intranet que possuem total funcionalidade de gestão do Configuration Manager. Se os clientes não conseguirem localizar ou estabelecer ligação a um ponto de gestão que está configurado para ligações de cliente na intranet, tentam estabelecer ligação a um ponto de gestão baseado na Internet, e se esta ligação tiver êxito, estes clientes são geridos pelos sistemas de sites baseados na Internet no respetivo site atribuído.  

 A vantagem da mudança automática entre gestão de clientes baseados na Internet e gestão de clientes na intranet é que os computadores cliente podem utilizar automaticamente todas as funcionalidades do Configuration Manager sempre que estiverem ligados à intranet e continuarem a ser geridos em funções de gestão essenciais quando estão na Internet. Além disso, uma transferência que começou na Internet pode continuar sem interrupções na intranet e vice versa.  

##  <a name="prerequisites-for-internet-based-client-management"></a>Pré-requisitos da Gestão de Clientes Baseada na Internet  
 Gestão de clientes baseados na Internet no Configuration Manager tem as seguintes dependências externas:  

-   Os clientes que são geridos na Internet têm de ter uma ligação à Internet.  

     O Configuration Manager utiliza as ligações existentes do fornecedor de serviços Internet (ISP) à Internet, que podem ser ligações permanentes ou temporárias. Os dispositivos móveis clientes têm de ter uma ligação à Internet direta, mas com computadores cliente podem ter uma ligação à Internet direta ou estabelecer ligação utilizando um servidor Web proxy.  

-   Os sistemas de sites que suportam a gestão de clientes baseados na Internet têm de ter conectividade à Internet e têm de estar num domínio do Active Directory.  

     Os sistemas de sites baseados na Internet não necessitam de uma relação de confiança com a floresta do Active Directory do servidor de sites. No entanto, quando o ponto de gestão baseado na Internet consegue autenticar o utilizador através da autenticação do Windows, são suportadas as políticas de utilizador. Se a autenticação do Windows falhar, apenas são suportadas as políticas de computador.  

    > [!NOTE]  
    >  Para suportar as políticas de utilizador, é necessário configurar para **Verdadeiro** as duas definições de cliente **Política do Cliente**:  
    >   
    >  -   **Ativar consulta de política de utilizador nos clientes**  
    > -   **Ativar pedidos da política do utilizador dos clientes Internet**  

     Um ponto do Web site do Catálogo de Aplicações baseado na Internet também necessita de autenticação do Windows para autenticar os utilizadores quando o respetivo computador está na Internet. Este requisito é independente das políticas de utilizador.  

-   É necessário ter uma infraestrutura de chaves públicas (PKI) compatível que possa implementar e gerir os certificados que os clientes necessitam e que são geridos na Internet e nos servidores dos sistemas de site baseados na Internet.  

     Para obter mais informações sobre o certificado PKI, veja [Requisitos de Certificado PKI para o Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

-   O nome de domínio completamente qualificado (FQDN) na Internet dos sistemas de sites que suportam a gestão de clientes baseados na Internet tem de estar registado como entradas de anfitrião nos servidores DNS públicos.  

-   Servidores proxy ou firewalls intermediários: têm de permitir a comunicação de clientes que está associada a sistemas de sites baseados na Internet.  

     Requisitos da comunicação de clientes:  

    -   Suportar HTTP 1.1  

    -   Permitir que o tipo de conteúdo HTTP do anexo multiparte de MIME (multiparte/misto e aplicação/sequência de octetos)  

    -   Permitir os seguintes verbos para o ponto de gestão baseado na Internet:  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   Permitir os seguintes verbos para o ponto de distribuição baseado na Internet:  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   Permitir os seguintes verbos para o ponto de estado de contingência baseado na Internet:  

        -   POST  

    -   Permitir os seguintes verbos para o ponto de Web site do Catálogo de Aplicações baseado na Internet:  

        -   POST  

        -   GET  

    -   Permitir os seguintes cabeçalhos HTTP para o ponto de gestão baseado na Internet:  

        -   Intervalo:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   Permitir o seguinte cabeçalho HTTP para o ponto de distribuição baseado na Internet:  

        -   Intervalo:  

     Para informações de configuração para suportar estes requisitos, consulte a documentação da sua firewall ou do seu servidor proxy.  

     Para requisitos de comunicação semelhantes quando utiliza o ponto de atualização de software para ligações de cliente a partir da Internet, consulte a documentação do Windows Server Update Services (WSUS). Por exemplo, para o WSUS no Windows Server 2003, consulte [apêndice d: Definições de segurança](http://go.microsoft.com/fwlink/p/?LinkId=143368), o anexo de implementação para definições de segurança.
