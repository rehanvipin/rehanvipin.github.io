---
title: 'Local AI'
pubDate: 2026-06-06
description: 'Offline development using AI coding tools'
tags: ["blogging", "learning in public"]
layout: ../../layout/BlogPost.astro
---
# AI coding tools without the internet
I've always liked offline programs.
I used to play Pokemon on my phone through an emulator. Pokemon Emerald was my favourite. It was great to be able to play them when I didn't have Wi-Fi.
It's a good feeling to be able to have complete independence from the internet to be able to run your program the way you want.
It's even better when such programs are open-source, as you can hack around to acomplish your goals.

Another good part about this setup is that there's no subscription costs. Like most people, I'm not a fan of maintaining subscriptions, so this worked out well. I wouldn't mind paying a one time fee for the software, but recurring payments? I try to avoid them.

Privacy is another point. You know for sure that your data isn't going anywhere. Yeah, telemetry is a thing, but I turn it off wherever I can see.

<br/>

## Understanding the setup
I've used GitHub Copilot and Claude Code for my enterprise work, so I knew what to expect, however, those tools abstract away some of the inner workings and the setup of the system. However, after some online research, OpenCode seemed to be a good starting point.

I used OpenCode for a while with some of their free models, that's quite similar to how our enterprise setup worked.
We use premium models, but at least *I* don't have to pay for them.

Then I went ahead and connected it to my Claude account through an API key. That showed how it was possible to have your coding tool and your model running in different places.

So I basically need to choose a model and run it on my system. How hard could it be? I've worked on deep learning projects before, and have trained and run models with PyTorch and Tensorflow on my laptop. Around 6 years ago, though.

I'll detail my experience below, but it was very different. Models have grown drastically in compute requirements, especially LLMs. Staying true to their name.

<br/>

## Finding a model
This isn't the first time I've tried to run a model locally. A year ago or so, I had tried to run one of the early DeepSeek models, and that crashed my Windows system, so I knew I had to be more careful with my choices. 

However, times have changed, and there's been a lot of improvement in local models. Gemma seemed to be getting some good news, so I picked them. Also, I'm running Linux as my Desktop OS this time, so it should have fewer competing processes running around.

Gemma 4 is the model I used. There's also so many variants of these models now. The model card and the hugging face docs do a good job of explaing them.

This is the model I ended up choosing - https://huggingface.co/unsloth/gemma-4-E2B-it-GGUF .
That's not very powerful according to the model card, but it's the only one which ran on my system.
The GGUF format seems to be an efficient format, and supports quantization too. I chose the Q4_K_M variant of the model.

<br/>

## Setting up a model inference server
This was something I had done for the first time. Ollama, LM Studio, and Jan were the initial contenders, but I heard that they could be slow. Heard where? On a few reddit forums. llama.cpp seems to be the most "efficient" model inference runner.

I wonder if these tools really need to be that complex. The main goal is to run the model with the specified wegihts efficiently.
Inference effectively.
I should do more research and see what's the complexity about.

<br/>

## Connecting with a AI agentic tool

After I downloaded the model weights, and got llama.cpp to read that and run a server, it was really simple to connect it to OpenCode.
Although, it is excruciatingly slow. The Web UI for the tool was slow too, but at least it returned responses.
OpenCode just terminated. I'll have to find more efficient models or figure out a better way to run the model.

I was able to find a fix for that, finally. Running `nvidia-smi` tells you if your GPU is being used.
And in my case, it wasn't so I checked the list of devices from the llama command and used a flag to tell it to use the GPU.

<br/>

## Finding a REST API client
I've tried out postman, insomnia, bruno over many years, and now yaak's the one which I like the most.
The UX is the simplest out of all the other tools, it's definitely not corporatey like the first two, and it solves the problems I have.
Check it out at [yaak.app](https://yaak.app). It has a plugin system too!

<br/>

## Making local inference faster
These are some of the steps I took to make inference faster:
1. Make llama cpp use the GPU using the -dev flag
2. Reduce the number of slots which it uses. By default, it's 4. I reduced it to 1 when a friend told me that it would reduce the split in memory. This reduces time by 3x. It actually controls parallel processing.
3. Use the Web UI which it brings up. I was using the openai based chat completion API and it used to take a minute to respond to a simple "hi", while the local webpage would respond within 5 seconds. I found that it passes an extra parameter in the request body - `"chat_template_kwargs":{"enable_thinking": false}`. This makes it much faster. There is a flag to turn it off at the server level, `--reasoning off`

With all this done, the qwen model (yes, I said gemma earlier in this article, but I switched to qwen since it's faster), gives responses much faster. It's usable from APIs, but now I need to figure out how to make it usable from opencode.

This is the model which seems to be able to work on a laptop setup - `unsloth/Qwen3.5-4B-GGUF:Q3_K_S`.

Need to figure out how to log the requests that llama receives.

It actually makes sense as to why the chain-of-thought slows down the response, since it generates a lot more tokens.
However, for simple prompts like "hi", there's no need to do this. I can understand that this is useful for reasoning models when they are working with complex tasks where thinking about an answer in a step-by-step fashion would improve correctness.

<br/>

## What do agentic AI coding harnesses do?
I added debug logs to the llama server to see how opencode was interacting with it. Some fun things:
1. Before actually responding to the user, it asks the model to generate a title for the conversation.
2. It prefers to operate in streaming mode. Which makes sense. To not keep the user waiting.
3. It asks the server to tell it how much tokens the model read / generated.
4. It adds large amount of system prompts in the API call, with generous number of examples on how to respond.
5. It tells the server what tools are available, and how to use them. This is not via text, but through a specific JSON object.

That's really all the special things which it did. Otherwise, the API calls are quite simple.

Debugging the API request / response on the local machine was made simple by tcpdump & scapy.

<br/>

## Next Learning Items
I found some new concepts when doing this experiment. Should go over them some time.
* Dynamic quantization. https://unsloth.ai/docs/basics/unsloth-dynamic-2.0-ggufs
* GGUF file format. https://huggingface.co/docs/hub/gguf
* What is MTP optimization? https://unsloth.ai/docs/models/mtp#qwen3.6-mtp
* Why does MTP not work on my device?