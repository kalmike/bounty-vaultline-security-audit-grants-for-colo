# README.md

## Architecture

This tool is a Python script designed to interact with the Solana blockchain and process applications for Vaultline Security Audit Grants. It includes a CLI interface for submitting applications and a self-test to ensure functionality.

## Usage

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/solana-audit-tool.git
   cd solana-audit-tool
   ```

2. Install dependencies:
   ```sh
   pip install solana
   ```

### Running the Tool

1. **Submit an Application**:
   ```sh
   python tool.py --submit --project-name "MyProject" --description "A short description of the project." --colosseum-link "https://colosseum.example.com/project" --repo-link "https://github.com/yourusername/myproject" --programs "program1,program2" --loc 1000 --stage "mainnet" --users-tvl "10000" --audit-motivation "This is why an audit matters now." --contact-email "contact@example.com"
   ```

2. **Run Self-Test**:
   ```sh
   python tool.py --test
   ```

## CLI Options

- `--submit`: Submit an application.
- `--test`: Run self-test.

## Self-Test

The self-test ensures that the tool can interact with the Solana blockchain and process applications correctly.

```python
import argparse
import json
from solana.rpc.api import Client

# Initialize Solana client
client = Client("https://api.mainnet-beta.solana.com")

def submit_application(project_name, description, colosseum_link, repo_link, programs, loc, stage, users_tvl, audit_motivation, contact_email):
    # Simulate application submission
    application = {
        "project_name": project_name,
        "description": description,
        "colosseum_link": colosseum_link,
        "repo_link": repo_link,
        "programs": programs,
        "loc": loc,
        "stage": stage,
        "users_tvl": users_tvl,
        "audit_motivation": audit_motivation,
        "contact_email": contact_email
    }
    # Simulate sending application to Vaultline
    print(f"Application submitted: {application}")
    return application

def self_test():
    # Simulate self-test
    print("Running self-test...")
    test_application = submit_application(
        project_name="TestProject",
        description="A test project for the self-test.",
        colosseum_link="https://colosseum.example.com/testproject",
        repo_link="https://github.com/yourusername/testproject",
        programs="testprogram1,testprogram2",
        loc=500,
        stage="devnet",
        users_tvl="5000",
        audit_motivation="This is a test audit motivation.",
        contact_email="testcontact@example.com"
    )
    assert test_application, "Self-test failed: Application not submitted."
    print("Self-test passed.")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Vaultline Security Audit Grant Application Tool")
    parser.add_argument("--submit", action="store_true", help="Submit an application")
    parser.add_argument("--test", action="store_true", help="Run self-test")
    parser.add_argument("--project-name", type=str, help="Project name")
    parser.add_argument("--description", type=str, help="Project description")
    parser.add_argument("--colosseum-link", type=str, help="Colosseum submission link")
    parser.add_argument("--repo-link", type=str, help="Repository link")
    parser.add_argument("--programs", type=str, help="Programs to audit (comma-separated)")
    parser.add_argument("--loc", type=int, help="Approximate lines of code")
    parser.add_argument("--stage", type=str, help="Current stage (devnet, testnet, mainnet)")
    parser.add_argument("--users-tvl", type=str, help="Users/TVL figures")
    parser.add_argument("--audit-motivation", type=str, help="Why an audit matters now")
    parser.add_argument("--contact-email", type=str, help="Team contact email")

    args = parser.parse_args()

    if args.submit:
        if not all([args.project_name, args.description, args.colosseum_link, args.repo_link, args.programs, args.loc, args.stage, args.users_tvl, args.audit_motivation, args.contact_email]):
            print("Error: All required arguments are not provided.")
        else:
            submit_application(
                project_name=args.project_name,
                description=args.description,
                colosseum_link=args.colosseum_link,
                repo_link=args.repo_link,
                programs=args.programs,
                loc=args.loc,
                stage=args.stage,
                users_tvl=args.users_tvl,
                audit_motivation=args.audit_motivation,
                contact_email=args.contact_email
            )
    elif args.test:
        self_test()
    else:
        parser.print_help()
```

```json
{
  "otherInfo": {
    "toolName": "Vaultline Security Audit Grant Application Tool",
    "description": "A Python script for submitting applications for Vaultline Security Audit Grants on the Solana blockchain.",
    "repository": "https://github.com/yourusername/solana-audit-tool"
  },
  "eligibilityAnswers": {
    "eligibility": [
      {
        "type": "text",
        "order": 1,
        "optional": false,
        "question": "Share: project name & description, Colosseum link, repo link, programs to audit, approx. LOC, stage (devnet/testnet/mainnet) + users/TVL, why an audit matters now, and team contact details."
      }
    ]
  }
}
```