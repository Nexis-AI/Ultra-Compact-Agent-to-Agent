 _   _  _____ __   __ _____ 
| \ | |/ ____|\ \ / // ____|
|  \| | (___   \ V /| (___  
| . ` |\___ \   > <  \___ \ 
| |\  |____) | / . \ ____) |
|_| \_|_____/ /_/ \_\_____/   

# Compact AI Interchange Protocol (Prototype)

<p align="center">
  <b>CAIP · Compact AI Interchange Protocol</b><br/>
  <a href="LICENSE"><img alt="MIT License" src="https://img.shields.io/badge/license-MIT-blue.svg"/></a>
  <img alt="Python 3.9+" src="https://img.shields.io/badge/python-3.9%2B-yellow.svg"/>
  <img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg"/>
</p>



⸻

✨ Overview

CAIP is a lightweight, AI-native messaging protocol that delivers the same semantic punch in 50–70 % fewer tokens. By combining symbolic syntax, abbreviations, and a structured envelope, it trims context-window overhead for LLMs—unlocking faster, cheaper agent-to-agent chatter.

Prototype status: minimal but functional. Perfect for experimentation; not production-hardened (yet).

⸻

📑 Table of Contents
	•	Overview
	•	How It Works
	•	Installation
	•	Usage
	•	Examples
	•	Extending the Prototype
	•	Contributing
	•	License
	•	Acknowledgments

⸻

⚙️ How It Works

sequenceDiagram
  participant Sender as Sender Agent
  participant Net as Network
  participant Receiver as Receiver Agent

  Sender->>Sender: generate_caip()
  Sender->>Net: transmit compact msg
  Net-->>Receiver: deliver msg
  Receiver->>Receiver: parse_caip()
  Receiver-->>Sender: optional response

The sender encodes a compact message, the network passes it along, and the receiver expands it back—all while minimising tokens inside the LLM context.

⸻

📦 Installation

CAIP is dependency-free—pure Python.

# 1. Clone
git clone https://github.com/YOUR_USERNAME/caip-prototype.git
cd caip-prototype

# 2. (Optional) Isolate
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

The core lives in caip.py; import it or copy-paste into your own project.

⸻

📝 Usage

from caip import generate_caip, parse_caip, SYMBOLS

# build a message
msg = generate_caip(
    sender="A",
    receiver="B",
    msg_type="query",
    body=f"inv(X,Y) {SYMBOLS['ACTION']}chk<100{SYMBOLS['IMPLIES']}ord(Z)"
         f"{SYMBOLS['AND']}ntfy(A)",
    priority="high",
    context="#SUM:prevDemand",
    negate=f"low{SYMBOLS['IMPLIES']}end"
)
print(msg)

# decode it
print(parse_caip(msg))

API surface

Function	Purpose
generate_caip()	Build a CAIP string from components.
parse_caip()	Reverse the process—returns a dict.


⸻

🔍 Examples

<details>
<summary>Inventory Query</summary>


◯A→◯B | Q:inv(X,Y) ●chk<100→ord(Z)∧ntfy(A) | *high | C:#SUM:prevDemand | !low→end

{
  "sender": "A",
  "receiver": "B",
  "type": "query",
  "body": "inv(X,Y) [ACTION]chk<100[IMPLIES]ord(Z)[AND]ntfy(A)",
  "priority": "high",
  "context": "#SUM:prevDemand",
  "negate": "low[IMPLIES]end"
}

</details>


<details>
<summary>Response</summary>


◯B→◯A | R:inv=80 ●ord(Z) | C:#REF:msg1∧#SUM:cost<10%

</details>


<details>
<summary>Handshake / Init</summary>


◯A→◯B | INIT:SEC:enc SHR:C001 ●init

</details>



⸻

🚀 Extending the Prototype

Idea	What to do
✨ More symbols	Add to SYMBOLS / ABBREVS.
📉 Dynamic compression	Plug in zlib (or similar) for summaries.
🤖 LLM integration	Prompt: “Convert natural text → CAIP body”.
🛡️ Validation	Escape delimiters, verify envelopes.
🤝 Multi-agent demo	Wire two toy agents with WebSockets.


⸻

🤝 Contributing

Pull requests are very welcome!

git checkout -b feature/AmazingFeature
git commit -m "Add AmazingFeature"
git push origin feature/AmazingFeature

Then open a PR. For big changes, start with an issue.

⸻

📝 License

This project is licensed under the MIT License—see LICENSE.

⸻

🙏 Acknowledgments
	•	Research on prompt compression, symbolic languages, and AI-agent protocols.
	•	Prototype built with a little help from Grok by xAI.

Have ideas or feedback?
Open an issue  •  Start a discussion  •  Join the conversation

⸻




