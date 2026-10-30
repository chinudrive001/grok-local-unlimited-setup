# Free & Unlimited Local Grok Setup

This repo gives you everything you need to run a Grok-style AI coding agent **completely free and with no rate limits** on your own machine.

It uses:
- Official open-source **Grok Build** (the agent / TUI / harness from xAI)
- Local models via Ollama / LM Studio / vLLM / llama.cpp (or any OpenAI-compatible endpoint)
- Optional: the open-source **Grok-1** weights if you have the hardware

Your forked copies:
- [grok-build](https://github.com/chinudrive001/grok-build) (will appear once the fork finishes)
- [grok-1](https://github.com/chinudrive001/grok-1) (will appear once the fork finishes)

---

## 1. Quick Start (Recommended – Local Models)

### Step 1 – Install a local model runner

**Ollama (easiest)**
```bash
# macOS / Linux
curl -fsSL https://ollama.com/install.sh | sh

# Then pull a strong model
ollama pull qwen2.5-coder:14b
# or
ollama pull llama3.2
# or any other model you like
```

**Alternatives**: LM Studio, llama.cpp, vLLM, etc.

### Step 2 – Get Grok Build

Once your fork is ready:
```bash
git clone https://github.com/chinudrive001/grok-build.git
cd grok-build
```

Or clone the official one:
```bash
git clone https://github.com/xai-org/grok-build.git
cd grok-build
```

Build it (requires Rust):
```bash
cargo build -p xai-grok-pager-bin --release
```

The binary will be at `target/release/xai-grok-pager`.

You can also use the official installer if you prefer the binary:
```bash
curl -fsSL https://x.ai/cli/install.sh | bash   # macOS / Linux
```

### Step 3 – Configure for local unlimited use

Create or edit `~/.grok/config.toml`:

```toml
[models]
default = "local-qwen"

[model.local-qwen]
model = "qwen2.5-coder:14b"          # change to whatever you pulled
base_url = "http://localhost:11434/v1"
name = "Local Qwen 2.5 Coder (Ollama)"
api_backend = "chat_completions"
context_window = 32768
# env_key is optional for local
```

### Step 4 – Run it

```bash
./target/release/xai-grok-pager
# or just `grok` if you installed the binary / aliased it
```

You now have a full Grok Build coding agent with **zero cost and no usage limits**.

---

## 2. Running the original Grok-1 (advanced)

Grok-1 is a 314B MoE model. You need multi-GPU hardware (lots of VRAM).

```bash
git clone https://github.com/chinudrive001/grok-1.git   # or xai-org/grok-1
cd grok-1

# Download weights (huge)
pip install huggingface_hub[hf_transfer]
huggingface-cli download xai-org/grok-1 --repo-type model --include ckpt-0/* --local-dir checkpoints --local-dir-use-symlinks False

pip install -r requirements.txt
python run.py
```

See the original repo README for full details.

---

## 3. Extra tips

- You can add multiple local models in `config.toml` and switch with `/model`.
- For even more free options, people sometimes put free-tier cloud providers (Groq, etc.) behind a local proxy, but pure local is the most unlimited & private.
- Grok Build supports skills, plugins, MCP servers, etc. – explore the source.

---

## Links

- Official Grok Build: https://github.com/xai-org/grok-build
- Official Grok-1: https://github.com/xai-org/grok-1
- Your forks will appear under https://github.com/chinudrive001

Enjoy unlimited local Grok-style AI.
