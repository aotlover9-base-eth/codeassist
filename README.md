# Beginner-Friendly Guide: Run Gensyn CodeAssist on a VPS

A fast, simple guide for setting up Gensyn CodeAssist on any cheap VPS—even if you’re new to this!

***

## Prerequisites
- VPS Specs: 4 CPU, 8 GB RAM, 32 GB Swap (minimum recommended)
- SSH knowledge: Be able to connect to your VPS from your PC
- Hugging Face account/token: Register at https://huggingface.co and create an access token with Write role

***

## Step 1: Connect to Your VPS
Open terminal or command prompt on your PC and run:
```bash
ssh root@YOUR_VPS_IP
```
(Replace YOUR_VPS_IP with your VPS’s actual IP)

***

## Step 2: Start a Screen Session
Keeps your process alive even if you disconnect:
```bash
screen -S codeassist
```

***

## Step 3: Install UV (Python Packager)
Install UV and reload bash:
```bash
curl -LsSf https://astral.sh/uv/install.sh | bash
source ~/.bashrc
```

***

## Step 4: Clone the CodeAssist Repository
```bash
git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
```

***

## Step 5: Change Default Port (3000 → 3001)

Edit compose.yml:
```bash
nano compose.yml
```

Find:
```
3000:3000
```

Change to:
```
3001:3000
```

Save: Ctrl+X, then Y, then Enter

Edit run.py:
```bash
nano run.py
```

Find:
```
"3000/tcp": ,
```

Change to:
```
"3000/tcp": 3001,
```

Save and exit

***

## Step 6: Run CodeAssist
```bash
uv run run.py
```

- Paste your Hugging Face Write token when prompted (it won’t appear as you type)
- Program will start running

***

## Step 7: Create an SSH Tunnel (From Your PC)
On your PC, open a new terminal window:
```bash
ssh -L 3001:localhost:3001 -L 8000:localhost:8000 -L 8008:localhost:8008 root@YOUR_VPS_IP
```

- Replace YOUR_VPS_IP with your VPS IP  
- Accept if prompted (yes), enter password  
- Keep this terminal open

***

## Step 8: Open CodeAssist Web Interface
Open in your browser:
```
http://localhost:3001
```
You should now see CodeAssist’s interface.

***

## Step 9: Use and Train CodeAssist
- Solve multiple coding problems/tasks
- When finished:
  - In your VPS terminal, stop the program (`Ctrl + C` — or use `kill` if needed)
- Training starts automatically; wait for it to finish

***

## Step 10: Check Your Hugging Face Account
- Log in to https://huggingface.co
- Go to your profile — your trained model should appear there

***

## Bonus: Detach/Resume Your Screen Session
Detach:
```
Ctrl + A, then D
```

Reattach:
```bash
screen -r codeassist
```

***

For any problem or support contact me on telegram @aotlover19
