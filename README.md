# Go-like-Elixir — Elixir Syntax, Go-style Execution Model

This project experiments with **Elixir-style syntax** combined with a **Go-style execution model**:
lightweight processes, message passing, and concurrency — but without the BEAM VM.

Surface syntax: **Elixir-like**  
Execution semantics: **Go-like goroutine model**  
Backend: meaning-level engine (no BEAM, no OTP)

Go + Elixir mashed into one experimental language prototype.

---

## 🎯 Goal

- Use Elixir-like syntax (pipe operators, pattern-like constructs, clean functional style)
- Replace BEAM VM with a **Go-like scheduler**
- Lightweight processes (goroutine-like)
- Message passing (chan/send semantics)
- No OTP, no BEAM bytecode, no Erlang VM
- Meaning-level runtime implemented manually

---

## 🌀 Concept Overview

### ✦ Elixir syntax (surface)
```elixir
x = 10
y = x |> add(5)
spawn fn -> IO.puts(y) end



✦ Go-style semantics




spawn → goroutine-like execution


message channels → Go-like chan<T>


scheduler → cooperative or small work-stealing loop


no actor mailboxes, no OTP




✦ Meaning IR example


bind x imm 10
call add(x, 5) → y
spawn(print(y))




🔧 Pipeline


[Elixir-Like Source]
      ↓
 Lexer (Rust or Go)
      ↓
 Parser → AST
      ↓
 Semantic Engine (Go-style concurrency rules)
      ↓
 Meaning IR
      ↓
 (optional) backend: NASM / C / interpreter (future)



(Current repo likely starts small with IR only.)



🛠 Feature Targets


✔ Elixir-like features




|> pipeline operator


simple pattern-like bindings


clean expression-based design




✔ Go-like runtime




goroutine scheduler


message channel abstraction


non-VM concurrency




✔ No BEAM / No OTP




Entire runtime is custom and lightweight


No .beam files


No Erlang semantics




✔ Fits Freeing-the-Lang ecosystem




experimental cross-language fusion


meaning-based runtime


simple extensible IR





📦 Example Program


Source:


def main do
  spawn fn ->
    IO.puts("Hello from process!")
  end

  chan = channel()
  send(chan, 42)
  val = recv(chan)
  IO.puts(val)
end



Meaning IR:


spawn(print("Hello from process!"))
chan = channel()
send(chan, 42)
val = recv(chan)
print(val)




🔮 Roadmap


Phase 1 — Frontend




tokenizer


minimal Elixir-like parser


basic expressions, pipelines




Phase 2 — Runtime Model




goroutine engine


simple channel implementation


select-like mechanism (optional)




Phase 3 — IR Completion




stable intermediate representation


transform rules for concurrency




Phase 4 — Output Backend (Optional)




NASM backend (Freeing-the-Lang style)


C backend (optional)


direct interpreter





📜 License


MIT License



---
