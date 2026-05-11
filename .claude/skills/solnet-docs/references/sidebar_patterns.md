# Padrões HTML do Sidebar

O sidebar está definido em `_layouts/default.html`. Todos os HTMLs inseridos devem seguir exatamente estes padrões.

---

## Padrão 1: Item simples dentro de um grupo existente

Quando você adiciona um novo arquivo a um módulo que já tem poucos itens (≤2 arquivos do mesmo subtema):

```html
<li><a href="{{ '/Modulo/nome_do_arquivo/' | relative_url }}">Rótulo Legível</a></li>
```

Insira dentro do `<ul class="sn-sidebar__items">` do grupo correspondente, mantendo a ordem: Visão geral → Documentação → Guia Rápido → FAQ → itens extras.

---

## Padrão 2: Grupo de módulo novo (primeiro nível)

Quando um módulo inteiro é criado:

```html
<details class="sn-sidebar__group" data-sn-group="nomemodulo">
  <summary class="sn-sidebar__group-summary">🎯 Nome do Módulo</summary>
  <ul class="sn-sidebar__items">
    <li><a href="{{ '/Modulo/' | relative_url }}">Visão geral</a></li>
    <li><a href="{{ '/Modulo/documentacao_tema/' | relative_url }}">Documentação [Tema]</a></li>
    <li><a href="{{ '/Modulo/guia_rapido/' | relative_url }}">Guia Rápido</a></li>
    <li><a href="{{ '/Modulo/faq/' | relative_url }}">FAQ</a></li>
  </ul>
</details>
```

**Atributo `data-sn-group`**: nome do módulo em lowercase, sem acentos, sem espaços. Exemplos: `financeiro`, `movimentacao`, `rh`.

**Emoji**: use os emojis estabelecidos para módulos existentes. Para módulos novos, escolha um semanticamente adequado e que não esteja em uso, e confirme com o usuário antes de commitar.

Emojis dos módulos existentes:
- 💰 Financeiro
- 🏛️ Fiscal
- 📦 Movimentação
- 👥 RH
- 🌱 Agronômico
- 🛒 Self Checkout

---

## Padrão 3: Subgrupo aninhado (segundo nível)

Use quando um tema dentro de um módulo tem **mais de 2 arquivos** (ex: 4 arquivos de Produção dentro de Movimentação).

### HTML — inserir dentro do `<ul class="sn-sidebar__items">` do módulo pai:

```html
<li class="sn-sidebar__subgroup-item">
  <details class="sn-sidebar__subgroup">
    <summary class="sn-sidebar__subgroup-summary">💡 Nome do Subtema</summary>
    <ul class="sn-sidebar__subitems">
      <li><a href="{{ '/Modulo/Subtema/' | relative_url }}">Visão geral</a></li>
      <li><a href="{{ '/Modulo/Subtema/documentacao_subtema/' | relative_url }}">Documentação</a></li>
      <li><a href="{{ '/Modulo/Subtema/guia_rapido/' | relative_url }}">Guia Rápido</a></li>
      <li><a href="{{ '/Modulo/Subtema/faq/' | relative_url }}">FAQ</a></li>
    </ul>
  </details>
</li>
```

### CSS — adicionar **uma única vez** no bloco `<style>` de `default.html` (verifique se já está presente antes de inserir):

```css
/* === Subgrupos de segundo nível no sidebar === */
.sn-sidebar__subgroup-item { list-style: none; }
.sn-sidebar__subgroup { border: none; }
.sn-sidebar__subgroup-summary {
  list-style: none;
  cursor: pointer;
  padding: 6px 20px 6px 41px;
  font-weight: 500;
  color: var(--sn-sidebar-text);
  display: flex;
  align-items: center;
  gap: 6px;
  user-select: none;
  font-size: 13px;
}
.sn-sidebar__subgroup-summary::-webkit-details-marker { display: none; }
.sn-sidebar__subgroup-summary::before {
  content: "▸";
  font-size: 9px;
  color: var(--sn-sidebar-muted);
  transition: transform 0.15s ease;
  display: inline-block;
  width: 9px;
}
.sn-sidebar__subgroup[open] > .sn-sidebar__subgroup-summary::before {
  transform: rotate(90deg);
}
.sn-sidebar__subgroup-summary:hover { background: var(--sn-sidebar-hover-bg); }
.sn-sidebar__subitems {
  list-style: none;
  margin: 0;
  padding: 2px 0 4px;
}
.sn-sidebar__subitems li { margin: 0; }
.sn-sidebar__subitems a {
  display: block;
  padding: 5px 20px 5px 60px;
  text-decoration: none;
  color: var(--sn-sidebar-text);
  border-left: 3px solid transparent;
  font-size: 13px;
  line-height: 1.35;
}
.sn-sidebar__subitems a:hover { background: var(--sn-sidebar-hover-bg); }
.sn-sidebar__subitems a.is-active {
  background: var(--sn-sidebar-active-bg);
  border-left-color: var(--sn-sidebar-accent);
  font-weight: 600;
  color: var(--sn-sidebar-accent);
}
/* === fim subgrupos === */
```

O script de ativação no final de `default.html` já percorre `sn-sidebar__items a` — os links dentro de `sn-sidebar__subitems` herdarão o comportamento de destaque automaticamente porque o script usa `closest('details.sn-sidebar__group')` para expandir o grupo pai, e o nested `<details>` abrirá junto.

---

## Onde inserir no HTML

Localize o `<details>` do módulo correto pelo atributo `data-sn-group`. Insira novos itens dentro do `<ul class="sn-sidebar__items">` desse grupo, respeitando a ordem: Visão geral sempre primeiro, depois documentação principal, guia rápido, FAQ, e itens/subgrupos extras por último.

---

## Regras gerais

- URLs seguem o padrão `{{ '/Pasta/nome_do_arquivo/' | relative_url }}` (com trailing slash — Jekyll `permalink: pretty`)
- Rótulos dos links devem ser legíveis para o suporte: use o nome da funcionalidade, não o nome do arquivo
- Quando criar subgrupo para um tema que antes tinha itens planos (ex: converter "Produção — Documentação" e "Produção — Guia Rápido" em um subgrupo "Produção"), remova os itens planos antigos e substitua pelo `<li class="sn-sidebar__subgroup-item">` aninhado
