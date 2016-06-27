# Угода щодо іменування

Для роботи з [БЕМ-сутностями](../key-concepts/key-concepts.uk.md#БЕМ-сутність) необхідно ознайомитися з правилами їх іменування.

Основна ідея угоди щодо іменування — зробити імена CSS селекторів максимально інформативними і зрозумілими. Це допоможе [спростити розробку](../solved-problems/solved-problems.uk.md#Як-спростити-код-і-полегшити-рефакторинг) і [отладку](../solved-problems/solved-problems.uk.md#Як-почати-повторно-використовувати-код-і-уникнути-взаємного-впливу-компонентів-один-на-одного) коду, а також вирішити деякі [проблеми](../solved-problems/solved-problems.uk.md#Як-отримати-самодокументируемый-код) веб-розробників.

В якості прикладу розглянемо CSS-селектор `menuitemvisible`. Швидкий перегляд такого запису не дає можливості визначити типи БЕМ-сутностей по імені.

Додамо роздільник:

`menu-item-visible` або `menuItemVisible`

У такому вигляді ім'я селектора явно поділяється на логічні частини. Можемо припустити, що `menu` виявиться блоком, `item` — елементом, а `visible` — модифікатором. Однак у реальному житті часто виникають більш складні і не настільки однозначні випадки, вирішити які допомагає угоду щодо іменування БЕМ.

БЕМ-методологія надає ідею по створенню правил формування імен і свій спосіб її реалізації — [угода щодо іменування CSS селекторів](#Угода-щодо-іменування-css-селекторів). Однак у світі веб-розробки існує ряд [альтернативних схем](#Альтернативні-схеми-іменування), заснованих на принципах БЕМ.

## Угода щодо іменування CSS селекторів

* Імена БЕМ-сутностей записуються з допомогою **цифр** і **латинських літер** **нижньому регістрі**.
* Для розділення слів в іменах використовується **дефіс** (`-`).
* Для зберігання інформації про імена блоків, елементів і модифікаторів використовуються **CSS-класи**.

Правила формування імен:

* [блоків](#Ім'я-блоку)
* [елементів](#Ім'я-елемента)
* [модифікаторів](#Ім'я-модифікатора)

### Ім'я блоку

Ім'я блоку формується за схемою `block-name` і задає [простір імен](https://uk.wikipedia.org/wiki/Простір_імен) елементів і модифікаторів.

Іноді до імен блоків можуть додаватися різні префікси. Детальніше про наш досвід використання префіксів розповідається в статті [Історія створення БЕМ](../history/history.uk.md#Поява-блоків).

**Приклад**

`menu`

`lang-switcher`

*HTML*

```html
<div class="menu">...</div>
```

*CSS*

```css
.menu { color: red; }
```

### Ім'я елемента

Простір імен, заданий ім'ям блоку, визначає належність елемента до цього блоку. Ім'я елемента відокремлюється від імені блоку двома підкресленнями (`__`).

Повне ім'я елемента створюється за схемою:

`block-name__elem-name`

Якщо блок має кілька однакових елементів, як у випадку пунктів меню, то всі вони будуть мати однакові імена `menu__item`.

_________________________________________

**Важливо!** У методології БЕМ [не існує елементів элементов](../../faq/faq.ru.md#Почему-в-БЭМ-не-рекомендуется-создавать-элементы-элементов-block__elem1__elem2).
_________________________________________

**Приклад**

`menu__item`

`lang-switcher__lang-icon`

*HTML*

```html
<div class="menu">
  ...
  <span class="menu__item"></span>
</div>
```

*CSS*

```css
.menu__item { color: red; }
```

### Ім'я модифікатора

Простір імен, заданий ім'ям блоку, визначає приналежність модифікатора до цього блоку або його елементу. Ім'я модифікатора відокремлюється від імені блоку або елемента одним підкресленням (`_`).

Повне ім'я модифікатора створюється за схемою:

* Для булевых модификаторов — `owner-name_mod-name`.

* Для модификаторов вида «ключ-значение» — `owner-name_mod-name_mod-val`.

_________________________________________________

**Важливо!** У методології БЕМ [модифікатор не може використовуватися у відриві від свого власника](../../faq/faq.uk.md#Навіщо-писати-ім'я-блоку-в-іменах-модифікаторів-і-елементів).
_________________________________________________

#### Модифікатор блоку

* **Булевий модифікатор**.

Значення такого модифікатора не вказується. Повне ім'я створюється за схемою:

`block-name_mod-name`.

**Приклад**

`menu_hidden`

* **Модифікатор типу «ключ — значення»**.

Значення модифікатора відокремлюється від імені одним підкресленням (`_`). Повне ім'я створюється за схемою:

`block-name_mod-name_mod-val`.

**Приклад**

`menu_theme_morning-forest`

*HTML*

```html
<div class="menu menu_hidden">...</div>
<div class="menu menu_theme_morning-forest">...</div>
```

>*Неправильна форма запису*

>```html
<div class="menu_hidden">...</div>
>```

>У даному випадку запис відсутній сам блок, на який впливає модифікатор.

*CSS*

```css
.menu_hidden { display: none }
.menu_theme_morning-forest { color: green; }
```

#### Модифікатор елемента

* **Булевий модифікатор**.

Значення такого модифікатора не вказується. Повне ім'я створюється за схемою:

`block-name__elem-name_mod-name`.

**Приклад**

`menu__item_visible`

* **Модифікатор типу «ключ — значення»**.

Значення модифікатора відокремлюється від імені одним підкресленням (`_`). Повне ім'я створюється за схемою:

`block-name__elem-name_mod-name_mod-val`.

**Приклад**

`menu__item_type_radio`

*HTML*

```html
<div class="menu">
  ...
  <span class="menu__item menu__item_visible menu__item_type_radio"></span>
</div>
```

*CSS*

```css
.menu__item_type_radio { color: blue; }
```

## Приклад використання угоди щодо іменування

Реалізація форми аутентифікації в HTML і CSS:

*HTML*

```html
<form class="form form_login form_theme_forest">
  <input class="form__input">
  <input class="form__submit form__submit_disabled">
</form>
```

*CSS*

```css
.form {}
.form_theme_forest {}
.form_login {}
.form__input {}
.form__submit {}
.form__submit_disabled {}
```

## Альтернативні схеми іменування

Існують альтернативні рішення, засновані на угоді по іменування БЕМ.

### Стиль Гаррі Робертса

Одним з перших, хто заговорив про БЕМ в англомовному світі, був [Гаррі Робертс](http://csswizardry.com/work/). У своїй статті [MindBEMding–getting your head 'round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) він розповів про угоду щодо іменування CSS-класів за БЕМ-методології. Гаррі Робертс запропонував свою схему іменування, засновану на принципах БЕМ:

`block-name__elem-name--mod-name`

* Імена записуються в нижньому регістрі.
* Для розділення слів в іменах БЕМ-сутностей використовується дефіс (`-`).
* Ім'я елемента відокремлюється від імені блоку за допомогою двох підкреслень (`__`).
* Булеві модифікатори відокремлюються за допомогою двох дефісів (`--`).
* Модифікатори виду «ключ-значення» не використовуються.

### Стиль CamelCase

`MyBlock__SomeElem_modName_modVal`

Цей стиль відрізняється від класичного використанням [CamelCase](https://uk.wikipedia.org/wiki/Верблюжий_регістр замість дефіса для розділення слів в іменах БЕМ-сутностей.

### Стиль без підкреслень

`blockName-elemName--modName--modVal`

* Для запису імен використовується CamelCase.
* Ім'я елемента відокремлюється від імені блоку з допомогою одного дефісу (`-`).
* Для відділення модифікатора використовується два дефіса (`--`).
* Значення модифікатора відокремлюється від його імені з допомогою двох дефісів (`--`).

### Стиль No-namespace

`_available`

Основна відмінність даного стилю у відсутності імені блоку та/або елемента перед модифікатором. Така схема накладає обмеження на використання [міксів](../key-concepts/key-concepts.uk.md#Мікс), так як не дає можливості визначити, до якого блоку/елементу відноситься модифікатор.

## Який стиль вибрати

Методологія БЕМ пропонує загальні принципи іменування БЕМ-сутностей. Вибір схеми іменування залежить від вимог вашого проекту та особистих уподобань. Использование предложенного методологией [соглашения по именованию](#Угода-щодо-іменування-css-селекторів) имеет один существенный плюс — наличие готовых инструментов для разработки, которые ориентируются именно на «классическое именование».

Крім цього, БЕМ-методологія не обмежується використанням технологій HTML і CSS, розглянутих у цьому документі. Поняття блоків, елементів і модифікаторів застосовуються при роботі з JavaScript, шаблонами і файловою системою БЕМ-проекту. Інструмент [bem-naming](https://uk.bem.info/toolbox/sdk/bem-naming/) дозволяє застосовувати однакові імена БЕМ-сутностей у всіх використовуваних [технологіях реалізації](../key-concepts/key-concepts.uk.md#Технологія-реалізації).

За замовчуванням `bem-naming` містить налаштування угоди щодо іменування, запропонованого методологією, але дозволяє додавати правила для використання альтернативних схем.