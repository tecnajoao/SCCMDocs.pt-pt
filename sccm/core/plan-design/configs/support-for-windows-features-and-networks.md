---
title: Suporte para funcionalidades do Windows
titleSuffix: Configuration Manager
description: Saiba que Windows e redes de funcionalidades do System Center Configuration Manager suporta.
ms.custom: na
ms.date: 8/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: "8"
caps.handback.revision: "0"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 988de3bb295f51722cab2b545bf894a553970e26
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Suporte para funcionalidades do Windows e redes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico identifica o suporte do System Center Configuration Manager para o Windows comuns e as funcionalidades de redes.  


##  <a name="bkmk_branchcache"></a> BranchCache  
Pode utilizar Windows BranchCache com o Configuration Manager quando ativar o BranchCache nos pontos de distribuição e configurar clientes para utilizar o BranchCache no modo de cache distribuída.

Pode configurar as definições do BranchCache num tipo de implementação para aplicações, na implementação de um pacote e para sequências de tarefas.  

Quando são cumpridos os requisitos para o BranchCache, esta funcionalidade permite que os clientes em localizações remotas obtenham conteúdo de clientes locais que tenham uma cache atual do conteúdo.  

Por exemplo, quando o primeiro computador cliente com capacidade BranchCache pedir conteúdo de um ponto de distribuição configurado como servidor BranchCache, o computador cliente transfere esse conteúdo e coloca-o em cache. Este conteúdo é então disponibilizado para os clientes na mesma sub-rede que pediu este conteúdo.

Estes clientes também colocam em cache o conteúdo. Desta forma, os clientes seguintes da mesma sub-rede não precisam de transferir o conteúdo a partir do ponto de distribuição e o conteúdo é distribuído por múltiplos clientes para futuras transferências.  

**Requisitos para suportar o BranchCache com o Configuration Manager:**  
-   **Configure pontos de distribuição:**  
    Adicione a funcionalidade **Windows BranchCache** ao servidor do sistema de sites que está configurado como ponto de distribuição.    

    -   Pontos de distribuição nos servidores que estão configurados para suportar o BranchCache não requerem nenhuma configuração adicional.   
    -   Não é possível adicionar o Windows BranchCache para um ponto de distribuição baseado na nuvem, mas pontos de distribuição baseado na nuvem suportam a transferência de conteúdos por parte dos clientes que estão configurados para o Windows BranchCache.  

-   **Configure os clientes:**    
    -   Os clientes que suportam o BranchCache tem de ser configurados para o modo de cache distribuída do BranchCache.  
    -   A definição do sistema operativo para as definições do cliente BITS tem de estar ativada para suportar o BranchCache.   <br /> <br />

    Para obter informações sobre como configurar clientes para suportar o BranchCache, consulte o [configurar clientes](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache#configure-clients-for-branchcache) secção [de atualizações de configurar o BranchCache para Windows 10](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache).


**O Configuration Manager suporta os seguintes sistemas de operativos de cliente com o Windows BranchCache:**  

|Sistema operativo|Detalhes do suporte|  
|----------------------|---------------------|  
|Windows 7 com SP1|Suportado por predefinição|  
|Windows 8|Suportado por predefinição|  
|Windows 8.1|Suportado por predefinição|  
|Windows 10|Suportado por predefinição|  
|Windows Server 2008 com SP2|**É necessário o BITS 4.0**: Pode instalar a versão de BITS 4.0 nos clientes do Configuration Manager através da utilização de atualizações de software ou a distribuição de software. Para mais informações sobre a versão do BITS 4.0, consulte [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> Neste sistema operativo, a funcionalidade de cliente BranchCache não é suportada para distribuição de software que é executada a partir da rede ou para transferências de ficheiros SMB. Além disso, este sistema operativo não pode utilizar a funcionalidade BranchCache com pontos de distribuição baseados na nuvem.|  
|Windows Server 2008 R2|Suportado por predefinição|  
|Windows Server 2012|Suportado por predefinição|  
|Windows Server 2012 R2|Suportado por predefinição|  

 Para obter mais informações sobre o BranchCache, consulte o artigo [BranchCache para Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) na documentação do Windows Server.  

##  <a name="bkmk_Workgroups"></a>Computadores em grupos de trabalho  
O Configuration Manager fornece suporte para clientes em grupos de trabalho.  

-   O Configuration Manager suporta a mudança de um cliente de um grupo de trabalho a um domínio ou de um domínio a um grupo de trabalho. Para obter mais informações, consulte [como instalar clientes do Configuration Manager em computadores de grupo de trabalho](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) no [como implementar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) tópico.  

> [!NOTE]  
>  Embora os clientes em grupos de trabalho são suportados, todos os sistemas de sites têm de ser membros de um domínio do Active Directory suportado.  


##  <a name="bkmmk_datadedup"></a> Eliminação de dados duplicados  
O Configuration Manager suporta a utilização de dados duplicados com pontos de distribuição nos seguintes sistemas operativos:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  



> [!IMPORTANT]  
>  O volume que aloja os ficheiros de origem do pacote não pode ser marcado para eliminação de dados duplicados. Isto acontece porque a eliminação de dados duplicados utiliza pontos de reanálise e do Configuration Manager não suporta a utilização de uma localização de origem de conteúdo com ficheiros armazenados em pontos de reanálise.  

Para obter mais informações, consulte [pontos de distribuição do Configuration Manager e eliminação de duplicados do Windows Server 2012 dados](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) no blogue de equipa do Configuration Manager, e [descrição geral da eliminação de duplicados de dados](http://technet.microsoft.com/library/hh831602.aspx) na Biblioteca TechNet do Windows Server.  

##  <a name="bkmk_DA"></a> DirectAccess  
O Configuration Manager suporta a funcionalidade DirectAccess no Windows Server 2008 R2 e posteriores para comunicação entre clientes e sistemas de servidor do site.  

-   Quando são cumpridos todos os requisitos para o DirectAccess, o DirectAccess permite aos clientes do Configuration Manager na Internet para comunicar com o respetivo site atribuído como se estivessem na intranet.  

-   Para ações iniciadas pelo servidor, como o controlo remoto e a instalação push do cliente, o computador a iniciar (por exemplo, o servidor do site) tem de executar o IPv6 e este protocolo tem de ser suportado em todos os dispositivos de rede intervenientes.  

O Configuration Manager não suporta o seguinte através do DirectAccess:  

-   A implementação de sistemas operativos  

-   Comunicação entre sites do Configuration Manager  

-   Comunicação entre servidores do sistema de sites do Configuration Manager num site  

##  <a name="bkmk_dualboot"></a> Computadores de arranque duplo  
 O Configuration Manager não consegue gerir mais do que um sistema operativo num único computador. Se existir mais do que um sistema operativo num computador que tem de ser gerido, ajuste os métodos de deteção e instalação que são utilizados para se certificar de que o Configuration Manager de cliente é instalado apenas no sistema operativo que tem de ser geridos.  

##  <a name="bkmk_IPv6"></a>Protocolo IP versão 6  
 Para além do protocolo IP versão 4 (IPv4), o Configuration Manager suporta o protocolo IP versão 6 (IPv6) com as seguintes exceções:  

|Função| Exceção no suporte de IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados na nuvem|O IPv4 é necessário para suportar pontos de distribuição baseados na nuvem e do Microsoft Azure.|  
|Dispositivos móveis que são inscritos pelo Microsoft Intune e do conector de serviços da Microsoft|O IPv4 é necessário para suportar dispositivos móveis que são inscritos pelo Microsoft Intune e do conector de serviços Microsoft.|  
|Deteção de Redes|O IPv4 é necessário quando configura o servidor DHCP para procurar na Deteção de Redes.|  
|Implementação do sistema operativo|O IPv4 é necessário para suportar a implementação do sistema operativo.|  
|Comunicação do proxy de reativação|O IPv4 é necessário para suportar os pacotes do proxy de reativação do cliente.|  
|Windows CE|O IPv4 é necessário para suportar o cliente do Configuration Manager em dispositivos Windows CE.|  

##  <a name="bkmk_NAT"></a> Tradução de Endereços de Rede  
 Tradução de endereços de rede (NAT) não é suportada no Configuration Manager, a menos que o site suporta clientes que estão na Internet e o cliente Deteta que está ligado à Internet. Para obter mais informações sobre a gestão de clientes baseada na Internet, consulte [planear a gestão de clientes baseados na Internet no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  

##  <a name="bkmk_storage"></a> Tecnologia de armazenamento especializado  
 O Configuration Manager funciona com qualquer hardware que esteja certificado na Windows Hardware Compatibility List para a versão do sistema operativo que o componente do Configuration Manager está instalado.

As funções do Servidor do Site precisam de sistemas de ficheiros NTFS para que possam ser definidas as permissões de ficheiro e diretório. Porque o Configuration Manager parte do princípio de que tem propriedade completa de uma unidade lógica, os sistemas de sites que são executados em computadores separados não podem partilhar uma partição lógica numa tecnologia de armazenamento. No entanto, os computadores conseguem utilizar uma partição lógica na mesma partição física de um dispositivo de armazenamento.  

 **Considerações sobre suporte:**  

-   **Rede de armazenamento**: Uma rede de área de armazenamento (SAN) é suportada se um servidor baseado em Windows suportado estiver anexado diretamente ao volume que é alojado pela SAN.  

-   **Single Instance Storage**: O Configuration Manager não suporta a configuração das pastas de assinatura e o pacote do ponto de distribuição num volume com capacidade para Single Instance Storage SIS.  

     Além disso, a cache de um cliente de Configuration Manager não é suportada num volume ativados por SIS.  

-   **Unidade de disco amovível**: O Configuration Manager não suporta a instalação de clientes ou sistemas de sites do Configuration Manager numa unidade de disco amovível.  
