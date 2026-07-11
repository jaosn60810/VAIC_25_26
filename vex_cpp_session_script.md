# VEX C++ Session — Reading Script
## VEX C++ 教學課程逐字稿(中英對照)

> **使用說明 / How to use this script:**
> - 黑色英文 = 老師對學生講的話(直接念出來)
> - *斜體中文* = 中文意思(老師看的,不要念)
> - 📌 灰色框 = 老師的內部提示(該做什麼動作,純中文,不要念)
> - 整堂課預計 90 分鐘,每個 section 標題後有預估時間

---

## 🧰 上課前 5 分鐘檢查 (Pre-class check)

📌 **老師上課前自己檢查這些:**
- [ ] Zoom / Google Meet / 視訊軟體連線正常
- [ ] 螢幕分享測試過
- [ ] 自己這邊先把 https://github.com/VEX-Robotics/VAIC_25_26 這個網頁打開備用
- [ ] 自己 Mac 上也先 clone 過一份(萬一學生卡住可以螢幕分享給他們看)
- [ ] 準備好下面這份稿子在另一個視窗

---

## ① Opening & Recap | 開場與回顧 (5 min)

"Hi! Good to see you again. How are you doing today?"

*嗨!很高興又見面了,你今天好嗎?*

📌 **等學生回應,簡單寒暄 30 秒。**

"So, last time we worked on Java together. Today is going to be a little different. We're going to look at C++ code, but **don't worry** — we are not going to learn how to *write* C++ today. We just need to learn how to *read* it."

*上次我們一起做 Java。今天會有點不一樣。我們要看 C++ 程式碼,但不用擔心,我們今天不是要學「寫」C++,只是學「讀」C++。*

"The good news is: C++ and Java look very similar. If you can read Java, you can read most C++ code. There are just a few small differences I'll show you."

*好消息是:C++ 跟 Java 長得很像。會看 Java 就能看懂大部分 C++。只有幾個小差異我會教你。*

"Our goal for today has two parts. First, we're going to set up your computer so you can open the VEX robotics code in VS Code. Second, I'll walk you through some real C++ files from the VEX AI competition, and we'll read them together."

*我們今天的目標分兩部分。第一,把你的電腦設定好,讓你可以在 VS Code 打開 VEX 機器人的程式碼。第二,我會帶你看 VEX AI 比賽真實的 C++ 檔案,我們一起讀。*

"Sound good? Let's start."

*聽起來 OK 嗎?我們開始吧。*

---

## ② What we're working with | 我們今天要看什麼 (3 min)

"Before we install anything, let me show you what we're going to read."

*在裝任何東西之前,讓我先給你看我們等下要讀什麼。*

📌 **分享螢幕,打開 https://github.com/VEX-Robotics/VAIC_25_26**

"This is the official VEX Robotics repository for the AI competition this season. Your team will use this code as a starting point. Take a look at the folders here."

*這是 VEX Robotics 官方為這一季 AI 競賽出的 repo。你的隊伍會用這份程式碼當起點。看一下這些資料夾。*

"There are four main folders. The one we care about today is `V5Example/ai_demo`. That's the C++ code that runs on the robot's main brain. The other folders are Python and TypeScript — we won't touch those today."

*有四個主要資料夾。今天我們關心的是 V5Example/ai_demo。那是跑在機器人主控板上的 C++ 程式碼。其他資料夾是 Python 和 TypeScript,今天不碰。*

📌 **點進 `V5Example/ai_demo` 給學生看裡面有 `include/` 和 `src/` 兩個資料夾。**

"See how there's an `include` folder and a `src` folder? In C++, this is a very common pattern. The `include` folder has the **header files**, which end in `.h`. The `src` folder has the **implementation files**, which end in `.cpp`. We'll talk a lot more about this in a few minutes."

*看到有 include 跟 src 兩個資料夾嗎?在 C++ 裡這是很常見的結構。include 放 header file(副檔名 .h),src 放實作檔(副檔名 .cpp)。等下我們會詳細講這個。*

---

## ③ Install VS Code | 安裝 VS Code (10 min)

"OK, now let's get your Mac set up. The first thing we need is VS Code itself. Do you already have it installed?"

*好,現在我們來把你的 Mac 設定好。第一個要做的是 VS Code。你已經裝過了嗎?*

📌 **如果學生說已經裝過 → 跳到 ④。如果沒裝過,繼續。**

"No problem. Let's go to the website. Open Safari or Chrome and go to `code.visualstudio.com`."

*沒問題。我們去網站。打開 Safari 或 Chrome,進 code.visualstudio.com。*

"You should see a big blue button that says 'Download for macOS'. Click that. It downloads a `.zip` file."

*你應該會看到一個藍色大按鈕寫 Download for macOS。按那個。會下載一個 .zip 檔。*

📌 **等學生下載完成。可能要等 1-2 分鐘。**

"Now open Finder and go to your Downloads folder. You should see `VSCode-darwin-universal.zip`. Double-click it to unzip. After it's unzipped, you'll see a `Visual Studio Code` app icon."

*打開 Finder,去 Downloads 資料夾。你應該看到 VSCode-darwin-universal.zip。連點兩下解壓縮。解壓後會看到 Visual Studio Code 的 app icon。*

"Important: drag that app from Downloads into your Applications folder. **Don't open it from Downloads** — macOS will complain about permissions."

*重要:把那個 app 從 Downloads 拖到 Applications 資料夾。**不要直接從 Downloads 打開**,macOS 會抱怨權限問題。*

"Now go to Applications and double-click Visual Studio Code. The first time you open it, macOS will ask if you're sure. Click 'Open'."

*然後去 Applications,連點 Visual Studio Code。第一次打開,macOS 會問你確定嗎,按 Open。*

📌 **等學生 VS Code 開起來。**

"Great. VS Code is open. Now let me tell you about the most important parts of this window."

*很好,VS Code 開起來了。現在我來告訴你這個視窗最重要的幾個部分。*

📌 **指給學生看(透過螢幕分享自己的 VS Code 對應位置)。**

"On the very left, you see a column of icons. That's called the **Activity Bar**. The top icon is the **Explorer** — it shows your files. The icon that looks like four squares is **Extensions** — that's where we install add-ons. We'll use it next."

*最左邊那一列 icon 叫做 Activity Bar。最上面那個是 Explorer,顯示你的檔案。長得像四個方塊那個是 Extensions,我們安裝外掛的地方,等下會用到。*

"Below that, there's the **Side Bar** which shows the contents. In the middle is the **Editor** where you actually look at code. And at the bottom you can open a **Terminal** by pressing Control + backtick. We'll use the terminal soon."

*再下面是 Side Bar 顯示內容。中間是 Editor,你看程式碼的地方。最下面按 Control + 反引號 (`) 可以開 Terminal,等下我們會用到。*

---

## ④ Verify Git is installed | 確認 Git 已安裝 (5 min)

"Now let's check if you have Git. Git is the tool that lets us download code from GitHub. Open the terminal in VS Code by pressing Control and the backtick key — that's the key above Tab, to the left of the number 1."

*現在來確認你有沒有 Git。Git 是讓我們從 GitHub 下載程式碼的工具。在 VS Code 裡按 Control + 反引號(那個鍵在 Tab 上面,數字 1 的左邊)打開 terminal。*

📌 **如果學生找不到反引號鍵,叫他們從選單 Terminal → New Terminal 開。**

"In the terminal, type this command and press Enter:"

*在 terminal 裡打這個指令然後按 Enter:*

```bash
git --version
```

📌 **兩種可能結果:**

**情況 A — 已經有 Git:**

"If you see something like `git version 2.39.x` — perfect, you already have Git. We can skip the next step."

*如果看到類似 git version 2.39.x 的東西,完美,你已經有 Git 了,可以跳過下一步。*

**情況 B — 還沒裝:**

"If a popup appears asking to install command line developer tools, click 'Install'. This will take about 5 to 10 minutes. We can use this time to talk about C++ while we wait."

*如果跳出一個對話框問要不要裝 command line developer tools,按 Install。這會花 5 到 10 分鐘。等待的時候我們可以先聊一下 C++。*

📌 **如果學生在等安裝,可以先跳到 ⑦ 講 Java vs C++ 的概念,等裝好再回來。**

"After installation finishes, run `git --version` again to confirm it works."

*安裝完成後,再跑一次 git --version 確認可以用。*

---

## ⑤ Install the VEX Extension | 安裝 VEX 擴充功能 (5 min)

"Now we're going to install the VEX Robotics extension. This extension knows how to talk to the robot, has the right compiler, and helps VS Code understand VEX code."

*現在我們要裝 VEX Robotics 擴充功能。這個擴充功能會跟機器人通訊、有正確的編譯器、也幫 VS Code 看懂 VEX 程式碼。*

"Click the Extensions icon in the Activity Bar — the one that looks like four squares. Or press Shift + Command + X."

*按 Activity Bar 上 Extensions 的 icon——長得像四個方塊那個。或是按 Shift + Command + X。*

"In the search bar at the top, type: VEX Robotics"

*在最上面的搜尋欄打:VEX Robotics*

"You should see two results. The one we want is just called **'VEX Robotics'** — published by VEX Robotics. Don't click 'VEX Robotics Feedback', that's a different one. Click the blue **Install** button."

*你應該會看到兩個結果。我們要的是叫做 VEX Robotics 的那個——出版者是 VEX Robotics。**不要**按 VEX Robotics Feedback,那是不同的。按藍色的 Install 按鈕。*

📌 **這時擴充功能會在背景下載 SDK 和 toolchain,大約 200MB,要等 3-5 分鐘。**

"This is going to take a few minutes because it's downloading the C++ compiler and the VEX SDK. While we wait, let me start telling you about the difference between Java and C++."

*這會花幾分鐘,因為它在下載 C++ 編譯器和 VEX SDK。等待的時候,我先開始跟你講 Java 和 C++ 的差別。*

📌 **跳到 ⑦ 開始講概念,等裝完再回 ⑥。**

"Once it's done, you should see a small VEX robot icon appear in your Activity Bar on the left. That means it worked."

*裝好後,你會看到 Activity Bar 左邊出現一個小機器人 icon。那就表示成功了。*

---

## ⑥ Clone the repository | 把程式碼下載下來 (10 min)

"Now we're going to download the VEX code from GitHub onto your computer. This is called 'cloning a repository'."

*現在我們要從 GitHub 把 VEX 程式碼下載到你的電腦上。這個動作叫做 "clone 一個 repository"。*

"Open the terminal again with Control + backtick. We need to pick a place to put the code. Let's use a folder called Developer in your home directory. Type this:"

*再開一次 terminal(Control + 反引號)。我們要選一個地方放程式碼。我們用 home 目錄底下一個叫 Developer 的資料夾。打這個指令:*

```bash
mkdir -p ~/Developer
cd ~/Developer
```

"The first command creates the folder if it doesn't exist. The second command moves into that folder. Make sense?"

*第一個指令是「如果資料夾不存在就建一個」。第二個指令是「進入那個資料夾」。懂嗎?*

📌 **等學生點頭或問問題。**

"Now we're going to clone the VEX repo. Type this:"

*現在我們要 clone VEX 的 repo。打這個:*

```bash
git clone https://github.com/VEX-Robotics/VAIC_25_26.git
```

📌 **等下載完成,大約 30 秒到 1 分鐘。**

"Done? Great. Now let's look at what we got. Type:"

*下載完了嗎?很好。我們來看看下載到了什麼。打:*

```bash
ls VAIC_25_26
```

"You should see four folders and a few files — exactly the same structure we saw on GitHub earlier."

*你應該會看到四個資料夾跟幾個檔案——就是剛剛在 GitHub 上看到的結構。*

"Now let's go into the C++ project folder:"

*現在進去 C++ 專案資料夾:*

```bash
cd VAIC_25_26/V5Example/ai_demo
```

"And let's open this folder in VS Code:"

*然後在 VS Code 裡打開這個資料夾:*

```bash
code .
```

📌 **如果 `code .` 指令找不到,叫學生用 VS Code 選單 File → Open Folder,選 ai_demo 那個資料夾。**

"If that command doesn't work, no problem. Go to VS Code, click File at the top, then Open Folder, and navigate to `Developer/VAIC_25_26/V5Example/ai_demo`."

*如果那個指令沒用,沒關係。去 VS Code 點上面的 File,然後 Open Folder,找到 Developer/VAIC_25_26/V5Example/ai_demo。*

📌 **第一次打開資料夾,VS Code 會問 "Do you trust the authors?",按 Yes/Trust。**

"VS Code might ask 'Do you trust the authors of the files in this folder?' — click 'Yes, I trust the authors'. We're opening official VEX code, so it's safe."

*VS Code 可能會問「你信任這個資料夾裡檔案的作者嗎」——按 Yes, I trust the authors。我們打開的是官方 VEX 程式碼,很安全。*

"Awesome! On the left side, you should now see the project files. Click on the `include` folder to expand it. You should see five `.h` files."

*太棒了!左邊應該看得到專案檔案。點開 include 資料夾,你應該看到五個 .h 檔。*

---

## ⑦ Java vs C++ — The big picture | Java 跟 C++ 的差別 (10 min)

📌 **這段可以在裝 extension 等待時講,或裝完後再講。**

"OK, before we open any code, let me explain the most important difference between Java and C++ that you need to know."

*OK,在打開任何程式碼之前,我來解釋你最需要知道的 Java 跟 C++ 差別。*

"In Java, when you write a class — let's say a class called `Robot` — you put **everything** in one file called `Robot.java`. The class declaration, all the methods, all the implementations — everything in one place. Right?"

*在 Java,當你寫一個 class——比如說一個叫 Robot 的 class——你把**所有東西**放在一個叫 Robot.java 的檔案。class 宣告、所有 method、所有實作——全部在同一個地方。對吧?*

"In C++, that one file gets **split into two files**. Let me show you with a simple example."

*在 C++,那一個檔案會被**拆成兩個檔案**。我用一個簡單的例子給你看。*

📌 **可以分享螢幕,在 VS Code 裡打開新檔案打範例,或在 terminal 裡 cat 一個簡單範例。**

"In C++, you would have:
- A file called `Robot.h` — this is the **header file**. It just *describes* the class. It says 'here is a class called Robot, it has these methods, it has these variables'. But it doesn't say how anything actually works.
- A file called `Robot.cpp` — this is the **implementation file**. It has the actual code that makes the methods do their job."

*在 C++,你會有:*
- *一個叫 Robot.h 的檔案——這是 header file。它只「描述」這個 class。它說「這裡有一個叫 Robot 的 class,它有這些 method、這些變數」。但它不說任何東西實際怎麼運作。*
- *一個叫 Robot.cpp 的檔案——這是實作檔。裡面有真正讓 method 做事的程式碼。*

"Think of it like a restaurant menu and a kitchen. The menu (`.h`) tells you what dishes exist. The kitchen (`.cpp`) is where the food actually gets cooked."

*想成餐廳菜單跟廚房。菜單(.h)告訴你有哪些菜。廚房(.cpp)是真正做菜的地方。*

"And here's the cool part: when you read C++ code, you usually only need to read the `.h` files to understand **what a piece of code can do**. You don't need to read the `.cpp` files unless you want to know the exact details. This is exactly what we're going to do today."

*而且重點來了:讀 C++ 程式碼的時候,你通常只需要讀 .h 檔就能知道「這段程式可以做什麼」。除非你想知道細節,不然不用讀 .cpp 檔。這就是我們今天要做的事情。*

"Got it? Any questions before we open a real file?"

*懂了嗎?在我們打開真的檔案之前有沒有問題?*

📌 **回答問題。常見問題:「為什麼要拆成兩個?」答:歷史原因 + 編譯效率,但你現在不用知道細節。**

---

## ⑧ Read our first header: ai_functions.h | 讀第一個 header 檔 (15 min)

"OK, let's read a real header file. In VS Code, click on `include` in the side bar, then click on `ai_functions.h`."

*OK,我們來讀一個真的 header 檔。在 VS Code 側邊欄點 include,然後點 ai_functions.h。*

📌 **學生打開後,這個檔案大約 46 行,很短。從上往下逐段講。**

"This is a small file, only about 40 lines. Let's read it from top to bottom together."

*這是一個小檔案,大概 40 行。我們從頭到尾一起讀。*

### Lines 1–11: Comments | 註解

"The first eleven lines are just a comment block. The `/*` starts a comment and the `*/` ends it. **Exactly the same as Java.** It just tells you what this file is and who wrote it. We can skip past it."

*前十一行只是註解區塊。/* 開始註解,*/ 結束註解。**跟 Java 一樣**。只是告訴你這個檔案是什麼、誰寫的。可以跳過。*

### Lines 13–14: #include statements | #include 語句

"Now look at lines 13 and 14:"

*看一下第 13 跟 14 行:*

```cpp
#include <vex.h>
#include <robot-config.h>
```

"In Java, you write `import com.something.SomeClass;` to use code from another file. In C++, we write `#include` instead. Same idea — 'I want to use stuff from this other file'."

*在 Java,你寫 import com.something.SomeClass; 來用別的檔案的程式碼。在 C++ 我們改寫 #include,意思一樣——「我要用另一個檔案的東西」。*

"There's a tiny difference in the brackets. `<vex.h>` with angle brackets means 'look for this in the standard places where libraries are installed'. If you see `\"something.h\"` with double quotes, that means 'look for it next to my own files'. Don't worry about this too much — just notice the pattern."

*括號有一個小差別。<vex.h> 用尖括號表示「去 library 安裝的標準位置找」。如果看到 "something.h" 用雙引號,表示「在我自己檔案旁邊找」。先不用太在意——知道有這個差別就好。*

### Lines 16–19: enum | 列舉

"Lines 16 to 19 — look at this:"

*第 16 到 19 行,看這個:*

```cpp
enum OBJECT {
    BallBlue,
    BallRed
};
```

"This is an `enum`. **Same word, same idea as in Java.** It says: 'There is a thing called OBJECT, and the only valid values are BallBlue or BallRed.' Easy."

*這是 enum。**跟 Java 同一個字、同一個概念**。它說:「有一個東西叫 OBJECT,合法的值只有 BallBlue 或 BallRed。」簡單。*

"One small difference: notice the **semicolon at the end**, after the closing curly brace. In C++, the `enum` block needs a semicolon after it. Java doesn't. This is one of the most common things you'll see — many things in C++ end with semicolons that Java doesn't have."

*一個小差別:注意**結束的大括號後面有分號**。在 C++,enum 區塊後面要分號。Java 不用。這是你會常常看到的差別——很多 C++ 要分號的地方 Java 不用。*

### Line 21: using namespace | 使用命名空間

```cpp
using namespace vex;
```

"This line says: 'I'm going to use lots of stuff from the vex library, so I don't want to type `vex::` in front of everything.' It's similar to a Java `import com.vex.*;` — 'import everything from this package'."

*這行說:「我等下要用很多 vex library 的東西,所以我不想每個前面都打 vex::。」類似 Java 的 import com.vex.*;——「把這個 package 的東西全部 import」。*

"In C++, `vex::` is how you say 'this thing belongs to the vex namespace'. The `::` is C++'s way of saying 'inside of'. In Java, you would use a dot: `vex.something`. In C++, you use double colon: `vex::something` for namespaces and static stuff."

*在 C++,vex:: 是「這個東西屬於 vex 這個 namespace」。:: 是 C++ 表示「裡面的」的方法。在 Java,你會用點:vex.something。在 C++ 對 namespace 和 static 的東西用兩個冒號:vex::something。*

### Lines 24–46: Function declarations | 函式宣告

"Now scroll down to the function declarations. Look at line 24:"

*往下看到函式宣告。看第 24 行:*

```cpp
double distanceTo(double target_x, double target_y);
```

"What does this look like to you?"

*你覺得這看起來像什麼?*

📌 **讓學生回答。期待的答案:看起來像 Java 的 method signature。**

"Exactly! It looks just like a Java method signature. It says: 'There is a function called `distanceTo`. It takes two `double` numbers as input. It returns a `double` number.' The only weird thing is the **semicolon at the end** and there's no curly brace after it."

*完全正確!看起來就跟 Java method signature 一樣。它說:「有一個函式叫 distanceTo。吃兩個 double 數字當輸入。回傳一個 double 數字。」唯一奇怪的是**結尾的分號**而且後面沒有大括號。*

"That semicolon is super important. It means: 'I am only **declaring** that this function exists. I'm not telling you how it works. The actual code is somewhere else — probably in a `.cpp` file.' Remember the menu and kitchen analogy? This is the menu listing."

*那個分號超重要。意思是:「我只是**宣告**這個函式存在。我不告訴你怎麼運作。真正的程式碼在別的地方——大概在某個 .cpp 檔。」記得菜單跟廚房的比喻嗎?這就是菜單上的項目。*

"Let's read the rest of the functions together. Look at the comments on top of each one — they tell you what the function does."

*我們一起讀剩下的函式。看每個函式上面的註解——告訴你函式做什麼。*

📌 **讓學生念每個函式上面的註解和函式名稱,確認他們抓到「這個檔案是個 API 清單」的感覺。**

"So if I asked you, 'using only this header file, can you tell me everything this code can do for the robot?' — what would you say?"

*所以如果我問你「只看這個 header 檔,你能告訴我這份程式可以幫機器人做哪些事嗎?」你會怎麼說?*

📌 **理想的答案應該包括:算到目標的距離、移動到位置、找特定物件、開到目標物、轉到特定角度、開特定距離、轉動 intake、停止 intake、開到球門。讓學生用自己的話講。**

"Great. You just learned to read a C++ header. That's the whole skill. **Read the includes, read the enum or class definitions, read the function names with their parameters.** That tells you the API."

*很好。你剛剛學會讀 C++ header 了。整個技能就這樣。**看 include、看 enum 或 class 定義、看函式名稱跟參數。**這就告訴你 API 是什麼。*

### Function overloading | 函式重載

"One more thing — look at lines 41 and 42:"

*還有一件事——看第 41 跟 42 行:*

```cpp
void runIntake(vex::directionType dir);
void runIntake(vex::directionType dir, int rotations, bool driveForward);
```

"Notice anything? **Two functions with the same name** but different parameters. This is called **function overloading**. Java has this exact same concept. It just means: 'You can call `runIntake` with one argument, or with three arguments — both will work.'"

*看到什麼?**兩個函式同名**但參數不同。這叫做 function overloading(函式重載)。Java 有完全一樣的概念。意思是:「你可以用一個參數呼叫 runIntake,或用三個參數呼叫,兩種都可以。」*

---

## ⑨ A more complex header: ai_jetson.h | 進階版 header (20 min)

"Now we're going to look at a bigger, more interesting file. Open `ai_jetson.h` in the include folder."

*現在我們要看一個更大、更有趣的檔案。打開 include 資料夾裡的 ai_jetson.h。*

📌 **這個檔案大約 165 行,有比較多東西。挑重點講就好,不要每行都念。**

"This file has more stuff in it. We don't need to understand every single line. I'll point out the parts that matter."

*這個檔案東西比較多。我們不用搞懂每一行。我會指出重要的部分。*

### Lines 14–15 and 165: Include guard | Include 防護

"Look at line 14, 15, and the very last line:"

*看第 14、15 行還有最後一行:*

```cpp
#ifndef AI_JETSON_H_
#define AI_JETSON_H_
// ... lots of code ...
#endif /* AI_JETSON_H_ */
```

"This is called an **include guard**. It's a C++ trick to make sure this file doesn't get included twice by accident. Java doesn't have this because Java handles it automatically."

*這叫 include guard。是 C++ 的小技巧,防止這個檔案不小心被 include 兩次。Java 沒有這個,因為 Java 自動處理。*

"You'll see this pattern in almost every header file you ever read. The pattern is: `#ifndef SOMETHING`, then `#define SOMETHING`, then all the code, then at the very bottom `#endif`. **You can just ignore it.** It's like wrapping paper around the file."

*你在幾乎每個 header 檔都會看到這個樣式。樣式是:#ifndef SOMETHING、然後 #define SOMETHING、然後所有程式碼、最底下 #endif。**你直接忽略就好。**就像檔案外面的包裝紙。*

"By the way, some modern C++ files use `#pragma once` instead — that does the same job in one line. Both are common."

*對了,有些比較新的 C++ 檔案改用 #pragma once,一行搞定同樣的事。兩種都很常見。*

### Lines 22–24 and 90–92: extern "C" | C 語言相容性

```cpp
#ifdef __cplusplus
extern "C" {
#endif
// ... stuff ...
#ifdef __cplusplus
}
#endif
```

"This block is something you can also ignore. It's saying 'treat the stuff between these braces as if it were the C language, not C++.' It's there for compatibility with older C code. **Just skip past it when you read.**"

*這個區塊也可以忽略。它說「把這對大括號之間的東西當作 C 語言、不要當 C++ 處理」。是為了跟舊的 C 程式碼相容。**讀的時候直接跳過。***

### Lines 26 and 29: #define | 巨集定義

```cpp
#define MAX_DETECTIONS 50
#define POS_GPS_CONNECTED 0x01
```

"`#define` creates a constant. The first one is saying 'wherever you see `MAX_DETECTIONS` in this code, treat it like the number 50'. It's similar to `public static final int MAX_DETECTIONS = 50;` in Java, but uglier."

*#define 建立常數。第一個說「這份程式裡看到 MAX_DETECTIONS 的地方,當作 50 處理」。類似 Java 的 public static final int MAX_DETECTIONS = 50;,但比較醜。*

"The `0x01` is just hex notation for the number 1. `0x` means 'this is hexadecimal'. Java has the same syntax. We'll see hex numbers a lot in robot code because they map to hardware bits."

*0x01 只是 1 的十六進位寫法。0x 表示「這是十六進位」。Java 有一樣的寫法。機器人程式碼裡你會看到很多十六進位數字,因為對應到硬體的 bit。*

### Lines 32–73: Structs | 結構體

"Now look at lines 32 to 42. This is a `struct`."

*看第 32 到 42 行。這是一個 struct。*

```cpp
typedef struct {
    int32_t framecnt;
    int32_t status;
    float x, y, z;
    float az;
    float el;
    float rot;
} POS_RECORD;
```

"A `struct` is basically a class that's just a bag of variables, with no methods. Think of it like a plain Java class with only public fields and no behavior. The name at the bottom — `POS_RECORD` — is the name of this struct."

*struct 基本上就是一個只裝變數、沒有 method 的 class。想成只有 public field、沒有 behavior 的 Java class。最下面的 POS_RECORD 是這個 struct 的名字。*

"Let's read what fields it has. The comments tell us:"

*我們看它有哪些欄位。註解告訴我們:*

- "`framecnt` — a frame counter"
- "`status` — 0 means all good"
- "`x, y, z` — the robot's position on the field in meters"
- "`az` — the robot's heading angle"
- "`el` and `rot` — pitch and roll angles"

📌 **讓學生用 Java 思維描述:就像一個 Position 物件,有這些 public field。**

"So whenever the code talks about a `POS_RECORD`, you know it's just a package of these numbers describing where the robot is and which way it's pointing."

*所以程式碼裡看到 POS_RECORD,你就知道它是一包數字,描述機器人在哪、朝哪個方向。*

"There are three more structs below: `IMAGE_DETECTION`, `MAP_DETECTION`, `DETECTION_OBJECT`, and `AI_RECORD`. Just look at their comments and field names — they describe objects the camera detected and where they are."

*下面還有三個 struct:IMAGE_DETECTION、MAP_DETECTION、DETECTION_OBJECT、AI_RECORD。看他們的註解跟欄位名稱就好——描述相機偵測到的物件跟它們在哪。*

### Lines 94–162: namespace and class | 命名空間與類別

"Now we get to the most important part. Scroll down to line 94."

*現在到了最重要的部分。捲到第 94 行。*

```cpp
namespace ai {
  class jetson  {
      public:
        jetson();
        ~jetson();

        int32_t    get_packets(void);
        int32_t    get_errors(void);
        int32_t    get_timeouts(void);
        int32_t    get_total(void);
        int32_t    get_data( AI_RECORD *map );
        void       request_map();

      private:
        // ... lots of stuff ...
    };
};
```

"OK, lots to unpack. Let's go piece by piece."

*OK,有很多要解釋。我們一塊一塊看。*

"`namespace ai { ... }` — this puts everything inside the `ai` namespace. Think of it like a Java package. Later, when other code wants to use this class, they'll write `ai::jetson` — meaning 'the jetson class inside the ai namespace'."

*namespace ai { ... }——把裡面的東西放進 ai 這個 namespace。想成 Java 的 package。等下別的程式要用這個 class 的時候,會寫 ai::jetson——意思是「ai namespace 裡的 jetson class」。*

"`class jetson { ... };` — and again, **don't forget the semicolon at the end of the closing brace.** Classes in C++ end with a semicolon. Always."

*class jetson { ... };——再說一次,**結尾的大括號後面別忘了分號。**C++ 的 class 一定要分號結尾。*

"Now look at this — `public:` and `private:` are not on each individual member like Java. In Java, you write `public int x;` for one variable. In C++, you write `public:` once, and **everything after it is public until you write something else like `private:`.** It's a section header, not a per-line modifier."

*看這個——public: 跟 private: 不是放在每個成員上,跟 Java 不一樣。在 Java 你寫 public int x; 一個變數一個。在 C++ 你寫一次 public:,然後**後面所有東西都是 public,直到你寫別的像是 private:。**它是區段標頭,不是每行的修飾詞。*

"So in this class, we have:
- A `public:` section with the constructor, destructor, and several methods
- A `private:` section with internal state
"

*所以這個 class 有:*
*- public: 區段,有建構子、解構子、跟幾個 method*
*- private: 區段,內部狀態*

### Constructor and destructor | 建構子與解構子

```cpp
jetson();
~jetson();
```

"`jetson()` is the **constructor**, just like Java. Same name as the class, no return type, gets called when you create an object."

*jetson() 是建構子,跟 Java 一樣。跟 class 同名、沒有回傳型別、創建物件時被呼叫。*

"`~jetson()` with the squiggle in front is the **destructor**. Java doesn't really have this — Java uses garbage collection. In C++, you have to clean up after yourself sometimes, and the destructor is where you do that. **You probably won't need to write one yourself.** Just recognize what it is when you see it."

*~jetson() 前面有個波浪號,叫**解構子(destructor)**。Java 沒有這個——Java 用 garbage collection。在 C++ 你有時候要自己清理,解構子就是清理的地方。**你大概不用自己寫一個。**看到認得就好。*

### The public methods | 公開的 method

"Now the important part — the public methods. These are the functions that other code can call on a `jetson` object. Let me read them out:"

*重要的部分——public method。這些是其他程式可以對 jetson 物件呼叫的函式。我念一下:*

- "`get_packets()` — returns how many packets we received"
- "`get_errors()` — returns how many errors happened"
- "`get_timeouts()` — returns how many timeouts happened"
- "`get_total()` — returns total amount of data"
- "`get_data(AI_RECORD *map)` — fills in an AI_RECORD with the latest data"
- "`request_map()` — asks the Jetson for a new map of objects"

"This is the **public API** of the jetson class. If your team writes code that uses the Jetson camera, these are the six functions you can call. That's it."

*這就是 jetson class 的**公開 API**。如果你的隊伍要寫程式用 Jetson 相機,你只能呼叫這六個函式。就這樣。*

### The pointer thing | 指標那個東西

"One thing you'll see a lot in C++ that doesn't exist in Java is the **asterisk** symbol. Look at `get_data(AI_RECORD *map)` — see the star before `map`?"

*你在 C++ 會看到很多 Java 沒有的東西,就是星號。看 get_data(AI_RECORD *map)——看到 map 前面的星號嗎?*

"`AI_RECORD *map` means: 'a pointer to an AI_RECORD'. A pointer is just an address — it's saying 'tell me where in memory the AI_RECORD lives, and I'll go fill it in for you'."

*AI_RECORD *map 意思是:「指向一個 AI_RECORD 的 pointer」。pointer 只是一個記憶體位址——意思是「告訴我那個 AI_RECORD 在記憶體哪裡,我會去幫你填資料」。*

"For now, **when you read C++ and see `Type *name`, just think of it as `Type name` for understanding what the function does**. The star is a C++ thing about how memory is passed. We can dive into pointers another day if you want to actually write C++."

*現在,**讀 C++ 看到 Type *name,就當作 Type name 來理解函式做什麼**。星號是 C++ 關於記憶體傳遞的東西。如果你之後真的要寫 C++,我們再深入講 pointer。*

### The private section | private 區段

"The `private:` section has all the internal state — packet counters, the current state of the parser, locks, buffers, and so on. **As a reader, you mostly skip this.** It's the implementation's bookkeeping."

*private 區段有所有內部狀態——packet counter、parser 目前的狀態、lock、buffer 之類的。**身為讀者,大部分時候跳過。**這是實作在記帳的東西。*

"The reason it's `private` is exactly the same reason as Java: outside code shouldn't touch this stuff. It's only for the class to manage itself."

*私有的原因跟 Java 一樣:外面的程式碼不該碰這些。只給 class 自己管理自己用。*

---

## ⑩ How .h and .cpp work together | .h 跟 .cpp 怎麼合作 (5 min)

"Let me show you one quick thing — how a `.h` file connects to its `.cpp` file."

*讓我快速給你看一個東西——.h 檔怎麼跟 .cpp 檔接起來。*

"In the side bar, expand the `src` folder and click `ai_jetson.cpp`."

*側邊欄展開 src 資料夾,點 ai_jetson.cpp。*

📌 **學生打開 ai_jetson.cpp 後,捲到看得到 method 實作的地方,例如 jetson::get_packets。**

"Find a function that looks like this:"

*找到一個長這樣的函式:*

```cpp
int32_t jetson::get_packets() {
    // ... actual code ...
}
```

"See the `jetson::` part before the function name? That's how C++ says 'this is the implementation of the `get_packets` method that belongs to the `jetson` class'. The `::` again — 'inside of'."

*看到函式名前面的 jetson:: 嗎?C++ 用這個說「這是屬於 jetson class 的 get_packets method 的實作」。又是 ::——「裡面的」。*

"Compare this with the header file. In the header, we said:"

*跟 header 檔比較。在 header 裡我們寫:*

```cpp
int32_t get_packets(void);   // in ai_jetson.h
```

"In the `.cpp` file, we say:"

*在 .cpp 檔我們寫:*

```cpp
int32_t jetson::get_packets() {  // in ai_jetson.cpp
    // ... real code here ...
}
```

"**Same return type. Same name. Same parameters. The difference is: the header has a semicolon and stops; the cpp has the actual code in curly braces, and the function name is prefixed with `jetson::` to say which class it belongs to.**"

*同樣的回傳型別、同樣的名字、同樣的參數。差別是:header 有分號就停了;cpp 在大括號裡有真正的程式碼,而且函式名前面加上 jetson:: 表示屬於哪個 class。*

"That's the link between the menu and the kitchen."

*這就是菜單跟廚房之間的連結。*

---

## ⑪ Big picture: main.cpp | 全貌:main.cpp (5 min)

"Last thing. Let's open `main.cpp` in the src folder. This is where the program starts."

*最後一件事。打開 src 裡的 main.cpp。這是程式開始的地方。*

📌 **打開 main.cpp,給學生看頂部的 #include 跟 main() 函式。**

"At the top, you see `#include "ai_functions.h"`. This pulls in all the function declarations we just read. Now `main.cpp` knows that functions like `goToObject` and `runIntake` exist."

*頂部看到 #include "ai_functions.h"。這把我們剛剛讀的所有函式宣告引入。現在 main.cpp 知道 goToObject、runIntake 這些函式存在了。*

"Scroll down to the `auto_Isolation` function around line 65. Look at this:"

*捲到第 65 行附近的 auto_Isolation 函式。看這個:*

```cpp
goToObject(OBJECT::BallBlue);
runIntake(directionType::fwd, 3, true);
goToGoal();
```

"Look familiar? These are functions we read in `ai_functions.h`. The robot is told: drive to a blue ball, run the intake forward for 3 rotations, then drive to the goal."

*眼熟嗎?這些就是我們在 ai_functions.h 讀過的函式。機器人被告知:開到藍球、intake 正轉 3 圈、開到球門。*

"And `OBJECT::BallBlue` — remember the `enum OBJECT { BallBlue, BallRed };` we read? That's where `BallBlue` came from."

*然後 OBJECT::BallBlue——記得我們讀過的 enum OBJECT { BallBlue, BallRed }; 嗎?BallBlue 就是從那來的。*

"This is the magic of headers. By reading just the header file, you knew enough to understand what this code does. **You didn't need to read the implementation to follow along.**"

*這就是 header 的魔法。只讀 header 檔,你就有足夠資訊看懂這段程式做什麼。**不用讀實作就能跟得上。***

---

## ⑫ Wrap up & Homework | 總結與作業 (5 min)

"Let's wrap up. Today you learned:"

*我們做總結。今天你學會了:*

1. "How to install VS Code, the VEX extension, and Git on your Mac"
   *怎麼在 Mac 上裝 VS Code、VEX 擴充功能、Git*
2. "How to clone code from GitHub"
   *怎麼從 GitHub clone 程式碼*
3. "The difference between `.h` and `.cpp` files in C++"
   *C++ .h 跟 .cpp 檔的差別*
4. "How to read a header file like a menu — looking at includes, enums, structs, classes, and function declarations"
   *怎麼像看菜單一樣讀 header——看 include、enum、struct、class、函式宣告*
5. "Six small differences between Java and C++ syntax — semicolons after class and enum, `::` for namespaces, `public:` as a section, the `~` destructor, `*` for pointers, and `#include` instead of import"
   *Java 跟 C++ 的六個小差別——class 跟 enum 後面的分號、:: 對應 namespace、public: 是區段、~ 解構子、* pointer、#include 取代 import*

"For homework, I want you to do this. Open `ai_robot_link.h` in VS Code. That's the third header file in the include folder. Don't try to write anything — just read it and answer these questions:"

*作業,我要你做這個。在 VS Code 打開 ai_robot_link.h——include 資料夾裡的第三個 header 檔。不用寫任何東西——讀它然後回答這些問題:*

1. "What `#include` files does it use?"
   *它 #include 了哪些檔案?*
2. "What namespace are things in?"
   *東西在哪個 namespace 裡?*
3. "What classes does it define?"
   *定義了哪些 class?*
4. "What public methods does each class have? Just list the names."
   *每個 class 有哪些 public method?把名字列出來就好。*

"You can write your answers in a text file or just on paper. Bring them to our next session and we'll go over them together."

*答案可以寫在 text 檔或紙上。下次上課帶來,我們一起看。*

"Any questions?"

*有問題嗎?*

📌 **回答問題。如果學生表現得很自信,可以提一下下次可能會看 main.cpp 裡 main() 函式怎麼運作,或開始寫一些 C++。**

"Great work today. See you next time!"

*今天做得很棒,下次見!*

---

## 🆘 Troubleshooting Cheat Sheet | 緊急狀況小抄

📌 **下面是上課中常見問題,純中文,給老師看的。**

### 學生 `git clone` 失敗
- 檢查網路連線
- 檢查指令有沒有打錯(常見:Robotics 拼成 Robitics)
- 如果是 corporate / school WiFi 有時候會擋 GitHub,叫他換成手機熱點試試

### `code .` 指令無效
- 沒關係,改用 VS Code 選單:File → Open Folder
- 如果想修好:在 VS Code 按 Cmd+Shift+P,搜 "Shell Command: Install 'code' command in PATH",執行一次就好

### VEX extension 安裝卡住或失敗
- 第一次裝會下載 SDK 跟 toolchain(約 200MB),要等
- 如果超過 10 分鐘還沒完成,叫他關掉 VS Code 重開,讓 extension 重新下載
- 若還是失敗,VS Code 版本可能太新或太舊,可以叫他到 https://code.visualstudio.com/updates 抓特定版本

### macOS 阻擋執行檔(Gatekeeper)
- 訊息類似「無法驗證開發者」
- 處理:系統設定 → 隱私權與安全性 → 最下面會有「仍要打開」按鈕

### VS Code 找不到 #include 的檔案(紅色波浪線)
- 大部分時候不影響閱讀,可以忽略
- 如果學生很介意,確認他打開的是 `ai_demo` 資料夾本身,不是 repo 根目錄
- C/C++ extension 應該會自動讀 .vscode 裡的設定

### 學生問「這個 `*` 到底是什麼」
- 如果只是要讀 code,告訴他「先當作普通變數理解」就好
- 如果學生很想懂,簡單解釋:`int x` 是「一個 int」,`int *x` 是「指向某個 int 的記憶體位址」
- 不要在這堂課深入講指標,會花太多時間

### 學生問「為什麼 C++ 要拆 .h 跟 .cpp」
- 簡單版:歷史原因 + 編譯效率(編譯器只要看 .h 就能編譯使用該 class 的程式碼,不用看實作)
- 不要展開講 declaration vs definition 的細節

---

## 📝 Tutor 自己的 Quick Reference | 老師快速參考

### Java vs C++ 對照(一頁版)

| Java | C++ | 備註 |
|------|-----|------|
| `import com.foo.Bar;` | `#include "Bar.h"` 或 `<bar.h>` | |
| `package com.foo;` | `namespace foo { ... }` | |
| `Foo.bar()` | `Foo::bar()` 或 `foo.bar()` 或 `foo->bar()` | 後者是透過 pointer |
| `public class Foo { ... }` | `class Foo { public: ... };` | **記得分號** |
| `public int x;` | `public:` 一次,後面都是 public | section,不是修飾詞 |
| `null` | `nullptr` | |
| `String` | `std::string` 或 `const char*` | |
| `Foo[] arr` | `Foo arr[]` 或 `std::vector<Foo>` | |
| `// 沒有對應` | `~Foo()` (destructor) | |
| `// 沒有對應` | `int *x` (pointer) | |
| `// 沒有對應` | `#define MAX 50` | C++ 巨集 |
| `// 沒有對應` | `#ifndef / #define / #endif` | include guard |

### 這個 repo 的檔案速查

```
V5Example/ai_demo/
├── include/
│   ├── ai_functions.h     ← 簡單,適合先讀(46 行)
│   ├── ai_jetson.h        ← 進階,有 class/struct/namespace(165 行)
│   ├── ai_robot_link.h    ← 作業讓學生自己讀
│   ├── robot-config.h
│   └── vex.h              ← 把所有東西兜起來的入口
├── src/
│   ├── main.cpp           ← 程式入口,看 auto_Isolation()
│   ├── ai_functions.cpp
│   ├── ai_jetson.cpp
│   ├── ai_robot_link.cpp
│   └── dashboard.cpp
└── makefile               ← 不用碰
```

---

*End of script | 稿子結束*
