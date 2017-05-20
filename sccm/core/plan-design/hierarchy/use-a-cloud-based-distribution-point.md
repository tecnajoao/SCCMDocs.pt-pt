---
title: "Ponto de distribuição baseado na nuvem | Documentos do Microsoft"
description: "Saiba mais sobre as configurações e as limitações à utilização de um ponto de distribuição baseado na nuvem com o System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 489f38d3f88391e42b5271c03151203d22b26d9e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um ponto de distribuição baseado na nuvem é um ponto de distribuição do System Center Configuration Manager que está alojado no Microsoft Azure. As informações que se seguem destinam-se a ajudá-lo a saber mais sobre as configurações e limitações da utilização de um ponto de distribuição baseado na nuvem.

Depois de ter instalado um site primário e estão prontos para instalar um ponto de distribuição baseado na nuvem, consulte o artigo [instalar pontos de distribuição baseado na nuvem no Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planear a utilização de um ponto de distribuição baseado na nuvem
Quando utilizar um ponto de distribuição baseado na nuvem, pode:  

-   **Configurar definições de cliente** para permitir aos utilizadores e dispositivos aceder ao conteúdo.  

-   **Especifique um site primário para gerir a transferência de conteúdo** ao ponto de distribuição.  

-   **Especificar limiares** para a quantidade de conteúdo que pretende armazenar no ponto de distribuição e a quantidade de conteúdo que pretende permitir que os clientes transfiram a partir do ponto de distribuição.  


Com base nos limiares que configura, o Configuration Manager pode emitir alertas para avisá-lo quando a quantidade combinada do conteúdo armazenado no ponto de distribuição se aproxima da quantidade de armazenamento especificada ou quando as transferências de dados de clientes se aproximam dos limiares definidos.  

Pontos de distribuição baseado na nuvem suportam várias funcionalidades tht são também ser oferecidas pelos pontos de distribuição no local:  

-   Gerir os pontos de distribuição baseado na nuvem individualmente ou como membros da distribuição grupos de pontos.  

-   Pode utilizar um ponto de distribuição baseado na nuvem como uma localização de conteúdo de contingência.  

-   Receberá suporte tanto para clientes baseados na intranet como baseados na Internet.  


Pontos de distribuição baseado na nuvem fornecem as seguintes vantagens adicionais:  

-   Conteúdo que é enviado para um ponto de distribuição baseado na nuvem é encriptado pelo Configuration Manager antes do Configuration Manager envia-a para o Azure.  

-   Azure permite dimensionar manualmente o serviço de nuvem a satisfazer evolutivos de pedidos de conteúdo por clientes, sem necessidade de instalar e aprovisionar pontos de distribuição adicionais.  

-   O ponto de distribuição baseado na nuvem suporta a transferência de conteúdos por parte de clientes que estejam configurados para o Windows BranchCache.  


Um ponto de distribuição baseado na nuvem tem as seguintes limitações:  

-  Antes de utilizar a versão 1610 com KB4010155 a correção, é possível utilizar um ponto de distribuição baseado na nuvem para alojar pacotes de atualização de software. Este problema for corrigido partir versão 1702 e versões posteriores.  

-   Não é possível utilizar um ponto de distribuição baseado na nuvem para implementações de multicast ativados ou PXE.  

-   Os clientes não poderão utilizar um ponto de distribuição baseado na nuvem como uma localização de conteúdo para uma sequência de tarefas que é implementada através da opção de implementação **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**. No entanto, as sequências de tarefas que são implementadas utilizando a opção de implementação **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** podem utilizar um ponto de distribuição baseado na nuvem como uma localização válida de conteúdos.  

-   Um ponto de distribuição baseado na nuvem não suporta pacotes que são executados a partir do ponto de distribuição. Todo o conteúdo tem de ser transferidos na íntegra pelo cliente e, em seguida, executado localmente.  

-   Um ponto de distribuição baseado na nuvem não suporta aplicações de transmissão em sequência através do Application Virtualization ou de programas similares.  

-   Um ponto de distribuição baseado na nuvem não suporta conteúdos pré-configurados. O Gestor de distribuição do site primário que gere o ponto de distribuição transfere os conteúdos ao ponto de distribuição.  

-   Um ponto de distribuição baseado na nuvem não pode ser configurado como um ponto de distribuição de solicitação.  

##  <a name="BKMK_PrereqsCloudDP"></a> Pré-requisitos de pontos de distribuição baseados na nuvem  
 Um ponto de distribuição baseado na nuvem necessita dos seguintes pré-requisitos para poder ser utilizado:  

-   Uma subscrição do Azure (consulte [acerca das subscrições e certificados](#BKMK_CloudDPCerts) neste tópico).

-   Um certificado de gestão auto-assinado ou pública infraestrutura de chaves (PKI) para comunicação a partir de um servidor de site primário do Configuration Manager para o serviço de nuvem do Azure (consulte [acerca das subscrições e certificados](#BKMK_CloudDPCerts) neste tópico).

-   Um certificado de serviço (PKI) que clientes do Configuration Manager utilizam para estabelecer ligação a pontos de distribuição baseado na nuvem e transferir conteúdos dos mesmos utilizando HTTPS.  

-  Tem de ter um dispositivo ou utilizador **pontos de permitir o acesso a distribuição de nuvem** definido como **Sim** no cliente do definição de **serviços em nuvem** para um dispositivo ou utilizador possa aceder ao conteúdo a partir de um ponto de distribuição baseado na nuvem. Por predefinição, este valor está definido como **Não**.  

-   Um cliente deve estar preparado para resolver o nome do serviço de nuvem, que requer um alias de sistema de nomes de domínio (DNS) e um registo CNAME no espaço de nomes DNS.  

-   Um cliente deve estar preparado para aceder à Internet para utilizar o ponto de distribuição baseado na nuvem.  

##  <a name="BKMK_CloudDPCost"></a> Custo de utilização da distribuição baseada na nuvem  
 Quando utiliza um ponto de distribuição baseado na nuvem, planeie o custo de armazenamento de dados e transferências de transferência que efetuam de clientes do Configuration Manager.  

 O Configuration Manager inclui opções para ajudar a controlar os custos e monitorizar o acesso a dados:  

-   Pode controlar e monitorizar a quantidade de conteúdo que armazena num serviço em nuvem.  

-   Pode configurar o Configuration Manager para o alertar quando **limiares** para transferências de clientes atinjam ou ultrapassem os limites mensais.  

-   Além disso, pode utilizar o ponto a ponto (Windows BranchCache) a colocação em cache para ajudar a reduzir o número de transferências de dados a partir de pontos de distribuição baseado na nuvem pelos clientes. Clientes do Configuration Manager que estão configurados para o BranchCache podem transferir conteúdo utilizando pontos de distribuição baseado na nuvem.  


**Opções:**  

-   **Definições de cliente para a nuvem**: Controlar o acesso a todos os pontos de distribuição baseado na nuvem de uma hierarquia utilizando **definições de cliente**.  

     Nas **Definições de Cliente**, a categoria **Definições de Nuvem** suporta a definição **Permitir acesso a pontos de distribuição de nuvem**. Por predefinição, esta definição encontra-se definida como **Não**. Pode ativar esta definição para utilizadores e dispositivos.  

-   **Limiares de transferência de dados de**: Pode configurar limiares para a quantidade de dados que pretende armazenar no ponto de distribuição e para a quantidade de dados transferidos pelos clientes do ponto de distribuição.  

     Os limiares para pontos de distribuição baseados em nuvem incluem:  

    -   **Limiar de alerta de armazenamento**: Um limiar de alerta de armazenamento define um limite superior a quantidade de dados ou conteúdo que pretende armazenar no ponto de distribuição baseado na nuvem. O Configuration Manager pode gerar um alerta de aviso quando o espaço livre restante face ao atingir o nível que especificar.  

    -   **Limiar de alerta de transferência**: Um limiar de alerta de transferência ajuda-o a monitorizar a quantidade de conteúdo que é transferido do ponto de distribuição a clientes durante um período de 30 dias. O limiar de alerta de transferência monitoriza as transferências de dados últimos 30 dias e pode emitir um alerta de aviso e um alerta crítico quando as transferências atingirem valores por si definidos.  

        > [!IMPORTANT]  
        >  O Configuration Manager monitoriza a transferência de dados, mas não a interromperá se a transferência de dados acima do limiar de alerta de transferência especificado.  

 Poderá especificar limiares para cada ponto de distribuição baseado em nuvem durante a instalação do ponto de distribuição ou editando as propriedades de cada ponto após a respetiva instalação.  

-   **Alertas**: Pode configurar o Configuration Manager para emitir alertas sobre as transferências de dados de e para cada ponto de distribuição baseado na nuvem, com base nos limiares de transferência de dados que especificou. Tais alertas ajudam a monitorizar as transferências de dados, pode ajudar a decidir quando para parar o serviço em nuvem, ajuste o conteúdo que é armazenado no ponto de distribuição ou modificar os clientes que podem utilizar a distribuição baseado na nuvem pontos.  

     Num ciclo horário, o site primário que monitoriza o ponto de distribuição baseado na nuvem transfere dados de transação a partir do Azure e armazena-os em CloudDP -&lt;ServiceName\>. log no servidor do site. O Configuration Manager avalia então esta informação face às quotas de armazenamento e transferência para cada ponto de distribuição baseado na nuvem. Quando a transferência de dados atinge ou excede o volume especificado para avisos ou alertas críticos, o Configuration Manager gera o alerta adequado.  

    > [!WARNING]  
    >  Como obter informações sobre as transferências de dados são transferidas a partir do Azure numa base horária, que a utilização de dados poderá exceder um limiar de aviso ou crítico, antes do Configuration Manager pode aceder aos dados e emitir um alerta.  

    > [!NOTE]  
    >  Os alertas para um ponto de distribuição baseado na nuvem dependem das estatísticas de utilização a partir do Azure, o que pode demorar até 24 horas a ficar disponíveis. Para obter informações sobre a análise de armazenamento para o Azure, incluindo a frequência de atualizações Azure utilização estatísticas, consulte o artigo [análise de armazenamento](http://go.microsoft.com/fwlink/p/?LinkID=275111) na biblioteca da MSDN.  


-   **Parar ou iniciar o serviço em nuvem a pedido**: Pode utilizar a opção para parar um serviço em nuvem em qualquer altura para impedir que os clientes utilizando o serviço de forma contínua. Quando para o serviço em nuvem, impede de imediato que os clientes transfiram conteúdo adicional a partir do mesmo. Também poderá reiniciar o serviço em nuvem para restaurar o acesso dos clientes. Por exemplo, poderá querer parar um serviço em nuvem quando os limiares de dados forem atingidos.  

     Quando para um serviço em nuvem, o serviço não elimina o conteúdo do ponto de distribuição nem impede o servidor do site de transferir conteúdo adicional para o ponto de distribuição baseado em nuvem.  

     Para parar um serviço em nuvem, na consola do Configuration Manager, selecione o ponto de distribuição a **pontos de distribuição de nuvem** nó em **serviços em nuvem**, no **administração** área de trabalho. Em seguida, escolha **parar serviço** para parar o serviço em nuvem executado no Azure.  

##  <a name="BKMK_CloudDPCerts"></a> Acerca das subscrições e certificados de pontos de distribuição baseados na nuvem  
 Pontos de distribuição baseado na nuvem necessitam de certificados para permitir que o Configuration Manager para gerir o serviço em nuvem que aloja o ponto de distribuição bem como os clientes de acesso a conteúdo da distribuição ponto. As informações seguintes proporcionam uma descrição geral sobre estes certificados. Para obter informações mais detalhadas, veja [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificados**  

-   **Certificado de gestão para o servidor de site para comunicação de ponto de distribuição**: O certificado de gestão estabelece a fidedignidade entre a API de gestão Azure e do Configuration Manager. Esta autenticação permite que o Configuration Manager efetuar chamadas à API do Azure ao executar tarefas como a implementação de conteúdo ou iniciar e parar o serviço em nuvem. Ao utilizar o Azure, pode criar seus próprios certificados de gestão, que podem ser certificados auto-assinados ou certificados emitidos por uma autoridade de certificação (AC):  

    -   Disponibilize o ficheiro. cer do certificado de gestão para o Azure quando configurar o Azure para o Configuration Manager. O ficheiro .cer contém a chave pública do certificado de gestão. Deverá carregar este certificado para o Azure antes de instalar um ponto de distribuição baseado na nuvem. Este certificado permite que o Configuration Manager para aceder à API do Azure.  

    -   Forneça o ficheiro. pfx do certificado de gestão do Configuration Manager quando instala o ponto de distribuição baseado na nuvem. O ficheiro .pfx contém a chave privada para o certificado de gestão. O Configuration Manager guarda este certificado na base de dados do site. Dado que o ficheiro. pfx contém a chave privada, tem de fornecer a palavra-passe para importar este ficheiro de certificado para a base de dados do Configuration Manager.  

    Se criar um certificado autoassinado, tem de exportar primeiro o certificado como um ficheiro. cer e, em seguida, de exportá-lo novamente como um ficheiro. pfx.  

    Opcionalmente, pode especificar uma versão um **. publishsettings** ficheiro a partir do Azure SDK 1.7. Para obter informações sobre os ficheiros. publishsettings, consulte a documentação do Azure.  

    Para obter mais informações, consulte o artigo [como criar um certificado de gestão](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [como adicionar um certificado de gestão para uma subscrição do Azure](http://go.microsoft.com/fwlink/p/?LinkId=241722) na secção plataforma Azure do biblioteca MSDN.  

-   **Certificado de serviço para comunicações de clientes para o ponto de distribuição**: O certificado de serviço do ponto de distribuição baseado na nuvem do Configuration Manager estabelece a fidedignidade entre os clientes do Configuration Manager e o ponto de distribuição baseado na nuvem e protege os dados transferidos a partir do mesmo pelos clientes através de Secure Socket Layer (SSL) sobre HTTPS.  

    > [!IMPORTANT]  
    >  O nome comum localizado na caixa de assunto do certificado correspondente ao certificado de serviço tem de ser exclusivo no seu domínio e não pode corresponder a qualquer dispositivo associado ao domínio.  

   Para um exemplo de implementação deste certificado, consulte a secção **implementar o certificado de serviço para pontos de distribuição baseado na nuvem** no tópico [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Tarefas de gestão comuns para pontos de distribuição baseados na nuvem  

-   **Servidor de sites para comunicação de ponto de distribuição baseado na nuvem**: Quando instala um ponto de distribuição baseado na nuvem, tem de atribuir um site primário para gerir a transferência de conteúdo para o serviço em nuvem. Esta ação equivale a instalar a função de sistema de sites de ponto de distribuição num site específico.  

-   **A comunicação de ponto de distribuição baseado na nuvem de cliente**: Quando um dispositivo ou utilizador de um dispositivo estiver configurado com a definição de cliente que permitem a utilização de um ponto de distribuição baseado na nuvem, o dispositivo pode receber o ponto de distribuição baseado na nuvem como uma localização válida de conteúdos:  

    -   O ponto de distribuição baseado na nuvem é considerado um ponto de distribuição remoto quando um cliente avalia as localizações de conteúdos disponíveis.  

    -   Clientes na intranet apenas utilizam pontos de distribuição baseado na nuvem como uma opção de contingência se pontos de distribuição no local não estão disponíveis.  

    Apesar de os instalar pontos de distribuição baseado na nuvem em regiões específicas do Azure, os clientes que utilizam pontos de distribuição baseado na nuvem não têm conhecimento das regiões do Azure e selecionam não determinística um ponto de distribuição em nuvem com base.

Isto significa que se instalar pontos de distribuição baseado na nuvem em várias regiões e um cliente receber vários pontos de distribuição baseado na nuvem como localizações de conteúdo, o cliente poderá não utilizar um ponto de distribuição baseado na nuvem a partir da mesma região Azure que o cliente.  

Os clientes que utilizam pontos de distribuição baseado na nuvem utilizam a seguinte sequência para pedidos de localização de conteúdo:  

1.  Um cliente que esteja configurado para utilizar pontos de distribuição baseados na nuvem tenta sempre obter primeiro os conteúdos a partir de um ponto de distribuição preferencial.  

2.  Quando um ponto de distribuição preferencial não está disponível, o cliente utiliza um ponto de distribuição remoto, se a implementação suporte esta opção e se estiver disponível um ponto de distribuição remoto.  

3.  Quando um ponto de distribuição preferencial ou ponto de distribuição remoto não estiverem disponíveis, o cliente pode reverter para obter os conteúdos a partir de um ponto de distribuição baseado na nuvem.  



  Quando um cliente utiliza um ponto de distribuição baseado na nuvem como uma localização de conteúdos, autentica próprio para o ponto de distribuição baseado na nuvem utilizando um token de acesso do Configuration Manager. Se o cliente considerar o certificado de ponto de distribuição baseado na nuvem do Configuration Manager, o cliente, em seguida, pode transferir os conteúdos solicitados.  

-   **Monitorizar pontos de distribuição baseado na nuvem**: Pode monitorizar o conteúdo que implementa em cada ponto de distribuição baseado na nuvem e pode monitorizar o serviço em nuvem que aloja o ponto de distribuição.  

    -   **Conteúdo**: Monitorizar o conteúdo que implementa para um ponto de distribuição baseado na nuvem da mesma forma que fazer quando implementar conteúdo em pontos de distribuição no local.  

    -   **Serviço em nuvem**: Periodicamente, o Configuration Manager verifica o serviço do Azure e gera um alerta se o serviço não estiver ativo ou se existirem problemas com subscrições ou certificados. Também pode ver detalhes sobre o ponto de distribuição no **pontos de distribuição de nuvem** nó **serviços em nuvem** no **administração** área de trabalho da consola do Configuration Manager. A partir desta localização, ver informações de alto nível sobre o ponto de distribuição. Pode também selecionar um ponto de distribuição e, em seguida, editar as propriedades dele.  

    Quando edita as propriedades de um ponto de distribuição baseado na nuvem, pode:  

    -   Ajuste os limiares de dados de armazenamento e alertas.  

    -   Gerir o conteúdo como se tratasse de uma distribuição no local ponto.  

    Finalmente, para cada ponto de distribuição baseado em nuvem poderá visualizar, mas não editar, o ID de subscrição, nome do serviço e outros detalhes relacionados especificados ao instalar o ponto de distribuição baseado em nuvem.  

-   **Cópia de segurança e recuperação para os pontos de distribuição baseado na nuvem**: Quando utiliza um ponto de distribuição baseado na nuvem na hierarquia, utilize as seguintes informações para o ajudar a planear a cópia de segurança ou recuperação do ponto de distribuição:  

    -   Quando utiliza o predefinidas **cópia de segurança do servidor do Site** tarefa de manutenção do Configuration Manager inclui automaticamente as configurações do ponto de distribuição baseado na nuvem.  

    -   É uma melhor prática de criar uma segurança e guarde uma cópia do certificado de gestão e o certificado de serviço que são utilizados com um ponto de distribuição baseado na nuvem. Se restaurar o site primário do Configuration Manager que gere o ponto de distribuição baseado na nuvem para outro computador, deve voltar a importar os certificados antes de poder continuar a utilizá-los.  

-   **Desinstalar um ponto de distribuição baseado na nuvem** : Para desinstalar um ponto de distribuição baseado na nuvem, selecione o ponto de distribuição na consola do Configuration Manager e, em seguida, selecione **eliminar**.  

    Quando elimina um ponto de distribuição baseado na nuvem de uma hierarquia, o Configuration Manager remove o conteúdo do serviço em nuvem no Azure.  

