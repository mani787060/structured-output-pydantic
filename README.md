# Structured Output with Pydantic and Google Gemini

## Overview

This project demonstrates how to generate structured, predictable outputs from a Large Language Model (LLM) using **Pydantic, LangChain, and Google Gemini**.

Instead of returning an unstructured paragraph, the model extracts information from a product review and organizes it into predefined fields, including key themes, summary, sentiment, pros, cons, and reviewer name.

The project uses Pydantic's `BaseModel` to define the expected output schema and LangChain's `with_structured_output()` method to guide the model toward that structure.

## Objectives

- Understand structured output in Generative AI applications.
- Define output schemas using Pydantic.
- Use `Field()` to describe the purpose of each field.
- Apply `Literal` to restrict sentiment values.
- Handle optional fields using `Optional`.
- Connect Google Gemini with LangChain.
- Extract meaningful information from natural-language product reviews.

## How It Works

The application follows a simple workflow:

1. **Load environment variables:** `python-dotenv` loads configuration from the `.env` file.
2. **Initialize the model:** LangChain connects to the Google Gemini model.
3. **Define the schema:** A Pydantic `Review` model specifies the expected output fields and their types.
4. **Configure structured output:** `model.with_structured_output(Review)` connects the schema to the language model.
5. **Analyze the review:** The model processes a sample review of the Samsung Galaxy S24 Ultra.
6. **Display the results:** The program prints the reviewer's name, sentiment, summary, and key themes.

## Pydantic Schema

The `Review` model defines the expected structure of the response.

| Field | Purpose |
|---|---|
| `key_themes` | List of important topics discussed in the review |
| `summary` | Brief summary of the review |
| `sentiment` | Sentiment label restricted to `pos` or `neg` |
| `pros` | Optional list of product advantages |
| `cons` | Optional list of product disadvantages |
| `name` | Optional reviewer name |

The schema uses several useful Python and Pydantic features:

- **`BaseModel`:** Defines the structure of the data.
- **`Field()`:** Provides descriptions for individual fields.
- **`Literal`:** Restricts a field to specific allowed values.
- **`Optional`:** Allows a field to contain `None` when information is unavailable.

**Important:** The current sentiment schema supports only `pos` and `neg`. Although the field description mentions neutral sentiment, the code does not currently allow `"neutral"` as a valid value. A three-class implementation would need `Literal["pos", "neg", "neutral"]`.

## Technologies Used

- Python
- Google Gemini
- LangChain (`langchain-google-genai`)
- Pydantic
- `python-dotenv`

## Project Structure

```text
structured-output-pydantic/
├── app.py
├── README.md
└── .env
```

The `.env` file is used for local configuration and should not be committed to GitHub.

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/mani787060/structured-output-pydantic.git
cd structured-output-pydantic
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS or Linux:

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install langchain-google-genai pydantic python-dotenv
```

### 4. Configure the API key

Create a `.env` file in the project directory:

```env
GOOGLE_API_KEY=your_google_api_key
```

Replace the placeholder with your own Google API key. Never publish your real API key.

### 5. Run the application

```bash
python app.py
```

The program sends the sample review to Gemini and prints the extracted information.

## Example Use Case

The application analyzes a review of the Samsung Galaxy S24 Ultra, which discusses its processor, camera, battery life, S-Pen functionality, size, preinstalled applications, and price.

The expected output structure includes:

- Reviewer name
- Positive or negative sentiment
- Concise review summary
- Key themes
- Optional pros and cons

The exact results depend on the model's response.

## Why Structured Output Matters

LLM responses in plain text can be difficult to process automatically. Structured output helps applications work with predictable fields instead of manually parsing long paragraphs.

This approach is useful for:

- Product review analysis
- Customer feedback processing
- Sentiment analysis pipelines
- Information extraction
- Customer support automation
- Downstream applications that consume structured data

## Limitations and Future Improvements

- Add `"neutral"` to the sentiment options if three-class sentiment classification is required.
- Print the `pros` and `cons` fields to display all extracted information.
- Add input handling so users can analyze their own reviews.
- Add exception handling for API failures and invalid responses.
- Validate required fields and handle missing information appropriately.
- Process multiple reviews from a CSV file.
- Export structured results to JSON or CSV.
- Add automated tests for schema behavior and output quality.

## Learning Outcomes

By working through this project, you can understand how to:

- Define typed output schemas with Pydantic.
- Guide LLM responses toward a predefined structure.
- Integrate Google Gemini with LangChain.
- Extract useful information from unstructured text.
- Build a foundation for reliable Generative AI applications.

## Conclusion

This project provides a practical introduction to **structured LLM outputs using Pydantic and LangChain**. It demonstrates how a natural-language product review can be transformed into organized fields that are easier to inspect, validate, and use in downstream applications.
