# Azure Devops PR Comment - Powershell Task
Powershell scripts to comment an active PR with the terraform plan summary
## Usage (yaml)

```steps:
  - task: PowerShell@2
    displayName: 'Comment PR with Terraform Plan'
    condition: and(succeeded(), eq(variables['Build.Reason'], 'PullRequest'))
    inputs:
      filePath: '$(System.DefaultWorkingDirectory)/scripts/TerraformAnnotate.ps1'
      arguments: '-JsonPlanPath $(System.DefaultWorkingDirectory)/plan/out.json'
      workingDirectory: $(System.DefaultWorkingDirectory)
    env:
      SYSTEM_ACCESSTOKEN: $(System.AccessToken)
```
