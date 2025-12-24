## 2025-12-24 - Kanban menu re-render blast radius
**Learning:** Um estado/prop global (ex.: `openActivityMenuId`) passado para *todos* os cards de uma lista grande amplia o “blast radius” de re-render: um clique no menu pode re-renderizar N cards sem necessidade.
**Action:** Para listas grandes, preferir props derivadas por-item (`isMenuOpen`) + `React.memo` e callbacks estáveis (useCallback) para limitar re-renders a O(1) componentes quando o estado muda.

## 2025-12-24 - O(S*N) em render no Kanban (filters/reduces por coluna)
**Learning:** Fazer `filteredDeals.filter(...)` e `reduce(...)` *dentro* do loop de colunas do Kanban cria custo O(S*N) por render e escala mal com muitos deals/estágios.
**Action:** Agrupar por `stageId` uma vez (useMemo) e ler por coluna; pré-calcular totais no mesmo passo para evitar trabalho repetido.
