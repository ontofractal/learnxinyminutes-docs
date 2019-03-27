---
language: Sophia
filename: learnSophia.aes
contributors:
  - ["ontofractal", "http://ontofractal.com"]
---

Sophia is a strongly-typed ML-style functional language developed for writing smart contracts for the Aeternity blockchain. Sophia design choices were based on the need to restrict mutable state, reduce number of side effects, better handling of concurrency, and ease of debugging and testing.

Aeternity VM is built with Erlang programming language and Sophia also shares a lot of qualities with Erlang and Erlang VM.

---

## Intro

Sophia is not a general purpose programming language and is designed only for writing smart contracts.

The primary unit of code organization in Sophia is a static smart contract. Sophia does not have modules. 

Contracts are similar to Erlang/Elixir GenServers and somewhat similar to classes in object oriented languages. Sophia contracts support local state and inheritance. Contract instances can exist only on the blockchain (whether mainnet, testnet or simulated) after the successful execution of the "create contract" transaction.

Contracts can be:
 - abstract 
    - can't be deployed to the blockchain
    - no types or functions definitions) 
 - concrete 
    - all types and functions are defined
    - only concrete contracts can be instantiated and deployed to the blockchain

### Mutable state

Just like with processes and GenServers in Erlang/Elixir, contracts in Sophia have local state associated with each contract instance.

- Each contract defines a type `state` encapsulating its mutable state.
- The initial state of a contract is computed by the contract's `init`
  function. The `init` function is *pure* and returns the initial state as its
  return value. At contract creation time, the `init` function is executed and
  its result is stored as the contract state.
- The value of the state is accessible from inside the contract
  through an implicitly bound variable `state`.
- State updates are performed by calling a function `put : state => ()`.
- Aside from the `put` function (and similar functions for transactions
  and events), the language is purely functional.
- Functions modifying the state need to be annotated with the `stateful` keyword.




