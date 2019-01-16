---
title: Configurar a infraestrutura de certificados
titleSuffix: Configuration Manager
description: Saiba como configurar a inscrição de certificado no System Center Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 783512841b61d6fa10e3f2832100e9000576e65a
ms.sourcegitcommit: 2687489aa409a050dcacd67f17b3dad3ab7f1804
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54316529"
---
# <a name="configure-certificate-infrastructure"></a>Configurar a infraestrutura de certificados

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Saiba como configurar a infraestrutura de certificados no System Center Configuration Manager. Antes de começar, verifique a existência de pré-requisitos listados em [Pré-requisitos para perfis de certificado no System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Utilize estes passos para configurar a infraestrutura para o SCEP ou certificados PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Passo 1 – instalar e configurar o serviço de inscrição de dispositivos de rede e dependências (para certificados SCEP)

 Tem de instalar e configurar o serviço de função Serviço de Inscrição de Dispositivos de Rede para Serviços de Certificados do Active Directory (AD CS), alterar as permissões de segurança nos modelos de certificados, implementar um certificado de cliente de infraestrutura de chave pública (PKI) e editar o registo para aumentar o limite do tamanho predefinido do URL do IIS (Serviços de Informação Internet). Se necessário, também tem de configurar a autoridade de certificação (AC) emissora para permitir um período de validade personalizado.  

> [!IMPORTANT]  
>  Antes de configurar o System Center Configuration Manager para trabalhar com o serviço de inscrição de dispositivos de rede, certifique-se de que a instalação e configuração do serviço de inscrição de dispositivos de rede. Se estas dependências não estão a funcionar corretamente, terá dificuldade em resolver problemas de inscrição de certificados com o System Center Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Para instalar e configurar o Serviço de Inscrição de Dispositivos de Rede e dependências  

1. Num servidor que esteja a executar o Windows Server 2012 R2, instale e configure o serviço de função Serviço de Inscrição de Dispositivos de Rede para a função de servidor Serviços de Certificados do Active Directory. Para obter mais informações, veja [Documentação de Orientação do Serviço de Inscrição de Dispositivos de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca Serviços de Certificados do Active Directory na TechNet.  

2. Verifique e, se necessário, modifique as permissões de segurança para os modelos de certificados que o Serviço de Inscrição de Dispositivos de Rede está a utilizar:  

   -   Para a conta que executa a consola do System Center Configuration Manager: **Leitura** permissão.  

        Esta permissão é necessária. Assim, quando executa o Assistente para Criar Perfil de Certificado, pode procurar para selecionar o modelo de certificado que pretende utilizar quando cria um perfil de definições de SCEP. A seleção de um modelo de certificado é sinónimo de que algumas definições no assistente são automaticamente preenchidas. Logo, há menos para si para configurar e é menor o risco de escolha de definições que não são compatíveis com os modelos de certificados que o Serviço de Inscrição de Dispositivos de Rede está a utilizar.  

   -   Para a conta de serviço SCEP que o conjunto aplicacional do serviço de inscrição de dispositivos de rede utiliza: **Leia** e **inscrever** permissões.  

        Este requisito não é específico para o System Center Configuration Manager, mas faz parte da configuração do serviço de inscrição de dispositivos de rede. Para obter mais informações, veja [Documentação de Orientação do Serviço de Inscrição de Dispositivos de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca Serviços de Certificados do Active Directory na TechNet.  

   > [!TIP]  
   >  Para identificar os modelos de certificado do serviço de inscrição de dispositivos de rede está a utilizar, veja a seguinte chave de registo no servidor que está a executar o serviço de inscrição de dispositivos de rede: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Estas são as permissões de segurança predefinidas que serão convenientes para a maior parte dos ambientes. No entanto, pode utilizar uma configuração de segurança alternativa. Para obter mais informações, veja [Planear permissões de modelo de certificado para perfis de certificado no System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Implemente neste servidor um certificado PKI que suporta a autenticação de cliente. É possível que já disponha de um certificado adequado instalado no computador que pode utilizar ou poderá ter de (ou preferir) implementar um certificado especificamente para esta finalidade. Para obter mais informações sobre os requisitos deste certificado, consulte os detalhes de servidores a executar o módulo de política do Configuration Manager com o serviço de função Serviço de inscrição de dispositivos de rede no **certificados PKI para servidores** secção do [requisitos de certificado PKI para o System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) tópico.  

   > [!TIP]
   >  Se precisar de ajuda para implementar este certificado, pode utilizar as instruções para [implementar o certificado de cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012), porque os requisitos de certificado são os mesmos com uma exceção:  
   > 
   > - Não selecione a caixa de verificação **Permitir que a chave privada seja exportada** no separador **Processamento de Pedidos** das propriedades para o modelo de certificado.  
   > 
   >   Não é necessário exportar este certificado com a chave privada porque poderá procurar o arquivo do computador local e selecioná-lo quando configurar o módulo de política do System Center Configuration Manager.  

4. Localize o certificado de raiz ao qual o certificado de autenticação de cliente está encadeado. Em seguida, exporte este certificado da AC de raiz para um ficheiro de certificados (. cer). Guarde este ficheiro numa localização segura à qual pode aceder em segurança quando, posteriormente, instalar e configurar o servidor do sistema de sites para o ponto de registo de certificados.  

5. No mesmo servidor, utilize o editor de registo para aumentar o limite do tamanho predefinido do URL do IIS, definindo os seguintes valores DWORD de chaves de registo em HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Defina a chave **MaxFieldLength** como **65534**.  

   - Defina a chave **MaxRequestBytes** como **16777216**.  

     Para obter mais informações, consulte o artigo [820129: Definições de registo de HTTP. sys do Windows](http://go.microsoft.com/fwlink/?LinkId=309013) na Base de dados de Conhecimento Microsoft.  

6. No mesmo servidor, no Gestor de Serviços de Informação Internet (IIS), modifique as definições de filtragem de pedidos para a aplicação de /certsrv/mscep e, em seguida, reinicie o servidor. Na caixa de diálogo **Editar Definições de Filtragem de Pedidos**, as definições de **Limites do Pedido** devem ser as seguintes:  

   - **Máximo comprimento de conteúdo permitido (Bytes)**: **30000000**  

   - **Comprimento máximo do URL (Bytes)**: **65534**  

   - **Cadeia de consulta máxima (Bytes)**: **65534**  

     Para obter mais informações sobre estas definições e como configurá-las, veja [Requests Limits](http://go.microsoft.com/fwlink/?LinkId=309014) na Biblioteca de Referência do IIS.  

7. Se pretender poder pedir um certificado que tenha um período de validade inferior ao modelo de certificado que está a utilizar: Esta configuração está desativada por predefinição para uma AC empresarial. Para ativar esta opção numa AC empresarial, utilize a ferramenta da linha de comandos Certutil e, em seguida, pare e reinicie o serviço de certificados utilizando os seguintes comandos:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Para obter mais informações, veja [Ferramentas e Definições dos Serviços de Certificados](http://go.microsoft.com/fwlink/p/?LinkId=309015) na biblioteca de Tecnologias PKI na TechNet.  

8. Certifique-se de que o serviço de inscrição de dispositivos de rede está a funcionar, utilizando a ligação seguinte como exemplo: **https://server.contoso.com/certsrv/mscep/mscep.dll**. Deverá ver a página Web incorporada do Serviço de Inscrição de Dispositivos de Rede. Esta página Web explica o que o serviço é e explica que os dispositivos de rede utilizam o URL para submeter pedidos de certificados.  

   Agora que o Serviço de Inscrição de Dispositivos de Rede e dependências estão configurados, está pronto para instalar e configurar o ponto de registo de certificados.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Passo 2 - instalar e configurar o ponto de registo de certificados.

Tem de instalar e configurar o ponto de registo de pelo menos um certificado na hierarquia do System Center Configuration Manager e pode instalar esta função de sistema de sites no site de administração central ou num site primário.  

> [!IMPORTANT]  
>  Antes de instalar o ponto de registo de certificados, veja a secção **Requisitos do Sistema de Sites** do tópico [Configurações suportadas do System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para obter os requisitos do sistema operativo e dependências para o ponto de registo de certificados.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Para instalar e configurar o ponto de registo de certificados  

1. Na consola do System Center Configuration Manager, clique em **administração**.  

2. Na área de trabalho **Administração**, expanda **Configuração do Site**, clique em **Servidores e Funções de Sistema de Sites** e selecione o servidor que pretende utilizar para o ponto de registo de certificados.  

3. No separador **Home Page**, no grupo **Servidor**, clique em **Adicionar Funções do Sistema de Sites**.  

4. Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.  

5. Na página de **Proxy**, clique em **Seguinte**. O ponto de registo de certificados não utiliza as definições de proxy de Internet.  

6. Na página **Seleção da Função do Sistema**, selecione o **Ponto de registo de certificados** na lista de funções disponíveis e clique em **Seguinte**. 

7. Sobre o **modo de registo de certificados** página, selecione se pretende que este ponto de registo de certificados para **pedidos de certificado SCEP de processo**, ou **pedidos de certificado PFX do processo** . Um ponto de registo de certificados não é possível processar os dois tipos de pedidos, mas pode criar certificado vários pontos de registo se estiver a trabalhar com ambos os tipos de certificado.

   Se a processar os certificados PFX, terá de escolher uma autoridade de certificação, a Microsoft ou Entrust.

8. O **definições de ponto de registo de certificados** página varia de acordo com o tipo de certificado:
   - Se tiver selecionado **pedidos de certificado SCEP de processo**, em seguida, configure o seguinte:
     -   **Nome do Web site**, **número de porta de HTTPS**, e **nome da aplicação Virtual** para o ponto de registo de certificados. Estes campos são preenchidos automaticamente com valores predefinidos. 
     -   **URL para o certificado de AC do serviço de inscrição de dispositivos de rede e de raiz** -clique em **Add**, em seguida, no **adicionar URL e certificado da AC de raiz** diálogo caixa, especifique o seguinte:
         - **URL para o serviço de inscrição de dispositivos de rede**: Especifique o URL no seguinte formato: https://*< server_FQDN >*/certsrv/mscep/mscep.dll. Por exemplo, se o FQDN do seu servidor que está a executar o serviço de inscrição de dispositivos de rede for server1.contoso.com, digite **https://server1.contoso.com/certsrv/mscep/mscep.dll**.
         - **Certificado de AC de raiz**: Procure e selecione o ficheiro de certificado (. cer) que criou e guardou no **passo 1: Instalar e configurar o serviço de inscrição de dispositivos de rede e dependências**. Este certificado de AC de raiz permite que o ponto de registo de certificados para validar o cliente de certificado de autenticação que o módulo de política do System Center Configuration Manager irá utilizar.  

   - Se tiver selecionado **pedidos de certificado PFX processo**, configure os detalhes de ligação e credenciais para a autoridade de certificado selecionado.

     - Para utilizar o Microsoft como a autoridade de certificação, clique em **Add** , em seguida, no **adicionar uma autoridade de certificação e uma conta** diálogo caixa, especifique o seguinte:
         - **Nome do servidor de autoridade de certificado** -introduza o nome do seu servidor de autoridade de certificado.
         - **Conta de autoridade de certificado** -clique em **definir** para selecionar ou criar a conta que tem permissões para inscrever em modelos na autoridade de certificação.
         - **Conta de ligação de ponto de registo de certificados** - selecione ou crie a conta que liga o ponto de registo de certificados para a base de dados do Configuration Manager. Alteratively, pode utilizar a conta de computador local do computador que aloja o ponto de registo de certificados.
         - **Conta do Active Directory certificado publicação** – Selecione uma conta, ou criar uma nova conta que será utilizada para publicar certificados para objetos de utilizador no Active Directory.

         - Na **URL para o certificado de AC de inscrição de dispositivos de rede e de raiz** caixa de diálogo, especifique o seguinte e, em seguida, clique em **OK**:  

     - Para utilizar Entrust como a autoridade de certificação, especifique:

       - O **URL de serviço web do MDM**
       - As credenciais de nome de utilizador e palavra-passe para o URL.

         Ao utilizar a API de MDM para definir o URL do serviço web Entrust, certifique-se de que utilizar, pelo menos, versão 9 da API, conforme mostrado no exemplo a seguir:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Versões anteriores da API não suportam a Entrust.

9. Clique em **Seguinte** e conclua o assistente.  

10. Aguarde alguns minutos para deixar a instalação chegar ao fim e, em seguida, verifique se o ponto de registo de certificados foi instalado com êxito através de qualquer um dos seguintes métodos:  

    -   Na área de trabalho **Monitorização**, expanda **Estado do Sistema**, clique em **Estado do Componente** e procure mensagens de estado no componente **SMS_CERTIFICATE_REGISTRATION_POINT**.  

    -   No servidor do sistema de sites, utilize o ficheiro *<ConfigMgr Installation Path\>* \Logs\crpsetup.log e o ficheiro *<ConfigMgr Installation Path\>* \Logs\crpmsi.log. Uma instalação com êxito irá devolver um código de saída igual a 0.  

    -   Com um browser, certifique-se de que pode ligar para o URL do € de pointâ de registo de certificados ", por exemplo, https://server1.contoso.com/CMCertificateRegistration. Deverá ver uma página **Erro de Servidor** para o nome da aplicação, com uma descrição de HTTP 404.  

11. Localize o ficheiro de certificado exportado para a AC de raiz que o ponto de registo de certificados criou automaticamente na seguinte pasta no computador do servidor do site primário: *<ConfigMgr Installation Path\>* \inboxes\certmgr.box. Guarde este ficheiro numa localização segura à qual pode aceder em segurança quando, posteriormente, instalar o módulo de política do System Center Configuration Manager no servidor que está a executar o serviço de inscrição de dispositivos de rede.  

    > [!TIP]  
    >  Este certificado não está imediatamente disponível nesta pasta. Poderá ter de aguardar algum tempo (por exemplo, meia hora) antes do System Center Configuration Manager copia o ficheiro para esta localização.  


## <a name="step-3----install-the-system-center-configuration-manager-policy-module-for-scep-certificates-only"></a>Passo 3 – instalar o módulo de política do System Center Configuration Manager (para certificados SCEP).

Tem de instalar e configurar o módulo de política do System Center Configuration Manager em cada servidor que especificou no **passo 2: Instalar e configurar o ponto de registo de certificados** como **URL para o serviço de inscrição de dispositivos de rede** nas propriedades para o ponto de registo de certificados.  

##### <a name="to-install-the-policy-module"></a>Para instalar o Módulo de Política  

1. No servidor que executa o serviço de inscrição de dispositivos de rede, inicie sessão como um administrador de domínio e copie os seguintes ficheiros do < Suportededadosdeinstalaçãodoconfigmgr\>\SMSSETUP\POLICYMODULE\X64 pasta sobre o System Center Configuration Manager suporte de dados de instalação para uma pasta temporária:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Além disso, se tiver uma pasta LanguagePack no suporte de dados de instalação, copie esta pasta e respetivo conteúdo.  

2. A partir da pasta temporária, execute PolicyModuleSetup.exe para iniciar o Assistente de configuração de módulo de política do System Center Configuration Manager.  

3. Na página inicial do assistente, clique em **Seguinte**, aceite os termos de licenciamento e clique em **Seguinte**.  

4. Na página **Pasta de Instalação**, aceite a pasta de instalação predefinida para o módulo de política ou especifique uma pasta alternativa e clique em **Seguinte**.  

5. Na página **Ponto de Registo de Certificados**, especifique o URL do ponto de registo de certificados utilizando o FQDN do servidor do sistema de sites e o nome da aplicação virtual que é especificado nas propriedades para o ponto de registo de certificados. O nome de aplicação virtual predefinido é CMCertificateRegistration. Por exemplo, se o servidor de sistema de sites tiver um FQDN do server1.contoso.com e utilizou o nome de aplicação virtual predefinido, especifique **https://server1.contoso.com/CMCertificateRegistration**.  

6. Aceite a porta predefinida **443** ou especifique o número da porta alternativa que o ponto de registo de certificados está a utilizar e clique em **Seguinte**.  

7. Sobre o **certificado de cliente para o módulo de política**página, procure e especifique o certificado de autenticação de cliente que implementou no **passo 1: Instalar e configurar o serviço de inscrição de dispositivos de rede e dependências**e, em seguida, clique em **próxima**.  

8. Sobre o **certificado do ponto de registo de certificados** página, clique em **procurar** para selecionar o ficheiro de certificado exportado para a AC de raiz que localizou e guardou no final do **passo 2: Instalar e configurar o ponto de registo de certificados**.  

   > [!NOTE]  
   >  Se não tiver guardado anteriormente este ficheiro de certificado, o mesmo está localizado em <ConfigMgr Installation Path\>\inboxes\certmgr.box no computador do servidor do site.  

9. Clique em **Seguinte** e conclua o assistente.  

   Se pretender desinstalar o módulo de política do System Center Configuration Manager, utilize **programas e funcionalidades** no painel de controlo. 

 
Agora que concluiu os passos de configuração, está pronto para implementar certificados para utilizadores e dispositivos através da criação e implementação de perfis de certificado. Para obter mais informações sobre como criar perfis de certificado, veja [Como criar perfis de certificado no System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  
