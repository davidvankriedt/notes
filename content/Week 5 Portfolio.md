---
title: Week 5 Portfolio
draft: false
tags:
  - computer-science
  - cybersec
---

## Security Everywhere 
 
My dad called me asking me if I was okay. He got a message saying that I had broken my phone, and that I needed help. Luckily, my dad noticed something was off and called me to check. I asked him to screenshot the message, and to not click on any links in case it was some sort of XSS attack. But I was still nervous about him even clicking on the text chat. This is another example of how easy it is to leak your information, and that it often isn’t an issue with the technology, but it’s the human condition that is the vulnerability.
 ![[Screenshot 2026-07-12 at 09.09.39.png]]
## Security Engineering 

### Where are you right now? 
 
 I have been into running lately. Since I get bored quite easily, I decided to use the app Strava, and additionally its child app Runna - a running coach that personalises weekly plans for you and helps you achieve set goals. Strava is a social platform where runners/swimmers/cyclists post their trails and create a community in their areas. Accordingly, it is clear from the start that given it tracks where you are running. More specifically, Strava tracks GPS coordinates (latitude, longitude) through your device’s GPS chip, as well as timestamps, and plots these on a map used to create a route at the end of a session - through this data they also calculate speed. Additionally, they request access to your device’s biometric data monitors to obtain heart rate (through PPG light sensors in smartwatches) and cadence. Since this app is mostly about tracking activities and measuring progress, alongside sharing achievements to other users, Strava makes it very clear they are tracking such things, and it’s mostly seen as a good thing that they are doing so, otherwise the app wouldn’t be so useful. In the beginning, users aren’t shown an informed consent form, but are rather informed by the OS to confirm consent, which isn’t a huge issue given what the app is meant for. Although the user isn’t constantly reminded, after a quick web search it is clear that Strava allows users to opt out of location and biometric tracking - in this case, users have to manually input the data of a given session. However, the app’s community-based environment makes it hard not to want to share this data - on a public account, your routes are publicised in the area and contribute to metrics such as most popular routes and alternatives, thus helping other users in the area.

If we begin to speculate, one could easily arrive at the idea that Strava could eventually sell this data to other companies such as Google, or government agencies, to monitor people traffic. Moreover, an existing concern is that people who habitually run or record workouts, are likely to do so near their home, and without explicitly trying to, users build a profile of habits around their house - where they take their dog, where they shop, where they meet their friend - and despite Strava attempting to obscure a users home address by hiding the starting and ending 5 minutes of a workout’s location, this data is very useful for home intruders and other criminal entities wanting to track a person.

In reality, there are few ways to avoid being tracked by Strava and Runna. Whilst it is true you can disable location and biometric tracking and input these values manually for every workout, this is tedious, and is what the app was initially meant for, meaning if you are going to do something like that, it’s probably best to not use the app at all; Strava and Runna are essentially popular tracking platforms, and using them inherently comes with these risks - is tracking your workout activities worth exposing your location?
 
### Password hash cracking 

#### Dictionary Attack

A Dictionary attack is using a subset of letters/symbols to figure out a password/decryption key. It runs these words through a hashing algorithm and compares those to the target. It originally used words from the dictionary, hence the name, but now refers more to the very large lists of leaked passwords found in the internet from previous attacks. This is more effective than a brute force attack because people are more likely to use a common password or the same password instead of a random set of symbols.

#### Rainbow/Lookup Tables

This is a large pre-computed table of hashes of commonly used passwords. Attackers use it to match the hash against the target rather than having to compute a hash each time. They are ineffective if the hash algorithm uses “salt” (meaning adding random characters to the password before hashing) like bcrypt. It is similar to the Dictionary attack, but is quicker because they’re given the hash output against the word.
Birthday Attack
There is a paradox in probability called the birthday paradox, which basically says that there is a very high possibility of 2 students sharing the same day in a classroom, despite there being quite a small chance that a student’s birthday is on a specific date. Through this paradox, attackers try to find a collision with a file they’re targeting, such that they can infiltrate a malicious file into a system with an identical hash that won’t alarm the system they’re attacking. This attack happens more frequently in older encryption hashing algorithms such as MD5 and SHA-1 which generate a much smaller output size (there’s less possibilities).

#### Chosen-plaintext Attack

This attack involves using the public encryption key to learn from how the encryption system encrypts plain text. Then, by continuously inputting plain text, we can use mathematics to watch patterns arise (studied in cryptanalysis) and the attacker can reverse engineer the password. It’s basically guessing inputs, and making educated guesses, until figuring out the encryption pattern. This is used for breaking encryption like AES rather than hashing, because since hashing is a one-way function, it doesn’t use a key that can be recovered through such an attack.

To decrypt the MD5 password hash: 482c811da5d5b4bc6d497ffa98491e38

#### Crack an MD5 Password Hash

I simply looked up a rainbow table/reverse-lookup for MD5, and inputted the hash, and immediately got back password123.

### Database Dump
For this exercise, I first tried to look up the same reverse-lookup or rainbow table for bcrypt, but since this hash algorithm uses salt (adding random characters to password before hashing), rainbow tables don’t work in this case…
I looked up how I could crack a bcrypt hash on the web, seen as I didn’t know how to implement an algorithm to use a dictionary for common passwords, and that’s how I found hashcat, which does exactly that given a hash and a password dictionary (if I set attack mode to 0), I then looked for popular password dictionaries and found rockyou.txt, but when I started hashcat with rockyou.txt it was going to take way too long to search the namespace (10 hours), so I gave up and looked at the hint in the exercise, which pointed to SecLists. I then looked at the seclists password lists and tried the 10k-most-common.txt against the 4 hashes given (1min per hash), but unfortunately all of the hashes failed against the 10k most common. I then tried the 100k-most-used-passwords-NCSC.txt. I still got no result. I finally tried xato-net-10-million-passwords-10000.txt. Unfortunately, after all of this, I still wasn’t able to find any of the passwords from the given hashes.

### Bitcoin mining 
 
I am more and more impressed by how many tools are available for free, such as openssl, and hashcat in the previous exercise! I found it very interesting to learn about blockchain technologies, and although creating a new block, and verifying it was very easy in this scenario - where the only criteria to be met is that my new has needs to start with a 0 - it was still a good exercise to get my head around how blockchain such as bitcoin might be verified.

One thought I did have about this activity is that I saw a few valid blocks, that were still incorrect due to concurrency issues with the commenting system - a few people had used what they might have thought was the last block in the chain, and whilst creating their own block and verifying it, someone else posted a new block, making their ‘previous block’ section invalid. This essentially erases blocks from the chain as only one block can be adjacent to another.

Moreover, it was very cool to see how only one number at the end of my string completely changed the hash output (going back to the policy that 1 bit must change at least 50% of the hash), and even though I expected it, it was quite interesting to see it put in practice - such a relatively short string provides sufficient encryption, to the point where sha256 still hasn’t been broken. 
 
## Extended 

### CTFs
#### Format String 1 - Number leak
This binary prompts the user to input a name, and then asks for a number. If you guess the number correctly, you get the flag. I approached this challenge after watching the extended lecture, and it was quite easy to get.

I began by inputting “test %d ing” as my name, this would force printf() to fetch the first thing in the stack after the function call. This gave me “0” back. Assuming that 0 wouldn’t be the answer, I decided to look into the source code:

![[Screenshot 2026-07-12 at 10.19.21.png]]


It was clear that the program got my inputted name through get_name(name), then generated the number, and then greeted me. This meant that myNum was likely to be within the most recent stack frames! So, I then decided to input “%d %d %d %d”, in the hopes that this would output the last 4 found numbers in the stack. Here is what I got in return:

Hi 0 9707 0 -4770552 134514874, I bet you can't guess my number!

Since I had already gotten 0, I tried the next number, and that was the answer! Although it remains confusing to me why the number wasn’t the first, it was still interesting to see how easy it is to look beyond scope with such a common function like printf(). This makes me think of how vulnerable the code written by COMP1511 students is, and really anyone unaware of this exploit.

#### Format String 2 - Advanced Login

This challenge took me longer than expected. After first running the program,  the user is prompted to guess a password. I first tried the input “test %d ing”, and this gave me “1229800513”, but it wasn’t the secret password. I decided to try “%d %d %d %d” like in the previous exercise - this gave me a bunch of random numbers, “1229800513 858927438 10 0“, and none of them were the secret password either.
From here, I thought that the numbers I was getting might not be numbers in the first place. So I inspected the code: 

![[Screenshot 2026-07-12 at 10.19.43.png]]
In the vuln() function, we see that after the password is inputted, if it’s wrong, it uses printf() to print our input. Luckily for us, the function declares and initiates 2 variables: input[100], and password[40]. I then knew that I was targeting the password char array.

So, I inputted “%c %c %c %c” in an attempt to fetch the first 4 characters of the array. However, even though I was getting letters, they were random, and they didn’t work as a password. Then I remembered, since I am working on 32 bit architecture, memory is stored in 4 bytes, meaning the password array was stored in rows of 4 bytes. This means that when I went to fetch “%c”, it got the first byte from that stack frame, and skipped the other 3 bytes, so I was basically getting the first character of each stack frame displayed. This meant that I had to find a way to get the 4 bytes. Here, I could use “%p” to fetch a pointer to a memory address in the stack frame, and given the input array stores 40 characters, this needed 10 memory addresses in the stack. I then inputted “%p %p %p %p %p %p %p %p %p %p”, and I ended up getting hexadecimal addresses! 0x494d4441 0x3332314e 0xa. Since I know the architecture is little-endian, I translated the hex values backwards, and got a readable message. I then used that as the password, and I was in!

####  Format String 3 - Favourite Number

 This program gives you a random number > 100, and then asks for your name. The goal is to change the number such that it is < 100 to capture the flag. I first tried the typical “test %d ing”. For the first time in this series of challenges, I got this response:

“Nice to meet you test %d ing”

I inspected the code:
 
 ![[Screenshot 2026-07-12 at 10.20.13.png]]
 
 Here, you can see that in main(), the favourite number (a global variable) is assigned a random value, and then we enter vuln(), where the input is an array of 40 bytes, and fgets is used to get the user’s name, meaning there is no buffer overflow from the input - I even tested this by inputting 1234567890123456789012345678901234567890 (40 characters) and only got 38 characters in return.

It is clear that my goal here is to exploit the printf() function, and then rewrite that address with a number < 100.

Luckily, I learnt in the lecture about “%n” and how it rewrites a specified memory address with the length of the input already in printf. To do this, I first needed to know the memory address of my target, favourite_number. I went into gdb and inputted “print &favourite_number” which gave me its memory address, 0x804a044.

Since %n won’t be given an argument pointer to go to, it’ll treat the first thing at the top of the stack as a pointer. Therefore, if I input text in the printf function before %n, it’ll write that text into the input buffer array, which will sit at the stack. Therefore, if I write the memory address of favourite_number, it’ll rewrite that memory address with the length of the memory address (4 bytes), which is < 100!

As I have to input a memory address in bytes, I can’t just use the terminal to input into the program as that would give text to the program. So I used python to write the bytes, the %n, and a \n at the end to input to the program:

python3 -c 'import sys; sys.stdout.buffer.write(b"\x44\xa0\x04\x08%n\n")' | nc fstring3.comp6841.xyz 5012

With this, I was able to change favourite_number, and got the flag!

This method is quite strange to me, it took quite a lot of guessing, like assuming whatever I wrote before %n would be sitting at the top of the stack when %n did its job. Although I got quite lucky, this exercise, alongside COMP3231, has really encouraged me to start learning gdb :)
 
## Analysis and Reflection 

### Tutorial 5: Snoop 

#### Government Surveillance vs the privacy of citizens

Points for government surveillance:
- Telecommunications and Other Legislation Amendment (Assistance and Access) Act allows gov agencies to request tech companies to help decrypt communications, and thus track down criminals through encrypted messages. Given the terror threats, cyber crime, foreign interference, and child exploitation in games like Roblox, law enforcement argues that backdoors to such communications systems are imperative.
- The Australian government built mobile phone detection cameras to save lives through reducing road fatalities.
- Facial scanning has been introduced into different sectors in order to use biometric tracking for convenience and safety.


Against:

- 329 people have died on NSW roads 2020. The state wants to cut the number of road fatalities by 30% by 2021. It did reduce in 2021, but has since increased in 2026 beyond the statistics in 2020, even though it did reduce phone distraction - didn’t solve the problem, but there’s still surveillance
- Alibaba's new FlyZoo Hotel using facial recognition to check in, lack of privacy for the customer.
- Taylor Swift using facial recognition secretly at a concert to detect stalkers.
- Cole’s partnered with Palantir for facial recognition, customer shopping habit tracking - customers stealing is a small factor
- Extended level of access to technologies exposes them to more potential hacker attacks.

Debate
 
 Government surveillance poses a greater threat to the freedom of citizens than the risks that such advances claim to reduce.

Pro-surveillance

Mass monitoring serves as a powerful mitigator to crime-prone activities, lowering the crime rate around areas where it’s implemented.
Facial recognition is operationally efficient and makes everyone safer, from venues to hospitals, to even shopping centres.
Monitoring of encrypted chats really does stop a lot of cybercrimes.

Anti-surveillance
 
Leaving backdoors within encrypted systems exposes the public to exploitations and cyberattacks.
Whilst facial recognition might help mitigate crime, there is still a massive loss of privacy for the citizen when their habits and biometric data is tracked and used for marketing, etc, and there is still the chance that such data could be leaked.
Mass surveillance in public roads, and other areas is always monitoring, and would probably remain there even if lower fatality goals fail to be realised, leaving to the unnecessary monitoring of the public.
Conclusion
 Whilst government surveillance promises to tackle very serious societal problems such as cybercrimes, child exploitation, crime circles, and road accidents, it also brings about a collection of citizen data, unproportionally large compared to the rare occasions where such data helps reduce crime. Therefore, increasing or even maintaining government surveillance instead adds risk to public freedom and needed privacy, as well as lowering the overall health of cybersecurity in Australia, and around the world in the long term, at the cost of lowering danger in the status quo.
