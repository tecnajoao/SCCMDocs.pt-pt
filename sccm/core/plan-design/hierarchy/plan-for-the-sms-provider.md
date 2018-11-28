---
title: Planear o Fornecedor de SMS
titleSuffix: Configuration Manager
description: Saiba mais sobre a função de sistema de sites do fornecedor de SMS no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 024714c564036cd61a6c1340724aa3b9cad782d2
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456401"
---
# <a name="plan-for-the-sms-provider"></a>Planear o Fornecedor de SMS 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir o Gestor de configuração, utilizar uma consola do Configuration Manager que se liga a uma instância do **fornecedor de SMS**. Por predefinição, instala um fornecedor de SMS no servidor do site quando instala um site de administração central ou site primário. 



##  <a name="BKMK_PlanSMSProv"></a> Acerca do Fornecedor de SMS  

O fornecedor de SMS é um fornecedor de Windows Management Instrumentation (WMI) que atribui **ler** e **escrever** acesso à base de dados do Configuration Manager num site.  

- Cada site de administração central e site primário precisa de, pelo menos, um Fornecedor de SMS. Se necessário, pode instalar fornecedores adicionais.  

- O **Admins de SMS** grupo de segurança fornece acesso ao fornecedor de SMS. Gestor de configuração cria automaticamente este grupo no servidor do site e em cada computador onde instala uma instância do fornecedor de SMS. Para obter mais informações, consulte [Admins de SMS](/sccm/core/plan-design/hierarchy/accounts#sms-admins).  

- Os sites secundários não suportam a função de fornecedor de SMS.  

Os utilizadores administrativos do Configuration Manager utilizam um fornecedor de SMS para aceder às informações armazenadas na base de dados. Para fazer isso, os administradores podem utilizar a consola do Configuration Manager, Explorador de recursos, ferramentas e scripts personalizados. O fornecedor de SMS não interage com clientes do Configuration Manager. Quando uma consola do Configuration Manager se liga a um site, consulta o WMI no servidor do site para localizar a instância do fornecedor de SMS a utilizar.  

O fornecedor de SMS ajuda a impor a segurança do Configuration Manager. Devolve apenas as informações que o utilizador da consola estiver autorizado a ver.  

> [!IMPORTANT]  
>  Quando cada instância do fornecedor de SMS para um site estiver offline, as consolas do Configuration Manager não consegue ligar ao site.  

 Para obter mais informações sobre como gerir o fornecedor de SMS, consulte [gerir o fornecedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).  



## <a name="installation-prerequisites"></a>Pré-requisitos de instalação  

 Para suportar o fornecedor de SMS, o servidor de destino tem de cumprir os seguintes pré-requisitos:  

-   Num domínio que tenha uma relação de confiança bilateral com o servidor de site e os sistemas de sites da base de dados  

-   Não pode ter uma função de sistema de sites de um site diferente  

-   Já não pode ter um fornecedor de SMS de qualquer site  

-   Executar uma versão suportada do SO  

-   Pelo menos, 650 MB de espaço livre em disco para suportar os componentes do Windows ADK. Para obter mais informações sobre o Windows ADK e o fornecedor de SMS, consulte [requisitos de implementação do sistema operacional](#BKMK_WAIKforSMSProv).  



##  <a name="bkmk_location"></a> localizações  

Quando instala um site, instalar automaticamente o primeiro fornecedor de SMS para o site. Pode especificar qualquer uma das seguintes localizações suportadas para o Fornecedor de SMS:  

-   O servidor do site  

-   O servidor de base de dados do site  

-   Outro servidor, que se adequa a [os pré-requisitos de instalação](#installation-prerequisites)  


Para ver as localizações de cada fornecedor de SMS para um site: 

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e, em seguida, selecione o **Sites** nó.  

2. Selecione o site pretendido na lista e, em seguida, escolha **propriedades** na faixa de opções.  

3. Na **gerais** separador do site **propriedades**, ver o **localização do fornecedor de SMS** campo.    


Cada Fornecedor de SMS suporta ligações simultâneas a partir de múltiplos pedidos. Os únicos limites destas ligações são o número de ligações de servidor que estão disponíveis para Windows e os recursos disponíveis no servidor para pedidos de ligação.  

Depois de instalar um site, pode executar novamente a configuração do Configuration Manager no servidor do site. Utilize a configuração para alterar a localização de um fornecedor de SMS existente ou para instalar fornecedores de SMS adicionais no mesmo site. Instale apenas um fornecedor de SMS num computador. Um computador não é possível alojar um fornecedor de SMS de mais de um site.  


### <a name="choosing-a-location"></a>Escolher uma localização 

As secções seguintes descrevem as vantagens e desvantagens da instalação de um fornecedor de SMS em cada localização suportada:  

#### <a name="configuration-manager-site-server"></a>Servidor de site do Configuration Manager

- **Vantagens:**  

    -   O fornecedor de SMS não utiliza os recursos do sistema do computador de base de dados do site.  

    -   Esta localização pode proporcionar melhor desempenho do que um Fornecedor de SMS localizado num computador que não o servidor do site ou o computador da base de dados do site.  

- **Desvantagens:**  

    -   O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações do servidor do site.  


#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server que aloja a base de dados do site

- **Vantagens:**  

    -   O fornecedor de SMS não utiliza recursos do sistema no servidor do site.  

    -   Esta localização pode proporcionar o melhor desempenho das três localizações, desde que estejam disponíveis recursos suficientes no servidor.  

- **Desvantagens:**  

    -   O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações de base de dados do site.  

    -   Se a base de dados do site estiver alojada numa instância em cluster do SQL Server, não é possível utilizar esta localização.  


#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Computador que não o servidor do site ou servidor de base de dados do site

- **Vantagens:**  

    -   Fornecedor de SMS não utiliza o servidor do site ou de recursos de sistema de banco de dados do site.  

    -   Este tipo de localização permite-lhe implementar Fornecedores de SMS adicionais para proporcionar uma elevada disponibilidade das ligações.  

- **Desvantagens:**  

    -   O desempenho do fornecedor de SMS poderá ser reduzido. Este comportamento é devido à atividade de rede adicional que é precisa para coordenar com o servidor de site e o computador de base de dados do site.  

    -   Este servidor tem de estar sempre acessível ao servidor de base de dados do site e a todos os computadores com a consola do Configuration Manager instalada.  

    -   Esta localização pode utilizar recursos de sistema que, em condições normais, estariam dedicados a outros serviços.  



## <a name="bkmk_auth"></a> Autenticação
<!--1357013-->

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. Aplica-se a todos os componentes que aceder ao fornecedor de SMS. Por exemplo, a consola do Configuration Manager, os métodos SDK e cmdlets do Windows PowerShell. 


### <a name="configure-authentication"></a>Configurar a autenticação

Para configurar esta definição, primeiro inicie sessão no Windows com o nível de autenticação pretendido. 

> [!Important]  
> Esta configuração é uma definição ao nível da hierarquia. Antes de alterar esta definição, certifique-se de que todos os administradores do Configuration Manager podem iniciar sessão no Windows com o nível de autenticação necessária. 

Para configurar esta definição, utilize os seguintes passos:

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2. Selecione **definições de hierarquia** na faixa de opções.  

3. Mude para o **autenticação** separador. Selecione o desejado [nível de autenticação](#authentication-levels)e, em seguida, selecione **OK**.  

    - Apenas quando necessário, selecione **adicionar** para excluir utilizadores ou grupos específicos. Para obter mais informações, consulte [exclusões](#exclusions).  


### <a name="authentication-levels"></a>Níveis de autenticação

Os seguintes níveis estão disponíveis:

- **Autenticação do Windows**: Exigir a autenticação com credenciais de domínio do Active Directory. Esta definição é o comportamento anterior e a predefinição atual. Quando atualizar o site, não há nenhuma alteração para o nível de autenticação.  

- **Autenticação de certificados**: Exigir a autenticação com um certificado válido emitido por uma autoridade de certificação fidedigna PKI. Não configure este certificado no Configuration Manager. O Configuration Manager requer que o administrador ser tem sessão iniciada no Windows utilizando o PKI.  

- **Windows Hello para autenticação de negócios**: Exigir a autenticação com a autenticação de dois fatores forte, que está associada a um dispositivo e utiliza a biometria ou um PIN. Pode utilizar o Configuration Manager para gerir e implementar o Windows Hello para políticas empresariais. Para obter mais informações, consulte [Windows Hello para empresas](/sccm/protect/deploy-use/windows-hello-for-business-settings).  


### <a name="exclusions"></a>Exclusões

Partir do **autenticação** separador das definições de hierarquia, também pode excluir certos usuários ou grupos. Utilize esta opção com moderação. Por exemplo, quando utilizadores específicos requerem acesso à consola do Configuration Manager, mas não é possível autenticar para o Windows no nível necessário. Também poderá ser necessário para a automatização ou serviços que são executados sob o contexto de uma conta do sistema.



##  <a name="BKMK_SMSProvLanguages"></a> Informações acerca dos idiomas do fornecedor de SMS  

O fornecedor de SMS funciona independentemente do idioma de apresentação do servidor em que instalar.  

Quando um utilizador administrativo ou dados de pedidos de processo do Configuration Manager utilizando o fornecedor de SMS, ele tenta devolver os dados num formato que corresponda ao idioma do SO do computador que efetuou.

A forma como ele tenta corresponder o idioma é indireto. O fornecedor de SMS não traduz as informações de um idioma para outro. Ao retornar dados para exibição na consola do Configuration Manager, o idioma de apresentação dos dados dependerá da origem do objeto e do tipo de armazenamento.  

Quando o Configuration Manager armazene os dados para um objeto na base de dados, os idiomas disponíveis dependem dos seguintes fatores:  

-   Gestor de configuração armazena objetos que cria ao utilizar o suporte para vários idiomas. Armazena o objeto da base de dados do site utilizando os idiomas que configurou para o site, quando executar a configuração. Consola do Configuration Manager apresenta esses objetos no idioma de apresentação do computador que, quando esse idioma está disponível para o objeto. Se a consola não é possível apresentar o objeto no idioma de apresentação do computador que efetuou, ele exibe o objeto no idioma padrão, que é o inglês.  

-   Gestor de configuração armazena objetos criados por um utilizador administrativo através da linguagem que foi utilizada para criar o objeto. Estes objetos são apresentados na consola do Configuration Manager neste mesmo idioma. O fornecedor de SMS não pode transformá-los e eles não têm opções de idiomas múltiplos.  



##  <a name="BKMK_MultiSMSProv"></a> Utilizar vários Fornecedores de SMS  

 Após um site concluir a instalação, poderá instalar Fornecedores de SMS adicionais para o site. Para instalar fornecedores de SMS adicionais, execute a configuração do Configuration Manager no servidor do site. 

Considere a instalação de fornecedores de SMS adicionais quando se verificar qualquer um dos seguintes procedimentos:  

- Número de utilizadores administrativo que tem de utilizar a consola do Configuration Manager e ligar a um site ao mesmo tempo.  

- Utilize o SDK do Configuration Manager ou outros produtos podem de apresentarem chamadas frequentes ao fornecedor de SMS.  

- Tem um requisito de negócio para elevada disponibilidade do fornecedor de SMS.  

Quando instalar múltiplos fornecedores de SMS num site e é feito um pedido de ligação, o site atribui aleatoriamente cada novo pedido de ligação para um fornecedor de SMS instalado. Não é possível especificar o fornecedor de SMS a utilizar com uma sessão de ligação específica.  

> [!NOTE]  
>  Considere as vantagens e desvantagens de cada localização do fornecedor de SMS. Para obter mais informações, consulte [localizações](#bkmk_location). Saldo estas considerações com as informações que não é possível controlar qual o fornecedor de SMS é utilizado para cada nova ligação.  

Quando liga uma consola do Configuration Manager pela primeira vez a um site, a ligação consulta o WMI no servidor do site. Esta consulta identifica uma instância do fornecedor de SMS que utiliza a consola. Esta instância específica do fornecedor de SMS continuará a ser utilizada pela consola até que termine a sessão. Se a sessão termine porque o servidor do fornecedor de SMS não está disponível na rede, quando voltar a ligar a consola ao site, se repete a consulta inicial. É possível que o site atribui a mesma instância do fornecedor de SMS que não está disponível. Se este comportamento ocorre, tente voltar a ligar a consola até que o site retorne um fornecedor de SMS disponível.  



##  <a name="BKMK_SMSProvNamespace"></a> Sobre o espaço de nomes do fornecedor de SMS  

O esquema WMI do Configuration Manager define a estrutura do fornecedor de SMS. Espaços de nomes do esquema descrevem a localização de dados do Configuration Manager no esquema do fornecedor de SMS. A tabela seguinte contém alguns dos espaços de nomes comuns que utiliza o fornecedor de SMS:  

|Espaço de nomes|Descrição|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|O fornecedor de SMS, que é amplamente utilizado pela consola do Configuration Manager, Explorador de recursos, ferramentas do Configuration Manager e scripts.|  
|`Root\SMS\SMS_ProviderLocation`|A localização dos computadores de fornecedor de SMS para um site.|  
|`Root\CIMv2`|A localização inventariada para as informações de espaço de nomes WMI durante o inventário de hardware e software.|  
|`Root\CCM`|As políticas de configuração do cliente do Configuration Manager e os dados de cliente.|  
|`Root\CIMv2\SMS`|A localização de classes que o agente de cliente de inventário recolhe de relatório de inventário. Os clientes compilam estas definições durante a avaliação da política de computador. Estas definições baseiam-se a configuração de definições de cliente para o computador.|  



##  <a name="BKMK_WAIKforSMSProv"></a> Requisitos de implementação do SO

O computador onde instala uma instância do fornecedor de SMS requer uma versão suportada do Windows ADK.  

Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura para implementação do SO](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10) e [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

Quando gerir implementações do sistema operacional, o Windows ADK permite ao fornecedor de SMS executar várias tarefas, tais como:  

-   Ver detalhes do ficheiro WIM  

-   Adicionar ficheiros de controladores a imagens de arranque existentes  

-   Criar arquivos ISO de arranque  


A instalação do Windows ADK pode precisar de até 650 MB de espaço livre em disco em cada computador que instala o Fornecedor de SMS. Este requisito de espaço de disco elevados é necessário para o Configuration Manager para instalar as imagens de arranque do Windows PE.  
