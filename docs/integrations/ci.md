
# Continuous Integration

Because of its **simple design** and **rich command line interface**, INGenious can integrate with ==any== CICD tool

INGenious is composed of all flat files like `xml` and `csv` in addition to the `java` files which makes version control system very easy.  

## What to push to the Repository

The working directory should contain the following `.gitignore` file :

```gitignore title=".gitignore"

LICENSE
logs/
Projects/*/Results/*/
web/
recent.items
log.txt
Tools/
lib/*.jar
```

After this, the corresponding **pipeline yaml** needs to be included in the repository. 

Please check out the pipeline integrations with the following solutions :



[GitHub Actions :simple-githubactions:](integrations/githubactions.md){ .md-button } [Azure DevOps :material-microsoft-azure-devops:](integrations/azuredevops.md){ .md-button }  [Circle CI :simple-circleci:](integrations/circleci.md){ .md-button } 




 -------------------------------------
