# GitHub Actions – Interview Questions and Answers

## 🟢 Beginner-Level

1. **What is GitHub Actions?**
   GitHub Actions is a CI/CD platform built into GitHub that allows you to automate tasks like testing, building, and deploying code using workflows defined in YAML files.

2. **Where are GitHub workflows defined?**
   In `.github/workflows/` directory of a GitHub repository using `.yml` or `.yaml` files.

3. **What are the key components of a GitHub Actions workflow?**
   `name`, `on` (triggers), `jobs`, `steps`, and `runs`.

4. **What events can trigger a workflow?**
   Common events include `push`, `pull_request`, `workflow_dispatch`, `schedule`, `issue_comment`, etc.

5. **What is the difference between `run` and `uses` in a step?**

   * `run` executes a shell command.
   * `uses` executes a defined GitHub Action (from a repo or Docker container).

6. **How do you pass secrets in GitHub Actions?**
   Secrets are stored in repository settings under **Settings → Secrets and variables** and accessed via `${{ secrets.SECRET_NAME }}`.

7. **What is a job matrix in GitHub Actions?**
   A matrix allows you to run a job with different input combinations (e.g., Node.js versions) in parallel.

---

## 🟡 Intermediate-Level

8. **How do you cache dependencies in GitHub Actions?**
   Use the `actions/cache` action with a `key` and `path` to avoid downloading dependencies repeatedly.

9. **What is a composite action?**
   A reusable group of steps written in YAML. It helps reduce duplication and organize workflows.

10. **How do you use workflow inputs with `workflow_dispatch`?**
    Define inputs in `on.workflow_dispatch` and use them with `${{ inputs.input_name }}` in steps.

11. **What’s the difference between `jobs.<job>.needs` and `jobs.<job>.dependencies`?**
    Only `needs` exists. It declares explicit dependencies between jobs and ensures correct execution order.

12. **How do you debug a failing GitHub Action?**
    Enable `ACTIONS_RUNNER_DEBUG=true` and `ACTIONS_STEP_DEBUG=true` as secrets or environment variables for verbose logs.

13. **Can GitHub Actions deploy to servers or cloud providers?**
    Yes, via CLI tools, API calls, or GitHub Marketplace actions for platforms like AWS, Azure, or GCP.

14. **What are reusable workflows?**
    Workflows designed to be called by other workflows using the `workflow_call` trigger.

---

## 🔴 Advanced-Level

15. **How do you write a custom GitHub Action in JavaScript?**

* Create an `action.yml`.
* Use `@actions/core`, `@actions/github`, etc., to access inputs and GitHub context.
* Push the code to a GitHub repo (public or internal).
  Example:

```yaml
name: 'My JS Action'
runs:
  using: 'node16'
  main: 'index.js'
```
# GitHub Actions Interview Q&A

## ❓ What’s the difference between container actions and JavaScript actions?

- **JavaScript Actions**: Run natively on the GitHub runner using Node.js.
- **Container Actions**: Run inside a Docker container. Support multiple languages and system dependencies.

---

## 🔄 How do you share data between jobs in GitHub Actions?

Use the `actions/upload-artifact` and `actions/download-artifact` actions to share files/artifacts between jobs.

---

## 🔗 How would you trigger one GitHub Action from another?

Use:
- `workflow_call` trigger for reusable workflows
- `repository_dispatch` for manual or API-triggered events
- `workflow_run` to trigger on completion of another workflow

---

## 🔐 How do you manage secrets across environments (dev/stage/prod)?

Define environments in GitHub and assign secrets to each one.  
Then use `environment:` in the workflow jobs to access appropriate secrets.

---

## 🚀 How would you build a CI/CD pipeline using GitHub Actions for a microservices repo?

- Create workflows per service
- Use `paths` to trigger builds only for modified services
- Use reusable workflows and matrix builds
- Implement caching, testing, and deploy jobs
- Use environment-based secrets for staging/production

---

## 🧩 Bonus: Types of Custom Actions in GitHub Actions

GitHub supports **three types** of custom actions:

### 1. JavaScript (Node.js) Actions
- **Description**: Implemented in Node.js, run directly in the GitHub-hosted runner.
- **Use Case**: Best for performance and built-in tool access.
- **Tools**: `@actions/core`, `@actions/github`, etc.
- **Example**: Lint checkers, changelog generators.

### 2. Docker (Container) Actions
- **Description**: Runs inside a Docker container.
- **Use Case**: Supports any language and system dependencies.
- **Tools**: Dockerfile, any language or binary.
- **Example**: Actions requiring ffmpeg, awscli, etc.

### 3. Composite Actions
- **Description**: Built by combining multiple shell-based steps, written in YAML.
- **Use Case**: Useful for grouping repetitive logic and making reusable workflows.
- **Limitations**: Cannot include Node.js or Docker directly.

---

## ✅ Summary Table

| Type              | Runs In        | Language/Tools       | Use Case                                              |
|-------------------|----------------|-----------------------|--------------------------------------------------------|
| JavaScript         | GitHub runner  | Node.js (@actions/*)  | Light, fast actions that need GitHub context access    |
| Docker             | Docker         | Docker, any language  | Complex dependencies or OS-level tooling               |
| Composite (YAML)   | GitHub runner  | YAML only             | Reusable workflows made of existing steps              |
