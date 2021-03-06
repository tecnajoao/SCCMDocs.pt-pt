---
title: Introdução aos perfis de certificado
titleSuffix: Configuration Manager
description: Saiba como funcionam os perfis de certificado no System Center Configuration Manager com os serviços de certificados do Active Directory.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5872a6a8ee69e50d0abfe5840a087aaf83ab7aa5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156615"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de certificado no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Perfis de certificado trabalham com os serviços de certificados do Active Directory e a função de serviço de inscrição de dispositivos de rede (NDES). Criar e implementar certificados de autenticação para dispositivos geridos para que os usuários podem facilmente acessar recursos da empresa. Por exemplo, pode criar e implementar perfis de certificado para fornecer os certificados necessários para os usuários se conectem a VPN e conexões sem fio.

Perfis de certificado podem configurar automaticamente os dispositivos dos utilizadores. Os utilizadores aceder a recursos da empresa, tais como redes Wi-Fi e servidores VPN sem instalar certificados manualmente ou através de um processo fora de banda. Certificado de perfis de ajudam a manter os recursos da empresa seguro porque pode usar as configurações mais seguras que são suportadas pela sua empresa infraestrutura de chaves públicas (PKI). Por exemplo, exigir autenticação de servidor para todas as ligações de VPN e Wi-Fi porque implementar os certificados necessários nos dispositivos geridos.   

Perfis de certificado fornecem as seguintes capacidades de gestão:  

-   Inscrição de certificados e renovação de uma autoridade de certificação (AC) empresarial para dispositivos que executam o iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Estes certificados, em seguida, podem ser utilizados para ligações Wi-Fi e VPN.  

-   Implementação de certificados de AC de raiz fidedigna e certificados de AC intermediária. Estes certificados configurar uma cadeia de fidedignidade em dispositivos para ligações VPN e Wi-Fi quando é necessária a autenticação de servidor.  

-   Monitorização e criação de relatórios sobre os certificados instalados.  

**Example:** Todos os funcionários tem de conseguir estabelecer ligação a hotspots Wi-Fi em várias localizações empresariais. Para ativar a ligação de utilizador fácil, primeiro implemente os certificados necessários para ligar ao Wi-Fi. Em seguida, implemente perfis de Wi-Fi que referenciam o certificado.  

**Example:** Tem um PKI ativo. Pretende mover para um método mais flexível e seguro de implementação de certificados. Os utilizadores devem ser capazes de aceder a recursos da empresa dos respetivos dispositivos pessoais sem comprometer a segurança. Configure perfis de certificado com definições e protocolos que são suportados para a plataforma de dispositivo específico. Os dispositivos podem, então, pedir estes certificados automaticamente a partir de um servidor de inscrição com acesso à Internet. Em seguida, configure perfis VPN para utilizar estes certificados, para que o dispositivo pode aceder aos recursos da empresa.  



## <a name="types-of-certificate-profiles"></a>Tipos de perfis de certificado  
 Existem três tipos de perfis de certificado:  

-   **Certificado de AC fidedigna** -implementar uma AC de raiz fidedigna ou certificado da AC intermediária. Estes certificados formam uma cadeia de confiança quando o dispositivo tiver de autenticar um servidor.  

-   **Protocolo de inscrição de certificado simples (SCEP)** -pedir um certificado para um dispositivo ou utilizador utilizando o protocolo SCEP. Este tipo requer a função de serviço de inscrição de dispositivos de rede (NDES) num servidor com o Windows Server 2012 R2 ou posterior.

    Para criar uma **protocolo simples de inscrição de certificados (SCEP)** perfil de certificado, primeiro crie um **certificado da AC fidedigna** perfil.

-   **Troca de informações pessoais (. pfx)** -pedir um certificado. pfx (também conhecido como PKCS #12) para um dispositivo ou utilizador.<!--1321368-->  

    Pode criar perfis de certificado PFX pela [importar as credenciais](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) de certificados existentes ou pelo [definindo um certificado](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) autoridade para processar pedidos.

    > [!Note]  
    > O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    A partir da versão 1706, pode utilizar o Microsoft ou da Entrust como autoridades de certificação para **troca de informações pessoais (. pfx)** certificados.


## <a name="requirements-and-supported-platforms"></a>Requisitos e plataformas suportadas  
Para implementar perfis de certificado que utilizem SCEP, instale o ponto de registo de certificados num servidor de sistema de sites. Também instalar um módulo de política para o NDES, o módulo de política do Configuration Manager, num servidor que executa o Windows Server 2012 R2 ou posterior. Este servidor requer a função de serviços de certificados do Active Directory e um trabalho NDES que seja acessível aos dispositivos que necessitam dos certificados. Para os dispositivos que são inscritos pelo Microsoft Intune, o NDES tem de ser acessível a partir da Internet. Por exemplo, numa sub-rede filtrada, também conhecido como uma rede de Perímetro.  

Os certificados PFX também requerem um ponto de registo de certificados. Especifique também a autoridade de certificação (AC) para o certificado e as credenciais de acesso relevantes. A partir da versão 1706, pode especificar Microsoft ou Entrust como autoridades de certificação.  

Para obter mais informações sobre como o serviço de inscrição de dispositivos de rede suporta um módulo de política para que o Configuration Manager possa implementar certificados, consulte [usando um módulo de política com o serviço de inscrição de dispositivos de rede](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Consoante os requisitos, o Configuration Manager suporta implementar certificados para vários arquivos de certificados em vários tipos de dispositivos e sistemas operacionais. São suportados os seguintes dispositivos e sistemas operativos:  

-   Windows RT 8.1  

-   Windows 8,1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implementar perfis para Android, iOS, Windows Phone e dispositivos Windows 8.1 ou posterior inscritos, estes dispositivos têm de ser [inscritos no Microsoft Intune](/intune/device-enrollment).   

Um cenário típico para o Configuration Manager é instalar certificados de AC de raiz fidedigna para autenticar Wi-Fi e servidores VPN, quando a conexão usa o EAP-TLS, EAP-TTLS e protocolos de autenticação do PEAP e IKEv2, L2TP/IPSec e túnel de VPN do Cisco IPsec protocolos.  

Um certificado de AC de raiz empresarial tem de ser instalado no dispositivo antes do dispositivo pode solicitar certificados utilizando um perfil de certificado SCEP.  

Pode especificar as definições num perfil de certificado SCEP para solicitar certificados personalizados para vários ambientes ou requisitos de conectividade. O **Create Certificate Profile Wizard** tem duas páginas de parâmetros de inscrição. A primeira **inscrição SCEP**, inclui definições para o pedido de inscrição e a localização para instalar o certificado. A segunda, **Propriedades do Certificado**, descreve o certificado pedido.  

## <a name="deploying-certificate-profiles"></a>Implementar perfis de certificado  
 Quando implementa um perfil de certificado, os ficheiros de certificado no perfil são instalados em dispositivos cliente. Quaisquer parâmetros SCEP também são implementados e os pedidos de SCEP são processados no dispositivo cliente. Pode implementar perfis de certificado para o utilizador ou coleções de dispositivos e especificar o arquivo de destino para cada certificado. As regras de aplicabilidade determinam se os certificados podem ser instalados no dispositivo. Quando os perfis de certificado são implementados em coleções de utilizadores, a afinidade dispositivo / utilizador determina que os dispositivos dos utilizadores a instalar os certificados. Quando os perfis de certificado que incluem certificados de utilizador são implementados para coleções de dispositivos, por predefinição, os certificados são instalados em todos os dispositivos dos utilizadores primários. Pode alterar este comportamento para instalar o certificado em qualquer um dos dispositivos dos utilizadores no **inscrição SCEP** página do **Create Certificate Profile Wizard**. Se os dispositivos forem computadores de grupo de trabalho, os certificados de utilizador não são implementados.  

## <a name="monitoring-certificate-profiles"></a>Monitorizar perfis de certificado  

Pode monitorizar implementações de perfis de certificado através da visualização dos resultados de compatibilidade ou de relatórios. Estas abordagens são descritas nas [como monitorizar perfis de certificado](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revogação automática de certificados  
 System Center Configuration Manager revoga automaticamente os certificados de utilizador e computador implementados através da utilização de perfis de certificado nas seguintes circunstâncias:  

- O dispositivo é retirado da gestão do System Center Configuration Manager.  

- O dispositivo é apagado seletivamente.  

- O dispositivo está bloqueado na hierarquia do System Center Configuration Manager.  

  Para revogar os certificados, o servidor do site envia um comando de revogação à autoridade de certificação emissora. O motivo da revogação é **Cessar a Operação**.  
