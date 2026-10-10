---

title: "Gemote"
author: "Mohammad Sarfaraz"
description: "Its a hand gesture remote which can control mouse pointers, clicks and srcoll edit"
created_at: "20-09-2026"

---

# September 20: Initial Journal/The Idea

Few months ago, My good friend [Ilham_Farooque](https://www.instagram.com/ilham_farooque/) got an idea to build a gyroscope based controller built in a handheld casing which would control the mouse pointer and clicks. 

So, he consulted me about his idea and we decided to work on it together after we were supposed to be done with our ongoing project. I remember I was making CYPRUS the split keyboard and he was working on some website for a CAFÉ.

Days passed then months and we litteraly never talked about it again except for posting few instagram stories. 

Coming back to the last night, I was thinking about some project ideas and I thought to myself I should try make something different this time, something where I can interact with physical world, something where I could put my knowledge of kinemetics and mechanics that I have learnt in highschool.

Then, BOOOOM — What better could be than making a hand gesture controlled car(Coming soon and its gonna be fire🔥🔥)!!
I decided to put the remote in gloves to get that expensive RC car vibe.

![alt text](JOURNAL_ASSETS/journal1_image1.png)

I have always wanted to get one of these!!!!!!!!! Never thought I would get to build it!!


Anyway, this project is a basic version of the remote I am going to be using in my RC car. Essentially its the combination of my design and his idea. The glove would monitor the hand gesture of the user and control the pointers and clicks on the monitor. 

**Total time spent: 0.4 hours**

# September 21: BOM and Workflow

I thought and thought then I used AI(i.e. Claude) to think and I thought more and so far I have come up with these features for my 'Gemote'.


* MPU-6050 — for monitoring rotational vector which would also be useful if I wanted to use this feature in my RC car remote.

![alt text](JOURNAL_ASSETS/journal2_image1.png)


* Flex Sensor — This is something I didnt know existed before I used Claude for parts requirement and I am glad I did. Basically its a device which changes its resistance depening on how much it is bent/flexed. So, I can use it on my fingers and palm to control stuffs like left click / right click. Or even I can use it to change modes without using any sort of push button.

![alt text](JOURNAL_ASSETS/journal2_image2.png)

* FSR fingertip pad — It is something that you wear at your finger tips and it detects the pressure applied on or by finger tips. Its mostly used in medical prosthetics which makes it even cooler!! SO, my plan is to use it so that I can register some input by pressing a finger by another. 

![alt text](JOURNAL_ASSETS/journal2_image3.png)

* Coin vibration motor — You can already guess by the name - its a small dc motor which I would use for feedback mechanism.

![alt text](JOURNAL_ASSETS/journal2_image4.png)

* Micro Controller — This is one the most crucial part of the design and I need to do it right. For now, I am choosing a board with good bluetooth capability since its a mouse. I am choosing Seeed XIAO nRF52840 instead of some Esp32 board because  
  One: It far excels in bluetooth capabilities than any Esp32 varient.  
  and Two: Its Seed Xiao so size wouldnt be an issue.   
The only issue is lower number of pins and I am likely going to need to use two of these boards, but we will see when we actually get to the build part. Maybe the cad would help me decide. 

![alt text](JOURNAL_ASSETS/journal2_image5.png)

* Power — Honestly I have yet not decided what to use to power the device. I guess I will decide it after I am done with the setup and coding. While its also high likely I will be using some sort of Rechargable Li-po battery.

* Others — Ofc gloves, fabrics, anything glvoes related and what not.

Also I wanted to say that I might change some components based on requirement.

---

Okay, now lets talk about how I am actually going to pull these off — **I DONT KN0W!!!!**     
First, I am gonna spend a week getting basics of C++ so that I can actually understand the moudues/libs that I am going to be using in firmware.   
Then I will start working on circuit part, I will make the schematics and if necessary a PCB. Then I will start coding the device which is actually the hardest yet the best part of the project.  
And then I will do some cad work for the body where all electronics will fit in and lastly I will put everything together on glove.  

Also, The workflow could change depending on what I feel like, so I guess you could say there is no workflow 😭😭. 

---

**Total time spent: 3.2 hours**

# October 7: Got the board's symbol..

I know, I know, its been more than 15 days since I wrote my last journal and its a bit relieving that I am finally getting back to it. Its really frustrating when you are in the middle of a project and life shit happens. Specially for me, I have my finals coming up, the college applications, the continuous thought of the future and of the life.  
And it scares me. It scares me to the extent that I had my first ever anxiety attack last week. 

Thanks to my friend I was able to get my shit together. 

Okay! that aside, I managed to put some work into the schematics. And as mentioned in my previous devlog I am going to be using [SEEED XIAO nRF52840 Sense PLUS](https://wiki.seeedstudio.com/XIAO_BLE/) as the micro controller. I chose this specific variant because I get just enough number of pins to work with and ofc more reasons I have stated in my previous devlog. 

Now, coming back to schematic part — 

I had hard time finding the kicad_symbol for the mcu. I mean I looked it up on [https://wiki.seeedstudio.com/XIAO_BLE/](https://wiki.seeedstudio.com/XIAO_BLE/), and it did have a link for design footprints and symbols. 

![alt text](JOURNAL_ASSETS/journal3_image3.png)

I added it in my kicad symbol library but for some reason it wouldn't appear in the symbol list.

So, I tried a different approach. I first downloaded the kicad project file from the website.

![alt text](JOURNAL_ASSETS/journal3_image4.png)

Then, opened the project in my kicad and exported the symbol of mcu using edit in symbol editor property.

![alt text](JOURNAL_ASSETS/journal3_image6.png)

\*sigh!!* 😭😭

After frying my brain for more than an hour I finally got it in the symbol list, then did some labelling. 

![alt text](JOURNAL_ASSETS/journal3_image5.png)

**Total time spent: 3.8 hours**

----

# October 10: Schematics complete!

Before I moved on to the other parts of the schematic, I wanted to have a basic idea about the board's battery compatibility. Although I knew that most SEEED XIAO Series have somewhat similar battery charging and protection circuitry, it was then that I realised there might be something wrong with my schematic symbol. 

So, basically, the board uses pin P0.14 and P0.31 for battery voltage monitoring with the ADC on P0.31.

![alt text](JOURNAL_ASSETS/journal4_image3.png)

I was a little confused by the fact that I had a breakout pin P0.31 on my board symbol but, in the documentation it says you can read the battery voltage from P0.31. 

And **BOY!!** My intuition was right.   
When I looked more closely at the schematics I realised that the wiring looked a little bit similar to how we read analog values from sensors(e.g., Photoresistor). 

![alt text](JOURNAL_ASSETS/journal4_image4.png)

*So why make the breakout pin if you already got the pin in use??* — **"I DONT KNOW"**


So, do I need to change my symbol??   
Well, I first thought of designing the symbol myself, and I even got started with the symbol design. But I thought I should compare my symbol with the breakout board on the official website one last time. 

![alt text](JOURNAL_ASSETS/journal4_image5.png)

![alt text](JOURNAL_ASSETS/journal4_image6.png)

And honestly, there weren't any major differences, just some extra pins and that was a relief. Then, I used a variable resistor symbol for flex sensors because essentially it is a resistor which changes its resistance based on how much its bent. Then, I wired and also used a 10k resistor as voltage divider which I might change the value of if necessary.

![alt text](JOURNAL_ASSETS/journal4_image1.png)

Next, I started working on the feedback part and I decided to go with mofset setup to control the ON/OFF and the frequency of the vibration of motor(PWM) by connecting the base of mofset with a PWM pin. I also learnt that you need to have a diode connected in parallel between the two pins of motor because when you turn off the current the coil of motor generates an induced voltage due to sudden change in current. 

![alt text](JOURNAL_ASSETS/journal4_image2.png)

The direction of the induced current depends on the current before the sudden change(i.e. decrease) as it tries to resists the change in magnetic flux. So, the diode in parallel makes a one way circuit for the induced current to flow and reenter the coil of motor(same direction) and that is the reason why motors stops gradually as the induced current decreases gradually.


Finally, I completed the rest of schematics which was pretty intuitive.

![alt text](Schematics/GEMOTE.svg)

Now time for coding!! — **I guess**. Also, I hope I dont come back to schematic again😭.

**Total time spent: 4.3 hours**

-----










