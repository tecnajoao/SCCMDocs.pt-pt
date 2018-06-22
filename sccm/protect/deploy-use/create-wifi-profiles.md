---
title: Como criar perfis Wi-Fi
titleSuffix: Configuration Manager
description: Saiba como utilizar perfis de Wi-Fi no System Center Configuration Manager para implementar definições de rede sem fios para utilizadores na sua organização.
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b665143f40973c20307b99c15f94d773d43b4914
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350814"
---
# <a name="create-wi-fi-profiles"></a>Criar perfis de Wi-Fi

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize perfis Wi-Fi no System Center Configuration Manager para implementar definições de rede sem fios para utilizadores na sua organização. Ao implementar estas definições, pode torna mais fácil para os seus utilizadores a estabelecer ligação ao Wi-Fi.  

 Por exemplo, ter uma rede Wi-Fi que pretende ativar todos os dispositivos iOS ligar a. Crie um perfil de Wi-Fi que contém as definições necessárias para ligar à rede sem fios. Em seguida, implemente o perfil para todos os utilizadores com dispositivos iOS na sua hierarquia. Os utilizadores de dispositivos com iOS veem a rede da empresa na lista de redes sem fios, podendo ligar-se de imediato à mesma.  

 Pode configurar os seguintes tipos de dispositivos com perfis Wi-Fi:  

-   Dispositivos com o Windows 8.1 de 32 bits  

-   Dispositivos com o Windows 8.1 de 64 bits  

-   Dispositivos com o Windows RT 8.1  

-   Dispositivos com o Windows 10 Desktop ou Mobile  

[Criar perfis de Wi-Fi para dispositivos móveis](../../mdm/deploy-use/create-wifi-profiles.md) fornece informações sobre como utilizar perfis de Wi-Fi no Configuration Manager para implementar definições de rede sem fios para utilizadores de dispositivos móveis. "

> [!IMPORTANT]  
>  Para implementar perfis para Android, iOS, Windows Phone e inscritos do Windows 8.1 ou posterior inscritos, estes dispositivos têm de estar inscritos no Microsoft Intune. Para obter informações sobre como inscrever os seus dispositivos, consulte [inscrever dispositivos para gestão no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Ao criar um perfil Wi-Fi, pode incluir um vasto leque de definições de segurança. Estas incluem certificados para autenticação de cliente e validação do servidor que tenham sido feito o Push através de perfis de certificado do Configuration Manager. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="create-a-wi-fi-profile"></a>Criar um perfil de Wi-Fi  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **as definições de compatibilidade** >  **acesso a recursos da empresa** > **perfis Wi-Fi**.  

3.  No **home page** separador o **criar** grupo, escolha **criar perfil Wi-Fi**.  

1.  No **geral** página, introduza um nome exclusivo e uma descrição para o perfil de Wi-Fi.  Se pretender utilizar as definições de outro perfil Wi-Fi, selecione **Importar um item de perfil Wi-Fi existente de um ficheiro**.  

    > [!IMPORTANT]  
    >  Certifique-se de que o perfil Wi-Fi que importou contém XML válido para um perfil Wi-Fi. Gestor de configuração não valida o perfil quando importar o ficheiro.  

3.  No **gravidade de incompatibilidade para relatórios**, especifique o nível de gravidade reportado se o perfil de Wi-Fi é identificado como estando em conformidade nos dispositivos cliente (por exemplo, se a instalação do perfil falhar). Os níveis de gravidade disponíveis são os seguintes:  

    -   **Nenhum**: Os computadores que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  

    -   **Informações**: Os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  

    -   **Aviso**: Os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  

    -   **Crítico**: Os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager.  

    -   **Crítico com evento**: Os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  

1.  No **perfil Wi-Fi** página fornecer o nome que os dispositivos apresentarão como nome de rede.  

    > [!IMPORTANT]  
    >  O Configuration Manager não suporta a utilização do apóstrofo (**â €˜**) nem da vírgula (**,**) no nome da rede.  

2.  Especifique a maiúsculas e minúsculas **SSID**
3.  Escolha as outras opções de conectividade adequadas, incluindo.   **Ligar quando a rede não estiver a difundir o nome (SSID)**, se existir a possibilidade de que o SSID é oculto  

4.  No **configuração de segurança** página, selecione o protocolo de segurança que a rede sem fios utiliza, ou selecionem **sem autenticação (aberto)** se a rede não for protegida.
    > [!IMPORTANT]  
    >  Se estiver a criar um perfil de Wi-Fi para no\-local gestão de dispositivos móveis, o ramo atual do Configuration Manager só suporta as seguintes configurações de segurança Wi-Fi:  
    >   
    >  Tipos de segurança: **WPA2 Enterprise** ou **WPA2 pessoal**  
    > Tipos de encriptação: **AES** ou **TKIP**  
    > Tipos de EAP: **Smart Card ou outro certificado** ou **PEAP**  

    > Para dispositivos Android, os tipos de segurança **WPA pessoal**, **WPA2 pessoal** e **WEP** não são suportadas.  

2.  Selecione o método de encriptação utilizado pela rede sem fios.  

3.  Selecione o tipo de EAP utilizado para a autenticação na rede sem fios.  

     Apenas para dispositivos Windows Phone: os tipos EAP **LEAP** e **EAP-FAST** não são suportados.  

4.  Clique em **Configurar** para especificar outras propriedades para o tipo de EAP selecionado. Esta opção pode não estar disponível nalguns tipos de EAP selecionados.  

    > [!IMPORTANT]  
    >  Quando clicar em **Configurar**, a caixa de diálogo que se abre é uma caixa de diálogo do Windows. Por este motivo, deve garantir que o sistema operativo do computador que executa o Gestor de configuração consola suporta a configuração do tipo EAP selecionado.  
    >   
    >  Para dispositivos iOS, se selecionar um método não-EAP para autenticação, independentemente do método que escolher, o MS-CHAP v2 será utilizado para a ligação.  

5.  Se pretender armazenar credenciais de utilizador para que os utilizadores não tenham de introduzir as credenciais sempre que iniciarem sessão, selecione **Lembrar as credenciais de utilizador em cada início de sessão**.  

6. **Para dispositivos iOS:**  
 Configure as informações de todos os certificados necessários à ligação Wi-Fi. Tem de configurar o certificado de cliente e o nome do certificado de servidor fidedigno ou o certificado de raiz do seguinte modo:  

    -   **Nomes de certificado de servidor fidedigno**: Se o servidor que o dispositivo estabelece ligação utilizar um certificado de autenticação de servidor para identificar o servidor e ajudar a proteger o canal de comunicação, introduza o nome ou nomes no € certificateâ™ s nome requerente ou nome alternativo do requerente. O nome ou nomes são normalmente o nome de domínio completamente qualificado do servidor. Por exemplo, se o certificado do servidor tiver um nome comum de srv1.contoso.com no requerente do certificado, introduza **srv1.contoso.com**. Se o certificado do servidor tiver vários nomes especificados no nome alternativo do requerente, introduza os nomes separados por ponto e vírgula.  

    > [!TIP]  
    >  Se o certificado de cliente selecionado para o EAP ou para a autenticação de cliente de um dispositivo iOS for utilizado para autenticação num servidor RADIUS (Remote Authentication Dial-In User Service), como um servidor que executa o Servidor de Políticas de Rede, tem de definir o Nome Alternativo do Requerente como Nome Principal de Utilizador.  

    -   **Selecionar certificados de raiz para validação do servidor**: Se o servidor que o dispositivo estabelece ligação utilizar um certificado de autenticação de servidor que o dispositivo não considera fidedigno, selecione o perfil de certificado que contém o certificado de raiz para o certificado de servidor, para criar uma cadeia de fidedignidade de certificados no dispositivo.  

    -   **Selecione um certificado de cliente para autenticação de cliente**: Se o servidor ou dispositivo de rede requer um certificado de cliente para autenticar o dispositivo de ligação, selecione o perfil de certificado que contém o certificado de autenticação de cliente.  

    > [!NOTE]  
    >  Antes de poder selecionar o certificado de raiz e o certificado de cliente, tem primeiro de os configurar e implementar como um perfil de certificado. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](introduction-to-certificate-profiles.md).  

7.  No **definições avançadas** página, especifique as definições avançadas para o perfil de Wi-Fi, como o modo de autenticação, as opções de início de sessão único e compatibilidade Federal Information Processing Standards. Para obter mais informações sobre estas opções, consulte a documentação do Windows. As definições avançadas podem não estar disponíveis ou podem variar consoante as opções selecionadas na página **Configuração de Segurança** do assistente.  

1.  No **as definições de Proxy** página, selecione **configurar definições de proxy para este perfil de Wi-Fi** se a rede sem fios utilizar um servidor proxy e, em seguida, forneça as informações de configuração.  

2. No **plataformas suportadas** página, selecione os sistemas operativos onde pretende instalar o perfil de Wi-Fi. Em alternativa, clique em **Selecionar tudo** para instalar o perfil Wi-Fi em todos os sistemas operativos disponíveis.  

### <a name="next-steps"></a>Passos seguintes
 Para obter informações sobre como implementar o perfil Wi-Fi, veja [Como implementar perfis Wi-Fi no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
