# Claude Code ↔ GPT(Codex) 연동 가이드

Claude Code 안에서 OpenAI Codex(GPT)를 MCP 서버로 불러 쓰는 방법입니다.

> **Claude에게:** 이 문서 링크를 받았다면 아래 단계를 순서대로 직접 실행하세요.
> 각 단계의 "확인" 명령이 실패하면 멈추고 사용자에게 원인을 알려주세요.
> 로그인(2단계)은 브라우저 인증이 필요하므로 사용자가 `! codex login` 으로 직접 실행하게 안내하세요.

## 준비물
- Node.js 18+ (`node -v`로 확인)
- Claude Code 설치됨
- ChatGPT 계정(Plus 이상 권장) 또는 OpenAI API 키

## 1. Codex CLI 설치
```bash
npm i -g @openai/codex
```
확인:
```bash
codex --version
```

## 2. Codex 로그인 (사용자가 직접)
```bash
codex login
```
- 브라우저가 열리면 ChatGPT 계정으로 로그인합니다.
- API 키를 쓰려면: `export OPENAI_API_KEY=sk-...` (Windows PowerShell: `$env:OPENAI_API_KEY="sk-..."`)

확인:
```bash
codex login status
```

## 3. Claude Code에 Codex MCP 서버 등록
```bash
claude mcp add codex -- codex mcp-server
```
확인:
```bash
claude mcp list
```
`codex`가 목록에 보이면 성공입니다. (Claude Code를 재시작해야 도구가 로드될 수 있음)

## 4. 사용하기
Claude Code에서 자연어로 시키면 됩니다.
- "이 변경사항을 Codex한테 코드 리뷰 시켜줘"
- "Codex에게 이 버그 원인을 물어보고 내 의견과 비교해줘"

MCP 없이 한 번만 쓰고 싶다면 Claude에게 Bash로 실행하게 해도 됩니다.
```bash
codex exec "이 저장소의 보안 문제를 점검해줘"
```

## 문제 해결
| 증상 | 해결 |
|---|---|
| `codex: command not found` | 터미널 재시작 또는 `npm config get prefix` 경로가 PATH에 있는지 확인 |
| `claude mcp list`에 안 보임 | 3단계 재실행 후 Claude Code 재시작 |
| 인증 오류 | `codex login` 재실행 |
| 등록 제거 | `claude mcp remove codex` |

## 주의
- Codex에 보내는 코드와 프롬프트는 OpenAI로 전송됩니다. 비밀키·개인정보가 든 파일은 넘기지 마세요.
- 사용량은 ChatGPT 요금제 한도 또는 API 과금에 따라 차감됩니다.
