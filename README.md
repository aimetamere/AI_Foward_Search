<h1 align=center><strong>Forward Search Uni Assessment 🤓</strong></h1>

# Hi, I'm Nicolas de Haan 👋
This is a small project I built while exploring logic inference systems during my studies at CODE University in Berlin. The idea was to create a forward search engine — something that could take a bunch of logical rules and facts, and try to figure out new truths from them.

I didn’t have much experience with this kind of reasoning at the start, so a lot of it was trial and error. I just wanted to see if I could make a program connect the dots on its own, kind of like how we do in our heads when something "clicks."

It’s far from perfect, but it works in most cases — and it gave me a better understanding of how reasoning engines tick. This project was also a nice way to apply what I’d learned from working with C and low-level logic into something a bit more abstract and algorithmic.

## What is the Outcome ? 

So, the way forward search works it goes like this: 

- Some **known facts** (like "Socrates is a man")
- Some **rules** (like "If someone is a man, then they are mortal")

Then:

- You keep inferring new stuff from what you already know.
- You do this over and over until either:
  1. You get the answer you were looking for
  2. You can't learn anything new, and you're stuck

There’s no backtracking, no guessing — just going forward through what feels logically provable.

## What the code actually does (line by line-ish)

### `check_proven(knowledge, query)`

This function checks if the query is already sitting in the knowledge base.  
- If it finds it -> returns `True`  
- If it finds the **negation** of it -> returns `False`  
- If it finds nothing useful -> returns `None`  

It’s the early-exit option for the loop, basically.

---

### `get_inferrable_knowledge(knowledge)`

This is where the inference happens.  
It loops over all the statements and tries to squeeze new facts out of implications or biconditionals:

- If we have something like `A -> B`, and we know `A`, then we can now say `B` is true.
- If we have a biconditional `A <-> B` and we know one side, we can infer the other.

I didn’t build anything fancy like chaining chains or resolving contradictions — just basic one-step logical inference.

---

### `forward_search(knowledge, query)`

This is the big one — it’s the loop that pulls everything together:

1. Make a fresh copy of the knowledge base (to avoid mutating the original — I learned this the hard way)
2. Dump all the facts into a set so we can track what we know.
3. Check if the query is already proven (`check_proven`) — easy win if yes.
4. Otherwise, ask: "Based on what I know, what else can I figure out?" (`get_inferrable_knowledge`)
5. If we find anything new, we add it to our known facts and loop again.
6. If we don’t, we give up.

From my humble understanding it like you have a keychain and you try them all one by one until it works or you run out. 

---