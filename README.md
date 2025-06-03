# MotivAI — Instant Motivation from Legendary Voices

MotivAI is a raw, powerful AI-driven prompt engine that transforms emotional user input into authentic motivational replies—delivered in the voice of legendary figures like David Goggins, Jocko Willink, Kobe Bryant, and more.

## ⚡ What It Does

MotivAI takes:

👤 The user's emotional message

🎙 A selected motivational persona

🎯 A desired tone (raw, comforting, bold, etc.)

#### And instantly generates:

-  A real or inspired quote from that persona

- A personalized, powerful, 5–6 line motivational message

- In that persona’s exact voice and style

## 🎯 Why Use It

This isn’t generic pep talk. It’s:

🔥 Bold, emotional, and raw

🧠 Context-aware and tailored to the user

🗣 Authentically voiced to match real motivational legends

⚙️ Easy to integrate into chatbots, coaching tools, or mental health apps

## Working (Ai Agents) 
```
This automation handles incoming user emotion + persona selection and returns a raw, persona-voiced motivational message. It uses the following modules:

🔴 Webhooks (Trigger)
Receives incoming POST request containing:

User emotional input

Selected persona

Desired tone (e.g., comforting, raw, tough love)

🔵 Google Gemini AI - Create a Completion (Module 1)

Analyzes the user’s emotional message

Extracts intent, emotion, and keywords

🔵 Google Gemini AI - Create a Completion (Module 2)

Selects or confirms the correct motivational persona and tone

Can override defaults for better alignment

🔵 Google Gemini AI - Create a Completion (Module 3)

Retrieves or generates a real or inspired quote in the voice of the persona

🔵 Google Gemini AI - Create a Completion (Module 4)

Crafts a 5–6 line, personalized motivational reply

Matches the persona’s tone, language, and intensity

🔴 Webhooks (Response)

Sends back the final output:

"As [Persona] once said, '[Quote].'
[Line 1]
[Line 2]
..."
```
![image](https://github.com/user-attachments/assets/4c3999bc-a290-4073-8166-0b44e7f843fb)

## Video: 
https://drive.google.com/file/d/1e18n_Dxlqx5hqEXvXz_1-r0mx-v78Sor/view?usp=sharing


## 🛠 Example Prompt
```
Input:

I'm tired of trying so hard and getting nowhere. It feels like I'm failing every day.

Persona:

David Goggins

Tone:

Raw and real

Output:

As David Goggins once said, "You are stopping you. You’re giving up instead of getting hard."
You’re not tired—you’re untested.
That voice in your head is lying.
You’ve got more in the tank, but you’re choosing comfort.
Pain unlocks the next level.
Get up. Go again. Stay hard.
```

## 💬 Persona Library (Sample)

David Goggins

Jocko Willink

Kobe Bryant

Angela Duckworth

Tony Robbins

Eric Thomas

Chris Williamson

Marie Forleo

...and more coming!



## My Twitter: 
https://x.com/codezxs
![image](https://github.com/user-attachments/assets/f04db95a-6b21-4c59-ad1f-72de11067d19)

## License

MIT License. Use it. Remix it. Spread the motivation.

[MIT](https://choosealicense.com/licenses/mit/)
