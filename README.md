# openai-gpt-google-sheets-integration
OpenAI API Integration with Google Sheets (Apps Script)
This project integrates OpenAI's API into Google Sheets using Google Apps Script. It securely stores API credentials and allows for programmatic access to the OpenAI completions endpoint from your spreadsheet.
________________________________________
🔐 API Key Security
Your OpenAI API key is securely stored in script properties — it is not hardcoded in the main logic or exposed in GitHub.
________________________________________
📁 Files and Structure
•	Code.gs: Initializes and stores API key and endpoint.
•	GPT_TRANSLATE.gs: Logic for translating cell contents.
•	GPT_SUMMARIZE.gs: Summarizes selected content.
•	GPT_FORMAT.gs: Formats content using GPT.
•	GPT_EXTRACT.gs: Extracts structured info from text.
•	GPT_CLASSIFY.gs: Classifies text using OpenAI.
•	GPT.gs.gs: Utility functions.
________________________________________
🔧 Setup Instructions
1. Link to Google Sheet
•	Open Google Sheets
•	Go to Extensions > Apps Script
•	Paste your code or import the content from this repository
2. Store API Key Securely
Run the following function once from the Apps Script editor:

function storeApiKeyAndConfig() {
  var apiKey = "YOUR_API_KEY"; // Replace with your actual API key
  PropertiesService.getScriptProperties().setProperty('OPENAI_API_KEY', apiKey);
  PropertiesService.getScriptProperties().setProperty('OPENAI_API_ENDPOINT', 'https://api.openai.com/v1/completions');
}
3. Verify Stored Values (Optional)
Run this to confirm your credentials were saved:

function getStoredValues() {
  var apiKey = PropertiesService.getScriptProperties().getProperty('OPENAI_API_KEY');
  var apiEndpoint = PropertiesService.getScriptProperties().getProperty('OPENAI_API_ENDPOINT');
  Logger.log('API Key: ' + apiKey);
  Logger.log('API Endpoint: ' + apiEndpoint);
}
4. Use Other GPT Functions
You can create custom functions like:
javascript
CopyEdit
function callOpenAI(prompt) {
  var apiKey = PropertiesService.getScriptProperties().getProperty('OPENAI_API_KEY');
  var endpoint = PropertiesService.getScriptProperties().getProperty('OPENAI_API_ENDPOINT');

  var payload = {
    model: "text-davinci-003",
    prompt: prompt,
    max_tokens: 150,
    temperature: 0.7
  };

  var options = {
    method: "post",
    contentType: "application/json",
    headers: {
      Authorization: "Bearer " + apiKey
    },
    payload: JSON.stringify(payload)
  };

  var response = UrlFetchApp.fetch(endpoint, options);
  var json = JSON.parse(response.getContentText());
  return json.choices[0].text.trim();
}

⚠️ Never Commit API Keys
Always store your key in PropertiesService. Never hardcode or push it to GitHub.
📌 Requirements
•	Google Workspace (Gmail/Sheets)
•	OpenAI API Key (Get it from https://platform.openai.com)
________________________________________
✅ License
MIT
MIT License
Copyright (c) 2025 Alireza Minagar
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell      copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:                        

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.                                

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE  SOFTWARE.

📂 Repository
GitHub: openai-gpt-google-sheets-integration
You can clone it using:
git clone https://github.com/aliminagar/openai-gpt-google-sheets-integration.git

