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

<br/>

## Next Learning Items
I found some new concepts when doing this experiment. Should go over them some time.
* How to run the mode locally. https://unsloth.ai/docs/models/gemma-4
* Dynamic quantization. https://unsloth.ai/docs/basics/unsloth-dynamic-2.0-ggufs
* GGUF file format. https://huggingface.co/docs/hub/gguf
* Is my GPU really being used? How do I figure that out?
* What is MTP optimization? https://unsloth.ai/docs/models/mtp#qwen3.6-mtp

I think a good overall target will be if I can get this setup to help me code this website.
