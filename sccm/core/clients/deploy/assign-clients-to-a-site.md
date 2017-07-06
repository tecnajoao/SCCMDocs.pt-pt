---
title: Atribuir clientes a um site | Documentos do Microsoft
description: Atribua clientes a um site no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: a0ccd453fbe346c239eb6e37bc3ed557487b1e27
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>Como atribuir clientes a um site no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Após um cliente do System Center Configuration Manager está instalado, tem associar um site primário do Configuration Manager, antes de poder geri-lo. O site que associa um cliente é designado por respetivo *site atribuído*. Os clientes não podem ser atribuídos a um site de administração central ou a um site secundário.  

O processo de atribuição ocorre após o cliente é instalado com êxito e determina qual o site que gere o computador cliente. Pode optar entre atribuir diretamente o cliente a um site ou, pode utilizar a atribuição automática de sites onde o cliente encontrará automaticamente um site apropriado com base na respetiva localização de rede atual ou um site de contingência que tenha sido configurado para a hierarquia.

Quando instala o cliente do dispositivo móvel durante a inscrição do Gestor de configuração, o dispositivo é sempre automaticamente atribuído a um site. Ao instalar o cliente num computador, pode escolher se pretende atribuir o cliente a um site ou não. No entanto, se o cliente estiver instalado mas não atribuído, permanecerá não gerido até a atribuição de site ser concluída com êxito.  
 

> [!NOTE]  
>  Sempre atribua clientes a sites que executem a mesma versão do Configuration Manager. Evite atribuir um cliente do Configuration Manager a partir de uma versão mais recente para um site a partir de uma versão mais antiga.   Se necessário, atualize o site primário para a mesma versão do Configuration Manager que está a utilizar para os clientes.  

Após o cliente ser atribuído a um site, permanecerá atribuído a esse site mesmo que o cliente altere o respetivo endereço IP ou faça roaming para outro site. Apenas um administrador pode atribuir o cliente a outro site ou remover a atribuição de cliente manualmente.  

> [!WARNING]  
>  A exceção à permanência da atribuição de um cliente a um site verifica-se quando o cliente é atribuído num dispositivo Windows Embedded enquanto os filtros de escrita estão ativados. Se não desativar em primeiro lugar os filtros de escrita que atribuiu ao cliente, o estado de atribuição de site do cliente regressará ao estado original durante o próximo reinício do dispositivo.  
>   
>  Por exemplo, se o cliente estiver configurado para a atribuição automática de sites, a reatribuição será feita durante o arranque e poderá resultar na atribuição a um site diferente. Se o cliente não está configurado para atribuição automática de site, mas necessita de uma atribuição manual do site, é de reatribuir manualmente o cliente após o arranque antes de poder gerir novamente este cliente utilizando o Gestor de configuração.  
>   
>  Para evitar este comportamento, desative os filtros de escrita antes de atribuir o cliente em dispositivos incorporados e, em seguida, ative os filtros de escrita após ter confirmado que a atribuição do site foi concluída com êxito.  

Se falhar a atribuição de cliente, o software de cliente permanecerá instalado, mas não será gerido. Um cliente é considerado não gerido quando é instalado, mas não atribuído a um site, ou quando é atribuído a um site mas não consegue comunicar com um ponto de gestão.  

##  <a name="using-manual-site-assignment-for-computers"></a>Utilizar a atribuição manual de sites a computadores  
 Pode atribuir manualmente computadores cliente a um site utilizando os dois métodos seguintes:  

-   Utilize uma propriedade de instalação de cliente que especifique o código do site.  

-   Em **Configuration Manager**do Painel de Controlo, especifique o código do site.  

> [!NOTE]  
>  Se atribuir manualmente um computador cliente para um código de site do Configuration Manager que não existe, a atribuição de site falhará.   

##  <a name="BKMK_AutomaticAssignment"></a> Utilizar a atribuição automática de sites a computadores  
 A atribuição automática de site pode ocorrer durante a implementação do cliente ou quando clica na opção **Procurar Site** do separador **Avançadas** das **Propriedades do Configuration Manager** no Painel de Controlo. O cliente do Configuration Manager compara a respetiva localização de rede com os limites que são configurados na hierarquia do Configuration Manager. Quando a localização de rede do cliente reside num grupo de limites que está ativada para atribuição de sites, ou a hierarquia está configurada para um site de contingência, o cliente é automaticamente atribuído a esse site sem que o operador precise de especificar um código de site.  

 Pode configurar limites utilizando um ou mais dos seguintes procedimentos:  

-   Sub-rede IP  

-   Site de Active Directory  

-   Prefixo IP v6  

-   Intervalo de endereços IP  

> [!NOTE]  
>  Se um cliente do Configuration Manager possui várias placas de rede e, por conseguinte, dispuser de vários endereços IP, o endereço IP utilizado para atribuição de um site de cliente de evaluate é atribuído aleatoriamente.  

 Para obter informações sobre como configurar grupos de limites para a atribuição de sites e configurar um site de contingência para atribuição automática de sites, veja [Definir limites de site e grupos de limites do System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Clientes do Configuration Manager que utilizam a atribuição automática de site tentam localizar grupos de limites que são publicados nos serviços de domínio do Active de sites. Se isto falhar (por exemplo, o Active Directory esquema não estiver expandido para o Configuration Manager, nem os clientes forem computadores de um grupo de trabalho), os clientes podem obter informações do grupo de limites a partir de um ponto de gestão.  

 Pode especificar um ponto de gestão para ser utilizado pelos computadores cliente após serem instalados ou os clientes podem localizar um ponto de gestão utilizando a publicação de DNS ou WINS.  

 Se o cliente não conseguir encontrar um site que esteja associado a um grupo de limites que contenha a respetiva localização de rede e caso a hierarquia não disponha de um site de contingência, o cliente tentará novamente de 10 em 10 minutos até conseguir ser atribuído a um site.  

 Computadores de cliente do Configuration Manager não podem ser automaticamente atribuídos a um site, se qualquer uma das situações seguintes e, em seguida, estes têm de ser manualmente atribuídos:  

-   Estão atualmente atribuídos a um site.  

-   Encontram-se na Internet ou configurados como clientes apenas de Internet.  

-   A respetiva localização de rede não coincide com nenhum dos grupos de limites configurados na hierarquia do Configuration Manager e não existe nenhum site de contingência para a hierarquia.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>A concluir a atribuição de site através da verificação da compatibilidade do site  
 Após um cliente encontrar o respetivo site atribuído, a versão e o sistema operativo do cliente é verificado para garantir que um site do Configuration Manager pode geri-lo. Por exemplo, o Configuration Manager não consegue gerir clientes do Configuration Manager 2007, os clientes do System Center 2012 Configuration Manager nem os clientes que executem o Windows 2000.  

 Atribuição de site falha se atribuir um cliente que execute o Windows 2000 a um site do Configuration Manager. Quando atribui um cliente do Configuration Manager 2007 ou um cliente do System Center 2012 Configuration Manager para um site do Configuration Manager (ramo atual), a atribuição de site tem êxito e suporta a atualização automática de cliente. No entanto, até que os clientes antigos e geração sejam atualizados para um cliente do Configuration Manager (ramo atual), o Configuration Manager não é possível gerir este cliente utilizando as definições de cliente, aplicações ou atualizações de software.  

> [!NOTE]  
>  Para suportar a atribuição de site de um Configuration Manager 2007 ou um cliente do System Center 2012 Configuration Manager para um site do Configuration Manager (ramo atual), tem de configurar a atualização automática de cliente para a hierarquia. Para obter mais informações, veja [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

O Configuration Manager também verifica se foi atribuído o cliente do Configuration Manager (ramo atual) a um site que o suporta. Os cenários seguintes podem ocorrer durante a migração a partir de versões anteriores do Gestor de configuração.  

-   Cenário: Pode ter utilizado a atribuição automática de site e os limites sobrepõem as definidas numa versão anterior do Configuration Manager.  

     Neste caso, o cliente tenta automaticamente localizar um site do Configuration Manager (ramo atual).  

     O cliente verifica primeiro os serviços de domínio do Active Directory e se encontrar um site do Configuration Manager (ramo atual) publicado, a atribuição de site é concluída com êxito. Se isto falhar (por exemplo, o Gestor de configuração do site não está publicado ou o computador for um cliente de grupo de trabalho), o cliente procurará em seguida informações sobre o site a partir do ponto de gestão atribuído.  

    > [!NOTE]  
    >  Pode atribuir um ponto de gestão para o cliente durante a instalação do cliente utilizando a propriedade de Client. msi **SMSMP =&lt;nome_do_servidor >**.  

     Se ambos estes métodos falharem, a atribuição do site não terá êxito e deverá atribuir manualmente o cliente.  

-   Cenário: Tem de atribuir o cliente do Configuration Manager (ramo atual), utilizando um código de site específico em vez de atribuição automática de site e especificou um código de site para uma versão do Configuration Manager anterior ao System Center 2012 R2 Configuration Manager.  

     Neste caso, a atribuição de site falha e, de reatribuir manualmente o cliente a um site do Configuration Manager (ramo atual).  

 A verificação de compatibilidade do site requer uma das seguintes condições:  

-   O cliente consegue aceder às informações do site publicadas nos Serviços de Domínio do Active Directory.  

-   O cliente consegue comunicar com um ponto de gestão do site.  

 Se a verificação de compatibilidade do site não conseguir concluir com êxito, a atribuição de site falhará e o cliente permanecerá não gerido até a verificação de compatibilidade do site será novamente executado e ser bem sucedida.  

 A exceção à realização da verificação de compatibilidade do site ocorre quando um cliente se encontra configurado para um ponto de gestão baseado na Internet. Neste caso, não é efetuada nenhuma verificação de compatibilidade do site. Se estiver a atribuir clientes a um site que contém sistemas de sites baseados na Internet e especificar um ponto de gestão baseado na Internet, certifique-se de que está a atribuir o cliente ao site correto. Se atribuir por engano o cliente a um site do Configuration Manager 2007, um site do System Center 2012 Configuration Manager, ou a um site do Configuration Manager que não tem funções do sistema de sites baseados na Internet, o cliente deixará de ser gerido.  

##  <a name="locating-management-points"></a>Localizar pontos de gestão  
 Quando um cliente é atribuído com êxito a um site, localiza um ponto de gestão nesse site.  

 Computadores cliente transferem uma lista de pontos de gestão que se possam ligar a no site. Isto acontece quando o cliente é reiniciado, ou cada 25 horas ou se o cliente detete uma alteração de rede, tais como o computador desliga e volta a ligar na rede ou receber um novo endereço IP. A lista inclui os pontos de gestão na intranet e a indicação de que aceitam ligações de cliente através de HTTP ou HTTPS. Quando o computador cliente se encontra na Internet e o cliente ainda não tem uma lista de pontos de gestão, estabelece a ligação ao ponto de gestão especificado baseado na Internet para obter uma lista de pontos de gestão. Se o cliente dispuser de uma lista de pontos de gestão para o respetivo site atribuído, selecionará um ponto para estabelecer a ligação:  

-   Quando o cliente se encontra na intranet e dispõe de um certificado PKI válido que pode utilizar, o cliente escolhe os pontos de gestão HTTPS antes dos pontos de gestão HTTP. Em seguida, localiza o ponto de gestão mais próximo, com base na respetiva associação de floresta.  

-   Quando o cliente está na Internet, aleatoriamente escolhe um dos pontos de gestão baseado na Internet.  

Dispositivo móvel, os clientes que são inscritos pelo Configuration Manager só ligarem a gestão de um ponto no respetivo site atribuído e nunca a pontos de gestão em sites secundários. Estes clientes ligam-se sempre através de HTTPS e o ponto de gestão tem de ser configurado para aceitar ligações de cliente através da Internet. Quando existe mais do que um ponto para clientes de dispositivos móveis no site primário, o Configuration Manager seleciona aleatoriamente um dos seguintes pontos de gestão durante a atribuição e o cliente do dispositivo móvel continuará a utilizar o mesmo ponto de gestão.  

Se o cliente tiver transferido a política de cliente a partir de um ponto de gestão do site, o cliente torna-se um cliente gerido.  

##  <a name="downloading-site-settings"></a>A transferir as definições do site  
 Após a atribuição do site com êxito e o cliente ter encontrado um ponto de gestão, um computador cliente que utilize os Serviços de Domínio do Active Directory para a respetiva verificação de compatibilidade com um site transfere as definições de site relacionadas com o cliente para o respetivo site atribuído. Estas definições incluem os critérios de seleção de certificado de cliente, de utilização de uma lista de revogação de certificados e os números de porta para pedidos de cliente. O cliente continuará a verificar periodicamente estas definições.  

 Quando os computadores cliente não conseguem obter as definições a partir dos Serviços de Domínio do Active Directory, transferem-nos a partir do respetivo ponto de gestão. Computadores cliente também podem obter as definições do site quando são instalados utilizando push de cliente, ou pode especificá-las manualmente utilizando as propriedades de instalação CCMSetup.exe e cliente. Para obter mais informações sobre as definições de instalação do cliente, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>A transferir as definições do cliente  
 Todos os clientes transferem a política de predefinições de cliente, bem como outras políticas personalizadas de definições de cliente aplicáveis. O Centro de Software baseia-se nestas políticas de configuração de clientes para os computadores com Windows e notificará os utilizadores de que não será possível executar o Centro de Software com êxito enquanto estas informações de configuração estiverem a ser transferidas. Dependendo das definições de cliente configuradas, a transferência inicial das definições de cliente poderão demorar algum tempo e algumas tarefas de gestão de clientes poderão não ser executadas até que este processo esteja concluído.  

##  <a name="verifying-site-assignment"></a>Verificar a atribuição de sites  
 Pode verificar o êxito da atribuição de site por qualquer um dos seguintes métodos:  

-   Para clientes em computadores Windows, utilize o Gestor de configuração no painel de controlo e certifique-se de que o código do site é apresentado corretamente no **Site** separador.  

-   Para computadores cliente, no **ativos e compatibilidade** área de trabalho > **dispositivos** nó, certifique-se de que o computador apresenta **Sim** para o **cliente** coluna e o site primário correto código a **código do Site** coluna.  

-   Para clientes de dispositivos móveis, na área de trabalho **Ativos e Compatibilidade** , utilize a coleção **Todos os Dispositivos Móveis** para verificar se o dispositivo móvel apresenta **Sim** na coluna **Cliente** e o código do site primário correto na coluna **Código do Site** .  

-   Utilize os relatórios para a atribuição de clientes e a inscrição do dispositivo móvel.  

-   Para computadores cliente, utilize o ficheiro LocationServices.log no cliente.  

##  <a name="roaming-to-other-sites"></a>Itinerância para outros sites  
 Quando os computadores cliente da intranet são atribuídos a um site primário, mas a localização da rede é alterada para ficarem incluídos num grupo de limites configurado para outro site, estes foram movidos para outro site. Quando este site é um site secundário do respetivo site atribuído, os clientes podem utilizar um ponto de gestão no site secundário para transferir a política de cliente e carregar dados do cliente, o que evita o envio destes dados através de uma rede potencialmente lenta. Porém, se estes clientes se moverem para os limites de outro site primário ou de um site secundário que não é um site subordinado do respetivo site atribuído, estes clientes utilizam sempre um ponto de gestão no seu site atribuído para transferir a política de cliente e carregar dados para o respetivo site.  

 Estes computadores cliente que se movem para outros sites (todos os sites primários e todos os sites secundários) podem sempre utilizar pontos de gestão noutros sites para pedidos de localização de conteúdo. Os pontos de gestão do site atual podem proporcionar aos clientes uma lista dos pontos de distribuição que possuem o conteúdo solicitados pelos clientes.  

 Para computadores cliente que estão configurados para gestão de clientes apenas de Internet e para dispositivos móveis e computadores Mac que são inscritos pelo Configuration Manager, estes clientes só comunicam com pontos de gestão do respetivo site atribuído. Estes clientes nunca comunicam com pontos de gestão de sites secundários nem com pontos de gestão de outros sites primários.  
