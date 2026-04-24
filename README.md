# Matriz de Competências (RH)

Aplicação web auto-contida para gestão da matriz de competências da organização.

## Como abrir localmente

**Opção A — abrir ficheiro directamente:**
Duplo-clique em `index.html` (abre em qualquer browser moderno: Chrome, Edge, Firefox).

> ⚠️ **Limitação do modo `file://`:** o microfone do Assistente IA pede permissão cada vez que clicas. Para evitar isto, usa a Opção B ou publica em HTTPS (Vercel).

**Opção B — servidor local (recomendado para testar o Assistente IA):**
```bash
npm start
# ou
npx serve .
```
Depois abre `http://localhost:3000`.

## Publicar na Vercel

A app é 100% estática — não precisa de build. Qualquer um destes caminhos funciona:

### Via CLI (mais rápido)
```bash
npm install -g vercel
vercel
```
Sigue o prompt. Primeira vez pede login. Depois cria o projeto e devolve o URL.

Para publicar em produção:
```bash
vercel --prod
```

### Via dashboard web
1. Cria repositório no GitHub (ou GitLab/Bitbucket) com estes ficheiros
2. Entra em [vercel.com](https://vercel.com) → **Add New** → **Project**
3. Importa o repositório
4. Clica **Deploy** (sem configurações — é detetado como site estático)

### O que está incluído
- `vercel.json` — define `Permissions-Policy: microphone=(self)` para o Assistente IA funcionar sem re-pedir permissão
- `.gitignore` — exclui `.vercel`, `node_modules`, ficheiros temporários
- Headers de segurança: `X-Content-Type-Options`, `Referrer-Policy`, `HSTS`

## Funcionalidades

- **Dashboard** — KPIs, gráficos por departamento/site e top gaps críticos
- **Colaboradores** — lista com filtros, ficha completa ao clicar no nome (avaliações, gaps, planos)
- **Competências** — catálogo técnico e comportamental com ligação a normas ISO
- **Requisitos** — matriz de competências exigidas por função/nível
- **Matriz (heatmap)** — visão colaborador × competência com código de cor por gap
- **Avaliações** — registo com peso, nível atual/esperado, plano, responsável, prazo
- **Planos** — lista de planos de desenvolvimento com estado
- **Nine-Box** — grid Performance × Potencial
- **Evolução** — histórico temporal (snapshots)
- **Admin** — configuração, utilizadores, backup, integração Supabase (opcional)
- **Assistente IA** — chat por voz ou texto (só Admin) que:
  - Abre fichas de colaboradores ("mostra o João")
  - Regista avaliações ("Maria em Liderança é excelente")
  - Dá sugestões ("sugestões para o Pedro")
  - Lista top gaps, resumos gerais, info de departamentos
- **Import/Export xlsx** — importa matriz existente, exporta snapshot com 3 planilhas

## Utilizadores demo

| Papel | Email | Senha |
|-------|-------|-------|
| Admin | admin@empresa.pt | admin123 |
| Coordenador | coord@empresa.pt | coord123 |
| Utilizador | user@empresa.pt | user123 |

> **Importante:** altera estas credenciais em Admin > Utilizadores antes de publicar em produção.

## Escala de avaliação

- **Nível atual / esperado:** 0 (não aplica) → 5 (especialista)
- **Gap = Esperado − Atual:** 0 (sem gap) → 4+ (gap crítico)
- **Score = Peso × Atual / 5**

## Stack técnica

- **Frontend:** React 18 (via CDN UMD) + htm para JSX sem build
- **UI:** Tailwind CSS (CDN)
- **Gráficos:** Chart.js 4
- **Importação/exportação:** SheetJS (xlsx), jsPDF, html2canvas
- **Persistência:** localStorage (cliente), opcional Supabase (configurável em Admin)
- **Voz:** Web Speech API (reconhecimento pt-PT + síntese)

## Próximos passos sugeridos

- Backend real (Node/Python + PostgreSQL) com autenticação
- Hashing de passwords (bcrypt/Argon2)
- App móvel para avaliação em campo
- Integração RH/ERP
- LLM externo para IA mais conversacional
