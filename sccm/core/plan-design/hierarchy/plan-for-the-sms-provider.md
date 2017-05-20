---
title: Planear o fornecedor de SMS | Documentos do Microsoft
description: Saiba mais sobre como o fornecedor de SMS ajuda-o a gerir o System Center Configuration Manager.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 11ac851696ce52642412ca29e4873679d50cf398
ms.openlocfilehash: 547dc39d5659c7c2e6f1ca670caddc127dbf22c4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Planear o Fornecedor de SMS para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir o System Center Configuration Manager, é utilizar uma consola do Configuration Manager que liga a uma instância do **fornecedor de SMS**. Por predefinição, instala um fornecedor de SMS no servidor do site quando instala um site de administração central ou site primário. 


##  <a name="BKMK_PlanSMSProv"></a> Acerca do Fornecedor de SMS  
 O fornecedor de SMS é um fornecedor de Windows Management Instrumentation (WMI) que atribui **ler** e **escrever** acesso à base de dados do Configuration Manager num site:  

-   Cada site de administração central e site primário precisa de, pelo menos, um Fornecedor de SMS. Se necessário, pode instalar fornecedores adicionais.  
-   O **Admins de SMS** grupo de segurança fornece acesso ao fornecedor de SMS. Gestor de configuração cria automaticamente este grupo no servidor do site e, em cada computador em que instalar uma instância do fornecedor de SMS.  

-   Os sites secundários não suportam o Fornecedor de SMS.  


Utilizadores administrativos do Configuration Manager utilizam um fornecedor de SMS acedam às informações armazenadas na base de dados. Para tal, os administradores podem utilizar a consola do Configuration Manager, Explorador de recursos, ferramentas e scripts personalizados. O fornecedor de SMS não interage com clientes do Configuration Manager. Quando uma consola do Configuration Manager estabelece ligação a um site, a consola do Configuration Manager consulta o WMI no servidor do site para localizar a instância do fornecedor de SMS para utilizar.  

 O fornecedor de SMS ajuda a impor a segurança do Configuration Manager. Devolve apenas as informações que o utilizador administrativo que está a executar a consola do Configuration Manager está autorizado a ver.  

> [!IMPORTANT]  
>  Quando um computador que suportar um fornecedor de SMS para um site estiver offline, as consolas do Configuration Manager não consegue ligar à base de dados desse site.  

 Para obter informações sobre como gerir o Fornecedor de SMS, veja [Gerir o Fornecedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) em [Modificar a infraestrutura do System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

## <a name="prerequisites-to-install-the-sms-provider"></a>Pré-requisitos para instalar o fornecedor de SMS  

 Para suportar o Fornecedor de SMS:  

-   O computador tem de estar num domínio que possua uma relação de fidedignidade bilateral com o servidor do site e os sistemas de sites da base de dados.  

-   O computador não pode ter uma função de sistema de sites com origem noutro site.  

-   O computador não pode ter um Fornecedor de SMS com origem em nenhum site.  

-   O computador tem de executar um sistema operativo que seja suportado para um servidor de site.  

-   O computador tem de ter pelo menos 650 MB de espaço livre em disco para suportar os componentes do Windows Automated Deployment Kit (Windows ADK) que são instalados com o fornecedor de SMS. Para obter mais informações sobre o Windows ADK e o Fornecedor de SMS, veja [Requisitos de Implementação do Sistema Operativo do Fornecedor de SMS](#BKMK_WAIKforSMSProv) neste tópico.  

##  <a name="bkmk_location"></a> Localizações do Fornecedor de SMS  
 Quando instala um site, instalar automaticamente o primeiro fornecedor de SMS para o site. Pode especificar qualquer uma das seguintes localizações suportadas para o Fornecedor de SMS:  

-   O computador do servidor do site  

-   O computador da base de dados do site  

-   Um computador de classe do servidor que não contenha um fornecedor de SMS ou uma função de sistema de sites a partir de um site diferente  


Para ver as localizações de cada fornecedor de SMS instalado num site, selecione o **geral** separador do site **propriedades** caixa de diálogo.  

 Cada Fornecedor de SMS suporta ligações simultâneas a partir de múltiplos pedidos. Os únicos limites destas ligações são o número de ligações de servidor que estão disponíveis no computador do Fornecedor de SMS e os recursos disponíveis no computador do Fornecedor de SMS para dar resposta aos pedidos de ligação.  

 Após a instalação de um site, pode executar novamente o Programa de Configuração no servidor do site para alterar a localização de um Fornecedor de SMS existente ou para instalar Fornecedores de SMS adicionais no mesmo site. Só pode instalar um Fornecedor de SMS num computador e um computador não pode instalar um Fornecedor de SMS a partir de mais do que um site.  

 Utilize as informações que se seguem para identificar as vantagens e desvantagens da instalação de um Fornecedor de SMS em cada localização suportada:  

 **Servidor de site do Configuration Manager**  

-   **Vantagens:**  

    -   O Fornecedor de SMS não utiliza os recursos do sistema do computador da base de dados do site.  

    -   Esta localização pode proporcionar melhor desempenho do que um Fornecedor de SMS localizado num computador que não o servidor do site ou o computador da base de dados do site.  

-   **Desvantagens:**  

    -   O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações do servidor do site.  


**O SQL Server que aloja a base de dados do site**  

-   **Vantagens:**  

    -   O Fornecedor de SMS não utiliza recursos do sistema de sites no servidor do site.  

    -   Esta localização pode proporcionar o melhor desempenho das três localizações, desde que estejam disponíveis recursos suficientes no servidor.  

-   **Desvantagens:**  

    -   O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações de base de dados do site.  

    -   Se a base de dados do site estiver alojada numa instância agrupada do SQL Server, não é possível utilizar esta localização.  


**Um computador que não o servidor do site ou o computador da base de dados do site**  

-   **Vantagens:**  

    -   O Fornecedor de SMS não utiliza recursos do computador do servidor do site ou da base de dados do site.  

    -   Este tipo de localização permite-lhe implementar Fornecedores de SMS adicionais para proporcionar uma elevada disponibilidade das ligações.  

-   **Desvantagens:**  

    -   O desempenho do fornecedor de SMS poderá ser reduzido devido à atividade de rede adicional que é necessário para coordenar as operações com o servidor do site e o computador de base de dados do site.  

    -   Este servidor tem de estar sempre acessível ao computador de base de dados do site e em todos os computadores com a consola do Configuration Manager instalada.  

    -   Esta localização pode utilizar recursos de sistema que, em condições normais, estariam dedicados a outros serviços.  

##  <a name="BKMK_SMSProvLanguages"></a>Informações sobre idiomas do fornecedor de SMS  
 O Fornecedor de SMS funciona independentemente do idioma de apresentação do computador onde está instalado.  

 Quando um utilizador administrativo ou dados de pedidos de processo do Configuration Manager, utilizando o fornecedor de SMS, o fornecedor de SMS tenta devolver os dados num formato que corresponda ao idioma do sistema operativo do computador que efetuou.

A forma como o mesmo tenta a corresponder ao idioma é pouco indireta. O Fornecedor de SMS não traduz as informações de um idioma para outro. Em vez disso, quando os dados forem devolvidos para apresentação na consola do Configuration Manager, o idioma de apresentação dos dados dependerá da origem do objeto e do tipo de armazenamento.  

 Quando os dados de um objeto são armazenados na base de dados, os idiomas que irão estar disponíveis dependem dos seguintes fatores:  

-   Os objetos criados pelo Gestor de configuração são armazenados na base de dados utilizando o suporte para múltiplos idiomas. O objeto é armazenado utilizando os idiomas que se encontram configurados no local onde o objeto é criado quando o Programa de Configuração é executado. Estes objetos são apresentados na consola do Configuration Manager no idioma de apresentação do computador que efetuou, quando esse idioma esteja disponível para o objeto. Se não for possível visualizar o objeto no idioma de apresentação do computador que efetuou o pedido, será apresentado no idioma predefinido, que é o inglês.  

-   Os objetos criados pelo utilizador administrativo são armazenados na base de dados no idioma que foi utilizado para criar o objeto. Estes objetos são apresentados na consola do Configuration Manager neste mesmo idioma. Estes não podem ser convertidos pelo fornecedor de SMS e não tem várias opções de idioma.  

##  <a name="BKMK_MultiSMSProv"></a> Utilizar vários Fornecedores de SMS  
 Após um site concluir a instalação, poderá instalar Fornecedores de SMS adicionais para o site. Para instalar fornecedores de SMS adicionais, execute a configuração do Configuration Manager no servidor do site. Pondere a instalação de Fornecedores de SMS adicionais, caso se verifique alguma das seguintes situações:  

-   Terá de vários utilizadores administrativos que executam uma consola do Configuration Manager e ligam a um site ao mesmo tempo.  

-   Irá utilizar o SDK do Configuration Manager ou outros produtos, que podem introduzir chamadas frequentes ao fornecedor de SMS.  

-   Pretende assegurar uma elevada disponibilidade do Fornecedor de SMS.  


Quando se encontram instalados vários fornecedores de SMS num site e é efetuado um pedido de ligação, o site atribui aleatoriamente cada novo pedido de ligação para um fornecedor de SMS instalado. Não pode especificar a localização do Fornecedor de SMS a utilizar para uma sessão de ligação específica.  

> [!NOTE]  
>  Considere as vantagens e desvantagens de cada localização de fornecedor de SMS. Saldo estes considerações com as informações que não é possível controlar qual o fornecedor de SMS é utilizado para cada nova ligação.  

Por exemplo, quando liga uma consola do Configuration Manager pela primeira vez a um site, a ligação consulta o WMI no servidor do site para identificar uma instância do fornecedor de SMS que a consola irá utilizar. Esta instância específica do fornecedor de SMS continuará a ser utilizada pela consola do Configuration Manager até que termine a sessão de consola do Configuration Manager. Caso a sessão termine porque o computador do fornecedor de SMS ficou indisponível na rede, quando voltar a ligar a consola do Configuration Manager, o site simplesmente repete a tarefa de identificar uma instância do fornecedor de SMS para ligar a. É possível que seja atribuído ao mesmo computador do Fornecedor de SMS, mas que este não esteja disponível. Se isto ocorrer, pode tentar restabelecer a ligação de consola do Configuration Manager até que seja atribuído um computador fornecedor de SMS disponível.  

##  <a name="BKMK_AboutSMSAdmins"></a> Acerca do grupo Admins de SMS  
 Pode utilizar o grupo Admins de SMS para fornecer aos utilizadores administrativos acesso ao Fornecedor de SMS. O grupo é automaticamente criado no servidor do site quando o site é instalado, bem como em cada computador que instalar um Fornecedor de SMS. Seguem-se informações adicionais sobre o grupo Admins de SMS:  

-   Caso o computador seja um servidor membro, o grupo Admins de SMS será criado como um grupo local.  

-   Caso o computador seja um controlador de domínio, o grupo Admins de SMS será criado como um grupo local de domínio.  

-   Caso o Fornecedor de SMS seja desinstalado de um computador, o grupo Admins de SMS não será removido do computador.  


Para que um utilizador possa estabelecer uma ligação com êxito a um Fornecedor de SMS, a respetiva conta de utilizador tem de ser membro do grupo Admins de SMS. Cada utilizador administrativo que configurar na consola do Configuration Manager é automaticamente adicionado ao grupo Admins de SMS em cada servidor de site e para cada computador fornecedor de SMS da hierarquia. Quando elimina um utilizador administrativo a partir da consola do Configuration Manager, esse utilizador é removido do grupo de Admins de SMS em cada servidor do site e em cada computador fornecedor de SMS da hierarquia.  

Depois de um utilizador efetua uma ligação com êxito para o fornecedor de SMS, a administração baseada em funções determina quais do Configuration Manager recursos que o utilizador pode aceder ou gerir.  

Pode ver e configurar as permissões e de direitos do grupo Admins de SMS, utilizando o snap-in MMC de controlo WMI. Por predefinição, **Todos** tem as permissões **Executar Métodos**, **Escrita do Fornecedor**e **Ativar Conta** . Após um utilizador estabelecer a ligação ao fornecedor de SMS, esse utilizador é concedido acesso aos dados da base de dados do site, com base nos seus direitos de segurança administrativa baseados na função, tal como definido na consola do Configuration Manager. O grupo Admins de SMS é concedido explicitamente **ativar conta** e **ativar remoto** permissões a **root\sms.** espaço de nomes.  

> [!NOTE]  
>  Cada utilizador administrativo que utilize uma consola remota do Configuration Manager necessita de permissões de ativação remota DCOM no computador do servidor de site e no computador do fornecedor de SMS. Embora possa atribuir estes direitos a qualquer utilizador ou grupo, é uma boa ideia conceder-lhes o grupo Admins de SMS para simplificar a administração. Para obter mais informações, veja a secção [Configurar permissões de DCOM para consolas remotas do Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) do tópico [Modificar a infraestrutura do System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  


##  <a name="BKMK_SMSProvNamespace"></a>Sobre o espaço de nomes do fornecedor de SMS  
A estrutura do Fornecedor de SMS é definida pelo esquema WMI. Espaços de nomes do esquema descrevem a localização dos dados do Configuration Manager dentro do esquema do fornecedor de SMS. A seguinte tabela contém alguns dos espaços de nomes comuns que são utilizados pelo Fornecedor de SMS.  

|Espaço de nomes|Descrição|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;código do site\>*|O fornecedor de SMS, que é amplamente utilizado pela consola do Configuration Manager, Explorador de recursos, ferramentas do Configuration Manager e scripts.|  
|Root\SMS\SMS_ProviderLocation|A localização dos computadores de fornecedor de SMS para um site.|  
|Root\CIMv2|A localização inventariada para as informações de espaço de nomes WMI durante o inventário de hardware e software.|  
|Root\CCM|Políticas de configuração de cliente do Configuration Manager e os dados de cliente.|  
|root\CIMv2\SMS|A localização das classes que são recolhidos pelo agente de cliente de inventário de relatório de inventário. Estas definições são compiladas pelos clientes durante a avaliação da política de computador e baseiam-se a configuração de definições de cliente para o computador.|  

##  <a name="BKMK_WAIKforSMSProv"></a>Requisitos de implementação do sistema operativo para o fornecedor de SMS  
O computador onde irá instalar uma instância do fornecedor de SMS tem de ter a versão necessária do Windows ADK que requer a versão do Configuration Manager que está a utilizar.  

 -   Por exemplo, a versão 1511 do Configuration Manager requer a versão do Windows 10 RTM (10.0.10240) do Windows ADK.  

 -   Para obter mais informações sobre este requisito, consulte o artigo [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

Quando gerir implementações do sistema operativo, o Windows ADK permite ao fornecedor de SMS executar várias tarefas, tais como:  

-   Ver detalhes do ficheiro WIM.  

-   Adicione ficheiros de controlador a imagens de arranque existentes.  

-   Crie de arranque. Ficheiros ISO.  


A instalação do Windows ADK pode precisar de até 650 MB de espaço livre em disco em cada computador que instala o Fornecedor de SMS. Este requisito de espaço em disco elevada é necessário para o Configuration Manager para instalar as imagens de arranque do Windows PE.  
