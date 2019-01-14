---
title: Acesso condicional com o cogestão
titleSuffix: Configuration Manager
description: Controlar o acesso de utilizador aos recursos organizacionais com base nas regras de conformidade do Intune
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f4cb468e7412167acd6d0242b49c8b0bf72ecae
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54251186"
---
# <a name="conditional-access-with-co-management"></a>Acesso condicional com o cogestão

Acesso condicional certifica-se de que apenas os utilizadores fidedignos podem aceder a recursos organizacionais em dispositivos fidedignos com aplicativos confiáveis. É criada a partir do zero na cloud. Se estiver a gerir dispositivos com o Intune ou expandir a sua implementação do Configuration Manager com cogestão, ele funciona da mesma forma.

No vídeo seguinte, gerente de programas sênior Joey Glocke e marketing Ainley Locky do Gestor de produtos, discutem e demonstrar o acesso condicional com o cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Com a cogestão, o Intune avalia todos os dispositivos na sua rede para determinar como confiável é. Ele faz essa avaliação das seguintes duas formas:

1. Intune torna-se de que um dispositivo ou aplicação é gerida e configurada de forma segura. Esta verificação depende de como definir políticas de conformidade da sua organização. Por exemplo, certifique-se de que todos os dispositivos tem a encriptação ativada e não estão desbloqueados por jailbreak.  

    - Essa avaliação é a violação de segurança anteriores e com a base de configuração  

    - Para dispositivos cogeridos, o Configuration Manager também faz com a base de configuração de avaliação. Por exemplo, exigia a conformidade de atualizações ou aplicações. Intune combina essa avaliação juntamente com sua própria avaliação.  

2. Intune Deteta incidentes de segurança do Active Directory num dispositivo. Ele usa a segurança inteligente da [a proteção de ameaças avançada do Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) e outras [fornecedores de defesa contra ameaças móveis](https://www.lookout.com/about/partners/microsoft). Estes parceiros executam análise comportamental em curso nos dispositivos. Esta análise Deteta incidentes activos e, em seguida, passa essas informações para o Intune para avaliação de conformidade em tempo real.  

    - Essa avaliação é pós-segurança falha e com base em incidentes  

Microsoft vice-presidente Brad Anderson discute o acesso condicional em profundidade com demonstrações ao vivo durante a apresentação do Ignite de 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Acesso condicional também fornece um local centralizado para ver o estado de funcionamento de todos os dispositivos ligados à rede. Obter as vantagens de escala da cloud, que é especialmente útil para as instâncias de produção do teste do Configuration Manager.


## <a name="benefits"></a>Benefícios

Cada equipe de TI é obsessão com segurança de rede. É obrigatório certificar-se de que cada dispositivo cumpre os requisitos de segurança e empresariais antes de aceder a sua rede. Com o acesso condicional, é possível determinar os seguintes fatores: 
- Se todos os dispositivos são encriptados  
- Se o software maligno é instalado  
- Se as respetivas definições são atualizadas  
- Se ele foi desbloqueado por jailbreak ou Root  

Acesso condicional combina um controle granular sobre dados organizacionais com uma experiência de usuário que maximize a produtividade de trabalho em qualquer dispositivo a partir de qualquer local.

O seguinte vídeo mostra como [proteção avançada de Thread](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) está integrado em cenários comuns que ocorrem regularmente:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Com a cogestão, o Intune pode incorporar responsabilidades do Configuration Manager para avaliar a conformidade de padrões de segurança das aplicações ou atualizações necessárias. Este comportamento é importante para qualquer organização de TI que deseja continuar a utilizar o Configuration Manager para aplicações complexas e gerenciamento de patches.

Acesso condicional também é uma parte crucial do desenvolvimento de sua [rede de confiança de Zero](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) arquitetura. Com o acesso condicional, os controlos de acesso de dispositivo em conformidade abrangem as camadas de base da rede de confiança do Zero. Esta funcionalidade é uma grande parte de como proteger a sua organização no futuro.

Para obter mais informações, consulte o postagem no blog sobre [melhorar o acesso condicional com os dados de risco do computador da proteção de ameaças avançada do Windows Defender](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Estudos de caso

A TI Wipro empresa de consultoria usa o acesso condicional para proteger e gerir os dispositivos utilizados por todos os 91,000 funcionários. Num estudo de caso recente, o vice-presidente de IT em Wipro indicado:

> *Obtenção de acesso condicional é uma grande vitória para Wipro. Agora, todos os nossos funcionários tenham acesso móvel a informações sob demanda. * 
>  *Aperfeiçoamos nossa produtividade de postura e funcionários de segurança. Agora 91,000 funcionários beneficiam altamente proteger o acesso a mais de 100 aplicações a partir de qualquer dispositivo, em qualquer lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Outros exemplos incluem: 

- Nestle, que utiliza o acesso condicional com base na aplicação para mais de 150 000 funcionários  

- A empresa de software de automatização, cadência, que agora pode certificar-se de que "apenas os dispositivos geridos têm acesso a aplicações do Office 365, como as Equipes e da intranet da empresa". Também podem oferecer sua força de trabalho "acesso mais seguro para outras aplicações com base na cloud, como o Salesforce e o Workday." Para obter mais informações sobre a experiência da cadência com o Intune, consulte [cadência aumenta o ritmo das empresas com ferramentas de colaboração móveis no Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune é também totalmente integrado com parceiros tais como Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Com estes parceiros, pode manter os controlos de acesso com base na inscrição do Intune e o estado de conformidade do dispositivo entre essas outras plataformas.

Para obter mais informações, veja os vídeos seguintes:
- [Acesso condicional do demonstrações de Brad Anderson em detalhes](https://youtu.be/8321obNofgM?t=547)  
- [Detalhes adicionais do ponto final de zona 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposta de valor

Com acesso condicional e integração de ATP, estiver fortifying um componente fundamental de cada organização de TI: proteger o acesso a cloud.

Em mais de 63% de todas as violações de dados, os invasores obtém acesso à rede da organização através de credenciais de utilizador fracas, padrão ou roubado. Porque o acesso condicional se foca em proteger a identidade do utilizador, restringe o roubo de credenciais. Acesso condicional gerencia e protege as identidades privilegiadas ou sem privilégios. Não há nenhuma maneira melhor de proteger os dispositivos e os dados nas mesmas.

Como o acesso condicional é um componente fundamental do Enterprise Mobility + Security (EMS), não existe nenhuma configuração no local ou arquitetura necessária. Com o Intune e Azure Active Directory (Azure AD), pode configurar rapidamente o acesso condicional na cloud. Se estiver a utilizar atualmente o Configuration Manager, pode facilmente estender seu ambiente na cloud com a cogestão e começar a usá-lo neste momento.

Para obter mais informações sobre a integração do ATP, veja esta mensagem de blogue [pontuação de risco do dispositivo do Windows Defender ATP expõe cyberattack novo, unidades de acesso condicional para proteger redes](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Ele detalha como um grupo de hacker avançadas utilizado nunca antes vistas ferramentas. A cloud da Microsoft detetado e parada-los uma vez que os utilizadores visados tinham acesso condicional. A intrusões ativado a política de acesso condicional baseado no risco do dispositivo. Embora o invasor já estabelecer sua posição na rede, as máquinas exploradas foram automaticamente restringidas de acesso aos serviços organizacionais e de dados geridos pelo Azure AD.



## <a name="configure"></a>Configurar

Acesso condicional é fácil de usar quando [ativar a cogestão](/sccm/comanage/how-to-enable). Exige a retirada da **políticas de conformidade** carga de trabalho para o Intune. Para obter mais informações, consulte [como mudar cargas de trabalho do Configuration Manager para o Intune](/sccm/comanage/how-to-switch-workloads). 

Para obter mais informações sobre como utilizar o acesso condicional, consulte os artigos seguintes: 

- [Acesso condicional no Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Políticas de conformidade de dispositivos do Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Acesso condicional com base na aplicação com o Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Funcionalidades de acesso condicional ficam disponíveis imediatamente para híbrido do Azure dispositivos associados ao AD. Estas funcionalidades incluem autenticação multifator e híbrida o controlo de acesso de associação do Azure AD. Este comportamento acontece porque eles são baseadas nas propriedades do Azure AD. Para aproveitar baseadas na configuração de avaliação do Intune e Configuration Manager, ative a cogestão. Essa configuração fornece, controlo de acesso diretamente a partir do Intune para dispositivos em conformidade. Ele também fornece recursos de avaliação de políticas de conformidade do Intune.  

