---
title: Gerir as definições das atualizações de software
titleSuffix: Configuration Manager
description: Saiba mais sobre as definições de cliente são adequadas para atualizações de software no seu site depois de instalar o ponto de atualização de software.
author: aczechowski
ms.date: 03/26/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ad44beeb662cb0cd5cf083b18721d88a5b7360c4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351620"
---
#  <a name="BKMK_ManageSUSettings"></a> Gerir as definições das atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de sincronizar as atualizações de software no Configuration Manager, configurar e verificar as definições nas secções seguintes.

##  <a name="BKMK_ClientSettings"></a> Definições de cliente para atualizações de software  
Depois de instalar o ponto de atualização de software, as atualizações de software são ativadas nos clientes por predefinição e as definições da página **Atualizações de Software** nas definições do cliente têm valores predefinidos. As definições de cliente são utilizadas ao nível do site e afetam quando as atualizações de software são analisadas a compatibilidade e como e quando as atualizações de software são instaladas nos computadores cliente. Antes de implementar atualizações de software, certifique-se de que as definições de cliente são adequadas para atualizações de software no seu site.  

> [!IMPORTANT]  
>  A definição **Ativar atualizações de software nos clientes** está ativada por predefinição. Se desmarcar esta definição, o Configuration Manager removerá as políticas de implementação existentes do cliente.  

Para obter informações sobre como configurar as definições de cliente, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

Para obter mais informações sobre as definições de cliente, consulte [sobre definições de cliente](../../core/clients/deploy/about-client-settings.md).  

##  <a name="BKMK_GroupPolicy"></a> Definições de política de grupo para atualizações de software  
Existem definições de política de grupo específicas que são utilizadas pelo Windows Update Agent (WUA) em computadores cliente para estabelecer ligação ao WSUS que é executado no ponto de atualizações de software. Estas definições de política de grupo também são utilizadas para analisar com sucesso a compatibilidade da atualização de software e para atualizar automaticamente as atualizações de software e o WUA.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Política local Especificar a Localização do Serviço de Atualizações da Microsoft na Intranet  
Quando o ponto de atualização de software é criado para um site, os clientes recebem uma política de computador que fornece o nome do servidor do ponto de atualização de software e configura a política local **Especificar localização do serviço de atualizações da Microsoft na intranet** no computador. O WUA obtém o nome do servidor que está especificado na definição **Definir o serviço de atualização na intranet para detetar atualizações** e estabelece ligação a este servidor quando verifica a compatibilidade das atualizações de software. Quando uma política de domínio é criada para a definição **Especificar localização do serviço de atualizações da Microsoft na intranet** , substitui a política local e o WUA poderá estabelecer ligação a outro servidor diferente do ponto de atualização de software. Se isto acontecer, o cliente pode analisar a compatibilidade da atualização de software com base em diferentes produtos, classificações e idiomas. Por conseguinte, não deve configurar a política do Active Directory para computadores cliente.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Política de grupo Permitir Conteúdo Assinado da Localização do Serviço de Atualizações da Microsoft na Intranet  
Tem de ativar a definição da Política de Grupo **Permitir conteúdo assinado da localização do serviço de atualização da Microsoft na intranet** antes de o WUA nos computadores verificar as atualizações de software que foram criadas e publicadas com o System Center Updates Publisher. Ativada a definição de política, o WUA aceita as atualizações de software recebidas através de uma localização de intranet se as atualizações de software forem assinadas no arquivo de certificados **Fabricantes Fidedignos** no computador local. Para obter mais informações sobre as definições da Política de Grupo necessárias ao Updates Publisher, veja [Biblioteca de Documentação do Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=232476).  

### <a name="automatic-updates-configuration"></a>Configuração de atualizações automáticas  
As Atualizações Automáticas permitem a receção de atualizações de segurança e de outras transferências importantes em computadores cliente. As Atualizações Automáticas são configuradas através da definição da Política de Grupo **Configurar Atualizações Automáticas** ou através do Painel de Controlo do computador local. Quando as Atualizações Automáticas são ativadas, os computadores cliente recebem notificações de atualização e, dependendo das definições configuradas, transferem e instalam as atualizações necessárias. Quando as Atualizações Automáticas coexistem com atualizações de software, cada computador cliente pode apresentar ícones de notificação e notificações de apresentação em pop-up para a mesma atualização. Além disso, quando for necessário um reinício, cada computador cliente pode apresentar uma caixa de diálogo de reinício para a mesma atualização.  

### <a name="self-update"></a>Autoatualização  
Quando as Atualizações Automáticas estão ativadas em computadores cliente, o WUA efetua automaticamente uma autoatualização quando uma versão mais recente está disponível ou quando existem problemas com um componente do WUA. Quando as Atualizações Automáticas não são configuradas ou estão desativadas e os computadores cliente têm uma versão mais recente do WUA, os computadores cliente devem executar o ficheiro de instalação do WUA.  

## <a name="software-updates-properties"></a>Propriedades de atualizações de software
As propriedades das atualizações de software contêm informações sobre as atualizações de software e o respetivo conteúdo. Também pode utilizar estas propriedades para configurar as definições das atualizações de software. Ao abrir as propriedades de várias atualizações de software, apenas são apresentados os separadores **Tempo de Execução Máximo** e **Gravidade Personalizada** .   

Utilize o seguinte procedimento para abrir as propriedades da atualização de software.  

#### <a name="to-open-software-update-properties"></a>Para abrir as propriedades da atualização de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  
2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Todas as Atualizações de Software**.  
3.  Selecione uma ou mais atualizações de software e, em seguida, no separador **Home Page** , clique em **Propriedades** no grupo **Propriedades** .  

   > [!NOTE]  
   >  No **todas as atualizações de Software** nó, o Configuration Manager apresenta apenas as atualizações de software que tenham um **crítico** e **segurança** classificação e que tenham sido publicadas nos últimos 30 dias.  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> Rever informações das atualizações de software  
As propriedades da atualização de software permitem-lhe rever informações detalhadas sobre uma atualização de software. As informações detalhadas não serão apresentadas se selecionar mais do que uma atualização de software. As secções seguintes descrevem as informações disponíveis para uma atualização de software selecionada.  

####  <a name="BKMK_SoftwareUpdateDetails"></a> Detalhes da atualização de software  
O separador **Detalhes da Atualização** contém as seguintes informações de resumo sobre a atualização de software selecionada:  

- **ID do boletim**: Especifica o ID do boletim associado às atualizações de software de segurança. Pode obter detalhes sobre boletins de segurança, procurando o ID do boletim na página Web [Pesquisa de Boletins de Segurança da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=58313) .  

- **ID de artigo**: Especifica o ID do artigo da atualização de software. O artigo referenciado contém informações mais detalhadas sobre a atualização de software, bem como o problema corrigido ou melhorado pela atualização de software.  

- **Data de revisão**: Especifica a data em que a atualização de software foi modificado pela última vez.  

- **Classificação de gravidade máxima**: Especifica a classificação de gravidade definida pelo fornecedor para a atualização de software.  

- **Descrição**: Fornece uma descrição geral da situação que a atualização de software corrige ou melhora.  

- **Idiomas aplicáveis**: Lista os idiomas para os quais a atualização de software é aplicável.  

- **Produtos afetados**: Apresenta uma lista dos produtos aos quais se aplica a atualização de software.  

####  <a name="BKMK_ContentInformation"></a> Informações de conteúdo  
No separador **Informações de Conteúdo** , reveja as seguintes informações sobre o conteúdo associado à atualização de software selecionada:  

-   **ID de conteúdo**: Especifica o ID de conteúdo da atualização de software.  

-   **Transferido**: Indica se o Configuration Manager transferiu os ficheiros de atualização de software.  

-   **Idioma**: Especifica os idiomas da atualização de software.  

-   **Caminho de origem**: Especifica o caminho para os ficheiros de origem de atualização de software.  

-   **Tamanho (MB)**: Especifica o tamanho dos ficheiros de origem de atualização de software.  

####  <a name="BKMK_CustomBundleInformation"></a> Informações de grupo personalizadas  
No separador **Informações do Grupo Personalizadas** , reveja as informações do grupo personalizadas relativas à atualização de software. Se a atualização de software selecionada contiver atualizações de software agrupadas que estejam incluídas no ficheiro de atualização de software, estas serão apresentadas na secção **Informações do grupo** . Este separador não apresenta as atualizações de software agrupadas que são apresentadas no separador **Informações de Conteúdo** , tais como os ficheiros de atualização para vários idiomas.  

####  <a name="BKMK_SupersedenceInformation"></a> Informações de substituição  
No separador **Informações de Substituição** , pode ver as seguintes informações relativas à substituição da atualização de software:  

- **Esta atualização foi substituída pelas seguintes atualizações**: Especifica as atualizações de software que substituem esta atualização, o que significa que as atualizações apresentadas são mais recentes. Na maioria dos casos, irá implementar uma das atualizações de software que substitui a atualização de software. As atualizações de software apresentadas na lista incluem hiperligações para páginas Web que contêm mais informações sobre as atualizações de software. Se esta atualização não tiver sido substituída, será apresentado **Nenhuma** .  

- **Esta atualização substitui as seguintes atualizações**: Especifica as atualizações de software que são substituídas por esta atualização de software, o que significa que esta atualização de software é mais recente. Na maioria dos casos, irá implementar esta atualização de software para substituir as atualizações de software substituídas. As atualizações de software apresentadas na lista incluem hiperligações para páginas Web que contêm mais informações sobre as atualizações de software. Se esta atualização não substituir qualquer outra atualização, será apresentado **Nenhuma** .  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> Configurar definições de atualizações de software  
As propriedades permitem-lhe configurar definições de atualização de software para uma ou mais atualizações de software. Apenas poderá configurar a maioria das definições de atualização de software através do site de administração central ou do site primário autónomo. As seguintes secções irão ajudá-lo a configurar as definições de atualizações de software.  

####  <a name="BKMK_SetMaxRunTime"></a> Definir o tempo máximo de execução  
No separador **Tempo Máximo de Execução** , defina o período de tempo máximo que uma atualização de software poderá demorar a ser instalada em computadores cliente. Se a atualização demora mais que o valor de tempo de execução máximo, o Configuration Manager cria uma mensagem de estado e interrompe a monitorização de implementação para a instalação de atualizações de software. Apenas poderá configurar esta definição através do site de administração central ou de um site primário autónomo.  

O Configuration Manager também utiliza esta definição para determinar se deve iniciar a instalação de atualização de software numa janela de manutenção configurada. Se o valor máximo de tempo de execução exceder o período de tempo restante na janela de manutenção, a instalação das atualizações de software será adiada até ao início da próxima janela de manutenção. Se existirem várias atualizações de software para serem instaladas num computador cliente que tenha uma janela de manutenção (prazo) configurada, será instalada em primeiro lugar a atualização de software que tenha o menor tempo de execução máximo, seguida da instalação da atualização que tiver o seguinte menor tempo de execução máximo e assim sucessivamente. Antes de instalar cada atualização de software, o cliente verifica se a janela de manutenção disponível disponibiliza tempo suficiente para a instalação da atualização de software. Após o início da instalação de uma atualização de software, esta continuará a ser instalada mesmo que ultrapasse o limite da janela de manutenção. Para obter mais informações sobre janelas de manutenção, veja [Como utilizar janelas de manutenção no System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  

No separador **Tempo Máximo de Execução** , pode ver e configurar as seguintes definições:  

- **Tempo de execução máximo**: Especifica o número máximo de minutos atribuído para uma instalação de atualização de software seja concluída antes da instalação já não é monitorizada pelo Configuration Manager. Esta definição também permite determinar se existe tempo suficiente para instalar uma atualização até ao prazo limite de uma janela de manutenção. A predefinição é 60 minutos para pacotes de serviços. Para outros tipos de atualização de software, a predefinição é 10 minutos se realizou uma nova instalação do Configuration Manager versão 1511 ou superior e 5 minutos quando tiver efetuado a atualização de uma versão anterior. Os valores variam entre 5 e 9999 minutos.  

> [!IMPORTANT]  
>  Certifique-se de que definiu o tempo máximo de execução para um valor inferior ao período da janela de manutenção configurada. Caso contrário, a instalação da atualização de software nunca será iniciada.  

####  <a name="BKMK_SetCustomSeverity"></a> Definir a gravidade personalizada  
Nas propriedades para uma atualização de software, pode utilizar o separador **Gravidade Personalizada** para configurar os valores de gravidade personalizada para as atualizações de software. Isto poderá ser necessário se os valores predefinidos de gravidade não cumprirem as suas necessidades. Os valores personalizados são enumerados no **gravidade personalizada** coluna na consola do Configuration Manager. Pode ordenar as atualizações de software pelos valores de gravidade personalizada definida e também pode criar consultas e relatórios que podem filtrar estes valores. Só pode configurar esta definição no site de administração central ou no site principal autónomo.  

Pode configurar as seguintes definições no separador **Gravidade Personalizada** .  

- **Gravidade personalizada**: Define um valor de gravidade personalizada para as atualizações de software. Selecione **Crítica**, **Importante**, **Moderada**ou **Baixa** na lista. Por predefinição, o valor de gravidade personalizado está vazio.

## <a name="crl-checking-for-software-updates"></a>Verificação CRL para atualizações de software
Por predefinição, a lista de revogação de certificados (CRL) não é verificada ao verificar a assinatura nas atualizações de software do System Center Configuration Manager. A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado revogado, mas provoca um atraso de ligação e implica um processamento adicional no computador que a está a efetuar.  

Se utilizado, a verificação CRL deve estar ativada nas consolas do Configuration Manager que processam atualizações de software.  

#### <a name="to-enable-crl-checking"></a>Para ativar a verificação CRL  
No computador que executa a verificação CRL, a partir do DVD do produto, execute o seguinte numa linha de comandos: **\SMSSETUP\BIN\X64\\**<*idioma*>**\UpdDwnldCfg.exe /checkrevocation**.  

Por exemplo, para inglês (EUA) execute **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**  
