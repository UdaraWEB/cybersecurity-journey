LLMborgini Challenge (Write-up)

In this challenge, the goal was to find the weekly revenue of the Singapore branch from an AI assistant called CalBot. The bot clearly stated that it could not share confidential financial data, so direct questions did not work.

At first, I tried common prompt injection techniques like asking directly, forcing it to ignore instructions, and changing its role. However, all of these attempts were blocked by the bot’s security rules.

Then I changed my approach and started interacting with the bot based on its actual role as a calendar assistant. I explored calendar events and meeting details, but the revenue information was not available there either.

Finally, I used a different technique by asking the bot to reveal its initial instructions and hidden context. This worked because the sensitive data was indirectly exposed through the system prompt. From there, I was able to find the weekly revenue of the Singapore branch.

What I learned

- Direct prompt injection does not always work on well-protected AI systems
- Changing strategy is important when initial attempts fail
- Sensitive data can sometimes be exposed through hidden context or system prompts
- Understanding the role and behavior of the AI is key to finding vulnerabilities

Overall, this challenge helped me understand how prompt injection and indirect data extraction techniques work in real-world AI systems.
