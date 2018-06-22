---
title: Funcionalidades no Technical Preview 1606
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f3ee48d60c46def5daef25a2f3654e8a79a0e9e1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339864"
---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1606. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    

**Problemas conhecidos neste Technical Preview:**  
*  Quando atualizar a partir do Technical Preview 1604 para 1605 e, em seguida, a versão 1606, a atualização poderá falhar e é registado um erro semelhante ao seguinte no **cmupdate.log**:

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    Se isto ocorrer, além de **atualizações e manutenção** clique do nó **procurar atualizações**e, em seguida, **repita** a instalação da atualização.
    ***

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="dmp_category"></a> Categorizar automaticamente os dispositivos para coleções
Pode criar categorias de dispositivo, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando inscreverem um dispositivo no Intune. Além disso, pode alterar a categoria de um dispositivo da consola do Configuration Manager.

**Importante:** Esta capacidade funciona com o **Junho de 2016** versão do Microsoft Intune. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

### <a name="try-it-out"></a>Experimente!

### <a name="create-a-set-of-device-categories"></a>Criar um conjunto de categorias de dispositivos
1.  No **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **coleções de dispositivos**.
2.  No **home page** separador o **categorias** , clique em **gerir categorias de dispositivo**.
3.  No **gerir categorias de dispositivo** caixa de diálogo, pode criar, editar ou remover categorias. Tente criar uma nova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção uma categoria de dispositivo
Quando associa uma coleção com uma categoria de dispositivo, todos os dispositivos da categoria que especificar serão adicionados a essa coleção.
1.  No **propriedades** caixa de diálogo para uma coleção de dispositivos, clique em **Adicionar regra** > **regra de categoria do dispositivo**.
2.  No **criar regra de associação de categoria de dispositivo** diálogo caixa, selecione a categoria que será aplicada a todos os dispositivos na coleção.
3.  Fechar o **criar regra de associação de categoria de dispositivo** caixa de diálogo e a caixa de diálogo de propriedades de coleção.

### <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo
1.  No **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **dispositivos**.
2.  Selecione um dispositivo do **dispositivos** lista e, em seguida, no **home page** separador o **dispositivo** , clique em **alterar categoria**.
3.  No **editar a categoria de dispositivo** diálogo caixa, selecione a categoria para aplicar a este dispositivo, em seguida, clique em **OK**.

## <a name="dmp_grace"></a> Período de tolerância de imposição para a aplicação necessária e implementações de atualizações de software

Em alguns casos, poderá conceder a utilizadores mais tempo para as implementações de aplicações de instalação necessária ou atualizações de software para além de qualquer prazos que configurou. Pode normalmente ser necessária quando um computador foi desativado por um longo período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização.
Por exemplo, se um utilizador final tiver apenas devolvido de férias, poderá ter de aguardar algum enquanto como uma aplicação em atraso implementações estão instaladas.
Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

### <a name="try-it-out"></a>Experimente!

Para configurar o período de tolerância, efetuar as seguintes ações:

1.  No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para a imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.  Uma nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador**, até ao período de tolerância definido nas definições do cliente.
Todas as implementações que tenham esta caixa de verificação selecionada e são os que são direcionadas para os dispositivos nos quais tiver implementado também a definição de cliente utilizará o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação da aplicação, será instalado na primeira janela de empresa-empresa que o utilizador configurado até esse período de tolerância. No entanto, o utilizador pode ainda abrir o Centro de Software e instalar a aplicação em qualquer altura em que pretende. Depois do período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.
Foram adicionadas opções semelhantes para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades.

##  <a name="dmp_devg"></a>Utilizar o Configuration Manager como um instalador gerido com a proteção de dispositivos

A proteção de dispositivos é uma funcionalidade do Windows 10 que utiliza o hardware e as funcionalidades de software para estritamente controlar o que pode ser executada no dispositivo.

Pode ler uma descrição detalhada do que faz Device Guard, e como funciona em [neste artigo do Technet](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

Nesta versão, o Configuration Manager pode interagir com Device Guard e [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) para que o executável e os ficheiros DLL, que são implementados com o Configuration Manager são automaticamente fidedignos que possam ser proveniente de um instalador geridos, que significa que terá permissão para ser executada no dispositivo de destino e outro software não será permitido a execução, a menos que explicitamente permitidos para ser executada por outras regras do AppLocker.  

Atualmente, esta capacidade não é configurável na consola do Configuration Manager. Para configurar a política requer que configure uma chave de registo em cada cliente e os serviços do Windows no cliente.
Quando isto é feito, configure o ficheiro de política de AppLocker. Depois de configurar o ficheiro de política, pode implementá-la a todos os dispositivos cliente compatível.


Como todas as políticas de AppLocker, as políticas com regras de instalador geridos podem executar em dois modos:

- Modo de auditoria – as aplicações são nota impedida a execução, mas todas as aplicações que teriam sido bloqueadas são comunicadas num ficheiro de registo (isto será suportado numa versão posterior do Configuration Manager).
- Imposição ativada – aplicações estão a respetiva execução bloqueada.

Mais informações sobre como utilizar a proteção de dispositivos com o Configuration Manager podem ser encontradas no [blogue do Enterprise Mobility e segurança](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Ler mais:

- [Introdução de proteção de dispositivos](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Certificação de proteção de dispositivos e de conformidade](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guia de implementação de proteção de dispositivos](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

 ##  <a name="dmp_onprem"></a> Vários pontos de gestão de dispositivos para gestão de dispositivos móveis no local  
 Com o Technical pré-visualizar 1606, no\-disponíveis para utilização do ponto de gestão de dispositivos móveis (MDM) suporta uma nova capacidade no Windows 10 aniversário da atualização que configura automaticamente um dispositivo inscrito tem mais do que uma gestão de dispositivos de local. Esta capacidade permite ao dispositivo para contingência para outro ponto de gestão de dispositivos quando um normal utiliza não está disponível. Esta capacidade funciona apenas para PCs com Windows 10 aniversário da atualização instalada.  

### <a name="try-it-out"></a>Experimente!  

1.  Instale mais do que um ponto de gestão de dispositivos na sua hierarquia.  

2.  Inscrever um dispositivo Windows 10 Anniversary Update no\-no local a gestão de dispositivos móveis.  

Para obter informações sobre como preparar o seu site e inscrever dispositivos para no\-local gestão de dispositivos móveis, consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Serviço de Proxy de nuvem para gerir clientes na Internet

O serviço de Proxy de nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local através de uma nova função de chamar o ponto de conector do proxy de nuvem. Assim que tiver completamente implementado e configurado, os clientes serão capazes de aceder às funções do sistema de sites no local do Configuration Manager, independentemente se estão ligados à rede privada interna ou na Internet.

Utilize a consola do Configuration Manager para implementar o serviço do Azure, adicione a função de ponto de conector de proxy de nuvem e configurar funções de sistema de sites para permitir o tráfego de proxy de nuvem. Serviço de Proxy de nuvem atualmente suporta apenas o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software.

São necessários certificados de cliente e certificados de Secure Socket Layer (SSL) para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço. Computadores cliente recebem normalmente um certificado de cliente através da imposição de política de grupo. Para encriptar o tráfego entre clientes e servidor de sistema de sites que alojam as funções, terá de criar um certificado SSL personalizado da AC. Para além destes dois tipos de certificados, também tem de configurar um certificado de gestão no Azure que permite ao Configuration Manager para implementar o serviço de Proxy de nuvem.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos para o serviço de Proxy de nuvem no TP 1606
- Computadores cliente e o servidor de sistema de sites com o ponto do conector do proxy de nuvem.
- Certificados SSL personalizados da AC interna - utilizado para encriptar a comunicação entre os computadores cliente e autenticar a identidade do serviço de Proxy de nuvem.
- Subscrição do Azure para serviços em nuvem.
- Certificado de gestão do Azure - utilizado para autenticar o Configuration Manager com o Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitações do serviço de Proxy de nuvem no TP 1606

- Só suporta o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software.
- Políticas de utilizador não são suportadas.
- Não pode ser utilizado com [gestão de dispositivos móveis no local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no Configuration Manager.
- Só é suportado na plataforma de nuvem pública do Azure.


### <a name="try-it-out"></a>Experimente!

O processo de implementação do serviço de Proxy de nuvem inclui os seguintes passos:

1. Criar e emitir um certificado SSL personalizado para o serviço de Proxy de nuvem.
1. Exporte a raiz do certificado de cliente.
2. Carregue o certificado de gestão para o Azure.
3. Configure o serviço de Proxy de nuvem na consola do Configuration Manager.
4. Configure o site primário a utilizar a autenticação de certificado de cliente.
5. Adicione o ponto de conector do proxy de nuvem ao seu site.
6. Configure as funções de sistema de sites para aceitar o tráfego de proxy de nuvem.

As secções seguintes fornecem informações adicionais para concluir estes passos.

#### <a name="create-a-custom-ssl-certificate"></a>Criar um certificado SSL personalizado

Pode criar um certificado SSL personalizado para o serviço de Proxy de nuvem da mesma forma que faria fazê-lo para um ponto de distribuição baseado na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetue os seguintes procedimentos de forma diferente:

* Quando configurar o novo modelo de certificado, atribua **leitura** e **inscrever** permissões para o grupo de segurança que configurou para servidores do Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exportar a raiz do certificado de cliente

A forma mais fácil de obter a raiz dos certificados de cliente utilizado na rede, está a abrir um certificado de cliente numa das máquinas associados a um domínio que tenha um e copie-a exportação.

>[!NOTE]
>São necessários certificados de cliente em qualquer computador que pretende gerir com o serviço de Proxy de nuvem e no servidor do sistema de sites que aloja o conector do proxy de nuvem do ponto. Se precisar de adicionar um certificado de cliente a qualquer uma destas máquinas, consulte [implementar o cliente certificados para computadores com o Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. Na janela executar, escreva **mmc** e prima regressar.
2. No menu ficheiro, na consola de gestão, clique em **Adicionar/Remover Snap-in...** .
3. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **certificados**, clique em **adicionar >**, clique em **conta de computador**, clique em **seguinte**, clique em **computador Local**e, em seguida, clique em **concluir**. Clique em **OK** para fechar a caixa de diálogo.
4. Aceda a **certificados > pessoal > certificados**.
5. Faça duplo clique o certificado para autenticação de cliente no computador, clique no separador de caminho de certificação e faça duplo clique a autoridade de raiz (na parte superior do caminho).
6.  Clique no separador de detalhes e clique em **copiar para ficheiro...** .
7. Conclua o Assistente para exportar certificados utilizando o formato de certificado predefinido. Tome nota do nome do e localização do certificado de raiz que cria. Precisará dele para configurar o serviço de Proxy de nuvem num passo posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Carregar o certificado de gestão para o Azure

Um certificado de gestão do Azure é necessário para o Configuration Manager para aceder à API do Azure e configurar o serviço de Proxy de nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gestão, consulte os artigos seguintes na documentação do Azure:
- [Descrição geral de certificados para serviços de nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Carregar um certificado de gestão de API de gestão do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Certifique-se ao copiar o ID de subscrição associado o certificado de gestão. Precisará dela para configurar o serviço de Proxy de nuvem na consola do Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurar o serviço de Proxy de nuvem

1. Na consola do Configuration Manager, vá para **administração > Serviços Cloud > serviço de Proxy de nuvem**.
2. Clique em **criar serviço de Proxy de nuvem**.
3. No assistente criar nuvem Proxy de serviço, introduza o seu ID de subscrição do Azure (copiada a partir do portal de gestão do Azure), em seguida, clique em Procurar e selecione o ficheiro de certificado utilizado para carregar um certificado de gestão do Azure. Clique em **Seguinte**. Aguarde um momento para a consola para ligar ao Azure.
4. Preencha os detalhes adicionais no assistente:
    - Especifique a chave privada (ficheiro. pfx) que exportou do certificado SSL personalizado.
    - Especifique o certificado de raiz exportado do certificado de cliente.
    - Especifique o mesmo nome de serviço FQDN que utilizou quando criou o novo modelo de certificado.
    - Desmarque a caixa junto a **verificar a revogação de certificados de cliente** (exceto se estiver a publicamente publicar as suas informações de CRL).
    - Clique em **seguinte** quando tiver terminado.
5. Reveja as definições e clique em **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Quando concluir o assistente, pode clicar em **fechar**; no entanto, irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique o **estado** coluna para a configuração recentemente o serviço de Proxy de nuvem para determinar quando o serviço está pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurar o site primário certificação para autenticação de cliente

1. Na consola do Configuration Manager, vá para **administração > Configuração do Site > Sites**.
2. Selecione o site primário para os clientes que pretende gerir através do serviço de Proxy de nuvem e clique em **propriedades**.
3. No separador de comunicações de computadores cliente da folha de propriedades de site primário, selecione a caixa junto **certificado de cliente PKI de utilização (autenticação de cliente) se estiver disponível**.
4. Certifique-se que limpe a caixa junto a **clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**. Esta opção apenas seriam necessária se publicamente foram publicar o CRL.
5. Clique em **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Adicionar o ponto de conector do proxy de nuvem

O ponto de conector do proxy de nuvem é uma nova função de sistema de site para comunicar com o serviço de Proxy de nuvem. Para adicionar o ponto de conector do proxy de nuvem, siga as instruções em [adicionar funções do sistema de site para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurar funções para o tráfego de proxy de nuvem

O passo final na configuração do serviço de Proxy de nuvem é configurar as funções de sistema de sites para aceitar o tráfego de proxy de nuvem. Para 1606 de pré-visualização do técnico, apenas o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software são suportadas para o serviço de Proxy de nuvem. Tem de configurar cada função em separado.

1. Na consola do Configuration Manager, vá para **administração > Configuração do Site > servidores e funções de sistema de sites**.
2. Clique no servidor do sistema de site para a função que pretende configurar para o tráfego de proxy de nuvem.
3. Clique na função e, em seguida, clique em **propriedades**.
4. Na folha de propriedades da função, em ligações de cliente, escolha **HTTPS**, a caixa de verificação junto a **tráfego de Proxy de nuvem do Configuration Manager permitem**e, em seguida, clique em **OK**. Repita estes passos para as restantes funções.

#### <a name="check-status-on-a-client-on-the-internet"></a>Verifique o estado num cliente na Internet

Depois do serviço e as funções se encontram completamente configuradas, os clientes internos irão obter a localização do serviço de Proxy de nuvem no próximo pedido de localização. Os clientes com informações de localização atualizada, em seguida, podem comunicar com o Configuration Manager na Internet. O ciclo de consulta de pedidos de localização é a cada 24 horas. Se não pretender aguardar que o pedido de localização normalmente agendada, pode forçar o pedido reiniciando o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.

Depois dos clientes têm as novas informações de localização do serviço de Proxy de nuvem, tente verificar o estado dos clientes que já não estão na rede privada interna, mas têm acesso à Internet. Também pode monitorizar o tráfego no serviço de Proxy de nuvem, acedendo a **administração > Serviços Cloud > serviço de Proxy de nuvem**, selecionando o serviço no painel de lista e visualizar as informações de tráfego no painel de detalhes.   

## <a name="manage_o365"></a>Gerir o agente do cliente do Office 365 no Configuration Manager  

A partir do Technical Preview 1606, pode utilizar uma definição, em vez de política de grupo de agente do cliente do Configuration Manager para permitir aos clientes do Office 365 receber atualizações do Configuration Manager. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente do cliente do Office 365 para transferir atualizações do Office 365 a partir de um ponto de distribuição e instalá-los. O Configuration Manager também demora inventário da definição do agente de cliente.

Para obter mais informações, consulte [de atualizações de gerir o Office 365 ProPlus](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Configurar o definição para gerir o agente do cliente do Office 365 de cliente do Configuration Manager
1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **as definições de cliente**.
2. Abra as definições de dispositivo adequados para ativar o agente de cliente. Para obter mais informações sobre as definições de cliente personalizadas e predefinidas, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  


## <a name="osdpreservedriveletter"></a>A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter determina se é ou não a sequência de tarefas utiliza a letra de unidade capturada no ficheiro WIM da imagem do sistema operativo ao aplicar essa imagem a um computador de destino.
- Esta variável de sequência de tarefas foi preterido no 1606 de pré-visualização técnica.

Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a letra de unidade melhor a utilizar (normalmente c). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecionar a localização onde pretende aplicar este sistema operativo** definição, selecione **letra de unidade lógica específica**e escolha a unidade que pretende utilizar. Tem de existir uma unidade atribuída com a letra que escolha no computador de destino. 

## <a name="updatesandservicing"></a>Alterações para as atualizações e manutenção de nó
Com o Technical Preview 1606 várias alterações foram introduzidas que se aplicam a atualizações e manutenção na consola do Configuration Manager:
- **Alteração do nome de nó:**

    No **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi mudado para **atualizações e manutenção estado**.
- **Estado de instalação mais:**

    Ao visualizar o estado de instalação de atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (Isto aplica-se apenas para o site de nível superior em que a função de sistema de sites de ponto de ligação de serviço está instalada)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, existe agora informações mais detalhadas de cada passo, incluindo no ficheiro de registo que pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **administração** e **monitorização** áreas de trabalho, o **atualizações e manutenção** nó inclui um novo botão no Friso denominado **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar os avisos de pré-requisitos (de dentro do Assistente de atualização), e que para a instalação da atualização com o estado de **aviso relatado**, em seguida, pode selecionar **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática dessa instalação de atualização que ignora os avisos de pré-requisitos.  



- **Vista de limpeza de atualizações:**

    Ao visualizar o **atualizações e manutenção** nós, agora ver apenas a atualização instalada mais recentemente e novas atualizações que estão disponíveis para a instalação. Para ver atualizações instaladas anteriormente, clique no novo **histórico** botão que aparece no Friso.  

-   **Opção cujo nome foi alterada para pré-produção:**

    As atualizações e manutenção de nó, o botão que foi atribuído o nome **opções de clientes** agora é alterado para **promover o cliente de pré-produção**.
