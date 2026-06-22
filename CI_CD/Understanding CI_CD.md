CI/CD - Continuous Integration Continuous Development

- CI --> the practice of automatically integrating code changes from multiple contributors into a shared repository several times a day
- CD --> Automatically releasing every change that passes all stages of the production pipeline
![[Screenshot 2026-06-08 at 12.38.37.png]]

This is so important because: 
- Ensures faster delivery 
- improved quality, catches bugs early and testing early
- Reducing risk of big failures 
- better collaboration

Popular CI/CD tools: 
- GitLab CI/CD
- GitHub Actions
- AWS/Azure/GCP native 
- Jenkins
- CircleCI
- TravisCI


So how does CI/CD fit into DevOps architecture: 
![[Screenshot 2026-06-08 at 12.44.13.png]]



what is actually the purpose of making CI/CD?
lets say you want to generate a new image or have image changes you want to implement but you are hosting your image in ECR. Then you would have to build the image, manually push the image to ECR, tag it appropriately and the update your terraform to pull this as well. 

 CI/CD automates this - Following you pushing the new image, a new Terraform plan will run so automatically your infrastructure is updated. So you dont have to update your task definitions, ecs clusters etc manually. 