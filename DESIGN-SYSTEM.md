# Reset Primal - Design System

**Versao:** 1.0
**Data:** 10 de fevereiro de 2026
**Status:** Production Ready

---

## Paleta de Cores

### Cores Primarias
| Nome | Hex | RGB | Uso |
|------|-----|-----|-----|
| Dark Navy | `#1e3c72` | rgb(30, 60, 114) | Headers, buttons primarios |
| Navy Medium | `#2a5298` | rgb(42, 82, 152) | Hero gradient, accents |
| Dark Brown/Gray | `#2c3e50` | rgb(44, 62, 80) | Text body |

### Cores de Status
| Nome | Hex | RGB | Uso |
|------|-----|-----|-----|
| Red/Alert | `#e74c3c` | rgb(231, 76, 60) | CTA buttons, warnings, alerts |
| Green/Success | `#28a745` | rgb(40, 167, 69) | Success boxes, positive results |
| Warning/Yellow | `#ffc107` | rgb(255, 193, 7) | Warning boxes, scarcity |
| Danger | `#dc3545` | rgb(220, 53, 69) | Critical alerts |

### Cores Neutras
| Nome | Hex | RGB | Uso |
|------|-----|-----|-----|
| Background Light | `#f8f9fa` | rgb(248, 249, 250) | Page backgrounds |
| Background White | `#ffffff` | rgb(255, 255, 255) | Cards, sections |
| Border Gray | `#ced4da` | rgb(206, 212, 218) | Input borders |
| Text Light Gray | `#6c757d` | rgb(108, 117, 125) | Secondary text |

### Gradientes
- **Hero Gradient:** `linear-gradient(135deg, #1e3c72 0%, #2a5298 100%)`
- **Offer Gradient:** `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- **Final CTA Gradient:** `linear-gradient(135deg, #1e3c72 0%, #2a5298 100%)`

---

## Tipografia

### Familia de Fontes
```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
```

### Escalas de Tamanho
| Elemento | Tamanho | Peso | Line Height | Uso |
|----------|---------|------|-------------|-----|
| H1 (Hero) | 42px | 800 | 1.2 | Headline principal |
| H2 (Section) | 32px | 700 | 1.3 | Titulos de secao |
| H3 (Subtitle) | 24px | 700 | 1.4 | Subtitulos |
| H4 (Card Title) | 20px | 700 | 1.5 | Titulos de cards |
| Body Text | 18px | 400 | 1.6 | Texto principal |
| Small Text | 16px | 400 | 1.6 | Texto secundario |
| Extra Small | 14px | 400 | 1.5 | Rodape, notas |

### Subheadline (Hero)
- Tamanho: 20px
- Peso: 400
- Opacity: 0.95
- Line Height: 1.6

---

## Componentes

### Botoes

#### CTA Button (Principal)
```css
background: #e74c3c;
color: white;
padding: 20px 40px;
font-size: 20px;
font-weight: 700;
border-radius: 8px;
box-shadow: 0 4px 15px rgba(231, 76, 60, 0.3);
transition: transform 0.2s, box-shadow 0.2s;

&:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(231, 76, 60, 0.4);
}
```

#### Botao Secundario (Email)
```css
background: #1e3c72;
color: white;
padding: 15px 30px;
border-radius: 6px;
font-weight: 600;
cursor: pointer;
```

### Secoes

#### Card/Section
```css
background: white;
padding: 40px 30px;
margin-bottom: 30px;
border-radius: 12px;
box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
```

#### Offer Box (Gradient)
```css
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
color: white;
padding: 40px;
border-radius: 12px;
margin: 40px 0;
```

#### Guarantee Box (Green)
```css
background: #d4edda;
border: 2px solid #28a745;
padding: 30px;
border-radius: 12px;
margin: 30px 0;
```

#### Scarcity Box (Warning)
```css
background: #fff3cd;
border-left: 4px solid #ffc107;
padding: 20px;
margin: 30px 0;
border-radius: 8px;
```

#### Warning/Alert Box (Red)
```css
background: #f8d7da;
color: #721c24;
border-left: 4px solid #dc3545;
padding: 20px;
border-radius: 8px;
```

### Listas

#### Problem List
```css
list-style: none;
margin: 20px 0;

li {
  padding: 12px 0 12px 30px;
  position: relative;
  font-size: 18px;

  &:before {
    content: "→";
    position: absolute;
    left: 0;
    color: #e74c3c;
    font-weight: bold;
  }
}
```

#### Mechanism List (Numerada)
```css
list-style: none;
counter-reset: mechanism-counter;

li {
  counter-increment: mechanism-counter;
  padding: 15px 0 15px 50px;
  position: relative;
  font-size: 17px;
  margin: 15px 0;

  &:before {
    content: counter(mechanism-counter);
    position: absolute;
    left: 0;
    top: 10px;
    background: #1e3c72;
    color: white;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
  }
}
```

### Testimonials

#### Testimonial Card
```css
background: #f8f9fa;
padding: 25px;
margin: 20px 0;
border-radius: 8px;
border-left: 4px solid #1e3c72;

.testimonial-avatar {
  width: 50px;
  height: 50px;
  background: #1e3c72;
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  font-weight: bold;
  margin-right: 15px;
}

.testimonial-name {
  font-weight: 700;
  font-size: 18px;
}

.testimonial-result {
  color: #28a745;
  font-weight: 600;
  font-size: 16px;
}

.testimonial-text {
  font-size: 16px;
  line-height: 1.6;
  font-style: italic;
}
```

### Formularios

#### Input Field
```css
padding: 15px;
border: 1px solid #ced4da;
border-radius: 6px;
font-size: 16px;
width: 100%;
margin-bottom: 10px;

&:focus {
  outline: none;
  border-color: #1e3c72;
  box-shadow: 0 0 0 3px rgba(30, 60, 114, 0.1);
}
```

#### Form Success Message
```css
background: #d4edda;
color: #155724;
padding: 15px 20px;
border-radius: 8px;
text-align: center;
font-weight: 600;
```

#### Form Error Message
```css
background: #f8d7da;
color: #721c24;
padding: 15px 20px;
border-radius: 8px;
text-align: center;
font-weight: 600;
```

---

## Espacamento

### Padding/Margin Scale
| Tamanho | Pixels | Uso |
|---------|--------|-----|
| xs | 5px | - |
| sm | 10px | - |
| md | 15px | Interno de inputs |
| lg | 20px | Padding de cards |
| xl | 30px | Padding de sections |
| 2xl | 40px | Padding de sections grandes |

### Gap
- Entre elementos: 10px
- Entre secoes: 30px
- Entre lista items: 15px

---

## Sombras

```css
/* Light Shadow (Cards) */
box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);

/* Button Shadow */
box-shadow: 0 4px 15px rgba(231, 76, 60, 0.3);

/* Button Hover Shadow */
box-shadow: 0 6px 20px rgba(231, 76, 60, 0.4);
```

---

## Border Radius

| Elemento | Radius |
|----------|--------|
| Buttons | 8px |
| Cards/Sections | 12px |
| Inputs | 6px |
| Avatars | 50% (circular) |
| Alert Boxes | 8px |

---

## Responsive Breakpoints

```css
/* Mobile */
@media (max-width: 600px) {
  h1 { font-size: 32px; }
  .section { padding: 30px 20px; }
  .container { padding: 20px; }
}
```

---

## Transicoes

```css
/* Default Transition */
transition: transform 0.2s, box-shadow 0.2s;

/* Button Hover Effect */
transform: translateY(-2px);
```

---

## Container

```css
.container {
  max-width: 720px;
  margin: 0 auto;
  padding: 20px;
}
```

---

## Hero Section

```css
background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
color: white;
padding: 60px 20px 40px;
text-align: center;
border-radius: 0 0 20px 20px;
margin-bottom: 40px;
```

---

## Footer

```css
text-align: center;
padding: 40px 20px;
color: #6c757d;
font-size: 14px;

p {
  margin: 10px 0;
}
```

---

## Prototipo/Referencia

**Landing Page URL:** `https://aamaro1978.github.io/reset-primal-landing/sales.html`

**Componentes em Uso:**
- Hero Section com Timer Countdown
- Problem/Agitation Section
- Offer Box com Pricing
- Scarcity Counter
- Mechanism Box (Como Funciona)
- Testimonials Grid
- Guarantee Box
- FAQ Section
- Email Capture Form
- Final CTA Section
- Footer

---

## Notas Para o Squad

1. **Cores Secundarias:** Gradientes sao usados em sections importantes (Hero, Offer, Final CTA)
2. **Tipografia:** Sem serifs, alinhada com design moderno e mobile-first
3. **Espacamento:** Consistente em 10px grid (multiples de 10)
4. **Acessibilidade:** Contraste minimo AA verificado (preto sobre cores, branco sobre gradientes)
5. **Performance:** Shadow CSS, nao imagens (render mais rapido)
6. **Botoes:** Sempre com hover state (transform + shadow)

---

**Proximo Passo:** Implementar em componentes React/Vue com Tailwind CSS ou CSS Modules

