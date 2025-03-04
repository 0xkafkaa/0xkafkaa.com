+++
title = "Building Suttakural - A fun little project"

[taxonomies]
tags = ["books", "tinkering", "code"]

[extra]
toc = false
+++

<div class="center">
<img src="/img/blogs/suttakural.png" alt="suttakural web UI">
</div>

What happens when you mix ancient wisdom with modern sarcasm?
So, ever since I had a look at this [Thirukural dataset](https://huggingface.co/datasets/Selvakumarduraipandian/Thirukural) I wanted to build something with it, that's when a simple thought: What if Thiruvalluvar could roast people based on their thoughts? Hence [Suttakural](https://suttakural.kafkaa.xyz/) was born - a webapp that roasts you using Thirukural, blending Valluvar's wisdom with AI-generated burns.

The stack is actually simple, the client sends a query to an LLM and the LLM picks up a relavant Thirukural and generates a bunch of roasts and later they are rendered in the frontend. Sounds simple right but I don't wanna do it this way primarily because of two reasons firstly, its boring and secondly, I don't wanna spend anything on acquiring an API key and also the roasts from Gemini are so lifeless.

That's when I decided to do this the hard way which is to generate the roasts beforehand using an LLM. I crafted a bunch of tailered prompts and got the data I needed.

```json
{
  "id": 928,
  "kural_tamil": "களிததறியேன எனபது கைவிடுக நெஞசதது\nஒளிதததூஉம ஆஙகே மிகும.",
  "kural_english": "No more in secret drink, and then deny thy hidden fraud; What in thy mind lies hid shall soon be known abroad.",
  "theme": "Secrets and Lies",
  "roasts": {
    "1": "You think no one knows? Bro, even your bottle is judging you harder than your conscience.",
    "2": "Stop pretending, your secrets are spilling out like your last drunk confession. We see it all.",
    "3": "The only thing hidden is your shame, and trust me, that’s coming out faster than you can cover it up.",
    "4": "You can lie about your drinking all you want, but the truth is already public knowledge, bro.",
    "5": "You’ve mastered the art of deceit — but the only thing you’re hiding now is the inevitable humiliation."
  }
}
```

Then I pushed them into a vector DB with the vector embeddings generated for the roasts using a [Sentence Transformer model](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) - it maps sentences & paragraphs to a 384 dimensional dense vector space and can be used for tasks like clustering or semantic search.

Then spun up a fastapi backend which sends a query to the vector DB and does a semantic search and retrieves the result which is later rendered in the frontend.

Now, everything works the way I wanted it to be. Not its ready to be deployed and I was in a notion that is should be pretty easy. But here is where I spent so much time troubleshooting.

<div class="center">
<img src="/img/blogs/sk-arch.png" alt="suttakural arch">
</div>

So, I ususally deploy by projects in my server as I have mentioned in the earlier blogs. But one problem was the Docker image of the backend was pretty huge and I know it should not be this case. Since I was using an ML model for generating text embeddings, it downloads a bunch of dependencies which I don't need to begin with and I haven't worked on ML models, so I had no clue whether this was normal. After a night of scouring the internet I understood how to make use of only the dependencies I need and finally reduced the size of the image. And now the backend is up and running.

Next hassle was with configuring the reverse proxy and I use Caddy as my reverse proxy, by the way. So, if you are not aware, Caddy automatically obtains and renews TLS certificates for all your sites by default. But for some reason my backend was running only in _http_ and it needs to be running in _https_ to connect to the frontend. I wasn't able to piece them together.

I tried a bunch of troubleshooting and even manually assigned the TLS certificates but nothing seemed to be working. But later found, I was making a dumb mistake. Reverse proxies should not be exposing the port in which the application is running, instead it should route traffic securely while keeping backend services hidden. But I was able to access the backend with my server IP tagged with the port running the application. So, the issue was I was binding the port of the backend to all interfaces with 0.0.0.0 instead of the localhost 127.0.0.1. Once I corrected this, everything worked as expected.

So, here you go. [Suttakural](https://suttakural.kafkaa.xyz/) - a web app that roasts you using Thirukkural, blending Thiruvalluvar’s wisdom with AI-generated burns.
