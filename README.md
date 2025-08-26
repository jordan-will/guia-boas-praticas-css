# Diretrizes para o uso de CSS eficiente em projetos
**Baseado no livro CSS Eficiente, da Casa do Código**

Este documento apresenta diretrizes práticas para escrever CSS de forma eficiente, utilizando conceitos das metodologias **OOCSS**, **SMACSS**, **BEM** e **CSS Namespaces**. As recomendações são flexíveis e podem ser adaptadas ao contexto de cada projeto.

## Princípios do CSS Orientado a Objetos (OOCSS)

- Separar estrutura (layout) da aparência (estilo visual)
- Criar variações visuais com pouco código
- Separar containers de conteúdo
- Evitar estilos dependentes de localização
- Um objeto deve manter sua aparência em qualquer contexto
- Reutilização extensiva de código
- Redução de reflow e repaint para melhor performance

**Exemplo:**
```css
.o-box {
  padding: 16px;
  border: 1px solid #ccc;
}

.t-dark {
  background-color: #333;
  color: #fff;
}
```

### Uso de Namespaces
Namespaces são prefixos que indicam a função de uma classe no CSS. Eles facilitam a leitura e manutenção do código.

Prefixo	Significado	Uso
```plaintext
o-:	Objeto, estrutura reutilizável
c-:	Componente, elementos de UI
u-:	Utilitário, estilos globais e imutáveis
t-:	Tema, estilos condicionais por tema
s-:	Escopo, regras específicas e aninhadas
is- / has-:	Estado, condições temporárias na UI
js-: JavaScript, elementos com interação JS, classe  sem estilos
qa-: Quality Assurance, classes para testes automatizados
```
**Exemplo**
```html
<button class="c-btn u-text-center is-active js-toggle">Clique</button>
```
##  SMACSS
SMACSS propõe uma categorização clara para organizar o CSS

### Base
- Regras padrão aplicadas a elementos HTML
- Não usa classes ou IDs
```html
a { text-decoration: none; }
input[type="text"] { border: 1px solid #ccc; }
```
### Layout
- Estrutura geral da página
- Divide em seções principais
- Prefixo: l- ou layout-
```css
.l-header { ... }
.l-sidebar { ... }
```
### Módulos
- Componentes reutilizáveis
- Isolados e específicos
- Prefixo: m- ou module-
```css
.m-card { ... }
.m-carousel { ... }
```
### Estado
- Estilos condicionais
- Prefixo: is-
```css
.is-collapsed { display: none; }
```
### Tema
- Aparência alternativa para módulos/layouts
- Sobrescreve estilos existentes
```css
.t-dark .m-card { background-color: #222; color: #fff; }
```
## BEM (Block, Element, Modifier)
BEM promove o desacoplamento e reutilização de código com uma estrutura clara:
- Bloco: Entidade independente (.menu)
- Elemento: Parte do bloco (.menu__item)
- Modificador: Variação de estilo (.menu__item--active)

**Exemplo**
```html
<nav class="menu menu--vertical">
  <ul class="menu__list">
    <li class="menu__item menu__item--active">Início</li>
  </ul>
</nav>
```
### Estrutura de Arquivos CSS recomendada
```plaintext
/style
  /base     → Estilos padrão
  /layout   → Estrutura da página
  /modules  → Componentes reutilizáveis
  /state    → Classes utilitárias
  /themes   → Estilos condicionais
  app.scss    
```


### Checklist de boas práticas
[x] Evitar o uso de IDs em seletores CSS
[x] Usar classes semânticas e descritivas
[x] Prefira transform e opacity para animações
[x] Agrupar alterações no DOM para evitar reflows
[x] Alinhar convenções de nomenclatura para a equipe
[x] Usar seletores curtos e performáticos
[x] Separar as responsabilidades entre estilo, comportamento e estrutura
