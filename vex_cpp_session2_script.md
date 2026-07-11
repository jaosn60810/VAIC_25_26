# VEX C++ Session 2 — Reading Script (Lecture Edition)
## VEX C++ 教學課程逐字稿 · 第二堂(中英對照 · 純講述加厚版)
### 主題:深入讀 header —— structs、namespace、class,以及 .h 如何接到 .cpp

> **使用說明 / How to use this script:**
> - 黑色英文 = 老師對學生講的話(直接念出來)
> - *斜體中文* = 中文意思(老師看的,不要念)
> - 📌 灰色框 = 老師的內部提示(純中文,不要念)
> - 這是**純講述版**:設計成老師一個人從頭講到尾,不依賴學生互動。所有「問句」都是老師自問自答,直接往下念即可。
> - 整堂課預計 **60 分鐘**。每段標題後有「**到此累計約 X 分**」的進度檢查點,你講太快時可以對照。
> - 學生用 **Mac**,接續上一堂(已裝好環境、clone 完 repo、讀完 `ai_functions.h`、學到 function overloading)

---

## 🧭 給老師:怎麼確保講滿 60 分鐘(純講述版)

📌 **你講得快、怕撐不滿。這份稿子已經把口白加厚成約兩倍。再給你三個保險:**

1. **照進度檢查點走。** 每段標題有「到此累計約 X 分」。如果你提早到,就放慢、把該段的比喻再講一次——重複講是好的教學,學生會記得更牢。
2. **善用「自問自答」。** 稿子裡的問句(例如 "So why does C++ do this?")念出來之後,稍微停一下(2 秒),再念下面的答案。這個停頓 + 你指著螢幕的動作,自然會吃掉時間。
3. **還是太早就加模組。** 檔案最後有「🧰 加長模組」,真的還剩很多時間,就加講 `ai_robot_link.h`、建構子裡的背景 thread、或十六進位小知識。

📌 **進度總表(對照用):**
```
00–10 分  ① 開場 + 回顧 + 背景故事
10–15 分  ② 暖身:重開專案 + 回看 findTarget
15–17 分  ③ ai_jetson.h 全景
17–25 分  ④ 包裝紙(guard / extern "C" / #define)
25–40 分  ⑤ structs ★(主菜,最慢)
40–52 分  ⑥ namespace + class jetson ★
52–58 分  ⑦ .h ↔ .cpp
58–66 分  ⑧ main.cpp ★(高潮)
66–70 分  ⑨ 總結 + 作業
```

---

## 🧰 上課前 5 分鐘檢查 (Pre-class check)

📌 **老師上課前自己檢查:**
- [ ] 視訊 / 螢幕分享測試過
- [ ] 自己這邊把 `V5Example/ai_demo` 在 VS Code 打開備用
- [ ] 把 `include/ai_jetson.h`、`src/ai_jetson.cpp`、`src/main.cpp` 三個檔先開在分頁
- [ ] 記得本堂「一句話高潮」:`main.cpp` 的 `local_map.pos.x`(struct 巢狀的回報)
- [ ] 這份稿子開在另一個視窗

---

## ① 開場 + 回顧 + 背景故事 | Opening, recap & context

📌 **到此累計約 10 分。這段全程你講,把背景講飽,後面就不趕。**

"Hey, good to see you again! How have you been? ... Awesome. Let's jump back in."

*嘿,很高興又見面!最近好嗎?……很好。我們繼續。*

"So let me remind you where we are, because last time we actually did a lot. In our first session together, we did two big things. First, we set up your whole computer from scratch — we installed VS Code, we made sure Git was working, we installed the VEX Robotics extension, and we downloaded — or in Git language, we *cloned* — the real VEX AI competition code from GitHub onto your Mac. That's the same code that real teams compete with. So you're not looking at a toy example. You're looking at the actual thing."

*我先幫你回憶一下我們進度到哪,因為上次其實做了很多。第一堂我們做了兩件大事。第一,從零把你的電腦設好——裝了 VS Code、確認 Git 能用、裝了 VEX Robotics 擴充功能,還從 GitHub 把真正的 VEX AI 比賽程式碼下載(用 Git 的話叫「clone」)到你的 Mac。那是真正比賽隊伍在用的程式碼。所以你看的不是玩具範例,是真槍實彈的東西。*

"And the second thing we did was the important one. We learned how to *read* C++ code, even though you've never written a line of C++. And the trick was one big idea. Do you remember it? The big idea was: a C++ program is usually split into two kinds of files. There are `.h` files, which we call *header files*, and there are `.cpp` files. And I gave you an analogy — the restaurant. The header file, the `.h`, is like the *menu*. It tells you what dishes exist — what the code can do — without telling you how they're cooked. And the `.cpp` file is like the *kitchen* — that's where the actual cooking happens, the real step-by-step code. And the punchline was: when you just want to *understand* what code does, you usually only need to read the menu. You almost never need to go into the kitchen."

*第二件事才是重點。我們學會了怎麼「讀」C++,即使你一行 C++ 都沒寫過。訣竅是一個大概念。記得嗎?大概念是:一個 C++ 程式通常被拆成兩種檔案。`.h` 檔,我們叫它 header file;還有 `.cpp` 檔。我給過你一個比喻——餐廳。header 檔(`.h`)像「菜單」,它告訴你有哪些菜——程式能做什麼——但不告訴你怎麼做。`.cpp` 檔像「廚房」——真正做菜、一步一步的程式碼在那。重點是:當你只想「看懂」程式做什麼,通常只要讀菜單,幾乎不用進廚房。*

"And then we read our very first real header file together — `ai_functions.h`. And you saw that it looked surprisingly familiar, right? Because C++ and Java look a lot alike. We saw an `enum`, just like Java. We saw function declarations that looked just like Java method signatures. And the very last thing we looked at was two functions with the same name, `runIntake`, but with different parameters — and that's called *function overloading*, which Java has too. So you already know more C++ than you think."

*然後我們一起讀了第一個真的 header 檔——`ai_functions.h`。你發現它意外地眼熟,對吧?因為 C++ 跟 Java 長得很像。我們看到 `enum`,跟 Java 一樣。看到函式宣告,跟 Java 的 method signature 一樣。最後看的是兩個同名的函式 `runIntake`,但參數不同——那叫 function overloading(函式重載),Java 也有。所以你會的 C++ 比你以為的多。*

"OK. So that's where we are. Now let me tell you where we're *going* today, and I want to give you a little bit of background first, because it'll make today make a lot more sense."

*好。進度就到這。現在我跟你說今天要去哪,我想先給你一點背景,因為這會讓今天的東西好懂很多。*

"Here's the big picture of what this robot actually is. In the VEX AI competition, your robot isn't just driven by a human with a controller. Part of the match is fully autonomous — the robot has to think for itself. And to think for itself, it needs two things: it needs to know *where it is* on the field, and it needs to know *what it can see* around it. Now, the main brain of the VEX robot — the V5 brain — is good at controlling motors, but it's not powerful enough to do real computer vision, like recognizing balls and goals in a camera image. So the robot has a *second* computer on board. It's a small AI computer called a Jetson — it's made by NVIDIA — and it has a camera. The Jetson's whole job is to look at the world through the camera, recognize objects like the blue balls and red balls, figure out where they are, and then send all of that information over to the V5 brain."

*我給你看這個機器人到底是什麼。在 VEX AI 比賽,你的機器人不是只靠人用搖桿開。比賽有一部分是全自動的——機器人要自己思考。要自己思考,它需要兩樣東西:它要知道「自己在場上的哪裡」,還要知道「周圍看得到什麼」。V5 主控板很會控制馬達,但它的運算力不足以做真正的電腦視覺,例如在相機畫面裡認出球和球門。所以機器人上面有「第二台」電腦,是一台小型 AI 電腦叫 Jetson(NVIDIA 出的),配一個相機。Jetson 的工作就是透過相機看世界、認出藍球紅球這些物件、算出它們在哪,然後把這些資訊全部傳給 V5 主控板。*

"So picture the flow: the camera sees the field, the Jetson does the heavy AI thinking and produces a little package of data that basically says 'here's where the robot is, and here are all the objects I can see and where they are.' Then it ships that package across a cable to the V5 brain. And the V5 brain reads that package and decides what to do — drive to that ball, pick it up, go to the goal. Keep that flow in your head, because *every single file we read today is part of that flow.* The file we're about to read, `ai_jetson.h`, is literally the code on the V5 side that describes that package of data and receives it. So now it's not abstract — you know what it's *for*."

*想像這個流程:相機看場地,Jetson 做繁重的 AI 運算,產生一小包資料,基本上在說「機器人在這裡,還有我看到的所有物件和它們的位置」。然後它把這包資料透過排線送到 V5 主控板。V5 主控板讀這包資料,決定要做什麼——開去那顆球、撿起來、去球門。把這個流程記在腦中,因為「今天讀的每一個檔案都是這個流程的一部分」。我們等下要讀的 `ai_jetson.h`,就是 V5 這端用來「描述那包資料」並「接收它」的程式碼。所以它不再抽象了——你知道它是「幹嘛用的」。*

"So here's the plan for today, in three parts. Part one: we're going to read a bigger header file called `ai_jetson.h`, and inside it we'll meet two brand-new C++ ideas — *structs*, which describe the shape of data, and a *class*, which is the worker that does the job. Part two: I'll show you exactly how a header file `.h` connects to its kitchen file `.cpp` — the link between the menu and the cooking. And part three, the fun part: we'll open the main program, `main.cpp`, and I'll show you something really satisfying — you'll be able to understand what the robot is doing using *only* the things we read in the headers. You won't believe how much you can read by the end. Let's get into it."

*所以今天的計畫,三部分。第一:讀一個比較大的 header 檔 `ai_jetson.h`,裡面會遇到兩個全新的 C++ 概念——struct(描述資料的形狀)和 class(做事的工人)。第二:我會給你看 header `.h` 怎麼接到它的廚房檔 `.cpp`——菜單和做菜之間的連結。第三,有趣的部分:我們打開主程式 `main.cpp`,我會給你看一個很爽的東西——你會「只用」我們在 header 讀過的東西,就看懂機器人在做什麼。你不會相信到最後你能讀懂多少。開始吧。*

---

## ② 暖身:重開專案 + 回看 ai_functions.h | Warm-up

📌 **到此累計約 15 分。**

"First, let's make sure your project is open. Look at VS Code. On the left side you should see a file panel. The folder we care about is called `ai_demo`. If you still have it open from last time, perfect. If your VS Code opened up empty, no problem — go up to the top menu, click File, then 'Open Recent', and you should see `ai_demo` in the list. Or you can click File, then 'Open Folder', and navigate to Developer, then VAIC_25_26, then V5Example, then ai_demo. Go ahead and get that open."

*首先確認你的專案開著。看 VS Code。左邊應該有檔案面板。我們要的資料夾叫 `ai_demo`。上次的還開著就完美。如果 VS Code 開起來是空的,沒關係——上面選單 File → Open Recent,清單裡應該有 `ai_demo`。或 File → Open Folder,找到 Developer → VAIC_25_26 → V5Example → ai_demo。把它打開。*

📌 **若跳出 "Do you trust the authors?",按 Yes。若左邊看不到檔案,確認開的是 ai_demo 本身。**

"Good. On the left, you should see two folders — `include` and `src`. Remember those? `include` holds the header files, the menus. `src` holds the `.cpp` files, the kitchens. We're going to live mostly in `include` today."

*很好。左邊應該看到兩個資料夾——`include` 和 `src`。記得吧?`include` 放 header 檔(菜單),`src` 放 `.cpp` 檔(廚房)。今天我們大部分待在 `include`。*

"Now, before we open today's new file, I want to do a thirty-second warm-up to connect back to last time. Click on `include`, and open `ai_functions.h` — the file we read last session. Don't read the whole thing. Just look at line 30. It says: `DETECTION_OBJECT findTarget(OBJECT type);`. Now last time, when we read this line, I kind of glossed over the return type. I just said 'this function finds a target and gives you back some object the camera detected.' The return type is `DETECTION_OBJECT`. And back then, that was just a mysterious word — we didn't know what was inside it."

*在打開今天的新檔之前,我想做個 30 秒的暖身,接回上次。點 `include`,打開 `ai_functions.h`——上次讀的檔。不用全讀。只看第 30 行:`DETECTION_OBJECT findTarget(OBJECT type);`。上次讀這行時,我對回傳型別輕輕帶過,只說「這函式找到一個目標,回傳相機偵測到的某個物件」。回傳型別是 `DETECTION_OBJECT`。那時它只是個神秘的詞——我們不知道它裡面有什麼。*

"Well, here's the cool thing. Today's file, `ai_jetson.h`, is the file where `DETECTION_OBJECT` is actually *defined*. So by the end of today, you're going to know exactly what's inside a `DETECTION_OBJECT` — every single field. This is how reading code works in the real world: you bump into a name in one file, and you go find the file where it's described. We're about to do exactly that. Let's open it."

*酷的地方來了。今天的檔 `ai_jetson.h`,就是 `DETECTION_OBJECT` 真正被「定義」的地方。所以到今天結束,你會完全知道 `DETECTION_OBJECT` 裡面有什麼——每一個欄位。這就是真實世界讀程式碼的方式:你在一個檔案撞見一個名字,就去找它被描述的那個檔案。我們等下就要做這件事。打開它吧。*

---

## ③ 全景:打開 ai_jetson.h | Big picture

📌 **到此累計約 17 分。**

"In the side bar, under `include`, click on `ai_jetson.h`. ... Got it open? Great."

*側邊欄的 `include` 底下,點 `ai_jetson.h`。……開好了?很好。*

"OK, first reaction — this file is bigger than the last one. It's about 165 lines. And I want you to take a breath, because here's the most important thing I'll say in this whole section: **we are not going to read every line, and you are not supposed to understand every line.** Real programmers don't read code like a novel, word by word, top to bottom. They skim. They look for the important landmarks and they skip the rest. So I'm going to teach you to skim like a pro."

*好,第一反應——這個檔比上一個大。大概 165 行。深呼吸,因為這整段我要講的最重要的一句話是:「我們不會每行都讀,你也不該每行都懂。」真正的程式設計師不會像讀小說一樣一個字一個字從頭讀到尾。他們是「掃」的。找重要的地標,其他略過。我來教你像高手一樣掃。*

"And here's the secret that makes this file un-scary. This entire 165-line file really only has three kinds of things in it. Number one: *wrapping paper* — boilerplate at the top and bottom that you can completely skip. Number two: *structs* — these describe the shape of data, like a form with labeled blank boxes. And number three: *one class* — that's the worker that actually talks to the Jetson camera. That's it. Wrapping paper, data shapes, one worker. Once you see it that way, 165 lines stops being scary. Let's take them in order, and we'll go fast through the boring stuff."

*還有一個讓這檔不可怕的秘密。這整個 165 行的檔,其實只有三種東西。第一:「包裝紙」——頭尾的樣板,可以完全跳過。第二:「struct」——描述資料的形狀,像一張有標籤空格的表格。第三:「一個 class」——真正跟 Jetson 相機溝通的工人。就這樣。包裝紙、資料形狀、一個工人。一旦你這樣看,165 行就不可怕了。我們照順序來,無聊的快速帶過。*

---

## ④ 包裝紙:可以略過的東西 | The wrapping paper

📌 **到此累計約 25 分。這段把「為什麼可以略過」講清楚,順便吃時間。**

### Include guard(14–15 行 + 165 行)

"Let's start at the very top of the real code. Look at lines 14 and 15. They say `#ifndef AI_JETSON_H_` and `#define AI_JETSON_H_`. Now scroll all the way to the bottom — the very last line, 165 — and you'll see `#endif`. So this whole file is wrapped between those lines, like a box."

*從真正程式碼的最上面開始。看第 14、15 行:`#ifndef AI_JETSON_H_` 和 `#define AI_JETSON_H_`。現在捲到最底——最後一行 165——你會看到 `#endif`。所以整個檔被包在這之間,像個盒子。*

"This wrapper is called an *include guard*. And let me explain what it's protecting against, because it tells you something about how C++ works that's different from Java. In C++, when one file says `#include` of another file, the compiler *literally pastes the entire text* of that file in. It's a copy-paste, before the program is even compiled. Now imagine this file, `ai_jetson.h`, gets pasted into the program. And then, because of some other chain of includes, it accidentally gets pasted in a *second* time. Now you've defined everything in here twice — two copies of the same struct, the same class — and the compiler throws an error, because it doesn't know which one you mean."

*這個外框叫 include guard。我解釋一下它在防什麼,因為這透露了 C++ 跟 Java 不一樣的地方。在 C++,當一個檔案 `#include` 另一個檔案,編譯器會「把那個檔的整段文字貼進來」。是複製貼上,而且在程式還沒編譯之前就做了。現在想像這個 `ai_jetson.h` 被貼進程式。然後因為某串 include 的關係,它不小心被貼了「第二次」。現在裡面所有東西都被定義了兩次——同一個 struct、同一個 class 各兩份——編譯器就報錯,因為它不知道你指哪一個。*

"The include guard prevents that. The logic is simple: the first time the file gets pasted in, it sets a little flag — that's the `#define AI_JETSON_H_`. The second time it gets pasted in, it checks 'hey, is that flag already set?' — that's the `#ifndef`, which means 'if not defined' — and since the flag is already there, it skips the entire file down to the `#endif`. So the contents only ever get included once. Java, by the way, never has this problem, because Java doesn't paste text — it looks up classes a smarter way. So this is purely a C++ thing. And the bottom line for you as a reader is simple: **when you see this guard, just ignore it. It's wrapping paper.** Some newer files use a single line, `#pragma once`, that does the same job. Same idea, ignore it too."

*include guard 就是防這個的。邏輯很簡單:第一次被貼進來時,它設一個小旗標——就是 `#define AI_JETSON_H_`。第二次被貼進來時,它檢查「欸,那個旗標已經設了嗎?」——就是 `#ifndef`,意思是「如果還沒定義」——既然旗標已經在了,它就跳過整個檔案直到 `#endif`。所以內容只會被納入一次。順帶一提,Java 從來沒這問題,因為 Java 不貼文字,它用更聰明的方式找 class。所以這純粹是 C++ 的事。對你這個讀者的結論很簡單:「看到這個 guard,直接忽略,它是包裝紙。」有些較新的檔用一行 `#pragma once` 做同樣的事。一樣的概念,也忽略。*

### extern "C"(22–24 行 + 90–92 行)

"Next piece of wrapping paper. Look at lines 22 through 24. You'll see `#ifdef __cplusplus`, then `extern \"C\" {`, then `#endif`. And if you scroll down to lines 90 to 92, you'll see it close again with a `}`. So there's a big chunk of the file wrapped inside this `extern \"C\"` thing."

*下一塊包裝紙。看第 22 到 24 行:`#ifdef __cplusplus`、`extern "C" {`、`#endif`。捲到第 90 到 92 行,你會看到它用 `}` 關起來。所以檔案有一大塊包在這個 `extern "C"` 裡。*

"You can skip this one too, but let me tell you what it's for in one breath, because it connects back to our story. Remember I said the Jetson camera computer and the V5 brain both need to agree on the data? Well, the Jetson side is often programmed in the older C language, and the V5 side is C++. This `extern \"C\"` block is basically a compatibility handshake — it makes the data definitions in this file readable and consistent for *both* the C world and the C++ world, so that when the two computers send bytes to each other, they agree perfectly on the layout. The `#ifdef __cplusplus` part just means 'only do this handshake when we're being compiled as C++.' So it's a 'this file is designed to be shared between two languages' marker. For reading purposes: **skip it.**"

*這個也可以跳過,但我一口氣告訴你它幹嘛,因為它接回我們的故事。記得我說 Jetson 相機電腦和 V5 主控板都要對資料有共識嗎?Jetson 那端常常是用比較舊的 C 語言寫的,V5 這端是 C++。這個 `extern "C"` 區塊基本上是一個相容性握手——它讓這個檔裡的資料定義對「C 世界」和「C++ 世界」都能讀、都一致,這樣兩台電腦互傳 byte 時,對排列方式完全有共識。`#ifdef __cplusplus` 的意思只是「只有用 C++ 編譯時才做這個握手」。所以它是「這個檔設計成兩種語言共用」的標記。讀的時候:「跳過。」*

### #define(26 行、29 行)

"Two more small things, then we're done with wrapping paper. Look at line 26: `#define MAX_DETECTIONS 50`. And line 29: `#define POS_GPS_CONNECTED 0x01`. The keyword `#define` creates a named constant. The first line is saying: 'anywhere in this code you see the word `MAX_DETECTIONS`, treat it as the number 50.' In Java you'd write something like `static final int MAX_DETECTIONS = 50;`. Same idea, just a different, older style. And what's it for? It's the maximum number of objects the camera will report at once — fifty. We'll see it used in a minute."

*還有兩個小東西,然後包裝紙就講完了。看第 26 行:`#define MAX_DETECTIONS 50`。和第 29 行:`#define POS_GPS_CONNECTED 0x01`。關鍵字 `#define` 建立一個有名字的常數。第一行說:「這份程式裡看到 `MAX_DETECTIONS` 這個字的地方,都當作數字 50。」在 Java 你會寫類似 `static final int MAX_DETECTIONS = 50;`。一樣的概念,只是比較舊的寫法。它幹嘛用的?是相機一次最多回報的物件數量——五十個。等下會看到它被用到。*

"Quick note on that second one, the `0x01`. Whenever you see `0x` in front of a number, that just means the number is written in *hexadecimal* — base sixteen — instead of the normal base ten we count in. `0x01` is just the number 1. You'll see hex a lot in robot and hardware code, because hexadecimal lines up nicely with how the hardware stores bits. Java uses the exact same `0x` notation, so this isn't even new. For now: see `0x`, think 'oh, that's just a number written in hex,' and move on."

*第二個 `0x01` 快速說明一下。看到數字前面有 `0x`,就是這個數字用「十六進位」(16 進位)寫的,而不是我們平常數數的 10 進位。`0x01` 就是數字 1。機器人和硬體程式碼裡常看到十六進位,因為它跟硬體存 bit 的方式對得很整齊。Java 用一模一樣的 `0x` 寫法,所以這甚至不是新東西。現在:看到 `0x`,想「喔,只是用十六進位寫的數字」,往下走。*

"And that's all the wrapping paper. Notice what we just did — we looked at lines 14, 15, 22 to 24, 26, 29, 90 to 92, and 165, and we confidently said 'skip, skip, skip.' That is a real skill. Knowing what to ignore is half of reading code. Now let's get to the good stuff — the actual data."

*包裝紙就這些。注意我們剛做了什麼——我們看了第 14、15、22 到 24、26、29、90 到 92、165 行,然後很有自信地說「跳過、跳過、跳過」。這是真本事。知道什麼該忽略,是讀程式碼的一半功力。現在來看好東西——真正的資料。*

---

## ⑤ 資料的形狀:structs | The shape of the data ★

📌 **到此累計約 40 分。這是主菜,最慢、講最飽。每個 struct 都走過去。**

"Now look at line 31. This is our first `struct`. Let me read it to you and then we'll unpack it."

*看第 31 行。這是我們第一個 `struct`。我先念給你聽,然後拆解。*

```cpp
typedef struct {
    int32_t  framecnt;      // 第幾幀
    int32_t  status;        // 0 = 一切正常
    float    x, y, z;       // 場地座標,單位公尺
    float    az;            // heading 朝向(度)
    float    el;            // pitch 俯仰(度)
    float    rot;           // roll 翻滾(度)
} POS_RECORD;
```

"So what is a `struct`? Here's the simplest way to think about it: **a struct is a class that's pure data.** It has fields — variables — but no methods, no behavior. It just holds information. If you've seen a Java class that's nothing but a bunch of public fields, with no real methods, that's basically a struct. Another way to picture it: it's like a paper form. A form has labeled blank boxes — Name, Address, Phone number — and you fill them in. A struct defines what boxes exist. It's the shape of a piece of information."

*所以什麼是 `struct`?最簡單的想法是:「struct 是一個純資料的 class。」它有欄位——變數——但沒有方法、沒有行為。它只裝資訊。如果你看過一個 Java class 裡面只有一堆 public 欄位、沒有真正的方法,那基本上就是一個 struct。另一個比喻:它像一張紙本表格。表格有貼標籤的空格——姓名、地址、電話——你去填。struct 定義了「有哪些格子」。它是一份資訊的形狀。*

"Now, one quirk of C++ syntax: notice the struct doesn't have its name at the top. The name is at the *bottom* — see it? `POS_RECORD`. That `typedef struct { ... } POS_RECORD;` pattern is an older C-language style, and the name you care about is the one at the end. So this struct is called `POS_RECORD` — a position record. And as a reader, your move is always the same: look at the name, then read the field names and the comments next to them. The author wrote those comments to help you, so use them."

*C++ 語法的一個怪癖:注意這個 struct 的名字不在最上面。名字在「最下面」——看到嗎?`POS_RECORD`。`typedef struct { ... } POS_RECORD;` 這個寫法是比較舊的 C 語言風格,你要在意的名字是最後那個。所以這個 struct 叫 `POS_RECORD`——位置記錄。身為讀者,你的動作永遠一樣:看名字,然後讀欄位名稱和旁邊的註解。作者寫那些註解是為了幫你,所以拿來用。*

"So let's actually read what's in a `POS_RECORD`. It has a `framecnt`, a frame counter — basically 'which snapshot in time is this.' It has a `status` — and the comment tells us zero means all good. Then it has `x`, `y`, and `z` — those are the robot's position on the field, measured in meters, and the comment even tells us that position zero-zero is the center of the field. Then `az`, `el`, and `rot` — those are three angles describing which way the robot is tilted and pointing: `az` is the heading, which direction it's facing; `el` is pitch, nose up or down; `rot` is roll, tilting side to side. So step back: a `POS_RECORD` is just a neat little package that answers one question — 'where is the robot, and which way is it oriented?' That's it. Six-ish numbers that pin down the robot in space."

*我們真的來讀 `POS_RECORD` 裡有什麼。它有 `framecnt`,幀計數——基本上是「這是哪個時間點的快照」。有 `status`——註解告訴我們 0 表示一切正常。然後 `x`、`y`、`z`——機器人在場上的位置,單位公尺,註解甚至告訴我們位置 0,0 是場地中心。然後 `az`、`el`、`rot`——三個角度,描述機器人怎麼傾斜和朝向:`az` 是 heading(朝哪個方向);`el` 是 pitch(機頭上下);`rot` 是 roll(左右翻滾)。退一步看:`POS_RECORD` 就是一個整齊的小包裹,回答一個問題——「機器人在哪、朝哪個方向?」就這樣。大約六個數字,把機器人在空間裡釘住。*

"Let me make it concrete. Imagine the robot is sitting dead center of the field, facing straight ahead, perfectly flat. Then in its `POS_RECORD`, `x` is zero, `y` is zero, `z` is basically zero, the angles are zero, and `status` is zero meaning everything's healthy. Now the robot drives forward two meters and turns ninety degrees — now `y` might be 2.0, and `az`, the heading, is 90. See how this little struct is like the robot's GPS readout? That's all it is."

*我講具體一點。想像機器人坐在場地正中央,朝正前方,完全平。那它的 `POS_RECORD` 裡,`x` 是 0、`y` 是 0、`z` 基本上是 0、角度都是 0、`status` 是 0 表示一切健康。現在機器人往前開兩公尺、轉 90 度——現在 `y` 可能是 2.0,而 `az`(heading)是 90。看到這個小 struct 像機器人的 GPS 讀數嗎?它就是這樣。*

"OK, let's keep going. There are a few more structs, and we'll go a bit quicker because you've got the idea now. Look at lines 44 to 49 — this one's called `IMAGE_DETECTION`. Read the comment: it describes an object the camera sees, but specifically *in the camera image*, in pixels. It has an `x` and `y` — the center of the object in the picture — and a `width` and `height` — the size of the box around it. So if you've ever seen one of those photos where the software draws a rectangle around a face, that rectangle is exactly an `IMAGE_DETECTION`. It's where the object is *on the screen*."

*好,繼續。還有幾個 struct,我們稍微快一點,因為你抓到概念了。看第 44 到 49 行——這個叫 `IMAGE_DETECTION`。讀註解:它描述相機看到的一個物件,但特別是「在相機畫面裡」,單位是像素。它有 `x` 和 `y`——物件在畫面裡的中心——還有 `width` 和 `height`——框住它的方框大小。如果你看過那種軟體在臉周圍畫一個方框的照片,那個方框就是一個 `IMAGE_DETECTION`。它是物件「在畫面上」的位置。*

"Now lines 51 to 57 — `MAP_DETECTION`. Almost the same idea, but read the comment — this one is the object's position *on the actual playing field*, in meters. So here's the key difference, and it's a neat one. `IMAGE_DETECTION` is where the object appears on the screen, in pixels. `MAP_DETECTION` is where the object actually is on the real field, in meters. The Jetson does the math to convert from 'a blob of pixels in this corner of the image' to 'a real ball sitting at this spot on the field.' Two different ways of describing the same object — one for the picture, one for the real world."

*現在第 51 到 57 行——`MAP_DETECTION`。概念幾乎一樣,但讀註解——這個是物件「在真實比賽場地上」的位置,單位公尺。所以關鍵差別來了,而且很巧妙。`IMAGE_DETECTION` 是物件出現在「畫面上」哪裡,單位像素。`MAP_DETECTION` 是物件實際在「真實場地上」哪裡,單位公尺。Jetson 做數學換算,從「畫面這個角落的一團像素」算出「一顆真實的球坐落在場地這個點」。同一個物件的兩種描述方式——一個給畫面,一個給真實世界。*

"OK, now watch what happens at lines 59 to 66. This struct is called `DETECTION_OBJECT` — and remember, this is the one `findTarget` returned back in the other file. Let me read it:"

*好,現在看第 59 到 66 行發生什麼事。這個 struct 叫 `DETECTION_OBJECT`——記得嗎,這就是另一個檔裡 `findTarget` 回傳的那個。我念給你聽:*

```cpp
typedef struct {
    int32_t          classID;          // 物件的種類
    float            probability;      // 是這個種類的機率(1.0 = 100%)
    float            depth;            // 距離相機多遠(公尺)
    IMAGE_DETECTION  screenLocation;   // 在畫面上的位置
    MAP_DETECTION    mapLocation;      // 在場地上的位置
} DETECTION_OBJECT;
```

"Do you see something new and interesting here? Look at the last two fields. `screenLocation` is of type `IMAGE_DETECTION`, and `mapLocation` is of type `MAP_DETECTION`. Those are the two structs we *just* read! So a struct can contain other structs inside it. It's boxes within boxes. A `DETECTION_OBJECT` is one object the camera detected, and it bundles together: what kind of object it is — `classID` — how confident the AI is that it got the type right — `probability`, where 1.0 means 100% sure — how far away it is — `depth` — and then both of its locations, the screen one and the field one, each of which is its own little struct. So `DETECTION_OBJECT` is the complete description of one detected thing. Pretty elegant, right? Small structs combine into bigger structs."

*你看到這裡有新鮮又有趣的東西嗎?看最後兩個欄位。`screenLocation` 的型別是 `IMAGE_DETECTION`,`mapLocation` 的型別是 `MAP_DETECTION`。那是我們「剛剛」讀的兩個 struct!所以一個 struct 可以在裡面裝其他 struct。是盒中盒。一個 `DETECTION_OBJECT` 是相機偵測到的「一個」物件,它把這些綁在一起:它是什麼種類——`classID`、AI 對種類判斷的信心多高——`probability`(1.0 表示 100% 確定)、它多遠——`depth`、然後它的兩個位置(畫面的和場地的),每個各自又是一個小 struct。所以 `DETECTION_OBJECT` 是「一個被偵測物件」的完整描述。蠻優雅的對吧?小 struct 組合成大 struct。*

"And now the grand finale of the structs — lines 68 to 73 — `AI_RECORD`. This is the big one. This is the whole package that the Jetson sends over to the V5 brain. Let me read it:"

*現在 struct 的大結局——第 68 到 73 行——`AI_RECORD`。這是最重要的。這就是 Jetson 送到 V5 主控板的「整包」資料。我念給你聽:*

```cpp
typedef struct {
    int32_t          detectionCount;             // 看到幾個物件
    POS_RECORD       pos;                         // 機器人自己的位置
    DETECTION_OBJECT detections[MAX_DETECTIONS];  // 看到的所有物件(一個陣列)
} AI_RECORD;
```

"Look at how this is built out of everything we just read. `detectionCount` — a simple number, how many objects the camera saw this frame. `pos` — and look at its type, it's a `POS_RECORD`, the robot's own position that we read first. And then `detections` — this is an *array* of `DETECTION_OBJECT`, and remember `MAX_DETECTIONS` was that constant we saw earlier, fifty. So this is room for up to fifty detected objects. In Java you'd recognize the square brackets as an array, same idea. So an `AI_RECORD` answers the robot's two big questions in one neat package: 'where am I?' — that's `pos` — and 'what do I see?' — that's `detections`, the list of objects, with `detectionCount` telling you how many are actually filled in."

*看這個怎麼用我們剛讀的所有東西組起來。`detectionCount`——一個簡單的數字,這一幀相機看到幾個物件。`pos`——看它的型別,是 `POS_RECORD`,就是我們最先讀的機器人自己的位置。然後 `detections`——這是一個 `DETECTION_OBJECT` 的「陣列」,記得 `MAX_DETECTIONS` 是稍早看到的那個常數,五十。所以這裡有空間裝最多五十個被偵測的物件。在 Java 你會認出方括號是陣列,一樣的概念。所以一個 `AI_RECORD` 用一個整齊的包裹回答機器人的兩大問題:「我在哪?」——就是 `pos`——和「我看到什麼?」——就是 `detections`(物件清單),`detectionCount` 告訴你實際填了幾個。*

📌 **在螢幕上把這棵樹講出來(這是主菜的高潮,慢慢講):**

"Let me draw the whole shape for you in words, because this is the heart of today. Picture `AI_RECORD` as a big box. Inside it: first, a count. Second, a `POS_RECORD` box called `pos`, and inside *that* box are x, y, z and the angles — the robot's location. Third, an array — a row of up to fifty boxes — and each one of those is a `DETECTION_OBJECT`, and inside *each* of those is the classID, the probability, the depth, and two more little boxes: a screen location and a field location. So it's a box, containing boxes, containing boxes. And here's the payoff I promised: you now understand the *exact* shape of the data the AI camera sends the robot — and you got all of that from reading the header. You never opened a single `.cpp`. Hold onto `AI_RECORD` in your memory, because the very last thing we do today is watch the main program use it."

*我用講的把整個形狀畫給你,因為這是今天的核心。把 `AI_RECORD` 想成一個大盒子。裡面:第一,一個數量。第二,一個叫 `pos` 的 `POS_RECORD` 盒子,「那個」盒子裡面是 x、y、z 和角度——機器人的位置。第三,一個陣列——一排最多五十個盒子——每一個是一個 `DETECTION_OBJECT`,「每一個」裡面又有 classID、probability、depth,還有兩個小盒子:一個畫面位置、一個場地位置。所以是盒子裝盒子裝盒子。然後我答應你的回報來了:你現在懂了 AI 相機送給機器人的資料「確切的形狀」——而這全是讀 header 得來的。你一個 `.cpp` 都沒打開。把 `AI_RECORD` 記在腦中,因為今天最後一件事就是看主程式怎麼用它。*

📌 **(可選,時間夠才講)76–88 行有 MAP_POS_SIZE 和一個 packed 的 struct。一句話帶過。**

"By the way, just below, around lines 79 to 88, there's one more struct marked with this funny `__attribute__((__packed__))`. You can skip it, but in one sentence: 'packed' tells the compiler to squeeze the fields together with no empty gaps, because this particular struct is the actual packet of bytes that travels over the cable, and both computers have to agree on the exact byte layout. So it's the literal envelope the data gets mailed in. Skip it when reading."

*順帶一提,就在下面,第 79 到 88 行,還有一個 struct 標了這個有趣的 `__attribute__((__packed__))`。可以跳過,但一句話:「packed」叫編譯器把欄位緊緊擠在一起、不留空隙,因為這個特定的 struct 是真正在排線上傳輸的那包 byte,兩台電腦必須對確切的 byte 排列有共識。所以它是資料被寄出去時用的那個信封。讀的時候跳過。*

---

## ⑥ 做事的人:namespace 與 class | The worker ★

📌 **到此累計約 52 分。**

"All right. We've seen the wrapping paper, and we've seen the data shapes. Now for the third and last kind of thing in this file: the worker. Scroll down to line 94. This is the most important part of the whole file. Let me show you the skeleton first, then we'll fill it in:"

*好。我們看過包裝紙,看過資料形狀。現在第三種、也是最後一種東西:工人。捲到第 94 行。這是整個檔最重要的部分。我先給你看骨架,再填內容:*

```cpp
namespace ai {              // line 94
  class jetson {            // line 95
      public:               // line 96
        jetson();
        ~jetson();
        int32_t  get_packets(void);
        int32_t  get_errors(void);
        int32_t  get_timeouts(void);
        int32_t  get_total(void);
        int32_t  get_data(AI_RECORD *map);
        void     request_map();
      private:              // line 108
        // ... 一堆內部狀態,讀者略過 ...
    };                      // line 161
};                          // line 162
```

### namespace(94 行)

"First line, line 94: `namespace ai`. A namespace is just a way to group related code under a name, so things don't collide. Think of it like a Java package, or honestly like a folder for names. Everything inside these curly braces 'lives in' the `ai` namespace. And later, when some other code wants to use this class, it'll refer to it as `ai::jetson` — meaning 'the jetson that lives inside ai.' Those two colons, `::`, are C++'s way of saying 'inside of' or 'belonging to.' In Java you'd use a dot for a lot of this; C++ uses the double colon for namespaces. You'll see `::` all over C++, so just train your eye: double colon means 'reach inside this thing to get that thing.'"

*第一行,第 94 行:`namespace ai`。namespace 只是一種把相關程式碼歸在一個名字底下、避免撞名的方式。想成 Java 的 package,或老實說像一個「裝名字的資料夾」。這對大括號裡的所有東西都「住在」`ai` 這個 namespace。之後別的程式要用這個 class 時,會把它叫做 `ai::jetson`——意思是「住在 ai 裡面的 jetson」。那兩個冒號 `::` 是 C++ 表示「裡面的」或「屬於」的方式。在 Java 很多這種你會用點;C++ 對 namespace 用兩個冒號。你會在 C++ 到處看到 `::`,所以訓練一下你的眼睛:兩個冒號就是「伸進這個東西裡拿到那個東西」。*

### class + 結尾分號(95、161 行)

"Line 95: `class jetson`. Now this is a class, and you know classes from Java. But here's a small C++ habit to notice: scroll down to where the class ends, line 161, and you'll see the closing curly brace is followed by a *semicolon*. In C++, classes and structs end with a semicolon after the closing brace. Java doesn't make you do that. It's a tiny thing, but it's one of those differences that'll trip you up if nobody tells you, so now you know — class ends, semicolon."

*第 95 行:`class jetson`。這是一個 class,你從 Java 認識 class。但注意一個 C++ 的小習慣:捲到 class 結束的地方,第 161 行,你會看到結束的大括號後面接一個「分號」。在 C++,class 和 struct 在結束大括號後要分號。Java 不用你這樣做。這是小事,但屬於那種沒人告訴你就會絆到你的差別,所以現在你知道了——class 結束,分號。*

### public: / private: 是區段(96、108 行)

"Now look at line 96, `public:`, and line 108, `private:`. These work a little differently from Java, and it's worth getting right. In Java, you put the word `public` or `private` on every single member, one at a time. In C++, `public:` is more like a *section heading*. You write it once, with a colon, and then *everything* below it is public — until you hit another heading, like `private:`. So in this class, everything between line 96 and line 108 is the public section, and everything after line 108 is the private section. Think of it like a document with two headings: 'Public Stuff' and then 'Private Stuff.' Same meaning as Java — public means outside code can use it, private means only the class itself can — but it's organized in blocks instead of marked per line."

*現在看第 96 行 `public:` 和第 108 行 `private:`。這跟 Java 有點不一樣,值得弄對。在 Java,你在每一個成員上各別寫 `public` 或 `private`。在 C++,`public:` 比較像一個「區段標題」。你寫一次,加個冒號,然後它下面「所有東西」都是 public——直到遇到另一個標題,像 `private:`。所以在這個 class,第 96 到 108 行之間全是 public 區段,第 108 行之後全是 private 區段。想成一份有兩個標題的文件:「公開的東西」然後「私有的東西」。意思跟 Java 一樣——public 表示外面的程式可以用,private 表示只有 class 自己能用——但它是用「區塊」來組織,不是每行標。*

### 建構子與解構子(97、98 行)

"OK, let's read the public members. Lines 97 and 98 are special. Line 97 is `jetson();` — that's the *constructor*. You know constructors from Java: it has the same name as the class, it has no return type, and it runs automatically when you create one of these objects. Line 98 is `~jetson();` — with a little squiggle, a tilde, in front. That's called the *destructor*. Java doesn't really have these, because Java has a garbage collector that cleans up automatically. C++ doesn't clean up for you — so the destructor is the special method that runs when the object is being thrown away, where you do any cleanup. You will basically never write one of these yourself for this project. Your job is just to recognize it: tilde plus the class name equals destructor, the cleanup method."

*好,我們來讀 public 成員。第 97、98 行很特別。第 97 行是 `jetson();`——那是「建構子」。你從 Java 認識建構子:它跟 class 同名、沒有回傳型別、建立這種物件時自動執行。第 98 行是 `~jetson();`——前面有個小波浪號(tilde)。那叫「解構子」。Java 基本上沒有這個,因為 Java 有垃圾回收器會自動清理。C++ 不會幫你清——所以解構子是物件被丟棄時執行的特殊方法,你在那裡做清理。這個專案你基本上永遠不用自己寫。你的工作只是認得它:波浪號加上 class 名字等於解構子,清理用的方法。*

📌 **岔題吃時間(很值得講,學生會覺得酷):建構子的小秘密。**

"And here's a fun behind-the-scenes detail about this particular constructor. We won't open it now, but in the kitchen file, the `.cpp`, this `jetson()` constructor does something sneaky and cool: the moment you create a jetson object, it quietly launches a background task — a separate little thread of execution — whose entire job is to sit there constantly listening for data coming in from the Jetson camera, around the clock. So that's why, later, the main program can just ask 'give me the latest data' and it's instantly there — because behind the scenes, since the moment of creation, this object has been continuously catching every packet the camera throws at it. You don't see any of that in the header — the header just says 'there's a constructor.' But that's the kind of thing a constructor can kick off."

*關於這個特定建構子,有個有趣的幕後細節。我們現在不打開它,但在廚房檔(`.cpp`)裡,這個 `jetson()` 建構子做了一件偷偷的酷事:你一建立 jetson 物件,它就悄悄啟動一個背景任務——一條獨立的小執行緒——它唯一的工作就是坐在那裡不停地聽 Jetson 相機傳進來的資料,全天候。所以這就是為什麼後面主程式只要說「給我最新的資料」,它馬上就在那——因為幕後從建立的那一刻起,這個物件就一直在接住相機丟來的每一個封包。這些你在 header 裡都看不到——header 只說「有一個建構子」。但這就是建構子可以啟動的那種事。*

### 公開 API:這個 class 能做什麼(100–105 行)

"Now lines 100 to 105 — these are the real public methods, and together they're the most important thing to take away from this class. These are the functions that *other* code is allowed to call on a jetson object. This is the menu for this class. Let me read them one by one. Line 100, `get_packets` — returns the number of good data packets we've received. Line 101, `get_errors` — how many came in broken. Line 102, `get_timeouts` — how many times the camera went quiet for too long. Line 103, `get_total` — the total amount of data received. Those four are basically health-and-statistics functions — 'how's the connection doing?'"

*現在第 100 到 105 行——這些是真正的 public method,合起來是這個 class 最重要的收穫。這些是「其他」程式被允許對 jetson 物件呼叫的函式。這是這個 class 的菜單。我一個一個念。第 100 行 `get_packets`——回傳我們收到的「好」資料封包數量。第 101 行 `get_errors`——多少個進來時是壞的。第 102 行 `get_timeouts`——相機安靜太久幾次。第 103 行 `get_total`——收到的資料總量。這四個基本上是健康和統計的函式——「連線狀況如何?」*

"Then line 104 is the star of the show: `get_data`. Read it — `get_data(AI_RECORD *map)`. This is the one that actually hands you the camera's data. And line 105, `request_map` — this one goes the other direction, it asks the camera 'please send me a fresh batch of data.' So that's the whole public API of the jetson class: four status functions, one function to grab the latest data, and one to request new data. Six functions. That's everything your team can do with the camera link. If you were going to write robot code that uses the AI camera, this short list is your entire toolbox. And you found it just by reading the public section of a header."

*然後第 104 行是主角:`get_data`。讀它——`get_data(AI_RECORD *map)`。這個才是真正把相機資料交給你的。第 105 行 `request_map`——這個是反方向,它跟相機說「請傳給我一批新資料」。所以這就是 jetson class 的整份公開 API:四個狀態函式、一個抓最新資料、一個要求新資料。六個函式。這就是你的隊伍對相機連線能做的全部。如果你要寫用 AI 相機的機器人程式,這份短短的清單就是你的整個工具箱。而你只是讀了 header 的 public 區段就找到它了。*

### 指標 *(104 行)

"Now I have to point out one symbol on line 104, because it's the one new piece of C++ punctuation you'll keep seeing, and it doesn't exist in Java: the asterisk, the star. Look again — `get_data(AI_RECORD *map)`. See that little star right before the word `map`? That star means `map` is a *pointer*. Now, pointers are a big topic, and we are absolutely not going down that rabbit hole today. But here's the practical idea in plain English. A pointer is basically an address — it's like writing down where something lives instead of carrying the thing itself. And the reason this function uses one is a pattern: instead of the function building a fresh `AI_RECORD` and handing it back to you, *you* create an empty `AI_RECORD`, and you tell the function 'here's the address of my empty box — go fill it in for me.' It's like handing someone a blank form and saying 'fill this out and give it back.' Why do it that way? Because an `AI_RECORD` is big — it's got room for fifty objects — and this avoids making expensive copies. But honestly, for reading purposes, here's all you need: **when you see `Type *name`, just read it in your head as `Type name`.** The star is a detail about how the data gets passed around. If you ever start actually writing C++, we'll spend a whole session on pointers. For today, star equals 'don't worry about it.'"

*現在我得指出第 104 行的一個符號,因為它是你會一直看到、而且 Java 沒有的新 C++ 標點:星號(asterisk)。再看一次——`get_data(AI_RECORD *map)`。看到 `map` 這個字正前面的小星號嗎?那個星號表示 `map` 是一個「指標(pointer)」。指標是個大題目,今天我們絕對不會鑽進這個兔子洞。但用白話講實用的概念。指標基本上是一個「位址」——像寫下某個東西住在哪,而不是把東西本身搬來搬去。這個函式用它的原因是一種模式:不是函式自己做一個全新的 `AI_RECORD` 交回給你,而是「你」做一個空的 `AI_RECORD`,然後告訴函式「這是我空盒子的位址——去幫我把它填好」。像把一張空白表格遞給某人說「填好還我」。為什麼這樣做?因為 `AI_RECORD` 很大——它有裝五十個物件的空間——這樣避免做昂貴的複製。但老實說,讀的時候你只需要:「看到 `Type *name`,在腦中就把它讀成 `Type name`。」星號是資料怎麼傳遞的細節。如果你之後真的開始寫 C++,我們會花一整堂講指標。今天,星號等於「別擔心」。*

### private 區段(108 行之後)

"Last thing in this class — the private section, starting at line 108. I'm going to scroll through it, but I want you to do the opposite of focus. Look at all this stuff: there are some `enum class` things, there are counters like `packets` and `errors`, there's a `timer`, there are buffers, there's a lock. This is the class's private workspace — its scratch paper, its internal bookkeeping. And the whole point of marking it `private` is the same reason as in Java: this is none of the outside world's business. The class manages this stuff itself, and nobody else is allowed to touch it. So as a reader, your skill here is to *recognize that it's private and move on.* You don't read the private section to understand what a class can do — you read the public section for that. I'm showing it to you mainly so that when you see a big private block in some future file, you don't panic. You just go 'ah, internal stuff, not my problem,' and you scroll past it. Which is exactly what we're going to do right now."

*這個 class 的最後一件事——private 區段,從第 108 行開始。我會捲過去,但我要你做「專注的相反」。看這些東西:有一些 `enum class`、有像 `packets` 和 `errors` 的計數器、有一個 `timer`、有緩衝區、有一個鎖。這是 class 的私人工作區——它的草稿紙、內部記帳。把它標成 `private` 的全部重點跟 Java 一樣:這不關外面世界的事。class 自己管這些,別人不准碰。所以身為讀者,你在這裡的本事是「認出它是私有的,然後往下走」。你不會靠讀 private 區段來了解一個 class 能做什麼——那要讀 public 區段。我給你看主要是為了讓你以後在某個檔案看到一大塊 private 區塊時不會慌。你就「啊,內部的東西,不關我的事」,然後捲過去。而我們現在就要這樣做。*

"So step back and look at what we just did. This whole class, `ai::jetson`, is the worker whose job is to talk to the Jetson camera and fill in an `AI_RECORD` for you. It has a public menu of six things you can ask it to do, and a private workspace you ignore. And combined with the structs from before, you now understand this entire file. Three kinds of things — wrapping paper, data shapes, one worker. You just read a real, non-trivial C++ header end to end. That's genuinely a skill a lot of people never learn."

*所以退一步看我們剛做了什麼。整個 class `ai::jetson` 是一個工人,工作是跟 Jetson 相機溝通、幫你填好一個 `AI_RECORD`。它有一個 public 菜單,六件你可以叫它做的事,和一個你忽略的 private 工作區。再加上前面的 struct,你現在懂了整個檔案。三種東西——包裝紙、資料形狀、一個工人。你剛剛從頭到尾讀完一個真實、不簡單的 C++ header。這真的是很多人從來沒學會的本事。*

---

## ⑦ .h 怎麼接到 .cpp | How the menu connects to the kitchen

📌 **到此累計約 58 分。**

"Now let me close a loop I opened at the very beginning. I keep saying `.h` is the menu and `.cpp` is the kitchen. Let me actually show you the bridge between them, so it's not just a metaphor. In the side bar, open the `src` folder this time, and click `ai_jetson.cpp`. This is the kitchen file that goes with the header we just read."

*現在我來收一個從一開始就開的迴圈。我一直說 `.h` 是菜單、`.cpp` 是廚房。我實際給你看它們之間的橋,這樣它就不只是比喻。側邊欄這次打開 `src` 資料夾,點 `ai_jetson.cpp`。這是配我們剛讀的 header 的廚房檔。*

"Scroll down to around line 74, and find the function called `get_data`. Remember `get_data`? It's the star method, the one that hands you the camera data. In the header, the menu, it looked like this — one line, ending in a semicolon: `int32_t get_data( AI_RECORD *map );`. That's the menu listing. It just announces 'this dish exists.' Now look at what's here in the `.cpp`:"

*捲到第 74 行附近,找到叫 `get_data` 的函式。記得 `get_data` 嗎?它是主角方法,把相機資料交給你的那個。在 header(菜單)裡,它長這樣——一行,以分號結尾:`int32_t get_data( AI_RECORD *map );`。那是菜單上的項目。它只是宣告「這道菜存在」。現在看 `.cpp` 裡有什麼:*

```cpp
int32_t jetson::get_data( AI_RECORD *map ) {
    ...
    memcpy( map, &last_map, sizeof(AI_RECORD));   // 把內部最新資料整個複製到你給的 map
    ...
}
```

"Look at how similar and how different these two are. Same return type — `int32_t`. Same name — `get_data`. Same parameter — `AI_RECORD *map`. So it's clearly the same function. But there are two differences. First, the header version ended in a semicolon and just stopped — the kitchen version has actual code inside curly braces. That code is the real recipe. Second, and this is the key bit, look at the name in the `.cpp`: it's not just `get_data`, it's `jetson::get_data`. There are those double colons again. That `jetson::` in front is how C++ says 'this is the get_data that *belongs to* the jetson class.' Because lots of different classes might have a `get_data` — the colon-colon tells you exactly whose recipe this is. So the bridge between the menu and the kitchen is: same signature, but the kitchen prefixes the function name with the class name and double colons, and then provides the real code. Menu announces it, kitchen cooks it."

*看這兩個多像、又多不一樣。同樣的回傳型別——`int32_t`。同樣的名字——`get_data`。同樣的參數——`AI_RECORD *map`。所以顯然是同一個函式。但有兩個差別。第一,header 版本以分號結尾就停了——廚房版本在大括號裡有真正的程式碼。那段程式碼是真正的食譜。第二,這是關鍵,看 `.cpp` 裡的名字:它不只是 `get_data`,是 `jetson::get_data`。又是那兩個冒號。前面那個 `jetson::` 是 C++ 在說「這是『屬於』jetson class 的 get_data」。因為很多不同的 class 可能都有 `get_data`——冒號冒號告訴你這到底是誰的食譜。所以菜單和廚房之間的橋是:同樣的簽名,但廚房在函式名前面加上 class 名字和兩個冒號,然後提供真正的程式碼。菜單宣告它,廚房煮它。*

📌 **再走一個更短的函式,加深印象、吃時間。**

"Let me show you one more, even quicker, so the pattern really sticks. Scroll up a little to around line 41, to `get_packets`. In the header it was `int32_t get_packets(void);` — just an announcement. Here in the kitchen it's `int32_t jetson::get_packets() {` and then inside, the entire recipe is one line: `return packets;`. That's it. It just hands back the counter. See the pattern again? `jetson::` plus the name, then the real code in braces. Once you've seen this two or three times, you'll recognize it instantly in any C++ project: if a function name has `SomethingName::` in front of it, you're looking at the kitchen — the real implementation — and the `SomethingName` tells you which class it belongs to."

*我再給你看一個,更快,讓這個模式真的記住。往上捲一點到第 41 行附近,`get_packets`。在 header 裡它是 `int32_t get_packets(void);`——只是個宣告。在這裡的廚房,它是 `int32_t jetson::get_packets() {`,然後裡面,整個食譜就一行:`return packets;`。就這樣。它只是把計數器交回去。又看到模式了嗎?`jetson::` 加名字,然後大括號裡的真正程式碼。看過兩三次之後,你在任何 C++ 專案都會立刻認出它:如果一個函式名前面有 `某名字::`,你看的就是廚房——真正的實作——而那個「某名字」告訴你它屬於哪個 class。*

---

## ⑧ 全部兜起來:main.cpp | Putting it all together ★

📌 **到此累計約 66 分。這是高潮。即使超過 60 分一點點也要把 local_map.pos.x 講到。**

"OK. Last file, and this is the payoff for everything we've done today and last time. Open `main.cpp` in the `src` folder. This is the heart of the program — it's where the robot's main logic lives, and it's where everything starts."

*好。最後一個檔,這是今天和上次所有努力的回報。打開 `src` 裡的 `main.cpp`。這是程式的心臟——機器人主邏輯在這、一切開始的地方。*

"Let me give you a tour from the top. Look at line 12: `#include \"ai_functions.h\"`. We talked about `#include` — it pulls another file in. So this line is saying 'I want to use all those robot functions we read last time.' And because `ai_functions.h` itself pulls in more files behind the scenes, this one line gives `main.cpp` access to basically everything — the robot functions, the structs, the jetson class, all of it."

*我從上面帶你逛。看第 12 行:`#include "ai_functions.h"`。我們講過 `#include`——它把另一個檔拉進來。所以這行在說「我要用上次讀的所有那些機器人函式」。而因為 `ai_functions.h` 自己幕後又拉進更多檔,這一行就讓 `main.cpp` 取得幾乎所有東西——機器人函式、struct、jetson class,全部。*

"Now look at lines 16 through 26. This is the robot's hardware being declared. Read down the list with me — there's a `brain`, that's the V5 brain itself; a `controller`, the handheld remote; then a bunch of `motor` lines — `leftDrive`, `rightDrive`, an `Intake` motor for grabbing balls, a `Belt` motor for moving them up. There's a `gps` sensor, and a `Drivetrain`. So this chunk is basically the robot saying 'here are all my body parts and which port each one is plugged into.' You don't need to memorize any of it — just recognize that this is the hardware setup."

*現在看第 16 到 26 行。這是機器人的硬體在被宣告。跟我讀下去——有一個 `brain`,就是 V5 主控板本身;一個 `controller`,手持遙控器;然後一堆 `motor` 行——`leftDrive`、`rightDrive`、一個抓球的 `Intake` 馬達、一個把球往上送的 `Belt` 馬達。有一個 `gps` 感測器、一個 `Drivetrain`。所以這塊基本上是機器人在說「這是我所有的身體部位,各自插在哪個埠」。你不用背任何一個——只要認出這是硬體設定。*

"Now this one matters — look at line 35: `ai::jetson jetson_comms;`. Do you recognize that type? `ai::jetson` — that's the class we just spent fifteen minutes reading! This line creates one actual jetson object and names it `jetson_comms`. So right here is the moment that worker gets hired. And remember the constructor secret I told you — the instant this line runs, that background listener thread starts up and begins catching camera data. From now on, `jetson_comms` is our live connection to the camera."

*這個很重要——看第 35 行:`ai::jetson jetson_comms;`。認得那個型別嗎?`ai::jetson`——就是我們剛花十五分鐘讀的那個 class!這行建立一個真正的 jetson 物件,命名為 `jetson_comms`。所以就在這裡,那個工人被雇用了。記得我告訴你的建構子秘密——這行一執行,那條背景監聽執行緒就啟動,開始接相機資料。從現在起,`jetson_comms` 是我們跟相機的活連線。*

"Now scroll down to line 65, the function called `auto_Isolation`. This is one of the robot's autonomous routines — the stuff it does on its own during a match. And this is where it gets satisfying. Let me read a few lines from inside it:"

*現在捲到第 65 行,叫 `auto_Isolation` 的函式。這是機器人的自動程序之一——比賽中它自己做的事。爽的地方來了。我念裡面幾行給你聽:*

```cpp
goToObject(OBJECT::BallBlue);
runIntake(directionType::fwd, 3, true);
goToGoal();
```

"Do these look familiar? They should — these are functions from `ai_functions.h`, the file we read last session! Read them like English: go to an object, specifically a blue ball; run the intake forward for three rotations; then go to the goal. That's a complete little robot strategy, and you can read it like a sentence. And look at `OBJECT::BallBlue` — remember last time we read `enum OBJECT { BallBlue, BallRed };`? `BallBlue` came from exactly that enum, and the double colon means 'the BallBlue that belongs to OBJECT.' So you are literally reading the robot's game plan, and you understand every piece of it, because you read the headers. There are a few more lines below — driving backwards, setting belt speed, running the intake again — but it's all the same idea: a readable list of commands."

*這些看起來眼熟嗎?應該要——這些是 `ai_functions.h` 的函式,上次讀的那個檔!像英文一樣讀:去一個物件,具體是藍球;intake 正轉三圈;然後去球門。這是一個完整的小小機器人策略,你可以像句子一樣讀。看 `OBJECT::BallBlue`——記得上次讀的 `enum OBJECT { BallBlue, BallRed };` 嗎?`BallBlue` 正是從那個 enum 來的,兩個冒號表示「屬於 OBJECT 的 BallBlue」。所以你根本就是在讀機器人的比賽計畫,而且你懂每一塊,因為你讀了 header。下面還有幾行——倒退、設定 belt 速度、再次轉 intake——但都是同樣的概念:一份可讀的指令清單。*

"And now, the grand finale. Scroll down to the main loop, starting around line 152. And let me set it up by looking at line 129 first, just above. Line 129 says: `static AI_RECORD local_map;`. Stop and appreciate that. `AI_RECORD` — that's the big data package we read, the one with the robot's position and the list of detected objects. So `local_map` is an empty `AI_RECORD`, a blank form, sitting here ready to be filled in. Now the loop:"

*現在,大結局。捲到主迴圈,從第 152 行附近開始。我先看上面一點的第 129 行來鋪陳。第 129 行說:`static AI_RECORD local_map;`。停下來體會一下。`AI_RECORD`——就是我們讀過的大資料包,有機器人位置和偵測物件清單的那個。所以 `local_map` 是一個空的 `AI_RECORD`,一張空白表格,放在這裡準備被填。現在看迴圈:*

```cpp
while(1) {
    jetson_comms.get_data( &local_map );                          // 154
    link.set_remote_location( local_map.pos.x, local_map.pos.y,
                              local_map.pos.az, local_map.pos.status );  // 157
    jetson_comms.request_map();                                   // 163
    this_thread::sleep_for(loop_time);                            // 166
}
```

"`while(1)` just means 'loop forever' — keep doing this over and over as long as the robot is on. Line 154: `jetson_comms.get_data( &local_map );`. Read it out loud in plain English: 'jetson_comms, please get the data and put it into local_map.' We're calling that star method, `get_data`, on our jetson worker, and handing it the address of our blank form — that's what the `&` does, it means 'the address of local_map' — so the worker can fill it in. After this line runs, `local_map` is full of fresh camera data."

*`while(1)` 就是「永遠迴圈」——只要機器人開著,就一遍又一遍做這個。第 154 行:`jetson_comms.get_data( &local_map );`。用白話大聲讀:「jetson_comms,請拿資料放進 local_map。」我們對我們的 jetson 工人呼叫那個主角方法 `get_data`,把我們空白表格的位址交給它——那就是 `&` 在做的,它表示「local_map 的位址」——這樣工人就能填它。這行執行完,`local_map` 就裝滿了新鮮的相機資料。*

📌 **這是全堂高潮,把 local_map.pos.x 一層一層拆,慢慢講:**

"Now look at line 157, and this is the moment I've been promising you all class. Look at this piece: `local_map.pos.x`. Let's take it apart one dot at a time, using only things we read today. `local_map` — what type is that? It's an `AI_RECORD`. Good. Now, what's inside an `AI_RECORD`? Remember the boxes-in-boxes. One of the things inside it was `pos` — so `local_map.pos` reaches into the record and grabs the `pos`. And what type was `pos`? It was a `POS_RECORD`. And what's inside a `POS_RECORD`? The position fields — including `x`. So `local_map.pos.x` means: go into the record, get the position, get the x-coordinate. In plain English, `local_map.pos.x` is *the robot's x-position on the field.* And here's the whole point of today: you just understood that line completely, and you never once opened the kitchen. You knew it purely from reading the structs in the header. That's the magic. Read the menu, understand the meal."

*現在看第 157 行,這就是我整堂課答應你的時刻。看這一塊:`local_map.pos.x`。我們一次一個點地拆開,只用今天讀過的東西。`local_map`——它是什麼型別?是一個 `AI_RECORD`。很好。那 `AI_RECORD` 裡面有什麼?記得盒中盒。裡面的東西之一是 `pos`——所以 `local_map.pos` 伸進記錄裡抓出 `pos`。`pos` 是什麼型別?是一個 `POS_RECORD`。`POS_RECORD` 裡面有什麼?位置欄位——包括 `x`。所以 `local_map.pos.x` 意思是:進到記錄、拿到位置、拿到 x 座標。用白話講,`local_map.pos.x` 就是「機器人在場上的 x 位置」。今天的整個重點來了:你剛剛完全看懂了那一行,而你一次都沒打開廚房。你純粹靠讀 header 裡的 struct 就知道了。這就是魔法。讀菜單,懂這道菜。*

"Let me finish the loop. The rest of line 157 takes the robot's position — x, y, the heading angle, and the status — and hands it to `link`, which sends it over to the partner robot, so the two robots on a team know where each other are. Then line 163, `jetson_comms.request_map()` — that asks the camera for the next fresh batch of data, so next time around the loop there's something new to get. And the last line tells the program to sleep for a tiny moment so other parts of the robot get a turn, and then the whole loop runs again. Over and over, many times a second: get the latest data, share my position with my teammate, ask for more, rest a beat, repeat."

*我把迴圈講完。第 157 行剩下的部分,把機器人的位置——x、y、heading 角度、和 status——交給 `link`,它把這個送到夥伴機器人,這樣隊上兩台機器人就知道彼此在哪。然後第 163 行 `jetson_comms.request_map()`——跟相機要下一批新鮮資料,這樣下一圈迴圈才有新東西可拿。最後一行叫程式睡一小下,讓機器人其他部分輪到,然後整個迴圈再跑一次。一遍又一遍,一秒很多次:拿最新資料、把我的位置分享給隊友、要更多、休息一拍、重複。*

"And there's our whole story from the beginning of class, alive in the code. Remember the flow? The camera sees the field, the Jetson packs an `AI_RECORD`, ships it over, the jetson class catches it, and the main loop reads `local_map` and acts on it. You just watched that entire flow happen, in real code, and you could read every important line. That's a huge amount of progress for two sessions."

*這就是開場那個故事,活在程式碼裡。記得那個流程嗎?相機看場地、Jetson 打包一個 `AI_RECORD`、送過來、jetson class 接住它、主迴圈讀 `local_map` 並依此行動。你剛剛看著整個流程在真實程式碼裡發生,而且你能讀懂每一行重要的。對兩堂課來說,這是巨大的進步。*

---

## ⑨ 總結 + 作業 | Wrap up & homework

📌 **到此累計約 70 分。可依實際時間壓縮。**

"Let's wrap up. Take a second and look at how much you learned today. You learned that any header file, no matter how scary it looks, really just has three kinds of things: wrapping paper you skip, structs that describe data, and classes that do work. You learned what a struct is — a pure-data shape, like a form — and that structs can nest inside other structs, boxes within boxes, building up to that big `AI_RECORD`. You learned what a class looks like in C++ — the public menu of what it can do, the private workspace you ignore, the constructor and the destructor. You learned how a header connects to its `.cpp` using the class name and double colons. And best of all, you read the real main program and understood what the robot does — `local_map.pos.x` and all — using nothing but the headers. That's the whole skill, and you've got it."

*我們做總結。花一秒看看你今天學了多少。你學到任何 header 檔,不管看起來多可怕,其實只有三種東西:你跳過的包裝紙、描述資料的 struct、做事的 class。你學到 struct 是什麼——純資料的形狀,像表格——而且 struct 可以巢狀在其他 struct 裡,盒中盒,堆成那個大 `AI_RECORD`。你學到 C++ 的 class 長什麼樣——它能做什麼的 public 菜單、你忽略的 private 工作區、建構子和解構子。你學到 header 怎麼用 class 名字和兩個冒號接到它的 `.cpp`。最棒的是,你讀了真正的主程式、看懂了機器人在做什麼——`local_map.pos.x` 等等——只用 header,什麼別的都沒用。這就是整個本事,你已經有了。*

"For homework, it's the same kind of reading you just did, on your own this time. Open the file `ai_robot_link.h` in the include folder. It's the header for the robot-to-robot communication — the code behind that `link` we just saw sharing positions between teammates. Don't write anything, don't worry about the `.cpp`. Just read the header and answer four things for me. One: what namespace is everything in? Two: what class does it define, and what are its public methods — just list the names. Three: there are some structs inside — what do they describe? The comments will help; they're about the packets the robots mail to each other. And four, a bonus, just to get your eyes on something new for next time: look at line 21, where it says `: public vex::serial_link`, and look at lines 39 and 40, where you'll see an ampersand, an `&`, in `float &x`. Don't try to figure those out — just notice them, take a guess if you want, and we'll talk about both next session."

*作業,跟你剛做的同一種閱讀,這次自己做。打開 include 資料夾裡的 `ai_robot_link.h`。它是機器人對機器人通訊的 header——就是我們剛看到那個在隊友間分享位置的 `link` 背後的程式碼。不要寫任何東西,不要管 `.cpp`。只要讀 header,回答我四件事。一:所有東西在哪個 namespace 裡?二:它定義了什麼 class,public method 有哪些——把名字列出來就好。三:裡面有一些 struct——它們描述什麼?註解會幫你,是關於機器人互寄的封包。四,加分,只是讓你的眼睛先看到下次的新東西:看第 21 行 `: public vex::serial_link`,還有第 39、40 行,你會看到一個 & 符號,在 `float &x` 裡。不要試著搞懂它們——只要注意到,想猜就猜,下次我們兩個都會講。*

📌 **第 4 題是替下一堂鋪路:`: public` 是繼承(inheritance,Java 的 extends),`&` 是 reference。學生猜不到沒關係,目的是讓他先注意到。**

"You can write your answers on paper or in a text file, whatever's easy. Bring them next time. Honestly, great work today — you read a real C++ class, you understood the data structures, and you saw how the whole program fits together. That's a lot. See you next time!"

*答案寫紙上或 text 檔都行,方便就好。下次帶來。老實說,今天做得很棒——你讀了一個真的 C++ class、懂了資料結構、看到整個程式怎麼兜起來。這很多了。下次見!*

---

## 🧰 加長模組:還剩很多時間就加講 | Expansion modules

📌 **如果你講太快、進度遠超前,從這裡挑來加。每個都是純講述,可以直接念。**

### 模組 A:現場帶讀作業檔 ai_robot_link.h（約 8 分,最推薦)

"Hey, we've got a little extra time, so let me give you a head start on the homework — let's read the first part of `ai_robot_link.h` together. Open it from the include folder. ... See the very top? Same wrapping paper as before — an include guard. Skip it. Now line 20, `namespace ai` — same namespace as the jetson class, makes sense, it's related code. Line 21: `class robot_link`. So this is another worker class. And its public section, lines 22 onward, has a constructor, a destructor, and then a menu of methods — `get_packets`, `get_errors`, and some `set_remote_location` and `get_remote_location` functions. Read those names: this class's job is to send and receive location info between two robots. See how fast that went? You've already got the muscle for this. The rest of the homework, finding the structs, you can totally do on your own now."

*欸,我們有點多的時間,我先讓你的作業起個頭——一起讀 `ai_robot_link.h` 的第一部分。從 include 資料夾打開。……看最上面?跟之前一樣的包裝紙——一個 include guard。跳過。現在第 20 行,`namespace ai`——跟 jetson class 同一個 namespace,合理,是相關的程式碼。第 21 行:`class robot_link`。所以這是另一個工人 class。它的 public 區段,第 22 行往後,有一個建構子、一個解構子,然後一份方法菜單——`get_packets`、`get_errors`,還有一些 `set_remote_location` 和 `get_remote_location` 函式。讀那些名字:這個 class 的工作是在兩台機器人之間傳送和接收位置資訊。看多快就過了?你已經有這個肌肉了。作業剩下的部分,找出 struct,你現在完全可以自己做。*

### 模組 B:建構子裡的背景執行緒(約 5 分)

"Want to see something cool that happens behind the scenes? Open `ai_jetson.cpp` and look near the top, around line 28, at the constructor `jetson::jetson()`. See this line — it creates a `thread`. A thread is like a second worker running at the same time as everything else. So when you create the jetson object, it spins up this background thread whose only job is to sit in a loop forever, catching every byte the camera sends and reassembling it into packets. That's why the main loop can just say 'get_data' and the data's already waiting — this little thread has been working the whole time, in the background, like an assistant quietly taking messages while you're busy. You'd never know it from the header — the header just says `jetson();`. But this is the kind of work a constructor can kick off."

*想看一個幕後發生的酷東西嗎?打開 `ai_jetson.cpp`,看最上面附近,第 28 行左右,建構子 `jetson::jetson()`。看這行——它建立一個 `thread`(執行緒)。執行緒像第二個工人,跟其他所有東西同時跑。所以你建立 jetson 物件時,它啟動這條背景執行緒,它唯一的工作就是永遠坐在一個迴圈裡,接住相機傳的每一個 byte、重組成封包。這就是為什麼主迴圈只要說「get_data」資料就已經在等了——這條小執行緒一直在背景工作,像一個助理在你忙的時候安靜地幫你收訊息。你從 header 永遠看不出來——header 只說 `jetson();`。但這就是建構子能啟動的那種工作。*

### 模組 C:十六進位小知識(約 3 分,學生喜歡數字才講)

"Quick fun aside about those `0x` numbers. Computers think in binary — ones and zeros — but writing long strings of ones and zeros is painful for humans. Hexadecimal is a shortcut: it's base sixteen, and one hex digit packs exactly four binary digits. So instead of writing eight ones and zeros, you write two hex characters. That's why you see `0x01` or `0xAA` all over hardware code — it lines up perfectly with how bits are grouped. `0xAA`, by the way, if you ever wonder, is the number 170, and in binary it's a tidy alternating one-zero-one-zero pattern, which is why it's often used as a 'sync' marker — it's easy to spot. You don't need any of this to read the code; it's just a peek at why hex shows up so much down at the hardware level."

*關於那些 `0x` 數字的快速趣味補充。電腦用二進位思考——一和零——但寫一長串一和零對人類很痛苦。十六進位是個捷徑:它是 16 進位,一個十六進位數字剛好裝四個二進位數字。所以不用寫八個一和零,你寫兩個十六進位字元。這就是為什麼你在硬體程式碼到處看到 `0x01` 或 `0xAA`——它跟 bit 分組的方式對得很整齊。順帶一提,`0xAA` 如果你好奇,是數字 170,二進位是整齊的一零一零交替樣式,所以它常被用作「同步」標記——很好認。讀程式碼你不需要這些;只是偷看一下為什麼十六進位在硬體層出現這麼多。*

---

## 🆘 Troubleshooting Cheat Sheet | 緊急狀況小抄

📌 **純中文,給老師看。**

### 學生看到紅色波浪線(VS Code 找不到 #include 的檔)
- 大部分不影響閱讀,叫他先忽略
- 確認打開的是 `ai_demo` 資料夾本身,不是 repo 根目錄

### 學生在 ai_jetson.h 裡迷路 / 覺得太多
- 拉回三分法:「這檔只有三種東西:包裝紙、struct、一個 class」
- 強調我們只挑重點,不是每行都讀

### 學生問「struct 和 class 到底差在哪」
- 簡單版:「在 C++ 幾乎一樣。慣例上 struct 放純資料,class 放有行為的東西。」
- 進階版(想聽才講):「唯一真正的差別是預設權限——struct 預設 public,class 預設 private。」

### 學生問「`*`(星號)到底是什麼」
- 「讀的時候,看到 `Type *name` 就當成 `Type name`。」
- 想懂:「`int x` 是一個 int;`int *x` 是『指向某個 int 的記憶體位址』。這裡是『你給我容器,我幫你填』。」
- 不要深入指標,會吃掉太多時間

### 學生問「`&` 是什麼」(main.cpp 的 `&local_map`)
- 「`&變數` 是『取出這個變數的位址』,配合 `*` 指標一起用——函式才知道要把資料填到哪。」
- 作業檔裡的 `float &x` 是另一個意思(reference),下次課再講

### 還是怕太快、想再慢一點
- 每講完一個 struct,就用「所以這個 struct 回答的問題是……」再總結一次
- 多用「Let me say that another way」換句話再講一次同一個概念
- 把 `local_map.pos.x` 的逐層拆解,從頭再走一次給學生聽

---

## 📝 Tutor 自己的 Quick Reference | 老師快速參考

### 本堂 Java ↔ C++ 對照

| Java | C++ | 備註 |
|------|-----|------|
| 只有 public 欄位的 class / record | `struct { ... };` | 純資料,結尾分號 |
| class 裡每個成員寫 public | `public:` / `private:` 是**區段標頭** | 寫一次,管到下一個 |
| 無解構子(有 GC) | `~ClassName()` | 解構子,認得就好 |
| 物件 = reference | `Type *name`(指標) | 讀的時候當 `Type name` |
| `obj.method()` | `obj.method()` 或 `ptr->method()` | |
| `Outer.Inner` | `namespace::Class` | `::` = 裡面的 |
| `import` | `#include`(貼文字) | |
| `static final X = 50` | `#define X 50` | preprocessor,較舊 |

### ai_jetson.h 地圖(真實行號)

```
14–15, 165 ── include guard（包裝紙,略過）
22–24, 90–92 ── extern "C"（C/C++ 相容,略過）
26, 29 ────── #define 常數（MAX_DETECTIONS=50；0x01 hex）
31–42 ─────── struct POS_RECORD        機器人位置/朝向
44–49 ─────── struct IMAGE_DETECTION   畫面像素框
51–57 ─────── struct MAP_DETECTION     場地座標
59–66 ─────── struct DETECTION_OBJECT  一個物件(含上面兩個)
68–73 ─────── struct AI_RECORD ★       總包(pos + detections[50])
79–88 ─────── struct map_packet（packed,傳輸封包,略過）
94 ────────── namespace ai
95–161 ────── class jetson  ★
  96  public:   建構子/解構子 + 6 個 API（含 get_data(AI_RECORD*)）
  108 private:  內部狀態(略過)
```

### 本堂「一句話高潮」(務必講到)
> `main.cpp` 第 157 行的 `local_map.pos.x`:`local_map` 是 `AI_RECORD` → `.pos` 是 `POS_RECORD` → `.x` 是場上 X 座標。**只讀 header 就懂,沒碰 .cpp。**

### 資料流一句話(開場 + 高潮都用)
> 相機看場地 → Jetson 打包成 `AI_RECORD` → 透過排線送到 V5 → `jetson` class 接住 → `main.cpp` 的主迴圈讀 `local_map` 並行動。

---

*End of Session 2 script (Lecture Edition) | 第二堂稿子(純講述版)結束*
