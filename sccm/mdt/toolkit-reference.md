---
title: "Referência do Toolkit"
titleSuffix: Microsoft Deployment Toolkit
description: "Detalhes de referência para o Microsoft implementação Toolkit 2013. "
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: ac670143-b7cd-47d0-86ed-14cb2554dfc7
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f9bd3e2d61ca8b1eddb83fd75de62ba4a123bb7a
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
---
# <a name="toolkit-reference-for-the-microsoft-deployment-toolkit"></a>Toolkit de referência para o Microsoft Deployment Toolkit
 Esta referência faz parte do Microsoft® Deployment Toolkit (MDT) 2013 e fornece definições de configuração que pode utilizar o processo de implementação. Reveja os documentos do MDT 2013 *guia de amostras do Toolkit de implementação do Microsoft* e *utilizar o Microsoft Deployment Toolkit* para obter ajuda na personalizar as definições de configuração para o ambiente de implementação.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

## <a name="task-sequence-steps"></a>Passos de sequência de tarefas  
 *As sequências de tarefas* são criados pelo Editor de sequência de tarefas e consistem de uma série de passos que foram concebidos para concluir uma ação combinada. Sequências de tarefas podem funcionar através de um reinício do computador e podem ser configuradas para automatizar tarefas num computador sem necessitarem da intervenção do utilizador. Além disso, pode adicionar passos de sequência de tarefas para um grupo de sequência de tarefas, o que ajuda a manter os passos de sequência de tarefas semelhantes para uma melhor organização e controlo de erros.  

 Cada passo de sequência de tarefas executa uma tarefa específica, como validar que é capaz de receber a imagem de implementação, armazenar os dados de utilizador numa localização segura, implementar uma imagem para um computador de destino, o computador de destino e restaurar a guardar dados de utilizador. Estes passos de sequência de tarefas realizar as respetivas tarefas utilizando utilitários e scripts fornecidos com o MDT ou pela equipa de implementação. Utilize esta referência para ajudar a determinar os grupos de sequências de tarefas correta e passos de sequência de tarefas para configurar o processo de implementação e o válido propriedades e opções para utilizar.  

 As seguintes informações são fornecidas para cada grupo de sequência de tarefas e passo:  

-   **Nome**. O nome do passo ou grupo de sequência de tarefas  

-   **Descrição**. Uma descrição da finalidade do grupo de sequência de tarefas ou passo e quaisquer informações sobre a personalização pertinentes  

-   **Propriedades**. Indica as propriedades de configuração válida que pode especificar para o passo ou grupo de sequência de tarefas que definem a forma como a tarefa é executada  

-   **Opções de**. Indica as opções de configuração válida que pode especificar para o passo ou grupo de sequência de tarefas que definem se e quando a tarefa é executada e o que é considerado um código de saída com êxito da tarefa  

 Para obter mais informações sobre o Editor de sequência de tarefas, consulte [implementação do sistema operativo: Editor de sequência de tarefas](http://technet.microsoft.com/library/bb680396.aspx).  

###  <a name="CommonPropertiesandOptionsforTaskSequenceStepTypes"></a>Propriedades e opções para tipos de passo de sequência de tarefas comuns  
 Cada grupo de sequência de tarefas e passo tem as definições configuráveis o **propriedades** e **opções** separadores que são comuns a todos os grupos de sequências de tarefas e passos. Estas definições comuns que são descritas nas secções seguintes.  

#### <a name="common-properties"></a>Propriedades comuns
 Tabela 1 mostra as definições que estão disponíveis no **propriedades** separador de cada passo de sequência de tarefas. Para obter mais informações sobre o **propriedades** separador para um passo de sequência de tarefas específica, consulte o tópico correspondente para o passo posterior nesta referência.  

> [!NOTE]
>  Os tipos de passo de sequência de tarefas aqui listados são as que estão disponíveis no Deployment Workbench. Tipos de passo de sequência de tarefas adicionais poderão estar disponíveis quando configurar sequências de tarefas utilizando o Microsoft System Center 2012 R2 Configuration Manager.  

##### <a name="table-1-settings-available-on-the-properties-tab"></a>Tabela 1. Definições estão disponíveis no separador de propriedades  

|**Nome**|**Descrição**|**Grupo**|**Passo**|  
|-|-|-|-|  
|**Tipo**|Um valor só de leitura que indica o tipo de grupo ou passo da sequência de tarefas. O tipo de será definido para um dos seguintes valores:<br /><br /> -Aplicar definições de rede<br /><br /> -Autorizar DHCP<br /><br /> -Capturar definições de rede<br /><br /> -Configurar o ADDS<br /><br /> -Configurar o DHCP<br /><br /> -Configurar o DNS<br /><br /> -Ativar o BitLocker<br /><br /> -Formatar e particionar disco<br /><br /> -Recolher<br /><br /> -Grupo<br /><br /> -Inserir controladores<br /><br /> -Instale a aplicação<br /><br /> -Instalar o sistema operativo<br /><br /> -Instalar funções e funcionalidades<br /><br /> -Instalar atualizações Offline<br /><br /> -Recuperar de uma falha de associação de domínio<br /><br /> -Reiniciar computador<br /><br /> -Executar linha de comandos<br /><br /> -Validar|-|-|  
|**Nome**|Um nome definido pelo utilizador que deve permitir a identificação fácil e de diferenciação de outra tarefa passos de sequência.|-|-|  
|**Descrição**|Uma descrição definida pelo utilizador que deve tornar os requisitos de passo de sequência de tarefas e as tarefas facilmente compreensíveis.|-|-|  

#### <a name="common-options"></a>Opções comuns  
 Tabela 2 mostra as definições que estão disponíveis no separador Opções do passo de sequência de tarefas. Para mais informações sobre o separador de opções, consulte [separador de opções de sequência de tarefas](http://technet.microsoft.com/library/bb693661.aspx).  

##### <a name="table-2-settings-available-on-the-options-tab"></a>Tabela 2. Definições estão disponíveis no separador Opções  

|**Nome**|**Descrição**|**Grupo**|**Passo**|  
|-|-|-|-|
|**Desativar este passo**|Selecione esta opção para desativar este passo de sequência de tarefas.|-|-|  
|**Códigos de êxito**|Sair códigos de utilitário associados a este passo de sequência de tarefas que indicam que o passo foi concluída com êxito.||-|  
|**Continuar com o erro** |Selecione esta opção para permitir que o sequenciador de tarefas processar os passos de sequência de tarefas adicionais se ocorrer uma falha.|-|-|  
|**Instruções condicionais**|Uma ou mais condições que limitam a execução deste passo ou grupo de sequência de tarefas. Estes condicional baseiam-se nos seguintes:<br /><br /> -Propriedades do ficheiro<br /><br /> -As propriedades da pasta<br /><br /> Versão do sistema operativo:<br /><br /> -É uma arquitetura de determinados<br /><br /> -É uma determinada versão<br /><br /> -Consulta Windows Management Instrumentation (WMI)<br /><br /> Definição do registo:<br /><br /> -Existe<br /><br /> -Não existe<br /><br /> -Igual a<br /><br /> -Não igual<br /><br /> -Superior a<br /><br /> -Maior ou igual a<br /><br /> -Inferior a<br /><br /> -Menor ou igual a<br /><br /> -Software instalado<br /><br /> Variável de sequência de tarefas:<br /><br /> -Existe<br /><br /> -Igual a<br /><br /> -Não igual<br /><br /> -Superior a<br /><br /> -Maior ou igual a<br /><br /> -Inferior a<br /><br /> -Menor ou igual a<br /><br /> Estas condições podem ser agrupadas utilizando **se** instruções testam todas as condições, qualquer condição ou nenhuma condição que avalia como verdadeiro.|-|-|  

> [!NOTE]
>  As instruções condicionais adicionais poderão estar disponíveis ao utilizar o Gestor de configuração para configurar os passos de sequência de tarefas.  

###  <a name="SpecificPropertiesandSettingsforTaskSequenceStepTypes"></a>Propriedades específicas e definições de tipos de passo de sequência de tarefas  
 Algumas propriedades e os parâmetros de cada tipo de passo de sequência de tarefas são exclusivos para esse tipo. Cada tipo com definições de propriedades exclusivas e é apresentado nas seguintes secções com a definições e propriedades de passo de sequência de tarefas exclusivo.  

#### <a name="apply-network-settings"></a>Aplicar Definições de Rede  
 Este passo de sequência de tarefas configura o adaptador de rede no computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTINICConfig.wsf](#ZTINICConfig.wsf).  

 As propriedades exclusivas e definições para o **aplicar definições de rede** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Aplicar Definições de Rede|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Nome**|O nome a atribuir à ligação de rede.|  
|**Obter um endereço IP automaticamente**|Quando selecionada, o protocolo de configuração dinâmica de anfitrião (DHCP) é utilizado para obter as definições necessárias para a configuração de Internet Protocol (IP) para a ligação de rede. Esta é a seleção predefinida.|  
|**Utilize o seguinte endereço IP**|Quando selecionada, pode fornecer um ou mais IP endereço e a sub-rede máscara combinações para além de gateways que serão atribuídos à ligação de rede.|  
|**Obter automaticamente um servidor de sistema de nomes de domínio (DNS)**|Quando selecionada, é utilizado o DHCP para obter as definições necessárias para a configuração de IP para a ligação de rede. Esta é a seleção predefinida.|  
|**Utilize os seguintes servidores DNS**|Quando selecionada, pode fornecer um ou mais DNS endereços IP do servidor que serão atribuídos à ligação de rede.|  
|**Sufixo DNS**|O sufixo DNS que será aplicado a todas as ligações de rede que utilizam o TCP/IP.|  
|**Registar o endereço desta ligação no DNS**|Especifica que o computador irá tentar registo dinâmico dos endereços IP (através de DNS) desta ligação com o nome completo do computador deste computador.|  
|**Utilize o sufixo DNS desta ligação no registo de DNS**|Especifica se a atualização dinâmica de DNS é utilizada para registar os endereços IP e o nome de domínio específico da ligação desta ligação.|  
|**Endereços de servidor WINS**|Pode fornecer servidor Windows Internet Naming Service (WINS) de um ou mais endereços IP que serão atribuídos à ligação de rede.|  
|**Ativar procura LMHOSTS**|Especifica se é utilizado um ficheiro de anfitriões Manager (LMHOSTS) de rede de área local (LAN) para resolução de nomes de sistema (NetBIOS) de rede básica entrada/saída.|  
|**Predefinição**|Especifica se esta ligação de rede obtém a definição para ativar ou desativar NetBIOS por TCP/IP (NetBT) de um servidor DHCP. Esta é a seleção predefinida.|  
|**Ativar o NetBIOS sobre TCP/IP**|Especifica que esta ligação de rede utiliza NetBT e WINS.|  
|**Desativar NetBIOS por TCP/IP**|Especifica que esta ligação de rede utiliza NetBT e o WINS.|  

#### <a name="authorize-dhcp"></a>Autorizar DHCP  
 Este passo de sequência de tarefas autoriza o computador de destino como um servidor DHCP. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIAuthorizeDHCP.wsf](#ZTIAuthorizeDHCP.wsf).  

 As propriedades exclusivas e definições para o **autorizar DHCP** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  

|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **autorizar o servidor de DHCP**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nome**|**Descrição**|  
|**Conta**|Uma conta de utilizador que seja membro do grupo Admins da empresa, a ser utilizado quando a autorização de DHCP para o computador de destino.|  

#### <a name="capture-network-settings"></a>Capturar definições de rede  
 Este passo de sequência de tarefas reúne as definições de adaptador de rede do computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTINICConfig.wsf](#ZTINICConfig.wsf).  

 As propriedades exclusivas e definições para o **capturar definições de rede** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|
|-|-|  
|**Nome**|**Descrição**|  
|**Tipo**|Definir este tipo de só de leitura **capturar definições de rede**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|Nenhum|Nenhum|  

#### <a name="configure-adds"></a>Configurar o ADDS  
 Este passo de sequência de tarefas configura o computador de destino como um controlador de domínio de serviços de domínio do Active Directory® (AD DS). Para obter mais informações sobre as definições apresentadas as tabelas seguintes e que pode configurar este passo de sequência de tarefas, consulte o artigo e suporte da Microsoft Help [automática a promoção e despromoção de domínio do Windows 2000 e no Windows Server 2003 controladores](http://support.microsoft.com/kb/223757).  

 As propriedades exclusivas e definições para o **configurar adiciona** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **configurar adiciona**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|Criar|Especifica o conjunto de configuração que será utilizado para configurar o computador de destino. Os conjuntos de configuração são:<br /><br /> - **Nova réplica do controlador de domínio**. Cria um controlador de domínio adicional num domínio existente do AD DS<br /><br /> - **Nova réplica (RODC) do controlador de domínio só de leitura**. Cria um RODC<br /><br /> - **Novo domínio numa floresta existente**. Cria um domínio numa floresta existente do AD DS<br /><br /> - **Nova árvore de domínio numa floresta existente**. Cria uma nova árvore numa floresta existente do AD DS<br /><br /> - **Nova floresta**. Cria uma nova floresta do AD DS|  
|**Nome DNS de domínio**|O nome DNS do domínio novo ou existente.|  
|**Nome NetBIOS do domínio**|O nome NetBIOS do novo domínio subordinado, árvore de domínio subordinado ou floresta pre-AD DS utilizam para aceder ao domínio. Este nome tem de ser exclusivo na rede.|  
|**Nome DNS**|O nome DNS do domínio subordinado ou árvore de domínio.|  
|**Controlador de domínio de origem de replicação**|O nome do controlador de domínio a partir da qual a origem do AD DS na nova réplica ou controlador de domínio de cópia de segurança atualizar instalações. Não se for fornecido nenhum valor, o controlador de domínio mais próximo do domínio a ser replicado será selecionado por predefinição.|  
|**Conta**|A conta a ser utilizada para executar a configuração.|  
|**Palavra-passe de recuperação (modo de segurança)**|A palavra-passe para a conta de administrador offline que é utilizada no modo de reparação do AD DS.|  
|**Instalar o DNS se ainda não estiver presente**|Quando selecionada, o DNS será instalado se não tiver já sido instalado.|  
|**Tornar este controlador de domínio um servidor de catálogo global (GC)**|Especifica se a réplica também será um servidor de GC. Quando selecionada, o computador de destino será configurado como um servidor de GC se o controlador de domínio de origem de replicação é um servidor de GC.|  
|**Aguarde apenas replicação crítica**|Quando selecionado, esta definição especifica que apenas replicação crítica é obtida durante a fase de replicação do Dcpromo. Retoma a replicação reinicio quando o computador é reiniciado como um controlador de domínio.|  
|**Nível funcional da floresta**|Especifica o nível funcional para uma nova floresta. As opções disponíveis são:<br /><br /> -Windows Server 2003<br /><br /> -Windows Server 2008<br /><br /> -Windows Server 2008 R2|  
|**Nível funcional do domínio**|Especifica o nível funcional para o novo domínio. As opções disponíveis são:<br /><br /> -Windows Server 2003<br /><br /> -Windows Server 2008<br /><br /> -Windows Server 2008 R2|  
|**Base de dados**|Totalmente qualificado, o diretório não – UNC Universal Naming Convention num disco rígido do computador local que irá alojar a base de dados do AD DS (NTDS.dit). Se o diretório existe, deve estar vazio. Se não existir, será criado. Espaço livre em disco na unidade lógica selecionada tem de ser 200 megabytes (MB) e, possivelmente, maior quando são encontrados erros de arredondamento e para acomodar todos os objetos no domínio. Para melhor desempenho, o diretório deve estar localizado num disco rígido dedicado.|  
|**Ficheiros de registo**|Totalmente qualificado, o diretório de não UNC num disco rígido no computador local para alojar o AD DS ficheiros de registo. Se o diretório existe, deve estar vazio. Se não existir, será criado.|  
|**SYSVOL**|Totalmente qualificado, o diretório de não UNC num disco rígido do computador local que irão alojar os ficheiros de AD DS System Volume (SYSVOL). Se o diretório existe, deve estar vazio. Se não existir, será criado. O diretório tem de estar localizado numa partição que é formatada com o sistema de ficheiros 5.0 de versão do NTFS. Para melhor desempenho, o diretório deve estar localizado num disco rígido físico diferente que o sistema operativo.|  
|**Nome do site**|O valor de um site existente do AD DS em que pretende localizar o novo controlador de domínio. Se não for especificado, será selecionado um site adequado. Esta opção só se aplica a nova árvore de um cenário de nova floresta. Para todos os outros cenários, um site será selecionado utilizar a configuração do site e sub-rede atual da floresta.|  

#### <a name="configure-dhcp"></a>Configurar o DHCP  
 Este passo de sequência de tarefas configura o serviço de servidor DHCP no computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIConfigureDHCP.wsf](#ZTIConfigureDHCP.wsf).  

 As propriedades exclusivas e definições para o **configurar DHCP** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **configurar o servidor DHCP**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nome**|Configurar o DHCP|  
|Detalhes de âmbito|Estas opções se aplicam a todos os computadores cliente que obtêm uma concessão dentro desse determinado âmbito. Configurar a opção de âmbito valores aplicam-se sempre em todos os computadores a obtenção de uma concessão num determinado âmbito, a menos que estes são substituídas por opções atribuídas a reserva de classe ou cliente.<br /><br /> Dentro do **detalhes de âmbito** definição, as seguintes definições secundárias são configuráveis:<br /><br /> - **Nome de âmbito**. Um nome de utilizador definable<br /><br /> - **Endereço IP inicial**. O endereço IP inicial para o âmbito<br /><br /> - **Endereço IP final**. O endereço IP final para o âmbito<br /><br /> - **Máscara de sub-rede**. A máscara de sub-rede da sub-rede do cliente<br /><br /> - **Duração da concessão para clientes DHCP**. A duração de concessão DHCP é válido para o cliente<br /><br /> - **Descrição**. Uma descrição do âmbito<br /><br /> - **Excluir o intervalo de endereços IP, endereço IP inicial**. O endereço IP inicial para o intervalo de endereços IP que estão a ser excluído do âmbito<br /><br /> -                                 **Excluir o intervalo de endereços IP, endereço IP final**. O endereço IP final para o intervalo de endereços IP que estão a ser excluído do âmbito<br /><br /> - **003 router**. Uma lista de endereços IP para os routers da sub-rede do cliente<br /><br /> - **006 servidores DNS**. Disponíveis para o cliente de servidores de nome de uma lista de endereços IP para o DNS<br /><br /> - **Nome de domínio 015 DNS**. O nome de domínio que o cliente DHCP deve utilizar ao resolver os nomes de domínio não qualificados com DNS<br /><br /> -                                 **044 WINS/NBNS servidores**. Apresenta uma lista de endereços IP para servidores de nome de NetBIOS (NBNSes) na rede<br /><br /> - **Tipo de nó de WINS/NBT 046**. Configura o tipo de nó de cliente para clientes de NetBT<br /><br /> - **Cliente PXE 060**. O endereço utilizado para o código de arranque de configuração de cliente de ambiente de execução pré-arranque (PXE)|  
|Opções de servidor|Estas opções aplicam-se globalmente para todos os âmbitos e classes definidas em cada servidor DHCP e para quaisquer clientes que os serviços de um servidor DHCP. Os valores de opção de servidor configurado aplicam-se sempre a menos que estes são substituídas por opções atribuídas para outra reserva de âmbito, classe ou cliente.<br /><br /> Dentro do **opções de servidor** definição, as seguintes definições secundárias são configuráveis:<br /><br /> - **003 router**. Uma lista de endereços IP para os routers da sub-rede do cliente<br /><br /> - **006 servidores DNS**. Disponíveis para o cliente de servidores de nome de uma lista de endereços IP para o DNS<br /><br /> - **Nome de domínio 015 DNS**. O nome de domínio que o cliente DHCP deve utilizar ao resolver os nomes de domínio não qualificados com DNS<br /><br /> - **044 WINS/NBNS servidores**. Apresenta uma lista de endereços IP para NBNSes na rede<br /><br /> -                                 **Tipo de nó de WINS/NBT 046**. Configura o tipo de nó de cliente para clientes de NetBT<br /><br /> - **Cliente PXE 060**. O endereço utilizado para o código de arranque de configuração de cliente PXE|  

#### <a name="configure-dns"></a>Configurar o DNS  
 Este passo de sequência de tarefas configura DNS no computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIConfigureDNS.wsf](#ZTIConfigureDNS.wsf).  

 As propriedades exclusivas e definições para o **configurar DNS** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **configurar o servidor DNS**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nome**|Configurar o DNS|  
|Zonas|Dentro do **detalhes de âmbito** definição, as seguintes definições secundárias são configuráveis:<br /><br /> -                                 **Nome da zona DNS**. Um nome de utilizador definable<br /><br /> -Type. O tipo de zona DNS a ser criado<br /><br /> - **Replicação**. Especifica o esquema de replicação utilizado para partilhar informações entre os servidores DNS<br /><br /> - **Nome de ficheiro de zona**. Ficheiro de base de dados a zona DNS<br /><br /> -                                 **Atualizações dinâmicas**. Permite que os computadores de cliente DNS registar e atualizar dinamicamente os registos de recursos com um servidor DNS sempre que ocorrerem alterações<br /><br /> -                                 **Scavenge registos de recursos obsoletos**. Remove obsoleta registos de recursos|  
|Propriedades do servidor|Na definição de propriedades do servidor, as seguintes definições secundárias são configuráveis:<br /><br /> -                                 **Desativar recursão**. Especifica que o servidor DNS não irá executar recursão em qualquer consulta<br /><br /> - **ENLACE secundárias**. Especifica se deve utilizar o formato de transferência rápida para transferir uma zona para servidores que executem legado implementações de domínio de nome de Internet de Berkeley (ENLACE)<br /><br /> - **Falha no carregamento se incorreto dados**. Especifica que o servidor DNS deve analisar ficheiros estritamente<br /><br /> -                                 **Ativar o round robin**. Especifica que o servidor DNS deve ser utilizado o mecanismo de round robin para rodar e existe uma lista de registos de recursos se existirem vários registos de recursos do mesmo tipo de reordenação para uma resposta de consulta<br /><br /> - **Ativar a ordenação de máscaras**. Especifica se o servidor DNS deve reordenar os registos de recursos dentro do mesmo registo de recursos definida na respetiva resposta a uma consulta com base no endereço IP de origem da consulta<br /><br /> - **Proteger a cache contra pollution**. Especifica se o servidor DNS irá tentar limpar as respostas para evitar pollution de cache<br /><br /> - **A verificar o nome**. Configura o método de verificação do nome a utilizar|  

> [!NOTE]
>  O **configurar DNS** passo de sequência de tarefas utiliza a ferramenta Dnscmd, que está incluída nas ferramentas de suporte do Windows, para configurar o DNS. Certifique-se de que as ferramentas de suporte do Windows está instalada antes de executar o **configurar DNS** passo de sequência de tarefas.  

> [!NOTE]
>  Para obter mais informações sobre estas propriedades de servidor, consulte [Dnscmd](http://technet.microsoft.com/library/cc772069.aspx).  

#### <a name="enable-bitlocker"></a>Ativar BitLocker  
 Este passo de sequência de tarefas configura a encriptação de unidade BitLocker® no computador de destino. Para obter mais informações sobre este tipo de passo, consulte [ativar BitLocker](http://technet.microsoft.com/library/bb632526.aspx).  

 As propriedades exclusivas e definições para o **ativar BitLocker** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **ativar BitLocker**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Unidade de sistema operativo atual**|Quando selecionada, a unidade de sistema operativo será configurada. Esta é a seleção predefinida.|  
|**Unidade específica**|Quando selecionada, a unidade especificada será configurada.|  
|**Apenas TPM**|Quando selecionada, o Trusted Platform Module (TPM) é necessário. Esta é a seleção predefinida.|  
|**Chave de arranque em USB apenas**|Quando selecionada, é necessária uma chave de arranque a unidade USB especificada.|  
|**Chave de TPM e arranque em USB**|Quando selecionada, o TPM é necessário para além de uma chave de arranque na unidade USB especificada.|  
|**No Active Directory**|Quando selecionada, a chave de recuperação é armazenada no AD DS. Esta é a seleção predefinida.|  
|**Não crie uma chave de recuperação**|Quando selecionada, a chave de recuperação não é criada. Não é recomendado utilizar esta opção.|  
|**Aguarde que o BitLocker concluir**|Quando selecionado, este passo não será concluída até depois de BitLocker terminou de processar todas as unidades.|  

####  <a name="ExecuteRunbook"></a>Executar o Runbook  
 Este passo de sequência de tarefas executa o Microsoft System Center 2012 Orchestrator runbooks no computador de destino. Um Orchestrator *runbook* é a sequência de atividades que orquestram ações em computadores e redes. Pode iniciar os runbooks do Orchestrator no MDT com este tipo de passo de sequência de tarefas.  

> [!NOTE]
>  Este passo de sequência de tarefas não está incluído qualquer modelos de sequência de tarefas do MDT. Tem de adicionar este passo de sequência de tarefas para sequências de tarefas que cria.  

 As propriedades exclusivas e definições para o **executar o Runbook** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **executar o Runbook**.|  
|**Nome**|O nome do passo de sequência de tarefas, o que deve refletir o nome do runbook a ser executado.|  
|**Descrição**|Informativo texto que fornece informações adicionais sobre o passo de sequência de tarefas|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|   
|**Servidor do Orchestrator**|Escreva o URL para o Orchestrator web service, que inclui o nome do servidor. Serviço web do Orchestrator pode utilizar o protocolo HTTP (Hypertext Transfer) ou HTTP através de Secure Sockets Layer (HTTPS). Predefinições para a porta 81 do serviço web do Orchestrator.<br /><br /> Serviço web do Orchestrator suporta múltiplos servidores runbook. Por predefinição, um runbook pode ser executado em qualquer servidor runbook. Um runbook pode ser configurado para especificar quais os servidores runbook devem ser utilizados para executar o runbook.<br /><br /> Nota:<br /><br /> Serviço web do Orchestrator suporta a capacidade para executar um runbook num servidor runbook específico. Esta funcionalidade não é suportada no MDT.<br /><br /> Especifique o URL em qualquer um dos seguintes formatos:<br /><br /> - ***ServerName***. Quando utilizar este formato, o URL será assumida a:<br /><br /> `http://<servername>:81/Orchestrator2012/Orchestrator.svc`<br /><br /> - ***servername:Port***. Quando utilizar este formato, o URL será assumida a:<br /><br /> `http://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br /><br /> -**http://*servername:port***. Quando utilizar este formato, o URL será assumida a:<br /><br /> `http://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br /><br /> -**http://*servername:port***. Quando utilizar este formato, o URL será assumida a:<br /><br /> `https://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br /><br /> - **http://*servername:port*/Orchestrator2012/Orchestrator.svc**. Quando utilizar este formato, o MDT parte do princípio de que está a fornecer o URL completamente qualificado, porque o valor termina com. svc.<br /><br /> -                                 **https://*servername:port*/Orchestrator2012/Orchestrator.svc**. Quando utilizar este formato, o MDT parte do princípio de que está a fornecer o URL completamente qualificado, porque o valor termina com. svc.|  
|**Runbook**|Clique em **procurar**e, em seguida, selecione o nome do runbook do Orchestrator que esta sequência de tarefas deve ser executada.<br /><br /> Nota:<br /><br /> Para procurar com êxito para os runbooks do Orchestrator, instale o [actualização do ADO.NET Data Services para .NET Framework 3.5 SP1 para Windows 7 e Windows Server 2008 R2](http://www.microsoft.com/download/details.aspx?displaylang=en&id=2343).|  
|**Fornecer automaticamente os parâmetros do runbook**|Selecione esta opção para fornecer automaticamente valores de parâmetro de entrada do runbook do Orchestrator (a que parte do princípio de que os valores de parâmetro de runbook são variáveis de sequência de tarefas). Por exemplo, se um runbook tem um parâmetro de entrada com o nome **OSDComputerName**, em seguida, a **OSDComputerName** valor de variável de sequência de tarefas é transferida para o runbook.<br /><br /> Nota:<br /><br /> Esta opção funciona apenas para os parâmetros de entrada que são nomes de variáveis de sequência de tarefas válido e não conter espaços ou outros carateres especiais. Apesar dos espaços e outros carateres especiais são suportados como nomes de parâmetro do Orchestrator, não têm nomes de variáveis de sequência de tarefas válido. Se tiver de passar valores para os parâmetros com espaços ou outros carateres especiais, utilize o **especificar os parâmetros do runbook explícita** opção.<br /><br /> A outra opção consiste **especificar os parâmetros do runbook explícita**.<br /><br /> Nota:<br /><br /> Os valores fornecidos para os parâmetros de entrada do runbook para o serviço web do Orchestrator são formatados como XML. Passar valores que contêm dados que se assemelha dados formatado em XML ou poderá causar erros.|  
|**Especifique os parâmetros do runbook explícita**|Selecione esta opção para fornecer explicitamente o Orchestrator parâmetros de entrada do runbook.<br /><br /> Tem de configurar as seguintes definições para cada parâmetro de entrada que o runbook do Orchestrator requer:<br /><br /> -                                 **Nome**. Este é o nome do parâmetro de entrada do runbook.<br /><br /> Nota:<br /><br /> Se alterar os parâmetros de um runbook do Orchestrator existente, terá de procurar novamente, (reselect) para o runbook porque MDT apenas obtém a lista de parâmetros ao adicionar inicialmente o runbook do Orchestrator.<br /><br /> - **Valor**. Isto pode ser uma constante ou uma variável, tal como uma variável de sequência de tarefas ou uma variável de ambiente. Por exemplo, pode especificar um valor de **% OSDComputerName %**, que irá passar o valor da **OSDComputerName** variável de sequência de tarefas para o parâmetro de entrada do runbook.|  
|**Aguarde que o runbook para concluir antes de continuar**|Esta caixa de verificação controla se o passo de sequência de tarefas irá aguardar que o runbook para concluir antes de avançar para o seguinte passo de sequência de tarefas.<br /><br /> Se esta caixa de verificação:<br /><br /> - **Selecionado**, em seguida, o passo de sequência de tarefas irá aguardar que o runbook para concluir antes de prosseguir para o próximo passo de sequência de tarefas.<br /><br /> Quando esta caixa de verificação está selecionada, o passo de sequência de tarefas irá consultar o serviço web do Orchestrator para o runbook para concluir. A quantidade de tempo entre inquéritos comece em 1 segundo, em seguida, aumenta a 2, 4, 8, 16, 32 e 64 segundos entre cada consulta. Quando a quantidade de tempo atingirem 64 segundos, o passo de sequência de tarefas continua a consultar cada segundos 64.<br /><br /> - **Limpo**, em seguida, o passo de sequência de tarefas não espera que o runbook para concluir antes de avançar para o seguinte passo de sequência de tarefas.<br /><br /> Nota:<br /><br /> Tem de selecionar esta caixa de verificação se o runbook devolve os parâmetros de saída.|  

#### <a name="format-and-partition-disk"></a>Formatar e Particionar Disco  
 Esta tarefa sequência passo particiona e formata discos no computador de destino. Para obter mais informações sobre este tipo de passo, consulte [formatar e particionar disco](http://technet.microsoft.com/library/bb680345.aspx).  

 As propriedades exclusivas e definições para o **formatar e particionar disco** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este tipo de só de leitura **formatar e particionar disco**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Número do disco**|O número físico do disco seja configurado.|  
|**Tipo de disco**|O tipo de unidade a ser criado. Os valores são:<br /><br /> -                                 **Padrão (MBR)** (registo de arranque principal)<br /><br /> - **GPT** (tabela de partições GUID [Identificador exclusivo global]).<br /><br /> A seleção predefinida é **padrão (MBR)**.|  
|**Volume**|Dentro do **Volume** definição, as seguintes definições secundárias são configuráveis:<br /><br /> -Partição **nome**. Um nome de utilizador definable.<br /><br /> - **Tipo de partição.** Os valores variam consoante o tipo de disco:<br /><br /> -MBR: **Primário** apenas<br /><br /> -GPT: **Primário**, **EFI**, ou **MSR**<br /><br /> - **Utilize uma percentagem de espaço restante.**<br /><br /> -                                 **Utilize tamanho de unidade específica.** Os valores são em incrementos de 1 MB ou de 1 gigabyte (GB).<br /><br /> -                                 **Tornar esta partição de arranque.**<br /><br /> -                                 **Sistema de ficheiros.** Os valores são **NTFS** ou **FAT32**.<br /><br /> - **Formatação rápida.** Quando selecionada, é efetuada uma formatação rápida.<br /><br /> - **Variável.** Letra de unidade que foi atribuída a esta partição recentemente configurada.|  

> [!NOTE]
>  Ao utilizar o ficheiro CustomSettings.ini para especificar o disco rígido e configurações de partição, apenas o primeiro disco rígido e o primeiro duas partições serão configuradas. Edite ZTIGather.xml para configurar os discos rígidos adicionais ou partições.  

#### <a name="gather"></a>Recolher  
 Este passo de sequência de tarefas recolhe dados e as regras de processamento para o computador de destino. As propriedades exclusivas e definições para o **recolher** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **recolher**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Recolher apenas dados locais**|Quando selecionado, este passo processa apenas as propriedades incluídas no ficheiro ZTIGather.xml.|  
|**Recolha de dados locais e processar as regras**|Quando selecionado, este passo processa as propriedades incluídas no ficheiro ZTIGather.xml e as propriedades incluídas no ficheiro que especifica o ficheiro de regras. Esta é a seleção predefinida.|  
|**Ficheiro de regras**|O nome do ficheiro de regras para processar. Se deixado em branco, o passo de sequência de tarefas tenta localizar e processar o ficheiro CustomSettings.ini.|  

> [!NOTE]
>  Este passo de sequência de tarefas está disponível nativamente no System Center 2012 R2 Configuration Manager como **definir variáveis dinâmicas**no grupo de geral.  

####  <a name="InjectDrivers"></a>Inserir controladores  
 Este passo de sequência de tarefas injects controladores que tenham sido configurados para implementação no computador de destino. As propriedades exclusivas e definições para o **inserir controladores** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **inserir controladores**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|   
|**Instalar apenas controladores correspondentes**|Injects apenas os controladores que requer que o computador de destino e que corresponda ao que está disponível na saída\-de\-controladores|  
|**Instalar todos os controladores**|Instala todos os controladores|  
|**Perfil de seleção**|Instala todos os controladores no perfil selecionado|  

#### <a name="install-application"></a>Instalar Aplicação  
 Este passo de sequência de tarefas instala as aplicações no computador de destino. Para obter mais informações sobre este tipo de passo, consulte [instalar Software](http://technet.microsoft.com/library/bb680842.aspx).  

 As propriedades exclusivas e definições para o **instalar aplicação** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|   
|**Tipo**|Definir este leitura\-apenas escreva para **instalar aplicação**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Instalar várias aplicações**|Instalar aplicações obrigatórias que o **MandatoryApplications** tem especificada a propriedade e aplicações opcionais que o **aplicações** tem especificada a propriedade. Estas propriedades estão configuradas por regras ou foram especificadas durante o processo de interview do Assistente de implementação. Esta é a seleção predefinida.|  
|**Instalar uma única aplicação**|A aplicação específica a instalar. Selecione a aplicação a partir de uma redução\-para baixo a lista que consiste em aplicações que tenham sido configuradas no nó de aplicações do Deployment Workbench.|  
|**Códigos de êxito**|Um espaço\-lista delimitada de códigos de saída de instalação de aplicações que deve ser utilizada ao determinar o êxito da instalação de aplicações.|  

#### <a name="install-operating-system"></a>Instalar o sistema operativo  
 Este passo de sequência de tarefas instala um sistema operativo no computador de destino. MDT pode implementar o Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2 utilizando:  

-   **Setup.exe**. Este método é o método tradicional utilizado, iniciada ao executar o setup.exe do suporte de dados de instalação. MDT utiliza setup.exe por predefinição.  

-   **ImageX.exe**. Este método instala a imagem do sistema operativo utilizando imagex.exe com o  **\/aplicar** opção. MDT utiliza este método quando não é possível utilizar o método setup.exe \(ou seja, este utilizará imagex.exe\).  

 Pode controlar que um destes métodos é utilizado pelo utilizando o **ForceApplyFallback** propriedade, o que também afeta as sequências de tarefas do sistema operativo estão listadas no Assistente de implementação para uma imagem de arranque de arquitetura de processador específico. Para obter mais informações, consulte o [ForceApplyFallback](#ForceApplyFallback) propriedade.  

 As propriedades exclusivas e definições para o **instalar sistema operativo** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|   
|**Tipo**|Definir este leitura\-apenas escreva para **instalar sistema operativo**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|   
|**Sistema operativo a instalar**|O nome do sistema operativo ser instalado no computador de destino. Selecione o sistema operativo a partir de uma redução\-compilada de sistemas operativos que tenham sido configurados no nó sistemas operativos do Deployment Workbench de lista pendente.|  
|**Disco**|O disco em que pretende instalar o sistema operativo.|  
|**Partição**|A partição em que pretende instalar o sistema operativo.|  

####  <a name="InstallRolesandFeatures"></a>Instalar funções e funcionalidades  
 Este passo de sequência de tarefas instala as funcionalidades e funções selecionadas no computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades utilizadas, consulte [ZTIOSRole.wsf](#ZTIOSRole.wsf).  

 As propriedades exclusivas e definições para o **instalar funções e funcionalidades** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **instalar funções e funcionalidades**.|  
|**Descrição**|Informativo texto que descreve a finalidade do passo de sequência de tarefas.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|    
|**Selecione o sistema operativo para o qual as funções são para ser instalada**|Selecione o sistema operativo ser implementado no computador de destino.|  
|**Selecione as funções e funcionalidades que devem ser instaladas**|Selecione um ou mais funções e funcionalidades para instalação no computador de destino.|  

#### <a name="install-language-packs-offline"></a>Instalar pacotes de idiomas Offline  
 Este passo de sequência de tarefas instala as atualizações à imagem de no computador de destino depois do sistema operativo tiver sido implementado, mas antes do destino o computador foi reiniciado. Estas atualizações incluem pacotes de idiomas. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIPatches.wsf](#ZTIPatches.wsf).  

 As propriedades exclusivas e definições para o **instalar os pacotes de idiomas Offline** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **instalar atualizações Offline**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nome do pacote**|O nome do pacote de pacote de idiomas que deve ser aplicado ao computador de destino|  

> [!NOTE]
>  Este passo de sequência de tarefas é válido apenas quando utilizar o MDT com o Configuration Manager.  

#### <a name="install-language-packs-online"></a>Instalar pacotes de idiomas Online  
 Este passo de sequência de tarefas instala os pacotes de idiomas para a imagem no computador de destino depois do sistema operativo tiver sido implementado e depois do computador de destino tiver sido reiniciado. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTILangPacksOnline.wsf](#ZTILangPacksOnline.wsf).  

 As propriedades exclusivas e definições para o **instale Language Packs Online** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **instale Language Packs Online**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nome do pacote**|O nome do pacote de pacote de idiomas que deve ser aplicado ao computador de destino|  

> [!NOTE]
>  Este passo de sequência de tarefas é válido apenas quando utilizar o MDT com o Configuration Manager.  

#### <a name="install-updates-offline"></a>Instalar atualizações Offline  
 Este passo de sequência de tarefas instala as atualizações à imagem de no computador de destino depois do sistema operativo tiver sido implementado, mas antes do destino o computador foi reiniciado. Estas atualizações incluem pacotes de idiomas. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIPatches.wsf](#ZTIPatches.wsf).  

 As propriedades exclusivas e definições para o **instalar atualizações Offline** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **instalar atualizações Offline**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Perfil de seleção**|O nome do perfil de seleção que deve ser aplicado ao computador de destino<br /><br /> Nota:<br /><br /> Ao utilizar o MDT com o Configuration Manager, especifique o nome do pacote de atualização que deve ser aplicado.|  

#### <a name="recover-from-domain-join-failure"></a>Recuperar de uma falha de associação de domínio  
 Este passo de sequência de tarefas verifica se o computador de destino foi associada ao domínio. As propriedades exclusivas e definições para o **recuperar de uma falha de associação do domínio** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para recuperar de **falha de associação de domínio**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Auto recuperar**|O passo de sequência de tarefas tenta associar o computador de destino a um domínio.|  
|**Recuperar manual**|Se o computador de destino não conseguir aderir a um domínio, o passo de sequência de tarefas faz com que o sequenciador de tarefas colocar em pausa, permitindo-lhe a tentar associar o computador de destino a um domínio.|  
|**Não recuperar**|Se o computador de destino não conseguir aderir a um domínio, a sequência de tarefas falha, a sequência de tarefas a parar.|  

#### <a name="restart-computer"></a>Reiniciar computador  
 Este passo de sequência de tarefas reinicia o computador de destino. As propriedades exclusivas e definições para o **reiniciar o computador** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **reiniciar o computador**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Nenhum**|Nenhum|  

#### <a name="run-command-line"></a>Executar Linha de Comandos  
 Este passo de sequência de tarefas executa os comandos especificados no computador de destino. Para obter mais informações sobre este tipo de passo, consulte [executar linha de comandos](http://technet.microsoft.com/library/bb632992.aspx).  

 As propriedades exclusivas e definições para o **executar linha de comandos** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **executar linha de comandos**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Linha de comandos**|Os comandos para ser executada quando este passo de sequência de tarefas é processado|  
|**Iniciar**|A pasta de partida para a aplicação \(o caminho tem de ser um caminho válido no computador de destino.\)|  
|**Executar este passo de como a seguinte conta**|Permite a especificação de credenciais de utilizador que será utilizada para executar o comando especificado|  
|**Conta**|As credenciais de utilizador que serão utilizadas para executar o comando especificado|  
|**Carregar o perfil do utilizador**|Quando selecionada, carrega o perfil de utilizador para a conta especificada|  

#### <a name="run-powershell-script"></a>Executar Script do PowerShell  
 Este passo de sequência de tarefas executa o script Windows PowerShell™ especificado no computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIPowerShell.wsf](#ZTIPowerShell.wsf).  

 As propriedades exclusivas e definições para o **executar Script do PowerShell** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **executar Script do PowerShell**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Script do PowerShell**|O script do Windows PowerShell para ser executada quando este passo de sequência de tarefas é processado|  
|Parâmetros|Os parâmetros a transmitir ao script do Windows PowerShell. Estes parâmetros devem ser especificado o mesmo como se estivesse a adicioná-los ao script do Windows PowerShell numa linha de comandos.<br /><br /> Os parâmetros fornecidos devem ser apenas esses parâmetros que consome o script, não para a linha de comandos do Windows PowerShell.<br /><br /> O seguinte exemplo seria um valor válido para esta definição:<br /><br /> `-MyParameter1 MyValue1 -MyParameter2 MyValue2`<br /><br /> O seguinte exemplo seria um valor inválido para esta definição \(itens a negrito são incorretos\):<br /><br /> `-nologo -executionpolicy unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`<br /><br /> O exemplo anterior é inválido, porque o valor inclui o comando do Windows PowerShell\-parâmetros de linha \(  **\-nologo** e **– executionpolicy sem restrições**\).|  

> [!NOTE]
>  Este passo de sequência de tarefas está disponível nativamente no System Center 2012 R2 Configuration Manager como **executar Script do PowerShell** no grupo de geral.  

#### <a name="set-task-sequence-variable"></a>Definir Variável da Sequência de Tarefas  
 Este passo de sequência de tarefas define a variável de sequência de tarefas especificada para o valor especificado. Para obter mais informações sobre este tipo de passo, consulte [Set Task Sequence Variable](http://technet.microsoft.com/library/bb694306.aspx).  

 As propriedades exclusivas e definições para o **Set Task Sequence Variable** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **Set Task Sequence Variable**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Variável de sequência de tarefas**|O nome da variável para modificar|  
|**Valor**|O valor para atribuir à variável especificada|  

####  <a name="UninstallRolesandFeatures"></a>Desinstalar funcionalidades e funções  
 Este passo de sequência de tarefas desinstala as funcionalidades e funções selecionadas de computador de destino. Para obter mais informações sobre o script elimina esta tarefa e as propriedades utilizadas, consulte [ZTIOSRole.wsf](#ZTIOSRole.wsf).  

 As propriedades exclusivas e definições para o **desinstalar funções e funcionalidades** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **desinstalar funções e funcionalidades**.|  
|**Descrição**|Informativo texto que descreve a finalidade do passo de sequência de tarefas.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Selecione o sistema operativo para o qual as funções são para ser instalada**|Selecione o sistema operativo ser implementado no computador de destino.|  
|**Selecione as funções e funcionalidades que devem ser instaladas**|Selecione um ou mais funções e funcionalidades para unstallation o computador de destino.|  

#### <a name="validate"></a>Validar  
 Este passo de sequência de tarefas verifica se o computador de destino cumpre as condições de pré-requisitos de implementação especificado. As propriedades exclusivas e definições para o **validar** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Definir este leitura\-apenas escreva para **validar**.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Certifique-se a memória mínima**|Quando selecionado, este passo verifica que a quantidade de memória, em megabytes, instalada nos computador de destino cumpre os ou excede o valor especificado. Esta é uma seleção predefinida.|  
|**Certifique-se a velocidade mínima do processador**|Quando selecionado, este passo verifica se a velocidade do processador, em megahertz \(MHz\), instalado os computador de destino cumpre os ou excede o valor especificado. Esta é uma seleção predefinida.|  
|**Certifique-se de que irá ajustar o tamanho de imagem especificado**|Quando selecionado, este passo verifica se a quantidade de espaço livre em disco, em megabytes, no computador de destino cumpre ou excede o valor especificado.|  
|**Certifique-se o sistema operativo atual atualizar**|Quando selecionado, este passo verifica se o sistema operativo instalado no computador de destino cumpre os requisitos especificados. Esta é uma seleção predefinida.|  

> [!NOTE]
>  Este passo de sequência de tarefas está disponível nativamente no System Center 2012 R2 Configuration Manager como **verificar disponibilidade** no grupo de geral.  

### <a name="out-of-box-task-sequence-steps"></a>Saída\-de\-caixa passos de sequência de tarefas  
 Os seguintes passos de sequência de tarefas são referenciados por uma ou mais dos modelos de sequência de tarefas disponíveis incluídos com o MDT. Cada os exemplos a seguir apresenta as propriedades pré-configuradas, parâmetros e as opções e pode ser utilizada como base para a criação de sequências de tarefas personalizadas.  

 Apenas as propriedades de passo de sequência tarefas, parâmetros e as opções e os valores correspondentes são listados nos exemplos.  

> [!NOTE]
>  Para obter mais informações sobre cada passo de sequência de tarefas, consulte os tópicos correspondentes [propriedades comuns e as opções para tipos de passo de sequência de tarefas](#CommonPropertiesandOptionsforTaskSequenceStepTypes) e [propriedades específicas e definições de tipos de passo de sequência de tarefas](#SpecificPropertiesandSettingsforTaskSequenceStepTypes).  

#### <a name="apply-network-settings"></a>Aplicar Definições de Rede  
 Este passo de sequência de tarefas configura o adaptador de rede no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTINICConfig.wsf](#ZTINICConfig.wsf).  

 A configuração predefinida do **aplicar definições de rede** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Aplicar Definições de Rede|  
|**Nome**|Aplicar Definições de Rede|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
||Não existem parâmetros estão pré-configuradas para este passo. Isto faz com que este passo, por predefinição, para configurar o adaptador de rede para utilizar DHCP.|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

> [!NOTE]
>  Ao utilizar o ficheiro CustomSettings.ini para especificar as configurações de adaptador de rede, apenas o primeiro adaptador de rede será configurado. Edite ZTIGather.xml para configurar adaptadores de rede adicionais.  

#### <a name="apply-patches"></a>Aplicar Patches  
 Este passo de sequência de tarefas instala as atualizações à imagem de no computador de destino depois do sistema operativo tiver sido implementado, mas antes do destino o computador foi reiniciado. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIPatches.wsf](#ZTIPatches.wsf).  

 A configuração predefinida do **instalar atualizações Offline** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Instalar atualizações Offline|  
|**Nome**|Aplicar Patches|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Perfil de seleção**|O nome do perfil utilizado ao selecionar os patches para instalar no computador de destino|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="apply-windows-pe"></a>Aplicar o Windows PE  
 Este passo de sequência de tarefas prepara o computador de destino para iniciar no ambiente de pré-instalação do Windows \(do Windows PE\). Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [LTIApply.wsf](#LTIApply.wsf).  

 A configuração predefinida do **aplicam-se o Windows PE** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Aplicar o Windows PE|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\LTIApply.wsf" /PE`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="backup"></a>Cópia de segurança  
 Este passo de sequência de tarefas cria cópias de segurança do computador de destino antes de iniciar a implementação do sistema operativo. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIBackup.wsf](#ZTIBackup.wsf).  

 A configuração predefinida do **cópia de segurança** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Cópia de segurança|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIBackup.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="capture-groups"></a>Captura de grupos  
 Este passo de sequência de tarefas captura as associações de grupos locais que existe no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIGroups.wsf](#ZTIGroups.wsf).  

 A configuração predefinida do **capturar grupos** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Captura de grupos|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIGroups.wsf" /capture`|  
|**Iniciar**|Não foi especificado.|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="capture-user-state"></a>Capturar Estado do Utilizador  
 Este passo de sequência de tarefas captura o estado do utilizador para perfis de utilizador existe no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIUserState.wsf](#ZTIUserState.wsf). Para obter mais informações sobre este tipo de passo, consulte [capturar estado do utilizador](http://technet.microsoft.com/library/bb680924.aspx).  

 A configuração predefinida do **capturar estado do utilizador** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Capturar Estado do Utilizador|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIUserState.wsf" /capture`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="check-bios"></a>Verifique o BIOS  
 Este passo de sequência de tarefas verifica a entrada básica\/sistema de saída \(BIOS\) do computador de destino para garantir que é compatível com o sistema operativo que está a implementar. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIBIOSCheck.wsf](#ZTIBIOSCheck.wsf).  

 A configuração predefinida do **verifique BIOS** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Verifique o BIOS|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIBIOSCheck.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="configure"></a>Configurar  
 Este passo de sequência de tarefas configura o ficheiro Unattend.xml com os valores de propriedade necessária que são aplicáveis ao sistema operativo que está a implementar no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [ZTIConfigure.wsf](#ZTIConfigure.wsf).  

 A configuração predefinida do **configurar** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Configurar|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIConfigure.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="copy-scripts"></a>Scripts de cópia  
 Esta copia de passo de sequência de tarefas os scripts de implementação utilizado durante os processos de implementação para um disco rígido local no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [LTICopyScripts.wsf](#LTICopyScripts.wsf).  

 A configuração predefinida do **cópia Scripts** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Scripts de cópia|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\LTICopyScripts.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="copy-sysprep-files"></a>Copie os ficheiros Sysprep  
 Este passo de sequência de tarefas copia os ficheiros Sysprep para o computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que utilizar, consulte [LTISysprep.wsf](#LTISysprep.wsf).  

 A configuração predefinida do **copiar ficheiros de Sysprep** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Copie os ficheiros Sysprep|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\LTISysprep.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="create-bitlocker-partition"></a>Criar a partição do BitLocker  
 Este passo de sequência de tarefas define a **BDEInstall** propriedade para verdadeiro, que indica que o BitLocker deve ser instalado no computador de destino. As propriedades exclusivas e definições para o **criar partições do BitLocker** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|   
|**Tipo**|Definir Variável da Sequência de Tarefas|  
|**Nome**|Criar a partição do BitLocker|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Variável de sequência de tarefas**|Instalação BDE|  
|**Valor**|Verdadeiro|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="create-wim"></a>Criar WIM  
 Este passo de sequência de tarefas cria uma cópia de segurança do computador de destino. As propriedades exclusivas e definições para o **criar WIM** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Criar WIM|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIBackup.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="disable-bde-protectors"></a>Desativar os Protetores de BDE  
 Se o BitLocker estiver instalado no computador de destino, este passo de sequência de tarefas desativa os protetores de BitLocker.  

 As propriedades exclusivas e definições para o **desativar Protetores de BDE** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Desativar os Protetores de BDE|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIDisableBDEProtectors.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="enable-bitlocker"></a>Ativar BitLocker  
 Este passo de sequência de tarefas ativa o BitLocker no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIBde.wsf](#ZTIBde.wsf).  

 A configuração predefinida do **ativar BitLocker** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Ativar BitLocker|  
|**Nome**|Ativar BitLocker|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Unidade de sistema operativo atual**|Selecionado|  
|**Apenas TPM**|Selecionado|  
|**Chave de arranque em USB apenas**|Não selecionada|  
|**Chave de TPM e arranque em USB**|Não selecionada|  
|**Unidade específica**|Não selecionada|  
|**No Active Directory**|Selecionado|  
|**Não crie uma chave de recuperação**|Não selecionada|  
|**Aguarde que o BitLocker concluir**|Não selecionada|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|**BdeInstallSuppress** não é igual a Sim|  

#### <a name="enable-oem-disk-configuration"></a>Ativar a configuração de disco OEM  
 Este passo de sequência de tarefas define a **DeploymentType**propriedade **NEWCOMPUTER**, que permite que o disco do computador de destino ser particionado e formatado.  

 As propriedades exclusivas e definições para o **ativar a configuração do disco OEM** são do tipo de passo de sequência de tarefas:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Definir Variável da Sequência de Tarefas |  
|**Nome**|Ativar a configuração de disco OEM|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Variável de sequência de tarefas**|deploymentType|  
|**Valor**|NEWCOMPUTER|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="end-phase"></a>Fase de fim  
 Este passo de sequência de tarefas é terminada a fase de implementação atual e reinicia o computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **fase final** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Reiniciar computador|  
|**Nome**|Fase de fim|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|Nenhum|Nenhum|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="execute-sysprep"></a>Executar o Sysprep  
 Este passo de sequência de tarefas é iniciado o Sysprep no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [LTISysprep.wsf](#LTISysprep.wsf).  

 A configuração predefinida do **executar Sysprep** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Executar o Sysprep|  
|**Descrição**|Nenhum|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\LTISysprep.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="force-diskpart-action"></a>Forçar Diskpart ação  
 Se unidade c:\\existe oem.wsf ficheiro, este passo de sequência de tarefas Elimina a unidade c:\\oem.wsf ficheiro, que lhe permitirá a **formatar e particionar disco** passo de sequência de tarefas para executar. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **Force Diskpart ação** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Forçar Diskpart ação|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cmd.exe /c if exist c:\oem.wsf del /q c:\oem.wsf`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0.1|  
|**Continuar com o erro**|Selecionado|  
|**Qualificador condicional**|Nenhum|  

#### <a name="format-and-partition-disk"></a>Formatar e Particionar Disco  
 Este passo de sequência de tarefas configura e formatos de disco partições no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIDiskpart.wsf](#ZTIDiskpart.wsf).  

 A configuração predefinida do **formatar e particionar disco** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Formatar e Particionar Disco|  
|**Nome**|Formatar e Particionar Disco|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Número do disco**|0|  
|**Tipo de disco**|Standard \(MBR\)|  
|**Volume**|Na definição de Volume, as seguintes sub\-definições são configuradas:<br /><br /> \-                                 **Nome de partição**. OSDisk<br /><br /> \-**Tipo de partição**. Primário<br /><br /> \-                                 **Utilize uma percentagem de espaço restante**. Selecionado<br /><br /> \-                                 **Tamanho\(%\)**. 100<br /><br /> \-**Utilizar tamanho de unidade específica**. Não selecionada<br /><br /> \-                                 **Tornar esta partição de arranque**. Selecionado<br /><br /> \-**Sistema de ficheiros**. NTFS<br /><br /> \-**Formatação rápida**. Selecionado<br /><br /> \-**Variável**. Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

> [!NOTE]
>  Ao utilizar o ficheiro CustomSettings.ini para especificar o disco rígido e configurações de partição, apenas o primeiro disco rígido e o primeiro duas partições serão configuradas. Edite ZTIGather.xml para configurar os discos rígidos adicionais ou partições.  

#### <a name="gather-local-only"></a>Recolher apenas local  
 Este passo de sequência de tarefas reúne as definições de configurações de implementação de origens de locais que se aplicam ao computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIGather.wsf](#ZTIGather.wsf).  

 A configuração predefinida do **recolha local apenas** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Recolher|  
|**Nome**|Recolher apenas local|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Recolher apenas dados locais**|Selecionado|  
|**Recolha de dados locais e processar as regras**|Não selecionada|  
|**Ficheiro de regras**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Nenhum|  

#### <a name="generate-application-migration-file"></a>Gerar o ficheiro de migração de aplicações  
 Este passo de sequência de tarefas gera o ficheiro de ZTIAppXmlGen.xml, que contém uma lista de associações de ficheiros que estão instalados no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIAppXmlGen.wsf](#ZTIAppXmlGen.wsf).  

 A configuração predefinida do **migração de aplicação gerar** passo de sequência de tarefas de ficheiro é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Gerar o ficheiro de migração de aplicações|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIAppXmlGen.wsf" /capture`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Nenhum|  

#### <a name="inject-drivers"></a>Inserir controladores  
 Este passo de sequência de tarefas injects controladores que tenham sido configurados para implementação no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIDrivers.wsf](#ZTIDrivers.wsf).  

 A configuração predefinida do **inserir controladores** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Inserir controladores|  
|**Nome**|Inserir controladores|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Instalar apenas controladores correspondentes**|Injects apenas os controladores que são necessários pelo computador de destino e corresponde com que está disponível na saída\-de\-controladores|  
|**Instalar todos os controladores**|Injects todos os controladores|  
|**Perfil de seleção**|Injects controladores que estão associados ao perfil selecionado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="install-applications"></a>Instalar aplicações  
 Este passo de sequência de tarefas instala as aplicações no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIApplications.wsf](#ZTIApplications.wsf).  

 A configuração predefinida do **instalar aplicações** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Instalar aplicações|  
|**Nome**|Instalar aplicações|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Instalar várias aplicações**|Selecionado|  
|**Instalar uma única aplicação**|Não selecionada|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="install-operating-system"></a>Instalar o sistema operativo  
 Este passo de sequência de tarefas instala um sistema operativo no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **instalar sistema operativo** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Instalar o sistema operativo|  
|**Nome**|Instalar o sistema operativo|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Sistema operativo a instalar**|Este valor corresponde ao sistema operativo que foi selecionado quando foi criada a sequência de tarefas.|  
|**Disco**|O disco em que o sistema operativo é instalado.|  
|**Partição**|A partição onde vai ser instalado o sistema operativo.|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="next-phase"></a>Fase seguinte  
 Este passo de sequência de tarefas atualiza o **fase** propriedade para a fase seguinte no processo de implementação. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTINextPhase.wsf](#ZTINextPhase.wsf).  

 A configuração predefinida do **fase seguinte** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Fase seguinte|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTINextPhase.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="post-apply-cleanup"></a>Post\-aplicar a limpeza  
 Este passo de sequência de tarefas limpa ficheiros desnecessários após a instalação de uma imagem no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [LTIApply.wsf](#LTIApply.wsf).  

 A configuração predefinida do **Post\-aplicar limpeza** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Post\-aplicar a limpeza|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\LTIApply.wsf" /post`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="recover-from-domain"></a>Recuperar a partir de domínio  
 Este passo de sequência de tarefas irá verificar que o computador de destino foi associado um domínio. Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIDomainJoin.wsf](#ZTIDomainJoin.wsf).  

 As propriedades exclusivas e definições para a recuperar a partir do tipo de passo de sequência de tarefas de domínio são:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Descrição**|  
|-|-|  
|**Tipo**|Leia\-apenas o tipo está definido como recuperar de uma falha de associação do domínio.|  

##### <a name="settings"></a>Definições  
|**Nome**|**Descrição**|  
|-|-|  
|**Auto recuperar**|O passo de sequência de tarefas irá tentar associar o computador de destino a um domínio.|  
|**Recuperar manual**|Se o computador de destino não conseguir aderir a um domínio, o passo de sequência de tarefas irá fazer com que o sequenciador de tarefas colocar em pausa, permitindo que o utilizador tenta associar o computador de destino a um domínio.|  
|**Não recuperar**|Se o computador de destino não conseguir aderir a um domínio, a sequência de tarefas falha, a sequência de tarefas a parar.|  

#### <a name="restart-computer"></a>Reiniciar computador  
 Este passo de sequência de tarefas reinicia o computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **reiniciar o computador** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Reiniciar computador|  
|**Nome**|Reiniciar computador|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|Nenhum|Nenhum|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="restore-groups"></a>Restaurar a grupos  
 Este passo de sequência de tarefas restaura a associação a grupos capturados anteriormente dos grupos locais no computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIGroups.wsf](#ZTIGroups.wsf).  

 A configuração predefinida do **restaurar grupos** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Restaurar a grupos|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIGroups.wsf" /restore`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Se todas as condições forem verdadeiras:<br /><br /> \-**DoCapture** não é igual a Sim<br /><br /> \-                                 **DoCapture** não é igual ao preparar|  

####  <a name="RestoreUserState"></a>Restaurar estado do utilizador  
 Este passo de sequência de tarefas restaura o estado de utilizador capturados anteriormente para o computador de destino. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIUserState.wsf](#ZTIUserState.wsf).  

 Para obter mais informações sobre este tipo de passo, consulte [restaurar estado do utilizador](http://technet.microsoft.com/library/bb632881.aspx).  

 A configuração predefinida do **restaurar estado do utilizador** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Restaurar Estado do Utilizador|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIUserState.wsf" /restore`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Se todas as condições forem verdadeiras:<br /><br /> \-Se **DoCapture** não é igual a Sim<br /><br /> \-Se **DoCapture** não é igual ao preparar|  

#### <a name="set-image-build"></a>Compilação de imagem de conjunto  
 Este passo de sequência de tarefas define a **ImageBuild** propriedade para o valor contida no **OSCurrentVersion**. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **definir imagem criar** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Definir Variável da Sequência de Tarefas|  
|**Nome**|Compilação de imagem de conjunto|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Variável de sequência de tarefas**|**ImageBuild**|  
|**Valor**|**% OSCurrentVersion %**|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|**0 3010**|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="set-image-flags"></a>Defina os sinalizadores de imagem  
 Este passo de sequência de tarefas define a **ImageFlags** propriedade para o valor contida no **OSSKU**. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 A configuração predefinida do **definir sinalizadores de imagem** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Definir Variável da Sequência de Tarefas|  
|**Nome**|Defina os sinalizadores de imagem|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Variável de sequência de tarefas**|ImageFlags|  
|**Valor**|% OSSKU %|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="tattoo"></a>Tattoo  
 Este passo de sequência de tarefas tattoos o computador de destino com informações de identificação e a versão. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTITatoo.wsf](#ZTITatoo.wsf).  

 A configuração predefinida do **Tattoo** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Tattoo|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTITatoo.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|Qualificador condicional|Não foi especificado|  

#### <a name="validate"></a>Validar  
 Este passo de sequência de tarefas valida se o computador de destino cumpre as condições de pré-requisitos de implementação especificado. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIValidate.wsf](#ZTIValidate.wsf).  

 A configuração predefinida do **validar** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Validar|  
|**Nome**|Validar|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Certifique-se a memória mínima \(MB\)**|Selecionado. O Seletor de valor está definido como **768**.|  
|**Certifique-se a velocidade mínima do processador \(MHz\)**|Selecionado. O Seletor de valor está definido como **800**.|  
|**Certifique-se de que o tamanho de imagem especificado se encaixa \(MB\)**|Não selecionado.|  
|**Certifique-se o sistema operativo atual atualizar**|Selecionado. O Seletor de valor está definido como **servidor** ou **cliente**, consoante o modelo utilizado para criar a sequência de tarefas.|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="windows-update-pre-application-installation"></a>Windows Update \(Pre\-instalação da aplicação)  
 Este passo de sequência de tarefas instala atualizações para o computador de destino antes da instalação de aplicações. Segue-se uma listagem breve das definições que mostram a forma como este passo foi originalmente configurado dos modelos de sequência de tarefas do MDT.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIWindowsUpdate.wsf](#ZTIWindowsUpdate.wsf).  

 A configuração predefinida do **Windows Update \(Pre\-instalação da aplicação\)**  passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|   
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Windows Update \(Pre\-instalação da aplicação\)|  
|**Descrição**|Não foi especificado|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIWindowsUpdate.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|   
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

#### <a name="windows-update-post-application-installation"></a>Atualização do Windows (pós-aplicação instalação)  
 Este passo de sequência de tarefas é igual a **(pré-aplicações de instalação) do Windows Update** passo de sequência de tarefas.  

#### <a name="wipe-disk"></a>Disco de eliminação de dados  
 Este passo de sequência de tarefas apaga todas as informações do disco com o **formato** comando.  

 Para obter mais informações sobre o script elimina esta tarefa e as propriedades que são utilizadas, consulte [ZTIWipeDisk.wsf](#ZTIWipeDisk.wsf).  

 A configuração predefinida do **apagar disco** passo de sequência de tarefas é:  

##### <a name="properties"></a>Propriedades  
|**Nome**|**Valor**|  
|-|-|  
|**Tipo**|Executar Linha de Comandos|  
|**Nome**|Disco de eliminação de dados|  
|**Descrição**|Este será apenas se executar **WipeDisk**= TRUE no CustomSettings.ini|  

##### <a name="settings"></a>Definições  
|**Nome**|**Valor**|  
|-|-|  
|**Linha de comandos**|`cscript.exe "%SCRIPTROOT%\ZTIWipeDisk.wsf"`|  
|**Iniciar**|Não foi especificado|  
|**Executar este passo de como a seguinte conta**|Não foi especificado|  

##### <a name="options"></a>Opções  
|**Nome**|**Valor**|  
|-|-|  
|**Desativar este passo**|Não selecionada|  
|**Códigos de êxito**|0 3010|  
|**Continuar com o erro**|Não selecionada|  
|**Qualificador condicional**|Não foi especificado|  

## <a name="properties"></a>Propriedades  
 Os scripts utilizado no Lite Touch Installation (LTI) e ZTI propriedades de referência para determinar as definições de configuração utilizadas durante o processo de implementação e passos do processo. Os scripts criar algumas destas propriedades automaticamente. Outras propriedades tem de ser configuradas no ficheiro CustomSettings.ini. Algumas destas propriedades são:  

-   Específicas ZTI apenas  

-   Específicas LTI apenas  

-   Para utilização no ZTI e LTI  

 Utilize esta referência para ajudar a determinar as propriedades corretas para configurar e os valores válidos para incluir para cada propriedade.  

 Para cada propriedade é fornecidas as seguintes informações:  

-   **Descrição**. Fornece uma descrição da finalidade da propriedade e qualquer pertinentes informações sobre a personalização da propriedade.  

    > [!NOTE]
    >  A menos que especificado explicitamente para ZTI ou LTI apenas, uma propriedade é válida para ZTI e LTI.  

-   **Valor e descrição**. Indica os valores válidos para a propriedade e uma breve descrição do que significa que cada valor. (Os valores no italics indicam que um valor é substituído — por exemplo, o valor *user1*, *Utilizador2* indica que *user1* e *Utilizador2* deverá ser substituído com o nome real do contas de utilizador.)  

-   **Exemplo**. Fornece um exemplo de uma propriedade utilização conforme poderá aparecer nos ficheiros de. ini.  

 Para obter mais informações sobre estas e outras propriedades de sequência de tarefas que podem ser referenciadas ao efetuar uma implementação de ZTI, consulte [variáveis de sequência de tarefas de implementação do sistema operativo](http://technet.microsoft.com/library/bb632442.aspx).  

 Os scripts de implementação, geralmente, requerem valores de ser especificado em maiúsculas, para que leem corretamente. Por conseguinte, ao especificar valores de propriedade, utilize letras maiúsculas.  

### <a name="property-definition"></a>Definição de propriedade  
 As secções seguintes descrevem as propriedades que estão disponíveis para as implementações LTI e ZTI no MDT.  

> [!TIP]
>  As propriedades são ordenadas por ordem alfabética.  

####  <a name="\_SMSTSOrgName"></a>\_SMSTSOrgName  
 Customizes faixa de apresentação do motor do sequenciador de tarefas  
|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*nome*|O nome que será utilizado na faixa de apresentação do motor do sequenciador de tarefas|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] _SMSTSOrgName=Woodgrove Bank`|  

####  <a name="ADDSLogPath"></a>ADDSLogPath  
 Totalmente qualificado, o diretório de não UNC num disco rígido no computador local para alojar o AD DS ficheiros de registo. Se o diretório existe deve estar vazio. Se não existir, será criado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*log_path*|Totalmente qualificado, o diretório de não UNC num disco rígido no computador local para alojar o AD DS ficheiros de registo|  

|**Exemplo**|
|-|   
|`[Settings] Priority=Default  [Default] ADDSLogPath=%DestinationLogicalDrive%\Windows\NTDS`|  

####  <a name="ADDSPassword"></a>ADDSPassword  
 Credenciais da conta que podem ser utilizadas ao promover o servidor a controlador de domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*palavra-passe*|Credenciais da conta que podem ser utilizadas para a operação de promoção|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password>`|  

####  <a name="ADDSUserDomain"></a>ADDSUserDomain  
 Este é o domínio a conta especificada por **ADDSUserName** deve ser extraído da. Se a operação é para criar uma nova floresta, ou se tornar um servidor membro de uma atualização do controlador de domínio de cópia de segurança é sem predefinição. Se a operação criar uma nova árvore, a predefinição é que o nome DNS da floresta do computador está atualmente associado. Se a operação é criar um novo domínio subordinado ou uma réplica, em seguida, a predefinição é o nome DNS do domínio, que o computador está associado. Se a operação despromover o computador e o computador é um controlador de domínio num domínio subordinado, a predefinição é o nome DNS dos domínios principal. Se a operação é despromover o computador e o computador é um controlador de domínio de um domínio de raiz da árvore, a predefinição é o nome DNS da floresta.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*domínio*|A conta de nome de utilizador de domínio deverão ser executado a partir do|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password>`|  

####  <a name="ADDSUserName"></a>ADDSUserName  
 Credenciais da conta que serão utilizadas ao promover o servidor a controlador de domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*user_name*|Credenciais da conta que serão utilizadas para a operação de promoção|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=complex_password`|  

####  <a name="Administrators"></a>Administradores  
 Uma lista de contas de utilizador e grupos de domínio que serão adicionados ao grupo de administrador local no computador de destino. O **administradores** propriedade é uma lista de valores de texto que pode ser qualquer valor não vazio. O **administradores** propriedade tem um sufixo numérico (por exemplo, **Administrators001** ou **Administrators002**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*nome*|O nome de um utilizador ou grupo que está a ser adicionado ao grupo de administrador local|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff Administrators002=WOODGROVEBANK\North America East Help Desk Staff PowerUsers001=WOODGROVEBANK\User01 PowerUsers002=WOODGROVEBANK\User02`|  

####  <a name="AdminPassword"></a>AdminPassword  
 Define a palavra-passe que será atribuída à conta de utilizador de administrador local no computador de destino. Se não for especificado, será utilizada a palavra-passe de pré-implementação da conta de utilizador administrador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*admin_password*|A palavra-passe que está a ser atribuída à conta de utilizador administrador no computador de destino|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff AdminPassword=<admin_password>`|  

####  <a name="Applications"></a>Aplicações  
 Uma lista de GUIDs de aplicação que deve ser instalado no computador de destino. Estas aplicações estão especificadas no nó de aplicações no Deployment Workbench. Estes GUIDs são armazenadas no ficheiro Applications.xml. O **aplicações** propriedade é uma lista de valores de texto que pode ser qualquer valor não vazio. O **aplicações** propriedade tem um sufixo numérico (por exemplo, **Applications001** ou **Applications002**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*application_guid*|O GUID especificado pelo Deployment Workbench para a aplicação para ser implementado no computador de destino. O GUID corresponde à aplicação que GUID armazenado no ficheiro Applications.xml.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] Applications001={1D7DF331-47B7-472C-87B3-442597EC2F7D} Applications002={9d2b8999-5e4d-4f3d-bb05-edaaf4fe5628}`|  

####  <a name="ApplicationSuccessCodes"></a>ApplicationSuccessCodes  
 Uma lista delimitada por espaços códigos de erro utilizada pelo ZTIApplications script que determinam o êxito da instalação de aplicações.  

> [!NOTE]
>  Esta propriedade só é aplicável para o **instalar aplicação** tipo de passo de sequência de tarefas e quando **instalar várias aplicações** está selecionada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*error_codes*|Os códigos de erro que determinam quando as aplicações foi instaladas com êxito. Os valores predefinidos são **0** e **3010**.|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] ApplicationSuccessCodes=0 3010`|  

####  <a name="ApplyGPOPack"></a>ApplyGPOPack  
 Esta propriedade é utilizada para determinar se o **aplicar pacote de GPO Local** passo de sequência de tarefas é executado.  

> [!NOTE]
>  O valor predefinido para esta propriedade sempre efetua a **aplicar pacote de GPO Local** passo de sequência de tarefas. Explicitamente tem de fornecer um valor de "Não" para substituir este comportamento...  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**SIM**|O **aplicar pacote de GPO Local** passo de sequência de tarefas é executado. Este é o valor predefinido.|  
|**NÃO**|O **aplicar pacote de GPO Local** não é executado um passo de sequência de tarefas.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ApplyGPOPack=NO`|  

####  <a name="Architecture"></a>Arquitetura  
 A arquitetura de processador do processador que está atualmente em execução, ou seja, não necessariamente a arquitetura de processador suportada pelo computador de destino. Por exemplo, quando executar um sistema operativo de 32 bits – compatível com no processador de 64 bits, **arquitetura** indicará que a arquitetura de processador é de 32 bits.  

 Utilize o **CapableArchitecture** propriedade para identificar a arquitetura de processador real que suporta o computador de destino.  

> [!NOTE]
>  Esta propriedade está dinamicamente definida pelos scripts de MDT e não está configurada no CustomSettings.ini. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**x86**|Arquitetura do processador é de 32 bits.|  
|**x64**|Arquitetura do processador é de 64 bits.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="AreaCode"></a>AreaCode  
 O código de área de ser configuradas para o sistema operativo no computador de destino. Esta propriedade permite apenas carateres. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Area_Code*|O código de área em que o computador de destino está a ser implementada|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|  

####  <a name="AssetTag"></a>AssetTag  
 O número de tag do elemento associado ao computador de destino. O formato para números de etiquetas de recurso não está definido. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um computador específico.  

> [!NOTE]
>  Esta propriedade dinamicamente é definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*asset_tag*|O formato da etiqueta do recurso não está definido e é determinado através do padrão de etiqueta de ativo de cada organização.|  

|**Exemplo 1**|  
|-|   
|`[Settings] Priority=Default  [Default] OSDComputerName=HP-%AssetTag%`|  

|**Exemplo 2**|  
|-|    
|`[Settings] Priority=AssetTag, Default  [Default] OSInstall=YES  [0034034931] OSDComputerName=HPD530-1  [0034003233] OSDNEWMACHINENAME=BVMXP`|  

####  <a name="AutoConfigDNS"></a>AutoConfigDNS  
 Especifica se o Assistente de instalação do Active Directory configura DNS para o novo domínio, se detetar que o protocolo de atualização dinâmica de DNS não está disponível.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Configura o DNS para o novo domínio se o protocolo de atualização dinâmica de DNS não está disponível|  
|**NÃO**|Não configurar o DNS para o domínio|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] AutoConfigDNS=YES`|  

####  <a name="BackupDir"></a>BackupDir  
 A pasta na qual são armazenadas as cópias de segurança do computador de destino. Esta pasta existe sob o caminho UNC especificado no **BackupShare** propriedade. Se a pasta já não existir, será criado automaticamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Pasta*|O nome da pasta existente sob a pasta partilhada especificada no **BackupShare** propriedade|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|  

####  <a name="BackupDrive"></a>BackupDrive  
 A unidade para incluir na cópia de segurança do computador de destino. Esta propriedade está predefinida para a unidade que contém partição de disco 0 1. Pode também definir **todos os**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*backup_drive*|A letra de unidade da unidade para efetuar cópias de segurança|  
|**TODOS OS**|Fazer cópias de segurança de todas as unidades no computador de destino|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|  

####  <a name="BackupFile"></a>Ficheiro  
 Especifica o ficheiro WIM que será utilizado pelo ZTIBackup.wsf script. Para obter mais informações sobre o script utiliza esta propriedade, consulte [ZTIBackup.wsf](#ZTIBackup.wsf).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*BackupDir*|O nome do ficheiro de formato Windows Imaging (WIM) a utilizar durante a cópia cópias de segurança.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupFile=%OSDComputerName%.wim`|  

####  <a name="BackupShare"></a>BackupShare  
 A pasta partilhada no qual estão armazenadas as cópias de segurança do computador de destino.  

 As credenciais utilizadas para aceder a esta pasta partilhada para:  

-   LTI são as credenciais introduzidas no Assistente de implementação.  

-   ZTI são as credenciais utilizadas pela conta do Configuration Manager avançadas cliente acesso à rede.  

 As permissões necessárias nesta partilha são os seguintes:  

-   **Computadores de domínio**. Permitir que a permissão de criar o pastas/Acrescentar dados.  

-   **Utilizadores de domínio**. Permitir que a permissão de criar o pastas/Acrescentar dados.  

-   **Proprietário criador**. Permitir que a permissão de controlo total.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*UNC_path*|O caminho UNC da pasta partilhada<br /><br /> Nota:<br /><br /> O caminho UNC especificado nesta propriedade tem de existir antes de implementar o sistema operativo de destino.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|  

####  <a name="BDEAllowAlphaNumericPin"></a>BDEAllowAlphaNumericPin  
 Esta propriedade configura se o BitLocker PINs conter valores alfanuméricos.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|São permitidos carateres alfanuméricos no PIN.<br /><br /> Nota:<br /><br /> Além de definir esta propriedade **Sim**, a **Permitir PINs melhorados para arranque** definição de política de grupo tem de estar ativada.|  
|**NÃO**|Apenas carateres são permitidos no PIN.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEAllowAlphaNumericPin=YES BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEDriveLetter"></a>BDEDriveLetter  
 A letra de unidade da partição que não está encriptada pelo BitLocker, também conhecido como o *Volume de sistema*. SYSVOL é o diretório que contém os ficheiros específicos de hardware necessários para carregar computadores Windows depois do BIOS tem arrancado da plataforma.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*Drive_letter*|A designação de letra da unidade lógica para o Volume de sistema (tais como S ou T). O valor predefinido é **S**.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEDriveSize"></a>BDEDriveSize  
 O tamanho da partição do sistema BitLocker. O valor for especificado em megabytes. No exemplo, o tamanho da partição BitLocker para criar é quase 2 GB (2.000 MB).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*drive_size*|O tamanho da partição em megabytes; os tamanhos de predefinição são:<br /><br /> -Windows 7 e Windows Server 2008 R2: 300 MB|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEInstall"></a>BDEInstall  
 O tipo de instalação do BitLocker para ser executada. Proteger o computador de destino utilizando um dos seguintes métodos:  

-   Um microcontroller TPM  

-   Um TPM e uma chave de arranque externa (utilizando uma chave que é normalmente armazenada numa unidade flash USB [pen USB])  

-   Um TPM e PIN  

-   Uma chave de arranque externa  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**TPM**|Proteger o computador com TPM apenas. O TPM é um microcontroller que armazena as chaves, palavras-passe e certificados digitais. O microcontroller é, geralmente, uma parte integral da motherboard computador.|  
|**TPMKey**|Proteger o computador com TPM e uma chave de arranque. Utilize esta opção para criar uma chave de arranque e para as guardar numa pen USB. A chave de arranque tem de estar presente na porta sempre que o computador é iniciado.|  
|**TPMPin**|Proteger o computador com TPM e um pin. Utilize esta opção juntamente com o **BDEPin** propriedade.|  
|**Chave**|Proteger o computador com uma chave externa (a chave de recuperação) que pode ser armazenada numa pasta, no AD DS, ou impressas.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEInstallSuppress"></a>BDEInstallSuppress  
 Indica se o processo de implementação deve ignorar a instalação do BitLocker.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**SIM**|Não tente instalar o BitLocker.|  
|**NÃO**|Tentativa de instalar o BitLocker.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=YES`|  

####  <a name="BDEKeyLocation"></a>BDEKeyLocation  
 A localização para armazenar a chave de recuperação do BitLocker e a chave de arranque.  

> [!NOTE]
>  Se esta propriedade for configurada utilizando o Assistente de implementação, a propriedade tem de ser a letra de unidade de um disco amovível. Se o **SkipBitLocker** propriedade está definida como **verdadeiro** para que o **especificar a configuração do BitLocker** é ignorada a página do assistente, esta propriedade pode ser definida como um caminho UNC CustomSettings.ini ou na base de dados de MDT (BD do MDT).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Localização*|Especifica onde será armazenada a chave de recuperação; tem de ser um caminho UNC ou a letra de unidade de um disco amovível. Se não definir primeira unidade amovível disponível será utilizada.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEPin"></a>BDEPin  
 O PIN para ser atribuído ao computador de destino, quando configurar o BitLocker e o **BDEInstall** ou **OSDBitLockerMode** propriedades forem definidas **TPMPin**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*PIN*|O PIN para ser utilizado para o BitLocker. O PIN pode estar entre 4 e 20 dígitos.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMPin BDEPin=123456789`|  

####  <a name="BDERecoveryKey"></a>BDERecoveryKey  
 Um valor booleano que indica se o processo cria uma chave de recuperação para o BitLocker. A chave é utilizada para recuperar dados encriptados num BitLocker volume. Esta chave é criptograficamente equivalente a uma chave de arranque. Se estiver disponível, a chave de recuperação desencriptar a chave mestra de volume (VMK), que, por sua vez, desencriptar a chave de encriptação de volume completo (FVEK).  

> [!NOTE]
>  A chave de recuperação é armazenada na localização especificada no **BDEKeyLocation** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**AD**|É criada uma chave de recuperação.|  
|Não foi especificado|Não é criada uma chave de recuperação.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|  

####  <a name="BDEWaitForEncryption"></a>BDEWaitForEncryption  
 Especifica que o processo de implementação deve continue até que o BitLocker concluiu o processo de encriptação para todas as unidades especificados. Especifica verdadeiro foi aumentar substancialmente o tempo necessário para concluir o processo de implementação.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Especifica que o processo de implementação deve aguardar para encriptação de unidade concluir.|  
|**FALSO**|Especifica que o processo de implementação não deve aguardar para encriptação de unidade concluir.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerStartupKeyDrive=C: OSDBitLockerCreateRecoveryPassword=AD BDEWaitForEncryption=TRUE`|  

####  <a name="BitsPerPel"></a>BitsPerPel  
 Uma definição para apresentar cores no computador de destino. A propriedade pode conter dígitos numéricos e corresponde à definição de qualidade de cor. No exemplo, **32** indica 32 bits por pixel da qualidade de cor. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

> [!NOTE]
>  Os valores predefinidos (no ficheiro de modelo Unattend.xml) são resolução horizontal de 1.024 pixéis, resolução vertical 768 pixéis, profundidade de cor de 32 bits e velocidade de atualização vertical Hertz 60 (Hz).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*bits_per_pixel*|O número de bits por pixel a utilizar para cores. O valor predefinido é a predefinição para o sistema operativo que está a ser implementada.|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|  

####  <a name="BuildID"></a>BuildID  
 Identifica a sequência de tarefas do sistema operativo ser implementado no computador de destino. Criar o ID de sequência de tarefas no nó sequências de tarefas no Deployment Workbench. O **BuildID** propriedade permite apenas carateres alfanuméricos, hífenes (-) e carateres de sublinhado (\_). O **BuildID** propriedade não pode estar em branco ou conter espaços.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*build_id*|Identificador da sequência de tarefas do sistema operativo, tal como definido no Deployment Workbench para o sistema de operativo de destino que está a ser implementada<br /><br /> Nota:<br /><br /> Certifique-se de utilizar o **TaskSequenceID** especificado na interface de utilizador (IU) do Deployment Workbench e não o GUID do **TaskSequenceID**.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] BuildID=BareMetal`|  

####  <a name="CapableArchitecture"></a>CapableArchitecture  
 A arquitetura de processador do processador suportado pelo computador de destino, não atual arquitetura do processador que está em execução. Por exemplo, quando executar um sistema operativo de 32 bits-compatível com no processador de 64 bits, **CapableArchitecture** indicará que a arquitetura de processador é de 64 bits.  

 Utilize o **arquitetura** propriedade para ver a arquitetura de processador que está atualmente em execução.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|**x86**|Arquitetura do processador é de 32 bits.|  
|**x64**|Arquitetura do processador é de 64 bits.|  

|**Exemplo**|  
|-|   
|Nenhum|  

####  <a name="CaptureGroups"></a>CaptureGroups  
 Controla se a associação do grupo de grupos locais no computador de destino é capturada. Esta associação de grupo é capturada durante a fase de captura de estado e é restaurada durante a fase de restauro de estado.  

> [!NOTE]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**NÃO**|Não captura nenhuma informação de associação de grupo.|  
|**TODOS OS**|Captura a associação de todos os grupos locais no computador de destino.|  
|**SIM**|Captura a associação a grupos listados nas propriedades dos grupos e os grupos incorporados administrador e de utilizadores avançados. Este é o valor predefinido se não for especificado outro valor. (**Sim** é o valor típico.)|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ CaptureGroups=YES Groups1=NYC Application Management Groups2=NYC Help Desk Users`|  

####  <a name="ChildName"></a>ChildName  
 Especifica se pretende acrescentar a etiqueta DNS no início do nome de um domínio de serviço de diretório existentes ao instalar um domínio subordinado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|O nome do domínio subordinado|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] ChildName=childdom.parentdom.WoodGroveBank.com`|  

####  <a name="ComputerBackupLocation"></a>ComputerBackupLocation  
 A pasta de rede partilhada onde está armazenada a cópia de segurança do computador. Se a pasta de destino ainda não existir, é criado automaticamente.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*em branco*|Igual ao **automática**.|  
|*UNC_path*|O caminho UNC para a pasta de rede partilhada onde está armazenada a cópia de segurança.|  
|**AUTOMÁTICA**|Cria uma cópia de segurança num disco rígido local, se espaço disponível. Caso contrário, a cópia de segurança é guardada numa localização de rede especificada no **BackupShare** e **BackupDir** propriedades.|  
|**REDE**|Cria uma cópia de segurança numa localização de rede especificada no **BackupShare** e **BackupDir**.|  
|**NENHUM**|Não será efetuada nenhuma cópia de segurança.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ ComputerBackupLocation=NETWORK BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE`|  

####  <a name="ComputerName"></a>ComputerName  
 Esta propriedade foi preterida. Utilize **OSDComputerName** em vez disso.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

|**Exemplo**|  
|-|   
|Nenhum|  

####  <a name="ConfigFileName"></a>ConfigFileName  
 Especifica o nome do ficheiro de configuração utilizado durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*file_name*|Especifica o nome do ficheiro de configuração utilizado durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="ConfigFilePackage"></a>ConfigFilePackage  
 Especifica o ID de pacote para o pacote de configuração utilizado durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*pacote*|Especifica o ID de pacote para o pacote de configuração utilizado durante implementações do OEM|  

|**Exemplo**|  
|-|   
|Nenhum|  

####  <a name="ConfirmGC"></a>ConfirmGC  
 Especifica se a réplica também é um catálogo global.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Torna a réplica um catálogo global, se a cópia de segurança foi um catálogo global.|  
|**NÃO**|Não faz a réplica um catálogo global.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] ConfirmGC=YES`|  

####  <a name="CountryCode"></a>Indicativo do país  
 O código de país para ser configurado para o sistema operativo no computador de destino. Esta propriedade permite apenas carateres. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*country_code*|O código de país em que o computador de destino está a ser implementada|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|  

####  <a name="CriticalReplicationOnly"></a>CriticalReplicationOnly  
 Especifica se a operação de promoção realiza apenas replicação crítica e, em seguida, continua, ignorar a parte reinicio (e potencialmente demorada) de replicação.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Ignora a replicação reinicio|  
|**NÃO**|Não ignore o reinicio replicação|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] CriticalReplicationOnly=YES`|  

####  <a name="CustomDriverSelectionProfile"></a>CustomDriverSelectionProfile  
 Especifica a seleção personalizada perfil utilizado durante a instalação de controlador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*perfil*|Perfil de seleção personalizados utilizado durante a instalação de controlador|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] CustomDriverSelectionProfile=CustomDrivers`|  

####  <a name="CustomPackageSelectionProfile"></a>CustomPackageSelectionProfile  
 Especifica a seleção personalizada perfil utilizado durante a instalação do pacote.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*perfil*|Perfil de seleção personalizados utilizado durante a instalação do pacote|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] CustomPackageSelectionProfile=CustomPackages`|  

####  <a name="CustomWizardSelectionProfile"></a>CustomWizardSelectionProfile  
 Especifica o perfil de seleção personalizada utilizado pelo Assistente para a apresentação de vários itens de filtragem.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*perfil*|Perfil de seleção personalizada pelo Assistente para a apresentação de vários itens de filtragem|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] CustomWizardSelectionProfile=CustomWizard`|  

####  <a name="Database"></a>Base de dados  
 A propriedade que especifica a base de dados a ser utilizado para consultar os valores de propriedade de colunas na tabela especificada no **tabela** propriedade. A base de dados reside num computador especificado no **SQLServer** propriedade. A instância do Microsoft SQL Server® no computador especificada no **instância** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|\-||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*base de dados*|O nome da base de dados a ser utilizado para consultar os valores de propriedade|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="DatabasePath"></a>DatabasePath  
 Especifica o completamente qualificado de não\-caminho UNC para um diretório num disco fixo no computador de destino que contém a base de dados do domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*caminho*|Especifica o completamente qualificado de não\-caminho UNC para um diretório num disco fixo no computador local que contém a base de dados do domínio|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DatabasePath=%DestinationLogicalDrive%\Windows\NTSD`|  

####  <a name="DBID"></a>DBID  
 Especifica a conta de utilizador utilizada para ligar ao computador com o SQL Server \(especificada pelo **SQLServer** propriedade\) utilizando a autenticação do SQL Server. O **DBPwd** propriedade fornece a palavra-passe da conta de utilizador no **DBID** propriedade.  

> [!NOTE]
>  Autenticação do SQL Server não é como segura como autenticação integrada do Windows. Autenticação integrada do Windows é o método de autenticação recomendada. Utilizar o **DBID** e **DBPwd** propriedades armazena as credenciais em texto não encriptado no ficheiro CustomSettings.ini e, por conseguinte, não é seguras. Para obter mais informações sobre como utilizar a autenticação integrada do Windows, consulte o [SQLShare](#SQLShare) propriedade.  

> [!NOTE]
>  Esta propriedade é configurável apenas ao editar manualmente os ficheiros CustomSettings.ini e BootStrap.ini.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|\-||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*utilizador\_id*|O nome das credenciais de conta de utilizador utilizada para aceder ao computador com o SQL Server utilizando a autenticação do SQL Server|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 DBID=SQL_User-01 DBPwd=<complex_password> NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="DBPwd"></a>DBPwd  
 Especifica a palavra-passe para a conta de utilizador especificado no **DBID** propriedade. O **DBID** e **DBPwd** propriedades fornecem as credenciais para efetuar a autenticação do SQL Server para o computador a executar o SQL Server \(especificada pelo **SQLServer**  propriedade\).  

> [!NOTE]
>  Autenticação do SQL Server não é como segura como autenticação integrada do Windows. Autenticação integrada do Windows é o método de autenticação recomendada. Utilizar o **DBID** e **DBPwd** propriedades armazena as credenciais em texto não encriptado no ficheiro CustomSettings.ini e, por conseguinte, não é seguras. Para obter mais informações sobre como utilizar a autenticação integrada do Windows, consulte o [SQLShare](#SQLShare) propriedade.  

> [!NOTE]
>  Esta propriedade é configurável apenas ao editar manualmente os ficheiros CustomSettings.ini e BootStrap.ini.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|\-||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*utilizador\_palavra-passe*|A palavra-passe para as credenciais da conta de utilizador especificado no **DBID** propriedade para utilizar autenticação do SQL Server|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 DBID=SQL_User-01 DBPwd=<complex_password> NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="Debug"></a>Depuração  
 Controla a verbosidade de mensagens escritas para os ficheiros de registo do MDT. Esta propriedade pode ser configurada para ajudar na resolução de problemas implementações, fornecendo informações expandidas sobre o processo de implementação do MDT.  

 Pode definir esta propriedade ao iniciar o script de LiteTouch.vbs com o  **\/debug: true** comando\-parâmetro de linha da seguinte forma:  

```  
cscript.exe LiteTouch.vbs /debug:true  
```  

 Depois do script de LiteTouch.vbs é iniciado, o **depurar** valor da propriedade está definido como **verdadeiro**, e todos os outros scripts são automaticamente ler o valor desta propriedade e fornecem informações verbosas.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou na base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Depurar o registo está ativado, que inclui o seguinte:<br /><br /> \-As mensagens verbosas são registadas.<br /><br /> \-Mensagens preteridas são registadas como erros.|  
|**FALSO**|Depurar o registo não está ativado. Este é o valor predefinido.|  

|**Exemplo**|  
|-|   
|Nenhum|  

####  <a name="DefaultGateway"></a>DefaultGateway  
 O endereço IP do gateway predefinido a ser utilizado pelo computador de destino. O formato do endereço IP devolvido pela propriedade é padrão separada por pontos\-notação decimal; por exemplo, 192.168.1.1. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um grupo de computadores com base nas sub-redes IP no qual estão localizados.  

> [!NOTE]
>  Esta propriedade dinamicamente é definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*predefinição\_gateway*|O endereço IP do gateway predefinido em padrão separada por pontos\-notação decimal|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=DefaultGateway, Default  [Default] OSInstall=YES  [DefaultGateway] 192.168.0.1=HOUSTON 11.1.1.11=REDMOND 172.28.20.1=REDMOND  [REDMOND] Packages001=XXX00004:Program4 Packages002=XXX00005:Program5  [HOUSTON] Packages001=XXX00006:Program6 Packages002=XXX00007:Program7 Packages003=XXX00008:Program8`|  

####  <a name="DeployDrive"></a>DeployDrive  
 O valor utilizado pelos scripts para aceder aos ficheiros e executar programas na partilha de implementação que cria a Deployment Workbench. A propriedade devolve a letra de unidade mapeada para o **DeployRoot** propriedade. ZTIApplications.wsf utiliza o **DeployDrive** propriedade quando executar qualquer comando\-linha programas com extensão. bat ou. cmd.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*unidade\_letra*|A designação de letra da unidade lógica em que o sistema operativo de destino é para ser instalada \(como C ou D\)|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="DeploymentMethod"></a>DeploymentMethod  
 O método que está a ser utilizado para a implementação (UNC, suporte de dados ou do Configuration Manager).  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**UNC**|A implementação é efetuada para o computador de destino através da rede.|  
|**Suporte de dados**|A implementação é feita a partir do suporte de dados local (por exemplo, DVD ou disco rígido) no computador de destino.|  
|**SCCM**|ZTI utiliza este método para o Configuration Manager.|  

|**Exemplo**|  
|-|   
|Nenhum|  

####  <a name="DeploymentType"></a>DeploymentType  
 O tipo de implementação a ser efetuada, com base no cenário de implementação. Para ZTI, esta propriedade está definida dinamicamente pelos scripts de MDT e não está configurada no CustomSettings.ini. Para LTI, pode ignorar a página no Assistente de implementação em que está selecionado o tipo de implementação. Além disso, pode especificar o tipo de implementação através da transmissão de um dos valores listados abaixo para o script de LiteTouch.wsf como uma opção de linha de comandos.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**NEWCOMPUTER**|O computador de destino é um novo computador que nunca foi um membro da rede.|  
|**ATUALIZAR**|O computador de destino é um computador existente na rede que necessita o padrão de ambiente de trabalho para voltar a implementar.|  
|**SUBSTITUIR**|Um computador existente na rede está a ser substituído por um novo computador. Os dados de migração de estado do utilizador são transferidos do computador existente para um novo computador.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeploymentType=NEWCOMPUTER`|  

####  <a name="DeployRoot"></a>DeployRoot  
 Especifica o caminho local para a pasta que é a raiz da estrutura de pasta que utiliza o MDT ou UNC. Esta estrutura de pasta contém os ficheiros de configuração, scripts e outras pastas e ficheiros que utiliza o MDT. O valor desta propriedade é definido com base das seguintes tecnologias de implementação do MDT:  

-   **LTI**. Esta propriedade é o caminho UNC para a partilha de implementação que cria o Deployment Workbench. Utilize esta propriedade para selecionar uma partilha de implementação específicos. A utilização desta propriedade mais comuns é no ficheiro BootStrap.ini para identificar uma partilha de implementação antes da ligação à partilha de implementação é estabelecida. Todas as outras pastas de partilha de implementação são relativa esta propriedade (tais como controladores de dispositivo, pacotes de idiomas ou sistemas operativos).  

-   **ZTI**. Esta propriedade é o caminho local para a pasta para o qual o pacote de ficheiros do MDT é copiado. O **utilizar o pacote do Toolkit** passo de sequência de tarefas copia o pacote de ficheiros do MDT para uma pasta local no computador de destino e, em seguida, configura automaticamente esta propriedade para a pasta local.  

    > [!NOTE]
    >  Para ZTI, esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou na base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*caminho*|O UNC ou o caminho local para o.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ UserDataLocation=NONE`|  

####  <a name="DestinationDisk"></a>DestinationDisk  
 Número do disco que a imagem será implementada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*disk_number*|O número do disco para o qual a imagem será implementada|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DestinationDisk=0`|  

####  <a name="DestinationLogicalDrive"></a>DestinationLogicalDrive  
 A unidade lógica a que a imagem será implementada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|   
|*logical_drive_number*|A unidade lógica a que a imagem será implementada|  

|**Exemplo 1**|  
|-|   
|`[Settings] Priority=Default  [Default] DestinationLogicalDrive=0`|  

|**Exemplo 2**|  
|-|  
|`[Settings] Priority=Default  [Default] DestinationLogicalDrive=0`<br /><br /> `[Settings] Priority=Default  [Default] InstallDNS=YES DomainNetBIOSName=WoodGroveBank NewDomain=Child DomainLevel=3 ForestLevel=3 NewDomainDNSName=newdom.WoodGroveBank.com ParentDomainDNSName=WoodGroveBank.com AutoConfigDNS=YES ConfirmGC=YES CriticalReplicationOnly=NO ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password> DatabasePath=%DestinationLogicalDrive%\Windows\NTDS ADDSLogPath=%DestinationLogicalDrive%\Windows\NTDS SysVolPath=%DestinationLogicalDrive%\Windows\SYSVOL SafeModeAdminPassword=<complex_password>`|  

####  <a name="DestinationPartition"></a>DestinationPartition  
 Partição de disco para o qual a imagem será implementada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*partition_number*|O número de partição para que a imagem será implementada|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DestinationPartition=1`|  

####  <a name="DHCPScopes"></a>DHCPScopes  
 Especifica o número de âmbitos DHCP para configurar.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|*âmbitos*|Especifica o número de âmbitos DHCP para configurar|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes=1`|  

####  <a name="DHCPScopesxDescription"></a>DHCPScopesxDescription  
 A descrição do âmbito de DHCP.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*Descrição*|A descrição do âmbito de DHCP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes0Description=DHCPScope0`|  

####  <a name="DHCPScopesxEndIP"></a>DHCPScopesxEndIP  
 Especifica o endereço IP final para o âmbito DHCP.  

 O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*end_IP*|Especifica o endereço IP final para o âmbito DHCP|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0EndIP=192.168.0.30`|  

####  <a name="DHCPScopesxExcludeEndIP"></a>DHCPScopesxExcludeEndIP  
 Especifica o endereço IP final para a exclusão de âmbito DHCP. Endereços IP que são excluídos do âmbito não são oferecidos pelo servidor DHCP aos clientes obter concessões de neste âmbito.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|*exclude_end_IP*|Especifica o endereço IP final para a exclusão de âmbito DHCP|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0ExcludeEndIP=192.168.0.15`|  

####  <a name="DHCPScopesxExcludeStartIP"></a>DHCPScopesxExcludeStartIP  
 Especifica o endereço IP inicial para a exclusão de âmbito DHCP. Endereços IP que são excluídos do âmbito não são oferecidos pelo servidor DHCP aos clientes obter concessões de neste âmbito.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*exclude_start_IP*|Especifica o endereço IP inicial para a exclusão de âmbito DHCP|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] DHCPScopes0ExcludeStartIP=192.168.0.10`|  

####  <a name="DHCPScopesxIP"></a>DHCPScopesxIP  
 Especifica a sub-rede IP do âmbito.  

 O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*IP*|Especifica a sub-rede IP do âmbito|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0IP=192.168.0.0`|  

####  <a name="DHCPScopesxName"></a>DHCPScopesxName  
 Um nome de utilizador definable atribuídos ao âmbito.  

 O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*nome*|Um nome de utilizador definable atribuídos ao âmbito|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0Name=DHCPScope0`|  

####  <a name="DHCPScopesxOptionDNSDomainName"></a>DHCPScopesxOptionDNSDomainName  
 Especifica o nome de domínio que o cliente DHCP deve utilizar ao resolver os nomes de domínio não qualificados com o DNS.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*DNS_domain_name*|Especifica o nome de domínio que o cliente DHCP deve utilizar ao resolver os nomes de domínio não qualificados com DNS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionDNSDomainName=WoodGroveBank.com`|  

####  <a name="DHCPScopesxOptionDNSServer"></a>DHCPScopesxOptionDNSServer  
 Especifica uma lista de endereços IP para servidores de nome DNS disponíveis para o cliente. Quando é atribuído a mais de um servidor, o cliente interpreta e utiliza os endereços ordem especificada.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*DNS_server*|Especifica uma lista de endereços IP para servidores de nome DNS disponíveis para o cliente|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionDNSServer=192.168.0.2`|  

####  <a name="DHCPScopesxOptionLease"></a>DHCPScopesxOptionLease  
 A duração de concessão DHCP é válido para o cliente.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*concessão*|A duração de concessão DHCP é válido para o cliente|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionLease=7`|  

####  <a name="DHCPScopesxOptionNBTNodeType"></a>DHCPScopesxOptionNBTNodeType  
 Especifica o tipo de nó de cliente para clientes de NetBT.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**1**|Configura o tipo de nó como nó de b|  
|**2**|Configura o tipo de nó como nó de p|  
|**4**|Configura o tipo de nó como nó de m|  
|**8**|Configura o tipo de nó como nó de h|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionNBTNodeType=4`|  

####  <a name="DHCPScopesxOptionPXEClient"></a>DHCPScopesxOptionPXEClient  
 Especifica o endereço IP utilizado para o código de arranque de configuração de cliente PXE.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|*PXE_client*|Especifica o endereço IP utilizado para o código de arranque de configuração de cliente PXE|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionPXEClient=192.168.0.252`|  

####  <a name="DHCPScopesxOptionRouter"></a>DHCPScopesxOptionRouter  
 Especifica uma lista de endereços IP para os routers na sub-rede de cliente. Quando é atribuído a mais do que um router, o cliente interpreta e utiliza os endereços ordem especificada. Esta opção é normalmente utilizada para atribuir um gateway predefinido para clientes DHCP numa sub-rede.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*router*|Especifica uma lista de endereços IP para os routers na sub-rede cliente|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionRouter=192.168.0.253`|  

####  <a name="DHCPScopesxOptionWINSServer"></a>DHCPScopesxOptionWINSServer  
 Especifica os endereços IP a ser utilizada para NBNSes na rede.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*WINS_server*|Especifica os endereços IP a ser utilizada para NBNSes na rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionWINSServer=192.168.0.2`|  

####  <a name="DHCPScopesxStartIP"></a>DHCPScopesxStartIP  
 O endereço IP inicial para o intervalo de endereços IP que estão a ser incluído no âmbito.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*start_IP*|O endereço IP inicial para o intervalo de endereços IP que estão a ser excluído do âmbito|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0StartIP=192.168.0.20`|  

####  <a name="DHCPScopesxSubnetMask"></a>DHCPScopesxSubnetMask  
 Especifica a máscara de sub-rede da sub-rede do cliente.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DHCP.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*subnet_mask*|Especifica a máscara de sub-rede da sub-rede IP do cliente|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPScopes0SubnetMask=255.255.255.0`|  

####  <a name="DHCPServerOptionDNSDomainName"></a>DHCPServerOptionDNSDomainName  
 Especifica o sufixo de domínio DNS específico da ligação de computadores cliente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|    
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|*DNS_domain_name*|Especifica o sufixo de domínio DNS específico da ligação de computadores cliente|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] DHCPServerOptionDNSDomainName=Fabrikam.com`|  

####  <a name="DHCPServerOptionDNSServer"></a>DHCPServerOptionDNSServer  
 Especifica uma lista de endereços IP a ser utilizados como servidores de nome DNS que estão disponíveis para o cliente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*DNS_server*|Especifica uma lista de endereços IP a ser utilizados como servidores de nome DNS que estão disponíveis para o cliente|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPServerOptionDNSServer=192.168.0.1,192.168.0.2`|  

####  <a name="DHCPServerOptionNBTNodeType"></a>DHCPServerOptionNBTNodeType  
 Especifica o tipo de nó de cliente para clientes de NetBT.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|**1**|Configura o tipo de nó como nó de b|  
|**2**|Configura o tipo de nó como nó de p|  
|**4**|Configura o tipo de nó como nó de m|  
|**8**|Configura o tipo de nó como nó de h|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPServerOptionNBTNodeType=4`|  

####  <a name="DHCPServerOptionPXEClient"></a>DHCPServerOptionPXEClient  
 Especifica o endereço IP utilizado para o código de arranque de configuração de cliente PXE.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*PXE_client*|Especifica o endereço IP utilizado para o código de arranque de configuração de cliente PXE|  

|**Exemplo**|  
|-|    
|`[Settings] Priority=Default  [Default] DHCPServerOptionPXEClient=192.168.0.252`|  

####  <a name="DHCPServerOptionRouter"></a>DHCPServerOptionRouter  
 Especifica uma lista de endereços IP para os routers na sub-rede de cliente. Quando é atribuído a mais do que um router, o cliente interpreta e utiliza os endereços ordem especificada. Esta opção é normalmente utilizada para atribuir um gateway predefinido para clientes DHCP numa sub-rede.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*router*|Especifica uma lista de endereços IP para os routers na sub-rede cliente|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DHCPServerOptionRouter=192.168.0.253`|  

####  <a name="DHCPServerOptionWINSServer"></a>DHCPServerOptionWINSServer  
 Especifica os endereços IP a ser utilizada para NBNSes na rede.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|    
|*WINS_server*|Especifica os endereços IP a ser utilizada para NBNSes na rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DHCPServerOptionWINSServer=192.168.0.2`|  

####  <a name="Dialing"></a>Marcação por  
 O tipo de marcação por suportadas pela infraestrutura de telefonia onde está localizado o computador de destino. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**PULSE**|A infraestrutura de telefonia suporta marcação pulse.|  
|**SINAL**|A infraestrutura de telefonia suporta touch-tone marcação.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|  

####  <a name="DisableTaskMgr"></a>DisableTaskMgr  
 Esta propriedade controla a capacidade de um utilizador para iniciar o Gestor de tarefas ao premir CTRL + ALT + DEL. Depois do utilizador inicia o Gestor de tarefas, pode interromper a sequência de tarefas LTI durante a execução no novo sistema operativo no computador de destino. Esta propriedade é utilizada em conjunto com o **HideShell** propriedade e só é válido quando o **HideShell** propriedade está definida como **Sim**.  

> [!NOTE]
>  Esta propriedade e o **HideShell** propriedade têm de ser definida **Sim** para impedir que o utilizador premir CTRL + ALT + DEL e interromper o LTI sequência de tarefas.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|   
|**SIM**|Impedi que o utilizador conseguir iniciar o Gestor de tarefas ao premir CTRL + ALT + DEL e subsequentemente interromper a sequência de tarefas LTI.|  
|**NÃO**|Permitir que o utilizador iniciar o Gestor de tarefas ao premir CTRL + ALT + DEL e subsequentemente interromper a sequência de tarefas LTI. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DisableTaskMgr=YES HideShell=YES`|  

####  <a name="DNSServerOptionBINDSecondaries"></a>DNSServerOptionBINDSecondaries  
 Determina se deve utilizar o formato de transferência rápida para a transferência de uma zona para os servidores DNS a executar implementações de ENLACE legadas.  

 Por predefinição, todos os servidores DNS baseado no Windows utilizam um formato de transferência de zona rápida. Este formato utiliza a compressão e pode incluir vários registos por mensagem TCP durante uma transferência ligada. Este formato também é compatível com os servidores DNS baseado no ENLACE mais recentes que executam a versão 4.9.4 e posterior.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|**VERDADEIRO**|Permite o ENLACE de dados secundárias|  
|**FALSO**|Não permitir que o ENLACE de dados secundárias|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSServerOptionBINDSecondaries=TRUE`|  

####  <a name="DNSServerOptionDisableRecursion"></a>DNSServerOptionDisableRecursion  
 Determina se utiliza ou não o servidor DNS recursão. Por predefinição, o serviço servidor DNS está ativado para utilizar recursão.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|    
|**VERDADEIRO**|Desativa a recursão no servidor DNS|  
|**FALSO**|Permite a recursão no servidor DNS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSServerOptionDisableRecursion=TRUE`|  

####  <a name="DNSServerOptionEnableNetmaskOrdering"></a>DNSServerOptionEnableNetmaskOrdering  
 Determina se o servidor DNS reordena registos de recursos de endereço (A) dentro do mesmo registo de recursos que está definido na resposta do servidor a uma consulta com base no endereço IP de origem da consulta.  

 Por predefinição, o serviço servidor DNS utiliza a prioridade de sub-rede local para registos de recursos A reordenação.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**VERDADEIRO**|Permite a ordenação de máscara de rede|  
|**FALSO**|Desativa a ordenação de máscara de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableNetmaskOrdering=TRUE`|  

####  <a name="DNSServerOptionEnableRoundRobin"></a>DNSServerOptionEnableRoundRobin  
 Determina se o servidor DNS utiliza o mecanismo de round robin para rodar e reordenar uma lista de registos de recursos, se existirem vários registos de recursos do mesmo tipo que existem para uma resposta de consulta.  

 Por predefinição, o serviço servidor DNS utiliza o round robin.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**VERDADEIRO**|Permite o round robin|  
|**FALSO**|Desativa o round robin|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableRoundRobin=TRUE`|  

####  <a name="DNSServerOptionEnableSecureCache"></a>DNSServerOptionEnableSecureCache  
 Determina se o servidor DNS tenta limpar as respostas para evitar pollution de cache. Esta definição está ativada por predefinição. Por predefinição, os servidores DNS utilizam uma opção de resposta segura que elimina adicionar registos de recursos não relacionados que estão incluídos na resposta referência para a respetiva cache. Na maioria dos casos, os nomes que são adicionados em respostas de referência são normalmente colocadas em cache e ajudam a agilizar a resolução de consultas DNS subsequentes.  

 No entanto, com esta funcionalidade, o servidor pode determinar que referida nomes estão potencialmente polluting ou inseguras e, em seguida, eliminação-las. O servidor determina se deve colocar em cache o nome que é oferecido numa referência on the basis of se faz parte da exata, relacionada, DNS nome árvore de domínio para o qual o nome de consultado original foi efetuado.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|   
|**VERDADEIRO**|Ativa a cache de segurança|  
|**FALSO**|Desativa a cache de segurança|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableSecureCache=TRUE`|  

####  <a name="DNSServerOptionFailOnLoad"></a>DNSServerOptionFailOnLoad  
 Especifica que o carregamento de uma zona deve falhar quando são encontrados dados incorretos.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|    
|**VERDADEIRO**|Ativar a falha no carregamento|  
|**FALSO**|Desativar a falha no carregamento|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DNSServerOptionFailOnLoad=TRUE`|  

####  <a name="DNSServerOptionNameCheckFlag"></a>DNSServerOptionNameCheckFlag  
 Especifica o padrão de caráter é utilizado quando a verificação de nomes DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**0**|Utiliza os caracteres de ANSI que estão em conformidade com a Internet Engineering Task Force (IETF) pedido para comentários (RFCs). Este valor corresponde do **RFC Strict (ANSI)** seleção quando configurar o DNS no Deployment Workbench.|  
|**1**|Caracteres de ANSI utiliza que não cumpram necessariamente IETF RFCs. Este valor corresponde do **não RFC (ANSI)** seleção quando configurar o DNS no Deployment Workbench.|  
|**2**|Utiliza múltiplos bytes carateres de USC transformação formato 8 (UTF-8). Esta é a predefinição. Este valor corresponde do **Multibyte (UTF-8)** seleção quando configurar o DNS no Deployment Workbench.|  
|**3**|Utiliza todos os carateres. Este valor corresponde do **todos os nomes de** seleção quando configurar o DNS no Deployment Workbench.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSServerOptionNameCheckFlag=2`|  

####  <a name="DNSZones"></a>DNSZones  
 Especifica o número de zonas DNS para configurar.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*zonas*|Especifica o número de zonas DNS para configurar|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSZones=1 DNSZones0Name=MyNewZone DNSZones0DirectoryPartition=Forest DNSZones0FileName=MyNewZone.dns DNSZones0MasterIP=192.168.0.1,192.168.0.2 DNSZones0Type=Secondary`|  

####  <a name="DNSZonesxDirectoryPartition"></a>DNSZonesxDirectoryPartition  
 Especifica a partição de diretório no qual pretende armazenar a zona quando configurar secundário ou zonas de stub.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**Domínio**|Replica os dados de zona para todos os servidor DNS no domínio do AD DS|  
|**Floresta**|Replica os dados de zona para todos os servidor DNS na floresta do AD DS|  
|**Legado**|Replica os dados de zona para todos os controladores de domínio no domínio do AD DS|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DNSZones0DirectoryPartition=Forest`|  

####  <a name="DNSZonesxFileName"></a>DNSZonesxFileName  
 Especifica o nome do ficheiro que irá armazenar as informações de zona.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*file_name*|Especifica o nome do ficheiro que irá armazenar as informações de zona|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DNSZones0FileName=MyNewZone.dns`|  

####  <a name="DNSZonesxMasterIP"></a>DNSZonesxMasterIP  
 Lista de endereços IP dos servidores mestres para ser utilizado pelo servidor DNS, ao atualizar as zonas secundárias especificadas delimitada por vírgulas. Esta propriedade tem de ser especificado quando configurar uma secundária ou stub zona DNS.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*IP1, IP2*|Uma lista delimitada por vírgulas de endereços IP dos servidores mestres|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DNSZones0MasterIP=192.168.0.1,192.168.0.2`|  

####  <a name="DNSZonesxName"></a>DNSZonesxName  
 Especifica o nome da zona.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Especifica o nome da zona|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSZones0Name=MyNewZone`|  

####  <a name="DNSZonesxScavenge"></a>DNSZonesxScavenge  
 Configura o servidor DNS principal para "scavenge" registos obsoletos — ou seja, para procurar a base de dados para os registos que tem desatualizados e eliminá-los.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permitir que os registos DNS obsoletos para ser scavenged.|  
|**FALSO**|Não permitir que os registos DNS obsoletos para ser scavenged.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSZones0Scavenge=TRUE`|  

#### <a name="dnszonesxtype"></a>DNSZonesxType  
 Especifica o tipo de zona para criar.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**DSPrimary**|Cria uma zona principal e especificar se devem ser armazenado no AD DS num servidor DNS configurado como um controlador de domínio|  
|**DSStub**|Cria uma zona de stub e especificar se devem ser armazenado no AD DS num servidor DNS configurado como um controlador de domínio|  
|**Primário**|Cria uma zona principal|  
|**Secundário**|Cria uma zona secundária|  
|**Stub**|Cria uma zona de stub|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DNSZones0Type=Secondary`|  

####  <a name="DNSZonesxUpdate"></a>DNSZonesxUpdate  
 Configura o servidor DNS primário para efetuar atualizações dinâmicas.  

> [!NOTE]
>  O *x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de DNS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|**0**|Não permite atualizações dinâmicas|  
|**1**|Permite que as atualizações dinâmicas|  
|**2**|Permite atualizações dinâmicas seguras|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DNSZones0Update=1`|  

####  <a name="DoCapture"></a>DoCapture  
 Indicador de se é uma imagem do computador de destino para serem capturadas. Se estiver, o Sysprep for executado no computador de destino para preparar a criação da imagem. Depois de executa o Sysprep, uma nova imagem WIM é criada e armazenada na pasta dentro da pasta partilhada designada para cópias de segurança de computador de destino (**BackupDir** e **BackupShare**, respetivamente).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Copie os ficheiros necessários para executar o Sysprep no computador de destino, execute o Sysprep no computador de destino e capturar uma imagem WIM.|  
|**NÃO**|Não executar o Sysprep no computador de destino e não capturar uma imagem WIM.|  
|**PREPARAR**|Copie os ficheiros necessários para executar o Sysprep no computador de destino, mas não a executar o Sysprep ou outros processos de captura de imagem.|  
|**SYSPREP**|Copie os ficheiros necessários para executar o Sysprep no computador de destino, execute o Sysprep no computador de destino, mas não capturar uma imagem WIM.<br /><br /> Nota:<br /><br /> É o objetivo principal deste valor permitir a criação de um VHD que contém um sistema operativo depois de executar o Sysprep e não captura de imagem é necessária.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DoCapture=YES DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|  

####  <a name="DomainAdmin"></a>DomainAdmin  
 As credenciais da conta de utilizador utilizadas para associar o computador de destino para o domínio especificado no **JoinDomain**. Especificar como *UserName*.  

> [!NOTE]
>  Para ZTI, são utilizadas as credenciais que o Configuration Manager Especifica normalmente. Se o **DomainAdmin** propriedade for especificada, as credenciais no **DomainAdmin** propriedade substituir as credenciais que especifica o Configuration Manager.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*domain_admin*|O nome das credenciais de conta do utilizador|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|  

####  <a name="DomainAdminDomain"></a>DomainAdminDomain  
 O domínio em que as credenciais do utilizador especificado no **DomainAdmin** residem.  

> [!NOTE]
>  Para ZTI, são utilizadas as credenciais que o Configuration Manager Especifica normalmente. Se o **DomainAdmin** propriedade for especificada, as credenciais no **DomainAdmin** propriedade substituir as credenciais que especifica o Configuration Manager.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*domain_admin_domain*|O nome do domínio onde residem as credenciais da conta de utilizador|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|  

####  <a name="DomainAdminPassword"></a>DomainAdminPassword  
 A palavra-passe utilizada para a conta de administrador especificada no domínio a **DomainAdmin** propriedade para associar o computador ao domínio.  

> [!NOTE]
>  Para ZTI, são utilizadas as credenciais que o Configuration Manager Especifica normalmente. Se o **DomainAdmin** propriedade for especificada, as credenciais no **DomainAdmin** propriedade substituir as credenciais que especifica o Configuration Manager.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*domain_admin_password*|A palavra-passe para o domínio de conta de administrador no computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|  

####  <a name="DomainLevel"></a>DomainLevel  
 Esta entrada especifica o nível funcional do domínio. Esta entrada é baseada nos níveis de que existe na floresta quando é criado um novo domínio numa floresta existente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*Nível*|Define o nível funcional do domínio para um dos seguintes:<br /><br /> -2, Windows Server 2003<br /><br /> -3, Windows Server 2008<br /><br /> -4, Windows Server 2008 R2<br /><br /> -5, Windows Server 2012|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DomainLevel=3`|  

####  <a name="DomainNetBiosName"></a>DomainNetBiosName  
 Atribui um nome NetBIOS para o novo domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Nome*|Atribui um nome NetBIOS para o novo domínio|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DomainNetBiosName=NewDom`|  

####  <a name="DomainOUs"></a>DomainOUs  
 Uma lista de unidades de organizacionais de AD DS (UOs) em que a conta de computador de destino pode ser criada. O **DomainOUs** propriedade apresenta uma lista de valores de texto que podem ser qualquer valor não vazio. O **DomainOUs** propriedade tem um sufixo numérico (por exemplo, **DomainOUs1** ou **DomainOUs2**). Os valores especificados por DomainOUs será apresentado no Assistente de implementação e selecionáveis pelo utilizador. O **MachineObjectOU** propriedade, em seguida, será definida para a UO selecionada.  

 Além disso, a mesma funcionalidade pode ser fornecida ao configurar o ficheiro DomainOUList.xml. O formato do ficheiro DomainOUList.xml é o seguinte:  

```  
<?xml version="1.0" encoding="utf-8"?>  
<DomainOUs>  
<DomainOU>  
  OU=Computers,OU=Tellers,OU=NYC,DC=WOODGROVEBANK,DC=Com  
</DomainOU>  
<DomainOU>  
  OU=Computers,OU=Managers,OU=NYC,DC=WOODGROVEBANK,DC=Com  
</DomainOU>  
</DomainOUs>  
```  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*UO*|A UO na qual é possível criar a conta de computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=Y DomainOUs1=OU=Computers, OU=Tellers, OU=NYC, DC=WOODGROVEBANK, DC=Com DomainOUs2=OU=Computers, OU=Managers, OU=NYC, DC=WOODGROVEBANK, DC=Com`|  

####  <a name="DoNotCreateExtraPartition"></a>DoNotCreateExtraPartition  
 Especifica que as implementações do Windows 7 e Windows Server 2008 R2 não irão criar a partição do sistema de 300 MB.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**SIM**|Não será possível criar a partição de sistema adicionais.|  
|**NÃO**|Será criada a partição de sistema adicionais.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] OSInstall=Y DoNotCreateExtraPartition=YES`|  

> [!NOTE]
>  Não utilize esta propriedade em conjunto com as propriedades para configurar as definições do BitLocker.  

####  <a name="DoNotFormatAndPartition"></a>DoNotFormatAndPartition  
 Esta propriedade é utilizada para configurar se o MDT efetua qualquer os passos de sequência de tarefas de formatação e criação de partições nas sequências de tarefas criadas utilizando os modelos de sequência de tarefas do MDT.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**SIM**|A criação de partições e de uma sequência de tarefas do MDT passos de sequência de tarefas de formatação serão executados.|  
|*Qualquer outro valor*|Não serão possível efetuar a criação de partições e de uma sequência de tarefas do MDT passos de sequência de tarefas de formatação. Este é o valor predefinido.|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES SkipUserData=YES USMTOfflineMigration=TRUE DoNotFormatAndPartition=YES OSDStateStorePath=\\WDG-MDT-01\StateStore$`|  

####  <a name="DriverGroup"></a>DriverGroup  
 Uma lista de valores de texto que associa os controladores de out-of-box criados no Deployment Workbench entre si (normalmente, baseado na marca e modelo de um computador). Um controlador pode estar associado um ou mais grupos de controlador. O **DriverGroup** propriedade permite que os controladores dentro de um ou mais grupos para ser implementada para um computador de destino.  

 Os valores de texto numa lista podem ser qualquer valor não vazio. O **DriverGroup** valor da propriedade tem um sufixo numérico (por exemplo, **DriverGroup001** ou **DriverGroup002**). Depois de se encontra definida, um grupo de controladores está associado um computador. Um computador pode estar associado a mais do que um grupo de controladores.  

 Por exemplo, existem duas secções para cada um dos fabricantes [Mfgr01] e [Mfgr02]. Dois grupos de controlador estão definidos para o fabricante Mfgr01: Controladores de vídeo Mfgr01 e Mfgr01 os controladores de rede. Para o fabricante Mfgr02, está definido um grupo de controladores, controladores de Mfgr02. Um grupo de controladores, controladores partilhados, é aplicado a todos os computadores encontrados na secção [predefinido].  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*driver_group_name*|O nome do grupo controladores definido no Deployment Workbench|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Make, Default  [Default] DriverGroup001=Shared Drivers :: [Mfgr01] DriverGroup001=Mfgr01 Video Drivers DriverGroup002=Mfgr01 Network Drivers  [Mfgr02] DriverGroup001=Mfgr02 Drivers`|  

####  <a name="DriverInjectionMode"></a>DriverInjectionMode  
 Esta propriedade é utilizada para controlar os controladores de dispositivo são injetados pelo [inserir controladores](#InjectDrivers) passo de sequência de tarefas.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|Automática|Inserir apenas controladores correspondentes do perfil de seleção ou pasta.  Este é o mesmo comportamento de MDT 2008, que injects todos os controladores correspondentes um do plug and play (PnP) de identificadores (IDs) no computador de destino.|  
|Todas|Inserir todos os controladores no perfil de seleção de ou pasta.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] DriverInjectionMode=ALL DriverSelectionProfile=Nothing DriverPaths001=\\NYC-AM-FIL-01\Drivers$ DriverPaths002=\\NYC-AM-FIL-03\WinDrvs`|  

####  <a name="DriverPaths"></a>DriverPaths  
 Uma lista de caminhos UNC para pastas partilhadas onde estão localizados os controladores de dispositivo adicionais. Estes controladores de dispositivo são instalados com o sistema operativo de destino no computador de destino. Os scripts de MDT copie o conteúdo destas pastas para a pasta de C:\Drivers no computador de destino. O **DriverPaths** propriedade é uma lista de valores de texto que pode ser qualquer valor não vazio. O **DriverPaths** propriedade tem um sufixo numérico (por exemplo, **DriverPaths001** ou **DriverPaths002**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*UNC_path*|Caminho UNC para a pasta partilhada na qual residem os controladores adicionais|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] DriverPaths001=\\NYC-AM-FIL-01\Drivers$ DriverPaths002=\\NYC-AM-FIL-03\Win8Drvs`|  

####  <a name="DriverSelectionProfile"></a>DriverSelectionProfile  
 Nome de perfil utilizado durante a instalação de controlador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*profile_name*|Nenhum|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DriverSelectionProfile=MonitorDrivers`|  

####  <a name="EventService"></a>EventService  
 O **EventService** propriedade especifica o URL onde o MDT monitorização do serviço está em execução. Por predefinição, o serviço utiliza a porta TCP 9800 comunicar. O MDT serviço de monitorização recolhe informações de implementação do processo de implementação que pode ser visualizado no Deployment Workbench e utilizando o [Get-MDTMonitorData](#Get-MDTMonitorData) cmdlet.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*url_path*|O URL para o MDT serviço de monitorização.|  

|**Exemplo**|  
|-|   
|`[Settings] Priority=Default  [Default] EventService=http://WDG-MDT-01:9800 DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$`|  

####  <a name="EventShare"></a>EventShare  
 O **EventShare** propriedade aponta para uma pasta partilhada no qual o MDT scripts eventos de registo.  

 Por predefinição, é criada na pasta partilhada no C:\Events.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*UNC_path*|O caminho UNC para a pasta partilhada no qual o MDT scripts eventos de registo. O nome da partilha predefinido é de eventos.|  

|**Exemplo**|  
|-|
|`[Settings] Priority=Default  [Default] EventShare=\\NYC-AM-FIL-01\Events DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$`|  

####  <a name="FinishAction"></a>FinishAction  
 Especifica a ação a executar quando uma sequência de tarefas LTI concluído, que é depois do **resumo** página do assistente no Assistente de implementação.  

> [!TIP]
>  Utilize esta propriedade em conjunto com o **SkipFinalSummary** propriedade para ignorar o **resumo** página do assistente no Assistente de implementação e automaticamente executar a ação.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|*ação*|Onde *ação* é um dos seguintes:<br /><br /> - **ENCERRAMENTO**. Encerramento do computador de destino.<br /><br /> - **REINICIAR**. Reinicia o computador de destino.<br /><br /> - **REINICIAR**. Igual ao **REINICIAR**.<br /><br /> - **TERMINAR SESSÃO**. Terminar a sessão do utilizador atual. Se o computador de destino está atualmente em execução do Windows PE, em seguida, o computador de destino será reiniciado.<br /><br /> - **em branco**. Sair do Assistente de implementação sem efetuar qualquer ação adicional. Esta é a predefinição.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] FinishAction=REBOOT`|  

####  <a name="ForceApplyFallback"></a>ForceApplyFallback  
 Controla o método utilizado para o Windows instalado:  

-   **Setup.exe**. Este método é o método tradicional, iniciado ao executar o setup.exe do suporte de dados de instalação. MDT utiliza este método, por predefinição.  

-   ImageX.exe. Este método instala a imagem do sistema operativo utilizando imagex.exe com o **/ aplicar** opção. MDT utiliza este método quando não é possível utilizar o método setup.exe (ou seja, MDT utilizará imagex.exe).  

 Para além de controlar o método utilizado para instalar estes sistemas operativos, esta propriedade afeta as sequências de tarefas do sistema operativo estão listadas no Assistente de implementação para uma imagem de arranque de arquitetura de processador específico. Quando o valor desta propriedade está definido como **nunca**, apenas a sequências que correspondem à arquitetura do processador da imagem de arranque são apresentadas de tarefa do sistema de operativo. Se o valor desta propriedade é definido como qualquer outro valor ou está em branco, todas as sequências de tarefas que podem utilizar o método de instalação imagex.exe são apresentadas, independentemente da arquitetura do processador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**NUNCA**|MDT utiliza sempre o método imagex.exe, se necessário. Apenas as sequências de tarefas implementar um sistema operativo que corresponde a imagem de arranque são apresentadas no Assistente de implementação.|  
|Qualquer outro valor, incluindo em branco| Qualquer sequência de tarefas que suporta o método imagex.exe é apresentada no Assistente de implementação.|  


|**Exemplo**|
 |-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ForceApplyFallback=NEVER`|  

####  <a name="ForestLevel"></a>ForestLevel  
 Esta entrada especifica o nível funcional da floresta quando é criado um novo domínio numa floresta nova.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*nível*|Define o nível funcional do domínio para um dos seguintes:<br /><br /> -2, Windows Server 2003<br /><br /> -3, Windows Server 2008<br /><br /> -4, Windows Server 2008 R2<br /><br /> -5, Windows Server 2012|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ForestLevel=3`|  

####  <a name="FullName"></a>FullName  
 O nome completo do utilizador do computador de destino fornecido durante a instalação do sistema operativo. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

> [!NOTE]
>  Este valor é diferente do que as credenciais de utilizador criadas após o sistema operativo é implementado. O **FullName** propriedade é fornecida como informações aos administradores de sistemas sobre o utilizador as aplicações em execução no computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*full_name*|O nome completo do utilizador do computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] CustomProperty=TRUE OrgName=Woodgrove Bank  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom FullName=Woodgrove Bank User  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP  ApplicationInstall=Minimum FullName=Woodgrove Bank Manager`|  

####  <a name="GPOPackPath"></a>GPOPackPath  
 Esta propriedade é utilizada para substituir o caminho predefinido para a pasta na qual residem os pacotes de GPO. O caminho especificado nesta propriedade é relativo à pasta de Templates\GPOPacks numa partilha de distribuição. MDT efetua análises automáticas a uma subpasta específica desta pasta com base no sistema operativo que está a ser implementado no computador de destino, como Templates\GPOPacks\\*operating_system* (onde *operating_ sistema* é o sistema operativo que está a ser implementada). Tabela 3 lista os sistemas operativos suportados e as subpastas que correspondem a cada sistema operativo.  

##### <a name="table-3-windows-operating-systems-and-corresponding-gpo-pack-subfolder"></a>Tabela 3. Sistemas operativos Windows e subpasta correspondente do pacote de GPO  

|**Sistema operativo**|**Subpasta do pacote de GPO**|  
|-|-|  
|Windows 7 com SP1|Win7SP1 MDTGPOPack|  
|Windows Server 2008 R2|WS2008R2SP1 MDTGPOPack|  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*caminho*|O caminho relativa a *distribution_share*\Templates\GPOPacks pasta (onde *distribution_share* é a pasta raiz da partilha de distribuição. O valor predefinido é o *distribution_share*\Templates\GPOPacks\\*operating_system* pasta (onde *operating_system* uma subpasta baseia-se no a versão de sistema operativo).<br /><br /> No exemplo abaixo, definir a propriedade GPOPackPath como um valor de "Win7 HighSecurity" configura o MDT para utilizar o *distribution_share*\Templates\GPOPacks\Win7-HighSecurity pasta como a pasta onde estão armazenados os pacotes de GPO.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] GPOPackPath=Win7-HighSecurity`|  

####  <a name="Groups"></a>Grupos  
 A lista de grupos locais no computador de destino que irá ser capturada cuja associação de grupo. Esta associação de grupo é capturada durante a fase de captura de estado e é restaurada durante a fase de restauro de estado. (Os grupos predefinidos são os administradores e utilizadores avançados.) O **grupos** propriedade é uma lista de valores de texto que pode ser qualquer valor não vazio. O **grupos** propriedade tem um sufixo numérico (por exemplo, **Groups001** ou **Groups002**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*group_name*|O nome do grupo local no computador de destino para o qual o grupo será possível capturar a associação|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ CaptureGroups=YES Groups001=NYC Application Management Groups002=NYC Help Desk Users`|  

####  <a name="HideShell"></a>HideShell  
 Esta propriedade controla o ecrã do Explorador do Windows, enquanto a sequência de tarefas LTI está em execução no novo sistema operativo no computador de destino. Esta propriedade pode ser utilizada em conjunto com o **DisableTaskMgr** propriedade.  

> [!NOTE]
>  Esta propriedade pode ser utilizada com o **DisableTaskMgr** propriedade para o ajudar a impedir que os utilizadores interromper a sequência de tarefas LTI. Para obter mais informações, consulte o [DisableTaskMgr](#DisableTaskMgr) propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|  
|**SIM**|Explorador do Windows está oculto até que a sequência de tarefas esteja concluída.|  
|**NÃO**|Explorador do Windows está visível enquanto a sequência de tarefas está em execução. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DisableTaskMgr=YES HideShell=YES`|  

####  <a name="OSHome_Page"></a>OSHome_Page  
 O URL a utilizar como a home page Windows Internet Explorer® após a implementação do sistema operativo de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*URL*|O URL da página web para ser utilizado como a home page do Internet Explorer no computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] Home_Page=http://portal.woodgrovebank.com`|  

####  <a name="HostName"></a>Nome de anfitrião  
 O nome de anfitrião IP do computador de destino (o nome atribuído ao computador de destino).  

> [!NOTE]
>  Este é o nome do computador de destino, não o nome de computador NetBIOS do computador de destino. O nome NetBIOS do computador pode ser mais curto do que o nome do computador. Além disso, esta propriedade está dinamicamente definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*host_name*|O nome de anfitrião IP atribuído ao computador de destino|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="ImagePackageID"></a>ImagePackageID  
 O ID de pacote utilizado para o sistema operativo para instalar durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|
|-|-|  
|Nenhum|O ID de pacote utilizado para o sistema operativo para instalar durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="InputLocale"></a>InputLocale  
 Uma lista de regiões de entrada para ser utilizado com o sistema operativo de destino. Pode ser especificado mais do que uma região de entrada para o sistema operativo de destino. Cada região tem de ser separado por ponto e vírgula (;). Se não for especificado, o Assistente de implementação utiliza a região de entrada configurada a imagem a ser implementado.  

 Exclua esta definição no Windows utilizador State Migration Tool (USMT) quando a cópia de segurança e restaurar informações de estado do utilizador. Caso contrário, as definições nas informações de estado de utilizador irão substituir os valores especificados no *InputLocale* propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|  
|*input_locale1; input_locale2*|A região do teclado ligado ao computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us InputLocale=0409:00000409;0413:00020409;0413:00000409;0409:00020409`|  

####  <a name="InstallPackageID"></a>InstallPackageID  
 O ID de pacote utilizado para o sistema operativo para instalar durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|O ID de pacote utilizado para o sistema operativo para instalar durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="Instance"></a>Instância  
 A instância do SQL Server utilizada para consultar os valores de propriedade de colunas na tabela especificada no **tabela** propriedade. A base de dados reside num computador especificado no **SQLServer** propriedade. A instância do SQL Server no computador especificada no **instância** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
||*instância*|O nome da instância do SQL Server para ser utilizado para consultar os valores de propriedade|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="IPAddress"></a>IPAddress  
 O endereço IP do computador de destino. O formato do endereço IP devolvido pela propriedade é padrão decimal separada por pontos notação; Por exemplo, 192.168.1.1. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um computador de destino específicos com base no endereço IP.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*IP\_endereço*|O endereço IP do computador de destino na norma separada por pontos\-notação decimal|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsDesktop"></a>IsDesktop  
 Indicador de indica se o computador é um ambiente de trabalho, porque o **Win32\_SystemEnclosure ChassisType** valor da propriedade é **3**, **4**, **5** , **6**, **7**, ou **15**.  

> [!NOTE]
>  Será verdadeira apenas uma das seguintes propriedades de cada vez: **IsDesktop**, **IsLaptop**, **IsServer**.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O computador de destino é um computador de secretária.|  
|**FALSO**|O computador de destino não é um computador de secretária.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsHypervisorRunning"></a>IsHypervisorRunning  
 Especifica se o hipervisor está presente no computador de destino. Esta propriedade for definida utilizando informações a partir de **CPUID** interface.  

 Para obter as informações recolhidas sobre as VMs e informações devolvidos pelo **CPUID** interface, consulte as seguintes propriedades:  

-   **IsVM**  

-   **SupportsHyperVRole**  

-   **SupportsNX**  

-   **SupportsVT**  

-   **Supports64Bit**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

> [!NOTE]
>  A propriedade IsVM deve ser utilizada para determinar se o computador de destino é uma máquina virtual ou física.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Foi detetado um hipervisor.|  
|**FALSO**|Não foi detetado um hipervisor.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsLaptop"></a>IsLaptop  
 Indicador de indica se o computador é um computador portátil, porque o **Win32\_SystemEnclosure ChassisType** valor da propriedade é **8**, **10**, **12**, **14**, **18**, ou **21**.  

> [!NOTE]
>  Será verdadeira apenas uma das seguintes propriedades de cada vez: **IsDesktop**, **IsLaptop**, **IsServer**.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O computador de destino é um computador portátil.|  
|**FALSO**|O computador de destino não é um computador portátil.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsServer"></a>IsServer  
 Indicador de indica se o computador é um servidor, porque o **Win32\_SystemEnclosure ChassisType** valor da propriedade é **23**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O computador de destino é um servidor.|  
|**FALSO**|O computador de destino não é um servidor.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsServerCoreOS"></a>IsServerCoreOS  
 Indicador de se o sistema operativo atual em execução no computador de destino é a opção de instalação Server Core do sistema operativo Windows Server.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O sistema operativo no computador de destino é a opção de instalação Server Core do Windows Server.|  
|**FALSO**|O sistema operativo no computador de destino não é a opção de instalação Server Core do Windows Server.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsServerOS"></a>IsServerOS  
 Indicador de se o sistema operativo atual em execução no computador de destino é um sistema operativo do servidor.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O sistema operativo no computador de destino é um sistema operativo do servidor.|  
|**FALSO**|O sistema operativo no computador de destino não é um sistema operativo do servidor.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsUEFI"></a>IsUEFI  
 Especifica se o computador de destino está atualmente em execução com a Interface de Firmware extensível Unified \(UEFI\). O UEFI é uma especificação que define uma interface de software entre um sistema operativo e o firmware da plataforma. UEFI é uma substituição mais segura para a interface de firmware de BIOS mais antiga presente em alguns computadores pessoais. Para obter mais informações sobre a UEFI, aceda a [http:\/\/www.uefi.org](http://www.uefi.org).  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O computador de destino está atualmente em execução com UEFI.|  
|**FALSO**|O computador de destino não está atualmente em execução com UEFI.<br /><br /> Nota:<br /><br /> É possível que o computador de destino pode suportar UEFI, mas está em execução no modo de compatibilidade que emula a interface de firmware de BIOS mais antiga. Nesta situação, este valor desta propriedade será definido como **falso** , apesar do computador de destino suportar UEFI.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="IsVM"></a>IsVM  
 Especifica se o computador de destino é uma VM com base nas informações recolhidas a partir de **CPUID** interface. Pode determinar o específico VM ambiente utilizando o **VMPlatform** propriedade.  

 Para obter as informações recolhidas sobre as VMs e informações devolvidos pelo **CPUID** interface, consulte as seguintes propriedades:  

-   **IsHypervisorRunning**  

-   **SupportsHyperVRole**  

-   **SupportsNX**  

-   **SupportsVT**  

-   **Supports64Bit**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O computador de destino é uma VM.|  
|**FALSO**|O computador de destino não é uma VM.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="JoinDomain"></a>JoinDomain  
 O domínio que o computador de destino é associado depois do sistema operativo de destino é implementado. Este é o domínio onde será criada a conta de computador para o computador de destino. O **JoinDomain** propriedade pode conter carateres alfanuméricos, hífenes \( \- \)e carateres de sublinhado \( \_ \). O **JoinDomain** propriedade não pode estar em branco ou conter espaços.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*domínio\_nome*|O nome do domínio que o computador de destino é associado|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] JoinDomain=WOODGROVEBANK MachineObjectOU=OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`|  

####  <a name="JoinWorkgroup"></a>JoinWorkgroup  
 O grupo de trabalho que o computador de destino é associado depois do sistema operativo de destino é implementado. O **JoinWorkgroup** propriedade pode conter carateres alfanuméricos, hífenes \( \- \)e carateres de sublinhado \( \_ \). O **JoinWorkgroup** propriedade não pode estar em branco ou conter espaços.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*grupo de trabalho\_nome*|O nome do grupo de trabalho que associa o computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] JoinWorkgroup=WDGV_WORKGROUP`|  

####  <a name="KeyboardLocale"></a>KeyboardLocale  
 Uma lista de regiões de teclado para ser utilizado com o sistema operativo de destino. Pode ser especificado mais do que uma região de teclado para o sistema operativo de destino. Cada região têm de ser separado por ponto e vírgula \(;\). Se não for especificado, o Assistente de implementação utiliza a região de teclado configurada na imagem a ser implementada.  

 Exclua esta definição no USMT quando a cópia de segurança e restaurar informações de estado do utilizador. Caso contrário, as definições nas informações de estado de utilizador irão substituir os valores especificados no **KeyboardLocale** propriedade.  

> [!NOTE]
>  Para esta propriedade funcione corretamente, tem de ser configurado no CustomSettings.ini e BootStrap.ini. BootStrap.ini é processada antes de uma partilha de implementação (que contém CustomSettings.ini) tiver sido selecionada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*keyboard_locale1; keyboard_locale2*|A região de teclado ligado ao computador de destino.<br /><br /> O valor pode ser especificado nos seguintes formatos:<br /><br /> -Texto (en-us)<br /><br /> -Hexadecimal (0409:00000409)|  

|**Exemplo 1**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=en-us`|  

|**Exemplo 2**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=0409:00000409;1809:00001809;041A:0000041A;083b:0001083b`|  

####  <a name="KeyboardLocalePE"></a>KeyboardLocalePE  
 O nome do idioma a ser utilizado no Windows PE apenas teclado.  

> [!NOTE]
>  Para esta propriedade funcione corretamente, tem de ser configurado no CustomSettings.ini e BootStrap.ini. BootStrap.ini é processada antes de uma partilha de implementação (que contém CustomSettings.ini) tiver sido selecionada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*keyboard_locale*|A região de teclado ligado ao computador de destino.<br /><br /> O valor pode ser especificado nos seguintes formatos:<br /><br /> -Texto (en-us)<br /><br /> -Hexadecimal (0409:00000409)|  

|**Exemplo 1**|  
|-|  
|`[Settings] Priority=Default  [Default] KeyboardLocalePE=en-us`|  

|**Exemplo 2**|  
|-|  
|`[Settings] Priority=Default  [Default] KeyboardLocalePE=0409:00000409`|  

####  <a name="LanguagePacks"></a>LanguagePacks  
 Uma lista de GUIDs para os pacotes de idiomas para implementação no computador de destino. Deployment Workbench Especifica estes pacotes de idiomas no nó de pacotes de SO. Estes GUIDs são armazenadas no ficheiro Packages.xml. O **LanguagePacks** propriedade tem um sufixo numérico (por exemplo, **LanguagePacks001** ou **LanguagePacks002**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*language_pack_guid*|O GUID que especifica o Deployment Workbench para os pacotes de idiomas instalar no computador de destino. O GUID correspondente ao GUID armazenado no Packages.xml o pacote de idiomas.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] LanguagePacks001={a1923f8d-b07b-44c7-ac1e-353b7cc4c1ad}`|  

####  <a name="LoadStateArgs"></a>LoadStateArgs  
 Os argumentos transmitidos para o processo de Loadstate da USMT. O script ZTI insere o registo adequado, progresso e os parâmetros do arquivo de estado. Se este valor não está incluído no ficheiro de definições, o processo de restauro do Estado de utilizador é ignorado.  

 Se o processo de Loadstate for concluído com êxito, as informações de estado do utilizador são eliminadas. Em caso de uma falha de Loadstate (ou código de retorno de diferente de zero), o armazenamento de Estados local é movido para %WINDIR%\StateStore para evitar a eliminação e para garantir que não existem informações de estado do utilizador são perdidas.  

> [!NOTE]
>  Não adicione qualquer um dos seguintes argumentos da linha de comandos quando configurar esta propriedade: **/hardlink**, **/nocompress**, **/desencriptar**, **/key**, ou **/keyfile**. Os scripts de MDT irão adicionar estes argumentos da linha de comandos, se aplicável para o cenário de implementação atual.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|Argumentos|Os argumentos da linha de comandos transmitida para Loadstate.exe.<br /><br /> Os argumentos predefinido, especificados pelo Deployment Workbench são os seguintes:<br /><br /> - **/v**. Permite uma saída verbosa no registo de Loadstate. A predefinição é **0**. Especifica qualquer número entre 0 e 15. O valor **5** permite verboso e saída de estado.<br /><br /> - **/c**. Quando especificado, Loadstate irá continuar a executar, mesmo se não existirem erros nonfatal. Sem o **/c** opção, Loadstate sai no primeiro erro.<br /><br /> - **/LAC**. Especifica que o se a conta que está a ser migrada é uma conta local (sem domínio) e não existe no computador de destino, em seguida, USMT irá criar a conta, mas será desativada.<br /><br /> Para obter mais informações sobre estas e outros argumentos, consulte os ficheiros de ajuda do USMT.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|  

####  <a name="Location"></a>Localização  
 A localização geográfica dos computadores de destino. Define uma lista de endereços IP que correspondem aos gateways predefinidos definidos para os computadores dentro dessa localização o **localização** propriedade. Um endereço IP para um gateway predefinido pode ser associado a mais de uma localização.  

 Normalmente, o valor para o **localização** for definida, efetuando uma consulta de base de dados na base de dados gerido através do Deployment Workbench. Deployment Workbench pode ajudar a criar as localizações, definir as definições de propriedade associadas as localizações e, em seguida, na configuração CustomSettings.ini para executar a consulta de base de dados para a localização da propriedade e as definições de propriedade associados as localizações.  

 Por exemplo, um `LocationSettings` secção CustomSettings.ini pode consultar a vista de LocationSettings na base de dados para uma lista de localizações que contêm o valor especificado no **DefaultGateway** propriedade listada no  **Os parâmetros** propriedade. A consulta devolve todas as definições associadas a cada gateway predefinido.  

 Em seguida, os scripts de analisar cada secção que corresponde às localizações devolvidas na consulta. Por exemplo, o valor `[Springfield]`e a secção `[Springfield-123 Oak Street-4th Floor]` no CustomSettings.ini pode representar as localizações correspondentes. Este é um exemplo de como um computador podem pertencer a duas localizações. O `[Springfield]`secção destina-se todos os computadores numa área geográfica maior (uma cidade completa) e o `[Springfield-123 Oak Street-4th Floor]` secção destina-se todos os computadores o quarto piso em Rua de Oak 123, no Springfield.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*location1,*location2|A lista de localizações sejam atribuídos a um computador individual ou um grupo de computadores|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=LSettings, Default  [Default] UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES ScanStateArgs=/v:15 /o /c LoadStateArgs=/v:7 /c  [LSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL$ Table=LocationSettings Parameters=DefaultGateway  [Springfield] UDDir=%OSDComputerName% UDShare=\\Springfield-FIL-01\UserData  [Springfield-123 Oak Street-4th Floor] DeployRoot=\\Springfield-BDD-01\Distribution1$`|  

####  <a name="LongDistanceAccess"></a>LongDistanceAccess  
 Os dígitos de marcação para obter acesso a uma linha externa para marcar longa distance. A propriedade pode conter apenas dígitos numéricos. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*language_pack_guid*|O GUID que especifica o Deployment Workbench para os pacotes de idiomas instalar no computador de destino. O GUID correspondente ao GUID armazenado no Packages.xml o pacote de idiomas.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|  

####  <a name="MACAddress"></a>MACAddress  
 O suporte de dados de acesso (endereço MAC control) camada do adaptador de rede principal do computador de destino. O **MACAddress** propriedade está incluída no **prioridade** linha para que podem ser fornecidos valores de propriedade específicos para um computador de destino. Criar uma secção para cada endereço MAC para cada um dos computadores de destino (tais como `[00:0F:20:35:DE:AC]`ou `[00:03:FF:FE:FF:FF]`) que contêm definições de – específicas do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*mac_address*|O endereço MAC do computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=MACAddress, Default  [Default] CaptureGroups=YES Groups1=NYC Application Management Groups2=NYC Help Desk Users  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP`|  

####  <a name="MachineObjectOU"></a>MachineObjectOU  
 AD DS UO no domínio de destino em que uma conta de computador para o computador de destino é criado.  

> [!NOTE]
>  A UO especificada nesta propriedade tem de existir antes de implementar o sistema operativo de destino.  

> [!NOTE]
>  Se já existir um objeto de computador no AD DS, especificando **MachineObjectOU** não fará com que o objeto de computador sejam movidas para a UO especificada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*UO\_nome*|O nome da UO onde será criada a conta de computador para o computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] JoinDomain=WOODGROVEBANK MachineObjectOU=OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`|  

####  <a name="Make"></a>Certifique-  
 O fabricante do computador de destino. O formato para **tornar** não está definido. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um fabricante de computadores específico \(mais frequentemente em conjunto com o **modelo** e **produto** propriedades\).  

> [!NOTE]
>  Esta propriedade dinamicamente é definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*Certifique-*|Fabricante do computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Make, Default  [Default]  [Dell Computer Corporation] Subsection=Dell-%Model%  [Dell-Latitude D600] Packages001=XXX00009:Program9 Packages002=XXX0000A:Program10`|  

####  <a name="MandatoryApplications"></a>MandatoryApplications  
 Uma lista de GUIDs de aplicação que será instalado no computador de destino. Estas aplicações estão especificadas no nó de aplicações no Deployment Workbench. Os GUIDs são armazenados no ficheiro Applications.xml. O **MandatoryApplications** propriedade é uma lista de valores de texto que pode ser qualquer não\-em branco valor. O **MandatoryApplications** propriedade tem um sufixo numérico \(por exemplo, **MandatoryApplications001** ou **MandatoryApplications002** \).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*aplicação\_guid*|O GUID especificado pelo Deployment Workbench para a aplicação para ser implementado no computador de destino. O GUID corresponde à aplicação que GUID armazenado no ficheiro Applications.xml.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D} MandatoryApplications002={9d2b8999-5e4d-4f3d-bb05-edaaf4fe5628} Administrators001=WOODGROVEBANK\NYC Help Desk Staff`|  

####  <a name="Memory"></a>Memória  
 A quantidade de memória instalada no computador de destino em megabytes. Por exemplo, o valor **2038** indica 2,038 MB \(ou 2 GB\) de memória está instalado no computador de destino.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*memória*|A quantidade de memória instalada no computador de destino em megabytes|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="Model"></a>Modelo  
 O modelo do computador de destino. O formato para **modelo** não está definido. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um número de modelo do computador específico para um fabricante de computadores específico \(mais frequentemente em conjunto com o **tornar** e  **Produto** propriedades\).  

> [!NOTE]
>  Esta propriedade dinamicamente é definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*modelo*|O modelo do computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Make, Default  [Default]  [Dell Computer Corporation] Subsection=Dell-%Model%  [Dell-Latitude D600] Packages001=XXX00009:Program9 Packages002=XXX0000A:Program10`|  

####  <a name="NetLib"></a>NetLib  
 O protocolo a ser utilizado para comunicar com o computador a executar o SQL Server especificado no **SQLServer** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|\-||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**DBNMPNTW**|Utilize o protocolo de pipes nomeados para comunicar.|  
|**DBMSSOCN**|Utilizar TCP\/sockets IP para comunicar.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="NewDomain"></a>NewDomain  
 Indica o tipo de um novo domínio: se um novo domínio numa floresta nova, a raiz de uma nova árvore numa floresta existente ou um subordinado de um domínio existente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|Subordinado|O novo domínio é um subordinado de um domínio existente.|  
|Floresta|O novo domínio é o primeiro domínio numa floresta nova de árvores de domínio.|  
|árvore|O novo domínio é a raiz de uma nova árvore numa floresta existente.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] NewDomain=Tree`|  

####  <a name="NewDomainDNSName"></a>NewDomainDNSName  
 Especifica o nome necessário de uma nova árvore de num domínio existente ou quando o programa de configuração instala uma nova floresta de domínios.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Especifica o nome necessário de uma nova árvore de num domínio existente ou quando o programa de configuração instala uma nova floresta de domínios|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] NewDomainDNSName=newdom.WoodGroveBank.com`|  

####  <a name="Order"></a>Ordem  
 A ordenação para o conjunto numa consulta da base de dados de resultados. O conjunto de resultados é baseado nas definições de configuração do **base de dados**, **tabela**, **SQLServer**, **parâmetros**e **ParameterCondition** propriedades. Mais do que uma propriedade pode ser fornecida para ordenar os resultados por mais do que uma propriedade.  

 Por exemplo, se **ordem\=sequência** é especificado no ficheiro CustomSettings.ini, em seguida, um **ORDER BY** cláusula de sequência é adicionada à consulta. **Especificação de Order\=tornar**, **modelo** adiciona um **ordem ao tornam, modelo** cláusula à consulta.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|\-||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*property1, property2,...*|As propriedades a definir a sequência de ordenação para o conjunto de resultados \(onde *propertyn* representa as propriedades nos critérios de ordenação\)|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=MakeModelSettings Parameters=SerialNumber, AssetTag ParameterCondition=OR Order=Make, Model`|  

####  <a name="OrgName"></a>OrgName  
 O nome da organização que detém o computador de destino. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*org\_nome*|O nome da organização que detém o computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac UserDataLocation=NONE CustomProperty=TRUE OrgName=Woodgrove Bank  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom FullName=Woodgrove Bank User  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP  ApplicationInstall=Minimum FullName=Woodgrove Bank Manager`|  

####  <a name="OSArchitecture"></a>OSArchitecture  
 O tipo de arquitetura de processador para o sistema operativo de destino. Esta propriedade é referenciada durante implementações do OEM. Os valores válidos são **x86** e **x64**.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**x86**|O tipo de arquitetura de processador para o sistema operativo é de 32 bits.|  
|**x64**|O tipo de arquitetura de processador para o sistema operativo é 64 bits.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSCurrentBuild"></a>OSCurrentBuild  
 O número de compilação do sistema operativo em execução.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**7600**|Windows 7|  
|**9600**|Windows 8,1|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSCurrentVersion"></a>OSCurrentVersion  
 O número de versão do sistema operativo em execução.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*version_number*|A versão de sistema operativo principal, secundária versão e criar números (major). Por exemplo, 6.3.9600 representaria Windows 8.1.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDAdapterxDescription"></a>OSDAdapterxDescription  
 Especifica o nome da ligação de rede, como é apresentado no item de ligações de rede do painel de controlo. O nome pode ser entre 0 e 255 carateres de comprimento.  

 Esta propriedade destina-se apenas ao LTI. Para a propriedade equivalente para ZTI, consulte [OSDAdapterxName](#OSDAdapterxName).  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0Description** ou **OSDAdapter1Description**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|Descrição|O nome da ligação de rede conforme é apresentado no item de ligações de rede do painel de controlo|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDAdapterxDNSDomain"></a>OSDAdapterxDNSDomain  
 Especifica o nome de domínio DNS (sufixo DNS) que será atribuído à ligação de rede. Esta propriedade destina-se apenas ao ZTI. Para LTI, consulte o [OSDAdapterxDNSSuffix](#OSDAdapterxDNSSuffix) propriedade.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0DNSDomain** ou **OSDAdapter1DNSDomain**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*DNS_domain_name*|Um nome de domínio DNS (sufixo DNS) que será atribuído à ligação de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSDomain=WoodGroveBank.com`|  

####  <a name="OSDAdapterxDNSServerList"></a>OSDAdapterxDNSServerList  
 Esta é uma lista delimitada por vírgulas de endereços IP de servidor DNS que será atribuído à ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0DNSServerList** ou **OSDAdapter1DNSServerList** .  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*DNS_servers*|Uma lista delimitada por vírgulas de endereços IP de servidor DNS que será atribuído à ligação de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSServerList=192.168.0.254,192.168.100.254`|  

####  <a name="OSDAdapterxDNSSuffix"></a>OSDAdapterxDNSSuffix  
 Um sufixo DNS que será atribuído à ligação de rede. Esta propriedade destina-se apenas ao LTI. Para ZTI, consulte o [OSDAdapterxDNSDomain](#OSDAdapterxDNSDomain) propriedade.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0DNSSuffix** ou **OSDAdapter1DNSSuffix**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Sufixo_dns*|Um sufixo DNS que será atribuído à ligação de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSSuffix= WoodGroveBank.com`|  

####  <a name="OSDAdapterxEnableDHCP"></a>OSDAdapterxEnableDHCP  
 Especifica se a ligação de rede irá ser configurada através de DHCP.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0EnableDHCP** ou **OSDAdapter1EnableDHCP**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|A ligação de rede será configurada através de DHCP.|  
|**FALSO**|A ligação de rede será configurada com uma configuração estático.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableDHCP=TRUE`|  

####  <a name="OSDAdapterxEnableDNSRegistration"></a>OSDAdapterxEnableDNSRegistration  
 Especifica se o registo de DNS está ativado na ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0EnableDNSRegistration** ou  **OSDAdapter1EnableDNSRegistration**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Registo de DNS|  
|**FALSO**|Desativa o registo de DNS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableDNSRegistration=TRUE`|  

####  <a name="OSDAdapterxEnableFullDNSRegistration"></a>OSDAdapterxEnableFullDNSRegistration  
 Especifica se o registo de DNS completo está ativado na ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0EnableFullDNSRegistration** ou  **OSDAdapter1EnableFullDNSRegistration**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Ativa o registo de DNS completo|  
|**FALSO**|Desativa o registo de DNS completo|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableFullDNSRegistration=TRUE`|  

####  <a name="OSDAdapterxEnableLMHosts"></a>OSDAdapterxEnableLMHosts  
 Especifica se a pesquisa LMHOSTS está ativada na ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém informações de adaptador de rede, tais como **OSDAdapter0EnableLMHosts** ou **OSDAdapter1EnableLMHosts** .  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite a pesquisa LMHOSTS|  
|**FALSO**|Desativa a pesquisa LMHOSTS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableLMHosts=TRUE`|  

####  <a name="OSDAdapterxEnableIPProtocolFiltering"></a>OSDAdapterxEnableIPProtocolFiltering  
 Esta propriedade especifica se a filtragem de protocolo IP deve ser ativada na ligação de rede.  

 O*x*no nome desta propriedade é um marcador de posição para uma matriz baseada em zero que contém rede informações da placa, tais como *OSDAdapter0EnableIPProtocolFiltering* ou  **OSDAdapter1EnableIPProtocolFiltering**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite a filtragem de protocolo IP|  
|**FALSO**|Desativa a filtragem de protocolo IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableIPProtocolFiltering =TRUE`|  

####  <a name="OSDAdapterxEnableTCPFiltering"></a>OSDAdapterxEnableTCPFiltering  
 Especifica se TCP\/IP filtragem deve ser ativada em ligação de rede. Esta propriedade destina-se apenas ao ZTI. Para LTI, consulte o [OSDAdapterxEnableTCPIPFiltering](#OSDAdapterxEnableTCPIPFiltering) propriedade.  

> [!NOTE]
>  O*x*deste nome da propriedade é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0EnableTCPFiltering** ou  **OSDAdapter1EnableTFiltering**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite que o TCP\/filtragem de IP|  
|**FALSO**|Desativa o TCP\/filtragem de IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableTCPFiltering=TRUE`|  

####  <a name="OSDAdapterxEnableTCPIPFiltering"></a>OSDAdapterxEnableTCPIPFiltering  
 Especifica se TCP\/IP filtragem deve ser ativada em ligação de rede. Esta propriedade destina-se apenas ao LTI. Para ZTI, consulte o [OSDAdapterxEnableTCPFiltering](#OSDAdapterxEnableTCPFiltering) propriedade.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0EnableTCPIPFiltering** ou  **OSDAdapter1EnableTCPIPFiltering**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite que o TCP\/filtragem de IP|  
|**FALSO**|Desativa o TCP\/filtragem de IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableTCPIPFiltering=TRUE`|  

####  <a name="OSDAdapterxEnableWINS"></a>OSDAdapterxEnableWINS  
 Especifica se será ativado WINS na ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0EnableWINS** ou  **OSDAdapter1EnableWINS**.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite que o WINS|  
|**FALSO**|Desativa o WINS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1`|  

####  <a name="OSDAdapterxGatewayCostMetric"></a>OSDAdapterxGatewayCostMetric  
 Uma vírgula\-lista delimitada de métricas de custo de Gateway especificado como números inteiros ou a cadeia "Automático" \(se estiver vazio, utiliza "Automático"\) que será configurado na ligação.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0GatewayCostMetric** ou  **OSDAdapter1GatewayCostMetric**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*Custo\_métricas*|Uma vírgula\-lista delimitada de métricas de custo de Gateway|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0GatewayCostMetrics=Automatic`|  

####  <a name="OSDAdapterxGateways"></a>OSDAdapterxGateways  
 Uma vírgula\-lista delimitada de gateways a atribuir à ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0Gateways** ou  **OSDAdapter1Gateways**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*gateways*|Uma vírgula\-lista delimitada de gateways|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0Gateways=192.168.0.1,192.168.100.1`|  

####  <a name="OSDAdapterxIPAddressList"></a>OSDAdapterxIPAddressList  
 Uma vírgula\-lista delimitada de IP endereços a ser atribuída a ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0IPAddressList** ou  **OSDAdapter1IPAddressList**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*IP\_endereços*|Uma lista delimitada de vírgulas de endereços IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0`|  

####  <a name="OSDAdapterxIPProtocolFilterList"></a>OSDAdapterxIPProtocolFilterList  
 Uma vírgula\-lista delimitada de filtros do protocolo IP a atribuir à ligação de rede. Esta propriedade pode ser configurada através do ficheiro CustomSettings.ini ou da base de dados do MDT mas não o Deployment Workbench. Se utilizar o Configuration Manager é também configuráveis utilizando um **aplicar definições de rede** passo de sequência de tarefas.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0IPProtocolFilterList** ou  **OSDAdapter1IPProtocolFilterList**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*protocolo\_filtro\_lista*|Uma vírgula\-lista delimitada de filtros de protocolo IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0IPProtocolFilterList=a list of approved IP protocols`|  

####  <a name="OSDAdapterxMacAddress"></a>OSDAdapterxMacAddress  
 Atribua as definições de configuração especificado para a placa de interface de rede que corresponde ao endereço MAC especificado.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0MacAddress** ou  **OSDAdapter1MacAddress**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*MAC\_endereço*|Endereço MAC do adaptador de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0MacAddress=00:0C:29:67:A3:6B`|  

####  <a name="OSDAdapterxName"></a>OSDAdapterxName  
 Atribua as definições de configuração especificado para o adaptador de rede que corresponda ao nome especificado. Esta propriedade destina-se apenas ao ZTI. Para a propriedade equivalente para LTI, consulte [OSDAdapterxDescription](#OSDAdapterxDescription).  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0Name** ou **OSDAdapter1Name**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Nome do adaptador de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0Name=3Com 3C920 Integrated Fast Ethernet Controller`|  

####  <a name="OSDAdapterxSubnetMask"></a>OSDAdapterxSubnetMask  
 Uma vírgula\-lista delimitada de máscaras de sub-rede IP a atribuir à ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0SubnetMask** ou  **OSDAdapter1SubnetMask**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*sub-rede\_máscaras de*|Uma vírgula\-lista delimitada de máscaras de sub-rede IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0`|  

#### <a name="osdadapterxtcpfilterportlist"></a>OSDAdapterxTCPFilterPortList  
 Uma vírgula\-lista delimitada de portas de filtro TCP a atribuir à ligação de rede. Esta propriedade pode ser configurada através do ficheiro CustomSettings.ini ou da base de dados do MDT mas não o Deployment Workbench. Se utilizar o Configuration Manager é também configuráveis utilizando um **aplicar definições de rede** passo de sequência de tarefas.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0TCPFilterPortList** ou  **OSDAdapter1TCPFilterPortList**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*porta\_lista*|Uma vírgula\-lista delimitada de TCP\/portas de filtro IP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0TCPFilterPortList=a list of approved TCP ports`|  

####  <a name="OSDAdapterxTCPIPNetBiosOptions"></a>OSDAdapterxTCPIPNetBiosOptions  
 Especifica o TCP\/opções de NetBIOS de IP a atribuir à ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0TCPIPNetBiosOptions** ou  **OSDAdapter1TCPIPNetBiosOptions**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**0**|Desative o reencaminhamento IP.|  
|**1**|Ative o reencaminhamento IP.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0TCPIPNetBiosOptions=0`|  

####  <a name="OSDAdapterxUDPFilterPortList"></a>OSDAdapterxUDPFilterPortList  
 Uma vírgula\-lista delimitada de protocolo de datagrama de utilizador \(UDP\) filtrar portas a atribuir à ligação de rede. Esta propriedade pode ser configurada através do ficheiro CustomSettings.ini e da base de dados do MDT mas não o Deployment Workbench. Se utilizar o Configuration Manager é também configuráveis utilizando um **aplicar definições de rede** passo de sequência de tarefas.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0UDPFilterPortList** ou  **OSDAdapter1UDPFilterPortList**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*porta\_lista*|Uma vírgula\-lista delimitada de portas UDP de filtro|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0UDPFilterPortList=a list of approved UDP ports`|  

####  <a name="OSDAdapterxWINSServerList"></a>OSDAdapterxWINSServerList  
 Um dois\-elemento, vírgula\-lista delimitada de IP do servidor WINS endereços a ser atribuída a ligação de rede.  

> [!NOTE]
>  O*x*nas propriedades do nome é um marcador de posição para um zero\-com base matriz que contém informações de adaptador de rede, tais como **OSDAdapter0WINSServerList** ou  **OSDAdapter1WINSServerList**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*WINS\_servidor\_lista*|Uma vírgula\-lista delimitada de endereços IP do servidor WINS|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1`|  

####  <a name="OSDAdapterCount"></a>OSDAdapterCount  
 Especifica o número de ligações de rede que estão a ser configurado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|Contagem|O número de adaptadores de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDAdapterCount=1 OSDAdapter0EnableDHCP=FALSE OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0 OSDAdapter0Gateways=192.168.0.1,192.168.100.1 OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1 OSDAdapter0TCPIPNetBiosOptions=0 OSDAdapter0MacAddress=00:0C:29:67:A3:6B OSDAdapter0GatewayCostMetrics=Automatic OSDAdapter0EnableTCPIPFiltering=TRUE OSDAdapter0EnableLMHosts=TRUE OSDAdapter0EnableFullDNSRegistration=TRUE OSDAdapter0EnableDNSRegistration=TRUE OSDAdapter0DNSSuffix=WoodGroveBank.com`|  

#### <a name="osdanswerfilepath"></a>OSDAnswerFilePath  
 Especifica o caminho para o ficheiro de resposta a utilizar durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*ficheiro\_caminho*|Especifica o caminho para o ficheiro de resposta a utilizar durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDBitLockerCreateRecoveryPassword"></a>OSDBitLockerCreateRecoveryPassword  
 Um valor booleano que indica se o processo cria uma chave de recuperação para o BitLocker. A chave é utilizada para recuperar dados encriptados num BitLocker volume. Esta chave é criptograficamente equivalente a uma chave de arranque. Se estiver disponível, a chave de recuperação desencripta VMK, que, por sua vez, desencripta o FVEK.  

> [!NOTE]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**AD**|É criada uma chave de recuperação.|  
|Não foi especificado|Não é criada uma chave de recuperação.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerStartupKeyDrive=C:`|  

####  <a name="OSDBitLockerMode"></a>OSDBitLockerMode  
 O tipo de instalação do BitLocker para ser executada. Proteger o computador de destino utilizando um dos seguintes métodos:  

-   Um microcontroller TPM  

-   Um TPM e uma chave de arranque externa \(utilizando uma chave que normalmente está armazenada numa pen USB\)  

-   Um TPM e PIN  

-   Uma chave de arranque externa  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**TPM**|Proteger o computador com TPM apenas. O TPM é um microcontroller que armazena as chaves, palavras-passe e certificados digitais. O microcontroller é, geralmente, uma parte integral da motherboard computador.|  
|**TPMKey**|Proteger o computador com TPM e uma chave de arranque. Utilize esta opção para criar uma chave de arranque e para as guardar numa pen USB. A chave de arranque tem de estar presente na porta sempre que o computador é iniciado.|  
|**TPMPin**|Proteger o computador com TPM e um pin. Utilize esta opção juntamente com o **BDEPin** propriedade.<br /><br /> Nota:<br /><br /> Este valor não é válido quando utilizar ZTI.|  
|**Chave**|Proteger o computador com uma chave externa \(a chave de recuperação\) que pode ser armazenado numa pasta, no AD DS, ou impressas.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPM OSDBitLockerCreateRecoveryPassword=AD`|  

####  <a name="OSDBitLockerRecoveryPassword"></a>OSDBitLockerRecoveryPassword  
 Em vez de gerar uma palavra-passe de recuperação aleatória, a ação da sequência de tarefas **Ativar BitLocker** utiliza o valor especificado como a palavra-passe de recuperação. O valor tem de ser uma palavra-passe de recuperação do BitLocker numérica válida.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|Um 48 válido\-palavra-passe de dígitos|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerRecoveryPassword=621280128854709621167486709731081433315062587367 OSDBitLockerStartupKeyDrive=C:`|  

####  <a name="OSDBitLockerStartupKey"></a>OSDBitLockerStartupKey  
 Em vez de gerar uma chave de arranque aleatória para a opção de gestão de chaves **chave de arranque em USB apenas**, a **ativar BitLocker** ação de sequência de tarefas utiliza o valor como a chave de arranque. O valor tem de ser válida, Base64\-codificado chave de arranque do BitLocker.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*chave de arranque*|Base64\-codificado chave de arranque do BitLocker|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=KEY OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerStartupKey=8F4922B8-2D8D-479E-B776-12629A361049`|  

####  <a name="OSDBitLockerStartupKeyDrive"></a>OSDBitLockerStartupKeyDrive  
 A localização para armazenar a chave de recuperação do BitLocker e a chave de arranque.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*localização*|A localização de armazenamento para a chave de recuperação e a chave de arranque \(ou local para o computador de destino ou para um UNC que aponta para uma pasta de rede partilhada\)|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLocker CreateRecoveryPassword=AD OSDBitLockerStartupKeyDrive=C:`|  

####  <a name="OSDBitLockerTargetDrive"></a>OSDBitLockerTargetDrive  
 Especifica a unidade sejam encriptados. Unidade predefinida é a unidade que contém o sistema operativo.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*unidade*|A unidade que está a encriptar|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDERecoveryPassword=TRUE OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerTargetDrive=C:`|  

####  <a name="OSDBitLockerWaitForEncryption"></a>OSDBitLockerWaitForEncryption  
 Especifica que o processo de implementação deve continue até que o BitLocker concluiu o processo de encriptação para todas as unidades especificados. Especifica verdadeiro foi aumentar substancialmente o tempo necessário para concluir o processo de implementação.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Especifica que o processo de implementação deve aguardar para encriptação de unidade concluir|  
|**FALSO**|Especifica que o processo de implementação não deve aguardar para encriptação de unidade concluir|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerStartupKeyDrive=C: OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerWaitForEncryption=TRUE`|  

####  <a name="OSDComputerName"></a>OSDComputerName  
 O novo nome de computador para atribuir ao computador de destino.  

> [!NOTE]
>  Esta propriedade também pode ser definida numa sequência de tarefas utilizando um personalizado **Set Task Sequence Variable** passo de sequência de tarefas.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*computador\_nome*|O novo nome de computador para atribuir ao computador de destino|  

|**Exemplo**|  
|-|  
|`[Default] OSDComputerName=%_SMSTSMachineName%`|  

####  <a name="OSDDiskAlign"></a>OSDDiskAlign  
 Esta propriedade é utilizada para transferir um valor para o **alinhar** parâmetro do **criar a partição primária** no **DiskPart** comando. O **alinhar** parâmetro é normalmente utilizado com o número de unidade lógica de RAID de hardware \(LUN\) matrizes para melhorar o desempenho quando as unidades lógicas \(LUs\) não são cilindro alinhado. O **alinhar** parâmetro alinhar a uma partição principal que não seja cilindro alinhado no início de um disco e arredonda o desvio para o limite de alinhamento mais próximo. Para mais informações sobre o **alinhar** parâmetro, consulte [criar a partição primária](http://technet.microsoft.com/library/cc771243\(WS.10\).aspx).  

> [!NOTE]
>  Esta propriedade pode ser utilizada em conjunto com o **OSDDiskOffset** propriedade definida a **desvio** parâmetro para o **criar a partição primária** no **DiskPart** comando. Para obter mais informações, consulte o [OSDDiskOffset](#OSDDiskOffset) propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*alinhamento\_valor*|Especifica o número de quilobytes \(KB\) desde o início do disco para o limite de alinhamento mais próximo.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDDiskAlign=1024 OSDDiskOffset=2048`|  

####  <a name="OSDDiskIndex"></a>OSDDiskIndex  
 Especifica o índice de disco que será configurado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*disco\_índice*|Especifica o índice de disco que será configurado \(o valor predefinido é **0**.\)|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDDiskIndex=0`|  

####  <a name="OSDDiskOffset"></a>OSDDiskOffset  
 Esta propriedade é utilizada para transferir um valor para o **desvio** parâmetro do **criar a partição primária** no **DiskPart** comando. Para mais informações sobre o **desvio** parâmetro, consulte [criar a partição primária](http://technet.microsoft.com/library/cc771243\(WS.10\).aspx).  

 Esta propriedade pode ser utilizada em conjunto com o **OSDDiskAlign** propriedade definida a **alinhar** parâmetro para o **criar a partição primária** no **DiskPart** comando. Para obter mais informações, consulte o [OSDDiskAlign](#OSDDiskAlign) propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*o desvio\_valor*|Especifica o deslocamento de byte no qual pretende criar a partição. Para o registo de arranque principal \(MBR\) o deslocamento de discos, arredonda para o limite de cilindro mais próximo.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDDiskAlign=1024 OSDDiskOffset=2048`|  

####  <a name="OSDDiskPartBiosCompatibilityMode"></a>OSDDiskPartBiosCompatibilityMode  
 Esta propriedade especifica se pretende desativar otimizações de alinhamento de cache ao particionar o disco rígido para compatibilidade com certos tipos de BIOS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Permite que as otimizações de alinhamento de cache ao particionar o disco rígido para compatibilidade com certos tipos de BIOS|  
|**FALSO**|Desativa a otimizações de alinhamento de cache ao particionar o disco rígido para compatibilidade com certos tipos de BIOS \(este é o valor predefinido.\)|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDDiskPartBiosCompatibilityMode=TRUE`|  

####  <a name="OSDImageCreator"></a>OSDImageCreator  
 Especifica o nome da conta de instalação que será utilizado durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*imagem\_criador*|Especifica o nome da conta de instalação que será utilizado durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDImageIndex"></a>OSDImageIndex  
 Especifica o índice da imagem do ficheiro. wim. Esta propriedade é referenciada durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*índice*|Especifica o índice da imagem no ficheiro WIM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDImagePackageID"></a>OSDImagePackageID  
 Especifica o ID de pacote para a imagem a instalar durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*pacote\_ID*|Especifica o ID de pacote para a imagem a instalar durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDInstallEditionIndex"></a>OSDInstallEditionIndex  
 Especifica o índice da imagem no ficheiro WIM. Esta propriedade é referenciada durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*índice*|Especifica o índice da imagem no ficheiro WIM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDInstallType"></a>OSDInstallType  
 Especifica o tipo de instalação utilizado para implementações do OEM. A predefinição é **Sysprep**.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*instalar\_tipo*|Especifica o tipo de instalação utilizado para implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDisk"></a>OSDisk  
 Especifica a unidade utilizada para instalar o sistema operativo durante implementações do OEM. O valor predefinido é **c:**.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*disco*|Especifica a unidade utilizada para instalar o sistema operativo durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDPartitions"></a>OSDPartitions  
 Especifica o número de configurações de partições definido. O número máximo de partições que pode ser configurada é dois. A predefinição é **nenhum**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*partições*|Especifica o número de configurações de partições definido|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions=1 OSDPartitions0Bootable=TRUE OSDPartitions0FileSystem=NTFS OSDPartitions0QuickFormat=TRUE OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB OSDPartitions0Type=Primary OSDPartitions0VolumeName=OSDisk OSDPartitions0VolumeLetterVariable=NewDrive1`|  

####  <a name="OSDPartitionsxBootable"></a>OSDPartitionsxBootable  
 A partição no índice especificado deve ser definida de arranque. A primeira partição de predefinição está definida suportes.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|A partição deve ser definida como suportes.|  
|**FALSO**|Não defina a partição de arranque para.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0Bootable=TRUE`|  

####  <a name="OSDPartitionsxFileSystem"></a>OSDPartitionsxFileSystem  
 O tipo de sistema de ficheiros para a partição no índice especificado. Os valores válidos são **NTFS** ou **FAT32**.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*file_system*|O tipo de sistema de ficheiros para a partição|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0FileSystem=NTFS`|  

####  <a name="OSDPartitionsxQuickFormat"></a>OSDPartitionsxQuickFormat  
 A partição no índice especificado deve ser formatada rápido. A predefinição é **verdadeiro**.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Formato de rápido a partição.|  
|**FALSO**|Efetue não rápida-format a partição.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0QuickFormat=TRUE`|  

####  <a name="OSDPartitionsxSize"></a>OSDPartitionsxSize  
 O tamanho da partição no índice especificado.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Tamanho*|Tamanho de partição|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB`|  

####  <a name="OSDPartitionsxSizeUnits"></a>OSDPartitionsxSizeUnits  
 As unidades de medida utilizada quando especificar o tamanho da partição. Os valores válidos são **MB**, **GB**, ou  **%** . O valor predefinido é **MB**.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*size_units*|As unidades de medida utilizada quando especificar o tamanho da partição|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB`|  

####  <a name="OSDPartitionsxType"></a>OSDPartitionsxType  
 O tipo de partição para criar o índice especificado.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**Primário**|Crie uma partição principal. Este é o valor predefinido.|  
|**Lógica**|Crie uma partição lógica.|  
|**Expandido**|Crie uma partição expandida.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0Type=Primary`|  

####  <a name="OSDPartitionsxVolumeLetterVariable"></a>OSDPartitionsxVolumeLetterVariable  
 A propriedade que recebe a letra de unidade que está atribuída à partição a ser gerida.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*volume_letter_variable*|O nome da variável que será atribuído a letra de unidade da partição que está a ser gerida|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0VolumeLetterVariable=NewDrive1`|  

####  <a name="OSDPartitionsxVolumeName"></a>OSDPartitionsxVolumeName  
 O nome do volume que irá ser atribuído à partição no índice especificado.  

> [!NOTE]
>  O*x* nas propriedades do nome é um marcador de posição para uma matriz baseada em zero que contém as configurações de partição.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*volume_name*|O nome do volume que será atribuído à partição|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSDPartitions0VolumeName=OSDisk`|  

####  <a name="OSDPreserveDriveLetter"></a>OSDPreserveDriveLetter  
 Esta propriedade é utilizada para determinar se o **aplicar SO** passo de sequência de tarefas deverá preservar a letra de unidade no ficheiro de imagem do sistema operativo (ficheiro. wim) que está a ser implementada no computador de destino.  

> [!NOTE]
>  Esta propriedade só deve ser definida no passo de sequência de tarefas, não no ficheiro CustomSettings.ini ou na base de dados do MDT.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|As letras de unidade no ficheiro de imagem do sistema operativo (ficheiro. wim) e o sistema operativo unidades letras depois de implementação são idênticos às letras de unidade no ficheiro. wim.|  
|**FALSO**|As letras de unidade no ficheiro de imagem do sistema operativo (ficheiro. wim) são ignoradas, que permite que a sequência de tarefas substituir as letras de controladores no ficheiro. wim.<br /><br /> Nota:<br /><br /> Para o MDT, este valor deve ser sempre selecionado.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDStateStorePath"></a>OSDStateStorePath  
 LTI e ZTI utilizar esta propriedade para definir o caminho onde serão armazenados os dados de migração de estado do utilizador, que pode ser um caminho UNC, um caminho local ou um caminho relativo.  

> [!NOTE]
>  O **OSDStateStorePath** propriedade tem precedência sobre a [StatePath](#StatePath) ou [UserDataLocation](#UserDataLocation) propriedade quando essas propriedades também são especificadas.  

 Num cenário de implementação de substituir o computador em ZTI, o [restaurar estado do utilizador](#RestoreUserState) passo de sequência de tarefas é ignorado se o **OSDStateStorePath** propriedade está definida como ou um caminho UNC válido. A solução é para definir o [USMTLocal](#USMTLocal) propriedade para verdadeiro. Se o fizer, força ZTI UserState.wsf para reconhecer o caminho no [OSDStateStorePath](#OSDStateStorePath) propriedade. Isto é causado pelo **solicitar armazenamento de Estados** tarefas passo de sequência de que está a ser ignorada e o valor anterior no **OSDStateStorePath** propriedade que está a ser retida.  

 Num cenário de implementação de substituir o computador em ZTI, onde os dados de migração de estado do utilizador e a computadores na íntegra são a cópia de segurança, o ficheiro de Backup.wim é armazenado na pasta especificada no **OSDStateStorePath** propriedade. Isto pode ser causado especificando o valor incorreto para a [ComputerBackupLocation](#ComputerBackupLocation) propriedade.  

 Por exemplo, o seguinte ficheiro CustomSettings.ini fará com que o ficheiro de Backup.wim para serem armazenados na mesma pasta especificada no **OSDStateStorePath** propriedade:  

```  
USMTLocal=True  
OSDStateStorePath=\\fs1\Share\Replace  

ComputerBackupLocation=NETWORK  
BackupShare=\\fs1\Share\ComputerBackup  
BackupDir=Client01  
```  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Caminho*|Será armazenado o caminho onde os dados de migração de estado do utilizador, que pode ser um caminho UNC, um caminho local ou um caminho relativo|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] USMTLocal=True OSDStateStorePath=\\fs1\Share\Replace ComputerBackupLocation=\\fs1\Share\ComputerBackup\Client01`|  

####  <a name="OSDTargetSystemDrive"></a>OSDTargetSystemDrive  
 Especifica a unidade onde será instalado o sistema operativo durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*System_drive*|Especifica a unidade onde será instalado o sistema operativo durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDTargetSystemRoot"></a>OSDTargetSystemRoot  
 Especifica o caminho de instalação em que o sistema operativo será instalado durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*system_root*|Especifica o caminho de instalação em que o sistema operativo será instalado durante implementações do OEM|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSFeatures"></a>OSFeatures  
 Uma lista delimitada por vírgulas da funcionalidade de servidor IDs que será instalado no computador de destino.  

> [!NOTE]
>  Nem todas as funcionalidades listadas no ficheiro ServerManager.xml são compatíveis com todos os sistemas operativos de servidor.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*ID1, ID2*|As funcionalidades de servidor que estão a ser instalado no computador de destino. Os valores válidos estão localizados no *program_files*\Microsoft Deployment Toolkit\Bin\ServerManager.xml ficheiro no servidor do MDT.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSFeatures=CMAK,MSMQ-Multicasting,RSAT`|  

####  <a name="OSInstall"></a>OSInstall  
 Indica se o computador de destino está autorizado a ter instalado o sistema de operativo de destino. Se o **OSInstall** propriedade não está listada, é a predefinição para permitir a implementação de sistemas operativos em qualquer computador de destino.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Implementação de um sistema operativo no computador de destino está autorizada. Este é o valor predefinido.|  
|**NÃO**|Implementação de um sistema operativo no computador de destino não está autorizada.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES`|  

####  <a name="OSRoles"></a>OSRoles  
 Uma lista delimitada por vírgulas dos IDs que será instalado no computador de destino da função de servidor.  

> [!NOTE]
>  Nem todas as funções são compatíveis com todos os sistemas operativos de servidor.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*ID1, ID2*|A função de servidor que está a ser instalado no computador de destino.|  

 Consulte "C:\Program Files\Microsoft implementação Toolkit\Bin\ServerManager.xml" para valores de ID válidos.  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSRoles=ADDS`|  

####  <a name="OSRoleServices"></a>OSRoleServices  
 Uma lista delimitada por vírgulas de serviço de função de servidor IDs que será instalado no computador de destino.  

> [!NOTE]
>  Função de servidor nem todos os IDs de serviço são compatíveis com todos os sistemas operativos de servidor.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*ID*|O serviço de função de servidor que será instalado no computador de destino. O valor válido é:<br /><br /> - **Adiciona controlador-domínio-**|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSRoleServices=ADDS-Domain-Controller`|  

####  <a name="OSSKU"></a>OSSKU  
 A edição do sistema operativo em execução. A edição do sistema operativo é determinada através da utilização de **OperatingSystemSKU** propriedade do **Win32_OperatingSystem WMI** classe. Para obter uma lista das edições a **OperatingSystemSKU** propriedade devolve, consulte a secção, "OperatingSystemSKU", no [classe Win32_OperatingSystem](http://msdn.microsoft.com/library/windows/desktop/aa394239\(v=vs.85\).aspx).  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*edição*|A edição do sistema operativo. Por exemplo, "" para uma edição de negócio de um sistema operativo ou empresariais "Empresarial" para uma edição Enterprise de um sistema operativo.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSVersion"></a>OSVersion  
 A versão do sistema operativo em execução. Esta propriedade só deve ser utilizada para detetar se o sistema operativo em execução for Windows PE. Utilize o [OSVersionNumber](#OSVersionNumber) propriedade para detetar outros sistemas operativos.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**WinPE**|Windows PE|  
|**2008 R2**|Windows Server 2008 R2|  
|**Win7Client**|Windows 7|  
|**Outros**|Sistemas operativos que não se encontram listados, incluindo o Windows 8 e Windows Server 2012|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSVersionNumber"></a>OSVersionNumber  
 O número de versão principal e secundária do sistema operativo. Esta propriedade é referenciada durante implementações do OEM.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*version_number*|O número de versão principal e secundária do sistema operativo|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OverrideProductKey"></a>OverrideProductKey  
 A cadeia de chave de ativação múltipla (MAK) a ser aplicadas após o funcionamento de destino é implementada no computador de destino. O valor especificado nesta propriedade é utilizado pelo ZTILicensing.wsf script durante a fase de restauro de estado para aplicar a MAK ao sistema operativo de destino. O script também configura a imagem de licenciamento em volume para utilizar a ativação da MAK em vez do serviço de gestão de chaves (KMS). O sistema operativo tem de ser ativado com a Microsoft após a MAK é aplicada. Isto é utilizado quando o computador de destino não é possível aceder a um servidor que está a executar o KMS.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*MAK*|A cadeia MAK ser fornecida para o sistema operativo de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF OverrideProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF`|  

####  <a name="PackageGroup"></a>PackageGroup  
 Uma lista de valores de texto que associa os pacotes de sistema a funcionar entre si (normalmente, com base no tipo de pacote do sistema operativo). Um pacote do sistema operativo pode ser associado um ou mais grupos de pacote. O **PackageGroup** propriedade permite que os pacotes de sistema operativo dentro de um ou mais grupos para ser implementada para um computador de destino.  

 Os valores de texto numa lista podem ser qualquer valor não vazio. O **PackageGroup** valor da propriedade tem um sufixo numérico (por exemplo, **PackageGroup001** ou **PackageGroup002**). Depois de se encontra definida, um grupo do pacote está associado um computador. Um computador pode estar associado a mais do que um grupo do pacote.  

> [!NOTE]
>  Pacotes do sistema operativo são criados no nó de pacotes do SO no Deployment Workbench.  

> [!NOTE]
>  O **PackageGroup** propriedade pode ser especificada no formato *PackageGroup1 = atualizações* ou *PackageGroup001 = atualizações*.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*package_group_name*|Nome do grupo do pacote seja implementado no computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] PackageGroup001=Updates`|  

####  <a name="Packages"></a>Pacotes  
 A lista de pacotes do Configuration Manager para ser implementado no computador de destino. O **pacotes** propriedade tem um sufixo numérico (por exemplo, Packages001 ou Packages002).  

> [!NOTE]
>  O **PackageGroup** propriedade pode ser especificada no formato *PackageGroup1 = atualizações* ou *PackageGroup001 = atualizações*.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*package_id:program_name*|Nome do pacote seja implementado no computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] Packages001=NYC00010:Install Packages002=NYC00011:Install`|  

####  <a name="PackageSelectionProfile"></a>PackageSelectionProfile  
 Nome de perfil utilizado durante a instalação do pacote.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*profile_name*|Nome do perfil utilizado durante a instalação do pacote|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] PackageSelectionProfile=CoreApplications`|  

####  <a name="Parameters"></a>Parâmetros  
 Os parâmetros a transmitir a uma consulta de base de dados que devolve valores de propriedade de colunas na tabela especificada no **tabela** propriedade. A tabela está localizada na base de dados especificada no **base de dados** propriedade no computador especificado no **SQLServer** propriedade. A instância do SQL Server no computador especificada no **instância** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Parameter1, parameter2*|A lista de parâmetros para passar para a consulta de base de dados|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="ParameterCondition"></a>ParameterCondition  
 Indicador de se um valor boleano e ou ou a operação é executada nas propriedades de listado no **parâmetros** propriedade.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**E**|Uma operação Booleano e é efetuada nas propriedades de listado no **parâmetros** propriedade. Só os resultados que correspondam a todas as propriedades especificadas no **parâmetros** propriedade são devolvidos. Este é o valor predefinido.|  
|**OU**|É efetuar uma operação booleano ou nas propriedades de listado no **parâmetros** propriedade. Os resultados que correspondam a qualquer propriedade especificada no **parâmetros** propriedade são devolvidos.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="ParentDomainDNSName"></a>ParentDomainDNSName  
 Especifica o nome de domínio DNS de um domínio de serviço de diretório existentes ao instalar um domínio subordinado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Especifica o nome de domínio DNS de um domínio de serviço de diretório existentes ao instalar um domínio subordinado|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ParentDomainDNSName=WoodGroveBank.com`|  

####  <a name="Password"></a>Palavra-passe  
 Especifica a palavra-passe para o nome de utilizador (as credenciais da conta) a utilizar para promover o servidor de membro para um controlador de domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|Especifica a palavra-passe para o nome de utilizador (as credenciais da conta) a utilizar para promover o servidor de membro para um controlador de domínio|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] Password=<complex_password>`|  

####  <a name="Phase"></a>Fase  
 A fase do processo de implementação atual. O sequenciador de tarefas utiliza estas fases para determinar as tarefas que têm de ser concluídas.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VALIDAÇÃO**|Identifica se o computador de destino é capaz de executar os scripts necessários para concluir o processo de implementação.|  
|**STATECAPTURE**|Guarda os dados de migração de estado do utilizador antes de implementar o novo sistema operativo de destino.|  
|**PREINSTALL**|Conclui as tarefas que necessitam de ser feito (como criar novas partições) antes de implementar o sistema operativo de destino.|  
|**INSTALAR**|Instala o sistema operativo de destino no computador de destino.|  
|**POSTINSTALL**|Conclui as tarefas que necessitam de ser efetuadas antes de restaurar os dados de migração de estado do utilizador. Estas tarefas personalizar o sistema de operativo de destino antes de iniciar a hora do computador o primeiro de destino (como instalar atualizações ou adicionar controladores).|  
|**STATERESTORE**|Restaura os dados de migração de estado de utilizador guardados durante a fase de captura de estado.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="Port"></a>Porta  
 O número da porta que deve ser utilizada ao ligar à instância de base de dados do SQL Server que é utilizada para consultar a propriedade valores das colunas na tabela especificada no **tabela** propriedade. A base de dados reside num computador especificado no **SQLServer** propriedade. A instância do SQL Server no computador especificada no **instância** propriedade. A porta utilizada durante a ligação é especificada no **porta** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*porta*|O número de porta a utilizar quando ligar ao SQL Server|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 Database=MDTDB Instance=MDT2010 Port=1433 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="PowerUsers"></a>PowerUsers  
 Uma lista de contas de utilizador e grupos de domínio a ser adicionado ao grupo de utilizadores avançados local no computador de destino. O **PowerUsers** propriedade é uma lista de valores de texto que pode ser qualquer valor não vazio. O **PowerUsers** propriedade tem um sufixo numérico (por exemplo, **PowerUsers1** ou **PowerUsers2**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Nome de utilizador ou grupo a adicionar ao grupo local de utilizadores avançados|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff PowerUsers001=WOODGROVEBANK\User01 PowerUsers002=WOODGROVEBANK\User02`|  

####  <a name="PrepareWinRE"></a>PrepareWinRE  
 Esta propriedade especifica se o ficheiro de LiteTouchPE.wim, que inclui o Windows RE e opcionalmente DaRT, é aplicado para a unidade de sistema como partição de recuperação. Isto permite que o computador de destino a utilizar a imagem de LiteTouchPE.wim para efetuar tarefas de recuperação. DaRT, opcionalmente, pode ser incluído na imagem, que disponibiliza funcionalidades de recuperação de DaRT no computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|SIM|O ficheiro de LiteTouchPE.wim, que inclui o Windows RE e opcionalmente DaRT, é aplicado a unidade do sistema como partição de recuperação.|  
|*qualquer outro valor*|O ficheiro de LiteTouchPE.wim, que inclui o Windows RE e opcionalmente DaRT, não se aplica a unidade do sistema como partição de recuperação. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] PrepareWinRE=YES`|  

####  <a name="Priority"></a>Prioridade  
 A propriedade reservada que determina a sequência para localizar os valores de configuração. O **prioridade** listas de propriedades reservada, cada secção a ser procurado e a ordem na qual são procuradas as secções. Quando é encontrado um valor de propriedade, o script de ZTIGather.wsf quits procura para a propriedade e as secções restantes não são analisadas relativamente a essa propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*section1, section2*|As secções a ser procurado pela ordem que estão a ser procurado|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=MACAddress, Default  [Default] UserDataLocation=NONE CustomProperty=TRUE  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP`|  

####  <a name="ProcessorSpeed"></a>ProcessorSpeed  
 A velocidade do processador instalado no computador de destino no MHz. Por exemplo, o valor **1995** indica o processador no computador de destino está em execução em 1,995 MHz ou 2 gigahertz.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*processor_speed*|A velocidade do processador no computador de destino em megahertz|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="Product"></a>Produto  
 O nome de produto do computador de destino. Com alguns fornecedores de computador, a marca e modelo poderão não ser suficientemente exclusivos para identificar as características de uma configuração específica (por exemplo, chipsets hyperthreaded ou não hyperthreaded). O **produto** propriedade pode ajudar a diferenciar.  

 O formato para **produto** não está definido. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um nome de produto específica para um número de modelo do computador específico para um fabricante de computadores específico (normalmente em conjunto com o **tornar** e **Modelo** propriedades).  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*produto*|O nome de produto do computador de destino|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="ProductKey"></a>ProductKey  
 A cadeia de chave produto ser configuradas para o computador de destino. Antes do sistema operativo de destino for implementado, a chave de produto especificada é automaticamente inserida na localização adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*product_key*|A chave de produto que seja atribuído ao computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF`|  

####  <a name="Properties"></a>Propriedades  
 Uma propriedade reservada que define as propriedades personalizadas, definido pelo utilizador. Estas propriedades definidas pelo utilizador estão localizadas pelo script ZTIGather.wsf no ficheiro CustomSettings.ini, ficheiro BootStrap.ini ou da base de dados do MDT. Estas propriedades são adições às propriedades predefinidas no MDT.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*custom_property1,*custom_property2|Propriedades personalizadas, definido pelo utilizador que seja resolvido|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac UserDataLocation=NONE CustomProperty=TRUE  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP ApplicationInstall=Minimum`|  

####  <a name="ReplicaDomainDNSName"></a>ReplicaDomainDNSName  
 Especifica o nome de domínio DNS do domínio a replicar.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Especifica o nome de domínio DNS do domínio para replicar|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ReplicaDomainDNSName=WoodGroveBank.com`|  

####  <a name="ReplicaOrNewDomain"></a>ReplicaOrNewDomain  
 Especifica se pretende instalar um novo controlador de domínio como o primeiro controlador de domínio num domínio de serviço de diretório novo ou instalá-lo como um controlador de domínio de serviço de diretório de réplica.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**Réplica**|Instala o novo controlador de domínio como um controlador de domínio de serviço de diretório de réplica.|  
|**Domínio**|Instala o novo controlador de domínio como o primeiro controlador de domínio num domínio de serviço de diretório novo. Tem de especificar o **TreeOrChild** entrada com um valor válido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ReplicaOrNewDomain=Domain`|  

####  <a name="ReplicationSourceDC"></a>ReplicationSourceDC  
 Indica o nome DNS completo do controlador de domínio a partir do qual replica as informações do domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Indica o nome DNS completo do controlador de domínio a partir do qual replica as informações do domínio|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ReplicationSourceDC=dc01.WoodGroveBank.com`|  

####  <a name="ResourceDrive"></a>ResourceDrive  
 A letra de unidade mapeado para o **ResourceRoot** propriedade para os scripts ZTIDrivers.wsf e ZTIPatches.wsf utilizar para instalar controladores e correções de erros para o computador de destino.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Drive_letter*|A designação de letra da unidade lógica que contém os recursos|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="ResourceRoot"></a>ResourceRoot  
 O valor desta propriedade é utilizado pelos scripts ZTIDrivers.wsf e ZTIPatches.wsf para instalar controladores e correções de erros para o computador de destino.  

> [!NOTE]
>  Para LTI, os scripts definido automaticamente o **ResourceRoot** propriedade para ser o mesmo que o **DeployRoot** propriedade. Para ZTI, os valores existentes no **DeployRoot** e **ResourceRoot** propriedades podem ser exclusivas.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*UNC_path*|O caminho UNC para a pasta partilhada que contém os recursos|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceDrive=R: ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE`|  

####  <a name="Role"></a>Função  
 O objetivo de um computador em que as tarefas executadas pelo utilizador no computador de destino. O **função** propriedade apresenta uma lista de valores de texto que podem ser qualquer valor não vazio. O **função** valor da propriedade tem um sufixo numérico (por exemplo, **Role1** ou **Role2**). Quando definida, uma função está associada um computador. Um computador pode efetuar mais do que uma função.  

 Normalmente, o valor para o **função** for definida, efetuando uma consulta de base de dados na base de dados do MDT. Deployment Workbench podem ajudar a criar as definições de função e propriedade associadas ao direito e, em seguida, o Deployment Workbench pode configurar CustomSettings.ini para executar a consulta de base de dados para o **função** propriedade e o definições de propriedade associadas ao direito.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Função*|As funções a ser atribuídas a um computador individual ou um grupo de computadores|  

|**Exemplo 1**|  
|-|  
|`[Settings] Priority=RoleSettings, Default  [Default] SkipCapture=NO UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES ScanStateArgs=/v:15 /o /c LoadStateArgs=/v:7 /c  [RoleSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL_Share Table=RoleSettings Parameters=Role`|  

|**Exemplo 2**|  
|-|  
|`[Settings] Priority=RoleSettings, Default  [Default] SkipCapture=NO UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES Role1=Teller Role2=Woodgrove User  [RoleSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL_Share Table=RoleSettings Parameters=Role`|  

####  <a name="SafeModeAdminPassword"></a>SafeModeAdminPassword  
 Fornece a palavra-passe da conta de administrador quando iniciar o computador no modo de segurança ou numa variante do modo de segurança, tais como o modo de restauro de serviços de diretório.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|Fornece a palavra-passe da conta de administrador quando iniciar o computador no modo de segurança ou numa variante do modo de segurança, tais como o modo de restauro de serviços de diretório|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SafeModeAdminPassword=<complex_password>`|  

####  <a name="ScanStateArgs"></a>ScanStateArgs  
 Argumentos transmitidos para o **USMT Scanstate** processo. Os scripts de chamar Scanstate.exe e, em seguida, insira o registo adequado, progresso e os parâmetros do arquivo de estado. Se este valor não está incluído no ficheiro de definições, o processo de cópia de segurança de estado de utilizador é ignorado.  

> [!NOTE]
>  Utilize o **USMTMigFiles** propriedade para especificar os ficheiros. XML a serem utilizadas pelo Scanstate.exe em vez de utilizar o parâmetro i o **ScanStateArgs** propriedade. Isto impede que o script de ZTIUserState.wsf potencialmente duplicar a mesma lista de ficheiros. XML.  

> [!NOTE]
>  Não adicione qualquer um dos seguintes argumentos de linha de comandos quando configurar esta propriedade: **/hardlink**, **/nocompress**, **/ encriptar**, **/key**, ou **/keyfile**. Os scripts de MDT irão adicionar estes argumentos da linha de comandos, se aplicável para o cenário de implementação atual.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*argumentos*|Os argumentos da linha de comandos transmitida para Scanstate.exe.<br /><br /> Os argumentos predefinido, especificados pelo Deployment Workbench são os seguintes:<br /><br /> - **/v**. Permite uma saída verbosa no registo de Scanstate. A predefinição é **0**. Especifica qualquer número entre 0 e 15. O valor **5** permite verboso e saída de estado.<br /><br /> - **/o**. Substitui quaisquer dados existentes no arquivo. Se não for especificado, Scanstate falhará se o arquivo já contém dados. Esta opção não é possível especificar mais do que uma vez numa janela de linha de comandos.<br /><br /> -                             **/c**. Quando especificado, Scanstate irá continuar a executar, mesmo se não existirem erros nonfatal. Sem o **/c** opção, Scanstate sai no primeiro erro.<br /><br /> Para obter mais informações sobre estas e outros argumentos, consulte os ficheiros de ajuda do USMT.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|  

####  <a name="SerialNumber"></a>SerialNumber  
 O número de série do computador de destino. O formato para os números de série está definido. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um computador específico.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*serial_number*|O formato do número de série está definido e é determinado pelo número de série padrão de cada fabricante de computadores.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="SiteName"></a>SiteName  
 Especifica o nome de um site existente, onde pode colocar o novo controlador de domínio.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|Especifica o nome de um site existente, onde pode colocar o novo controlador de domínio|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SiteName=FirstSite`|  

####  <a name="SkipAdminAccounts"></a>SkipAdminAccounts  
 Indica se o **Local de administradores** página do assistente é ignorada.  

> [!NOTE]
>  Este valor predefinido para esta propriedade é **Sim**, que significa que o **Local de administradores** página do assistente será ignorada por predefinição. Para apresentar a página do assistente, tem de definir especificamente o valor desta propriedade como **não** CustomSettings.ini ou na base de dados do MDT.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas. Este é o valor predefinido.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminAccounts=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipAdminPassword"></a>SkipAdminPassword  
 Indica se o **palavra-passe de administrador** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipApplications"></a>SkipApplications  
 Indica se o **selecione um ou mais aplicações a instalar** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipBDDWelcome"></a>SkipBDDWelcome  
 Indica se o **bem-vindo à implementação do Windows** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!NOTE]
>  Para esta propriedade funcione corretamente, tem de ser configurado no CustomSettings.ini e BootStrap.ini. BootStrap.ini é processada antes de uma partilha de implementação (que contém CustomSettings.ini) tiver sido selecionada.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipBitLocker"></a>SkipBitLocker  
 Indica se o **especificar a configuração do BitLocker** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipBitLocker=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipBuild"></a>SkipBuild  
 Indica se o **Selecione uma sequência de tarefas para executar neste computador** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

 Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipBuild=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipCapture"></a>SkipCapture  
 Indica se o **Especifique se pretende capturar uma imagem** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipComputerBackup"></a>SkipComputerBackup  
 Indica se o **especificar onde pretende guardar uma cópia de segurança de computador completo** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=YES SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipComputerName"></a>SkipComputerName  
 Indica se o **configurar o nome do computador** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipComputerName=YES SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipDomainMembership"></a>SkipDomainMembership  
 Indica se o **associar o computador a um domínio ou grupo de trabalho** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipDomainMembership=NO`|  

####  <a name="SkipFinalSummary"></a>SkipFinalSummary  
 Indica se o **implementação do sistema operativo foi concluída com êxito** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!NOTE]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipGroupSubFolders"></a>SkipGroupSubFolders  
 Por predefinição, quando especificar pastas a incluir quando inserirem controladores, patches \(pacotes\), e assim sucessivamente, os valores são especificados como:  

```  
DriverGroup001=TopFolder\SecondFolder  
PackageGroup001=TopFolder\SecondFolder  
```  

 Isto, por predefinição, também inclui todas as subchaves\-pastas localizadas em "SecondFolder." Se **SkipGroupSubFolders** está definido como **Sim** no CustomSettings.ini, este comportamento será alterado para que as subpastas serão excluídas e apenas o conteúdo de "SecondFolder" será adicionado.  

 Para excluir subpastas aquando da correspondência contra grupos, tais como DriverGroup001, PackageGroup001 e assim sucessivamente, defina **SkipGroupSubFolders** para **Sim**.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não inclua subpastas aquando da correspondência contra grupos.|  
|**NÃO**|Inclua subpastas aquando da correspondência contra grupos. Este é o comportamento predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipGroupSubFolders=NO`|  

####  <a name="SkipLocaleSelection"></a>SkipLocaleSelection  
 Indica se o **seleção de região** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipPackageDisplay"></a>SkipPackageDisplay  
 Indica se o **pacotes** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=YES SkipLocaleSelection=NO`|  

####  <a name="SkipProductKey"></a>SkipProductKey  
 Indica se o **especificar a chave de produto necessária para instalar este sistema operativo** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipRearm"></a>SkipRearm  
 Esta propriedade é utilizada para configurar se o MDT rearms o 25 do Microsoft Office 2010\-período de tolerância de ativação do dia. Se o Microsoft Office 2010 é capturado uma imagem personalizada, o utilizador verá caixas de diálogo de notificação de ativação imediatamente depois da imagem é implementada em vez de 25\-dias após a implementação.  

 Por predefinição, o MDT rearms o 25 do Microsoft Office 2010\-tolerância de ativação de dia período quando executar o script de LTISysprep.wsf. Pode definir o valor desta propriedade como **Sim** para que o MDT ignora a rearming o 25 do Microsoft Office 2010\-período de tolerância de ativação do dia.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|MDT não rearmamento o 25 do Microsoft Office 2010\-período de tolerância de ativação do dia.|  
|**NÃO**|MDT rearms o 25 do Microsoft Office 2010\-período de tolerância de ativação do dia. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=Y SkipCapture=YES SkipAdminPassword=NO SkipProductKey=YES SkipRearm=YES DoCapture=YES`|  

####  <a name="SkipRoles"></a>SkipRoles  
 Indica se o **funções e funcionalidades** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=Yes SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipRoles=YES SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipSummary"></a>SkipSummary  
 Indica se o **pronto para começar a** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=Yes SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipTaskSequence"></a>SkipTaskSequence  
 Indica se o **Selecione uma sequência de tarefas para executar neste computador** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!NOTE]
>  Especifique o **SkipBuild** propriedade quando utilizar o Deployment Workbench para configurar o Assistente de implementação para ignorar o **Selecione uma sequência de tarefas para executar neste computador** página do assistente.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=NO SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipTimeZone"></a>SkipTimeZone  
 Indica se o **definir o fuso horário** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipTimeZone=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|  

####  <a name="SkipUserData"></a>SkipUserData  
 Indica se o **Especifique se pretende restaurar dados de utilizador** e **especificar onde pretende guardar as definições e dados** página do assistente é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentada a página do assistente e as informações nessa página não são recolhidas.|  
|**NÃO**|É apresentada a página do assistente e as informações na página de que são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|  

####  <a name="SkipWizard"></a>SkipWizard  
 Indica se todo o **Assistente de implementação** é ignorada.  

 Para outras propriedades que devem ser configuradas quando esta propriedade está definida como **Sim**, consulte [fornecer propriedades para páginas do Assistente de implementação ignorada](#ProvidingPropertiesforSkippedDeploymentWizardPages).  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**SIM**|Não é apresentado o Assistente de todo e nenhuma das informações nas páginas do assistente é recolhida.|  
|**NÃO**|É apresentado o assistente e as informações nas páginas do assistente ativada são recolhidas. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SkipWizard=YES`|  

####  <a name="SLShare"></a>SLShare  
 A pasta de rede partilhada em que os registos de implementação são armazenados no final do processo de implementação.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|\-||ZTI|\-|  

|**Valor**|**Descrição**|  
|-|-|
|*shared_folder*|O nome da pasta partilhada de rede no script de que os registos são armazenados|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO SkipAdminPassword=YES SkipProductKey=YES`|  

####  <a name="SLShareDynamicLogging"></a>SLShareDynamicLogging  
 A pasta partilhada de rede no qual MDT todos os registos devem ser escritos durante a implementação. Isto é utilizado para avançadas em tempo real de depuração só.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*shared_folder*|O nome da pasta partilhada de rede no script de que os registos são armazenados|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ SLShareDynamicLogging=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO SkipAdminPassword=YES SkipProductKey=YES`|  

####  <a name="SMSTSAssignUserMode"></a>SMSTSAssignUserMode  
 Especifica se a afinidade de dispositivo do utilizador (UDA) deve ser ativada e se é necessária aprovação. Esta propriedade só funciona com a funcionalidade UDA no Configuration Manager.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**Automática**|A afinidade entre um utilizador e o dispositivo de destino é estabelecida e aprovação é automaticamente executada.|  
|**Pendente**|A afinidade entre um utilizador e o dispositivo de destino é estabelecida e aprovação foi submetida para aprovação do administrador do Configuration Manager.|  
|**Desativar**|A afinidade entre um utilizador e o dispositivo de destino não for estabelecida.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SMSTSAssignUserMode=Auto SMSTSUdaUsers=Fabrikam\Ken, Fabrikam\Pilar`|  

####  <a name="SMSTSRunCommandLineUserName"></a>SMSTSRunCommandLineUserName  
 Especifica o nome de utilizador no *Domain\User_Name* formato deve ser utilizado com um **executar linha de comandos** passo que está configurado para ser executado como um utilizador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*user_name*|Especifica o nome de utilizador que deve ser utilizado com um **executar linha de comandos** passo|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SMSTSRunCommandLineUserName=Fabrikam\Ken SMSTSRunCommandLineUserPassword=<complex_password>`|  

####  <a name="SMSTSRunCommandLineUserPassword"></a>SMSTSRunCommandLineUserPassword  
 Especifica a palavra-passe que deve ser utilizada com um **executar linha de comandos** passo que está configurado para ser executado como um utilizador.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*user_password*|Especifica a palavra-passe que deve ser utilizada com um **executar linha de comandos** passo|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SMSTSRunCommandLineUserName=Fabrikam\Ken SMSTSRunCommandLineUserPassword=<complex_password>`|  

####  <a name="SMSTSUdaUsers"></a>SMSTSUdaUsers  
 Especifica os utilizadores que serão atribuídos afinidade com um dispositivo específico utilizando a funcionalidade UDA, que está disponível apenas no Configuration Manager.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*User1, Utilizador2,...*|A lista de valores separados por vírgulas de utilizadores na *Domain\User_Name* formato que será atribuído afinidade com o dispositivo de destino.<br /><br /> Nota:<br /><br /> Só pode utilizar o nome de domínio NetBIOS este valor, tal como *Fabrikam\Ken*. Não é possível utilizar o nome de domínio completamente qualificado (fabrikam.com\Ken) ou a notação de UPN (ken@fabrikam.com).|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SMSTSAssignUserMode=Auto SMSTSUdaUsers=Fabrikam\Ken, Fabrikam\Pilar`|  

####  <a name="SQLServer"></a>SQLServer  
 A identidade do computador a executar o SQL Server que executa uma consulta de base de dados que devolve valores de propriedade de colunas na tabela especificada no **tabela** propriedade. A consulta é com base nos parâmetros especificados no **parâmetros** e **ParameterCondition** propriedades. A instância do SQL Server no computador especificada no **instância** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*SQL_server*|O nome do computador com o SQL Server|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="SQLShare"></a>SQLShare  
 O nome de uma pasta partilhada no computador com o SQL Server (especificada pelo **SQLServer** propriedade). As credenciais utilizadas para autenticação são fornecidas pelo **UserDomain**, **UserID**, e **UserPassword** propriedades (para LTI e ZTI) ou pelo Configuration Manager Credenciais da conta cliente avançadas (ZTI apenas).  

> [!NOTE]
>  Esta propriedade tem de ser especificada para efetuar a autenticação integrada do Windows. Este é o método de autenticação recomendada, em vez de utilizar o **DBID** e **DBPwd** propriedades (que suportam o método de autenticação do SQL Server).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*shared_folder*|O nome de uma pasta partilhada no computador com o SQL Server|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default Properties=MyCustomProperty  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=MDT2010 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="StatePath"></a>StatePath  
 Esta propriedade é utilizada para definir o caminho onde serão armazenados os dados de migração de estado do utilizador, que pode ser um caminho UNC, um caminho local ou um caminho relativo. O [OSDStateStorePath](#OSDStateStorePath) propriedade tem precedência sobre a **StatePath** ou [UserDataLocation](#UserDataLocation) propriedade quando essas propriedades também são especificadas.  

> [!NOTE]
>  Esta propriedade é fornecida para retrocompatibilidade com versões anteriores do MDT. Utilize o [OSDStateStorePath](#UserDataLocation) propriedade em vez disso.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Caminho*|Será armazenado o caminho onde os dados de migração de estado do utilizador, que pode ser um caminho UNC, um caminho local ou um caminho relativo|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SitePath=\\fs1\Share\Replace ComputerBackupLocation=\\fs1\Share\ComputerBackup\Client01`|  

####  <a name="StoredProcedure"></a>StoredProcedure  
 O nome do procedimento armazenado utilizado durante a execução de uma consulta de base de dados que devolve valores de propriedade de colunas na tabela ou vista. O procedimento armazenado está localizado na base de dados especificada no **base de dados** propriedade. O computador com o SQL Server é especificado no **SQLServer** propriedade. A instância do SQL Server no computador especificada no **instância** propriedade. O nome do procedimento armazenado é especificado no **StoredProcedure** propriedade.  

 Para obter mais informações sobre como utilizar um procedimento armazenado para consultar uma base de dados do SQL Server, consulte a secção "A implementar aplicações com base na aplicação versões anteriores", no MDT documentar *guia de amostras do Toolkit de implementação do Microsoft*.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*stored_procedure*|O nome do procedimento armazenado utilizado para consultar a base de dados do SQL Server|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=DynamicPackages, Default  [Default] OSInstall=YES  [DynamicPackages] SQLDefault=DB_DynamicPackages  [DB_DynamicPackages] SQLServer=SERVER1 Database=MDTDB StoredProcedure=RetrievePackages Parameters=MacAddress SQLShare=Logs Instance=MDT2013 Port=1433 Netlib=DBNMPNTW`|  

####  <a name="SupportsHyperVRole"></a>SupportsHyperVRole  
 Especifica se os recursos do processador no computador de destino podem suportar a função de servidor Hyper-V no Windows Server. Esta propriedade é verdadeiro se o valor para as seguintes propriedades estiver definido como **verdadeiro**:  

-   **SupportsNX**  

-   **SupportsVT**  

-   **Supports64Bit**  

 Cada uma das propriedades anteriores é definida utilizando informações a partir de **CPUID** interface. Para obter as informações recolhidas sobre as VMs e informações devolvidos pelo **CPUID** interface, consulte as seguintes propriedades:  

-   **IsHypervisorRunning**  

-   **IsVM**  

-   **SupportsNX**  

-   **SupportsVT**  

-   **Supports64Bit**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Recursos do processador do computador de destino podem suportar a função de servidor Hyper-V no Windows Server.|  
|**FALSO**|Recursos do processador do computador de destino não suportam a função de servidor Hyper-V no Windows Server.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="SupportsNX"></a>SupportsNX  
 Especifica se os recursos do processador no computador de destino suportarem a tecnologia de não execução (NX). A tecnologia NX é utilizada nos processadores para segregar as áreas de memória para utilização por qualquer um dos armazenamento de instruções de processador (código) ou para armazenamento de dados. Esta propriedade for definida utilizando informações a partir de **CPUID** interface.  

 Para obter as informações recolhidas sobre as VMs e informações devolvidos pelo **CPUID** interface, consulte as seguintes propriedades:  

-   **IsHypervisorRunning**  

-   **IsVM**  

-   **SupportsHyperVRole**  

-   **SupportsVT**  

-   **Supports64Bit**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Recursos do processador do computador de destino suportam tecnologia NX.|  
|**FALSO**|Recursos do processador do computador de destino não suportam a tecnologia NX.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="SupportsVT"></a>SupportsVT  
 Especifica se os recursos do processador no computador de destino suportam a funcionalidade de tecnologia de Virtualização (VT). VT é utilizada para suportar ambientes virtualizados atuais, como o Hyper-V. Esta propriedade é definida com informações da CPUID interface.  

 Para obter informações adicionais recolhidas sobre VMs e as informações devolvidas a partir da interface do CPUID, consulte as seguintes propriedades:  

-   **IsHypervisorRunning**  

-   **IsVM**  

-   **SupportsHyperVRole**  

-   **SupportsNX**  

-   **Supports64Bit**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Recursos do processador do computador de destino suportam tecnologia VT.|  
|**FALSO**|Recursos do processador do computador de destino não suportam a tecnologia de VT.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="Supports64Bit"></a>Supports64Bit  
 Especifica se os recursos do processador no computador de destino suportam sistemas operativos Windows de 64 bits. Ambientes de Virtualização mais modernos necessitam de arquitetura de processador de 64 bits. Esta propriedade for definida utilizando informações a partir de **CPUID** interface.  

 Para obter as informações recolhidas sobre as VMs e informações devolvidos pelo **CPUID** interface, consulte as seguintes propriedades:  

-   **IsHypervisorRunning**  

-   **IsVM**  

-   **SupportsHyperVRole**  

-   **SupportsNX**  

-   **SupportsVT**  

-   **VMPlatform**  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Recursos do processador do computador de destino suportam um sistema operativo do Windows de 64 bits.|  
|**FALSO**|Recursos do processador do computador de destino não suportam um sistema operativo do Windows de 64 bits.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="SysVolPath"></a>SysVolPath  
 Especifica o caminho completamente qualificado de não UNC para um diretório num disco fixo no computador local.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*caminho*|Especifica o caminho completamente qualificado de não UNC para um diretório num disco fixo no computador local|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] SysVolPath=%DestinationLogicalDrive%\Windows\Sysvol`|  

####  <a name="Table"></a>Tabela  
 O nome da tabela ou vista para ser utilizado na execução de uma consulta de base de dados que devolve valores de propriedade de colunas na tabela ou vista. A consulta é com base nos parâmetros especificados no **parâmetros** e **ParameterCondition** propriedades. A tabela ou vista está localizada na base de dados especificada no **base de dados** propriedade. O computador com o SQL Server é especificado no **SQLServer** propriedade. A instância do SQL Server no computador especificada no **instância** propriedade.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome_tabela*|O nome da tabela ou vista para ser consultado para valores de propriedade|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=MDT2010 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|  

####  <a name="TaskSequenceID"></a>TaskSequenceID  
 Identifica a sequência de tarefas do sistema operativo ser implementado no computador de destino. O ID de sequência de tarefas é criado no nó sequências de tarefas no Deployment Workbench. O **TaskSequenceID** propriedade permite apenas carateres alfanuméricos, hífenes (-) e carateres de sublinhado (\_). O **TaskSequenceID** propriedade não pode estar em branco ou conter espaços.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*task_sequence_id*|Identificador da sequência de tarefas de sistema operativo definida no Deployment Workbench para o sistema de operativo de destino que está a ser implementada<br /><br /> Nota:<br /><br /> Certifique-se de utilizar o **TaskSequenceID** especificado na IU do Workbench a implementação, não o GUID do **TaskSequenceID**.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] TaskSequenceID=BareMetal`|  

####  <a name="TaskSequenceName"></a>TaskSequenceName  
 Especifica o nome da sequência de tarefas a ser executado.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*task_sequence_name*|Nome da sequência de tarefas a ser executada, tais como implementar *Windows 8.1 para o computador de referência*|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="TaskSequenceVersion"></a>TaskSequenceVersion  
 Especifica a versão da sequência de tarefas a ser executada.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*task_sequence_version*|Versão da sequência de tarefas a ser executada, tais como *1.00*|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="TimeZoneName"></a>TimeZoneName  
 O fuso horário no qual está localizado o computador de destino. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*time_zone_name*|O valor de texto que indica o fuso horário onde está localizado o computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] TimeZoneName=Pacific Standard Time DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE`|  

####  <a name="ToolRoot"></a>ToolRoot  
 Especifica o caminho UNC para as ferramentas\\*proc_arch* pasta (onde *proc_arch* é a arquitetura de processador do sistema operativo em execução e pode ter um valor de **x86** ou **x64**), que é imediatamente abaixo da raiz da estrutura da pasta especificada no **DeployRoot** propriedade. As ferramentas\\*proc_arch* pasta contém utilitários que utiliza o MDT durante o processo de implementação.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*caminho*|O UNC ou o caminho local para as ferramentas\\*proc_arch* pasta (onde *proc_arch* é a arquitetura de processador do sistema operativo em execução e pode ter um valor de  **x86** ou **x64**) imediatamente abaixo da raiz da estrutura da pasta especificada pelo **DeployRoot** propriedade|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="TPMOwnerPassword"></a>TPMOwnerPassword  
 A palavra-passe do TPM (também conhecido como o *palavra-passe de administração de TPM*) para o proprietário do computador de destino. A palavra-passe pode ser guardada num ficheiro ou armazenada no AD DS.  

> [!NOTE]
>  Se a propriedade TPM já está definida ou não é permitida a propriedade do TPM, em seguida, a **TPMOwnerPassword** propriedade é ignorada. Se não for necessária a palavra-passe TPM e **TPMOwnerPassword** propriedade não for fornecida, a palavra-passe TPM é definida para a palavra-passe de administrador local.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|A palavra-passe TPM para o proprietário do computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=TRUE BDEKeyLocation=C: TPMOwnerPassword=<complex_password> BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|  

####  <a name="UDDir"></a>UDDir  
 A pasta na qual os dados de migração de estado do utilizador estão armazenados. Esta pasta existe sob a pasta partilhada de rede especificada no **UDShare**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*pasta*|O nome da pasta existente sob a pasta partilhada de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|  

####  <a name="UDProfiles"></a>UDProfiles  
 Uma lista delimitada por vírgulas de perfis de utilizador que têm de ser guardado pelo Scanstate.exe durante a fase de captura de estado.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*user_profiles*|A lista de perfis de utilizador a ser guardadas, separados por vírgulas|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|  

####  <a name="UDShare"></a>UDShare  
 A partilha de rede onde os dados de migração de estado de utilizador estão armazenados.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*UNC_path*|O caminho UNC para a partilha de rede armazenar dados de migração de estado de utilizador|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|  

####  <a name="UILanguage"></a>UILanguage  
 O idioma predefinido a ser utilizado com o sistema operativo de destino. Se não for especificado, o **Assistente de implementação** utiliza o idioma configurado na imagem a ser implementada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*UI_language*|O idioma predefinido para o sistema operativo no computador de destino|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us UILanguage=en-us KeyboardLocale=0409:00000409`|  

####  <a name="UserDataLocation"></a>UserDataLocation  
 A localização na qual o USMT armazena dados de migração de estado do utilizador.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|Em branco|Se **UserDataLocation**não for especificado ou se for deixado em branco, o Assistente de implementação será predefinida para utilizar o comportamento automático.|  
|*UNC_path*|O caminho UNC para a pasta de rede partilhada onde os dados de migração de estado do utilizador são armazenados.|  
|**AUTOMÁTICA**|Os scripts de implementação armazenam dados de migração de estado do utilizador num disco rígido local, se espaço disponível. Caso contrário, os dados de migração de estado do utilizador são guardados numa localização de rede, que é especificada no **UDShare** e **UDDir** propriedades.|  
|**REDE**|Os dados de migração de estado do utilizador são armazenados na localização designada pelo **UDShare** e **UDDir** propriedades.|  
|**NENHUM**|Os dados de migração de estado de utilizador não são guardados.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% UserDataLocation=NETWORK DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|  

####  <a name="UserDomain"></a>UserDomain  
 O domínio em que as credenciais de um utilizador (especificado no **UserID** propriedade) residem.  

> [!NOTE]
>  Para uma implementação LTI totalmente automatizada, fornece esta propriedade no CustomSettings.ini e BootStrap.ini. No entanto, tenha em atenção que a armazenar as credenciais do utilizador nesses ficheiros armazena as credenciais em texto não encriptado e, por conseguinte, não é segura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*domínio*|O nome do domínio onde residem as credenciais da conta de utilizador|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC Help Desk Staff UserPassword=<complex_password>`|  

####  <a name="UserID"></a>ID de utilizador  
 As credenciais de utilizador para aceder a recursos de rede.  

> [!NOTE]
>  Para uma implementação LTI totalmente automatizada, fornece esta propriedade no CustomSettings.ini e BootStrap.ini. No entanto, tenha em atenção que a armazenar as credenciais do utilizador nesses ficheiros armazena as credenciais em texto não encriptado e, por conseguinte, não é segura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*USER_ID*|O nome das credenciais da conta de utilizador utilizada para aceder os recursos de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC-HelpDesk UserPassword=<complex_password>`|  

####  <a name="UserLocale"></a>UserLocale  
 A região do utilizador a ser utilizado com o sistema operativo de destino. Se não for especificado, o **Assistente de implementação** utiliza a região do utilizador configurada na imagem a ser implementada.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*user_locale*|A região do utilizador no computador de destino. O valor for especificado como um valor de texto (en-us).|  

|**Exemplo 1**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=0409:00000409`|  

|**Exemplo 2**|  
|-|  
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=en-us`|  

####  <a name="UserPassword"></a>UserPassword  
 A palavra-passe para as credenciais de utilizador especificado no **UserID** propriedade.  

> [!NOTE]
>  Para uma implementação LTI totalmente automatizada, fornece esta propriedade no CustomSettings.ini e BootStrap.ini. No entanto, tenha em atenção que a armazenar as credenciais do utilizador nesses ficheiros armazena as credenciais em texto não encriptado e, por conseguinte, não é segura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|-||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*user_password*|A palavra-passe para as credenciais da conta de utilizador|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC-HelpDesk UserPassword=<complex_password>`|  

####  <a name="USMTConfigFile"></a>USMTConfigFile  
 O ficheiro XML de configuração do USMT que deve ser utilizado ao executar **Scanstate** e **Loadstate**.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*USMTConfigFile*|O nome do ficheiro de configuração XML que deve ser utilizado ao executar Scanstate.exe e Loadstate.exe|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTMigFiles1=MigApp.xml USMTMigFiles2=MigUser.xml USMTMigFiles3=MigSys.xml USMTMigFiles4=MigCustom.xml USMTConfigFile=USMTConfig.xml UserDataLocation=NONE`|  

####  <a name="USMTLocal"></a>USMTLocal  
 Esta propriedade especifica se as informações de estado de utilizador do USMT são armazenadas localmente no computador de destino. Esta propriedade é utilizada principalmente pelo [ZTIUserState.wsf](#ZTIUserState.wsf) e [ZTIBackup.wsf](#ZTIBackup.wsf) scripts para indicar que o **solicitar armazenamento de Estados** e **estado da versão Arquivo** passos de sequência de tarefas para implementações do Configuration Manager são ignorados. Para obter mais informações, consulte o [OSDStateStorePath](#OSDStateStorePath) propriedade.  

> [!NOTE]
>  Esta propriedade só deve ser utilizada em circunstância descrita a [OSDStateStorePath](#OSDStateStorePath) propriedade).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI||  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|As informações de estado de utilizador do USMT são armazenadas localmente no computador de destino e o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** os passos de sequência de tarefas são ignorados.|  
|**FALSO**|As informações de estado de utilizador do USMT não são armazenadas localmente no computador de destino e o **solicitar armazenamento de Estados** e **disponibilizar armazenamento de Estados** passos de sequência de tarefas são executados.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTLocal=TRUE USMTMigFiles001=MigApp.xml USMTMigFiles002=MigUser.xml USMTMigFiles003=MigSys.xml USMTMigFiles004=MigCustom.xml UserDataLocation=NONE`|  

####  <a name="USMTMigFiles"></a>USMTMigFiles  
 Uma lista de ficheiros no formato XML que são utilizadas pelo USMT (Scanstate.exe) para identificar informações de migração de estado do utilizador sejam guardados. Quando esta propriedade não for especificada, o script de ZTIUserState.wsf utiliza MigApp.xml, MigUser.xml e MigSys.xml. Caso contrário, ZTIUserState.wsf utiliza os ficheiros explicitamente referenciados nesta propriedade. O **USMTMigFiles** propriedade tem um sufixo numérico (por exemplo, **USMTMigFiles001** ou **USMTMigFiles002**).  

> [!NOTE]
>  Utilize esta propriedade para especificar os ficheiros XML a serem utilizadas pelo Scanstate.exe em vez de utilizar o **i** parâmetro o **ScanStateArgs** propriedade. Isto impede que o script de ZTIUserState.wsf potencialmente duplicar a mesma lista de ficheiros XML.  

> [!NOTE]
>  Este nome de propriedade pode ser especificada utilizando dígito nomenclature (**USMTMigFiles1**) ou nomenclature triple-dígitos (**USMTMigFiles001**).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*USMTMigFile*|O nome do ficheiro. XML a ser utilizada como entrada para Scanstate.exe, em linhas separadas. Se não for especificado, a predefinição é MigApp.xml, MigUser.xml e MigSys.xml.<br /><br /> Nota:<br /><br /> Se este valor for especificado, os ficheiros predefinidos (MigApp.xml, MigUser.xml e MigSys.xml) devem também ser adicionados à lista, se estes ficheiros estão a ser incluído.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTMigFiles001=MigApp.xml USMTMigFiles002=MigUser.xml USMTMigFiles003=MigSys.xml USMTMigFiles004=MigCustom.xml UserDataLocation=NONE`|  

####  <a name="USMTOfflineMigration"></a>USMTOfflineMigration  
 Esta propriedade determina se o MDT utiliza USMT para efetuar uma migração de estado do utilizador offline. Numa migração offline, a captura é executada no Windows PE em vez do sistema operativo existente.  

 Está a utilizar a migração offline USMT é efetuado para:  

-   UDI sempre, independentemente da definição do **USMTOfflineMigration** propriedade  

-   ZTI apenas para o cenário de implementação do MDT atualizar computador e apenas quando o **USMTOfflineMigration** propriedade está definida como **"TRUE"**  

    > [!NOTE]
    >  Não é possível efetuar a migração de estado de utilizador offline USMT no cenário de implementação MDT novo computador utilizando ZTI.  

-   LTI para o:  

    1.  Cenário de implementação do MDT novo computador utilizando o **mover dados e definições** página do assistente no Assistente de implementação  

    2.  Cenário de implementação do MDT atualizar computador e apenas quando o **USMTOfflineMigration** propriedade está definida como **"TRUE"**  

 Para obter mais informações sobre como utilizar o MDT e USMT para efetuar uma migração de estado do utilizador offline, consulte "Configurar o USMT Offline migração estado do utilizador".  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|MDT utiliza a USMT para efetuar uma migração de estado do utilizador offline.|  
|*Qualquer outro valor*|MDT não efetuar uma migração de estado do utilizador offline. Em vez disso, a migração de estado do utilizador é captada no sistema operativo existente. Este é o valor predefinido.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] OSInstall=YES SkipUserData=YES USMTOfflineMigration=TRUE DoNotFormatAndPartition=YES OSDStateStorePath=\\WDG-MDT-01\StateStore$`|  

####  <a name="UUID"></a>UUID  
 O Universal exclusivo identificador (UUID) armazenados no BIOS de gestão do sistema do computador de destino.  

 O formato do UUID é um valor de 16 bytes com dígitos hexadecimais no seguinte formato: *12345678-1234-1234-1234-123456789ABC*. Utilize esta propriedade para criar uma subsecção que contenha definições direcionadas para um computador específico.  

> [!NOTE]
>  Esta propriedade dinamicamente é definida pelos scripts de MDT e não pode ter o respetivo valor definido no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura. No entanto, pode utilizar esta propriedade no CustomSettings.ini ou da base de dados do MDT, conforme ilustrado nos exemplos seguintes, para ajudar a definir a configuração do computador de destino.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*UUID*|O UUID do computador de destino|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="ValidateDomainCredentialsUNC"></a>ValidateDomainCredentialsUNC  
 Esta propriedade é utilizada para especificar um caminho UNC para uma pasta partilhada de rede que é utilizado para validar as credenciais fornecidas para associar o computador de destino a um domínio. As credenciais que está a ser validadas estão especificadas no **DomainAdmin**, **DomainAdminDomain**, e **DomainAdminPassword** propriedades.  

> [!NOTE]
>  Certifique-se de que não existem outras propriedades no MDT utilizam o servidor de partilhar a pasta nesta propriedade. Utilizar um servidor que já é referenciado por outras propriedades do MDT pode resultar em inadequada validação das credenciais.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*unc_path*|Especifica o caminho completamente qualificado de UNC para uma pasta partilhada de rede|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] ValidateDomainCredentialsUNC=\\wdg-fs-01\Source$`|  

####  <a name="VHDCreateDiffVHD"></a>VHDCreateDiffVHD  
 Esta propriedade é utilizada para especificar o nome de um VHD de diferenciação (também conhecido como um *subordinado VHD*) ficheiros. Um VHD de diferenciação é semelhante a um VHD de expansão dinâmica mas contém apenas os blocos de disco modificação do VHD do principal associado. O elemento principal VHD é só de leitura, pelo que tem de modificar o VHD de diferenciação. O ficheiro VHD de diferenciação é criado na mesma pasta, como o VHD principal do ficheiro, apenas o nome de ficheiro é especificado nesta propriedade. Esta propriedade só é válida para o cenário de implementação do MDT novo computador.  

> [!NOTE]
>  Todos os ficheiros VHD principal criados pelo MDT são armazenados na pasta VHD na raiz da unidade principal.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar Virtual disco rígido (VHD)** tipo de sequência de tarefas. Pode substituir o valor de **criar Virtual disco rígido (VHD)** passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*nome de ficheiro*|Especifica o nome do ficheiro VHD diferenciação, que está localizado na mesma pasta que o ficheiro VHD principal<br /><br /> O ficheiro VHD de diferenciação não pode ter o mesmo nome que o ficheiro VHD principal.|  
|**ALEATÓRIO**|Gera automaticamente um nome aleatório para o ficheiro VHD de diferenciação, que está localizado na mesma pasta que o ficheiro VHD principal|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VHDCreateDiffVHD=Win7Diff_C.vhd VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDCreateFileName"></a>VHDCreateFileName  
 Esta propriedade é utilizada para especificar o nome de um ficheiro VHD. O tipo de ficheiro VHD baseia-se no valor da **VHDCreateType** propriedade. A propriedade só inclui o nome de ficheiro, não o caminho para o nome de ficheiro e só é válida para o cenário de implementação do MDT novo computador.  

> [!NOTE]
>  Os ficheiros VHD criados pelo MDT são armazenados na pasta VHD na raiz da unidade principal.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar Virtual disco rígido (VHD)** tipo de sequência de tarefas. Pode substituir o valor de **criar Virtual disco rígido (VHD)** passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*file_name*|Especifica o nome do ficheiro VHD|  
|**ALEATÓRIO**|Gera automaticamente um nome aleatório para o ficheiro VHD, o que está localizado na pasta VHD na raiz da unidade principal|  
|Em branco|Mesmo um **aleatório**|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDCreateSizeMax"></a>VHDCreateSizeMax  
 Esta propriedade é utilizada para especificar o tamanho máximo do ficheiro VHD em megabytes (MB). O tamanho do ficheiro VHD no momento da criação baseia-se no tipo de ficheiro VHD a ser criado. Para obter mais informações, consulte o [VHDCreateType](#VHDCreateType) propriedade. Esta propriedade só é válida para o cenário de implementação do MDT novo computador.  

> [!NOTE]
>  Se esta propriedade não for especificada, o valor predefinido para o tamanho máximo do ficheiro VHD é de 90% do espaço de disco disponível no disco principal.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar Virtual disco rígido (VHD)** tipo de sequência de tarefas. Pode substituir o valor que o **criar Virtual disco rígido (VHD)** passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*tamanho*|O tamanho máximo do ficheiro VHD especificado em MB. Por exemplo, 130,048 MB é igual a 127 GB. O valor predefinido é de 90% do espaço de disco disponível no disco principal.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=FIXED VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDCreateSource"></a>VHDCreateSource  
 Esta propriedade é utilizada para especificar o nome de um ficheiro VHD que é utilizado como um modelo (origem) para criar um novo ficheiro VHD. Pode especificar o nome de ficheiro com um caminho UNC, o caminho local, o caminho relativo ou apenas o nome de ficheiro. Se apenas o nome de ficheiro for especificado, o MDT tenta localizar o ficheiro VHD no computador de destino. Esta propriedade só é válida para o cenário de implementação do MDT novo computador.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar Virtual disco rígido (VHD)** tipo de sequência de tarefas. Pode substituir o valor que o **criar Virtual disco rígido (VHD)**passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|O nome de ficheiro, que pode ser especificado utilizando um caminho UNC, o caminho local, o caminho relativo ou apenas o nome de ficheiro. Se apenas o nome de ficheiro for especificado, o MDT tenta localizar o ficheiro VHD no computador de destino.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateSource=\\wdg-mdt-01\vhds\win7_template.vhd VHDCreateType=FIXED VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDCreateType"></a>VHDCreateType  
 Esta propriedade é utilizada para especificar o tipo de ficheiro VHD que é especificado o **VHDCreateFileName** propriedade e pode ser um dos seguintes tipos de ficheiro VHD:  

-   **Ficheiro VHD fixo**. Para este tipo VHD, o tamanho do VHD especificado durante a criação do atribuída e não se altera automaticamente após a criação. Por exemplo, se criar um 24\-gigabyte \(GB\) corrigido ficheiro VHD, o ficheiro será aproximadamente 24 GB \(com algum espaço utilizado para a estrutura interna do VHD\) , independentemente da quantidade informações são armazenadas no ficheiro VHD.  

-   **Ficheiro VHD de expansão dinâmica**. Para este tipo VHD, é atribuída apenas numa pequena percentagem do tamanho do VHD especificado no momento de criação. Em seguida, o ficheiro VHD continua a crescer como informações mais são armazenadas na mesma. No entanto, o ficheiro VHD não é possível aumentar o tamanho especificado durante a criação. Por exemplo, se criar um VHD de expansão dinâmica de GB 24, irá ser pequeno durante a criação. No entanto, como informações são armazenadas no ficheiro VHD, o ficheiro continuará a aumentar, mas nunca exceder o tamanho máximo de 24 GB.  

 Esta propriedade só é válida para o cenário de implementação do MDT novo computador.  

> [!NOTE]
>  O tamanho máximo do ficheiro VHD especificado no **VHDCreateSizeMax** propriedade.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar disco rígido Virtual \(VHD\)**  tipo de sequência de tarefas. Pode substituir o valor que o **criar disco rígido Virtual \(VHD\)**  passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|**EXPANSÍVEL**|Cria um ficheiro VHD fixo|  
|**FIXO**|Cria um ficheiro VHD de expansão dinâmica|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDDisks"></a>VHDDisks  
 Esta propriedade contém uma lista de números de unidade física atribuídas para ficheiros VHD separados por espaços. Sempre que é criado um ficheiro VHD, MDT adiciona o índice de disco do disco recentemente criado para esta propriedade utilizando o **índice** propriedade o **Win32\_DiskDrive** classe WMI.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar disco rígido Virtual \(VHD\)**  tipo de sequência de tarefas. Pode substituir o valor que o **criar disco rígido Virtual \(VHD\)**  passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*index1 index2 index3*|Uma lista de números de unidade física atribuídas para os ficheiros VHD separados por espaços — por exemplo, *1 2 5*.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VHDInputVariable"></a>VHDInputVariable  
 Esta propriedade contém uma variável que contém a unidade no computador de destino onde os ficheiros VHD serão criados. MDT cria ficheiros VHD na pasta VHD na raiz nesta unidade.  

> [!NOTE]
>  Se esta propriedade for omitida, o MDT tenta criar os ficheiros VHD na pasta do VHD na raiz da unidade de sistema primeiro.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar disco rígido Virtual \(VHD\)**  tipo de sequência de tarefas. Pode substituir o valor que o **criar disco rígido Virtual \(VHD\)**  passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDrives**  

-   **VHDOutputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*variável*|Variável que contém a letra de unidade no computador de destino onde os ficheiros VHD serão criados. MDT cria ficheiros VHD na pasta VHD na raiz nesta unidade. Por exemplo, se esta propriedade tem um valor de **VHDTargetDisk**, a **VHDTargetDisk** propriedade contém a letra de unidade \(como *H*\).|  

|**Exemplo**|  
|-|  
|`VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd  VHDInputVariable=VHDTargetDisk`|  

####  <a name="VHDOutputVariable"></a>VHDOutputVariable  
 Esta propriedade contém uma variável que contém o número de unidade física que lhe foi atribuído ao ficheiro VHD recentemente criado. Sempre que é criado um ficheiro VHD, MDT define esta propriedade para o índice de disco da utilização de disco criado recentemente o **índice** propriedade o **Win32\_DiskDrive** classe WMI.  

 Esta propriedade for definida normalmente utilizando um passo de sequência de tarefas criado utilizando o **criar disco rígido Virtual \(VHD\)**  tipo de sequência de tarefas. Pode substituir o valor que o **criar disco rígido Virtual \(VHD\)**  passo de sequência de tarefas define ao configurar esta propriedade no CustomSettings.ini.  

> [!NOTE]
>  Para configurar esta propriedade no CustomSettings.ini, tem de adicionar esta propriedade para o **propriedades** linha no CustomSettings.ini.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDTargetDisk**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|\-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Variável*|Variável será contém o número de unidade física atribuído para o ficheiro VHD recentemente criado. Por exemplo, se esta propriedade tem um valor de **OSDDiskIndex**, a **OSDDiskIndex** propriedade irá conter o número de unidade física atribuído para o ficheiro VHD recém-criado \(como *4*\).|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VHDTargetDisk"></a>VHDTargetDisk  
 Especifica a unidade no computador de destino onde é possível criar o VHD. Esta propriedade é referenciada mais tarde a [VHDInputVariable](#VHDInputVariable) propriedade.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

 Para as propriedades relacionadas que são utilizadas com ficheiros VHD, consulte:  

-   **VHDCreateDiffVHD**  

-   **VHDCreateFileName**  

-   **VHDCreateSizeMax**  

-   **VHDCreateSource**  

-   **VHDCreateType**  

-   **VHDDisks**  

-   **VHDInputVariable**  

-   **VHDOutputVariable**  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|\-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*Disco*|Especifica a unidade onde é possível criar o VHD|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VMHost"></a>VMHost  
 Especifica o nome da Hyper\-anfitrião V que execute a VM onde MDT está em execução. Esta propriedade só está disponível quando o Hyper\-V componentes de integração estão instalados e em execução.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

Tabela 4 apresenta uma lista de sistemas operativos do Windows que MDT suporta e os respetivos Hyper correspondente\-suporta componentes de integração V.  

### <a name="table-4-windows-operating-systems-and-hyper-v-integration-components-support"></a>Tabela 4. Sistemas operativos Windows e suporte de componentes de integração do Hyper-V  

|**Sistema operativo**|**Componentes de integração de Hyper-V**|  
|-|-|  
|Windows PE|Componentes de integração não estão disponíveis.|  
|Windows 7|Está disponível por predefinição nas edições Enterprise, Ultimate e profissionais.|  
|Windows Server 2008 R2|Está disponível por predefinição em todas as edições.|  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*Nome*|O nome do anfitrião Hyper-V que executa a VM onde MDT está em execução|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VMName"></a>VMName  
 Especifica o nome da VM onde MDT está em execução. Esta propriedade só está disponível quando os componentes de integração do Hyper-V estão instalados e em execução.  

 Tabela 5 apresenta uma lista de sistemas operativos Windows suportados pelo MDT e o respetivo suporte de componentes de integração do Hyper-V correspondente.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

### <a name="table-5-windows-operating-systems-and-hyper-v-integration-components-support"></a>Tabela 5. Sistemas operativos Windows e suporte de componentes de integração do Hyper-V  

|**Sistema operativo**|**Componentes de integração de Hyper-V**|  
|-|-|  
|Windows PE|Componentes de integração não estão disponíveis.|  
|Windows 7|Está disponível por predefinição nas edições Enterprise, Ultimate e profissionais.|  
|Windows Server 2008 R2|Está disponível por predefinição em todas as edições.|  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*nome*|O nome da VM onde MDT está em execução|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VMPlatform"></a>VMPlatform  
 Especifica informações específicas sobre o ambiente de Virtualização do computador de destino quando o computador de destino é uma VM. A plataforma VM é determinada através da utilização de WMI.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**Hyper-V**|Hyper-V|  
|**VirtualBox**|Caixa virtual|  
|**VMware**|Plataforma de Virtualização VMware|  
|**Xen**|Servidor do Citrix Xen|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="VRefresh"></a>VRefresh  
 Vertical taxa de atualização para o monitor no computador de destino. A taxa de atualização vertical é especificada em Hertz. No exemplo, o valor **60** indica que a taxa de atualização vertical do monitor é 60 Hz. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

> [!NOTE]
>  Os valores predefinidos (no ficheiro de modelo Unattend.xml) são resolução horizontal de 1.024 pixéis, resolução vertical 768 pixéis, profundidade de cor de 32 bits e velocidade de atualização vertical 60 Hz.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*refresh_rate*|Vertical taxa de atualização para o monitor no computador de destino no Hertz|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|  

####  <a name="VSSMaxSize"></a>VSSMaxSize  
 Esta propriedade é utilizada para transferir um valor para o **maxsize** parâmetro o **vssadmin redimensionar shadowstorage** comando no **Vssadmin** comando. O **maxsize** parâmetro é utilizado para especificar a quantidade máxima de espaço no volume de destino que pode ser utilizado para armazenar as cópias sombra. Para mais informações sobre o **maxsize** parâmetro, consulte [Vssadmin redimensionar shadowstorage](http://technet.microsoft.com/library/cc788050\(WS.10\).aspx).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*maxsize_value*|Especifica a quantidade máxima de espaço que pode ser utilizada para armazenar as cópias sombra. O valor pode ser especificado em bytes ou como uma percentagem do volume de destino.<br /><br /> Para especificar o valor:<br /><br /> -Em bytes, o valor tem de ser 300 MB ou superior e aceite os seguintes sufixos: KB, MB, GB, TB, PB e EB. Também pode utilizar o B, K, M, G, T, P e i como sufixos — por exemplo:<br /><br /> `VSSMaxSize=60G`<br /><br /> -A como uma percentagem, utilize o caráter de % como o sufixo ao valor numérico — por exemplo:<br /><br /> `VSSMaxSize=20%`<br /><br /> Nota:<br /><br /> Se não for fornecido um sufixo, o sufixo de predefinido é bytes. Por exemplo, `VSSMaxSize=1024` indica que o **VSSMaxSize** será definida para 1.024 bytes.<br /><br /> Se o valor estiver definido como **UNBOUNDED**, em seguida, não há nenhum limite colocada a quantidade de espaço de armazenamento que pode ser utilizada — por exemplo:<br /><br /> `VSSMaxSize=UNBOUNDED`|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] VSSMaxSize=25%`|  

####  <a name="WDSServer"></a>WDSServer  
 O computador a executar o serviços de implementação do Windows que é utilizado para instalar serviços de implementação de imagens. O valor predefinido é o servidor executar serviços de implementação do Windows de que a imagem foi iniciada.  

> [!NOTE]
>  Esta propriedade está definida dinamicamente pelos MDT scripts e não está configurada no CustomSettings.ini ou da base de dados do MDT. Trate esta propriedade como só de leitura.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*WDS_server*|O nome do computador a executar o serviços de implementação do Windows|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="WindowsSource"></a>WindowsSource  
 MDT utiliza esta propriedade para definir a localização da pasta sources\sxs na pasta de rede partilhada que contém os ficheiros de origem do sistema operativo. Esta propriedade é utilizada quando:  

-   O MDT é execução de uma sequência de tarefas personalizada ou implementar uma imagem personalizada  

-   MDT está a instalar funções ou funcionalidades no Windows 8 e Windows Server 2012  

-   O computador não tem acesso à Internet  

 Quando a situação descrita na lista com marcas acima ocorre, MDT poderá não ser possível localizar o sistema operativo localmente os ficheiros de origem e a instalação irá tentar transferir os ficheiros a partir da Internet. Porque o computador não tem acesso à Internet, o processo irá falhar. Definir esta propriedade para o valor adequado ajuda a impedir que este problema ocorra.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|***folder_unc***|Um caminho UNC para a pasta de Sources\sxs para o sistema operativo que está a ser implementada.<br /><br /> Nota:<br /><br /> O caminho UNC tem de incluir a pasta de Sources\sxs.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WindowsSource=%DeployRoot%\Operating Systems\Windows 8\Sources\sxs`|  

####  <a name="WipeDisk"></a>WipeDisk  
 Especifica se o disco deve ser eliminado. Se **WipeDisk** for TRUE, o script de ZTIWipeDisk.wsf irá limpar o disco utilizando o **formato** comando. O **formato** comando não é a forma mais "segura" de limpeza do disco.  

 Eliminar em segurança o disco deve ser feito de forma que se segue EUA Departamento da defesa padrão 5220.22-M, quais os Estados "para limpar magnéticas discos, substituir todas as localizações de três vezes (pela primeira vez com um caráter, segunda vez ao respectivo complemento e a hora terceira com um caráter aleatório)."  

 Quando o MDT apaga o disco, utiliza o **formato** comando com o **/P:3** comutador, que dá instruções ao **formato** zero cada setor no volume e realizar a operação de três vezes. Não é possível dizer o **formato** comando para utilizar um caráter específico ou um caráter aleatório.  

> [!NOTE]
>  Se o disco tem de ser eliminado em segurança, uma ferramenta de limpeza do disco segura não sejam da Microsoft deve ser adicionada para a sequência de tarefas utilizando o **executar linha de comandos** passo de sequência de tarefas.  

> [!CAUTION]
>  Este valor da propriedade tem de ser especificado em letras maiúsculas, para que os scripts de implementação podem lê-lo corretamente.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|Se **WipeDisk** está definido como **verdadeiro**, será formatada Win32_DiskPartition em DiskIndex 0 e no índice 0.|  
|**FALSO**|O disco não será formatado.|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WipeDisk=TRUE`|  

####  <a name="WizardSelectionProfile"></a>WizardSelectionProfile  
 Nome de perfil utilizado pelo Assistente para a apresentação de vários itens de filtragem.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*profile_name*|Nome de perfil utilizado pelo Assistente para a apresentação de vários itens de filtragem|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WizardSelectionProfile=SelectTaskSequenceOnly`|  

####  <a name="WSUSServer"></a>WSUSServer  
 Este é o nome do servidor Windows Server Update Services (WSUS) que o computador de destino deve utilizar quando ao analisar, transferir e instalar atualizações.  

 Para obter mais informações sobre o script utiliza esta propriedade, consulte [ZTIWindowsUpdate.wsf](#ZTIWindowsUpdate.wsf).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*SERVER_NAME*|O nome do servidor WSUS, especificado no formato HTTP|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WSUSServer=http://WSUSServerName[Settings] Priority=Default  [Default] WSUSServer=http://WSUSServerName`|  

####  <a name="WUMU_ExcludeKB"></a>WUMU_ExcludeKB  
 A lista de atualizações de software do Windows Update/Microsoft Update para ignorar (por artigos da Base de dados de conhecimento associados).  

 Membros do agrupamento de projeto de implementação irão querer rever periodicamente a lista de atualizações que está a ser instaladas pelo script ZTIWindowsUpdate.wsf para verificar se cada atualização cumpre necessidades e as expectativas do projeto. Todas as atualizações são registadas e registadas no ficheiro ZTIWindowsUpdate.log, que é gerado durante a implementação. Cada atualização irá indicar o respetivo estado que instalar ou ignorar e lista o UpdateID, o nome de atualização e QNumber associados a cada atualização. Se uma atualização tem de ser excluídos, essa atualização deve ser adicionada ao ficheiro CustomSettings.ini (para implementações LTI).  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*WUMU_ExcludeKB*|A lista de atualizações de software do Windows Update/Microsoft Update para ignorar por QNumber|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WUMU_ExcludeKB1=925471`|  

#### <a name="wumuexcludeid"></a>WUMU_ExcludeID  
 A lista de atualizações de software do Windows Update/Microsoft Update para ignorar (por atualização correspondente ID).  

 Membros do agrupamento de projeto de implementação irão querer rever periodicamente a lista de atualizações que está a ser instaladas pelo script ZTIWindowsUpdate.wsf para verificar se cada atualização cumpre necessidades e as expectativas do projeto. Todas as atualizações são registadas e registadas no ficheiro ZTIWindowsUpdate.log, que é gerado durante a implementação. Cada atualização irá indicar o respetivo estado que instalar ou ignorar e lista o UpdateID, o nome de atualização e QNumber associados a cada atualização. Se uma atualização deve ser excluída, essa atualização deve ser adicionada ao ficheiro CustomSettings.ini (para implementações LTI).  

 Por exemplo, se deve ser excluída a instalação da ferramenta de remoção de Software Malicioso do Windows, procure a linha no ZTIWindowsUpdate.log que mostra onde a atualização foi identificada e instalada e, em seguida, selecione o número de UpdateID. Por exemplo, o número de UpdateID para a ferramenta de remoção de Software Malicioso do Windows é adbe6425-6560-4 d 40-9478-1e35b3cdab4f.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|||ZTI||  

|**Valor**|**Descrição**|  
|-|-|
|*WUMU_ExcludeID*|A lista de atualizações de software do Windows Update/Microsoft Update para ignorar, por número de UpdateID|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] WUMU_ExcludeID1={adbe6425-6560-4d40-9478-1e35b3cdab4f}[Settings] Priority=Default  [Default] WUMU_ExcludeID1={adbe6425-6560-4d40-9478-1e35b3cdab4f}`|  

####  <a name="XResolution"></a>XResolution  
 Resolução horizontal de monitor no computador de destino especificado em pixéis. No exemplo, o valor **1024** indica a resolução horizontal de monitor é 1.024 pixéis. Este valor é inserido as definições de configuração adequada no Unattend.xml.  

> [!NOTE]
>  Os valores predefinidos (no ficheiro de modelo Unattend.xml) são resolução horizontal de 1.024 pixéis, resolução vertical 768 pixéis, profundidade de cor de 32 bits e velocidade de atualização vertical 60 Hz.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*horizontal_resolution*|A resolução horizontal de monitor no computador de destino em pixéis|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|  

####  <a name="YResolution"></a>YResolution  
 Resolução vertical do monitor no computador de destino especificado em pixéis. No exemplo, o valor **768** indica a resolução vertical do monitor é 768 pixéis. Este valor obtém inserido as definições de configuração adequada no Unattend.xml.  

> [!NOTE]
>  Os valores predefinidos (no ficheiro de modelo Unattend.xml) são resolução horizontal de 1.024 pixéis, resolução vertical 768 pixéis, profundidade de cor de 32 bits e velocidade de atualização vertical 60 Hz.  

|**Propriedade configurada por**|||**Propriedade aplica-se a**||  
|-|-|-|-|-|  
|BootStrap.ini|||LTI|-|  
|CustomSettings.ini|-||||  
|BD DO MDT|-||ZTI|-|  

|**Valor**|**Descrição**|  
|-|-|
|*vertical_resolution*|A resolução vertical do monitor no computador de destino em pixéis|  

|**Exemplo**|  
|-|  
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|  

###  <a name="ProvidingPropertiesforSkippedDeploymentWizardPages"></a>Fornecer propriedades para as páginas do Assistente de implementação ignorada  
 Tabela 6 apresenta uma lista de páginas do Assistente de implementação individuais, a propriedade para ignorar a página do assistente correspondente e as propriedades que tem de ser configuradas quando a ignorar a página do assistente.  

 Se o **SkipWizard** propriedade é utilizada para ignorar todas as páginas do Assistente de implementação, forneça todas as propriedades do **configurar estas propriedades**coluna. Para exemplos de vários cenários de implementação avance páginas do Assistente de implementação, consulte a secção "Totalmente automatizado LTI cenário de implementação", no documento MDT *guia de amostras do Toolkit de implementação do Microsoft*.  

> [!NOTE]
>  Em situações onde a **configurar estas propriedades** coluna está em branco, sem propriedades tem de ser configurado quando a ignorar a página do assistente correspondente.  

### <a name="table-6-deployment-wizard-pages"></a>Tabela 6. Páginas de Assistente de implementação  

|**Ignorar esta página do Assistente**|**Com esta propriedade**|**Configurar estas propriedades**|  
|-|-|-|  
|**Bem-vindo**|SkipBDDWelcome||  
|**Especifique as credenciais para ligar a partilhas de rede**|Foi ignorada, fornecendo as propriedades na coluna seguinte|-O ID de utilizador<br /><br /> -UserDomain<br /><br /> -UserPassword|  
|**Sequência de tarefas**|SkipTaskSequence|-TaskSequenceID|  
|**Detalhes do Computador**|SkipComputerName,<br /><br /> SkipDomainMembership|-OSDComputerName<br /><br /> -JoinWorkgroup<br /><br /> – ou –<br /><br /> -JoinDomain<br /><br /> -DomainAdmin|  
|**Dados de utilizador**|SkipUserData|-UDDir<br /><br /> -UDShare<br /><br /> -UserDataLocation|  
|**Mover dados e definições**|SkipUserData|-UDDir<br /><br /> -UDShare<br /><br /> -UserDataLocation|  
|**Dados de utilizador (recuperação)**|SkipUserData|-UDDir<br /><br /> -UDShare<br /><br /> -UserDataLocation|  
|**Cópia de segurança do computador**|SkipComputerBackup|-BackupDir<br /><br /> -BackupShare<br /><br /> -ComputerBackupLocation|  
|**Chave de produto**|SkipProductKey|-ProductKey<br /><br /> – ou –<br /><br /> -OverrideProductKey|  
|**Pacotes de idiomas**|SkipPackageDisplay|LanguagePacks|  
|**Região e hora**|SkipLocaleSelection, SkipTimeZone|-KeyboardLocale<br /><br /> -UserLocale<br /><br /> -UILanguage<br /><br /> -TimeZoneName|  
|**Funções e funcionalidades**|SkipRoles|-OSRoles<br /><br /> -OSRoleServices<br /><br /> -OSFeatures|  
|**Aplicações**|SkipApplications|Aplicações|  
|**Palavra-passe de administrador**|SkipAdminPassword|adminPassword|  
|**Administradores locais**|SkipAdminAccounts|-Administradores|  
|**Captura de imagem**|SkipCapture|-ComputerBackupLocation|  
|**BitLocker**|SkipBitLocker|-BDEDriveLetter<br /><br /> -BDEDriveSize<br /><br /> -BDEInstall<br /><br /> -BDEInstallSuppress<br /><br /> -BDERecoveryKey<br /><br /> -TPMOwnerPassword<br /><br /> -OSDBitLockerStartupKeyDrive<br /><br /> -OSDBitLockerWaitForEncryption|  
|**Pronto para começar**|SkipSummary|–|  
|**Implementação do sistema operativo foi concluída com êxito**|SkipFinalSummary|–|  
|**Implementação do sistema operativo não foi concluída com êxito**|SkipFinalSummary|–|  

##  <a name="Scripts"></a>Scripts  
 Os scripts utilizado em implementações LTI e ZTI propriedades de referência que determinam os passos do processo e as definições de configuração utilizadas durante o processo de implementação. Utilize esta secção de referência para ajudar a determinar os scripts corretos para incluir as ações e os argumentos válidos para fornecer ao executar cada script. As seguintes informações são fornecidas para cada script:  

-   **Nome**. Especifica o nome do script.  

-   **Descrição**. Fornece uma descrição da finalidade do script e qualquer informação pertinentes relativas a personalização de script.  

-   **Entrada**. Indica os ficheiros utilizados para a entrada para o script.  

-   **Saída**. Indica os ficheiros criados ou modificados pelo script.  

-   **Referências**. Indica a outros scripts ou ficheiros de configuração que são referenciados pelo script.  

-   **Localização**. Indica a pasta onde o script pode ser encontrado. As informações para a localização, são utilizadas as seguintes variáveis:  

    -   **Program_Files**. Esta variável aponta para a localização da pasta ficheiros de programa no computador onde está instalado o MDT.  

    -   **distribuição**. Esta variável aponta para a localização da pasta de distribuição para a partilha de implementação.  

    -   **plataforma**. Esta variável é um marcador de posição para a plataforma do sistema operativo (x86 ou x64).  

-   **Utilize**. Fornece os comandos e as opções que pode especificar.  

-   **Os argumentos e uma descrição**. Indica os argumentos válidos para o script e uma breve descrição do que significa que cada argumento.  

-   **Propriedades**. As propriedades referenciadas pelo script.  

###  <a name="BDD_Autorun.wsf"></a>BDD_Autorun.wsf  
 Este script apresenta uma caixa de diálogo que indica o suporte de dados de implementação do utilizador introduzido criados pelo processo de MDT (como um DVD de arranque ou um disco rígido amovível). É apresentada a mensagem para 15 segundos. Se foi efetuada nenhuma ação, o script inicia LiteTouch.vbs.  

 Para obter mais informações sobre LiteTouch.vbs, consulte o tópico correspondente no [Scripts](#Scripts).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações necessárias pelos scripts para concluir o processo de implementação|  
|**Saída**|Nenhum|  
|**Referências**|**LiteTouch.vbs**. Inicia LTI|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|Nenhum|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="BDD_Welcome_ENU.xml"></a>BDD_Welcome_ENU.XML  
 Este ficheiro XML que contém o código de script e o esquema HTML para o **bem-vindo à implementação do Windows** página que é apresentada no início do Assistente de implementação. Este ficheiro XML é lida por Wizard.hta, que executa as páginas do assistente incorporadas existentes neste ficheiro XML.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|- **NICSettings_Definition_ENU.xml**. Permite ao utilizador fornecer definições de configuração para adaptadores de rede<br /><br /> - **Wizard.hta**. Apresenta as páginas do Assistente de implementação<br /><br /> - **WPEUtil.exe**. Inicia o Windows PE e ligações de rede inicia LTI|  
|**Localização**|*distribuição*\Tools\\*plataforma*|  
|**Utilize**|`mshta.exeWizard.hta BDD_Welcome_ENU.xml`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**KeyboardLocalePE**|-||  
|**WelcomeWizardCommand**||-|  
|**WizardComplete**||-|  

###  <a name="Credentials_ENU.xml"></a>Credentials_ENU.XML  
 Este ficheiro XML que contém o código de script e o esquema HTML para o **especificar credenciais para ligar a partilhas de rede** página do assistente no Assistente de implementação. Este ficheiro XML é lida por Wizard.hta, que executa as páginas do assistente incorporadas existentes neste ficheiro XML.  

> [!NOTE]
>  Só é apresentada a página do assistente se ocorrer uma falha ao validar as credenciais de utilizador predefinidas.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|**Credentials_scripts.vbs**. Contém funções de suporte de credenciais de utilizador|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`mshta.exe Wizard.hta /NotWizard /definition:Credentials_ENU.xml [/ValidateAgainstDomain:domain &#124; /ValidateAgainstUNCPath:uncpath]  </DoNotSave> </LeaveShareOpen>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="Credentials_scripts.vbs"></a>Credentials_scripts.vbs  
 Este script analisa os argumentos fornecidos ao carregar o ficheiro de Credentials_ENU.xml para o Assistente de implementação. Também executa validação de credenciais do utilizador. Este script é lido pelo ficheiro Credentials_ENU.xml.  

 Para obter mais informações sobre Credentials_ENU.xml, consulte o tópico correspondente no [Scripts](#Scripts).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Mensagem de evento são escritos para estes ficheiros de registo:<br /><br /> - **Credentials_scripts.log**. Ficheiro de registo que contém os eventos gerados por este script<br /><br /> - **BDD.log**. Ficheiro de registo que contém os eventos gerados por todos os scripts de MDT|  
|**Referências**|Nenhum|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="Credentials_scripts.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**UserCredentials**||-|  
|**UserDomain**|-||  

###  <a name="DeployWiz_Definition_ENU.xml"></a>DeployWiz_Definition_ENU.xml  
 Este ficheiro XML contém o código de script e o esquema HTML para cada página do assistente no Assistente de implementação. Este ficheiro é lida por Wizard.hta, que executa as páginas do assistente incorporadas existentes neste ficheiro XML. Este ficheiro. XML contém as seguintes páginas do assistente:  

-   **Bem-vindo**  

-   **Especifique as credenciais para ligar a partilhas de rede**  

-   **Sequência de tarefas**  

-   **Detalhes do Computador**  

-   **Dados de utilizador**  

-   **Mover dados e definições**  

-   **Dados de utilizador (recuperação)**  

-   **Cópia de segurança do computador**  

-   **Chave de produto**  

-   **Pacotes de idiomas**  

-   **Região e hora**  

-   **Funções e funcionalidades**  

-   **Aplicações**  

-   **Palavra-passe de administrador**  

-   **Administradores locais**  

-   **Captura de imagem**  

-   **BitLocker**  

-   **Pronto para começar**  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|- **DeployWiz_Initialization.vbs**. Inclui as funções de suporte e subroutines utilizados pelo script<br /><br /> - **DeployWiz_Validation.vbs**. Inclui as funções de suporte e subroutines utilizados pelo script<br /><br /> - **ZTIBackup.wsf**. Cria uma cópia de segurança do computador de destino<br /><br /> - **ZTIPatches.wsf**. Instala atualizações (pacotes de idiomas, atualizações de segurança e assim sucessivamente)<br /><br /> - **ZTIUserState.wsf**. Inicia a migração de estado do utilizador para capturar e restaurar o estado do utilizador no computador de destino|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|Nenhum|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DoCapture**|-||  
|**ImageBuild**|-||  
|**ImageFlags**|-||  
|**IsBDE**|-||  
|**IsServerOS**|-||  
|**JoinDomain**|-||  
|**OSDComputerName**|-||  
|**OSVersion**|-||  
|**SkipAdminAccounts**|-||  
|**SkipAdminPassword**|-||  
|**SkipApplications**|-||  
|**SkipBitLocker**|-||  
|**SkipCapture**|-||  
|**SkipComputerBackup**|-||  
|**SkipComputerName**|-||  
|**SkipDomainMembership**|-||  
|**SkipLocaleSelection**|-||  
|**SkipPackageDisplay**|-||  
|**SkipProductKey**|-||  
|**SkipRoles**|-||  
|**SkipSummary**|-||  
|**SkipTaskSequence**|-||  
|**SkipTimeZone**|-||  
|**SkipUserData**|-||  
|**TaskSequenceTemplate**|-||  
|**UserDomain**|-||  
|**ID de utilizador**|-||  
|**UserPassword**|-||  
|**USMTOfflineMigration**|-||  

###  <a name="DeployWiz_Initialization.vbs"></a>DeployWiz_Initialization.vbs  
 Este script inicia as páginas de **Assistente de implementação** (armazenado na [DeployWiz_Definition_ENU.xml](#DeployWiz_Definition_ENU.xml)). Também contém funções e subroutines que chama o Assistente de implementação durante uma implementação LTI.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|- **DomainOUList.xm**l. Contém uma lista de domínio UOs<br /><br /> - **ListOfLanguages.xml**<br /><br /> - **LocationServer.xml**. Contém uma lista de partilhas de implementação disponíveis<br /><br /> - **As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação; as variáveis de ambiente são preenchidas pelo ZTIGather.wsf|  
|**Saída**|Mensagem de evento são escritos para estes ficheiros de registo:<br /><br /> - **DeployWiz_Initialization.log**. Ficheiro de registo que contém os eventos gerados por este script<br /><br /> - **BDD.log**. Ficheiro de registo que contém os eventos gerados por todos os scripts de MDT|  
|**Referências**|**ZTIApplications.wsf**. Instalação da aplicação inicia|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="DeployWiz_Initialization.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**Aplicações**|-||  
|**BackupDir**|-||  
|**Ficheiro**|-||  
|**BackupShare**|-||  
|**BDEInstall**|-||  
|**BDEKeyLocation**|-||  
|**BDERecoveryKey**|-||  
|**BDEWaitForEncryption**|-||  
|**CapableArchitecture**|-||  
|**ComputerBackupLocation**|-||  
|**CustomWizardSelectionProfile**|-||  
|**DeploymentType**|-||  
|**DeployRoot**|-||  
|**DomainAdmin**|-||  
|**DomainAdminDomain**|-||  
|**DomainAdminPassword**|-||  
|**DomainOUs**|-||  
|**ImageBuild**|-||  
|**ImageFlags**|-||  
|**ImageLanguage**|-||  
|**ImageLanguage001**|-||  
|**ImageProcessor**|-||  
|**IsServerOS**|-||  
|**KeyboardLocale**|-||  
|**KeyboardLocale_Edit**|-||  
|**LanguagePacks**|-||  
|**LanguagePacks001**|-||  
|**LocalDeployRoot**|-||  
|**MandatoryApplications**|-||  
|**OSDComputerName**|-||  
|**OSCurrentBuild**|-||  
|**OSDBitLockerCreateRecoveryPassword**|-||  
|**OSDBitLockerMode**|-||  
|**OSDBitLockerStartupKeyDrive**|-||  
|**OSDBitLockerWaitForEncryption**|-||  
|**OSSKU**|-||  
|**OSVersion**|-||  
|**OverrideProductKey**|-||  
|**ProductKey**|-||  
|**SkipCapture**|-||  
|**SkipDomainMembership**|-||  
|**TaskSequenceID**|-||  
|**TimeZoneName**|-||  
|**TSGUID**|-||  
|**UDDir**|-||  
|**UDShare**|-||  
|**UILanguage**|-||  
|**UserDataLocation**|-||  
|**UserDomain**|-||  
|**ID de utilizador**|-||  
|**UserLocale**|-||  
|**UserPassword**|-||  
|**WizardSelectionProfile**|-||  

###  <a name="DeployWiz_Validation.vbs"></a>DeployWiz_Validation.vbs  
 Este script inicia e valida as informações que escreveu nas páginas do Assistente de implementação (armazenado na [DeployWiz_Definition_ENU.xml](#DeployWiz_Definition_ENU.xml)). Este script contém funções e subroutines que chama o Assistente de implementação durante uma implementação LTI.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|- **OperatingSystems.xml**. Contém a lista dos sistemas operativos disponíveis para implementação<br /><br /> - **As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações necessárias pelos scripts para concluir o processo de implementação; as variáveis de ambiente são preenchidas pelo ZTIGather.wsf|  
|**Saída**|Nenhum|  
|**Referências**|- **Credentials_ENU.XML**. Pede ao utilizador as credenciais que será utilizada ao ligar a recursos de rede<br /><br /> - **ZTIGather.wsf**. Reúne propriedades e as regras de processamento|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="DeployWiz_Validation.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**DeploymentType**|-|-|  
|**DeployTemplate**||-|  
|**ImageBuild**|-||  
|**ImageProcessor**|-|-|  
|**OSVersion**|-||  
|**TaskSequenceID**||-|  
|**TSGUID**|-||  
|**UserCredentials**|-||  
|**UserDomain**||-|  
|**ID de utilizador**||-|  
|**UserPassword**||-|  

###  <a name="LiteTouch.vbs"></a>LiteTouch.vbs  
 Este script é chamado pelo Assistente de implementação para iniciar LTI. O script:  

-   Remove a pasta C:\MININT (se existir)  

-   Verifica se o computador de destino cumpre os requisitos para executar o Assistente de implementação ao chamar [ZTIPrereq.vbs](#ZTIPrereq.vbs)  

-   Inicia o Assistente de implementação executando [LiteTouch.wsf](#LiteTouch.wsf)  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|- **BDDRun.exe**<br /><br /> - **ZTIPrereq.vbs**. Utilizado para determinar se o computador de destino cumpre os pré-requisitos para implementar um novo sistema operativo<br /><br /> - **LiteTouch.wsf**. O script responsável para controlar o processo de implementação LTI|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LiteTouch.vbs </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> - **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> - **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="LiteTouch.wsf"></a>LiteTouch.wsf  
 Este script é chamado pelo [LiteTouch.vbs](#LiteTouch.vbs) e é responsável por controlar o processo de implementação LTI. Isto inclui:  

-   Executar o Assistente de implementação  

-   Executar o processo de implementação LTI utilizando o ficheiro de sequência de tarefas apropriada  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|-***task_sequence_file*.xml**. Contém as tarefas e a sequência de tarefas para o processo de implementação LTI<br /><br /> - **As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações necessárias pelos scripts para concluir o processo de implementação; as variáveis de ambiente são preenchidas pelo ZTIGather.wsf|  
|**Saída**|-                          **LiteTouch.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **BDD_Welcome_ENU.XML**. Apresenta o Assistente de implementação **boas-vindas** página para a implementação LTI<br /><br /> -                          **DeployWiz_Definition_ENU.xml**. Apresenta as páginas do Assistente de implementação para a implementação LTI<br /><br /> -                          **DiskPart.exe**. Utilitário, que permite a gestão automática de discos, partições e volumes<br /><br /> -                          **LTICleanup.wsf**. Executa tarefas de limpeza após a conclusão da implementação<br /><br /> -                          **LTICopyScripts.wsf**. Copia os scripts de implementação para um disco rígido local no computador de destino<br /><br /> -                          **MSHTA.exe**. Anfitrião de aplicação HTML<br /><br /> -                          **RecEnv.exe**. Se este utilitário existe, é pedido ao utilizador para determinar se pretende iniciar o ambiente de recuperação do Windows.<br /><br /> -                          **Regsvr32.exe**. Regista os ficheiros (. dll, .exe,. ocx e assim sucessivamente) com o sistema operativo<br /><br /> -                          **Summary_Definition_ENU.XML**. Apresenta os resultados de resumos para a implementação LTI<br /><br /> -                          **TsmBootStrap.exe**. Utilitário de arranque de configuração de sequência de tarefas<br /><br /> -                          **Wizard.hta**. Apresenta as páginas do Assistente de implementação<br /><br /> -                          **WPEUtil.exe**. Inicia o Windows PE e ligações de rede inicia LTI<br /><br /> -                          **ZTIGather.wsf**. Reúne propriedades e as regras de processamento<br /><br /> -                          **ZTIPrereq.vbs**. Verifica se o computador de destino cumpre os requisitos para executar o Assistente de implementação<br /><br /> -                          **ZTINICConfig.wsf**. Configura os adaptadores de rede ativada<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`BDDRun.exe "wscript.exe <ScriptDirectory>\LiteTouch.wsf </debug:value>"`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  
|**/ Iniciar**|Cria um atalho no novo sistema operativo que é executado assim que for iniciada a shell|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_DoNotCleanLiteTouch**|-||  
|**_SMSTSPackageName**||-|  
|**AdminPassword**|-||  
|**Arquitetura**|-|-|  
|**BootPE**|-|-|  
|**ComputerBackupLocation**||-|  
|**ComputerName**|-||  
|**DeployDrive**|-|-|  
|**DeploymentMethod**|-|-|  
|**DeploymentType**|-|-|  
|**DeployRoot**|-|-|  
|**DestinationLogicalDrive**||-|  
|**DomainAdmin**||-|  
|**DomainAdminDomain**||-|  
|**DomainAdminPassword**||-|  
|**FinishAction**|-||  
|**Nome de anfitrião**|-||  
|**IsServerCoreOS**|-||  
|**JoinDomain**|-||  
|**JoinWorkgroup**|-|-|  
|**KeyboardLocalePE**|-||  
|**LTISuspend**|-||  
|**OSDAdapterCount**|-||  
|**OSDComputerName**|-|-|  
|**Fase**|-|-|  
|**ResourceDrive**|-|-|  
|**ResourceRoot**|-|-|  
|**RetVal**||-|  
|**SkipBDDWelcome**|-||  
|**SkipFinalSummary**|-|-|  
|**SkipWizard**|-||  
|**SMSTSLocalDataDrive**||-|  
|**TaskSequenceID**|-||  
|**TimeZoneName**||-|  
|**UserDataLocation**|-|-|  
|**UserDomain**|-||  
|**ID de utilizador**|-||  
|**UserPassword**|-||  
|**WelcomeWizardCommand**|-||  
|**WizardComplete**|-||  

###  <a name="LTIApply.wsf"></a>LTIApply.wsf  
 Este script é responsável pela instalação de uma imagem do Windows PE para o computador de destino. Imagem do Windows PE é utilizada para recolher informações sobre o computador de destino e executar tarefas de implementação no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **LTIApply.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **LTIApply_wdsmcast.log**. Ficheiro de registo que contém os eventos que gera o utilitário de Wdsmcast<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Bootsect.exe**. Aplica-se um setor de arranque para o disco rígido<br /><br /> -                          **ImageX.exe**. Um utilitário utilizado para criar e gerir ficheiros WIM<br /><br /> -                          **ZTIBCDUtility.vbs**. Inclui as funções de utilitário utilizadas ao efetuar o arranque do Gestor de tarefas<br /><br /> -                          **ZTIConfigFile.vbs**. Inclui rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIDiskUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **Wdsmcast.exe**. Um utilitário que utilizam computadores de destino para associar um transmissão multicast|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTIApply.wsf </pe> </post> </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/PE**|Utiliza o processo para instalar a imagem do Windows PE no computador de destino|  
|**/Post**|Limpa ficheiros desnecessários após a instalação de uma imagem|  
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**BootPE**||-|  
|**DeployRoot**|-||  
|**DestinationLogicalDrive**|-|-|  
|**OSGUID**|-||  
|**OSCurrentVersion**|-||  
|**OSVersion**|-||  
|**ImageBuild**|-||  
|**ImageFlags**|-||  
|**ImageProcessor**|-||  
|**ISBDE**|-||  
|**SourcePath**||-|  
|**TaskSequenceID**|-||  
|**UserDomain**|-||  
|**ID de utilizador**|-||  
|**UserPassword**|-||  
|**WDSServer**|-||  

###  <a name="LTICleanup.wsf"></a>LTICleanup.wsf  
 Este script remove quaisquer ficheiros ou as definições de configuração (por exemplo, scripts, pastas, as entradas de registo ou as definições de configuração do início de sessão automático) do computador de destino após a conclusão do processo de implementação.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|-                          **LTICleanup.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Bootsect.exe**. Aplica-se um setor de arranque para o disco rígido<br /><br /> -                          **NET.exe**. Executa tarefas de gestão de rede<br /><br /> -                          **RegSvr32.exe**. Regista os ficheiros (. dll, .exe,. ocx e assim sucessivamente) com o sistema operativo<br /><br /> -                          **ZTIBCDUtility.vbs**. Inclui as funções de utilitário utilizadas ao efetuar o arranque do Gestor de tarefas<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTICleanup.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_DoNotCleanLiteTouch**|-||  
|**DeployRoot**|-||  
|**DestinationLogicalDrive**|-||  
|**OSVersion**|-||  

###  <a name="LTICopyScripts.wsf"></a>LTICopyScripts.wsf  
 Este script copia os scripts de implementação para os processos de implementação LTI e ZTI para um disco rígido local no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|-                          **Summary_Definition_ENU.XML**. Apresenta os resultados de resumos para a implementação LTI<br /><br /> -                          **As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **LTICopyScripts.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTICopyScripts.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="LTIGetFolder.wsf"></a>LTIGetFolder.wsf  
 Este script apresenta uma caixa de diálogo que permite que o utilizador procura para uma pasta. O caminho de pasta selecionada é armazenado na variável de ambiente de FOLDERPATH.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|Nenhum|  
|**Referências**|-                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **WizUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza a IU (por exemplo, as páginas do assistente)|  
|**Localização**|-                          *distribuição*\Scripts<br /><br /> -                          *Program_Files*\Microsoft Deployment Toolkit\Scripts|  
|**Utilize**|`cscript LTIGetFolder.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/Debug:value**|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DefaultFolderPath**|-||  
|**FolderPath**||-|  

###  <a name="LTIOEM.wsf"></a>LTIOEM.wsf  
 Este script é utilizado por um OEM durante um cenário de LTI OEM para copiar o conteúdo de uma partilha de implementação de suportes de dados para o disco de rígido do computador de destino para o preparar para duplicação.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|-                          **LTIOEM.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **RoboCopy.exe**. Ferramenta de cópia de ficheiros e pastas<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTIOEM.wsf </BITLOCKER &#124; /BDE> </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  
|**/ BITLOCKER**|Ativa o BitLocker|  
|**/ BDE**|Ativa o BitLocker|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_DoNotCleanLiteTouch**||-|  
|**DeployDrive**|-||  
|**DeployRoot**|-||  
|**TSGUID**|-||  

###  <a name="LTISuspend.wsf"></a>LTISuspend.wsf  
 Este script suspende uma sequência de tarefas para permitir que as tarefas manuais ser executada. Quando este script é executado, cria um **sequência de tarefas de retomar** atalho no ambiente de trabalho do utilizador que permite ao utilizador para reiniciar a sequência de tarefas manuais após todas as tarefas estão concluídas.  

> [!NOTE]
>  Este script só é suportado no sistema operativo completo.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|-                          **LTISuspend.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **LiteTouch.wsf**. Controla o processo de implementação LTI<br /><br /> -                          **LTICopyScripts.wsf**. Copia os scripts de implementação para um disco rígido local no computador de destino<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTISuspend.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  
|**/ Retomar**|–|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**LTISuspend**||-|  
|**SMSTSRebootRequested**||-|  

###  <a name="LTISysprep.wsf"></a>LTISysprep.wsf  
 Este script prepara o computador de destino para executar o Sysprep, executa o Sysprep no computador de destino e, em seguida, verifica se o Sysprep executou com êxito.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|-                          **LTISysprep.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Expand.exe**. Expande os ficheiros comprimidos<br /><br /> -                          **Sysprep.exe**. Prepara computadores duplicação<br /><br /> -                          **ZTIConfigFile.vbs**. Contém rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript LTISysprep.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**DeployRoot**|-||  
|**DestinationLogicalDrive**|-||  
|**DoCapture**|-||  
|**OSCurrentBuild**|-||  
|**OSDAnswerFilePath**|-||  
|**OSGUID**|-||  
|**SourcePath**|-|-|  
|**TaskSequenceID**|-||  

###  <a name="NICSettings_Definition_ENU.xml"></a>NICSettings_Definition_ENU.xml  
 Este ficheiro XML que contém o código de script e o esquema HTML para o **configurar definições de rede de IP estático** página do assistente no Assistente de implementação. Durante uma implementação LTI, Wizard.hta lê este ficheiro e executa a página do assistente incorporados que solicita a configuração de endereçamento de rede necessária. Não se for fornecida nenhum configuração de endereçamento IP estático, os scripts de implementação serão predefinido para utilizar DHCP para obter a configuração de rede necessários.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|**ZTINICUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|Nenhum|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**OSDAdapterxDNSServerList**||-|  
|**OSDAdapterxDNSSuffix**||-|  
|**OSDAdapterxGateways**||-|  
|**OSDAdapterxIPAddressList**||-|  
|**OSDAdapterxMacAddress**||-|  
|**OSDAdapterxSubnetMask**||-|  
|**OSDAdapterxWINSServerList**||-|  
|**OSDAdapterCount**||-|  

> [!NOTE]
>  O*x*os nomes de propriedade listado acima é um marcador de posição para uma matriz baseada em zero que contém as informações da placa de rede.  

###  <a name="Summary_Definition_ENU.xml"></a>Summary_Definition_ENU.XML  
 Este ficheiro XML que contém o código de script e o esquema HTML para o **resumo de implementação** página do assistente no Assistente de implementação. Durante uma implementação LTI, Wizard.hta lê este ficheiro e executa a página do assistente incorporados que apresenta os resultados de resumos para a implementação LTI. Este ficheiro XML contém as seguintes páginas do assistente:  

-   **Êxito**. Notificação sobre a conclusão das tarefas de implementação com êxito  

-   **Falha de**. Notificação sobre a falha de concluir as tarefas de implementação com êxito  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|**Summary_Scripts.vbs**. Inclui as funções de suporte e subroutines que as páginas do assistente incorporadas nesta utilização do ficheiro XML|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|Nenhum|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**SkipFinalSummary**|-||  
|**RetVal**|-||  

###  <a name="Summary_scripts.vbs"></a>Summary_scripts.vbs  
 Este script é chamado pelo **resumo** página do Assistente do Assistente de implementação. Contém as funções e subroutines utilizadas para a inicialização e de validação.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|Mensagem de evento são escritos para estes ficheiros de registo:<br /><br /> -                          **Summary_scripts.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|Nenhum|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="Summary_Scripts.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeploymentType**|-||  
|**RetVal**|-||  

###  <a name="Wizard.hta"></a>Wizard.hta  
 Esta aplicação de hipertexto apresenta as páginas do Assistente de implementação.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém a lista de valores de propriedade, propriedades personalizadas, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação. As variáveis de ambiente são preenchidas pelo ZTIGather.wsf.|  
|**Saída**|-                          **Wizard.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **LTIGetFolder.wsf**. Ficheiro de script que inicia uma **BrowseForFolder** caixa de diálogo<br /><br /> -                          **ZTIConfigFile.vbs**. Inclui rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **WizUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|-                          *distribuição*\Scripts<br /><br /> -                          *Program_Files*\Microsoft Deployment Toolkit\Scripts|  
|**Utilize**|`mshta.exe Wizard.hta </definition:filename> </NotWizard> </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ NotWizard**|Utilizado para ignorar pedidos de página do Assistente|  
|**/ Definição de: * nome de ficheiro***|Especifica o ficheiro XML que está a ser carregados para o Assistente|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Definição**|-||  
|**DefaultFolderPath**||-|  
|**FolderPath**|-||  
|**WizardComplete**||-|  

###  <a name="WizUtility.vbs"></a>WizUtility.vbs  
 Este script contém funções e subroutines que referenciam os vários scripts de Assistente de implementação.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **WizUtility.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**LTIGetFolder.wsf**. Ficheiro de script que inicia uma **BrowseForFolder**caixa de diálogo|  
|**Localização**|-                          *distribuição*\Scripts<br /><br /> -                          *Program_Files*\Microsoft Deployment Toolkit\Scripts|  
|**Utilize**|`<script language="VBScript" src="WizUtility.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DefaultFolderPath**||-|  
|**DefaultDestinationDisk**|-||  
|**DefaultDestinationIsDirty**|-||  
|**DefaultDestinationPartition**|-||  
|**DeploymentType**|-||  
|**DestinationDisk**|-||  
|**FolderPath**|-||  
|**OSVersion**|-||  
|**UserDomain**|-||  
|**UserCredentials**||-|  

###  <a name="ZTIApplications.wsf"></a>ZTIApplications.wsf  
 Este script inicia uma instalação de aplicações que tenham sido configurados no nó de aplicações no Deployment Workbench. Este script não irá tentar instalar qualquer aplicação que:  

-   Não suporta o tipo de plataforma do computador de destino  

-   Não suporta o tipo de processador do computador de destino  

-   Tem uma entrada de desinstalação no registo em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall**  

> [!NOTE]
>  Se a aplicação listada tem quaisquer aplicações dependentes definidas, este script tenta instalar essas aplicações dependentes antes de instalar a aplicação listada.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIApplications.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **ZTIConfigFile.vbs**. Inclui rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **BDDRun.exe**. Executa um comando que necessite de interação do utilizador|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIApplications.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**ApplicationGUID**|-||  
|**ApplicationSuccessCodes**|-||  
|**DependentApplications**|-||  
|**DeploymentMethod**|-||  
|**InstalledApplications**|-|-|  
|**ResourceDrive**|-||  
|**ResourceRoot**|-|-|  
|**SMSTSRebootRequested**||-|  
|**SMSTSRetryRequested**||-|  

###  <a name="ZTIAppXmlGen.wsf"></a>ZTIAppXmlGen.wsf  
 Este script gera uma utilização de file—ZTIAppXmlGen.xml—to XML automaticamente capturar os dados de utilizador (documentos) associados a aplicações instaladas. Faz, por isso, através de **HKEY_CLASSES_ROOT\Software\Classes** chave de registo e captura todas as aplicações que:  

-   Não estão associados com uma destas extensões de ficheiro:. mp3, .mov, .wma,. wmv, *.chm, .evt, .evtx, .exe, empresa>.com ou .fon  

-   Não estão associados com o Microsoft Office, como o sistema Office 2007 ou o Microsoft Office 2003.  

-   Tem um processador abra válido listado em **HKEY_CLASSES_ROOT\application\shell\open\command**  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIAppXmlGen.xml**. Contém uma lista de aplicações instaladas no computador de destino<br /><br /> -                          **ZTIAppXmlGen.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIAppXmlGen.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**ImageBuild**|-||  
|**OSCurrentVersion**|-||  
|**USMTMigFiles**|-|-|  

###  <a name="ZTIAuthorizeDHCP.wsf"></a>ZTIAuthorizeDHCP.wsf  
 Este script utiliza a ferramenta de Netsh para configurar o computador de destino para que seja um servidor DHCP autorizado no AD DS.  

 Para obter mais informações sobre a autorizar os servidores DHCP, consulte [como utilizar Netsh.exe para autorizar, Unauthorize lista de servidores e DHCP no Active Directory](http://support.microsoft.com/kb/303351).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIAuthorizeDHCP.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Netsh.exe**. Um utilitário utilizado para automatizar a configuração de componentes de rede<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIAuthorizeDHCP.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**IPAddress**|-||  

###  <a name="ZTIBackup.wsf"></a>ZTIBackup.wsf  
 Este script executa uma cópia de segurança do computador de destino utilizando o utilitário do ImageX. A cópia de segurança é armazenada na localização especificada no [BackupDir](#BackupDir) e [BackupShare](#BackupShare) propriedades.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIBackup.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **ZTIBackup_imagex.log**. Ficheiro de registo que contém os eventos que gera o ImageX<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **ImageX.exe**. Um utilitário utilizado para criar e gerir ficheiros WIM<br /><br /> -                          **ZTIBCDUtility.vbs**. Inclui as funções de utilitário utilizadas ao efetuar o arranque do Gestor de tarefas<br /><br /> -                          **ZTIDiskUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIBackup.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**BackupDir**|-||  
|**BackupDisk**|-||  
|**BackupDrive**|-||  
|**Ficheiro**|-||  
|**BackupPartition**|-||  
|**BackupScriptComplete**||-|  
|**BackupShare**|-||  
|**ComputerBackupLocation**|-||  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DestinationLogicalDrive**|-|-|  
|**DoCapture**|-||  
|**ImageBuild**|-||  
|**ImageFlags**|-||  
|**OSDStateStorePath**|-||  
|**Fase**|-||  
|**TaskSequenceID**|-||  
|**USMTLocal**|-||  

###  <a name="ZTIBCDUtility.vbs"></a>ZTIBCDUtility.vbs  
 Este script contém funções de utilitário que alguns scripts de MDT utilizam ao efetuar o arranque do Gestor de tarefas.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|Nenhum|  
|**Referências**|**BCDEdit.exe**. Uma ferramenta para editar a configuração de arranque do Windows|  
|**Localização**|-                          *distribuição*\Scripts<br /><br /> -                          *Program_Files*\Microsoft Deployment Toolkit\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTIBCDUtility.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTIBde.wsf"></a>ZTIBde.wsf  
 Este script instala e configura o BitLocker no computador de destino. Configuração do BitLocker está limitada a cenários de novo computador que tenha discos rígidos configurados com uma única partição.  

> [!NOTE]
>  Para implementações ZTI e UDI, o **UILanguage** propriedade tem de ser definida no CustomSettings.ini ou na base de dados MDT, porque ZTIBde.wsf tenta ler a região do **UILanguage** propriedade.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIBde.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **ZTIBdeFix_diskpart.log**. Ficheiro de registo que contém os eventos que a ferramenta de Diskpart gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Defrag.exe**. Defragments o disco rígido<br /><br /> -                          **DiskPart.exe**. Utilitário que permite a gestão automática de discos, partições e volumes<br /><br /> -                          **ServerManagerCmd.exe**<br /><br /> -                          **ZTIDiskUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTIOSRole.wsf**. A instalação de funções de servidor<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIBde.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**AdminPassword**|-||  
|**BDEDriveLetter**|-|-|  
|**BDEDriveSize**|-||  
|**BDEInstall**|-||  
|**BDEInstallSuppress**|-||  
|BDEKeyLocation|-||  
|**BDEPin**|-||  
|**BDERecoveryKey**|-||  
|**BDESecondPass**|-|-|  
|**BdeWaitForEncryption**|-||  
|**BitlockerInstalled**|-|-|  
|**DeploymentMethod**|-||  
|**ISBDE**|-||  
|**OSDBitLockerCreateRecoveryPassword**|-||  
|**OSDBitLockerMode**|-||  
|**OSDBitLockerStartupKey**|-||  
|**OSDBitLockerStartupKeyDrive**|-||  
|**OSDBitLockerTargetDrive**|-||  
|**OSDBitLockerWaitForEncryption**|-||  
|**OSCurrentBuild**|-||  
|**OSCurrentVersion**|-||  
|**OSFeatures**|-|-|  
|**OSRoles**|-|-|  
|**OSRoleServices**|-|-|  
|**OSVersion**|-||  
|**SMSTSRebootRequested**|-|-|  
|**SMSTSRetryRequested**||-|  
|**TPMOwnerPassword**|-||  

###  <a name="ZTIBIOSCheck.wsf"></a>ZTIBIOSCheck.wsf  
 Este script verifica a BIOS no computador de destino e, em seguida, observa uma lista de BIOSes que são incompatíveis com o Windows. A lista de BIOSes incompatível é armazenada no [ZTIBIOSCheck.xml](#ZTIBIOSCheck.xml) ficheiro.  

 Se o BIOS no computador de destino está listado no [ZTIBIOSCheck.xml](#ZTIBIOSCheck.xml) de ficheiros, em seguida, o script devolve um Estado que indica o BIOS é incompatível com o Windows e o processo de implementação deve ser terminado. Para obter informações sobre a preencher a lista de BIOSes incompatível, consulte [ZTIBIOSCheck.xml](#ZTIBIOSCheck.xml).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|-                          **ZTIBIOSCheck.xml**. Contém uma lista de BIOSes são conhecidos por ser incompatível com o Windows<br /><br /> -                          **As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIBIOSCheck.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIBIOSCheck.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não é fornecido)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTICoalesce.wsf"></a>ZTICoalesce.wsf  
 O Configuration Manager requer pacotes para ser numeradas sequencialmente começadas **PACKAGES001**, com nenhuma lacunas na sequência de número. Caso contrário, a instalação irá falhar.  

 Este script permite-lhe definir e variáveis com informações de identificação sobre o programa para ser executada de nome — por exemplo, **ComputerPackages100**, **ComputerPackages110**, ou  **CollectionPackages150**. Em seguida, quando este script é executado, o Configuration Manager localiza todas as variáveis que correspondam a um padrão (por exemplo, todos os nomes de variáveis que contenham a cadeia **pacotes**) e cria uma lista de sequencial, sem lacunas, utilizando o nome de base  **PACOTES**.  

 Por exemplo, se as seguintes variáveis foram definidas (utilizar variáveis de computador, as variáveis de coleção, ou num CustomSettings.ini ou da base de dados do MDT, por exemplo):  

-   **ComputerPackages100 = XXX00001:Program**  

-   **ComputerPackages110 = XXX00002:Program**  

-   **CollectionPackages150 = XXX00003:Program**  

-   **Packages001 = XXX00004:Program**  

 Depois do script é executado, a lista seria:  

-   **PACKAGES001 = XXX00004:Program**  

-   **PACKAGES002 = XXX00001:Program**  

-   **PACKAGES003 = XXX00002:Program**  

-   **PACKAGES004 = XXX00003:Program**  

 O Configuration Manager, em seguida, seria capaz de executar todos os programas de quatro.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTICoalesce.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTICoalesce.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ CoalesceDigits: * valor***|Especifica o número de dígitos que precisam de ser fornecido ao criar a sequência de numeração. Por exemplo, um valor de:<br /><br /> -                              **2** criaria PACKAGE03<br /><br /> -                              **3**criaria PACKAGE003<br /><br /> O valor predefinido se este argumento não for fornecido é **3**.|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**CoalescePattern**|-||  
|**CoalesceTarget**|-||  

###  <a name="ZTIConfigFile.vbs"></a>ZTIConfigFile.vbs  
 Este script contém rotinas comuns para processar ficheiros XML do MDT.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConfigFile.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|NET.exe|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTIConfigFile.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**IsSafeForWizardHTML**|-||  
|**MandatoryApplications**|-||  
|**SkipGroupSubFolders**|-||  

###  <a name="ZTIConfigure.wsf"></a>ZTIConfigure.wsf  
 Este script configura o ficheiro Unattend.xml com os valores de propriedade especificados anteriormente no processo de implementação MDT. O script configura o ficheiro adequado com base no sistema operativo que está a ser implementado.  

 Este script lê o ficheiro de ZTIConfigure.xml para determinar como atualizar o ficheiro Unattend.xml com os valores adequados especificados nas propriedades de implementação. O ficheiro ZTIConfigure.xml contém as informações para traduzir as propriedades para as definições no ficheiro Unattend.xml.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|-                          **ZTIConfigure.xml**. Contém uma lista de valores de propriedade (especificados anteriormente no processo de implementação) e as respetivas definições de configuração correspondentes<br /><br /> -                          **As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConfigure.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIConfigure.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**ComputerName**|-|-|  
|**DeploymentType**|-||  
|**DeploymentMethod**|-||  
|**DeployRoot**|-||  
|**DestinationLogicalDrive**|-||  
|DomainAdminDomain|-||  
|**ImageBuild**|-||  
|**OSDAnswerFilePath**|-||  
|**OSDAnswerFilePathSysprep**|-||  
|**OSDComputerName**|-||  
|**Fase**|-||  
|**TaskSequenceID**|-||  

###  <a name="ZTIConfigureADDS.wsf"></a>ZTIConfigureADDS.wsf  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConfigureADDS.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Dcpromo.exe**. Instala e remove o AD DS<br /><br /> -                          **NET.exe**. Executa tarefas de gestão de rede<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIConfigureADDS.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**ADDSLogPath**|-||  
|**ADDSPassword**|-||  
|**ADDSUserDomain**|-||  
|**ADDSUserName**|-||  
|**AutoConfigDNS**|-||  
|**ChildName**|-||  
|**ConfirmGC**|-||  
|**DatabasePath**|-||  
|**DomainLevel**|-||  
|**DomainNetBiosName**|-||  
|**ForestLevel**|-||  
|**NewDomain**|-||  
|**NewDomainDNSName**|-||  
|**OSVersion**|-||  
|**ParentDomainDNSName**|-||  
|**ReplicaOrNewDomain**|-|-|  
|**ReplicaDomainDNSName**|-||  
|**ReplicationSourceDC**|-||  
|**SafeModeAdminPassword**|-||  
|**SiteName**|-||  
|**SysVolPath**|-||  

###  <a name="ZTIConfigureDHCP.wsf"></a>ZTIConfigureDHCP.wsf  
 Este script configura o DHCP no computador de destino.  

> [!NOTE]
>  DHCP já deve estar instalado no computador de destino antes de executar este script.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConfigureDHCP.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Netsh.exe**. Um utilitário que permite automatizar a configuração de componentes de rede<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIConfigureDHCP.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DHCPScopesxDescription**|-||  
|**DHCPScopesxEndIP**|-||  
|**DHCPScopesxExcludeStartIP**|-||  
|**DHCPScopesxExcludeEndIP**|-||  
|**DHCPScopesxIP**|-||  
|**DHCPScopesxName**|-||  
|**DHCPScopesxOptionRouter**|-||  
|**DHCPScopesxOptionDNSDomainName**|-||  
|**DHCPScopesxOptionDNSServer**|-||  
|**DHCPScopesxOptionLease**|-||  
|**DHCPScopesxOptionNBTNodeType**|-||  
|**DHCPScopesxOptionPXEClient**|-||  
|**DHCPScopesxOptionWINSServer**|-||  
|**DHCPScopesxStartIP**|-||  
|**DHCPScopesxSubnetmask**|-||  
|**DHCPServerOptionDNSDomainName**|-||  
|DHCPServerOptionDNSServer|-||  
|**DHCPServerOptionNBTNodeType**|-||  
|**DHCPServerOptionPXEClient**|-||  
|**DHCPServerOptionRouter**|-||  
|**DHCPServerOptionWINSServer**|-||  

> [!NOTE]
>  O *x*nas propriedades de listados aqui é um marcador de posição para uma matriz baseada em zero que contém informações de configuração de DHCP.  

###  <a name="ZTIConfigureDNS.wsf"></a>ZTIConfigureDNS.wsf  
 Este script configura DNS no computador de destino. Para executar as tarefas de configuração real, o script utiliza o utilitário de Dnscmd.  

 Para mais informações sobre Dnscmd.exe, consulte [descrição geral de Dnscmd](http://technet.microsoft.com/library/cc778513%28WS.10%29.aspx).  

> [!NOTE]
>  DNS já deve estar instalado no computador de destino antes de executar este script.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConfigureDNS.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **DNSCMD.exe**. Ajuda os administradores de com gestão de DNS<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIConfigureDNS.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DNSServerOptionDisableRecursion**|-||  
|**DNSServerOptionBINDSecondaries**|-||  
|**DNSServerOptionFailOnLoad**|-||  
|**DNSServerOptionEnableRoundRobin**|-||  
|**DNSServerOptionEnableNetmaskOrdering**|-||  
|**DNSServerOptionEnableSecureCache**|-||  
|**DNSServerOptionNameCheckFlag**|-||  
|**DNSZonesxName**|-||  
|**DNSZonesxType**|-||  
|**DNSZonesxMasterIP**|-||  
|**DNSZonesxDirectoryPartition**|-||  
|**DNSZonesxFileName**|-||  
|**DNSZonesxScavenge**|-||  
|**DNSZonesxUpdate**|-||  

> [!NOTE]
>  O *x*nas propriedades de listados aqui é um marcador de posição para uma matriz baseada em zero que contém informações de configuração de DNS.  

###  <a name="ZTIConnect.wsf"></a>ZTIConnect.wsf  
 O processo de implementação do MDT utiliza este script para autenticar com um computador de servidor (por exemplo, um computador a executar o SQL Server ou noutro servidor que tenha uma pasta de rede partilhada). Quando este script é executado, valida que pode criar uma ligação para a pasta partilhada de rede especificada no **/uncpath** argumento.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIConnect.log**.  Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIConnect.wsf /UNCPath:<uncpath> </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/UNCPath:uncpath**|Especifica um caminho completamente qualificado de UNC para uma pasta partilhada de rede|  
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTICopyLogs.wsf"></a>ZTICopyLogs.wsf  
 Copie os ficheiros Smsts.log e BDD.log para uma subpasta sob a partilha de que o **SLShare** Especifica a propriedade. A subpasta aceita o nome que **OSDComputerName**, **smstsmachinename**, ou **HostName** especifica.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTICopyLogs.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTICopyLogs.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: *valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTIDataAccess.vbs"></a>ZTIDataAccess.vbs  
 Este script contém rotinas comuns para acesso de base de dados.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIDataAccess.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|Nenhum|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTIDataAccess.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_SMSTSReserved1**|-||  
|**_SMSTSReserved2**|-||  
|**RulesFile**|-||  
|**UserDomain**|-|-|  
|**ID de utilizador**|-|-|  
|**UserPassword**|-|-|  

###  <a name="ZTIDisableBDEProtectors.wsf"></a>ZTIDisableBDEProtectors.wsf  
 Se o BitLocker estiver ativado, este script suspende os protetores de BitLocker configurados no sistema.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIDisableBDEProtectors.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIDisableBDEProtectors.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**ImageBuild**|-||  
|**ISBDE**||-|  
|**OSCurrentBuild**|-||  
|**OSCurrentVersion**|-||  
|**OSVersion**|-||  

###  <a name="ZTIDiskpart.wsf"></a>ZTIDiskpart.wsf  
 Este script cria as partições de disco no computador de destino ao chamar o utilitário Diskpart. Os parâmetros utilizados para configurar o disco são especificados pelo Sequencer tarefas ou na CustomSettings.ini. ZTIDiskpart.wsf principalmente é executado em cenários de novo computador. O processo funciona da seguinte forma:  

1.  O processo de implementação do MDT executa o script de ZTIDiskpart.wsf com base dos passos e a sequência de passos do sequenciador de tarefas.  

2.  ZTIDiskpart.wsf inicia o utilitário Diskpart e envia-os comandos de configuração necessárias.  

3.  ZTIDiskpart.wsf executa Diskpart.exe e fornece um ficheiro. txt como um parâmetro da linha de comandos.  

4.  O disco inicialmente limpos enviando Diskpart o **limpar** comando.  

5.  Se este é o primeiro disco e não foi especificada nenhuma configuração de disco pelo sequenciador de tarefas ou no CustomSettings.ini, é criada uma única partição para armazenar o sistema operativo. No entanto, se tiver sido especificada uma configuração de disco, o disco será configurado, de acordo com a configuração especificada.  

6.  Se o BitLocker estiver ativado, está reservado espaço no final do primeiro disco.  

7.  Todos os comandos de formato são colocados em fila até após a conclusão da Diskpart. Se não explicitamente especificado pelo Sequencer tarefas ou em CustomSettings.ini, ZTIDiskpart.wsf efetua uma formatação rápida da unidade C utilizando o seguinte comando: `FORMAT C: /FS:NTFS /V:OSDisk /Q /Y`.  

8.  ZTIDiskpart.wsf copia os ficheiros de ZTIDiskpart_diskpart.log e BDD.log do disco de RAM para o disco rígido.  

 Personalize a configuração do disco do computador de destino, fornecendo as informações necessárias no sequenciador de tarefas ou no CustomSettings.ini.  

 Para obter mais informações sobre a configuração de discos, consulte o documento de MDT *utilizar o Microsoft Deployment Toolkit*.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIDiskpart.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **DiskPart.exe**. Utilitário que permite a gestão automática de discos, partições e volumes<br /><br /> -                          **Format.com**. Formata o disco rígido<br /><br /> -                          **ZTIDiskUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIDiskpart.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**BDEDriveLetter**|-||  
|**BDEDriveSize**|-||  
|**BDEInstall**|-||  
|**DeployDrive**|-||  
|**DeploymentType**|-||  
|**DestinationDisk**|-||  
|**DestinationLogicalDrive**||-|  
|**DoNotCreateExtraPartition**|-||  
|**ImageBuild**|-||  
|**OSDDiskIndex**|-||  
|**OSDDiskpartBiosCompatibilityMode**|-|-|  
|**OSDDiskType**|-||  
|**OSDPartitions**|-||  
|**OSDPartitionStyle**|-||  
|**SMSTSLocalDataDrive**||-|  
|**VolumeLetterVariable**|-||  

###  <a name="ZTIDiskUtility.vbs"></a>ZTIDiskUtility.vbs  
 Este script contém funções relacionadas com o disco e subroutines que os scripts de vários na implementação do MDT processam chamada.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|-                          **ZTIDiskUtility.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **BcdBoot.exe**. Configura a partição do sistema<br /><br /> -                          **DiskPart.exe**. Utilitário que permite a gestão automática de discos, partições e volumes|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTIDiskUtility.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DestinationLogicalDrive**|-||  
|**UILanguage**|-|-|  

###  <a name="ZTIDomainJoin.wsf"></a>ZTIDomainJoin.wsf  
 Durante a fase de implementação de restauro de estado, este script verifica se o computador estiver associado a um domínio e recupera de tentativas falhadas para associar um domínio.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIDomainJoin.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **LTISuspend.wsf**<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIDomainJoin.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: *valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ DomainErrorRecovery: *valor***|A tentar associar o computador ao domínio. Se o valor especificado no valor é:<br /><br /> -                              **AUTO**. Repita o processo de associação de domínio. Reinicie e tente novamente. Este é o comportamento de script predefinido.<br /><br /> -                              **FALHAR**. Interrompe a todo o processamento. Todas as paragem do processamento de sequência de tarefas.<br /><br /> -                              **MANUAL**. Parar processamento; permite ao utilizador associar manualmente o computador ao domínio.|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DomainAdmin**|-||  
|**DomainAdminDomain**|-||  
|**DomainAdminPassword**|-||  
|**DomainErrorRecovery**|-||  
|**DomainJoinAttempts**|-|-|  
|**JoinDomain**|-||  
|**JoinWorkgroup**|-||  
|**LTISuspend**||-|  
|**MachineObjectOU**|-||  
|**SMSTSRebootRequested**||-|  
|**SMSTSRetryRequested**||-|  

###  <a name="ZTIDrivers.wsf"></a>ZTIDrivers.wsf  
 Este script instala controladores de dispositivo adicionais no computador de destino antes de iniciar a configuração do sistema operativo. Este script lê o ficheiro Drivers.xml e copia a lista de ficheiros de controlador de dispositivo no ficheiro Drivers.xml (criados e geridos no nó controladores no Deployment Workbench) para o computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **PnpEnum.xml**. Contém uma lista de todos os dispositivos instalado no computador de destino<br /><br /> -                          **ZTIDrivers.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Attrib.exe**. Define os atributos de ficheiros e pastas<br /><br /> -                          **CMD.exe. Permite a execução de ferramentas da linha de comandos**<br /><br /> -                          **Microsoft.BDD.PnpEnum.exe**. Utilitário que enumera dispositivos Plug and Play<br /><br /> -                          **Reg.exe**. A ferramenta de registo de consola para ler e modificar os dados de registo<br /><br /> -                          **ZTIConfigFile.vbs**. Inclui rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIDrivers.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**CustomDriverSelectionProfile**|-||  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DestinationLogicalDrive**|-|-|  
|**DoCapture**|-||  
|**DriverPaths**|-||  
|**DriverSelectionProfile**|-||  
|**ImageBuild**|-||  
|**InstallFromPath**|-||  
|**OSDAnswerFilePath**|-||  
|**OSDAnswerFilePathSysPrep**|-||  
|**OSDPlatformArch**|-||  
|**Fase**|-||  
|**ResourceRoot**|-||  

###  <a name="ZTIExecuteRunbook.wsf"></a>ZTIExecuteRunbook.wsf  
 Este script executa os runbooks do Orchestrator no computador de destino. Um Orchestrator *runbook* é a sequência de atividades que orquestram ações em computadores e redes. Pode iniciar os runbooks do Orchestrator no MDT utilizando o [executar o Runbook](#ExecuteRunbook) tipo de passo de sequência, que por sua vez executa este script de tarefas.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|As variáveis de ambiente contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação.|  
|**Saída**|-BDD.log contém os eventos que geram todos os scripts de MDT.<br /><br /> -Estado devolvido da conclusão do runbook.<br /><br /> -Devolva os parâmetros da saída do runbook.|  
|**Referências**|-ZTIUtility.vbs inclui as funções de suporte e subroutines que utiliza o script.|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIExecuteRunbook.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**OrchestratorServer**|-||  
|**RunbookName**|-||  
|**RunbookID**|-||  
|**RunbookParameterMode**|-||  
|**RunbookParametersxParameterID**|-||  
|**RunbookParametersxParameterValue**|-||  
|***RunbookOutputParameters***<br /><br /> Nota:<br /><br /> Se um runbook devolve os parâmetros de saída, uma variável de sequência de tarefas é criada para cada um dos parâmetros e o valor devolvido do parâmetro está atribuído à variável de sequência de tarefas.||-|  

 Este script cria as variáveis de sequência de tarefas listadas na seguinte tabela para utilização interna de script. Não defina estas variáveis de sequência de tarefas no CustomSettings.ini ou na base de dados do MDT.  

|**Nome**|**Descrição**|  
|-|-|  
|**OrchestratorServer**|Nome do servidor a executar do Orchestrator especificado no **Orchestrator Server** no [executar o Runbook](#ExecuteRunbook) passo de sequência de tarefas|  
|**RunbookName**|Nome do runbook especificado no **Runbook** no [executar o Runbook](#ExecuteRunbook) passo de sequência de tarefas|  
|**RunbookID**|Identificador atribuído para o runbook no servidor do Orchestrator|  
|**RunbookParametersxParameterID**|Identificador atribuído a um parâmetro de runbook específico no servidor do Orchestrator|  
|**RunbookParametersxParameterName**|Nome atribuído a um parâmetro de runbook específico no servidor do Orchestrator|  
|**RunbookParametersxParameterValue**|Valor atribuído a um parâmetro de runbook específico no servidor do Orchestrator|  

###  <a name="ZTIGather.wsf"></a>ZTIGather.wsf  
 Este script reúne as propriedades e as regras de processamento que controlam o processo de implementação. As propriedades e regras (também conhecido como *propriedades local*) são explicitamente definido neste script e contidos no ficheiro ZTIGather.xml, no ficheiro CustomSettings.ini e na base de dados MDT (criada no nó de base de dados na implementação Workbench).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIGather.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Wpeutil.exe**. Inicia o Windows PE e ligações de rede inicia LTI<br /><br /> -                          **ZTIDataAccess.vbs**. Contém rotinas de acesso de base de dados<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIGather.wsf </debug:value> </localonly> </inifile:ini_file_name>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/localOnly**|Apenas devolverá informações sobre o computador de destino e o sistema operativo atual instalada no computador de destino; analisar o ficheiro de. ini de entrada (especificado no **/inifile** argumento); devolve propriedades e as regras especificadas no ficheiro. ini<br /><br /> Se não for especificado, o script devolve informações sobre o computador de destino e o sistema operativo atualmente instalado; analisa o ficheiro. ini|  
|**/Inifile:ini_file_name**|Nome e caminho do ficheiro. ini de entrada que contém as propriedades e regras utilizadas no processIf a implementação não especificado, o script utiliza o valor predefinido no CustomSettings.ini|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Todos os**|-|-|  

###  <a name="ZTIGroups.wsf"></a>ZTIGroups.wsf  
 Este script de captura e restaura a associação de grupo local no computador de destino. Este script é chamado com o**/capturar** argumento para a cópia de segurança a associação ao grupo do computador de destino antes de implementar o sistema operativo. O **CaptureGroups** propriedade contém a lista de grupos que o script cria cópias de segurança. O script é chamado com o**/restaurar** argumento para restaurar a associação a grupos após o sistema operativo é implementado. Quando efetuar uma operação de restauro, restaura a associação de todos os grupos que foram copiados em segurança durante a execução do script utilizando o **/capturar** argumento.  

> [!NOTE]
>  Ao restaurar a associação ao grupo, o script não criar quaisquer grupos de destino que já existe no computador de destino. Por conseguinte, não se esqueça de incluir todos os grupos necessários no computador de referência ao criar o ficheiro de imagem.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIGroups.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que gera todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIGroups.wsf </debug:value> </backup> </restore>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/Capture**|Cria cópias de segurança a associação a grupos dos grupos locais no computador de destino, conforme especificado no **CaptureGroups** propriedade|  
|**/Restore**|Restaura as associações aos grupos locais de cópia de segurança anteriormente no processo de implementação|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**CaptureGroups**|-||  
|**Grupos**|-|-|  
|Nome de anfitrião|-||  

###  <a name="ZTILangPacksOnline.wsf"></a>ZTILangPacksOnline.wsf  
 Este script instala os pacotes de idiomas para os sistemas operativos Windows.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTILangPacksOnline.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Lpksetup.exe**. A ferramenta de configuração de pacote de idioma utilizada para adicionar ou remover pacotes de idiomas<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTILangPacksOnline.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**OSVersion**|-||  

###  <a name="ZTIModifyVol.wsf"></a>ZTIModifyVol.wsf  
 Este script modifica um volume para definir os atributos para volumes de utilitário e GPT ID que é necessário para a criação de partições do Windows RE em computadores com UEFI. Este script tem de ser chamado quando a implementar em computadores com UEFI para estas situações:  

-   Implementações LTI onde estruturas de partições personalizado (volume) estão a ser criadas, tais como criar uma partição cinco em vez das partições de quatro padrão são typicaly criada para utilizar com UEFI  

-   Todas as implementações ZTI e UDI  

> [!NOTE]
>  Este script se destina a ser chamado apenas quando criar estruturas de partições para utilizam com UEFI. Este script não deve ser chamado durante a criação de partições estruturas de modo a ser utilizados em implementações sem UEFI.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|BDD.log contém os eventos que geram todos os scripts de MDT.|  
|**Referências**|ZTIUtility.vbs inclui as funções de suporte e subroutines que utiliza o script.|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIModifyVol.wsf /UtilityVol:value </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ UtilityVol: * valor***|Fornece a letra de unidade do volume que tem de ser configurado para uma partição do Windows RE ferramentas para utilização com computadores com UEFI (por exemplo, "e")|  
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**UtilityVol**|-||  

###  <a name="ZTIMoveStateStore.wsf"></a>ZTIMoveStateStore.wsf  
 Este script move o estado de utilizador capturados e os ficheiros de cópia de segurança para C:\Windows\Temp\StateStore.  

> [!NOTE]
>  Este script é executado apenas quando a implementação de imagens com o Configuration Manager.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIMoveStateStore.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIMoveStateStore.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTINextPhase.wsf"></a>ZTINextPhase.wsf  
 Este script atualiza o **fase** propriedade para a fase seguinte no processo de implementação. O sequenciador de tarefas utiliza estas fases para determinar a sequência em que cada tarefa tem de ser concluída. O **fase** propriedade inclui os seguintes valores:  

-   **VALIDAÇÃO**. Identifica-se de que o computador de destino é capaz de executar os scripts necessários para concluir o processo de implementação.  

-   **STATECAPTURE**. Guarde os dados de migração de estado do utilizador antes de implementar o novo sistema operativo de destino.  

-   **PREINSTALL**. Conclua todas as tarefas que precisam de ser feito (como criar novas partições) antes de implementar o sistema operativo de destino.  

-   **INSTALAR**. Instale o sistema de operativo de destino no computador de destino.  

-   **POSTINSTALL**. Conclua todas as tarefas que precisam de ser efetuadas antes de restaurar os dados de migração de estado do utilizador. Estas tarefas personalizar o sistema de operativo de destino antes de iniciar o computador de destino pela primeira vez após a implementação (como instalar atualizações ou adicionar controladores).  

-   **STATERESTORE**. Restaure os dados de migração de estado de utilizador guardados durante a fase de captura de estado.  

 Para obter mais informações sobre o **fase** propriedade, consulte o tópico correspondente no [propriedades](#Properties).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTINextPhase.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTINextPhase.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeploymentMethod**|-||  
|**Fase**|-|-|  

###  <a name="ZTINICConfig.wsf"></a>ZTINICConfig.wsf  
 Este script configura adaptadores de rede ativada com valores ZTIGather.wsf capturado com base nas propriedades listadas no ficheiro CustomSettings.ini ou da base de dados do MDT (criada no nó de base de dados no Deployment Workbench).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTINICConfig.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTINicUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTINicConfig.wsf </debug:value> </ForceCapture> </RestoreWithinWinPE>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ ForceCapture**|Se existirem quaisquer local adaptadores de rede com endereços IP estáticos, guardados, este script captura essas definições e guarda-os no ambiente local — por exemplo, C:\MININT\SMSOSD\OSDLogs\Variables.dat. Este script pode ser úteis para capturar as definições de IP estático para um grande número de computadores para a automatização.|  
|/ RestoreWithinWinPE|Quando especificado, aplica-se as definições de rede IP estáticas guardadas no computador local, quando adequado; utilizado para processar interna apenas.|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeployDrive**|-|-|  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DeployRoot**|-||  
|**OSDAdapterCount**|-|-|  
|**OSGuid**|-||  
|**OSDMigrateAdapterSettings**|-||  
|**Fase**|-||  

###  <a name="ZTINICUtility.vbs"></a>ZTINICUtility.vbs  
 Este script contém funções relacionadas com o adaptador de rede e subroutines que os scripts de vários na implementação do MDT processam chamada.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Netsh.exe**. Um utilitário utilizado para automatizar a configuração de componentes de rede|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTINicUtility.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**OSDAdapter * AdapterIndexAdapterName***|-|-|  

> [!NOTE]
>  *AdapterIndex*esta propriedade é um marcador de posição para uma matriz baseada em zero que contém as informações da placa de rede.  

###  <a name="ZTIOSRole.wsf"></a>ZTIOSRole.wsf  
 Este script instala as funções de servidor para computadores de destino que estejam a executar sistemas operativos Windows. O script lê o **OSRoles**, **OSRoleServices**, e **OSFeatures** propriedades para determinar o que deve ser instalado.  

> [!NOTE]
>  Este script se destina a ser chamado apenas pelo **instalar funções e funcionalidades** e**desinstalar funções e funcionalidades** passos de sequência de tarefas. Não é suportado a chamar diretamente este script.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIOSRole.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **OCSetup.exe**. Adiciona ou remove componentes opcionais do Windows<br /><br /> -                          **ServerManagerCmd.exe**. Instala, configura e gere o Windows Server funções e funcionalidades<br /><br /> -                          **Sysocmgr.exe**. Adiciona ou remove os componentes do Windows<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIOSRole.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ Desinstalação**|Se for indicado, este argumento indica que as funções e funcionalidades serão desinstaladas. Se não for indicado, o script pressupõe que as funções e funcionalidades serão instaladas.|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**IsServerCoreOS**|-||  
|**OSFeatures**|-||  
|**OSRoles**|-||  
|**OSRoleServices**|-||  
|**OSVersion**|-||  
|**SMSTSRebootRequested**||-|  

###  <a name="ZTIPatches.wsf"></a>ZTIPatches.wsf  
 Este script instala atualizações (pacotes de idiomas, atualizações de segurança e assim sucessivamente) que estão listadas no ficheiro Packages.xml. O script Self-termina se a implementação não está a ser um dos seguintes Estados:  

-   **Fase** é igual a **PREINSTALL**  

-   **DeploymentMethod** é igual a **SCCM**  

 O script inicia Pkgmgr se **DeploymentMethod** é igual a **SCCM**.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIPatches.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Expand.exe**. Expande os ficheiros comprimidos<br /><br /> -                          **Pkgmgr.exe**. Instala ou atualiza o Windows Vista offline<br /><br /> -                          **ZTIConfigFile.vbs**. Inclui rotinas de processamento de ficheiros XML<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIPatches.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**CustomPackageSelectionProfile**|-||  
|**DeployRoot**|-||  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DestinationLogicalDrive**|-||  
|**LanguagePacks**|-||  
|**OSDAnswerFilePath**|-||  
|**OSDPlatformArch**|-||  
|**PackageSelectionProfile**|-||  
|**Fase**|-||  
|**ResourceRoot**|-||  

###  <a name="ZTIPowerShell.wsf"></a>ZTIPowerShell.wsf  
 Este script executa um script do Windows PowerShell através de um anfitrião personalizado do Windows PowerShell.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIPowerShell.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT<br /><br /> -                          **Código de retorno**. O valor numérico devolvido pelo script do Windows PowerShell após a conclusão, o que indica o estado de conclusão do script.|  
|**Referências**|-                          **Microsoft.BDD.TaskSequencePSHost.exe**. Anfitrião do Windows PowerShell personalizado utilizado para executar o script do Windows PowerShell.|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIPowerShell.wsf`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**Nenhum**||  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Nenhum**|||  

###  <a name="ZTIPrereq.vbs"></a>ZTIPrereq.vbs  
 Este script verifica se o computador de destino tem os pré-requisitos de software instalado e que está funcional. As verificações que o script executa são:  

-   Determine se a versão do Script do Windows é igual ou superior à versão 5.6.  

-   Certifique-se de que não ocorrer erros ao objeto referências são instanciadas para Wscript.Shell, Wscript.Network, Scripting.FileSystemObject MSXML2. DOMDocument e o ambiente de processo.  

 Se qualquer uma das verificações falha, é gerado um erro e o script sair o **ValidatePrereq** procedimento.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|Nenhum|  
|**Saída**|Nenhum|  
|**Referências**|Nenhum|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`None`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|Nenhum|||  

###  <a name="ZTISCCM.wsf"></a>ZTISCCM.wsf  
 Este script inicializa ZTI quando implementar a utilizar o Configuration Manager. O script executa o seguinte procedimento:  

1.  Se a depuração está ativada, o script cria o OSD. Ficheiro de depuração.  

2.  O script configura estas propriedades:  

    -   **ScriptRoot**está definido para a pasta principal do script em execução.  

    -   **DeployRoot** está definido para a pasta principal do **ScriptRoot**.  

    -   **ResourceRoot** está definido como **DeployRoot**.  

    -   **DeploySystemDrive** está definido como **c:**.  

    -   **DeploymentMethod** está definido como **SCCM**.  

3.  Quando **DeployRoot**contém **:\\***:*  

    -   O **DeployRoot** pasta é copiada para **smstsmdatapath**\WDPackage  

    -   **ScriptRoot** está definido como **smstsmdatapath**\WDPackage\Scripts  

    -   **DeployRoot** está definido para a pasta principal do **ScriptRoot**  

    -   **ResourceRoot** está definido como **DeployRoot**  

4.  Quando **fase** é **nulo**:  

    -   Se a variável de ambiente % SystemDrive % **x:**, em seguida, **DeploymentType**está definido como **NEWCOMPUTER** e **fase** está definido como **PREINSTALL**. Caso contrário,**DeploymentType** está definido como **substituir** e **fase** está definido como **validação**.  

    -   Se o **OldComputer**ficheiro .tag existe na pasta principal do script em execução atual, **DeploymentType** está definido como **substituir** e **fase**está definido como **validação**. Caso contrário,**DeploymentType** está definido como **ATUALIZAR** e **fase** está definido como **validação**.  

 Para obter mais informações sobre estas propriedades, consulte os tópicos correspondentes [propriedades](#Properties).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTISCCM.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTISCCM.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Smstsmdatapath**|-||  
|**Arquitetura**|-||  
|**BDDPackageID**|-|-|  
|**DeploymentMethod**|-|-|  
|**DeploymentType**|-|-|  
|**DeployRoot**|-|-|  
|**Fase**|-|-|  
|**ResourceRoot**|-|-|  
|**ScriptRoot**|-|-|  
|**ToolRoot**|-|-|  

###  <a name="ZTISetVariable.wsf"></a>ZTISetVariable.wsf  
 Este script define a variável de sequência de tarefas global especificada que corresponde ao nome contido no **VariableName** para o valor contido no **VariableValue**.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTISetVariable.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|**ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTISetVariable.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**VariableName**|-||  
|**VariableValue**|-||  

###  <a name="ZTITatoo.wsf"></a>ZTITatoo.wsf  
 Este script tattoos o computador de destino com informações de identificação e a versão. O script executa o seguinte procedimento:  

1.  Localize e copie o ficheiro ZTITatoo.mof para a pasta de %SystemRoot%\System32\Wbem. Serão eliminados quaisquer ZTITatoo.mof pré-existentes que existe no destino antes de iniciar a operação de cópia.  

2.  Mofcomp.exe será executada utilizando o seguinte comando:  

    ```  
    %SystemRoot%\System32\Wbem\Mofcomp.exe -autorecover %SystemRoot%\System32\Wbem\ZTITatoo.mof.  
    ```  

3.  Para todos os métodos de implementação (LTI, ZTI e UDI), estes detalhes de implementação são escritos para todos os métodos de implementação para o registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:  

    -   **Método de implementação** está definido para o método de implementação que está a ser utilizado e pode ser definido como **LTI**, **ZTI**, ou **UDI**, consoante o método de implementação a ser efetuar.  

    -   **Origem de implementação** está definido como origem para a implementação e pode ser definido como **OEM**, **multimédia**, ou o valor do **DeploymentMethod** propriedade.  

    -   **Tipo de implementação** está definido como o **DeploymentType** propriedade.  

    -   **Implementação Timestamp** está definido para a data atual no formato de data do WMI.  

    -   **Versão do Toolkit de implementação** está definido como o **versão** propriedade.  

4.  Para implementações LTI, estes detalhes de implementação são escritos no registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:  

    -   **ID de sequência de tarefas** está definido como o **TaskSequenceID**propriedade.  

    -   **Nome da sequência de tarefas** está definido como o **TaskSequenceName** propriedade.  

    -   **Versão de sequência de tarefas** está definido como o **TaskSequenceVersion** propriedade.  

5.  Para todas as implementações de Configuration Manager (ZTI e UDI para o Configuration Manager), estes detalhes de implementação são escritos no registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:  

    -   O ID de pacote de OSD está definido o **_SMSTSPackageID** variável de sequência de tarefas.  

    -   **Nome do programa de OSD** está sempre definido como "**\***".  

    -   **ID de anúncio de OSD** está definido como o **_SMSTSAdvertID** variável de sequência de tarefas.  

6.  Para implementações de LTI onde uma imagem está a ser capturada, estes detalhes de implementação são escritos no registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:  

    -   **Captura de método** está definido para o método de implementação que está a ser utilizado e pode ser definido como **LTI**, **ZTI**, ou **UDI**, consoante o método de implementação a ser efetuar.  

    -   **Capturar Timestamp** está definido para a data atual no formato de data do WMI.  

    -   **Versão do Toolkit de captura** está definido como o **versão** propriedade.  

    -   **ID de sequência de tarefas de captura** está definido como o **TaskSequenceID**propriedade.  

    -   **Capturar o nome da sequência de tarefas** está definido como o **TaskSequenceName** propriedade.  

    -   **Versão de sequência de tarefas de captura** está definido como o **TaskSequenceVersion** propriedade.  

7.  Para todas as do Configuration Manager implementações (ZTI e UDI para o Configuration Manager) no qual está a ser capturada uma imagem, estes detalhes de implementação são escritos no registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4** :  

    -   **Captura de ID de pacote de OSD** está definido como o **_SMSTSPackageID** variável de sequência de tarefas.  

    -   **Capturar o nome do programa de OSD** está sempre definido como "***".  

    -   **Captura de ID de anúncio de OSD** está definido como o **_SMSTSAdvertID**variável de sequência de tarefas.  

    > [!NOTE]
    >  Este script não foi concebido para ser executada no Windows PE.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTITatoo.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Mofcomp.exe**. Compilador do ficheiro da linha de comandos. MOF<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTITatoo.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_SMSTSAdvertID**|-||  
|**_SMSTSPackageID**|-||  
|**_SMSTSSiteCode**|-||  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**Versão**|-||  
|**TaskSequenceID**|-||  
|**TaskSequenceName**|-||  
|**TaskSequenceVersion**|-||  

###  <a name="ZTIUserState.wsf"></a>ZTIUserState.wsf  
 Este script inicializa USMT para capturar e restaurar o estado do utilizador no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIUserState.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Loadstate.exe**. Depósitos dados de estado do utilizador num computador de destino<br /><br /> -                          **Msiexec.exe**. Gere a instalação de aplicações baseadas em. msi<br /><br /> -                          **Scanstate.exe**. Recolhe dados de utilizador e definições<br /><br /> -                          **Ficheiros de aplicação do USMT**<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIUserState.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|/Debug:value|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ Captura**|–|  
|**/ Estimativa**|–|  
|**/ Restauro**|–|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**DeploymentMethod**|-||  
|**DeploymentType**|-||  
|**DestinationLogicalDrive**|-||  
|**ImageBuild**|-||  
|**ImageSize**|-||  
|**ImageSizeMultiplier**|-||  
|**InstallFromPath**|-||  
|**IsServerOS**|-||  
|**LoadStateArgs**|-||  
|**OSCurrentVersion**|-||  
|**OSDMigrateAdditionalCaptureOptions**|-|-|  
|**OSDMigrateAdditionalRestoreOptions**|-|-|  
|**OSDPackagePath**|-||  
|**OSDStateStorePath**||-|  
|**OSVersion**|-||  
|**ScanStateArgs**|-||  
|**StatePath**|-|-|  
|**UDDir**|-||  
|**UDProfiles**|-||  
|**UDShare**|-||  
|**UserDataLocation**|-|-|  
|**USMTConfigFile**|-||  
|**USMTEstimate**|-|-|  
|**USMTLocal**||-|  
|**USMTMigFiles**|-||  

###  <a name="ZTIUtility.vbs"></a>ZTIUtility.vbs  
 Este script contém funções de utilitário que utilizam a maioria dos MDT scripts.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|Nenhum|  
|**Referências**|-                          **Credentials_ENU.XML**. Pede ao utilizador as credenciais que será utilizada ao ligar a recursos de rede<br /><br /> -                          **IPConfig.exe**. Apresenta todos os valores de configuração de rede do TCP/IP atuais e atualiza as definições de DHCP e DNS<br /><br /> -                          **MSHTA.exe**. Anfitrião de aplicação HTML<br /><br /> -                          **Regsvr32.exe**. Regista os ficheiros (. dll, .exe,. ocx e assim sucessivamente) com o sistema operativo<br /><br /> -                          **Xcopy.exe**. Ficheiros de cópias e diretórios, incluindo subdiretórios|  
|**Localização**|-                          *distribuição*\Scripts<br /><br /> -                          *Program_Files*\Microsoft Deployment Toolkit\Scripts|  
|**Utilize**|`<script language="VBScript" src="ZTIUtility.vbs"/>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|Nenhum|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**_SMSTSAdvertID**|-||  
|**Smstscurrentactionname**|-||  
|**_SMSTSCustomProgressDialogMessage**|-||  
|**_SMSTSInstructionTableSize**|-||  
|**Smstslogpath**|-||  
|**Smstsmachinename**|-||  
|**_SMSTSNextInstructionPointer**|-||  
|**Smstsorgname**|-||  
|**_SMSTSPackageID**|-||  
|**_SMSTSPackageName**|-||  
|**_SMSTSPackagePath**|-||  
|**_SMSTSReserved1**|-||  
|**_SMSTSReserved2**|-||  
|**Arquitetura**|-||  
|**AssetTag**|-||  
|**ComputerName**|-||  
|**Depuração**|-|-|  
|**DeploymentMethod**|-||  
|**DeployRoot**|-||  
|**DestinationDisk**|-|-|  
|**DestinationLogicalDrive**|-|-|  
|**DestinationPartition**|-|-|  
|**EventShare**|-||  
|**Nome de anfitrião**|-||  
|**ImageBuild**|-|-|  
|**ImageFlags**||-|  
|**ImageIndex**||-|  
|**ImageLanguage**||-|  
|**ImageProcessor**||-|  
|**ImageSize**||-|  
|**InstallFromPath**||-|  
|**JoinDomain**|-||  
|**LogPath**|-|-|  
|**MacAddress**|-||  
|**OSCurrentVersion**|-||  
|**OSDAdvertID**|-||  
|**OSDAnswerFilePath**|-|-|  
|**OSDAnswerFilePathSysprep**|-|-|  
|**OSDComputerName**|-|-|  
|**OSDPackageID**|-||  
|**OSDPackagePath**|-||  
|**OSDTargetSystemDrive**|-||  
|**OSGUID**||-|  
|**OSSKU**|-||  
|**OSVersion**|-||  
|**Fase**|-||  
|**Processor_Architecture**|-||  
|**ResourceRoot**|-||  
|**SLShare**|-||  
|**SLShareDynamicLogging**|-||  
|**TaskSequenceID**|-||  
|**TaskSequenceName**||-|  
|**TaskSequenceVersion**||-|  
|**UDDir**|-||  
|**UDShare**|-||  
|**UserDomain**|-|-|  
|**ID de utilizador**|-|-|  
|**UserPassword**|-|-|  
|**UUID**|-||  
|**Versão**<br /><br /> **Nota:** Esta variável é uma variável interna que representa a versão do MDT.|-|-|  
|**WDSServer**|-||  

###  <a name="ZTIValidate.wsf"></a>ZTIValidate.wsf  
 Este script garante que é seguro para a implementação para continuar ao validar a condição do computador de destino. Os processos de script são:  

-   Se **DeploymentType** é igual a ATUALIZAÇÃO e o computador de destino é um servidor, o script sair.  

-   Se **OSInstall** existe e não é igual a Sim, o script sair.  

-   Certifique-se de que a quantidade mínima de RAM existe no computador de destino; caso contrário, o script sair.  

-   Certifique-se de que o processador cumpre a mínimo necessária velocidade; caso contrário, o script sair.  

-   Certifique-se de que o tamanho de disco rígido cumpre os requisitos de tamanho mínimo; caso contrário, o script sair.  

-   Certifique-se de que o sistema operativo do computador de destino está instalado na unidade C; caso contrário, o script sair.  

-   Se **DeploymentType = ATUALIZAÇÃO**, certifique-se de que a unidade C não será comprimida executando `Compact /u C:\`.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIValidate.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Compact.exe**. Apresenta ou altera a compressão de ficheiros em partições de sistema de ficheiros NTFS<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIValidate.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**DeploymentType**|-||  
|**DestinationLogicalDrive**|-|-|  
|**ImageBuild**|-||  
|**ImageMemory**|-||  
|**ImageProcessorSpeed**|-||  
|**ImageSize**|-||  
|**ImageSizeMultiplier**|-||  
|**IsServerOS**|-||  
|**Memória**|-||  
|**OSDPackagePath**|-||  
|**OSInstall**|-||  
|**ProcessorSpeed**|-||  
|**SMSTSLocalDataDrive**||-|  
|**VerifyOS**|-||  

###  <a name="ZTIVHDCreate.wsf"></a>ZTIVHDCreate.wsf  
 Este script é utilizado para criar um ficheiro de (. vhd ou. avhd) de disco rígido virtual no computador de destino e montar o ficheiro. vhd como um disco. Em seguida, outras partes do processo de implementação LTI implementar o sistema operativo Windows e aplicações para o disco rígido virtual criado recentemente. Os processos de script são os seguintes:  

-   O **Class_Initialize** método é utilizado para inicializar o **VHDInputVariable** variável.  

-   Validar **VHDCreateSource** está definido e localiza o ficheiro. VHD de origem (se especificada).  

-   Gerar um nome de ficheiro. vhd aleatório se **VHDCreateFilename** aleatório de é igual a ou "" (nulo).  

-   Certifique-se de que existe a pasta onde o ficheiro. vhd (especificado na **VHDCreateFileName**) está a ser criado.  

-   Criar o ficheiro. VHD utilizando os valores existentes na **VHDCreateSizePercent**, **VHDCreateSizeMax**, e **VHDCreateType**.  

-   Criar um disco de diferenciação (se especificada) com o valor no **VHDCreateDiffVHD**.  

-   O ficheiro. vhd criado recentemente e o disco de diferenciação opcional estão montados.  

-   O número do disco do disco rígido virtual montado é devolvido.  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIVHDCreate.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **ZTIDiskUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIVHDCreate.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**VHDCreateDiffVHD**|-||  
|**VHDCreateFileName**|-||  
|**VHDCreateSizeMax**|-||  
|**VHDCreateSource**|-||  
|**VHDCreateType**|-||  
|**VHDDisks**||-|  
|**VHDInputVariable**|-||  
|**VHDOutputVariable**|-||  

###  <a name="ZTIWindowsUpdate.wsf"></a>ZTIWindowsUpdate.wsf  
 Este script transfere e instala as atualizações de computadores na rede empresarial que estejam a executar o WSUS, o Windows Update ou Microsoft Update utilizando o [Windows Update Agent (WUA)](http://msdn2.microsoft.com/library/Aa387099.aspx) interface de programação de aplicações (API). Por predefinição, esta funcionalidade está desativada na cada sequência de tarefas e tem de ser manualmente ativada para ser executada.  

 A maioria das empresas já terão equipas e infraestruturas no local para atualizar recentemente implementado computadores através da rede empresarial. Este processo envolve o conjunto mais recente de atualizações disponíveis para cada configuração de ambiente de trabalho, controladores e patches de controlo e determinar que atualizações devem ser transferidas e instaladas para cada configuração. Se a organização já tem um processo estabelecido, este script não pode ser necessário. Este script foi concebido para preencher uma necessidade para as equipas de implementação que poderá ter processos estabelecidos, ainda não pretende garantir que os computadores de destino são atualizados quando implementado.  

 Este script analisa o computador de destino e transfere uma vasta gama de atualizações que estão localizados para serem aplicáveis automaticamente. Entre estas são:  

-   Pacotes de serviço do Windows  

-   Controladores de sem ser da Microsoft que foram colocadas no Windows Update  

-   As atualizações mais recentes de correção  

-   Atualizações do Microsoft Office  

-   Atualizações do Microsoft Exchange Server e SQL Server  

-   Microsoft Visual Studio® atualizações  

-   Algumas atualizações de aplicações de terceiros  

> [!TIP]
>  Vários fabricantes de hardware tem colocados os controladores no Windows Update. Estes controladores já não precisam de ser mantida no diretório de controladores. Experimentação ao remover os controladores de partilha de distribuição para aqueles estão disponíveis no Windows Update. Tenha em atenção que o se os controladores não são incluídos com o Windows por predefinição, não remover a rede ou controladores de armazenamento, porque o sistema operativo irá exigir a intervenção do utilizador.  

 MDT suporta a capacidade de implementar uma versão atualizada do WUA como parte da implementação do sistema operativo. Isto ajuda a garantir que os computadores de destino estiver a executar a versão correta do WUA quando estão implementadas. Também ajuda a eliminar a necessidade de acesso à Internet e transferir a versão mais recente do WUA após a implementação.  

 MDT também pode configurar o WUA para recolher as atualizações de computadores na rede da empresa que estejam a executar o WSUS em vez de ligar ao Microsoft Updates através da Internet. MDT opcionalmente, pode configurar o WUA para utilizar um computador específico com o WSUS utilizando o **WSUSServer** propriedade.  

 Para obter informações adicionais e para obter instruções de implementação do WUA, consulte [como instalar o Windows Update Agent nos computadores cliente](http://technet.microsoft.com/library/bb932139.aspx).  

 Obter a versão mais recente do instalador autónomo do WUA para:  

-   x86 versões (WindowsUpdateAgent30 x86.exe) em [http://go.microsoft.com/fwlink/?LinkID=100334](http://go.microsoft.com/fwlink/?LinkID=100334)  

-   x64 versão (WindowsUpdateAgent30 x64.exe) no [http://go.microsoft.com/fwlink/?LinkID=100335](http://go.microsoft.com/fwlink/?LinkID=100335)  

 Windows 7 e posteriores incluem a versão mais recente do WUA, sendo necessária nenhum atualização.  

 Para obter mais informações, consulte [atualizar o Windows Update Agent](http://msdn2.microsoft.com/library/aa387285.aspx).  

 Quando ativado no sequenciador de tarefas, este script é executada várias vezes na fase de restauro do Estado de implementação do sistema operativo. É executado pela primeira vez depois do sistema operativo foi iniciado pela primeira vez. Certifique-se de que as atualizações mais recentes e service packs que são instalados antes da instalação de todas as aplicações que poderá dependem atualizações específicas ou pacotes de serviço que está a ser instalado no computador de destino. Por exemplo, uma aplicação pode ser depende a versão mais recente do Microsoft .NET Framework que está a ser instalado.  

 Este script também é executada após a instalação de aplicações, que garante que os pacotes do serviço de aplicações mais recentes e as atualizações foram aplicadas. Por exemplo, utilize este script para se certificar de que as atualizações mais recentes são aplicadas para Microsoft Office 2010 ou o sistema do Office 2007.  

 É possível que, durante a instalação de uma ou mais atualizações, o computador de destino terá de ser reiniciado para permitir uma instalação de atualização concluir a completamente. Certifique-se de que as atualizações estão corretamente instaladas, se o script Deteta que a instalação de uma atualização requer que o computador de destino ser reiniciado, o script automaticamente reinicia o computador de destino e retoma se atualizações adicionais foram detetadas e instalação pendente. O script sai se determina se o computador de destino é totalmente atualizado. Será registado um erro se, ao atualizar o computador de destino, o script tem sete tentativas sem êxito para instalar as atualizações e o computador de destino ainda requer um reinício.  

 Durante o tempo de execução, o script executa as seguintes tarefas:  

-   Configure o computador de destino para utilizar um servidor WSUS, se o **WSUSServer** propriedade foi especificada.  

-   Certifique-se de que a versão mais recente do WUA é instalada no computador de destino.  

-   Procure o computador de destino para detetar atualizações aplicáveis que ainda não estejam instaladas e que pode ser normalmente oculto.  

-   Cada atualização tenha um associados **UpdateID** e **QNumber** propriedade:  

    -   O **UpdateID** propriedade está no formato GUID, tais como *67da2176-5c57-4614-a514-33abbdd51f67*.  

    -   O **QNumber** propriedade é um valor numérico, tal como *987654*.  

-   O script compara o **UpdateID** e **KBArticle** valores de propriedade face à lista de exclusões especificado nas propriedades do MDT seguintes:  

    -   **WUMU_ExcludeID**. Uma lista de UpdateIDs para excluir; qualquer atualizar com um **UpdateID** encontrado na lista não será instalada.  

    -   **WUMU_ExcludeKB**. Uma lista de **QNumbers** para excluir; qualquer atualizar com um **QNumber** encontrado na lista não será instalada.  

    -   Além disso, qualquer atualização requer intervenção do utilizador será excluída e não instalada.  

-   Todas as atualizações que necessitem de aprovação de um contrato de licença do utilizador final (EULA) serão automaticamente ser aprovadas pelo script. Lembre-se de que manualmente ler e verificar cada EULA antes de executar este script num ambiente de produção.  

-   A atividade de cada atualização é escrita para o ficheiro de ZTIWindowsUpdate.log, com a cadeia de instalação ou ignorar se a atualização tiver sido aprovada para instalação, juntamente com o UpdateID, uma breve descrição da atualização e o QNumber.  

-   Cada atualização a instalar é transferida e instalada em lotes.  

-   O computador de destino pode exigir mais de um reinício durante a instalação da atualização.  

> [!NOTE]
>  Windows Internet Explorer 7 requer interação do utilizador, pelo que não está instalado com este script.  

> [!NOTE]
>  Por predefinição, incluem **QNumber 925471** no **WUMU_ExcludeKB** lista para impedir que Windows Vista Ultimate instalar pacotes de idiomas adicionais.  

> [!NOTE]
>  Se as origens de intranet não estiverem disponíveis, este script transfere ficheiros de dois sites da Microsoft: [http://update.microsoft.com/redist/wuredist.cab](http://update.microsoft.com/redist/wuredist.cab) e [http://download.windowsupdate.com/v6/windowsupdate/ redist/standalone/muauth.cab](http://download.windowsupdate.com/v6/windowsupdate/redist/standalone/muauth.cab).  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIWindowsUpdate.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **Expand.exe**. Expande os ficheiros comprimidos<br /><br /> -                          **NET.exe**. Executa tarefas de gestão de rede<br /><br /> -                          **WindowsUpdateAgent30 x86.exe**. Instala o WUA<br /><br /> -                          **WindowsUpdateAgent30 x64.exe**. Instala o WUA<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIWindowsUpdate.wsf </debug:value> </UpdateCommand:"<IsInstalled=0&#124;1> <IsHidden=0&#124;1>"> </Query:true&#124;false>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  
|**/ UpdateCommand: * param***|-                              **IsInstalled**. Definido como **0** a consulta para as atualizações que não estão instalados.<br /><br /> -                              **IsHidden**. Definido como **0** a consulta para as atualizações que estão ocultas.|  
|**/ Consultar: * valor***|-                              **Verdadeiro**. Consulta apenas para as atualizações necessárias. Não transferir e instalar os binários.<br /><br /> -                              **FALSO**. Consultar e instalar as atualizações necessárias. Transferir e instalar os binários.|  

> [!NOTE]
>  Quando especificado, **UpdateCommand** requer, pelo menos, uma opção.  

> [!NOTE]
>  Se especificar ambas as opções de **UpdateCommand**, devem ser separadas por *e*.  

> [!NOTE]
>  O valor predefinido para **UpdateCommand** é **IsInstalled = 0** e **IsHidden = 0**.  

> [!NOTE]
>  Para obter mais informações sobre **UpdateCommand**, consulte [IUpdateSearcher::Search método](http://msdn.microsoft.com/library/aa386526\(VS.85\).aspx).  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Arquitetura**|-||  
|**DoCapture**|-||  
|**InstalledUpdates**||-|  
|**MSIT_WU_Count**|-|-|  
|**NoAutoUpdate_Previous**|-|-|  
|**SMSTSRebootRequested**|-|-|  
|**SMSTSRetryRequested**|-|-|  
|**WSUSServer**|-||  
|**WUMU_ExcludeID**|-||  
|**WUMU_ExcludeKB**|-||  

###  <a name="ZTIWipeDisk.wsf"></a>ZTIWipeDisk.wsf  
 Este script formata o disco rígido do computador de destino. O script:  

-   Sai se **WipeDisk** não é igual ao **verdadeiro**  

-   Determina a unidade adequada para formatar  

-   Formata o disco ao chamar `cmd /c format <Drive> /fs:ntfs /p:3 /Y` (onde `<Drive>` é a letra de unidade da unidade de disco rígido ser formatado)  

|**Valor**|**Descrição**|  
|-|-|
|**Entrada**|**As variáveis de ambiente**. Contém os valores de propriedade, valores de propriedade personalizada, ligações de base de dados, regras de implementação e outras informações que os scripts necessitam para concluir o processo de implementação|  
|**Saída**|-                          **ZTIWipeDisk.log**. Ficheiro de registo que contém os eventos que este script gera<br /><br /> -                          **BDD.log**. Ficheiro de registo que contém os eventos que geram todos os scripts de MDT|  
|**Referências**|-                          **CMD.exe**. Permite a execução de ferramentas da linha de comandos<br /><br /> -                          **Format.com**. Formata o disco rígido<br /><br /> -                          **ZTIUtility.vbs**. Inclui as funções de suporte e subroutines que utiliza o script|  
|**Localização**|*distribuição*\Scripts|  
|**Utilize**|`cscript ZTIWipeDisk.wsf </debug:value>`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ debug: * valor***|Saídas as mensagens de evento para a consola e os ficheiros. log. Se o valor especificado no valor é:<br /><br /> -                              **Verdadeiro**, mensagens de evento são enviadas para a consola e os ficheiros. log<br /><br /> -                              **FALSO**, mensagens de evento são enviadas apenas para os ficheiros. log (este é o comportamento quando o argumento não for fornecido.)|  

#### <a name="properties"></a>Propriedades  

|**Nome**|**Leitura**|**Escrita**|  
|-|-|-|  
|**WipeDisk**|-||  

##  <a name="SupportFiles"></a>Ficheiros de suporte  
 Os scripts e utilitários utilizado em implementações LTI e ZTI ficheiros de configuração externos de referência para determinar as definições de configuração utilizadas durante o processo de implementação e passos do processo.  

 As seguintes informações são fornecidas para cada utilitário:  

-   **Nome**. Especifica o nome do ficheiro  

-   **Descrição**. Fornece uma descrição da finalidade do ficheiro  

-   **Localização**. Indica a pasta onde o ficheiro pode ser encontrado; as informações para a localização, são utilizadas as seguintes variáveis:  

    -   **Program_Files**. Esta variável aponta para a localização da pasta ficheiros de programa no computador onde está instalado o MDT.  

    -   **distribuição**. Esta variável aponta para a localização da pasta de distribuição para a partilha de implementação.  

    -   **plataforma**. Esta variável é um marcador de posição para a plataforma do sistema operativo (x86 ou x64).  

###  <a name="ApplicationGroups.xml"></a>ApplicationGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="Applications.xml"></a>Applications.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="BootStrap.ini"></a>BootStrap.ini  
 O ficheiro de configuração utilizado quando o computador de destino não é possível estabelecer ligação com a partilha de implementação adequada. Esta situação ocorre no novo computador e os cenários de substituir o computador.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="CustomSettings.ini"></a>CustomSettings.ini  
 O ficheiro de configuração principal para o MDT regras utilizadas em todos os cenários de processamento.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="Deploy.xml"></a>Deploy.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*Program_Files*\Microsoft Deployment Toolkit\Control|  

###  <a name="DriverGroups.xml"></a>DriverGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="Drivers.xml"></a>Drivers.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|Descrição|  
|-|-|  
|**Localização**|*distribuição*\Control|  

###  <a name="LinkedDeploymentShares.xml"></a>LinkedDeploymentShares.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="ListOfLanguages.xml"></a>ListOfLanguages.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="MediaGroups.xml"></a>MediaGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="Medias.xml"></a>Medias.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="OperatingSystemGroups.xml"></a>OperatingSystemGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="OperatingSystems.xml"></a>OperatingSystems.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="PackageGroups.xml"></a>PackageGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="Packages.xml"></a>Packages.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="SelectionProfileGroups.xml"></a>SelectionProfileGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="SelectionProfiles.xml"></a>SelectionProfiles.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="ServerManager.xml"></a>ServerManager.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*Program_Files*\Microsoft Deployment Toolkit\Bin|  

###  <a name="Settings.xml"></a>Settings.XML  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="TaskSequenceGroups.xml"></a>TaskSequenceGroups.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="TaskSequences.xml"></a>TaskSequences.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control|  

###  <a name="TS.xml"></a>TS.xml  

> [!NOTE]
>  Este ficheiro XML é gerido pelo MDT e não deve requerer a modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Control\\*task_sequence_id*|  

> [!NOTE]
>  *Task_sequence_id* é um marcador de posição para o ID de sequência de tarefas que lhe foi atribuído a cada sequência de tarefas quando foi criado no nó sequências de tarefas no Deployment Workbench.  

###  <a name="Wimscript.ini"></a>Wimscript.ini  
 Este ficheiro. ini é um ficheiro de configuração do ImageX que contém a lista de pastas e ficheiros que serão excluídos de uma imagem. Esta é referenciada por ImageX durante a fase de captura LTI.  

 Para obter ajuda com personalizar este ficheiro, consulte a secção "Criar um ImageX ficheiro de configuração" no *Guia do utilizador do ambiente de pré-instalação do Windows (Windows PE)*.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Tools\\*plataforma*|  

###  <a name="ZTIBIOSCheck.xml"></a>ZTIBIOSCheck.xml  
 Este ficheiro XML contém metadados sobre BIOSes para computadores de destino. Este ficheiro é editado manualmente e é lida por [ZTIBIOSCheck.wsf](#ZTIBIOSCheck.wsf). Extrair as informações necessárias a partir de um computador de destino para criar uma entrada neste ficheiro XML utilizando o programa de Microsoft Visual Basic® Scripting Edition (VBScript) (ZTIBIOS_Extract_Utility.vbs) que está incorporado neste ficheiro XML.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="ZTIConfigure.xml"></a>ZTIConfigure.xml  
 Este ficheiro XML é utilizado pelo [ZTIConfigure.wsf](#ZTIConfigure.wsf) script traduzir os valores de propriedade (especificados anteriormente no processo de implementação) para configurar as definições no ficheiro Unattend.xml. Este ficheiro já é personalizado para tornar as traduções apropriadas e não deve requerer mais modificação.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="ZTIGather.xml"></a>ZTIGather.xml  

> [!NOTE]
>  Este ficheiro XML é pré-configurado e não deve requerer a modificação. Defina as propriedades personalizadas no ficheiro CustomSettings.ini ou da base de dados do MDT.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="ZTIUserState_config.xml"></a>ZTIUserState_config.xml  
 Este ficheiro XML é utilizado pelo [ZTIUserState.wsf](#ZTIUserState.wsf) script como um ficheiro de configuração do USMT predefinido. Este ficheiro é utilizado por predefinição, se for especificado nenhum ficheiro de configuração personalizada pelo [USMTConfigFile](#USMTConfigFile) propriedade. Consulte o [Config.xml ficheiro](http://technet.microsoft.com/library/dd560760.aspx) tópico na documentação do USMT para obter mais informações sobre a sintaxe e de utilização.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

###  <a name="ZTITatoo.mof"></a>ZTITatoo.mof  
 Este ficheiro. MOF, quando importado para o repositório WMI do computador de destino utilizando Mofcomp.exe, cria o **Microsoft_BDD_Info** classe WMI. Esta classe contém informações relacionadas com a implementação, tais como:  

-   DeploymentMethod  

-   deploymentType  

-   DeploymentTimestamp  

-   BuildID  

-   BuildName  

-   BuildVersion  

-   OSDPackageID  

-   OSDProgramName  

-   OSDAdvertisementID  

-   TaskSequenceID  

-   TaskSequenceName  

-   TaskSequenceVersion  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Scripts|  

## <a name="utilities"></a>Utilitários  
 Os scripts utilizar LTI e ZTI utilitários de referência que efetuem tarefas especializadas, os passos utilizados durante o processo de implementação de suporte. Utilize as seguintes informações para ajudar a determinar os utilitários corretos para incluir as ações e os argumentos válidos para fornecer ao executar cada utilitário.  

 As seguintes informações são fornecidas para cada utilitário:  

-   **Nome**. Especifica o nome do utilitário  

-   **Descrição**. Fornece uma descrição da finalidade do utilitário  

-   **Localização**. Indica a pasta onde é possível encontrar o utilitário; as informações para a localização, são utilizadas as seguintes variáveis:  

    -   **Program_Files**. Esta variável aponta para a localização da pasta ficheiros de programa no computador onde está instalado o MDT.  

    -   **distribuição**. Esta variável aponta para a localização da pasta de distribuição para a partilha de implementação.  

    -   **plataforma**. Esta variável é um marcador de posição para a plataforma do sistema operativo (x86 ou x64).  

-   **Utilize**. Fornece os comandos e as opções que podem ser especificadas  

-   **Os argumentos e uma descrição**. Indica os argumentos válidos para ser especificado para o utilitário e uma breve descrição do que significa que cada argumento  

###  <a name="BCDBoot.exe"></a>BCDBoot.exe  
 BCDBoot é uma ferramenta utilizada para configurar rapidamente a uma partição do sistema ou reparar o ambiente de arranque localizado na partição de sistema. A partição do sistema é configurada ao copiar um pequeno conjunto de ficheiros do ambiente de arranque de uma imagem do Windows instalada. BCDBoot também cria um arquivo de dados de configuração de arranque (BCD) na partição do sistema, com uma nova entrada de arranque, que permite que o Windows arrancar a imagem do Windows instalada.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte a ajuda da linha de comandos fornecida por este utilitário.|  

###  <a name="BDDRun.exe"></a>BDDRun.exe  
 Este utilitário é executado como uma ação, o sequenciador de tarefas para executáveis (por exemplo, um script ou outro código) que exigem a interação do utilizador. Por predefinição, a sequência de tarefas não é possível executar um executável que necessite de interação do utilizador. No entanto, este utilitário permite o sequenciador de tarefas executar um executável que necessite de interação do utilizador.  

 O executável que necessite de interação do utilizador é fornecido como um argumento para este utilitário. Este utilitário é executado o executável num ambiente de comando diferente.  

> [!NOTE]
>  Este utilitário só pode ser utilizado em implementações LTI. Implementações ZTI proíbem qualquer interação do utilizador.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Tools\\*plataforma*|  
|**Utilize**|`BDDRun.exe commandline`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|*linha de comando*|O comando ser executado que requer interação do utilizador|  

> [!NOTE]
>  Colocar as aspas à volta de qualquer parte do *da linha de comandos* parte do argumento que contém espaços em branco. Por exemplo: `BDDRun.exe MyAppInstall.exe /destinationdir: "%ProgramFiles%\AppName"`.  

###  <a name="Bootsect.exe"></a>Bootsect.exe  
 Bootsect.exe atualiza o código de arranque principal para partições de disco rígido alternar entre BOOTMGR e NTLDR. Utilize este utilitário para restaurar o setor de arranque no computador.  

 Para obter mais informações sobre Bootsect.exe, consulte a secção "Opções da linha de comandos Bootsect", no *Guia do utilizador do ambiente de pré-instalação do Windows (Windows PE)*.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Tools\\*plataforma*|  
|**Utilize**|`bootsect.exe /nt52 C:`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/ Ajuda**|Mostra as instruções de utilização listadas aqui.|  
|**/nt52**|Aplica-se o código de arranque principal compatível com NTLDR para **SYS**, **todos os**, ou *Letradaunidade*. O sistema operativo instalado no **SYS**, **todos os**, ou *Letradaunidade* tem de ser uma versão anterior do Windows Vista.|  
|**/NT60**|Aplica-se o código de arranque principal compatível com BOOTMGR para **SYS**, **todos os**, ou *Letradaunidade*. O sistema operativo instalado no **SYS**, **todos os**, ou *Letradaunidade* tem de ser Windows Vista.|  
|**SYS**|Atualiza o código de arranque principal na partição do sistema utilizada para iniciar o Windows.|  
|**Todos os**|O código de arranque principal em todas as partições de atualizações. **Todos os** não necessariamente a atualizar o código de arranque para cada volume. Em vez disso, esta opção atualiza o código de arranque para os volumes que podem ser utilizados como volumes de arranque do Windows, o que exclui quaisquer volumes dinâmicos não ligados com uma partição de disco subjacente. Esta restrição se encontra presente, porque o código de arranque tem de estar localizado no início de uma partição de disco.|  
|***Letradaunidade***|Atualiza o código de arranque principal no volume associado esta letra de unidade. O código de arranque não será atualizado se qualquer um dos (1) **Letradaunidade** não está associado um volume ou (2) **Letradaunidade** está associado a um volume não ligado a uma partição de disco subjacente.|  
|**/ Force**|A forçar a dismounts os volumes durante a atualização de código de arranque. Utilize esta opção com cuidado.|  

###  <a name="Compact.exe"></a>Compact.exe  
 Apresenta ou altera a compressão de ficheiros em partições de sistema de ficheiros NTFS.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**/C**|Comprimir os ficheiros especificados. Diretórios serão marcados para que os ficheiros adicionados mais tarde, irão ser comprimidos.|  
|**/V**|Descomprime os ficheiros especificados. Diretórios serão marcados para que os ficheiros adicionados mais tarde, não serão comprimidos.|  
|**/S**|Efetua a operação especificada em ficheiros no diretório especificado e em todos os subdiretórios. Dir predefinido é o diretório atual.|  
|**/A**|Apresenta os ficheiros com o oculto ou atributos de sistema. Estes ficheiros estão omitidos por predefinição.|  
|**I**|Continua a efetuar a operação especificada, mesmo após ocorreram erros. Por predefinição, o Compact.exe para quando é encontrado um erro.|  
|**/F**|Força a operação de comprimir em ficheiros de todos os especificado, incluindo os que já são comprimidos. Os ficheiros comprimidos já são ignorados por predefinição.|  
|**/Q**|Comunica apenas as informações mais essenciais.|  
|***nome de ficheiro***|Especifica um padrão, ficheiro ou diretório.|  

###  <a name="Diskpart.exe"></a>DiskPart.exe  
 DiskPart é um interpretador de comandos do modo de texto que permite a gestão de objetos (discos, partições nem volumes) utilizando scripts ou de uma entrada direta numa janela de linha de comandos.  

 Para obter mais informações sobre o Diskpart.exe, consulte a secção "Opções da linha de comandos Diskpart", no *Guia do utilizador do ambiente de pré-instalação do Windows (Windows PE)*.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows PE|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte o guia referenciado na descrição do utilitário.|  

###  <a name="Expand.exe"></a>Expand.exe  
 Este utilitário é executado para expandir ficheiros (extract) de ficheiros comprimidos.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  
|**Utilize**|`Expand.exe -r wuredist.cab -F:wuRedist.xml %temp%`|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|**-r**|Muda expandido ficheiros|  
|**-D**|Mostra uma lista de ficheiros no diretório de origem|  
|***Origem***|Especificação de ficheiro de origem (podem ser utilizados carateres universais.)|  
|**-F: * ficheiros***|Nome de ficheiros para expandir a partir de um ficheiro. cab|  
|***Destino***|Ficheiro de destino &#124; especificação de caminho (**destino** pode ser um diretório. Se **origem** é vários ficheiros e **- r** não for especificado, **destino** tem de ser um diretório.)|  

###  <a name="ImageX.exe"></a>ImageX.exe  
 ImageX é um utilitário da linha de comandos que lhe permite OEMs e as empresas para capturar, modificar e aplicar imagens do disco baseado em ficheiros para a implementação rápida. ImageX funciona com ficheiros WIM para copiar para uma rede ou poder funcionar com outras tecnologias que utilizam imagens WIM, tais como a configuração do Windows e os serviços de implementação do Windows.  

 Para obter mais informações sobre o ImageX, consulte a secção, "O que é ImageX," no *Guia do utilizador do ambiente de pré-instalação do Windows (Windows PE)*.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Tools\\*plataforma*|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte o guia referenciado na descrição do utilitário.|  

###  <a name="Microsoft.BDD.PnpEnum.exe"></a>Microsoft.BDD.PnpEnum.exe  
 Este utilitário é executado ao enumerar os dispositivos Plug and Play instalados no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|*distribuição*\Tools\\*plataforma*|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|Nenhum|–|  

###  <a name="Mofcomp.exe"></a>Mofcomp.exe  
 Mofcomp.exe consiste no compilador do formato de objeto gerido que analisa um ficheiro que contém instruções de formato de objeto gerido e adiciona as classes e instâncias de classes definidas no ficheiro para o repositório de WMI. Mofcomp.exe fornece ajuda da linha de comandos no comutador utiliza opções.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte a ajuda da linha de comandos que este utilitário fornece.|  

###  <a name="Netsh.exe"></a>Netsh.exe  
 Netsh.exe é um utilitário de linha de comandos e script utilizado para automatizar a configuração de componentes de rede. Para obter mais informações sobre Netsh.exe, consulte [utilitário de linha de comandos de Netsh o](http://technet.microsoft.com/library/cc785383%28WS.10%29.aspx).  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte a ajuda da linha de comandos que este utilitário fornece ou as informações encontrado no URL listado na descrição do utilitário.|  

###  <a name="Reg.exe"></a>Reg.exe  
 A ferramenta de registo da consola é utilizada para ler e modificar os dados de registo.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte a ajuda da linha de comandos que este utilitário fornece.|  

###  <a name="Regsvr32.exe"></a>Regsvr32.exe  
 Este utilitário é utilizado para registar os ficheiros (. dll, .exe,. ocx e assim sucessivamente) com o sistema operativo.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
|***ficheiro***|O nome do ficheiro para registar ou anular o registo|  
|**/s**|Executa o utilitário no modo silencioso|  
|**u**|Anula o registo do ficheiro|  

###  <a name="Wpeutil.exe"></a>Wpeutil.exe  
 O utilitário de Windows PE (Wpeutil) é um utilitário da linha de comandos com a qual os comandos de várias podem ser executados numa sessão do Windows PE. Por exemplo, um administrador pode encerrar ou reiniciar o Windows PE, ativar ou desativar uma firewall, configurar definições de idioma e inicializar uma rede. MDT utiliza o utilitário para inicializar o Windows PE e ligações de rede e iniciar as implementações LTI.  

 Para obter mais informações sobre Wpeutil.exe, consulte a secção "Opções da linha de comandos Wpeutil", no *Guia do utilizador do ambiente de pré-instalação do Windows (Windows PE)*.  

|**Valor**|**Descrição**|  
|-|-|
|**Localização**|Incluído nos ficheiros de origem do Windows PE|  

#### <a name="arguments"></a>Argumentos  

|**Valor**|**Descrição**|  
|-|-|
||Consulte o guia referenciado na descrição do utilitário.|  

## <a name="mdt-windows-powershell-cmdlets"></a>Cmdlets do Windows PowerShell do MDT  
 Para além do Deployment Workbench, partilhas de implementação do MDT podem ser geridas utilizando cmdlets do Windows PowerShell. O Windows PowerShell do MDT cmdlets estão incluídos num snap-in—Microsoft.BDD.PSSnapIn—which do Windows PowerShell está incluído com a instalação do MDT.  

 Os cmdlets do MDT tem de ser executados a partir de uma consola do Windows PowerShell que tenha o Windows PowerShell do MDT snap-in carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in Windows PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

 A tabela 7 apresenta uma lista de cmdlets do Windows PowerShell do MDT e fornece uma breve descrição de cada cmdlet. Cada cmdlet é abordada mais detalhadamente numa secção subsequente.  

### <a name="table-7-mdt-windows-powershell-cmdlets"></a>A tabela 7. Cmdlets do Windows PowerShell do MDT  

|**Cmdlet**|**Descrição**|  
|-|-|  
|[MDTPersistentDrive adicionar](#Add-MDTPersistentDrive)|Adiciona uma partilha de implementação para a lista de MDT persistente unidades que podem ser restauradas utilizando o [restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet.|  
|[Desativar MDTMonitorService](#Disable-MDTMonitorService)|Desativa o MDT monitorização dos serviços.|  
|[Ativar MDTMonitorService](#Enable-MDTMonitorService)|Permite que o MDT monitorização dos serviços.|  
|[Get-MDTDeploymentShareStatistics](#Get-MDTDeploymentShareStatistics)|Mostra as estatísticas de uma partilha de implementação, incluindo o número de entidades por principais pasta na partilha de implementação.|  
|[Get-MDTMonitorData](#Get-MDTMonitorData)|Apresenta o MDT informações recolhidas para um ou mais implementações MTD monitorizadas de monitorização.|  
|[Get-MDTOperatingSystemCatalog](#Get-MDTOperatingSystemCatalog)|Devolve o catálogo de sistema operativo para um sistema operativo específico. Se o catálogo de sistema operativo não existe ou está desatualizado, em seguida, o catálogo de sistema operativo é novamente gerado.|  
|[Get-MDTPersistentDrive](#Get-MDTPersistentDrive)|Mostra uma lista de partilhas de implementação que pode ser restaurada utilizando o [restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet.|  
|[Importar MDTApplication](#Import-MDTApplication)|Importa uma aplicação para uma partilha de implementação.|  
|[Importar MDTDriver](#Import-MDTDriver)|Importa um ou mais controladores de dispositivo para uma partilha de implementação.|  
|[Importar MDTOperatingSystem](#Import-MDTOperatingSystem)|Importa um ou mais sistemas de operativos para uma partilha de implementação.|  
|[Importar MDTPackage](#Import-MDTPackage)|Importa um ou mais pacotes de sistema operativo para uma partilha de implementação.|  
|[Importar MDTTaskSequence](#Import-MDTTaskSequence)|Importa uma sequência de tarefas para uma partilha de implementação.|  
|[Novo MDTDatabase](#New-MDTDatabase)|Cria ou atualiza uma base de dados de base de dados do MDT que está associado uma partilha de implementação.|  
|[Remover MDTMonitorData](#Remove-MDTMonitorData)|Remove o MDT um ou mais itens de dados a partir do MDT recolhido dados numa partilha de implementação de monitorização de monitorização.|  
|[Remover MDTPersistentDrive](#Remove-MDTPersistentDrive)|Remove uma partilha de implementação da lista de MDT persistente unidades do Windows PowerShell que podem ser restauradas utilizando o [restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet.|  
|[Restauro MDTPersistentDrive](#Restore-MDTPersistentDrive)|Cria uma unidade do Windows PowerShell para cada partilha de implementação na lista de MDT persistente unidades do Windows PowerShell.|  
|[Conjunto MDTMonitorData](#Set-MDTMonitorData)|Cria um novo ou atualiza um MDT monitorização dados item existente nos dados de monitorização MDT recolhidos numa partilha de implementação.|  
|[Teste MDTDeploymentShare](#Test-MDTDeploymentShare)|Verifica a integridade de uma partilha de implementação.|  
|[Teste MDTMonitorData](#Test-MDTMonitorData)|Verifica se o MDT monitorização dos serviços está configurado corretamente e em execução.|  
|[Atualização MDTDatabaseSchema](#Update-MDTDatabaseSchema)|Atualiza o esquema de base de dados de base de dados do MDT.|  
|[Atualização MDTDeploymentShare](#Update-MDTDeploymentShare)|Uma partilha de implementação de atualizações.|  
|[Atualização MDTLinkedDS](#Update-MDTLinkedDS)|Replica conteúdo a partir de uma partilha de implementação para uma partilha de implementação ligado.|  
|[Atualização MDTMedia](#Update-MDTMedia)|Replica conteúdo a partir de uma partilha de implementação para uma pasta de suporte de dados de implementação.|  

###  <a name="Add-MDTPersistentDrive"></a>MDTPersistentDrive adicionar  
 Esta secção descreve o **PowerShell Add-MDTPersistentDriveWindows** cmdlet. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Add-MDTPersistentDrive [-Name] <String> [[-InputObject] <PSObject>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet adiciona uma unidade do Windows PowerShell existente criada com o **MDTProvider** a uma lista de unidades que sejam persistentes no Deployment Workbench ou uma sessão do Windows PowerShell utilizando o [ Restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet. Este cmdlet é chamado quando criar ou abrir uma partilha de implementação no Deployment Workbench.  

> [!NOTE]
>  A lista de persistente **MDTProvider** unidades é mantido num por utilizador com base no perfil de utilizador.  

 A lista de persistente **MDTProvider** unidades podem ser apresentadas utilizando o **Get-MDTPersistentDrive** cmdlet.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **adicionar MDTPersistentDriveWindows** cmdlet.  

##### <a name="-name-string"></a>-Nome < cadeia\>  
 Especifica o nome de uma unidade do Windows PowerShell criada com o fornecedor do MDT e corresponde a uma partilha de implementação existente. O nome foi criado utilizando o [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet e especificando o **MDTProvider** no *PSProvider* parâmetro.  

 Para obter mais informações sobre como criar um novo do Windows PowerShell unidade utilizando o **MDTProvider** e como criar uma implementação de partilhar com o Windows PowerShell, consulte a secção "Criar uma implementação partilhar utilizando o Windows PowerShell" no Documento do MDT, *guia de amostras do Toolkit de implementação do Microsoft*.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|Nenhum|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-inputobject-psobject"></a>-InputObject < PSObject\>  
 Este parâmetro especifica um objeto de unidade do Windows PowerShell que foi criado anteriormente no processo. Introduza um objeto de PSObject, tal como um gerados pelo [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**3** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para o objeto de unidade do Windows PowerShell foi adicionado à lista de unidades persistentes.  

 Este cmdlet também produz um **cadeia** tipo object, se o *verboso* parâmetro comum está incluído.  

#### <a name="example-1"></a>Exemplo 1  

```  
Add-MDTPersistentDrive –Name DS001  
```  

##### <a name="description"></a>Descrição  
 Este exemplo adiciona a partilha de implementação com o nome da unidade do Windows PowerShell de *DS001* à lista de unidades persistentes.  

#### <a name="example-2"></a>Exemplo 2  

```  
$MDTPSDrive = New-PSDrive -Name "DS001" -PSProvider "MDTProvider" –Root "C:\DeploymentShare$" -Description "MDT Deployment Share" -NetworkPath \\WDG-MDT-01\DeploymentShare$ -Verbose  
Add-MDTPersistentDrive –InputObject $MDTPSDrive  
```  

##### <a name="description"></a>Descrição  
 Este exemplo adiciona o nome da unidade do Windows PowerShell *DS001,* criados pelo [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet, à lista de MDT persistente unidades utilizando o *$MDTPSDrive* variável.  

#### <a name="example-3"></a>Exemplo 3  

```  
New-PSDrive -Name "DS001" -PSProvider "MDTProvider" –Root "C:\DeploymentShare$" -Description "MDT Deployment Share" -NetworkPath \\WDG-MDT-01\DeploymentShare$ -Verbose | Add-MDTPersistentDrive –Verbose  
```  

##### <a name="description"></a>Descrição  
 Este exemplo adiciona o nome da unidade do Windows PowerShell *DS001,* criados pelo [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet, à lista de MDT persistente unidades, encaminhando o objeto de unidade do Windows PowerShell recentemente criado para o  **MDTPersistentDrive adicionar** cmdlet.  

###  <a name="Disable-MDTMonitorService"></a>Desativar MDTMonitorService  
 Esta secção descreve o **desativar MDTMonitorService** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Disable-MDTMonitorService [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet desativa o MDT monitorização do serviço, que é executado no computador onde está instalado o MDT. O serviço de monitorização do MDT recolhe informações de monitorização que podem ser apresentadas:  

-   No nó de monitorização na partilha de implementação no Deployment Workbench  

-   Utilizar o [Get-MDTMonitorData](#Get-MDTMonitorData) cmdlet  

 O MDT serviço de monitorização, subsequentemente, pode ser ativado através de [ativar MDTMonitorService](#Enable-MDTMonitorService).  

 Para obter mais informações sobre o MDT monitorização do serviço, consulte a secção "Monitorização MDT implementações" no documento do MDT, *utilizar o Microsoft Deployment Toolkit*.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **desativar MDTMonitorService** cmdlet.  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters," que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **cadeia** tipo object, se o *verboso* parâmetro comum é incluído; caso contrário, nenhuma saída é gerada.  

#### <a name="example-1"></a>Exemplo 1  

```  
Disable-MDTMonitorService  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo desativa o MDT serviço de monitorização.  

###  <a name="Enable-MDTMonitorService"></a>Ativar MDTMonitorService  
 Esta secção descreve o **ativar MDTMonitorService** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Enable-MDTMonitorService [-EventPort] <Int32> [-DataPort] <Int32> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet permite que o MDT monitorização do serviço, que é executado no computador onde está instalado o MDT. O serviço de monitorização do MDT recolhe informações de monitorização que podem ser apresentadas:  

-   No nó de monitorização na partilha de implementação no Deployment Workbench.  

-   Utilizar o [Get-MDTMonitorData](#Get-MDTMonitorData) cmdlet  

 O MDT serviço de monitorização pode ser desativado através do [desativar MDTMonitorService](#Disable-MDTMonitorService).  

 Para obter mais informações sobre o MDT monitorização do serviço, consulte a secção "Monitorização MDT implementações" no documento do MDT, *utilizar o Microsoft Deployment Toolkit*.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **ativar MDTMonitorService** cmdlet.  

##### <a name="-eventport-int32"></a>-EventPort < Int32\>  
 Este parâmetro especifica o TCP porta utilizada como a porta de eventos para o MDT serviço de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|**9800**|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-dataport-int32"></a>-DataPort < Int32\>  
 Este parâmetro especifica o TCP porta utilizada como a porta de dados para o MDT serviço de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**3** e **com o nome**|  
|**Valor predefinido**|**9801**|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **cadeia** tipo object, se o *verboso* parâmetro comum é incluído; caso contrário, nenhuma saída é gerada.  

#### <a name="example-1"></a>Exemplo 1  

```  
Enable-MDTMonitorService  
```  

##### <a name="description"></a>Descrição  
 Este exemplo permite o MDT monitorização do serviço no computador local utilizando o valor predefinido de **9800** para a porta de evento e o valor da **9801** para a porta de dados no MDT serviço de monitorização.  

#### <a name="example-2"></a>Exemplo 2  

```  
Enable-MDTMonitorService –EventPort 7000 –DataPort 7001  
```  

##### <a name="description"></a>Descrição  
 Este exemplo permite o MDT monitorização do serviço no computador local utilizando o valor do **7000** para a porta de evento e o valor da **7001** para a porta de dados no MDT serviço de monitorização.  

###  <a name="Get-MDTDeploymentShareStatistics"></a>Get-MDTDeploymentShareStatistics  
 Esta secção descreve o **Get-MDTDeploymentShareStatistics** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Get-MDTDeploymentShareStatistics [-Path <String>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet apresenta as estatísticas de uma partilha de implementação com base na unidade MDTProvder que é especificada o *caminho* parâmetro. As estatísticas incluem o número de itens na partilha de implementação especificado:  

-   Aplicações  

-   Controladores  

-   Sistemas Operativos  

-   Pacotes  

-   Sequências de tarefas  

-   Perfis de seleção  

-   Partilhas de implementação ligado  

-   Suporte de dados do MDT  

-   Computadores na base de dados do MDT  

-   Marca e modelos na base de dados do MDT  

-   Localizações na base de dados do MDT  

-   Funções na base de dados do MDT  

> [!NOTE]
>  Os valores para as estatísticas relacionados com a base de dados do MDT não estão preenchidos e sempre devolvem um valor de zero.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **Get-MDTDeploymentShareStatistics** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica a unidade de MDTProvider Windows PowerShell para a partilha de implementação pretendida.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido a uma localização na unidade de pretendido MDTProvider Windows PowerShell.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo que contém as estatísticas para a partilha de implementação.  

#### <a name="example-1"></a>Exemplo 1  

```  
Get-MDTDeploymentShareStatistics –Path DS001:  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo devolve as estatísticas de partilha de implementação para a partilha de implementação que é especificada o DS001: Unidade de MDTProvider Windows PowerShell.  

#### <a name="example-2"></a>Exemplo 2  

```  
cd DS001:  
Get-MDTDeploymentShareStatistics  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo devolve as estatísticas de partilha de implementação para a partilha de implementação que é especificada o DS001: Unidade de MDTProvider Windows PowerShell. Utilize o **cd** comandos para definir o diretório de trabalho para o Windows PowerShell para o DS001: Unidade de MDTProvider Windows PowerShell.  

###  <a name="Get-MDTMonitorData"></a>Get-MDTMonitorData  
 Esta secção descreve o **Get-MDTMonitorData** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Get-MDTMonitorData [-Path <String>] [-ID <Nullable>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet apresenta o MDT dados que estão a ser reportados para a partilha de implementação de monitorização especificado no *caminho* parâmetro. Exemplo de resultado deste cmdlet é o seguinte:  

```  
Name               : WDG-REF-01  
PercentComplete    : 100  
Settings           :  
Warnings           : 0  
Errors             : 0  
DeploymentStatus   : 3  
StartTime          : 5/23/2012 6:45:39 PM  
EndTime            : 5/23/2012 8:46:32 PM  
ID                 : 1  
UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1  
CurrentStep        : 88  
TotalSteps         : 88  
StepName           :  
LastTime           : 5/23/2012 8:46:32 PM  
DartIP             :  
DartPort           :  
DartTicket         :  
VMHost             : WDG-HOST-01  
VMName             : WDG-REF-01  
ComputerIdentities : {}  

```  

> [!NOTE]
>  A unidade de MDTProvider Windows PowerShell que faça referência a este cmdlet tem de existir antes de executar este cmdlet.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que pode utilizar com o **Get - MDTMonitorData** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica a unidade de MDTProvider Windows PowerShell para a partilha de implementação pretendida.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido a uma localização na unidade de pretendido MDTProvider Windows PowerShell.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-id-nullable"></a>-ID < que pode ser nulo\>  
 Este parâmetro especifica o identificador específico para a implementação de um computador específico. Se este parâmetro não for especificado, todos os dados de monitorização para implementações na partilha de implementação são apresentados.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**3** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para cada computador monitorizado, que contém os dados de monitorização para o computador.  

#### <a name="example-1"></a>Exemplo 1  

```  
Get-MDTMonitorData –Path DS001:  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo devolve os dados de monitorização para todas as implementações na partilha de implementação que é especificada o DS001: Unidade de MDTProvider Windows PowerShell.  

#### <a name="example-2"></a>Exemplo 2  

```  
cd DS001:  
Get-MDTMonitorData  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo devolve os dados de monitorização para todas as implementações na partilha de implementação que é especificada o DS001: Unidade de MDTProvider Windows PowerShell. Utilize o **cd** comandos para definir o diretório de trabalho para o Windows PowerShell para o DS001: Unidade de MDTProvider Windows PowerShell.  

#### <a name="example-3"></a>Exemplo 3  

```  
Get-MDTMonitorData –Path DS001: -ID 22  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo devolve os dados de monitorização para a implementação com o ID de 22 na partilha de implementação que é especificada o DS001: Unidade de MDTProvider Windows PowerShell.  

###  <a name="Get-MDTOperatingSystemCatalog"></a>Get-MDTOperatingSystemCatalog  
 Esta secção descreve o **Get-MDTOperatingSystemCatalog** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Get-MDTOperatingSystemCatalog [-ImageFile] <String> [-Index] <Int32> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet obtém ou cria um catálogo de sistema operativo para uma imagem de sistema operativo personalizada, para que possa modificar o ficheiro unattend.xml correspondente com o Gestor de imagem de sistema do Windows (WSIM). Se o catálogo de sistema operativo não estiver disponível, ou se o catálogo de sistema operativo existente é inválido ou desatualizada, este cmdlet irá gerar um novo catálogo de sistema operativo.  

> [!NOTE]
>  O processo de gerar um novo catálogo de sistema operativo pode demorar muito tempo, como a imagem do sistema operativo personalizado tem de ser montada, inspecionada e desmontar antes de concluir a criação do catálogo de sistema operativo.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **Get-MDTOperatingSystemCatalog** cmdlet.  

##### <a name="-imagefile-string"></a>-ImageFile < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para o ficheiro de imagem do sistema operativo personalizada (ficheiro. wim), incluindo o nome de ficheiro de imagem de sistema operativo personalizada.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-index-int32"></a>-Índice < Int32\>  
 Este parâmetro especifica o índice da imagem do sistema operativo pretendido no ficheiro de imagem de sistema operativo (ficheiro. wim).  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**3** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo que contém o caminho para o catálogo de sistema operativo.  

#### <a name="example-1"></a>Exemplo 1  

```  
Get-MDTOperatingSystemCatalog –ImageFile "DS001:\Operating Systems\Windows 8\sources\install.wim" –Index 2  
```  

##### <a name="description"></a>Descrição  
 O sistema operativo imagem ficheiro DS001:\Operating Systems\Windows 8\sources\install.wim devolve o catálogo de sistema operativo para a imagem do sistema operativo no índice de 2 neste exemplo.  

###  <a name="Get-MDTPersistentDrive"></a>Get-MDTPersistentDrive  
 Esta secção descreve o **Get-MDTPersistentDrive** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Get-MDTPersistentDrive [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet apresenta a lista de unidades do Windows PowerShell do MDT persistentes. A lista de unidades persistentes do MDT Windows PowerShell é gerida utilizando o [adicionar MDTPersistentDrive](#Add-MDTPersistentDrive) e [remover MDTPersistentDrive](#Remove-MDTPersistentDrive) cmdlets ou Deployment Workbench.  

 O resultado deste cmdlet contém as seguintes informações:  

-   Nome de unidade do Windows PowerShell, como DS001  

-   Caminho do diretório, tais como \\\WDG-MDT-01\DeploymentShare$  

 Unidades de MDT Windows PowerShell persistentes são semelhantes aos mapeamentos de unidade de rede persistente.  

> [!NOTE]
>  Esta lista de unidades persistentes do MDT Windows PowerShell é mantido numa base por utilizador e são armazenadas no perfil de utilizador.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **Get - MDTPersistentDrive** cmdlet.  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para cada MDT persistente unidade é idêntica do **PSObject** tipo de objeto que o [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet devolve.  

#### <a name="example-1"></a>Exemplo 1  

```  
Get-MDTPersistentDrive  
```  

##### <a name="description"></a>Descrição  
 Este exemplo mostra uma lista do MDT persistente unidades.  

###  <a name="Import-MDTApplication"></a>Importar MDTApplication  
 Esta secção descreve o **importação MDTApplication** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Import-MDTApplication [-Path <String>] -Name <String> ApplicationSourcePath <String> -DestinationFolder <String> [-Move] [<CommonParameters>]  
```  

 – ou –  

```  
Import-MDTApplication [-Path <String>] -Name <String> NoSource [<CommonParameters>]  
```  

 – ou –  

```  
Import-MDTApplication [-Path <String>] -Name <String> Bundle [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet importa uma aplicação para uma partilha de implementação. Os seguintes tipos de aplicação podem ser importados utilizar este cmdlet:  

-   As aplicações que têm ficheiros de origem, utilizando o *ApplicationSourcePath*, *DestinationFolder*, e *mover* parâmetros. O primeiro exemplo de sintaxe ilustra a utilização deste cmdlet para este tipo de aplicação.  

-   Aplicações sem ficheiros de origem ou com os ficheiros de origem localizados na outra rede partilhado pastas utilizando o *NoSource* parâmetro. O segundo exemplo de sintaxe ilustra a utilização deste cmdlet para este tipo de aplicação.  

-   Os pacotes de aplicação, que são utilizados para agrupar um conjunto de aplicações relacionadas, utilizando o *pacote* parâmetro. O exemplo de sintaxe da última ilustra a utilização deste cmdlet para este tipo de aplicação.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **importação MDTApplication** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente onde a aplicação que está a ser importada irão ser colocada na partilha de implementação. Se o *DestinationFolder* parâmetro é utilizado, em seguida, a pasta especificada no *DestinationFolder* parâmetro é criado sob a pasta especificada neste parâmetro. Este parâmetro é utilizado em todas as utilizações de sintaxe para este cmdlet.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-name-string"></a>-Nome < cadeia\>  
 Este parâmetro especifica o nome da aplicação a ser adicionado à partilha de implementações e tem de ser exclusivo dentro da partilha de implementação. Este parâmetro é utilizado em todas as utilizações de sintaxe para este cmdlet.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-applicationsourcepath-string"></a>-ApplicationSourcePath < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para os ficheiros de origem da aplicação para a aplicação que serão importados para a partilha de implementação. Este parâmetro só é válido para utilização no primeiro exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-destinationfolder-string"></a>-DestinationFolder < cadeia\>  
 Este parâmetro especifica a pasta na partilha de implementação em que os ficheiros de origem da aplicação estão a ser importado. Esta pasta é criada sob a pasta especificada no *caminho* parâmetro. Este parâmetro só é válido para utilização no primeiro exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-move-switchparameter"></a>-Mover [< SwitchParameter\>]  
 Este parâmetro especifica se devem ser movidos de ficheiros de origem da aplicação (em vez de copiar) na pasta onde estão localizados os ficheiros de origem da aplicação, que é especificado no *ApplicationSourcePath* parâmetro.  

 Se este parâmetro é:  

-   Especificado, em seguida, os ficheiros são movidos e os ficheiros na pasta especificada no *ApplicationSourcePath* parâmetro são eliminados  

-   Não especificado, em seguida, os ficheiros são copiados e os ficheiros na pasta especificada no *ApplicationSourcePath* parâmetro são retidos  

 Este parâmetro só é válido para utilização no primeiro exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-nosource-switchparameter"></a>-NoSource [< SwitchParameter\>]  
 Este parâmetro especifica que a aplicação que está a ser importada é uma aplicação que tenha não existem ficheiros de origem ser copiados. Quando utilizar este parâmetro, os ficheiros de origem da aplicação são:  

-   Na pasta partilhada de rede, que é especificado nas definições da aplicação instalação linha de comandos ou trabalho diretório configuração  

-   Já está presente na imagem do sistema operativo  

 Este parâmetro só é válido para utilização no segundo exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-bundle-switchparameter"></a>-Agrupar [< SwitchParameter\>]  
 Este parâmetro especifica que a aplicação que está a ser importada é uma aplicação que é um pacote de dois ou mais aplicações. Este parâmetro só é válido para utilização no último exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo que faça referência a aplicação que acabou de importar.  

#### <a name="example-1"></a>Exemplo 1  

```  
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" ApplicationSourcePath "\\WDG-MDT-01\Source$\Office2010ProPlus\x86" DestinationFolder "Office2010ProPlusx86"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa uma aplicação com ficheiros de origem da pasta partilhada de rede em \\\WDG-MDT-01\Source$\Office2010ProPlus\x86 e copia os ficheiros de origem para DS001:\Applications\Office2010ProPlusx86 na partilha de implementação. Os ficheiros de origem são retidos.  

#### <a name="example-2"></a>Exemplo 2  

```  
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" ApplicationSourcePath "\\WDG-MDT-01\Source$\Office2010ProPlus\x86" DestinationFolder "Office2010ProPlusx86" -Move  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa uma aplicação com ficheiros de origem da pasta partilhada de rede em \\\WDG-MDT-01\Source$\Office2010ProPlus\x86 e move os ficheiros de origem para DS001:\Applications\Office2010ProPlusx86 na partilha de implementação. Os ficheiros de origem são removidos da pasta partilhada de rede em \\\WDG-MDT-01\Source$\Office2010ProPlus\x86. A aplicação é designada *Office 2012 Professional Plus 32 bits.*  

#### <a name="example-3"></a>Exemplo 3  

```  
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" NoSource  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa uma aplicação com o nome *Office 2012 Professional Plus 32-bit* com não existem ficheiros de origem.  

#### <a name="example-4"></a>Exemplo 4  

```  
Import-MDTApplication -Path "DS001:\Applications" -Name "Woodgrove Bank Core Applications" Bundle  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa um pacote de aplicação com o nome *aplicações de núcleo do Woodgrove Bank.*  

###  <a name="Import-MDTDriver"></a>Importar MDTDriver  
 Esta secção descreve o **importação MDTDriver** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Import-MDTDriver [-Path <String>] -SourcePath <String[]> [ImportDuplicates] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet importa um ou mais controladores de dispositivo para uma partilha de implementação. Este cmdlet procura controladores de dispositivos que começa com a pasta especificada no *SourcePath* parâmetro. Este cmdlet irá localizar vários controladores de dispositivo encontrados na estrutura dessa pasta.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **importação MDTDriver** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente onde o controlador de dispositivo que está a ser importado irão ser colocado na partilha de implementação.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação. Este parâmetro tem de ser fornecido se o *SourcePath* parâmetro não é indicado.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sourcepath-string-"></a>-SourcePath < String [] >  
 Este parâmetro especifica um ou mais caminhos completamente qualificados numa matriz de cadeia para as pastas de origem onde estão localizados os ficheiros de controlador de dispositivo. Cada estrutura de pastas, começando com a pasta especificada neste parâmetro será pesquisada controladores de dispositivo, incluindo todas as subpastas e os conteúdos dos ficheiros. cab na estrutura da pasta.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a pasta onde estão localizados os ficheiros de controlador de dispositivo. Este parâmetro tem de ser fornecido se o *caminho* parâmetro não é indicado.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**1** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-importduplicates-switchparameter"></a>-ImportDuplicates [< SwitchParameter\>]  
 Este parâmetro especifica se este cmdlet deve importar controladores de dispositivo duplicado. Por predefinição, os controladores de dispositivo duplicado não foram importados. Controladores de dispositivo duplicados são detetados pelo calcular um valores de hash para todos os ficheiros numa pasta do controlador de dispositivo. Se o valor de hash calculado corresponde a outro controlador de dispositivo, o controlador de dispositivo para ser importado é considerado um duplicado.  

 Se for detetado um controladores duplicados e este parâmetro não for fornecido, o controlador de dispositivo será adicionado e ligado para o controlador de dispositivo original, existentes.  

 Se este parâmetro é:  

-   Especificado, em seguida, os controladores de dispositivo duplicado são importados  

-   Não especificado, em seguida, os controladores de dispositivo serão adicionados e ligados para os controladores de dispositivo original, existente  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um ou mais **PSObject** objetos (um para cada controlador de dispositivo importado) do tipo.  

#### <a name="example-1"></a>Exemplo 1  

```  
Import-MDTDriver -Path "DS001:\Out-of-Box Drivers" SourcePath "\\WDG-MDT-01\Source$\Drivers"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa todos os controladores de dispositivo na estrutura de pastas com a raiz da estrutura de pasta no \\\WDG-MDT-01\Source$\Drivers. Os controladores de dispositivo são armazenados na pasta dos controladores na partilha de implementação que está mapeada para o DS001: Unidade de MDTProvder Windows PowerShell. Se os controladores de dispositivo duplicados são detetados, os controladores de dispositivo serão adicionados e ligados para os controladores de dispositivo original, existentes na partilha de implementação.  

#### <a name="example-2"></a>Exemplo 2  

```  
$DriverSourcePath="\\WDG-MDT-01\Source$\VendorADrivers", "\\WDG-MDT-01\Source$\VendorBDrivers"  
Import-MDTDriver -Path "DS001:\Out-of-Box Drivers" SourcePath $DriverSourcePath ImportDuplicates  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa todos os controladores de dispositivo na estrutura de pastas especificados na matriz da cadeia $DriverSourcePath. Os controladores de dispositivo são armazenados na pasta dos controladores na partilha de implementação que está mapeada para o DS001: Unidade de MDTProvder Windows PowerShell. Se os controladores de dispositivo duplicados são detetados, os controladores de dispositivo duplicado são importados.  

###  <a name="Import-MDTOperatingSystem"></a>Importar MDTOperatingSystem  
 Esta secção descreve o **importação MDTOperatingSystem** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Import-MDTOperatingSystem [-Path <String>] -SourcePath <String> [-DestinationFolder <String>] [-Move] [<CommonParameters>]  
```  

 – ou –  

```  
Import-MDTOperatingSystem [-Path <String>] [DestinationFolder <String>] -SourceFile <String> [SetupPath <String>] [-Move] [<CommonParameters>]  
```  

 – ou –  

```  
Import-MDTOperatingSystem [-Path <String>] -WDSServer <String> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet importa um sistema operativo para uma partilha de implementação. Os seguintes tipos de sistema operativo podem ser importados utilizar este cmdlet:  

-   Sistemas operativos a partir de ficheiros de origem original, utilizando o *SourcePath* parâmetros. O primeiro exemplo de sintaxe ilustra a utilização deste cmdlet para este tipo de importação de sistema operativo.  

-   Ficheiros, tais como imagens de captura de computadores de referência, através de imagem de sistemas de operativos personalizados a *SourceFile* parâmetro. O segundo exemplo de sintaxe ilustra a utilização deste cmdlet para este tipo de importação de sistema operativo.  

-   Imagens de sistema operativo que estejam presentes dos serviços de implementação do Windows utilizando o *WDSServer* parâmetro. O exemplo de sintaxe da última ilustra a utilização deste cmdlet para este tipo de importação de sistema operativo.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **importação MDTOperatingSystem** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente na partilha de implementação em que o sistema operativo que está a ser importado será efetuado. Se o *DestinationFolder* parâmetro é utilizado, em seguida, a pasta especificada no *DestinationFolder* parâmetro é criado sob a pasta especificada neste parâmetro. Este parâmetro é utilizado em todas as utilizações de sintaxe para este cmdlet.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sourcepath-string"></a>-SourcePath < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para os ficheiros de origem do sistema operativo para o sistema operativo que serão importados para a partilha de implementação. Este parâmetro só é válido para utilização no primeiro exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-destinationfolder-string"></a>-DestinationFolder < cadeia\>  
 Este parâmetro especifica a pasta na partilha de implementação em que os ficheiros de origem do sistema operativo estão a ser importado. Esta pasta é criada sob a pasta especificada no *caminho* parâmetro. Este parâmetro só é válido para utilização nos exemplos de sintaxe primeiro e segundo.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-move-switchparameter"></a>-Mover [< SwitchParameter\>]  
 Este parâmetro especifica se os ficheiros de origem do sistema operativo devem ser movidos (em vez de copiar) na pasta onde estão localizados os ficheiros de origem do sistema operativo, que é especificado no *DestinationFolder* parâmetro.  

 Se este parâmetro é:  

-   Especificado, em seguida, os ficheiros são movidos e os ficheiros na pasta especificada no *DestinationFolder* parâmetro são eliminados  

-   Não especificado, em seguida, os ficheiros são copiados e os ficheiros na pasta especificada no *DestinationFolder* parâmetro são retidos  

 Este parâmetro só é válido para utilização nos exemplos de sintaxe primeiro e segundo.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sourcefile-string"></a>-SourceFile < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para o ficheiro. wim de origem do sistema operativo para o sistema operativo que será importado para a partilha de implementação. Este parâmetro só é válido para utilização no segundo exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-setuppath-string"></a>-SetupPath < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para os ficheiros de configuração do sistema operativo que têm de ser importado juntamente com o ficheiro. wim especificado no *SourceFile* parâmetro. Este parâmetro só é válido para utilização no segundo exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-wdsserver-string"></a>-WDSServer < cadeia\>  
 Este parâmetro especifica o nome do servidor de serviços de implementação do Windows em que se encontram os ficheiros de imagem do sistema operativo a ser importados. Serão importados todos os ficheiros de imagem de sistema operativo no servidor de serviços de implementação do Windows para a partilha de implementação. Os ficheiros de imagem do sistema de operativo real não são copiados para a partilha de implementação. Em vez disso, a partilha de implementação contém uma ligação para cada ficheiro de sistema operativo no servidor de serviços de implementação do Windows.  

 Este parâmetro só é válido para utilização no último exemplo de sintaxe.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um ou mais **PSObject** objetos (um para cada sistema operativo que foram importado) do tipo.  

#### <a name="example-1"></a>Exemplo 1  

```  
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" SourcePath "\\WDGMDT01\Source$\Windows8" DestinationFolder "Windows8x64"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa um sistema operativo a partir da pasta de rede partilhada em \\\WDG-MDT-01\Source$\Windows8 e copia os ficheiros de origem para DS001:\Operating Systems\Windows8x64 na partilha de implementação. Os ficheiros de origem são retidos.  

#### <a name="example-2"></a>Exemplo 2  

```  
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" SourcePath "\\WDGMDT01\Source$\Windows8" DestinationFolder "Windows8x64" -Move  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa um sistema operativo a partir da pasta de rede partilhada em \\\WDG-MDT-01\Source$\Windows8 e copia os ficheiros de origem para DS001:\Operating Systems\Windows8x64 na partilha de implementação. Os ficheiros de origem são removidos da pasta partilhada de rede em \\\WDG-MDT-01\Source$\Windows8.  

#### <a name="example-3"></a>Exemplo 3  

```  
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" DestinationFolder "Windows8x64-Reference" –SourceFile "\\WDGMDT01\Capture$\WDG-REF-01_Capture.wim"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa um ficheiro de imagem capturada, personalizada do sistema operativo (ficheiro. wim) a partir de \\\WDG-MDT-01\ capturar$ \WDG-REF-01_Capture.wim e copiar o ficheiro de imagem para DS001:\Operating Systems\Windows8x64-referência na partilha de implementação. O ficheiro. wim de origem é mantido na pasta partilhada de rede.  

#### <a name="example-4"></a>Exemplo 4  

```  
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" WDSServer "WDG-WDS-01"  
```  

##### <a name="description"></a>Descrição  
 Este exemplo importa todas as imagens de sistema operativo do servidor de serviços de implementação do Windows com o nome WDG-WDS-01 e cria uma ligação para cada imagem de sistema operativo nos sistemas de DS001:\Operating na partilha de implementação. Os ficheiros de imagem do sistema operativo de origem no servidor de serviços de implementação do Windows são mantidos no servidor de serviços de implementação do Windows.  

###  <a name="Import-MDTPackage"></a>Importar MDTPackage  
 Esta secção descreve o **importação MDTPackage** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Import-MDTPackage [-Path <String>] [[-SourcePath] <String[]>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet importa um ou mais pacotes de sistema operativo para uma partilha de implementação. Os tipos de pacotes do sistema operativo que podem ser importados incluem atualizações de segurança, pacotes de idiomas ou novos componentes. Os Service packs não devem ser importados como pacotes do sistema operativo como não pode ser instalados offline.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **importação MDTPackage** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente na partilha de implementação em que os pacotes de sistema operativo que está a ser importados serão efetuados.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sourcepath-string"></a>-SourcePath < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado para uma estrutura de pasta para ser analisada importar pacotes do sistema operativo. A estrutura da pasta especificado será analisada para ficheiros. cab e. msu. Para ficheiros. msu, os ficheiros. cab dentro os ficheiros. msu automaticamente são extraídos.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**1** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo que referencia o pacote que acabou de importar.  

#### <a name="example-1"></a>Exemplo 1  

```  
Import-MDTOperatingSystem -Path "DS001:\Packages" SourcePath "\\WDGMDT01\Source$\OSPackages"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo analisa a pasta de rede partilhada em \\\WDG-MDT-01\Source$\OSPackages para o sistema operativo, os pacotes e copia os ficheiros de origem para DS001:\Packages pasta na partilha de implementação. Os ficheiros de origem são removidos da pasta partilhada de rede em \\\WDG-MDT-01\Source$\OSPackages.  

###  <a name="Import-MDTTaskSequence"></a>Importar MDTTaskSequence  
 Esta secção descreve o **importação MDTTaskSequence** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Import-MDTTaskSequence [-Path <String>] -Template <String> -Name <String> -ID <String> [[-Comments] <String>] [[-Version] <String>] [-OperatingSystemPath <String>] [-OperatingSystem <PSObject>] [-FullName <String>] [-OrgName <String>] [-HomePage <String>] [-ProductKey <String>] [-OverrideProductKey <String>] [-AdminPassword <String>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet importa uma sequência de tarefas para uma partilha de implementação. A sequência de tarefas recentemente importados será baseada num modelo existente de sequência de tarefas especificado no *modelo* propriedade.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **importação MDTPackage** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente na partilha de implementação em que a sequência de tarefas a ser importada será efetuada. Por predefinição, o caminho deve apontar para a pasta de controlo e ou uma subpasta da pasta de controlo na partilha de implementação. O valor da *ID* parâmetro será utilizado para criar uma subpasta no caminho especificado neste parâmetro.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-template-string"></a>-Modelo < cadeia\>  
 Este parâmetro especifica o modelo de sequência de tarefas a ser utilizado para importar a nova sequência de tarefas. Os modelos de sequência de tarefas são ficheiros. XML que contém os passos de sequência de tarefas para um determinado tipo de sequência de tarefas. Se a sequência de tarefas modelo está localizado em:  

-   O *installation_folder*\Templates pasta (onde *installation_folder* é a pasta na qual está instalado o MDT), em seguida, é necessário apenas o nome de ficheiro. XML.  

-   Outra pasta, em seguida, o caminho completamente qualificado, incluindo o nome de XML de modelo de sequência de tarefas, é necessária.  

 Para obter mais informações sobre os modelos de sequência de tarefas que estão incluídas com o MDT para implementações LTI, consulte a secção "Criar uma nova tarefa de sequência no Deployment Workbench" no documento do MDT, *utilizar o Microsoft Deployment Toolkit*.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**1** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-name-string"></a>-Nome < cadeia\>  
 Este parâmetro especifica o nome da sequência de tarefas a serem importados. O valor deste parâmetro tem de ser exclusivo dentro da partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-id-string"></a>-ID < cadeia\>  
 Este parâmetro especifica o identificador da sequência de tarefas a serem importados. O valor deste parâmetro tem de ser exclusivo dentro da partilha de implementação. O valor atribuído para este parâmetro deve estar em maiúsculas e sem quaisquer espaços ou carateres especiais. Este valor é utilizado para criar uma subpasta na pasta especificada no *caminho* parâmetro, que deve estar sob a pasta de controlo na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**3** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-comments-string"></a>-Comentários < cadeia\>  
 Este parâmetro especifica o texto que fornece informações adicionais e descritivas sobre a sequência de tarefas a serem importados. Estas informações descritivas estão visíveis no Deployment Workbench.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**4** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-version-string"></a>-Versão < cadeia\>  
 Este parâmetro especifica o número de versão da sequência de tarefas a serem importados. O valor deste parâmetro se a fins informativo apenas e não é utilizado pelo MDT para processamento relacionado com a versão.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**4** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-operatingsystempath-string"></a>-OperatingSystemPath < cadeia\>  
 Este parâmetro especifica o caminho completamente qualificado do Windows PowerShell para a pasta na partilha de implementação que contém o sistema operativo a ser utilizada com esta sequência de tarefas, tais como DS001:\Operating Systems\Windows 8. O sistema operativo tem de existir na partilha de implementação em que a sequência de tarefas está a ser importada.  

> [!NOTE]
>  Se não fornecer este parâmetro e tem da sequência de tarefas fazer referência a um sistema operativo, em seguida, tem de fornecer o *OperatingSystem* parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-operatingsystem-psobject"></a>-OperatingSystem < PSObject\>  
 Este parâmetro especifica o objeto de sistema operativo a ser utilizada com esta sequência de tarefas. O sistema operativo tem de existir na partilha de implementação em que a sequência de tarefas está a ser importada.  

 Pode obter o objeto do Windows PowerShell para um sistema operativo utilizando o **Get-Item** cmdlet, tais como o exemplo seguinte:  

```  
$OS=Get-Item "DS001:\Operating Systems\Windows 8"  
```  

 Para mais informações sobre o **Get-Item** cmdlet, consulte [utilizando o Cmdlet Get-Item](http://technet.microsoft.com/library/ee176851).  

> [!NOTE]
>  Se não fornecer este parâmetro e tem da sequência de tarefas fazer referência a um sistema operativo, em seguida, tem de fornecer o *OperatingSystemPath* parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-fullname-string"></a>-FullName < cadeia\>  
 Este parâmetro especifica o nome do proprietário registado do sistema operativo a ser utilizada com esta sequência de tarefas. Este nome é guardado no **RegisteredOwner** chave de registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion**. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-orgname-string"></a>-OrgName < cadeia\>  
 Este parâmetro especifica o nome da organização para o proprietário registado do sistema operativo a ser utilizada com esta sequência de tarefas. Este nome é guardado no **RegisteredOrganization** chave de registo em **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion**. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-homepage-string"></a>Home page - < cadeia\>  
 Este parâmetro especifica o URL a utilizar como a home page do Internet Explorer. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-productkey-string"></a>-ProductKey < cadeia\>  
 Este parâmetro especifica a chave de produto a utilizar para o sistema operativo a ser utilizada com esta sequência de tarefas. Esta chave de produto é válido apenas para versões de revenda dos sistemas operativos Windows. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

> [!NOTE]
>  Se este parâmetro não for fornecido, em seguida, a chave de produto deve ser fornecida ao implementar esta sequência de tarefas no Assistente de implementação, no ficheiro CustomSettings.ini ou na base de dados do MDT.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-overrideproductkey-string"></a>-OverrideProductKey < cadeia\>  
 Este parâmetro especifica a chave MAK para ser utilizado para o sistema operativo a ser utilizada com esta sequência de tarefas. Esta chave de produto é válido apenas para versões de licença de volume do Windows. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

> [!NOTE]
>  Se este parâmetro não for fornecido, em seguida, a chave MAK tem de fornecer ao implementar esta sequência de tarefas no Assistente de implementação, no ficheiro CustomSettings.ini ou na base de dados do MDT.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-adminpassword-string"></a>-AdminPassword < cadeia\>  
 Este parâmetro especifica a palavra-passe a atribuir à conta de administrador incorporada, local no computador de destino. O valor deste parâmetro está injetado no ficheiro Unattend.xml estar associado este sequências de tarefas.  

> [!NOTE]
>  Se este parâmetro não for fornecido, em seguida, a palavra-passe a atribuir à incorporada, conta de administrador local no computador de destino tem de ser fornecida quando implementar esta sequência de tarefas no Assistente de implementação, no ficheiro CustomSettings.ini ou na base de dados do MDT.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo que faça referência a sequência de tarefas que acabou de importar.  

#### <a name="example-1"></a>Exemplo 1  

```  
Import-MDTTaskSequence -Path "DS001:\Control" –Template "Client.xml" –Name "Deploy Windows 8 to Reference Computer" –ID "WIN8REFERENCE" –Comments "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)" –Version "1.00" –OperatingSystemPath "DS001:\Operating Systems\Windows 8_x64" –FullName "Woodgrove Bank Employee" –OrgName "Woodgrove Bank" HomePage "http://www.woodgrovebank.com"  OverrideProductKey "1234512345123451234512345" AdministratorPassword "P@ssw0rd"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa uma sequência de tarefas com o nome *implementar o Windows 8 para o computador de referência* e cria a sequência de tarefas na pasta DS001:\Control\WIN8REFERENCE na partilha de implementação. O comentário, "Sequência de tarefas para implementar o Windows 8 para o computador de referência (WDG-REF-01), de tarefas" está atribuído à sequência de tarefas. O número de versão da sequência de tarefas está definido como **1.00**.  

 O sistema operativo associado a sequência de tarefas está localizado em DS001:\Operating Systems\Windows 8_x64 na partilha de implementação. O proprietário registado do sistema operativo será definido para **Woodgrove Bank empregado**. A organização registado do sistema operativo será definida para **Banco Woodgrove**. Home page do Internet Explorer será predefinido para **http://www.woodgrovebank.com**. A palavra-passe local, conta de administrador incorporada será definida para um valor de  **P@ssw0rd** . A chave de produto para o sistema operativo será definida para **1234512345123451234512345**.  

#### <a name="example-2"></a>Exemplo 2  

```  
$OSObject=Get-Item "DS001:\Operating Systems\Windows 8_x64"  
Import-MDTTaskSequence -Path "DS001:\Control" –Template "Client.xml" –Name "Deploy Windows 8 to Reference Computer" –ID "WIN8REFERENCE" –Comments "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)" –Version "1.00"–OperatingSystem $OSObject –FullName "Woodgrove Bank Employee" –OrgName "Woodgrove Bank" HomePage "http://www.woodgrovebank.com"  AdministratorPassword "P@ssw0rd"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo importa uma sequência de tarefas com o nome *implementar o Windows 8 para o computador de referência* e cria a sequência de tarefas na pasta DS001:\Control\WIN8REFERENCE na partilha de implementação. O comentário, "Sequência de tarefas para implementar o Windows 8 para o computador de referência (WDG-REF-01), de tarefas" está atribuído à sequência de tarefas. O número de versão da sequência de tarefas está definido como **1.00**.  

 O sistema operativo associado a sequência de tarefas está localizado em DS001:\Operating Systems\Windows 8_x64 na partilha de implementação, o que é transmitida para o cmdlet utilizando o *$OSObject* variável. O *$OSObject* variável é definida para uma utilização de objeto de sistema operativo existente a **Get-Item** cmdlet.  

 O proprietário registado do sistema operativo será definido para **Woodgrove Bank empregado**. A organização registado do sistema operativo será definida para **Banco Woodgrove**. Home page do Internet Explorer será predefinido para **http://www.woodgrovebank.com**. A palavra-passe local, conta de administrador incorporada será definida para um valor de  **P@ssw0rd** . A chave de produto para o sistema operativo tem de ser fornecido quando implementar esta sequência de tarefas no Assistente de implementação, no ficheiro CustomSettings.ini ou na base de dados do MDT.  

###  <a name="New-MDTDatabase"></a>Novo MDTDatabase  
 Esta secção descreve o **New-MDTDatabase** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
New-MDTDatabase [-Path <String>] [-Force] -SQLServer <String> [-Instance <String>] [-Port <String>] [-Netlib <String>] -Database <String> [-SQLShare <String>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet cria uma base de dados nova BD do MDT que está associado uma partilha de implementação. Cada partilha de implementação pode ser associada com apenas uma base de dados de base de dados do MDT.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **New-MDTDatabase** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado do Windows PowerShell para a partilha de implementação para que a nova base de dados do MDT DB será associado colocá-la.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-force-switchparameter"></a>-Force [< SwitchParameter\>]  
 Este parâmetro especifica que as tabelas dentro da base de dados do MDT deverá ser recriadas, se a base de dados especificada no *base de dados* parâmetro já existe. Se este parâmetro é:  

-   Fornecidas, em seguida, as tabelas dentro de uma base de dados existente do MDT serão recriadas  

-   For omitido, em seguida, as tabelas dentro de uma base de dados existente do MDT não serão novamente criadas  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sqlserver-string"></a>-SQLServer < cadeia\>  
 Este parâmetro especifica o nome do computador com o SQL Server onde será criada a nova base de dados de base de dados do MDT.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-instance-string"></a>-Instância < cadeia\>  
 Este parâmetro especifica a instância do SQL Server em que será criada a nova base de dados de base de dados do MDT. Se este parâmetro for omitido, é criado a base de dados do MDT base de dados na instância predefinida do SQL Server.  

> [!NOTE]
>  O serviço SQL Browser tem de estar em execução no computador que executa o SQL Server para o cmdlet para localizar a instância especificada neste parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-port-string"></a>-Porta < cadeia\>  
 Este parâmetro especifica a porta TCP para ser utilizado na comunicação com a instância do SQL Server especificada no *SQLServer* parâmetro. A porta predefinida que utiliza o SQL Server é 1433. Especifique este parâmetro quando o SQL Server está configurado para utilizar uma porta que não seja o valor predefinido. O valor deste parâmetro tem de corresponder à porta configurada do SQL Server.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-netlib-string"></a>-Netlib < cadeia\>  
 Este parâmetro especifica a biblioteca de rede do SQL Server utilizada em comunicação com a instância do SQL Server especificada no *SQLServer* parâmetro. O parâmetro pode ser definido como um dos seguintes valores:  

-   **DBNMPNTW**, que é utilizada para especificar a comunicação de pipes nomeados  

-   **DBSMSOCN**, que é utilizada para especificar o TCP/IP sockets comunicação  

 Se este parâmetro não for fornecido, a biblioteca de rede do SQL de pipes nomeados (DBNMPNTW) é utilizada.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-database-string"></a>-Base de dados < cadeia\>  
 Este parâmetro especifica o nome da base de dados a ser criado na instância do SQL Server especificada no *instância* parâmetro no SQL Server especificado no *SQLServer* parâmetro. A localização predefinida e uma convenção de nomenclatura serão utilizados para os ficheiros de registo e base de dados ao criar a base de dados.  

 Se a base de dados especificado neste parâmetro já existir, a base de dados não irão ser recriada. As tabelas na base de dados podem ser recriadas com base no *Force* parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-sqlshare-string"></a>-SQLShare < cadeia\>  
 Este parâmetro especifica o nome da pasta partilhada de rede no computador onde está a executar o SQL Server. Esta ligação é utilizada para estabelecer ligações de segurança integrada do Windows utilizando o protocolo de Pipes nomeados.  

> [!NOTE]
>  Se este parâmetro não for incluído, uma ligação segura de $ IPC não for estabelecida. Como resultado, com o nome pipes comunicação com o SQL Server poderá falhar.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para a BD do MDT nova que tenha sido criada.  

#### <a name="example-1"></a>Exemplo 1  

```  
New-MDTDatabase -Path "DS001:" –SQLServer "WDGSQL01" Database "MDTDB" –SQLShare "\\WDGSQL01\MDTShare$"  
```  

##### <a name="description"></a>Descrição  
 Este exemplo cria uma base de dados do MDT com o nome *MDTDB* na instância predefinida do SQL Server num computador denominado *WDG-SQL-01.* Se a base de dados já existe, não irão ser recriadas as tabelas na base de dados existente. A ligação será efetuada utilizando a porta de TCP do SQL Server predefinida e o protocolo de Pipes nomeados.  

#### <a name="example-2"></a>Exemplo 2  

```  
New-MDTDatabase -Path "DS001:" –Force –SQLServer "WDGSQL01" –Instance "MDTInstance" Database "MDTDB" –SQLShare "\\WDGSQL01\MDTShare$"  
```  

##### <a name="description"></a>Descrição  
 Este exemplo cria uma base de dados do MDT com o nome *MDTDB* na instância do SQL Server com o nome *MDTInstance* num computador denominado *WDG-SQL-01.* Se a base de dados já existir, irão ser recriadas as tabelas na base de dados existente. A ligação será efetuada utilizando a porta de TCP do SQL Server predefinida e o protocolo de Pipes nomeados.  

###  <a name="Remove-MDTMonitorData"></a>Remover MDTMonitorData  
 Esta secção descreve o **Get-MDTPersistentDrive** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Remove-MDTMonitorData [-Path <String>] [-ID <Int32>] [<CommonParameters>]  
```  

 – ou –  

```  
Remove-MDTMonitorData [-Path <String>] [-ComputerObject <PSObject>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet Remove os dados de monitorização recolhidos os dados de monitorização recolhidos existentes numa partilha de implementação. Pode identificar os dados de monitorização para remover especificando o:  

-   Identificador (ID) do item de monitorização para uma partilha de implementação específica. Os IDs de item de monitorização são gerados automaticamente e atribuiu ao item quando o item é criado para a partilha de implementação. O primeiro exemplo de sintaxe ilustra esta utilização.  

-   Objeto de computador para o item de monitorização na partilha de implementação. O objeto de computador pode ser obtido utilizando o **Get-MDTMonitorData** cmdlet. O exemplo de sintaxe da última ilustra esta utilização.  

> [!NOTE]
>  Depois dos dados de monitorização foi removidos, não há nenhum método para recuperar as informações.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **Get - MDTMonitorData** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o **MDTProvider** unidade do Windows PowerShell para a partilha de implementação pretendida.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido a uma localização na unidade de pretendido MDTProvider Windows PowerShell.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-id-nullable"></a>-ID < que pode ser nulo\>  
 Este parâmetro especifica o item de dados de monitorização para ser removida utilizando o identificador do item dos dados de monitorização. Se este parâmetro não for especificado, em seguida, a *ComputerObject* parâmetro deve ser especificado para identificar um determinado item de dados de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-computerobject-psobject"></a>-ComputerObject < PSObject\>  
 Este parâmetro especifica o item de dados de monitorização a ser removida utilizando um objeto de computador. Se este parâmetro não for especificado, em seguida, a *ID* parâmetro deve ser especificado para identificar um determinado item de dados de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet pode saída um **cadeia** tipo object, se o *verboso* parâmetro comum é incluído; caso contrário, nenhuma saída é gerada.  

#### <a name="example-1"></a>Exemplo 1  

```  
Remove-MDTMonitorData -Path "DS001:" -ID 3  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove o item de dados de monitorização com um ID que tem um valor de **3** da implementação partilhar no caminho do Windows PowerShell DS001:.  

#### <a name="example-2"></a>Exemplo 2  

```  
Remove-MDTMonitorData -ID 3  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove o item de dados de monitorização com um ID que tem um valor de **3** da implementação partilhar no caminho predefinido do Windows PowerShell.  

#### <a name="example-3"></a>Exemplo 3  

```  
$MonitorObject=Get-MDTMonitorData | Where-Object {$_.Name eq 'WDG-REF-01'}  
Remove-MDTMonitorData -ComputerObject $MonitorObject  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove qualquer item de dados de monitorização onde o nome do computador é WDG-REF-01. É possível localizar o objeto com o **Get-MDTMonitorData** cmdlet e os **Where-Object** cmdlet. Para mais informações sobre o **Where-Object** cmdlet, consulte [utilizando o Cmdlet Where-Object](http://technet.microsoft.com/library/ee177028.aspx).  

###  <a name="Remove-MDTPersistentDrive"></a>Remover MDTPersistentDrive  
 Esta secção descreve o **remover MDTPersistentDriveWindows** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Remove-MDTPersistentDrive [-Name] <String> [[-InputObject] <PSObject>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet Remove uma unidade do Windows PowerShell existente criada com o **MDTProvider** da lista de unidades que sejam persistentes no Deployment Workbench ou uma sessão do Windows PowerShell utilizando o [ Restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet. Este cmdlet é chamado quando uma partilha de implementação está fechada (removido) Deployment Workbench.  

> [!NOTE]
>  A lista de persistente **MDTProvider** unidades é mantido num por utilizador com base no perfil de utilizador.  

 A lista de persistente **MDTProvider** unidades podem ser apresentadas utilizando o **Get-MDTPersistentDrive** cmdlet. Uma unidade de MDTProvider pode ser adicionada à lista de unidades persistentes utilizando o **adicionar MDTPersistentDrive** cmdlet.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **adicionar MDTPersistentDriveWindows** cmdlet.  

##### <a name="-name-string"></a>-Nome < cadeia\>  
 Especifica o nome de uma unidade do Windows PowerShell criada com o fornecedor do MDT e corresponde a uma partilha de implementação existente. O nome foi criado utilizando o [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet e especificando o **MDTProvider** no *PSProvider* parâmetro.  

 Para obter mais informações sobre como criar um novo do Windows PowerShell unidade utilizando o **MDTProvider** e como criar uma implementação de partilhar com o Windows PowerShell, consulte a secção "Criar uma implementação partilhar utilizando o Windows PowerShell" no Documento do MDT, *guia de amostras do Toolkit de implementação do Microsoft*.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**1** e **com o nome**|  
|**Valor predefinido**|**Nenhum**|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-inputobject-psobject"></a>-InputObject < PSObject\>  
 Este parâmetro especifica um objeto de unidade do Windows PowerShell que foi criado anteriormente no processo. Introduza um **PSObject** objeto, tal como um gerados pelo [New-PSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**2** e **com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet fornece não saídas.  

#### <a name="example-1"></a>Exemplo 1  

```  
Remove-MDTPersistentDrive –Name "DS001:"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove a partilha de implementação com o nome da unidade do Windows PowerShell de *DS001* da lista de unidades persistentes.  

#### <a name="example-2"></a>Exemplo 2  

```  
$MDTPSDrive = Get-PSDrive | Where-Object {$_.Root -eq "C:\DeploymentShare" -and $_.Provider -like "*MDTProvider"}   
Remove-MDTPersistentDrive –InputObject $MDTPSDrive  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove a partilha de implementação em C:\DeploymentShare$ da lista de unidades persistentes. O **GetPSDrive** e **Where-Object** cmdlets são utilizados para devolver o MDT persistente unidade do Windows PowerShell para o **remover MDTPersistentDrive** cmdlet utilizando o *$MDTPSDrive* variável. Para mais informações sobre o **Where-Object** cmdlet, consulte [utilizando o Cmdlet Where-Object](http://technet.microsoft.com/library/ee177028.aspx). Para mais informações sobre o **Get-PSDrive** cmdlet, consulte [utilizando o Cmdlet Get-PSDrive](http://technet.microsoft.com/library/ee176856).  

###  <a name="Restore-MDTPersistentDrive"></a>Restauro MDTPersistentDrive  
 Esta secção descreve o **restauro MDTPersistentDrive** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Restore-MDTPersistentDrive [-Force] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet restaura uma unidade do Windows PowerShell do MDT persistente à lista de unidade do Windows PowerShell Active Directory para cada partilha de implementação que foi adicionada à lista de unidades do Windows PowerShell do MDT persistentes. A lista de unidades persistentes do MDT Windows PowerShell é gerida utilizando o [adicionar MDTPersistentDrive](#Add-MDTPersistentDrive) e [remover MDTPersistentDrive](#Remove-MDTPersistentDrive) cmdlets ou Deployment Workbench.  

 Este cmdlet chama o **New-PSDrive** cmdlet para criar uma unidade do Windows PowerShell para cada unidade o MDT persistente lista. Unidades de MDT Windows PowerShell persistentes são semelhantes aos mapeamentos de unidade de rede persistente.  

> [!NOTE]
>  Esta lista de unidades persistentes do MDT Windows PowerShell é mantido numa base por utilizador e são armazenadas no perfil de utilizador.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **restauro MDTPersistentDrive** cmdlet.  

##### <a name="-force-switchparameter"></a>-Force [< SwitchParameter\>]  
 Este parâmetro especifica que a partilha de implementação deve ser atualizada quando restaurado (se necessário). Se este parâmetro é:  

-   Fornecidas, em seguida, a partilha de implementação será atualizada quando restaurado (se necessário)  

-   For omitido, em seguida, partilha de implementação não será atualizada quando restaurada  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para cada unidade do Windows PowerShell do MDT fornecedor é restaurada.  

#### <a name="example-1"></a>Exemplo 1  

```  
Get-MDTPersistentDrive  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo restaura a lista de MDT persistente unidades, criando um Windows PowerShell unidade utilizando o **MDTProvider** tipo. A partilha de implementação não será atualizada quando restaurado.  

#### <a name="example-2"></a>Exemplo 2  

```  
Get-MDTPersistentDrive -Force  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo restaura a lista de MDT persistente unidades, criando um Windows PowerShell unidade utilizando o **MDTProvider** tipo. A partilha de implementação será atualizada quando restaurado (se necessário).  

###  <a name="Set-MDTMonitorData"></a>Conjunto MDTMonitorData  
 Esta secção descreve o **Get-MDTPersistentDrive** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Set-MDTMonitorData [-Path <String>] [-ComputerObject <PSObject>] [-Settings <Hashtable>] [<CommonParameters>]  
```  

 – ou –  

```  
Set-MDTMonitorData [-Path <String>] [-MacAddress <String>] [Settings <Hashtable>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet cria um novo item de dados de monitorização ou um existente monitorização item de dados, numa partilha de implementação de atualizações. Pode identificar os dados de monitorização para remover especificando o:  

-   Objeto de computador para o item de monitorização na partilha de implementação. O objeto de computador pode ser obtido utilizando o **Get-MDTMonitorData** cmdlet. O primeiro exemplo de sintaxe ilustra esta utilização.  

-   Endereço MAC do adaptador de rede principal do item de monitorização para uma partilha de implementação específica. O endereço MAC é atribuído automaticamente ao item de dados de monitorização quando o item é criado para a partilha de implementação. O exemplo de sintaxe da última ilustra esta utilização.  

> [!NOTE]
>  Depois dos dados de monitorização foi removidos, não há nenhum método para recuperar as informações.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **Get - MDTMonitorData** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica a unidade de MDTProvider Windows PowerShell para a partilha de implementação pretendida.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido a uma localização na unidade de pretendido MDTProvider Windows PowerShell.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-computerobject-psobject"></a>-ComputerObject < PSObject\>  
 Este parâmetro especifica o item de dados de monitorização a ser criada ou atualizada com um objeto de computador. Se este parâmetro não for especificado, em seguida, a *MACAddress* parâmetro deve ser especificado para identificar um determinado item de dados de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-macaddress-string"></a>-MACAddress < cadeia\>  
 Este parâmetro especifica o item de dados de monitorização a ser criada ou atualizada com o endereço MAC do adaptador de rede principal do computador que está a ser monitorizado. O formato do MACAddress é *xx:xx:xx:xx:xx:xx,* onde *x* é um caráter hexadecimal especificado em maiúsculas (conforme necessário). Se este parâmetro não for especificado, em seguida, a *ComputerObject* parâmetro deve ser especificado para identificar um determinado item de dados de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-settings-hashtable"></a>-Definições < tabela hash\>  
 Este parâmetro especifica as definições de dados monitorização para o item de dados de monitorização a ser criadas ou atualizadas. O formato da tabela hash fornecido com este parâmetro é `@{"Setting"="Value"; "Setting1"="Value1"; "Setting2"="Value2}`. Se este parâmetro não for especificado, em seguida, o item de dados de monitorização é criado, mas não existem informações de monitorização são armazenadas.  

 `"Setting"`pode ser qualquer propriedade listada no ficheiro ZTIGather.xml. `Value`pode ser qualquer valor válido para o propriedade de passando na `"Setting"`.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet não gera qualquer saída.  

#### <a name="example-1"></a>Exemplo 1  

```  
$MonitorObject=Get-MDTMonitorData | Where-Object {$_.Name eq 'WDG-REF-01'}  
Set-MDTMonitorData -ComputerObject $MonitorObject Setting @{"OSDComputerName"="WDG-MDT-01";"SkipWizard"="YES"}  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo remove qualquer item de dados de monitorização onde o nome do computador é *WDG-REF-01.* É possível localizar o objeto com o **Get-MDTMonitorData** cmdlet e os **Where-Object** cmdlet. Para mais informações sobre o **Where-Object** cmdlet, consulte [utilizando o Cmdlet Where-Object](http://technet.microsoft.com/library/ee177028.aspx). O [OSDComputerName](#OSDComputerName) propriedade é registada como tendo um valor de **WDG-MDT-01**e o [SkipWizard](#SkipWizard) propriedade é registada como tendo um valor de **Sim**.  

#### <a name="example-2"></a>Exemplo 2  

```  
Set-MDTMonitorData -MACAddress "00:11:22:33:44:55" MonitorObject Setting @{"OSDComputerName"="WDG-MDT-01";"SkipWizard"="YES"}  
```  

##### <a name="description"></a>Descrição  
 Este exemplo cria ou atualiza um item de dados de monitorização com um **MACAddress** que tem um valor de **00:11:22:33:44:55**. O [OSDComputerName](#OSDComputerName) propriedade é registada como tendo um valor de **WDG-MDT-01**e o [SkipWizard](#SkipWizard) propriedade é registada como tendo um valor de **Sim**.  

###  <a name="Test-MDTDeploymentShare"></a>Teste MDTDeploymentShare  
 Embora este cmdlet é devolvido utilizando o **Get-Command** cmdlet como estando no Microsoft.BDD.PSSnapIn snap-in, não está implementada.  

###  <a name="Test-MDTMonitorData"></a>Teste MDTMonitorData  
 Esta secção descreve o **teste MDTMonitorData** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Test-MDTMonitorData -ServerName <String> -EventPort <Int32> -DataPort <Int32> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet valida se o MDT monitorização do serviço, que é executado no computador no qual o MDT é instalado, ativado e em execução corretamente. O serviço de monitorização do MDT recolhe informações de monitorização que podem ser apresentadas:  

-   No nó de monitorização na partilha de implementação no Deployment Workbench  

-   Utilizar o [Get-MDTMonitorData](#Get-MDTMonitorData) cmdlet  

 O MDT serviço de monitorização pode ser desativado através do [desativar MDTMonitorService](#Disable-MDTMonitorService). Informações de monitorização podem ser escrita para o MDT monitorização serviço a utilizar o [conjunto MDTMonitorData](#Set-MDTMonitorData) cmdlet.  

> [!NOTE]
>  Para que este cmdlet funcione corretamente tem de existir pelo menos um item de dados de monitorização de outros MDT na partilha de implementação. Se tem sido registado sem MDT informações de monitorização, a partilha de implementação irá falhar o teste.  

 Para obter mais informações sobre o MDT monitorização do serviço, consulte a secção "Monitorização MDT implementações" no documento do MDT, *utilizar o Microsoft Deployment Toolkit*.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **teste MDTMonitorData** cmdlet.  

##### <a name="-server-string"></a>-Servidor < cadeia\>  
 Especifica o nome do computador no qual está instalado o MDT e o MDT monitorização do serviço está em execução.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|Nenhum|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-dataport-int32"></a>-DataPort < Int32\>  
 Este parâmetro especifica o TCP porta utilizada como a porta de dados para o MDT serviço de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-eventport-int32"></a>-EventPort < Int32\>  
 Este parâmetro especifica o TCP porta utilizada como a porta de eventos para o MDT serviço de monitorização.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um valor booleano que representa o êxito (true) ou a falha (false) do texto.  

#### <a name="example-1"></a>Exemplo 1  

```  
Test-MDTMonitorData -Server "WDG-MDT-01" -DataPort "9801" EventPort "9800"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo verifica se o MDT monitorização do serviço no WDG-MDT-01 está instalado e em execução. O cmdlet irá verificar a utilizar uma porta de dados de 9801 e uma porta de eventos de 9800.  

###  <a name="Update-MDTDatabaseSchema"></a>Atualização MDTDatabaseSchema  
 Esta secção descreve o **atualização MDTDatabaseSchema** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Update-MDTDatabaseSchema -SQLServer <String> [-Instance <String>] [-Port <String>] [-Netlib <String>] -Database <String> [-SQLShare <String>] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet atualiza uma base de dados existente do MDT base de dados para a versão mais recente do esquema de base de dados de base de dados do MDT. Cada partilha de implementação pode ser associada com apenas uma base de dados de base de dados do MDT.  

 Este cmdlet automaticamente é chamado quando uma partilha de implementação está a ser atualizada, como quando executar o [restauro MDTPersistentDrive](#Restore-MDTPersistentDrive) cmdlet com o *Force* parâmetro e o [ Atualização MDTDeploymentShare](#Update-MDTDeploymentShare) cmdlet.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **atualização MDTDatabaseSchema** cmdlet.  

##### <a name="-sqlserver-string"></a>-SQLServer < cadeia\>  
 Este parâmetro especifica o nome do computador com o SQL Server onde a base de dados do MDT DB será atualizada.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-instance-string"></a>-Instância < cadeia\>  
 Este parâmetro especifica a instância do SQL Server no qual existe a base de dados de base de dados do MDT a ser atualizado. Se este parâmetro for omitido, é assumido a base de dados do MDT BD deve para estar na instância predefinida do SQL Server.  

> [!NOTE]
>  O serviço SQL Browser tem de estar em execução no computador que executa o SQL Server para o cmdlet para localizar a instância especificada neste parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-port-string"></a>-Porta < cadeia\>  
 Este parâmetro especifica a porta TCP para ser utilizado na comunicação com a instância do SQL Server especificada no *SQLServer* parâmetro. A porta predefinida que utiliza o SQL Server é 1433. Especifique este parâmetro quando o SQL Server está configurado para utilizar uma porta que não seja o valor predefinido. O valor deste parâmetro tem de corresponder à porta configurada do SQL Server.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-netlib-string"></a>-Netlib < cadeia\>  
 Este parâmetro especifica a biblioteca de rede do SQL Server que é utilizada na comunicação com a instância do SQL Server especificada no *SQLServer* parâmetro. O parâmetro pode ser definido como um dos seguintes valores:  

-   **DBNMPNTW**, que é utilizada para especificar a comunicação de pipes nomeados  

-   **DBSMSOCN**, que é utilizada para especificar o TCP/IP sockets comunicação  

 Se este parâmetro não for fornecido, os SQL Server de pipes nomeados biblioteca de rede (**DBNMPNTW**) é utilizado.  

> [!NOTE]
>  Deployment Workbench não fornece a opção para configurar a biblioteca de rede do SQL Server. Deployment Workbench utiliza sempre a comunicação de pipes nomeados. No entanto, a biblioteca de rede do SQL Server pode ser configurada no ficheiro CustomSettings.ini.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-database-string"></a>-Base de dados < cadeia\>  
 Este parâmetro especifica o nome da base de dados para ser actualizado na instância do SQL Server especificada no *instância* parâmetro na instância do SQL Server especificado no *SQLServer* parâmetro.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **PSObject** objeto de tipo para a base de dados do MDT que foi atualizado. Este cmdlet também produz um **cadeia** escreva dados se o *verboso* parâmetro comum está incluído.  

#### <a name="example-1"></a>Exemplo 1  

```  
Update-MDTDatabaseSchema –SQLServer "WDGSQL01" Database "MDTDB"   
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza o esquema para uma base de dados do MDT com o nome *MDTDB* na instância predefinida do SQL Server num computador denominado *WDG-SQL-01.* A ligação será efetuada para a instância do SQL Server utilizando a porta TCP predefinida e o protocolo de Pipes nomeados.  

#### <a name="example-2"></a>Exemplo 2  

```  
Update-MDTDatabaseSchema –SQLServer "WDGSQL01" –Instance "MDTInstance" -Port "6333" Database "MDTDB"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza o esquema para uma base de dados do MDT com o nome *MDTDB* na instância do SQL Server com o nome *MDTInstance* num computador denominado *WDG-SQL-01.* A ligação será efetuada para o SQL Server utilizando a porta TCP 6333 e o protocolo de Pipes nomeados.  

###  <a name="Update-MDTDeploymentShare"></a>Atualização MDTDeploymentShare  
 Esta secção descreve o **atualização MDTDeploymentShare** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Update-MDTDeploymentShare [-Path <String>] [-Force] [Compress] [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet atualiza uma partilha de implementação existente com os ficheiros mais recentes do Windows ADK. Este cmdlet também atualiza ou as imagens de arranque do Windows PE necessárias em formatos de ficheiro ISO e WIM gera de novo.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **atualização MDTDeploymentShare** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para uma pasta existente na partilha de implementação que está a ser atualizada.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-force-switchparameter"></a>-Force [< SwitchParameter\>]  
 Este parâmetro especifica se imagens de arranque do Windows PE (ficheiros. ISO e. wim) para a partilha de implementação devem ser completamente serão geradas. Se este parâmetro é:  

-   Fornecidos, em seguida, o cmdlet cria novas versões das imagens de arranque do Windows PE. Este processo demora mais tempo a otimizar as imagens de arranque existentes do Windows PE.  

-   For omitido, em seguida, o cmdlet otimiza as imagens de arranque existentes do Windows PE. Este processo demora menos tempo a gerar novas versões das imagens de arranque do Windows PE. Se este parâmetro for omitido, o *comprimir* parâmetro pode ser utilizado para reduzir o tamanho das imagens de arranque como parte do processo de otimização de imagem de arranque do Windows PE.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="-compress-switchparameter"></a>-Comprimir [< SwitchParameter\>]  
 Este parâmetro especifica se devem ser comprimidas imagens de arranque do Windows PE (ficheiros. ISO e. wim) para a partilha de implementação, quando são otimizados (sem o *Force* parâmetro). Se este parâmetro é:  

-   Fornecidas, em seguida, o cmdlet comprime as imagens de arranque do Windows PE, tal como estão a ser otimizados  

-   For omitido, em seguida, o cmdlet não comprimir as imagens de arranque do Windows PE que estão a ser otimizados  

> [!NOTE]
>  Este parâmetro só deve ser fornecido se o *Force* parâmetro não é indicado. Se o *Force* parâmetro está incluído, novas imagens de arranque do Windows PE são geradas e estão comprimidas para o tamanho mínimo.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**FALSO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**Verdadeiro** (**ByValue**)|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **cadeia** escreva dados e produz adicionais **cadeia** escreva dados se o *verboso* parâmetro comum está incluído.  

#### <a name="example-1"></a>Exemplo 1  

```  
Update-MDTDepoymentShare   
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza a partilha de implementação no diretório de trabalho do Windows PowerShell. As imagens de arranque do Windows PE serão otimizadas. As imagens de arranque do Windows PE não serão comprimidas.  

#### <a name="example-2"></a>Exemplo 2  

```  
Update-MDTDepoymentShare -Path "DS001:"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza a partilha de implementação na unidade do Windows PowerShell do MDT com o nome *DS001:.* As imagens de arranque do Windows PE serão otimizadas. As imagens de arranque do Windows PE não serão comprimidas.  

#### <a name="example-3"></a>Exemplo 3  

```  
Update-MDTDepoymentShare -Path "DS001:" -Compress  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza a partilha de implementação na unidade do Windows PowerShell do MDT com o nome *DS001:.* As imagens de arranque do Windows PE serão otimizadas. As imagens de arranque do Windows PE irão ser comprimidas.  

#### <a name="example-4"></a>Exemplo 4  

```  
Update-MDTDepoymentShare -Path "DS001:" -Force  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo atualiza a partilha de implementação na unidade do Windows PowerShell do MDT com o nome *DS001:.* Serão geradas novas versões das imagens de arranque do Windows PE.  

###  <a name="Update-MDTLinkedDS"></a>Atualização MDTLinkedDS  
 Esta secção descreve o **atualização MDTLinkedDS** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Update-MDTLinkedDS -Path <String> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet replica conteúdo a partir de uma partilha de implementação para uma partilha de implementação ligado com o perfil de seleção utilizado para definir a partilha de implementação ligado. O comportamento de replicação é determinado com base nas definições de configuração para a partilha de implementação ligado.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **atualização MDTLinkedDS** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado da partilha de implementação ligado que está a ser atualizado.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **cadeia** escreva dados e produz adicionais **cadeia** escreva dados se o *verboso* parâmetro comum está incluído.  

#### <a name="example-1"></a>Exemplo 1  

```  
Update-MDTLinkedDS -Path "DS001:\Linked Deployment Shares\LINKED001"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo replica conteúdo a partir da partilha de implementação para a partilha de implementação ligado, a pasta de DS001:\Linked implementação Shares\LINKED001 do caminho do Windows PowerShell.  

###  <a name="Update-MDTMedia"></a>Atualização MDTMedia  
 Esta secção descreve o **atualização MDTMedia** cmdlet do Windows PowerShell. Execute este cmdlet a partir de uma consola do Windows PowerShell que tenha o MDT snap-in do PowerShell carregado. Para obter mais informações sobre como iniciar uma consola do Windows PowerShell que tenha o snap-in do PowerShell do MDT carregado, consulte "ao carregar o MDT Windows Snap-In do PowerShell".  

#### <a name="syntax"></a>Sintaxe  

```  
Update-MDTMedia -Path <String> [<CommonParameters>]  
```  

#### <a name="description"></a>Descrição  
 Este cmdlet replica conteúdo a partir de uma partilha de implementação para uma pasta que contém o suporte de dados de implementação a utilizar o perfil de seleção utilizado para definir o suporte de dados de implementação. O comportamento de replicação é determinado com base nas definições de configuração para o suporte de dados de implementação.  

 Suporte de dados no LTI permite-lhe efetuar implementações LTI apenas a partir do suporte de dados local sem ligar a uma partilha de implementação. Pode armazenar o suporte de dados num DVD, USB disco rígido ou outro dispositivo portátil. Depois de criar o suporte de dados, gere imagens WIM de arranque que permitem a implementação ser efetuada a partir de dispositivos de um suporte portátil localmente disponíveis no computador de destino.  

#### <a name="parameters"></a>Parâmetros  
 Esta subsecção fornece informações sobre os vários parâmetros que podem ser utilizadas com o **atualização MDTMedia** cmdlet.  

##### <a name="-path-string"></a>-Path < String\>  
 Este parâmetro especifica o caminho completamente qualificado para a pasta que contém o suporte de dados de implementação que está a ser atualizado.  

> [!NOTE]
>  Se este parâmetro não for fornecido, o diretório de trabalho do Windows PowerShell tem predefinido para a localização pretendida na partilha de implementação.  

|**Parâmetro**|**Valor**|  
|-|-|  
|**Necessário?**|**VERDADEIRO**|  
|**Posição?**|**Com o nome**|  
|**Valor predefinido**|–|  
|**Aceitar entrada de pipeline?**|**FALSO**|  
|**Aceitar carateres universais?**|**FALSO**|  

##### <a name="commonparameters"></a>< Parâmetroscomuns\>  
 Este cmdlet suporta os seguintes parâmetros comuns: *Verboso, depuração, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* e *WarningVariable.* Para obter mais informações, consulte o tópico "about_CommonParameters", que pode aceder, escrevendo o seguinte comando e, em seguida, premindo ENTER:  

```  
Get-Help about_CommonParameters  
```  

#### <a name="outputs"></a>saídas  
 Este cmdlet devolve um **cadeia** escreva dados e produz adicionais **cadeia** escreva dados se o *verboso* parâmetro comum está incluído.  

#### <a name="example-1"></a>Exemplo 1  

```  
Update-MDTMedia -Path "DS001:\Media\MEDIA001"  
```  

##### <a name="description"></a>Descrição  
 Neste exemplo replica conteúdo a partir da partilha de implementação para a pasta que contém o suporte de dados de implementação, a pasta de DS001:\Media \MEDIA001 do caminho do Windows PowerShell.  

## <a name="tables-and-views-in-the-mdt-db"></a>As tabelas e vistas na base de dados do MDT  
 No MDT, muitas definições de propriedade podem ser armazenadas (geralmente, configurado no ficheiro CustomSettings.ini) numa base de dados. Configurar as propriedades numa base de dados ajuda a criar um ficheiro CustomSettings.ini genérico que requer menos modificações e permite que um ficheiro CustomSettings.ini ser utilizado mais imagens (porque o ficheiro é mais genérico).  

 Personalize a base de dados no nó de base de dados no Deployment Workbench. Utilizar o Deployment Workbench, as definições de implementação podem ser configuradas e guardadas em tabelas.  

 No entanto, são realizadas consultas sobre as informações nas tabelas utilizar as vistas. Vistas de ajudam a simplificar as consultas ao associar resultados de várias tabelas. As vistas para devolver o resultado definido que consulta o ZTIGather.wsf o **parâmetros** e **ParameterCondition** especificar propriedades.  

### <a name="tables-in-the-mdt-db"></a>Tabelas na base de dados do MDT  
 A tabela seguinte lista as tabelas de base de dados que Deployment Workbench cria e gere.  

|**Tabela**|**Descrição**|  
|-|-|  
|ComputerIdentity|Utilizado para identificar um computador específico, utilizando qualquer combinação da **AssetTag, UUID, SerialNumber**, e **MACAddress** propriedades. A tabela inclui um **Descrição** coluna para fornecer um método amigável de utilizador que descrevem o computador (geralmente, o nome de computador).|  
|Descrições|Contém descrições de todas as propriedades configuráveis através da base de dados.|  
|LocationIdentity|Utilizado para identificar a localizações geográficas utilizando o **localização** propriedade. Os valores para esta propriedade são armazenados numa coluna correspondente na tabela.|  
|LocationIdentity_DefaultGateway|Está relacionada com os valores de gateway predefinidos com uma localização identificada na tabela LocationIdentity. Há uma relação um-para-muitos entre esta tabela e a tabela de LocationIdentity.|  
|MakeModelIdentity|Utilizado para identificar uma marca específica e o modelo de um computador com o **tornar** e **modelo** propriedades. Os valores para estas propriedades são armazenados nas colunas correspondentes na tabela.|  
|PackageMapping|Utilizado para associar o nome apresentado no item de adicionar ou remover o painel de controlo programas com um pacote do Configuration Manager e o programa para ser implementada em vez da aplicação adicionar ou remover programas. Para obter mais informações sobre esta tabela, consulte a secção "A implementar aplicações com base na aplicação versões anteriores", no documento MDT *guia de amostras do Toolkit de implementação do Microsoft.*|  
|RoleIdentity|Utilizado para identificar o objetivo de um computador ou os utilizadores de um computador com o **função** propriedade. Os valores para esta propriedade são armazenados numa coluna correspondente na tabela.|  
|Definições|Identifica as definições que são aplicadas a um computador individual ou um grupo de computadores com base nas definições nos computadores, funções, locais e efetuam e modelo de nós no nó de base de dados no Deployment Workbench.|  
|Settings_Administrators|Identifica as contas de utilizador a ser adicionado ao grupo de administrador local no computador de destino com base nas definições em computadores, funções, localizações e marca e modelo de nós no nó de base de dados no Deployment Workbench.|  
|Settings_Applications|Identifica as aplicações a ser implementado no computador de destino com base nas definições em computadores, funções, localizações e marca e modelo de nós no nó de base de dados no Deployment Workbench.|  
|Settings_Packages|Identifica os pacotes para ser implementado no computador de destino com base nas definições em computadores, funções, localizações e marca e modelo de nós no nó de base de dados no Deployment Workbench.|  
|Settings_Roles|Identifica as funções a associar ao computador de destino com base nas definições em computadores, localizações e marca e modelo de nós no nó de base de dados no Deployment Workbench.|  

### <a name="views-in-the-mdt-db"></a>Vistas na base de dados do MDT  
 A tabela seguinte lista e descreve as vistas da base de dados que são utilizadas ao consultar as informações de configuração na base de dados do MDT.  

|**Vista**|**Descrição**|  
|-|-|
|ComputerAdministrators|Utilizado para localizar todas as contas para ser tornados membros do grupo Administradores local no computador de destino. A vista é uma União das tabelas ComputerIdentity e Settings_Administrators.|  
|ComputerApplications|Utilizado para localizar todas as aplicações a ser implementado no computador de destino. A vista é uma União das tabelas ComputerIdentity e Settings_Applications.|  
|ComputerPackages|Utilizado para localizar todos os pacotes para ser implementado no computador de destino. A vista é uma União das tabelas ComputerIdentity e Settings_Packages.|  
|ComputerRoles|Utilizado para localizar todas as funções a associar ao computador de destino. A vista é uma União das tabelas ComputerIdentity e Settings_Roles.|  
|ComputerSettings|Utilizado para localizar todas as definições de propriedade para ser configurado para o computador de destino. A vista é uma União das tabelas ComputerIdentity e definições.|  
|LocationAdministrators|Utilizado para localizar todas as contas para ser tornada membro do grupo de administradores locais nos computadores de destino dentro de uma localização. A vista é uma União das tabelas LocationIdentity, LocationIdentity_DefaultGateway e Settings_Administrators.|  
|LocationApplications|Utilizado para localizar todas as aplicações para implementação em computadores de destino dentro de uma localização. A vista é uma União das tabelas LocationIdentity, LocationIdentity_DefaultGateway e Settings_Applications.|  
|LocationPackages|Utilizado para localizar todos os pacotes de implementação para computadores de destino dentro de uma localização. A vista é uma União das tabelas LocationIdentity, LocationIdentity_DefaultGateway e Settings_Packages.|  
|LocationRoles|Utilizado para localizar todas as funções de estar associado a computadores de destino dentro de uma localização. A vista é uma União das tabelas LocationIdentity, LocationIdentity_DefaultGateway e Settings_Roles.|  
|localizações|Utilizado para localizar os endereços IP para os gateways predefinidos dentro de uma localização ou para todas as localizações que contém um endereço IP especificado para um gateway predefinido. A vista é uma União das tabelas LocationIdentity e LocationIdentity_DefaultGateway.|  
|LocationSettings|Utilizado para localizar todas as definições de propriedade ser configuradas para computadores de destino dentro de uma localização. A vista é uma União das tabelas LocationIdentity, LocationIdentity_DefaultGateway e definições.|  
|MakeModelAdministrators|Utilizado para localizar todas as contas para ser tornados membros do grupo Administradores local nos computadores de destino com uma determinada marca e o modelo. A vista é uma União das tabelas MakeModelIdentity e Settings_Administrators.|  
|MakeModelApplications|Utilizado para localizar todas as aplicações para implementação em computadores de destino com uma determinada marca e o modelo. A vista é uma União das tabelas MakeModelIdentity e Settings_Applications.|  
|MakeModelPackages|Utilizado para localizar todos os pacotes para implementação em computadores de destino com uma determinada marca e o modelo. A vista é uma União das tabelas MakeModelIdentity e Settings_Applications.|  
|MakeModelRoles|Utilizado para localizar todas as funções associadas ao computadores de destino com uma determinada marca e o modelo. A vista é uma União das tabelas MakeModelIdentity e Settings_Roles.|  
|MakeModelSettings|Utilizado para localizar todas as definições de propriedade ser configuradas para computadores de destino com uma determinada marca e o modelo. A vista é uma União das tabelas MakeModelIdentity e definições.|  
|RoleAdministrators|Utilizado para localizar todas as contas para ser tornados membros do grupo Administradores local nos computadores de destino com uma função especificada. A vista é uma União das tabelas RoleIdentity e Settings_Administrators.|  
|RoleApplications|Utilizado para localizar todas as aplicações para implementação em computadores de destino com uma função especificada. A vista é uma União das tabelas RoleIdentity e Settings_Applications.|  
|RolePackages|Utilizado para localizar todos os pacotes para implementação em computadores de destino com uma função especificada. A vista é uma União das tabelas RoleIdentity e Settings_Packages.|  
|RoleSettings|Utilizado para localizar todas as definições de propriedade ser configuradas para computadores de destino com uma função especificada. A vista é uma União das tabelas RoleIdentity e definições.|  

## <a name="windows-7-feature-dependency-reference"></a>Referência de dependência do Windows 7 de funcionalidade  
 Tabela 8 apresenta uma lista de funcionalidades do Windows 7, a funcionalidade principal e quaisquer funcionalidades dependentes. Pode utilizar estas informações para determinar as funcionalidades e funções tem de ser instalado para suportar funcionalidades específicas a utilizar o [instalar funções e funcionalidades](#InstallRolesandFeatures) e [desinstalar funções e funcionalidades](#UninstallRolesandFeatures) sequência de tarefas passos.  

### <a name="table-8-windows-7-feature-dependency-reference"></a>Tabela 8. Referência de dependência do Windows 7 de funcionalidade  

|**Funcionalidade**|**Funcionalidade principal**|**Funcionalidades dependentes**|  
|-|-|-|  
|Windows Media® Center|Funcionalidades de suporte de dados|Pode afetar outras funcionalidades do Windows|  
|Maker de DVD do Windows|Funcionalidades de suporte de dados|Pode afetar outras funcionalidades do Windows|  
|Windows Media Player|Funcionalidades de suporte de dados|Pode afetar outras funcionalidades do Windows|  
|Procura do Windows|N/D|Pode afetar outras funcionalidades do Windows|  
|Internet Explorer (amd64)|N/D|Pode afetar outras funcionalidades do Windows|  
|Serviços da World Wide Web|Serviços de informação de Internet da Microsoft (IIS)|-Suporte da Microsoft colocação de mensagens (MSMQ) HTTP<br /><br /> -Ativação Windows Communication Foundation (WCF) HTTP|  
|Compatibilidade WMI do IIS 6|IIS, as ferramentas de gestão Web, compatibilidade de gestão do IIS 6|Ferramentas de script do IIS 6|  
|Extensibilidade de Microsoft .NET|IIS, serviços da World Wide Web, as funcionalidades de desenvolvimento de aplicações|-Microsoft ASP.NET<br /><br /> -O suporte MSMQ HTTP<br /><br /> -Ativação HTTP do WCF|  
|Documento predefinido|IIS, serviços da World Wide Web, as funcionalidades HTTP comuns|Suporte MSMQ HTTP|  
|Navegação nos diretórios|IIS, serviços da World Wide Web, as funcionalidades HTTP comuns|Suporte MSMQ HTTP|  
|Redirecionamento de HTTP|IIS, serviços da World Wide Web, as funcionalidades HTTP comuns|Suporte MSMQ HTTP|  
|Conteúdo estático|IIS, serviços da World Wide Web, as funcionalidades HTTP comuns|-Baseada na web o Distributed Authoring and Versioning (WebDAV) publicação<br /><br /> -O suporte MSMQ HTTP|  
|Registo personalizado|IIS, serviços da World Wide Web, o estado de funcionamento e diagnósticos|Suporte MSMQ HTTP|  
|Registo de HTTP|IIS, serviços da World Wide Web, o estado de funcionamento e diagnósticos|Suporte MSMQ HTTP|  
|Registo de ODBC|IIS, serviços da World Wide Web, o estado de funcionamento e diagnósticos|Suporte MSMQ HTTP|  
|Monitor de Pedidos|IIS, serviços da World Wide Web, o estado de funcionamento e diagnósticos|Suporte MSMQ HTTP|  
|rastreio|IIS, serviços da World Wide Web, o estado de funcionamento e diagnósticos|Suporte MSMQ HTTP|  
|Compressão de conteúdo estático|IIS, serviços da World Wide Web, as funcionalidades de desempenho|Suporte MSMQ HTTP|  
|Segurança|IIS, os serviços da World Wide Web|-A extensibilidade Microsoft .NET<br /><br /> -O suporte MSMQ HTTP<br /><br /> -Ativação HTTP do WCF|  
|Filtragem de Pedidos|IIS, serviços da World Wide Web, de segurança|-A extensibilidade Microsoft .NET<br /><br /> -O suporte MSMQ HTTP<br /><br /> -Ativação HTTP do WCF|  
|Visualizador XPS|N/D|Pode afetar outras funcionalidades do Windows|  

## <a name="udi-reference"></a>Referência de UDI  
 Esta referência fornece mais informações sobre UDI e inclui os tópicos em:  

-   Conceitos UDI conforme descrito em [conceitos de UDI](#UDIConcepts)  

-   OSDResults conforme descrito em [OSDResults referência](#OSDResultsReference)  

-   O instalador de aplicação centrado em utilizador conforme descrito em [referência de instalador de aplicação do utilizador Centric](#UserCentricAppInstallerReference)  

-   UDI prepara conforme descrito em [UDI fase referência](#UDIStageReference)  

-   Tarefas de UDI conforme descrito em [UDI tarefas referência](#UDITaskReference)  

-   Validações UDI conforme descrito em [UDI do validador de referência](#UDIValidatorReference)  

-   Páginas de Assistente de UDI conforme descrito em [referência de página do Assistente de UDI](#UDIWizardPageReference)  

 Cada um destes tópicos de referência são abordadas nas secções subsequentes.  

###  <a name="UDIConcepts"></a>Conceitos UDI  
 Esta secção contém conceitos que o ajudam a descrever UDI, o Assistente de UDI e o UDI Wizard Designer.  

####  <a name="DisplayName"></a>Nome a apresentar  
 O nome a apresentar é utilizado para fornecer um nome amigável de utilizador e descritivo para uma página do assistente na biblioteca de página no UDI Wizard Designer. O nome a apresentar é apresentado no texto azul para cada página do assistente, na biblioteca de página e no **fluxo** separador o UDI Wizard Designer.  

 Quando adicionar uma página para a biblioteca de página, tem de fornecer o nome a apresentar. Depois do Assistente de página é adicionada à biblioteca de página, não é possível alterar o nome a apresentar.  

####  <a name="Flow"></a>Fluxo  
 O **fluxo** separador mostra uma lista de páginas do assistente dentro de uma fase UDI no UDI Wizard Designer. Pode utilizar o **fluxo** separador para realizar as seguintes tarefas:  

-   Adicione uma página do Assistente da biblioteca de página para uma fase UDI arrastando a página da biblioteca de página para a fase UDI.  

-   Remova uma página do Assistente de uma fase UDI.  

-   Altere a sequência de páginas de assistente dentro de uma fase UDI.  

####  <a name="PageLibrary"></a>Biblioteca de página  
 A biblioteca de página contém todas as páginas actualmente carregadas no UDI Wizard Designer. Quando carregar um ficheiro de configuração do Assistente de UDI, todas as páginas do assistente definidas no ficheiro de configuração são apresentadas para a biblioteca de página. A biblioteca de página mostra as páginas do assistente, por ordem alfabética por tipos de página. Cada instância de um tipo de página específica está listada no tipo de página.  

 Por exemplo, poderá ter dois diferentes **WelcomePage** páginas do Assistente para diferentes fases. As duas **WelcomePage** páginas do assistente, serão listadas sob o **WelcomePage** tipo de página do assistente na biblioteca de página no UDI Wizard Designer.  

 Além disso, cada instância de página do assistente na biblioteca de página indica o número de vezes a página do assistente é utilizada em fluxos de fase. Quando paira o rato sobre uma página do assistente na biblioteca de página, é apresentada uma miniatura de página do assistente, juntamente com as fases que incluem essa página.  

####  <a name="PageName"></a>Nome da página  
 O nome da página é utilizado para identificar exclusivamente uma página do assistente na biblioteca de página no UDI Wizard Designer. O *nome da página* é o nome de uma fase UDI referencia para que o Assistente de UDI sabe qual página do Assistente para apresentar dentro de uma fase UDI específica. Quando adicionar uma página para a biblioteca de página, tem de fornecer o nome da página. Depois do Assistente de página é adicionado à biblioteca de página, não é possível alterar o nome da página. No UDI Wizard Designer, o nome da página é apresentado na parte inferior da página cada assistente na biblioteca de página no texto mais pequeno e não negrito.  

####  <a name="PrestagedMediaDeployments"></a>Implementações de suportes de dados  
 Suporte de suporte de dados pré-configurado é uma funcionalidade de implementação do sistema operativo no Configuration Manager que permite que um administrador para copiar e aplicar pré-configurar suportes de dados e processar de uma imagem do sistema operativo para um disco rígido antes do aprovisionamento. Este trabalho pode reduzir o tráfego de rede e o tempo necessário para o processo de aprovisionamento. Suporte de dados pré-configurado pode ser implementado como parte do processo de fabrico ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager.  

 Para obter mais informações sobre implementações de suportes de dados pré-configurados, consulte os seguintes recursos:  

-   [Planeamento de implementações de sistema operativo do suporte de dados no Configuration Manager](http://technet.microsoft.com/library/hh499044.aspx)  

-   [Sobre o suporte de dados pré-configurado para implementação do sistema operativo](http://technet.microsoft.com/library/gg294171.aspx)  

#### <a name="stage-group"></a>Fase de grupo  
 Utilize uma fase fases ao grupo do grupo de um ou mais o UDI Wizard Designer. Grupos de fase UDI aproximadamente ligado estão relacionados com cenários de implementação do MDT, mas não existe nenhum uma correlação entre os dois.  

####  <a name="Stage"></a>Fase  
 A *fase* é um subconjunto de todas as páginas no ficheiro de configuração do Assistente de UDI que utiliza um cenário de implementação do MDT. Quando inicia o Assistente de UDI utilizando o **Assistente de UDI** passo de sequência de tarefas, o **/testar** parâmetro especifica a fase para executar, que por sua vez Especifica o conjunto de páginas a utilizar. Pode pré-visualizar a forma como as páginas do assistente irão aparecer numa fase clicando **pré-visualização** no **assistente Preview** grupo no Friso. Pode utilizar uma fase UDI mais do que um cenário de implementação MDT, apesar da fase UDI está definida apenas uma vez o UDI Wizard Designer. Por exemplo, a fase de NewComputer pode ser utilizada em cenários de implementação MDT novo computador e de substituir o computador.  

####  <a name="Task"></a>Tarefa  
 *Tarefas UDI* software que é executado numa página do Assistente para realizar funções específicas. Em alguns casos, estas tarefas são utilizadas para verificar se o computador de destino está pronto para a implementação. Outras tarefas podem ser utilizadas para efetuar os passos de implementação, tais como copiar ficheiros de configuração ou o resultado.  

> [!NOTE]
>  O **seguinte** botão na página do assistente, em que as tarefas são executadas será desativado se qualquer uma das tarefas concluída com aviso ou erro de estado de conclusão.  

 UDI inclui várias tarefas incorporadas que permitem-lhe executar a maioria das tarefas necessárias para a implementação. Para obter mais informações sobre as tarefas de incorporada de UDI, consulte [incorporada UDI tarefas](#BuiltinUDITasks).  

 O **Shell executar** tarefa UDI incorporada permite-lhe executar qualquer software (scripts) que pode ser iniciado a partir de uma linha de comandos, como scripts de Visual Basic ou o Windows PowerShell. Esta funcionalidade permite que criar tarefas utilizando familiares linguagens de scripts. Para obter mais informações, consulte [Shell executar tarefas](#ShellExecuteTask).  

 Se os requisitos de ponha scripting, pode escrever tarefas UDI personalizadas. *Tarefas UDI* são DLLs escritos em C++ e implemente o **ITask** interface. Registe a DLL com a biblioteca de tarefas de UDI Wizard Designer através da criação de um ficheiro de configuração (. config) de UDI Wizard Designer e colocá-lo no *installation_folder*\Bin\Config pasta (onde *installation_ pasta* é a pasta na qual instalou o MDT). Para obter mais informações sobre o desenvolvimento das tarefas UDI personalizadas, consulte a secção "Criar personalizado UDI tarefas", no *guia para programadores do modo instalação*.  

####  <a name="UDITaskSequence"></a>Sequência de tarefas UDI  
 Criar uma sequência de tarefas UDI utilizando um dos seguintes específicos de UDI MDT tarefas sequência modelos, que execute o Assistente de UDI o passo da sequência de tarefas adequadas:  

-   **Sequência de tarefas de instalação orientado por utilizador.** Este modelo de sequência de tarefas é utilizado para os cenários de implementação do novo computador, atualize e de computador substituir MDT do computador.  

-   **Sequência de tarefas de substituição de instalação orientado por utilizador.** Este modelo de sequência de tarefas é o primeiro passo num processo de dois passos do cenário de implementação de substituir o computador e é utilizado para capturar os dados de migração de estado do utilizador. O segundo passo no processo de dois passos é o modelo de sequência de tarefas de sequência de tarefas de instalação de modo, que utilizar para implementar o sistema operativo e aplicações de destino e restaurar os dados de migração de estado de utilizador guardados durante o primeiro passo do processo.  

 Para obter mais informações sobre modelos de sequência de tarefas UDI, consulte a secção "Identificar o UDI tarefas sequência modelos no MDT", no documento MDT *utilizar o Microsoft Deployment Toolkit*. Para obter mais informações sobre estes componentes, consulte a secção "Identificar UDI processo componentes de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit*, que está incluída no MDT.  

####  <a name="UDIWizard"></a>Assistente UDI  
 O Assistente de UDI fornece da IU para recolher as definições de implementação que as sequências de tarefas UDI consumam. O Assistente de UDI é iniciado como parte de uma sequência de tarefas UDI e recolhe as informações de configuração necessários para personalizar a implementação dos sistemas operativos cliente Windows e aplicações. As páginas do assistente ler as respetivas definições de configuração do ficheiro de configuração de Assistente de UDI, personalizado com o UDI Wizard Designer.  

 O Assistente de UDI é iniciado pelo **Assistente de UDI** passo de sequência de tarefas nas sequências de tarefas criadas utilizando os modelos de sequência de tarefas UDI. O **Assistente de UDI** passo de sequência de tarefas executa o script de UDIWizard.wsf, que por sua vez inicia o Assistente de UDI (OSDSetupWizard.exe). 9 de tabela lista os parâmetros da linha de comandos do Assistente de UDI e fornece uma breve descrição de cada.  

### <a name="table-9-udi-wizard-command-line-parameters"></a>Tabela 9. Parâmetros de linha de comandos de assistente UDI  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**/Preview**|Permite-lhe pré-visualizar a configuração atual do assistente, Ativando a **seguinte** botão, o que lhe permite mover de uma página sem necessidade de entrada válida.|  
|**/XML**|Especifica o nome do ficheiro de configuração do Assistente de UDI. O script de UDIWizard.wsf define automaticamente este parâmetro para o ficheiro OSDSetupWizard.xml, que é armazenado na pasta em que a sequência de tarefas armazena os ficheiros de registo. Este parâmetro assume o ficheiro config.xml.<br /><br /> A sintaxe para este parâmetro é o seguinte (onde `<full_path>` é o caminho completamente qualificado para o ficheiro. XML, incluindo o nome de ficheiro e a extensão):<br /><br /> `/xml:<full_path>`|  
|**/Stage**|Especifica o nome a fase de UDI para ser executada. O script de UDIWizard.wsf define automaticamente este parâmetro para a fase apropriada, conforme descrito em [referência de fase de UDI](#UDIStageReference). Este parâmetro será assumida a primeira fase no ficheiro de configuração do Assistente de UDI.<br /><br /> A sintaxe para este parâmetro é o seguinte (onde `<stage_name>` é o nome da fase a ser executada):<br /><br /> `/stage:<stage_name>`<br /><br /> Nota:<br /><br /> O valor de < stage_name > é sensível às maiúsculas e minúsculas.|  
|**/Locale**|Especifica a linguagem a utilizar o Assistente de UDI sob a forma de um identificador de região (LCID), que é representada por um valor numérico. Para obter uma lista dos LCIDs disponíveis, consulte [IDs de região atribuídos pela Microsoft](http://msdn.microsoft.com/goglobal/bb964664).<br /><br /> Teria de utilizar esta lista para identificar o idioma que pretende utilizar e, em seguida, forneça o LCID correspondente.<br /><br /> A sintaxe para este parâmetro é o seguinte (onde `<locale_id>` é o valor numérico do LCID a ser utilizado):<br /><br /> `/locale:<locale_id>`|  

####  <a name="UDIWizardApplicationConfigurationFile"></a>Ficheiro de configuração da aplicação de assistente UDI  
 O **ApplicationPage** página do assistente configura o ficheiro de configuração de aplicação do Assistente de UDI, que mantém a lista de software seja instalado. Este ficheiro contém uma entrada para cada aplicação do Configuration Manager ou programa e pacote que foi adicionado com o UDI Wizard Designer.  

 Este ficheiro tem o mesmo nome que o ficheiro de configuração do Assistente de UDI, mas com uma extensão. App. Por exemplo, se o ficheiro de configuração do Assistente de UDI é denominado *Config.xml,* , em seguida, o ficheiro de configuração de aplicação de Assistente de UDI correspondente seria *Config.xml.app.* Este ficheiro é complementar para o ficheiro de configuração do Assistente de UDI.  

####  <a name="UDIWizardConfigurationFile"></a>Ficheiro de configuração do assistente UDI  
 O Assistente de UDI lê o ficheiro de configuração do Assistente de UDI para determinar as páginas do Assistente para ser apresentada, a sequência de páginas do assistente, qualquer predefinido para os controlos nas páginas do assistente, e se os controlos estão ativados ou desativados. Este ficheiro contém todas as definições de configuração que são apresentadas no Assistente de UDI e são configuradas utilizando o UDI Wizard Designer.  

 Um ficheiro de configuração separado — o ficheiro de configuração de aplicação de Assistente de UDI — é utilizado para configurar as aplicações sejam instaladas no computador de destino.  

####  <a name="UDIWizardDesigner"></a>UDI Wizard Designer  
 O UDI Wizard Designer é a principal ferramenta para personalizar as páginas do Assistente para os cenários de implementação diferentes UDI suporta. As alterações efetuadas o UDI Wizard Designer são guardadas no ficheiro de configuração do Assistente de UDI e, em última análise se refletir a experiência de utilizador no Assistente de UDI. O utilizador efetua a implementação irá ver apenas as páginas do assistente no Assistente de UDI que tenha selecionado e configurado com o UDI Wizard Designer.  

 Embora o Assistente de UDI iria executar com o ficheiro de configuração do Assistente de UDI predefinição, as páginas do assistente não seriam configuradas corretamente. É recomendado que utilize o UDI Wizard Designer para configurar a experiência de utilizador do Assistente de UDI.  

> [!NOTE]
>  Para executar o UDI Wizard Designer, tem de ter os direitos adequados no Configuration Manager para aceder aos objetos, tais como imagens, pacotes ou aplicações.  

####  <a name="Validator"></a>A validação do  
 Utilize validações UDI para ajudar a garantir que as informações corretas são introduzidas em campos de texto nas páginas do assistente no Assistente de UDI. UDI inclui várias validações incorporadas que ajuda a realizar validações típicas de campos utilizados para introdução de texto, tais como impedir os utilizadores a introduzir carateres inválidos e garantir que o campo é não vazia. Quando um validador Deteta uma entrada inválida numa caixa de texto, será apresentada uma mensagem na página do assistente e o **seguinte** botão está desativado até que todas as entradas inválidas sejam resolvidas.  

 UDI inclui validações incorporadas que permitem-lhe executar a maioria da validação necessária para a implementação. Para obter mais informações sobre validadores UDI incorporadas, consulte [incorporada UDI validações](#BuiltinUDIValidators).  

 Se os requisitos de ponha validações UDI incorporadas, pode escrever validações UDI personalizadas. *Validações UDI* são DLLs escritos em C++, que implementa o **IValidator** interface. Registe a DLL com a biblioteca de validação de UDI Wizard Designer através da criação de um ficheiro de configuração (. config) de UDI Wizard Designer e colocá-lo no *installation_folder*\Bin\Config pasta (onde *installation_ pasta* é a pasta na qual instalou o MDT). Para obter mais informações sobre o desenvolvimento das tarefas UDI personalizadas, consulte a secção "Criar personalizado UDI Validators", no documento MDT *guia para programadores do modo instalação*.  

####  <a name="WizardPage"></a>Página do Assistente  
 Utilize uma página do Assistente para recolher informações de configuração no Assistente de UDI. Configure páginas de assistente UDI com o UDI Wizard Designer. As definições de configuração são armazenadas no ficheiro de configuração do Assistente de UDI e são lidas pela página do assistente, quando a página é inicializada no Assistente de UDI.  

 Páginas de assistente são armazenadas no Assistente de biblioteca de página e podem ser utilizadas nas fases UDI um ou mais. Esta estrutura permite-lhe configurar uma página do assistente que é partilhada entre fases, uma vez para todas as fases, reduzindo significativamente a quantidade de esforço e a complexidade de configuração de página do Assistente de atualização.  

 UDI inclui páginas do assistente incorporadas e editores de página do assistente que são normalmente suficientes para a maioria das implementações. Para obter mais informações sobre as páginas do assistente incorporadas, consulte [incorporada páginas do Assistente de UDI](#BuiltinUDIWizardPages).  

 Se os requisitos de ponha as páginas do assistente UDI incorporadas e correspondente editores de página do assistente, pode escrever páginas do assistente UDI personalizadas e editores de página do assistente. Páginas de assistente UDI são implementadas como dll, que lê o Assistente de UDI. Editores de página do assistente, são criados utilizando C++ no Visual Studio.  

 Para obter mais informações sobre o desenvolvimento das páginas do assistente UDI personalizadas, consulte a secção "Criar personalizado UDI páginas do assistente", no documento MDT *guia para programadores do modo instalação*.  

####  <a name="WizardPageEditor"></a>Editor de página do Assistente  
 Utilize um editor de página do Assistente para configurar uma página do Assistente de UDI Wizard Designer. Um editor de página do assistente atualiza as definições de configuração de página do assistente no ficheiro de configuração do Assistente de UDI; UDI inclui um editor de página do assistente incorporadas para cada página do assistente incorporada. Para obter mais informações sobre as páginas do assistente incorporadas e editores de página do assistente, consulte [incorporada páginas do Assistente de UDI](#BuiltinUDIWizardPages).  

 Se os requisitos de ponha as páginas do assistente UDI incorporadas e correspondente editores de página do assistente, pode escrever páginas do assistente UDI personalizadas e editores de página do assistente. Editores de página do assistente UDI são implementados como dll, que lê o UDI Wizard Designer. Crie página do Assistente para editores utilizando:  

-   [Windows Presentation Foundation](http://msdn.microsoft.com/library/ms754130.aspx) versão 4.0  

-   [Microsoft prisma](http://compositewpf.codeplex.com/) versão 4.0  

-   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) versão 2.1  

 Para obter mais informações sobre o desenvolvimento das personalizado editores de página do assistente UDI, consulte a secção "Criar personalizado assistente página editores", no documento MDT *guia para programadores do modo instalação*.  

###  <a name="OSDResultsReference"></a>Referência de OSDResults  
 **OSDResults** é uma parte de UDI que apresenta os resultados de uma implementação efetuada utilizando o UDI. **OSDResults** apresenta o **implementação concluída** caixa de diálogo. **OSDResults** é apresentada antes da hora de início de sessão primeiro Windows o computador de destino é iniciado. O utilizador pode utilizar **OSDResults** e as informações apresentadas a **implementação concluída** caixa de diálogo para determinar o estado de conclusão do processo de implementação e a configuração do computador antes iniciar sessão pela primeira vez. Além disso, as informações no **OSDResults** pode ser utilizado para resolver quaisquer problemas durante o processo de implementação.  

 Pode configurar alguns dos elementos de interface de utilizador para **OSDResults** através do ficheiro OSDResults.exe.config, que reside no Tools\OSDResults no MDT ficheiros de pacote do Configuration Manager. Tabela 10 lista as definições de configuração no ficheiro OSDResults.exe.config.  

### <a name="table-10-configuration-settings-in-the-osdresultsexeconfig-file"></a>Tabela 10. Definições de configuração no ficheiro OSDResults.exe.config  

|**Definição**|**Descrição**|  
|-|-|  
|**headerImagePath**|Esta definição permite-lhe especificar o caminho completamente qualificado ou relativo para um ficheiro de *.bmp que é apresentado no cabeçalho de **OSDResults** caixa de diálogo.<br /><br /> O valor predefinido para esta definição é o seguinte:<br /><br /> `images\UDI_Wizard_Banner.bmp`|  
|**backgroundWallpaper**|Esta definição permite-lhe especificar o caminho completamente qualificado ou relativo para um ficheiro. jpg, que é apresentado como a imagem de fundo no **OSDResults** caixa de diálogo.<br /><br /> O valor predefinido para esta definição é o seguinte:<br /><br /> `images\Wallpaper.jpg`|  
|**welcomeText**|Esta definição permite-lhe especificar o texto que agradece o utilizador e fornece informações sobre o processo de implementação. É apresentada no **OSDResults** caixa de diálogo.|  
|**completedText**|Esta definição permite-lhe especificar o texto que indica se o processo de implementação está completado. É apresentada no **OSDResults** caixa de diálogo.|  
|**timeoutMinutes**|Esta definição permite-lhe especificar o período de tempo a **OSDResults** é apresentada a caixa de diálogo antes de apresentar automaticamente o ecrã de início de sessão do Windows. O valor para esta definição é especificado em minutos.<br /><br /> O valor predefinido para esta definição é zero (0), que indica que o **OSDResults** irá ser apresentada a caixa de diálogo indefinidamente até fechado manualmente.|  

 Segue-se o processo de alto nível para o **OSDResults** funcionalidade funciona em UDI:  

1.  Uma sequência de tarefas é executado no computador de destino.  

     A sequência de tarefas é baseada dos modelos de sequência de tarefas followUDI:  

    -   **Utilizador suscitada pelo departamento de sequência de tarefas de instalação**. Este modelo de sequência de tarefas é utilizado para cenários de implementação MDT novo computador, atualize e de computador substituir MDT do computador.  

    -   **Sequência de tarefas de substituição de instalação condicionada por utilizador**. Este modelo de sequência de tarefas é o primeiro passo num processo de dois passos do cenário de implementação do MDT substituir o computador e é utilizado para capturar os dados de migração de estado do utilizador. O segundo passo no processo de dois passo é o cenário de implementação do MDT novo computador com o **sequência de tarefas de instalação orientadas por utilizador** modelo de sequência de tarefas, que é utilizado para implementar as aplicações de destino e o sistema operativo e restaurar os dados de migração de estado de utilizador guardados durante o primeiro passo do processo  

     Para obter mais informações sobre o:  

    -   Modelos de sequência de tarefas UDI, consulte a secção "Identificar o UDI tarefas sequência modelos no MDT", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

    -   Relação entre os cenários de implementação do MDT e fases UDI, consulte [UDI fase referência](#UDIStageReference)  

2.  Durante a sequência de tarefas, as definições de configuração fornecidas pelo variáveis de sequência de tarefas e da intervenção do utilizador no Assistente de UDI são guardadas no *% DEPLOYROOT %*\Tools\OSDResults pasta no computador de destino (onde *%D % EPLOYROOT* é a raiz da pasta na qual os ficheiros do MDT são localmente colocadas em cache no computador de destino).  

3.  No **OSD resultados e Branding** grupo na sequência de tarefas, os seguintes passos de sequência de tarefas são executados que afetem **OSDResults**:  

    -   **Resultados OSD da cache.** Este passo de sequência de tarefas copia os conteúdos do *% DEPLOYROOT %*\Tools\OSDResults pasta para a pasta %WINDIR%\UDI no computador de destino. Isto garante que o conteúdo da pasta OSDResults irá ser persistente, após a conclusão da sequência de tarefas.  

    -   **Execute os resultados OSD.** Este passo de sequência de tarefas configura o computador de destino para executar **OSDResults** na primeira vez que o computador é iniciado.  

4.  O computador de destino é iniciado pela primeira vez, e OSDResults.exe é executado antes do ecrã de início de sessão do Windows.  

     O **boas-vindas** separador o **implementação concluída** é apresentada a caixa de diálogo. O **boas-vindas** separador fornece informações úteis sobre as implementação e informações de contacto no caso de que são descobertos problemas com a implementação.  

     Reveja as informações de **resumo de implementação** e **aplicações instaladas** separadores para verificar se o sistema operativo e as aplicações foram instaladas corretamente. Quando tiver terminado de rever estas tabelas, clique em **iniciar Windows** para iniciar sessão do Windows 7 pela primeira vez.  

    > [!NOTE]
    >  Aplicações do Configuration Manager não são apresentadas no **aplicações instaladas** separador. As aplicações do Configuration Manager são detetadas quando o utilizador inicia sessão no computador de destino pela primeira vez.  

5.  É apresentado o ecrã de início de sessão do Windows e o processo de início de sessão continua normalmente.  

     AppInstall.exe está a executar na primeira vez que um utilizador inicia sessão computador de destino. Para obter mais informações sobre este processo, consulte [centrada no utilizador referência de instalador de aplicação](#UserCentricAppInstallerReference).  

###  <a name="UserCentricAppInstallerReference"></a>Referência de instalador de aplicação centrada no utilizador  
 A funcionalidade de instalador de aplicação centrada no utilizador no UDI é utilizada para comunicar todas as aplicações instaladas durante o processo de implementação de UDI para a funcionalidade de catálogo de aplicações no Configuration Manager. A funcionalidade de instalador de aplicação centrada no utilizador fornece a ligação entre as aplicações selecionadas no **ApplicatonPage** página do assistente no Assistente de UDI e quaisquer aplicações do Configuration Manager opcional publicitado aos utilizadores.  

 Para obter mais informações sobre a funcionalidade de catálogo de aplicações no Configuration Manager, consulte [gestão de aplicações no Configuration Manager](http://technet.microsoft.com/library/gg699373.aspx).  

 Segue-se o processo de alto nível para o funcionamento a funcionalidade de instalação da aplicação num UDI:  

1.  Aplicações do Configuration Manager são criadas no Configuration Manager.  

     Para obter mais informações sobre como criar e gerir aplicações do Configuration Manager, consulte os seguintes recursos:  

    -   [Como criar aplicações no Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Operações e manutenção de gestão de aplicações no Configuration Manager](http://technet.microsoft.com/library/gg681963.aspx)  

2.  As coleções de utilizador do Configuration Manager são criadas e os utilizadores são adicionados à coleção.  

     Para obter mais informações sobre como criar e gerir coleções de utilizadores e adicionar utilizadores em coleções, consulte os seguintes recursos:  

    -   [Coleções no Configuration Manager](http://technet.microsoft.com/library/gg682169.aspx)  

    -   [Como criar coleções no Configuration Manager](http://technet.microsoft.com/library/gg712295.aspx)  

3.  As aplicações do Configuration Manager são implementadas em coleções de utilizadores.  

     Para obter mais informações sobre como implementar aplicações para coleções de utilizadores, consulte [como implementar aplicações no Configuration Manager](http://technet.microsoft.com/library/gg682082.aspx).  

4.  As aplicações do Configuration Manager são disponibilizadas no **ApplicatonPage** página do assistente com o UDI Wizard Designer.  

     Para obter mais informações sobre como disponibilizar aplicações do Configuration Manager no **ApplicatonPage** página do assistente, consulte a secção "passo 5-11: Personalizar o ficheiro de configuração do Assistente de UDI para o computador de destino,"no documento MDT *guia rápido para a instalação de modo*.  

5.  UDA for configurado através de um dos seguintes métodos:  

    -   Na consola do Configuration Manager (para obter mais informações sobre como configurar UDA na consola do Configuration Manager, consulte [como gerir afinidade dispositivo / utilizador no Configuration Manager](http://technet.microsoft.com/library/gg699365.aspx).)  

    -   No **UDAPage** página do assistente no Assistente de UDI (para obter mais informações sobre o **UDAPage** página do assistente, consulte [UDAPage](#UDAPage).)  

     Após UDA estiver configurada, a conta de utilizador especificado será o utilizador primário para o computador de destino.  

    > [!NOTE]
    >  Só pode ser configurada por UDI UDA o cenário de implementação do novo computador. Não pode ser configurado nos cenários de implementação computador atualizar ou substituir.  

6.  A sequência de tarefas é executada e o utilizador seleciona as aplicações do Configuration Manager no **ApplicatonPage** página do assistente no Assistente de UDI.  

     O Assistente de UDI é executado **Assistente de UDI** passo de sequência de tarefas no **Preinstall** grupo da sequência de tarefas. Quando o utilizador seleciona aplicações do Configuration Manager no **ApplicatonPage** página do assistente, a página do assistente cria uma variável de sequência de tarefas separadas para cada aplicação selecionada.  

     Para obter mais informações sobre as aplicações do Configuration Manager no **ApplicatonPage** página do assistente no Assistente de UDI, consulte a secção "passo 6-4: Iniciar o computador de destino com os suportes de sequência de tarefas", no documento MDT *guia rápido para a instalação de modo*.  

7.  A sequência de tarefas instala as aplicações do Configuration Manager que foram selecionadas no passo anterior.  

     As aplicações do Configuration Manager são instaladas utilizando os seguintes passos de sequência de tarefas no **instalar aplicações** grupo da sequência de tarefas:  

    -   **Converter a lista de dois dígitos**  

    -   **Instalar a aplicação**  

8.  A sequência de tarefas efetua as seguintes tarefas a **OSD resultados e Branding** grupo antes de iniciar o sistema operativo de destino pela primeira vez:  

    -   Copia informações utilizadas para OSDResults.exe para a pasta %WINDIR%\UDI no computador de destino no **Cache OSD resultados** passo de sequência de tarefas  

    -   Regista as variáveis de sequência de tarefas criadas no passo 6 para as aplicações do Configuration Manager no registo no computador de destino no **imagem corporativa Reg** e **imagem corporativa Reg x64** passos de sequência de tarefas  

         As variáveis de sequência de tarefas são guardadas na seguinte localização no registo:  

         **HKEY_LOCAL_MACHINE\Software\Microsoft\MPSD\OSD**  

    -   Configura o sistema operativo de destino para OSDResults.exe executar automaticamente quando o computador é iniciado antes do ecrã de início de sessão do Windows no **executar resultados de OSD** passo de sequência de tarefas  

    -   Configura o sistema operativo de destino para executar automaticamente AppInstall.exe quando um utilizador inicia sessão no computador para a primeira vez o **executar resultados de OSD** passo de sequência de tarefas  

    -   Configura uma tarefa no sistema operativo de destino para remover a pasta %WINDIR%\UDI um mês a data da implementação  

9. O computador de destino é iniciado e OSDResults.exe é executado.  

     Para mais informações sobre OSDResults.exe, consulte [OSDResults referência](#OSDResultsReference).  

10. Um utilizador inicia sessão computador de destino e AppInstall.exe inicia automaticamente.  

11. AppInstall verifica se o utilizador com sessão atualmente iniciada a um utilizador primário que foi configurado no UDA.  

     A *utilizador primário* é um utilizador que utiliza o dispositivo regularmente e é considerado o proprietário ou um dos proprietários, do dispositivo.  

     Se o utilizador atualmente com sessão iniciada é:  

    -   Não é um utilizador principal, em seguida, AppInstall.exe interrompe  

    -   Um utilizador principal, em seguida, AppInstall.exe lê as entradas do registo guardadas no passo 8 para determinar quais as aplicações que foram instaladas  

12. AppIntaller estabelece ligação ao Configuration Manager e lê o catálogo de aplicações utilizando os seguintes passos:  

    1.  AppInstall irá aguardar 5 minutos depois desta ser iniciada permitir que as políticas do Configuration Manager estar disponível.  

    2.  Após 5 minutos, AppInstall tenta estabelecer ligação ao catálogo de aplicações.  

    3.  Se AppInstall não é possível estabelecer ligação, em seguida, irá aguardar por um período de tempo antes de tentar estabelecer novamente a ligação.  

    4.  AppInstall tenta ligar-se até cinco vezes antes de sair.  

     Pode configurar o atraso de tempo limite de ligação e o número de tentativas de AppInstall através do ficheiro AppInstall.exe.config, que reside na pasta Tools\OSDResults no pacote de Configuration Manager de ficheiros do MDT. Tabela 11 lista as definições de configuração no ficheiro AppInstall.exe.config.  

### <a name="table-11-configuration-settings-in-the-appinstallexeconfig-file"></a>Tabela 11. Definições de configuração no ficheiro AppInstall.exe.config  

|**Definição**|**Descrição**|  
|-|-|  
|**timeoutMinutes**|Esta definição permite-lhe especificar o período de tempo para AppInstall aguardar uma resposta do catálogo de aplicações do Configuration Manager antes de exceder o tempo limite. O valor for especificado em minutos. O valor predefinido para esta definição é **5**.|  
|**delayTimer**|Esta definição permite-lhe especificar o período de tempo para AppInstall a aguardar antes de tentar efetuar a ligação ao catálogo de aplicações do Configuration Manager. O valor for especificado em minutos. O valor predefinido para esta definição é **5**.|  

1.  AppInstall compara a lista de aplicações detetadas no registo com a lista de aplicações disponíveis no Configuration Manager catálogo de aplicações para o utilizador com sessão iniciado atualmente.  

     Se a aplicação detetada no registo:  

    -   Está disponível no catálogo de aplicações, em seguida, AppInstall.exe mapeia as aplicações e identifica as aplicações como existentes no registo e no catálogo de aplicações. Estas aplicações serão utilizadas no passo seguinte.  

    -   Não está disponível no catálogo de aplicações, em seguida, AppInstall.exe não cria um mapeamento. Estas aplicações não serão utilizadas no passo seguinte.  

2.  AppInstall utiliza APIs do Configuration Manager para iniciar a instalação das aplicações mapeadas.  

     As aplicações utilizadas neste passo foram mapeadas no passo anterior. Que diga, estes foram listados no registo tanto encontrados no catálogo de aplicações.  

3.  Como parte do processo de instalação, o Configuration Manager Deteta se a aplicação já está instalada.  

     Porque a aplicação já foi instalada, registos do Configuration Manager que a aplicação foi implementada com êxito para esse utilizador e a aplicação serão apresentados no Centro de Software para esse utilizador. O Configuration Manager começa a gestão e monitorização da aplicação para esse utilizador.  

4.  Depois de 1 mês, a tarefa criada no computador de destino no passo 8 executa e remove a pasta %WINDIR%\UDI.  

     A pasta é mantida para 1 mês para que os utilizadores primários tem uma oportunidade para ser o registo no e executar AppInstall.exe.  

###  <a name="UDIStageReference"></a>Referência de fase UDI  
 Os cenários de implementação do MDT utilizam um ou mais UDI [fase](#Stage). Cada fase UDI utilizada nos cenários de implementação MDT é abordado na secção subsequente no contexto do cenário de implementação MDT. Em alguns cenários de implementação do MDT, é utilizada apenas uma fase. Outros cenários de implementação do MDT, várias fases são utilizadas no cenário. Para obter mais informações sobre os cenários de implementação do MDT, consulte a secção "Identificar cenários de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit.*  

 A tabela 12 lista os cenários de implementação do MDT e fornece uma breve descrição de cada um, como cada cenário está selecionado e as fases UDI são utilizados em cada cenário de implementação. MDT automaticamente determina qual o cenário de implementação MDT para utilizar com base no modelo de sequência de tarefas do MDT que utilizar para criar a sequência de tarefas e na forma como a sequência de tarefas é iniciada.  

 Cada fase UDI utilizada nos cenários de implementação MDT é abordado na secção subsequente no contexto do cenário de implementação MDT. Em alguns cenários de implementação do MDT, é utilizada apenas uma fase. Outros cenários de implementação do MDT, várias fases são utilizadas no cenário. Para obter mais informações sobre os cenários de implementação do MDT, consulte a secção "Identificar cenários de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit.*  

### <a name="table-12-mdt-deployment-scenarios-and-udi-stages"></a>A tabela 12. Cenários de implementação do MDT e UDI fases  

|**Cenário**|**Descrição**|   
|-|-|  
|Novo computador|O MDT para UDI seleciona automaticamente este cenário quando tiver:<br /><br /> -Criar a sequência de tarefas anunciado utilizando o modelo de sequência de tarefas de sequência de tarefas de instalação de modo<br /><br /> -Inicie a sequência de tarefas no Windows PE utilizando o arranque PXE, suportes de dados de arranque de sequência de tarefas ou suportes de dados para o NEWCOMPUTER. Fase pré-configurado<br /><br /> Este cenário pode ser utilizado com implementações tradicionais ou com implementações de suportes de dados como suportado no Configuration Manager. Execute o Assistente de UDI com as seguintes fases UDI para suportar cada tipo de implementação:<br /><br /> - **Fase NEWCOMPUTER.** O Assistente de UDI é executado com esta fase no **sequência de tarefas de instalação de modo** sequência de tarefas, quando a imagem do sistema operativo é armazenada nos pontos de distribuição. Para obter mais informações, consulte [NEWCOMPUTER fase](#NEWCOMPUTERStage).<br /><br /> -                         **NEWCOMPUTER. Fase de pré-configuração.** O Assistente de UDI é executado com esta fase no **sequência de tarefas de instalação de modo** sequência de tarefas, quando a imagem do sistema operativo é armazenada num disco local no computador de destino (pré-configurados). Para obter mais informações, consulte [NEWCOMPUTER. Fase de pré-configurado](#NEWCOMPUTERPrestagedStage).|  
|Atualizar computador|O MDT para UDI seleciona automaticamente este cenário quando tiver:<br /><br /> -Criar a sequência de tarefas anunciado utilizando o modelo de sequência de tarefas de sequência de tarefas de instalação de modo<br /><br /> -Iniciar a sequência de tarefas no sistema operativo existente do Windows no computador de destino (e não no Windows PE)<br /><br /> -O Assistente de UDI é executado com a fase de ATUALIZAÇÃO para suportar este cenário de implementação. Para obter mais informações, consulte [ATUALIZAR fase](#REFRESHStage).|  
|Substituir o computador|Este cenário inclui a um computador existente e um computador de substituição. Uma sequência de tarefas separadas é criada e executar em cada computador, conforme descrito na seguinte processo:<br /><br /> -                          **No computador existente.** O MDT para UDI seleciona automaticamente esta parte do cenário quando tiver:<br /><br /> -Criar a sequência de tarefas anunciado utilizando o modelo de sequência de tarefas de instalação de modo substituir a sequência de tarefas<br /><br /> Iniciar a sequência de tarefas no sistema operativo existente do Windows no computador de destino (e não no Windows PE)<br /><br /> O Assistente de UDI é executado com as seguintes fases UDI para suportar este cenário de implementação:<br /><br /> - **Fase de substituição.** Nesta fase é executada no sistema operativo Windows existente e capturas de informações de configuração no Windows.<br /><br /> -                          **SUBSTITUA. Fase WinPE.** Nesta fase é executada no Windows PE e conclui a captura de informações de configuração do computador existente — por exemplo, executar USMT e o utilizador a capturar dados de migração de estado.<br /><br /> O estado do utilizador é capturado para uma pasta partilhada de rede ou para uma unidade USB local.<br /><br /> Para mais informações sobre a substituir e a substituir. Fases do WinPE, consulte [substituir e a substituir. Fases do WinPE](#REPLACEandREPLACEWinPEStages).<br /><br /> -                          **No computador de substituição.** Esta parte do cenário é idêntica do cenário de novo computador, exceto que o estado de utilizador capturado no passo anterior é restaurado. O MDT para UDI seleciona automaticamente esta parte do cenário quando tiver:<br /><br /> -Criar a sequência de tarefas anunciado utilizando o modelo de sequência de tarefas de sequência de tarefas de instalação de modo<br /><br /> -Inicie a sequência de tarefas no Windows PE utilizando o arranque PXE, suportes de dados de arranque de sequência de tarefas ou suportes de dados para o NEWCOMPUTER. Fase pré-configurado.<br /><br /> Esta parte do cenário pode ser utilizada com as implementações tradicionais ou com as implementações de suportes de dados como suportado no Configuration Manager. Como parte desta parte do cenário, os dados de migração de estado do utilizador são restaurados. O Assistente de UDI é executado com as seguintes fases UDI para suportar cada tipo de implementação:<br /><br /> -                          **Fase NEWCOMPUTER.** O Assistente de UDI é executado com esta fase no **sequência de tarefas de instalação de modo** sequência de tarefas, quando a imagem do sistema operativo é armazenada nos pontos de distribuição. Para obter mais informações, consulte [NEWCOMPUTER fase](#NEWCOMPUTERStage).<br /><br /> -                          **NEWCOMPUTER. Fase de pré-configuração.** O Assistente de UDI é executado com esta fase no **sequência de tarefas de instalação de modo** sequência de tarefas, quando a imagem do sistema operativo é armazenada num disco local no computador de destino (pré-configurados). Para obter mais informações, consulte [NEWCOMPUTER. Fase de pré-configurado](#NEWCOMPUTERPrestagedStage).|  

#####  <a name="NEWCOMPUTERStage"></a>Fase NEWCOMPUTER  
 Figura 1 ilustra a utilização da fase NEWCOMPUTER numa sequência de tarefas criada utilizando o utilizador\-modelo de sequência de tarefas condicionadas sequência de tarefas de instalação. A principal diferença entre as sequências de tarefas chamar a fase NEWCOMPUTER e o NEWCOMPUTER. Fase de pré-configurado que está a chamar o NEWCOMPUTER de sequência de tarefas. Fase pré-configurado não é executado o **aplicar imagem do sistema operativo** passo de sequência de tarefas porque a imagem do sistema operativo já está localizada no computador de destino.  

 ![Referência de UDI 1](media/UDIReference1.jpg)  

 **Figura SEQ Figure \\ \* ARABIC 1. Fluxo de processo para a fase NEWCOMPUTER**  

#####  <a name="NEWCOMPUTERPrestagedStage"></a>NEWCOMPUTER. Fase pré-configurado  
 Figura 2 ilustra o elevado\-fluxo de nível de processo para o NEWCOMPUTER. Pré-configurado fase numa sequência de tarefas criada utilizando o utilizador\-modelo de sequência de tarefas condicionadas sequência de tarefas de instalação. A principal diferença entre as sequências de tarefas chamar a fase NEWCOMPUTER e o NEWCOMPUTER. Fase de pré-configurado que está a chamar o NEWCOMPUTER de sequência de tarefas. Fase pré-configurado não é executado o **aplicar imagem do sistema operativo** passo de sequência de tarefas porque a imagem do sistema operativo já está localizada no computador de destino.  

 ![Referência de UDI 2](media/UDIReference2.jpg)  

 **Figura 2. Fluxo de processos para o NEWCOMPUTER. Fase pré-configurado**  

####  <a name="REFRESHStage"></a>Fase de ATUALIZAÇÃO  
 Figura 3 ilustra a alta\-fluxo de nível de processo para a fase de ATUALIZAÇÃO numa sequência de tarefas criada utilizando o utilizador\-modelo de sequência de tarefas condicionadas sequência de tarefas de instalação.  

 ![Referência de UDI 3](media/UDIReference3.jpg)  

 **Figura SEQ Figure \\ \* ARABIC 3. Fluxo de processo para a fase de ATUALIZAÇÃO**  

####  <a name="REPLACEandREPLACEWinPEStages"></a>SUBSTITUIR e a substituir. Fases do WinPE  
 A figura 4 ilustra o elevado\-fluxo de nível de processo para a substituir e a substituir. Fases de WinPE numa sequência de tarefas criada utilizando o utilizador\-modelo de sequência de tarefas condicionadas instalação substituir sequência de tarefas.  

 ![Referência de UDI 4](media/UDIReference4.jpg)  

 **Figura 4. Fluxo de processo para a substituir e a substituir. Fases do WinPE**  

###  <a name="UDITaskReference"></a>Referência da tarefa de UDI  
 *Tarefas UDI* software que é executado numa página do assistente que efetuam funções específicas. Em alguns casos, estas tarefas são utilizadas para verificar se o computador de destino está pronto para a implementação. Outras tarefas podem ser utilizadas para efetuar os passos de implementação, tais como copiar ficheiros de configuração ou o resultado.  

> [!NOTE]
>  O **seguinte** botão na página do assistente, em que as tarefas são executadas será desativado se qualquer uma das tarefas concluída com aviso ou erro de estado de conclusão.  

 Esta referência inclui:  

-   Uma descrição geral de UDI tarefas, conforme descrito em [UDI descrição geral de tarefas](#UDITaskOverview)  

-   Uma descrição das definições de configuração de UDI tarefas, conforme descrito em [UDI definições de configuração de tarefas](#UDITaskConfigurationSettings)  

-   Uma descrição da incorporado\-no validações UDI que são fornecidas com o MDT, conforme descrito em [incorporado\-em tarefas de UDI](#BuiltinUDITasks)  

####  <a name="UDITaskOverview"></a>Descrição geral de tarefas UDI  
 Tarefas UDI permitem a execução de software no computador de destino que ajuda-o com o processo de implementação. UDI inclui várias incorporada\-em tarefas que o ajudam a realizar tarefas comuns, tais como de se certificar de que o computador de destino não está em execução uma bateria e está ligado a uma ligação de rede com fios.  

 Para além de incorporado\-em tarefas UDI, pode criar tarefas UDI personalizadas utilizando o kit de desenvolvimento de software UDI \(SDK\). Para obter mais informações sobre a criação de tarefas UDI personalizadas utilizando o SDK de UDI, consulte *utilizador\-orientadas por guia para programadores do instalação*.  

####  <a name="UDITaskConfigurationSettings"></a>Definições de configuração de tarefas UDI  
 Gerir tarefas, utilizando o UDI Wizard Designer. Pode adicionar tarefas, remover tarefas e editar a configuração de uma tarefa no UDI Wizard Designer. As definições de configuração para uma tarefa são armazenadas no ficheiro de configuração do Assistente de UDI e são lidos pelo Assistente de UDI quando for apresentada a página do assistente que contém a tarefa.  

 Tarefas UTI tem algumas definições de configuração que são comuns a todas as tarefas UDI, tal como indicado na tabela 13. Para as definições de configuração que são específicas para cada tarefa UDI, consulte a secção correspondente no [incorporado\-em tarefas de UDI](#BuiltinUDITasks).  

### <a name="table-13-configuration-settings-common-to-all-udi-tasks"></a>Tabela 13. Definições de configuração comum para todas as tarefas UDI  

|**Tarefa**|**Descrição**|  
|-|-|  
|**Nome de ficheiro de mapa de bits**|Este parâmetro especifica o gráfico utilizado para indicar o tipo de tarefa.|  
|**Nome a apresentar**|Esta ação Especifica o nome da tarefa, que é apresentado na página do assistente, quando a tarefa for executada.|  
|**Valores de código de saída**|Esta ação Especifica uma lista de possíveis códigos de retorno para a tarefa. Existe um item na lista para cada código de retorno possíveis.|  
|**Valores de código de erro**|Esta ação Especifica uma lista de exceções inesperadas possíveis que pode ser encontrado \(emitida\) pela tarefa. Existe um item na lista para cada exceção possíveis.|  

####  <a name="BuiltinUDITasks"></a>Incorporado\-em tarefas UDI  
 Tabela 14 apresenta uma lista de incorporado\-em tarefas UDI. Cada incorporada\-no UDI tarefa é abordada numa secção subsequente.  

### <a name="table-14-built-in-udi-tasks"></a>Tabela 14. Incorporado\-em tarefas UDI  

|**Tarefa**|**Descrição**|  
|-|-|  
|[Verificação de energia de AC](#ACPowerCheck)|Esta tarefa UDI é utilizada para identificar se o computador de destino está ligado à potência de AC, não apenas com bateria.|  
|[Deteção de aplicação](#ApplicationDiscovery)|Esta tarefa UDI é utilizada para detetar aplicações que estão instaladas no computador de destino.|  
|[CheckSMSFolderOnUSB](#CheckSMSFolderOnUSB)|Esta tarefa UDI é utilizada para determinar se o \_SMSTaskSequence pasta está localizada numa unidade USB no computador de destino.|  
|[Tarefas de ficheiros de cópia](#CopyFilesTask)|Esta tarefa UDI é utilizada para copiar ficheiros enquanto o Assistente de UDI está em execução no computador de destino.|  
|[Shell de execução da tarefa](#ShellExecuteTask)|Esta tarefa UDI é utilizada para executar o software que pode ser iniciado a partir de uma linha de comandos.|  
|[Verificação de rede com fios](#WiredNetworkCheck)|Esta tarefa UDI é utilizada para identificar se o computador de destino está ligado a uma rede com fios, não ligada através de uma ligação de rede sem fios.|  

#####  <a name="ACPowerCheck"></a>Verificação de energia de AC  
 Utilize esta tarefa UDI para identificar se o computador de destino está ligado à potência de AC. Esta tarefa utiliza apenas esses parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 Tabela 15 apresenta o erro e códigos de saída que o **AC energia verifique** gera de tarefas.  

### <a name="table-15-error-and-exit-codes-for-the-ac-power-check-task"></a>Tabela 15. Tarefa de verificação de erro e códigos de saída para a potência de AC  

|**Código de saída ou de erro**|**Valor**|**Estado**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que o computador de destino está ligado à power de AC|  
|Saída|**\***|**Erro**, que indica que o computador de destino não está ligado à power de AC|  

#####  <a name="ApplicationDiscovery"></a>Deteção de aplicação  
 Utilize esta tarefa UDI para detetar aplicações que estão instaladas no computador de destino.  

 Tabela 16 lista os parâmetros que o **deteção de aplicação** utiliza de tarefas.  

### <a name="table-16-parameters-used-by-the-application-discovery-task"></a>Tabela 16. Parâmetros utilizados pela tarefa de deteção de aplicação  

|**Tarefa**|**Descrição**|  
|-|-|  
|**Readcfg**|Este parâmetro especifica o caminho completamente qualificado ou relativo para a localização do ficheiro. App que tem uma lista de aplicações para a tarefa de deteção. O ficheiro. App contém a lista de itens de software disponíveis onde o utilizador pode seleccionar.<br /><br /> O **deteção de aplicação** tarefas lê o ficheiro. App e determina se qualquer um destes itens de software está instalado. Se um item de software é instalado, o item foi adicionado ao ficheiro especificado no **Writecfg** parâmetro.<br /><br /> Certifique-se de que este parâmetro utiliza o mesmo nome de ficheiro e a localização que o [ApplicationPage](#ApplicationPage) página do assistente.|  
|**Writecfg**|Este parâmetro especifica o caminho completamente qualificado ou relativo para a localização do ficheiro. XML que contém uma lista das aplicações detetados pela tarefa.|  
|**Registo**|Este parâmetro especifica o caminho completamente qualificado ou relativo para a localização do ficheiro de registo gerado por esta tarefa. O nome de ficheiro do ficheiro de registo é AppDiscovery.log.|  

 Para além dos parâmetros na tabela 16, esta tarefa utiliza os parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros comuns, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 Tabela 17 apresenta o erro e códigos de saída que o **deteção de aplicação** gera de tarefas.  

### <a name="table-17-error-and-exit-codes-for-the-application-discovery-task"></a>Tabela 17. Erro e códigos de saída para a tarefa de deteção de aplicação  

|**Código de saída ou de erro**|**Valor**|**Estado e a descrição**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que a tarefa foi analisado com êxito para aplicações|  
|Saída|**\***|**Aviso**, que indica que o motor de deteção de aplicação não foi possível executar por algum motivo desconhecido|  
|Saída|**1**|**Aviso**, que indica que o motor de deteção de aplicação encontrou um ou mais avisos|  
|Saída|**16777216**|**Aviso**, que indica que foram encontrados problemas críticos ao inicializar o motor de deteção de aplicação|  
|Saída|**33554432**|**Aviso**, que indica que foram encontrados problemas críticos ao processar a lista de principal da aplicação|  

#####  <a name="CheckSMSFolderOnUSB"></a>CheckSMSFolderOnUSB  
 Utilize esta tarefa UDI para identificar se o \_SMSTaskSequence pasta está localizada numa unidade USB no computador de destino. Por predefinição, o sequenciador de tarefas do Configuration Manager coloca o \_SMSTaskSequence pasta na unidade com o mais espaço livre em disco. Isto pode causar problemas mais tarde no processo de implementação se a unidade USB é removida.  

 Esta tarefa verifica se a pasta está localizada numa unidade USB e impede a implementação de continuar, se for. Esta tarefa utiliza apenas esses parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 Se o \_SMSTaskSequence pasta está localizada numa unidade USB, esta tarefa falha e impede a implementação de continuar. Para resolver este problema e efetuar a implementação, execute os seguintes passos:  

1.  Desligar a unidade USB do computador de destino antes de iniciar a sequência de tarefas.  

2.  Inicie a sequência de tarefas.  

3.  Aguarde até que o Assistente de UDI é iniciado.  

4.  Ligue a unidade USB.  

5.  Conclua o assistente UDI.  

 Tabela 18 apresenta o erro e códigos de saída que o **CheckSMSFolderOnUSB** gera de tarefas.  

### <a name="table-18-error-and-exit-codes-for-the-checksmsfolderonusb-task"></a>Tabela 18. Erro e códigos de saída da tarefa CheckSMSFolderOnUSB  

|**Código de saída ou de erro**|**Valor**|**Estado**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que o \_SMSTaskSequence pasta não está localizada numa unidade USB e pode continuar a implementação.|  
|Saída|**\***|**Erro**, que indica que o \_SMSTaskSequence pasta está localizada numa unidade USB e não pode continuar a implementação.|  

#####  <a name="CopyFilesTask"></a>Tarefas de ficheiros de cópia  
 Utilize esta tarefa UDI para copiar ficheiros enquanto o Assistente de UDI está em execução no computador de destino.  

 Tabela 19 lista os parâmetros que o **ficheiros de cópia** utiliza de tarefas.  

### <a name="table-19-parameters-used-by-the-copy-files-task"></a>Tabela 19. Parâmetros utilizados pela tarefa de ficheiros de cópia  

|**Tarefa**|**Descrição**|  
|-|-|  
|**Origem**|Este parâmetro especifica o caminho completamente qualificado ou relativo para o ficheiro de origem, o que pode conter carateres universais para copiar ficheiros vários com uma única tarefa.|  
|**Destino**|Este parâmetro especifica o caminho completamente qualificado ou relativo para o ficheiro de destino sem um nome de ficheiro.|  

 Para além dos parâmetros na tabela 19, esta tarefa utiliza os parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 A tabela 20 apresenta o erro e códigos de saída que o **ficheiros de cópia** gera de tarefas.  

### <a name="table-20-error-and-exit-codes-for-the-copy-files-task"></a>A tabela 20. Erro e códigos de saída para a tarefa de ficheiros de cópia  

|**Código de saída ou de erro**|**Valor**|**Estado e a descrição**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que o processo de cópia com êxito|  
|Saída|**\***|**Erro**, que indica que o processo de cópia falhou|  
|Erro|**\-1**|**Erro**, que indica que o processo de cópia falhou|  

#####  <a name="ShellExecuteTask"></a>Shell de execução da tarefa  
 Utilize esta tarefa UDI para executar o software que pode ser iniciado a partir de uma linha de comandos.  

 Tabela 21 lista os parâmetros que o **Shell executar** utiliza de tarefas.  

### <a name="table-21-parameters-used-by-the-shell-execute-task"></a>Tabela 21. Parâmetros utilizados pela tarefa de execução de Shell  

|**Tarefa**|**Descrição**|  
|-|-|  
|**Nome de ficheiro**|Este parâmetro especifica o caminho completamente qualificado ou relativo para o comando para a tarefa ser executada.|  
|**Parâmetros**|Este parâmetro especifica o comando\-parâmetros que estão a ser fornecido quando executar o comando de linha.|  

 Para além dos parâmetros na tabela 21, esta tarefa utiliza os parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 Também pode executar scripts personalizados do Visual Basic concebidos para serem executados no cscript.exe utilizando o **Shell executar** tarefas. Para executar scripts de Visual Basic, execute os seguintes passos:  

1.  Escreva o seguinte texto no **Filename** parâmetro:  

    ```  
    %windir%\system32\cscript.exe  
    ```  

2.  Nome de tipo de ficheiro de script do Visual Basic \(vbs ficheiro\) no **parâmetros** parâmetro, incluindo quaisquer comandos\-parâmetros para o script de linha.  

     Por exemplo executar um script do Visual Basic chamada *SelfTest.vbs* com um valor de parâmetro de **depurar**, escreva o seguinte \(onde *script\_caminho*é o caminho completamente qualificado para o ficheiro SelfTest.vbs\):  

    ```  
    <script_path>\SelfTest.vbs Debug  
    ```  

 Tabela 22 apresenta o erro comuns e os códigos de saída que o **Shell executar** gera de tarefas.  

> [!NOTE]
>  Cada tarefa específica com base no **Shell executar** tarefa tem um conjunto exclusivo de códigos de erro e de saída. Verifique os códigos de retorno para o software que está a executar esta tarefa a utilizar.  

### <a name="table-22-common-error-and-exit-codes-for-the-shell-execute-task"></a>Tabela 22. Erro comuns e códigos de saída para a tarefa de execução da Shell  

|**Código de saída ou de erro**|**Valor**|**Estado e a descrição**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que a tarefa foi concluído com êxito|  
|Saída|**\***|**Erro**, que indica que a tarefa falhou|  

#####  <a name="WiredNetworkCheck"></a>Verificação de rede com fios  
 Utilize esta tarefa UDI para determinar se o computador de destino está ligado a uma rede com fios, não a utilizar uma ligação de rede sem fios. Esta tarefa utiliza apenas os parâmetros comuns a todas as tarefas UDI. Para obter mais informações sobre estes parâmetros, consulte [definições de configuração de tarefas de UDI](#UDITaskConfigurationSettings).  

 Tabela 23 apresenta o erro comuns e os códigos de saída que o **verifique de rede com fios** gera de tarefas.  

### <a name="table-23-error-and-exit-codes-for-the-wired-network-check-task"></a>Tabela 23. Tarefa de verificação de erro e códigos de saída para a rede com fios  

|**Código de saída ou de erro**|**Valor**|**Estado e a descrição**|  
|-|-|-|  
|Saída|**0**|**Êxito**, que indica que o computador de destino está ligado a uma rede com fios|  
|Saída|**\***|**Erro**, que indica que o computador de destino não está ligado a uma rede com fios|  

###  <a name="UDIValidatorReference"></a>Referência de validação UDI  
 Validações UDI são utilizadas para validar os valores introduzidos nos campos de texto nas páginas do assistente. Quando um validador UDI Deteta uma entrada inválida, é apresentada uma mensagem para o primeiro erro encontrado na parte inferior da página do assistente. A seguinte mensagem de erro de validação, se existir, é apresentada depois de resolver o primeiro erro de validação. Este processo continua até que todos os erros de validação são resolvidos. O **seguinte** botão está desativado até que todos os erros de validação na página do assistente sejam resolvidos.  

 Esta referência inclui:  

-   Uma descrição geral dos validadores UDI, conforme descrito em [descrição geral de validação de UDI](#UDIValidatorOverview)  

-   Uma descrição da incorporado\-no validações UDI fornecidas com o MDT, conforme descrito em [incorporado\-no UDI validações](#BuiltinUDIValidators)  

####  <a name="UDIValidatorOverview"></a>Descrição geral de validação UDI  
 Validações UDI são utilizadas para ajudar a garantir que os utilizadores forneçam as informações corretas nos campos de texto nas páginas do assistente no Assistente de UDI. UDI inclui várias incorporada\-no validações que ajuda a realizar validações típicas de campos utilizados para introdução de texto, tais como impedir os utilizadores a introduzir carateres inválidos ou garantir que o campo está não vazio.  

 Para além de incorporado\-validações UDI, pode criar validações UDI personalizadas utilizando o SDK de UDI. Para obter mais informações sobre a criação personalizadas validações UDI utilizando o SDK de UDI, consulte o documento de MDT *utilizador\-orientadas por guia para programadores do instalação*.  

####  <a name="BuiltinUDIValidators"></a>Validações UDI incorporadas  
 Tabela 24 lista validações UDI incorporadas. Cada validador incorporado é abordada numa secção subsequente. Quando um validador Deteta uma entrada inválida numa caixa de texto, será apresentada uma mensagem na página do assistente e o **seguinte** botão está desativado até que todas as entradas inválidas sejam resolvidas.  

### <a name="table-24-built-in-udi-validators"></a>Tabela 24. Validações UDI incorporadas  

|**A validação do**|**Descrição**|  
|-|-|  
|[InvalidChars](#InvalidChars)|Este validador identifica quaisquer carateres inválidos que tenham sido introduzidos a partir de uma lista que configurar.|  
|[NamedPattern](#NamedPattern)|Este validador ajuda Certifique-se de que o texto segue um padrão predefinido.|  
|[NonEmpty](#NonEmpty)|Este validador é utilizado para exigir um campo de texto.|  
|[RegEx](#RegEx)|Este validador permite, certifique-se de que o texto corresponde a uma expressão regular que especificar como parte do validador.|  

#####  <a name="InvalidChars"></a>InvalidChars  
 Este validador impede que os utilizadores a introduzir carateres específicas. O **mensagem** caixa permite-lhe introduzir uma mensagem que é apresentada se o campo de texto contiver qualquer um dos carateres inválidos. O **carateres inválidos** caixa permite-lhe introduzir os carateres que são considerados inválidos. Os carateres são introduzidos sem espaços entre eles.  

#####  <a name="NamedPattern"></a>NamedPattern  
 Este validador ajuda Certifique-se de que o texto segue um padrão predefinido. O **mensagem** caixa permite-lhe introduzir uma mensagem que é apresentada se o campo de texto não corresponde ao padrão com nome. O **denominado padrão** caixa permite-lhe introduzir o nome do padrão predefinido e tem de ser **Username**, **ComputerName**, ou **Workgroup**.  Os nomes são sensível a maiúsculas e minúsculas.  

#####  <a name="NonEmpty"></a>NonEmpty  
 Utilize este validador para requerer um campo de texto. O **mensagem** caixa permite-lhe introduzir uma mensagem que é apresentada se o campo de texto está vazio.  

#####  <a name="RegEx"></a>RegEx  
 Este validador permite, certifique-se de que o texto corresponde a uma expressão regular que especificar como parte do validador. O **mensagem** caixa permite-lhe introduzir uma mensagem que é apresentada se o campo de texto não corresponde à expressão regular. O **expressão Regular** caixa permite-lhe introduzir a expressão regular utilizada para a validação. Para obter mais informações sobre como criar expressões regulares para esta validação, consulte [expressões regulares TR1](http://msdn.microsoft.com/library/bb982727.aspx).  

###  <a name="UDIWizardPageReference"></a>Referência de página do assistente UDI  
 Adicionar um UDI [página do assistente](#WizardPage) para fases do [página biblioteca](#PageLibrary) no [UDI Wizard Designer](#UDIWizardDesigner). Páginas de assistente UDI são apresentadas no [Assistente de UDI](#UDIWizard).  

 Esta referência inclui:  

-   Uma descrição geral das páginas de assistente UDI, conforme descrito em [descrição geral de página do Assistente de UDI](#UDIWizardPageOverview)  

-   Uma descrição das páginas de assistente UDI incorporadas que são fornecidos com o MDT, conforme descrito em [páginas do Assistente de UDI incorporadas](#BuiltinUDIWizardPages)  

####  <a name="UDIWizardPageOverview"></a>Descrição geral de página do assistente UDI  
 Páginas do assistente são apresentadas no [Assistente de UDI](#UDIWizard) e recolher as informações necessárias para concluir o processo de implementação. Criar páginas de assistente utilizando C++ no Visual Studio. As páginas do assistente personalizados são implementadas como dll, que lê o Assistente de UDI.  

 Cada página do assistente UDI incorporada tem um UDI correspondente [editor de página do assistente](#WizardPageEditor), que utiliza para configurar a página do assistente no [UDI Wizard Designer](#UDIWizardDesigner).  

 Para além das páginas de assistente UDI incorporadas, pode criar páginas do assistente UDI personalizadas utilizando o SDK de UDI. Para obter mais informações sobre como criar páginas do assistente UDI personalizadas utilizando o SDK de UDI, consulte o documento de MDT *guia para programadores do modo instalação*.  

 Cada página do assistente, pode referenciar os seguintes tipos de variáveis:  

-   Variáveis de sequência de tarefas  

-   Variáveis de memória  

-   Variáveis de ambiente  

 Pode referenciar sequência de tarefas e as variáveis de ambiente através da utilização de parênteses em variável utilizando sinais de percentagem (%), tal como *% OSDImageIndex %.* Pode referenciar variáveis de memória através da utilização de parênteses em variável utilizando cifrões ($), tal como *$VolumeArchitecture$.*  

> [!NOTE]
>  Se uma variável de sequência de tarefas e uma variável de ambiente têm o mesmo nome, em seguida, a variável de sequência de tarefas tem precedência sobre a variável de ambiente.  

 Tabela 25 lista as variáveis de memória que são definidas quando é iniciado o Assistente de UDI, a descrição das variáveis, e se o Assistente de UDI leituras ou escritas as variáveis durante o arranque.  

### <a name="table-25-memory-variables-set-by-the-udi-wizard-at-startup-and-their-descriptions"></a>Tabela 25. Variáveis de memória definidas pelo Assistente de UDI no arranque e as respetivas descrições  

|**Variável**|**Leitura**|**Escrita**|  
|-|-|-|  
|**LogPath**<br /><br /> Especifica o caminho completamente qualificado para os ficheiros de registo para que o Assistente de UDI. Pode definir esta variável para um dos seguintes valores:<br /><br /> -O valor de **smstslogpath** variável de sequência de tarefas<br /><br /> -O valor de % TEMP % ambiente variável se o **smstslogpath** variável de sequência de tarefas não está definido|Não|Sim|  
|**WizardConfigFilename**<br /><br /> Especifica o nome do ficheiro de configuração do Assistente de UDI atualmente em utilização. O **ApplicationPage** página do assistente lê o valor desta variável como localizar o ficheiro. App correspondente, que contém a lista de aplicações. Por exemplo, se o ficheiro de configuração do Assistente de UDI é denominado *config.xml,* , em seguida, a página do assistente irá procurar o ficheiro. App correspondente (config.xml.app).|Não|Sim|  

####  <a name="BuiltinUDIWizardPages"></a>Páginas de assistente UDI incorporadas  
 26 tabela lista as páginas do assistente UDI incorporadas. Cada página do assistente UDI incorporada é abordada numa secção subsequente.  

### <a name="table-26-built-in-wizard-pages-and-their-descriptions"></a>26 de tabela. Páginas do assistente incorporados e as respetivas descrições  

|**Página do Assistente**|**Descrição**|  
|-|-|  
|[AdminAccounts](#AdminAccounts)|Utilize esta página do Assistente para definir a palavra-passe da conta de administrador local e adicionar outros utilizadores ao grupo de administradores local no computador de destino.|  
|[ApplicationPage](#ApplicationPage)|Utilize esta página do Assistente para configurar a lista de aplicações que pode ser instalado durante o processo de configuração. Estas aplicações podem incluir aplicações ou pacotes e programas do Configuration Manager.|  
|[BitLockerPage](#BitLockerPage)|Utilize esta página do Assistente para configurar as definições do BitLocker para o computador de destino.|  
|[ComputerPage](#ComputerPage)|Utilize esta página do Assistente para configurar o nome do computador de destino, o domínio ou grupo de trabalho e a credencial a ser utilizado quando a associação a um domínio.|  
|[ConfigScanPage](#ConfigScanPage)|Utilize esta página do Assistente para executar tarefas de UDI analisar a configuração do computador de destino para determinar se o computador de destino está pronto para a implementação da imagem do sistema operativo. Esta preparação inclui ter recursos de sistema suficientes e garantir que os pré-requisitos de software está instalado e configurado corretamente.|  
|[LanguagePage](#LanguagePage)|Utilize esta página do Assistente para determinar que pacote de idiomas deve ser instalado, o idioma predefinido para o sistema operativo de destino, a região de teclado e o fuso horário em que o computador será fisicamente localizado.|  
|[ProgressPage](#ProgressPage)|Utilize esta página do Assistente para executar tarefas de UDI capturar os dados de migração de estado de utilizador do computador de destino.|  
|[RebootPage](#RebootPage)|Utilize esta página do Assistente para notificar o utilizador que o computador de destino será reiniciado. Pode configurar a mensagem de notificação com o UDI Wizard Designer.|  
|[SummaryPage](#RebootPage)|Utilize esta página do Assistente para notificar o utilizador sobre as opções de configuração que foram selecionados ao executar o Assistente de UDI. As informações de configuração apresentadas nesta página do assistente automaticamente são recolhidas a partir de outras páginas do assistente. Alguns campos nas outras páginas de assistente permitem-lhe configurar a legenda (etiqueta) apresentada nesta página do assistente com o UDI Wizard Designer.|  
|[UDAPage](#UDAPage)|Utilize esta página do Assistente para configurar o UDA entre o computador de destino e um utilizador especificado. Definir a afinidade entre um computador e um utilizador permite a instalação automática de software que é implementado num utilizador. A funcionalidade UDA só está disponível no Configuration Manager e o cenário de UDI novo computador.|  
|[UserStatePage](#UserStatePage)|Utilize esta página do Assistente para configurar as definições para capturar ou restaurar os dados de migração de estado do utilizador. Página do assistente permite ao utilizador selecionar a localização para capturar a migração de estado do utilizador para ou restaurar dados de migração de estado de utilizador.|  
|[VolumePage](#VolumePage)|Utilize esta página do Assistente para configurar as definições para o volume de disco no computador de destino em que o sistema operativo será implementado. Estas definições incluem a seleção do sistema operativo de destino, selecionar a unidade de destino, selecionar qualquer instalação do Windows e determinar se a unidade de destino deve ser formatada como parte do processo de implementação.|  
|[WelcomePage](#WelcomePage)|Utilize esta página do Assistente para fornecer informações para o utilizador sobre o Assistente de UDI e o processo de implementação. Pode configurar a mensagem de notificação com o UDI Wizard Designer.|  

#####  <a name="AdminAccounts"></a>AdminAccounts  
 Utilize esta página do Assistente para definir a palavra-passe da conta de administrador local e para adicionar outro utilizador ao grupo de administradores local no computador de destino.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 27 o **AdminAccounts** com a descrição, as variáveis de sequência de tarefas e determina se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI.  

### <a name="table-27-adminaccounts-task-sequence-variables"></a>27 de tabela. Variáveis de sequência de tarefas AdminAccounts  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**OSDAddAdmin**<br /><br /> Especifica uma lista de nomes de utilizador adicional seja adicionado ao grupo local de administradores no computador de destino.|Sim|Sim|Sim|  
|**OSDLocalAdminPassword**<br /><br /> Especifica as palavras-passe para a conta de administrador local incorporada no computador de destino.|Sim|Sim|Sim|  

#####  <a name="ApplicationPage"></a>ApplicationPage  
 Utilize esta página do Assistente para configurar a lista de software da aplicação que pode ser instalado durante o processo de configuração. Estas aplicações podem incluir aplicações ou pacotes e programas do Configuration Manager.  

> [!NOTE]
>  Se as aplicações são apresentadas seja desativado, a aplicação poderá exigir a aprovação do administrador, mas ainda não tiver sido aprovada. Se o **exigir aprovação do administrador caso os utilizadores solicitem esta aplicação** caixa de verificação está selecionada para a aplicação, certifique-se de que a aplicação tiver sido aprovada. Para obter mais informações, consulte [como implementar aplicações no Configuration Manager](http://technet.microsoft.com/library/gg682082.aspx).  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 28 a **ApplicationPage** com a descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-28-applicationpage-task-sequence-variables"></a>28 de tabela. Variáveis de sequência de tarefas ApplicationPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**ApplicationBaseVariable**<br /><br /> Especifica o nome utilizado como base para os nomes variável de sequência de tarefas criados para cada aplicação do Configuration Manager selecionada no **ApplicationPage** página do assistente. Esta variável é configurada utilizando o **editar definições de Software** clique no botão no **editar definições de** grupo no Friso do UDI Wizard Designer.<br /><br /> É criada uma variável de sequência de tarefas separadas para cada aplicação seleccionada nesta página. O valor predefinido para esta variável é **aplicações**. Por isso, por exemplo, os nomes predefinidos da tarefa de variáveis de sequência criadas para cada aplicação seleccionada nesta página será *APPLICATIONS001, APPLICATIONS002, APPLICATIONS003,* , etc.|Não|Sim|Sim|  
|**OSDApplicationList**<br /><br /> Especifica a lista de identificadores de aplicações que deve ser inicialmente selecionada. A variável contém uma lista de valores numéricos, separados por ponto e vírgula (;).<br /><br /> Os identificadores de aplicação encontram-se no **Id** atributo o **aplicação** elemento no ficheiro de configuração de aplicação do Assistente de UDI (UDIWizard_Config.xml.app). Há um separado **aplicação** elemento para cada aplicação apresentado na página do assistente.|Sim|Não|Não|  
|**OSDArchitecture**<br /><br /> Especifica a arquitetura de processador do computador de destino. O **ApplicationPage** página do assistente utiliza esta variável para filtrar as aplicações disponíveis quando o **VolumeArchitecture** variável de memória não foi definido. No entanto, se o **VolumeArchitecture** variável de memória foi definido, que demora sempre precedência sobre esta variável de sequência de tarefas para filtrar as aplicações disponíveis.<br /><br /> O valor desta variável pode ser:<br /><br /> -                                      **x86**, que indica uma arquitetura de processador de 32 bits<br /><br /> -                                      **AMD64**, que indica uma arquitetura de processador de 64 bits|Sim|Não|Não|  
|**OSDBaseVariableName**<br /><br /> Especifica o nome utilizado como base para os nomes de variáveis de sequência de tarefas criados para cada pacote de Configuration Manager e o programa selecionado no **ApplicationPage** página do assistente. Esta variável é configurada utilizando o **editar definições de Software** clique no botão no **página comportamento** grupo no Friso do UDI Wizard Designer.<br /><br /> É criada uma variável de sequência de tarefas separadas para cada aplicação seleccionada nesta página. O valor predefinido para esta variável é **PACOTES**. Por isso, por exemplo, os nomes predefinidos da tarefa de variáveis de sequência criadas para cada aplicação seleccionada nesta página será *PACKAGES001, PACKAGES002, PACKAGES003,* , etc.|Não|Sim|Sim|  

##### <a name="memory-variables"></a>Variáveis de memória  
 Apresenta uma lista de 29 de tabela a **ApplicationPage** variáveis de memória com a descrição e se a variável de leitura ou escrita por página do assistente.  

### <a name="table-29-applicationpage-memory-variables"></a>29 de tabela. Memória ApplicationPage variáveis  

|**Variável**|**Leitura**|**Escrita**|  
|-|-|-|  
|**VolumeArchitecture**<br /><br /> Especifica a arquitetura de processador de imagem do sistema operativo de destino para ser implementado (se a imagem contém um sistema operativo de 32 bits ou 64 bits). Quando esta página é apresentada, verifica para ver se esta variável foi alterada. Se a variável foi alterada desde a última vez que foi apresentada a página do assistente, a página do assistente filtra os programas disponíveis para seleção com base na arquitetura do sistema operativo de destino. Por exemplo, é possível implementar um sistema operativo de 32 bits, em seguida, a página do assistente remove (filtros) todas as aplicações de 64 bits da lista de aplicações disponíveis na página do assistente.|Sim|Não|  
|**WizardConfigFilename**<br /><br /> Especifica o nome do ficheiro de configuração do Assistente de UDI atualmente em utilização. Se o valor da **Link.Uri** propriedade setter está vazia, o **ApplicationPage** página do assistente lê o valor desta variável como localizar o ficheiro. App correspondente, que contém a lista de aplicações. Por exemplo, se o ficheiro de configuração do Assistente de UDI é denominado *config.xml,* , em seguida, a página do assistente irá procurar o ficheiro. App correspondente (config.xml.app). Esta variável é definida quando o Assistente de UDI é iniciado.<br /><br /> O **Link.Uri** setter de propriedade é definido a **definições de Software** caixa de diálogo, que pode ser aberta utilizando o **editar definições de Software** clique no botão no **página Comportamento** grupo no Friso do UDI Wizard Designer.|Sim|Não|  

#####  <a name="BitLockerPage"></a>BitLockerPage  
 Página do assistente é utilizada para configurar definições do BitLocker para o computador de destino.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 30 tabela lista as variáveis de sequência de tarefas BitLockerPage com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI.  

### <a name="table-30-bitlockerpage-task-sequence-variables"></a>30 de tabela. Variáveis de sequência de tarefas BitLockerPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**BDEInstallSuppress**<br /><br /> Especifica se a instalação do BitLocker deve ser suprimida. Se a variável é definida como:<br /><br /> - **Sim**, em seguida, a **ativar BitLocker** caixa de verificação está selecionada e a instalação é executada<br /><br /> - **NÃO**, em seguida, a **ativar BitLocker** caixa de verificação está desmarcada e não é efetuada a instalação|Sim|Sim|Sim|  
|**BDEKeyLocation**<br /><br /> Especifica o caminho completamente qualificado para a localização onde estão armazenadas as chaves de encriptação do BitLocker, que pode ser uma localização ou caminho UNC. Esta variável é definida para o valor da **KeyLocation** valor setter no ficheiro de configuração do Assistente de UDI o **BitLockerPage**. Esta variável é apenas considerada válido quando o **OSDBitLockerMode** está definido como **TPMKEY** ou **chave**.|Não|Sim|Não|  
|**BDEPin**<br /><br /> Especifica o valor de PIN do BitLocker, se o **ativar BitLocker utilizando o TPM e Pin** opção está selecionada.|Sim|Sim|Sim|  
|**OSDBitLockerCreateRecoveryPassword**<br /><br /> Especifica se uma palavra-passe de recuperação do BitLocker deve ser armazenada no AD DS. Se a variável é definida como:<br /><br /> -                                      **AD**, em seguida, a **no Active Directory** opção está selecionada e as chaves de recuperação serão armazenadas no AD DS (recomendado)<br /><br /> - **NENHUM**, em seguida, a **não criar uma chave de recuperação** opção está selecionada e as chaves de recuperação não serão armazenadas no AD DS (não recomendado)|Não|Sim|Não|  
|**OSDBitLockerMode**<br /><br /> Especifica o modo a ser utilizado quando ativar o BitLocker no computador de destino. Os valores válidos incluem:<br /><br /> -                                      **TPM.** Este valor indica que o **ativar o BitLocker com só TPM** opção está selecionada e esse TPM só será utilizado ao ativar o BitLocker no computador de destino.<br /><br /> -                                      **TPMPIN.** Este valor indica que o **ativar BitLocker utilizando o TPM e Pin** opção está selecionada e esse TPM e um PIN de utilizador especificado serão utilizado ao ativar o BitLocker no computador de destino.<br /><br /> -                                      **TPMKEY.** Este valor indica que o **ativar BitLocker utilizando o TPM e chave de arranque** opção está selecionada e esse TPM e uma chave de arranque serão utilizadas quando ativar o BitLocker no computador de destino.<br /><br /> - **CHAVE.** Este valor indica que o **ativar BitLocker utilizando apenas uma chave de arranque externa** opção está selecionada e que vai ser utilizada apenas uma chave de arranque externa quando ativar o BitLocker no computador de destino.|Não|Sim|Não|  
|**OSDBitLockerStartupKeyDrive**<br /><br /> Especifica a letra de unidade em que a chave de arranque externa do BitLocker será armazenada no computador de destino. Esta variável é apenas considerada válidos quando **OSDBitLockerMode** está definido como **TPMKEY** ou **chave**.|Não|Sim|Não|  
|**OSDBitLockerWaitForEncryption**<br /><br /> Especifica se a sequência de tarefas deve aguardar até a encriptação BitLocker termina. Se a variável é definida como:<br /><br /> -                                      **Sim**, em seguida, a **Aguarde que a encriptação BitLocker em todas as unidades antes de continuar** caixa de verificação está selecionada e a sequência de tarefas irá esperar até que a instalação estiver concluída<br /><br /> -                                      **NÃO**, em seguida, a **Aguarde que a encriptação BitLocker em todas as unidades antes de continuar** caixa de verificação está desmarcada e a sequência de tarefas não irá esperar até que a instalação estiver concluída|Sim|Sim|Sim|  

###### <a name="configuration-variables"></a>Variáveis de configuração  
 Apresenta uma lista de tabela 31 a **BitLockerPage** variáveis de configuração com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI.  

### <a name="table-31-bitlockerpage-configuration-variables"></a>31 de tabela. Variáveis de configuração BitLockerPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**KeyLocation**<br /><br /> Especifica o caminho completamente qualificado para a localização onde estão armazenadas as chaves de encriptação do BitLocker, que pode ser uma localização ou caminho UNC. Este valor de configuração é utilizado para definir o valor da **BDEKeyLocation** variável de sequência de tarefas para o **BitLockerPage**. Esta variável é apenas considerada válidos quando **OSDBitLockerMode** está definido como **TPMKEY** ou **chave**.|Sim|Não|Sim|  

#####  <a name="ComputerPage"></a>ComputerPage  
 Utilize esta página do Assistente para configurar o nome do computador de destino, o domínio ou grupo de trabalho e as credenciais a utilizar ao associar um domínio. Quando configura esta página para associar o computador de destino a um domínio, esta página do assistente irá validar as credenciais que fornece para aderir ao domínio do AD DS por predefinição. Página do assistente, em seguida, tenta modificar um objeto de computador no AD DS para verificar que as credenciais de utilizador fornecidas nesta página têm permissões para criar ou modificar o objeto de computador. Pode desativar um dos seguintes comportamentos. Se desativar a validação das credenciais, a verificação de permissões para criar ou modificar objetos de computador também é desativada. Ambos estes validações ocorrerem quando o **seguinte** botão é clicado. Se qualquer uma das validações encontra um erro, será apresentada uma mensagem de erro e esta página irá continuar a ser apresentado.  

 Segue-se a ordem de precedência para determinar o nome predefinido do computador:  

1.  Se o **UserExistingComputerName** valor no ficheiro de configuração do Assistente de UDI está definido como **verdadeiro**, será utilizado o nome de computador existente \(se estiver presente\).  

2.  Se o **OSDComputerName** variável de sequência de tarefas estiver definida, em seguida, o nome do computador nessa variável é utilizado.  

3.  Se for especificado um valor predefinido para o nome do computador no ficheiro de configuração do Assistente de UDI, esse valor é utilizado.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 32 o **ComputerPage** com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-32-computerpage-task-sequence-variables"></a>Tabela 32. Variáveis de sequência de tarefas ComputerPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**OSDComputerName**<br /><br /> Especifica o nome do computador de destino. O valor desta variável é definido **nome do computador** caixa.|Sim|Sim|Sim|  
|**OSDDomainName**<br /><br /> Especifica o nome do domínio ao qual o computador de destino está a ser associada. O valor desta variável é definido **domínio** caixa.|Sim|Sim|Sim|  
|**OSDDomainOUName**<br /><br /> Especifica o nome da UO dentro do domínio ao qual o objeto de computador de destino está a ser colocados. O valor desta variável é definido **unidade organizacional** caixa.|Sim|Sim|Sim|  
|**OSDJoinAccount**<br /><br /> Especifica a conta de utilizador utilizada para associar o computador de destino ao domínio. O valor desta variável é definido **nome de utilizador** caixa.|Sim|Sim|Sim|  
|**OSDJoinPassword**<br /><br /> Especifica a palavra-passe da conta de utilizador utilizada para associar o computador de destino ao domínio. O valor desta variável é definido **palavra-passe** e **Confirmar palavra-passe** caixas.|Sim|Sim|Sim|  
|**OSDNetworkJoinType**<br /><br /> Especifica se o computador de destino é associado a um grupo de trabalho ou domínio. Se o valor estiver definido como:<br /><br /> \-**0**, em seguida, a **domínio** opção está selecionada e o computador de destino será associado a um domínio<br /><br /> \-                                      **1**, em seguida, a **Workgroup** opção está selecionada e o computador de destino será associado a um grupo de trabalho|Não|Sim|Não|  
|**SMSTSAssignUsersMode**<br /><br /> Especifica o modo para configurar a afinidade de utilizador no Configuration Manager. Utilize esta variável para configurar o comportamento de criação de afinidade entre as contas de utilizador e computador de destino no **SMSTSUdaUsers** variável de sequência de tarefas. Se esta variável não for especificada antes de apresentar nesta página, o valor desta variável é definido como **pendente**.<br /><br /> Valores possíveis incluem variável:<br /><br /> \-                                      **Automática.** O processamento de afinidade é automaticamente aprovado pelo Configuration Manager.<br /><br /> \-**Pendente.** A afinidade processar regras irá exigir a aprovação por um administrador do Configuration Manager.<br /><br /> \-                                      **Desativado.** Nenhum processamento afinidade irá ocorrer.|Não|Sim|Não|  

###### <a name="configuration-variables"></a>Variáveis de configuração  
 Apresenta uma lista de tabela 33 o **ComputerPage** variáveis de configuração com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI.  

### <a name="table-33-computerpage-configuration-variables"></a>33 de tabela. Variáveis de configuração ComputerPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**ADComputerObjectCheck**<br /><br /> Especifica se o **ComputerPage** página do assistente validará que as credenciais fornecidas têm as permissões adequadas para modificar um objeto de computador no AD DS antes de continuar para a página seguinte do assistente.<br /><br /> Nota:<br /><br /> Esta definição de configuração é ignorada se **ADCredentialCheck** está definido como **falso**.<br /><br /> Se o valor estiver definido como:<br /><br /> \-**Verdadeiro**, em seguida, a **verifique de objeto de computador de diretório Active Directory** caixa de verificação está selecionada no editor de página do assistente no **credenciais de associação de domínio** secção no Assistente de UDI Designer e permissões para modificar um objeto de computador para as credenciais serem validadas<br /><br /> \-**Falso**, em seguida, a **verifique de objeto de computador de diretório Active Directory** caixa de verificação está desmarcada no editor de página do assistente no **credenciais de associação de domínio** secção no Assistente de UDI Designer e permissões para modificar um objeto de computador para as credenciais não são validadas|Sim|Não|Sim|  
|**ADCredentialCheck**<br /><br /> Especifica se o **ComputerPage** página do assistente irá validar as credenciais fornecidas para a associação a um domínio antes de continuar para a página seguinte do assistente. Se o valor estiver definido como:<br /><br /> \-                                      **Verdadeiro**, em seguida, a **verificação de credenciais do Active Directory** caixa de verificação está selecionada no editor de página do assistente no **credenciais de associação de domínio** secção o UDI Wizard Designer, e credenciais serem validadas<br /><br /> Se esta definição de configuração estiver definida como **verdadeiro**, em seguida, das credenciais serem validadas, mesmo se os campos de credencial estiverem desativados \(bloqueado\).<br /><br /> \-**Falso**, em seguida, a **verificação de credenciais do Active Directory** caixa de verificação está desmarcada no editor de página do assistente no **credenciais de associação de domínio** secção no Assistente de UDI Estruturador e as credenciais não são validadas<br /><br /> Se esta definição de configuração estiver definida como **falso**, em seguida, a **ADComputerObjectCheck** definição de configuração é ignorada e a validação do que as credenciais fornecidas podem modificar um computador de objeto no AD DS Não é executado.|Sim|Não|Sim|  
|**UseExistingComputerName**<br /><br /> Especifica se o **ComputerPage** página do assistente irá utilizar o nome de computador existente no computador de destino como predefinição para o nome do computador.<br /><br /> Nota:<br /><br /> Esta caixa de verificação só é relevante para o cenário de implementação de atualizar o computador.<br /><br /> Se o valor estiver definido como:<br /><br /> \-**Verdadeiro**, em seguida, a **utilize o nome de computador existente** caixa de verificação está selecionada no editor de página do assistente no **nome do computador** secção o UDI Wizard Designer e o existente nome de computador será utilizado como o nome de computador predefinido para o computador de destino depois do novo sistema operativo ser implementado<br /><br /> \-                                      **FALSO**, em seguida, a **utilize o nome de computador existente** caixa de verificação está desmarcada no editor de página do assistente no **nome do computador** secção o UDI Wizard Designer e o nome de computador existente não será utilizada como o nome de computador predefinido para o computador de destino depois do novo sistema operativo ser implementado|Sim|Não|Sim|  

#####  <a name="ConfigScanPage"></a>ConfigScanPage  
 Utilize esta página do Assistente para executar tarefas de UDI analisar a configuração do computador de destino para determinar se o computador de destino está pronto para a implementação da imagem do sistema operativo. Esta preparação inclui ter recursos de sistema suficientes e os pré-requisitos de software que está a ser instalado e configurado corretamente. Além disso, outras tarefas UDI são executadas essas informações de configuração recolher sobre o computador de destino, tal como a identificação:  

-   Indica se o computador está ligado ao power \(, por oposição a executar um bateria\)  

-   Indica se o computador está ligado a uma ligação de rede com fios \(, por oposição a utilizar uma ligação de rede sem fios\)  

-   As aplicações instaladas  

-   Qualquer instaladas impressoras  

#####  <a name="LanguagePage"></a>LanguagePage  
 Utilize esta página do Assistente para determinar quais os pacotes de idioma devem ser instalados, o idioma predefinido para o sistema operativo de destino, a região de teclado e o fuso horário em que o computador será localizado.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 34 o **LanguagePage** com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-34-languagepage-task-sequence-variables"></a>34 de tabela. Variáveis de sequência de tarefas LanguagePage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**InputLocale**<br /><br /> Especifica a região de entrada do sistema operativo de destino. Definir o valor desta variável no **formato de hora e a moeda** caixa. Se não for especificado, é utilizada a região de entrada configurada na imagem.|Sim|Sim|Sim|  
|**KeyboardLocale**<br /><br /> Especifica a região de teclado do sistema operativo de destino. Defina o valor desta variável no **esquema do teclado** caixa. Se não for especificado, é utilizada a região de teclado configurada na imagem.|Sim|Sim|Sim|  
|**OSDTimeZone**<br /><br /> Especifica o fuso horário onde estarão localizado fisicamente o computador de destino. Defina o valor desta variável no **fuso horário** caixa. Se não for especificado, é utilizado o fuso horário configurado na imagem.|Sim|Sim|Sim|  
|**UILanguage**<br /><br /> Especifica o idioma predefinido a ser utilizado para o sistema operativo de destino. Defina o valor desta variável no **idioma instalar** caixa. Se não for especificado, é utilizado o idioma configurado na imagem.|Sim|Sim|Sim|  

#####  <a name="ProgressPage"></a>ProgressPage  
 Utilize esta página do Assistente para executar tarefas de UDI capturar os dados de migração de estado de utilizador do computador de destino. Estas tarefas incluem:  

-   Copiar o ficheiro de deteção de aplicação para a localização selecionada no [UserStatePage](#UserStatePage) página do Assistente  

-   Copiar o ficheiro de configuração de impressora para a localização selecionada no [UserStatePage](#UserStatePage) página do Assistente  

-   Copiar a lista de produtos instalados para a localização selecionada no [UserStatePage](#UserStatePage) página do Assistente  

-   Dados de migração para a localização selecionada de estado de executar a USMT e guardar o utilizador a [UserStatePage](#UserStatePage) página do Assistente  

#####  <a name="RebootPage"></a>RebootPage  
 Utilize esta página do Assistente para notificar o utilizador que o computador de destino será reiniciado. Pode configurar a mensagem de notificação com o UDI Wizard Designer.  

#####  <a name="SummaryPage"></a>SummaryPage  
 Utilize esta página do Assistente para notificar o utilizador sobre as opções de configuração que foram selecionados ao executar o Assistente de UDI. As informações de configuração apresentadas nesta página do assistente automaticamente são recolhidas a partir de outras páginas do assistente. Alguns campos nas outras páginas de assistente permitem-lhe configurar a legenda \(etiqueta\) apresentadas nesta página do assistente com o UDI Wizard Designer.  

#####  <a name="UDAPage"></a>UDAPage  
 Utilize esta página do Assistente para configurar o UDA entre o computador de destino e um utilizador especificado. Atribuir um utilizador que o utilizador principal de um computador permite a instalação automática do software que é implementado para esse utilizador. A funcionalidade UDA só está disponível no Configuration Manager e apenas o cenário de implementação do novo computador.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 35 a **UDAPage** com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-35-udapage-task-sequence-variables"></a>35 de tabela. Variáveis de sequência de tarefas UDAPage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**SMSTSAssignUsersMode**<br /><br /> Especifica o modo para configurar a afinidade de utilizador no Configuration Manager. Utilize esta variável para configurar o comportamento de criação de afinidade entre as contas de utilizador e computador de destino no **SMSTSUdaUsers** variável de sequência de tarefas. Para definir esta variável, selecione o **afinidade dispositivo / utilizador de utilização** caixa de verificação.<br /><br /> Se a variável é definida como:<br /><br /> \-                                      **Auto**, em seguida, o processamento de afinidade é automaticamente aprovado pelo Configuration Manager<br /><br /> \-**Pendente**, em seguida, a afinidade processar regras irá exigir a aprovação por um administrador do Configuration Manager \(este é o valor utilizado quando o **afinidade dispositivo / utilizador de utilização** caixa de verificação está selecionado.\)<br /><br /> \-                                      **Desativado**, em seguida, ocorrerá o não processamento de afinidade|Não|Sim|Não|  
|**SMSTSUdaUsers**<br /><br /> Especifica que os utilizadores associados ao computador de destino. O **conta de afinidade de dispositivo do utilizador** define esta variável. Esta variável pode ter um ou vários utilizadores especificados e está no formato `Domain\User1, Domain\User2`.|Sim|Sim|Sim|  

#####  <a name="UserStatePage"></a>UserStatePage  
 Utilize esta página do Assistente para configurar as definições para capturar ou restaurar os dados de migração de estado do utilizador. Página do assistente é utilizada para captura de dados de migração de estado de utilizador e de restauro.  

 O **UserStatePage** pode capturar ou restaurar os dados de migração de estado do utilizador a partir de um disco ligado localmente no computador de destino, uma unidade USB ligada ao computador de destino ou uma pasta partilhada de rede. Além disso, pode optar por não restaurar os dados do utilizador. A lógica de código por trás de página do assistente ativa, desativa ou seleciona automaticamente a cada uma das seguintes opções, com base no cenário de implementação e se o disco está a ser formatado:  

-   **Não existem dados para restauro.** Esta opção não indica que não existe nenhum dados de migração de estado de utilizador para restaurar e define o **OSDUserStateMode** variável de sequência de tarefas e **UserStateMode** variável à **NoData**.  

-   **Local.** Esta opção indica que os dados de migração de estado de utilizador devem ser armazenados num disco ligado localmente para o computador de destino e define o **OSDUserStateMode** variável de sequência de tarefas e **UserStateMode** variável à **Local**.  

-   **USB.** Esta opção indica que os dados de migração de estado de utilizador devem ser armazenados num disco USB ligado localmente para o computador de destino e define o **OSDUserStateMode** variável de sequência de tarefas e **UserStateMode** variável à **USB**.  

-   **Rede.** Esta opção indica que os dados de migração de estado de utilizador devem ser armazenados em conjuntos e uma pasta de rede partilhada a **OSDUserStateMode** variável de sequência de tarefas e **UserStateMode** variável à **Rede**.  

######  <a name="NEWCOMPUTERStageBehavior"></a>Comportamento de fase NEWCOMPUTER  
 A fase NEWCOMPUTER é utilizada para computadores nos quais não existem dados de migração de estado de utilizador existem. O cenário de implementação do novo computador pode ser utilizado como a segunda parte do cenário de implementação de substituir o computador. Se o utilizador seleciona para:  

-   Formatar o disco no computador de destino, em seguida, a **UserStatePage** parte do princípio de que não existem dados de migração de estado de utilizador estão localizados no disco rígido local, por isso, o **Local** opção está desativada e todas as outras opções são ativado  

-   Formata o disco no computador de destino, em seguida, a **UserStatePage** parte do princípio de que não há dados de migração de estado de utilizador a ser restaurado e todas as opções são desativadas diferente do **Local** opção \(Utilizando o **Local** opção fornece um método mais rápido para restaurar o utilizador de estado de dados de migração de que o USB ou métodos de pasta partilhada de rede.\)  

 36 tabela lista o comportamento das opções na página do Assistente para a fase NEWCOMPUTER. O **formato** coluna indica se o disco rígido de destino deve ser formatado como parte da implementação. Outras colunas indicam a configuração das opções quando o **UserStatePage** está carregada.  

### <a name="table-36-behavior-of-options-for-the-newcomputer-stage"></a>Tabela 36. Comportamento de opções para a fase NEWCOMPUTER  

|**Formato**|**NoData**|**Local**|**USB**|**Rede**|  
|-|-|-|-|-|  
|Sim|Ativado|Desativado|Ativado|Ativado|  
|Não|Desativado|Selecionado|Desativado|Desativado|  

######  <a name="NewComputerPrestagedStageBehavior"></a>Comportamento de fase de NewComputer.Prestaged  
 NEWCOMPUTER. Fase pré-configurado baseia-se a funcionalidade de suporte de dados pré-configurado no Configuration Manager. Como é novo disco rígido local, não há nenhum dados de migração de estado do utilizador a ser restaurado a partir do disco rígido local, por isso, o **Local** opção está desativada. Todas as outras opções são válidas para este cenário de implementação e estão ativadas. Nenhuma opção de predefinição está selecionada.  

 37 tabela lista o comportamento das opções na página do Assistente para a fase de NewComputer.Prestaged. O **formato** coluna indica se o disco rígido de destino deve ser formatado como parte da implementação. Outras colunas indicam a configuração das opções quando o **UserStatePage** está carregada.  

### <a name="table-37-behavior-of-options-for-the-newcomputerprestaged-stage"></a>37 de tabela. Comportamento de opções para a fase de NewComputer.Prestaged  

|**Formato**|**NoData**|**Local**|**USB**|**Rede**|  
|-|-|-|-|-|  
|N\/A|Ativado|Desativado|Ativado|Ativado|  

######  <a name="REFRESHStageBehavior"></a>Comportamento de fase de ATUALIZAÇÃO  
 A fase de ATUALIZAÇÃO é iniciada a um sistema operativo Windows completo, em vez do Windows PE. Se o utilizador seleciona para:  

-   Formatar o disco no computador de destino, em seguida, a **UserStatePage** parte do princípio de que não existem dados de migração de estado de utilizador estão a ser restaurado e todas as opções são desativadas diferente do **NoData** opção  

-   Formata o disco no computador de destino, em seguida, a **UserStatePage** parte do princípio de que não há dados de migração de estado de utilizador a ser restaurado e todas as opções são desativadas diferente do **Local** opção \(Utilizando o **Local** opção fornece um método mais rápido para restaurar o utilizador de estado de dados de migração de que o USB ou métodos de pasta partilhada de rede.\)  

 38 tabela lista o comportamento das opções na página do Assistente para a fase de ATUALIZAÇÃO. O **formato** coluna indica se o disco rígido de destino deve ser formatado como parte da implementação. Outras colunas indicam a configuração das opções quando o **UserStatePage** está carregada.  

### <a name="table-38-behavior-of-options-for-the-refresh-stage"></a>Tabela de 38. Comportamento de opções para a fase de ATUALIZAÇÃO  

|**Formato**|**NoData**|**Local**|**USB**|**Rede**|  
|-|-|-|-|-|  
|Sim|Selecionado|Desativado|Desativado|Desativado|  
|Não|Desativado|Selecionado|Desativado|Desativado|  

######  <a name="REPLACEWinPEStageBehavior"></a>SUBSTITUA. Comportamento de fase WinPE  
 A substituir. Fase WinPE captura os dados de migração de estado de utilizador do existente \(antigo\) computador e, em seguida, restaura os dados de migração de estado de utilizador mais tarde utilizando um dos cenários de implementação do novo computador. Porque os dois computadores diferentes estiverem envolvidos na implementação, os dados de migração de estado do utilizador tem de ser guardados para uma unidade USB ou para uma pasta partilhada de rede. Guardar dados de migração de estado do utilizador num disco local não está disponível.  

 39 tabela lista o comportamento das opções na página do Assistente para a substituição. Fase WinPE. O **formato** coluna indica se o disco rígido de destino deve ser formatado como parte da implementação. Outras colunas indicam a configuração das opções quando o **UserStatePage** está carregada.  

### <a name="table-39-behavior-of-options-for-the-replacewinpe-stage"></a>39 de tabela. Comportamento das opções para a substituição. Fase WinPE  

|**Formato**|**NoData**|**Local**|**USB**|**Rede**|  
|-|-|-|-|-|  
|N\/A|Desativado|Desativado|Ativado|Ativado|  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 40 a **UserStatePage** com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-40-userstatepage-task-sequence-variables"></a>40 de tabela. Variáveis de sequência de tarefas UserStatePage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**\_SMSTsInWinPE**<br /><br /> Especifica se o Assistente de UDI está em execução no Windows PE. Se a variável é definida como:<br /><br /> \-**Verdadeiro**, em seguida, o Assistente de UDI está em execução no Windows PE<br /><br /> \-                                      **FALSO**, em seguida, o Assistente de UDI não está em execução no Windows PE, mas em vez de um sistema operativo Windows completo|Sim|Não|Não|  
|**OSDDataSourceDirectory**<br /><br /> Especifica o diretório no qual os dados de migração de estado do utilizador são armazenados.|Não|Sim|Não|  
|**OSDDataSourceDrive**<br /><br /> Especifica a unidade USB utilizada para capturar e restaurar dados de migração estado de utilizador, que é selecionar os **unidade USB destino** caixa. Se a variável é definida antes de mostrar a página do assistente, é utilizado o valor da variável como o valor predefinido.|Sim|Sim|Não|  
|**OSDDiskPart**<br /><br /> Especifica se a unidade selecionada para a instalação do sistema operativo de destino deve ser formatada e particionada. Definir esta variável no [VolumePage](#VolumePage) página do assistente e o código na página do assistente utilizado para determinar que opções estão selecionadas e ativadas por predefinição. Para obter mais informações, consulte [UserStatePage](#UserStatePage).|Sim|Não|Sim|  
|**OSDHardLinks**<br /><br /> Especifica se os dados de migração de estado do utilizador está a ser capturada para ou restaurado a partir de uma unidade local. Se a variável é definida como:<br /><br /> \-                                      **Verdadeiro**, em seguida, a **Local** opção tiver sido selecionada, e os dados de migração de estado do utilizador serão capturados ou restaurados a partir de uma unidade local que está ligada ao computador de destino<br /><br /> \-**Falso**, em seguida, a **Local** não foi selecionada opção e não existem dados de migração de estado do utilizador serão capturados ou restaurados a partir de uma unidade local que está ligada ao computador de destino|Não|Sim|Não|  
|**OSDRestoreData**<br /><br /> Especifica se há dados a ser restaurado. Se a variável é definida como:<br /><br /> \-                                      **Verdadeiro**, em seguida, a **Local**, **unidade USB destino**, ou **rede** opção tiver sido selecionada, e os dados de migração de estado do utilizador serão capturados ou restaurados a partir de o computador de destino<br /><br /> \-**Falso**, em seguida, a **sem dados para restauro** opção tiver sido selecionada, e não existem dados de migração de estado do utilizador serão capturados ou restaurados a partir do computador de destino|Não|Sim|Não|  
|**OSDUserStateKey**<br /><br /> Especifica o nome de utilizador utilizado para proteger os dados de migração de estado do utilizador. O nome de utilizador é fornecido quando os dados de migração de estado do utilizador são capturados. O mesmo nome de utilizador e palavra-passe tem de ser fornecidos quando os dados de migração de estado do utilizador são restaurados. Definir o valor desta variável no **nome de utilizador** caixa.|Sim|Sim|Sim|  
|**OSDUserStateKeyPassword**<br /><br /> Especifica a palavra-passe para o nome de utilizador utilizada para proteger os dados de migração de estado do utilizador. Defina o valor desta variável no **palavra-passe** e **Confirmar palavra-passe** caixas.|Sim|Sim|Sim|  
|**OSDUserStateMode**<br /><br /> Especifica o modo \(método\) para capturar ou restaurar os dados de migração de estado do utilizador. O valor desta variável é definido pelas opções selecionadas. Se a variável é definida como:<br /><br /> \-**NoData**, em seguida, a **sem dados para restauro** opção tiver sido selecionada, e não existem dados de migração de estado do utilizador serão capturados ou restaurados<br /><br /> \-**Local**, em seguida, a **Local** opção tiver sido selecionada, e os dados de migração de estado do utilizador serão capturados ou restaurados a partir de um disco rígido local no computador de destino<br /><br /> \-**Rede**, em seguida, a **rede** opção tiver sido selecionada e o estado do utilizador **migração** dados serão capturados para ou restaurados a partir de uma pasta partilhada de rede<br /><br /> \-Quando utilizado no modo de captura, esta opção cria uma pasta com base num hash do nome de utilizador e palavra-passe para que a identidade de dados de migração de estado do utilizador está protegida. Exato mesmo nome de utilizador e palavra-passe tem de ser utilizados ao restaurar os dados de migração de estado de utilizador para que a página do assistente com precisão possam localizar a pasta.<br /><br /> \-**USB**, em seguida, a **unidade USB destino** opção tiver sido selecionada, e os dados de migração de estado do utilizador serão capturados para ou restaurados a partir de uma pen USB que esteja fisicamente anexada ao computador de destino<br /><br /> \-O comportamento de página do Assistente para unidades USB também é afetado pelo **formato**, **FormatPrompt**, e **MinimumDriveSize** variáveis.|Não|Sim|Não|  
|**SMSConnectNetworkFolderPath**<br /><br /> Especifica a pasta partilhada de rede utilizada para capturar e restaurar dados de migração estado de utilizador, que são selecionados o **rede** caixa. O **rede** caixa apresenta um utilizador\-nome amigável para a rede partilhado pasta que está configurada no **partilhas de rede** caixa o **caixa de combinação de rede** secção no editor de página do assistente no UDI Wizard Designer. Se a variável é definida antes de mostrar a página do assistente, é utilizado o valor da variável como o valor predefinido.|Sim|Sim|Sim|  

###### <a name="memory-variables"></a>Variáveis de memória  
 Apresenta uma lista de tabela 41 o **UserStatePage** variáveis de memória com uma descrição e se a variável de leitura ou escrita por página do assistente.  

### <a name="table-41-userstatepage-memory-variables"></a>Tabela 41. Memória UserStatePage variáveis  

|**Variável**|**Leitura**|**Escrita**|  
|-|-|-|  
|**Letradaunidade**<br /><br /> Especifica a letra de unidade para a unidade USB selecionado no **unidade USB destino** caixa na página do assistente. O valor da variável desta será a letra de unidade, incluindo o sufixo de dois pontos (:), tal como *m:.*|Não|Sim|  
|**TargetDrive**<br /><br /> Especifica a legenda apresentada no **unidade USB destino** caixa na página do Assistente para a unidade USB selecionada no computador de destino. O valor desta variável será semelhante ao seguinte exemplo:<br /><br /> `M: VendorA Ultra TD v1.0 USB Device (74.5 GB)`|Não|Sim|  
|**UserStateMode**<br /><br /> Especifica a opção selecionada com as opções na página do assistente e está definido para o mesmo valor que o **OSDUserStateMode** variável. Valores válidos incluem variável:<br /><br /> -                                      **NoData**, que indica que o **sem dados para restauro** opção tiver sido selecionada<br /><br /> -                                      **Local**, que indica que o **Local** opção tiver sido selecionada<br /><br /> -                                      **USB**, que indica que o **unidade USB destino** opção tiver sido selecionada<br /><br /> - **Rede**, que indica que o **rede** opção tiver sido selecionada|Não|Sim|  

###### <a name="configuration-variables"></a>Variáveis de configuração  
 Apresenta uma lista de tabela 42 o **UserStatePage** variáveis de configuração com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI.  

### <a name="table-42-userstatepage-configuration-variables"></a>42 de tabela. Variáveis de configuração UserStatePage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**DataSourceText**<br /><br /> Especifica uma mensagem meramente informativa que dá instruções ao utilizador efetuar o estado do utilizador capturar ou restaurar sobre como utilizar a página do assistente. Definir o valor desta variável no **texto de instrução** caixa o **mensagem** secção no Assistente para bloco paginado editor no UDI Wizard Designer.|Sim|Não|Sim|  
|**Formato**<br /><br /> Especifica se a unidade USB selecionada para capturar estado do utilizador no computador de destino deve ser particionada e formatada antes da captura de dados de migração de estado do utilizador. Defina o valor desta variável, selecionando o **formata a pen USB antes da captura** caixa de verificação a **caixa de combinação de USB** editor no UDI Wizard Designer do bloco paginado secção no Assistente para.<br /><br /> Se a variável é definida como:<br /><br /> - **Verdadeiro**, em seguida, a unidade é formatada antes da captura de dados de migração de estado de utilizador<br /><br /> -                                      **FALSO**, em seguida, a unidade não está formatada antes da captura de dados de migração de estado de utilizador|Sim|Não|Sim|  
|**FormatPrompt**<br /><br /> Especifica se o utilizador tem de confirmar que a unidade USB utilizada para capturar os dados de migração de estado de utilizador está a ser formatado antes de efetuar a captura. Defina o valor desta variável, selecionando o **solicitar ao utilizador antes da unidade de destino de formatação** caixa de verificação a **caixa de combinação de USB** editor no UDI Wizard Designer do bloco paginado secção no Assistente para.<br /><br /> Nota:<br /><br /> Esta variável só é válida se o **OSDUserStateMode** variável de sequência de tarefas está definido como **USB**.|Sim|Não|Sim|  
|**MinimumDriveSize**<br /><br /> Especifica o espaço em disco mínimo disponível em gigabytes necessários para uma unidade para estar disponível para armazenar dados de migração de estado do utilizador. O valor desta variável age como um filtro e defini-lo no **tamanho de unidade mínimo** caixa de texto **caixa de combinação de USB** secção no Assistente para bloco paginado editor no UDI Wizard Designer.|Sim|Não|Sim|  
|**NetworkDrive**<br /><br /> Especifica a letra de unidade que utiliza esta página do Assistente para mapear para a pasta partilhada de rede no **SMSConnectNetworkFolderPath** variável de sequência de tarefas. O mapeamento de pasta partilhada de rede é utilizado para capturar ou restaurar os dados de migração de estado do utilizador. Defina o valor desta variável no **letra de unidade mapeada** caixa o **caixa de combinação de rede** editor no UDI Wizard Designer do bloco paginado secção no Assistente para. A letra de unidade especificada tem de incluir a vírgula (:) após a letra de unidade e não deve estar em utilização no computador de destino. Por exemplo, se o computador de destino tiver unidades c e d:, em seguida, c e d: não foi possível utilizar esta variável.<br /><br /> Nota:<br /><br /> Esta variável só é válida se o **OSDUserStateMode** variável de sequência de tarefas está definido como **rede**.|Sim|Não|Sim|  
|**Estado**<br /><br /> Especifica se a página do assistente está a ser utilizada para capturar ou restaurar os dados de migração de estado do utilizador. Defina o valor desta variável no **capturar ou restaurar** caixa o **capturar/restaurar a localização** secção no Assistente para bloco paginado editor no UDI Wizard Designer. Se a variável é definida como:<br /><br /> - **Capturar**, em seguida, a página do assistente utilizada para capturar os dados de migração de estado do utilizador<br /><br /> -                                      **Restaurar**, em seguida, a página do assistente é utilizada para restaurar dados de migração de estado de utilizador|Sim|Não|Sim|  

#####  <a name="VolumePage"></a>VolumePage  
 Utilize esta página do Assistente para configurar as definições para o volume de disco no computador de destino no qual o sistema operativo será implementado. Estas definições incluem a seleção do sistema operativo de destino, selecionar a unidade de destino, selecionar qualquer instalação do Windows e determinar se a unidade de destino deve ser formatada como parte do processo de implementação.  

###### <a name="task-sequence-variables"></a>Variáveis de sequência de tarefas  
 Apresenta uma lista de tabela 43 o **VolumePage** com uma descrição e se a variável é lida por página do assistente, escrita pelo página do assistente, ou pode ser configurada no ficheiro de configuração do Assistente de UDI as variáveis de sequência de tarefas.  

### <a name="table-43-volumepage-task-sequence-variables"></a>43 de tabela. Variáveis de sequência de tarefas VolumePage  

|**Variável**|**Leitura**|**Escrita**|**Configuração**|  
|-|-|-|-|  
|**OSDDiskPart**<br /><br /> Especifica se a unidade selecionada para implementação do sistema de operativo de destino no computador de destino deve ser particionada e formatada antes da captura de dados de migração de estado do utilizador. O valor desta variável é definido por um dos seguintes caixas de verificação na página do assistente:<br /><br /> -                                      **Limpar o volume selecionado.** Esta caixa de verificação é apresentada quando o Assistente de UDI está em execução num sistema operativo Windows completo. Pode configurar a mensagem de texto utilizando o **FormatFullOS** propriedade setter para a página do assistente no ficheiro de configuração do Assistente de UDI.<br /><br /> -                                      **Particionar e formatar o disco 0.** Esta caixa de verificação é apresentada quando o Assistente de UDI está em execução no Windows PE. Pode configurar a mensagem de texto utilizando o **FormatWinPE** propriedade setter para a página do assistente no ficheiro de configuração do Assistente de UDI.<br /><br /> A lógica de código por trás do [UserStatePage](#UserStatePage) página do assistente utiliza esta variável para determinar que opções estão selecionadas e ativadas por predefinição.<br /><br /> Se a variável é definida como:<br /><br /> - **Verdadeiro**, em seguida, a unidade está particionada e formatada antes de implementar o sistema operativo de destino<br /><br /> -                                      **FALSO**, em seguida, a unidade não está particionada e formatada antes de implementar o sistema operativo de destino|Sim|Sim|Sim|  
|**OSDImageIndex**<br /><br /> Especifica um índice numérico da imagem do sistema operativo no ficheiro. wim, o que está selecionado no **seleção da imagem** caixa de combinação. Configurar a lista de imagens do sistema de operativo possíveis no **seleção da imagem** caixa o **valores da caixa de combinação imagem** lista o **caixa de combinação de imagem** secção sobre o  **VolumePage** editor de página do assistente. O índice de imagem é configurado como parte de cada imagem no **valores da caixa de combinação imagem** lista.|Sim|Sim|Sim|  
|**OSDImageName**<br /><br /> Especifica o nome da imagem do sistema operativo no ficheiro. wim, o que está selecionado no **seleção da imagem** caixa. A lista de imagens do sistema de operativo possíveis no **seleção da imagem** caixa de combinação está configurada no **valores da caixa de combinação imagem** lista o **caixa de combinação de imagem** secção no **VolumePage** editor de página do assistente. O nome da imagem é configurado como parte de cada imagem no **valores da caixa de combinação imagem** lista.|Não|Sim|Não|  
|**OSDTargetDrive**<br /><br /> Especifica a letra de unidade para o volume selecionado no **Volume** caixa na página do assistente. O valor da variável desta será a letra de unidade, incluindo o sufixo de dois pontos (:), tal como *c.*|Não|Sim|Não|  
|**OSDWinPEWindir**<br /><br /> Especifica a localização de uma instalação existente do Windows no computador de destino. Defina o valor desta variável no **Windows Directory** caixa na página do assistente.|Não|Sim|Não|  

###### <a name="memory-variables"></a>Variáveis de memória  
 Apresenta uma lista de tabela 44 o **VolumePage** variáveis de memória com uma descrição e se a variável de leitura ou escrita por página do assistente.  

### <a name="table-44-volumepage-memory-variables"></a>44 de tabela. Memória VolumePage variáveis  

|**Variável**|**Leitura**|**Escrita**|  
|-|-|-|  
|**VolumeArchitecture**<br /><br /> Especifica a arquitetura de processador do sistema operativo ser implementado, o que está selecionada no **seleção da imagem** caixa. O **VolumeArchitecture** consome esta variável para filtrar a arquitetura de aplicações apresentada na página de que a página do assistente. Por exemplo, se um sistema operativo de 32 bits está a ser implementado, a **VolumeArchitecture** página do Assistente de remove (filtros) todas as aplicações de 64 bits da lista de aplicações disponíveis.<br /><br /> Se a variável é definida como:<br /><br /> -                                      **x86**, em seguida, foi selecionado um sistema operativo de 32 bits<br /><br /> - **AMD64**, em seguida, o sistema operativo de 64 bits foi selecionado|Não|Sim|  

#####  <a name="WelcomePage"></a>WelcomePage  
 Utilize esta página do Assistente para fornecer informações para o utilizador sobre o Assistente de UDI e o processo de implementação. Pode configurar a mensagem de notificação com o UDI Wizard Designer.  

### <a name="udi-build-your-own-page-toolbox-control-reference"></a>UDI criar a seus próprios referência de controlo de caixa de ferramentas da página  
 A funcionalidade de criar sua própria página no UDI permite-lhe criar páginas de assistente personalizado que pode utilizar para recolher informações de implementação adicional para utilização num UDI. Pode criar páginas de assistente personalizado utilizando a:  

-   **Crie a funcionalidade da sua página próprio.** Esta funcionalidade permite-lhe criar uma página do assistente personalizado para recolha de informações de implementação sem necessidade de escrever código ou ter as competências de programador. Utilize esta funcionalidade se de que precisa para recolher informações básicas, sem interação do utilizador avançado. Por exemplo, não é possível adicionar qualquer código ou personalizar tipos de letra IU utilizar esta funcionalidade.  

-   **SDK de UDI e o Visual Studio**. Utilize este SDK se pretender criar uma página do Assistente Avançadas e totalmente personalizados no Visual Studio para recolher informações de implementação. Embora o SDK de UDI permite-lhe criar páginas de assistente personalizados, tais como adicionar código personalizado ou alterar tipos de letra, este método requer competências de programador.  

     Para obter mais informações sobre como utilizar o SDK de UDI criar páginas do assistente personalizada, consulte "Criar personalizado UDI páginas do assistente" no *guia para programadores do utilizador unidade instalação*.  

 A funcionalidade de criar sua própria página inclui uma caixa de ferramentas de controlos que pode adicionar à sua página do assistente personalizadas da caixa de criar sua própria página ferramentas, que é apresentada quando visualiza a página do assistente personalizado no **configurar** separador no Assistente de UDI Designer.  

 45 tabela lista os tipos de controlos para a página do assistente personalizadas, que é ilustrado na figura 5. Cada um destes controlos é abordada mais detalhadamente numa secção subordinada.  

### <a name="table-45-types-of-controls-in-the-udi-build-your-own-page-toolbox"></a>Tabela 45. Tipos de controlos de UDI criar as suas próprias ferramentas da página  

|**Tipo de controlo**|**Descrição**|  
|-|-|  
|[Controlo de caixa de verificação](#CheckboxControl)|Este controlo permite selecionar ou desmarcar uma opção de configuração e funciona como uma caixa de verificação de IU tradicional.|  
|[Controlo de caixa de combinação](#ComboboxControl)|Este controlo permite-lhe selecionar um item de uma lista de itens e funciona como uma tradicional IU na lista pendente.|  
|[Controlo de linha](#LineControl)|Este controlo permite-lhe adicionar uma linha horizontal dividir uma parte da página do assistente personalizada de outro.|  
|[Controlo de etiqueta](#LabelControl)|Este controlo permite-lhe adicionar texto descritivo só de leitura para a página do assistente.|  
|[Controlo de botões de opção](#RadioControl)|Este controlo permite-lhe selecionar uma opção de configuração de um grupo de dois ou mais opções.|  
|[Controlo de mapa de bits](#BitmapControl)|Este controlo permite-lhe adicionar um gráfico de mapa de bits (*.bmp ficheiro) para a página do assistente personalizado.|  
|[Controlo de caixa de texto](#TextboxControl)|Este controlo permite-lhe introduzir o texto na página do assistente personalizado.|  

 Pode adicionar qualquer combinação destes controlos para a página do assistente personalizadas com base nas informações que pretende recolher. Além disso, pode utilizar o **Mostrar linhas de grelha** caixa de verificação para mostrar ou ocultar linhas de grelha que podem ser utilizadas para ajudar a conceber visualmente a página do assistente personalizado.  

 Figura 5 fornece um exemplo de uma página do assistente personalizados e a caixa de ferramentas de compilação da página próprio.  

 ![Referência de UDI 5](media/UDIReference5.jpg)  

 **Figura SEQ Figure \\ \* ARABIC 5. Página do assistente personalizada de exemplo**  

####  <a name="CheckboxControl"></a>Controlo de caixa de verificação  
 Este controlo permite selecionar ou desmarcar uma opção de configuração e funciona como uma caixa de verificação de IU tradicional. Este controlo tem uma etiqueta correspondente que pode utilizar para descrever o objetivo da caixa de verificação. O estado deste controlo é verdadeiro quando a caixa de verificação está selecionada e falso quando a caixa de verificação está desmarcada. O estado da caixa de verificação é armazenado na variável de sequência de tarefas configurada para este controlo.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 46 tabela lista as propriedades de esquema para o **caixa de verificação** controlar e fornece uma breve descrição de cada propriedade  

### <a name="table-46-checkbox-control-layout-properties"></a>46 de tabela. Propriedades de esquema do controlo de caixa de verificação  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Etiqueta**|Utilize esta propriedade para configurar o texto descritivo associado com a caixa de verificação.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é maior do que a largura do controlo, o texto é anexado e não apresentado.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é taller que a altura do controlo, o texto está anexado.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 Propriedades das definições são utilizadas para configurar os dados apresentados inicialmente num controlo (o valor predefinido) e onde as informações recolhidas do utilizador é guardada. 47 tabela lista as propriedades de definições para o **caixa de verificação** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-47-checkbox-control-settings-properties"></a>47 de tabela. Propriedades de definições de controlo de caixa de verificação  

|**Propriedade**|**Descrição**|  
|-|-|  
|**Valor predefinido**|Utilize esta propriedade para configurar o valor predefinido para o controlo. Para uma caixa de verificação, o valor predefinido é **falso**.|  
|**Nome de variável de sequência de tarefas**|Utilize esta propriedade para configurar a variável de sequência de tarefas armazenar as informações recolhidas do utilizador. Se a sequência de tarefas variável:<br /><br /> -Ainda não existir, a variável de sequência de tarefas é criada e fornece definido como o valor do utilizador<br /><br /> -Já existe, o valor da variável de sequência de tarefas existente é substituído com o valor fornece ao utilizador|  
|**Nome a apresentar amigável visível na página de resumo**|Utilize esta propriedade para configurar o nome descritivo que aparece no **resumo** página do assistente. Este nome é utilizado para descrever o valor que foi guardado no **nome de variável de sequência de tarefas** propriedade para este controlo.|  
|**Foi desbloqueada**|Utilize esta propriedade para configurar se o utilizador é capaz de interagir com o controlo. Por predefinição, o controlo está activado. Este botão apresenta o estado do seguinte:<br /><br /> - **Foi desbloqueada.** O controlo está ativado e os utilizadores podem introduzir informações utilizá-la.<br /><br /> -                                  **Bloqueado.** O controlo está desativado e os utilizadores não conseguem introduzir informações utilizá-la.<br /><br /> **Tenha em atenção** se desativar um controlo (bloqueio), tem de fornecer as informações de controlo recolhido através da configuração de propriedades do MDT no CustomSettings.ini ou na base de dados do MDT. Caso contrário, o Assistente de UDI não irá recolher as informações necessárias e a implementação de UDI irá falhar.|  

####  <a name="ComboboxControl"></a>Controlo de caixa de combinação  
 Este controlo permite-lhe selecionar um item de uma lista de itens e funciona como uma tradicional IU na lista pendente. Este controlo permite-lhe adicionar ou remover itens da lista e forneça um valor correspondente, que será definido na variável de sequência de tarefas configurada para este controlo.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 48 tabela lista as propriedades de esquema para o **Combobox** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-48-combobox-control-layout-properties"></a>Tabela 48. Propriedades de esquema do controlo de caixa de combinação  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no controlo for maior do que a largura do controlo, não será apresentado o texto.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no controlo taller que a altura do controlo, o texto está anexado.|  
|**Itens de dados**|Utilize esta propriedade para configurar a lista de itens de dados apresentada no controlo. Cada item de dados tem as seguintes propriedades:<br /><br /> -                                  **Valor.** O valor armazenado na variável de sequência de tarefas quando o item de dados é seleccionado<br /><br /> -                                  **DisplayValue.** O valor apresentado ao utilizador no controlo<br /><br /> É possível:<br /><br /> -Adicionar itens de dados para a lista com o botão de sinal de adição azul imediatamente para a direita da lista de itens de dados<br /><br /> -Remover itens de dados da lista utilizando a vermelho **X** botão imediatamente para a direita da lista de itens de dados<br /><br /> **Tenha em atenção** não é possível alterar a sequência do item de dados na lista depois de um item é adicionado à lista. Certifique-se de que introduz os itens de dados pela ordem que quer para serem apresentadas no controlo.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 Propriedades das definições são utilizadas para configurar os dados que está inicialmente mostrado num controlo (o valor predefinido) e onde as informações recolhidas do utilizador são guardadas. 49 tabela lista as propriedades de definições para o **Combobox** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-49-combobox-control-settings-properties"></a>49 de tabela. Propriedades de definições de controlo de caixa de combinação  

|**Propriedade**|**Descrição**|  
|-|-|  
|**Nome de variável de sequência de tarefas**|Utilize esta propriedade para configurar a variável de sequência de tarefas armazenar as informações recolhidas do utilizador. Se a sequência de tarefas variável:<br /><br /> -Ainda não existir, a variável de sequência de tarefas é criada e fornece definido como o valor do utilizador<br /><br /> -Já existe, o valor da variável de sequência de tarefas existente é substituído com o valor fornece ao utilizador|  
|**Nome a apresentar amigável visível na página de resumo**|Utilize esta propriedade para configurar o nome descritivo que aparece no **resumo** página do assistente. Este nome é utilizado para descrever o valor que foi guardado no **nome de variável de sequência de tarefas** propriedade para este controlo.|  
|**Foi desbloqueada**|Utilize esta propriedade para configurar se o utilizador é capaz de interagir com o controlo. Por predefinição, o controlo está activado. Este botão apresenta o estado do seguinte:<br /><br /> -                                  **Foi desbloqueada.** O controlo está ativado e os utilizadores podem introduzir informações utilizá-la.<br /><br /> - **Bloqueado.** O controlo está desativado e os utilizadores não conseguem introduzir informações utilizá-la.<br /><br /> **Tenha em atenção** se desativar um controlo (bloqueio), tem de fornecer as informações de controlo recolhido através da configuração de propriedades do MDT no CustomSettings.ini ou na base de dados do MDT. Caso contrário, o Assistente de UDI não irá recolher as informações necessárias e a implementação de UDI irá falhar.|  

####  <a name="LineControl"></a>Controlo de linha  
 Este controlo permite-lhe adicionar uma linha horizontal dividir uma parte da página do assistente personalizada de outro. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 50 tabela lista as propriedades de esquema para o **linha** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-50-line-control-layout-properties"></a>50 de tabela. Propriedades de esquema de controlo de linha  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** aumentar esta propriedade não aumenta a altura ou a largura da linha.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 O **linha** controlo não tem definições propriedades.  

####  <a name="LabelControl"></a>Controlo de etiqueta  
 Este controlo permite-lhe adicionar texto descritivo só de leitura para a página do assistente. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 51 tabela lista as propriedades de esquema para o **etiqueta** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-51-label-control-layout-properties"></a>51 de tabela. Propriedades de esquema do controlo de etiqueta  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Etiqueta**|Utilize esta propriedade para configurar o texto descritivo associado a este controlo.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é maior do que a largura do controlo, o texto é anexado e não apresentado.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é taller que a altura do controlo, o texto está anexado.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 O **etiqueta** controlo não tem definições propriedades.  

####  <a name="RadioControl"></a>Controlo de botões de opção  
 Este controlo permite-lhe selecionar uma opção de um grupo de dois ou mais opções. À semelhança de botões de opção tradicionais, pode agrupar dois ou mais destes controlos; em seguida, o utilizador pode selecionar uma das opções no grupo.  

 Um valor exclusivo é atribuído a cada botão de opção. O valor atribuído ao controlo de botão de opção selecionada é guardado na variável de sequência de tarefas configurada para este controlo.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 52 tabela lista as propriedades de esquema para o **botões de opção** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-52-radio-control-layout-properties"></a>52 de tabela. Propriedades de esquema do controlo de botões de opção  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Etiqueta**|Utilize esta propriedade para configurar o texto descritivo associado com o botão de opção.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é maior do que a largura do controlo, o texto é anexado e não apresentado.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no **etiqueta** propriedade é taller que a altura do controlo, o texto está anexado.|  
|**RadioGroup**|Utilize esta propriedade para o grupo dois ou mais botões de opção. Quando os botões de opção pertencem ao mesmo grupo, apenas um dos botões de opção dentro de um grupo pode ser selecionado.<br /><br /> Se precisar de vários grupos de botões de opção, configure esta propriedade para cada grupo de botões de opção correspondentes.|  
|**Valor**|Utilize esta propriedade para configurar o valor armazenado na variável de sequência de tarefas quando o botão de opção está selecionado.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 Propriedades das definições são utilizadas para configurar os dados apresentados inicialmente num controlo (o valor predefinido) e onde as informações recolhidas do utilizador é guardada. 53 tabela lista as propriedades de definições para o **botões de opção** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-53-radio-control-settings-properties"></a>53 de tabela. Propriedades de definições de controlo de botões de opção  

|**Propriedade**|**Descrição**|  
|-|-|  
|**Valor predefinido**|Utilize esta propriedade para configurar o valor predefinido para o controlo. Por predefinição, o valor é definido para o ID de controlo.|  
|**Nome de variável de sequência de tarefas**|Utilize esta propriedade para configurar a variável de sequência de tarefas armazenar as informações recolhidas do utilizador. Se a sequência de tarefas variável:<br /><br /> -Ainda não existir, a variável de sequência de tarefas é criada e fornece definido como o valor do utilizador<br /><br /> -Já existe, o valor da variável de sequência de tarefas existente é substituído com o valor fornece ao utilizador|  
|**Nome a apresentar amigável visível na página de resumo**|Utilize esta propriedade para configurar o nome descritivo que aparece no **resumo** página do assistente. Este nome é utilizado para descrever o valor que foi guardado no **nome de variável de sequência de tarefas** propriedade para este controlo.|  
|**Foi desbloqueada**|Utilize esta propriedade para configurar se o utilizador é capaz de interagir com o controlo. Por predefinição, o controlo está activado. Este botão apresenta o estado do seguinte:<br /><br /> -                                  **Foi desbloqueada.** O controlo está ativado e os utilizadores podem introduzir informações utilizá-la.<br /><br /> -                                  **Bloqueado.** O controlo está desativado e os utilizadores não conseguem introduzir informações utilizá-la.<br /><br /> **Tenha em atenção** se desativar um controlo (bloqueio), tem de fornecer as informações de controlo recolhido através da configuração de propriedades do MDT no CustomSettings.ini ou na base de dados do MDT. Caso contrário, o Assistente de UDI não irá recolher as informações necessárias e a implementação de UDI irá falhar.|  

####  <a name="BitmapControl"></a>Controlo de mapa de bits  
 Este controlo permite-lhe adicionar um gráfico de mapa de bits (*.bmp ficheiro) para a página do assistente personalizado. Este controlo não recolhe quaisquer valores de configuração, mas em vez disso, é utilizado para melhorar visualmente a IU.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 54 em que tabela lista as propriedades de esquema para o **mapa de bits** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-54-bitmap-control-layout-properties"></a>54 em tabela. Propriedades de esquema do controlo de mapa de bits  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o gráfico selecionado o **origem** propriedade é maior do que a largura do controlo, o gráfico está anexado.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o gráfico selecionado o **origem** propriedade é taller que a altura do controlo, o gráfico está anexado.|  
|**Origem**|Utilize esta propriedade para configurar o caminho completamente qualificado para o ficheiro *.bmp, incluindo o nome de ficheiro. O caminho para o ficheiro *.bmp é relativo à localização do Assistente de UDI (OSDSetupWizard.exe), que é um dos seguintes pastas (onde *mdt_tookit_package* é a localização do pacote do toolkit do MDT no Configuration Manager):<br /><br /> -                                  *mdt_tookit_package*\Tools\x86<br /><br /> -                                  *mdt_tookit_package*\Tools\x64<br /><br /> Para ver o gráfico quando pré-visualizar a página do assistente personalizado, também deve estar localizado o ficheiro *.bmp nas seguintes pastas (onde *mdt_install_folder* é a pasta onde instalou o MDT):<br /><br /> -                                  *mdt_install_folder*\Template\Distribution\Tools\x86<br /><br /> -                                  *mdt_install_folder* \Template\Distribution\Tools\x64|  

##### <a name="settings-properties"></a>Propriedades das definições  
 O **mapa de bits** controlo não tem definições propriedades.  

####  <a name="TextboxControl"></a>Controlo de caixa de texto  
 Este controlo permite-lhe introduzir o texto na página do assistente personalizado. O texto digitado neste controlo é guardado na variável de sequência de tarefas configurada para este controlo.  

##### <a name="layout-properties"></a>Propriedades de esquema  
 Propriedades do esquema são utilizadas para configurar as características de IU do controlo e são configuradas no **esquema** separador o UDI Wizard Designer. 55 tabela lista as propriedades de esquema para o **Textbox** controlar e fornece uma breve descrição de cada propriedade.  

### <a name="table-55-textbox-control-layout-properties"></a>55 de tabela. Propriedades de esquema do controlo de caixa de texto  

|**Propriedade**|**Descrição**|  
|-|-|  
|**X**|Utilize esta propriedade para configurar a posição horizontal do controlo.|  
|**Y**|Utilize esta propriedade para configurar a posição vertical do controlo.|  
|**Largura**|Utilize esta propriedade para configurar a largura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no controlo for maior do que a largura do controlo, o texto é anexado e não apresentado.|  
|**Altura**|Utilize esta propriedade para configurar a altura do controlo.<br /><br /> **Tenha em atenção** se o texto introduzido no controlo taller que a altura do controlo, o texto está anexado.|  

##### <a name="settings-properties"></a>Propriedades das definições  
 Propriedades das definições são utilizadas para configurar os dados que está inicialmente mostrado num controlo (o valor predefinido) e onde as informações recolhidas do utilizador são guardadas. 56 tabela lista as propriedades de definições para o **Textbox** controlar e fornece uma breve descrição de cada propriedade  

### <a name="table-56-textbox-control-settings-properties"></a>56 de tabela. Propriedades de definições de controlo de caixa de texto  

|**Propriedade**|**Descrição**|  
|-|-|  
|**Valor predefinido**|Utilize esta propriedade para configurar o valor predefinido para o controlo.|  
|**Nome de variável de sequência de tarefas**|Utilize esta propriedade para configurar a variável de sequência de tarefas armazenar as informações recolhidas do utilizador. Se a sequência de tarefas variável:<br /><br /> -Ainda não existir, a variável de sequência de tarefas é criada e fornece definido como o valor do utilizador<br /><br /> -Já existe, o valor da variável de sequência de tarefas existente é substituído com o valor fornece ao utilizador|  
|**Nome a apresentar amigável visível na página de resumo**|Utilize esta propriedade para configurar o nome descritivo que aparece no **resumo** página do assistente. Este nome é utilizado para descrever o valor que foi guardado no **nome de variável de sequência de tarefas** propriedade para este controlo.|  
|**Lista de validações atribuídos a este controlo**|Esta propriedade contém uma lista de validações utilizado para verificar se o conteúdo introduzido na caixa de texto.<br /><br /> É possível:<br /><br /> -Adicionar validações para a lista com o botão de sinal de adição azul imediatamente para a direita da lista de validações<br /><br /> -Editar validações na lista com o botão de lápis imediatamente para a direita da lista de validações<br /><br /> -Remover validações da lista utilizando a vermelho **X** botão imediatamente para a direita da lista de validações|  
|**Foi desbloqueada**|Utilize esta propriedade para configurar se o utilizador é capaz de interagir com o controlo. Por predefinição, o controlo está activado. Este botão apresenta o estado do seguinte:<br /><br /> - **Foi desbloqueada.** O controlo está ativado e os utilizadores podem introduzir informações utilizá-la.<br /><br /> -                                  **Bloqueado.** O controlo está desativado e os utilizadores não conseguem introduzir informações utilizá-la.<br /><br /> Nota:<br /><br /> **Tenha em atenção** se desativar um controlo (bloqueio), tem de fornecer as informações de controlo recolhido através da configuração de propriedades do MDT no CustomSettings.ini ou na base de dados do MDT. Caso contrário, o Assistente de UDI não irá recolher as informações necessárias e a implementação de UDI irá falhar.|  

###  <a name="UDITaskSequenceVariables"></a>Variáveis de sequência de tarefas UDI  
 As variáveis de sequência de tarefas nesta secção são utilizadas apenas em implementações de modo instalação (UDI). Além destas variáveis de sequência de tarefas, as seguintes variáveis de sequência de tarefas ZTI também sejam utilizadas pelo UDI e estão documentadas nos seus respetivas secções, anteriormente neste guia:  

-   [KeyboardLocale](#KeyboardLocale)  

-   [OSDComputerName](#OSDComputerName)  

-   [UILanguage](#UILanguage)  

-   [UserLocale](#UserLocale)  

####  <a name="OSDAddAdmin"></a>OSDAddAdmin  
 Esta variável de sequência de tarefas Especifica uma lista de contas de domínio ou contas locais para ser adicionado ao local incorporado grupo de administradores no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|*domain\account_name1; computer\account_name2*|O formato das contas para ser tornados membros do grupo Administradores no computador de destino no formato de *domínio \ conta* e separados por ponto e vírgula, onde *domínio* pode ser o nome de um ativo Domínio de diretório ou o nome do computador de destino.|  

|**Exemplo**|  
|-|  
|`OSDAddAdmin=domain\user01;Win7-01\LocalUser01`|  

####  <a name="OSDApplicationList"></a>OSDApplicationList  
 Esta variável de sequência de tarefas Especifica quais as aplicações que devem ser selecionadas por predefinição no **instalar Software** página do Assistente de configuração de implementação do sistema operativo (OSD).  

|**Valor**|**Descrição**|  
|-|-|
|*app_id1; app_id2*|Uma lista delimitada por ponto e vírgula da aplicação para ser selecionado por predefinição no **instalar Software** página do Assistente de configuração de implementação do sistema operativo (OSD); cada aplicação é representada por um ID de aplicação e separada por um ponto e vírgula. O ID de aplicação é derivado de **Id** atributo de cada aplicação no ficheiro UDIWizard_Config.xml. Excerpt seguinte de um ficheiro de UDIWizard_Config.xml, o sistema do Microsoft Office 2007 com SP2 aplicação tem um **Id** atributo **1**:<br /><br /> `<Application DisplayName="Office 2007 SP2" State="Disabled" Id="1">`|  

|**Exemplo**|  
|-|  
|`OSDApplicationList=2;3`|  

####  <a name="OSDArchitecture"></a>OSDArchitecture  
 Esta variável de sequência de tarefas Especifica a arquitetura de processador do sistema de operativo de destino para ser implementada.  

|**Valor**|**Descrição**|  
|-|-|
|x86|Sistema operativo de destino é um sistema de operativo de 32 bits.|  
|AMD64|Sistema operativo de destino é um sistema de operativo de 64 bits.|  

|**Exemplo**|  
|-|  
|`OSDArchitecture=amd64`|  

####  <a name="OSDBitlockerStatus"></a>OSDBitlockerStatus  
 Esta variável de sequência de tarefas Especifica se o BitLocker estiver ativado no computador de destino, a verificação de verificação prévia do BitLocker.  

|**Valor**|**Descrição**|  
|-|-|
|**PROTEGIDO**|O computador de destino com o BitLocker ativado.|  
|Não existe|Se o computador de destino não tenha o BitLocker ativado, em seguida, a variável de sequência de tarefas não existe.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDDiskPart"></a>OSDDiskPart  
 Esta variável de sequência de tarefas Especifica se a partição de disco de destino deve ser formatada.  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|A partição de disco de destino será formatada.|  
|**FALSO**|A partição de disco de destino não será formatada.|  

|**Exemplo**|  
|-|  
|`OSDDiskPart=TRUE`|  

####  <a name="OSDDomainName"></a>OSDDomainName  
 Esta variável de sequência de tarefas Especifica o nome do domínio ao qual o computador de destino será associado, se o computador estiver configurado para ser um membro de domínio.  

|**Valor**|**Descrição**|  
|-|-|
|*nome_domínio*|O nome do domínio ao qual o computador de destino será associado. Se tiver configurado o **computador** página do assistente no Assistente de configuração de implementação do sistema operativo (OSD) para ser **automática**, o valor nesta variável de sequência de tarefas tem de corresponder ao valores especificados no UDI Designer de assistente. Caso contrário, será apresentada a página do assistente.<br /><br /> Nota:<br /><br /> Esta variável de sequência de tarefas é necessário apenas quando estiver a criar uma nova conta de computador na UO. Se a conta de computador já existir, esta variável não é necessária.|  

|**Exemplo**|  
|-|  
|`OSDDomainName=domain01`|  

####  <a name="OSDDomainOUName"></a>OSDDomainOUName  
 Esta variável de sequência de tarefas Especifica o nome da UO no domínio ao qual a conta de computador de destino será criada quando o computador adere a um domínio.  

|**Valor**|**Descrição**|  
|-|-|
|*ou_name*|O nome da UO no domínio em que será criada a conta de computador<br /><br /> Nota:<br /><br /> Esta variável de sequência de tarefas é necessário apenas quando estiver a criar uma nova conta de computador na UO. Se a conta de computador já existir, esta variável não é necessária.|  

|**Exemplo**|  
|-|  
|`OSDDomainOUName=NewDeployOU`|  

####  <a name="OSDImageIndex2"></a>OSDImageIndex  
 Esta variável de sequência de tarefas Especifica o número de índice de sistema operativo de destino num ficheiro WIM.  

|**Valor**|**Descrição**|  
|-|-|
|*index_number*|O número de índice de destino, o que é começa com um número de índice de 1 para o sistema operativo primeiro no ficheiro WIM|  

|**Exemplo**|  
|-|  
|`OSDImageIndex=1`|  

####  <a name="OSDImageName"></a>OSDImageName  
 Esta variável de sequência de tarefas Especifica o nome da imagem do sistema operativo no ficheiro. wim selecionado no **seleção da imagem** caixa no [VolumePage](#VolumePage) página do assistente. A lista de imagens do sistema de operativo possíveis no **seleção da imagem** caixa está configurada no **valores da caixa de combinação imagem** lista o **caixa de combinação de imagem** secção sobre o [ VolumePage](#VolumePage) editor de página do assistente. O nome da imagem é configurado como parte de cada imagem no **valores da caixa de combinação imagem** lista.  

> [!NOTE]
>  **Tenha em atenção** esta variável de sequência de tarefas é definido pelo [VolumePage](#VolumePage) assistente e não deve ser configurado no ficheiro CustomSettings.ini, ou na base de dados do MDT. No entanto, esta variável de sequência de tarefas pode ser utilizado para definir condições para os passos de sequência de tarefas, conforme descrito na secção, "Configurar UDI tarefas sequências para implementar sistemas operativos diferentes", no documento MDT *utilizando o Microsoft Deployment Toolkit*.  

|**Valor**|**Descrição**|  
|-|-|
|*image_name*|O nome da imagem do sistema operativo no ficheiro. wim selecionado no **seleção da imagem** caixa no [VolumePage](#VolumePage) página do Assistente|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDJoinAccount"></a>OSDJoinAccount  
 Esta variável de sequência de tarefas Especifica a conta de acesso baseado em domínio utilizada para associar o computador de destino para o domínio especificado no **OSDDomainName** variável de sequência de tarefas. Esta variável de sequência de tarefas é necessário se o computador de destino será associado a um domínio.  

|**Valor**|**Descrição**|  
|-|-|
|*nome_conta*|O nome da conta utilizada para associar o computador de destino ao domínio no formato de *domínio \ conta*|  

|**Exemplo**|  
|-|  
|`OSDJoinAccount=domain\admin01`|  

####  <a name="OSDJoinPassword"></a>OSDJoinPassword  
 Esta variável de sequência de tarefas Especifica a palavra-passe para a conta de acesso baseado em domínio utilizada para associar o computador de destino para o domínio especificado no **OSDJoinAccount** variável de sequência de tarefas. Esta variável de sequência de tarefas é necessário se o computador de destino será associado a um domínio.  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|A palavra-passe da conta utilizada para associar ao domínio|  

|**Exemplo**|  
|-|  
|`OSDJoinPassword=P@ssw0rd10`|  

####  <a name="OSDLocalAdminPassword"></a>OSDLocalAdminPassword  
 Esta variável de sequência de tarefas Especifica a palavra-passe da conta de administrador local incorporada no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|*palavra-passe*|A palavra-passe de administrador local conta incorporada no computador de destino|  

|**Exemplo**|  
|-|  
|`OSDLocalAdminPassword=P@ssw0rd10`|  

####  <a name="OSDNetworkJoinType"></a>OSDNetworkJoinType  
 Esta variável de sequência de tarefas Especifica se o computador de destino é associado um domínio ou grupo de trabalho.  

|**Valor**|**Descrição**|  
|-|-|
|**0**|O computador de destino será associado um domínio.<br /><br /> Se selecionar esta opção e configurar a página do Assistente de configuração de implementação do sistema operativo (OSD) correspondente ao ser **automática**, também tem de fornecer valores para o **OSDJoinAccount**,  **OSDJoinPassword**, **OSDDomainName**, e **OSDDomainOUName** variáveis de sequência de tarefas em conformidade. Além disso, tem de selecionar **domínio** no **seleção predefinida** no painel de área de trabalho a **computador página** no UDI Wizard Designer.|  
|**1**|O computador de destino será associado um grupo de trabalho.<br /><br /> Se selecionar esta opção e configurar a página do Assistente de configuração de implementação do sistema operativo (OSD) correspondente ao ser **automática**, também tem de fornecer um valor para o **OSDWorkgroupName** sequência de tarefas variável. Além disso, tem de selecionar **grupo de trabalho** no **seleção predefinida** no painel de área de trabalho a **computador página** no UDI Wizard Designer.|  

|**Exemplo**|  
|-|  
|`OSDNetworkJoinType=0`|  

####  <a name="OSDSetupWizCancelled"></a>OSDSetupWizCancelled  
 Esta variável de sequência de tarefas Especifica se o utilizador cancelou o Assistente de configuração de implementação do sistema operativo (OSD).  

|**Valor**|**Descrição**|  
|-|-|
|**VERDADEIRO**|O utilizador cancelou o Assistente de configuração de implementação do sistema operativo (OSD).|  
|Não existe|Se o assistente não foi cancelado, a variável de sequência de tarefas não existe.|  

|**Exemplo**|  
|-|  
|Nenhum|  

####  <a name="OSDTargetDrive"></a>OSDTargetDrive  
 Esta variável de sequência de tarefas Especifica o volume de disco em que o sistema operativo de destino será implementado.  

|**Valor**|**Descrição**|  
|-|-|
|*disk_volume*|A designação de volume do disco|  

|**Exemplo**|  
|-|  
|`OSDTargetDrive=C:`|  

####  <a name="OSDWinPEWinDir"></a>OSDWinPEWinDir  
 Esta variável de sequência de tarefas Especifica a pasta na qual o sistema operativo Windows está atualmente instalado no computador de destino.  

|**Valor**|**Descrição**|  
|-|-|
|*windows_directory*|O diretório no qual está atualmente instalado o sistema operativo Windows|  

|**Exemplo**|  
|-|  
|`OSDWinPEWinDir=C:\Windows`|  

####  <a name="OSDWorkgroupName"></a>OSDWorkgroupName  
 Esta variável de sequência de tarefas Especifica o nome do grupo de trabalho ao qual o computador de destino será associado, se o computador estiver configurado para ser um membro do grupo de trabalho.  

|**Valor**|**Descrição**|  
|-|-|
|*workgroup_name*|O nome do grupo de trabalho ao qual o computador de destino será associado|  

|**Exemplo**|  
|-|  
|`OSDWorkgroupName=WORKGROUP01`|  

###  <a name="OSDResultsexeconfigFileElementValues"></a>Valores de elemento do ficheiro de OSDResults.exe.config  
 O programa de resultados de OSD, OSDResults.exe, é executado no final de uma implementação de UDI e apresenta os resultados do processo de implementação. O comportamento do programa de resultados de OSD pode ser personalizado ao modificar os valores de elemento do ficheiro OSDResults.exe.config. O ficheiro de OSDResults.exe.config é armazenado na Tools\OSDResults no pacote MDT na sequência de tarefas de instalação de unidade de utilizador.  

####  <a name="backgroundOpacity"></a>backgroundOpacity  
 Este elemento XML configura opaqueness da imagem de imagem de fundo de fundo especificada como uma percentagem decimal formatado no **backgroundWallpaper** elemento.  

|**Valor**|**Descrição**|  
|-|-|
|*opacity_percent*|A percentagem de opaqueness do **backgroundWallpaper** elemento especificado na percentagem formatada decimal — por exemplo, um valor de **0.8** designa opaqueness 80%.|  

|**Exemplo**|  
|-|  
|`<add key="backgroundOpacity" value="0.8"/>`|  

####  <a name="backgroundWallpaper"></a>backgroundWallpaper  
 Este elemento XML fornece o nome de ficheiro e caminho relativo para a imagem que é apresentado como o fundo do **resultados de OSD** caixa de diálogo. O caminho é relativo à pasta de Tools\OSDResults no pacote do MDT.  

|**Valor**|**Descrição**|  
|-|-|
|*caminho\\\file_name*|Inclui o caminho relativo e o nome de ficheiro da imagem de fundo; o caminho é delimitado com barras duplas (/ /).|  

|**Exemplo**|  
|-|  
|`<add key="backgroundWallpaper" value="images\\Wallpaper.jpg"/>`|  

####  <a name="completedText"></a>completedText  
 Este elemento XML fornece o texto que é apresentado no **resultados de OSD** caixa de diálogo quando a implementação está completa.  

|**Valor**|**Descrição**|  
|-|-|
|*texto*|O texto a apresentar no **resultados de OSD** caixa de diálogo no aspas marca quando implementação está completa|  

|**Exemplo**|  
|-|  
|`<add key="completedText" value="Deployment Complete"/>`|  

####  <a name="headerImagePath"></a>headerImagePath  
 Este elemento XML fornece o nome de ficheiro e caminho relativo para a imagem que é apresentado no cabeçalho de **resultados de OSD** caixa de diálogo. O caminho é relativo à pasta de Tools\OSDResults no pacote do MDT.  

|**Valor**|**Descrição**|  
|-|-|
|*caminho\\\file_name*|Inclui o caminho relativo e o nome de ficheiro da imagem de cabeçalho; o caminho é delimitado com barras invertidas duplas (\\\\).|  

|**Exemplo**|  
|-|  
|`<add key="headerImagePath" value="images\\Windows7_h_rgb.png"/>`|  

####  <a name="timeoutMinutes"></a>timeoutMinutes  
 Este elemento XML configura minutos a **OSD resultado** é apresentada a caixa de diálogo antes da caixa de diálogo é fechada automaticamente e o computador é reiniciado.  

|**Valor**|**Descrição**|  
|-|-|
|*Valor numérico não*|Abre o permanece de caixa de diálogo até **iniciar Windows** é clicado.|  
|*Valor negativo*|Abre o permanece de caixa de diálogo até **iniciar Windows** é clicado.|  
|**0**|Abre o permanece de caixa de diálogo até **iniciar Windows** é clicado.|  
|Incluir vírgula decimal|Abre o permanece de caixa de diálogo até **iniciar Windows** é clicado.|  
|**1 - 10080**|O número de minutos que será apresentada a caixa de diálogo, com um valor mínimo de 1 minuto e um valor máximo de 10080 minutos (1 semana).|  

|**Exemplo**|  
|-|  
|`<add key="timeoutMinutes" value="30"/>`|  

####  <a name="welcomeText"></a>welcomeText  
 Este elemento XML fornece o texto de boas-vindas que é apresentado no **resultados de OSD** caixa de diálogo.  

|**Valor**|**Descrição**|  
|-|-|
|*welcome_text*|O texto a apresentar no Bem-vindo a **resultados de OSD** caixa de diálogo aspas|  

|**Exemplo**|  
|-|  
|`<add key="welcomeText" value="Congratulations, Windows 7 has been successfully deployed to your computer."/>`|
