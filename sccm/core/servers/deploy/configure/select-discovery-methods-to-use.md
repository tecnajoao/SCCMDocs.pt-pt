---
title: "Selecione métodos de deteção para o Configuration Manager | Documentos do Microsoft"
description: "Reveja as considerações para os métodos da utilizar e os sites em que executá-los."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f72317cefab5ce8cad13b3120c3c93c856fa40b7
ms.openlocfilehash: 4b6be888be2ad6c1f5e7c0be33d9830bb870114e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Selecione os métodos de deteção a utilizar para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com êxito e eficiente utilizar a deteção para o System Center Configuration Manager, tem de considerar os métodos da utilizar e os sites em que executá-los.  

 Uma vez deteção pode gerar um grande volume de tráfego de rede e os registos de dados resultante de deteção (DDR) podem utilizar os recursos de CPU significativos durante o processamento, utilize apenas os métodos de deteção necessários para atingir os seus objetivos. Poderá iniciar utilizando apenas um ou dois métodos de deteção e, em seguida, ativar mais tarde métodos adicionais de forma controlada para expandir o nível de deteção no seu ambiente. As informações neste tópico podem ajudar a tomar as decisões informadas.  

 Para obter informações sobre os diferentes métodos de deteção, consulte o artigo [sobre métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Selecione os métodos de deteção de elementos diferentes  
 Para detetar recursos de utilizador ou de possíveis computadores de cliente do Configuration Manager, tem de ativar os métodos de deteção adequados. Pode utilizar diversas combinações de métodos de deteção para localizar recursos diferentes e para detetar informações adicionais sobre esses recursos. Os métodos de deteção que utilizar determinam o tipo de recursos que são detetados e os serviços do Configuration Manager e agentes que são utilizados no processo de deteção. Também determinam o tipo de informações sobre os recursos que é possível detetar.  

### <a name="discover-computers"></a>Detetar computadores   
Quando pretender detetar computadores, pode utilizar **deteção de sistema do Active Directory** ou **deteção de rede**.  

 Por exemplo, se pretender detetar recursos que podem instalar o cliente do Configuration Manager antes de utilizar a instalação de push de cliente, poderá executar a deteção de sistema do Active Directory. Utilizar este método, não só detetar o recurso, mas também detetar informações básicas mesmo expandidas informações acerca do mesmo a partir de serviços de domínio do Active Directory. Estas informações poderão ser úteis criar consultas complexas e coleções para utilizar para a atribuição de definições de cliente ou implementação de conteúdos.

Em alternativa, pode executar a deteção de rede e utilizar as opções da mesma para detetar o sistema operativo de recursos (necessários para utilizar posteriormente a instalação push do cliente). Deteção de rede fornece informações sobre a topologia de rede que não é possível obter com outros métodos de deteção. Este método não, no entanto, fornece quaisquer informações sobre o ambiente do Active Directory.

 Também existe um método denominado **deteção de Heartbeat**. É possível utilizar apenas a deteção de Heartbeat para forçar a deteção de clientes que tenha instalado com métodos diferentes da instalação push do cliente. No entanto, ao contrário de outros métodos de deteção, a deteção de Heartbeat não consegue detetar computadores que não tenham um cliente ativo do Configuration Manager. Devolve um conjunto limitado de informações, que se destina a manter um registo de base de dados existente, em vez de ser a base desse registo. As informações submetidas pela deteção de Heartbeat poderão não ser suficientes para criar consultas complexas ou coleções.  

 Se utilizar **deteção de grupo do Active Directory** para detetar a associação de um grupo especificado, poderá detetar informações limitadas do sistema ou do computador. Não substitui uma deteção completa de computadores, mas pode fornecer informações básicas. Estas informações são insuficientes para a instalação push do cliente.  

### <a name="discover-users"></a>Detetar utilizadores   
Quando pretender detetar informações sobre utilizadores, utilize **deteção de utilizador do Active Directory**. De forma semelhante à deteção de sistemas do Active Directory, este método Deteta utilizadores do Active Directory. Inclui informações básicas, além de informações expandidas do Active Directory. Pode utilizar estas informações para criar consultas complexas e coleções semelhantes de computadores.  

### <a name="discover-group-information"></a>Detetar informações de grupo   
Quando pretender detetar informações sobre grupos e associações a grupos, utilize **deteção de grupo do Active Directory**. Este método de deteção cria registos de recursos de grupos de segurança.  

 Pode utilizar este método para pesquisar um grupo específico do Active Directory e identificar os membros desse grupo, para além dos grupos aninhados que existam nesse grupo. Também pode utilizar este método para procurar grupos numa localização do Active Directory e pesquisar recursivamente cada contentor subordinado dessa localização nos serviços de domínio do Active Directory.  

 Este método de deteção também pode procurar as associações de grupos de distribuição. Pode identificar as relações de grupo de utilizadores e computadores.  

 Quando Deteta um grupo, também pode detetar informações limitadas acerca dos seus membros. Esta não substitui os Active Directory sistema ou o utilizador métodos de deteção, entanto. É geralmente é insuficiente para criar consultas complexas e coleções ou servir como a base de uma instalação de push de cliente.  

### <a name="discover-infrastructure"></a>Detetar a infraestrutura   
Existem dois métodos que pode utilizar para detetar a infraestrutura de rede, **deteção de floresta do Active Directory** e **deteção de rede**.  

 Utilize a deteção de floresta do Active Directory para procurar numa floresta do Active Directory para obter informações sobre sub-redes e configurações de site do Active Directory. Estas configurações podem, em seguida, ser automaticamente introduzidas com o Configuration Manager como localizações limite.  

 Quando pretender detetar a topologia da rede, utilize a deteção de rede. Enquanto outros métodos de deteção devolvem informações relacionadas com serviços de domínio do Active Directory e podem identificar a localização de rede atual de um cliente, não fornecem informações sobre a infraestrutura com base na topologia do router da rede e sub-redes.  

##  <a name="bkmk_shared"></a>Dados de deteção são partilhados entre os sites  
 Depois do Configuration Manager adiciona dados de deteção a uma base de dados, estes são rapidamente partilhados entre todos os sites na hierarquia. Uma vez que normalmente, não existe qualquer benefício em detetar as mesmas informações em vários sites na hierarquia, considere configurar uma instância única de cada método de deteção utilizada para executar num único site. É uma boa ideia efetuar esta ação em vez de executar várias instâncias de um único método em sites diferentes.  

 No entanto, para alguns ambientes poderá ser útil atribuir o mesmo método de deteção para ser executada em vários sites, cada uma com uma configuração e agenda separadas. Por exemplo, ao utilizar a deteção de rede, pode querer direcionar cada site para detetar a sua rede local, em vez de tentar detetar todas as localizações de rede através de uma WAN.

Se configurar várias instâncias dos mesmos métodos de deteção para ser executada em sites diferentes, planeie cuidadosamente a configuração de cada site. Pretender evitar que dois ou mais sites detetem os mesmos recursos a partir da sua rede ou do Active Directory. Isto pode consumir largura de banda de rede adicional e criar DDR duplicados.

A tabela seguinte identifica os sites em que pode configurar os diferentes métodos de deteção.  

|Método de deteção|Localizações suportadas|  
|----------------------|-------------------------|  
|Deteção de Florestas do Active Directory|Site de administração central<br /><br /> Site primário|  
|Deteção de Grupos do Active Directory|Site primário|  
|Deteção de Sistemas do Active Directory|Site primário|  
|Deteção de Utilizadores do Active Directory|Site primário|  
|Deteção de heartbeat<sup>1</sup>|Site primário|  
|Deteção de Redes|Site primário<br /><br /> Site Secundário|  

 <sup>1</sup> sites secundários não é possível configurar a deteção de Heartbeat mas podem receber o DDR de Heartbeat de um cliente.  

 Quando os sites secundários executam a deteção de rede, ou recebem DDRs da deteção de Heartbeat, transferem o DDR através da replicação baseada em ficheiros para o respetivo site primário principal. Isto acontece porque os sites primários apenas e os sites de administração central podem processar DDR. Para mais informações sobre como os DDR é processados, consulte o artigo [acerca de registos de dados de deteção](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Considerações sobre diferentes métodos de deteção  
 Uma vez que cada site server e ambiente de rede for diferente, é boa ideia limite as configurações iniciais de deteção. Em seguida, monitorize atentamente a capacidade processar os dados de deteção que são gerados cada servidor do site.  

Quando utiliza um **do Active Directory** método de deteção de sistemas, utilizadores ou grupos:  

-   Execute a deteção num site que tenha uma ligação de rede rápida aos controladores de domínio.  

-   Considere a topologia de replicação do Active Directory para garantir a deteção pode aceder às informações mais recentes.  

-   Considere o âmbito da configuração da deteção e limitar a deteção apenas aos localizações do Active Directory e os grupos que tiver de detetar.  

Se utilizar **deteção de rede**:  

-   Utilize uma configuração inicial limitada para identificar a topografia de rede.  

-   Depois de identificar a topografia de rede, configure a deteção de rede para executar em sites específicos centralizados áreas de rede que pretende detetar mais detalhadamente.  

Porque **deteção de Heartbeat** não é executada num site específico, não é necessário considerá-la no planeamento geral dos locais onde executar a deteção.  

##  <a name="bkmk_best"></a>Melhores práticas de deteção  
Para obter melhores resultados de deteção, recomendamos o seguinte:

 - **Executar a deteção de sistema do Active Directory e deteção de utilizador do Active Directory antes de executar a deteção de grupo do Active Directory.**  

 Quando a deteção de grupo do Active Directory identifica um computador ou o utilizador não detetado anteriormente como membro de um grupo, tenta detetar as informações básicas do utilizador ou do computador. Uma vez que a deteção de grupo do Active Directory não está otimizada para este tipo de deteção, este processo pode causar para ser executada lentamente. Além disso, a deteção de grupo do Active Directory identifica apenas as informações básicas sobre os utilizadores e computadores que Deteta e não criar um utilizador completo ou registo de deteção de computador. Ao executar a deteção de sistema do Active Directory e a deteção de utilizador do Active Directory, os atributos adicionais do Active Directory para cada tipo de objeto estão disponíveis. Como resultado, a deteção de grupo do Active Directory é executada com mais eficácia.  

- **Quando configurar a deteção de grupo do Active Directory, especifique apenas os grupos que utiliza com o Configuration Manager.**  

 Para ajudar a controlar a utilização de recursos pela deteção de grupo do Active Directory, especifique apenas os grupos que utiliza com o Configuration Manager. Isto acontece porque a deteção de grupo do Active Directory recursivamente cada grupo que Deteta para utilizadores, computadores e grupos aninhados. A procura de cada grupo aninhado pode expandir o âmbito da deteção de grupo do Active Directory e reduzir o desempenho. Além disso, ao configurar a deteção de diferenças para a deteção de grupo do Active Directory, o método de deteção monitoriza a existência de alterações de cada grupo. Este procedimento reduz ainda mais desempenho quando o método tem de procurar grupos desnecessários.  

- **Configure métodos de deteção com um intervalo maior entre deteções completas e um período mais frequente de deteção de diferenças.**  

 Uma vez que a deteção de diferenças utiliza menos recursos do que um ciclo de deteção completa e pode identificar recursos novos ou modificados no Active Directory, pode reduzir a frequência dos ciclos de deteção completa para serem realizadas semanalmente (ou menos). A deteção de diferenças para deteção de sistema do Active Directory, deteção de utilizador do Active Directory e deteção de grupo do Active Directory identifica quase todas as alterações de objetos do Active Directory e pode manter dados de deteção exatos de recursos.  

- **Execute métodos de deteção do Active Directory num site primário que tenha uma localização de rede mais próxima do controlador de domínio do Active Directory.**  

 Para melhorar o desempenho de deteção do Active Directory, é aconselhável a execução detetar um site primário que tem uma ligação de rede rápida aos controladores de domínio. Se executar o mesmo método de deteção do Active Directory em vários sites, configure cada método de deteção para evitar sobreposições. Ao contrário decorridos desde as versões do Configuration Manager, dados de deteção são partilhados entre os sites. Por conseguinte, não é necessário detetar as mesmas informações em vários sites. Para obter mais informações, consulte o artigo [dados de deteção são partilhados entre sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Execute a deteção de floresta do Active Directory apenas num site quando planear criar automaticamente limites a partir de dados de deteção.**  

 Se executar a deteção de floresta do Active Directory em mais do que um site numa hierarquia, é uma boa ideia ative apenas as opções criar automaticamente limites num único site. Isto acontece porque, quando a deteção de floresta do Active Directory é executada em cada site e cria limites, Configuration Manager não conseguir intercalar esses limites num único objeto de limites. Ao configurar a deteção de floresta do Active Directory para criar automaticamente limites em vários sites, o resultado pode ser objetos de limites duplicado na consola do Configuration Manager.  

