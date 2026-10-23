# Estoque Fácil — Controle de Estoque para Pequenas Lojas

Painel administrativo em **Next.js (App Router) + TypeScript + Tailwind + Prisma + PostgreSQL**.

## Funcionalidades

- Cadastro, edição e exclusão de produtos (com confirmação)
- Preços armazenados em **centavos** (inteiros) e exibidos em R$
- Entradas e saídas de estoque (transacionais, sem saldo negativo)
- Estoque mínimo por produto e alerta de estoque baixo
- Valor financeiro total do estoque
- Histórico de movimentações, relatórios e exportação CSV
- Interface em pt-BR, responsiva, com skeletons, toasts e estados de erro/vazio

## Como executar

Pré-requisitos: Node.js 20+ e uma conta gratuita no Neon (https://neon.tech).

```bash
npm install
cp .env.example .env      # depois edite o .env com as URLs do Neon
npx prisma migrate deploy
npm run db:seed
npm run dev
```

Acesse http://localhost:3000.

## Banco de dados

Tabela `produtos`: `id`, `nome` (varchar 80), `precoCentavos`, `quantidade` (padrão 0), `estoqueMinimo` (padrão 5), `criadoEm`.

A migration `20260101000001_restricoes` adiciona restrições que o Prisma não expressa:
preço `> 0`, quantidade `>= 0`, estoque mínimo `>= 0` e nome não vazio.
A tabela `movimentacoes` guarda o histórico (entrada/saída, saldo anterior e novo).

## Estrutura

```
prisma/            schema, migrations e seed
src/app/api/       rotas: produtos, movimentar, movimentacoes, resumo
src/app/           páginas: painel, produtos, histórico, relatórios
src/components/    UI, layout e módulos de produtos
src/lib/           Prisma, validações Zod, formatação pt-BR
```

## Scripts

`npm run dev` · `npm run build` · `npm run typecheck` · `npm run db:studio`
