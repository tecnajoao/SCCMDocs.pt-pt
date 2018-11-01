---
title: Gerenciamento de conteúdo de segurança e privacidade
titleSuffix: Configuration Manager
description: Otimize a segurança e privacidade para gestão de conteúdos no Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f24760e11dd3972c43600225eec405523988696c
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411070"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Segurança e privacidade para gestão de conteúdos no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo contém informações de privacidade para gestão de conteúdos no Configuration Manager e de segurança. 



##  <a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gestão de conteúdo  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Vantagens e desvantagens de HTTPS ou HTTP para pontos de distribuição de intranet
Para pontos de distribuição na intranet, considere as vantagens e desvantagens da utilização de HTTPS e HTTP. Na maioria dos cenários, a utilização de HTTP e o pacote de contas de acesso para autorização proporciona mais segurança do que através de HTTPS com encriptação, mas sem autorização. No entanto, se o conteúdo incluir dados confidenciais que pretende encriptar durante a transferência, utilize o HTTPS.  

-   **Se utilizar o HTTPS para um ponto de distribuição**, o Configuration Manager não utiliza contas de acesso de pacotes para autorizar o acesso ao conteúdo, mas o conteúdo é encriptado quando é transferido através da rede.  

-   **Se utilizar HTTP para um ponto de distribuição**, pode utilizar contas de acesso de pacotes para autorização, mas o conteúdo não é encriptado quando é transferido através da rede.  

A partir da versão 1806, considere ativar **avançada HTTP** para o site. Esta funcionalidade permite que os clientes utilizar a autenticação do Azure Active Directory para comunicar de forma segura com um ponto de distribuição de HTTP. Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).

#### <a name="protect-the-client-authentication-certificate-file"></a>Proteger o ficheiro de certificado de autenticação de cliente
Se utilizar um certificado de autenticação de cliente PKI em vez de um certificado autoassinado para o ponto de distribuição, proteja o ficheiro de certificado (. pfx) com uma palavra-passe segura. Se armazenar o ficheiro na rede, proteja o canal de rede quando importar o ficheiro para o Configuration Manager.

Quando precisar de uma palavra-passe para importar o certificado de autenticação de cliente que o ponto de distribuição utiliza para comunicar com pontos de gestão, esta configuração ajuda a proteger o certificado de um atacante. Utilize a assinatura de bloco de mensagem de servidor (SMB) ou IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere o ficheiro de certificado.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Remover a função de ponto de distribuição do servidor do site
Por predefinição, a configuração do Configuration Manager instala um ponto de distribuição no servidor do site. Os clientes não precisem de comunicar diretamente com o servidor do site. Para reduzir a superfície de ataque, atribua a função de ponto de distribuição a outros sistemas de sites e removê-lo ao servidor do site.  

#### <a name="secure-content-at-the-package-access-level"></a>Proteja o conteúdo no nível de acesso do pacote
O compartilhamento do ponto de distribuição permite o acesso de leitura a todos os utilizadores. Para restringir os utilizadores que podem aceder ao conteúdo, utilize contas de acesso aos pacotes quando o ponto de distribuição estiver configurado para HTTP. Esta configuração não se aplica a pontos de distribuição de nuvem, que não suportam contas de acesso de pacotes. Para obter mais informações, consulte [contas de acesso a pacote](/sccm/core/plan-design/hierarchy/accounts#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configurar o IIS na função do ponto de distribuição
Se o Configuration Manager instala o IIS quando adicionar uma função de sistema de sites de ponto de distribuição, remova o redirecionamento de HTTP ou Scripts de gestão do IIS e ferramentas de quando a instalação do ponto de distribuição estiver concluída. O ponto de distribuição não precisa de redirecionamento de HTTP ou ferramentas e Scripts de gestão do IIS. Para reduzir a superfície de ataque, remova estes serviços de função para a função de servidor web.  Para obter mais informações sobre os serviços de função para a função de servidor web para pontos de distribuição, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Definir as permissões de acesso do pacote quando criar o pacote
Uma vez que as alterações às contas de acesso nos ficheiros do pacote entram em vigor apenas quando redistribuir o pacote, defina cuidadosamente as pacote permissões de acesso quando cria o pacote pela primeira vez. Esta configuração é importante quando o pacote é grande ou distribuído por muitos pontos de distribuição e quando a capacidade de largura de banda de rede para a distribuição de conteúdo é limitada.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementar controlos de acesso para proteger os suportes de dados que contêm conteúdo pré-configurado
Conteúdo pré-configurado está comprimido, mas não encriptado. Um intruso poderia ler e modificar os ficheiros que são transferidos para dispositivos. Clientes do Configuration Manager rejeitam conteúdo adulterado, mas ainda o transferem.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importe o conteúdo pré-configurado com ExtractContent
Importar apenas o conteúdo pré-configurado utilizando a ferramenta de linha de comando ExtractContent.exe. Para evitar a adulteração e a elevação de privilégios, utilize apenas a linha de comandos ferramenta autorizada fornecida com o Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Proteja o canal de comunicação entre o servidor do site e a localização de origem do pacote
Utilize IPsec ou assinatura SMB entre o servidor de site e a localização de origem do pacote quando criar aplicações e pacotes. Esta configuração ajuda a impedir que um atacante adultere os ficheiros de origem.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Remova os diretórios virtuais predefinidos para o Web site personalizado com a função de ponto de distribuição
Se alterar a opção de configuração de site para utilizar um Web site personalizado em vez de Web site predefinido depois de instalar uma função de ponto de distribuição, remova os diretórios virtuais predefinidos. Quando mudar do Web site predefinido para um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Remova os seguintes diretórios virtuais do Configuration Manager criado originalmente sob o Web site predefinido:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Para pontos de distribuição de nuvem, proteja os detalhes da subscrição do Azure e certificados
Quando utiliza pontos de distribuição de nuvem, proteja os seguintes itens de alto valor:
- O nome de utilizador e palavra-passe para a sua subscrição do Azure
- O certificado de gestão do Azure 
- O certificado de serviço do ponto de distribuição em nuvem

Store os certificados de forma segura. Se navegar até-los através da rede quando configurar o ponto de distribuição de nuvem, utilize IPsec ou assinatura SMB entre o servidor de sistema de sites e a localização de origem.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Para continuidade do serviço, monitorize a data de expiração dos certificados de ponto de distribuição na cloud
O Configuration Manager não avisa quando os certificados importados para o ponto de distribuição em nuvem estão prestes a expirar. Monitorize as datas de expiração de forma independente do Configuration Manager. Certifique-se de que renova e, em seguida, importar os novos certificados antes da data de expiração. Esta ação é importante se adquirir um certificado de autenticação de servidor de um fornecedor externo, público, pois pode necessitar de mais tempo para adquirir um certificado renovado.  

 Se um dos certificados expirar, o Gestor de serviços Cloud gera o ID de mensagem de estado **9425**. O ficheiro de Cloudmgr contém uma entrada que indica que o certificado **está no estado expirado**, com a data de expiração também registada em UTC.  



## <a name="security-considerations-for-content-management"></a>Considerações de segurança para gestão de conteúdo  

Ao planear a gestão de conteúdo, considere os seguintes pontos:  

-   Os clientes não validam o conteúdo apenas depois de ser transferido.  

     Clientes do Configuration Manager validam o hash no conteúdo apenas depois de ser transferido para a respetiva cache do cliente. Se um intruso adulterar a lista de ficheiros para transferir ou com o próprio conteúdo, o processo de transferência pode demorar até largura de banda de rede considerável, apenas para o cliente rejeite depois o conteúdo quando encontrar o hash inválido.  

-   Quando utiliza pontos de distribuição de nuvem, o acesso ao conteúdo é automaticamente restrito a sua empresa. Não pode restringi-la com utilizadores ou grupos selecionados.  

-   Quando utiliza pontos de distribuição de nuvem, os clientes são autenticados pelo ponto de gestão e, em seguida, utilizam um token do Configuration Manager para aceder a pontos de distribuição de nuvem. O token é válido para oito horas. Este comportamento significa que se bloquear um cliente porque ele já não é fidedigno, pode continuar a transferir conteúdo de um ponto de distribuição de nuvem, até que o período de validade do token expirou. Neste momento, o ponto de gestão não emitirá outro token para o cliente, porque o cliente está bloqueado.  

     Para evitar um cliente bloqueado Transfira conteúdo durante esse período de oito horas, pare o serviço em nuvem. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **pontos de distribuição de nuvem** nó.  



##  <a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade da gestão de conteúdo  

 O Configuration Manager não inclui quaisquer dados de utilizador nos ficheiros de conteúdo, embora um utilizador administrativo possa optar por efetuar esta ação.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  

- [Segurança e privacidade para gestão de aplicações](/sccm/apps/plan-design/security-and-privacy-for-application-management)  

- [Segurança e privacidade para atualizações de software](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

- [Segurança e privacidade para implementação do SO](/sccm/osd/plan-design/security-and-privacy-for-operating-system-deployment)  