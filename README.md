# Text-Generation
# 🤖 Text Generation using AI

A simple **AI-powered Text Generation application** built using **Python, Streamlit, Hugging Face Transformers, and the Qwen language model**.

The application allows users to enter a prompt and generate AI-based text. Users can also control the **maximum length** and **temperature** of the generated text.

---

## 📌 Project Overview

Text generation is an Artificial Intelligence and Natural Language Processing (NLP) task where an AI model generates human-like text based on a given input prompt.

For example, if the user enters:

```text
Artificial Intelligence is
```

the AI model can continue the sentence and generate relevant text.

This project provides a simple web interface where users can enter prompts and generate text without directly interacting with the Python code.

---

## 🎯 Objectives

* Understand the basics of **AI-based text generation**
* Learn how to use **Hugging Face Transformers**
* Integrate a pre-trained language model into a Python application
* Build an interactive AI application using **Streamlit**
* Understand text-generation parameters such as `max_length` and `temperature`
* Generate text based on user-provided prompts

---

## 🛠️ Technologies Used

| Technology                   | Purpose                          |
| ---------------------------- | -------------------------------- |
| 🐍 Python                    | Programming language             |
| 🎈 Streamlit                 | Web application interface        |
| 🤗 Hugging Face Transformers | Loading and running the AI model |
| 🧠 Qwen                      | Pre-trained language model       |
| 💻 VS Code                   | Development environment          |

---

## 🧠 Model Used

The project uses the following Hugging Face model:

```text
Qwen/Qwen3.8-2.4T-A95B
```

The model is loaded using the Hugging Face `pipeline()` function with the:

```python
"text-generation"
```

task.

The model receives the user's prompt and generates a continuation based on that prompt.

---

## 🔄 How the Project Works

The application follows this workflow:

```text
User enters a prompt
        ↓
Streamlit receives the input
        ↓
Prompt is sent to the Qwen model
        ↓
Model generates text
        ↓
Generated text is displayed
```

---

## ⚙️ Working of the Application

### 1. Import Required Libraries

The project uses Streamlit and Hugging Face Transformers:

```python
import streamlit as st
from transformers import pipeline
```

**Streamlit** is used to create the web interface.

**Transformers** is used to load the pre-trained AI model.

---

### 2. Configure the Streamlit Page

The page is configured using:

```python
st.set_page_config(
    page_title="Text Generation App",
    page_icon="🤖"
)
```

This sets:

* Page title → `Text Generation App`
* Page icon → 🤖

---

### 3. Create the Application Title

The application displays:

```python
st.title("🤖 Text Generation using AI")
st.write("Enter a prompt and let the AI generate text.")
```

This provides a simple introduction to the application.

---

### 4. Load the AI Model

The text-generation model is loaded using:

```python
@st.cache_resource
def load_model():
    generator = pipeline(
        "text-generation",
        model="Qwen/Qwen3.8-2.4T-A95B"
    )
    return generator
```

The `pipeline()` function creates a text-generation pipeline.

The model is loaded only once using:

```python
@st.cache_resource
```

This helps avoid repeatedly loading the model every time the Streamlit application reruns.

---

## 📝 User Prompt

The application provides a text area:

```python
prompt = st.text_area(
    "Enter your prompt:",
    placeholder="Example: Artificial Intelligence is"
)
```

The user can enter any prompt they want the AI to continue.

### Example

```text
Artificial Intelligence is
```

or

```text
Once upon a time
```

---

## 🎛️ Generation Settings

The application provides two controls.

### Maximum Length

```python
max_length = st.slider(
    "Maximum length",
    min_value=30,
    max_value=200,
    value=100
)
```

This allows the user to control the maximum number of tokens/sequence length used for generation.

The available range is:

```text
30 → 200
```

The default value is:

```text
100
```

---

### Temperature

```python
temperature = st.slider(
    "Temperature",
    min_value=0.1,
    max_value=1.5,
    value=0.7
)
```

Temperature controls the randomness of the generated text.

Generally:

| Temperature | Effect                          |
| ----------- | ------------------------------- |
| Lower       | More predictable output         |
| Medium      | Balanced output                 |
| Higher      | More varied and creative output |

The application allows values from:

```text
0.1 → 1.5
```

with a default value of:

```text
0.7
```

---

## 🚀 Generate Text

When the user clicks:

```text
Generate Text 🚀
```

the application checks whether the prompt is empty.

```python
if prompt.strip() == "":
    st.warning("Please enter a prompt.")
```

If the prompt is not empty, the model generates text.

```python
result = generator(
    prompt,
    max_length=max_length,
    temperature=temperature,
    do_sample=True,
    num_return_sequences=1
)
```

### Parameters Used

**`max_length`**

Controls the maximum sequence length.

**`temperature`**

Controls the randomness of the generated output.

**`do_sample=True`**

Enables sampling so that the model can generate varied outputs.

**`num_return_sequences=1`**

Generates one text sequence.

---

## 📤 Displaying the Output

The generated text is extracted using:

```python
generated_text = result[0]["generated_text"]
```

The application then displays:

```python
st.subheader("Generated Text")
st.write(generated_text)
```

The generated content appears directly on the Streamlit page.

---

## 🖥️ Application Flow

```text
             TEXT GENERATION APP
                     │
                     ▼
             Enter Your Prompt
                     │
                     ▼
          Set Maximum Length
                     │
                     ▼
             Set Temperature
                     │
                     ▼
            Generate Text 🚀
                     │
                     ▼
             Qwen AI Model
                     │
                     ▼
            Generated Text
```

---

## 📂 Project Structure

```text
text-generation/
│
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```

### File Description

| File               | Description                |
| ------------------ | -------------------------- |
| `app.py`           | Main Streamlit application |
| `requirements.txt` | Required Python libraries  |
| `README.md`        | Project documentation      |
| `.gitignore`       | Files excluded from Git    |

---

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/text-generation.git
```

### 2. Open the Project

```bash
cd text-generation
```

### 3. Install Dependencies

```bash
pip install streamlit transformers torch
```

Or install from the requirements file:

```bash
pip install -r requirements.txt
```

---

## 📄 Requirements

A basic `requirements.txt` file can contain:

```text
streamlit
transformers
torch
```

---

## ▶️ Run the Application

Start the Streamlit application using:

```bash
streamlit run app.py
```

The application will open in your browser.

---

## 🧪 Example

### Input

```text
Artificial Intelligence is
```

### Settings

```text
Maximum length: 100
Temperature: 0.7
```

### Output

The AI model generates a continuation based on the given prompt.

Example:

```text
Artificial Intelligence is transforming the way people
work, learn, communicate, and solve complex problems.
```

*The exact output can vary because text generation uses sampling.*

---

## ✨ Features

* 🤖 AI-powered text generation
* 📝 Custom user prompts
* 🎛️ Adjustable maximum length
* 🌡️ Adjustable temperature
* 🚀 One-click text generation
* 💻 Simple Streamlit interface
* 🤗 Hugging Face Transformers integration
* 🧠 Pre-trained Qwen model
* ⚡ Model caching using Streamlit

---

## 📚 Concepts Learned

This project demonstrates the following concepts:

### 1. Natural Language Processing

NLP enables computers to understand and generate human language.

### 2. Large Language Models

Large language models can generate text based on patterns learned from large amounts of training data.

### 3. Text Generation

Text generation is the process of producing new text based on an input prompt.

### 4. Hugging Face Transformers

The Transformers library provides access to many pre-trained AI models.

### 5. Streamlit

Streamlit makes it possible to create interactive Python-based web applications.

### 6. Prompt-Based Generation

The user's input acts as a prompt that guides the model's generated output.

---

## ⚠️ Limitations

The generated text may:

* Contain incorrect information
* Repeat certain phrases
* Produce unexpected results
* Depend heavily on the input prompt
* Change when generation settings are modified
* Require significant computing resources depending on the model

AI-generated content should therefore be reviewed before being used for important or factual purposes.

---

## 🚀 Future Improvements

The project can be extended with:

* 📋 Copy generated text button
* 🗑️ Clear prompt button
* 📥 Download generated text
* 📊 Word/token counter
* 💬 Chat-style interface
* 📝 Multiple text-generation modes
* 🔄 Generate multiple responses
* 💾 Save previous generations
* 🎨 Improved Streamlit interface
* 🌐 Deployment using Streamlit Community Cloud
* ⚙️ Additional generation parameters such as `top
