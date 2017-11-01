---
title: "Certificados de implementação de PKI"
titleSuffix: Configuration Manager
description: Siga um exemplo passo a passo para saber como criar e implementar certificados PKI que utiliza o System Center Configuration Manager.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: "11"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 092e3e752a27ab652f2b38c0ba43e6e2e26c99c8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Exemplo passo a passo implementação dos certificados PKI para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta implementação de exemplo passo a passo, que utiliza uma autoridade de certificação (AC) do Windows Server 2008, tem de procedimentos que mostram como criar e implementar os certificados de infraestrutura de chaves públicas (PKI) que utiliza o System Center Configuration Manager. Estes procedimentos utilizam uma autoridade de certificação (AC) empresarial e modelos de certificado. Os passos são adequados apenas para uma rede de teste, como prova de conceito.  

 Porque não existe nenhum método de implementação único para os certificados necessários, consulte a documentação de implementação de PKI específica para os procedimentos necessários e as melhores práticas para implementar os certificados necessários para um ambiente de produção. Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Pode adaptar as instruções neste tópico para sistemas operativos que não estão documentados na secção de requisitos de rede de teste. No entanto, se estiver a executar a AC emissora no Windows Server 2012, não lhe será solicitada a indicação da versão do modelo de certificado. Em vez disso, especifique isto no **compatibilidade** separador de propriedades do modelo:  
>   
>  -   **Autoridade de certificação**: **Windows Server 2003**  
> -   **Destinatário do certificado**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Nesta secção  
 As secções seguintes incluem instruções passo a passo de exemplo para criar e implementar os seguintes certificados que podem ser utilizados com o System Center Configuration Manager:  

 [Requisitos de rede de teste](#BKMK_testnetworkenvironment)  

 [Descrição geral dos certificados](#BKMK_overview2008)  

 [Implementar o certificado de servidor web para sistemas de sites que executam o IIS](#BKMK_webserver2008_cm2012)  

 [Implementar o certificado de serviço para pontos de distribuição baseado na nuvem](#BKMK_clouddp2008_cm2012)  

 [Implementar o certificado de cliente para computadores Windows](#BKMK_client2008_cm2012)  

 [Implementar o certificado de cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012)  

 [Implementar o certificado de inscrição para dispositivos móveis](#BKMK_mobiledevices2008_cm2012)  

 [Implementar os certificados para AMT](#BKMK_AMT2008_cm2012)  

 [Implementar o certificado de cliente para computadores Mac](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a>Requisitos de rede de teste  
 As instruções passo a passo têm os seguintes requisitos:  

-   A rede de teste está a executar os Serviços de Domínio do Active Directory com o Windows Server 2008 e está instalada como único domínio e única floresta.  

-   Tem um servidor membro com o Windows Server 2008 Enterprise Edition, que tem a função de serviços de certificados do Active Directory instalada no mesmo e está configurado como uma autoridade de certificação de raiz empresarial (AC).  

-   Tem um computador que tenha o Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou posterior) instalado no mesmo, que o computador está designado como servidor membro e serviços de informação Internet (IIS) está instalado no mesmo. Este computador será o servidor de sistema de sites do System Center Configuration Manager irá ser configurado com um nome de domínio completamente qualificado (FQDN) para suportar ligações de cliente na intranet e um FQDN de Internet caso seja necessário suportar dispositivos móveis que são inscritos pelo System Center Configuration Manager e os clientes de intranet na Internet.  

-   Ter um cliente do Windows Vista com service pack mais recente instalado e este computador está configurado com um nome de computador que abrange carateres ASCII e está associado ao domínio. Este computador será um computador de cliente do System Center Configuration Manager.  

-   Pode iniciar sessão com uma conta de administrador de domínio de raiz ou uma conta de administrador de domínio da empresa e utilizar esta conta para todos os procedimentos nesta implementação de exemplo.  

##  <a name="BKMK_overview2008"></a>Descrição geral dos certificados  
 A tabela seguinte lista os tipos de certificados PKI que poderão ser necessárias para o System Center Configuration Manager e descreve a forma como são utilizados.  

|Requisito de Certificado|Descrição do Certificado|  
|-----------------------------|-----------------------------|  
|Certificado de servidor Web para os sistemas de sites que executam o IIS|Este certificado é utilizado para encriptar dados e autenticar o servidor para clientes. Tem de ser instalado externamente do System Center Configuration Manager em servidores de sistemas de sites que executam os serviços de informação Internet (IIS) e que estão configurados no System Center Configuration Manager para utilizar HTTPS.<br /><br /> Para obter os passos configurar e instalação deste certificado, consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](#BKMK_webserver2008_cm2012) neste tópico.|  
|Certificado de serviço para clientes que ligam a pontos de distribuição baseados na nuvem|Para obter os passos de configuração e instalação deste certificado, consulte [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](#BKMK_clouddp2008_cm2012) neste tópico.<br /><br /> **Importante:** Este certificado é utilizado em conjunto com o certificado de gestão do Windows Azure. Para mais informações sobre o certificado de gestão, consulte [como criar um certificado de gestão](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [como adicionar um certificado de gestão a uma subscrição do Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) na secção plataforma Windows Azure da biblioteca MSDN.|  
|Certificado de cliente para computadores com o Windows|Este certificado é utilizado para autenticar computadores de cliente do System Center Configuration Manager para sistemas de sites que estão configurados para utilizar HTTPS. Também pode ser utilizado para pontos de gestão e pontos de migração de estado para monitorizar o respetivo estado operacional quando estão configurados para utilizar HTTPS. Tem de ser instalado externamente do System Center Configuration Manager em computadores.<br /><br /> Para obter os passos configurar e instalação deste certificado, consulte [implementar o certificado de cliente para computadores Windows](#BKMK_client2008_cm2012) neste tópico.|  
|Certificado de cliente para pontos de distribuição|Este certificado tem duas finalidades:<br /><br /> O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão ativado para HTTPS antes de o ponto de distribuição enviar mensagens de estado.<br /><br /> Quando a opção do ponto de distribuição **Ativar suporte PXE para clientes** está selecionada, o certificado é enviado para computadores com arranque PXE para que liguem a um ponto de gestão ativado para HTTPS durante a implementação do sistema operativo.<br /><br /> Para obter os passos configurar e instalação deste certificado, consulte [implementar o certificado de cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012) neste tópico.|  
|Certificado de inscrição para dispositivos móveis|Este certificado é utilizado para autenticar clientes de dispositivo móvel do System Center Configuration Manager para sistemas de sites que estão configurados para utilizar HTTPS. Tem de ser instalado como parte da inscrição de dispositivos móveis no System Center Configuration Manager e escolha o modelo de certificado configurado como uma definição de cliente de dispositivo móvel.<br /><br /> Para obter os passos configurar este certificado, consulte [implementar o certificado de inscrição para dispositivos móveis](#BKMK_mobiledevices2008_cm2012) neste tópico.|  
|Certificados para o Intel AMT|Três certificados estão relacionadas com a gestão fora de banda para computadores baseados em Intel AMT:<ul><li>Um certificado de aprovisionamento Active Management Technology (AMT)</li><li>Um certificado de servidor de web AMT</li><li>Opcionalmente, um certificado de autenticação de cliente para redes com ou sem fios 802.1 X</li></ul>O certificado de aprovisionamento de AMT deve ser instalado externamente do System Center Configuration Manager no computador do ponto de serviço fora de banda e, em seguida, escolha o certificado instalado nas propriedades do ponto de serviço fora de banda. O certificado de servidor de web AMT e o certificado de autenticação de cliente são instaladas durante o aprovisionamento de AMT e de gestão e escolha os modelos de certificado configurado nas propriedades do componente de gestão fora de banda.<br /><br /> Para obter os passos configurar estes certificados, consulte [implementar os certificados para AMT](#BKMK_AMT2008_cm2012) neste tópico.|  
|Certificado de cliente para computadores Mac|Pode pedir e instalar este certificado a partir de um computador Mac quando utiliza a inscrição do System Center Configuration Manager e escolha o modelo de certificado configurado como uma definição de cliente de dispositivo móvel.<br /><br /> Para obter os passos configurar este certificado, consulte [implementar o certificado de cliente para computadores Mac](#BKMK_MacClient_SP1) neste tópico.|  

##  <a name="BKMK_webserver2008_cm2012"></a>Implementar o certificado de servidor web para sistemas de sites que executam o IIS  
 Esta implementação de certificados possui os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado na autoridade de certificação de servidor web  

-   Pedir o certificado de servidor web  

-   Configurar o IIS para utilizar o certificado de servidor web  

###  <a name="BKMK_webserver22008"></a>Criar e emitir o modelo de certificado na autoridade de certificação de servidor web  
 Este procedimento cria um modelo de certificado para sistemas de sites do System Center Configuration Manager e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de servidor Web na autoridade de certificação  

1.  Crie um grupo de segurança denominado **servidores IIS do ConfigMgr** com os servidores membro para instalar sistemas de sites do System Center Configuration Manager que executam o IIS.  

2.  No servidor membro que tem os serviços de certificados instalados, a consola da autoridade de certificação, clique com botão direito **modelos de certificado** e, em seguida, escolha **gerir** ao carregar o **modelos de certificado** consola.  

3.  No painel de resultados, faça duplo clique na entrada que tem **servidor Web** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de servidor Web do ConfigMgr**para gerar os certificados web que serão utilizados nos sistemas de sites do Configuration Manager.  

6.  Escolha o **nome do requerente** separador e certifique-se de que **fornecer no pedido** está selecionada.  

7.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins do domínio** e **Admins de empresa** grupos de segurança.  

8.  Escolha **adicionar**, introduza **servidores IIS do ConfigMgr** no texto da caixa e, em seguida, escolha **OK**.  

9. Escolha o **inscrever** permissão para este grupo e não desmarque a **leitura** permissão.  

10. Escolha **OK**e, em seguida, feche o **consola de modelos de certificado**.  

11. Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

12. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de servidor Web do ConfigMgr**e, em seguida, escolha **OK**.  

13. Se não precisar de criar e emitir mais certificados, feche **autoridade de certificação**.  

###  <a name="BKMK_webserver32008"></a>Pedir o certificado de servidor web  
 Este procedimento permite-lhe especificar os valores de FQDN de Internet que irão configurar as propriedades de servidor do sistema de sites e da intranet e, em seguida, instala o certificado de servidor web no servidor membro que executa o IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para pedir o certificado de servidor Web  

1.  Reinicie o servidor membro que executa o IIS para se certificar de que o computador pode aceder o modelo de certificado que criou utilizando o **leitura** e **inscrever** permissões que configurou.  

2.  Escolha **iniciar**, escolha **executar**e, em seguida, escreva **mmc.exe.** Na consola vazia, escolha **ficheiro**e, em seguida, escolha **Adicionar/Remover Snap-in**.  

3.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **adicionar**.  

4.  No **snap-in de certificados** diálogo caixa, escolha **conta de computador**e, em seguida, escolha **seguinte**.  

5.  No **selecionar computador** diálogo caixa, certifique-se de que **computador Local: (o computador onde esta consola está em execução no)** está selecionada e, em seguida, escolha **concluir**.  

6.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **OK**.  

7.  Na consola, expanda **certificados (computador Local)**e, em seguida, escolha **pessoais**.  

8.  Clique com botão direito **certificados**, escolha **todas as tarefas**e, em seguida, escolha **requisitar um novo certificado**.  

9. No **antes de começar** página, escolha **seguinte**.  

10. Se vir o **selecionar política de inscrição de certificado** página, escolha **seguinte**.  

11. No **pedir certificados** página, identifique o **certificado de servidor Web do ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **são necessárias mais informações para fazer a inscrição deste certificado. Clique aqui para configurar as definições**.  

12. No **propriedades do certificado** caixa de diálogo a **requerente** separador, não faça quaisquer alterações aos **nome do requerente**. Isto significa que a caixa **Valor** para a secção **Nome do requerente** permanece em branco. Em vez disso, a partir de **nome alternativo** secção, escolha o **tipo** pendente lista e, em seguida, escolha **DNS**.  

13. No **valor** caixa, especifique os valores FQDN que irá especificar nas propriedades do sistema de site do System Center Configuration Manager e, em seguida, escolha **OK** para fechar o **propriedades do certificado** caixa de diálogo.  

     Exemplos:  

    -   Se o sistema de sites apenas aceitar ligações de cliente a partir da intranet e o FQDN da intranet do servidor do sistema de sites é **server1.internal.contoso.com**, introduza **server1.internal.contoso.com**e, em seguida, escolha **adicionar**.  

    -   Se o sistema de sites aceitar ligações de cliente a partir da intranet e da Internet e o FQDN de intranet do servidor do sistema de sites for **server1.internal.contoso.com** e o FQDN de Internet do servidor do sistema de sites for **server.contoso.com**:  

        1.  Introduza **server1.internal.contoso.com**e, em seguida, escolha **adicionar**.  

        2.  Introduza **server.contoso.com**e, em seguida, escolha **adicionar**.  

        > [!NOTE]  
        >  Pode especificar o FQDN para o System Center Configuration Manager por qualquer ordem. No entanto, verifique se todos os dispositivos que irão utilizar o certificado, tais como dispositivos móveis e servidores web proxy, podem utilizar um nome alternativo do requerente de certificado (SAN) e múltiplos valores no SAN. Se os dispositivos têm suporte limitado para valores de SAN nos certificados, terá de alterar a ordem dos FQDN ou utilizar em vez disso o valor Requerente.  

14. No **pedir certificados** página, escolha **certificado de servidor Web do ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **inscrever**.  

15. No **resultados da instalação de certificados** página, aguarde até que o certificado está instalado e, em seguida, escolha **concluir**.  

16. Feche **Certificados (Computador Local)**.  

###  <a name="BKMK_webserver42008"></a>Configurar o IIS para utilizar o certificado de servidor web  
 Este procedimento vincula o certificado instalado ao **Web Site Predefinido**do IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Para configurar o IIS para utilizar o certificado de servidor web  

1.  No servidor membro que tem o IIS instalado, escolha **iniciar**, escolha **programas**, escolha **ferramentas administrativas**e, em seguida, escolha **Gestor dos serviços de informação Internet (IIS)**.  

2.  Expanda **Sites**, faça duplo clique **Web Site predefinido**e, em seguida, escolha **editar enlaces**.  

3.  Escolha o **https** entrada e, em seguida, escolha **editar**.  

4.  No **Editar enlace de Site** caixa de diálogo, selecione o certificado que pediu, através do modelo de certificados de servidor Web do ConfigMgr e, em seguida, escolha **OK**.  

    > [!NOTE]  
    >  Se não tem a certeza de que é o certificado correto, escolha um e, em seguida, escolha **vista**. Isto permite-lhe comparar os detalhes do certificado selecionado para os certificados no snap-in certificados. Por exemplo, o snap-in de certificados mostra o modelo de certificado que foi utilizado para pedir o certificado. Poderá então comparar a thumbprint do certificado que foi pedido utilizando o modelo de certificados de servidor Web do ConfigMgr para o thumbprint do certificado atualmente selecionado no **Editar enlace de Site** caixa de diálogo.  

5.  Escolha **OK** no **Editar enlace de Site** diálogo caixa e, em seguida, escolha **fechar**.  

6.  Feche o **Gestor de Serviços de Informação Internet (IIS)**.  

 O servidor membro está agora definido com um certificado de servidor web do System Center Configuration Manager.  

> [!IMPORTANT]  
>  Quando instala o servidor de sistema de sites do System Center Configuration Manager neste computador, certifique-se de que especifica os mesmos FQDN nas propriedades do sistema de sites que especificou quando pediu o certificado.  

##  <a name="BKMK_clouddp2008_cm2012"></a>Implementar o certificado de serviço para pontos de distribuição baseado na nuvem  

Esta implementação de certificados possui os seguintes procedimentos:  

-   [Criar e emitir o modelo de certificado na autoridade de certificação de um servidor web personalizado](#BKMK_clouddpcreating2008)  

-   [Pedir o certificado de servidor web personalizado](#BKMK_clouddprequesting2008)  

-   [Exportar o certificado de servidor web personalizado para pontos de distribuição baseado na nuvem](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a>Criar e emitir o modelo de certificado na autoridade de certificação de um servidor web personalizado  
 Este procedimento cria um modelo de certificado personalizado baseado no modelo de certificado de servidor web. O certificado é para os pontos de distribuição baseados na nuvem do System Center Configuration Manager e a chave privada tem de ser exportável. Após a criação do modelo de certificado, este é adicionado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado de servidor web que criou para sistemas de sites que executam o IIS. Embora ambos os certificados necessitem de capacidade de autenticação de servidor, o certificado para pontos de distribuição baseados na nuvem requer que introduza um valor personalizado para o nome do requerente e a chave privada tem de ser exportada. Como melhor prática de segurança, efetue não configurar modelos de certificado para que a chave privada pode ser exportada, a menos que esta configuração é necessária. O ponto de distribuição baseado na nuvem necessita desta configuração porque é necessário importar o certificado como um ficheiro, vez escolhê-lo a partir do arquivo de certificados.  
>   
>  Quando cria um novo modelo de certificado para este certificado, pode restringir os computadores que podem solicitar um certificado cujo chave privada pode ser exportada. Numa rede de produção, também poderá considerar adicionar as seguintes alterações para este certificado:  
>   
>  -   Exigir a aprovação para instalar o certificado para segurança adicional.  
> -   Aumente o período de validade do certificado. Porque tem de exportar e importar o certificado de cada vez antes de expirar, um aumento do período de validade reduz a frequência tem de repetir este procedimento. No entanto, um aumento do período de validade também reduz a segurança do certificado porque fornece mais algum tempo para um atacante desencriptar a chave privada e roubar o certificado.  
> -   Utilize um valor personalizado no Nome Alternativo do Requerente (SAN) do certificado para ajudar a identificar este certificado entre certificados de servidor Web padrão que utiliza com o IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado na autoridade de certificação de servidor web personalizado  

1.  Crie um grupo de segurança denominado **servidores do Site ConfigMgr** com os servidores membro para instalar servidores de site primário do System Center Configuration Manager que irão gerir pontos de distribuição baseados na nuvem.  

2.  No servidor membro que está a executar a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** para carregar a consola de gestão de modelos de certificado.  

3.  No painel de resultados, faça duplo clique na entrada que tem **servidor Web** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de ponto de distribuição baseado na nuvem do ConfigMgr**para gerar o certificado de servidor web para pontos de distribuição baseado na nuvem.  

6.  Escolha o **processamento de pedidos** separador e, em seguida, escolha **permitir que a chave privada seja exportada**.  

7.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins de empresa** grupo de segurança.  

8.  Escolha **adicionar**, introduza **servidores do Site ConfigMgr** no texto da caixa e, em seguida, escolha **OK**.  

9. Selecione a permissão **Inscrever** para este grupo e não desmarque a permissão **Leitura** .  

10. Escolha **OK**e, em seguida, feche **consola de modelos de certificado**.  

11. Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

12. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de ponto de distribuição baseado na nuvem do ConfigMgr**e, em seguida, escolha **OK**.  

13. Se não necessitar de criar e emitir mais certificados, feche **autoridade de certificação**.  

###  <a name="BKMK_clouddprequesting2008"></a>Pedir o certificado de servidor web personalizado  
 Este procedimento pede e, em seguida, instala o certificado de servidor web personalizado no servidor membro que irá executar o servidor do site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para pedir o certificado de servidor Web personalizado  

1.  Reinicie o servidor membro depois de criar e configurar o **servidores do Site ConfigMgr** grupo de segurança para se certificar de que o computador pode aceder o modelo de certificado que criou utilizando o **leitura** e **inscrever** permissões que configurou.  

2.  Escolha **iniciar**, escolha **executar**e, em seguida, introduza **mmc.exe.** Na consola vazia, escolha **ficheiro**e, em seguida, escolha **Adicionar/Remover Snap-in**.  

3.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **adicionar**.  

4.  No **snap-in de certificados** diálogo caixa, escolha **conta de computador**e, em seguida, escolha **seguinte**.  

5.  No **selecionar computador** diálogo caixa, certifique-se de que **computador Local: (o computador onde esta consola está em execução no)** está selecionada e, em seguida, escolha **concluir**.  

6.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **OK**.  

7.  Na consola, expanda **certificados (computador Local)**e, em seguida, escolha **pessoais**.  

8.  Clique com botão direito **certificados**, escolha **todas as tarefas**e, em seguida, escolha **requisitar um novo certificado**.  

9. No **antes de começar** página, escolha **seguinte**.  

10. Se vir o **selecionar política de inscrição de certificado** página, escolha **seguinte**.  

11. No **pedir certificados** página, identifique o **certificado de ponto de distribuição baseado na nuvem do ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **mais informação é necessária a inscrição para este certificado. Escolha aqui configurar as definições**.  

12. No **propriedades do certificado** caixa de diálogo a **requerente** separador, para o **nome do requerente**, escolha **nome comum** como o **tipo**.  

13. Na caixa **Valor** , especifique a sua escolha de nome de serviço e o nome do domínio utilizando um formato FQDN. Por exemplo: **pdnuvem1.contoso.com**.  

    > [!NOTE]  
    >  Certifique-o nome do serviço exclusivo no seu espaço de nomes. Irá utilizar DNS para criar um alias (registo CNAME) para mapear este nome de serviço para um identificador (GUID) gerado automaticamente e um endereço IP do Windows Azure.  

14. Escolha **adicionar**e, em seguida, escolha **OK** para fechar o **propriedades do certificado** caixa de diálogo.  

15. No **pedir certificados** página, escolha **certificado de ponto de distribuição baseado na nuvem do ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **inscrever**.  

16. No **resultados da instalação de certificados** página, aguarde até que o certificado está instalado e, em seguida, escolha **concluir**.  

17. Feche **Certificados (Computador Local)**.  

###  <a name="BKMK_clouddpexporting2008"></a>Exportar o certificado de servidor web personalizado para pontos de distribuição baseado na nuvem  
 Este procedimento exporta o certificado de servidor Web personalizado para um ficheiro para que possa ser importado quando criar o ponto de distribuição baseado na nuvem.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar o certificado de servidor Web personalizado para pontos de distribuição baseados na nuvem  

1.  No **certificados (computador Local)** consola, faça duplo clique no certificado que acabou de instalar, escolha **todas as tarefas**e, em seguida, escolha **exportar**.  

2.  No Assistente para exportar certificados, escolha **seguinte**.  

3.  No **exportar chave privada** página, escolha **Sim, exportar a chave privada**e, em seguida, escolha **seguinte**.  

    > [!NOTE]  
    >  Se esta opção não estiver disponível, o certificado foi criado sem a opção para exportar a chave privada. Neste cenário, não é possível exportar o certificado no formato necessário. Tem de configurar o modelo de certificado para que a chave privada pode ser exportado e, em seguida, pedir o certificado novamente.  

4.  No **exportar formato de ficheiro** página, certifique-se de que o **Personal Information Exchange - PKCS #12 (. PFX)** opção está selecionada.  

5.  No **palavra-passe** página, especifique uma palavra-passe segura para proteger o certificado exportado com a respetiva chave privada e, em seguida, escolha **seguinte**.  

6.  No **ficheiro a exportar** página, especifique o nome do ficheiro que pretende exportar e, em seguida, escolha **seguinte**.  

7.  Para fechar o assistente, escolha **concluir** no **Assistente para exportar certificados** página e, em seguida, escolha **OK** na caixa de diálogo de confirmação.  

8.  Feche **Certificados (Computador Local)**.  

9. Guarde o ficheiro de forma segura e certifique-se de que consegue aceder-lhe a partir da consola do System Center Configuration Manager.  

 O certificado está agora pronto para ser importado quando criar um ponto de distribuição baseado na nuvem.  

##  <a name="BKMK_client2008_cm2012"></a>Implementar o certificado de cliente para computadores Windows  
 Esta implementação de certificados possui os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  

-   Configurar a inscrição automática do modelo de autenticação de estação de trabalho utilizando a política de grupo  

-   Inscrever o certificado de autenticação de estação de trabalho e certifique-se a instalação nos computadores automaticamente  

###  <a name="BKMK_client02008"></a>Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  
 Este procedimento cria um modelo de certificado para o cliente do System Center Configuration Manager, computadores e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de Autenticação de Estação de Trabalho na autoridade de certificação  

1.  No servidor membro que está a executar a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** para carregar a consola de gestão de modelos de certificado.  

2.  No painel de resultados, faça duplo clique na entrada que tem **autenticação de estação de trabalho** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

3.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de cliente do ConfigMgr**, para gerar os certificados de cliente que serão utilizados nos computadores de cliente do Configuration Manager.  

5.  Escolha o **segurança** separador, selecione o **computadores de domínio** grupo e, em seguida, selecione as permissões adicionais **leitura** e **inscrever automaticamente**. Não desmarque **Inscrever**.  

6.  Escolha **OK**e, em seguida, feche **consola de modelos de certificado**.  

7.  Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

8.  No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de cliente do ConfigMgr**e, em seguida, escolha **OK**.  

9. Se não precisar de criar e emitir mais certificados, feche **autoridade de certificação**.  

###  <a name="BKMK_client12008"></a>Configurar a inscrição automática do modelo de autenticação de estação de trabalho utilizando a política de grupo  
 Este procedimento configura a política de grupo para inscrever automaticamente o certificado de cliente em computadores.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar a inscrição automática do modelo de autenticação de estação de trabalho utilizando a política de grupo  

1.  No controlador de domínio, escolha **iniciar**, escolha **ferramentas administrativas**e, em seguida, escolha **gestão de políticas de grupo**.  

2.  Aceda ao seu domínio, clique com botão direito do domínio e, em seguida, escolha **criar um GPO neste domínio e ligá-lo aqui**.  

    > [!NOTE]  
    >  Este passo utiliza a melhor prática de criar uma nova Política de Grupo para definições personalizadas, em vez de editar a Política de Domínios Predefinida que é instalada com os Serviços de Domínio do Active Directory. Ao atribuir esta política de grupo ao nível do domínio, irá aplicá-la a todos os computadores no domínio. Num ambiente de produção, pode restringir a inscrição automática, de modo a que inscreva apenas computadores selecionados. Pode atribuir a política de grupo ao nível de uma unidade organizacional ou pode filtrar o política de grupo com um grupo de segurança do domínio para que aplica-se apenas aos computadores no grupo. Se restringir a inscrição automática, não se esqueça de incluir o servidor que está configurado como ponto de gestão.  

3.  No **novo GPO** caixa de diálogo, introduza um nome, como **certificados de inscrição automática**, para a nova política de grupo e, em seguida, escolha **OK**.  

4.  No painel de resultados, no **objetos de política de grupo ligados** separador, clique com o botão direito a nova política de grupo e, em seguida, escolha **editar**.  

5.  No **Editor de gestão de políticas de grupo**, expanda **políticas** em **configuração do computador**e, em seguida, aceda a **definições do Windows** / **definições de segurança** / **políticas de chaves públicas**.  

6.  Clique com o botão direito do tipo de objeto com o nome **cliente de serviços de certificados - inscrição automática**e, em seguida, escolha **propriedades**.  

7.  Do **modelo de configuração** pendente lista, escolha **ativado**, escolha **renovar certificados expirados, atualizar certificados pendentes, remover certificados revogados**, escolha **atualizar certificados que utilizam modelos de certificado**e, em seguida, escolha **OK**.  

8.  Feche a **Gestão de Políticas de Grupo**.  

###  <a name="BKMK_client22008"></a>Inscrever o certificado de autenticação de estação de trabalho e certifique-se a instalação nos computadores automaticamente  
 Este procedimento instala o certificado de cliente nos computadores e verifica a instalação.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para inscrever o certificado de autenticação de estação de trabalho e verificar a instalação no computador cliente automaticamente  

1.  Reinicie o computador de estação de trabalho e aguarde alguns minutos antes de iniciar sessão.  

    > [!NOTE]  
    >  Reiniciar um computador é o método mais fiável de garantir o sucesso da inscrição automática de certificados.  

2.  Inicie sessão com uma conta que tenha privilégios administrativos.  

3.  Na caixa de pesquisa, introduza **mmc.exe.**e, em seguida, prima **Enter**.  

4.  Na consola de gestão vazia, escolha **ficheiro**e, em seguida, escolha **Adicionar/Remover Snap-in**.  

5.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **adicionar**.  

6.  No **snap-in de certificados** diálogo caixa, escolha **conta de computador**e, em seguida, escolha **seguinte**.  

7.  No **selecionar computador** diálogo caixa, certifique-se de que **computador Local: (o computador onde esta consola está em execução no)** está selecionada e, em seguida, escolha **concluir**.  

8.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **OK**.  

9. Na consola, expanda **certificados (computador Local)**, expanda **pessoais**e, em seguida, escolha **certificados**.  

10. No painel de resultados, confirme que tem um certificado **autenticação de cliente** no **objetivo pretendido** coluna e que **certificado de cliente do ConfigMgr** está a ser o **modelo de certificado** coluna.  

11. Feche **Certificados (Computador Local)**.  

12. Repita os passos 1 a 11 para o servidor de membro verificar se o servidor que irá ser configurado como ponto de gestão também tem um certificado de cliente.  

 O computador está agora definido com um certificado de cliente do System Center Configuration Manager.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a>Implementar o certificado de cliente para pontos de distribuição  

> [!NOTE]  
>  Este certificado também pode ser utilizado para imagens de suportes de dados que não utilizem o arranque PXE, uma vez que os requisitos de certificados são os mesmos.  

 Esta implementação de certificados possui os seguintes procedimentos:  

-   Criar e emitir um modelo de certificado de autenticação de estação de trabalho personalizado na autoridade de certificação  

-   Pedir o certificado de autenticação de estação de trabalho personalizado  

-   Exportar o certificado de cliente para pontos de distribuição  

###  <a name="BKMK_clientdistributionpoint02008"></a>Criar e emitir um modelo de certificado de autenticação de estação de trabalho personalizado na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para pontos de distribuição do System Center Configuration Manager para que a chave privada pode ser exportada e adiciona o modelo de certificado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado que criou para computadores cliente. Embora ambos os certificados necessitem de capacidade de autenticação de cliente, o certificado para pontos de distribuição requer que a chave privada é exportada. Como melhor prática de segurança, efetue não configurar modelos de certificado para a chave privada pode ser exportada, a menos que esta configuração é necessária. O ponto de distribuição necessita desta configuração porque é necessário importar o certificado como um ficheiro vez escolhê-lo a partir do arquivo de certificados.  
>   
>  Quando cria um novo modelo de certificado para este certificado, pode restringir os computadores que podem solicitar um certificado cujo chave privada pode ser exportada. No nosso exemplo de implementação, este será o grupo de segurança que criou anteriormente para servidores de sistema de sites do System Center Configuration Manager que executam o IIS. Numa rede de produção que distribua as funções de sistema de sites do IIS, considere criar um novo grupo de segurança para os servidores que executam pontos de distribuição para poder restringir o certificado apenas a estes servidores do sistema de sites. Também poderá considerar adicionar as seguintes alterações a este certificado:  
>   
>  -   Exigir a aprovação para instalar o certificado para segurança adicional.  
> -   Aumente o período de validade do certificado. Porque tem de exportar e importar o certificado de cada vez antes de expirar, um aumento do período de validade reduz a frequência tem de repetir este procedimento. No entanto, um aumento do período de validade também reduz a segurança do certificado porque fornece mais algum tempo para um atacante desencriptar a chave privada e roubar o certificado.  
> -   Utilize um valor personalizado no campo Requerente ou Nome Alternativo do Requerente (SAN) do certificado para ajudar a identificar este certificado entre os certificados de cliente padrão. Isto pode ser particularmente útil se pretender utilizar o mesmo certificado para vários pontos de distribuição.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de Autenticação de Estação de Trabalho personalizado na autoridade de certificação  

1.  No servidor membro que está a executar a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** para carregar a consola de gestão de modelos de certificado.  

2.  No painel de resultados, faça duplo clique na entrada que tem **autenticação de estação de trabalho** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

3.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de ponto de distribuição de cliente do ConfigMgr**para gerar o certificado de autenticação de cliente para pontos de distribuição.  

5.  Escolha o **processamento de pedidos** separador e, em seguida, escolha **permitir que a chave privada seja exportada**.  

6.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins de empresa** grupo de segurança.  

7.  Escolha **adicionar**, introduza **servidores IIS do ConfigMgr** no texto da caixa e, em seguida, escolha **OK**.  

8.  Selecione a permissão **Inscrever** para este grupo e não desmarque a permissão **Leitura** .  

9. Escolha **OK**e, em seguida, feche **consola de modelos de certificado**.  

10. Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

11. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de ponto de distribuição de cliente do ConfigMgr**e, em seguida, escolha **OK**.  

12. Se não necessitar de criar e emitir mais certificados, feche **autoridade de certificação**.  

###  <a name="BKMK_clientdistributionpoint12008"></a>Pedir o certificado de autenticação de estação de trabalho personalizado  
 Este procedimento pede e, em seguida, instala o certificado de cliente personalizadas no servidor membro que executa o IIS e que irá ser configurado como um ponto de distribuição.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para pedir o certificado de Autenticação de Estação de Trabalho personalizado  

1.  Escolha **iniciar**, escolha **executar**e, em seguida, introduza **mmc.exe.** Na consola vazia, escolha **ficheiro**e, em seguida, escolha **Adicionar/Remover Snap-in**.  

2.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **adicionar**.  

3.  No **snap-in de certificados** diálogo caixa, escolha **conta de computador**e, em seguida, escolha **seguinte**.  

4.  No **selecionar computador** diálogo caixa, certifique-se de que **computador Local: (o computador onde esta consola está em execução no)** está selecionada e, em seguida, escolha **concluir**.  

5.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **OK**.  

6.  Na consola, expanda **certificados (computador Local)**e, em seguida, escolha **pessoais**.  

7.  Clique com botão direito **certificados**, escolha **todas as tarefas**e, em seguida, escolha **requisitar um novo certificado**.  

8.  No **antes de começar** página, escolha **seguinte**.  

9. Se vir o **selecionar política de inscrição de certificado** página, escolha **seguinte**.  

10. No **pedir certificados** página, escolha **certificado de ponto de distribuição de cliente do ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **inscrever**.  

11. No **resultados da instalação de certificados** página, aguarde até que o certificado está instalado e, em seguida, escolha **concluir**.  

12. No painel de resultados, confirme que tem um certificado **autenticação de cliente** no **objetivo pretendido** e que a coluna **certificado de ponto de distribuição de cliente do ConfigMgr** está a ser o **modelo de certificado** coluna.  

13. Não feche **Certificados (Computador Local)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a>Exportar o certificado de cliente para pontos de distribuição  
 Este procedimento exporta o certificado de autenticação de estação de trabalho personalizado para um ficheiro para que possa ser importado nas propriedades do ponto de distribuição.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar o certificado de cliente para pontos de distribuição  

1.  No **certificados (computador Local)** consola, faça duplo clique no certificado que acabou de instalar, escolha **todas as tarefas**e, em seguida, escolha **exportar**.  

2.  No Assistente para exportar certificados, escolha **seguinte**.  

3.  No **exportar chave privada** página, escolha **Sim, exportar a chave privada**e, em seguida, escolha **seguinte**.  

    > [!NOTE]  
    >  Se esta opção não estiver disponível, o certificado foi criado sem a opção para exportar a chave privada. Neste cenário, não é possível exportar o certificado no formato necessário. Tem de configurar o modelo de certificado para que a chave privada pode ser exportado e, em seguida, pedir o certificado novamente.  

4.  No **exportar formato de ficheiro** página, certifique-se de que o **Personal Information Exchange - PKCS #12 (. PFX)** opção está selecionada.  

5.  No **palavra-passe** página, especifique uma palavra-passe segura para proteger o certificado exportado com a respetiva chave privada e, em seguida, escolha **seguinte**.  

6.  No **ficheiro a exportar** página, especifique o nome do ficheiro que pretende exportar e, em seguida, escolha **seguinte**.  

7.  Para fechar o assistente, escolha **concluir** no **Assistente para exportar certificados** página e escolha **OK** na caixa de diálogo de confirmação.  

8.  Feche **Certificados (Computador Local)**.  

9. Guarde o ficheiro de forma segura e certifique-se de que consegue aceder-lhe a partir da consola do System Center Configuration Manager.  

 O certificado está agora pronto para ser importado quando configurar o ponto de distribuição.  

> [!TIP]  
>  Pode utilizar o mesmo ficheiro de certificado quando configurar imagens de suportes de dados para uma implementação de sistema operativo que não utilize arranque PXE e a sequência de tarefas para instalar a imagem tem de contactar um ponto de gestão requer ligações de cliente HTTPS.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a>Implementar o certificado de inscrição para dispositivos móveis  
 Esta implementação de certificado tem um procedimento único para criar e emitir o modelo de certificado de inscrição na autoridade de certificação.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Criar e emitir o modelo de certificado de inscrição na autoridade de certificação  
 Este procedimento cria um modelo de certificado de inscrição para dispositivos móveis do System Center Configuration Manager e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de inscrição na autoridade de certificação  

1.  Crie um grupo de segurança que tenha os utilizadores que irão inscrever dispositivos móveis no System Center Configuration Manager.  

2.  No servidor membro que tem os serviços de certificados instalados, a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** para carregar a consola de gestão de modelos de certificado.  

3.  No painel de resultados, faça duplo clique na entrada que tem **sessão autenticada** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de inscrição de dispositivos do ConfigMgr móvel**para gerar os certificados de inscrição para os dispositivos móveis para serem geridos pelo System Center Configuration Manager.  

6.  Escolha o **nome do requerente** separador, certifique-se de que **incorporar a partir destas informações do Active Directory** está selecionado, selecione **nome comum** para o **formato de nome do requerente:**e, em seguida, desmarque **nome principal de utilizador (UPN)** de **incluir estas informações no nome do requerente alternativo**.  

7.  Escolha o **segurança** separador, escolha o grupo de segurança que tenha os utilizadores que tenham dispositivos móveis para inscrever e, em seguida, escolha a permissão adicional de **inscrever**. Não desmarque **Leitura**.  

8.  Escolha **OK**e, em seguida, feche **consola de modelos de certificado**.  

9. Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

10. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de inscrição de dispositivos do ConfigMgr móvel**e, em seguida, escolha **OK**.  

11. Se não for necessário criar e emitir mais certificados, feche a consola de autoridade de certificação.  

 O modelo de certificado de inscrição de dispositivos móveis está agora pronto para ser selecionado quando configurar um perfil de inscrição de dispositivos móveis nas definições do cliente.  

##  <a name="BKMK_AMT2008_cm2012"></a>Implementar os certificados para AMT  
 Esta implementação de certificados possui os seguintes procedimentos:  

-   Criar, emitir e instalar o certificado de aprovisionamento de AMT  

-   Criar e emitir o certificado de servidor web para computadores baseados em AMT  

-   Criar e emitir certificados de autenticação 802.1 X AMT em computadores de cliente  

###  <a name="BKMK_AMTprovisioning2008"></a>Criar, emitir e instalar o certificado de aprovisionamento de AMT  
 Crie o certificado de aprovisionamento com a AC interna quando os computadores baseados em AMT estão configurados com o thumbprint do certificado da sua AC de raiz interna. Quando não for este o caso e tem de utilizar uma autoridade de certificação externa, utilize as instruções da empresa que emitiu o certificado de aprovisionamento de AMT, que geralmente envolverá pedir o certificado de web site público da empresa. Também poderá encontrar instruções detalhadas para sua escolhida AC externa no [Intel vPro Expert Center: Capacidade de gestão web site do Microsoft vPro](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  As ACs externas poderão não suportar o identificador do objeto de aprovisionamento de AMT da Intel. Quando for este o caso, forneça o **Intel (r) Client Setup Certificate** atributo UO.  

 Quando solicitar um certificado de uma AC externa de aprovisionamento de AMT, instale o certificado no arquivo de certificados pessoais do computador no servidor membro que irá alojar o ponto de serviço fora de banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Para pedir e emitir o certificado de aprovisionamento de AMT  

1.  Crie um grupo de segurança que tenha as contas de computador dos servidores do sistema de sites que executarão o ponto de serviço fora de banda.  

2.  No servidor membro que tem os serviços de certificados instalados, a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** ao carregar o **modelos de certificado** consola.  

3.  No painel de resultados, faça duplo clique na entrada que tem **servidor Web** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **aprovisionamento de AMT do ConfigMgr**, para o modelo de certificado de aprovisionamento de AMT.  

6.  Escolha o **nome do requerente** separador, escolha **incorporar a partir destas informações do Active Directory**e, em seguida, escolha **nome comum**.  

7.  Escolha o **extensões** separador, certifique-se de que **políticas de aplicações** está selecionada e, em seguida, escolha **editar**.  

8.  No **Editar extensão de políticas de aplicação** diálogo caixa, escolha **adicionar**.  

9. No **Adicionar política de aplicação** diálogo caixa, escolha **novo**.  

10. No **nova política de aplicação** caixa de diálogo, introduza **aprovisionamento de AMT** no **nome** campo e, em seguida, introduza o número seguinte para o **identificador de objeto**: **2.16.840.1.113741.1.2.3**.  

11. Escolha **OK**e, em seguida, escolha **OK** no **Adicionar política de aplicação** caixa de diálogo.  

12. Escolha **OK** no **Editar extensão de políticas de aplicação** caixa de diálogo.  

13. No **propriedades de novo modelo** caixa de diálogo, o seguinte está listado como o **políticas de aplicações** Descrição: **Autenticação de servidor** e **aprovisionamento de AMT**.  

14. Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins do domínio** e **Admins de empresa** grupos de segurança.  

15. Escolha **adicionar**, introduza o nome de um grupo de segurança que tenha a conta de computador para a função de sistema de sites de ponto de serviço fora de banda e, em seguida, escolha **OK**.  

16. Escolha o **inscrever** permissão para este grupo e não desmarque a **leitura** permissão...  

17. Escolha **OK**e, em seguida, feche o **modelos de certificado** consola.  

18. No **autoridade de certificação**, faça duplo clique **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

19. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **aprovisionamento de AMT do ConfigMgr**e, em seguida, escolha **OK**.  

    > [!NOTE]  
    >  Se não conseguir concluir o passo 18 ou 19, certifique-se de que está a utilizar a Enterprise Edition do Windows Server 2008. Apesar de poder configurar modelos com o Windows Server Standard Edition e os serviços de certificados, não é possível implementar certificados utilizando os modelos de certificado modificados, exceto se estiver a utilizar a Enterprise Edition do Windows Server 2008.  

20. Não feche a **Autoridade de Certificação**.  

 O certificado de aprovisionamento de AMT da AC interna está agora pronto para ser instalada no computador do ponto de serviço fora de banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Para instalar o certificado de aprovisionamento de AMT  

1.  Reinicie o servidor membro que executa o IIS para garantir que este consegue aceder ao modelo de certificado com a permissão configurada.  

2.  Escolha **iniciar**, escolha **executar**e, em seguida, introduza **mmc.exe.** Na consola vazia, escolha **ficheiro**e, em seguida, escolha **Adicionar/Remover Snap-in**.  

3.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **adicionar**.  

4.  No **snap-in de certificados** diálogo caixa, escolha **conta de computador**e, em seguida, escolha **seguinte**.  

5.  No **selecionar computador** diálogo caixa, certifique-se de que **computador Local: (o computador onde esta consola está em execução no)** está selecionada e, em seguida, escolha **concluir**.  

6.  No **adicionar ou Remover Snap-ins** diálogo caixa, escolha **OK**.  

7.  Na consola, expanda **certificados (computador Local)**e, em seguida, escolha **pessoais**.  

8.  Clique com botão direito **certificados**, escolha **todas as tarefas**e, em seguida, escolha **requisitar um novo certificado**.  

9. No **antes de começar** página, escolha **seguinte**.  

10. Se vir o **selecionar política de inscrição de certificado** página, escolha **seguinte**.  

11. No **pedir certificados** página, selecione **aprovisionamento de AMT** da lista de certificados disponíveis e, em seguida, escolha **inscrever**.  

12. No **resultados da instalação de certificados** página, aguarde até que o certificado está instalado e, em seguida, escolha **concluir**.  

13. Feche **Certificados (Computador Local)**.  

 O certificado de aprovisionamento de AMT da AC interna está agora instalado e está pronto para ser selecionado nas propriedades do ponto de serviço fora de banda.  

### <a name="create-and-issue-the-web-server-certificate-for-amt-based-computers"></a>Criar e emitir o certificado de servidor web para computadores baseados em AMT  
 Utilize o procedimento seguinte para preparar os certificados de servidor Web para computadores baseados em AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Para criar e emitir o modelo de certificado de servidor web  

1.  Crie um grupo de segurança vazio com as contas de computador AMT System Center Configuration Manager cria durante o aprovisionamento de AMT.  

2.  No servidor membro que tem os serviços de certificados instalados, a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** ao carregar o **modelos de certificado** consola.  

3.  No painel de resultados, faça duplo clique na entrada que tem **servidor Web** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition.**  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de servidor Web de AMT do ConfigMgr**para gerar os certificados web que serão utilizados para gestão fora de banda em computadores AMT.  

6.  Escolha o **nome do requerente** separador, escolha **incorporar a partir destas informações do Active Directory**, escolha **nome comum** para o **formato de nome de requerente**e, em seguida, desmarque **nome principal de utilizador (UPN)** para o nome alternativo do requerente.  

7.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins do domínio** e **Admins de empresa** grupos de segurança.  

8.  Escolha **adicionar**, introduza o nome do grupo de segurança que criou para o aprovisionamento de AMT e, em seguida, escolha **OK**.  

9. Escolha o seguinte **permitir** permissões para este grupo de segurança: **Leitura** e **inscrever**.  

10. Escolha **OK**e, em seguida, feche o **modelos de certificado** consola.  

11. No **autoridade de certificação** consola, faça duplo clique **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

12. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de servidor Web de AMT do ConfigMgr**e, em seguida, escolha **OK**.  

13. Se não necessitar de criar e emitir mais certificados, feche **autoridade de certificação**.  

 O modelo de servidor AMT Web está agora preparado para configurar computadores baseados em AMT com certificados de servidor web. Escolha este modelo de certificado no propriedades do componente de gestão fora de banda.  

### <a name="create-and-issue-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Criar e emitir certificados de autenticação 802.1 X AMT em computadores de cliente  
 Utilize o procedimento seguinte se os computadores baseados em AMT forem utilizar certificados de cliente para redes com ou sem fios com autenticação 802.1X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Para criar e emitir o modelo de certificado de autenticação de cliente da AC  

1.  No servidor membro que tem os serviços de certificados instalados, a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** ao carregar o **modelos de certificado** consola.  

2.  No painel de resultados, faça duplo clique na entrada que tem **autenticação de estação de trabalho** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition.**  

3.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de autenticação de cliente do ConfigMgr AMT 802.1 X**, para gerar os certificados de cliente que serão utilizados para gestão fora de banda em computadores AMT.  

4.  Escolha o **nome do requerente** separador, escolha **incorporar a partir destas informações do Active Directory**e, em seguida, escolha **nome comum** para o **formato de nome de requerente**. Limpar **nome DNS** para o requerente alternativo nome e, em seguida, escolha **nome principal de utilizador (UPN)**.  

5.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins do domínio** e **Admins de empresa** grupos de segurança.  

6.  Escolha **adicionar**, introduza o nome do grupo de segurança que irá especificar nas propriedades do componente de gestão fora de banda para conter as contas de computador dos computadores baseados em AMT e, em seguida, escolha **OK**.  

7.  Selecione o seguinte **permitir** permissões para este grupo de segurança: **Leitura** e **inscrever**.  

8.  Escolha **OK**e, em seguida, feche o **modelos de certificado** consola de gestão, **certtmpl - [modelos de certificado]**.  

9. No **autoridade de certificação** consola de gestão, faça duplo clique **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

10. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de autenticação de cliente do ConfigMgr AMT 802.1 X**e, em seguida, escolha **OK**.  

11. Se não precisar de criar e emitir mais certificados, feche **autoridade de certificação**.  

 O modelo de certificado de autenticação de cliente está agora pronto para emitir certificados para computadores baseados em AMT que podem ser utilizados para autenticação 802.1 X de clientes. Escolha este modelo de certificado no propriedades do componente de gestão fora de banda.  

##  <a name="BKMK_MacClient_SP1"></a>Implementar o certificado de cliente para computadores Mac  

Esta implementação de certificado tem um procedimento único para criar e emitir o modelo de certificado de inscrição na autoridade de certificação.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a>Criar e emitir o modelo de certificado na autoridade de certificação de um cliente de Mac  
 Este procedimento cria um modelo de certificado personalizado para computadores Mac do System Center Configuration Manager e adiciona o modelo de certificado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado que pode ter criado para computadores cliente com Windows ou para pontos de distribuição.  
>   
>  Quando cria um novo modelo de certificado para este certificado, pode restringir o pedido de certificado para os utilizadores autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de cliente Mac na autoridade de certificação  

1.  Crie um grupo de segurança que tenha as contas de utilizador para os utilizadores administrativos que irão inscrever o certificado no computador Mac utilizando o System Center Configuration Manager.  

2.  No servidor membro que está a executar a consola da autoridade de certificação, clique com botão direito **modelos de certificado**e, em seguida, escolha **gerir** para carregar a consola de gestão de modelos de certificado.  

3.  No painel de resultados, faça duplo clique na entrada que apresenta **sessão autenticada** no **nome a apresentar do modelo** coluna e, em seguida, escolha **Duplicar modelo**.  

4.  No **Duplicar modelo** diálogo caixa, certifique-se de que **Windows 2003 Server, Enterprise Edition** está selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  No **propriedades de novo modelo** caixa de diálogo a **geral** separador, introduza um nome de modelo, tal como **certificado de cliente Mac do ConfigMgr**para gerar o certificado de cliente Mac.  

6.  Escolha o **nome do requerente** separador, certifique-se de que **incorporar a partir destas informações do Active Directory** é selecionado, escolher **nome comum** para o **formato de nome do requerente:**e, em seguida, desmarque **nome principal de utilizador (UPN)** de **incluir estas informações no nome alternativo do requerente**.  

7.  Escolha o **segurança** separador e, em seguida, remova o **inscrever** permissão a partir do **Admins do domínio** e **Admins de empresa** grupos de segurança.  

8.  Escolha **adicionar**, especifique o grupo de segurança que criou no passo um e, em seguida, escolha **OK**.  

9. Escolha o **inscrever** permissão para este grupo e não desmarque a **leitura** permissão.  

10. Escolha **OK**e, em seguida, feche **consola de modelos de certificado**.  

11. Na consola de autoridade de certificação, clique com botão direito **modelos de certificado**, escolha **novo**e, em seguida, escolha **modelo de certificado a emitir**.  

12. No **ativar modelos de certificado** diálogo caixa, selecione o novo modelo que acabou de criar, **certificado de cliente Mac do ConfigMgr**e, em seguida, escolha **OK**.  

13. Se não necessitar de criar e emitir mais certificados, feche **autoridade de certificação**.  

 O modelo de certificado de cliente Mac está agora pronto para ser selecionado quando configurar as definições de cliente para inscrição.
