---
title: "Implementar Wi-Fi, VPN, correio eletrónico e perfis de certificado | Documentos do Microsoft"
description: "Saiba como implementar Wi-Fi, VPN, correio eletrónico e perfis de certificado no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
caps.latest.revision: 5
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c2e3aef41e9a890d136039f85777ab07284e5c27
ms.openlocfilehash: 70372d5df13034b48f3e43b766776442f1be5823
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Implementar perfis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis devem ser implementados numa ou mais coleções para que poderem ser utilizados.  

 Utilize o **implementar perfil Wi-Fi**, **implementar perfil VPN**, **implementar perfil do Exchange ActiveSync**, ou **implementar perfil de certificado** caixa de diálogo para configurar a implementação destes perfis. Como parte da configuração, deve definir a coleção à qual o perfil deve ser implementado e especificar com que frequência o perfil é avaliado para compatibilidade.  

> [!NOTE]  
>  Se implementar vários perfis de acesso a recursos da empresa para o mesmo utilizador, ocorre o seguinte comportamento:  
>   
>  -   Se uma definição em conflito contiver um valor opcional, este não será enviado para o dispositivo.  
> -   Se uma definição em conflito contiver um valor obrigatório, o valor predefinido será enviado para o dispositivo. Se não existir um valor predefinido, todo o perfil de acesso a recursos da empresa irá falhar. Por exemplo, se implementar dois perfis de e-mail no mesmo utilizador e os valores especificados para **Anfitrião do Exchange ActiveSync** ou **Endereço de e-mail** forem diferentes, ambos os perfis de e-mail irão falhar, uma vez que são definições obrigatórias.  

> -   Para poder implementar perfis de certificado, primeiro é necessário configurar a infraestrutura e criar perfis de certificado. Para obter mais informações, consulte os tópicos seguintes:  
>   
>  -   [Configurar a infraestrutura de certificados no System Center Configuration Manager](certificate-infrastructure.md)  
> -   [Como criar perfis de certificado no System Center Configuration Manager](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  Quando uma implementação do perfil VPN é removida, não é removido dos dispositivos cliente. Se pretender remover o perfil dos dispositivos, tem de removê-lo manualmente.
>   

## <a name="deploying--profiles"></a>Implementação de perfis  


1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.  

2.  No **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**, expanda **acesso a recursos da empresa**e, em seguida, selecione o tipo de perfil apropriado, tal como **perfis Wi-Fi**.  

3.  Na lista de perfis, selecione o perfil que pretende implementar, e, em seguida, no **base** separador o **implementação** grupo, clique em **implementar**.  

4.  Na caixa de diálogo de perfil a implementar, especifique as seguintes informações:  

    -   **Recolha** -clique em **procurar** para selecionar a coleção onde pretende implementar o perfil.  

    -   **Gerar um alerta** -ative esta opção para configurar um alerta que é gerado se a compatibilidade do perfil for inferior a uma percentagem especificada até uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

    -   -   **Atraso aleatório (horas)**: (Apenas para perfis de certificado que contêm as definições de Simple Certificate Enrollment Protocol) Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é **64** horas.  

    -   **Especifique o agendamento de avaliação de compatibilidade para este <type> perfil** -especifique o agendamento através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado.  

        > [!NOTE]  
        >  O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.  

5.  Clique em **OK** para fechar a caixa de diálogo e para criar a implementação.

### <a name="see-also"></a>Consulte também  

[Como monitorizar Wi-Fi, VPN e perfis de e-mail no System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md)

[Como monitorizar perfis de certificado no System Center Configuration Manager](monitor-certificate-profiles.md)

