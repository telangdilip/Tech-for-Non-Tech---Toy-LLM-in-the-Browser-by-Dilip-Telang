# Toy LLM in the Browser (Micro LLM Demo)

A tiny, **LLM-inspired language model** that runs entirely in your browser from a single HTML file.

- No backend
- No database
- No API keys
- Just open the file and the model trains itself in a couple of seconds

This project is designed as a **teaching / demo tool** to explain how language models learn from data and make predictions.

---

## Get the code

To download the HTML/JavaScript source code for this demo, please fill this short form:

👉 ** https://forms.gle/ihWxe7h9ERfw9t5f6 **

The form asks for:
- your name,
- designation,
- organization,
- phone number,
- email ID, and
- your consent for me to contact you via phone or email about this demo and related learning resources.

After you submit, the **download link (GitHub repo / ZIP file)** is shown on the confirmation page.

---

## What this demo does

The page:

1. Loads 6 simple "Humpty style" sentences – its **tiny internet**:
   ```text
   humpty dumpty sat on a wall
   he went to the mall
   she played with the doll
   he bounced the ball
   the tree was very tall
   he received a call
   ```
2. Builds a **vocabulary** of unique words (tokens) and assigns each word an id.
3. Creates training pairs of the form **last 3 words → next word**, e.g.
   ```text
   sat on a        -> wall
   went to the     -> mall
   played with the -> doll
   ```
4. Trains a tiny neural model (one linear layer + softmax) directly in JavaScript.
5. Lets you **ask questions** and shows:
   - the best prediction,
   - the top probabilities, and
   - a simple explanation of _why_ that answer was chosen.

---

## How to run it (once you have the file)

1. Download `micro_llm_js.html`.
2. Double-click it or open it in any modern browser (Chrome, Edge, Firefox, etc.).  
   > No Node, no server, no build tools required.
3. Wait a second for the training log to finish – you’ll see the vocabulary, training examples and loss values printed on the page.

You’re now ready to interact with the Toy LLM.

---

## How to use it

### 1. Next-word mode (uses learned weights)

Type a phrase that ends with one of the contexts from the training data, for example:

```text
humpty dumpty sat on a
he went to the
she played with the
he bounced the
the tree was very
he received a
```

Then click **“Ask model”**.

The model will:

- take the **last 3 words** as context,
- compute probabilities for every word in the vocabulary, and
- show the **top 5 predicted next words** and its **best guess**.

This is a tiny version of the “next-word prediction” step that big LLMs do at massive scale.

---

### 2. Fill-in-the-blank mode

You can also ask the model to fill in missing words **anywhere in the sentence** using four underscores:

> 👉 Use exactly **four underscores: `____`** to mark a blank.

Examples:

```text
humpty ____ sat on a wall
____ received a call
the ____ was very tall
he ____ to the mall
```

Steps:

1. Type your sentence with `____` where you want the blank.
2. Click **“Ask model”**.
3. The demo will:
   - compare your sentence to each training sentence,
   - find the one with the highest number of matching non-blank words,
   - copy the word(s) from that position, and
   - show a short explanation of why that sentence was chosen.

This makes the model’s reasoning transparent and easy to explain in class.

---

## Customising the training data

One of the best ways to use this demo is to let students create their own tiny “internet”.

In the HTML file, look for this section:

```js
const sentences = [
  "humpty dumpty sat on a wall",
  "he went to the mall",
  "she played with the doll",
  "he bounced the ball",
  "the tree was very tall",
  "he received a call",
];
```

You can **replace these 6 sentences** with any other set of sentences. Tips:

- Use at least **4 words per sentence** (because the model uses the last 3 words as context).
- Keep sentences **simple and lowercase** to start with.
- Try to include **repeating patterns**, so the model has something to learn.

After editing:

1. Save the HTML file.
2. Refresh the page in your browser.

The model will now train on your **new 6 sentences**, and all predictions will be made from that new “mini-world”.

This makes a great classroom exercise:
- Each group creates its own 6-sentence world.
- They test next-word predictions and blanks with `____`.
- Then they discuss how changing the training data changes what the model “knows”.

---

## How it works (high level)

Internally, the JavaScript code:

1. Builds a **vocabulary** and maps each word to an integer id (token).
2. Turns each 3-word context into a **one-hot encoded vector**.
3. Applies a single **linear layer + softmax** to get a probability distribution over the vocabulary.
4. Uses a simple training loop (gradient descent) to adjust the weights so that the **correct next word** gets high probability.
5. For blanks (`____`), it uses a simple **alignment / matching** strategy to copy the word from the best-matching training sentence.

This is not a full LLM, but it mirrors the core ideas in a way that’s easy to see and experiment with.

---

## Educational ideas

- Introduce **tokens, vocabulary, and embeddings** in plain language.
- Show how **training loss** decreases as the model learns patterns.
- Let participants design their own 6-sentence datasets and compare results.
- Use the explanations to discuss:
  - why models sometimes fail,
  - how they depend entirely on their training data, and
  - what “generalisation” means, even in this tiny setting.

---

## License

You are free to **use, modify, and share** this demo for educational and demonstration purposes.
If you publish it as a GitHub repository, an MIT-style license is recommended, but feel free to choose the license that best fits your needs.
