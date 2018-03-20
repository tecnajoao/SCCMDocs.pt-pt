---
title: "Planear a implementação do cliente em dispositivos Windows Embedded"
titleSuffix: Configuration Manager
description: "Planear a implementação do cliente em dispositivos Windows Embedded no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: 
caps.handback.revision: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: c4f3d8a9b043707340e56d3ae483ad66ca17dc10
ms.sourcegitcommit: 52080ef1b0f9a27c123711ef274ac3ffe070e8e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/20/2018
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>Planear a implementação do cliente em dispositivos Windows Embedded no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<a name="BKMK_DeployClientEmbedded"></a> Se o seu dispositivo Windows Embedded não inclui o cliente do System Center Configuration Manager, pode utilizar qualquer um dos métodos de instalação do cliente se o dispositivo cumpra as dependências necessárias. Se o dispositivo incorporado suportar filtros de escrita, terá de desativar esses filtros antes de instalar o cliente e, em seguida, de reativar novamente os filtros após a instalação do cliente e da atribuição do mesmo a um site.  

 Tenha em atenção que, ao desativar os filtros, não deve desativar os controladores dos filtros. Normalmente, estes controladores são iniciados automaticamente quando o computador é iniciado. Desativar os controladores irá impedir a instalação do cliente ou irá interferir com a orquestração do filtro de escrita, o que fará com que as operações do cliente falhem. Eis os serviços associados a cada um dos tipos de filtro de escrita que têm de ser mantidos em execução:  

|Tipo de Filtro de Escrita|Controlador|Type|Descrição|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementa um redirecionamento de E/S ao nível dos setores em volumes protegidos.|  
|FBWF|FBWF|Sistema de ficheiros|Implementa um redirecionamento de E/S ao nível dos ficheiros em volumes protegidos.|  
|UWF|uwfreg|Kernel|Redirecionador de Registo UWF|  
|UWF|uwfs|Sistema de ficheiros|Redirecionador de Ficheiros UWF|  
|UWF|uwfvol|Kernel|Gestor de Volumes UWF|  

 Os filtros de escrita controlam a forma como o sistema operativo no dispositivo incorporado é atualizado quando efetuar alterações, por exemplo quando instalar software. Se os filtros de escrita estiverem ativados, em vez de serem efetuadas diretamente no sistema operativo, estas alterações serão redirecionadas para uma sobreposição temporária. Se as alterações apenas forem escritas na sobreposição, serão perdidas quando o dispositivo incorporado for encerrado. No entanto, caso os filtros de escrita sejam temporariamente desativados, as alterações poderão tornar-se permanentes, evitando a necessidade de voltar a efetuar essas alterações (ou de reinstalar o software) sempre que o dispositivo incorporado for reiniciado. No entanto, a desativação temporária e posterior reativação dos filtros de escrita implicará uma ou mais reinicializações, pelo que, em condições normais, será preferível controlar o momento em que esta operação irá decorrer, configurando janelas de manutenção que permitam as reinicializações fora do horário de expediente.  

 Pode configurar opções para desativar e reativar automaticamente os filtros de escrita quando implementar software como aplicações, sequências de tarefas, atualizações de software e o cliente do Endpoint Protection. A exceção são as linhas de base de configuração com itens de configuração que utilizem a remediação automática. Neste cenário, a remediação ocorre sempre ao nível da sobreposição, pelo que apenas ficará disponível até o dispositivo ser reiniciado. A remediação é novamente aplicada durante o ciclo de avaliação seguinte, mas apenas ao nível da sobreposição, cujos dados são eliminados durante o reinício. Para forçar o Gestor de configuração para consolidar as alterações da remediação, pode implementar a linha de base de configuração e, em seguida, outra implementação de software que suporte a consolidação da alteração logo que possível.  

 Se os filtros de escrita estiverem desativados, poderá instalar software nos dispositivos Windows Embedded utilizando o Centro de Software. No entanto, se os filtros de escrita estiverem ativados, a instalação falha e o Configuration Manager apresenta uma mensagem de erro que não tem permissões suficientes para instalar a aplicação.  

> [!WARNING]  
>  Mesmo se não selecionar as opções do Configuration Manager para consolidar as alterações, as alterações poderão ser confirmadas se outra instalação de software ou alteração for efetuada confirmando alterações. Neste cenário, as alterações originais serão confirmadas para além das novas alterações.  

 Quando o Configuration Manager desative os filtros de escrita para tornar as alterações permanentes, apenas os utilizadores que têm direitos administrativos locais podem iniciar sessão e utilizar o dispositivo incorporado. Durante este período, os utilizadores com direitos restritos são bloqueados e recebem uma mensagem a informar que o computador está indisponível por estar em manutenção. Isto ajuda a proteger o dispositivo enquanto está num estado em que as alterações podem ser aplicadas permanentemente, sendo este comportamento de bloqueio no modo de manutenção outra razão para configurar uma janela de manutenção por um período em que os utilizadores não irão iniciar sessão nestes dispositivos.  

 O Configuration Manager suporta a gestão dos seguintes tipos de filtros de escrita:  

-   Ficheiro-Based Write Filter (FBWF) - para mais informações, consulte [filtro de escrita baseados em ficheiros](http://go.microsoft.com/fwlink/?LinkID=204717).  

-   Avançado escrever filtro RAM (EWF) - para mais informações, consulte [Enhanced Write Filter](http://go.microsoft.com/fwlink/?LinkId=204718).  

-   O filtro de escrita unificado (UWF) - para mais informações, consulte [filtro de escrita unificado](http://go.microsoft.com/fwlink/?LinkId=309236).  

 O Configuration Manager não suporta operações de filtro de escrita quando o dispositivo Windows Embedded está no modo de EWF RAM Reg.  

> [!IMPORTANT]  
>  Se puder escolher, utilize filtros de escrita baseados em ficheiros (FBWF) com o Configuration Manager para maior eficácia e escalabilidade superior.
>
> **Para dispositivos que utilizam FBWF apenas:** Configure as seguintes exceções para manter o estado do cliente e os dados de inventário entre reinícios do dispositivo:  
>   
>  -   CCMINSTALLDIR\\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  Os dispositivos que executam o Windows Embedded 8.0 e posterior não suportam exclusões que contêm carateres universais. Nestes dispositivos, tem de configurar as seguintes exclusões individualmente:  
>   
>  -   Todos os ficheiros em CCMINSTALLDIR com a extensão .sdf, normalmente:  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **Para dispositivos que utilizam FBWF e UWF apenas:** Quando os clientes num grupo de trabalho utilizam certificados para autenticação para pontos de gestão, também tem de excluir a chave privada para garantir que o cliente continua a comunicar com o ponto de gestão. Nestes dispositivos, configure as seguintes exceções:  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 Para um cenário de exemplo implementar e gerir com filtro escrita ativado Windows Embedded Consulte dispositivos no Configuration Manager [cenário de exemplo para implementação e gestão de clientes do System Center Configuration Manager em dispositivos Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Para mais informações sobre como criar imagens para dispositivos Windows Embedded e configurar filtros de escrita, consulte a documentação do Windows Embedded ou contacte o OEM.  

> [!NOTE]  
>  Quando seleciona as plataformas aplicáveis para implementações de software e itens de configuração, estas apresentam famílias Windows Embedded em vez de versões específicas. Utilize a lista seguinte para mapear a versão específica do Windows Embedded para as opções na caixa de listagem:  
>   
>  -   **Os Sistemas Operativos Incorporados baseados no Windows XP (32 bits)** incluem o seguinte:  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   **Os sistemas operativos incorporados baseados no Windows 7 (32 bits)** incluem o seguinte:  
>   
>      -   Windows Embedded Standard 7 (32 bits)  
>     -   Windows Embedded POSReady 7 (32 bits)  
>     -   Windows ThinPC  
> -   **Os sistemas operativos incorporados baseados no Windows 7 (64 bits)** incluem o seguinte:  
>   
>      -   Windows Embedded Standard 7 (64 bits)  
>     -   Windows Embedded POSReady 7 (64 bits)
