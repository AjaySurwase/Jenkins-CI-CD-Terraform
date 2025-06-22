Developer -> Push to feature branch -> PR created ->
↳ Triggers Job 1 (terraform-plan) -> Generates tfplan.txt -> Plan reviewed

Manager -> Approves PR -> Merges to main ->
↳ Triggers Job 2 (terraform-apply) -> terraform apply

your-repo/
├── Jenkinsfiles/
│   ├── plan.Jenkinsfile
│   └── apply.Jenkinsfile
├── main.tf
├── variables.tf
└── ...

In Jenkins (when creating the job):
Use a Pipeline Job (not Multibranch)

Under "Pipeline Script from SCM":

SCM: Git

Script Path:

For Job 1: Jenkinsfiles/plan.Jenkinsfile

For Job 2: Jenkinsfiles/apply.Jenkinsfile