# tmp-github-actions-2

Mindmapping

    CI
      with:
        watch: [src, tests, pgk, requirements.txt]
      if-changed app or dockerfile
        ci-gradle|python|rust...
        lint docker

      if-changed helm
        lint helm

      if-changed terraform
        lint terraform
        terraform plan + comment

    CD
      if-changed app or dockerfile
        build docker
        push docker image

      matrix: [dev,prd]
        WF if-changed terraform
          terraform apply

        WF 
          - if-changed app or dockerfile
            entur/helm-deploy $image
              with:
                image=${pr.number}-pr
          - if-changed helm
            entur/helm-deploy $image
              with:
                image=kc get image


