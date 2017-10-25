---
title: Como criar perfis de certificado SCEP | Microsoft Docs
description: Saiba como utilizar perfis de certificado para aprovisionar dispositivos geridos com certificados que precisam no System Center Configuration Manager.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 1e00804d27ecef2aadd8bfa395db1919c46243ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="create-certificate-profiles"></a>Criar perfis de certificado

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize perfis de certificado no Configuration Manager (SCCM) para aprovisionar dispositivos geridos com certificados necessitam para aceder a recursos da empresa. Antes de criar perfis de certificado, configurar a infraestrutura de certificados conforme descrito em [configurar a infraestrutura de certificados para o System Center Configuration Manager](certificate-infrastructure.md).  

Este tópico descreve como criar de raiz fidedigna e perfis de certificado SCEP. Se pretender criar perfis de certificado PFX, consulte [perfis de certificado PFX criar](../../protect/deploy-use/create-pfx-certificate-profiles.md).

Para criar um perfil de certificado:

1.  Inicie o Assistente de perfil de certificado de criar.
1.  Fornece informações gerais sobre o certificado.
1.  Configure um certificado de autoridade (AC) de certificados fidedignos.  
1.  Configure informações de certificado SCEP (apenas para certificados SCEP).  
1.  Especificar as plataformas suportadas para o perfil de certificado.


## <a name="start-the-create-certificate-profile-wizard"></a>Iniciar o Assistente para criar perfil de certificado  

1.  Na consola do System Center Configuration Manager, clique em **ativos e compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Definições de Compatibilidade**, expanda **Acesso a Recursos da Empresa**e clique em **Perfis de Certificado**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Perfil de Certificado**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Fornecer informações gerais sobre o perfil de certificado  

Na página **Geral** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

-   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

-   **Descrição**: Forneça uma descrição que proporcione uma descrição geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

-   **Especifique o tipo de perfil de certificado que pretende criar**: Escolha um certificado que se segue tipos de perfil:  

-   **Certificado de AC fidedigna**: Selecione este tipo de perfil de certificado se pretender implementar uma autoridade de certificação (AC) de raiz fidedigna ou certificado de AC intermediária para formar uma cadeia de fidedignidade de certificados quando o utilizador ou dispositivo tem de autenticar outro dispositivo. Por exemplo, o dispositivo poderá ser um servidor RADIUS (Remote Authentication Dial-In User Service) ou um servidor de rede privada virtual (VPN). Tem também de configurar um perfil de certificado de AC fidedigna para poder criar um perfil de certificado SCEP. Neste caso, o certificado de AC fidedigna tem de ser o certificado de raiz fidedigna para a AC que emitirá o certificado para o utilizador ou o dispositivo.  

-   **Definições do protocolo de inscrição de certificados (SCEP) Simple**: Selecione este tipo de perfil de certificado se pretender pedir um certificado para um utilizador ou dispositivo, utilizando o protocolo de inscrição de certificado simples e o serviço de função Serviço de inscrição de dispositivos de rede.

-   **Definições de informações Exchange PKCS #12 (PFX) pessoais - importar**: Selecione esta opção para importar um certificado PFX. Para obter mais informações sobre a criação do certificado PFX, consulte [perfis de certificado PFX importação](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md).

-   **Criar definições de informações Exchange PKCS #12 (PFX) pessoais -**: Selecione esta opção para processar os certificados PFX através de uma autoridade de certificação. Para obter mais informações sobre a criação do certificado PFX, consulte [perfis de certificado PFX criar](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md).


## <a name="configure-a-trusted-ca-certificate"></a>Configurar um certificado de AC fidedigna  

> [!IMPORTANT]  
>  Tem de configurar pelo menos um perfil de certificado de AC fidedigna para poder criar um perfil de certificado SCEP.    
>  
>  Se alterar qualquer um destes valores depois do certificado é implementado um novo certificado ser solicitado:
>  -  Fornecer armazenamento de chaves
>  -  Nome do modelo de certificado
>  -  Tipo de certificado
>  -  Formato de nome do requerente
>  -  Nome alternativo do requerente
>  -  Período de validade do certificado
>  -  Utilização de chave
>  -  Tamanho da chave
>  -  Utilização alargada da chave
>  -  Certificado de AC de raiz

1.  Na página **Certificado de AC fidedigna** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

 -   **Ficheiro de certificado**: Clique em **importação** e, em seguida, navegue para o ficheiro de certificado que pretende utilizar.  

 -   **Arquivo de destino**: Para dispositivos que tenham mais do que um arquivo de certificados, selecione onde pretende armazenar o certificado. Para dispositivos que têm apenas um armazenamento, esta definição é ignorada.  

2.  Utilize o valor **Thumbprint do certificado** para verificar se importou o certificado correto.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Configure as informações de certificado SCEP (apenas para certificados SCEP)  

1.  Na página **Servidores do SCEP** do Assistente para Criar Perfil de Certificado, especifique os URLs para os Servidores NDES que irão emitir certificados através do SCEP. Pode optar por atribuir automaticamente um URL de NDES com base na configuração do servidor do sistema de sites Ponto de Registo de Certificados ou adicionar os URLs manualmente.  

2.  Concluir o **inscrição SCEP** página do Assistente para criar perfil de certificado.

 -  **Repete**: Especifique o número de vezes que o dispositivo repete automaticamente o pedido de certificado para o servidor que está a executar o serviço de inscrição de dispositivos de rede. Esta definição suporta o cenário onde um gestor de AC tem de aprovar um pedido de certificado antes de ser aceite. Esta definição é normalmente utilizada para ambientes de alta segurança ou se tiver uma AC emissora autónoma, em vez de uma AC empresarial. Também poderá utilizar esta definição para fins de teste, para poder inspecionar as opções de pedido de certificado antes de a AC emissora processar o pedido de certificado. Utilize esta definição com a definição **Intervalo entre repetições (minutos)** .  

 -   **Intervalo entre repetições (minutos)**: Especifique o intervalo, em minutos, entre cada tentativa de inscrição quando utilizar a aprovação do Gestor de AC antes da AC emissora processar o pedido de certificado. Se utilizar a aprovação do gestor para fins de teste, provavelmente pretenderá especificar um valor baixo, de modo a não esperar muito tempo para que o dispositivo repita o pedido de certificado após a aprovação do pedido. No entanto, se utilizar a aprovação do gestor numa rede de produção, é provável que pretenda especificar um valor maior para dar tempo suficiente ao administrador da AC para verificar e aprovar ou negar aprovações pendentes.  

 -   **Limiar de renovação (%)**: Especifique a percentagem da duração do certificado que permanece antes do dispositivo pedir renovação do certificado.  

 -   **Chave (KSP) do fornecedor de armazenamento**: Especifique onde será armazenada a chave para o certificado. Escolha um dos seguintes valores:  

   -   **Instalar no Trusted Platform Module (TPM) caso esteja presente**: Instala a chave no TPM. Se o TPM não estiver presente, a chave será instalada no fornecedor de armazenamento da chave de software.  

   -   **Instalar no Trusted Platform Module (TPM) de falhar, caso contrário**: Instala a chave no TPM. Se o módulo TPM não estiver presente, a instalação falhará.  

   -   **Instalar para Windows Hello para falhar caso contrário, negócio**: Esta opção está disponível para dispositivos Windows 10 Desktop e Mobile. Inscreve a chave para **Windows Hello para empresas**, descritas na [Windows Hello para definições da empresa no System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md). Esta opção também lhe permite **Exigir autenticação multifator** durante a inscrição de dispositivos antes de emitir certificados para os mesmos. Consulte [Proteger os dispositivos Windows com a autenticação multifator](https://technet.microsoft.com/library/dn889751.aspx) para mais informações.

   > [!NOTE]  
   > 
   > Quando um utilizador cria um Windows Hello para empresas PIN, o Windows envia uma notificação que o Configuration Manager escuta. Isto permite tornar-se rapidamente com suporte para o Configuration Manager dos utilizadores que criou um Windows Hello PIN. O Configuration Manager, em seguida, também podem emitir novos certificados para esses utilizadores se o Windows Hello é utilizado como o fornecedor de armazenamento de chaves num perfil de certificado.  

   -   **Instalar no fornecedor de armazenamento de chaves de Software**: Instala a chave para o fornecedor de armazenamento da chave de software.  

 -   **Dispositivos para inscrição de certificados**: Se o perfil de certificado for implementado numa coleção de utilizador, selecione se pretende permitir inscrição de certificados apenas o dispositivo primário do utilizador ou em todos os dispositivos que o utilizador inicia sessão. Se o perfil de certificado for implementado numa coleção de dispositivos, selecione se pretende permitir a inscrição de certificados apenas ao utilizador principal do dispositivo ou a todos os utilizadores que iniciem sessão no dispositivo.  

3.  Na página **Propriedades do Certificado** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

 -   **Nome do modelo de certificado**: Clique em **procurar** para selecionar o nome de um modelo de certificado que o serviço de inscrição de dispositivos de rede está configurado para utilizar e que tenha sido adicionado a uma AC emissora. Para encontrar modelos de certificado, a conta de utilizador que está a utilizar para executar a consola do System Center Configuration Manager tem de ter permissão de leitura para o modelo de certificado. Em alternativa, se não conseguir utilizar **Procurar**, escreva o nome do modelo de certificado.  

 > [!IMPORTANT]
 >   
 >  Se o nome do modelo de certificado contiver carateres não ASCII (por exemplo, carateres do alfabeto chinês), o certificado não será implementado. Para garantir que o certificado é implementado, tem de criar primeiro uma cópia do modelo de certificado na AC e mudar o nome da cópia utilizando carateres ASCII.  

   Tenha em atenção o seguinte, consoante procurar o modelo de certificado ou escrever o nome do certificado:  

 -   Se procurar para selecionar o nome do modelo de certificado, alguns campos da página serão preenchidos automaticamente a partir do modelo de certificado. Em alguns casos, não é possível alterar estes valores, a menos que escolha um modelo de certificado diferente.  

 -   Se escrever o nome do modelo de certificado, certifique-se de que o nome corresponde exatamente a um dos modelos de certificado listados no registo do servidor com o Serviço de Inscrição de Dispositivos de Rede em execução. Certifique-se de que especifica o nome do modelo de certificado e não o nome a apresentar do modelo de certificado.  

   Para localizar os nomes dos modelos de certificado, navegue para a seguinte chave: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP. Verá os modelos de certificado listados como valores para **EncryptionTemplate**, **GeneralPurposeTemplate**e **SignatureTemplate**. Por predefinição, o valor dos três modelos de certificado é **IPSECIntermediateOffline**, que é mapeado para o nome a apresentar de modelo **IPSec (Pedido offline)**.  

   > [!WARNING]  
   > 
   >  Porque o System Center Configuration Manager não consegue verificar o conteúdo do modelo de certificado quando escreve o nome do modelo de certificado em vez de procurar, poderá conseguir Selecionar opções que não suporta o modelo de certificado, que resultará num pedido de certificado falhado. Quando isto acontecer, verá uma mensagem de erro de w3wp.exe no ficheiro CPR.log que indica que o nome do modelo na solicitação de assinatura de certificado (CSR) do certificado e no desafio não coincidem.  
   >   
   >  Quando escrever o nome do modelo de certificado especificado para o valor **GeneralPurposeTemplate** , terá de selecionar as opções **Cifragem de chaves** e **Assinatura digital** para este perfil de certificado. No entanto, se pretender ativar apenas a opção **Cifragem de chaves** neste perfil de certificado, especifique o nome do modelo de certificado da chave **EncryptionTemplate** . Da mesma forma, se pretender ativar apenas a opção **Assinatura digital** neste perfil de certificado, especifique o nome do modelo de certificado da chave **SignatureTemplate** .  

 -   **Tipo de certificado**: Selecione se o certificado será implementado num dispositivo ou um utilizador.  
 -   **Formato de nome de requerente**: Na lista, selecione a forma como o System Center Configuration Manager cria automaticamente o nome do requerente no pedido de certificado. Se o certificado se destinar a um utilizador, pode também incluir o endereço de e-mail do utilizador no nome do requerente. 
    
   > [!NOTE]  
   > 
   > Selecionar **número IMEI** ou **número de série** permite-lhe diferenciar entre vários dispositivos que pertencem ao mesmo utilizador. Por exemplo, esses dispositivos foi possível partilhar o nome comum, mas não um número IMEI ou número de série. Se o dispositivo não comunica um número de série ou IMEI, o certificado será emitido com o nome comum.

 -   **Nome alternativo do requerente**: Especifique a forma como o System Center Configuration Manager cria automaticamente os valores de nome alternativo do requerente (SAN) no pedido de certificado. Por exemplo, se tiver selecionado um tipo de certificado de utilizador, pode incluir o nome principal de utilizador (UPN) no nome alternativo do requerente.  Se o certificado de cliente for utilizado para autenticar um Servidor de Políticas de Rede, tem de definir o nome alternativo do requerente com o UPN.  

   > [!NOTE]  
   >  - Os dispositivos iOS suportam formatos de nome do requerente e de nome alternativo do requerente limitados em certificados SCEP. Se especificar um formato que não seja suportado, os certificados não serão inscritos em dispositivos iOS. Quando configurar um perfil de certificado SCEP para implementação em dispositivos iOS, utilize o **Nome comum** para o **Formato de nome do requerente**e **Nome DNS**, **Endereço de correio eletrónico** ou **UPN** para o **Nome alternativo do requerente**.  

 -   **Período de validade do certificado**: Se tiver executado o certutil - setreg Policy\EditFlags + comando EDITF_ATTRIBUTEENDDATE na AC emissora, que permite um período de validade personalizado, pode especificar a quantidade de tempo restante até o certificado expirar. Para obter mais informações sobre este comando, consulte [infraestrutura de certificados no System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md) tópico.  

   Pode especificar um valor inferior ao período de validade do modelo de certificado especificado, mas não superior. Por exemplo, se o período de validade do certificado no modelo de certificado for dois anos, pode especificar um valor de um ano, mas não um valor de cinco anos. O valor deve também ser inferior ao período de validade restante do certificado da AC emissora.  

 -   **Utilização da chave**: Especifique as opções de utilização de chave para o certificado. Pode selecionar de entre as seguintes opções:  

        -   **Cifragem de chaves**: Permitir a troca de chaves apenas quando a chave for encriptada.  

        -   **Assinatura digital**: Permitir a troca de chave apenas quando uma assinatura digital ajudar a proteger a chave.  

   Se tiver selecionado um modelo de certificado utilizando **Procurar**, poderá não conseguir alterar estas definições, a menos que selecione outro modelo de certificado.  

   O modelo de certificado selecionado deve ser configurado com uma ou ambas as duas opções de utilização da chave acima. Caso contrário, verá a mensagem **Utilização da chave no CSR e no desafio não correspondem** no ficheiro de registo do ponto de registo de certificados, **Crp.log**.  


   -   **Tamanho da chave (bits)**: Selecione o tamanho da chave em bits.  

   -   **Utilização da chave expandida**: Clique em **selecione** para adicionar valores para o certificado do objetivo. Na maioria dos casos, o certificado irá exigir a **Autenticação de Cliente** para o utilizador ou dispositivo poder ser autenticado num servidor. Contudo, pode adicionar mais utilizações de chave conforme necessário.  


   -   **Algoritmo hash**: Selecione um dos tipos de algoritmo hash disponíveis para utilizar com este certificado. Selecione o maior nível de segurança que os dispositivos de ligação suportam.  

   > [!NOTE]  
   > 
   >  **SHA-2** suporta SHA-256, SHA-384 e SHA-512. O**SHA-3** suporta apenas SHA-3.  

   -   **Certificado de AC de raiz**: Clique em **selecione** para selecionar um perfil de certificado de AC que tenha configurado anteriormente e implementado no utilizador ou dispositivo de raiz. Este certificado da AC tem de ser o certificado de raiz da AC que irá emitir o certificado que está a configurar neste perfil de certificado.  

   > [!IMPORTANT]  
   >  Se especificar um certificado de AC de raiz que não seja implementado no utilizador ou dispositivo, o System Center Configuration Manager não iniciará o pedido de certificado que está a configurar neste perfil de certificado.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Especificar as plataformas suportadas para o perfil de certificado  

1. Na página **Plataformas Suportadas** do Assistente para Criar Perfil de Certificado, selecione os sistemas operativos onde pretende instalar o perfil de certificado. Ou, clique em **Selecionar tudo** para instalar o perfil de certificado para todos os sistemas operativos disponíveis.
2. Reveja o **resumo** página do assistente e escolha **concluir**. 
 
 
O novo perfil de certificado aparece no **perfis de certificado** no nó de **ativos e compatibilidade** área de trabalho e está pronto para ser implementada para utilizadores ou dispositivos, conforme descrito em [como implementar perfis no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  