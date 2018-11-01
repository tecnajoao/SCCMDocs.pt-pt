---
title: Segurança e privacidade para implementação do SO
titleSuffix: Configuration Manager
description: Saiba mais sobre segurança e melhores práticas de privacidade para a implementação do sistema operacional no Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e2bb7992854f8743efa45f924e3d3d0718a3efe
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411396"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Segurança e privacidade para implementação do sistema operacional no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo contém informações de privacidade para a funcionalidade de implementação do sistema operacional no Configuration Manager e de segurança.  



##  <a name="bkmk_security"></a> Melhores práticas de segurança para a implementação de SO  

 Utilize as seguintes práticas recomendadas de segurança ao implementar sistemas operativos com o Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementar controlos de acesso para proteger os suportes de dados de arranque

 Ao criar suportes de dados de arranque, atribua sempre uma palavra-passe para ajudar a proteger os suportes de dados. Mesmo com uma palavra-passe, esta encripta apenas ficheiros que contêm informações confidenciais e todos os ficheiros podem ser substituídos.  

 Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente.  

 Para ajudar a impedir que um cliente instale conteúdo ou adultere a política de cliente, o conteúdo é protegido por hash e tem de ser utilizado com a política original. Se o hash de conteúdo falha ou a verificação de que o conteúdo corresponde à política, o cliente não utilizar suportes de dados. Apenas o conteúdo é protegido por hash. A política não está protegido por hash, mas é encriptada e protegida se especificar uma palavra-passe. Este comportamento torna mais difícil para um invasor modificar com êxito a política.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Utilizar uma localização segura quando criar suportes de dados para imagens do sistema operacional

 Se utilizadores não autorizados tiverem acesso à localização, eles poderão adulterar os ficheiros que criar. Também pode utilizar todo o espaço em disco disponível, para que a criação de suportes de dados falhar.  


### <a name="protect-certificate-files"></a>Proteger ficheiros de certificado 

 Protege ficheiros de certificado (. pfx) com uma palavra-passe segura. Se os armazenar na rede, proteja o canal de rede ao importá-los para o Configuration Manager

 Quando precisar de uma palavra-passe para importar o certificado de autenticação de cliente que utiliza para suportes de dados, esta configuração ajuda a proteger o certificado de um atacante.  

 Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere o ficheiro de certificado.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloquear ou revogar todos os certificados comprometidos 

 Se o certificado de cliente for comprometido, bloqueie o certificado do Configuration Manager. Se for um certificado PKI, revogue-o.  

 Para implementar um sistema operacional com suportes de dados e arranque PXE, tem de ter um certificado de autenticação de cliente com uma chave privada. Se esse certificado for comprometido, bloqueie o certificado no nó **Certificados** da área de trabalho de **Administração**, nó **Segurança**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Proteja o canal de comunicação entre o servidor de site e o fornecedor de SMS

 Quando o fornecedor de SMS é remoto do servidor do site, proteja o canal de comunicação para proteger as imagens de arranque.

 Quando modificar imagens de arranque e o fornecedor de SMS está em execução num servidor que não seja o servidor do site, as imagens de arranque estão vulneráveis a ataques. Proteja o canal de rede entre estes computadores utilizando a assinatura SMB ou IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Ativar pontos de distribuição para comunicação de cliente PXE apenas em segmentos de rede seguros

Quando um cliente envia um pedido de arranque PXE, não terá de nenhuma forma para se certificar de que a solicitação é atendida por um ponto de distribuição com PXE ativado válido. Este cenário apresenta os seguintes riscos de segurança:  

 - Um ponto de distribuição não autorizado que responda a pedidos PXE poderia fornecer uma imagem adulterada aos clientes.  

 - Um atacante poderia lançar um ataque man-in-the-middle contra o protocolo TFTP utilizado pelo PXE. Este ataque foi possível enviar código malicioso juntamente com os ficheiros de sistema operacional. O invasor também pode criar um cliente não autorizado para fazer pedidos TFTP diretamente ao ponto de distribuição.  

 - Um atacante poderia utilizar um cliente malicioso para lançar um ataque denial-of-service contra o ponto de distribuição.  

Utilize defesa em profundidade para proteger os segmentos de rede onde os clientes acedem aos pontos de distribuição com PXE ativado.  

> [!WARNING]  
>  Devido a estes riscos de segurança, não a ativar um ponto de distribuição para comunicação PXE quando estiver numa rede não fidedigna, como uma rede de perímetro.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configurar pontos de distribuição PXE ativados para responder a pedidos PXE apenas em interfaces de rede especificadas  

 Se permitir que o ponto de distribuição responda a pedidos PXE em todas as interfaces de rede, esta configuração poderá expor o serviço PXE a redes não fidedignas  


### <a name="require-a-password-to-pxe-boot"></a>Exigir uma palavra-passe para efetuar o arranque PXE

 Quando necessitar de uma palavra-passe para o arranque PXE, esta configuração adiciona um nível extra de segurança para o processo de inicialização PXE. Esta configuração ajuda a salvaguardar contra a adesão de clientes ingressar na hierarquia do Configuration Manager.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Restringir o conteúdo em imagens de sistema operacional utilizado para efetuar o arranque PXE ou multicast

 Não inclua aplicações de linha de negócio ou software que contenham dados confidenciais numa imagem que utiliza para efetuar o arranque PXE ou multicast.  

 Devido os inerentes os riscos de segurança com arranque PXE e multicast, reduza os riscos, se um computador não autorizado transfere a imagem de sistema operacional.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Restringir o conteúdo instalado por meio de variáveis de sequência de tarefas

 Não incluir aplicações de linha de negócio ou variáveis de sequências de software que contenham dados confidenciais em pacotes de aplicativos instalados através da tarefa.  

 Ao implementar software utilizando variáveis de sequências de tarefas, poderá ser instalada em computadores e utilizadores que não estão autorizados a recebê-lo.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Proteja o canal de rede após a migração de estado do utilizador

 Ao migrar o estado de utilizador, proteja o canal de rede entre o cliente e o ponto de migração de estado utilizando a assinatura SMB ou IPsec.  

 Após a ligação inicial através de HTTP, os dados da migração de estado de utilizador são transferidos utilizando SMB. Se não proteger o canal de rede, um invasor pode ler e modificar esses dados.  


### <a name="use-the-latest-version-of-usmt"></a>Utilizar a versão mais recente do USMT

 Utilize a versão mais recente do utilizador State Migration Tool (USMT) suportado pelo Configuration Manager.  

 A versão mais recente do USMT fornece melhoramentos de segurança e um maior controlo ao migrar dados de estado do utilizador.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Eliminar manualmente as pastas em pontos de migração de estado quando desativá-los  

 Quando remover uma pasta de ponto de migração de estado na consola do Configuration Manager no propriedades do ponto de migração de estado, o site não elimina a pasta física. Para proteger os dados de migração de estado de utilizador contra divulgação de informações, manualmente remover a partilha de rede e elimine a pasta.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Não configure a política de eliminação para eliminar imediatamente o estado do utilizador  

 Se configurar a política de eliminação no ponto de migração de estado imediatamente remover os dados que estão marcados para eliminação e se um atacante conseguir obter os dados de estado do utilizador antes do computador válido faz, o site elimina imediatamente os dados de estado do utilizador. Defina o **Eliminar depois de**  intervalo de modo a ser suficientemente longo para verificar o sucesso do restauro dos dados de estado de utilizador.  


### <a name="manually-delete-computer-associations"></a>Elimine manualmente as associações de computadores 

 Elimine manualmente as associações de computadores quando o restauro de dados de migração de estado de utilizador estiver concluído e verificado.

 O Configuration Manager não remove automaticamente as associações de computadores. Ajude a proteger a identidade dos dados de estado de utilizador eliminando manualmente as associações de computadores que não são mais necessárias.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Fazer manualmente cópias de segurança dos dados de migração de estado de utilizador no ponto de migração de estado  

 Cópia de segurança do Configuration Manager não inclui dados de migração de perfil do usuário na cópia de segurança do site.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementar controlos de acesso para proteger os suportes de dados pré-configurados  

 Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente e dados confidenciais.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementar controlos de acesso para proteger o processo de processamento de imagens do computador de referência  

 Certificar-se de que o computador de referência que utilizar para capturar imagens do sistema operacional está num ambiente seguro. Utilize controlos de acesso adequados, para que o software inesperado ou malicioso não pode ser instalado e nem incluir na imagem capturada. Ao capturar a imagem, certifique-se de que a localização de rede de destino é segura. Este processo ajuda a tornar-se de que a imagem não pode ser violada depois de capturá-la.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Instalar sempre as atualizações de segurança mais recentes no computador de referência  

 Se o computador de referência tiver as atualizações de segurança mais recentes, isso ajudará a reduzir a janela de vulnerabilidade dos novos computadores durante o primeiro arranque.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementar controlos de acesso ao implementar um sistema operacional num computador desconhecido

 Se tiver de implementar um sistema operacional para um computador desconhecido, implemente controlos de acesso para impedir que computadores não autorizados se conectem à rede.  

 Aprovisionamento de computadores desconhecidos fornece um método conveniente para implementar novos computadores a pedido. Mas também pode permitir que um invasor com eficiência se tornar num cliente fidedigno na sua rede. Limite o acesso físico à rede e monitorize os clientes para detetar computadores não autorizados. 

 Computadores que respondam a uma implementação de sistema operacional iniciadas por PXE podem ter todos os seus dados destruídos durante o processo. Esse comportamento pode resultar em perda de disponibilidade de sistemas que são reformatados de forma inadvertida.  


### <a name="enable-encryption-for-multicast-packages"></a>Ativar a encriptação de pacotes multicast  

 Para cada pacote de implementação do sistema operacional, pode ativar a encriptação quando o Configuration Manager transfere o pacote utilizando multicast. Esta configuração ajuda a impedir a adesão de computadores de ingressar na sessão multicast. Ele também ajuda a impedir atacantes de adulterarem a transmissão.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Monitorizar pontos de distribuição multicast ativados não autorizados  

 Se os atacantes conseguirem aceder à sua rede, pode configurar servidores multicast para falsificar a implementação do SO não autorizados.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Ao exportar sequências de tarefas para uma localização de rede, proteja a localização e o canal de rede

 Limite quem pode aceder à pasta de rede.  

 Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere a sequência de tarefas exportada.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Se utilizar a conta run as de sequência de tarefas, tome precauções de segurança adicionais

 Se utilizar o [uma conta run as de sequência de tarefas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account), siga os passos seguintes de precaução:  

 - Utilize uma conta com o mínimo de permissões necessárias.  

 - Não utilize a conta de acesso de rede para esta conta.  

 - Nunca torne a conta num administrador do domínio.  

 - Nunca configure perfis itinerantes para essa conta. Quando a sequência de tarefas é executada, transfere o perfil itinerante para a conta, o que deixará o perfil vulnerável a acesso no computador local.  

 - Limite o âmbito da conta. Por exemplo, crie contas para cada sequência de tarefas run as de sequência de tarefas diferente. Se uma conta for comprometida, apenas os computadores de cliente aos quais essa conta tem acesso sejam comprometidos. Se a linha de comandos exigir acesso administrativo no computador, considere criar uma conta de administrador local apenas para a conta run as de sequência de tarefas. Criar esta conta local em todos os computadores que executam a sequência de tarefas e eliminar a conta quando já não seja necessário.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Restrinja e monitorize os utilizadores administrativos que recebem o sistema operacional função de segurança do Gestor de implementação

 Os utilizadores administrativos que recebem o **Gestor de implementação do sistema operacional** função de segurança pode criar certificados autoassinados. Estes certificados, em seguida, podem ser utilizados para representar um cliente e obter a política de cliente do Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Usar HTTP avançada para reduzir a necessidade de uma conta de acesso de rede

A partir da versão 1806, quando ativa [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http), vários cenários de implementação do sistema operacional não precisam de uma conta de acesso de rede ao transferir o conteúdo a partir de um ponto de distribuição. Para obter mais informações, consulte [sequências de tarefas e a rede aceder à conta](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problemas de segurança de implementação do SO  

 Embora a implantação de sistema operacional pode ser um meio cómodo para implementar os sistemas de operativos mais seguros e configurações para computadores na sua rede, ela possui os seguintes riscos de segurança:  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgação de informações e denial-of-service  

 Se um atacante obtiver o controlo da sua infraestrutura do Configuration Manager, eles poderiam executar quaisquer sequências de tarefas. Esse processo pode incluir a formatar os discos rígidos de todos os computadores cliente. As sequências de tarefas podem ser configuradas para conter informações confidenciais, tais como contas que tenham permissões para aderir ao domínio e chaves de licenciamento em volume.  


### <a name="impersonation-and-elevation-of-privileges"></a>Representação e elevação de privilégios  

 As sequências de tarefas permitem associar um computador ao domínio, o que poderá fornecer acesso autenticado de rede a um computador não autorizado. 

 Protege o certificado de autenticação de cliente que é utilizado para dados de sequência de tarefas de arranque e para implementação de arranque PXE. Ao capturar um certificado de autenticação de cliente, este processo fornece um invasor uma oportunidade para obter a chave privada do certificado. Este certificado permite que eles representar um cliente válido na rede. Neste cenário, o computador não autorizado pode transferir a política, que pode conter dados confidenciais.  

 Se os clientes utilizam a conta de acesso de rede para acessar dados armazenados no ponto de migração de estado, estes clientes partilham efetivamente a mesma identidade. Eles poderiam acessar dados de migração de estado de outro cliente que utiliza a conta de acesso de rede. Os dados são encriptados para poderem ser lidos apenas pelo cliente original, mas podem ser adulterados ou eliminados.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Autenticação de cliente para o ponto de migração de estado é efetuada através de um token do Configuration Manager que é emitido pelo ponto de gestão.  

 O Configuration Manager não limita nem gere a quantidade de dados armazenados no ponto de migração de estado. Um atacante pode preencher o espaço em disco disponível e causar uma negação de serviço.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais  

 Embora as variáveis de coleção ofereçam um método flexível de implementar sistemas operativos, esta funcionalidade pode resultar em divulgação de informações.  



##  <a name="bkmk_privacy"></a> Informações de privacidade para implementação do SO  

 Para além de implementar um sistema operacional em computadores sem um, o Configuration Manager pode ser usado para migrar arquivos e configurações de usuários de um computador para outro. O administrador configura as informações para transferência, incluindo ficheiros de dados pessoais, definições de configuração e cookies do browser.  

 Configuration Manager armazena as informações num ponto de migração de estado e criptografa-o durante a transmissão e o armazenamento. O novo computador associado com as informações de estado pode obter as informações armazenadas. Se o novo computador perder a chave para recuperar as informações, um administrador do Configuration Manager com o **ver informações de recuperação** diretamente na objetos de instância de associação de computador podem aceder às informações e associá-la com um novo computador. Depois do novo computador restaura as informações de estado, este elimina os dados após um dia, por predefinição. Pode configurar o momento de remoção dos dados marcados para eliminação pelo ponto de migração de estado. Configuration Manager não armazena as informações de migração de estado do banco de dados do site e não enviar à Microsoft.  

 Se utilizar o suporte de dados de arranque para implementar imagens do sistema operacional, utilize sempre a opção predefinida para o suporte de dados de arranque proteger por senha. A palavra-passe encripta todas as variáveis armazenadas na sequência de tarefas, mas informações não armazenadas numa variável poderão ficar sujeitas a divulgação.  

 Implantação de sistema operacional pode utilizar sequências de tarefas para executar muitas tarefas diferentes durante o processo de implantação, que inclui a instalação de aplicações e atualizações de software. Quando configurar sequências de tarefas, também deve estar ciente das implicações de privacidade da instalação de software.  

 O Configuration Manager não implementa a implantação de sistema operacional por predefinição. Ele requer vários passos de configuração antes de recolher informações de estado de utilizador ou criar sequências de tarefas ou imagens de arranque.  

 Antes de configurar a implementação do SO, considere os requisitos de privacidade.  



## <a name="see-also"></a>Consulte também

[Dados de diagnóstico e de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)

[Segurança e privacidade do Configuration Manager](/sccm/core/plan-design/security/security-and-privacy)