# Azure Devops PR Comment - Powershell Task
Powershell scripts to comment an active PR with the terraform plan summary
## Usage (yaml)

```steps:
  - task: PowerShell@2
    displayName: 'Comment PR with Terraform Plan'
    condition: and(succeeded(), eq(variables['Build.Reason'], 'PullRequest'))
    inputs:
      filePath: '$(System.DefaultWorkingDirectory)/scripts/terraformAnnotate.ps1'
      arguments: '-JsonPlanPath $(System.DefaultWorkingDirectory)/plan/out.json'
      workingDirectory: $(System.DefaultWorkingDirectory)
    env:
      SYSTEM_ACCESSTOKEN: $(System.AccessToken)
```
Make sure you run `terraform show` with json output
```
terraform plan -out='./plan/out.txt'
terraform show -no-color -json ./plan/out.txt > ./plan/out.json
```
