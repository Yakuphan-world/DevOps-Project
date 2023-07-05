## Helm Part of k8s Project

- Install Helm
```bash
cd /home/ubuntu/project206
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm version
```

- Create your Helm Chart
```bash
helm create pb-helmchart
rm -rf pb-helmchart/templates/*
cp k8s/* pb-helmchart/templates/
```

- Go your GitHub and create a repo form helm charts (i will name it as `helmrepo-pb`)

- Return to your VsCode
```bash
cd /home/ubuntu/project206
git clone https://github.com/devopswizard/helmrepo-pb.git
cd helmrepo-pb/
helm package ../pb-helmchart/
helm repo index .
git config --global user.email "joshuatallman78@gmail.com" # enter your own credentials
git config --global user.name "Joshua Tallman" # enter your own credentials
git add .
git commit -m "chart is added"
git push  # enter your GitHub credentials (provide TOKEN as password)
```

- Go to your GitHub Repo and get your raw address of your repo by clicking index.yaml >> raw button
mine is --> https://raw.githubusercontent.com/devopswizard/helmrepo-pb/main/

- Edit Helm Repo commad as below (change it according to your details and use raw repo url + TOKEN):
```bash
helm repo add --username devopswizard --password *****TOKEN HERE***** phonebook-helm-repo 'https://raw.githubusercontent.com/devopswizard/helmrepo-pb/main/'
helm repo ls   # now you repositories in the list
helm search repo phonebook-helm-repo   # now you see your chart in the list
```

- Deploy your Application directly from your Helm Repo (pushed to GitHub)
```bash
helm install pb-release phonebook-helm-repo/pb-helmchart
helm ls
```

- Delete your release
```bash
helm delete pb-release
```