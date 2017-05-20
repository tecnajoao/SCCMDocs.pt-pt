---
title: Suporte para funcionalidades do Windows | Documentos do Microsoft
description: Saiba quais Windows e o funcionamento em rede funcionalidades do System Center Configuration Manager suporta.
ms.custom: na
ms.date: 3/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d5166b16ffbe46af561b1ce98c0494cc4aaa72a8
ms.openlocfilehash: e040552dab21ba9a71e06a78f6acc2ffe1b0eb61
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Suporte para funcionalidades do Windows e as redes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico identifica suporte do System Center Configuration Manager para o Windows comuns e funcionalidades de rede.  


##  <a name="bkmk_branchcache"></a> BranchCache  
Pode utilizar o BranchCache do Windows com o Configuration Manager quando ativar o BranchCache nos pontos de distribuição e configurar clientes para utilizar o BranchCache no modo de cache distribuída.

Pode configurar as definições do BranchCache num tipo de implementação para aplicações, na implementação de um pacote e para sequências de tarefas.  

Quando os requisitos do BranchCache são satisfeitos, esta funcionalidade permite que os clientes em localizações remotas obtenham conteúdo de clientes locais que tenham uma cache atual do conteúdo.  

Por exemplo, quando o primeiro computador cliente com capacidade BranchCache pedir conteúdo de um ponto de distribuição configurado como servidor BranchCache, o computador cliente transfere esse conteúdo e coloca-o em cache. Este conteúdo é então disponibilizado para clientes na mesma sub-rede que pediu este conteúdo.

Estes clientes também colocam em cache o conteúdo. Desta forma, os clientes seguintes da mesma sub-rede não precisam de transferir o conteúdo a partir do ponto de distribuição e o conteúdo é distribuído por múltiplos clientes para futuras transferências.  

**Requisitos para suportam o BranchCache com o Configuration Manager:**  
-   **Configure pontos de distribuição:**  
    Adicione a funcionalidade **Windows BranchCache** ao servidor do sistema de sites que está configurado como ponto de distribuição.    

    -   Pontos de distribuição nos servidores que estão configurados para suportar o BranchCache não requerem nenhuma configuração adicional.   
    -   Não é possível adicionar o Windows BranchCache para um ponto de distribuição baseado na nuvem, mas os pontos de distribuição baseado na nuvem suportam a transferência de conteúdos por parte dos clientes que estão configurados para o Windows BranchCache.  

-   **Configure os clientes:**    
    -   Os clientes que suportam o BranchCache tem de ser configurados para o modo de cache distribuída BranchCache.  
    -   A definição de sistema operativo para as definições do cliente BITS tem de estar ativada para suportam o BranchCache.   <br /> <br />
        
    Para obter informações sobre como configurar os clientes suportam o BranchCache, consulte o [configurar clientes](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache#configure-clients-for-branchcache) secção [configurar BranchCache para Windows 10 atualizações](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache).


**O Configuration Manager suporta os seguintes sistemas operativos cliente com o Windows BranchCache:**  

|Sistema operativo|Detalhes do suporte|  
|----------------------|---------------------|  
|Windows 7 com SP1|Suportado por predefinição|  
|Windows 8|Suportado por predefinição|  
|Windows 8.1|Suportado por predefinição|  
|Windows 10|Suportado por predefinição|  
|Windows Server 2008 com SP2|**Requer o BITS 4.0**: Pode instalar a versão de BITS 4.0 em clientes do Configuration Manager através da utilização de atualizações de software ou a distribuição de software. Para mais informações sobre a versão do BITS 4.0, consulte [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> Neste sistema operativo, a funcionalidade de cliente BranchCache não é suportada para distribuição de software que é executada a partir da rede ou para transferências de ficheiros SMB. Além disso, este sistema operativo não pode utilizar a funcionalidade BranchCache com pontos de distribuição baseados na nuvem.|  
|Windows Server 2008 R2|Suportado por predefinição|  
|Windows Server 2012|Suportado por predefinição|  
|Windows Server 2012 R2|Suportado por predefinição|  

 Para obter mais informações sobre o BranchCache, consulte o artigo [BranchCache para Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) na documentação do Windows Server.  

##  <a name="bkmk_Workgroups"></a>Computadores em grupos de trabalho  
O Configuration Manager oferece suporte para clientes em grupos de trabalho.  

-   O Configuration Manager suporta a mover de um cliente a partir de um grupo de trabalho a um domínio ou de um domínio para um grupo de trabalho. Para obter mais informações, consulte o artigo [como instalar clientes do Configuration Manager em computadores de grupo de trabalho](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) no [como implementar clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) tópico.  

> [!NOTE]  
>  Embora os clientes em grupos de trabalho são suportados, todos os sistemas de sites têm de ser membros de um domínio do Active Directory suportados.  


##  <a name="bkmmk_datadedup"></a> Eliminação de dados duplicados  
O Configuration Manager suporta a utilização da eliminação de duplicados de dados com pontos de distribuição nos seguintes sistemas operativos:  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  O volume que aloja os ficheiros de origem do pacote não pode ser marcado para eliminação de dados duplicados. Isto acontece porque a eliminação de dados duplicados utiliza pontos de reanálise e do Configuration Manager não suporta a utilização de uma localização de origem de conteúdo com os ficheiros que estão armazenados nos pontos de reanálise.  

Para obter mais informações, consulte o artigo [pontos de distribuição do Configuration Manager e eliminação de duplicados do Windows Server 2012 dados](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) no blogue da equipa do Configuration Manager, e [descrição geral da eliminação de duplicados de dados](http://technet.microsoft.com/library/hh831602.aspx) na Biblioteca TechNet do Windows Server.  

##  <a name="bkmk_DA"></a> DirectAccess  
O Configuration Manager suporta a funcionalidade DirectAccess no Windows Server 2008 R2 e posterior para comunicação entre clientes e sistemas de servidor do site.  

-   Quando cumprir todos os requisitos para o DirectAccess, o DirectAccess permite aos clientes de Configuration Manager na Internet para comunicar com o respetivo site atribuído, como se fossem na intranet.  

-   Para ações iniciadas pelo servidor, como o controlo remoto e a instalação push do cliente, o computador a iniciar (por exemplo, o servidor do site) tem de executar o IPv6 e este protocolo tem de ser suportado em todos os dispositivos de rede intervenientes.  

O Configuration Manager não suporta os seguintes através do DirectAccess:  

-   A implementação de sistemas operativos  

-   Comunicação entre sites do Configuration Manager  

-   Comunicação entre servidores de sistema de sites do Configuration Manager dentro de um site  

##  <a name="bkmk_dualboot"></a> Computadores de arranque duplo  
 O Configuration Manager não consegue gerir mais do que um sistema operativo num único computador. Se existir mais do que um sistema operativo num computador que têm de ser gerido, ajuste os métodos de deteção e instalação são utilizados para se certificar de que o Configuration Manager cliente é instalado apenas num sistema operativo que tem de ser geridos.  

##  <a name="bkmk_IPv6"></a>Versão de protocolo de Internet 6  
 Para além de versão do protocolo de Internet 4 (IPv4), o Configuration Manager suporta a versão de protocolo de Internet 6 (IPv6) com as seguintes exceções:  

|Função| Exceção no suporte de IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados na nuvem|O IPv4 é necessário para suportar pontos de distribuição baseados na nuvem e do Microsoft Azure.|  
|Dispositivos móveis inscritos pelo Microsoft Intune e o conector de serviços Microsoft|IPv4 é necessário para suportar dispositivos móveis inscritos pelo Microsoft Intune e o conector de serviços Microsoft.|  
|Deteção de Redes|O IPv4 é necessário quando configura o servidor DHCP para procurar na Deteção de Redes.|  
|Implementação do sistema operativo|O IPv4 é necessário para suportar a implementação do sistema operativo.|  
|Comunicação do proxy de reativação|O IPv4 é necessário para suportar os pacotes do proxy de reativação do cliente.|  
|Windows CE|IPv4 é necessário para suportar o cliente do Configuration Manager em dispositivos Windows CE.|  

##  <a name="bkmk_NAT"></a> Tradução de Endereços de Rede  
 Tradução de endereços de rede (NAT) não é suportada no Configuration Manager, a menos que o site suporta clientes que se encontram na Internet e o cliente Deteta que está ligado à Internet. Para obter mais informações sobre a gestão de clientes baseada na Internet, consulte o artigo [planeamento da gestão de clientes baseados na Internet no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  

##  <a name="bkmk_storage"></a> Tecnologia de armazenamento especializado  
 Do Configuration Manager é funciona com qualquer hardware certificado na lista de compatibilidade de Hardware Windows para a versão do sistema operativo que o componente do Configuration Manager está instalado.

As funções do Servidor do Site precisam de sistemas de ficheiros NTFS para que possam ser definidas as permissões de ficheiro e diretório. Uma vez que o Configuration Manager parte do princípio de que tem a propriedade concluída de uma unidade lógica, sistemas de sites que são executados em computadores separados não é possível partilhar uma partição lógica em qualquer tecnologia de armazenamento. No entanto, os computadores conseguem utilizar uma partição lógica na mesma partição física de um dispositivo de armazenamento.  

 **Considerações sobre suporte:**  

-   **Rede de armazenamento**: Uma rede de área de armazenamento (SAN) é suportada quando um servidor baseado em Windows suportado está ligado diretamente para o volume que está alojado por SAN.  

-   **Single Instance Storage**: O Configuration Manager não suporta a configuração de pastas de pacote e assinatura do ponto de distribuição num volume ativado Single Instance Storage SIS.  

     Além disso, a cache de um cliente do Configuration Manager não é suportada num volume ativado o SIS.  

-   **Unidade de disco amovível**: O Configuration Manager não suporta a instalação de clientes ou sistemas de site do Configuration Manager numa unidade de disco amovível.  

