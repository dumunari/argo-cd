# Visão geral

<!-- markdownlint-disable MD026 -->
## O que é o Argo CD?
<!-- markdownlint-enable MD026 -->

O Argo CD é uma ferramenta declarativa de entrega contínua (Continuous Delivery), baseada em GitOps, para Kubernetes.

![Interface do Argo CD](assets/argocd-ui.gif)

<!-- markdownlint-disable MD026 -->
## Por que Argo CD?
<!-- markdownlint-enable MD026 -->

As definições, configurações e ambientes das aplicações devem ser declarativos e controlados por versionamento.

A implantação e o gerenciamento do ciclo de vida das aplicações devem ser automatizados, auditáveis e fáceis de entender.

## Primeiros Passos

### Início Rápido

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Siga nosso [guia de primeiros passos](getting_started.md). [Documentação](user-guide/) adicional orientada ao usuário
é fornecida para recursos extras. Se você está procurando atualizar o Argo CD, consulte o [guia de atualização](./operator-manual/upgrading/overview.md).
[Documentação](developer-guide/) orientada ao desenvolvedor está disponível para pessoas interessadas em construir integrações de terceiros.

## Como funciona

O Argo CD segue o padrão **GitOps** de usar repositórios Git como fonte da verdade para definir
o estado desejado da aplicação. Os manifestos do Kubernetes podem ser especificados de várias formas:

* Aplicações [kustomize](https://kustomize.io)
* Charts [helm](https://helm.sh)
* Arquivos [jsonnet](https://jsonnet.org)
* Diretório simples de manifestos YAML/json
* Qualquer ferramenta personalizada de gerenciamento de configuração configurada como plugin de gerenciamento de configuração

O Argo CD automatiza a implantação dos estados desejados da aplicação nos ambientes de destino especificados.
As implantações de aplicações podem acompanhar atualizações de branches, tags, ou ser fixadas a uma versão específica de
manifestos em um commit Git. Consulte [estratégias de rastreamento](user-guide/tracking_strategies.md) para detalhes
adicionais sobre as diferentes estratégias de rastreamento disponíveis.

Para uma visão geral rápida de 10 minutos do Argo CD, confira a demonstração apresentada na reunião da
comunidade Sig Apps:

[![Demonstração da Visão Geral do Argo CD](https://img.youtube.com/vi/aWDIQMbp1cc/0.jpg)](https://youtu.be/aWDIQMbp1cc?t=1m4s)

## Arquitetura

![Arquitetura do Argo CD](assets/argocd_architecture.png)

O Argo CD é implementado como um controlador Kubernetes que monitora continuamente aplicações em execução
e compara o estado atual e ativo contra o estado de destino desejado (conforme especificado no repositório Git).
Uma aplicação implantada cujo estado ativo se desvia do estado de destino é considerada `Fora de Sincronização (Out of Sync)`.
O Argo CD relata e visualiza as diferenças, enquanto fornece facilidades para sincronizar automática ou
manualmente o estado ativo de volta ao estado de destino desejado. Quaisquer modificações feitas ao estado
de destino desejado no repositório Git podem ser automaticamente aplicadas e refletidas nos ambientes de destino
especificados.

Para detalhes adicionais, consulte [visão geral da arquitetura](operator-manual/architecture.md).

## Recursos

* Implantação automatizada de aplicações em ambientes de destino especificados
* Suporte para múltiplas ferramentas de gerenciamento de configuração/templates (Kustomize, Helm, Jsonnet, YAML simples)
* Capacidade de gerenciar e implantar em múltiplos clusters
* Integração SSO (OIDC, OAuth2, LDAP, SAML 2.0, GitHub, GitLab, Microsoft, LinkedIn)
* Políticas de multi-tenancy e RBAC para autorização
* Rollback/Roll-anywhere para qualquer configuração de aplicação commitada no repositório Git
* Análise de status de saúde dos recursos da aplicação
* Detecção e visualização automatizada de drift de configuração
* Sincronização automática ou manual de aplicações para seu estado desejado
* Interface web que fornece visualização em tempo real da atividade da aplicação
* CLI para automação e integração com Integração Contínua (CI)
* Integração com webhooks (GitHub, BitBucket, GitLab)
* Tokens de acesso para automação
* Hooks PreSync, Sync, PostSync para suportar rollouts complexos de aplicações (ex: atualizações blue/green e canary)
* Trilhas de auditoria para eventos de aplicações e chamadas de API
* Métricas do Prometheus
* Substituições de parâmetros para sobrescrever parâmetros helm no Git

## Status de Desenvolvimento

O Argo CD está sendo ativamente desenvolvido pela comunidade. Nossos lançamentos podem ser encontrados [aqui](https://github.com/argoproj/argo-cd/releases).

## Adoção

Organizações que adotaram oficialmente o Argo CD podem ser encontradas [aqui](https://github.com/argoproj/argo-cd/blob/master/USERS.md).