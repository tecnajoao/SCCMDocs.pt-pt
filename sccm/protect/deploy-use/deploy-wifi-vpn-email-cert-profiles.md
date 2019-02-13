---
title: Implementar perfis Wi-Fi, VPN, de e-mail e de certificado
titleSuffix: Configuration Manager
description: Saiba como implementar o Wi-Fi, VPN, e-mail e perfis de certificado no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63b52b42a9957ed8728d0942988067fef2be6271
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129719"
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Implementar perfis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis tem de ser implementados para uma ou mais coleções para que poderem ser utilizados.  

 Utilize o **implementar perfil Wi-Fi**, **implementar perfil VPN**, **implementar perfil do Exchange ActiveSync**, ou **implementar perfil de certificado** caixa de diálogo para configurar a implementação desses perfis. Como parte da configuração, define a coleção na qual o perfil deve ser implementado e especificar a frequência com que o perfil é avaliado relativamente à conformidade.  

> [!NOTE]
>  Se implementar vários perfis de acesso a recursos da empresa para o mesmo utilizador, ocorre o seguinte comportamento:  
> 
> - Se uma definição em conflito contiver um valor opcional, este não será enviado para o dispositivo.  
>   -   Se uma definição em conflito contiver um valor obrigatório, o valor predefinido será enviado para o dispositivo. Se não existir um valor predefinido, todo o perfil de acesso a recursos da empresa irá falhar. Por exemplo, se implementar dois perfis de e-mail no mesmo utilizador e os valores especificados para **Anfitrião do Exchange ActiveSync** ou **Endereço de e-mail** forem diferentes, ambos os perfis de e-mail irão falhar, uma vez que são definições obrigatórias.  
> 
> - Para poder implementar perfis de certificado, primeiro é necessário configurar a infraestrutura e criar perfis de certificado. Para obter mais informações, consulte os tópicos seguintes:  
> 
>   -   [Configurar a infraestrutura de certificado no System Center Configuration Manager](certificate-infrastructure.md)  
> - [Como criar perfis de certificado no System Center Configuration Manager](create-certificate-profiles.md)    
> 
> [!IMPORTANT]
>  Quando uma implementação de perfil VPN é removida, não é removido dos dispositivos cliente. Se pretender remover o perfil dos dispositivos, tem de removê-lo manualmente.

## <a name="deploying--profiles"></a>Implementação de perfis  


1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**, expanda **acesso a recursos da empresa**e, em seguida, escolha o tipo de perfil adequado, como  **Perfis Wi-Fi**.  

3.  Na lista de perfis, selecione o perfil que pretende implementar, e, em seguida, no **home page** separador a **implantação** , clique em **implementar**.  

4.  Na caixa de diálogo de perfil a implementar, especifique as seguintes informações:  

    -   **Recolha** -clique em **procurar** para selecionar a coleção onde pretende implementar o perfil.  

    -   **Gerar um alerta** -ative esta opção para configurar um alerta que é gerado se a compatibilidade do perfil for inferior a uma percentagem especificada até uma data especificada e a hora. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

    -   -   **Atraso aleatório (horas)**: (Apenas para perfis de certificado que contêm as definições de Simple Certificate Enrollment Protocol) Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é **64** horas.  

    -   **Especifique a agenda de avaliação de conformidade para que isso <type> perfil** -especifique o agendamento através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado.  

        > [!NOTE]  
        >  O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.  

5.  Clique em **OK** para fechar a caixa de diálogo e criar a implementação.

### <a name="see-also"></a>Consulte também  

[Como monitorizar o Wi-Fi, VPN e perfis de e-mail no System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md)

[Como monitorizar perfis de certificado no System Center Configuration Manager](monitor-certificate-profiles.md)
