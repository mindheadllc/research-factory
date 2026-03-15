# Contributing to Research Factory

This framework was built through iterative design — testing ideas about how to make AI-assisted research rigorous, finding failure modes, and patching them. It will continue to improve the same way, and your experience using it is the most valuable input.

## How to Contribute

### Share Your Experience

The most useful contribution is a report of how the framework performed on a real project:

- **What worked well?** Which components added the most value? Which checklists caught real problems?
- **What didn't work?** Where did the process create friction without adding quality? What did you skip, and did skipping it matter?
- **What's missing?** What failure mode did you hit that the framework didn't anticipate?
- **What did you modify?** If you adapted the framework for your specific use case, what did you change and why?

Open an issue with the label `experience-report` and share as much or as little as you're comfortable with.

### Suggest Improvements

If you have a specific improvement in mind:

1. **Open an issue first** describing the problem and proposed solution. This lets us discuss before you invest time in a PR.
2. **For process changes** (new checklist items, modified phase gates, new prompts): explain the failure mode the change addresses and how you discovered it.
3. **For structural changes** (new agent roles, modified file tree, changed handoff protocols): explain what's broken about the current design and why the change fixes it without introducing new problems.

### Submit a Pull Request

- Keep changes focused. One concern per PR.
- If modifying a checklist or prompt, explain the reasoning in the PR description.
- If adding a new template or agent, include the cold-start protocol and explain how it integrates with the existing process.

## What We're Especially Interested In

- **Domain-specific failure modes documents.** If you've generated one for your research intersection and it revealed useful pitfalls, consider contributing it to `examples/` so others in similar domains can benefit.
- **Prompt refinements.** If you found that modifying a prompt from the library produced better results, share the refinement and what improved.
- **Anti-patterns.** If you discovered a way of using the framework that looks right but produces bad outcomes, document it.
- **Adaptations for specific contexts.** Using this for a different kind of computational research? Working in a team rather than solo? Adapted it for a teaching context? We'd like to hear about it.

## Code of Conduct

Be constructive. This is a research tool, not a battleground. Critique the framework, not the people using it. Share failures honestly — they're more useful than successes.

## License

By contributing, you agree that your contributions will be licensed under CC BY-SA 4.0, consistent with the project's license.
