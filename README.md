# SDK Playground (Ambiente Profissional de Testes)

Monorepo para testar QUALQUER SDK em um cenário de e-commerce (login, checkout, dados sensíveis).

## Estrutura
- `apps/backend` — API Node.js/Express (TS) com Postgres/Redis.
- `apps/frontend` — Loja em React + Vite + Tailwind.
- `apps/dashboard` — Painel (Next.js) para visualizar eventos/logs de SDKs.
- `sdks/` — SDKs plugáveis (ex.: risk-sdk e web-collector de exemplo).
- `docker/` — `docker-compose.yml` com Postgres e Redis.

## Rodando sem Docker (dev rápido)
```bash
yarn
yarn dev:api
# em outro terminal
yarn dev:web
# opcional (dashboard)
yarn dev:dash
```

## Rodando com Docker
```bash
docker compose -f docker/docker-compose.yml up -d
# Em outro terminal, rode a API e o Front localmente (ou dockerize se preferir)
```

## Como plugar seu SDK
- **Backend:** exponha um arquivo em `sdks/<meu-sdk>/server/index.ts` exportando `middleware(req,res,next)`.
- **Frontend:** exponha `sdks/<meu-sdk>/web/index.ts` com `initSDK()` opcional para coleta.
- A API carrega middlewares dinamicamente de todos os diretórios em `sdks/*/server`.
- O Front tem um loader opcional de SDKs web em `src/sdkLoader.ts`.
