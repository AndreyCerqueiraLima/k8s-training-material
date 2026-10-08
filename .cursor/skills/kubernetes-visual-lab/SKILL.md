---
name: kubernetes-visual-lab
description: >-
  Guides work on KubeWorld (processador-example): every feature and copy must align
  with official Kubernetes documentation, and changes should teach how Kubernetes
  works through visual simulation. Use when editing this repo, adding simulator
  behavior, YAML parsing, UI copy, probes, Services, or any Kubernetes concept
  in index.html.
---

# KubeWorld — laboratório visual de Kubernetes

## Princípios do projeto

1. **Tudo que for feito deve ser baseado na documentação do Kubernetes** ([kubernetes.io](https://kubernetes.io/docs/)).
2. **A ideia deste projeto é ilustrar visualmente como o Kubernetes funciona** — o simulador é didático, não um substituto de cluster real.

Antes de implementar ou explicar comportamento, confira conceitos e campos da API na documentação oficial (conceitos, tasks e referência da API). Se o lab simplificar algo, deixe isso explícito na UI ou em comentários curtos no código.

## O que é este repositório

- Aplicação principal em **`index.html`** (KubeWorld): cluster interativo, editor YAML, missões, modais de inspeção, documentação K8s embutida (`k8sApiDocs`), tipos de Service, lab de probes, etc.
- Não invente semântica de API: nomes de campos, tipos de recurso, probes, Service types e fluxos de control plane devem refletir o que a documentação descreve (com abstração visual aceitável).

## Ao adicionar ou alterar funcionalidade

1. **Fonte da verdade**: [kubernetes.io/docs](https://kubernetes.io/docs/) — preferir páginas de conceitos + referência da API do recurso (ex.: Pod v1, Service v1, Deployment apps/v1).
2. **Visual primeiro**: cada mudança deve ajudar o usuário a *ver* reconciliação, rede, scaling, self-healing, probes ou tipos de Service — diagrama, animação, telemetria ou aba “Documentação K8s” com link oficial.
3. **YAML declarativo**: o estado desejado vem dos manifestos aplicados; o simulador reconcilia a tela (padrão já usado no projeto).
4. **i18n**: textos de UI em `uiText` / `extraText` / `structureText` (pt-BR e en-US).
5. **Escopo mínimo**: alterar só o necessário em `index.html`; não expandir o repo sem pedido explícito.

## Simplificações já aceitas no lab (manter coerência)

- `kind: Cluster` com `spec.nodes` é extensão do simulador, não um recurso Kubernetes real — documentar como “configuração do lab”.
- IPs ClusterIP / LoadBalancer e alguns timings são **simulados**; labels na UI devem indicar “simulado” quando relevante.
- Parser YAML é intencionalmente limitado (regex); novos campos devem seguir o mesmo estilo e validar o que a doc exige para o cenário didático.

## Checklist rápido antes de concluir

- [ ] Comportamento novo está alinhado à doc oficial (não só “faz sentido”).
- [ ] Há suporte visual ou textual para o usuário entender o *porquê* no modelo Kubernetes.
- [ ] Links ou tabela de propriedades apontam para kubernetes.io quando aplicável.
- [ ] Traduções PT/EN atualizadas se mudou copy.
- [ ] Script inline continua válido (sem erros de sintaxe em `index.html`).

## Referências úteis no código

- `structures`, `k8sApiDocs`, `parseYaml`, `renderWorld`, `openObjectDetail`, `normalizeServiceRecord` — padrões para recursos e diagramas.
- Inspeção: clique em objetos `[data-structure]`; abas Visão geral, Informações avançadas, Documentação K8s.
