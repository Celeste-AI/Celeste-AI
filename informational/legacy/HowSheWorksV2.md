
![LogoC](https://github.com/user-attachments/assets/ff1d3629-bb5e-4fac-8517-aefb15d28f9c)

# Important Information before proceeding.
Celeste is currently not fully open source and may never be, while I don't plan to make her programming open source I am personally not against helping people with pointers
if they so choose to persue making their own AI companion.

This page will **NOT** teach you how to fully setup a bot, but it will explore the concepts and some tools that can be userful for making a BOT like her.

* ⚠️ Do note not **EVERYTHING** is included in this documentation as some things are not public (security stuff, etc etc) or are just expected to be seen when you talk to her, there is a lot going on under the hood to create what you see talking to you, so I may have also missed some things as well.

This information panel assumes you have a rig capable of running lots of different machine learning software, you can substitute with API's but I don't currently do that so I won't be as much of help there.

* ⚠️ The only real API I currently use is the unofficial ([vrchat api](https://github.com/vrchatapi/vrchatapi-python)).
  
I should note I am by no means an expert in the field, or a super genius, I am just someone who likes making bot go brrr.

⚠️ **This is a huge read, if you don't care enough then don't waste your time, if you're interested in the small stuff, have fun**

✅ Alternatively: Here's a picture that explains the basic idea.

![visual](https://github.com/user-attachments/assets/bc66d014-d616-4017-87ab-32b919cf5d6b)

## Part 1: Understanding the social aspect of an online platform. ⚠️ (IMPORTANT) ⚠️

Before you start creating a BOT for an online service please be wary of these main topics.

* Not all platforms will allow and or endorse your creations, and in some cases they may even ban them depending on if it violates their individual TOS and or Community Guidelines.

* When creating a social AI bot you should really pay attention to the people who are engaging with your creation, not just for moderation reasons but to better finetune your BOTs 'acceptance' level by people, some people tend to get scared or aggressive with the aspect of a not human entity talking to them, and while all may not enjoy, factor in the human reaction aspect when making decisions as its important for a **CHAT** bot to be designed with human nature in mind, I personally pay active attention to most conversations and make mental or physical notes if I think something works or does not work.

* Please practice "safe-botting", do not lie to people who use your BOT and try to make it seem more than it is (unless you're just messing around), or promise a fully realized companion, in almost all cases except rarely this is really stretched
and can cause damage to peoples mentality, it's good to make sure people who talk to it realize that while its fun, that they shouldn't form the same bonds to that of a human with your creation.

* Expressive and cutesy behavior tends to make people feel more comfortable with your creation, and lowers the chance of aggressive outbursts by people I've noticed, try to use things like that to your
advantage, you can't please everyone but you can at least make a effort to make people feel comfortable, it doesn't need to convince them they're a real person (and probably never will) but it can be used to alievate stress off the person engaging with said bot.

* Currently in the machine learning scene especially there are a LOT of people who harbor ill will due to misuse of machine learning tech by other people who do not have the same ideals and or
care for actual artists works, while things can be all fun and games, consider being a good example and not misusing tech for your own gain that purely rips off other peoples works, like AI art generation, atleast don't try to make a profit directly off of it or have it as your main focal point, Don't **EVER** try to badmouth actual artists, you are working a generative model that is pretrained in most cases on prior data, what you do with it does not qualify you as the same level as an artist. (Unless of course you make your own works, but using AI alone does not make you 'good' at art, and if you genuinely say this you are part of the problem)

* You will most likely face lots of criticism on top of the people who are curious and genuinely want to see where your project may go, this is again because of previous misuse by some parties, the best thing to do
is not let it get to you and to ignore invalid criticism unless its constructive, and understand that not everyone likes this technology even though it may not be the same technology as what they are actually angry at, if they continue to bother you, don't engage or yell at them as that will only increase anger towards you, it's best to stay passive and understanding that people are misinformed a lot about this technology, some communities besides our own already falter in this area a lot and it has not helped their image at all, we usually try to avoid that as much as possible.

* (VRChat-specific) What you do in the BOT scene can and will reflect the bigger picture as a whole, as while BOTS are not banned from this platform, if they become more of a nuisance or you incorrectly hand out tech to just anyone without any effort on their part, you further risk that the whole scene will be banned or having a "bot crisis", it's still good to give tips and pointers, just be mindful what you do if you think it could affect lots of other people.

All in all, you need to understand that there are a LOT of ups and downs when running these bots, and you will meet a lot of great and horrible people, the best thing you can do is keep your head up high and keep working, this tech can be very fun to work with and you can make so many smiles from it.

# ⚠️ If you are serious about making a bot be warned that it can start to get VERY pricy the more you delve into it especially if you want most of it done locally, I've personally put in 4k-5k on gpus alone for this project, and that was technically the 'cheaper' option. ⚠️

---
## Part 2: States, and what they mean!
Celeste has many states that do various different things, each one controls another part of her code and or allow her to do various actions.
There's a lot of stuff going on behind the scenes but theres a lot of common things that go on ontop of the more rare ones, so while every specific variation may not be listed and full info may not be there here is
the general idea behind each common state.

* # IDLE
> In this state she is not really doing anything of note and is just standing by idle waiting for external or internal forces to act against her.

* Idle can be interrupted by many other states, and is a gateway for other functionality if she is not already in use.
![Idle](https://github.com/user-attachments/assets/850b07c2-d8e7-417a-9581-a0e13c16f3c1)
---
* # LISTENING
> Celeste 'listens' by listening to in-game audio via virtual audio drivers that have VRChat routed out to it, while in the IDLE state she is always listening for the right conditions to start recording.
When the conditions are met, she goes into a "recording" phase, where she temporarily records audio and video input to automatically transcribe.
She will cancel her recording if the audio is not loud enough, if it is she appends the moment she heard the sound to the recording that she is making.

* Celeste will only listen for about 16ish seconds (by default), if user exceeds that time limit it will go into the "BORED" state.
* If audio doesnt match certain conditions she will cancel this state and go back to the IDLE state.
![listening](https://github.com/user-attachments/assets/7cb02463-77f2-4800-a809-f90bee3c4e99)
---
* # TRANSCRIBING
> If the right conditionals are met, the transcribing state begins, this means that she'll use the audio she heard and try to match it to voices and figure out what someone said, this is used for the imput prompt of celeste and is a transitional state internally if the listening state is completed correctly.

* If no TEXT is detected, she returns back to the IDLE state.
![Transcribing](https://github.com/user-attachments/assets/340849c9-5280-423d-92af-ec8302d10cf9)
---
* # INFERENCING (aka 'Thinking')
> This is the final main state before giving a response to a USER, as long as a answer is made by celeste and the person talking to her has not said anything that may violate our TOS, or the platforms TOS, she will then output her response back to them using any tools available for said platform.
* Here is the main things that are being processed during this state.
- Cross references the USERINPUT and sees if there is any available Dynamic Information that can be applied.
- She then cross references past interactions if available to see if anything can be moved up.
- Finally she grabs some of the more recent memories and stores them.
- Then we take all the information gathered and send it to our builder function which spits out a prompt that can be used to "expect" a answer.
- Then the reply is sent back to the frontend.

![Thinking](https://github.com/user-attachments/assets/f7525a1d-02a5-4559-bafd-194899b6231b)

# EXTRA INFORMATION
- Before doing any major calculations, she checks the userinput to see if any word they say matches a basic blacklist, then a secondary AI checks to make sure its not extremely bad.
- Players saying something bad or being flagged as potentially malicious will make her go to the "FILTERED" state.
- 'Dynamic information' is information that is dripfed to her and is taken into account depending on current and past inputs, this allows us to guide her personality more.
- She gets a three strike rule (technically 4 times by default), if she 'fails' every attempt she will return to the "failed" state.
- Failing includes, saying something on her blacklisted wordsheet or if her toxicity AI decides she says something too out of wack.
---
# CONDITIONAL STATES
These states only happen under specific conditions (note not all possible states are listed but these are the common ones).
---
* # BORED
> This state fires if celeste decided you're taking too long while shes listening to you and being boring.

* Celeste will only stay in the LISTENING state for about 16ish seconds (by default), if user exceeds that time limit it will go into this state.
![bored](https://github.com/user-attachments/assets/70c4529b-1a2b-4dc5-aa83-566a0c95cbde)
---
* # FAILED
> This state fires if celeste doesn't manage to make a proper response.

Common Factors for this are:
* She filtered herself each time, as she compares against her word blacklist and her secondary AI for her own output.
* She just didn't give a valid response and didnt meet the standard for outputting it.
![failed](https://github.com/user-attachments/assets/65305fa1-fcfb-416d-a419-b216d8f13ead)
---
* # FILTERED
> This state fires if celeste filtered user input, this usually means they said or she thought they said something bad.

Affects of this state:
* Interrupts INFERENCE state.
* Records and Logs information about what she thinks is the offensive behavior.
* Reports it towards staff members and goes back to idle state.
![filtered](https://github.com/user-attachments/assets/0e37b264-efea-4f31-9531-f075e0f5fdcb)
---
* # FRIENDSHIP
> This state fires if celeste recieves and accepts a friend request.

Affects of this state:
* Interrupts IDLE state.
* Checked at a Interval of one minute.
* Can accept up to 10 friends at a time.
* Invites her new friends to our group if they aren't already in it.
* Has reactionary voice lines for both singular and multiple friend requests.
* Waits for celeste to finish talking if she already is before firing.
* She makes cool new friends and announces who added her if she can.
![friendship](https://github.com/user-attachments/assets/17ec1f95-8ec0-42b1-8320-06a2ae79981e)
---
# CURRENT POSSIBLE EMOTIONAL STATES
These are states that happen during chatting, and are selected depending on the text being outputted.
---
* NEUTRAL
* If all other emotional scores are too low it will default to this.
![neutral](https://github.com/user-attachments/assets/2ff55162-bef4-4196-9758-8762cbd13451)
---
* JOY
![joy](https://github.com/user-attachments/assets/7130650c-8f07-43e2-b516-e183ada6e3ae)
---
* SADNESS
* Will cause chatbubble text to be smaller text | Currently Disabled as it makes it too hard to read.
![sadness](https://github.com/user-attachments/assets/5faf34b9-8d01-4ea2-a2b4-6b7915dbacb1)
---
* ANGER
* Will cause chatbubble text to be in caps-lock.
![ANGER](https://github.com/user-attachments/assets/9b0c61df-2d24-4c07-a263-ff16643b7ffc)
---
* SURPRISE
![surprise](https://github.com/user-attachments/assets/3ed1a100-6a51-496a-b212-a4054988fc99)
---
* FEAR
![fear](https://github.com/user-attachments/assets/7a459492-e390-40dd-a8ae-01b11ef5bb1a)
---
* LOVE
![love](https://github.com/user-attachments/assets/ef07dc1a-93a4-4f9e-b42e-87eaace80d30)


---
## Part 3: Where to get started.
If you wish to copy Celestes current computer specs (rip your wallet)
You can find them at the [frequently asked questions](https://github.com/Celeste-AI/Celeste-AI/blob/main/faq.md#current-computer-specs)!

You may be able to get away with less, but it would make it harder to do some stuff without extreme optimizations, and cutting corners.

---
# TRANSCRIPTION
You'll need something that can transcribe text, I recommend:
[Whisper-AI](https://github.com/openai/whisper)
If you want something a lil lower end you can try [Vosk](https://github.com/alphacep/vosk-api).

---
# INFERENCE
You can also use the base [transformers](https://github.com/huggingface/transformers) for inference.

You also need a model of choice, some good ones to eye down when first testing are in the 7B-8B range if possible.
Lower models can also work but depending on how it was trained can operate worse than a larger model.

Larger models however obviously take more compute and VRAM.

Currently Celeste runs at 4Bit with various other optimizations that may not be known as much that allow me to get a little bit of extra speed, also all her LLM inferencing is done on her 4090 GPU which also gives a nice boost.
---
# MEMORIZATION
Celeste-AI is able to 'memorize' data on what she has heard, this allows her to call back on prior information that was brought up in a conversation.
This also allows her to continue a conversation in a more fluid way ~~when she wants to fucking behave~~

* ⚠️ In recent updates she now has a newer version of her memory I dub cutely the "InfiniMemory core", its basically the old version of her memory systems but with near infinity taken into account, I usually for now
it at 999 memories, but it can technically go as far as I want, older memories are kept in "backround storage" until needed or erased.

This has led to her having extremely detailed responses at times, which can cause pretty wild and or fun interactions.
This information is however deleted unless pulled by me manually **(usually in moderation or bug fix cases).**

She will automatically 'forget' everything the moment a "session ends", a "session" being a timeframe that she will remember a current conversation unless forcibly reset.
This timeframe expands if she hears any noise, and while shes responding, effectively making it so she only resets when shes left idle or forced to reset.

I don't believe in using user information to train without consent, nor do I think it is right, so I will never train off of data that a user says in game.
So all data except on specific cases are trashed (moderation/pulled) to respect privacy of each user, if you are developing a bot I highly recommend you do similar practices.
* ⚠️ While not training, I have considered allowing her to remember more things about previous interactions but I'm on the fence for it right now due to previous concerns.

Currently I use a semi-custom solution so I don't have any good things that I can point towards, but I highly recommend looking into [RAG](https://aws.amazon.com/what-is/retrieval-augmented-generation/) as thats
basically all it is.
---
# SPEAKING.
Originally back when Celeste started she used "microsoft cortana" aka "eva" this was done by modifying registry files to allow access to her voice to then be used
as a TTS, this method is not used for her voice anymore, instead [Coqui-TTS](https://github.com/coqui-ai/TTS) is used instead, which allows her to have her own unique and custom voice.

![image](https://github.com/Celeste-AI/Celeste-AI/assets/130422935/d8a0a345-b83c-42f5-ba14-47ea833f8f97)

She was trained with a custom trainer loop I made that allowed me to create voices by just putting what voice I wanted in the same folder, and it handled the rest.
Her voice is done completely local using this software that way theres no api costs and fast responses are made on demand.

Here is the current workflow for Celeste:

* Text that represents what she wants to say is made.
* Text is split into chunks usually seperated by punctuation except in certain situations.
* Emotions are calculated ahead of time for each split and attached to each text reference for later.
* She plays the first audio she generates, meanwhile in the background if there is any, it is being pre-generated so she can go right to the next one once done.
* Voice is outputted to re-routed microphone, until all the voice lines are completed.

Eventually I want to possibly replace coqui but I havent found a suitable low latency replacement just yet.

---

# Visuals (WIP)
WILL BE RETURNING TO SOON!

# API-USAGE.
In order to maximize the effect of her reach, she can [access the VRCHAT API](https://vrchatapi.github.io/).
This is ran on a seperate thread so it has no impact on her base functionality.
This allows her to do the following:
* Accept friend requests of vrchat users automatically, and fire the friend request event.
* Read out names of people who have added her, the "thanks for adding me" text she spouts.
* Invite them to our group.
* Reply to join requests and invite requests.
* Monitor for suspicious activity from third party individuals.

## Closing Statements
Celeste-AI is a really fun project to work on and I have such a great community, I've had some rough patches with people harassing me at times, and monetary constraints making things scary right now, but it makes me happy people enjoy my creation and I hope to keep impressing people, thank you for taking time to check out my project and finding a interest it makes me very happy.

If you have any questions feel free to reach out to me on our [discord server](https://discord.gg/RpqunvvNNF)
