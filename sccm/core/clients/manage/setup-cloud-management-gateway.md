---
title: "Configurar o Gateway de gestão de nuvem"
titleSuffix: Configuration Manager
description: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.date: 09/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 7463cd7199098b21843fd5b99ed284a12ff91e00
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gestão de nuvem para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)* o processo de configuração do gateway de gestão de nuvem no Configuration Manager inclui os seguintes passos:

## <a name="step-1-configure-required-certificates"></a>Passo 1: Configurar os certificados necessários

> [!TIP]  
> Antes de pedir um certificado, confirme que o nome de domínio do Azure pretendida (por exemplo, GraniteFalls.CloudApp.Net) é exclusivo. Para tal, inicie sessão no [portal do Microsoft Azure](https://manage.windowsazure.com), clique em **novo**, selecione **serviço em nuvem**e, em seguida, **criação personalizada**. No **URL** campo escreva o nome de domínio pretendida (não clique na marca de verificação para criar o serviço). O portal irá refletir se o nome de domínio está disponível ou já se encontra em utilização por outro serviço.

### <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Opção 1 (preferencial) - utilizar o certificado de autenticação de servidor de um fornecedor de certificado pública e globalmente fidedignas (por exemplo, VeriSign)

Quando utiliza este método, os clientes automaticamente confiam no certificado e não terá de criar um certificado SSL personalizado por si.

1. Crie um registo de nome canónico (CNAME) no serviço de nome de domínio público da sua organização (DNS) para criar um alias para o serviço de gateway de gestão de nuvem para um nome amigável que será utilizado o certificado público.
Por exemplo, Contoso nomes os serviço de gateway de gestão de nuvem **GraniteFalls**, que no Azure será **GraniteFalls.CloudApp.Net**. O administrador DNS público contoso.com espaço de nomes DNS da Contoso, cria um novo registo CNAME para **GraniteFalls.Contoso.com** para o nome de anfitrião real, **GraniteFalls.CloudApp.net**.
2. Em seguida o pedido de um fornecedor público com o nome comum (CN) do CNAME alias de um certificado de autenticação de servidor.
Por exemplo, a Contoso utiliza **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie o serviço de gateway de gestão de nuvem na consola do Configuration Manager utilizando este certificado.
    - No **definições** página do assistente criar uma nuvem gestão Gateway: Ao adicionar o certificado de servidor para este serviço em nuvem (de **ficheiro de certificado**), o assistente extrair o nome de anfitrião do certificado CN como o nome do serviço e, em seguida, anexe que para **cloudapp.net**(ou **usgovcloudapp.net** para a nuvem do Azure US Government) como o FQDN de serviço para criar o serviço no Azure.
Por exemplo, quando criar o gateway de gestão de nuvem contoso, o nome de anfitrião **GraniteFalls** é extraído do certificado CN, para que o serviço real do Azure é criado como **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Opção 2 - criar um certificado SSL personalizado para o gateway de gestão de nuvem da mesma forma para um ponto de distribuição baseado na nuvem

Pode criar um certificado SSL personalizado para o gateway de gestão de nuvem da mesma forma que faria fazê-lo para um ponto de distribuição baseado na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) mas efetue os seguintes procedimentos de forma diferente:

- Quando pedir o certificado de servidor web personalizado, fornecer um FQDN para o nome comum do certificado que termine em **cloudapp.net** para utilizar o gateway de gestão de nuvem na nuvem pública do Azure ou **usgovcloudapp.net** para a nuvem do Azure government.


## <a name="step-2-export-the-client-certificates-root"></a>Passo 2: Exportar a raiz do certificado de cliente

É a forma mais fácil para exportar a raiz dos certificados de cliente utilizado na rede, para abrir um certificado de cliente numa das máquinas associados a um domínio que tenha um e copiá-lo.

> [!NOTE]
>
> São necessários certificados de cliente em qualquer computador que pretende gerir com o gateway de gestão de nuvem e no servidor do sistema de sites que aloja o conector de gateway de gestão de nuvem do ponto. Se precisar de adicionar um certificado de cliente a qualquer uma destas máquinas, consulte [implementar o cliente certificados para computadores com o Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Na janela executar, escreva **mmc** e prima regressar.

2.  No menu ficheiro, escolha **Adicionar/Remover Snap-in...** .

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, escolha **certificados** > **adicionar &gt;**   >  **conta de computador** > **seguinte** > **computador Local** > **concluir**.

4.  Aceda a **certificados** &gt; **pessoais** &gt; **certificados**.

5.  Faça duplo clique o certificado para autenticação de cliente no computador, escolha o separador de caminho de certificação e faça duplo clique a autoridade de raiz (na parte superior do caminho).

6.  No separador de detalhes, selecione **copiar para ficheiro...** .

7.  Conclua o Assistente para exportar certificados utilizando o formato de certificado predefinido. Tome nota do nome do e localização do certificado de raiz que cria. Terá de configurar o gateway de gestão em nuvem um [passo posterior](#step-4-set-up-cloud-management-gateway).

>[!NOTE]
>Se o certificado de cliente foi emitido por uma autoridade de certificação subordinada terá de repetir este passo para cada certificado na cadeia.

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Passo 3: Carregar o certificado de gestão para o Azure

Um certificado de gestão do Azure é necessário para o Configuration Manager para aceder à API do Azure e configurar o gateway de gestão de nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gestão, consulte os artigos seguintes na documentação do Azure:

- [Descrição geral de certificados para serviços de nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Carregar um certificado de gestão de API de gestão do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Certifique-se ao copiar o ID de subscrição associado o certificado de gestão. Terá de configurar o gateway de gestão de nuvem na consola do Configuration Manager no [passo seguinte](#step-4-set-up-cloud-management-gateway).



## <a name="step-4-set-up-cloud-management-gateway"></a>Passo 4: Configurar o gateway de gestão de nuvem

>[!NOTE]
>Na versão 1610, o gateway de gestão de nuvem é uma funcionalidade de pré-lançamento. Para ativá-la, consulte o artigo [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

1. Na consola do Configuration Manager, vá para **administração** > **serviços em nuvem** > **Gateway de gestão de nuvem**.
2. Escolha **criar Gateway de gestão de nuvem**.

3. No assistente criar nuvem gestão de Gateway, introduza o seu ID de subscrição do Azure (copiada a partir do portal de gestão do Azure) e procure o ficheiro de certificado é utilizado para carregar um certificado de gestão do Azure. Escolha **seguinte** e, em seguida, aguarde alguns momentos para a consola para ligar ao Azure.

4. Preencha os detalhes adicionais no assistente:

    - Especifique o nome para o serviço que serão executadas no Azure. Nome do serviço tem de ser apenas carateres alfanuméricos e 3 a 24 carateres de comprimento.

    - Escolha a região do Azure que pretende que o serviço para executar.

    - Especifique o número de máquinas virtuais que pretende utilizar para o serviço. A predefinição é 1, mas pode executar até 16 máquinas virtuais para o serviço.

    >[!NOTE]
    >Se utilizar um proxy de internet para o ponto de ligação de gateway de gestão de nuvem, terá de aumentar o número de portas no proxy de pelo número de máquinas virtuais que utiliza, começando porta 10124.

    - Especifique a chave privada (ficheiro. pfx) que exportou do certificado SSL personalizado.

    - Especifique o certificado de raiz (e quaisquer certificados subordinados) exportado do certificado de cliente. O assistente aceita até dois certificados de raiz e certificados de subordinados quatro.

    -   Especifique o mesmo nome de serviço FQDN que utilizou quando criou o novo modelo de certificado. Tem de especificar um dos seguintes sufixos para o nome do serviço FQDN com base na nuvem do Azure que está a utilizar:

    Nuvem do Azure | Prefixo FQDN
    --------------|-------------
    Nuvem pública de (comercial) | . cloudapp.net    
    Nuvem do Governo dos EUA | . usgovcloudapp.net

  - Desmarque a caixa junto a **verificar a revogação de certificados de cliente** (exceto se estiver a publicamente publicar as suas informações de CRL).

  - Escolha **seguinte** quando tiver terminado.

5. Se pretender monitorizar o tráfego de gateway de gestão de nuvem com um limiar de 14 dias, selecione a caixa de verificação para ativar o alerta do limiar. Em seguida, especifique o limiar e a percentagem no qual pretende elevar os níveis de alerta diferentes. Escolha **seguinte** quando tiver terminado.

6. Reveja as definições e escolha **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Depois de fechar o assistente, irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique o **estado** coluna para o novo gateway de gestão de nuvem determinar quando o serviço está pronto.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Passo 5: Configurar o site primário certificação para autenticação de cliente

1. Na consola do Configuration Manager, vá para **administração** > **configuração do Site** > **Sites**.

2. Selecione o site primário para os clientes que pretende gerir através do gateway de gestão de nuvem e escolha **propriedades**.

3. No separador de comunicações de computadores cliente da folha de propriedades de site primário, verifique **certificado de cliente PKI de utilização (autenticação de cliente) se estiver disponível**.

4. Certifique-se limpar **clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**. Esta opção apenas seriam necessária se publicamente foram publicar o CRL.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Passo 6: Adicionar o ponto de conector de gateway de gestão de nuvem

O ponto de conector de gateway de gestão de nuvem é uma nova função de sistema de sites para comunicação com o gateway de gestão de nuvem. Para adicionar o ponto de conector de gateway de gestão de nuvem, siga as instruções em [adicionar funções do sistema de site para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Passo 7: Configurar funções para o tráfego de gateway de gestão de nuvem

O passo final na configuração do gateway de gestão de nuvem é configurar as funções de sistema de sites para aceitar o tráfego de gateway de gestão de nuvem. Apenas as software e de ponto de atualização ponto funções de gestão são suportadas para o gateway de gestão de nuvem. Configure cada função em separado.

1. Na consola do Configuration Manager, vá para **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.

2. Escolha o servidor de sistema de sites para a função que pretende configurar para o tráfego de gateway de gestão de nuvem.

3. Escolha a função e, em seguida, escolha **propriedades**.

4. Na folha de propriedades da função, em ligações de cliente, selecione a caixa junto **tráfego de gateway de gestão de nuvem de permitir que o Configuration Manager**e, em seguida, escolha **OK**. Repita estes passos para as restantes funções. Ativar o **HTTPS** opção também é recomendável como melhor prática de segurança, mas não é necessária.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Passo 8: Configurar clientes para o gateway de gestão de nuvem

Após a gestão de nuvem se encontram completamente configuradas funções do sistema de gateway e o site e em execução, os clientes obtêm a localização do serviço de gateway de gestão de nuvem automaticamente no próximo pedido de localização. Os clientes tem de estar na rede empresarial para receber a localização do serviço de gateway de gestão de nuvem. O ciclo de consulta de pedidos de localização é a cada 24 horas. Se não pretender aguardar que o pedido de localização normalmente agendada, pode forçar o pedido reiniciando o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.

Com a localização do serviço de gateway de gestão de nuvem configurado no cliente, pode automaticamente determinar se se encontra numa intranet ou à Internet. Se o cliente pode contactar o controlador de domínio ou no local ponto de gestão, irá utilizá-lo para comunicar com o Configuration Manager. Caso contrário, iremos considerar está na Internet e utilizar a localização do serviço de gateway de gestão de nuvem para comunicar.

>[!NOTE]
> Pode forçar o cliente utiliza sempre o gateway de gestão de nuvem independentemente de ser na intranet ou à Internet. Para tal, defina a seguinte chave de registo no computador cliente: \
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Para verificar se os clientes podem contactar o Configuration Manager, pode executar o seguinte comando do PowerShell no computador cliente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Este comando apresenta os pontos de gestão, que o cliente pode contactar incluindo o serviço de gateway de gestão de nuvem.

## <a name="next-steps"></a>Passos seguintes

[Monitorizar clientes para gateway de gestão de nuvem](monitor-clients-cloud-management-gateway.md)
