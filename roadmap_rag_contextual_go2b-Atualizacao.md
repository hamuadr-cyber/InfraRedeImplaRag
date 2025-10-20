# GUIA DE ATUALIZAÇÃO DE DOCUMENTOS ESTRATÉGICOS
## Sistema RAG - Caso GO2B | Processo nº 1039604-94.2023.8.26.0405

**Versão:** 1.0  
**Data:** 14 de outubro de 2025  
**Autor:** Análise Estratégica Especializada  
**Classificação:** CONFIDENCIAL - Manual Técnico Operacional

---

## 📋 SUMÁRIO

1. [Princípios Fundamentais](#1-princípios-fundamentais)
2. [Arquitetura JSON Base](#2-arquitetura-json-base)
3. [Campos de Inteligência Estratégica](#3-campos-de-inteligência-estratégica)
4. [Processo de Atualização](#4-processo-de-atualização)
5. [Checklist de Qualidade](#5-checklist-de-qualidade)
6. [Exemplos Práticos](#6-exemplos-práticos)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. PRINCÍPIOS FUNDAMENTAIS

### 1.1. Missão do Sistema

O sistema RAG (Retrieval-Augmented Generation) GO2B é uma **ferramenta de inteligência jurídica estratégica** que transforma documentos não-estruturados em dados estruturados JSON para alimentar análises especializadas em litígio complexo.

### 1.2. Princípios Invioláveis

#### 🔴 PRINCÍPIO #1: PRESERVAÇÃO ESTRUTURAL ABSOLUTA
**Regra de Ouro:** NUNCA modificar ou remover campos existentes. SEMPRE adicionar novos campos.

```json
// ❌ ERRADO - Modifica campo existente
{
  "doc_id": "doc63_modificado"  // NUNCA FAZER ISSO
}

// ✅ CORRETO - Adiciona novo campo
{
  "doc_id": "doc63",  // Campo original preservado
  "doc_id_versao_enriquecida": "doc63_v2"  // Novo campo adicionado
}
```

#### 🔴 PRINCÍPIO #2: RASTREABILIDADE TOTAL
Toda informação DEVE ter fonte identificável.

```json
{
  "evidencia": "CNPJ 12.068.851/0001-55",
  "fonte": "Receita Federal + JUCESP",
  "localizacao_doc": "Dossiê Seção 1.4",
  "evidencia_documental": "Reportagem Metrópoles 10/06/2024"
}
```

#### 🔴 PRINCÍPIO #3: UTILIDADE PRÁTICA IMEDIATA
Cada campo deve responder perguntas concretas de advogados.

**Teste de Utilidade:**
- ❓ "Qual fundamento legal usar na exceção impedimento?" 
- ✅ Campo `mapa_probatorio.cadeias[0].fundamento_legal` responde

#### 🔴 PRINCÍPIO #4: DADOS REAIS, ZERO PLACEHOLDERS
Proibido deixar arrays vazios ou valores `null` quando dados existem na fonte.

```json
// ❌ ERRADO
"evidencias": []

// ✅ CORRETO
"evidencias": [
  {
    "id": "ev_001",
    "tipo": "documento_publico",
    "descricao": "CNPJ...",
    "fonte": "Receita Federal"
  }
]
```

---

## 2. ARQUITETURA JSON BASE

### 2.1. Estrutura Hierárquica

```
doc63 (JSON raiz)
├── Metadados Identificação
│   ├── doc_id
│   ├── doc_nome_base
│   └── titulo_humano
├── Campos Originais (v1-v4)
│   ├── mapeamento_fontes
│   ├── reconciliada_base
│   ├── analise_inicial_v1
│   ├── texto_fonte_v3/v4
│   ├── normalizacao
│   ├── referencia_md_acessivel
│   ├── referencia_md_omniconvert
│   ├── analise_ia_real
│   └── descricao_adriano
└── Campos Inteligência Estratégica (NOVOS)
    ├── grafo_rede_criminosa
    ├── timeline_nexo_causal
    ├── mapa_probatorio_estrategico
    ├── matriz_riscos_cenarios
    ├── correlacoes_documentais
    ├── plano_acao_estrategico
    └── analise_contraditorio
```

### 2.2. Tipos de Dados Padronizados

| Campo | Tipo | Exemplo | Observação |
|-------|------|---------|------------|
| Datas | ISO 8601 | `"2025-10-14"` | Sempre YYYY-MM-DD |
| Valores BRL | float | `387055636.47` | Sem separador milhares |
| Probabilidades | int (0-100) | `85` | Percentual inteiro |
| CNPJs | string | `"12.068.851/0001-55"` | Com formatação |
| Processos | string | `"1039604-94.2023.8.26.0405"` | Número completo |

### 2.3. Campos Obrigatórios por Categoria

**Metadados (sempre presentes):**
- `doc_id`, `doc_nome_base`, `titulo_humano`, `mapeamento_fontes`

**Campos Originais (preservar 100%):**
- Todos de `v1` a `v4` + `reconciliada_base` + `analise_ia_real`

**Campos Estratégicos (adicionar quando aplicável):**
- Os 7 campos conforme necessidade do caso

---

## 3. CAMPOS DE INTELIGÊNCIA ESTRATÉGICA

### 3.1. GRAFO_REDE_CRIMINOSA

**Propósito:** Mapear visualmente conexões entre agentes.

**Estrutura Mínima:**
```json
{
  "grafo_rede_criminosa": {
    "metadata": {
      "gerado_em": "ISO_DATE",
      "total_nodes": 0,
      "total_edges": 0
    },
    "nodes": [],
    "edges": [],
    "clusters": [],
    "caminhos_criticos": []
  }
}
```

**Como Preencher:**

1. **Identificar Agentes:**
   - Ler Dossiê Seção 1 (Identificação Agentes)
   - Cada pessoa/empresa = 1 node
   - Atribuir `id` único (ex: `"marcello_perino"`)

2. **Mapear Conexões:**
   - Parentesco → tipo: `"parentesco"`
   - Transação comercial → tipo: `"transacao_comercial"`
   - Sociedade → tipo: `"sociedade_empresarial"`
   - Nomeação judicial → tipo: `"nomeacao_judicial"`

3. **Definir Clusters:**
   - Agrupar agentes por função operacional
   - Ex: "Núcleo SP", "Operadores Pressão", "Conexão Interestadual"

4. **Identificar Caminhos Críticos:**
   - Cadeia que fundamenta impedimento principal
   - Ex: Juiz → Irmão → Parceiro → Sócio → Esposa → AJ

**Exemplo Real:**
```json
{
  "nodes": [
    {
      "id": "marcello_perino",
      "nome": "Marcello do Amaral Perino",
      "tipo": "magistrado",
      "papel_rede": "Nomeador/Controlador",
      "risco_juridico": "CRITICO",
      "impedimento_legal": "Art. 144, VI, CPC",
      "dados_adicionais": {
        "vara": "1ª Vara Empresarial Osasco",
        "processo": "1039604-94.2023.8.26.0405"
      }
    }
  ],
  "edges": [
    {
      "source": "marcello_perino",
      "target": "fernando_perino",
      "tipo": "parentesco",
      "descricao": "Irmão - 1º grau",
      "evidencia": "Público e notório + Metrópoles",
      "relevancia_juridica": "Impedimento Art. 144, VI"
    }
  ]
}
```

**Validação:**
- [ ] Todo node tem `id`, `nome`, `tipo`, `papel_rede`
- [ ] Todo edge tem `source`, `target`, `tipo`, `evidencia`
- [ ] Caminhos críticos têm fundamentação jurídica

---

### 3.2. TIMELINE_NEXO_CAUSAL

**Propósito:** Linha do tempo com análise de causalidade.

**Estrutura Mínima:**
```json
{
  "timeline_nexo_causal": {
    "metadata": {
      "periodo": "YYYY-MM-DD a YYYY-MM-DD",
      "total_eventos": 0
    },
    "eventos": [],
    "fases_cronologicas": [],
    "padroes_temporais": [],
    "janelas_criticas": []
  }
}
```

**Como Preencher:**

1. **Extrair Eventos:**
   - Ler Dossiê Seção 5 (Timeline) + Parecer Técnico Seção 8
   - Data + Evento + Agentes + Valores + Causa + Consequência

2. **Analisar Nexo Causal:**
   - Para CADA evento, perguntar: "Por que aconteceu? O que resultou?"
   - Documentar em `causa_provavel` e `consequencia_observada`

3. **Identificar Padrões:**
   - Renúncias coordenadas?
   - Nomeações recíprocas?
   - Omissões sistemáticas?

4. **Marcar Criticidade:**
   - MAXIMA: Eventos que fundamentam medidas urgentes
   - ALTA: Eventos relevantes mas não determinantes
   - MEDIA/BAIXA: Contextuais

**Exemplo Real:**
```json
{
  "eventos": [
    {
      "data": "2020-10-01",
      "timestamp_unix": 1601510400,
      "evento": "Garcia concede procuração R$ 17MM para Fernando Perino",
      "agentes_envolvidos": ["fabio_garcia", "fernando_perino"],
      "valores_financeiros": [17000000.0],
      "contexto_temporal": "Mesmo ano Marcello assume vara empresarial",
      "causa_provavel": "Estabelecimento vínculo comercial irmão juiz + operador rede",
      "consequencia_observada": "Parceria que fundamenta impedimento judicial",
      "evidencia_documental": "Metrópoles 23/10/2023",
      "relevancia_juridica": "Fundamento central exceção impedimento Art. 144, VI",
      "vinculo_go2b": "Vício de origem - juiz impedido desde início",
      "criticidade": "MAXIMA",
      "dias_processo_go2b": -1169
    }
  ]
}
```

**Validação:**
- [ ] Todos eventos têm data ISO format
- [ ] Causa-consequência documentada
- [ ] Evidência identificada
- [ ] Criticidade atribuída

---

### 3.3. MAPA_PROBATORIO_ESTRATEGICO

**Propósito:** Conectar Evidência → Fundamento → Medida Judicial.

**Estrutura Cadeias:**
```json
{
  "cadeias_argumentativas": [
    {
      "id": "cadeia_001",
      "tese_juridica": "Impedimento absoluto juiz (Art. 144, VI, CPC)",
      "categoria": "impedimento",
      "evidencias": [
        {
          "id": "ev_001",
          "tipo": "documento_publico_oficial",
          "descricao": "CNPJ comprova sociedade Andrea-Garcia",
          "fonte": "Receita Federal",
          "forca_probatoria": "DIRETA",
          "refutabilidade": "IMPOSSIVEL",
          "localizacao_doc": "Dossiê Seção 4.2"
        }
      ],
      "fundamento_legal": {
        "dispositivo": "Art. 144, VI, CPC",
        "texto": "Há impedimento quando...",
        "interpretacao": "Jurisprudência STJ reconhece..."
      },
      "medida_judicial": {
        "tipo": "Exceção de Impedimento",
        "fundamento": "Art. 146, CPC",
        "prazo_legal": "15 dias",
        "efeito": "Suspensão imediata"
      },
      "probabilidade_sucesso": 85
    }
  ]
}
```

**Como Preencher:**

1. **Identificar Teses:**
   - Impedimento, Suspeição, Crime, Ato inexistente
   - Uma cadeia por tese

2. **Listar Evidências:**
   - Documentos públicos (força DIRETA)
   - Investigações (força INSTITUCIONAL)
   - Padrões (força INDICIARIA)

3. **Fundamentar Legalmente:**
   - Dispositivo específico
   - Interpretação doutrinária
   - Jurisprudência aplicável

4. **Conectar à Medida:**
   - Qual petição protocolar?
   - Prazo legal?
   - Efeito esperado?

**Validação:**
- [ ] Cada evidência tem fonte + localização
- [ ] Fundamento legal citado corretamente
- [ ] Probabilidade realista (não otimista demais)
- [ ] Medida judicial cabível especificada

---

### 3.4. MATRIZ_RISCOS_CENARIOS

**Propósito:** Quantificar riscos por cenário de ação/inação.

**Estrutura:**
```json
{
  "cenarios": [
    {
      "id": "cenario_a",
      "nome": "INÉRCIA TOTAL",
      "acao_necessaria": "Nenhuma (omissão)",
      "probabilidade_ocorrencia": 95,
      "impactos": {
        "financeiro": {},
        "juridico": {},
        "reputacional": {}
      },
      "riscos_especificos": [],
      "mitigacoes_possiveis": [],
      "viabilidade": "INACEITAVEL",
      "pontuacao_risco": 100
    }
  ]
}
```

**Como Preencher:**

1. **Definir Cenários:**
   - Mínimo 3: Inércia, Ação Isolada, Ação Combinada
   - Opcional 4º: Estratégia Completa (judicial + institucional)

2. **Quantificar Impactos:**
   - Financeiro: Valores estimados recuperação/perda
   - Jurídico: Probabilidades decisões
   - Social: Empregos salvos/perdidos

3. **Ser Realista:**
   - Não otimismo excessivo
   - Basear em dados do caso
   - Considerar jurisprudência

**Exemplo:**
```json
{
  "cenario_c_acao_combinada": {
    "investimento": 75000.0,
    "beneficio_estimado": 174000000.0,
    "roi": "2.320x",
    "probabilidade_sucesso": 85,
    "impactos": {
      "credores": {
        "percentual_recuperacao": "30-60%",
        "melhoria_vs_inercia": "+25 a +55 pontos"
      }
    }
  }
}
```

**Validação:**
- [ ] Valores financeiros calculados
- [ ] Probabilidades somam lógica (não >100%)
- [ ] ROI calculado corretamente
- [ ] Viabilidade classificada

---

### 3.5. CORRELACOES_DOCUMENTAIS

**Propósito:** Mapear como doc63 se relaciona com outros docs.

**Estrutura:**
```json
{
  "documentos_relacionados": {
    "doc62": {
      "titulo": "Relatório Completo",
      "tipo_relacao": "complementar_expandido",
      "grau_dependencia": "ALTO",
      "uso_estrategico": "..."
    }
  },
  "matriz_uso_por_peticao": {
    "excecao_impedimento": {
      "documentos_principais": ["doc63"],
      "secoes_especificas": ["Grafo rede", "Timeline"],
      "forca_argumentativa": 95
    }
  }
}
```

**Como Preencher:**

1. **Identificar Docs Relacionados:**
   - Ler campo `mapeamento_fontes`
   - Checar referências cruzadas no texto

2. **Classificar Relação:**
   - Complementar, Evidência direta, Prejudicialidade, Fundação

3. **Mapear Uso por Petição:**
   - Para cada tipo de petição (exceção, destituição, etc)
   - Listar quais docs/seções usar

**Validação:**
- [ ] Todos docs referenciados existem
- [ ] Uso estratégico definido
- [ ] Matriz completa para principais petições

---

### 3.6. PLANO_ACAO_ESTRATEGICO

**Propósito:** Roadmap executivo com checklist ações.

**Estrutura:**
```json
{
  "urgencia_maxima_24_48h": [],
  "urgencia_alta_3_7_dias": [],
  "urgencia_media_7_15_dias": [],
  "monitoramento_continuo": [],
  "marcos_criticos": []
}
```

**Como Preencher:**

1. **Priorizar por Prazo Legal:**
   - Exceção impedimento: 15 dias (MÁXIMA)
   - Medidas urgentes: 24-48h
   - Representações: 3-7 dias

2. **Especificar CADA Ação:**
   ```json
   {
     "id": "acao_001",
     "acao": "Protocolar Exceção Impedimento",
     "tipo": "judicial",
     "fundamento_legal": "Art. 146, CPC",
     "evidencias_chave": ["CNPJ", "Procuração R$ 17MM"],
     "prazo_fatal": "15 dias",
     "responsavel": "Advogado processualista",
     "custo_estimado": 15000.0,
     "probabilidade_sucesso": 85,
     "status": "PENDENTE",
     "prioridade": 1
   }
   ```

3. **Definir Monitoramento:**
   - O que monitorar?
   - Frequência (diária/semanal)?
   - Alerta se (condição)?

**Validação:**
- [ ] Todas ações têm prazo
- [ ] Custos estimados
- [ ] Responsáveis definidos
- [ ] Prioridades ordenadas

---

### 3.7. ANALISE_CONTRADITORIO

**Propósito:** Antecipar e neutralizar argumentos adversos.

**Estrutura:**
```json
{
  "teses_adversas_previsiveis": [
    {
      "id": "tese_001",
      "tese": "GO2B inventa máfia judicial",
      "fundamento_adverso": "Teoria conspiratória",
      "probabilidade_uso": 90,
      "refutacao_estruturada": {
        "argumento_1": "Corregedoria investiga independentemente",
        "argumento_2": "MPF instaurou inquérito",
        "conclusao": "Impossível 4 instituições inventarem"
      },
      "forca_refutacao": 95
    }
  ]
}
```

**Como Preencher:**

1. **Pensar Como Adversário:**
   - Ler Parecer Estratégico-Ideológico
   - Quais argumentos usariam?

2. **Estruturar Refutação:**
   - Argumento 1, 2, 3...
   - Evidências que refutam
   - Conclusão lógica

3. **Identificar Vulnerabilidades Próprias:**
   - Ser honesto sobre pontos fracos
   - Definir mitigações

**Validação:**
- [ ] Teses mais prováveis mapeadas
- [ ] Refutações com evidências
- [ ] Vulnerabilidades reconhecidas + mitigadas

---

## 4. PROCESSO DE ATUALIZAÇÃO

### 4.1. Workflow Padrão

```
┌──────────────┐
│ 1. Receber   │
│    JSON Base │
└──────┬───────┘
       │
       v
┌──────────────────┐
│ 2. Analisar      │
│    Docs Fonte    │
│    (Dossiê +     │
│     Pareceres)   │
└──────┬───────────┘
       │
       v
┌──────────────────┐
│ 3. Extrair Dados │
│    Relevantes    │
└──────┬───────────┘
       │
       v
┌──────────────────┐
│ 4. Preencher     │
│    7 Campos      │
│    Estratégicos  │
└──────┬───────────┘
       │
       v
┌──────────────────┐
│ 5. Validar       │
│    (Checklist)   │
└──────┬───────────┘
       │
       v
┌──────────────────┐
│ 6. Gerar JSON    │
│    Enriquecido   │
└──────────────────┘
```

### 4.2. Passo-a-Passo Detalhado

**PASSO 1: Preparação**
- [ ] Ter JSON base (v4 ou superior)
- [ ] Ter acesso aos docs fonte (Dossiê + Pareceres)
- [ ] Ambiente de edição JSON configurado

**PASSO 2: Análise Documental**
- [ ] Ler `referencia_md_acessivel` (Dossiê completo)
- [ ] Ler `analise_ia_real` (Pareceres Técnico + Estratégico)
- [ ] Identificar seções relevantes para cada campo

**PASSO 3: Extração Estruturada**

Criar planilha/tabela auxiliar:

| Campo | Seção Fonte | Dados Extraídos | Status |
|-------|-------------|-----------------|--------|
| Grafo | Dossiê Seção 1-4 | 10 nodes, 12 edges | ✅ |
| Timeline | Dossiê Seção 5 + Parecer Seção 8 | 35 eventos | ✅ |
| ... | ... | ... | ... |

**PASSO 4: Preenchimento**

Para CADA campo:
1. Copiar estrutura template (seção 3 deste guia)
2. Preencher com dados reais extraídos
3. Adicionar fontes/evidências em TODOS os itens
4. Verificar tipos de dados (datas ISO, valores float, etc)

**PASSO 5: Validação**
- [ ] Rodar checklist seção 5
- [ ] Verificar rastreabilidade (toda info tem fonte?)
- [ ] Testar queries exemplo (seção 6)

**PASSO 6: Finalização**
- [ ] Atualizar `metadados_ingestao`
- [ ] Adicionar campo `auditoria` com timestamp
- [ ] Gerar hash SHA256 (opcional)
- [ ] Salvar JSON enriquecido

---

## 5. CHECKLIST DE QUALIDADE

### 5.1. Validação Estrutural

- [ ] **Preservação 100%:** Nenhum campo original removido
- [ ] **JSON válido:** Sem erros sintaxe (vírgulas, chaves, aspas)
- [ ] **Hierarquia correta:** Campos novos dentro de nível adequado
- [ ] **Tipos consistentes:** Datas ISO, valores float, IDs string

### 5.2. Validação de Conteúdo

- [ ] **Zero placeholders:** Nenhum array vazio quando dados existem
- [ ] **Rastreabilidade:** Toda informação tem `fonte` ou `evidencia_documental`
- [ ] **Precisão:** Valores financeiros exatos (não arredondados)
- [ ] **Consistência:** Datas/valores coincidem entre campos

### 5.3. Validação de Utilidade

- [ ] **Queries funcionam:** Teste queries exemplo (seção 6)
- [ ] **Advogado usaria:** Informação imediatamente útil?
- [ ] **Completo:** Responde perguntas operacionais?

### 5.4. Validação de Rastreamento

Para 10 informações aleatórias do JSON:
- [ ] É possível encontrar a fonte no Dossiê/Parecer?
- [ ] Campo `localizacao_doc` está correto?
- [ ] Evidência existe e está acessível?

### 5.5. Validação de Integridade

- [ ] **Grafos fecham:** Todos nodes de edges existem?
- [ ] **Timeline ordenado:** Eventos em ordem cronológica?
- [ ] **Valores batem:** Somam corretamente quando agregados?
- [ ] **Lógica coerente:** Probabilidades não excedem 100%?

---

## 6. EXEMPLOS PRÁTICOS

### 6.1. Exemplo: Adicionar Novo Node ao Grafo

**Cenário:** Descobriu novo agente "João Silva" relacionado ao caso.

**Passo-a-Passo:**

```json
// 1. Identificar dados do agente no Dossiê
{
  "id": "joao_silva",
  "nome": "João Silva",
  "tipo": "advogado",  // magistrado, advogado, empresa, perito
  "papel_rede": "Operador secundário",
  "risco_juridico": "MEDIO",
  "dados_adicionais": {
    "oab": "123.456/SP",
    "escritorio": "Silva & Associados"
  }
}

// 2. Adicionar ao array nodes
"nodes": [
  // ... nodes existentes ...
  {
    "id": "joao_silva",
    ...
  }
]

// 3. Se houver conexões, adicionar edges
"edges": [
  // ... edges existentes ...
  {
    "source": "fabio_garcia",
    "target": "joao_silva",
    "tipo": "parceria_profissional",
    "descricao": "Atuaram juntos em processo X",
    "evidencia": "Autos processo Y",
    "relevancia_juridica": "Demonstra rede colaboração"
  }
]

// 4. Atualizar metadata
"metadata": {
  "total_nodes": 11,  // Era 10, agora 11
  "total_edges": 13   // Se adicionou edge
}
```

### 6.2. Exemplo: Adicionar Evento ao Timeline

**Cenário:** Descobriu evento "15/03/2024 - Reunião documentada entre agentes".

```json
{
  "data": "2024-03-15",
  "timestamp_unix": 1710460800,
  "evento": "Reunião documentada entre Garcia e Bissolatti",
  "descricao_completa": "Email evidencia reunião para 'alinhamento estratégico caso X'",
  "agentes_envolvidos": ["fabio_garcia", "kleber_bissolatti"],
  "valores_financeiros": [],  // Vazio se não houver valores
  "contexto_temporal": "Durante período crítico processo GO2B",
  "causa_provavel": "Coordenação de atuação na rede",
  "consequencia_observada": "Padronização argumentos em múltiplos processos",
  "evidencia_documental": "Email anexo doc_XYZ",
  "relevancia_juridica": "Demonstra coordenação - Lei 12.850/2013",
  "vinculo_go2b": "Mesmo padrão aplicado no caso",
  "criticidade": "MEDIA",
  "dias_processo_go2b": 105  // Calcular diferença para 2023-12-01
}
```

### 6.3. Exemplo: Criar Nova Cadeia Probatória

**Cenário:** Identificou novo fundamento jurídico não mapeado.

```json
{
  "id": "cadeia_007",
  "tese_juridica": "Fraude processual (Art. 347 CP)",
  "categoria": "crime",
  "evidencias": [
    {
      "id": "ev_007_001",
      "tipo": "documento_falso",
      "descricao": "Petição com data adulterada",
      "fonte": "Perícia documento fls. XXX",
      "forca_probatoria": "DIRETA",
      "refutabilidade": "BAIXA",
      "localizacao_doc": "Autos processo fls. XXX",
      "peso_juridico": 8
    }
  ],
  "fundamento_legal": {
    "dispositivo": "Art. 347 CP",
    "texto": "Inovar artificialmente prova em processo...",
    "interpretacao": "..."
  },
  "medida_judicial": {
    "tipo": "Denúncia Criminal",
    "fundamento": "Art. 347 CP",
    "prazo": "Não há prazo específico",
    "efeito": "Processo criminal + nulidade atos baseados em prova adulterada"
  },
  "probabilidade_sucesso": 70
}
```

### 6.4. Exemplo: Query no Sistema RAG

**Query:** "Qual a melhor estratégia para proteção GO2B?"

**Resposta Sistema (baseada no JSON):**

```
Fonte: matriz_riscos_cenarios.cenario_d
Resposta: Estratégia Institucional Completa
  - Investimento: R$ 200.000
  - Benefício estimado: R$ 213.000.000
  - ROI: 1.065x + intangíveis
  - Probabilidade sucesso: 90%
  - Ações: judicial (8) + institucional (5) + comunicação (3)

Fonte: plano_acao_estrategico.urgencia_maxima_24_48h
Primeiras ações (24-48h):
  1. Exceção impedimento (prob. 85%)
  2. Destituição AJ (prob. 80%)
  3. Declaração ato inexistente DNS (prob. 95%)

Fonte: mapa_probatorio.estrategia_combinada
Fundamentos mais fortes:
  - Cadeia 001: Impedimento (CNPJ oficial) - 95%
  - Cadeia 005: Ato inexistente (Certificado Registro.br) - 98%
```

---

## 7. TROUBLESHOOTING

### 7.1. Problemas Comuns

#### ❌ **Erro: "Campo duplicado"**

**Causa:** Tentou adicionar campo que já existe.

**Solução:** Renomear novo campo ou usar sufixo:
```json
// Ao invés de
"analise_ia_real": {...}  // JÁ EXISTE

// Use
"analise_ia_real_v2": {...}
// ou
"analise_ia_enriquecida": {...}
```

#### ❌ **Erro: "Array vazio quando não deveria"**

**Causa:** Não preencheu dados reais.

**Solução:** 
1. Verificar se dados existem na fonte
2. Se existem, extrair e preencher
3. Se NÃO existem, documentar: `"evidencias": []  // Nenhuma evidência disponível fonte"`

#### ❌ **Erro: "Fonte não rastreável"**

**Causa:** Informação sem campo `fonte` ou `evidencia_documental`.

**Solução:** SEMPRE adicionar:
```json
{
  "descricao": "Juiz foi promovido em 2024",
  "fonte": "Comunicado TJSP Órgão Especial",  // ← OBRIGATÓRIO
  "evidencia_documental": "Dossiê Seção 1.1"  // ← OBRIGATÓRIO
}
```

#### ❌ **Erro: "Data formato incorreto"**

**Causa:** Data não está em ISO format.

**Solução:**
```json
// ❌ ERRADO
"data": "14/10/2025"
"data": "14-out-2025"

// ✅ CORRETO
"data": "2025-10-14"
```

#### ❌ **Erro: "JSON inválido"**

**Causa:** Erro sintaxe (vírgula faltando, chave não fechada).

**Solução:** Usar validador JSON online (jsonlint.com) ou ferramenta VS Code.

### 7.2. Perguntas Frequentes

**P: Posso modificar campos originais do JSON base?**  
R: **NÃO.** NUNCA modificar campos existentes. SEMPRE adicionar novos.

**P: E se dados não existem na fonte?**  
R: Documentar explicitamente: `"eventos": []  // Nenhum evento disponível em fonte"`

**P: Quantos campos estratégicos adicionar?**  
R: Depende do caso. Mínimo 3 (grafo, timeline, mapa probatório). Máximo 7 (todos). Use bom senso.

**P: Preciso preencher TODOS os sub-campos?**  
R: Sim, se dados existem. Não deixar `null` ou vazio quando informação está na fonte.

**P: Como calcular probabilidades de sucesso?**  
R: Baseie em: (1) Força evidências, (2) Jurisprudência, (3) Experiência. Seja realista, não otimista.

**P: Posso usar este guia para outros casos?**  
R: Sim! Estrutura é genérica. Adapte nomes/valores ao caso específico.

**P: Como versionar JSONs enriquecidos?**  
R: Adicionar campo `"versao_enriquecimento": "1.0"` e incrementar em atualizações.

---

## CONCLUSÃO

Este guia capacita qualquer pessoa (humana ou IA) a atualizar documentos JSON estratégicos do sistema RAG GO2B com **qualidade profissional jurídica**.

### Resumo dos Princípios:

1. ✅ **PRESERVAR** estrutura original 100%
2. ✅ **RASTREAR** toda informação à fonte
3. ✅ **USAR** dados reais, zero placeholders
4. ✅ **VALIDAR** com checklist rigoroso
5. ✅ **DOCUMENTAR** metodologia e versões

### Próximos Passos:

- [ ] Testar processo com caso exemplo
- [ ] Criar template JSON vazio para novos casos
- [ ] Automatizar validações com script Python
- [ ] Integrar com sistema RAG produção
- [ ] Treinar equipe jurídica no uso

---

**Versão do Guia:** 1.0  
**Última Atualização:** 14/10/2025  
**Autor:** Sistema de Inteligência Jurídica GO2B  
**Contato:** juridico@go2b.com.br

---

**FIM DO GUIA DE ATUALIZAÇÃO**