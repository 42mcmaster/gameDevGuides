# Pac-Man на C# — посібник зі створення гри

Цей посібник доповнює [відеоурок MOO ICT про гру Pac-Man](https://www.youtube.com/watch?v=zM8xPtzI8z0). Ви створите гру Pac-Man мовою C# у Visual Studio за допомогою Windows Forms.

Використовуйте відео і цей посібник разом. Відео показує, куди натискати і як усе має виглядати. У посібнику є код для кожної частини, пояснення, що робить цей код, і вказівки, як перевірити роботу, перш ніж переходити далі.

> Назви кнопок, меню й налаштувань подано англійською, так само як вони виглядають у Visual Studio. Код теж англійською.

**Чого ви навчитеся**

- Як програма реагує на **події** (events): натискання клавіші, клацання кнопки або тік таймера
- Як працює **ігровий цикл** (game loop): таймер, який запускає ваш код приблизно 50 разів на секунду
- Як працюють позиції на екрані (**Left** і **Top**)
- Як визначити, що два об'єкти торкнулися (**зіткнення**, collision)
- Як використовувати **списки** і **цикли**, щоб працювати з багатьма об'єктами одночасно
- Як написати **клас** і створити з нього кілька **об'єктів** (чотирьох привидів)

---

## Зміст

- [Перш ніж почати](#перш-ніж-почати)
- [Як читати код C#](#як-читати-код-c)
- [Розділ 1: Створення форми](#розділ-1-створення-форми)
  - [Частина 1: Створення проєкту](#частина-1-створення-проєкту)
  - [Частина 2: Налаштування форми](#частина-2-налаштування-форми)
  - [Частина 3: Стіни](#частина-3-стіни)
  - [Частина 4: Додавання Pac-Man](#частина-4-додавання-pac-man)
  - [Частина 5: Монети](#частина-5-монети)
  - [Частина 6: Ігровий таймер](#частина-6-ігровий-таймер)
  - [Частина 7: Стартове меню](#частина-7-стартове-меню)
  - [Частина 8: Підключення подій](#частина-8-підключення-подій)
- [Розділ 2: Код для Pac-Man](#розділ-2-код-для-pac-man)
  - [Частина 9: Файл класу Ghost](#частина-9-файл-класу-ghost)
  - [Частина 10: Змінні гри](#частина-10-змінні-гри)
  - [Частина 11: Порожні методи](#частина-11-порожні-методи)
  - [Частина 12: Метод SetUp](#частина-12-метод-setup)
  - [Частина 13: Керування з клавіатури](#частина-13-керування-з-клавіатури)
  - [Частина 14: Рух Pac-Man і кнопка запуску](#частина-14-рух-pac-man-і-кнопка-запуску)
  - [Частина 15: Перехід через краї екрана](#частина-15-перехід-через-краї-екрана)
  - [Частина 16: Зупинка біля стін](#частина-16-зупинка-біля-стін)
  - [Частина 17: Збирання монет](#частина-17-збирання-монет)
- [Розділ 3: Клас Ghost](#розділ-3-клас-ghost)
  - [Частина 18: Змінні привида](#частина-18-змінні-привида)
  - [Частина 19: Конструктор привида](#частина-19-конструктор-привида)
  - [Частина 20: Створення чотирьох привидів](#частина-20-створення-чотирьох-привидів)
  - [Частина 21: Рух привидів](#частина-21-рух-привидів)
  - [Частина 22: Привиди залишаються в лабіринті](#частина-22-привиди-залишаються-в-лабіринті)
  - [Частина 23: Режим переслідування](#частина-23-режим-переслідування)
- [Розділ 4: Завершення гри](#розділ-4-завершення-гри)
  - [Частина 24: Скидання привидів](#частина-24-скидання-привидів)
  - [Частина 25: Кінець гри](#частина-25-кінець-гри)
  - [Частина 26: Зіткнення з привидом і перемога](#частина-26-зіткнення-з-привидом-і-перемога)
- [Усунення проблем](#усунення-проблем)
- [Спробуйте ще](#спробуйте-ще)
- [Основні терміни](#основні-терміни)

---

## Перш ніж почати

### Що потрібно

- Комп'ютер з **Windows**. Windows Forms не працює на Mac або Chromebook.
- **Visual Studio** (вже встановлено на комп'ютерах у класі). Якщо хочете працювати вдома, можна безкоштовно завантажити **Visual Studio Community**. Під час встановлення позначте **.NET desktop development**.
- **Зображення для гри**: Pac-Man, повернутий ліворуч, праворуч, угору і вниз (анімовані GIF), чотири привиди (червоний, синій, жовтий, рожевий) і монета. Mr. McMaster скаже, де їх узяти. Збережіть їх у папку, яку легко знайти.

### Як користуватися цим посібником

1. Перегляньте одну частину відео.
2. Зробіть цю частину. Перевіряйте свій код за посібником.
3. На кожній **контрольній точці** (✅) запускайте гру й перевіряйте, що все працює, перш ніж іти далі. Одну маленьку помилку виправити набагато легше, ніж десять наприкінці.

### Правила, які заощадять час

- **C# розрізняє великі й малі літери.** `pacman`, `Pacman` і `PacMan` — це три різні назви.
- **Назви мають збігатися точно.** Якщо в дизайнері ви назвали щось `gameTimer`, то й у коді має бути `gameTimer`.
- **Часто зберігайте** роботу комбінацією **Ctrl+S**.
- Автор відео іноді називає речі трохи інакше, ніж у цьому посібнику. Підходить будь-яка назва. Просто виберіть одну і використовуйте її всюди.

У цьому посібнику використано такі назви:

| Елемент на формі | Назва (Name) | Інші налаштування |
|---|---|---|
| PictureBox для Pac-Man | `pacman` | Size 50, 50 |
| Ігровий таймер | `gameTimer` | Interval 20, Enabled False |
| Панель меню | `pnlMenu` | |
| Кнопка Play | `btnStart` | |
| Напис з інструкціями / рахунком | `lblInfo` | |

---

## Як читати код C#

Щоб зробити цю гру, не потрібно вивчати всю мову C#, але ці частини трапляються всюди. Якщо ви знайомі з Python, в останньому стовпці показано відповідник на Python.

| C# | Що це означає | Python |
|---|---|---|
| `int score = 0;` | Створити змінну для цілого числа з назвою `score`, яка починається з 0 | `score = 0` |
| `bool goLeft;` | Створити змінну «так/ні» (true/false) | `go_left = False` |
| `string message` | Змінна, що зберігає текст | `message = ""` |
| `;` | Завершує рядок коду. Вона потрібна майже в кожному рядку. | (новий рядок) |
| `{ }` | Об'єднують рядки, які належать разом | відступи |
| `// comment` | Примітка для людей. Комп'ютер її ігнорує. | `# comment` |
| `=` | Присвоїти значення | `=` |
| `==` | Перевірити, чи дві речі рівні | `==` |
| `&&` | І (and) | `and` |
| `score++` | Додати 1 до score | `score += 1` |
| `pacman.Left -= speed;` | Відняти speed від pacman.Left | `pacman.left -= speed` |
| `if (goLeft) { ... }` | Якщо goLeft дорівнює true, виконати код у фігурних дужках | `if go_left:` |
| `foreach (PictureBox coin in coins)` | Пройти по кожній монеті у списку coins | `for coin in coins:` |
| `private void ShowCoins()` | Метод (функція) з назвою ShowCoins | `def show_coins():` |
| `pacman.Left` | Крапка дає доступ до того, що належить об'єкту | `pacman.left` |

У C# **кожна змінна має тип** (`int`, `bool`, `string`, `PictureBox` тощо). Тип потрібно вказувати, коли створюєте змінну.

---

## Розділ 1: Створення форми

У цьому розділі ви створите ігровий екран, перетягуючи елементи на форму. Коду поки що немає.

### Частина 1: Створення проєкту

1. Відкрийте Visual Studio і натисніть **Create a new project**.
2. Виберіть **Windows Forms App** (C#). **Не** вибирайте варіант з написом **.NET Framework**.
3. Натисніть **Next**. Visual Studio підставить назву проєкту на кшталт `WinFormsApp1`. **Змініть її на `PacManV2`.** Натисніть **Next**.
4. Залиште фреймворк за замовчуванням (наприклад, .NET 10.0). У відео використано .NET 8, але новіша версія працює так само. Натисніть **Create**.

**Чому важлива назва проєкту:** Назва з'являється в рядку `namespace` на початку ваших файлів коду. Зрозуміла назва на кшталт `PacManV2` допоможе легше знайти проєкт пізніше і порівнювати свій код із цим посібником. Використовуйте лише латинські літери та цифри, без пробілів.

**Що ви бачите на екрані**

- Сіре вікно посередині — це **Form1**, вікно, у якому працюватиме ваша гра. Це режим **Design view**.
- **Solution Explorer** (праворуч) показує файли вашого проєкту.
- **Properties** (праворуч, зазвичай під Solution Explorer) показує налаштування вибраного елемента.
- **Toolbox** (ліворуч) містить елементи керування, які можна перетягувати на форму.
- Якщо якесь із цих вікон не видно, відкрийте меню **View**.

> Під час роботи з великою кількістю зображень у Design view екран може трохи мерехтіти. Це нормально.

### Частина 2: Налаштування форми

Клацніть на заголовок форми, щоб її вибрати. У вікні Properties встановіть:

| Властивість (Property) | Значення (Value) |
|---|---|
| Text | `Pac-Man Game` |
| Size | `1030, 775` |
| BackColor | Black |
| DoubleBuffered | True |

**Як це працює**

- **Text** — це назва у верхній частині вікна.
- **DoubleBuffered** змушує форму спочатку малювати кожен кадр непомітно, а потім показувати його повністю. Так зменшується мерехтіння, коли щось рухається.

### Частина 3: Стіни

1. Перетягніть із Toolbox на форму **PictureBox**. Розтягніть його в довгу тонку смугу вздовж верхнього краю.
2. Встановіть для нього **BackColor** синього кольору.
3. Скопіюйте його: виберіть і **перетягніть, утримуючи Ctrl**. Так створюється копія. Щоб вибрати кілька елементів, клацайте на кожен, утримуючи **Shift**.
4. Створіть **вісім стін**: дві вгорі, дві внизу, дві з лівого боку і дві з правого. Залиште **проміжок посередині кожного боку**. Pac-Man проходитиме крізь ці проміжки й з'являтиметься з протилежного боку екрана.
5. Проміжки на протилежних боках мають бути навпроти один одного й однакового розміру, інакше Pac-Man зачеплятиметься за край.
6. Виберіть усі вісім стін (Shift+клацання). У Properties встановіть **Tag** = `wall`.

**Як це працює**

**Tag** — це мітка, яку можна додати до будь-якого елемента. Пізніше код перегляне все на формі й збере кожен PictureBox із міткою `wall`. Тож стін може бути 8 або 80, а код не зміниться. Мітки чутливі до регістру: пишіть `wall`, а не `Wall`.

### Частина 4: Додавання Pac-Man

1. Перетягніть на форму новий **PictureBox**. Встановіть **Name** = `pacman`.
2. Клацніть на ньому правою кнопкою миші й виберіть **Choose Image**.
3. Виберіть **Project resource file**, потім натисніть **Import**. Виберіть **усі** зображення гри одразу й натисніть **Open**. Виберіть одне із зображень Pac-Man і натисніть **OK**.
4. Встановіть **Size** = `50, 50` і **SizeMode** = **StretchImage**.
5. Залиште Pac-Man посередині форми.

**Чому важливо вибрати Project resource file**

Так зображення стають частиною проєкту, і код може використовувати їх за назвою, наприклад `Properties.Resources.left`. Якщо натомість вибрати **Local resource**, код із частини 13 не зможе знайти зображення.

### Частина 5: Монети

1. Створіть новий PictureBox (або скопіюйте Pac-Man через Ctrl+C, Ctrl+V). Клацніть правою кнопкою, виберіть **Choose Image** і виберіть монету.
2. Встановіть **Size** = `20, 20` і **SizeMode** = **StretchImage**.
3. Встановіть **Tag** = `coin`. Зробіть це **до** копіювання, бо копії зберігають мітку.
4. Утримуючи **Ctrl, перетягуйте**, щоб створювати копії. Коли буде готовий ряд, виберіть увесь ряд і перетягніть його з Ctrl, щоб зробити ще один.
5. Заповніть лабіринт монетами. Залиште місце в **чотирьох кутах**, бо там з'являються привиди.

У відео вийшло 104 монети. Підійде будь-яка кількість.

### Частина 6: Ігровий таймер

1. У Toolbox відкрийте **Components** і перетягніть на форму **Timer**. Він з'явиться на панелі **під** формою, а не на самій формі.
2. Встановіть такі властивості:

| Property | Value |
|---|---|
| Name | `gameTimer` |
| Interval | `20` |
| Enabled | False |

**Як це працює**

Таймер — це **ігровий цикл**. Кожні 20 мілісекунд (приблизно 50 разів на секунду) він запускає ваш код: рухає Pac-Man, перевіряє стіни, перевіряє монети, рухає привидів. Спочатку він вимкнений (**Enabled = False**), щоб гра не починалася, доки гравець не натисне Play.

### Частина 7: Стартове меню

1. Перетягніть **Panel** на середину форми. Встановіть **Name** = `pnlMenu`. Панель — це контейнер, у якому розміщуються інші елементи.
2. Перетягніть **Button** **всередину** панелі. Встановіть **Text** = `Play`, **Font** = Bold, розмір 16, і **Name** = `btnStart`.
3. Перетягніть **Label** всередину панелі для назви гри:
   - **Text:** `Pac-Man`
   - **ForeColor:** жовтий (yellow)
   - **Font:** будь-який шрифт, великий розмір
   - **AutoSize:** False, потім розтягніть напис на всю ширину панелі
   - **TextAlign:** MiddleCenter
4. Додайте всередину панелі другий напис з тими самими налаштуваннями. Встановіть **Name** = `lblInfo`, а в **Text** напишіть інструкції, наприклад: `Use the arrow keys to move. Collect all the coins and avoid the ghosts.` Інструкції можна написати будь-якою мовою.

**Як це працює**

Оскільки кнопка й написи розташовані **всередині** панелі, один рядок коду може сховати або показати їх усі одразу. Пізніше напис `lblInfo` показуватиме повідомлення «You Win» або «You Died» і рахунок.

Перейменовувати елементи важливо. Назви `gameTimer` і `lblInfo` одразу пояснюють, що це таке. Назви `timer1` і `label2` — ні.

### Частина 8: Підключення подій

**Подія** (event) — це те, що стається під час роботи програми: натискання клавіші, тік таймера або клацання кнопки. **Обробник події** (event handler) — це метод, який виконується, коли стається ця подія.

1. Клацніть на заголовок форми, щоб її вибрати. У вікні Properties натисніть значок **блискавки**, щоб побачити **Events**. Знайдіть **KeyDown**, введіть `KeyIsDown` і натисніть **Enter**. Visual Studio створить порожній метод і відкриє код. Поверніться на вкладку Design view.
2. Виберіть **gameTimer** на панелі під формою. У Events знайдіть **Tick**, введіть `GameTimerEvent` і натисніть **Enter**.
3. Виберіть кнопку **Play**. У Events знайдіть **Click**, введіть `StartButtonClick` і натисніть **Enter**.

> **Нехай Visual Studio сама створить ці три методи.** Не вводьте їхні перші рядки вручну. Коли Visual Studio створює методи, вона також непомітно підключає їх до елементів. Якщо ввести їх вручну, вони ніколи не запустяться.

Перемикання між режимами: **F7** відкриває код, **Shift+F7** відкриває дизайн.

Тепер ваш код у `Form1.cs` має виглядати так. Рядок `namespace` відповідатиме назві вашого проєкту. Залиште свій.

```csharp
namespace PacManV2
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void KeyIsDown(object sender, KeyEventArgs e)
        {

        }

        private void GameTimerEvent(object sender, EventArgs e)
        {

        }

        private void StartButtonClick(object sender, EventArgs e)
        {

        }
    }
}
```

---

## Розділ 2: Код для Pac-Man

Тепер ви напишете код, який рухає Pac-Man, зупиняє його біля стін і збирає монети.

### Частина 9: Файл класу Ghost

У відео файл для привидів створюють саме зараз. Заповнювати його ви будете в розділі 3.

1. У **Solution Explorer** клацніть правою кнопкою на **проєкті** (той, що зі значком C#, а не рішення в самому верху).
2. Виберіть **Add > Class**.
3. Назвіть файл `Ghost.cs` (з великої G) і натисніть **Add**.

Поки що залиште його порожнім і поверніться до `Form1.cs`.

> У відео автор починає вводити змінні одразу після створення файлу Ghost. Ці змінні пишуться у **Form1.cs**, а не в Ghost.cs.

### Частина 10: Змінні гри

**Файл:** `Form1.cs`, всередині `public partial class Form1 : Form {`, **над** `public Form1()`.

```csharp
// Which way Pac-Man is moving right now
bool goUp, goDown, goLeft, goRight;

// True when a wall is blocking Pac-Man in that direction
bool noUp, noDown, noLeft, noRight;

// Lists that will hold every wall and every coin on the form
List<PictureBox> walls = new List<PictureBox>();
List<PictureBox> coins = new List<PictureBox>();

int speed = 12;   // how many pixels Pac-Man moves each timer tick
int score = 0;    // how many coins Pac-Man has collected

// The four ghosts. They get created in the SetUp method (Part 20).
Ghost red, yellow, blue, pink;

// A list of all the ghosts, so we can loop through them
List<Ghost> ghosts = new List<Ghost>();
```

**Як це працює**

- Змінні, створені тут (всередині класу, але поза будь-яким методом), можна використовувати в **кожному методі** Form1.
- `goLeft` та інші показують, у якому напрямку рухається Pac-Man. Одночасно лише одна з них має дорівнювати true.
- `noLeft` та інші дорівнюють true, коли на шляху стіна. У цьому напрямку не можна рухатися, доки ви не повернете.
- **List** (список) зберігає багато елементів одного типу. `List<PictureBox>` — це список PictureBox.
- `Ghost` — це клас, який ви створили в частині 9. `Ghost red` означає «буде привид з назвою red». Сам привид ще не створено.

> **Зелені хвилясті лінії** — це попередження. Гра все одно запуститься. **Червоні хвилясті лінії** — це помилки, їх потрібно виправити.

### Частина 11: Порожні методи

**Файл:** `Form1.cs`, під трьома методами подій, але все ще всередині класу.

Поки що вони порожні. Ви заповнюватимете їх у наступних частинах.

```csharp
// Collects the walls and coins into lists and creates the ghosts
private void SetUp()
{

}

// Moves Pac-Man in the direction he is going
private void PlayerMovements()
{

}

// Makes all the coins visible again
private void ShowCoins()
{

}

// Stops Pac-Man if he runs into a wall
private void CheckBoundaries(PictureBox pacman, PictureBox wall)
{

}

// Collects a coin if Pac-Man touches it
private void CollectingCoins(PictureBox pacman, PictureBox coin)
{

}

// Ends the game if a ghost touches Pac-Man
private void GhostCollision(Ghost g, PictureBox pacman, PictureBox ghost)
{

}

// Stops the game and shows the menu with a message
private void GameOver(string message)
{

}
```

**Як це працює**

- **Метод** — це іменований блок коду, який можна запустити, викликавши його за назвою, наприклад `ShowCoins();`
- `private void` означає, що використовувати метод може тільки Form1 (`private`) і що метод не повертає відповіді (`void`).
- Те, що в дужках, — це **параметри**: значення, які ви передаєте методу під час виклику. Коли код викликає `CheckBoundaries(pacman, wall)`, метод отримує справжнього Pac-Man і одну справжню стіну. Якщо метод змінить `pacman.Left`, рухатиметься справжній Pac-Man.
- Якщо поділити гру на невеликі методи, код таймера залишиться коротким і зрозумілим.

### Частина 12: Метод SetUp

**Крок 1.** У конструкторі `Form1()` додайте `SetUp();` після `InitializeComponent();`

```csharp
public Form1()
{
    InitializeComponent();   // builds everything you made in Design view
    SetUp();                 // then runs our setup code
}
```

**Крок 2.** Заповніть `SetUp()`. Останній рядок — тимчасова перевірка.

```csharp
private void SetUp()
{
    // Look at every control on the form, one at a time
    foreach (Control x in this.Controls)
    {
        // If it is a picture box tagged "wall", add it to the walls list
        if (x is PictureBox && (string)x.Tag == "wall")
        {
            walls.Add((PictureBox)x);
        }

        // If it is a picture box tagged "coin", add it to the coins list
        if (x is PictureBox && (string)x.Tag == "coin")
        {
            coins.Add((PictureBox)x);
        }
    }

    // TEMPORARY TEST: show the counts in the title bar
    this.Text = walls.Count + " " + coins.Count;
}
```

**Як це працює**

- `InitializeComponent()` завантажує все, що ви створили в Design view. `SetUp()` виконується одразу після нього.
- `this.Controls` — це всі елементи на формі. `this` означає «ця форма».
- `x is PictureBox` перевіряє, чи є елемент PictureBox.
- `(string)x.Tag == "wall"` читає Tag як текст і перевіряє, чи там написано `wall`.
- `(PictureBox)x` називається **приведенням типу** (casting). Воно каже C# розглядати цей елемент як PictureBox, бо саме такий тип потрібен, щоб додати його до списку.

> У відео написано `x.Tag == "wall"`. У цьому посібнику використано `(string)x.Tag == "wall"` — це правильніший спосіб порівнювати текст у C#. У цьому проєкті працюють обидва варіанти.

**✅ Контрольна точка:** Натисніть **F5** (або зелену кнопку Start). У заголовку вікна має з'явитися `8 104` (кількість монет у вас може бути іншою). Якщо бачите 0, перевірте мітки Tag. Потім **видаліть рядок перевірки.**

### Частина 13: Керування з клавіатури

**Файл:** `Form1.cs`, всередині `KeyIsDown`.

```csharp
private void KeyIsDown(object sender, KeyEventArgs e)
{
    // LEFT arrow, and no wall blocking the left
    if (e.KeyCode == Keys.Left && noLeft == false)
    {
        goRight = goDown = goUp = false;     // stop the other directions
        noRight = noDown = noUp = false;     // clear the other wall blocks
        goLeft = true;                       // start moving left
        pacman.Image = Properties.Resources.left;   // face left
    }

    // RIGHT arrow
    if (e.KeyCode == Keys.Right && noRight == false)
    {
        goLeft = goUp = goDown = false;
        noLeft = noUp = noDown = false;
        goRight = true;
        pacman.Image = Properties.Resources.right;
    }

    // UP arrow
    if (e.KeyCode == Keys.Up && noUp == false)
    {
        goLeft = goRight = goDown = false;
        noLeft = noRight = noDown = false;
        goUp = true;
        pacman.Image = Properties.Resources.up;
    }

    // DOWN arrow
    if (e.KeyCode == Keys.Down && noDown == false)
    {
        goLeft = goRight = goUp = false;
        noLeft = noRight = noUp = false;
        goDown = true;
        pacman.Image = Properties.Resources.down;
    }
}
```

**Як це працює**

- `e.KeyCode` показує, яку клавішу натиснуто.
- `&& noLeft == false` означає «тільки якщо ліворуч немає стіни».
- `goRight = goDown = goUp = false;` встановлює всі три змінні в false одним рядком, тож Pac-Man рухається лише в одному напрямку.
- Pac-Man продовжує рухатися, коли ви відпускаєте клавішу, як у справжній грі. Тому події KeyUp тут немає.

> **Назви зображень:** введіть `Properties.Resources.` (з крапкою), і з'явиться список з назвами ваших зображень. Назви беруться з імен файлів. Якщо ваші відрізняються від `left`, `right`, `up` і `down`, використовуйте свої.

### Частина 14: Рух Pac-Man і кнопка запуску

**Крок 1.** Заповніть `PlayerMovements()`:

```csharp
private void PlayerMovements()
{
    if (goLeft)  { pacman.Left -= speed; }   // move left
    if (goRight) { pacman.Left += speed; }   // move right
    if (goUp)    { pacman.Top -= speed; }    // move up
    if (goDown)  { pacman.Top += speed; }    // move down
}
```

**Крок 2.** Викличте його з таймера:

```csharp
private void GameTimerEvent(object sender, EventArgs e)
{
    PlayerMovements();
}
```

**Крок 3.** Заповніть метод кнопки запуску:

```csharp
private void StartButtonClick(object sender, EventArgs e)
{
    // Hide the menu (this hides the button and labels too)
    pnlMenu.Enabled = false;
    pnlMenu.Visible = false;

    // Reset movement and wall blocks
    goLeft = goRight = goUp = goDown = false;
    noLeft = noRight = noUp = noDown = false;

    score = 0;

    // (Ghost resets get added here in Part 24)

    gameTimer.Start();   // start the game loop
}
```

**Як це працює**

- **Left** — це відстань від PictureBox до лівого краю форми. **Top** — відстань до верхнього краю.
- На екрані **Top збільшується, коли рухаєтеся вниз**. Це протилежно до графіків на уроках математики. Тому рух угору означає віднімання від Top.
- Кожен тік таймера переміщує Pac-Man на 12 пікселів. При 50 тіках на секунду рух виглядає плавним.

**✅ Контрольна точка:** Запустіть гру й натисніть **Play**. Користуйтеся клавішами зі стрілками. Pac-Man має рухатися й не зупинятися. Він проходитиме крізь стіни. Це буде виправлено в частині 16.

### Частина 15: Перехід через краї екрана

**Файл:** `Form1.cs`. Додайте це в **кінець** `PlayerMovements()`, після чотирьох рядків руху.

```csharp
// Went off the left side? Come back on the right side.
if (pacman.Left < -30)
{
    pacman.Left = this.ClientSize.Width - pacman.Width;
}

// Went off the right side? Come back on the left side.
if (pacman.Left + pacman.Width > this.ClientSize.Width)
{
    pacman.Left = -10;
}

// Went off the top? Come back at the bottom.
if (pacman.Top < -30)
{
    pacman.Top = this.ClientSize.Height - pacman.Height;
}

// Went off the bottom? Come back at the top.
if (pacman.Top + pacman.Height > this.ClientSize.Height)
{
    pacman.Top = -10;
}
```

**Як це працює**

- `ClientSize` — це внутрішня частина вікна без рамки й заголовка.
- `pacman.Left + pacman.Width` — це положення **правого** краю Pac-Man.
- Коли Pac-Man виходить за один край, код переносить його до протилежного.

> У цьому посібнику `ClientSize` використано в усіх чотирьох перевірках. Якщо ви робили як у відео і Pac-Man стрибає туди-сюди біля краю, змініть свій код, щоб він відповідав цьому.

**✅ Контрольна точка:** Пройдіть крізь проміжок у стіні. Pac-Man має з'явитися з протилежного боку.

### Частина 16: Зупинка біля стін

**Крок 1.** Заповніть `CheckBoundaries()`:

```csharp
private void CheckBoundaries(PictureBox pacman, PictureBox wall)
{
    // Are Pac-Man and this wall overlapping?
    if (pacman.Bounds.IntersectsWith(wall.Bounds))
    {
        if (goLeft)
        {
            noLeft = true;                    // block left
            goLeft = false;                   // stop moving
            pacman.Left = wall.Right + 2;     // push him just right of the wall
        }

        if (goRight)
        {
            noRight = true;
            goRight = false;
            pacman.Left = wall.Left - pacman.Width - 2;   // just left of the wall
        }

        if (goUp)
        {
            noUp = true;
            goUp = false;
            pacman.Top = wall.Bottom + 2;     // just below the wall
        }

        if (goDown)
        {
            noDown = true;
            goDown = false;
            pacman.Top = wall.Top - pacman.Height - 2;    // just above the wall
        }
    }
}
```

**Крок 2.** У `GameTimerEvent` додайте цикл, який перевіряє кожну стіну:

```csharp
private void GameTimerEvent(object sender, EventArgs e)
{
    PlayerMovements();

    // Check Pac-Man against every wall
    foreach (PictureBox wall in walls)
    {
        CheckBoundaries(pacman, wall);
    }
}
```

**Як це працює**

- **Bounds** — це невидимий прямокутник навколо елемента.
- `IntersectsWith` дорівнює true, коли два прямокутники перекриваються. Саме так більшість 2D-ігор перевіряє зіткнення.
- Коли Pac-Man врізається в стіну, код перевіряє, куди він рухався, зупиняє його, блокує цей напрямок і відсуває його на 2 пікселі, щоб він не застряг у стіні.
- Цикл `foreach` показує, чому корисний список стін: один короткий цикл перевіряє всі вісім стін.

**✅ Контрольна точка:** Pac-Man має зупинятися біля кожної стіни в усіх чотирьох напрямках. Він має могти повернути й відійти.

### Частина 17: Збирання монет

**Крок 1.** Заповніть `CollectingCoins()`:

```csharp
private void CollectingCoins(PictureBox pacman, PictureBox coin)
{
    if (pacman.Bounds.IntersectsWith(coin.Bounds))
    {
        // Only collect coins that are still showing
        if (coin.Visible)
        {
            coin.Visible = false;   // hide the coin
            score++;                // add 1 to the score
        }
    }
}
```

**Крок 2.** Заповніть `ShowCoins()`:

```csharp
private void ShowCoins()
{
    foreach (PictureBox coin in coins)
    {
        coin.Visible = true;
    }
}
```

**Крок 3.** Оновіть `GameTimerEvent`:

```csharp
private void GameTimerEvent(object sender, EventArgs e)
{
    PlayerMovements();

    foreach (PictureBox wall in walls)
    {
        CheckBoundaries(pacman, wall);
    }

    // Check Pac-Man against every coin
    foreach (PictureBox coin in coins)
    {
        CollectingCoins(pacman, coin);
    }

    // TEMPORARY: when every coin is collected, bring them all back
    // (Part 26 replaces this with a "You Win" message)
    if (score == coins.Count)
    {
        ShowCoins();
        score = 0;
    }
}
```

**Як це працює**

- Монети **ховаються**, а не видаляються. Так їх легко повернути для наступної гри.
- Перевірка `if (coin.Visible)` не дає Pac-Man збирати ту саму сховану монету знову і знову.
- `coins.Count` — це кількість монет у списку. Коли рахунок дорівнює цьому числу, зібрано всі монети.

**✅ Контрольна точка:** Монети зникають, коли Pac-Man їх торкається. Коли ви зберете останню, усі вони повернуться.

---

## Розділ 3: Клас Ghost

**Що таке клас?** Клас — це **креслення** (шаблон). Клас Ghost описує, що **має** кожен привид (зображення, швидкість, напрямок) і що кожен привид **може робити** (рухатися, змінювати напрямок). Потім за цим кресленням ви створите чотири **об'єкти**-привиди: червоного, синього, жовтого й рожевого.

Кожен привид сам стежить за своїм положенням і напрямком, але код привида ви пишете лише **один раз**. Без класу довелося б писати код руху чотири рази, для кожного привида окремо.

### Частина 18: Змінні привида

**Файл:** `Ghost.cs`. Ось як має виглядати файл після цієї частини. Залиште свій рядок `namespace`.

```csharp
using System.Drawing;         // for Image
using System.Windows.Forms;   // for PictureBox and Form

namespace PacManV2
{
    internal class Ghost
    {
        int speed = 8;    // speed when moving in a straight line
        int xSpeed = 4;   // left/right speed in seek mode (half speed)
        int ySpeed = 4;   // up/down speed in seek mode (half speed)

        // The area the ghosts are allowed to move in.
        // These numbers come from YOUR form. See "Finding your numbers" below.
        int maxHeight = 685;
        int minHeight = 81;
        int maxWidth = 970;
        int minWidth = 76;

        int change = 0;   // countdown until the ghost picks a new direction
        Random random = new Random();

        // The five things a ghost can do
        string[] directions = { "left", "right", "up", "down", "seek" };
        string direction = "left";   // the ghost starts by moving left

        // The ghost's picture box. Public so Form1 can use it.
        public PictureBox image = new PictureBox();
    }
}
```

**Як це працює**

- `string[] directions` — це **масив**, фіксований список значень. Кожен привид випадково вибиратиме одне з цих п'яти.
- `Random` створює випадкові числа.
- Лише `image` позначено як `public`, бо він потрібен Form1 (щоб повертати привида на початкове місце і перевіряти, чи торкнувся він Pac-Man). Усе інше залишається private, бо використовується лише в класі Ghost.

**Як знайти свої числа**

Чотири числа min/max тримають привидів у межах стін. Ваші числа залежать від того, як ви побудували лабіринт.

1. У Design view клацніть на монету (або будь-який PictureBox) у **найдальшій верхній лівій точці** всередині стін. Подивіться на її **Location** у Properties. Значення X — це `minWidth`. Значення Y — це `minHeight`.
2. Клацніть на щось у **найдальшій нижній правій точці** всередині стін. Додайте 50 (розмір привида) до X, щоб отримати `maxWidth`. Додайте 50 до Y, щоб отримати `maxHeight`.

Числа у відео можуть трохи відрізнятися від наведених вище. Головне, щоб вони відповідали вашому лабіринту.

### Частина 19: Конструктор привида

**Файл:** `Ghost.cs`, всередині класу, під змінними.

```csharp
// The constructor runs once, every time a new Ghost is created
public Ghost(Form game, Image img, int x, int y)
{
    image.Image = img;                                  // the ghost picture
    image.SizeMode = PictureBoxSizeMode.StretchImage;   // fit the picture to the box
    image.Width = 50;
    image.Height = 50;
    image.Left = x;                                     // starting position
    image.Top = y;

    game.Controls.Add(image);   // put the ghost on the form
}
```

**Як це працює**

- **Конструктор** має таку саму назву, як клас, і не має типу повернення. Він запускається автоматично, коли ви створюєте новий об'єкт.
- Параметри дають змогу кожному привиду бути іншим:
  - `game` — це форма, щоб привид міг додати себе на неї
  - `img` — зображення привида (червоного, синього, жовтого чи рожевого)
  - `x` і `y` — місце, де він з'являється
- `game.Controls.Add(image)` розміщує PictureBox на формі. Без цього рядка привид існує в коді, але не з'являється на екрані.

### Частина 20: Створення чотирьох привидів

**Файл:** `Form1.cs`, у **кінці** `SetUp()`, після циклу `foreach`.

```csharp
// Create each ghost: (this form, its picture, starting X, starting Y)
// Then add it to the ghosts list
red = new Ghost(this, Properties.Resources.red, 100, 100);
ghosts.Add(red);

blue = new Ghost(this, Properties.Resources.blue, 848, 597);
ghosts.Add(blue);

yellow = new Ghost(this, Properties.Resources.yellow, 132, 584);
ghosts.Add(yellow);

pink = new Ghost(this, Properties.Resources.pink, 877, 130);
ghosts.Add(pink);
```

**Як це працює**

- `new Ghost(...)` створює справжнього привида за кресленням. Це викликає конструктор із частини 19.
- `this` означає «ця форма». Її передають, щоб кожен привид міг додати себе на форму.
- Кожен привид — це **екземпляр** (instance) класу Ghost. Одне креслення, але різні зображення і початкові місця.

**✅ Контрольна точка:** Запустіть гру. Ви маєте побачити чотирьох привидів, по одному біля кожного кута. Поки що вони не рухаються. Якщо привид схований за монетами чи стінами, дивіться розділ [Усунення проблем](#усунення-проблем).

### Частина 21: Рух привидів

**Крок 1.** **Файл:** `Ghost.cs`, всередині класу, під конструктором.

```csharp
// Moves this ghost. Called from the game timer.
public void GhostMovement(PictureBox pacman)
{
    // Count down. When the countdown hits 0, pick a new direction.
    if (change > 0)
    {
        change--;
    }
    else
    {
        change = random.Next(50, 80);                            // new countdown
        direction = directions[random.Next(directions.Length)];  // random direction
    }

    // Move based on the current direction
    switch (direction)
    {
        case "left":
            image.Left -= speed;
            break;

        case "right":
            image.Left += speed;
            break;

        case "up":
            image.Top -= speed;
            break;

        case "down":
            image.Top += speed;
            break;

        // "seek" gets added in Part 23
    }
}
```

**Крок 2.** **Файл:** `Form1.cs`, у кінці `GameTimerEvent`:

```csharp
// Move each ghost. Each one needs to know where Pac-Man is.
red.GhostMovement(pacman);
blue.GhostMovement(pacman);
yellow.GhostMovement(pacman);
pink.GhostMovement(pacman);
```

**Як це працює**

- `change` зменшується на 1 з кожним тіком. Коли він доходить до 0, привид вибирає нове число для відліку і новий випадковий напрямок.
- `random.Next(50, 80)` вибирає випадкове число від 50 до 79. При 50 тіках на секунду це приблизно 1–1,5 секунди до повороту привида.
- `directions[random.Next(directions.Length)]` вибирає випадкову позицію в масиві. `directions.Length` дорівнює 5, тож вибирається 0, 1, 2, 3 або 4.
- **switch** порівнює одне значення з кількома варіантами. Він робить те саме, що й низка команд `if`. Кожен `case` має закінчуватися `break;`.
- `GhostMovement` позначено як `public`, бо його має викликати Form1.

**✅ Контрольна точка:** Привиди блукають, і деякі з них виходять за межі екрана. Це буде виправлено в наступній частині. Якщо привид на мить зупиняється, це означає, що він вибрав `"seek"`, який ви додасте в частині 23.

### Частина 22: Привиди залишаються в лабіринті

**Файл:** `Ghost.cs`, у кінці `GhostMovement`, **після** закривної фігурної дужки switch.

```csharp
// If the ghost reaches an edge of the maze, turn it around
if (image.Left < minWidth)
{
    direction = "right";
}

if (image.Left + image.Width > maxWidth)
{
    direction = "left";
}

if (image.Top < minHeight)
{
    direction = "down";
}

if (image.Top + image.Height > maxHeight)
{
    direction = "up";
}
```

**Як це працює**

Після того як привид зрушив, ці перевірки дивляться, чи не вийшов він за край лабіринту. Якщо вийшов, привид змінює напрямок на протилежний, тож завжди залишається всередині.

**✅ Контрольна точка:** Усі чотири привиди блукають, але залишаються в межах стін.

### Частина 23: Режим переслідування

**Файл:** `Ghost.cs`, всередині switch у `GhostMovement`. Додайте цей case після `case "down":`.

```csharp
case "seek":
    // Move toward Pac-Man, left or right
    if (image.Left > pacman.Left)
    {
        image.Left -= xSpeed;
    }
    if (image.Left < pacman.Left)
    {
        image.Left += xSpeed;
    }

    // Move toward Pac-Man, up or down
    if (image.Top > pacman.Top)
    {
        image.Top -= ySpeed;
    }
    if (image.Top < pacman.Top)
    {
        image.Top += ySpeed;
    }
    break;
```

**Як це працює**

- Режим переслідування в коді називається `"seek"`. Привид порівнює своє положення з положенням Pac-Man. Якщо привид праворуч від Pac-Man, він рухається ліворуч. Якщо нижче — рухається вгору. І так далі.
- Оскільки за один тік він може рухатися і ліворуч/праворуч, **і** вгору/вниз, привид у режимі переслідування рухається **по діагоналі**. Так можна зрозуміти, що привид женеться за вами.
- У режимі переслідування використовується половинна швидкість (4 замість 8), щоб гравець мав шанс утекти.
- Саме тому `GhostMovement` отримує Pac-Man як параметр: привид має знати, де Pac-Man.

**✅ Контрольна точка:** Час від часу привид рухається по діагоналі й трохи переслідує Pac-Man, а потім знову блукає.

---

## Розділ 4: Завершення гри

### Частина 24: Скидання привидів

**Крок 1.** **Файл:** `Ghost.cs`, всередині класу, під `GhostMovement`.

```csharp
// Pick a new random direction (used when the game ends)
public void ChangeDirection()
{
    direction = directions[random.Next(directions.Length)];
}
```

**Крок 2.** **Файл:** `Form1.cs`, у `StartButtonClick`. Замініть коментар `// (Ghost resets get added here in Part 24)` на:

```csharp
// Put each ghost back at its starting spot
red.image.Location = new Point(100, 100);
blue.image.Location = new Point(848, 597);
yellow.image.Location = new Point(132, 584);
pink.image.Location = new Point(877, 130);
```

**Як це працює**

- `ChangeDirection` гарантує, що привид, який щойно спіймав Pac-Man, не кинеться на нього знову одразу на початку наступної гри.
- `new Point(x, y)` зберігає X і Y разом. Якщо встановити `Location`, PictureBox переміститься в цю точку.
- `red.image` дає доступ до PictureBox привида. Це працює, бо `image` позначено як `public`.

### Частина 25: Кінець гри

**Файл:** `Form1.cs`, заповніть `GameOver()`.

```csharp
private void GameOver(string message)
{
    // Show the menu again
    pnlMenu.Visible = true;
    pnlMenu.Enabled = true;

    gameTimer.Stop();   // stop the game loop

    ShowCoins();        // bring back any coins that were collected

    // Put Pac-Man back at his starting spot.
    // Use YOUR Pac-Man's Location from the Properties window.
    pacman.Location = new Point(490, 350);

    lblInfo.Text = message;   // show the win or lose message
}
```

**Як знайти початкове місце Pac-Man:** У Design view панель меню може закривати Pac-Man. Скористайтеся **випадним списком угорі вікна Properties**, щоб вибрати `pacman`, а потім скопіюйте числа з **Location**.

**Як це працює**

Параметр `message` дає змогу одному методу показувати різні повідомлення. І перемога, і програш завершують гру, але повідомлення в них різні.

### Частина 26: Зіткнення з привидом і перемога

**Крок 1.** **Файл:** `Form1.cs`, заповніть `GhostCollision()`.

```csharp
private void GhostCollision(Ghost g, PictureBox pacman, PictureBox ghost)
{
    // Did this ghost touch Pac-Man?
    if (pacman.Bounds.IntersectsWith(ghost.Bounds))
    {
        GameOver("You Died! Your Score: " + score);
        g.ChangeDirection();   // give this ghost a new direction for next game
    }
}
```

**Крок 2.** У `GameTimerEvent` **замініть** тимчасову перевірку монет із частини 17 на перевірку перемоги й додайте в кінці цикл, який перевіряє кожного привида. Готовий таймер виглядає так:

```csharp
private void GameTimerEvent(object sender, EventArgs e)
{
    PlayerMovements();

    foreach (PictureBox wall in walls)
    {
        CheckBoundaries(pacman, wall);
    }

    foreach (PictureBox coin in coins)
    {
        CollectingCoins(pacman, coin);
    }

    // All coins collected: the player wins
    if (score == coins.Count)
    {
        GameOver("You Win! You collected all " + score + " coins.");
    }

    red.GhostMovement(pacman);
    blue.GhostMovement(pacman);
    yellow.GhostMovement(pacman);
    pink.GhostMovement(pacman);

    // Check every ghost against Pac-Man
    foreach (Ghost ghost in ghosts)
    {
        GhostCollision(ghost, pacman, ghost.image);
    }
}
```

**Як це працює**

- `GhostCollision` отримує три речі: **об'єкт** привида (щоб викликати `ChangeDirection`), Pac-Man і **PictureBox** привида (щоб перевірити зіткнення).
- `"You Died! Your Score: " + score` поєднує текст і число в одне повідомлення.
- Цикл `foreach (Ghost ghost in ghosts)` працює так само, як цикли для стін і монет, але перебирає об'єкти Ghost замість PictureBox.

**✅ Контрольна точка:** Дотик до привида завершує гру й показує ваш рахунок. Натисніть Play, щоб почати знову.

**Перевірка перемоги:** Зібрати всі монети, коли за вами женуться привиди, важко. Щоб перевірити перемогу, поставте `//` перед кожним рядком циклу зіткнення з привидами, грайте, доки не зберете всі монети, і перевірте, чи з'являється повідомлення «You Win». Потім **приберіть `//`**, щоб привиди знову працювали.

🎉 **Вашу гру готово.**

---

## Усунення проблем

**Як читати помилки:** Відкрийте **View > Error List**. Двічі клацніть на помилку, щоб перейти до відповідного рядка. Рядок із проблемою часто розташований **над** тим місцем, де з'являється червона хвиляста лінія.

| Проблема | Імовірна причина і як виправити |
|---|---|
| `; expected` або `} expected` | Бракує крапки з комою або фігурної дужки. Перевірте рядок, на який вказує помилка, і рядок над ним. |
| `The name 'something' does not exist in the current context` | Помилка в назві чи в регістрі літер, або код розташований поза фігурними дужками методу. Порівняйте з кодом у відповідній частині посібника. |
| Червона хвиляста лінія під `Properties.Resources.left` | Ваше зображення має іншу назву. Введіть `Properties.Resources.` і виберіть назву зі списку. Якщо в списку немає зображень, у частині 4 ви вибрали **Local resource**. Знову виберіть **Choose Image** та імпортуйте через **Project resource file**. |
| Зелені хвилясті лінії | Це попередження. Гра все одно працює. |
| У заголовку `0 0` або 0 у частині 12 | У мітці Tag помилка або велика літера. Має бути точно `wall` або `coin`. |
| Монет менше, ніж очікувалося | Можливо, деякі монети потрапили **всередину** панелі меню. Перемістіть їх за межі панелі. |
| Один із методів подій ніколи не запускається | Метод введено вручну, а не створено через список Events. Виберіть елемент, відкрийте Events (блискавка) і виберіть метод у випадному списку біля події. |
| Кнопка Play працює, а стрілки — ні | Перевірте, що для події форми **KeyDown** вибрано `KeyIsDown`. Якщо так, встановіть властивість форми **KeyPreview** = True. |
| Pac-Man не рухається після натискання Play | Для події таймера **Tick** не вибрано `GameTimerEvent`, або бракує `gameTimer.Start();`. |
| Pac-Man стрибає туди-сюди біля краю | Використовуйте `ClientSize` в усіх чотирьох перевірках переходу через край (частина 15). |
| Pac-Man проходить крізь стіни | У таймері бракує циклу `foreach` для стін, або стіни не мають мітки `wall`. |
| Привиди з'являються за монетами чи стінами | У конструкторі Ghost додайте `image.BringToFront();` у рядку після `game.Controls.Add(image);` |
| Привиди виходять із лабіринту чи застрягають біля краю | Ваші числа min/max не відповідають лабіринту. Ще раз виконайте «Як знайти свої числа» з частини 18. |
| Гра закінчується одразу після натискання Play | Початкове місце привида перекривається з початковим місцем Pac-Man. Пересуньте одного з них. |

Досі не виходить? Порівняйте свій код рядок за рядком із кодом у відповідній частині посібника, потім запитайте однокласника, а потім — Mr. McMaster.

---

## Спробуйте ще

Коли гра запрацює, спробуйте щось змінити. Після кожної зміни запускайте гру й дивіться, що вийшло.

1. **Змініть швидкість.** Зробіть Pac-Man швидшим або повільнішим (`speed` у Form1). Зробіть привидів швидшими або повільнішими (`speed`, `xSpeed`, `ySpeed` у Ghost).
2. **Показуйте рахунок під час гри.** У `GameTimerEvent` додайте `this.Text = "Score: " + score;`
3. **Додайте стіни всередині лабіринту.** Додайте нові PictureBox із міткою `wall`. Змінювати код не потрібно. Чому це працює?
4. **Скоротіть код таймера.** Замініть чотири рядки з `GhostMovement` одним циклом `foreach` по списку `ghosts`.
5. **Додайте п'ятого привида.** Використайте одне з наявних зображень привидів і нове початкове місце. Зверніть увагу, як мало коду для цього потрібно. У цьому й полягає користь класу.
6. **Нехай привиди переслідують частіше.** Додайте `"seek"` у масив `directions` ще раз. Кожен напрямок має однаковий шанс бути вибраним, тож так шанс режиму переслідування подвоїться.
7. **Додайте життя.** Дайте гравцеві 3 життя. Коли привид ловить Pac-Man, забирайте одне життя й повертайте всіх на початкові місця. Викликайте `GameOver` лише тоді, коли життів не залишилося.

---

## Основні терміни

У відео ці терміни звучать англійською, тому в другому стовпці наведено англійські назви.

| Термін | Англійською | Значення |
|---|---|---|
| **Змінна** | Variable | Іменоване місце для зберігання значення, наприклад `score` або `speed` |
| **Тип** | Type | Яке значення зберігає змінна: `int` (ціле число), `bool` (true/false), `string` (текст), `PictureBox` тощо |
| **Список** | List | Набір елементів одного типу, який може збільшуватися, наприклад `List<PictureBox>` |
| **Масив** | Array | Набір фіксованого розміру, наприклад `string[] directions` |
| **Цикл** | Loop | Код, що повторюється. `foreach` виконується один раз для кожного елемента списку. |
| **Метод** | Method | Іменований блок коду, який можна запустити, викликавши його за назвою |
| **Параметр** | Parameter | Значення, яке ви передаєте методу під час виклику |
| **Подія** | Event | Те, що стається під час роботи програми: натискання клавіші, клацання, тік таймера |
| **Обробник події** | Event handler | Метод, що виконується, коли стається подія |
| **Ігровий цикл** | Game loop | Код, який повторюється знову і знову, щоб гра тривала. Тут це таймер. |
| **Зіткнення** | Collision | Коли два об'єкти на екрані перекриваються. Перевіряється через `Bounds.IntersectsWith`. |
| **Клас** | Class | Креслення, яке описує, що об'єкт має і що він може робити |
| **Об'єкт / екземпляр** | Object / Instance | Одна справжня річ, створена з класу. `red` — екземпляр класу `Ghost`. |
| **Конструктор** | Constructor | Особливий метод, який запускається під час створення нового об'єкта |
| **public / private** | public / private | `public` означає, що це можуть використовувати інші класи. `private` — лише цей клас. |
| **Приведення типу** | Casting | Вказівка C# розглядати значення як певний тип, наприклад `(PictureBox)x` |
