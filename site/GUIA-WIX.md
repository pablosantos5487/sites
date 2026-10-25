# Guia rápido — Como colocar o site DaHora Açaí no Wix

Este site é um arquivo único (`index.html`) + pasta `img/` com as fotos reais da loja.
Ele **não publica sozinho no Wix** — abaixo estão os 2 caminhos possíveis, do mais rápido ao mais completo.

---

## ✅ Antes de tudo: preencha os dados reais

Abra o `index.html`, localize o bloco `CONFIG` (início do `<script>`) e preencha:

| Campo | O que colocar |
|---|---|
| `whatsappNumero` | Número oficial da loja, formato internacional, só dígitos. Ex: `"5551987654321"` (55 + DDD + número) |
| `enderecoLoja` | Endereço real da unidade (Igrejinha e/ou Parobé) |
| `horarioLoja` | Horários reais de funcionamento |
| `taxaEntrega` | Valor real da taxa, ou deixe `null` para a loja confirmar no WhatsApp |
| `limiteAcomp` | Regra real de acompanhamentos por tamanho (o cardápio confirma apenas o 1L: "até 7 liberados") |
| Preços dos **copos trufados** | Os preços de 300 ml e 400 ml estavam cortados na tela — cadaastre quando confirmar |

Não invente nenhum desses dados: o site mostra "a confirmar" até você preencher.

---

## Caminho 1 — Embutir o site no Wix (mais rápido, 10 min)

1. No editor Wix: **Adicionar → Incorporar → Embed HTML/IFrame** (Elemento "HTML personalizado").
   *Alternativa sem código:* hospede o `index.html` em qualquer hospedagem estática (Netlify, Vercel, GitHub Pages) e use o elemento **Website** (iframe) apontando para a URL.
2. Publique. O cardápio, o personalizador, o carrinho e o botão de WhatsApp já funcionam dentro do Wix.
3. Limitação: o pedido não entra no painel do Wix — ele chega pelo WhatsApp, que é exatamente o fluxo pedido no projeto.

## Caminho 2 — Reconstruir nativamente no Wix (mais integrado)

Use **Wix Stores** para catálogo + carrinho e um app de checkout por WhatsApp:

1. **Wix Stores**: cadastre as categorias (Açaí tradicional, Açaí com cupuaçu, Açaí cravejado, Copos trufados, Cupuaçu puro, Bebidas) e os produtos com as fotos da pasta `img/` e os preços transcritos.
   - Nos produtos montáveis, use **opciones/escolhas de produto** do Wix Stores para tamanhos e acompanhamentos.
2. **App de WhatsApp**: no **Wix App Market**, pesquise por "WhatsApp Checkout" / "WhatsApp cart". Instale, conecte ao seu número e teste se a mensagem leva **todos os itens, acompanhamentos e o total**.
   - ⚠️ **Confira no App Market se o app é gratuito, tem período de teste ou mensalidade** — isso muda de app para app e não pode ser presumido.
3. **Se nenhum app atender** (ex: não transmite os acompanhamentos na mensagem), use **Wix Velo**:
   - Monte o carrinho com a API `wix-stores` (`cart` / `createOrder`) e gere o link `https://wa.me/NUMERO?text=` + `encodeURIComponent(mensagem)` num evento `onClick`.
   - O modelo exato da mensagem está pronto neste site (função `finalizarWhatsApp()`) — é só portar para Velo.
4. Configure **entrega/retirada** e a taxa em Configurações de loja, para o cliente escolher no checkout.

---

## 🧪 Testes antes de publicar (obrigatórios)

Em celular **e** computador:

- [ ] Adicionar produtos, mudar quantidade, remover, carrinho vazio
- [ ] Montar açaí: etapas, limite de acompanhamentos, preço em tempo real
- [ ] Entrega × retirada (endereço exigido na entrega)
- [ ] Botão do WhatsApp abre o número certo, com acentos e quebras de linha corretas
- [ ] Totais corretos com vários itens e adicionais
- [ ] Taxa de entrega exibida conforme a regra real

## 🔎 Referências dos dados usados

- Preços e categorias: transcrição literal do cardápio oficial da loja (pedido.anota.ai — prints fornecidos).
- Instagram: [@dahoracaiteria](https://www.instagram.com/dahoracaiteria) · linktr.ee/dahoraacaiigrejinha
- Pedido mínimo exibido no cardápio: R$ 14,00 (confirmar).
- Horário exibido no cardápio: "Aberto até 18h" (confirmar).
