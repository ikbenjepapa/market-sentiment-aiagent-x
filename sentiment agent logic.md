# Agent Overlook

## **Requirement**
1. required api [twitter, openai]
2. python script
3. data folder [data/sentiment/data.csv]
4. API access [twitter dev account]
5. Dependencies [torch, transformers, pandas, dotenv, asyncio]

![](agentprofile.jpg)


This project uses a sentiment analysis model to evaluate the public sentiment around cryptocurrencies like **Solana**, **Bitcoin**, and **Ethereum** by analyzing tweets. The agent fetches tweets for these tokens, processes them through a sentiment analysis model, and outputs the results with optional voice announcements.

## How Sentiment is Analyzed
1. **Fetch Tweets**:
   - The agent collects tweets related to a specific cryptocurrency (e.g., "Bitcoin") from Twitter.
   - Unwanted content (e.g., tweets with links, ads) is filtered out using a predefined ignore list.

2. **Tokenize Tweets**:
   - Tweets are broken into smaller components (tokens) that can be processed by the sentiment analysis model.

3. **Sentiment Prediction**:
   - The **`bertweet-base-sentiment-analysis`** model predicts the sentiment of each tweet:
     - **Negative** (e.g., criticism).
     - **Neutral** (e.g., factual or balanced).
     - **Positive** (e.g., optimism).

4. **Score Calculation**:
   - The model assigns probabilities to each sentiment (Negative, Neutral, Positive).
   - A **sentiment score** is calculated:
     ```
     Sentiment Score = Positive Probability - Negative Probability
     ```
   - Scores range from `-1` (completely negative) to `1` (completely positive).

5. **Batch Aggregation**:
   - The sentiment scores for all tweets in a batch are averaged to determine the overall sentiment for the cryptocurrency.

6. **Output Results**:
   - Results are printed to the console, saved to a CSV file (`data/sentiment_history.csv`), and optionally announced using text-to-speech.

## Key Features
- **Sentiment Tracking**:
  - Monitors sentiment trends for specified tokens.
  - Saves results for long-term analysis.
- **Voice Announcements**:
  - Announces results using a text-to-speech engine.
  - Highlights significant sentiment shifts.
- **12-Hour Interval**:
  - Runs sentiment analysis every 12 hours.

## Example Output
```plaintext
Sentiment for solana: positive (0.04)
Sentiment for bitcoin: positive (0.05)
Sentiment for ethereum: positive (0.09)
Next run at 2025-01-19 01:08:11
```

## How to Use
1. **Install Dependencies**:
   ```bash
   pip install torch transformers pandas python-dotenv pyttsx3
   ```
2. **Set Up API Keys**:
   - Store your API keys in a `.env` file (if integrating with Twitter API in the future).

3. **Run the Script**:
   ```bash
   python sentiment_agent.py
   ```

## How the Agent Works (Simplified)
1. **Fetch Tweets**:
   Collects tweets about specific cryptocurrencies.
2. **Analyze Sentiment**:
   Calculates how positive or negative the tweets are using probabilities.
3. **Save Results**:
   Stores sentiment scores in a CSV file.
4. **Repeat**:
   Runs every 12 hours to update the sentiment trend.

---

## Contact
For any questions or improvements, feel free to submit an issue or pull request on GitHub!







