# call

Category
Developer Tooling
Details

Stylus aims to interoperate with existing Solidity contracts, but today some common interface patterns, especially overloaded functions, inherited interfaces, and tuple or struct shaped ABI types, can be difficult or impossible to express cleanly with current Stylus interface generation approaches, leading to failed builds or error prone manual wiring. SIPB is critical because it makes this interoperability repeatable and safer in real repositories. It ships a drop in stylus interfaces crate covering ERC20, ERC721, ERC1155, and IERC165, plus a stylus bindgen CLI and a CI preflight that generate selector exact, overload safe Rust bindings from ABI JSON and fail builds when required bindings are missing or out of date.
What innovation or value will your project bring to Arbitrum? What previously unaddressed problems is it solving? Is the project introducing genuinely new mechanisms.
Innovation and value SIPB brings to Arbitrum
SIPB makes a common Stylus workflow more reliable: calling existing Solidity contracts from Stylus when the ABI includes overloaded functions, inherited interfaces, or tuple shaped types.
SIPB reduces repeated manual work around selectors and interface wiring by providing a reusable interface pack for the most common standards and a generator for the rest.
SIPB adds a CI gate that prevents known interop blockers from reaching main or release branches, which improves release confidence for teams building with Stylus.
Previously unaddressed problems it solves
Documented limitation: the default interface macro states that inheritance is not supported and has a restricted interface surface.
Compile blocking breakage: open issues show real failures for
interface inheritance usage (example issue #322: https://github.com/OffchainLabs/stylus-sdk-rs/issues/322 )
ERC721 overload name collisions (example issue #359: https://github.com/OffchainLabs/stylus-sdk-rs/issues/359)
Type handling gap: there is explicit demand for better support of tuple or struct shaped ABI types in interface generation workflows (example issue discussing struct handling: https://github.com/OffchainLabs/stylus-sdk-rs/issues/74 ).
Selector and interface safety concerns: audits highlight risks around selector and interface ID correctness in Stylus related tooling, which supports the need for stronger, repeatable guardrails.
New mechanisms introduced by SIPB
Interface Packs
a published stylus interfaces crate with pre generated bindings for ERC20, ERC721, ERC1155, and IERC165 that avoids known overload collision patterns by using selector exact wrappers.
Deterministic bindgen scheme
ABI JSON to Rust bindings with stable naming for overloads and deterministic ordering so output is reviewable and diff friendly across commits.
inheritance flattening at the ABI set level so teams can work with inherited interface shapes without relying on unsupported macro inheritance.
Fail closed CI preflight
a CI check that flags known interop blocker patterns and fails builds when required bindings are missing or out of date, with SARIF output for PR annotations and an optional baseline mode for gradual adoption.
What is the current stage of your project.
Ideation
Do you have a target audience? If so, which one.
Yes.
Primary audience Stylus contract developers who need to call existing Solidity contracts on Arbitrum, especially ERC20, ERC721, ERC1155, and common DeFi ABIs that include overloads, inherited interfaces, or tuple shaped types.
Secondary audience Teams porting Solidity contracts to Stylus who still depend on Solidity interfaces for integration with existing protocols.
Tertiary audience Maintainers of Stylus examples, templates, and libraries who want a repeatable, CI enforced interop workflow that others can copy without hitting compile blockers.
