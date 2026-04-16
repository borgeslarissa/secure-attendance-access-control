# Meet Check-in App

Aplicação em Streamlit rodando no Databricks para controle de presença em reuniões via link dinâmico.

## Funcionalidades

* Check-in via link único (`token`)
* Validação de CPF
* Controle de acesso por horário (5 min antes até 1h depois)
* Expiração e desativação de links
* Registro em tabela Delta (Databricks)
* Redirecionamento automático para Google Meet
* Prevenção de acessos fora da janela permitida

## Analytics de Presença

O projeto inclui camadas analíticas prontas para monitoramento:

* **vw_presenca** → base consolidada de presença com atraso e validação
* **vw_indicadores_reuniao** → métricas por reunião
* **vw_indicadores_gerais** → visão consolidada
* **vw_duplicidade** → controle de múltiplos check-ins

### Métricas disponíveis:

* Total de check-ins
* Participantes únicos
* Taxa de presença válida
* Atraso médio (min)
* Primeiro e último acesso
* Duplicidade de CPF

## Arquitetura

* **Frontend:** Streamlit (Databricks Apps)
* **Backend:** Databricks SQL Warehouse
* **Storage:** Delta Tables
* **Autenticação:** Token via query param (`hash_link`)

## Estrutura do Projeto

```
.
├── app.py                # Aplicação principal
├── requirements.txt     # Dependências
├── sql/
│   ├── 01_create_tables.sql
│   ├── 02_seed_data.sql
│   ├── 03_views.sql     # Camada analítica
├── runbook.md           # Guia operacional
```

## Como executar

1. Criar as tabelas e views:

```sql
-- executar arquivos em /sql
```

2. Deploy no Databricks Apps

3. Acessar via:

```
https://<app-url>/?token=<hash_link>
```

## Segurança

* Links controlados por `hash_link`
* Possibilidade de expiração (`expira_em`)
* Desativação manual (`ativo = false`)
* Validação dupla de horário (frontend + ação)

## Casos de uso

* Monitoramento de presença em reuniões clínicas
* Controle de participação em grupos terapêuticos
* Gestão de presença em reuniões corporativas
* Acompanhamento de engajamento em sessões online

## Próximos passos

* Dashboard de presença (Databricks SQL / Power BI)
* Bloqueio de duplicidade em tempo real
* Geração automática de tokens


## Autora

Larissa Borges
