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

## Uso de Namespaces
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
- Aplicados a seletores de elementos, atributos, pseudo classes, etc.
- Não inclui ids e classes.
- Definem a aparência padrão dos elementos.

```html
a { text-decoration: none; }
input[type="text"] { border: 1px solid #ccc; }
```
### Layout
- São únicos
- Componentes maiores em um projeto.
- Divide as páginas em seções, contendo um ou mais módulos.
- Prefixo: l- ou layout-
```css
.l-header { ... }
.l-sidebar { ... }
```
### Módulos
- Contém as principais regras de estilização
- São mais específicos que  os layouts
- São isolados
- Proibido uso de ids e seletores de elementos.
- Prefixo: m- ou module-
```css
.m-card { ... }
.m-carousel { ... }
```
### Estado
- Define como um layout ou módulo se comporta sob determinada condição/estado.
- Sobrecrever ou incrementar estilos.
- É possível usar o atributo data-
- Prefixo: is-
```css
.is-collapsed { display: none; }
```
### Tema
- Como layouts e módulos devem aparentar sob determinadas condições.
- Quando o projeto quer oferecer aparência diferenciada
- Sobrescrever regras já criadas em outras categorias SMACSS
- Prefixo: t- ou theme-
```css
.t-dark .m-card { background-color: #222; color: #fff; }
```
## BEM (Block, Element, Modifier)
BEM promove o desacoplamento e reutilização de código com uma estrutura clara:
### Bloco 
- Entidade independente com seu próprio significado (.menu)
- O nome da classe é o nome do bloco

### Elemento 
- Descendente de um bloco, ajuda a formá-lo.
- São delimitados com __ (.menu__item)

### Modificador:
- Um estado diferente de um bloco ou elemento.
- Delimitados com -- (.menu__item--active)


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

### Dica prática para evitar conflitos
- Use BEM para estruturar seus componentes (modules)
- Use OOCSS para criar objetos reutilizáveis (layout, base)
- Use SMACSS para definir estados e temas (state, themes)
- Use Namespaces para dar clareza à função da classe (c-, l-, u-, is-, js-)

### Benefícios
- Código desacoplado
- Reúso automático de código
- Menos repetições
- Rápida identificação de estruturas HTML através do CSS e vice-versa
- Independência absoluta de classe
- Seletores menores e mais performáticos
- CSS mais manutenível
- Padronização do CSS

### Checklist de boas práticas
- [x] Evitar o uso de IDs em seletores CSS  
- [x] Usar classes semânticas e descritivas  
- [x] Prefira transform e opacity para animações  
- [x] Agrupar alterações no DOM para evitar reflows  
- [x] Alinhar convenções de nomenclatura para a equipe  
- [x] Usar seletores curtos e performáticos  
- [x] Separar as responsabilidades entre estilo, comportamento e estrutura  

