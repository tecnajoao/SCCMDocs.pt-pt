---
title: Preparar a instalação de sites
titleSuffix: Configuration Manager
description: Se estiver a planear instalar vários sites do Configuration Manager, estas informações para ajudar a poupar tempo e para evitar erros de leitura.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f07a321ac6f10f5287a88d0df7064920f538ae5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Preparar a instalação de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para preparar para uma implementação com êxito de um ou mais sites do System Center Configuration Manager, se familiarize com os detalhes deste artigo. Estes passos podem poupar tempo durante a instalação de vários sites e ajudar a evitar missteps que poderão resultar na necessidade de reinstalar um ou mais sites.

> [!TIP]
> Ao gerir o site do System Center Configuration Manager e a infraestrutura de hierarquia, os termos de licenciamento *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes. Para saber como cada termo é utilizado, consulte [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).

## <a name="bkmk_options"></a> Opções para a instalação de diferentes tipos de sites
Quando instala um novo site do Configuration Manager, a versão dos ficheiros de origem que pode utilizar depende da versão de sites que já estão a ser a hierarquia (se aplicável). Os métodos de instalação que pode utilizar dependem do tipo de site que pretende instalar.  

Antes de instalar um site, certifique-se ter planeou a sua hierarquia e que compreende o tipo de site que pretende instalar. Para obter mais informações, consulte [estruturar uma hierarquia de sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Primeiro site
O primeiro site que instalar numa hierarquia será um site primário autónomo ou um site de administração central.

**Suporte de instalação**: Para instalar um site de administração central ou um site primário autónomo como o primeiro site numa nova hierarquia, deve [utilizar uma versão de linha de base](../../../../core/servers/manage/updates.md#bkmk_Baselines) do Configuration Manager. Não instalar o primeiro site numa nova hierarquia utilizando ficheiros de origem atualizados a partir de [CD. Pasta mais recente](../../../../core/servers/manage/the-cd.latest-folder.md) de qualquer site.

**Método de instalação**: Pode instalar o tipo de site utilizando o [Assistente de configuração do Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md), ou pode configurar um script para utilizar com um [convertidos em script de instalação da linha de comandos](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites adicionais
Após a instalação de site inicial, pode adicionar mais sites em qualquer altura. Tem as seguintes opções para adicionar sites (até [suportado limites](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Site tiver|Tipo de site adicionais que pode instalar|
|---|---|
|Site de administração central|Site principal subordinado|
|Site principal subordinado|Site Secundário|
|Site primário autónomo|Site secundário (pode expandir o site primário, que converte o site primário autónomo a um site primário subordinado)|

**Suporte de instalação**: Quando instala um site de administração central para expandir um site primário autónomo ou, se instalar um novo site primário subordinado numa hierarquia existente, tem de utilizar suportes de dados de instalação (que contém ficheiros de origem) que corresponde à versão do site existente ou sites.

> [!IMPORTANT]
> Se instalou atualizações na consola que alteraram a versão dos sites anteriormente instalados, não utilize o suporte de dados de instalação original. Em alternativa, utilize ficheiros de origem nesse cenário, o [CD. Pasta mais recente](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Configuration Manager requer a utilização de ficheiros de origem que corresponde à versão do site existente que o novo site irá ligar ao.

Um site secundário tem de ser instalado a partir da consola do Configuration Manager. Desta forma, os sites secundários são sempre instalados através da utilização de ficheiros de origem do site primário principal.

**Método de instalação**: O método utilizado para instalar sites adicionais depende do tipo de site que pretende instalar.
-   **Adicionar um site de administração central**:  Pode utilizar o Assistente de configuração do Configuration Manager ou uma linha de comandos de script para instalar o novo site de administração central como site principal para o site primário autónomo existente. Para obter mais informações, consulte [expandir um site primário autónomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Adicionar um site primário subordinado**:  Pode utilizar o Assistente de configuração do Configuration Manager ou uma instalação de linha de comandos para adicionar um site primário subordinado abaixo de um site de administração central.
-   **Adicionar um site secundário**:  Utilize a consola do Configuration Manager para instalar um site secundário como site subordinado abaixo de um site primário. Outros métodos não são suportados para adicionar os sites secundários.

## <a name="bkmk_tasks"></a>  Tarefas comuns para concluir antes de iniciar uma instalação
-   **Compreender a topologia da hierarquia que irá utilizar para a implementação**    
Para obter mais informações, consulte [estruturar uma hierarquia de sites para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

-   **Preparar e configurar servidores individuais para satisfazer os pré-requisitos e as configurações suportadas para utilização com o Configuration Manager**         
Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

-   **Instalar e configurar o SQL Server para alojar a base de dados do site**     
Para obter mais informações, consulte [suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Preparar o ambiente de rede para suportar o Configuration Manager**      
Para obter mais informações, consulte [configurar firewalls, portas e domínios para se preparar para o Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Se pretender utilizar uma infraestrutura de chaves públicas (PKI), prepare a sua infraestrutura e certificados**      
Para obter mais informações, consulte [requisitos de certificado PKI para o Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

-   **Instalar as atualizações de segurança mais recentes em computadores que irá utilizar como servidores do site ou servidores do sistema de sites e, quando for necessário, reiniciá-las**

## <a name="bkmk_sitecodes"></a>  Sobre os nomes de site e códigos de site
Códigos de site e os nomes de site são utilizados para identificar e gerir os sites numa hierarquia do Configuration Manager. Na consola do Configuration Manager, o código do site e o nome de site são apresentados no &lt; *código do site*\> - &lt;*nome do site* \> formato. Todos os códigos de site que utiliza na sua hierarquia tem de ser exclusivo. Se o esquema do Active Directory é expandido para o Configuration Manager e os sites estiverem a publicar dados, os códigos de site utilizados numa floresta do Active Directory tem de ser exclusivos, mesmo que se estão a ser utilizadas numa hierarquia do Configuration Manager diferente ou se que tenham sido utilizados em instalações anteriores do Configuration Manager. Lembre-se de que planeia cuidadosamente os códigos de site e os nomes de site antes de implementar a hierarquia.

### <a name="specify-a-site-code-and-site-name"></a>Especifique um código de site e o nome do site
Quando executar a configuração do Configuration Manager, lhe for pedido um código de site e o nome do site para o site de administração central e para cada site primário e a instalação do site secundário. Um código de site deve identificar de forma exclusiva cada site na hierarquia. Como o código do site é utilizado em nomes de pastas, nunca utilize os seguintes nomes para o código de site, que incluem nomes reservados para o Configuration Manager e o Windows:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuração do Configuration Manager verifica se um código de site já não está a ser utilizado.

Introduza o código do site para um site quando estiver a executar o programa de configuração do Configuration Manager, tem de introduzir três carateres alfanuméricos. Apenas as letras *A* através de *Z* e os números *0* através de *9*, qualquer combinação, são permitidas em códigos de site. A sequência de letras ou números não tem efeito na comunicação entre sites. Por exemplo, não é necessário para o nome de um site primário *ABC* e um site secundário *DEF*.

O nome do site é um identificador de nome amigável para o site. Só pode utilizar os carateres *A* através de *Z*, *um* através de *z*, *0* através de *9*e o hífen (*-*) em nomes de site.

> [!IMPORTANT]
> Não é suportada uma alteração do código do site ou o nome de site após a instalação do site.

### <a name="reuse-a-site-code"></a>Reutilizar um código de site
Códigos de site não não possível utilizar mais do que uma vez numa hierarquia do Configuration Manager para um site de administração central ou para um site primário, mesmo que o original site e o código de site tem sido desinstalados. Se reutilizar um código de site, o risco de ter conflitos de ID de objeto na sua hierarquia. Pode reutilizar o código do site para um site secundário se esse site secundário e o código do site já não estão em utilização na sua hierarquia do Configuration Manager ou na floresta do Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limites e restrições para os sites instalados
Antes de instalar um site, é importante compreender as seguintes limitações que se aplicam a sites e hierarquias de sites:
-   Depois de executar o programa de configuração, não é possível alterar as seguintes propriedades do site sem desinstalar o site e, em seguida, reinstalá-lo ao utilizar os novos valores:  
  -   Diretório de instalação de ficheiros de programa  
  -   Código do site  
  -   Descrição do site  
-   Quando a hierarquia inclui um site de administração central:  
  -   O Configuration Manager não suporta a mover de um site primário subordinado fora de uma hierarquia para criar um site primário autónomo ou ligue-o para uma hierarquia diferente. Em vez disso, desinstale o site primário subordinado e, em seguida, reinstalá-la como um novo site primário autónomo ou como um site subordinado do site de administração central de uma hierarquia diferente.  


## <a name="bkmk_optionalsteps"></a>  Passos opcionais antes de executar o programa de configuração
**Executar manualmente [dispositivo de transferência da configuração](../../../../core/servers/deploy/install/setup-downloader.md)**

Para transferir os ficheiros de configuração atualizados para o Configuration Manager, pode executar o programa de configuração. Se o computador onde irá executar a configuração não está ligado à Internet ou se pretende instalar vários servidores de site, considere utilizar o dispositivo de transferência da configuração para transferir as atualizações necessárias para a configuração. Segue-se informações adicionais:
-  Por predefinição, o programa de configuração estabelece ligação à Internet para transferir ficheiros de configuração atualizados.
-  Por predefinição, os ficheiros são armazenados na pasta Redist.
-  Pode direcionar a configuração para uma localização na sua rede onde tenha anteriormente armazenado uma cópia destes ficheiros.

**Executar manualmente [Verificador de pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Para identificar e corrigir problemas antes de executar a configuração para instalar um site e antes de instalar uma função de sistema de sites num servidor, pode executar o Verificador de pré-requisitos. Verificador de pré-requisitos ajuda a garantir que o computador cumpre os requisitos para alojar o site ou função do sistema de sites. Segue-se informações adicionais:
 -  Por predefinição, a configuração executa o Verificador de pré-requisitos.
 -  Se existirem erros, o programa de configuração para até o problema ser corrigido.

**Identifique portas opcionais**

Pode identificar portas opcionais para sistemas de sites e clientes para utilizarem. Segue-se informações adicionais:
 -  Por predefinição, clientes e sistemas de sites utilizam portas predefinidas para comunicar.
 -  Durante a configuração, pode configurar portas alternativas.

 Para obter mais informações, consulte [portas utilizadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md).
