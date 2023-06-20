![Banner](https://user-images.githubusercontent.com/64008721/231066235-b29fdfe0-559c-4196-9ac9-82048582fc43.png)
# Introductory.
While Celeste-AI is not open source, I do wish to provide a way for parties more interested in the technical side of her to find out more.
This will **NOT** teach you how to setup a bot, but it will explain the more technical side ideas of Celeste-AI, do whatever with the information.

I will not use any third party services that require me to connect to an API unless absolutely needed, as I want celeste to be able to communicate as fast as possible to the user for the best experience possible.

The goal is also not to make Celeste a "super genius" that can never fail, the goal of the project is to further my own personal research into social behaviors & interactions with an AI, also just because its [F.U.N](https://www.youtube.com/watch?v=g_y15ozNchY)!

The end goal of the project is to keep making her more autonomous to the point I don't need to intervene much anymore, and so far its been staying on that track.

I should note I am by no means an expert in the field, or a super genius, I am just someone who likes making bot go brrr.

⚠️ **This is a huge read, if you don't care enough then don't waste your time, if you're interested in the small stuff, have fun**

## Part 1: Understanding the social aspect of a online platform.
⚠️ **Possibly one of the most important fundementals to consider while working on these things in my opinion**
* Due to this being an online social experience, you have to remember that people are people, at the end of the day if you don't understand this even a little.
You will struggle and possibly even fail, and while I am not perfect at this myself, I do actively pay attention to how users talk and or engage with celeste to gauge if a feature does or doesn't work, and I make adjustments as I see fit.

* Of course not everyone is trusting of AI as well, so I try to mediate that by making celeste more over the top in expression to eleviate some of the uncanny valley of the bot just standing there menacingly, which is why you see her react visibly more, as that's one of the more visible things I've noticed that make people more comfortable.

* In my own personal notes, I've noticed and adapted the idea of making her more expressionate not to confuse the user on her "validity as a human" but as a entity that
won't hurt them, or spy on them, which is also why I don't like the idea of public streaming celeste in public lobbies and never will. (moderation might go brr tho in private channels).

* I've also had to deal with many people who will straight up attack me and or belittle my work constantly as while its not much, it does mean a little bit to me as I put months of my time into my passion, I usually ignore invalid criticism, but some of them will even try to disrupt service, which is when unfortunately I have to actually moderate a instance, this is ALSO why I dislike it when people try to make assumptions or false claims on my projects because it tends to lead to people becoming hostile towards me and my work, while I am just trying to have fun and keep improving my service, this is also why celeste is in a public group instance, this allows me to have a bit more control of the people who refuse to act civilized, also is nice to kick crashers and malicious users :)

* People who spread misinformation may not always be bad people either, some people just don't look into a project enough or at all and just assume, or now and then some people are ANTI-AI (usually due to bad experiences with AI in the past) I find it personally silly to think all Artificial Intelligence is bad because of one bad experience but to each their own, which is why I usually TRY to be patient, but sometimes even I fail at this, I am constantly trying to improve my behavior while also studying the effects of an AI in vrchat, and working on her with those ideas in mind.

* All in all, you need to understand that there are a LOT of ups and downs when running these bots, and you will meet a lot of great and horrible people, the best thing you can do is keep your head up high and keep working, even if people don't always appreciate it, as long as you don't do anything bad.


## Part 2: Hearing
Celeste 'hears' by listening to in-game audio, she is always waiting for audio to reach a certain decibel.
When the conditions are met, she goes into a "recording" phase, where she temporarily records audio and video input to automatically transcribe.
She will cancel out the recording if the starting sound is not large enough, if it is she appends the moment she heard the sound to the recording that she is making.

Think of it like a TV clicker remote.

Here's to know when she heard a sound.

![Hearing](https://cdn.discordapp.com/attachments/1118304616627568770/1120698979450109952/image.png)

Here's when she is now in recording mode.

![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/8dfa8bb8-637f-40b0-ac5b-1ec61050dcb8)

During this mode, she will continue to listen to the user until they stop talking or until they hit the "max" limit for how long she can listen (around 15 seconds).

Once the conditions are met, she will then send this information over to her 'AIServices', after compressing and decompressing the data down to reduce network traffic.

# Introducing [Whisper-AI](https://github.com/openai/whisper)

Whisper AI once it recieves the decompressed audio buffer, takes in the information and then tries its best to transcribe it, since her computer is built for this task, she can do it quite quickly, she then also checks her filters and a secondary ai filter for specific cases of bad behavior, then returns the output of what she heard in text.

This can then be fed into the next part of her program.

# Part 3: Response Generation
Celeste 'thinks' by using a [HuggingFace transformers model ran locally](https://huggingface.co/docs/transformers/index).
She can load any model that is compatible with huggingface.
She basically sits her fat ass in the VRAM, which is why I like and or need stronger hardware.

This is the "thinking phase" of celeste.

![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/19789263-3e08-4817-b226-781cf4be2a84)

**(cheeks RGB, hand in a 'thinking' pose and eyes closed)**

During this phase, celeste is actively accessing her GPU with the input we recieved earlier and using her model that was loaded in VRAM to generate a response.
This is more cost effective long term, as using third parties can raise up quite a penny. (also I don't like giving even anonymized data to third parties).

Her computer is then able to effectively 'respond' extremely quickly, currently due to hardware limitations she is using a weaker version of her AI, if I wanted to improve her further in this regard I'd need better hardware. (multi gpu setup)

She tends to respond better if the user input is good as well, so saying simple stuff makes her act more simple a lot of times.

Celeste is given a 3 strike rule while generating a response.

⚠️ **She will fail a "attempt" if any of the conditions are met while generating a response.**
* She attempts to say a filtered word.
* She fails to stay in prompt.

If she fails all 3 strikes + the initial attempt, she will inform the user she could not make a response, this is to avoid an endless loop of her trying to answer
something her AI cannot seem to figure out.

## Part 4: Memorization.
Celeste-AI is able to 'memorize' data on what she has heard, this allows her to call back on prior information that was brought up in a conversation.
This also allows her to continue a conversation in a more fluid way ~~when she wants to fucking behave~~

This has led to her having extremely detailed responses at times, which can cause pretty wild and or fun interactions.
This information is however deleted unless pulled by me manually **(usually in moderation or bug fix cases).**

She will automatically 'forget' everything the moment a "session ends", a "session" being a timeframe that she will remember a current conversation unless forcibly reset.
This timeframe expands if she hears any noise, and while shes responding, effectively making it so she only resets when shes left idle or forced to reset.

I don't believe in using user information to train without consent, nor do I think it is right, so I will never train off of data that a user says in game.
So all data except on specific cases are trashed (moderation/pulled) to respect privacy of each user, if you are developing a bot I highly recommend you do similar practices as a moral standpoint, but I digress.

## Part 5: Speaking & Speaking.
Originally she used "microsoft cortana" or "eva", this was done by modifying registry files to allow her voice
to be used as a tts, this method is not used anymore for her new voice, instead 

![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/d8a0a345-b83c-42f5-ba14-47ea833f8f97)

[Coqui-TTS](https://github.com/coqui-ai/TTS) is used instead, which allows her to have her own voice.

She was trained using my custom software that combines whisper and reused portions of her hearing code, this allows me to copy any voice insanely quickly just by dragging files into folders as long as I have lots of data on the voice.

![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/55718de7-18d0-4b0f-8832-9c1517c76e36)

The trainer, is the best tool I've made for her so far, it saves so much time, and hassle and handles the nitty gritty.

Celeste has a locally trained voice that was made for her, this allows her to sound more 'unique' without the costs of using an API service.
This can take a while to train however.

This is the same for her singing voice which currently uses:
[so-vits-fork](https://github.com/voicepaw/so-vits-svc-fork)
however I cannot do this live, I preload her up like a mp3 player.

Back onto the topic of actually speaking, she has to double check that her AI can actually SAY a word before outputting it, sometimes she can crash due to trying to divide by zero (lol) if I don't do this. So she does some basic sanitization before trying to speak the response.

During this, for each sentence break, celeste attempts to 'figure' out what emotion she has with a emotional wheel AI, if she does not detect any emotion to a certain degree she stays neutral, if she does she can use the following emotions.

**HAPPY**
![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/1cbbcca0-38e7-4edd-bd98-29dcce02928b)

**SAD**
![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/3de5115b-6f51-4a42-bf67-a72ee0cca5f1)

**ANGRY**
![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/aa766952-d776-468d-a8f0-7e1d2e360d69)

**SURPRISED**
![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/68f4e2e0-bfb8-44ca-8701-b76ce18ca838)

**FEAR**
![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/2fe5d0fa-018c-46aa-9e46-c00c598f63b3)

This improves her expressiveness and has huge impacts on the approachability chances with her.
She sometimes guesses a lil off though, but in my opinion it adds to her personal charm.

## Part 6: Visuals (WIP)
Celeste is able to see technically, but I am still working out the fine details, she is also able to object detection but that has not been ported over to the new version of her software yet, I am in the process of doing this as we finish some shader math to better understand the
Position & Rotation of celeste in world space, which will eventually allow her to not need any assistance with moving anymore. (hopefully)

## Part 5: API-USAGE.
In order to maximize the effect of her reach, she is able to [access the VRCHAT API](https://vrchatapi.github.io/).
This allows her to do the following:
* Accept friend requests of vrchat users automatically.
* Read out names of people who have added her, the "thanks for adding me" text she spouts.
* Invite them to our group.
* Monitor for suspicious activity from third party individuals.

## Closing Statements
All in all, Celeste is a really fun project to work on and I honestly truly want to keep improving her, I'm still learning so I am a little bit slow but each day I'm getting better at it, Celeste got me into python coding all those months back and I want to keep getting better.
There is a TON more optimizations and cogs going on than what I have informed of in this passage, but I hope it paints the basic picture of celestes design and the future I'm going for and continue to go for, thank you for listening to my ted talk.

If you have any questions feel free to reach out to me on our [discord server](https://discord.gg/RpqunvvNNF)
