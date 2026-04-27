
AI Threat Modelling Assessment / LLM Security Room (Write-up)

In this room, I learned about three main LLM-related attacks: prompt injection, data leakage, and data poisoning.

First, prompt injection is when a user tries to trick the model by giving special instructions to ignore previous rules. This showed me how important the prompt layer is and how attacks can control the model’s behavior.

Second, data leakage is about the model exposing sensitive information. I learned that data can come from places like databases or retrieval systems, so those layers need protection.

Third, data poisoning is when incorrect or malicious data is added to the system, which causes the model to give wrong answers. This made me understand that controlling input data and storage is also very important.

Overall, I learned that LLM systems work like a chain (input → prompt → model → data), and attacks can happen at different points. Instead of guessing, I need to understand the attack flow and protect the correct layer.
