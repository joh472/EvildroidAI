

## EvildroidAI Overview

EvildroidAI are autonomous AI agents that act just like real hackers - they run your code dynamically, find vulnerabilities, and validate them through actual proof-of-concepts. Built for developers and security teams who need fast, accurate security testing without the overhead of manual pentesting or the false positives of static analysis tools.

**Key Capabilities:**

- **Full hacker toolkit** out of the box
- **Teams of agents** that collaborate and scale
- **Real validation** with PoCs, not false positives
- **Developer‑first** CLI with actionable reports
- **Auto‑fix & reporting** to accelerate remediation


<br>


<div align="center">
  <a href="https://strix.ai">
    <img src=".github/screenshot.png" alt="Strix Demo" width="1000" style="border-radius: 16px;">
  </a>
</div>


## Use Cases

- **Application Security Testing** - Detect and validate critical vulnerabilities in your applications
- **Rapid Penetration Testing** - Get penetration tests done in hours, not weeks, with compliance reports
- **Bug Bounty Automation** - Automate bug bounty research and generate PoCs for faster reporting
- **CI/CD Integration** - Run tests in CI/CD to block vulnerabilities before reaching production



### Installation & First Scan

```bash
# Install Strix
curl -sSL https://EvildroidAI.ai/install | bash

# Configure your AI provider
export STRIX_LLM="openai/gpt-5"  # or "strix/gpt-5" via Strix Router (https://models.strix.ai)
export LLM_API_KEY="your-api-key"

# Run your first security assessment
EvildroidAI --target ./app-directory
```

> [!NOTE]
> First run automatically pulls the sandbox Docker image. Results are saved to `strix_runs/<run-name>`

---


---


### Agentic Security Tools

EvildroidAI agents come equipped with a comprehensive security testing toolkit:

- **Full HTTP Proxy** - Full request/response manipulation and analysis
- **Browser Automation** - Multi-tab browser for testing of XSS, CSRF, auth flows
- **Terminal Environments** - Interactive shells for command execution and testing
- **Python Runtime** - Custom exploit development and validation
- **Reconnaissance** - Automated OSINT and attack surface mapping
- **Code Analysis** - Static and dynamic analysis capabilities
- **Knowledge Management** - Structured findings and attack documentation

### Comprehensive Vulnerability Detection
EvildroidAI can identify and validate a wide range of security vulnerabilities:

- **Access Control** - IDOR, privilege escalation, auth bypass
- **Injection Attacks** - SQL, NoSQL, command injection
- **Server-Side** - SSRF, XXE, deserialization flaws
- **Client-Side** - XSS, prototype pollution, DOM vulnerabilities
- **Business Logic** - Race conditions, workflow manipulation
- **Authentication** - JWT vulnerabilities, session management
- **Infrastructure** - Misconfigurations, exposed services

### Graph of Agents

Advanced multi-agent orchestration for comprehensive security testing:

- **Distributed Workflows** - Specialized agents for different attacks and assets
- **Scalable Testing** - Parallel execution for fast comprehensive coverage
- **Dynamic Coordination** - Agents collaborate and share discoveries

---

## Usage Examples

### Basic Usage

```bash
# Scan a local codebase
EvildroidAI --target ./app-directory

# Security review of a GitHub repository
EvildroidAI --target https://github.com/org/repo

# Black-box web application assessment
EvildroidAI --target https://your-app.com
```

### Advanced Testing Scenarios

```bash
# Grey-box authenticated testing
EvildroidAI --target https://your-app.com --instruction "Perform authenticated testing using credentials: user:pass"

# Multi-target testing (source code + deployed app)
EvildroidAI -t https://github.com/org/app -t https://your-app.com

# Focused testing with custom instructions
EvildroidAI --target api.your-app.com --instruction "Focus on business logic flaws and IDOR vulnerabilities"

# Provide detailed instructions through file (e.g., rules of engagement, scope, exclusions)
EvildroidAI --target api.your-app.com --instruction-file ./instruction.md
```

### Headless Mode

Run EvildroidAI programmatically without interactive UI using the `-n/--non-interactive` flag—perfect for servers and automated jobs. The CLI prints real-time vulnerability findings, and the final report before exiting. Exits with non-zero code when vulnerabilities are found.

```bash
EvildroidAI -n --target https://your-app.com
```

### CI/CD (GitHub Actions)

EvildroidAI can be added to your pipeline to run a security test on pull requests with a lightweight GitHub Actions workflow:

```yaml
name: EvildroidAI-penetration-test

on:
  pull_request:

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6

      - name: Install EvildroidAI
        run: curl -sSL https://EvildroidAI.ai/install | bash

      - name: Run EvildroidAI
        env:
          STRIX_LLM: ${{ secrets.STRIX_LLM }}
          LLM_API_KEY: ${{ secrets.LLM_API_KEY }}

        run: EvildroidAI -n -t ./ --scan-mode quick
```

### Configuration

```bash
export STRIX_LLM="openai/gpt-5"
export LLM_API_KEY="your-api-key"

# Optional
export LLM_API_BASE="your-api-base-url"  # if using a local model, e.g. Ollama, LMStudio
export PERPLEXITY_API_KEY="your-api-key"  # for search capabilities
export STRIX_REASONING_EFFORT="high"  # control thinking effort (default: high, quick scan: medium)
```

> [!NOTE]
> EvildroidAI automatically saves your configuration to `~/.EvildroidAI/cli-config.json`, so you don't have to re-enter it on every run.

**Recommended models for best results:**

- [OpenAI GPT-5](https://openai.com/api/) — `openai/gpt-5`
- [Anthropic Claude Sonnet 4.6](https://claude.com/platform/api) — `anthropic/claude-sonnet-4-6`
- [Google Gemini 3 Pro Preview](https://cloud.google.com/vertex-ai) — `vertex_ai/gemini-3-pro-preview`

See the [LLM Providers documentation](https://docs.strix.ai/llm-providers/overview) for all supported providers including Vertex AI, Bedrock, Azure, and local models.



> [!WARNING]
> Only test apps you own or have permission to test. You are responsible for using Strix ethically and legally.

</div>
