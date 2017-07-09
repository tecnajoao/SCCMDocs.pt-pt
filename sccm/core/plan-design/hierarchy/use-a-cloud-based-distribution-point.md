---
title: "Ponto de distribuição baseado em nuvem | Microsoft Docs"
description: "Saiba mais sobre as configurações e limitações para usar um ponto de distribuição baseado em nuvem com o System Center Configuration Manager."
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
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 8caf3319d93b98680ed4a719a8db714c7e4e96ce
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Um ponto de distribuição baseado em nuvem é um ponto de distribuição do System Center Configuration Manager que é hospedado no Microsoft Azure. As informações que se seguem destinam-se a ajudá-lo a saber mais sobre as configurações e limitações da utilização de um ponto de distribuição baseado na nuvem.

Depois de instalar um site primário e está pronto para instalar um ponto de distribuição baseado em nuvem, consulte [instalar pontos de distribuição baseado em nuvem no Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planear a utilização de um ponto de distribuição baseado na nuvem
Quando utilizar um ponto de distribuição baseado na nuvem, pode:  

-   **Definir configurações do cliente** para permitir que usuários e dispositivos acessar o conteúdo.  

-   **Especifique um site primário para gerenciar a transferência de conteúdo** ao ponto de distribuição.  

-   **Especifique os limites de** para a quantidade de conteúdo que você deseja armazenar no ponto de distribuição e a quantidade de conteúdo que você deseja permitir que os clientes transfiram do ponto de distribuição.  


Com base nos limites configurados, o Configuration Manager pode gerar alertas que avisam quando a quantidade combinada de conteúdo que você armazenou no ponto de distribuição está próximo do volume de armazenamento especificado ou quando as transferências de dados pelos clientes estão próximos aos limites que você definiu.  

Pontos de distribuição baseado em nuvem oferecem suporte a vários recursos que também são oferecidos pelos pontos de distribuição local:  

-   Gerenciar pontos de distribuição baseado em nuvem individualmente ou como membros da distribuição de grupos de pontos.  

-   Você pode usar um ponto de distribuição baseado em nuvem como local de fallback de conteúdo.  

-   Receberá suporte tanto para clientes baseados na intranet como baseados na Internet.  


Pontos de distribuição baseado em nuvem fornecem os seguintes benefícios adicionais:  

-   Conteúdo que é enviado para um ponto de distribuição baseado em nuvem é criptografado pelo Configuration Manager antes do Configuration Manager envia para o Azure.  

-   No Azure, você pode Dimensionar manualmente o serviço de nuvem para atender às demandas de alteração para solicitações de conteúdo por clientes, sem a necessidade de instalar e provisionar pontos de distribuição adicionais.  

-   O ponto de distribuição baseado na nuvem suporta a transferência de conteúdos por parte de clientes que estejam configurados para o Windows BranchCache.  


Um ponto de distribuição baseado na nuvem tem as seguintes limitações:  

-  Antes de usar a versão 1610 com o Hotfix KB4010155, você não pode usar um ponto de distribuição baseado em nuvem para hospedar pacotes de atualização de software. Esse problema é corrigido começando pela versão 1702 e posterior.  

-   Você não pode usar um ponto de distribuição baseado em nuvem para PXE ou implantações habilitados para multicast.  

-   Os clientes não poderão utilizar um ponto de distribuição baseado na nuvem como uma localização de conteúdo para uma sequência de tarefas que é implementada através da opção de implementação **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**. No entanto, as sequências de tarefas que são implementadas utilizando a opção de implementação **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** podem utilizar um ponto de distribuição baseado na nuvem como uma localização válida de conteúdos.  

-   Um ponto de distribuição baseado na nuvem não suporta pacotes que são executados a partir do ponto de distribuição. Todo o conteúdo deve ser baixado pelo cliente e, em seguida, executado localmente.  

-   Um ponto de distribuição baseado na nuvem não suporta aplicações de transmissão em sequência através do Application Virtualization ou de programas similares.  

-   Um ponto de distribuição baseado na nuvem não suporta conteúdos pré-configurados. O Gerenciador de distribuição do site primário que gerencia o ponto de distribuição transfere todo o conteúdo ao ponto de distribuição.  

-   Um ponto de distribuição baseado na nuvem não pode ser configurado como um ponto de distribuição de solicitação.  

##  <a name="BKMK_PrereqsCloudDP"></a> Pré-requisitos de pontos de distribuição baseados na nuvem  
 Um ponto de distribuição baseado na nuvem necessita dos seguintes pré-requisitos para poder ser utilizado:  

-   Uma assinatura do Azure (consulte [sobre assinaturas e certificados](#BKMK_CloudDPCerts) neste tópico).

-   Um certificado de gerenciamento autoassinado ou pública (PKI) do infraestrutura de chave para a comunicação de um servidor de site primário do Configuration Manager para o serviço de nuvem no Azure (consulte [sobre assinaturas e certificados](#BKMK_CloudDPCerts) neste tópico).

-   Um certificado de serviço (PKI) usado por clientes do Configuration Manager para se conectar aos pontos de distribuição baseado em nuvem e descarregar conteúdo usando HTTPS.  

-  Um dispositivo ou usuário deve ter **pontos de acesso permite a distribuição de nuvem** definida como **Sim** no cliente de configuração de **serviços de nuvem** antes que um dispositivo ou usuário possa acessar o conteúdo de um ponto de distribuição baseado em nuvem. Por predefinição, este valor está definido como **Não**.  

-   Um cliente deve ser capaz de resolver o nome do serviço em nuvem, que requer um alias de sistema de nome de domínio (DNS) e um registro CNAME no seu namespace DNS.  

-   Um cliente deve estar preparado para aceder à Internet para utilizar o ponto de distribuição baseado na nuvem.  

##  <a name="BKMK_CloudDPCost"></a> Custo de utilização da distribuição baseada na nuvem  
 Quando você usa um ponto de distribuição baseado em nuvem, planeje o custo de armazenamento de dados e as transferências de download que executam clientes do Configuration Manager.  

 Gerenciador de configurações inclui opções para ajudar a controlar os custos e monitorar o acesso a dados:  

-   Pode controlar e monitorizar a quantidade de conteúdo que armazena num serviço em nuvem.  

-   Você pode configurar o Configuration Manager para alertá-lo quando **limites** para downloads do cliente atingirem ou excederem os limites mensais.  

-   Além disso, você pode usar o cache (Windows BranchCache) de sistemas pares para ajudar a reduzir o número de transferências de dados de pontos de distribuição baseado em nuvem por clientes. Clientes do Configuration Manager que estão configurados para o BranchCache podem transferir conteúdo usando pontos de distribuição baseado em nuvem.  


**Opções:**  

-   **Configurações do cliente para nuvem**: Controlar o acesso a todos os pontos de distribuição baseado em nuvem em uma hierarquia usando **configurações do cliente**.  

     Nas **Definições de Cliente**, a categoria **Definições de Nuvem** suporta a definição **Permitir acesso a pontos de distribuição de nuvem**. Por predefinição, esta definição encontra-se definida como **Não**. Você pode habilitar essa configuração para usuários e dispositivos.  

-   **Limites para transferências de dados de**: Você pode configurar limites para a quantidade de dados que você deseja armazenar no ponto de distribuição e a quantidade de dados que os clientes baixam do ponto de distribuição.  

     Os limiares para pontos de distribuição baseados em nuvem incluem:  

    -   **Limite de alerta de armazenamento**: Um limite de alerta de armazenamento define um limite superior na quantidade de dados ou conteúdo que você deseja armazenar no ponto de distribuição baseado em nuvem. Gerenciador de configuração pode gerar um alerta de aviso quando o espaço livre restante atinge o nível que você especificar.  

    -   **Transferência de limite de alerta**: Um limite de alerta de transferência ajuda a monitorar a quantidade de conteúdo que você transfere do ponto de distribuição aos clientes por um período de 30 dias. O limite de alerta de transferência monitora a transferência de dados dos últimos 30 dias e pode emitir um alerta de aviso e um alerta crítico quando as transferências atingem os valores que você definir.  

        > [!IMPORTANT]  
        >  Configuration Manager monitora a transferência de dados, mas não interrompe a transferência de dados além do limite de alerta de transferência especificado.  

 Poderá especificar limiares para cada ponto de distribuição baseado em nuvem durante a instalação do ponto de distribuição ou editando as propriedades de cada ponto após a respetiva instalação.  

-   **Alertas**: Você pode configurar o Configuration Manager para emitir alertas sobre transferências de dados em cada ponto de distribuição baseado em nuvem, com base em limites de transferência de dados que você especificar. Esses alertas ajudam você a monitorar as transferências de dados e pode ajudá-lo a decide quando parar o serviço de nuvem, ajustar o conteúdo que você armazena no ponto de distribuição ou modificar quais clientes podem usar a distribuição com base em nuvem pontos.  

     Em um ciclo por hora, o site primário que monitora o ponto de distribuição baseado em nuvem baixa dados de transação do Azure e armazena em CloudDP -&lt;ServiceName\>. log no servidor do site. Em seguida, o Configuration Manager avalia essas informações com as cotas de armazenamento e transferência para cada ponto de distribuição baseado em nuvem. Quando a transferência de dados atinge ou excede o volume especificado para avisos ou alertas críticos, o Configuration Manager gera o alerta apropriado.  

    > [!WARNING]  
    >  Como obter informações sobre transferências de dados são baixadas do Azure por hora, que o uso de dados pode exceder um limite de aviso ou crítico antes que o Configuration Manager pode acessar os dados e emitir um alerta.  

    > [!NOTE]  
    >  Alertas de um ponto de distribuição baseado em nuvem dependem de estatísticas de uso do Azure, que pode levar até 24 horas para ficar disponível. Para obter informações sobre análise de armazenamento do Azure, incluindo a frequência de atualizações do Azure usam estatísticas, consulte [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) na biblioteca MSDN.  


-   **Interromper ou iniciar o serviço de nuvem sob demanda**: Você pode usar a opção para interromper um serviço de nuvem a qualquer momento para impedir que clientes usem o serviço continuamente. Quando para o serviço em nuvem, impede de imediato que os clientes transfiram conteúdo adicional a partir do mesmo. Também poderá reiniciar o serviço em nuvem para restaurar o acesso dos clientes. Por exemplo, poderá querer parar um serviço em nuvem quando os limiares de dados forem atingidos.  

     Quando para um serviço em nuvem, o serviço não elimina o conteúdo do ponto de distribuição nem impede o servidor do site de transferir conteúdo adicional para o ponto de distribuição baseado em nuvem.  

     Para interromper um serviço de nuvem no console do Configuration Manager, selecione o ponto de distribuição no **pontos de distribuição em nuvem** nó **serviços de nuvem**, no **administração** espaço de trabalho. Em seguida, escolha **parar serviço** para interromper o serviço de nuvem que é executado no Azure.  

##  <a name="BKMK_CloudDPCerts"></a> Acerca das subscrições e certificados de pontos de distribuição baseados na nuvem  
 Pontos de distribuição baseado em nuvem requerem certificados para habilitar o Configuration Manager para gerenciar o serviço de nuvem que hospeda o ponto de distribuição e para os clientes para acessar o conteúdo da distribuição ponto. As informações a seguir fornecem uma visão geral sobre esses certificados. Para obter informações mais detalhadas, veja [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificados**  

-   **Certificado de gerenciamento do servidor do site para comunicação do ponto de distribuição**: O certificado de gerenciamento estabelece uma relação de confiança entre a API de gerenciamento do Azure e o Configuration Manager. Essa autenticação permite que o Configuration Manager para chamar a API do Azure, quando você executa tarefas como implantação de conteúdo ou iniciar e parar o serviço de nuvem. Usando o Azure, você pode criar seus próprios certificados de gerenciamento, que podem ser certificados autoassinados ou certificados emitidos por uma autoridade de certificação (CA):  

    -   Forneça o arquivo. cer do certificado de gerenciamento do Azure ao configurar o Azure para o Configuration Manager. O ficheiro .cer contém a chave pública do certificado de gestão. Você deve carregar este certificado para o Azure antes de instalar um ponto de distribuição baseado em nuvem. Este certificado permite que o Configuration Manager para acessar a API do Azure.  

    -   Forneça o arquivo. pfx de certificado de gerenciamento para o Configuration Manager quando você instala o ponto de distribuição baseado em nuvem. O ficheiro .pfx contém a chave privada para o certificado de gestão. O banco de dados do site, o Configuration Manager armazena este certificado. Como o arquivo. pfx contém a chave privada, você deve fornecer a senha para importar esse arquivo de certificado para o banco de dados do Configuration Manager.  

    Se você criar um certificado autoassinado, você deve primeiro exportar o certificado como um arquivo. cer e, em seguida, exportá-lo novamente como um arquivo. pfx.  

    Opcionalmente, você pode especificar uma versão de um **. publishsettings** arquivo do Azure SDK 1.7. Para obter informações sobre arquivos. publishsettings, consulte a documentação do Azure.  

    Para obter mais informações, consulte [como criar um certificado de gerenciamento](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [como adicionar um certificado de gerenciamento a uma assinatura do Azure](http://go.microsoft.com/fwlink/p/?LinkId=241722) na seção plataforma Windows Azure da biblioteca MSDN.  

-   **Certificado de serviço para comunicação de cliente para o ponto de distribuição**: O certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager estabelece a relação de confiança entre os clientes do Configuration Manager e o ponto de distribuição baseado em nuvem e protege os dados que os clientes baixam dele usando Secure Socket Layer (SSL) sobre HTTPS.  

    > [!IMPORTANT]  
    >  O nome comum localizado na caixa de assunto do certificado correspondente ao certificado de serviço tem de ser exclusivo no seu domínio e não pode corresponder a qualquer dispositivo associado ao domínio.  

   Para um exemplo de implantação deste certificado, consulte a seção **Implantando o certificado de serviço para pontos de distribuição baseado em nuvem** no tópico [exemplo passo a passo de implantação da PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Tarefas de gestão comuns para pontos de distribuição baseados na nuvem  

-   **Servidor do site para comunicação do ponto de distribuição baseado em nuvem**: Quando você instala um ponto de distribuição baseado em nuvem, você deve atribuir um site primário para gerenciar a transferência de conteúdo para o serviço de nuvem. Esta ação equivale a instalar a função de sistema de sites de ponto de distribuição num site específico.  

-   **Cliente para comunicação do ponto de distribuição baseado em nuvem**: Quando um dispositivo ou usuário de um dispositivo é configurado com a configuração do cliente que permite o uso de um ponto de distribuição baseado em nuvem, o dispositivo pode receber o ponto de distribuição baseado em nuvem como um local de conteúdo válido:  

    -   O ponto de distribuição baseado em nuvem é considerado um ponto de distribuição remoto quando um cliente avalia os locais de conteúdo disponíveis.  

    -   Clientes na intranet só usam pontos de distribuição baseado em nuvem como uma opção de fallback se os pontos de distribuição em locais não estão disponíveis.  

    Mesmo que você instale pontos de distribuição baseado em nuvem em regiões específicas do Azure, os clientes que usam pontos de distribuição baseado em nuvem não estão cientes das regiões do Azure e selecionam de forma não determinística um ponto de distribuição baseado em nuvem.

Isso significa que se você instala pontos de distribuição baseado em nuvem em várias regiões, e um cliente receber vários pontos de distribuição baseado em nuvem como locais de conteúdo, o cliente não poderá usar um ponto de distribuição baseado em nuvem da mesma região do Azure que o cliente.  

Os clientes que usam pontos de distribuição baseado em nuvem usam a sequência a seguir para solicitações de localização de conteúdo:  

1.  Um cliente que esteja configurado para utilizar pontos de distribuição baseados na nuvem tenta sempre obter primeiro os conteúdos a partir de um ponto de distribuição preferencial.  

2.  Quando um ponto de distribuição preferencial não estiver disponível, o cliente usa um ponto de distribuição remoto, se a implantação dá suporte a essa opção e um ponto de distribuição remoto está disponível.  

3.  Quando um ponto de distribuição preferencial ou ponto de distribuição remoto não estiverem disponíveis, o cliente pode reverter para obter os conteúdos a partir de um ponto de distribuição baseado na nuvem.  



  Quando um cliente usa um ponto de distribuição baseado em nuvem como local de conteúdo, o cliente se autentica para o ponto de distribuição baseado em nuvem usando um token de acesso do Configuration Manager. Se o cliente confia o certificado do ponto de distribuição baseado em nuvem do Configuration Manager, o cliente pode, em seguida, baixe o conteúdo solicitado.  

-   **Monitorar pontos de distribuição baseado em nuvem**: Você pode monitorar o conteúdo que você implanta em cada ponto de distribuição baseado em nuvem, e você pode monitorar o serviço de nuvem que hospeda o ponto de distribuição.  

    -   **Conteúdo**: Você monitora o conteúdo que você implanta em um ponto de distribuição baseado em nuvem da mesma maneira que faria quando você implanta conteúdo em pontos de distribuição local.  

    -   **Serviço de nuvem**: Configuration Manager periodicamente verifica se o serviço do Azure e emitirá um alerta se o serviço não estiver ativo ou se houver problemas de assinatura ou certificado. Você também pode exibir detalhes sobre o ponto de distribuição no **pontos de distribuição em nuvem** nó **serviços de nuvem** no **administração** espaço de trabalho do console do Configuration Manager. Nesse local, você deve exibir informações de alto nível sobre o ponto de distribuição. Você pode também selecionar um ponto de distribuição e editar suas propriedades.  

    Quando edita as propriedades de um ponto de distribuição baseado na nuvem, pode:  

    -   Ajuste os limites de dados para armazenamento e alertas.  

    -   Gerencie conteúdo como você faria para uma local ponto de distribuição.  

    Finalmente, para cada ponto de distribuição baseado em nuvem poderá visualizar, mas não editar, o ID de subscrição, nome do serviço e outros detalhes relacionados especificados ao instalar o ponto de distribuição baseado em nuvem.  

-   **Backup e recuperação de pontos de distribuição baseado em nuvem**: Quando você usa um ponto de distribuição baseado em nuvem em sua hierarquia, use as seguintes informações para ajudá-lo a planejar para fazer backup ou recuperação do ponto de distribuição:  

    -   Quando você usa predefinida **servidor do Site de Backup** tarefa de manutenção, o Configuration Manager inclui automaticamente as configurações do ponto de distribuição baseado em nuvem.  

    -   É uma prática recomendada fazer backup e salvar uma cópia do certificado de gerenciamento e o certificado de serviço que estão em uso com um ponto de distribuição baseado em nuvem. Se você restaurar o site primário do Configuration Manager que gerencia o ponto de distribuição baseado em nuvem para um computador diferente, reimporte os certificados antes de continuar a usá-los.  

-   **Desinstalar um ponto de distribuição baseado em nuvem** : Para desinstalar um ponto de distribuição baseado em nuvem, selecione o ponto de distribuição no console do Configuration Manager e, em seguida, selecione **excluir**.  

    Quando você exclui um ponto de distribuição baseado em nuvem de uma hierarquia, o Configuration Manager removerá o conteúdo do serviço de nuvem no Azure.  

