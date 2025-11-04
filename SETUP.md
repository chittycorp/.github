# ChittyCorp Organization Setup Instructions

## Overview

This directory contains all the files needed to set up the `chittycorp/.github` repository, which provides default community health files and organization profile for all ChittyCorp repositories.

## Files Created

```
/tmp/chittycorp-github/
├── profile/
│   └── README.md                          # Organization profile (https://github.com/chittycorp)
├── workflow-templates/
│   ├── nodejs-ci.yml                      # Reusable Node.js CI workflow
│   └── nodejs-ci.properties.json          # Workflow metadata
├── CODE_OF_CONDUCT.md                     # Default CoC for all repos
├── SECURITY.md                            # Default security policy
├── SUPPORT.md                             # Default support guide
├── FUNDING.yml                            # Sponsor button config
├── README.md                              # This .github repo's README
└── SETUP.md                               # These instructions
```

## Setup Steps

### 1. Create the `.github` Repository

On GitHub.com:

1. Go to https://github.com/organizations/chittycorp/repositories/new
2. Repository name: `.github` (exactly this, with the dot)
3. Description: "Default community health files and organization profile"
4. Visibility: **Public** (required for profile to show)
5. Initialize: **Do NOT** check "Add a README" (we have our own)
6. Click "Create repository"

### 2. Clone and Populate

```bash
# Clone the new empty repository
git clone git@github.com:chittycorp/.github.git
cd .github

# Copy all files from /tmp/chittycorp-github/
cp -r /tmp/chittycorp-github/* .

# Verify structure
tree -L 2
# Should show: profile/, workflow-templates/, *.md, *.yml

# Stage everything
git add .

# Commit
git commit -m "feat: initialize ChittyCorp organization profile and defaults

- Add organization profile with mission, vision, and product pillars
- Add CODE_OF_CONDUCT.md reflecting ChittyFoundation principles
- Add SECURITY.md with tri-minting process and vulnerability reporting
- Add SUPPORT.md with FAQ and resource links
- Add FUNDING.yml for sponsor button
- Add Node.js CI workflow template
- Update all links to chittycorp.com

These files automatically apply to all ChittyCorp repositories.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>"

# Push
git push origin main
```

### 3. Verify Organization Profile

1. Visit https://github.com/chittycorp
2. You should see the profile README with:
   - ChittyCorp mission and vision
   - Product pillars table
   - Featured repositories
   - Contact information

### 4. Verify Default Files

Test on any repository that doesn't have its own community health files:

1. Visit any `chittycorp/{repo}` that lacks a CODE_OF_CONDUCT.md
2. GitHub should show "Code of conduct inherited from chittycorp/.github"
3. Click it to verify it shows our custom CoC

### 5. Enable Workflow Templates

1. Go to any `chittycorp/{repo}`
2. Navigate to "Actions" tab
3. Click "New workflow"
4. You should see "Node.js CI Workflow" in the "By ChittyCorp" section

## File Purpose

### `profile/README.md`
- Displays at https://github.com/chittycorp
- First impression for all visitors
- Highlights products, mission, and getting started

### `CODE_OF_CONDUCT.md`
- Default CoC for repos without their own
- Reflects ChittyFoundation Charter principles
- Customized beyond standard Contributor Covenant

### `SECURITY.md`
- Vulnerability reporting procedures
- Response timelines by severity
- Known security considerations
- Bug bounty program info (launching Q4 2025)

### `SUPPORT.md`
- How to get help (GitHub Discussions, email)
- Common questions and answers
- Tri-minting process explained
- Self-service troubleshooting

### `FUNDING.yml`
- Configures "Sponsor" button on all repos
- Links to https://chittycorp.com/support
- Email for commercial licensing

### `workflow-templates/nodejs-ci.yml`
- Reusable CI workflow for TypeScript projects
- Cross-platform testing (Ubuntu, macOS, Windows)
- Node 18 + 20 matrix
- Lint → Build → Test

## Customization by Repository

Individual repos can override any default by creating their own version:

**Example:** `chittycorp/chittycan` already has its own:
- `CODE_OF_CONDUCT.md` ✅ (uses its own)
- `SECURITY.md` ✅ (uses its own)
- `CONTRIBUTING.md` ✅ (uses its own)

**Example:** `chittycorp/newproject` has none:
- `CODE_OF_CONDUCT.md` → inherits from `.github`
- `SECURITY.md` → inherits from `.github`
- `SUPPORT.md` → inherits from `.github`

## Updating Organization Defaults

When you want to change a policy across all repos:

1. Edit the file in `chittycorp/.github`
2. Commit and push
3. Change immediately affects all repos without their own version

**Important:** Repos with their own versions are NOT affected. You'd need to update those individually.

## Next Steps

### Immediate
- [ ] Create the `.github` repository
- [ ] Push all files
- [ ] Verify organization profile shows correctly
- [ ] Test that defaults inherit properly

### Soon
- [ ] Set up GitHub Sponsors (update FUNDING.yml)
- [ ] Create remaining product repositories (chittyid, chittyconnect, etc.)
- [ ] Add workflow templates for Python, Cloudflare Workers
- [ ] Update chittycan to use org defaults where appropriate

### Future
- [ ] Add CONTRIBUTING.md to org defaults
- [ ] Create issue/PR templates for org defaults
- [ ] Add automated compliance checks
- [ ] Set up organization-level GitHub Actions secrets

## Troubleshooting

**Profile not showing:**
- Ensure `.github` repository is **public**
- Verify `profile/README.md` path is exact
- Wait 5-10 minutes for GitHub cache to refresh

**Defaults not inheriting:**
- Check file names are exact (case-sensitive)
- Ensure files are in root, not subdirectory
- Verify repository doesn't have its own version

**Workflow templates not appearing:**
- Ensure `.properties.json` files exist
- Check JSON syntax is valid
- Restart "New workflow" page

## Documentation

- [GitHub Docs: Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [GitHub Docs: Customizing your organization's profile](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile)
- [GitHub Docs: Creating workflow templates](https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization)

---

**Questions?** Email dev@chitty.cc or open a discussion at https://github.com/orgs/chittycorp/discussions

**Last Updated:** 2025-01-04
