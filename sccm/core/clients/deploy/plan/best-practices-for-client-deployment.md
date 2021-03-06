---
title: Práticas recomendadas de implantação de cliente
titleSuffix: Configuration Manager
description: Obtenha melhores práticas para implementação do cliente no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3f5be163775e667571d97ef8a9d417ce6256b2d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122003"
---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Melhores práticas para a implementação do cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilizar a instalação de cliente baseada em atualização de software para computadores do Active Directory  
 Este método de implementação do cliente usa tecnologias existentes do Windows, integra-se com sua infraestrutura de Active Directory, requer o mínimo de configuração no Configuration Manager, é o mais fácil a configuração de firewalls e é a mais segura. Ao utilizar grupos de segurança e filtragem WMI para a configuração de diretiva de grupo, tem também uma grande flexibilidade para controlar quais os computadores que instalar o cliente do Configuration Manager.  

 Para obter mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando a Instalação Baseada em Atualizações de Software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Expandir o esquema do Active Directory e publicar o site para que possa executar o CCMSetup sem opções da linha de comandos  
 Quando expande o esquema do Active Directory para o Configuration Manager e o site é publicado para serviços de domínio do Active Directory, muitas propriedades de instalação de cliente são publicadas para serviços de domínio do Active Directory. Se um computador conseguir localizar estas propriedades de instalação do cliente, pode utilizá-los durante a implementação de cliente do Configuration Manager. Como estas informações são geradas automaticamente, o risco de erro humano associado à introdução manual das propriedades de instalação é eliminado.  

 Para obter mais informações, veja [Acerca das propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Utilizar uma implementação faseada para gerir a utilização da CPU  
 Minimize o efeito dos requisitos de processamento da CPU no servidor do site utilizando uma implementação faseada dos clientes. Implemente clientes fora do horário comercial para que outros serviços tenham a largura de banda mais disponível durante o dia e os utilizadores não são interrompidos se seus computadores ficarem lentos ou ser reiniciado.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Ativar a atualização automática após a conclusão da implementação principal do cliente  
 [Atualizações automáticas de clientes](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) são úteis quando quiser atualizar um pequeno número de computadores cliente que possa ter falhado por seu método de instalação principal do cliente, talvez porque eram offline. 

> [!NOTE]  
>  Melhorias de desempenho no Configuration Manager poderão permitir a utilização de atualizações automáticas como método de atualização principal do cliente. No entanto, o desempenho dependerá da infraestrutura da hierarquia, como por exemplo o número de clientes.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilizar SMSMP e FSP se instalar o cliente com propriedades client.msi  
 A propriedade SMSMP especifica o ponto de gestão inicial com que o cliente deverá comunicar, removendo a dependência de soluções de localização de serviços tais como os Serviços de Domínio do Active Directory, DNS e WINS.  

 Utilize a propriedade FSP e instale um ponto de estado de contingência para que possa monitorizar a instalação e atribuição de clientes e identificar eventuais problemas de comunicação.  

 Para obter mais informações sobre estas opções, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Instalar pacotes de idiomas de cliente antes de instalar os clientes  
Recomendamos que instale os pacotes de idiomas de cliente antes de implementar o cliente. Se instalar [pacotes de idiomas de cliente](../../../../core/servers/deploy/install/language-packs.md) (para habilitar os idiomas adicionais) num site depois de instalar clientes, tem de reinstalar os clientes antes de poderem utilizar esses idiomas. Para clientes de dispositivos móveis, tem de apagar o dispositivo móvel e inscrevê-lo novamente.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Preparar antecipadamente os certificados PKI necessários  
 Para gerir dispositivos na Internet, dispositivos móveis inscritos e computadores Mac, terá de possuir certificados PKI nos sistemas de sites (pontos de gestão e pontos de distribuição) e nos dispositivos cliente. Em redes em ambiente de produção, poderá ser necessário solicitar a aprovação da gestão de alterações para utilizar novos certificados, reiniciar os servidores do sistema de sites ou os utilizadores poderão ter de terminar e reiniciar sessão para a nova associação a grupo. Além disso, poderá ter que permitir tempo suficiente para a replicação das permissões de segurança e eventuais novos modelos de certificado.  

 Para obter mais informações sobre certificados PKI necessários, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Antes de instalar os clientes, configure todas as definições de cliente e janelas de manutenção necessárias  
 Embora possa [configurar definições de cliente](../../../../core/clients/deploy/configure-client-settings.md) e janelas de manutenção antes ou depois dos clientes são instalados, é melhor configurar definições necessárias antes de instalar clientes, para que eles são usados quando a instalação do cliente. 

 Configure janelas de manutenção para servidores e para dispositivos Windows Embedded garantir a continuidade do negócio para dispositivos fundamentais. Janelas de manutenção irão garantir que atualizações de software necessárias e o antimalware software não reiniciar o computador durante o horário comercial.  

> [!IMPORTANT]  
>  Para os computadores com o Windows 10 que pretende proteger com o Filtro de Escrita Unificado (UWF), deve configurar o dispositivo para UWF antes de instalar o cliente. Isto permite que o Configuration Manager para instalar o cliente com um provedor de credenciais personalizadas que bloqueia os utilizadores com direitos restritos de iniciar sessão no dispositivo durante o modo de manutenção.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planeie a sua experiência de inscrição de utilizador para computadores Mac e dispositivos móveis   
 Se os utilizadores inscreverem os seus próprios computadores Mac e dispositivos móveis com o Configuration Manager, planeie a experiência do usuário. Por exemplo, poderá criar um script de instalação e o processo de inscrição utilizando uma página da web para que os utilizadores introduzam um mínimo de informações necessárias e enviar instruções com uma ligação por e-mail.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Utilizar dispositivos baseados em ficheiros escrever filtros para Windows Embedded 
 É provável que ocorram ressincronizações de mensagens de estado em dispositivos incorporados que utilizem Filtros de Escrita Avançados (EWF). Se tiver apenas alguns dispositivos incorporados que utilizem Filtros de Escrita Avançados, poderá não reparar nesta questão. No entanto, se tiver muitos dispositivos incorporados que ressincronizem as respetivas informações, enviando por exemplo inventários completos em vez de alterações ao inventário, isso poderá gerar um aumento notório dos pacotes de rede e um processamento superior na CPU do servidor do site.  

 Se puder escolher o tipo de filtro de escrita para ativar, escolha filtros de escrita baseados em ficheiros e configure exceções para manter o estado do cliente e dados de inventário entre reinícios do dispositivo para a rede e a eficiência da CPU no cliente do Configuration Manager. Para obter mais informações sobre os filtros de escrita, veja   [Planear a implementação do cliente em dispositivos Windows Embedded no System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Para mais informações sobre o número máximo de clientes Windows Embedded suportado por um site primário, veja [Sistemas operativos suportados por clientes e dispositivos](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
