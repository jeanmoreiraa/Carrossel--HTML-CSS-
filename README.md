# Como Criar um Carrossel com HTML e CSS

Vou explicar como criar um carrossel de imagens semelhante ao dos arquivos compartilhados. Este carrossel tem uma estrutura simples, com imagens que deslizam horizontalmente e botões de navegação.

## Estrutura HTML Básica

1. Crie a estrutura básica do carrossel:
   - Um container principal com classe "carrossel"
   - Botões de navegação (esquerda e direita)
   - Um container para imagens
   - Imagens individuais com classe "imagem"

```html
<div class="carrossel">
  <div class="botao flex esquerda">&#10094;</div>
  <div class="botao flex direita">&#10095;</div>
  
  <div class="container">
    <div class="imagens flex">
      <div class="imagem flex">
        <img src="imagem1.webp" alt="Descrição 1" />
      </div>
      <div class="imagem flex emfoco">
        <img src="imagem2.webp" alt="Descrição 2" />
      </div>
      <div class="imagem flex">
        <img src="imagem3.webp" alt="Descrição 3" />
      </div>
      <!-- Mais imagens conforme necessário -->
    </div>
  </div>
</div>
```

## Estilização com CSS

1. **Configuração inicial**: Primeiro, defina estilos gerais:
   ```css
   * {
     padding: 0;
     margin: 0;
     box-sizing: border-box;
   }

   html {
     font-size: 62.5%; /* Permite usar rem com base em 10px */
   }

   body {
     font-family: 'Montserrat', sans-serif;
     font-size: 1.6rem;
   }
   ```

2. **Classe flex utilitária**: Crie classes para flexbox:
   ```css
   .flex {
     display: flex;
   }
   .flex.wrap {
     flex-flow: row wrap;
   }
   .flex.col {
     flex-flow: column;
   }
   ```

3. **Estrutura do carrossel**:
   ```css
   .carrossel {
     position: relative;
     max-width: 100rem;
   }

   .carrossel .container {
     overflow: hidden; /* Oculta conteúdo que ultrapassar os limites */
   }

   .carrossel .imagens {
     gap: 0.82rem;
     width: max-content; /* Permite que as imagens fiquem lado a lado */
   }
   ```

4. **Estilização das imagens**:
   ```css
   .carrossel .imagem {
     position: relative;
     width: calc((100rem - (2 * 0.82rem)) / 3); /* Distribui 3 imagens por vez */
     justify-content: center;
     align-items: center;
     overflow: hidden;
     aspect-ratio: 1/1; /* Imagens quadradas */
     border-radius: 1.5rem;
   }

   /* Efeito das imagens que não estão em foco */
   .carrossel .imagem::after {
     content: '';
     position: absolute;
     width: 100%;
     height: 100%;
     background-color: rgba(255, 255, 255, 0.6);
     backdrop-filter: blur(2px);
   }

   /* Imagem em foco não tem efeito blur */
   .carrossel .imagem.emfoco::after {
     background-color: transparent;
     backdrop-filter: none;
   }
   
   .carrossel .imagem img {
     height: 100%;
   }
   ```

5. **Botões de navegação**:
   ```css
   .carrossel .botao {
     position: absolute;
     background-color: #303030;
     color: white;
     border-radius: 0.8rem;
     width: 3rem;
     height: 3rem;
     justify-content: center;
     align-items: center;
     z-index: 1;
     top: 50%;
     cursor: pointer;
     box-shadow: 0 0 0.4rem rgba(0, 0, 0, 0.2);
   }

   .carrossel .botao.esquerda {
     transform: translate(-50%, -50%);
   }

   .carrossel .botao.direita {
     right: 0;
     transform: translate(50%, -50%);
   }
   ```

## Resumo dos Conceitos-Chave

1. **Container com overflow: hidden** - Limita a exibição apenas às imagens visíveis
2. **Imagens em width: max-content** - Permite que todas as imagens fiquem lado a lado horizontalmente
3. **Posicionamento relativo/absoluto** - Para botões de navegação e efeitos de sobreposição
4. **Classe "emfoco"** - Destaca a imagem central removendo o efeito de blur
5. **Cálculo responsivo de largura** - Para que as imagens se ajustem ao tamanho do container

## Observações Finais

Este código HTML/CSS cria a estrutura visual do carrossel, mas não inclui a funcionalidade de navegação. Para tornar o carrossel funcional, você precisaria adicionar JavaScript para manipular os cliques nos botões e fazer o deslocamento das imagens.

A classe "emfoco" é aplicada manualmente no HTML à imagem que deve estar destacada. Em uma implementação completa com JavaScript, essa classe seria adicionada/removida dinamicamente conforme o usuário navega pelas imagens.
