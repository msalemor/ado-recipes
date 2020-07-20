# Tips and Tricks

## Copy and Publish Artifact

Typically a when a job runs, the output (.EXE, DLLs, etc.) is stored to an agent's folder ($(System.DefaultWorkingDirectory)). You then need to copy these output files to the artifacts staging folder ($(Build.ArtifactStagingDirectory)) and from there the artifacts need to be published. The artifact name (drop) can be changed. For example:

```yaml
steps:
- script: ./buildSomething.sh 
- task: CopyFiles@2
  inputs:
    contents: '_buildOutput/**' #$(System.DefaultWorkingDirectory)/_buildOutput/**
    targetFolder: $(Build.ArtifactStagingDirectory)
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: $(Build.ArtifactStagingDirectory)
    artifactName: drop
```
- You can repeat the task and copy other folders:
```yaml
- task: CopyFiles@2
  inputs:
    contents: 'project1/bin/**' 
    targetFolder: $(Build.ArtifactStagingDirectory)/project1
- task: CopyFiles@2
  inputs:
    contents: 'project2/bin/**'
    targetFolder: $(Build.ArtifactStagingDirectory)/project2
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: $(Build.ArtifactStagingDirectory)
    artifactName: SolutionAritifacts # will have project1 and project 2 folders
```

## Variables

- In most pipelines use ```$(variable)``` instead of ```$variable```

## Powershell, Bash, Shell, CLI

- If you cannot find a suitable task, remember that you can run shell scripts appropriate for the OS you have selected.
- Inline:
```bash
steps:
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: echo $MYSECRET
  env:
    MYSECRET: $(Foo)
```
- From a file:
```bash
- task: ShellScript@2
  inputs:
    scriptPath:
    #args: '' # Optional
    #disableAutoCwd: false # Optional
    #cwd: '' # Optional
    #failOnStandardError: false
```
- From Powershell:
```powershell
# for PowerShell Core
steps:
- pwsh: ./my-script.ps1

# for Windows PowerShell
steps:
- powershell: .\my-script.ps1
```

## C# Solution vs Project

- Many example show how to deploy one project, but what if it is a solution that has many projects?