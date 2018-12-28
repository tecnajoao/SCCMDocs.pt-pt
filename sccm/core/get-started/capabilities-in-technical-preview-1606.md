---
title: Funcionalidades no Technical Preview versão 1606
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
ms.openlocfilehash: 14e982592491ec5e8a10cd3313f748bddac40cff
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420079"
---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1606. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    

**Problemas conhecidos neste Technical Preview:**  
*  Quando atualizar a partir do Technical Preview 1604 para 1605 e, em seguida, para a versão 1606, a atualização poderá falhar e um erro semelhante ao seguinte tem sessão iniciado a **cmupdate. log**:

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    Se isto ocorrer, além do **atualizações e manutenção** nó clique **procurar atualizações**e, em seguida, **repita** a instalação da atualização.
    ***

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="dmp_category"></a> Categorizar automaticamente os dispositivos em coleções
Pode criar categorias de dispositivos, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Em seguida, os utilizadores têm de escolher uma categoria de dispositivo quando estes inscrevem um dispositivo no Intune. Além disso, é possível alterar a categoria de um dispositivo da consola do Configuration Manager.

**Importante:** Esse recurso funciona com o **Junho de 2016** versão do Microsoft Intune. Certifique-se de que tiver sido atualizado para esta versão antes de experimentar estes procedimentos.

### <a name="try-it-out"></a>Experimente!

### <a name="create-a-set-of-device-categories"></a>Criar um conjunto de categorias de dispositivos
1.  Na **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **coleções de dispositivos**.
2.  Sobre o **home page** separador a **categorias** , clique em **gerir categorias de dispositivos**.
3.  Na **gerir categorias de dispositivos** caixa de diálogo, pode criar, editar ou remover as categorias. Tente criar uma nova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo
Quando associa uma coleção com uma categoria de dispositivo, todos os dispositivos da categoria que especificar serão adicionados a essa coleção.
1.  Na **propriedades** caixa de diálogo para uma coleção de dispositivos, clique em **Adicionar regra** > **regra de categoria de dispositivo**.
2.  Na **criar regra de associação de categoria de dispositivo** diálogo caixa, selecione a categoria que será aplicada a todos os dispositivos na coleção.
3.  Fechar o **criar regra de associação de categoria de dispositivo** caixa de diálogo e a caixa de diálogo de propriedades de coleção.

### <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo
1.  Na **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **dispositivos**.
2.  Selecione um dispositivo a partir da **dispositivos** lista e, em seguida, no **home page** separador o **dispositivo** , clique em **alterar categoria**.
3.  Na **Editar categoria de dispositivos** caixa de diálogo caixa, escolha a categoria para aplicar a este dispositivo, em seguida, clique em **OK**.

## <a name="dmp_grace"></a> Período de tolerância de imposição para a aplicação necessária e implementações de atualizações de software

Em alguns casos, talvez queira dar aos utilizadores mais tempo para implementações de aplicações é necessária instalação ou atualização de software para além de quaisquer prazos configurados. Isso pode normalmente ser necessário quando um computador foi desativado por um longo período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização.
Por exemplo, se um utilizador final acabou de voltar de férias, poderá ter de aguardar por um longo enquanto como aplicação em atraso implementações estão instaladas.
Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

### <a name="try-it-out"></a>Experimente!

Para configurar o período de tolerância, efetue as seguintes ações:

1.  Sobre o **agente do computador** página de definições de cliente, configurar a nova propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.  Numa nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, sobre o **agendamento** , selecione a caixa de verificação **Trasar imposição para esta implementação, de acordo com as preferências do usuário**, até o período de tolerância definido nas definições do cliente.
Todas as implementações com esta caixa de verificação selecionada e que é direcionado para os dispositivos em que implementou também a definição de cliente utilizará o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação do aplicativo, será instalado na primeira janela não comerciais que o utilizador configurado até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação a qualquer momento que desejarem. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.
Foram adicionadas opções similares para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades.

##  <a name="dmp_devg"></a>Utilizar o Configuration Manager como um instalador gerido com Device Guard

O Device Guard é uma funcionalidade do Windows 10 que utiliza o hardware e as funcionalidades de software para estritamente controlar o que pode ser executada no dispositivo.

Pode ler uma visão geral detalhada do que o Device Guard faz e como ele funciona em [este artigo do Technet](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

Nesta versão, o Configuration Manager podem interoperar com o Device Guard e [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) para que o executável e os arquivos DLL, que são implementados com o Configuration Manager são considerados como fidedignos automaticamente à medida que elas venham de uma gerida Instalador, que significa que terá permissão para executar no dispositivo de destino e outro software não terá permissão para ser executado, a menos que explicitamente permissão para ser executada por outras regras de AppLocker.  

No momento, esta capacidade não está configurável a partir da consola do Configuration Manager. Para configurar a política tem de configurar uma chave de registo em cada cliente e configurar os serviços do Windows no cliente.
Depois de o fazer, configure o arquivo de política de AppLocker. Depois de configurar o ficheiro de política, pode implementá-la para qualquer dispositivo de cliente compatível.


Como todas as políticas de AppLocker, as políticas com regras de instalador gerido podem ser executado em dois modos:

- Modo de auditoria – os aplicativos são nota impedida a execução, mas todas as aplicações que poderiam ter sido bloqueadas são comunicadas num ficheiro de registo (isso vai ser suportado numa versão posterior do Configuration Manager).
- Imposição ativada – aplicativos ficam bloqueados de execução.

Obter mais informações sobre como utilizar o Device Guard com o Configuration Manager podem ser encontradas no [blogue do Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Leitura adicional:

- [Introdução de proteção do dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Certificação de proteção de dispositivos e conformidade](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guia de implementação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="dmp_onprem"></a> Vários pontos de gestão de dispositivos para gestão de dispositivos móveis no local  
  Com o Technical Preview versão 1606, no\-disponível para utilização do ponto de gestão de dispositivos móveis (MDM) suporta uma nova capacidade na atualização de aniversário do Windows 10 que configura automaticamente um dispositivo inscrito para ter mais de uma gestão de dispositivos de local. Esta capacidade permite ao dispositivo para contingência para outro ponto de gestão de dispositivos quando aquele normal utiliza não está disponível. Esta funcionalidade só funciona para PCs com Windows 10 Anniversary Update instalado.  

### <a name="try-it-out"></a>Experimente!  

1.  Instale mais do que um ponto de gestão de dispositivos na sua hierarquia.  

2.  Inscrever um dispositivo de atualização de aniversário do Windows 10 no\-no local a gestão de dispositivos móveis.  

Para obter informações sobre como preparar o seu site e inscrever dispositivos para em\-locais gestão de dispositivos móveis, consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Serviço de Proxy de nuvem para gerir clientes na Internet

Serviço de Proxy de nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, o que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local com uma nova função chamada o ponto de conector de proxy de nuvem. Assim que tiver totalmente implementado e configurado, os clientes será capazes de acessar as funções do sistema de sites no local do Configuration Manager, independentemente de se eles estão conectados à rede interna privada ou na Internet.

Utilize a consola do Configuration Manager para implementar o serviço no Azure, adicione a função de ponto de conector de proxy de nuvem e configurar funções de sistema de sites para permitir o tráfego do proxy de nuvem. Serviço de Proxy de nuvem atualmente suporta apenas o ponto de gestão, ponto de distribuição e funções de ponto de atualização de software.

São necessários certificados de cliente e certificados de Secure Socket Layer (SSL) para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço. Computadores cliente normalmente recebem um certificado de cliente por meio de imposição de política de grupo. Para encriptar o tráfego entre clientes e servidor de sistema de sites que alojam as funções, terá de criar um certificado SSL personalizado a partir da AC. Além desses dois tipos de certificados, também tem de configurar um certificado de gestão do Azure, que permite ao Configuration Manager para implementar o serviço de Proxy de nuvem.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos para o serviço de Proxy de nuvem no TP 1606
- Computadores cliente e o servidor de sistema de sites com o proxy de nuvem ponto do conector.
- Certificados SSL personalizados da AC interna - utilizado para encriptar a comunicação dos computadores cliente e autenticar a identidade do serviço de Proxy de nuvem.
- Subscrição do Azure para serviços em nuvem.
- Certificado de gestão do Azure – utilizado para autenticar o Configuration Manager com o Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitações do serviço de Proxy de nuvem no TP 1606

- Suporta apenas o ponto de gestão, ponto de distribuição e funções de ponto de atualização de software.
- Políticas de utilizador não são suportadas.
- Não pode ser utilizado com [gestão de dispositivos móveis no local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no Configuration Manager.
- Só é suportado na plataforma de cloud pública do Azure.


### <a name="try-it-out"></a>Experimente!

O processo de implementação do serviço de Proxy de nuvem inclui os seguintes passos:

1. Criar e emitir um certificado SSL personalizado para o serviço de Proxy de nuvem.
1. Exporte a raiz do certificado de cliente.
2. Carregar o certificado de gestão para o Azure.
3. Configure o serviço de Proxy de nuvem na consola do Configuration Manager.
4. Configure o site primário para utilizar a autenticação de certificado de cliente.
5. Adicione o ponto de conector de proxy de nuvem ao seu site.
6. Configure as funções de sistema de sites para aceitar o tráfego do proxy de nuvem.

As secções seguintes fornecem mais informações para concluir estes passos.

#### <a name="create-a-custom-ssl-certificate"></a>Criar um certificado SSL personalizado

Pode criar um certificado SSL personalizado para o serviço de Proxy de nuvem da mesma forma que deve fazer isso para um ponto de distribuição baseado na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseados na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetue os seguintes procedimentos de forma diferente:

* Quando configurar o novo modelo de certificado, atribua **leitura** e **inscrever** permissões para o grupo de segurança que configurou para os servidores do Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exportar a raiz do certificado de cliente

A maneira mais fácil para obter a raiz dos certificados de cliente utilizado na rede, é abrir um certificado de cliente em uma das máquinas associado a um domínio que tenha um e copie-a exportação.

>[!NOTE]
>Certificados de cliente são necessários em qualquer computador que pretende gerir com o serviço de Proxy de nuvem e no servidor do sistema de sites que aloja o conector do proxy de nuvem do ponto. Se precisar de adicionar um certificado de cliente a qualquer uma dessas máquinas, consulte [implementação de certificado de cliente para Windows computadores](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. Na janela executar, escreva **mmc** e pressiona Return.
2. No menu Arquivo, na consola de gestão, clique em **Adicionar/Remover Snap-in...** .
3. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **certificados**, clique em **adicionar >**, clique em **conta de computador**, clique em **seguinte**, clique em **Computador local**e, em seguida, clique em **concluir**. Clique em **OK** para fechar a caixa de diálogo.
4. Aceda a **certificados > pessoal > certificados**.
5. Clique duas vezes o certificado para autenticação de cliente no computador, clique no separador de caminho de certificação e clique duas vezes a autoridade de raiz (na parte superior do caminho).
6.  Clique no separador de detalhes e clique em **copiar para ficheiro...** .
7. Conclua o Assistente para exportar certificados utilizando o formato de certificado predefinido. Torne nota do nome e localização do certificado de raiz que cria. Irá precisar dele para configurar o serviço de Proxy de nuvem num passo posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Carregar o certificado de gestão para o Azure

Um certificado de gestão do Azure é necessário para o Configuration Manager para aceder à API do Azure e configurar o serviço de Proxy de nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gestão, veja os artigos seguintes na documentação do Azure:
- [Descrição geral de certificados para serviços Cloud do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Carregar um certificado de gestão de API de gestão do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Certifique-se copiar o ID de subscrição associado ao certificado de gestão. Irá precisar dele para configurar o serviço de Proxy de nuvem na consola do Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurar o serviço de Proxy de nuvem

1. Na consola do Configuration Manager, aceda a **administração > Serviços Cloud > serviço de Proxy de nuvem**.
2. Clique em **criar serviço de Proxy de nuvem**.
3. No Cloud Proxy de serviço de Assistente para criar, introduza o seu ID de subscrição do Azure (copiado de portal de gestão do Azure), em seguida, clique em Procurar e selecione o ficheiro de certificado utilizado para carregar como um certificado de gestão do Azure. Clique em **Seguinte**. Aguarde alguns momentos para a consola ligar ao Azure.
4. Preencha os detalhes adicionais no assistente:
    - Especifica a chave privada (ficheiro. pfx) que exportou a partir do certificado SSL personalizado.
    - Especifique o certificado de raiz exportado a partir do certificado de cliente.
    - Especifique o mesmo nome de serviço FQDN que utilizou quando criou o novo modelo de certificado.
    - Desmarque a caixa junto a **verificar revogação de certificados de cliente** (a menos que está publicando publicamente suas informações de CRL).
    - Clique em **seguinte** quando terminar.
5. Reveja as definições e clique em **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Quando concluir o assistente, pode clicar **fechar**, no entanto, irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique os **estado** coluna para a configuração recentemente o serviço de Proxy de nuvem para determinar quando o serviço está pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurar o site primário para a autenticação de certificação do cliente

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > Sites**.
2. Selecione o site primário para os clientes que pretende gerir através do serviço de Proxy de nuvem e clique em **propriedades**.
3. No separador de comunicações do computador cliente, o site primário da folha de propriedades, selecione a caixa junto a **certificado de cliente PKI de utilização (autenticação de cliente) quando estiverem disponíveis**.
4. Lembre-se de que desmarque a caixa junto a **os clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**. Esta opção só seriam necessária se publicamente estivessem publicando seu CRL.
5. Clique em **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Adicionar o ponto de conector de proxy de nuvem

O ponto de conector de proxy de nuvem é uma nova função de sistema de sites para comunicação com o serviço de Proxy de nuvem. Para adicionar o ponto de conector de proxy de nuvem, siga as instruções em [adicionar funções do sistema de site para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurar funções para o tráfego do proxy de nuvem

A etapa final na configuração de serviço de Proxy de nuvem é configurar as funções de sistema de sites para aceitar o tráfego do proxy de nuvem. Para Tech Preview 1606, apenas o ponto de gestão, ponto de distribuição e funções de ponto de atualização de software são suportadas para o serviço de Proxy de nuvem. Tem de configurar cada função em separado.

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > servidores e funções de sistema de sites**.
2. Clique no servidor do sistema de site para a função que pretende configurar para o tráfego do proxy de nuvem.
3. Clique na função e, em seguida, clique em **propriedades**.
4. Na folha de propriedades de função, em ligações de cliente, escolha **HTTPS**, a caixa de verificação junto a **tráfego do Proxy de nuvem do Configuration Manager permitem**e, em seguida, clique em **OK**. Repita estes passos para as funções restantes.

#### <a name="check-status-on-a-client-on-the-internet"></a>Verificar o estado num cliente na Internet

Depois do serviço e as funções são totalmente configuradas, os clientes internos irão obter a localização do serviço de Proxy de nuvem no próximo pedido de localização. Os clientes com informações de localização atualizada, em seguida, podem comunicar com o Configuration Manager na Internet. O ciclo de consulta para pedidos de localização é a cada 24 horas. Se não quiser aguardar que o pedido de localização normalmente agendada, pode forçar o pedido ao reiniciar o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.

Depois dos clientes tiverem as novas informações de localização de serviço de Proxy de nuvem, tente verificar o estado de clientes que já não estão na rede interna privada, mas têm acesso à Internet. Também pode monitorizar o tráfego no serviço de Proxy de nuvem ao aceder **administração > Serviços Cloud > serviço de Proxy de nuvem**, selecione o serviço no painel de lista e consulte as informações de tráfego no painel de detalhes.   

## <a name="manage_o365"></a>Gerir o agente de cliente do Office 365 no Configuration Manager  

A partir da versão 1606 de pré-visualização técnica, pode utilizar uma definição, em vez de diretiva de grupo, de agente do cliente do Configuration Manager para permitir que os clientes do Office 365 receber atualizações do Configuration Manager. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente de cliente do Office 365 para transferir atualizações do Office 365 a partir de um ponto de distribuição e instalá-los. O Configuration Manager também substitui o inventário de definição do agente de cliente.

Para obter mais informações, consulte [atualizações de gerir o Office 365 ProPlus](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Definir a definição para gerir o agente do cliente do Office 365 de cliente do Configuration Manager
1.  Na consola do Configuration Manager, clique em **Administration** > **descrição geral** > **as definições de cliente**.
2. Abra as definições de dispositivo adequados para ativar o agente de cliente. Para obter mais informações sobre o padrão e definições de cliente personalizadas, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  


## <a name="osdpreservedriveletter"></a>A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter determina se é ou não a sequência de tarefas utiliza a letra de unidade capturada no ficheiro WIM da imagem do sistema operativo ao aplicar essa imagem a um computador de destino.
- Esta variável de sequência de tarefas foi preterida 1606 de pré-visualização técnica.

Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a melhor letra de unidade a utilizar (normalmente c). Se pretender especificar uma unidade diferente para utilizar, pode alterar o local no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecione a localização onde pretende aplicar este sistema operativo** definição, selecione **letra de unidade lógica específica**e escolha a unidade que pretende utilizar. Tem de existir uma unidade atribuída com a letra que escolher no computador de destino. 

## <a name="updatesandservicing"></a>Alterações para o nó atualizações e manutenção
Com a versão 1606 de pré-visualização técnica várias alterações foram introduzidas que se aplicam a atualizações e manutenção na consola do Configuration Manager:
- **Alteração de nome de nó:**

    Na **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi alterado para **atualizações e estado de manutenção**.
- **Estado de instalação mais:**

    Ao visualizar o estado de instalação de atualização para um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (Isto aplica-se apenas para o site de nível superior onde está instalada a função de sistema de sites de ponto de ligação de serviço)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, agora há informações mais detalhadas para cada passo, incluindo o ficheiro de registo pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **Administration** e **monitorização** áreas de trabalho, o **atualizações e manutenção** nó inclui um novo botão da faixa de opções com o nome **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar avisos de pré-requisitos (no Assistente de atualizações), e a instalação dessa atualização parar com um Estado de **aviso de pré-requisitos**, em seguida, pode selecionar **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática da instalação dessa atualização que ignora os avisos de pré-requisitos.  



- **Exibição mais clara de atualizações:**

    Ao visualizar o **atualizações e manutenção** nó, agora, ver apenas a atualização instalada mais recentemente e quaisquer novas atualizações que estão disponíveis para instalação. Para ver atualizações instaladas anteriormente, clique no novo **histórico** botão que aparece na faixa de opções.  

-   **Opção de nome mudada para pré-produção:**

    As atualizações e manutenção de nó, o botão que foi chamado **opções de clientes** agora foi mudado para **promover cliente de pré-produção**.
