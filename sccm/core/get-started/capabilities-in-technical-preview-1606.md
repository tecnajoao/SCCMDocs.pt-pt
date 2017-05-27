---
title: "Capacidades na pré-visualização técnica 1606 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1606."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
caps.latest.revision: 31
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 7cb553d553a1d2e3118731118a566c38e7b4e161
ms.openlocfilehash: 08747ca981f6697e2bd621afe5df0e3bd06b332d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1606 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1606. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    

**Problemas conhecidos neste pré-visualização técnica:**  
*  Quando atualizar a partir da pré-visualização técnica 1604 para 1605 e, em seguida, à versão 1606, a atualização poderá falhar e um erro semelhante ao seguinte é registado **cmupdate.log**:

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    Se isto ocorrer, no **atualizações e a manutenção** nó clique **procurar atualizações**e, em seguida, **repita** a instalação da atualização.
    ***

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="dmp_category"></a>Categorizar automaticamente os dispositivos em coleções
Pode criar categorias de dispositivo, o que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando está a utilizar o Configuration Manager com o Microsoft Intune. Os utilizadores, em seguida, são necessários para escolher uma categoria de dispositivo quando estes inscreverem um dispositivo no Intune. Além disso pode alterar a categoria de um dispositivo a partir da consola do Configuration Manager.

**Importante:** Esta capacidade é funciona com o **Junho de 2016** versão do Microsoft Intune. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

### <a name="try-it-out"></a>Experimente!

### <a name="create-a-set-of-device-categories"></a>Criar um conjunto de categorias de dispositivos
1.  No **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **coleções de dispositivos**.
2.  No **base** separador o **categorias** grupo, clique em **gerir categorias de dispositivo**.
3.  No **gerir categorias de dispositivo** caixa de diálogo, pode criar, editar ou remover categorias. Tente criar uma nova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo
Quando associar uma coleção com uma categoria de dispositivo, todos os dispositivos da categoria que especificar serão adicionados a essa coleção.
1.  No **propriedades** caixa de diálogo para uma coleção de dispositivos, clique em **Adicionar regra** > **dispositivo categoria de regra**.
2.  No **criar regra de associação de categoria de dispositivo** diálogo caixa, selecione a categoria que será aplicada a todos os dispositivos da coleção.
3.  Fechar o **criar regra de associação de categoria de dispositivo** caixa de diálogo e a caixa de diálogo de propriedades de coleção.

### <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo
1.  No **ativos e compatibilidade** área de trabalho da consola do Configuration Manager, expanda **descrição geral**, em seguida, clique em **dispositivos**.
2.  Selecione um dispositivo a partir do **dispositivos** lista e, em seguida, no **base** no separador de **dispositivo** grupo, clique em **alterar uma categoria**.
3.  No **Editar categoria de dispositivo** diálogo caixa, selecione a categoria para aplicar a este dispositivo, em seguida, clique em **OK**.

## <a name="dmp_grace"></a>Período de tolerância de imposição para aplicação necessária e implementações de atualizações de software

Em alguns casos, poderá conceder aos utilizadores mais tempo a instale necessário implementações de aplicações ou atualizações de software para além de qualquer prazos que configurou. Isto pode normalmente ser necessário quando um computador foi desativado por um determinado período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização.
Por exemplo, se um utilizador final apenas tiver devolvido de férias, poderá ter de aguardar por uma longa enquanto como uma aplicação em atraso implementações estão instaladas.
Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição implementando definições de cliente do Configuration Manager a uma coleção.

### <a name="try-it-out"></a>Experimente!

Para configurar o período de tolerância, execute as ações seguintes:

1.  No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.  Uma nova implementação de aplicações necessárias, ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar a imposição desta implementação, de acordo com as preferências do utilizador**, até o período de tolerância definido nas definições de cliente.
Todas as implementações que tenham esta caixa de verificação selecionada e são direcionadas para dispositivos em que também implementada a definição de cliente irão utilizar o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação da aplicação, este será instalado na primeira janela de negócio não que o utilizador configurado até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação em qualquer altura que queiram. Depois do período de tolerância expirar, a imposição reverte para comportamento normal para implementações em atraso.
Foram adicionadas opções semelhantes ao Assistente de regras de implementação automática, o Assistente de implementação de atualizações de software e páginas de propriedades.

##  <a name="dmp_devg"></a>Utilizar o Configuration Manager como um instalador gerido com a proteção de dispositivo

Proteção de dispositivo é uma funcionalidade do Windows 10 que utiliza o hardware e funcionalidades de software para estritamente controlar o que é permitido para ser executada no dispositivo.

Pode ler uma descrição geral detalhada do objetivo de proteção de dispositivo e como funciona no [neste artigo da Technet](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

Nesta versão, o Configuration Manager pode interagir com a proteção de dispositivo e [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) para que o executável e os ficheiros DLL que são implementados com o Configuration Manager são automaticamente fidedignos como voltarem a partir de um instalador geridos, que significa que que terá permissão para ser executado no dispositivo de destino e outros programas de software não terá permissão para ser executada, a menos que explicitamente permitida a execução por outras regras AppLocker.  

Atualmente, esta capacidade não é configurável a partir da consola do Configuration Manager. Configurar a política tem de configurar uma chave de registo em cada cliente e configurar os serviços Windows no cliente.
Depois de esta operação é feita, configure o ficheiro de política de AppLocker. Depois de configurar o ficheiro de política, pode implementá-lo em qualquer dispositivo de cliente compatível.


Como todas as políticas AppLocker, políticas com regras de instalador geridos podem executar nos dois modos:

- Modo de auditoria – as aplicações são nota impedida a execução, mas todas as aplicações que poderiam ter sido bloqueadas são comunicadas num ficheiro de registo (isto será suportado numa versão posterior do Configuration Manager).
- Imposição ativada – aplicações estão bloqueados relativamente em execução.

Mais informações sobre como utilizar a proteção de dispositivo com o Configuration Manager podem ser encontradas no [blogue Enterprise Mobility e segurança](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Leitura adicional:

- [Introdução de proteção do dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Certificação de proteção do dispositivo e conformidade](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guia de implementação de proteção do dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

 ##  <a name="dmp_onprem"></a>Vários pontos de gestão de dispositivos para gestão de dispositivos móveis no local  
 Pré-visualizar 1606, com técnicos\-disponíveis para utilização do ponto de instalações, gestão de dispositivos móveis (MDM) suporta uma nova funcionalidade no Windows 10 aniversário Update que configura automaticamente um dispositivo para ter mais do que uma gestão de dispositivos inscrito. Esta capacidade permite que o dispositivo reversão para outro ponto de gestão de dispositivos, quando um normal utiliza não está disponível. Esta capacidade é funciona apenas para PCs com Windows 10 aniversário atualização instalada.  

### <a name="try-it-out"></a>Experimente!  

1.  Instale mais do que um ponto de gestão de dispositivos na sua hierarquia.  

2.  Inscrever um dispositivo de atualização do Windows 10 aniversário no\-local gestão de dispositivos móveis.  

Para obter informações sobre como preparar o seu site e inscrever dispositivos para no\-local gestão de dispositivos móveis, consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Serviço de Proxy de nuvem para gerir clientes na Internet

Serviço de Proxy de nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, que é implementado para o Microsoft Azure e necessita de uma subscrição do Azure, liga-se para a infraestrutura do Configuration Manager no local com uma nova função de denominado o ponto de proxy de conector em nuvem. Assim que tiver completamente implementados e configurados, os clientes serão capazes de aceder às funções do sistema de sites no local do Configuration Manager, independentemente de se estão ligados à rede privada interna ou na Internet.

Utilize a consola do Configuration Manager para implementar o serviço para o Azure, adicione a função de ponto de conector de proxy de nuvem e configurar funções de sistema de sites para permitir tráfego de proxy de nuvem. Serviço de Proxy de nuvem atualmente só suporta o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software.

São necessário para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço de certificados de cliente e certificados de Secure Socket Layer (SSL). Computadores cliente, normalmente, recebem um certificado de cliente através de imposição de política de grupo. Para encriptar o tráfego entre clientes e que aloja as funções de servidor do sistema de sites, terá de criar um certificado SSL personalizado a partir da AC. Para além destes dois tipos de certificados, também tem de configurar um certificado de gestão no Azure que permite ao Configuration Manager para implementar o serviço de Proxy de nuvem.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos para o serviço de Proxy de nuvem no TP 1606
- Computadores cliente e servidor de sistema do site, o proxy de nuvem a executar o ponto de conector.
- Certificados SSL personalizados a partir da AC interna - utilizado para encriptar a comunicação a partir de computadores cliente e autenticar a identidade do serviço de Proxy de nuvem.
- Subscrição do Azure para serviços em nuvem.
- Certificado de gestão do Azure – utilizado para autenticar o Configuration Manager com o Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitações do serviço de Proxy de nuvem no TP 1606

- Só suporta o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software.
- Não são suportadas políticas de utilizador.
- Não pode ser utilizado com [gestão de dispositivos móveis no local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no Configuration Manager.
- Só é suportado na plataforma de nuvem pública do Azure.


### <a name="try-it-out"></a>Experimente!

O processo de implementação de serviço de nuvem do Proxy inclui os seguintes passos:

1. Criar e emitir um certificado SSL personalizado para o serviço de Proxy de nuvem.
1. Exportação de raiz do certificado de cliente.
2. Carregar o certificado de gestão para o Azure.
3. Configure o serviço de Proxy de nuvem na consola do Configuration Manager.
4. Configure o site primário para utilizar a autenticação de certificados de cliente.
5. Adicione o ponto de proxy de conector em nuvem para o seu site.
6. Configure as funções do sistema de sites para aceitar o tráfego de proxy de nuvem.

As secções seguintes fornecem informações adicionais para concluir estes passos.

#### <a name="create-a-custom-ssl-certificate"></a>Criar um certificado SSL personalizado

Pode criar um certificado SSL personalizado para o serviço de Proxy de nuvem da mesma forma que faria fazê-lo para um ponto de distribuição baseado na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetuar o seguinte diferente:

* Quando configurar o novo modelo de certificado, dê **leitura** e **inscrever** permissões para o grupo de segurança que configurou para servidores do Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exportação de raiz do certificado de cliente

A forma mais fácil obter exportação raiz dos certificados de cliente utilizado na rede, deve abrir um certificado de cliente numa das máquinas associados a um domínio que tenha uma e copie-o.

>[!NOTE]
>São necessários certificados de cliente em qualquer computador que pretende gerir com o serviço de Proxy de nuvem e no servidor do sistema de sites que aloja o conector do proxy de nuvem ponto. Se precisar de adicionar um certificado de cliente a qualquer uma destas máquinas, consulte o artigo [implementar o cliente certificado para computadores com o Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. Na janela executar, escreva **mmc** e prima ENTER.
2. No menu ficheiro na consola de gestão, clique em **Adicionar/Remover Snap-in...** .
3. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **certificados**, clique em **adicionar >**, clique em **conta de computador**, clique em **seguinte**, clique em **computador Local**e, em seguida, clique em **concluir**. Clique em **OK** para fechar a caixa de diálogo.
4. Aceda a **certificados > pessoal > certificados**.
5. Faça duplo clique no certificado para autenticação de cliente no computador, clique no separador de caminho de certificação e faça duplo clique na autoridade de raiz (na parte superior do caminho).
6.  Clique no separador de detalhes e clique em **copiar para o ficheiro...** .
7. Conclua o Assistente para exportar certificados utilizando o formato de certificado de predefinição. Fazer nota do nome e localização do certificado de raiz que cria. Irá precisar dele para configurar o serviço de Proxy de nuvem num passo posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Carregar o certificado de gestão para o Azure

Um certificado de gestão do Azure é necessário para o Configuration Manager para aceder à API do Azure e configurar o serviço de Proxy de nuvem. Para mais informações e instruções sobre como carregar um certificado de gestão, consulte os artigos seguintes na documentação do Azure:
- [Descrição geral de certificados para serviços de nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Carregar um certificado de gestão de API de gestão Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Certifique-se copiar o ID de subscrição associado o certificado de gestão. Irá precisar dele para configurar o serviço de Proxy de nuvem na consola do Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurar o serviço de Proxy de nuvem

1. Na consola do Configuration Manager, aceda a **administração > Serviços em nuvem > serviço de nuvem do Proxy**.
2. Clique em **criar serviço de Proxy de nuvem**.
3. No assistente criação de nuvem Proxy de serviço, introduza o seu ID de subscrição do Azure (copiado a partir do portal de gestão do Azure), clique em Procurar e selecione o ficheiro de certificado que utilizou para carregar como um certificado de gestão do Azure. Clique em **Seguinte**. Aguarde alguns momentos para que a consola para ligar ao Azure.
4. Preencha os detalhes adicionais no assistente:
    - Especifique a chave privada (ficheiro. pfx) que exportou a partir do certificado SSL personalizado.
    - Especifique o certificado de raiz exportado a partir do certificado de cliente.
    - Especifique o mesmo nome de serviço FQDN que utilizou quando criou o novo modelo de certificado.
    - Desmarque a caixa junto a **Certifique-se de revogação de certificados de cliente** (exceto se estiver publicamente publicar as informações de CRL).
    - Clique em **seguinte** quando terminar.
5. Reveja as definições e clique em **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Quando o assistente ser concluído, pode clicar **fechar**; no entanto, irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique o **estado** coluna para a configuração recentemente o serviço de Proxy de nuvem para determinar quando o serviço está pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurar o site primário para autenticação de certificação de cliente

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > Sites**.
2. Selecione o site primário para os clientes que pretende gerir através do serviço de Proxy de nuvem e clique em **propriedades**.
3. No separador da folha de propriedades de site primário as comunicações do computador cliente, selecione a caixa junto a **certificado de cliente PKI de utilização (autenticação do cliente) se estiver disponível**.
4. Certifique-se de que desmarque a caixa junto a **verificam a lista de revogação de certificados (CRL) para sistemas de sites**. Esta opção apenas seria necessária se foram publicamente publicação de CRL.
5. Clique em **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Adicionar o ponto de proxy de conector em nuvem

O ponto de proxy de conector em nuvem é uma nova função de sistema de sites para comunicação com o serviço de Proxy de nuvem. Para adicionar o ponto de proxy de conector em nuvem, siga as instruções em [adicionar funções do sistema de sites para o System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurar funções para o tráfego de proxy de nuvem

O passo final na configuração do serviço de nuvem do Proxy é configuram as funções de sistema de sites para aceitar o tráfego de proxy de nuvem. Para Tech 1606 de pré-visualização, apenas o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software são suportadas para o serviço de Proxy de nuvem. Tem de configurar cada função separadamente.

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > servidores e funções de sistema de sites**.
2. Clique no servidor do sistema de sites para a função que pretende configurar para o tráfego de proxy de nuvem.
3. Clique a função e, em seguida, clique em **propriedades**.
4. Na folha de propriedades da função, em ligações de cliente, escolha **HTTPS**, a caixa de verificação junto a **tráfego de Proxy de nuvem do Configuration Manager permitir**e, em seguida, clique em **OK**. Repita estes passos para as restantes funções.

#### <a name="check-status-on-a-client-on-the-internet"></a>Verificar o estado de um cliente na Internet

Depois do serviço e as funções completamente estiverem configuradas, os clientes internos obterão a localização do serviço de Proxy de nuvem a pedido de localização seguinte. Os clientes com as informações de localização atualizada, em seguida, podem comunicar com o Configuration Manager na Internet. O ciclo de consulta para pedidos de localização é a cada 24 horas. Se não pretender aguardar que o pedido de localização normalmente agendadas, pode forçar o pedido, reiniciando o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.

Os clientes tiverem as novas informações de localização do serviço de Proxy de nuvem, experimente a verificar o estado de clientes que já não se encontram na rede privada interna, mas tiver acesso à Internet. Também poderá monitorizar o tráfego de serviço de Proxy de nuvem acedendo a **administração > Serviços em nuvem > serviço de nuvem do Proxy**, selecionando o serviço no painel de lista e visualizar as informações de tráfego no painel de detalhes.   

## <a name="manage_o365"></a>Gerir o agente de cliente do Office 365 no Configuration Manager  

Iniciar 1606 de pré-visualização técnica, pode utilizar uma definição, em vez de política de grupo de agente do cliente do Configuration Manager para permitir que os clientes do Office 365 receber atualizações do Configuration Manager. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente de cliente do Office 365 para transferir atualizações do Office 365 a partir de um ponto de distribuição e instalá-los. O Configuration Manager também aceita inventário da definição do agente de cliente.

Para obter mais informações, consulte o artigo [atualizações gerir Office 365 ProPlus](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Configurar a definição para gerir o agente de cliente do Office 365 do cliente do Configuration Manager
1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **definições de cliente**.
2. Abra as definições de dispositivo adequados para ativar o agente de cliente. Para mais informações sobre predefinida e definições personalizadas de cliente, consulte o artigo [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  


## <a name="osdpreservedriveletter"></a>A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável de sequência de tarefas OSDPreserveDriveLetter determina se utiliza ou não a sequência de tarefas a letra de unidade capturada no ficheiro WIM da imagem do sistema operativo ao aplicar essa imagem a um computador de destino.
- Esta variável de sequência de tarefas foi preterido no 1606 de pré-visualização técnica.

Durante uma implementação do sistema operativo por predefinição, a configuração do Windows agora determina a letra de unidade melhor utilizar (normalmente c:). Se pretender especificar uma unidade diferente para utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Aceda ao **selecionar a localização onde pretende aplicar este sistema operativo** definição, selecione **letra de unidade lógica específica**e selecione a unidade que pretende utilizar. Tem de existir uma unidade de atribuídos com a letra que escolher no computador de destino. 

## <a name="updatesandservicing"></a>Alterações para as atualizações e manutenção nó
Com 1606 de pré-visualização técnica várias alterações foram introduzidas que se aplicam a atualizações e a manutenção na consola do Configuration Manager:
- **Alteração do nome de nó:**

    No **monitorização** área de trabalho, o **estado de manutenção do Site** nó foi mudado para **atualizações e o estado de manutenção**.
- **Estado de instalação de mais:**

    Quando visualiza o estado de instalação de atualização de um site, a consola apresenta agora detalhes separados para as seguintes ações:
    - **Transferir** (aplica-se apenas para o site de nível superior onde está instalada a função de sistema de sites de ponto de ligação de serviço)
    - **Replicação**
    - **Verificação de Pré-requisitos**
    - **Instalação**

  Além disso, é agora informações mais detalhadas sobre cada passo, incluindo o ficheiro de registo pode ver para obter mais informações.  
-   **Nova opção para repetir a falhas de pré-requisitos:**

    Em ambos os **administração** e **monitorização** áreas de trabalho, o **atualizações e a manutenção** nó inclui um novo botão no friso com o nome **ignorar os avisos de pré-requisitos**.

    Quando instalar atualizações sem utilizar a opção para ignorar os avisos de pré-requisitos (a partir no Assistente para atualizações), e que a instalação da atualização halts com um Estado de **pré-requisitos aviso**, em seguida, pode selecionar **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática dessa instalação de atualização que ignora os avisos de pré-requisitos.  



- **Vista de limpeza de atualizações:**

    Quando visualiza o **atualizações e a manutenção** nó, agora verá apenas a atualização instalada mais recentemente e quaisquer novas atualizações que estão disponíveis para instalação. Para ver atualizações instaladas anteriormente, clique em novo **histórico** botão que aparece no Friso.  

-   **Opção cujo nome foi mudada de pré-produção:**

    As atualizações e manutenção nó, o botão que era designado **opções de cliente** sido agora alterado para **promover cliente de pré-produção**.

