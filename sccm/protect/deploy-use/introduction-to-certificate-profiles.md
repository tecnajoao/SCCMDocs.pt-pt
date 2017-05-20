---
title: "Introdução aos perfis de certificado | Documentos do Microsoft"
description: "Saiba como os perfis de certificado no System Center Configuration Manager trabalhar com serviços de certificados do Active Directory."
ms.custom: na
ms.date: 03/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: aa8924a013ebdbee888cab33001fddbe7ad2d67e
ms.openlocfilehash: 1864f814152233d3c67bd83a96623e4a6e051569
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de certificado no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Perfis de certificado funcionam com o serviços de certificados do Active Directory e a função de serviço de inscrição de dispositivos de rede para aprovisionar certificados de autenticação para dispositivos geridos para que os utilizadores forma totalmente integrada podem aceder a recursos da empresa. Por exemplo, pode criar e implementar perfis de certificado para fornecer os certificados necessários para que os utilizadores iniciem as ligações VPN e sem fios. 

Os perfis de certificado podem configurar automaticamente dispositivos de utilizadores para que seja possível aceder aos recursos da empresa, como redes Wi-Fi e servidores VPN, sem necessidade de instalar certificados manualmente ou utilizar um processo fora da banda. Além disso, os perfis de certificado ajudam a manter protegidos os recursos da empresa, na medida em que pode utilizar definições mais seguras que são suportadas pela infraestrutura de chaves públicas (PKI) da sua empresa. Por exemplo, pode requerer a autenticação de servidor para todas as ligações VPN e Wi-Fi porque aprovisionou os certificados necessários nos dispositivos geridos.   

Perfis de certificado fornecem as seguintes capacidades de gestão:  

-   Inscrição e renovação de certificados de uma autoridade de certificação (AC) empresarial para dispositivos que executam o iOS, Windows 8.1, Windows RT 8.1, o ambiente de trabalho do Windows 10 e Mobile e Android. Estes certificados podem ser utilizados para ligações VPN e Wi-Fi.  

-   Implementação de certificados de AC de raiz fidedigna e de certificados de AC intermediária para configurar uma cadeia de fidedignidade em dispositivos para ligações VPN e Wi-Fi quando é necessária a autenticação de servidor.  

-   Monitorização e criação de relatórios sobre os certificados instalados.  

**Exemplo:** Todos os funcionários têm de conseguir ligar a hotspots Wi-Fi em várias localizações empresariais. Implementar os certificados necessários para estabelecer ligação ao Wi-Fi e implementar perfis de Wi-Fi que referenciam o certificado para ativar a ligação de utilizador totalmente integrada.  

**Exemplo:** Tem uma PKI no local e pretender mover para um método mais flexível, seguro de aprovisionamento de certificados de que esta definição permite aos utilizadores aceder aos recursos da empresa dos seus dispositivos pessoais sem comprometer a segurança. Configure perfis de certificado com definições e protocolos que são suportados para a plataforma específica do dispositivo. Os dispositivos podem, então, pedir estes certificados automaticamente a partir de um servidor de inscrição com acesso à Internet. Em seguida, configure perfis da VPN para utilizar estes certificados, de modo a que o dispositivo possa aceder aos recursos da empresa.  

## <a name="types-of-certificate-profiles"></a>Tipos de perfis de certificado  
 Existem três tipos de perfis de certificado:  

-   **Certificado de AC fidedigna** -permite-lhe implementar uma AC de raiz fidedigna ou certificado da AC intermediária para formar uma cadeia de fidedignidade de certificados quando o dispositivo tem de ser autenticado num servidor.  

-   **Certificado de inscrição de protocolo SCEP (Simple)** -permite-lhe solicitar um certificado para um dispositivo ou utilizador utilizando o protocolo SCEP e o serviço de inscrição de dispositivos de rede num servidor com o Windows Server 2012 R2.
-   **Exchange informações pessoais (. pfx)** -permite-lhe solicitar um certificado. pfx (também conhecido como PKCS #12) para um dispositivo ou utilizador.

    > [!NOTE]  
    >  Tem de criar um perfil de certificado do tipo **certificado da AC fidedigna** antes de poder criar um **Simple Certificate Enrollment Protocol (SCEP)** perfil de certificado.  

## <a name="requirements-and-supported-platforms"></a>Requisitos e plataformas suportadas  
 Para implementar perfis de certificado que utilizam SCEP, tem de instalar o ponto de registo de certificados num servidor de sistema do site, no site de administração central ou num site primário. Também tem de instalar um módulo de política para o NDES, o módulo de política do Configuration Manager, num servidor que executa o Windows Server 2012 R2 com a função Serviços de certificados do Active Directory e um operacional NDES que esteja acessível aos dispositivos que necessitam dos certificados. Para os dispositivos que são inscritos pelo Microsoft Intune, isto requer que o NDES ser acessível a partir da Internet, por exemplo, numa sub-rede filtrada (também conhecida como DMZ).  

 Para obter mais informações sobre como o serviço de inscrição de dispositivos de rede suporta um módulo de política para que o Configuration Manager pode implementar certificados, consulte o artigo [utilizando um módulo de política com o serviço de inscrição de dispositivos de rede](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 O Configuration Manager suporta a implementação de certificados em vários arquivos de certificados, consoante os requisitos, o tipo de dispositivo e o sistema operativo. São suportados os seguintes dispositivos e sistemas operativos:  

-   Windows RT 8.1  

-   Windows 8,1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implementar perfis para Android, iOS, Windows Phone e inscritos do Windows 8.1 e dispositivos posteriores, estes dispositivos têm de ser [inscrito no Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

Um cenário típico para o System Center Configuration Manager é instalar certificados de AC de raiz fidedigna para autenticar Wi-Fi e servidores VPN quando a ligação utiliza EAP-TLS, EAP-TTLS e protocolos de autenticação PEAP e IKEv2, L2TP/IPsec e protocolos de túnel do Cisco IPsec VPN.  

Tem de certificar-se de que está instalado um certificado de AC de raiz empresarial no dispositivo para que este possa solicitar certificados utilizando um perfil de certificado de SCEP.  

Pode especificar uma variedade de definições num perfil de certificado de SCEP para solicitar certificados personalizados para vários ambientes ou requisitos de conectividade. O **Assistente para Criar Perfil de Certificado** contém duas páginas de parâmetros de inscrição. A primeira, **Inscrição SCEP**, contém definições para o pedido de inscrição e a localização para instalação do certificado. A segunda, **Propriedades do Certificado**, descreve o certificado pedido.  

## <a name="deploying-certificate-profiles"></a>Implementar perfis de certificado  
 Quando implementa um perfil de certificado, os ficheiros de certificado no perfil são instalados em dispositivos cliente. Serão também implementados todos os parâmetros de SCEP, e os pedidos de SCEP serão processados no dispositivo cliente. Pode implementar perfis de certificado para o utilizador ou coleções de dispositivos e especificar o arquivo de destino de cada certificado. As regras de aplicabilidade determinam se os certificados podem ser instalados no dispositivo. Quando os perfis de certificado são implementados em coleções de utilizadores, a afinidade dispositivo / utilizador determina que dispositivos dos utilizadores irá instalar os certificados. Quando os perfis de certificado que contêm os certificados de utilizador são implementados em coleções de dispositivos, por predefinição, os certificados serão instalados em cada um dos dispositivos primários dos utilizadores. Pode alterar este comportamento para instalar o certificado em qualquer um dos dispositivos dos utilizadores sobre a **inscrição SCEP** página do **criar Assistente de perfil de certificado**. Além disso, os certificados de utilizador não serão implementados em dispositivos que forem computadores de grupo de trabalho.  

## <a name="monitoring-certificate-profiles"></a>Monitorizar perfis de certificado  

Pode monitorizar implementações de perfis de certificado ao visualizar os resultados de compatibilidade ou de relatórios. Estas abordagens são descritas nas [como monitorizar perfis de certificado](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revogação automática de certificados  
 System Center Configuration Manager revoga automaticamente os certificados de utilizador e computador implementados através da utilização de perfis de certificado nas seguintes circunstâncias:  

-   O dispositivo é retirado da gestão do System Center Configuration Manager.  

-   O dispositivo é apagado seletivamente.  

-   O dispositivo está bloqueado a partir da hierarquia do System Center Configuration Manager.  

 Para revogar os certificados, o servidor do site envia um comando de revogação à autoridade de certificação emissora. O motivo da revogação é **Cessar a Operação**.  
