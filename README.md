# Git Configuration Experiment

A simple experiment out of curiosity to see what happens when you commit with different git user configurations and then push to GitHub.

## Table of Contents

- [Project Structure](#project-structure)
- [Experiment Flow](#experiment-flow)
- [Setup](#setup)
- [Experiment Documentation](#experiment-documentation)
  - [Phase 2: Original Credentials](#phase-2-original-credentials)
  - [Phase 3: Different Credentials](#phase-3-different-credentials)
  - [Phase 4: Git and GitHub Results](#phase-4-git-and-github-results)
    - [git log results](#git-log-results)
    - [GitHub Commits History](#github-commits-history)
    - [GitHub Contributors](#github-contributors)
    - [Non-existent Git User Configuration](#non-existent-git-user-configuration)
    - [Non-existent GitHub User Commit](#non-existent-github-user-commit)
- [Conclusion](#conclusion)
  - [Key Learnings](#key-learnings)
  - [Findings](#findings)
  - [Possible Consequences](#possible-consequences)
  - [Is This a Bug or Intentional Feature?](#is-this-a-bug-or-intentional-feature)
  - [How to Use This Responsibly](#how-to-use-this-responsibly)
  - [Final Notes](#final-notes)

## Project Structure

```
/
├── README.md
└── images/
    ├── 01-initial-setup/             # Screenshots before any commits
    ├── 02-original-credentials/      # After commits with my original git config
    ├── 03-different-credentials/     # After commits with different git config
    └── 04-git-and-github-results/    # Screenshots of GitHub showing contributors and commits
```

## Experiment Flow

1. Add initial screenshots (before any commits)
2. Set git configuration to my original credentials and make some commits
3. Change git configuration to someone else's credentials and make more commits
4. Change git configuration back to my original credentials and make final commits
5. Push all commits to GitHub
6. Screenshot the GitHub repository to see how contributors and commits are attributed


## Setup

Before making commits, configure git with your credentials:

```bash
git config --global user.email "your@example.com"
git config --global user.name "Your Name"
```

If you get an error about empty ident, run the commands above to set your identity:

![Author identity unknown error](images/01-initial-setup/identity-error.jpg)

## Experiment Documentation

### Phase 2: Original Credentials

Configuration set to my actual credentials:

![Original git configuration](images/02-original-credentials/git-config--original.jpg)

### Phase 3: Different Credentials

Configuration set to someone else' credentials:

> [!NOTE]
> I have taken her consent for this experimentation, and this work is just for educational cause.

![Colleague's git configuration](images/03-different-credentials/git-config--faked.jpg)

### Phase 4: Git and GitHub Results

#### git log results

![Git Log results](images/04-git-and-github-results/git-log.jpg)

#### GitHub Commits History

![GitHub Commits History](images/04-git-and-github-results/github-commits-history.jpg)

#### GitHub Contributors

![GitHub Contributors](images/04-git-and-github-results/github-contributors.jpg)

#### Non-existent Git User Configuration

![Non-existent GitHub Contributor](images/04-git-and-github-results/nonexistent-git-user-config.jpg)

#### Non-existent GitHub User Commit

![Non-existent GitHub User Commit](images/04-git-and-github-results/nonexistent-github-user-commit.jpg)

## Conclusion

### Key Learnings

> [!IMPORTANT]
> This experiment reveals critical differences between local Git configuration and GitHub's user attribution system. Git commits are attributed based on the email and name in the local configuration, but GitHub's display and functionality depend on whether those credentials match actual GitHub accounts.

#### Findings

1. **Existent GitHub User (Real Account)**
   - When commits are made with credentials matching a real GitHub account, that user appears as a contributor
   - The GitHub profile is clickable and navigable
   - Contribution history and statistics are properly attributed
   - The user appears in the contributors list on the repository

2. **Non-Existent User (Fake Credentials)**
   - Commits are still recorded in `git log` with the configured name and email
   - The commits are pushed to GitHub successfully
   - However, since the user doesn't exist on GitHub, they don't appear in the contributors list
   - The author name appears on commits but is **not clickable or navigable**
   - No profile information or contribution statistics are available for the non-existent user

> [!NOTE]
> This demonstrates that GitHub relies on matching email addresses to registered GitHub accounts to create the connection between commits and user profiles.

### Possible Consequences

> [!WARNING]
> **Security & Attribution Risks**
> - **Identity Spoofing**: Anyone can attribute commits to a real GitHub user by using their email in local git configuration
> - **False Attribution**: Commits can be made to appear as if they were done by someone else (with their consent in this case, but malicious intent is possible)
> - **Reputation Impact**: A user's contribution history could be polluted with commits they didn't actually make
> - **Compliance Issues**: In professional settings, this could violate code review policies and accountability standards

### Is This a Bug or Intentional Feature?

> [!IMPORTANT]
> **This is an Intentional Feature, Not a Bug**
> 
> GitHub's system works as designed: it matches the commit author email to registered GitHub accounts. This is intentional because:
> - It allows flexibility in local development environments
> - Users can commit from different machines/configurations
> - It respects the principle that email is the primary identifier
> 
> However, GitHub has security measures in place.

### How to Use This Responsibly

> [!TIP]
> **Best Practices for Git Configuration**
> 
> 1. **Always use your own credentials** in your local git configuration
>    ```bash
>    git config --global user.email "your.email@github.com"
>    git config --global user.name "Your Name"
>    ```
> 
> 2. **Verify your configuration** before making commits:
>    ```bash
>    git config --global user.email
>    git config --global user.name
>    ```
> 
> 3. **For collaborative work**, use GPG signing to cryptographically verify commits:
>    ```bash
>    git config --global commit.gpgSign true
>    ```
> 
> 4. **Communicate** with team members about who is responsible for which commits

> [!NOTE]
> **GitHub's Response to Impersonation**
> 
> While technically possible, GitHub addresses this through:
> - Public commit history visibility (anyone can audit commits)
> - GPG signature verification (proves cryptographic ownership)
> - Email verification (prevents unauthorized commits with someone else's email)
> - Repository access logs and GitHub's audit system
> 
> For sensitive repositories, enable additional security measures like branch protection rules and required status checks.

### Final Notes

This experiment demonstrates the importance of understanding the distinction between local Git configuration and GitHub's identity verification system. While the technical capability to misattribute commits exists, it should only be used for educational purposes (with proper consent) and serves as a reminder to implement proper security measures in professional and sensitive repositories.

The key takeaway: **Git trusts the local configuration, but GitHub trusts the email-to-account mapping** — and this is by design.
