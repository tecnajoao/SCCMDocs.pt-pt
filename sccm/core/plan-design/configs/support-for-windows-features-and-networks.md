---
title: Suporte para funcionalidades do Windows
titleSuffix: Configuration Manager
description: Saiba quais Windows e as funcionalidades de rede do Configuration Manager suporta.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1ac3262acff35e23de4faa1e80c796f5ee4e4b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156700"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Suporte para funcionalidades do Windows e redes no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo identifica o suporte do Configuration Manager para Windows comuns e as funcionalidades de rede.  



##  <a name="bkmk_branchcache"></a> BranchCache  

Utilize o Windows BranchCache com o Configuration Manager ao ativá-la em pontos de distribuição e configurar os clientes para utilizá-lo em modo de cache distribuída.

Configure as definições de BranchCache num tipo de implementação para aplicações, na implementação de um pacote e para sequências de tarefas. A partir da versão 1802, BranchCache está ativado por predefinição. 

Quando os requisitos do BranchCache são cumpridos, esta funcionalidade permite que os clientes em localizações remotas obtenham conteúdo de clientes locais que tenham uma cache atual do conteúdo.  

Por exemplo, quando o primeiro cliente de capacidade para BranchCache pede conteúdo a partir de um ponto de distribuição é configurado como servidor BranchCache, o cliente transfere e coloca em cache o conteúdo. Este conteúdo é então disponibilizado para clientes na mesma sub-rede que solicitou este conteúdo.

Estes clientes também colocam em cache o conteúdo. Outros clientes na mesma sub-rede não precisam de transferir o conteúdo do ponto de distribuição. O conteúdo é distribuído por vários clientes para futuras transferências.  


### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Requisitos para suportar o BranchCache com o Configuration Manager

#### <a name="configure-distribution-points"></a>Configurar pontos de distribuição
Adicionar a **Windows BranchCache** funcionalidade para o servidor de sistema de sites que está configurado como um ponto de distribuição.    
- Os pontos de distribuição nos servidores que estão configurados para suportar o BranchCache não requerem nenhuma configuração adicional.   
- Não é possível adicionar o Windows BranchCache para um ponto de distribuição baseado na nuvem. Pontos de distribuição baseado na nuvem suportam a transferência de conteúdo por clientes que estão configurados para o Windows BranchCache.  

#### <a name="configure-clients"></a>Configurar os clientes    
- Os clientes que podem suportar o BranchCache têm de ser configurados para o modo de cache distribuída do BranchCache.  
- A definição de sistema operacional para as definições de cliente BITS tem de estar ativada para suportar o BranchCache.  

Para obter informações, consulte [configurar clientes para BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) na documentação do Windows.


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Versões de SO com o Windows BranchCache com suporte do Configuration Manager

|Operar&nbsp;sistema|Detalhes do suporte|  
|----------------------|---------------------|  
|Windows 7 com SP1|Suportado por predefinição|  
|Windows 8|Suportado por predefinição|  
|Windows 8.1|Suportado por predefinição|  
|Windows 10|Suportado por predefinição|  
|Windows Server 2008 com SP2|**É necessário o BITS 4.0**: Instale a versão de BITS 4.0 nos clientes do Configuration Manager ao utilizar atualizações de software ou de distribuição de software. Para obter mais informações, consulte [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> Neste SO, a funcionalidade de cliente BranchCache não é suportada para distribuição de software que é executada a partir da rede ou para transferências de ficheiros SMB. Além disso, esse SO não é possível utilizar a funcionalidade BranchCache com pontos de distribuição baseado na nuvem.|  
|Windows Server 2008 R2|Suportado por predefinição|  
|Windows Server 2012|Suportado por predefinição|  
|Windows Server 2012 R2|Suportado por predefinição|  
|Windows Server 2016|Suportado por predefinição|  

Para obter mais informações, consulte [BranchCache para Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) na documentação do Windows Server.  



##  <a name="bkmk_Workgroups"></a> Computadores em grupos de trabalho  

O Configuration Manager fornece suporte para clientes em grupos de trabalho.  

- O Configuration Manager suporta a mudança de um cliente de um grupo de trabalho a um domínio ou de um domínio a um grupo de trabalho. Para obter mais informações, consulte [como instalar clientes do Configuration Manager em computadores de grupo de trabalho](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup).  

> [!NOTE]  
>  Embora os clientes em grupos de trabalho têm suporte, todos os sistemas de sites têm de ser membros de um domínio do Active Directory suportado.  



##  <a name="bkmmk_datadedup"></a> Eliminação de dados duplicados  

O Configuration Manager suporta a utilização da eliminação de duplicados de dados com pontos de distribuição nos seguintes sistemas operativos:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  O volume que anfitriões ficheiros de origem do pacote não pode ser marcado para eliminação de duplicados de dados. Esta limitação é porque os pontos de reanálise de eliminação de duplicados de dados utiliza. O Configuration Manager não suporta a utilização de uma localização de origem de conteúdo com arquivos armazenados em pontos de reanálise.  

Para obter mais informações, consulte [pontos de distribuição do Configuration Manager e eliminação de duplicados do Windows Server 2012 dados](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) no blog da Equipe do Configuration Manager, e [descrição geral da eliminação de duplicados de dados](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) no Documentação de Windows Server.  



##  <a name="bkmk_DA"></a> DirectAccess  

O Configuration Manager suporta a funcionalidade do DirectAccess para a comunicação entre clientes e sistemas de servidor do site.  

- Quando são cumpridos todos os requisitos para o DirectAccess, permite que clientes do Configuration Manager na internet para comunicar com o respetivo site atribuído como se estivessem na intranet.  

- Para ações iniciadas pelo servidor, como o controlo remoto e da instalação push do cliente, o computador de início tem de executar o IPv6. Este protocolo tem de ser suportado em todos os dispositivos de rede intervenientes.  

O Configuration Manager não suporta a seguinte funcionalidade através do DirectAccess:  

-   Implementação de SO   

-   Comunicação entre sites do Configuration Manager  

-   Comunicação entre servidores do sistema de sites do Configuration Manager dentro de um site  



##  <a name="bkmk_dualboot"></a> Computadores de arranque duplo  

O Configuration Manager não consegue gerir mais do que um sistema operacional num único computador. Se houver mais de um SO num computador para gerir, ajuste a deteção do site e os métodos de instalação de cliente para se certificar de que o cliente do Configuration Manager está instalado apenas no sistema operacional que tem de ser geridos.  



##  <a name="bkmk_IPv6"></a> IPv6  

Protocolo IP versão 4 (IPv4), o Configuration Manager suporta o protocolo IP versão 6 (IPv6), com as seguintes exceções:  

|Função| Exceção no suporte de IPv6|  
|--------------|-------------------------------|  
|Pontos de distribuição baseados na nuvem|O IPv4 é necessário para suportar pontos de distribuição baseados na nuvem e do Microsoft Azure.|  
|Gateway de gestão na cloud|O IPv4 é necessário para suportar o Microsoft Azure e o gateway de gestão na cloud.|  
|Dispositivos móveis inscritos pelo Microsoft Intune e do conector de serviços da Microsoft|O IPv4 é necessário para suportar dispositivos móveis inscritos pelo Microsoft Intune e do conector de serviços da Microsoft.|  
|Deteção de Redes|O IPv4 é necessário quando configura o servidor DHCP para procurar na Deteção de Redes.|  
|Implementação de SO|Na versão 1802 e anterior, o IPv4 é necessário para suportar a implementação do sistema operacional.  </br> </br> A partir da versão 1806, ative o dispositivo de resposta PXE num ponto de distribuição sem o serviço de implementação do Windows. Este novo serviço de resposta do PXE oferece suporte ao IPv6. Outros aspetos da funcionalidade de implementação do sistema operacional, como capturar ou definir endereços IP estáticos durante a sequência de tarefas, continuam a exigir o IPv4. |  
|Comunicação do proxy de reativação|O IPv4 é necessário para suportar os pacotes do proxy de reativação do cliente.|  
|Windows CE|O IPv4 é necessário para suportar o cliente de Configuration Manager em dispositivos Windows CE.|  



##  <a name="bkmk_NAT"></a> Tradução de Endereços de Rede  

Tradução de endereços de rede (NAT) não é suportada no Configuration Manager, a menos que o site suporta clientes que estejam ligados à internet e o cliente Deteta que está ligado à internet. Para obter mais informações sobre a gestão de clientes baseada na internet, consulte [planear a gestão de clientes baseados na internet](/sccm/core/clients/deploy/plan/plan-for-managing-internet-based-clients).  



##  <a name="bkmk_storage"></a> Tecnologia de armazenamento especializado  

O Configuration Manager funciona com qualquer hardware que esteja certificado na lista de compatibilidade de Hardware Windows para a versão do sistema operacional que o componente do Configuration Manager está instalado no.

Funções de servidor de site requerem NTFS, para que o Configuration Manager possa definir permissões de diretório e arquivo. O Configuration Manager parte do princípio de que tem propriedade completa de uma unidade lógica. Sistemas de sites que são executados em computadores separados não podem partilhar uma partição lógica numa tecnologia de armazenamento. No entanto, os computadores conseguem utilizar uma partição lógica na mesma partição física de um dispositivo de armazenamento.  

### <a name="support-considerations"></a>Considerações sobre suporte

- **Rede de armazenamento**: Uma rede de área de armazenamento (SAN) é suportada se um servidor baseado em Windows suportado estiver anexado diretamente ao volume que é alojado pela SAN.  

- **Single Instance Storage**: O Configuration Manager não suporta a configuração de pastas de pacote e a assinatura do ponto de distribuição num volume com capacidade para Single Instance Storage SIS.  

     Além disso, a cache de um cliente do Configuration Manager não é suportada num volume com capacidade para SIS.  

- **Unidade de disco amovível**: O Configuration Manager não suporta a instalação de sistemas de sites do Configuration Manager ou de clientes numa unidade de disco amovível.  
